---
title: AEM Formsas a Cloud Service — 通訊
description: 自動將資料與XDP和PDF模板合併，或以PCL、ZPL和PostScript格式生成輸出
exl-id: 9fa9959e-b4f2-43ac-9015-07f57485699f
source-git-commit: 20e54ff697c0dc7ab9faa504d9f9e0e6ee585464
workflow-type: tm+mt
source-wordcount: '1203'
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

### 多租用戶API

* 檔案公用程式API

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

### 驗證多租用戶API

#### 驗證標題

對Cloud Manager API發出的每個傳入HTTP API呼叫都必須包含以下三個標題：

* `x-api-key`
* `x-gw-ims-org-id`
* `Authorization`

應在 `x-api-key` 和 `x-gw-ims-org-id` 標題會顯示在「認證詳細資訊」畫面中的 [Adobe Developer Console](https://developer.adobe.com/console). 的值 `x-api-key` header是用戶端ID和 `x-gw-ims-org-id` header是組織ID。

#### 設定Adobe Developer主控台以產生存取權杖

若要設定驗證API，請在Adobe Developer Console中建立專案，並將通訊API新增至Adobe Developer Console上的專案。 整合會產生API金鑰、用戶端密碼、裝載(JWT):

1. 請連絡您的Adobe Developer Console管理員。 要求管理員新增為開發人員。
1. 登入 `https://developer.adobe.com/console/`. 使用管理員已布建的開發人員帳戶登入Adobe Developer Console。
1. 從右上角選取您的組織。 如果您不清楚自己的組織為何，請聯絡您的管理員。
1. 點選 **[!UICONTROL 建立新專案]**. 隨即顯示開始使用新專案的畫面。 點選 **[!UICONTROL 新增API]**. 畫面會顯示為您的帳戶啟用所有API的清單。
1. 選擇 **[!UICONTROL AEM Forms — 通訊]** 點選 **[!UICONTROL 下一個]**. 畫面隨即顯示設定API的畫面。
1. 選擇 **[!UICONTROL 選項1生成密鑰對]** 點選 **[!UICONTROL 產生鍵對]**. 它會建立及下載設定檔案。 下載的組態檔包含您的所有應用程式設定，以及唯一的私密金鑰復本。 Adobe不會記錄您的私密金鑰，請務必安全地儲存下載的檔案。 點選 **[!UICONTROL 下一個]**.
1. 選擇 **[!UICONTROL 整合 — Cloud Service]** 點選 **[!UICONTROL 儲存已設定的API]**. 點選 **[!UICONTROL 服務帳戶(JWT)]** 檢視API金鑰、用戶端密碼和存取API所需的其他資訊。 您設為使用Token來存取API。

#### 以程式設計方式產生和使用存取權杖

若要以程式設計方式產生存取權杖，請產生JSON網頁權杖(JWT)，並與AdobeIdentity Management服務(IMS)交換以取得存取權杖。

使用下列索引鍵（稱為聲明）來建構JWT JSON物件：

* `exp` — 要求的存取權杖過期時間，以自1970年1月1日起的秒數表示。 對於大多數使用案例而言，這是相對較小的值。 例如，5分鐘，若從現在開始計算，則此值應為1670923791。
* `iss` - Adobe Developer Console專案中的組織ID，格式為org_ident@AdobeOrg。
* `sub`  — 來自Adobe Developer主控台整合的技術帳戶ID，格式為：id@techacct.adobe.com。
* `aud`  — 在Adobe Developer主控台整合的前端加上 `https://ims-na1.adobelogin.com/c/`.
* `https://ims-na1-stg1.adobelogin.com/s/ent_aemforms_docprocessing`  — 設為常值 `true`

然後，此JSON物件必須使用專案的私密金鑰進行base64編碼和簽署。 最後，在POST請求的正文中傳送編碼值至 `https://ims-na1.adobelogin.com/ims/exchange/jwt` 以及專案的用戶端ID和用戶端密碼。

##### 範例

```JSON
    ========================= REQUEST ==========================
    POST https://ims-na1.adobelogin.com/ims/exchange/jwt
    -------------------------- body ----------------------------
    client_id={myClientId}&client_secret={myClientSecret}&jwt_token={myJSONWebToken}
    ------------------------- headers --------------------------
    Content-Type: application/x-www-form-urlencoded
    Cache-Control: no-cache
```

#### JWT的語言支援

雖然可以在自訂程式碼中執行整個JWT產生和交換程式，但使用較高層級的程式庫來執行更常見的作法。 許多這類程式庫會列於 [Adobe I/OJWT檔案](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/).

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
