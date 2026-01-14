---
title: 如何使用Forms as a Cloud Service將資料與XDP和PDF範本合併，或產生PCL、ZPL和PostScript格式的輸出？
description: 自動將資料與 XDP 和 PDF 範本合併，或產生 PCL、ZPL 和 PostScript 格式的輸出
exl-id: 9fa9959e-b4f2-43ac-9015-07f57485699f
feature: Adaptive Forms,APIs & Integrations
role: Admin, Developer, User
source-git-commit: 43b648eb3984867fda35ee04de10b78dd836b481
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 6%

---


# 使用同步處理 {#sync-processing-introduction}

Forms as a Cloud Service - Communications API可讓您建立、彙總及提供品牌導向和個人化通訊，例如業務往來函、檔案、報表、索賠處理信函、利益通知、索賠處理信函、每月帳單和歡迎套件。 您可以使用Communications API將範本(XFA或PDF)與客戶資料結合，以產生PDF、PS、PCL、DPL、IPL和ZPL格式的檔案。

假設您有一或多個範本，且每個範本有多個XML資料記錄。 您可以使用Communications API為每筆記錄產生列印檔案。 <!-- You can also combine the records into a single document. -->結果為非互動式PDF檔案。 非互動式PDF檔案不允許使用者在其欄位中輸入資料。

Forms as a Cloud Service — 通訊功能提供隨選和批次API （非同步API），用於產生排程檔案：

* 同步API適用於隨選、低延遲和單一記錄檔案產生使用案例。 這些 API 更適合根據使用者動作的使用案例。例如，在使用者填寫表單後產生檔案。

* 批次API （非同步API）適合用於排程的高輸送量多檔案產生使用案例。 這些 API 批次產生文件。例如，每月產生的電話帳單、信用卡報表和福利報表。

## 使用同步作業 {#batch-operations}

同步作業是以線性方式產生檔案的程式。 這些API分類為單一租使用者API和多租使用者API：

### 單一租使用者API

* 檔案產生API
* 檔案操作API

<!-- 
### Multi-tenant APIs

* Document utility APIs -->


### 驗證單一租使用者API

單一租使用者API操作支援兩種型別的驗證：

* **基本驗證**：基本驗證是內建在HTTP通訊協定中的簡單驗證配置。 使用者端傳送的HTTP要求具有Authorization標頭，其中包含Basic這個字，後面接著空格以及base64編碼字串使用者名稱:password。 例如，若要授權為管理員/管理員，使用者端會傳送基本[base64編碼字串使用者名稱]： [base64編碼字串密碼]。

* **權杖式驗證：**&#x200B;權杖式驗證使用存取權杖（持有者驗證權杖）向Experience Manager as a Cloud Service提出要求。 AEM Forms as a Cloud Service提供API以安全地擷取存取Token。 若要擷取並使用權杖來驗證請求：

   1. [從Developer Console](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html)擷取Experience Manager as a Cloud Service認證。
   1. [在您的環境中安裝Experience Manager as a Cloud Service認證](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html)。 (應用程式伺服器、網頁伺服器或其他非AEM伺服器)設定為傳送要求給（進行呼叫）雲端服務。
   1. [產生JWT權杖並與Adobe IMS API交換存取權杖](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html)。
   1. 使用存取權杖作為持有者驗證權杖來執行Experience Manager API。
   1. [在Experience Manager環境中為技術帳戶使用者設定適當的許可權](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=en#configure-access-in-aem)。

  >[!NOTE]
  >
  >Adobe建議在生產環境中使用權杖型驗證。

  >[!IMPORTANT]
  >
  > 如需詳細資訊，請參閱[OAuth伺服器對伺服器驗證](/help/forms/oauth-api-authetication.md)和[JWT伺服器對伺服器驗證](/help/forms/jwt-api-authentication.md)。
<!-- 

### Authenticate a multi-tenant API

#### Authentication Headers

Every inbound HTTP API call to the multi-tenant API must contain these three headers:


* `x-api-key`
* `x-gw-ims-org-id`
* `Authorization`

The values which should be sent in the `x-api-key` and `x-gw-ims-org-id` headers are provided in the Credentials details screen in the [Adobe Developer Console](https://developer.adobe.com/console). The value of the `x-api-key` header is the Client ID and the value for the `x-gw-ims-org-id` header is the Organization ID.

#### Configure Adobe Developer console to generate an access token

To set up authentication APIs, create a project in Adobe Developer Console and add Communication APIs to the project on Adobe Developer Console. The integration generates API Key, Client Secret, Payload (JWT):

1. Contact you Adobe Developer Console administrator. Ask the administrator to add as a developer.
1. Log in to `https://developer.adobe.com/console/`. Use your developer account that your administrator has provisioned to log in to Adobe Developer Console.
1. Select your organization from the top-right corner. If you do not know your organization, contact your administrator.
1. Select **[!UICONTROL Create new project]**. A screen to get started with your new project appears. Select **[!UICONTROL Add API]**. A screen with list of all the APIs enabled for your account appears.
1. Select **[!UICONTROL AEM Forms - Communications]** and select **[!UICONTROL Next]**. A screen to configure the API appears.
1. Select **[!UICONTROL OPTION 1 Generate a key pair]** and select **[!UICONTROL Generate keypair]**. It creates and downloads the configuration file. The downloaded configuration file contains all your app settings, along with the only copy of your private key. Adobe does not record your private key, make sure to securely store the downloaded file. Select **[!UICONTROL Next]**.
1. Select **[!UICONTROL Integrations - Cloud Service]** and select **[!UICONTROL Save configured API]**. Select **[!UICONTROL Service Account (JWT)]** to view the API Key, Client Secret, and other information required to access the APIs. You set to use the token to access the APIs.

#### Programmatically generate and use an access token

To programmatically generate an access token, generate a JSON Web Token (JWT) and exchange it with the Adobe Identity Management Service (IMS) for an access token.

Use the following keys, referred to as claims, to construct JWT JSON object:


* `exp`- the requested expiration of the access token, expressed as several seconds since January 1, 1970 GMT. For most use cases, this is a relatively small value. For example, 5 minutes, for five minutes from now, this value should be 1670923791.
* `iss` - the Organization ID from the Adobe Developer Console project, in the format org_ident@AdobeOrg.
* `sub` - the Technical Account ID from the Adobe Developer Console integration, in the format: id@techacct.adobe.com.
* `aud` - the Client ID from the Adobe Developer Console integration prepended with `https://ims-na1.adobelogin.com/c/`.
* `https://ims-na1-stg1.adobelogin.com/s/ent_aemforms_docprocessing` - set to the literal value `true`

This JSON object must be then base64 encoded and signed using the private key for the project. Finally, the encoded value is sent in the body of a POST request to `https://ims-na1.adobelogin.com/ims/exchange/jwt` along with the Client ID and Client Secret for the project.

##### Example

```JSON

    ========================= REQUEST ==========================
    POST https://ims-na1.adobelogin.com/ims/exchange/jwt
    -------------------------- body ----------------------------
    client_id={myClientId}&client_secret={myClientSecret}&jwt_token={myJSONWebToken}
    ------------------------- headers --------------------------
    Content-Type: application/x-www-form-urlencoded
    Cache-Control: no-cache

```

#### Language Support for JWT

While it is possible to do the entire JWT generation and exchange process in custom code, it is more common to use a higher-level library to do so. A number of such libraries are listed on the [Adobe I/O JWT Documentation](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/).

-->

### （僅適用於Document Generation API）設定資產和許可權

若要使用同步API，需具備下列條件：

* 具有Experience Manager管理員許可權的使用者
* 將範本和其他資產上傳到您的Experience Manager Forms Cloud Service執行個體

### （僅適用於Document Generation API）將範本和其他資產上傳至您的Experience Manager執行個體

組織通常有多個範本。 例如，信用卡對帳單、福利對帳單，以及索賠申請各有一個範本。 將所有這類XDP和PDF範本上傳到您的Experience Manager執行個體。 若要上傳範本：

1. 開啟Experience Manager執行個體。
1. 前往「Forms > Forms和檔案」
1. 按一下「建立>資料夾」並建立資料夾。 開啟資料夾。
1. 按一下「建立>檔案上傳」並上傳範本。

### 叫用API

[API參考檔案](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)提供API提供的所有引數、驗證方法和各種服務的詳細資訊。 API參考檔案也提供.yaml格式的API定義檔案。 您可以下載.yaml檔案並將其上傳到[Postman](https://www.postman.com/)，以檢查API的功能。

>[!VIDEO](https://video.tv.adobe.com/v/335771)

>[!NOTE]
>
> 瞭解叫用AEM Forms Communication API的詳細步驟，請參閱[使用OAuth伺服器對伺服器驗證叫用AEM Forms Communications API](/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md)文章。

>[!MORELIKETHIS]
>
>* [AEM Forms as a Cloud Service通訊簡介](/help/forms/aem-forms-cloud-service-communications-introduction.md)
>* 最適化AEM Forms和通訊API的[Forms as a Cloud Service架構](/help/forms/aem-forms-cloud-service-architecture.md)
>* [通訊處理 — 同步API](/help/forms/aem-forms-cloud-service-communications.md)
>* [通訊處理 — 批次API](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)
>* [Forms Communications API — 教學課程](/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md)