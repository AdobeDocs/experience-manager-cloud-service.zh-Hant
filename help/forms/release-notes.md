---
title: '[!DNL AEM Forms] as a Cloud Service發行說明'
description: '[!DNL AEM Forms] as a Cloud Service發行說明'
exl-id: 35950b81-6e45-4a75-bd27-8c28fd68e42e
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '2024'
ht-degree: 2%

---


# [!DNL Experience Manager Forms] as a Cloud Service發行說明 {#overview}

Adobe Experience Manager [!DNL AEM Forms] as a Cloud Service不斷改進。 如欲瞭解最新發展，請定期造訪此頁面。 此頁面內含下列資訊：

- 新功能
- 改善功能
- 發行前功能
- 測試版功能
- 錯誤修正
- 已棄用功能
- 特殊說明
- 未來變更計劃

>[!NOTE]
>
>如需其他AEMas a Cloud Service發行元件的發行說明，請參閱 [最新發行說明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=zh-Hant).

## 2021.10.0 {#sep-2021-10-0}

### 新增功能 [!DNL Forms] {#what-is-new-forms-oct-2021}

- **適用性Forms**:您現在可以透過Adobe Analytics for Adaptive Forms，擷取及追蹤登入與非登入（匿名）的行為，以收集一般使用者分析。 它有助於根據資料做出明智的決策，以改善一般使用者體驗。

### 中提供的新功能 [!DNL Forms] 預發行管道 {#prerelease-features-forms-oct-2021}

- **將AEM工作流程資料外部化，以安全處理**:您可以將包含敏感個人資料(SPD)元素的處理中AEM工作流程資料(AEM工作流程變數資料)儲存在客戶管理的存放庫中，以進行安全處理。 資料元素和工作流程變數不會儲存在AEM存放庫中，並會在處理工作流程時，從客戶管理的存放庫隨選擷取。

### 測試版功能 [!DNL Forms] {#sep-what-is-new-forms-oct-prerelease}

- **[!DNL AEM Forms as a Cloud Service - Communications]**: [通訊API](aem-forms-cloud-service-communications.md) 幫助您結合模板和XML資料，以生成各種格式的打印文檔。 此服務可讓您以同步和批次模式產生檔案。 API可讓您建立應用程式，以便您：

   - 使用XML資料填入範本檔案(PDF和XDP)，以產生檔案。
   - 以各種格式生成輸出表單，包括非互動式PDF打印流。

您可以寫入 [!DNL formscsbeta@adobe.com] 註冊測試版計畫。

## 2021.9.0 {#sep-2021-09-0}

### 新增功能 [!DNL Forms] {#what-is-new-forms-sep-2021}

- **在適用性表單中使用Adobe Sign角色**:Adobe Sign（適用於業務和企業服務層級）可以選擇除簽署者外，擴展協定收件者的角色，以更符合其工作流程需求。 您現在可以 [讓每個合約收件者都能在適用性表單中設定其角色](working-with-adobe-sign.md#addsignerstoanadaptiveform)，預設角色為簽署者。

- **適用性Forms**:您現在可以擷取 [透過Adobe Analytics追蹤一般使用者行為](integrate-aem-forms-with-adobe-analytics.md) 以收集一般使用者分析。 它有助於根據資料做出明智的決策，以改善一般使用者體驗。

- **輕鬆連接AEM Forms與Microsoft Dynamics和Salesforce**:此服務提供Microsoft Dynamics和Salesforce的現成可用資料來源設定和資料模型，讓 [開發人員可更快更輕鬆地將Microsoft Dynamics和Salesforce設定為最適化表單的資料來源](configure-msdynamics-salesforce.md).

- **使用DocuSign對最適化表單進行電子簽署：** [您可以使用DocuSign對最適化表單進行電子簽署](integrate-docusign-adaptive-forms.md). 此服務提供自訂提交動作，以搭配最適化表單使用DocuSign。

### 測試版功能 [!DNL Forms] {#sep-what-is-new-forms-prerelease}

- **統一儲存連接器：** 使用Unified Storage Connector將客戶管理的儲存庫中的處理中資料外部化。 例如，您可以將包含敏感個人資料(SPD)的處理中AEM工作流程資料(AEM工作流程變數資料)儲存在客戶管理的存放庫中。

   <!--* Enable Forms Portal’s save and resume functionality and store adaptive forms drafts in a customer-managed data repository.-->

- **[!DNL AEM Forms as a Cloud Service - Communications]**: [通訊API](aem-forms-cloud-service-communications.md) 幫助您結合XDP模板和XML資料，以生成各種格式的打印文檔。 此服務可讓您以同步模式產生檔案。 API可讓您建立應用程式，以便您：
   - 使用XML資料填入範本檔案，以產生檔案。
   - 以各種格式生成輸出表單，包括非互動式PDF打印流。
   - 從XFA表單PDF和Adobe Acrobat表單產生列印PDF檔案。

您可以寫入 [!DNL formscsbeta@adobe.com] 註冊測試版計畫。

### 限制 {#limitations}

- Adobe Analytics只能追蹤已驗證使用者的表單量度。

<!--

### New features available in [!DNL Forms] prerelease channel {#prerelease-features-forms-sep-2021}

* **Forms Portal:**  In a typical forms-centric portal deployment scenario, forms development and portal development are two disjoint activities. While Form Designers design and store forms in a repository, Web Developers create a web application to list forms and handle submission of forms. Forms are copied over to the web tier as there is no communication between the forms repository and the web application.

  Such scenarios often result in management issues and production delays. For example, if there is a newer version of a form available in the repository, you need to replace the form on the web tier, modify the web application, and redeploy the form on the public site. Redeploying the web application might cause some server downtime. Typically, the server downtime is a planned activity and therefore the changes cannot be pushed to the public site instantaneously.

  AEM Forms provides portal components that reduce management overheads and production delays. The components equip Web Developers to create and customize a forms portal on websites authored using Adobe Experience Manager (AEM). The form portal components allow you to add the following functionality:

  * List forms in customized layouts. Out of the box, List view and Card view are provided.

  * List published adaptive forms on an AEM Sites page.

  * Enable searching of forms based on a various criteria, such as form properties, metadata, and tags.

  * Lists drafts and submissions related to Adaptive Form created by end user.

  -->

## 2021.8.0 {#aug-2021-08-0}

### 新增功能 [!DNL Forms] {#what-is-new-forms-aug-2021}

<!-- * Automated Forms Conversion service can [convert PDF Forms in Italian and Portuguese language](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) to Adaptive Forms. -->

- AEMFormsas a Cloud Service的原型專案現在包含 [Microsoft Dynamics和Salesforce的表單資料模型](setup-local-development-environment.md).

- **基於Acroform的記錄文檔**:AEM Formsas a Cloud Service支援使用 [Adobe Acrobat表單PDF(AcroformPDF)](generate-document-of-record-for-non-xfa-based-adaptive-forms.md) 作為記錄檔的範本，而非以XFA為基礎的表單範本。

- **Microsoft Azure資料儲存連接器**:您現在可以 [將表單資料模型連接到Microsoft Azure Storage](configure-azure-storage.md). 它可讓您將最適化表單資料擷取並儲存至Microsoft Azure Storage as a BLOB。

### 測試版功能 [!DNL Forms] {#aug-what-is-new-forms-prerelease}

- **統一儲存連接器：** 使用Unified Storage Connector將客戶管理的儲存庫中的處理中資料外部化。 例如，您可以

   - 啟用Forms Portal的儲存和繼續功能，並將最適化表單草稿儲存在客戶管理的資料存放庫中。
   - 儲存在客戶管理存放庫中包含敏感個人資料(SPD)的AEM工作流程資料(AEM工作流程變數資料)。

- **[!DNL AEM Forms as a Cloud Service - Communications]**: [通訊API](aem-forms-cloud-service-communications.md) 幫助您結合XDP模板和XML資料，以生成各種格式的打印文檔。 此服務可讓您以同步模式產生檔案。 API可讓您建立應用程式，以便您：
   - 使用XML資料填入範本檔案，以產生檔案。
   - 以各種格式生成輸出表單，包括非互動式PDF打印流。
   - 從XFA表單PDF和Adobe Acrobat表單產生列印PDF檔案。

您可以寫入 [!DNL formscsbeta@adobe.com] 註冊測試版計畫。

### 中提供的新功能 [!DNL Forms] 預發行管道 {#prerelease-features-forms-aug-2021}

- **在適用性表單中使用Adobe Sign角色**:Adobe Sign（適用於業務和企業服務層級）可以選擇除簽署者外，擴展協定收件者的角色，以更符合其工作流程需求。 您現在可以 [讓每個合約收件者都能在適用性表單中設定其角色](working-with-adobe-sign.md#addsignerstoanadaptiveform)，預設角色為簽署者。

- **適用性Forms**:您現在可以透過Adobe Analytics for Adaptive Forms擷取及追蹤一般使用者行為，以收集一般使用者分析。 它有助於根據資料做出明智的決策，以改善一般使用者體驗。

- **輕鬆連接AEM Forms與Microsoft Dynamics和Salesforce**:此服務提供Microsoft Dynamics和Salesforce的現成可用資料來源設定和資料模型，讓 [開發人員可更快更輕鬆地將Microsoft Dynamics和Salesforce設定為最適化表單的資料來源](configure-msdynamics-salesforce.md).

## 2021.7.0 {#july-2021-07-0}

### 新增功能 [!DNL Forms] {#july-what-is-new-forms}

- 您現在可以使用Automated forms conversion服務 [轉換法文、德文和西班牙文PDF forms](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) 最適化表單。
- 新增個別面板至範本編輯器，以顯示與最適化表單元件相關的錯誤。 它有助於在單一位置整合所有最適化表單錯誤，並縮短解析時間。

### 中提供的新功能 [!DNL Forms] 預發行管道 {#july-prerelease-features-forms}

- **基於Acroform的記錄文檔**:您也可以 [使用Adobe Acrobat表單PDF(AcroformPDF)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) 作為記錄檔的範本，而非以XFA為基礎的表單範本。

- **Microsoft Azure資料儲存連接器**:您現在可以 [將表單資料模型連接到Microsoft Azure Storage](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html). 它可讓您將最適化表單資料擷取並儲存至Microsoft Azure Storage as a BLOB。

- **變數資料外部化程式**:您可以將AEM工作流程變數的資料儲存在您的組織所管理的外部儲存系統上。

### 測試版功能 [!DNL Forms] {#july-what-is-new-forms-prerelease}

- **[!DNL AEM Forms as a Cloud Service - Communications]**: [通訊API](aem-forms-cloud-service-communications.md) 幫助您結合XDP模板和XML資料，以生成各種格式的打印文檔。 此服務可讓您以同步模式產生檔案。 API可讓您建立應用程式，以便您：
   - 使用XML資料填入範本檔案，以產生檔案。
   - 以各種格式生成輸出表單，包括非互動式PDF打印流。
   - 從XFA表單PDF和Adobe Acrobat表單產生列印PDF檔案。

## 2021.6.0 {#july-2021-06-0}

### 新增功能 [!DNL Forms] {#june-what-is-new-forms}

- 新增篩選AEM收件匣中自訂欄的功能。
- 新增使用最適化表單編輯器的主題編輯器和樣式層來設定驗證碼元件樣式的功能。
- 已改善自動偵測來源PDF forms中邏輯區段並將其轉換為相應最適化表單面板的速度和準確度。
- 新增移動動作，可將PDF或XDP檔案從一個資料夾移至另一個資料夾。

### 測試版功能 [!DNL Forms] {#june-what-is-new-forms-prerelease}

- **[!DNL AEM Forms as a Cloud Service - Communications]**:通訊API可協助您結合XDP範本和XML資料，以產生各種格式的列印檔案。 此服務可讓您以同步模式產生檔案。 API可讓您建立應用程式，以便您：

   - 使用XML資料填入範本檔案，以產生最終表單檔案。
   - 以各種格式生成輸出表單，包括非互動式PDF打印流。
   - 從XFA表單PDF和Adobe Acrobat表單(AcroForm)產生列印PDF。

- **變數資料外部化程式**:您可以將AEM工作流程變數的資料儲存在您的組織所管理的外部儲存系統上。

您可以寫入 [!DNL formscsbeta@adobe.com] 註冊測試版計畫。

### 修正的錯誤 [!DNL Forms] {#june-forms-bugs-fixed}

- 在透過表單資料模型(FDM)將資料提交至後端服務之前驗證欄位時，驗證會成功，但表單資料模型服務無法叫用後期驗證。
- 當您從Apple iOS裝置提交包含標準HTML上傳欄位的表單時，有時不會傳送檔案內容，而會在另一端收到0位元組檔案。 Apple iOS 15.1已修正問題。

## 2021.5.0 {#may-2021-05-0}

## [!DNL Adobe Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### 新增功能 [!DNL Forms] {#may-what-is-new-forms}

- **內容說明**:新增適用性表單編輯器、範本編輯器和主題編輯器的內容說明，協助作者更清楚了解編輯器的各種功能。
- **屬性瀏覽器中的錯誤訊息**:已針對適用性Forms屬性瀏覽器中的每個屬性新增錯誤訊息。 這些訊息有助於了解欄位的允許值。

### 即將推出的測試版功能 [!DNL Forms] {#may-what-is-new-forms-prerelease}

輸出雲端服務：輸出服務可協助您結合XDP範本和XML資料，以產生各種格式的列印檔案。 此服務可讓您以同步和非同步批次模式產生檔案。 通過輸出服務，您可以建立應用程式，以便您：

- 使用XML資料填入範本檔案，以產生最終表單檔案。
- 以各種格式生成輸出表單，包括非互動式PDF打印流。
- 從XFA表單PDF產生列印PDF。

您可以寫信到formscsbeta@adobe.com註冊測試版計畫。

### 修正的錯誤 [!DNL Forms] {#may-forms-bugs-fixed}

- 在AEM Forms工作流程的「指派任務」步驟中，當您以珊瑚圖示取代動作按鈕的預設圖示時，工作流程會停止運作並記錄例外狀況。 使用預設圖示時，工作流程會如預期般執行。
- 在版面層中，當您變更欄數時，請開啟編輯層，並拖曳面板中的某些元件，適用性表單編輯器的內容區域會開始出現方形藍色方塊，而編輯器會停止回應。
- 與提供適用性或外部資產的URL相關的規則編輯器選項的錯誤訊息太長，且不方便使用。

## 2021.4.0 {#april-2021-04-0}

### 新增功能 [!DNL Forms] {#april-what-is-new-forms}

- **在啟用Adobe Sign的適用性Forms中使用政府ID身分驗證方法**

   Adobe Sign的政府ID程式採用進階的機器學習演算法，讓全球公司能夠確保收件者身分的高品質驗證。 現在，您可以在啟用Adobe Sign的適用性Forms中使用政府ID身分驗證方法。

   政府ID是進階身分驗證方法，可指示收件者 [上傳政府頒發的身份證件（駕照、國家身份證、護照）的影像](https://helpx.adobe.com/in/sign/using/adobesign-authentication-government-id.html)，然後評估該檔案以確保其真實。

- **支援非同步最適化表單提交使用表單內簽署體驗**

   您現在可以使用表單內簽署體驗，以非同步最適化表單提交。 您也可以將最適化表單嵌入 [!DNL Experience Manager Sites] 頁面，並使用表單內簽署體驗來提交最適化表單。

- **支援在為「指派任務」步驟預填適用性表單時使用變數指定附件**

   為「指派任務」步驟預填適用性表單時，您現在可以使用檔案類型變數來為適用性表單選取輸入附件。

- **支援使用常值選項來設定JSON類型變數的值**

   您可以在AEM工作流程的設定變數步驟中使用文字選項來設定JSON類型變數的值。 文字選項可讓您以字串的形式指定JSON。

- **使用本地開發環境建立記錄文檔(DoR)**

   您可以在Cloud Service例項和AEM Formsas a Cloud ServiceSDK（本機開發環境）上使用XDP作為記錄檔案範本。 過去，支援僅限於Cloud Service例項。

### 中的錯誤修正 [!DNL Forms] {#april-bug-fixes-forms}

- 將配置為不生成記錄文檔的適用性表單提交到配置為生成記錄文檔的AEM工作流時，不會顯示錯誤消息，且任務無法提交。
