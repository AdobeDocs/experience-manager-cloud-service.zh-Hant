---
title: 在發佈層級上支援AEM as a Cloud Service的開放ID連線
description: 瞭解如何在發佈層級為AEM as a Cloud Service設定Open ID Connect (OIDC)
feature: Security
role: Admin
source-git-commit: 7f96e51861cb544f83f8ff557dd923fa5b59c0b2
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 0%

---


# 在發佈層級上支援AEM as a Cloud Service的開放ID連線

## 簡介 {#introduction}

隨著組織更新其數位體驗，安全且可擴充的身分管理成為基本需求。 Adobe Experience Manager (AEM) Cloud Service現在支援Publish層級的OpenID Connect (OIDC)，可與領先的身分提供者(IdP)進行順暢且以標準為基礎的整合，例如Entra ID (Azure AD)、Google、Okta、Auth0、Ping Identity、ForgeRock和OIDC支援的IDP。

OIDC是OAuth 2.0通訊協定之上的身分層，可在維持開發人員簡易性的同時，提供強大的使用者驗證功能。 企業對消費者(B2C)、內部網路和合作夥伴入口網站案例廣泛採用此功能，這類案例需要安全的使用者登入和身分聯盟。

在此之前，AEM客戶負責在發佈層級上實作自己的自訂登入邏輯，這會增加開發時間並帶來長期的維護與安全性挑戰。 透過OIDC的原生支援，AEM Cloud Service為存取發佈環境的一般使用者提供安全、可延伸且支援Adobe的驗證機制，消除了這項負擔。

無論您是要提供個人化的消費者網站或經過驗證的內部入口網站，OIDC on Publish都能透過集中化的身分控管簡化身分同盟，並降低風險。 此外，還能協助企業在不犧牲靈活性的情況下，符合現代化的法規遵循與安全性標準。

## 設定AEM以進行OIDC驗證 {#configure-aem-oidc-authentication}

### 先決條件 {#prerequisits}

我們假設下列資訊可供使用或定義：

1. AEM存放庫中受保護內容的路徑
1. 要設定之IdP的識別碼。 可以是任何字串

IdP設定的資訊：

1. IdP中設定的使用者端ID
1. 在Idp中設定的使用者端密碼。 若已在Idp上設定PKCE，則使用者端密碼不可用。 請勿將純文字值儲存在設定檔案中。 使用CM密碼並加以參照
1. 在Idp上設定的範圍。 至少必須提供範圍`openid`
1. IdP上是否啟用PKCE
1. `callbackUrl`是使用點1所定義的其中一個設定路徑，並新增尾碼來定義： `/j_security_check`
1. 存取標準`baseUrl`檔案的`.well-known`。 例如，如果已知的URL為： `https://login.microsoftonline.com/53279d7a-438f-41cd-a6a0-fdb09efc8891/v2.0/.well-known/openid-configuration`，`baseUrl`為： `https://login.microsoftonline.com/53279d7a-438f-41cd-a6a0-fdb09efc8891`

### 組態檔概述 {#overview-of-the-configuration-files}

在下方尋找需要設定的檔案清單：

1. **OIDC連線**： `OidcAuthenticationHandler`將使用此連線來驗證使用者，或其他元件將使用此連線來授權[使用OAuth存取受IdP保護的資源](https://github.com/apache/sling-org-apache-sling-auth-oauth-client)
1. **OIDC驗證處理常式**：這是用來驗證存取設定路徑之使用者的驗證處理常式
1. **UserInfoProcessor**：此元件會處理IdP收到的資訊。 客戶可以擴充此功能以實作自訂邏輯
1. [**預設同步處理常式**](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html)：此元件會在存放庫中建立使用者
1. [**ExternalLoginModule**](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html)：此元件驗證本機Oak存放庫中的使用者。

下圖顯示提及的組態元素如何連結。 請注意，由於這些是`ServiceFactory`元件，`~uniqueid`可以是任何隨機唯一字串：

![OIDC組態圖表](/help/security/assets/oidc-diagram.png)

### 設定OIDC連線 {#configure-the-oidc-connection}

首先，我們需要設定OIDC連線。 可以設定多個OIDC連線，而且每個連線都必須有不同的名稱。

1. 建立將容納組態的新`.cfg.json`檔案。 例如，您可以使用`org.apache.sling.auth.oauth_client.impl.OidcConnectionImpl~azure.cfg.json` - **azure**&#x200B;尾碼必須是連線的唯一識別碼
1. 請遵循以下範例中的設定格式：

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

1. 依照以下方式設定其屬性：
   * **「名稱」**&#x200B;可由使用者定義
   * `baseUrl`、`clientid`和`clientSecret`是來自IdP的設定值。
   * 範圍必須至少包含值`openid`。

### 設定OIDC驗證處理常式 {#configure-oidc-authentication-handler}

現在設定OIDC驗證處理常式。 可以設定多個OIDC連線。 每個檔案都必須有不同的名稱。 如果他們共用相同的[OAK外部身分提供者](https://jackrabbit.apache.org/oak/docs/security/authentication/identitymanagement.html)，則可以共用使用者。

1. 建立組態檔。 在此範例中，我們將使用`org.apache.sling.auth.oauth_client.impl.OidcConnectionImpl~azure.cfg.json`。 `azure`尾碼必須是唯一識別碼。 請參閱以下的設定檔範例：

   ```
   {
     "path":"/content/tests/us/en/test-7",
     "callbackUri":"http://localhost:14503/content/tests/us/en/test-7/j_security_check",
     "pkceEnabled":false,
     "defaultConnectionName":"azure"
     "idp": "azure-idp"
   }
   ```

1. 接著，依照下列方式設定其屬性：
   * `path`：要保護的路徑
   * `callbackUri`：至要保護的路徑，新增尾碼： `/j_security_check`
   * `defaultConnectionName`：使用先前步驟中為OIDC連線定義的相同名稱進行設定+
   * `pkceEnabled`：授權代碼流程上代碼交換(PKCE)的`true`證明金鑰
   * `idp`： [OAK外部身分提供者](https://jackrabbit.apache.org/oak/docs/security/authentication/identitymanagement.html)的名稱。 請注意，不同的OAK IDP無法共用使用者或群組

### 設定SlingUserInfoProcessor

1. 建立組態檔。 在此範例中，我們將使用`org.apache.sling.auth.oauth_client.impl.SlingUserInfoProcessor~azure.cfg.json`。 `azure`尾碼必須是唯一識別碼。 請參閱以下的設定檔範例：

   ```
   {
      "groupsInIdToken":true,
      "groupsClaimName": "groups",
      "connection":"azure",
      "storeAccessToken": false,
      "storeRefreshToken": false
   }
   ```

1. 接著，依照下列方式設定其屬性：
   * `groupsInIdToken`：如果群組是以ID權杖傳送，則設為true。 如果值為false或未指定，則會從UserInfo端點讀取群組。
   * `groupsClaimName`：宣告的名稱包含要在AEM中同步的群組。
   * `connection`：使用先前步驟中為OIDC連線定義的相同名稱進行設定
   * `storeAccessToken`： true如果存取權杖必須儲存在存放庫中。 預設為false。 只有在AEM需要代表儲存在受相同IdP保護的外部伺服器中的使用者存取資源時，才可將其設為true。
   * `storeRefreshToken`：如果重新整理權杖必須儲存在存放庫中，則為true。 預設為false。 只有在AEM需要代表儲存在受相同IdP保護的外部伺服器中的使用者存取資源，並需要從IdP重新整理權杖時，才可將其設為true。
請注意，存取Token和重新整理Token是以AEM主要金鑰加密儲存。


### 設定同步處理常式 {#configure-the-synchronization-handler}

必須至少設定一個同步處理常式，才能同步在Oak中驗證的使用者。 如需詳細資訊，請參閱[此](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html)頁面。

建立名為`org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler~azure.cfg.json`的檔案。 **azure**&#x200B;尾碼必須是唯一識別碼。 如需如何設定其屬性的詳細資訊，請參閱[Oak使用者和群組同步檔案](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html)。 請尋找下方的設定範例：

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

以下是一些要在DefaultSyncHandler中設定的最相關屬性。 請注意應一律在Cloud Services中啟用動態群組成員資格。

| 屬性名稱 | 備註 | 建議值 |
|---|---|---|
| `user.expirationTime` | 同步的使用者過期之前的持續時間。 使用者只會在到期時間之後進行同步處理。 | 1h |
| `user.membershipExpTime` | 同步的使用者成員資格到期之前的持續時間。 使用者會籍僅在到期時間後同步。 | 1h |
| `user.dynamicMembership` | 我們建議啟用動態群組成員資格 | true |
| `user.enforceDynamicMembership` | 我們建議啟用動態群組成員資格的強制執行 | true |
| `group.dynamicGroups` | 我們建議啟用動態群組 | true |
| user.propertyMapping | 提供的`UserInfoProcessor`實作只會同步少數幾個屬性。 您可以修改和自訂。 | <code>&quot;profile/givenName=profile/given_name&quot;，</code><br><code>&quot;profile/familyName=profile/family_name&quot;，</code><br><code>&quot;rep:fullname=profile/name&quot;，</code><br><code>&quot;profile/email=profile/email&quot;，</code><br><code>&quot;access_token=access_token&quot;，</code><br><code>&quot;refresh_token=refresh_token&quot;</code> |  |
| `user.membershipNestingDepth` | 同步成員關係時，傳回群組巢狀的最大深度。 如果值為0，則會有效地停用群組成員資格查閱。 值1隻會新增使用者的直接群組。 只有在同步使用者成員資格祖先時，同步個別群組時，這個值才無效。 | 1 |

### 設定外部登入模組 {#configure-the-external-login-module}

最後，您需要設定外部登入模組。

1. 建立名為`org.apache.jackrabbit.oak.spi.security.authentication.external.impl.ExternalLoginModuleFactory~azure.cfg.json`的檔案。 請參閱以下的設定範例：

   ```
   {
    "sync.handlerName":"azure",
    "idp.name":"azure-idp"
   }
   ```

1. 依照以下方式設定其屬性：

   * `sync.handlerName`：先前定義的同步處理常式名稱
   * `idp.name`：在OIDC驗證處理常式中定義的OAK身分提供者

### 可選：實作自訂UserInfoProcessor {#implement-a-custom-userinfoprocessor}

使用者已由ID權杖驗證，並且會在為IdP定義的`userInfo`端點中擷取其他屬性。 如果必須執行其他非標準作業，則[UserInfoProcessor](https://github.com/apache/sling-org-apache-sling-auth-oauth-client/blob/master/src/main/java/org/apache/sling/auth/oauth_client/impl/SlingUserInfoProcessorImpl.java)的自訂實作是Sling的預設實作。

## 範例：使用Azure Active Directory設定OIDC驗證

### 在Azure Active Directory中設定新的應用程式 {#configure-a-new-application-in-azure-ad}

1. 依照[Azure Active Directory檔案](https://learn.microsoft.com/en-us/power-pages/security/authentication/openid-settings#create-an-app-registration-in-azure)在Azure Active Directory中建立新的應用程式。  請參閱下方詳細說明應用程式概觀的畫面外觀：

   ![應用程式概述](/help/security/assets/odic-application-overview.png)

1. 如果需要群組或應用程式角色，請按照[檔案](https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-use-app-roles-customers)中的說明為應用程式啟用它們，並在ID權杖中傳送。 以下是已設定群組的範例：

![OIDC宣告權杖識別碼](/help/security/assets/oidc-claim-id-token.png)

1. 按照先前記錄的步驟建立所需的組態檔。 以下是特定於Azure AD的範例，其中：
   * 我們將oidc連線、驗證處理常式和DefaultSyncHandler的名稱定義為： `azure`
   * 網站URL為： `www.mywebsite.com`
   * 我們保護路徑`/content/wknd/us/en/adventures`
   * 租使用者為： `tennat-id`，
   * 使用者端識別碼為： `client-id`，
   * 密碼為： `secret`，
   * 群組會以ID權杖傳送，宣告名稱為： `groups`

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

### Azure AD群組的其他資訊 {#additional-information-about-azure-ad-groups}

若要在Microsoft Azure入口網站中為企業應用程式設定群組，您必須在&#x200B;**企業應用程式**&#x200B;上搜尋應用程式並新增群組： <!-- Alexandru: this bit cound be clearer-->

![OIDC群組新增](/help/security/assets/oidc-ad-additional-info.png)

若要在ID權杖中啟用群組宣告，請在Microsoft Azure入口網站的&#x200B;**權杖設定**&#x200B;區段中新增宣告： <!-- Alexandru: this bit cound be clearer as well-->

![OIDC宣告權杖識別碼](/help/security/assets/oidc-claim-id-token.png)

必須修改`SlingUserInfoProcessor`的設定，如同下列範例一樣。

需要修改的檔案名稱是`org.apache.sling.auth.oauth_client.impl.SlingUserInfoProcessorImpl.cfg.json`。 內容應依照以下方式設定：

```
{
  "connection": "azure",
  "groupsInIdToken": "true",
  "storeAccessToken": "false",
  "storeRefreshToken": "false"
}
```
