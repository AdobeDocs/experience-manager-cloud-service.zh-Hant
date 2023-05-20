---
title: AEM Formsas a Cloud Service — 通信
description: 自動將資料與 XDP 和 PDF 範本合併，或產生 PCL、ZPL 和 PostScript 格式的輸出
exl-id: 9fa9959e-b4f2-43ac-9015-07f57485699f
source-git-commit: 33e59ce272223e081710294a2e2508edb92eba52
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 7%

---


# 使用同步處理 {#sync-processing-introduction}

Formsas a Cloud Service — 通信API允許您建立、匯編和提供面向品牌的個性化通信，如業務信函、文檔、報表、理賠信函、利益通知、理賠信函、每月帳單和歡迎套件。 您可以使用Communications API將模板(XFA或PDF)與客戶資料組合，以PDF、PS、PCL、DPL、IPL和ZPL格式生成文檔。

請考慮一個方案，其中每個模板有一個或多個模板和多個XML資料記錄。 可以使用Communications API為每條記錄生成打印文檔。 <!-- You can also combine the records into a single document. --> 結果是非互動式PDF文檔。 非互動式PDF文檔不允許用戶在其欄位中輸入資料。

Formsas a Cloud Service — 通信提供按需和批處理API（非同步API），用於計畫文檔生成：

* 同步API適用於按需、低延遲和單記錄文檔生成使用情形。 這些 API 更適合根據使用者動作的使用案例。例如，在用戶填寫表單後生成文檔。

* 批處理API（非同步API）適用於計畫的高吞吐量多文檔生成使用情形。 這些 API 批次產生文件。例如，每月產生的電話帳單、信用卡報表和福利報表。

## 使用同步操作 {#batch-operations}

同步操作是以線性方式生成文檔的過程。 這些API被分類為單租戶API和多租戶API:

### 單租戶API

* 文檔生成API
* 文檔處理API

<!-- 
### Multi-tenant APIs

* Document utility APIs -->


### 驗證單租戶API

單租戶API操作支援兩種身份驗證類型：

* **基本身份驗證**:基本身份驗證是內置在HTTP協定中的簡單身份驗證方案。 客戶端發送HTTP請求，其Authorization標頭包含Basic後跟空格和base64編碼的字串username:password。 例如，要授權為admin/admin ，客戶端將發送基本 [base64編碼的字串用戶名]: [base64編碼的字串密碼]。

* **基於令牌的身份驗證：** 基於令牌的Experience Manager使用訪問令牌（承載驗證令牌）來請求as a Cloud Service。 AEM Formsas a Cloud Service提供API以安全地檢索訪問令牌。 要檢索並使用令牌來驗證請求，請執行以下操作：

   1. [從開發人員控制台檢索Experience Manageras a Cloud Service憑據](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html)。
   1. [在Experience Manager上安裝as a Cloud Service憑據](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html)。 (應用程式伺服器、Web伺服器或其AEM他非伺服器)，配置為向雲服務發送請求。
   1. [生成JWT令牌，並與Adobe IMS API交換該令牌以獲取訪問令牌](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html)。
   1. 使用訪問令牌作為承載身份驗證令牌運行Experience ManagerAPI。
   1. [在Experience Manager環境中為技術帳戶用戶設定適當的權限](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=en#configure-access-in-aem)。

   >[!NOTE]
   >
   >Adobe建議在生產環境中使用基於令牌的身份驗證。

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

### （僅適用於文檔生成API）配置資產和權限

要使用同步API，需要執行以下操作：

* 具有Experience Manager管理員權限的用戶
* 將模板和其他資產上載到您的Experience Manager FormsCloud Service實例

### （僅用於文檔生成API）將模板和其他資產上載到您的Experience Manager實例

組織通常具有多個模板。 例如，信用卡對帳單、福利對帳單和索賠申請各有一個模板。 將所有此類XDP和PDF模板上載到您的Experience Manager實例。 要上載模板，請執行以下操作：

1. 開啟Experience Manager實例。
1. 轉到Forms>Forms和文檔
1. 按一下「建立」>「資料夾」並建立資料夾。 開啟資料夾。
1. 按一下「建立」(Create)>「檔案上載」(File Upload)並上載模板。

### 調用API

的 [API參考文檔](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/) 提供了有關API提供的所有參數、驗證方法和各種服務的詳細資訊。 API參考文檔還提供.yaml格式的API定義檔案。 您可以下載.yaml檔案並將其上載到 [Postman](https://www.postman.com/) 檢查API的功能。

>[!VIDEO](https://video.tv.adobe.com/v/335771)

>[!NOTE]
>
>只有表單用戶組的成員才能訪問通信API。
