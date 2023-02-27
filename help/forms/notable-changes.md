---
title: AEM 6.5 Forms與AEM雲端服務之間的變更
description: 您是Experience Manager Forms使用者，且想要升級至Adobe Experience Manager Formsas a Cloud Service? 在升級或移轉至Cloud Service之前，請先了解最顯著的變更。
exl-id: 46fcc1b4-8fd5-40e1-b0fc-d2bc9df3802e
contentOwner: khsingh
source-git-commit: da53f453b0f2def98d92aae0e3e92d13eb748dab
workflow-type: tm+mt
source-wordcount: '1178'
ht-degree: 3%

---

# 現有Adobe Experience Manager 6.5 Forms使用者的重大變更  {#notable-changes-for-existing-AEM-Forms-users}

Adobe Experience Manager Forms as a Cloud Service對現有功能進行了幾項重大變更，比如Adobe Experience Manager Forms On-Premise和 [!DNL Adobe-Managed Service] 環境。 主要差異列於下列：

| 功能 | [!DNL AEM Forms] as a Cloud Service | AEM 6.5 Forms |
|---|---|---|
| 雲端原生架構 | ✅ | ⛌ |
| 根據負載自動縮放 | ✅ | ⛌ |
| 零停機升級 | ✅ | ⛌ |
| 功能轉出頻率 | 雅居利* | 每季 |
| 包含的CDN（內容傳遞網路） | ✅ | ⛌ |
| 優化的拓撲，以實現最大的可復原性和效率 | ✅ | ⛌ |
| 雲端原生開發環境 | ✅ | ⛌ |
| 透過Cloud Manager提供自助服務 | ✅ | ⛌ |
| 通過連續整合和連續傳送(CI/CD)實現自動升級 | ✅ | ⛌ |
|  與 [!DNL Micosoft Power Automate] 整合 | ✅ | ⛌ |
|  與 [!DNL DocuSign] 整合 | ✅ | ⛌ |
| 與Microsoft Dynamics和Salesforce輕鬆連接 | ✅ | ⛌ |
| 與Microsoft Azure資料儲存區輕鬆連線 | ✅ | ⛌ |
| 強化規則編輯器 | ✅ | ⛌ |
| 表單建立精靈 | ✅ | ⛌ |
| 記錄檔案的自訂XCI支援 | ✅ | ⛌ |
| 適用性Forms <sup>1</sup> | ✅ | ✅ |
| 與多個資料來源的資料整合 | ✅ | ✅ |
| 通訊API（檔案服務） <sup>2,3</sup> | ✅ | ✅ |
| automated forms conversion服務 <sup>4</sup> | ✅ | ✅ |
|  與 [!DNL Adobe Sign] 整合 | ✅ | ✅ |
|  與 [!DNL AEM Sites] 整合 | ✅ | ✅ |
|  與 [!DNL Adobe Launch] 整合 | ✅ | ✅ |
|  與 [!DNL Adobe Analytics] 整合 | ✅ | ✅ |
| Forms入口網站 <sup>5</sup> | ✅ | ✅ |
| AEM 工作流程 | ✅ | ✅ |
| 記錄文件 | ✅ | ✅ |
| 隱形驗證碼 | ✅ | ✅ |
| 可重複使用的表單資料模型配置 | ✅ | ✅ |
| 基於Acroform的記錄文檔 | ✅ | ✅ |
| 啟用適用性Adobe Sign的政府ID身分驗證Forms | ✅ | ✅ |
| HTML5 <sup>6</sup> | ⛌ | ✅ |
| 文件安全性 | ⛌ | ✅ |

在繼續提供服務之前，請考慮以下特殊情況：

+++ 1.適應性Forms

* **基於XSD的適用性Forms:** 此服務不支援HTML5 Forms(行動Forms)。 如果您將XDP型表單轉譯為HTML5 Forms，則可繼續使用AEM 6.5 Forms上的功能。 您可以使用XDP模板來設計「要記錄的文檔」模板。 此服務不支援以XFA為基礎的適用性Forms
* **匯入最適化表單範本：** 使用程式的建置管道和對應的Git存放庫，以匯入現有的最適化表單範本。
* **規則編輯器：** AEM Formsas a Cloud Service [規則編輯器](rule-editor.md#visual-rule-editor). Forms as a Cloud Service上無法使用程式碼編輯器。 移轉公用程式可協助您移轉具有自訂規則的表單（在程式碼編輯器中建立）。 此公用程式會將這些規則轉換為Forms as a Cloud Service上支援的自訂函式。 您可以使用可重複使用的函式搭配規則編輯器，繼續取得使用規則指令碼取得的結果。 `onSubmitError` 或 `onSubmitSuccess` 函式現在可作為規則編輯器中的動作使用。
* **草稿和提交：** 服務不會保留草稿和已提交適用性Forms的中繼資料。
* **預填服務：** 預設情況下，預填服務會合併用戶端上的適用性表單資料，而非合併AEM 6.5 Forms中的伺服器上的資料。 此功能有助於縮短預填最適化表單的所需時間。 您一律可以設定在Adobe Experience Manager Forms伺服器上執行合併動作。
* **提交操作：** 此 **以電子郵件方式PDF** 無法使用動作。 此 **電子郵件** 「提交」操作提供了發送附件和附加「記錄文檔(DoR)」和電子郵件的選項。
* **元件**:此服務不支援表單內簽署體驗，也不包含適用性Forms的摘要和驗證元件。



+++


+++ 2.檔案服務：文檔操作API（組合器服務）


該服務不支援依賴於其他服務或應用程式的操作：

* 不支援將非PDF格式的文檔轉換為PDF格式。 例如，不支援Microsoft Word轉PDF、Microsoft Excel轉PDF、HTML轉PDF。 如果文檔為非PDF格式。 使用具有「通信文檔操作API」的文檔之前，將這些文檔轉換為PDF格式。 例如，如果您的檔案為Microsoft Office、HTML、PostScript(PS)、XDP格式，請先將這些檔案轉換為PDF格式，再將這些檔案與PDF檔案搭配使用。
* Adobe不支援以Distiller為基礎的轉換。 例如，將PostScript(PS)PDF
* Forms不支援以服務為基礎的轉換。 例如，從XDP轉換為PDF forms。
* 此服務不支援將已簽名的PDF或透明PDF轉換為其他PDF格式。
* 無法使用Reader擴充功能服務套用使用權。
* 此服務無法將已簽署或透明的PDF檔案轉換為PDF/A格式。

+++


+++ 3.檔案服務：檔案產生API（輸出服務）

在單一API呼叫或批次中，您只能使用一個範本搭配多個DATA XML檔案。 不支援在單一API呼叫中使用多個範本及多個資料檔案。

+++

+++ 4.Automated forms conversion服務

服務不提供Automated forms conversion服務的元模型。 您可以 [從Automated forms conversion服務檔案下載](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model).

+++

+++ 5.Forms門戶

無法立即使用Forms入口網站(OOTB)，且無法提供匿名使用支援。 您可以自訂表單入口網站，為未登入的使用者啟用顯示表單功能。

+++


+++ 6.HTML5Forms(行動Forms)

此服務不支援HTML5 Forms(行動Forms)。 如果您將XDP型表單轉譯為HTML5 Forms，則可繼續使用AEM 6.5 Forms上的功能。

+++


+++ 7.表單資料模型

Forms資料模型僅支援HTTP和HTTP端點來提交資料。 此服務不支援REST連接器的Mutual SSL，以及SOAP資料來源的x509憑證式驗證。 * Formsas a Cloud Service允許將Microsoft Azure Blob、Microsoft Sharepoint、Microsoft OneDrive和支援一般CRUD（建立、讀取、更新和刪除）操作的服務用作資料儲存，支援Open API規範2.0和Open API規範。 此服務也支援JDBC連接器。

+++


+++ 8.開發人員環境

* 雲端原生環境沒有Web主控台(configuration manager)。 您可以使用 [[!DNL AEM Forms] as a Cloud ServiceSDK產生設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart) 和CI/CD管道 [部署配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) 至您的Cloud Service例項。
* 依預設，電子郵件僅支援HTTP和HTTP通訊協定。 [聯絡支援團隊](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) 啟用用於發送電子郵件的埠，並為您的環境啟用SMTP協定。
* 此服務不支援將已簽名的PDF或透明PDF轉換為其他PDF格式。 在搭配Formsas a Cloud Service使用客戶套件組合之前，請使用本地化適用性Forms的最新版adobe-aemfd-docmanager* URL慣例，重新編譯自訂程式碼，現在支援在URL中指定地區設定。 新的URL慣例會啟用快取Dispatcher或CDN上的本地化表單。 在Cloud Service環境中，使用URL格式 `http://host:port/content/forms/af/<afName>.<locale>.html` 請求本地化版本的最適化表單，而非 `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`. Adobe建議使用Dispatcher或CDN快取。 有助於改善預填表單的轉譯速度
* Adobe Experience Manager Forms as a Cloud Service為您的AEM專案帶來許多新功能，並帶來許多可能性。 不過，Adobe Experience Manager Maven專案需進行一些變更，才能與AEM Cloud Service相容。 在高階層，AEM需要將內容和程式碼分離為離散子封裝，以遵循可變和不可變內容之間的分割。 使用 [Repository Modernizer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html) 工具，借由將內容和程式碼分離為獨立套件，以與為Adobe Experience Manager as a Cloud Service定義的專案結構相容，來重新建構現有專案套件。


+++

<!-- 

### HTML5 Forms (Mobile Forms)

The service does not support HTML5 Forms (Mobile Forms). If you render your XDP-based forms as HTML5 Forms, you can continue using the feature on AEM 6.5 Forms.

### Adaptive Forms 

* **XSD-Based Adaptive Forms:** The service does not support HTML5 Forms (Mobile Forms). If you render your XDP-based forms as HTML5 Forms, you can continue using the feature on AEM 6.5 Forms. You can use XDP-template to design a template for Document for Record. The service does not support XFA based Adaptive Forms  
* **Importing Adaptive Form templates:** Use build pipeline and corresponding Git repository of your program to import existing Adaptive Form templates. 
*  **Rule editor:** AEM Forms as a Cloud Service provides a hardened [Rule editor](rule-editor.md#visual-rule-editor). The code editor is not available on Forms as a Cloud Service. The migration utility helps you migrate your forms that have custom rules (created in code editor). The utility converts such rules into custom functions supported on Forms as a Cloud Service. You can use the reusable functions with Rule editor to continue obtaining results obtained with rule scripts  The `onSubmitError` or `onSubmitSuccess` functions are now available as actions the Rule Editor.  
* **Drafts and submissions:** The service does not retain metadata for drafts and submitted Adaptive Forms.  
* **Prefill Service:** By default, the prefill service merges data with an Adaptive Form at client as opposed to merging data on Server in AEM 6.5 Forms. The feature helps improve the time required to prefill an Adaptive Form. You can always configure to run the merge action on the Adobe Experience Manager Forms Server. 
* **Submit actions:** The **Email as PDF** action is not available. The **Email** submit action provide options to send attachments and attach Document of Record (DoR) with email. 
* **Components**:  The service does not support in-form signing experience and does not include the Summary and Verify components for Adaptive Forms.  
* **Forms portal**: Support for anonymous use of Forms portal is not available out of the box (OOTB). You can customize the forms portal to enable displaying forms for non-logged in users.

### Form Data Model

* Forms data model supports only HTTP and HTTPs endpoints to submit data. The service does not support Mutual SSL for REST connector and x509 certificate-based authentication for SOAP data sources. * Forms as a Cloud Service allows to use Microsoft Azure Blob, Microsoft Sharepoint, Microsoft OneDrive, and services supporting general CRUD (Create, Read, Update, and Delete) operations as data stores, both Open API specification 2.0 and Open API specification are supported. The service also provides support for JDBC connector.


### Automated Forms Conversion Service     

The service does not provide meta-model for Automated Forms Conversion Service. You can [download it from Automated Forms Conversion Service documentation](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model).


### Configurations

* Email support only HTTP and HTTPs protocols, by default. [Contact the support team](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) to enable ports for sending emails and to enable SMTP protocol for your environment.  
* If you use custom bundles, recompile your code with latest version of adobe-aemfd-docmanager before using these bundles with Forms as a Cloud Service. 


### Document Services: Document Manipulation APIs (Assembler Service)

The service does not support operations dependent on other services or applications:  

* Conversion of documents in a non-PDF format to a PDF format is not supported. For example, Microsoft Word to PDF, Microsoft Excel to PDF, and HTML to PDF are not supported. If your documents are in a non-PDF format. Convert such documents to PDF format before using those with Communications Document Manipulation APIs. For example, if your documents are in Microsoft Office, HTML, PostScript (PS), XDP format, convert these documents to PDF format before using those with PDF documents. 
* Adobe Distiller-based conversions are not supported. For example, PostScript(PS) to PDF
* Forms Service-based conversions are not supported. For example, XDP to PDF Forms.
* The service does not support converting a Signed PDF or Transparent PDF to another PDF format.
* Applying usage rights using Reader Extensions Service is not available. 
* The service does not provide the ability to convert signed or transparent PDF Documents to PDF/A format. 

### Document Services: Document Generation APIs (Output Service)

* In a single API call or batch, you can use one template with multiple DATA XML files. Using mutiple templates with multiple data files in a single API call is not supported. 

### Other differences

* A cloud-native environment does not have web console (configuration manager). You can use [[!DNL AEM Forms] as a Cloud Service SDK to generate configurations](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart) and CI/CD pipeline to [deploy the configuration](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) to your Cloud Service instance.
* Email support only HTTP and HTTPs protocols, by default. [Contact the support team](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) to enable ports for sending emails and to enable SMTP protocol for your environment.
* The service does not support converting a Signed PDF or Transparent PDF to another PDF format.* Before using your customer bundles with Forms as a Cloud Service, recompile your custom code with the latest version of adobe-aemfd-docmanager* URL convention of localized Adaptive Forms now supports specifying a locale in the URL. New URL convention enables caching localized forms on a Dispatcher or CDN. On Cloud Service environment, use the URL format `http://host:port/content/forms/af/<afName>.<locale>.html` to request a localized version of an Adaptive Form instead of `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`. Adobe recommends using Dispatcher or CDN caching. It helps improve rendering speed of prefilled forms 
* Adobe Experience Manager Forms as a Cloud Service brings many new features and possibilities into your AEM Projects. However, there are some changes required to Adobe Experience Manager Maven projects to be compatible with AEM Cloud Service. At a high-level, AEM requires a separation of content and code into discrete subpackages to respect the split between mutable and immutable content. Use the [Repository Modernizer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html) tool to restructure existing project packages by separating content and code into discrete packages to be compatible with the project structure defined for Adobe Experience Manager as a Cloud Service.
-->




