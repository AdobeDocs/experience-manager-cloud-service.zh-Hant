---
title: OAuth2對郵件服務的支援
description: Oauth2對Adobe Experience Manager as a Cloud Service中郵件服務的支援
exl-id: 93e7db8b-a8bf-4cc7-b7f0-cda481916ae9
source-git-commit: 5f8da9f846c159aa00273909b93aa10358daf609
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 0%

---

# OAuth2對郵件服務的支援 {#oauth2-support-for-the-mail-service}

AEM as a Cloud Service為其整合式Mail Service提供OAuth2支援，讓組織能遵守安全的電子郵件需求。

您可以為多個電子郵件提供者設定OAuth。 以下是設定AEM Mail Service以透過OAuth2使用Microsoft Office 365 Outlook進行驗證的逐步指示。 其他廠商也能以類似方式進行設定。

如需AEMas a Cloud Service郵件服務的詳細資訊，請參閱 [傳送電子郵件](/help/implementing/developing/introduction/development-guidelines.md#sending-email).

## Microsoft Outlook {#microsoft-outlook}

1. 前往 [https://portal.azure.com/](https://portal.azure.com/) 並登入。
1. 搜尋 **Azure Active Directory** 在搜尋列中，按一下結果。 或者，您可以直接瀏覽至 [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. 按一下 **應用程式註冊** - **新註冊**

   ![](assets/oauth-outlook1.png)

1. 根據您的需求填寫資訊，然後按一下 **註冊**
1. 前往新建立的應用程式，然後選取 **API權限**
1. 前往 **新增權限** - **圖表權限** - **委派權限**
1. 選取您應用程式的下列權限，然後按一下 **新增權限**:
   * `SMTP.Send`
   * `Mail.Read`
   * `Mail.Send`
   * `openid`
   * `offline_access`
1. 前往 **驗證** - **新增平台** - **Web**，和 **重新導向Url** 區段中，新增下列URL — 一個含有，一個不含正斜線：
   * `http://localhost/`
   * `http://localhost`
1. Press **設定** 新增每個URL，並根據您的需求進行設定
1. 接下來，轉到 **憑證和機密**，按一下 **新用戶端密碼** 並依照畫面上的步驟建立密碼。 請務必注意此機密以供日後使用
1. Press **概述** 並複製 **應用程式（客戶端）ID** 和 **目錄（租用戶）ID** 供稍後使用

若要重述，您需要下列資訊才能為AEM端的Mail服務設定OAuth2:

* 驗證URL，將以租用戶ID建構。 它會有此表格： `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/authorize`
* 代號URL，將以租用戶ID建構。 它會有此表格： `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* 將以租用戶ID建構的重新整理URL。 它會有此表格： `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* 用戶端ID
* 用戶端密碼

### 產生重新整理代號 {#generating-the-refresh-token}

接下來，您需要產生重新整理Token，這將是後續步驟中OSGi設定的一部分。

您可以依照下列步驟來執行此操作：

1. 取代後，在瀏覽器中開啟下列URL `clientID` 和 `tenantID` 以及您帳戶的特定值： `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/authorize?client_id=<clientId>&response_type=code&redirect_uri=http://localhost&response_mode=query&scope=https%3A%2F%2Foutlook.office365.com%2FSMTP.Send%20EWS.AccessAsUser.All%20https%3A%2F%2Foutlook.office365.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office365.com%2FMail.Read%20https%3A%2F%2Foutlook.office365.com%2FMail.Send%20openid%20offline_access&state=12345`
1. 詢問時允許權限
1. URL會重新導向至以此格式建構的新位置： `http://localhost/?code=<code>&state=12345&session_state=4f984c6b-cc1f-47b9-81b2-66522ea83f81#`
1. 複製 `<code>` 在上述範例中
1. 使用下列cURL命令來取得refreshToken。 您需要將tenantID、clientID和clientSecret取代為您帳戶的值，以及 `<code>`:

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

### 驗證Token {#validating-the-tokens}

在AEM端繼續設定OAuth之前，請務必透過下列程式驗證accessToken和refreshToken:

1. 使用先前程式中產生的refreshToken來產生accessToken。 您可以透過下列curl來達成此目標，取代 `<client_id>`,`<client_secret>` 和 `<refreshToken>`:

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

1. 使用accessToken傳送郵件，以查看是否正常運作。

>[!NOTE]
>
> 您可以從以下位置取得Postman API集合： [此位置](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-oauth2-auth-code-flow).

### 與AEMas a Cloud Service整合 {#integration-with-aem-as-a-cloud-service}

1. 建立名為的OSGI屬性檔案 `com.day.cq.mailer.oauth.impl.OAuthConfigurationProviderImpl.cfg.json` 在 `/apps/<my-project>/osgiconfig/config` 語法：

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

1. 填入 `authUrl`, `tokenUrl` 和 `refreshURL` 依前一節所述建構。
1. 將以下作用域添加到配置中：
   * `openid`
   * `offline_access`
   * `https://outlook.office365.com/Mail.Send`
   * `https://outlook.office365.com/Mail.Read`
   * `https://outlook.office365.com/SMTP.Send`
1. 建立OSGI屬性檔案 `called com.day.cq.mailer.DefaultMailService.cfg.json`
在 
`/apps/<my-project>/osgiconfig/config`  語法：

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

1. 對於Outlook, `smtp.host` 設定值為 `smtp.office365.com`
1. 在執行階段中，將 `refreshToken values` 和 `clientSecret` 使用Cloud Manager變數API的機密（如所述） [此處](/help/implementing/deploying/configuring-osgi.md#setting-values-via-api). 變數的值 `SECRET_SMTP_OAUTH_REFRESH_TOKEN`  和 `SECRET_SMTP_OAUTH_CLIENT_SECRET` 應定義。

### 疑難排解 {#troubleshooting}

如果郵件服務無法正常運作，在大多數情況下，您將需要重新產生 `refreshToken` 如上所述，透過Cloud Manager API傳遞新值。 部署新值需要幾分鐘的時間。
