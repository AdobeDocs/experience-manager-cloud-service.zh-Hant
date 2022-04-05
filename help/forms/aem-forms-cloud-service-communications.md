---
title: AEM Formsas a Cloud Service — 通信
description: 自動將資料與XDP和PDF模板合併，或以PCL、ZPL和PostScript格式生成輸出
exl-id: 9fa9959e-b4f2-43ac-9015-07f57485699f
source-git-commit: a3c817dedbf20b21e609ad0e5bfd0d3c4fa9a431
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 0%

---


# 使用同步處理 {#sync-processing-introduction}

通信允許您建立、匯編和提供面向品牌的個性化通信，如業務通信、文檔、報表、理賠信函、利益通知、理賠信函、每月帳單和歡迎套件。 您可以使用Communications API將模板(XFA或PDF)與客戶資料組合，以PDF、PS、PCL、DPL、IPL和ZPL格式生成文檔。

請考慮一個方案，其中每個模板有一個或多個模板和多個XML資料記錄。 可以使用Communications API為每條記錄生成打印文檔。 <!-- You can also combine the records into a single document. --> 結果是非互動式PDF文檔。 非互動式PDF文檔不允許用戶在其欄位中輸入資料。


通信為按需和計畫文檔生成提供了API。 您可以將同步API用於按需API，而將批處理API（非同步API）用於計畫文檔生成：

* 同步API適用於按需、低延遲和單記錄文檔生成使用情形。 這些API更適合基於用戶操作的使用案例。 例如，在用戶填寫表單後生成文檔。

* 批處理API（非同步API）適用於計畫的高吞吐量多文檔生成使用情形。 這些API以批次形式生成文檔。 例如，每月生成電話單、信用卡對帳單和福利對帳單。

## 使用同步操作 {#batch-operations}

同步操作是以線性方式生成文檔的過程。 可以使用單獨的API:

* 從模板生成PDF文檔並將資料合併到該文檔。
* 從XDP檔案或PDF文檔生成PostScript(PS)、打印機命令語言(PCL)、Zebra打印語言(ZPL)文檔。
* 匯編PDF文檔
* 拆卸PDF文檔
* 將文檔轉換為符合PDF/A的文檔
* 驗證符合PDF/A的文檔


### 驗證API調用

同步操作支援兩種身份驗證：

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


### （僅適用於文檔生成API）配置資產和權限

要使用同步API，需要執行以下操作：

* PDF或XDP模板
* [要與模板合併的資料](#form-data)
* 具有Experience Manager管理員權限的用戶
* 將模板和其他資產上載到您的Experience Manager FormsCloud Service實例

### （僅用於文檔生成API）將模板和其他資產上載到您的Experience Manager實例

組織通常具有多個模板。 例如，信用卡對帳單、福利對帳單和索賠申請各有一個模板。 將所有此類XDP和PDF模板上載到您的Experience Manager實例。 要上載模板，請執行以下操作：

1. 開啟Experience Manager實例。
1. 轉到Forms>Forms和文檔
1. 按一下「建立」>「資料夾」並建立資料夾。 開啟資料夾。
1. 按一下「建立」(Create)>「檔案上載」(File Upload)並上載模板。


### 調用API

的 [API參考文檔](https://www.adobe.io/experience-manager-forms-cloud-service-developer-reference/api/sync/#tag/Communications-Services) 提供了有關API提供的所有參數、驗證方法和各種服務的詳細資訊。 API參考文檔還提供.yaml格式的API定義檔案。 您可以下載.yaml檔案並將其上載到郵遞員，以檢查API的功能。

>[!VIDEO](https://video.tv.adobe.com/v/335771)

>[!NOTE]
>
>只有表單用戶組的成員才能訪問通信API。
