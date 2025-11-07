---
title: 發佈階層上適用於 AEM as a Cloud Service 的 Open ID Connect 支援
description: 了解如何在發佈階層為 AEM as a Cloud Service 設定 Open ID Connect (OIDC)
feature: Security
role: Admin
exl-id: d2f30406-546c-4a2f-ba88-8046dee3e09b
source-git-commit: 2e257634313d3097db770211fe635b348ffb36cf
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 100%

---

# 發佈階層上適用於 AEM as a Cloud Service 的 Open ID Connect 支援 {#open-id-connect-support-for-aem-as-a-cloud-service-on-publish-tier}

## 簡介 {#introduction}

隨著組織的數位體驗現代化，安全又能擴展的身分管理即成為基本需求。Adobe Experience Manager (AEM) Cloud Service 現在可在發佈階層支援 OpenID Connect (OIDC)，允許與業界領先的身分提供者 (IdP) (例如 Entra ID (Azure AD)、Google、Okta、Auth0、Ping Identity、ForgeRock 和支援 OIDC 的 IdP) 進行緊密整合和標準型整合。

OIDC 是 OAuth 2.0 通訊協定上的身分層，可以在為開發人員維持簡潔操作的同時實現強大的使用者驗證。其廣泛應用於企業對消費者 (B2C)、內部網路和合作夥伴入口網站等情境，這些情境都需要安全的使用者登入和身分識別同盟。

目前為止，AEM 客戶都負責在發佈階層實施自己的自訂登入邏輯，這既增加了開發時間，也帶來長期維護和安全性的挑戰。透過對 OIDC 的原生支援，AEM Cloud Service 為存取發佈環境的一般使用者提供安全、可擴充且 Adobe 支援的驗證機制，從而消除此負擔。

無論您提供的是個人化的消費者網站還是經過驗證的內部入口網站，發佈的 OIDC 都可以簡化身分識別同盟並透過集中身分治理降低風險。它還可以幫助組織在不犧牲靈敏度的情況下滿足現代的合規性和安全性標準。

## 設定 AEM 以進行 OIDC 驗證 {#configure-aem-oidc-authentication}

### 先決條件 {#prerequisits}

我們假設以下資訊可用或已定義：

1. AEM 存放庫中受保護內容的路徑
1. 待設定 IdP 的識別碼。這可以是任何字串

IdP 設定的資訊：

1. IdP 中設定的用戶端 ID
1. IdP 中設定的用戶端密碼若已在 Idp 上設定 PKCE，則用戶端密碼不可用。請勿在設定檔中儲存純文字值。使用 CM 密碼並將其用來參照
1. 在 Idp 上設定的範圍。至少必須提供 `openid` 範圍
1. 是否啟用了 IdP 上的 PKCE
1. `callbackUrl` 使用第 1 點定義的設定路徑之一新增字尾加以定義：`/j_security_check`
1. 存取標準 `.well-known` 檔案的 `baseUrl`。例如，如果知名 URL 是：`https://login.microsoftonline.com/53279d7a-438f-41cd-a6a0-fdb09efc8891/v2.0/.well-known/openid-configuration`，那麼 `baseUrl` 就是：`https://login.microsoftonline.com/53279d7a-438f-41cd-a6a0-fdb09efc8891`

### 設定檔概觀 {#overview-of-the-configuration-files}

以下是需要設定的檔案清單：

1. **OIDC 連線**：這將由 `OidcAuthenticationHandler` 用於對使用者進行驗證，或由其他元件用於 [授權以 OAuth 存取受 IdP 保護的資源](https://github.com/apache/sling-org-apache-sling-auth-oauth-client?lang=zh-Hant)
1. **OIDC 驗證處理常式**：這是用於對存取設定路徑的使用者進行驗證的驗證處理常式
1. **UserInfoProcessor**：此元件會處理 IdP 收到的資訊。客戶可以將其擴充以實施自訂邏輯
1. [**預設同步處理常式**](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html?lang=zh-Hant)：此元件在存放庫中建立使用者
1. [**外部登入模組**](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html?lang=zh-Hant)：此元件在本機 oak 存放庫中對使用者進行驗證。

下圖顯示上述設定元素如何相互連結。請注意，由於這些是 `ServiceFactory` 元件，因此 `~uniqueid` 可以是任何隨機的唯一字串：

![OIDC 設定圖表](/help/security/assets/oidc-diagram.png)

### 設定 OIDC 連線 {#configure-the-oidc-connection}

首先，我們需要設定 OIDC 連線。可以設定多個 OIDC 連線，且每個連線必須有不同名稱。

1. 建立新的 `.cfg.json` 檔案來儲存設定。例如，您可以使用 `org.apache.sling.auth.oauth_client.impl.OidcConnectionImpl~azure.cfg.json`：**azure** 字尾必須是連線的唯一識別碼
1. 遵循以下範例中的設定格式：

   ```
   {
    "name":"azure",
    "scopes":[
      "openid"
    ],
    "baseUrl":"<https://login.microsoftonline.com/53279d7a-438f-41cd-a6a0-fdb09efc8891/v2.0>",
    "clientId":"5199fc45-8000-473e-ac63-989f1a78759f",
    "clientSecret":"xxxxxx"
   }
   ```

1. 依以下方式設定其屬性：
   * **「名稱」** 可由使用者定義
   * `baseUrl`、`clientid` 和 `clientSecret` 是來自 IdP 的設定值。
   * 範圍必須至少包含值 `openid`。

### 設定 OIDC 驗證處理常式 {#configure-oidc-authentication-handler}

現在，設定 OIDC 驗證處理常式可設定多個 OIDC 連線。每個都必須有不同的名稱。如果這些連線共用相同的 [OAK 外部身分提供者](https://jackrabbit.apache.org/oak/docs/security/authentication/identitymanagement.html?lang=zh-Hant)，就可以共用使用者。

1. 建立設定檔。對於此範例，我們將使用 `org.apache.sling.auth.oauth_client.impl.OidcAuthenticationHandler~azure.cfg.json`。`azure` 字尾必須是唯一識別碼。請參閱以下的設定檔範例：

   ```
   {
     "path":"/content/tests/us/en/test-7",
     "callbackUri":"http://localhost:14503/content/tests/us/en/test-7/j_security_check",
     "pkceEnabled":false,
     "defaultConnectionName":"azure"
     "idp": "azure-idp"
   }
   ```

1. 接著，請依以下方式設定其屬性：
   * `path`：要保護的路徑
   * `callbackUri`：前往需要保護的路徑，新增字尾： `/j_security_check`
   * `defaultConnectionName`：使用先前步驟中為 OIDC 連線定義的相同名稱進行設定 +
   * `pkceEnabled`：授權代碼流程的 `true` Proof Key for Code Exchange (PKCE)
   * `idp`：[OAK 外部身分提供者](https://jackrabbit.apache.org/oak/docs/security/authentication/identitymanagement.html?lang=zh-Hant)的名稱。請注意，不同的 OAK IDP 無法共用使用者或群組

### 設定 SlingUserInfoProcessor

1. 建立設定檔。對於此範例，我們將使用 `org.apache.sling.auth.oauth_client.impl.SlingUserInfoProcessor~azure.cfg.json`。`azure` 字尾必須是唯一識別碼。請參閱以下的設定檔範例：

   ```
   {
      "groupsInIdToken":true,
      "groupsClaimName": "groups",
      "connection":"azure",
      "storeAccessToken": false,
      "storeRefreshToken": false
   }
   ```

1. 接著，請依以下方式設定其屬性：
   * `groupsInIdToken`：如果群組在 ID 權杖中傳送，則設為真。如果值為假或未指定，則從 UserInfo 端點讀取群組。
   * `groupsClaimName`：申請的名稱包含要在 AEM 中同步的群組。
   * `connection`：使用先前步驟中為 OIDC 連線定義的相同名稱進行設定
   * `storeAccessToken`：如果存取權杖必須儲存在存放庫，則為真。在預設情況下，則為假。只有當 AEM 需要代表儲存在受相同 IdP 保護的外部伺服器中的使用者存取資源時，才將其設為真。
   * `storeRefreshToken`：如果重新整理權杖必須儲存在存放庫，則為真。在預設情況下，則為假。只有當 AEM 需要代表儲存在受相同 IdP 保護的外部伺服器中的使用者存取資源並且需要從 IdP 重新整理權杖時，才將其設為真。
請注意，存取權杖和重新整理權杖以 AEM 主要金鑰加密儲存。


### 設定同步處理常式 {#configure-the-synchronization-handler}

必須設定至少一個同步處理常式來同步在 oak 中經過驗證的使用者。如需詳細資訊，請參閱[此](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html?lang=zh-Hant)頁面。

建立一個名為 `org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler~azure.cfg.json` 的檔案。**azure** 字尾必須是唯一識別碼。關於更多如何設定其屬性的資訊，請參閱 [Oak 使用者和群組同步文件](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html?lang=zh-Hant)。請參閱以下的範例設定：

```
{
  "user.expirationTime":"300s",
  "user.membershipExpTime":"300s",
  "user.propertyMapping":[
    "profile/familyName=profile/familyName",
    "profile/givenName=profile/givenName",
    "rep:fullname=cn",
    "profile/email=profile/email",
    "oauth-tokens"
  ],
  "user.pathPrefix":"azure",
  "handler.name":"azure"
}
```

下列為一些最相關的屬性，要在預設同步處理常式中設定。請注意，應始終在雲端服務中啟用動態群組會籍。

| 屬性名稱 | 備註 | 建議值 |
|---|---|---|
| `user.expirationTime` | 同步使用者過期前的持續時間。使用者只有在過期時間後才進行同步。 | 1h |
| `user.membershipExpTime` | 同步使用者會籍過期前的持續時間。使用者會籍只有在過期時間後才進行同步。 | 1h |
| `user.dynamicMembership` | 我們建議啟用動態群組會籍 | true |
| `user.enforceDynamicMembership` | 我們建議對動態群組會籍啟用強制執行 | true |
| `group.dynamicGroups` | 我們建議啟用動態群組 | true |
| user.propertyMapping | 提供的 `UserInfoProcessor` 實施僅同步少數屬性。它可以修改和自訂。 | <code>&quot;profile/givenName=profile/given_name&quot;、</code><br><code>“profile/familyName=profile/family_name”、</code><br><code>&quot;rep:fullname=profile/name&quot;、</code><br><code>&quot;profile/email=profile/email&quot;、</code><br><code>&quot;access_token=access_token&quot;、</code><br><code>&quot;refresh_token=refresh_token&quot;</code> |
| `user.membershipNestingDepth` | 傳回會籍關係同步時群組內嵌的深度上限。值為 0 可有效停用群組會籍查詢。值為 1 僅新增使用者的直接群組。僅在同步使用者會籍系譜時，此值同步單一群組無效。 | 1 |

### 設定外部登入模組 {#configure-the-external-login-module}

最後，您需要設定外部登入模組。

1. 建立一個名為 `org.apache.jackrabbit.oak.spi.security.authentication.external.impl.ExternalLoginModuleFactory~azure.cfg.json` 的檔案。請參閱以下範例設定：

   ```
   {
    "sync.handlerName":"azure",
    "idp.name":"azure-idp"
   }
   ```

1. 依以下方式設定其屬性：

   * `sync.handlerName`：先前定義的同步處理常式的名稱
   * `idp.name`：OIDC 驗證處理常式中定義的 OAK 身分提供者

### 選用：實施自訂 UserInfoProcessor {#implement-a-custom-userinfoprocessor}

使用者透過 ID 權杖驗證，其他的屬性則在為 IdP 定義的 `userInfo` 端點撷取。如果必須執行額外的非標準操作，則 [UserInfoProcessor](https://github.com/apache/sling-org-apache-sling-auth-oauth-client/blob/master/src/main/java/org/apache/sling/auth/oauth_client/impl/SlingUserInfoProcessorImpl.java?lang=zh-Hant) 的自訂實施是 Sling 的預設實施。

## 範例：使用 Azure Active Directory 設定 OIDC 驗證

### 在 Azure Active Directory 中設定新的應用程式 {#configure-a-new-application-in-azure-ad}

1. 請依照 [Azure Active Directory 文件](https://learn.microsoft.com/zh-tw/power-pages/security/authentication/openid-settings#create-an-app-registration-in-azure)在 Azure Active Directory 中建立新的應用程式。請參閱以下詳細介紹應用程式概觀的畫面：

   ![應用程式概觀](/help/security/assets/odic-application-overview.png)

1. 如果需要群組或應用程式角色，請遵循[文件](https://learn.microsoft.com/zh-tw/entra/external-id/customers/how-to-use-app-roles-customers)以在應用程式啟用並將其傳送進 ID 權杖中。以下是設定群組的範例：

![OIDC 宣告令牌 ID](/help/security/assets/oidc-claim-id-token.png)

1. 依照前文記錄的步驟建立必要的設定檔。以下是針對 Azure AD 的特定範例：
   * 我們將 OIDC 連線、驗證處理常式和預設同步處理常式的名稱定義為：`azure`
   * 網站網址為：`www.mywebsite.com`
   * 我們保護路徑 `/content/wknd/us/en/adventures`
   * 租用戶為：`tennat-id`，
   * 用戶端識別碼為：`client-id`，
   * 密碼為：`secret`，
   * 這些群組在 ID 權杖中用以下申請形式傳送：`groups`

#### org.apache.sling.auth.oauth_client.impl.OidcConnectionImpl~azure.cfg.json

```
{
  "name":"azure",
  "scopes":[
    openid", "User.Read", "profile", "email
  ],
  "baseUrl":"https://login.microsoftonline.com/tenant-id/v2.0",
  "clientId":"client-id",
  "clientSecret":"secret"
}
```

#### org.apache.sling.auth.oauth_client.impl.OidcAuthenticationHandler~azure.cfg.json

```
{
  "callbackUri":"https://www.mywebsite.com/content/wknd/us/en/adventures/j_security_check",
  "path":[
    "/content/wknd/us/en/adventures"
  ],
  "idp":"azure",
  "defaultConnectionName":"azure"
}
```

#### org.apache.jackrabbit.oak.spi.security.authentication.external.impl.ExternalLoginModuleFactory~azure.cfg.json

```
{
  "sync.handlerName":"azure",
  "idp.name":"azure"
}
```

#### org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler~azure.cfg.json

```
{
  "user.expirationTime":"1s",
  "user.membershipExpTime":"1s",
  "user.propertyMapping":[
    "profile/givenName=profile/given_name",
    "profile/familyName=profile/family_name",
    "rep:fullname=profile/name",
    "profile/email=profile/email",
    "access_token=access_token",
    "refresh_token=refresh_token"
  ],
  "user.pathPrefix":"azure",
  "group.pathPrefix": "oidc",
  "user.membershipNestingDepth": "1",
  "handler.name":"azure"
}
```

#### org.apache.sling.auth.oauth_client.impl.SlingUserInfoProcessorImpl~azure.cfg.json

```
{
  "groupsInIdToken": "true",
  "storeAccessToken": "false",
  "storeRefreshToken": "false",
  "connection": "azure",
  "groupsClaimName": "groups"
}
```

### 關於 Azure AD 群組的其他資訊 {#additional-information-about-azure-ad-groups}

要在 Microsoft Azure 入口網站中為企業應用程式設定群組，您需要在&#x200B;**企業應用程式**&#x200B;搜尋該應用程式並新增群組：<!-- Alexandru: this bit cound be clearer-->

![OIDC 群組新增 ](/help/security/assets/oidc-ad-additional-info.png)

若要在 ID 權杖中啟用群組申請，請在 Microsoft Azure 入口網站的&#x200B;**權杖設定**&#x200B;欄位新增申請：<!-- Alexandru: this bit cound be clearer as well-->

![OIDC 申請權杖 ID](/help/security/assets/oidc-claim-id-token.png)

`SlingUserInfoProcessor` 的設定必須依照下列範例進行修改。

需要修改的檔案名稱為 `org.apache.sling.auth.oauth_client.impl.SlingUserInfoProcessorImpl.cfg.json`。內容應設定如下：

```
{
  "connection": "azure",
  "groupsInIdToken": "true",
  "storeAccessToken": "false",
  "storeRefreshToken": "false"
}
```
