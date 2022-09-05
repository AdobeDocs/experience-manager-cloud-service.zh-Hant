---
title: AEM Formsas a Cloud Service — 通訊
description: 自動將資料與XDP和PDF模板合併，或以PCL、ZPL和PostScript格式生成輸出
exl-id: 9fa9959e-b4f2-43ac-9015-07f57485699f
source-git-commit: 07b9118b8cfc27bc9e2bfa134fbb57c7ae2728ad
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 0%

---


# 使用同步處理 {#sync-processing-introduction}

通信允許您建立、組合和提供面向品牌的個性化通信，如業務通信、文檔、對帳單、理賠處理信函、福利通知、理賠處理信函、每月賬單和歡迎套件。 您可以使用通信API將模板(XFA或PDF)與客戶資料結合，以PDF、PS、PCL、DPL、IPL和ZPL格式生成文檔。

假設您有一或多個範本，以及每個範本的多個XML資料記錄。 您可以使用通信API為每條記錄生成打印文檔。 <!-- You can also combine the records into a single document. --> 結果是非互動式PDF檔案。 非互動式PDF檔案不會讓使用者在其欄位中輸入資料。


通訊提供API，以供隨選和排程的檔案產生。 您可以針對隨需和批次API（非同步API）使用同步API，以排程產生檔案：

* 同步API適用於隨需、低延遲和單記錄檔案產生使用案例。 這些API更適合使用者動作的使用案例。 例如，在用戶填寫表單後生成文檔。

* 批次API（非同步API）適用於排程的高吞吐量多檔案產生使用案例。 這些API會以批次產生檔案。 例如，每月生成電話賬單、信用卡對帳單和福利對帳單。

## 使用同步操作 {#batch-operations}

同步操作是以線性方式生成文檔的過程。 您可以使用個別API:

* 從模板生成PDF文檔並將資料合併到其中。
* 從XDP檔案或PDF文檔生成PostScript(PS)、打印機命令語言(PCL)、Zebra打印語言(ZPL)文檔。
* 匯編PDF文檔
* 拆解PDF文檔
* 將文檔轉換為PDF/A相容文檔
* 驗證PDF/A相容文檔


### 驗證API呼叫

同步操作支援兩種身份驗證：

* **基本驗證**:基本驗證是內建在HTTP通訊協定中的簡單驗證方案。 用戶端會以Authorization標題傳送HTTP要求，該標題包含Basic一字，後面接著空格和base64編碼字串username:password。 例如，若要以管理員/管理員身分授權用戶端傳送基本 [base64編碼字串使用者名稱]: [base64編碼字串密碼].

* **基於令牌的驗證：** 基於令牌的驗證使用訪問令牌（承載驗證令牌）來請求Experience Manageras a Cloud Service。 AEM Formsas a Cloud Service提供API，以安全地擷取存取權杖。 若要擷取並使用Token來驗證請求：

   1. [從開發人員控制台擷取Experience Manageras a Cloud Service憑證](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).
   1. [在您的環境中安裝Experience Manageras a Cloud Service憑證](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html). (應用程式伺服器、Web伺服器或其他非AEM伺服器)，設定為傳送要求給雲端服務（進行呼叫）。
   1. [產生JWT代號，並與Adobe IMS API交換以取得存取代號](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).
   1. 以存取權杖作為承載驗證權杖，執行Experience ManagerAPI。
   1. [在Experience Manager環境中為技術帳戶使用者設定適當的權限](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=en#configure-access-in-aem).

   >[!NOTE]
   >
   >Adobe建議在生產環境中使用代號式驗證。


### （僅適用於檔案產生API）設定資產和權限

若要使用同步API，需要下列項目：

* PDF或XDP範本
* [要與範本合併的資料](#form-data)
* 具有Experience Manager管理員權限的用戶
* 將範本和其他資產上傳至您的Experience Manager FormsCloud Service例項

### （僅適用於檔案產生API）將範本和其他資產上傳至您的Experience Manager例項

組織通常有多個範本。 例如，信用卡報表、福利報表和報銷申請各一個模板。 將所有這類XDP和PDF範本上傳至您的Experience Manager執行個體。 上傳範本：

1. 開啟您的Experience Manager例項。
1. 前往Forms > Forms和檔案
1. 按一下「建立」>「資料夾」並建立資料夾。 開啟資料夾。
1. 按一下「建立>檔案上傳」並上傳範本。


### 叫用API

此 [API參考檔案](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/) 提供API所提供所有參數、驗證方法和各種服務的詳細資訊。 API參考檔案也提供.yaml格式的API定義檔案。 您可以下載.yaml檔案並將其上傳至postman以檢查API的功能。

>[!VIDEO](https://video.tv.adobe.com/v/335771)

>[!NOTE]
>
>只有表單使用者群組的成員才能存取通訊API。
