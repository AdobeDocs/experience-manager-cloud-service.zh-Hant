---
title: 郵件服務的OAuth2支援
description: Oauth2對Adobe Experience Manager as a Cloud Service郵件服務的支援
exl-id: 93e7db8b-a8bf-4cc7-b7f0-cda481916ae9
source-git-commit: 4a5967f682d122d20528b1d904590fb82f438fa7
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 0%

---

# 郵件服務的OAuth2支援 {#oauth2-support-for-the-mail-service}

AEMas a Cloud Service為其整合郵件服務提供OAuth2支援，以便組織能夠遵守安全電子郵件要求。

您可以為多個電子郵件提供程式配置OAuth。 以下是有關將郵件服務配置為通過OAuth2AEM與MicrosoftOffice 365 Outlook進行身份驗證的逐步說明。 其他供應商可以以類似方式進行配置。

有關as a Cloud Service郵件服AEM務的詳細資訊，請參見 [發送電子郵件](/help/implementing/developing/introduction/development-guidelines.md#sending-email)。

## Microsoft展望 {#microsoft-outlook}

1. 轉到 [https://portal.azure.com/](https://portal.azure.com/) 登錄。
1. 搜索 **Azure Active Directory** 的子菜單。 或者，您可以直接瀏覽到 [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. 按一下 **應用註冊** - **新建註冊**

   ![](assets/oauth-outlook1.png)

1. 根據您的要求填寫資訊，然後按一下 **註冊**
1. 轉到新建立的應用，然後選擇 **API權限**
1. 轉到 **添加權限** - **圖形權限** - **授權權限**
1. 為你的應用選擇以下權限，然後按一下 **添加權限**:
   * `SMTP.Send`
   * `Mail.Read`
   * `Mail.Send`
   * `openid`
   * `offline_access`
1. 轉到 **驗證** - **添加平台** - **Web**&#x200B;的 **重定向URL** 部分，添加以下URL — 一個帶正斜槓，一個不帶正斜槓：
   * `http://localhost/`
   * `http://localhost`
1. 按 **配置** 添加每個URL並根據您的要求配置設定後
1. 下一步，轉到 **證書和機密**，按一下 **新客戶機密鑰** 並按照螢幕上的步驟建立機密。 請務必注意此機密供以後使用
1. 按 **概述** 在左窗格中，複製 **應用程式（客戶端）ID** 和 **目錄（租戶）ID** 供以後使用

若要重新訪問，您需要以下資訊來為一側的Mail服務配置OAuth2AEM :

* 將使用租戶ID構建的身份驗證URL。 它將具有以下形式： `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/authorize`
* 將使用租戶ID構建的令牌URL。 它將具有以下形式： `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* 將使用租戶ID構建的刷新URL。 它將具有以下形式： `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* 客戶端ID
* 客戶機密碼

### 生成刷新令牌 {#generating-the-refresh-token}

接下來，您需要生成刷新令牌，該令牌將是後續步驟中OSGi配置的一部分。

您可以通過以下步驟來完成此操作：

1. 替換後在瀏覽器中開啟以下URL `clientID` 和 `tenantID` 具有特定於帳戶的值： `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/authorize?client_id=<clientId>&response_type=code&redirect_uri=http://localhost&response_mode=query&scope=https%3A%2F%2Foutlook.office365.com%2FSMTP.Send%20EWS.AccessAsUser.All%20https%3A%2F%2Foutlook.office365.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office365.com%2FMail.Read%20https%3A%2F%2Foutlook.office365.com%2FMail.Send%20openid%20offline_access&state=12345`
1. 在詢問時允許權限
1. URL將重定向到以下格式構建的新位置： `http://localhost/?code=<code>&state=12345&session_state=4f984c6b-cc1f-47b9-81b2-66522ea83f81#`
1. 複製的值 `<code>` 上例
1. 使用以下cURL命令獲取refreshToken。 您需要用帳戶的值以及 `<code>`:

   ```
   curl --location --request POST 'https://login.microsoftonline.com/<tenantId>/oauth2/v2.0/token' \
   --header 'Content-Type: application/x-www-form-urlencoded' \
   --header 'Cookie: buid=0.ARgAep0nU49DzUGmoP2wnvyIkcQjsx26HEpOnvHS0akqXQgYAAA.AQABAAEAAAD--DLA3VO7QrddgJg7Wevry9XPJSKbGVlPt5NWYxLtTl3K1W0LwHXelrffApUo_K02kFrkvmGm94rfBT94t25Zq4bCd5IM3yFOjWb3V22yDM7-rl112sLzbBQBRCL3QAAgAA; esctx=AQABAAAAAAD--DLA3VO7QrddgJg7Wevr4a8wBjYcNbBXRievdTOd15caaeAsQdXeBAQA3tjVQaxmrOXFGkKaE7HBzsJrzA-ci4RRpor-opoo5gpGLh3pj_iMZuqegQPEb1V5sUVQV8_DUEbBv5YFV2eczS5EAhLBAwAd1mHx6jYOL8LwZNDFvd2-MhVXwPd6iKPigSuBxMogAA; x-ms-gateway-slice=estsfd; stsservicecookie=estsfd; fpc=Auv6lTuyAP1FuOOCfj9w0U_5vR5dAQAAALDXP9gOAAAAwIpkkQEAAACT2T_YDgAAAA' \
   --data-urlencode 'client_id=<clientID>' \
   --data-urlencode 'scope=https://outlook.office365.com/SMTP.Send https://outlook.office365.com/Mail.Read https://outlook.office365.com/Mail.Send openid' \
   --data-urlencode 'redirect_uri=http://localhost' \
   --data-urlencode 'grant_type=authorization_code' \
   --data-urlencode 'client_secret=<clientSecret>' \
   --data-urlencode 'code=<code>'
   ```

1. 記下refreshToken和accessToken。

### 驗證令牌 {#validating-the-tokens}

在繼續在一側配置OAuth之AEM前，請確保使用以下過程驗證accessToken和refreshToken:

1. 使用上一過程中生成的refreshToken生成accessToken。 可以通過以下curl來實現此目的，並替換 `<client_id>`。`<client_secret>` 和 `<refreshToken>`:

   ```
   curl --location --request POST 'https://login.microsoftonline.com/<tenetId>/oauth2/v2.0/token' \
   --header 'Content-Type: application/x-www-form-urlencoded' \
   --header 'Cookie: buid=0.ARgAep0nU49DzUGmoP2wnvyIkcQjsx26HEpOnvHS0akqXQgYAAA.AQABAAEAAAD--DLA3VO7QrddgJg7Wevry9XPJSKbGVlPt5NWYxLtTl3K1W0LwHXelrffApUo_K02kFrkvmGm94rfBT94t25Zq4bCd5IM3yFOjWb3V22yDM7-rl112sLzbBQBRCL3QAAgAA; esctx=AQABAAAAAAD--DLA3VO7QrddgJg7Wevr4a8wBjYcNbBXRievdTOd15caaeAsQdXeBAQA3tjVQaxmrOXFGkKaE7HBzsJrzA-ci4RRpor-opoo5gpGLh3pj_iMZuqegQPEb1V5sUVQV8_DUEbBv5YFV2eczS5EAhLBAwAd1mHx6jYOL8LwZNDFvd2-MhVXwPd6iKPigSuBxMogAA; x-ms-gateway-slice=estsfd; stsservicecookie=estsfd; fpc=Auv6lTuyAP1FuOOCfj9w0U_IezHLAQAAAPeNSdgOAAAA' \
   --data-urlencode 'client_id=<client_id>' \
   --data-urlencode 'scope=https://outlook.office365.com/SMTP.Send https://outlook.office365.com/Mail.Read https://outlook.office365.com/Mail.Send openid' \
   --data-urlencode 'redirect_uri=http://localhost' \
   --data-urlencode 'grant_type=refresh_token' \
   --data-urlencode 'client_secret=<client_secret>' \
   --data-urlencode 'refresh_token=<refreshToken>'
   ```

1. 使用accessToken發送郵件，以查看是否正常工作。

>[!NOTE]
>
> 您可以從 [此位置](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-oauth2-auth-code-flow)。

### 與AEMas a Cloud Service {#integration-with-aem-as-a-cloud-service}

1. 建立名為的OSGI屬性檔案 `com.day.cq.mailer.oauth.impl.OAuthConfigurationProviderImpl.cfg.json` 在 `/apps/<my-project>/osgiconfig/config` 使用以下語法：

   ```
   {
       authUrl: "<Authorization Url>",
       tokenUrl: "<Token Url>",
       clientId: "<clientID>",
       clientSecret: "$[secret:SECRET_SMTP_OAUTH_CLIENT_SECRET]",
       scopes: [
          "scope1",
          "scope2"
       ],
       refreshUrl: "<Refresh token Url>",
       refreshToken: "$[secret:SECRET_SMTP_OAUTH_REFRESH_TOKEN]"
   }
   ```

1. 填寫 `authUrl`。 `tokenUrl` 和 `refreshURL` 按前一節所述構建。
1. 將以下作用域添加到配置中：
   * `openid`
   * `offline_access`
   * `https://outlook.office365.com/Mail.Send`
   * `https://outlook.office365.com/Mail.Read`
   * `https://outlook.office365.com/SMTP.Send`
1. 建立OSGI屬性檔案 `called com.day.cq.mailer.impl.DefaultMailService.cfg.json`
在 
`/apps/<my-project>/osgiconfig/config`  使用以下語法：

   ```
   {
    "smtp.host": "<smtp hostname>"
    "smtp.user": "<user account that logged into get the oauth tokens>",
    "smtp.password": "value not used",
    "smtp.port": 587,
    "from.address": "<from address used for sending>"
    "smtp.ssl": false,
    "smtp.starttls": true,
    "smtp.requiretls": true,
    "debug.email": false,
    "oauth.flow": true
   }
   ```

1. 對於Outlook, `smtp.host` 配置值為 `smtp.office365.com`
1. 在運行時，傳入 `refreshToken values` 和 `clientSecret` 使用Cloud Manager變數API的機密（如所述） [這裡](/help/implementing/deploying/configuring-osgi.md#setting-values-via-api)。 變數的值 `SECRET_SMTP_OAUTH_REFRESH_TOKEN`  和 `SECRET_SMTP_OAUTH_CLIENT_SECRET` 應該定義。

### 疑難排解 {#troubleshooting}

如果郵件服務無法正常工作，則在大多數情況下，您需要重新生成 `refreshToken` 如上所述，通過Cloud Manager API傳遞新值。 部署新值需要幾分鐘。
