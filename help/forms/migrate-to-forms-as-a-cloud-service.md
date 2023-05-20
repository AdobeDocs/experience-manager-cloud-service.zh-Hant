---
title: 如何從6.AEM5Forms和6.4AEMForms遷移到 [!DNL AEM Forms] as a Cloud Service環境？
description: 從 [!DNL AEM Forms] （本地和AMS環境）到 [!DNL AEM Forms] as a Cloud Service環境
contentOwner: khsingh
feature: Adaptive Forms
role: User, Developer
level: Intermediate
topic: Migration
exl-id: 090e77ff-62ec-40cb-8263-58720f3b7558
source-git-commit: d9c19d0b567a9a97973c4c4e25e64722da109dbb
workflow-type: tm+mt
source-wordcount: '1335'
ht-degree: 3%

---

# 從 [!DNL AEM Forms] （本地和AMS環境）到 [!DNL AEM Forms] as a Cloud Service  {#Harden-your-AEM-Forms-as-a-Cloud-Service-environment}

您可以從中遷移您的自適應Forms、主題、模板和雲配置 <!-- AEM 6.3 Forms--> OSGiAEM上的Forms6.4 AEMOSGi上的Forms6.5 [!DNL AEM] as a Cloud Service。 在遷移這些資產之前，請使用遷移實用程式將早期版本中使用的格式轉換為 [!DNL AEM] as a Cloud Service。 運行遷移實用程式時，將更新以下資產：

* 自適應Forms的自定義元件
* 自適應Forms模板和主題
* 雲配置
* 代碼編輯器指令碼被轉換為可重用的函式並應用於可視規則。

## 考量事項 {#consideration}

* 該服務僅幫助從 [!DNL AEM Forms] 在OSGi環境中。 從遷移內容 [!DNL AEM Forms] 不支援將JEE連接到Cloud Service環境。

* (僅適用於AEM6.3Forms或舊版本環境，升級到AEM6.4Forms或AEM6.5Forms)基於出廠設定模板和6.3Forms或舊版本中提供的主題的自適應Forms不支援 [!DNL AEM Forms] as a Cloud Service。

* Adobe Experience Manager Formsas a Cloud Service與Adobe Experience Manager6.5Forms(內部部署和Adobe管理服務)環境相比，對現有功能進行了一些顯著的更改。 在繼續遷移到服務之前， [瞭解這些不可記錄的更改](notable-changes.md) 和 [特徵級差](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en#viewing-report) 根據組織需要的功能決定遷移。




<!-- 
## Difference with AEM 6.5 Forms 

| Feature         | Difference with AEM 6.5 Forms    |
|--------------|-----------|
| HTML5 Forms (Mobile Forms)     | The service does not support HTML5 Forms (Mobile Forms). If you render your XDP-based forms as HTML5 Forms, you can continue using the feature on AEM 6.5 Forms. |
| Adaptive Forms     | <li><b>XSD-Based Adaptive Forms:</b> The service does not support HTML5 Forms (Mobile Forms). If you render your XDP-based forms as HTML5 Forms, you can continue using the feature on AEM 6.5 Forms. </li> <li><b> Adaptive Form templates:</b> Use build pipeline and corresponding Git repository of your program to import existing Adaptive Form templates. </li><li><b>Rule editor:</b> AEM Forms as a Cloud Service provides a hardened [Rule editor](rule-editor.md#visual-rule-editor). The code editor is not available on Forms as a Cloud Service. The migration utility helps you migrate your forms that have custom rules (created in code editor). The utility converts such rules into custom functions supported on Forms as a Cloud Service. You can use the reusable functions with Rule editor to continue obtaining results obtained with rule scripts  The `onSubmitError` or `onSubmitSuccess` functions are now available as actions the Rule Editor. </li> <li><b>Drafts and submissions:</b> The service does not retain metadata for drafts and submitted Adaptive Forms. </li> <li><b> Prefill Service:</b> By default, the prefill service merges data with an Adaptive Form at client as opposed to merging data on Server in AEM 6.5 Forms. The feature helps improve the time required to prefill an Adaptive Form. You can always configure to run the merge action on the Adobe Experience Manager Forms Server. </li><li><b>Submit actions:</b> The **Email as PDF** action is not available. The **Email** submit action provide options to send attachments and attach Document of Record (DoR) with email. </li>|
| Form Data Model | <li>Forms data model supports only HTTP and HTTPs endpoints to submit data. </li><li>Forms as a Cloud Service allows to use Microsoft Azure Blob, Microsoft Sharepoint, Microsoft OneDrive, and services supporting general CRUD (Create, Read, Update, and Delete) operations as data stores. The service does not support JDBC connector, Mutual SSL for Rest connector, and x509 certificate-based authentication for SOAP data sources. </li>|
| Automated Forms Conversion Service     | The service does not provide meta-model for Automated Forms Conversion Service. You can [download it from Automated Forms Conversion Service documentation](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model).|
|Configurations|<li>Email support only HTTP and HTTPs protocols, by default. [Contact the support team](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) to enable ports for sending emails and to enable SMTP protocol for your environment. </li> <li>If you use custom bundles, recompile your code with latest version of adobe-aemfd-docmanager before using these bundles with Forms as a Cloud Service.</li> |
| Document Manipulation APIs (Assembler Service)| The service does not support operations dependent on other services or applications: <li>Conversion of documents in a non-PDF format to a PDF format is not supported. For example, Microsoft Word to PDF, Microsoft Excel to PDF, and HTML to PDF are not supported</li><li>Adobe Distiller-based conversions are not supported. For example, PostScript(PS) to PDF</li><li>Forms Service-based conversions are not supported. For example, XDP to PDF Forms.</li><li>The service does not support converting a Signed PDF or Transparent PDF to another PDF format.</li>| -->

## 必備條件 {#prerequisites}

* [啟用Forms — 數字註冊](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/setting-up-program.html?#editing-program) 選項，以及您的FormsCloud Service計畫 [運行管線](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html)。

   ![試執行結果](assets/enable-add-on.png)

* 在Cloud Service環境中，遷移實用程式與用戶映射工具和內容傳輸工具結合使用。 遷移實用程式 [!DNL AEM Forms] 與Cloud Service相容的資產，內容傳輸工具將內容從 [!DNL AEM Forms] 環境 [!DNL AEM] as a Cloud Service環境。 在使用遷移實用程式之前，請瞭解 [移到AEMas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/home.html)。 該過程有兩種工具：
   * [用戶映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration):用戶映射工具可幫助您將用戶與相應的Adobe IMS用戶帳戶進行映射。
   * [內容傳輸工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration):內容傳輸工具可幫助您準備內容並將內容從現有環境傳輸到Cloud Service環境。
* 具有管理員權限的帳戶 [!DNL AEM Forms] as a Cloud Service和本地 [!DNL AEM Forms] 環境。
* 下載並安裝Best Practice Analyzer 、內容傳輸工具，以及 [!DNL AEM Forms] 遷移實用程式 [軟體分發門戶](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)

* 運行 [最佳做法分析器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration) 工具並修復報告的問題。 有關從Adobe Experience Manager Forms遷移到Adobe Experience Manager Formsas a Cloud Service的可能問題，請參見 [FormsAEMas a Cloud Service模式檢測](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en#viewing-report)。


<!-- * Download the latest [compatibility package](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#aem-65-forms-releases) for your [!DNL AEM Forms] version. -->

## 遷移 [!DNL AEM Forms] 資產  {#use-the-migration-utility}

執行以下步驟，使 [!DNL AEM Forms] 與Cloud Service相容的資產，並將其 [!DNL AEM] as a Cloud Service環境。

1. 建立 [克隆](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/correct-method-to-clone-the-aem-environment/qaq-p/363487) 您現有 [!DNL AEM Forms] 環境。

   始終使用克隆的環境運行內容傳輸工具和遷移實用程式。 內容傳輸工具和遷移實用程式對內容和資產做了一些更改。 因此，不要在生產環境中運行內容傳輸工具和遷移實用程式。

1. 使用管理權限登錄到克隆的環境。

1. 運行 [用戶映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration) 將用戶與相應的Adobe IMS用戶帳戶映射。 您需要Adobe IMS用戶帳戶登錄到 [!DNL AEM Forms] as a Cloud Service實例。

1. 下載並安裝 [內容傳輸工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration) 和 [!DNL AEM Forms] as a Cloud Service遷移實用程式 [軟體分發門戶](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) 在克隆的環境中。 可以使用包管AEM理器來安裝工具和實用程式。

1. 導航到 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL 內容遷移]**。

1. 開啟 **[!UICONTROL 為Forms遷移做好準備]** 卡。 瀏覽器顯示五個選項：
   * **[!UICONTROL AEM Forms 資產移轉]**
   * **[!UICONTROL 自適應Forms自定義元件遷移]**
   * **[!UICONTROL 自適應Forms模板遷移]**
   * **[!UICONTROL AEM 表單雲端組態移轉]**
   * **[!UICONTROL 代碼編輯器指令碼遷移]**

1. 使用一個接一個的選項 [!DNL AEM Forms] 與 [!DNL AEM] as a Cloud Service:

   1. 點擊 **[!UICONTROL AEM Forms資產遷移]**，在下一個螢幕中，點擊 **[!UICONTROL 開始遷移]**。 它使Adaptive Forms和主題 [!DNL AEM Forms] 環境相容 [!DNL AEM] as a Cloud Service。

   1. 點擊 **[!UICONTROL 自適應Forms自定義元件遷移]** 在「自定義元件遷移」頁中，按一下 **[!UICONTROL 開始遷移]**。 它使任何為自適應Forms開發的定製元件和元件覆蓋在您的 [!DNL AEM Forms] 環境相容 [!DNL AEM] as a Cloud Service。

   1. 點擊 **[!UICONTROL 自適應Forms模板遷移]** 在「自定義元件遷移」頁中，按一下 **[!UICONTROL 開始遷移]**。 它使/apps或/conf上的Adaptive Form模板與相容，並使用模板編AEM輯器建立 [!DNL AEM] as a Cloud Service。

   1. 點擊 **[!UICONTROL AEM Forms雲配置遷移]** 然後在「配置遷移」頁上，按一下 **[!UICONTROL 開始遷移]**。 它會更新以下Cloud Services並將其移動到新位置：

      * 表單資料模型Cloud Service
      * GooglereCAPTCHACloud Service
      * [!DNL Adobe Sign] 雲端服務
      * Adobe FontsCloud Service
   1. 點擊 **[!UICONTROL 代碼編輯器指令碼遷移]**，指定保存可重用函式的位置，然後點擊**[!UICONTROL 開始遷移]。

   該Cloud Service不支援規則編輯器指令碼。 的 **[!UICONTROL 代碼編輯器指令碼遷移]** 工具將環境中的所有規則指令碼轉換為可重用函式，並將可重用函式應用到適當位置的可視編輯器。 這些可重用功能以客戶端庫的形式保存，並幫助您保持現有功能不變。 該工具自動將生成的可重用函式應用到相應的自適應Forms。

   使用 [包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#contentmanagement) 將可重用函式（客戶端庫）導出到包。

1. [部署](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#deploying-content-packages-via-cloud-manager-and-package-manager) 可重用的函式（客戶端庫）包， [自定義代碼，元件，配置](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html#cloud-manager)，自定義區域設定特定的庫 [!DNL AEM] as a Cloud Service環境。

   <!-- 1. Install the latest [Compatibility Package](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration) to your cloned [!DNL AEM Forms] environment. -->

1. 運行 [內容傳輸工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration)。 在上指定參數時 **[!UICONTROL 建立遷移集]** 框中，指定自適應Forms、主題、模板、表單資料模型、Cloud Services、自定義元件和其他AEM Forms特定資產的路徑 **[!UICONTROL 要包括的路徑]** 的雙曲餘切值。 它添加了指定的 [!DNL AEM Forms] 要遷移的資產。

## AEM Forms特有資產的路徑

* **自適應Forms**:可以在以下位置找到自適應表單 `/content/dam/formsanddocuments/`和/content/forms/af。 例如，對於標題為WKND註冊的自適應表單添加路徑 `/content/dam/formsanddocuments/wknd-registration` 和 `/content/forms/af/wknd-registration`。
* **表單資料模式**:可在以下位置找到所有表單資料模型 `/content/dam/formsanddocuments-fdm`。 比如說， `/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`。

* **客戶端庫**:客戶端庫的預設路徑是 `/etc/clientlibs/fd/theme`。

* **自適應表單模板**:模板的預設路徑是 `/conf/<template folder>`。 例如，對於標題為基本添加路徑的模板 `/conf/ReferenceEditableTemplates/settings/wcm/templates/basic`。

* **自適應表單主題和客戶端庫**:主題的預設路徑是 ` /content/dam/formsanddocuments-themes/` 而客戶端庫的預設路徑為 `/etc/clientlibs/fd/theme`。 例如，對於標題為WKND主題的模板添加路徑 ` /content/dam/formsanddocuments-themes/wkndtheme` 和客戶端庫(位於 `/etc/clientlibs/reference-themes/wkndtheme-3-0`。 您還可以在其它自定義路徑上使用主題和客戶端庫。

* **雲配置**:您可以在以下位置找到雲配置： `/conf/`。 例如，表單資料模型雲配置位於 `/conf/global/settings/cloudconfigs/fdm`。

* **工作流模型**:可以在以下位AEM置找到工作流模型 `/conf/global/settings/workflow/models/`。 例如，對於標題為WKND註冊添加路徑的工作流模型 `/conf/global/settings/workflow/models/wknd-registration`

您可以添加下面列出的頂級資料夾路徑或特定資料夾路徑，如下所述。 它使您能夠同時遷移特定資產和所有資產和表單。

* /content/dam/formsanddocuments-fdm
* /content/dam/formsanddocuments/主題
* /內容/表單/af
* /etc/clientlibs/fd/theme

要遷移工AEM作流模型，請指定以下路徑：

* /conf/global/settings/workflow/models/
* /conf/global/settings/workflow/launcher
* /var/workflow/models
