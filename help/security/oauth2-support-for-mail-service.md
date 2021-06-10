---
title: OAuth2對郵件服務的支援
description: Oauth2對Adobe Experience Manager as aCloud Service中郵件服務的支援
source-git-commit: b46062697b25aa8d3f215a8a4249f5203bec268e
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 0%

---


# OAuth2對郵件服務{#oauth2-support-for-the-mail-service}的支援

AEM as aCloud Service針對其整合式郵件服務提供OAuth2支援，讓組織能夠遵守安全的電子郵件需求。

您可以為多個電子郵件提供者設定OAuth。 以下是配置AEM Mail Service以通過OAuth2使用Microsoft Office 365 Outlook進行身份驗證的逐步說明。 其他廠商也能以類似方式進行設定。

有關AEM as a A Service的詳細資訊，請參閱[Sending Email](/help/implementing/developing/introduction/development-guidelines.md#sending-email)。

## Microsoft Outlook {#microsoft-outlook}

1. 前往[https://portal.azure.com/](https://portal.azure.com/)並登入。
1. 在搜索欄中搜索&#x200B;**Azure Active Directory**，然後按一下結果。 或者，您也可以直接瀏覽至[https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. 按一下&#x200B;**App Registration** - **New Registration**

   ![](assets/oauth-outlook1.png)

1. 根據您的要求填寫資訊，然後按一下&#x200B;**註冊**
1. 前往新建立的應用程式，並選取&#x200B;**API權限**
1. 前往&#x200B;**新增權限** - **圖表權限** - **委派權限**
1. 選取您應用程式的下列權限，然後按一下「**新增權限**」：
   * `SMTP.Send`
   * `Mail.Read`
   * `Mail.Send`
   * `openid`
   * `offline_access`
1. 前往&#x200B;**Authentication** - **新增平台** - **Web**，並在&#x200B;**Redirect Urls**&#x200B;區段中，新增下列URL — 一個包含斜線，一個不含斜線：
   * `http://localhost/`
   * `http://localhost`
1. 新增每個URL後，按&#x200B;**設定**，並根據您的需求進行設定
1. 接下來，轉到&#x200B;**Certificates and Secrets**，按一下&#x200B;**New client secret**，然後按照螢幕上的步驟建立密碼。 請務必注意此機密以供日後使用
1. 在左窗格中按&#x200B;**Overview**，並複製&#x200B;**Application(client)ID**&#x200B;和&#x200B;**Directory(tenant)ID**&#x200B;的值，以供稍後使用

若要重述，您需要下列資訊才能為AEM端的Mail服務設定OAuth2:

* 驗證URL，將以租用戶ID建構。 它會有此表格：`https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/authorize`
* 代號URL，將以租用戶ID建構。 它會有此表格：`https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* 將以租用戶ID建構的重新整理URL。 它會有此表格：`https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* 用戶端ID
* 用戶端密碼

### 生成刷新令牌{#generating-the-refresh-token}

接下來，您需要產生重新整理Token，這將是後續步驟中OSGi設定的一部分。

您可以依照下列步驟來執行此操作：

1. 將`clientID`和`tenantID`取代為帳戶的特定值後，請在瀏覽器中開啟下列URL:`https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/authorize?client_id=<clientId>&response_type=code&redirect_uri=http://localhost&response_mode=query&scope=https%3A%2F%2Foutlook.office365.com%2FSMTP.Send%20EWS.AccessAsUser.All%20https%3A%2F%2Foutlook.office365.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office365.com%2FMail.Read%20https%3A%2F%2Foutlook.office365.com%2FMail.Send%20openid%20offline_access&state=12345`
1. 詢問時允許權限
1. URL會重新導向至以此格式建構的新位置：`http://localhost/?code=<code>&state=12345&session_state=4f984c6b-cc1f-47b9-81b2-66522ea83f81#`
1. 複製上述範例中的`<code>`值
1. 使用下列cURL命令來取得refreshToken。 您需要將tenantID、clientID和clientSecret取代為您的帳戶值，以及`<code>`的值：

   `curl --location --request POST 'https://login.microsoftonline.com/<tenantId>/oauth2/v2.0/token' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--header 'Cookie: buid=0.ARgAep0nU49DzUGmoP2wnvyIkcQjsx26HEpOnvHS0akqXQgYAAA.AQABAAEAAAD--DLA3VO7QrddgJg7Wevry9XPJSKbGVlPt5NWYxLtTl3K1W0LwHXelrffApUo_K02kFrkvmGm94rfBT94t25Zq4bCd5IM3yFOjWb3V22yDM7-rl112sLzbBQBRCL3QAAgAA; esctx=AQABAAAAAAD--DLA3VO7QrddgJg7Wevr4a8wBjYcNbBXRievdTOd15caaeAsQdXeBAQA3tjVQaxmrOXFGkKaE7HBzsJrzA-ci4RRpor-opoo5gpGLh3pj_iMZuqegQPEb1V5sUVQV8_DUEbBv5YFV2eczS5EAhLBAwAd1mHx6jYOL8LwZNDFvd2-MhVXwPd6iKPigSuBxMogAA; x-ms-gateway-slice=estsfd; stsservicecookie=estsfd; fpc=Auv6lTuyAP1FuOOCfj9w0U_5vR5dAQAAALDXP9gOAAAAwIpkkQEAAACT2T_YDgAAAA' \
--data-urlencode 'client_id=<clientID>' \
--data-urlencode 'scope=https://outlook.office365.com/SMTP.Send https://outlook.office365.com/Mail.Read https://outlook.office365.com/Mail.Send openid' \
--data-urlencode 'redirect_uri=http://localhost' \
--data-urlencode 'grant_type=authorization_code' \
--data-urlencode 'client_secret=<clientSecret>' \
--data-urlencode 'code=<code>'`

1. 記下refreshToken和accessToken。

### 驗證Token {#validating-the-tokens}

在AEM端繼續設定OAuth之前，請務必透過下列程式驗證accessToken和refreshToken:

1. 使用先前程式中產生的refreshToken來產生accessToken。 您可以透過下列curl來達成此目標，取代`<client_id>`、`<client_secret>`和`<refreshToken>`的值：

   `curl --location --request POST 'https://login.microsoftonline.com/<tenetId>/oauth2/v2.0/token' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--header 'Cookie: buid=0.ARgAep0nU49DzUGmoP2wnvyIkcQjsx26HEpOnvHS0akqXQgYAAA.AQABAAEAAAD--DLA3VO7QrddgJg7Wevry9XPJSKbGVlPt5NWYxLtTl3K1W0LwHXelrffApUo_K02kFrkvmGm94rfBT94t25Zq4bCd5IM3yFOjWb3V22yDM7-rl112sLzbBQBRCL3QAAgAA; esctx=AQABAAAAAAD--DLA3VO7QrddgJg7Wevr4a8wBjYcNbBXRievdTOd15caaeAsQdXeBAQA3tjVQaxmrOXFGkKaE7HBzsJrzA-ci4RRpor-opoo5gpGLh3pj_iMZuqegQPEb1V5sUVQV8_DUEbBv5YFV2eczS5EAhLBAwAd1mHx6jYOL8LwZNDFvd2-MhVXwPd6iKPigSuBxMogAA; x-ms-gateway-slice=estsfd; stsservicecookie=estsfd; fpc=Auv6lTuyAP1FuOOCfj9w0U_IezHLAQAAAPeNSdgOAAAA' \
--data-urlencode 'client_id=<client_id>' \
--data-urlencode 'scope=https://outlook.office365.com/SMTP.Send https://outlook.office365.com/Mail.Read https://outlook.office365.com/Mail.Send openid' \
--data-urlencode 'redirect_uri=http://localhost' \
--data-urlencode 'grant_type=refresh_token' \
--data-urlencode 'client_secret=<client_secret>' \
--data-urlencode 'refresh_token=<refreshToken>'`

1. 使用accessToken傳送郵件，以查看是否正常運作。

>[!NOTE]
>
> 您可以從[此位置](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-oauth2-auth-code-flow)取得Postman API集合。

### 與AEM as aCloud Service整合{#integration-with-aem-as-a-cloud-service}

1. 使用以下語法，在`/apps/<my-project>/osgiconfig/config`下建立名為`com.day.cq.mailer.oauth.impl.OAuthConfigurationProviderImpl.cfg.json`的OSGI屬性檔案：

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

1. 如前一節所述，透過建構`authUrl`、`tokenUrl`和`refreshURL`來填入。
1. 將以下作用域添加到配置中：
   * `openid`
   * `offline_access`
   * `https://outlook.office365.com/Mail.Send`
   * `https://outlook.office365.com/Mail.Read`
   * `https://outlook.office365.com/SMTP.Send`
1. 建立OSGI屬性檔案`called com.day.cq.mailer.impl.DefaultMailService.cfg.json`
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

1. 對於Outlook,`smtp.host`配置值為`smtp.office365.com`
1. 在執行階段，使用Cloud Manager變數API傳遞`refreshToken values`和`clientSecret`機密，如[此處](/help/implementing/deploying/configuring-osgi.md#setting-values-via-api)所述。 應定義變數`SECRET_SMTP_OAUTH_REFRESH_TOKEN`和`SECRET_SMTP_OAUTH_CLIENT_SECRET`的值。

### 疑難排解 {#troubleshooting}

如果郵件服務無法正常運作，在大多數情況下，您將需要如上所述重新產生`refreshToken`，並透過Cloud Manager API傳入新值。 部署新值需要幾分鐘的時間。
