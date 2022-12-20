---
title: AEM Formsas a Cloud Service — 通訊
description: 自動將資料與XDP和PDF模板合併，或以PCL、ZPL和PostScript格式生成輸出
exl-id: 9fa9959e-b4f2-43ac-9015-07f57485699f
source-git-commit: 33e59ce272223e081710294a2e2508edb92eba52
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 0%

---


# 使用同步處理 {#sync-processing-introduction}

Formsas a Cloud Service — 通訊API可讓您建立、組合及提供以品牌為導向的個人化通訊，例如商業信函、檔案、對帳單、理賠處理信函、福利通知、理賠處理信函、每月帳單和歡迎套件。 您可以使用通信API將模板(XFA或PDF)與客戶資料結合，以PDF、PS、PCL、DPL、IPL和ZPL格式生成文檔。

假設您有一或多個範本，以及每個範本的多個XML資料記錄。 您可以使用通信API為每條記錄生成打印文檔。 <!-- You can also combine the records into a single document. --> 結果是非互動式PDF檔案。 非互動式PDF檔案不會讓使用者在其欄位中輸入資料。

Formsas a Cloud Service — 通訊提供隨選和批次API（非同步API），以產生排程的檔案：

* 同步API適用於隨需、低延遲和單記錄檔案產生使用案例。 這些API更適合使用者動作的使用案例。 例如，在用戶填寫表單後生成文檔。

* 批次API（非同步API）適用於排程的高吞吐量多檔案產生使用案例。 這些API會以批次產生檔案。 例如，每月生成電話賬單、信用卡對帳單和福利對帳單。

## 使用同步操作 {#batch-operations}

同步操作是以線性方式生成文檔的過程。 這些API會分類為單租用戶API和多租用戶API:

### 單租用戶API

* 檔案產生API
* 檔案操作API

<!-- 
### Multi-tenant APIs

* Document utility APIs -->


### 驗證單一租用戶API

單租用戶API操作支援兩種驗證類型：

* **基本驗證**:基本驗證是內建在HTTP通訊協定中的簡單驗證方案。 用戶端會以Authorization標題傳送HTTP要求，該標題包含Basic一字，後面接著空格和base64編碼字串username:password。 例如，若要以管理員/管理員身分授權用戶端傳送基本 [base64編碼字串使用者名稱]: [base64編碼字串密碼].

* **基於令牌的驗證：** 基於令牌的驗證使用訪問令牌（承載驗證令牌）來請求Experience Manageras a Cloud Service。 AEM Formsas a Cloud Service提供API，以安全地擷取存取權杖。 若要擷取並使用Token來驗證請求：

   1. [從開發人員控制台檢索Experience Manageras a Cloud Service憑據](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).
   1. [在您的環境中安裝Experience Manageras a Cloud Service憑證](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html). (應用程式伺服器、Web伺服器或其他非AEM伺服器)，設定為傳送要求給雲端服務（進行呼叫）。
   1. [產生JWT代號，並與Adobe IMS API交換以取得存取代號](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).
   1. 以存取權杖作為承載驗證權杖，執行Experience ManagerAPI。
   1. [在Experience Manager環境中為技術帳戶使用者設定適當的權限](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=en#configure-access-in-aem).

   >[!NOTE]
   >
   >Adobe建議在生產環境中使用代號式驗證。

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
1. Tap **[!UICONTROL Create new project]**. A screen to get started with your new project appears. Tap **[!UICONTROL Add API]**. A screen with list of all the APIs enabled for your account appears.
1. Select **[!UICONTROL AEM Forms - Communications]** and tap **[!UICONTROL Next]**. A screen to configure the API appears.
1. Select **[!UICONTROL OPTION 1 Generate a key pair]** and tap **[!UICONTROL Generate keypair]**. It creates and downloads the configuration file. The downloaded configuration file contains all your app settings, along with the only copy of your private key. Adobe does not record your private key, make sure to securely store the downloaded file. Tap **[!UICONTROL Next]**.
1. Select **[!UICONTROL Integrations - Cloud Service]** and tap **[!UICONTROL Save configured API]**. Tap **[!UICONTROL Service Account (JWT)]** to view the API Key, Client Secret, and other information required to access the APIs. You set to use the token to access the APIs.

#### Programmatically generate and use an access token

To programmatically generate an access token, generate a JSON Web Token (JWT) and exchange it with the Adobe Identity Management Service (IMS) for an access token.

Use the following keys, referred to as claims, to construct JWT JSON object:


* `exp`- the requested expiration of the access token, expressed as a number of seconds since January 1, 1970 GMT. For most use cases, this is a relatively small value. For example, 5 minutes, for five minutes from now, this value should be 1670923791.
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

### （僅適用於檔案產生API）設定資產和權限

若要使用同步API，需要下列項目：

* 具有Experience Manager管理員權限的用戶
* 將範本和其他資產上傳至您的Experience Manager FormsCloud Service例項

### （僅適用於檔案產生API）將範本和其他資產上傳至您的Experience Manager例項

組織通常有多個範本。 例如，信用卡報表、福利報表和報銷申請各一個模板。 將所有這類XDP和PDF範本上傳至您的Experience Manager執行個體。 上傳範本：

1. 開啟您的Experience Manager例項。
1. 前往Forms > Forms和檔案
1. 按一下「建立」>「資料夾」並建立資料夾。 開啟資料夾。
1. 按一下「建立>檔案上傳」並上傳範本。

### 叫用API

此 [API參考檔案](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/) 提供API所提供所有參數、驗證方法和各種服務的詳細資訊。 API參考檔案也提供.yaml格式的API定義檔案。 您可以下載.yaml檔案並將其上傳至 [Postman](https://www.postman.com/) 來檢查API的功能。

>[!VIDEO](https://video.tv.adobe.com/v/335771)

>[!NOTE]
>
>只有表單使用者群組的成員才能存取通訊API。
