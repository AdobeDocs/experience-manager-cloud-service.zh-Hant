---
title: '"[!DNL AEM Forms] as a Cloud Service 發行說明"'
description: '"[!DNL AEM Forms] as a Cloud Service 發行說明"'
exl-id: 35950b81-6e45-4a75-bd27-8c28fd68e42e
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '2024'
ht-degree: 100%

---


# [!DNL Experience Manager Forms] as a Cloud Service 發行說明 {#overview}

Adobe Experience Manager [!DNL AEM Forms] as a Cloud Service 會持續進行改善。如欲瞭解最新發展，請定期造訪此頁面。 此頁面內含下列資訊：

- 新功能
- 改善功能
- 搶鮮版功能
- Beta 版功能
- 錯誤修正
- 已棄用功能
- 特殊說明
- 未來變更計劃

>[!NOTE]
>
>如需所有其他 AEM as a Cloud Service 發行元件的發行說明，請參閱[目前版本注意事項](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=zh-Hant)。

## 2021.10.0 {#sep-2021-10-0}

### [!DNL Forms]的新增功能 {#what-is-new-forms-oct-2021}

- **Analytics for Adaptive Forms**：您現在可以透過 Adobe Analytics for Adaptive Forms 擷取及追蹤已登入和未登入 (匿名) 的行為，以收集一般用戶的深入解析。它可幫助您根據資料來進行明智的決策，以改善一般用戶體驗。

### [!DNL Forms] 搶鮮版頻道中可用的新功能 {#prerelease-features-forms-oct-2021}

- **外部化 AEM Workflow 資料以進行安全處理**：您可以將包含敏感個人資料 (SPD) 元素的程序內 AEM 工作流程資料 (AEM 工作流程變數資料) 儲存在客戶管理的存放庫中，以進行安全處理。資料元素和工作流程變數未儲存在 AEM 存放庫，並在處理工作流程時隨選從客戶管理的存放庫擷取。

### [!DNL Forms]的 Beta 版功能 {#sep-what-is-new-forms-oct-prerelease}

- **[!DNL AEM Forms as a Cloud Service - Communications]**：[通訊 API](aem-forms-cloud-service-communications.md) 可幫助您合併範本和 XML 資料，以產生多種格式的列印文件。 此服務可讓您以同步和批次模式產生文件。 這些 API 可讓您建立以下用途的應用程式：

   - 使用 XML 資料填寫範本檔案 (PDF 和 XDP) 來產生文件。
   - 產生多種格式的輸出表單，包括非互動式 PDF 列印資料流。

您可以寫信寄到 [!DNL formscsbeta@adobe.com] 來註冊 beta 版計劃。

## 2021.9.0 {#sep-2021-09-0}

### [!DNL Forms]的新增功能 {#what-is-new-forms-sep-2021}

- **在最適化表單中使用 Adobe Sign 角色**：適用於商業和企業服務等級的 Adobe Sign 可選擇擴充協議收件者的角色，而不只是簽署者，以便更符合其工作流程需求。您現在可以[啟用每個協議收件者，以便在最適化表單中設定其角色](working-with-adobe-sign.md#addsignerstoanadaptiveform)，並將簽署者設定為預設角色。

- **Analytics for Adaptive Forms**：您現在可以透過 [Adobe Analytics](integrate-aem-forms-with-adobe-analytics.md) for Adaptive Forms 擷取及追蹤一般用戶行為，以收集一般用戶的深入解析。 它可幫助您根據資料來進行明智的決策，以改善一般用戶體驗。

- **輕鬆地將 AEM Forms 連線到 Microsoft Dynamics 和 Salesforce**：此服務會提供 Microsoft Dynamics 和 Salesforce 適用的資料模型，好讓[開發人員更快且更輕鬆地將 Microsoft Dynamics 和 Salesforce 設定為最適化表單的資料來源](configure-msdynamics-salesforce.md)。

- **使用 DocuSign 在最適化表單上進行電子簽名：** [您可以使用 DocuSign 在最適化表單上進行電子簽名](integrate-docusign-adaptive-forms.md)。此服務會提供自訂提供動作，以搭配最適化表單使用 DocuSign。

### [!DNL Forms]的 Beta 版功能 {#sep-what-is-new-forms-prerelease}

- **統一的儲存連接器：**&#x200B;使用統一的儲存連接器可將客戶管理的存放庫中的程序內資料外部化。 例如，您可以將包含敏感個人資料 (SPD) 的程序內 AEM 工作流程資料 (AEM 工作流程變數資料) 儲存在客戶管理的存放庫中。

   <!--* Enable Forms Portal’s save and resume functionality and store adaptive forms drafts in a customer-managed data repository.-->

- **[!DNL AEM Forms as a Cloud Service - Communications]**：[通訊 API](aem-forms-cloud-service-communications.md) 可幫助您合併 XDP 範本和 XML 資料，以產生多種格式的列印文件。 此服務可讓您以同步模式產生文件。 這些 API 可讓您建立以下用途的應用程式：
   - 使用 XML 資料填寫範本檔案來產生文件。
   - 產生多種格式的輸出表單，包括非互動式 PDF 列印資料流。
   - 從 XFA 表格 PDF 和 Adobe Acrobat Form 產生列印 PDF 檔案。

您可以寫信寄到 [!DNL formscsbeta@adobe.com] 來註冊 beta 版計劃。

### 限制 {#limitations}

- Adobe Analytics 可以僅追蹤已驗證身分的用戶的表單量度。

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

### [!DNL Forms]的新增功能 {#what-is-new-forms-aug-2021}

<!-- * Automated Forms Conversion service can [convert PDF Forms in Italian and Portuguese language](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) to Adaptive Forms. -->

- AEM Archetype 專案 (適用於 Forms as a Cloud Service) 現在包含 [Microsoft Dynamics 和 Salesforce 適用的表單資料模型](setup-local-development-environment.md)。

- **根據 Acroform 的記錄文件**：除了根據 PDF 的表單範本以外，AEM Forms as a Cloud Service 也支援使用 [Adobe Acrobat Form PDF (Acroform PDF)](generate-document-of-record-for-non-xfa-based-adaptive-forms.md) 作為 XFA 式表格範本以外的記錄文件範本。

- **Microsoft Azure 資料存放區連接器**：您現在可以[將表單資料模型連接至 Microsoft Azure Storage](configure-azure-storage.md)。它可讓您擷取最適化表單資料，並將該資料作為 BLOB 儲存於 Microsoft Azure Storage。

### [!DNL Forms]的 Beta 版功能 {#aug-what-is-new-forms-prerelease}

- **統一的儲存連接器：**&#x200B;使用統一的儲存連接器可將客戶管理的存放庫中的程序內資料外部化。 例如，您可以

   - 啟用 Forms Portal 的儲存並繼續功能，並將最適化表單草稿儲存在客戶管理的資料存放庫中。
   - 將包含敏感個人資料 (SPD) 的程序內 AEM 工作流程資料 (AEM 工作流程變數資料) 儲存在客戶管理的存放庫中。

- **[!DNL AEM Forms as a Cloud Service - Communications]**：[通訊 API](aem-forms-cloud-service-communications.md) 可幫助您合併 XDP 範本和 XML 資料，以產生多種格式的列印文件。 此服務可讓您以同步模式產生文件。 這些 API 可讓您建立以下用途的應用程式：
   - 使用 XML 資料填寫範本檔案來產生文件。
   - 產生多種格式的輸出表單，包括非互動式 PDF 列印資料流。
   - 從 XFA 表格 PDF 和 Adobe Acrobat Form 產生列印 PDF 檔案。

您可以寫信寄到 [!DNL formscsbeta@adobe.com] 來註冊 beta 版計劃。

### [!DNL Forms] 搶鮮版頻道中可用的新功能 {#prerelease-features-forms-aug-2021}

- **在最適化表單中使用 Adobe Sign 角色**：適用於商業和企業服務等級的 Adobe Sign 可選擇擴充協議收件者的角色，而不只是簽署者，以便更符合其工作流程需求。 您現在可以[啟用每個協議收件者，以便在最適化表單中設定其角色](working-with-adobe-sign.md#addsignerstoanadaptiveform)，並將簽署者設定為預設角色。

- **Analytics for Adaptive Forms**：您現在可以透過 Adobe Analytics for Adaptive Forms 擷取及追蹤一般用戶行為，以收集一般用戶的深入解析。 它可幫助您根據資料來進行明智的決策，以改善一般用戶體驗。

- **輕鬆地將 AEM Forms 連線到 Microsoft Dynamics 和 Salesforce**：此服務會提供 Microsoft Dynamics 和 Salesforce 適用的資料模型，好讓[開發人員更快且更輕鬆地將 Microsoft Dynamics 和 Salesforce 設定為最適化表單的資料來源](configure-msdynamics-salesforce.md)。

## 2021.7.0 {#july-2021-07-0}

### [!DNL Forms]的新增功能 {#july-what-is-new-forms}

- 您現在可以使用 Automated Forms Conversion 服務[將法文、德文和西班牙文 PDF Forms 轉換](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model)成最適化表單。
- 範本編輯器新增個別面板，以顯示與最適化表單元件相關的錯誤。它有助於在同一處整合所有最適化表單錯誤，並縮短解決時間。

### [!DNL Forms] 搶鮮版頻道中可用的新功能 {#july-prerelease-features-forms}

- **Acroform-based Document of Record**：您也可以[使用 Adobe Acrobat Form PDF (Acroform PDF)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) 作為 XFA 式表格範本以外的記錄文件範本。

- **Microsoft Azure 資料存放區連接器**：您現在可以[將表單資料模型連接至 Microsoft Azure Storage](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html)。它可讓您擷取最適化表單資料，並將該資料作為 BLOB 儲存於 Microsoft Azure Storage。

- **Variable Data Externalizer**：您可以將 AEM 工作流程變數的資料儲存於您的組織管理的外部儲存系統。

### [!DNL Forms]的 Beta 版功能 {#july-what-is-new-forms-prerelease}

- **[!DNL AEM Forms as a Cloud Service - Communications]**：[通訊 API](aem-forms-cloud-service-communications.md) 可幫助您合併 XDP 範本和 XML 資料，以產生多種格式的列印文件。 此服務可讓您以同步模式產生文件。 這些 API 可讓您建立以下用途的應用程式：
   - 使用 XML 資料填寫範本檔案來產生文件。
   - 產生多種格式的輸出表單，包括非互動式 PDF 列印資料流。
   - 從 XFA 表格 PDF 和 Adobe Acrobat Form 產生列印 PDF 檔案。

## 2021.6.0 {#july-2021-06-0}

### [!DNL Forms]的新增功能 {#june-what-is-new-forms}

- 新增篩選 AEM 收件匣中自訂欄的功能
- 新增使用最適化表單的主題編輯器和樣式圖層的功能，以設定驗證碼元件的樣式。
- 改善自動偵測來源 PDF 表單中邏輯區段並將這些區段轉換成對應的最適化表單面板的速度和準確性。
- 新增將 PDF 或 XDP 檔案從一個資料夾移至另一個資料夾的移動動作。

### [!DNL Forms]的 Beta 版功能 {#june-what-is-new-forms-prerelease}

- **[!DNL AEM Forms as a Cloud Service - Communications]**：通訊 API 可幫助您合併 XDP 範本和 XML 資料，以產生多種格式的列印文件。此服務可讓您以同步模式產生文件。 這些 API 可讓您建立以下用途的應用程式：

   - 使用 XML 資料填寫範本檔案來產生最終表單文件。
   - 產生多種格式的輸出表單，包括非互動式 PDF 列印資料流。
   - 從 XFA 表單 PDF 和 Adobe Acrobat 表單 (AcroForm) 產生列印 PDF。

- **Variable Data Externalizer**：您可以將 AEM 工作流程變數的資料儲存於您的組織管理的外部儲存系統。

您可以寫信寄到 [!DNL formscsbeta@adobe.com] 來註冊 beta 版計劃。

### 修正在[!DNL Forms]中的錯誤 {#june-forms-bugs-fixed}

- 當欄位在透過表單資料模型 (FDM) 提交資料到後端服務前驗證時，雖然會成功驗證，但表單資料模型無法叫用發佈驗證。
- 從 Apple iOS 裝置提交包含標準 HTML 上傳欄位的表單時，有時不會傳送檔案內容並在另一端收到 0 位元組檔案。Apple iOS 15.1 提供此問題的修正。

## 2021.5.0 {#may-2021-05-0}

## [!DNL Adobe Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms]的新增功能 {#may-what-is-new-forms}

- **關聯式說明**：新增最適化表單編輯器、範本編輯器和主題編輯器的關聯式說明，以協助作者更能了解編輯器的各種功能。
- **屬性瀏覽器中的錯誤訊息**：新增最適化表單屬性瀏覽器中每種屬性的錯誤訊息。這些訊息有助於了解欄位允許的值。

### [!DNL Forms]即將推出的 Beta 版功能 {#may-what-is-new-forms-prerelease}

Output as a Cloud service：Output 服務可幫助您合併 XDP 範本和 XML 資料，以產生多種格式的列印文件。 此服務可讓您以同步和非同步批次模式產生文件。 Output 服務可讓您建立以下用途的應用程式：

- 使用 XML 資料填寫範本檔案來產生最終表單文件。
- 產生多種格式的輸出表單，包括非互動式 PDF 列印資料流。
- 從 XFA 表單 PDF 產生列印 PDF。

您可以寫信寄到 formscsbeta@adobe.com 來註冊 beta 版計劃。

### 修正在[!DNL Forms]中的錯誤 {#may-forms-bugs-fixed}

- 在 AEM Forms 工作流程的指派任務步驟中，當您以珊瑚圖示取代將動作按鈕的預設圖示時，工作流程會停止運作並記錄例外狀況。使用預設圖示時工作流程則會如預期執行。
- 在版面圖層，當您變更欄數、開啟編輯圖層，以及在面板中拖曳某些元件時，藍色正方形方塊會開始在最適化表單編輯器的內容區域中出現，且編輯器開始沒有回應。
- 與提供最適化或外部資產的 URL 關聯的規則編輯器的錯誤訊息過長或不人性化。

## 2021.4.0 {#april-2021-04-0}

### [!DNL Forms]的新增功能 {#april-what-is-new-forms}

- **在啟用 Adobe Sign 的最適化表格中使用政府機關身分證件驗證方法**

   在先進的機器學習演算法的支援下，Adobe Sign 的政府機關身分證件流程讓全球的公司能夠確保對其接收者身分進行高品質的驗證。 現在，您可以在啟用 Adobe Sign 的最適化表格中使用政府機關身分證件驗證方法。

   政府機關身分證件是優質的身分驗證方法，會指示接收者[上傳政府機構簽發的身分證件 (駕照、國民身分證、護照) 的影像](https://helpx.adobe.com/in/sign/using/adobesign-authentication-government-id.html)，然後評估該證件以確保其真實性。

- **支援使用表格中的簽名體驗來提交非同步的最適化表格**

   您現在可以使用表格中的簽名體驗來提交非同步的最適化表格。 您也可以將最適化表格內嵌到 [!DNL Experience Manager Sites] 頁面上，並使用表格中的簽名體驗來提交最適化表格。

- **為指派工作步驟預先填寫最適化表格時，支援使用變數來指定附件**

   為指派工作步驟預先填寫最適化表格時，您現在可以使用文件類型變數為最適化表格選取輸入附件。

- **支援使用常值選項來設定 JSON 類型變數的值**

   您可以在 AEM 工作流程的設定變數步驟中，使用常值選項來設定 JSON 類型變數的值。 此常值選項可讓您使用字串形式來指定 JSON。

- **使用本機開發環境來建立記錄文件 (DoR)**

   您可以在雲端服務實例及 AEM Forms as a Cloud Service SDK (本機開發環境) 中使用 XDP 當做記錄文件範本。 在過去，支援僅限於雲端服務實例。

### [!DNL Forms]中的錯誤修正 {#april-bug-fixes-forms}

- 當將設為不產生記錄文件的最適化表單提交給設為產生記錄文件的 AEM 工作流程，則會顯示無錯誤訊息，且任務無法提交。
