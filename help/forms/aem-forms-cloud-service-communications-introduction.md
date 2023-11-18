---
title: 什麼是Formsas a Cloud Service通訊API？
description: 使用通訊API來簽署、認證或保護您的檔案、自動化PDF產生流程，以及將PDF檔案轉換為另一種格式。
Keywords: How to generate document?, Generate PDF document, Manipulation PDF documents, Assembling PDF documents, Validating PDF document, APIs used in encrypting or decrypting PDFs
exl-id: b6f05b2f-5665-4992-8689-d566351d54f1
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1446'
ht-degree: 78%

---

# AEM Formsas a Cloud Service通訊簡介 {#frequently-asked-questions}


| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-document-services/overview-aem-document-services.html) |
| AEM as a Cloud Service  | 本文章 |

通訊功能可協助您建立品牌核准的、個性化的和標準化的文件，例如業務信函、報表、索賠處理函、福利通知、每月帳單或歡迎套件。

該功能提供 API 來產生和操控文件。您可以隨需產生和操控文件，或建立批次作業以按定義的時間間隔產生多個文件。通訊 API 提供：

* 簡化的隨需和批次文件產生功能。

* 能夠隨需合併、重新排列和驗證 PDF 文件。

* 用於輕鬆地與外部系統整合的 HTTP API。包括個別的 API 用於隨需 (低延遲) 和批次操作 (高輸送量操作)。

* 安全存取資料。通訊 API 僅連接到客戶指定的資料存放庫並從中存取資料，從而使通訊高度安全。

![信用卡對帳單範例](assets/statement.png)
可以使用通訊 API 建立信用卡對帳單。此對帳單範例使用相同的範本，但根據每個客戶的信用卡使用情況為每個客戶提供個別的資料。

## 文件產生

通訊文件產生 API 可協助將範本 (XFA 或 PDF) 與客戶資料 (XML) 相結合，以產生 PDF 和列印格式 (例如 PS、PCL、DPL、IPL 和 ZPL 格式) 的文件。這些 API 使用 PDF 和 XFA 範本搭配 [XML 資料](communications-known-issues-limitations.md#form-data)以產生單一隨需文件或使用批次作業產生多個文件。

通常，您使用 [Designer](use-forms-designer.md) 建立範本，並使用通訊 API 將資料與範本合併。您的應用程式可以將輸出文件傳送到網路印表機、本機印表機或儲存系統進行封存。典型的立即可用和自訂工作流程如下所示：

![通訊文件產生工作流程](assets/communicaions-workflow.png)

視使用案例而定，您也可以讓這些文件可透過網站或儲存伺服器下載。

一些文件產生 API 範例：

### 建立 PDF 文件 {#create-pdf-documents}

您可以使用文件產生 API 建立根據表單設計和 XML 表單資料的 PDF 文件。輸出是非互動式 PDF 文件。也就是說，使用者不能輸入或修改表單資料。基本的工作流程是將 XML 表單資料與表單設計合併以建立 PDF 文件。下圖顯示將表單設計與 XML 表單資料合併以產生 PDF 文件。

![建立 PDF 文件](assets/outPutPDF_popup.png)
圖：建立 PDF 文件的典型工作流程

### 建立 PostScript (PS)、印表機命令語言 (PCL)、Zebra 列印語言 (ZPL) 文件 {#create-PS-PCL-ZPL-documents}

您可以使用文件產生 API 建立根據 XDP 表單設計或 PDF 文件的 PostScript (PS)、印表機命令語言 (PCL)、Zebra 列印語言 (ZPL) 文件。這些 API 可協助將表單設計與表單資料合併以產生文件。您可以將文件儲存到檔案和開發自訂流程將其傳送到印表機。

<!-- ### Processing batch data to create multiple documents

Communications APIs can create separate documents for each record within an XML batch data source. The APIs can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you instruct the APIs to create a separate document for each record (for example, PDF documents). As a result, the APIs generate ten PDF documents.

The following illustration also shows Communications APIs processing an XML data file that contains multiple records. However, assume that you instruct the APIs to create a single PDF document that contains all data records. In this situation, the APIs generate one document that contains all the records.

The following illustration shows Communications APIs processing an XML data file that con tains multiple records. Assume that you instruct the Communications APIs to create a separate PDF document for each data record. In this situation, the APIs generates a separate PDF document for each data record.

 -->

### 處理批次資料以建立多個文件 {#processing-batch-data-to-create-multiple-documents}

您可以使用文件產生 API 為 XML 批次資料來源中的每筆記錄建立單獨的文件。您可以採大量和同步模式產生文件。您可以設定各種轉換參數，然後開始批次處理。

![建立 PDF 文件](assets/ou_OutputBatchMany_popup.png)

<!-- You can can also create a single document that contains all records (this functionality is the default).  Assume that an XML data source contains ten records and you have a requirement to create a separate document for each record (for example, PDF documents). You can use the Communication APIs to generate ten PDF documents. -->

<!-- The following illustration shows the Communication APIs processing an XML data file that contains multiple records. However, assume that you instruct the Communication APIs to create a single PDF document that contains all data records. In this situation, the Communication APIs generate one document that contains all the records.

![Create PDF Documents](assets/ou_OutputBatchSingle_popup.png)

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. Assume that you instruct the Communication APIs to create a separate PDF document for each data record. In this situation, the Communication APIs generates a separate PDF document for each data record.

![Create PDF Documents](assets/ou_OutputBatchMany_popup.png)

For detailed information on using Batch APIs, see Communication APIs: Processing batch data to create multiple documents. 

### Flatten interactive PDF documents {#flatten-interactive-pdf-documents}

You can use document generation APIs to transform an interactive PDF document (for example, a form) to a non-interactive PDF document. An interactive PDF document lets users enter or modify data located in the PDF document fields. The process of transforming an interactive PDF document to a non-interactive PDF document is called flattening. When a PDF document is flattened, a user cannot modify the data located in the document's fields. One reason to flatten a PDF document is to ensure that data cannot be modified.

You can flatten the following types of PDF documents:

* Interactive PDF documents created in Designer (that contain XFA streams).

* Acrobat PDF forms

If you attempt to flatten a non-interactive PDF document, an exception occurs.

### Retain Form State {#retain-form-state}

An interactive PDF document contains various elements that constitute a form. These elements may include fields (to accept or display data), buttons (to trigger events), and scripts (commands to perform a specific action). Clicking a button may trigger an event that changes the state of a field. For example, choosing a gender option may change the color of a field or the appearance of the form. This is an example of a manual event causing the form state to change.

When such an interactive PDF document is flattened using the Communications APIs, the state of the form is not retained. To ensure that the state of the form is retained even after the form is flattened, set the Boolean value _retainFormState_ to True to save and retain the state of the form. -->

## 文件操控

通訊文件操控 API 可協助合併、重新排列和驗證 PDF 文件。通常，您會建立一個 DDX 並將其提交給文件操控 API 以組合或重新排列文件。[DDX 文件](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf)提供了有關如何使用來源文件產生一組所需文件的說明。DDX 參考文件提供關於所有支援之作業的詳細資訊。部分文件操控範例：

### 組合 PDF 文件

您可以使用文件操控 API 將兩個或更多 PDF 或 XDP 文件組成單一 PDF 文件或 PDF 組合。以下是一些組合 PDF 文件的方法：

* 組合一個簡單 PDF 文件
* 建立 PDF 組合
* 組合加密的文件
* 使用貝茨編號 (Bates numbering) 組合文件
* 扁平化及組合文件

![將多個 PDF 文件組合成一個簡單 PDF 文件](assets/as_document_assembly.png)
圖：將多個 PDF 文件組合成一個簡單 PDF 文件

### 分解 PDF 文件

您可以使用文件操控 API 來分解 PDF 文件。API 可以從來源文件擷取頁面或根據書籤分隔來源文件。通常，如果 PDF 文件最初是從許多個別的文件 (例如報表集合) 建立的，則此作業很有幫助。

* 從來源文件擷取頁面
* 根據書籤分隔來源文件

![根據書籤將一個來源文件分隔成多個文件](assets/as_intro_pdfsfrombookmarks.png)
圖：根據書籤將一個來源文件分隔成多個文件

### 轉換為 PDF/A 相容文件並進行驗證

您可以使用文件操控 API 將 PDF 文件轉換為 PDF/A 相容文件，並確定 PDF 文件是否 PDF/A 相容。PDF/A是一種用於長期儲存檔案內容的封存格式。 字體內嵌在文件中，檔案未壓縮。因此，PDF/A 文件通常比標準 PDF 文件大。此外，PDF/A 文件不包含音訊和視訊內容。

<!-- 

## Document utilities

Document utilities synchronous APIs helps you convert documents between PDF and XDP file formats, and query information about a PDF document. For example, you can determine whether a PDF document contains comments or attachments. 

### Retrieve PDF document properties

You can [query a PDF document](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/pdf-utility-sync/#tag/Document-Extraction/) for the following information:

* Is a PDF Document: Check whether the source document is a PDF document.
* Is a fillable form: Check whether the source PDF document is a fillable form.
* Form Type: Retrieve the form type of the document.
* Check for Attachments: Check whether the source PDF document has any attachments.
* Check for Comments: Check whether the source PDF document has any review comments.
* Is a PDF Package: Check whether the document is a PDF package.
* Get the PDF Version: Retrieve the [version of the PDF document](https://en.wikipedia.org/wiki/History_of_PDF).
* Recommended Acrobat Version: Retrieve the required version of Acrobat (Reader) to open the PDF document.
* Is an XFA Document: Check whether the source PDF document is an XFA-based PDF document.
* Is Shell PDF: Check whether the source PDF document is shell PDF. A shell PDF contains only an XFA stream, font and image resources, and one page that is either blank or contains a warning that the document must be opened using Acrobat or Adobe Reader. The shell PDF is used with PDF transformation to optimize delivery of PDFForm transformations only.
* Get the XFA Version: Retrieve the [XFA Version for an XFA-based PDF document](https://en.wikipedia.org/wiki/XFA#XFA_versions).

### Convert PDF Documents into XDP Documents

The [PDF to XDP API](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/pdf-utility-sync/#tag/Document-Conversion) converts a PDF document to an XDP file. For a PDF document to be successfully converted to an XDP file, the PDF document must contain an XFA stream in the dictionary. -->

## 檔案保證 {#doc-assurance}

DocAssurance服務包含簽名和加密API：

### 簽名API

簽名 API 可讓您的組織保護所分發和接收 Adobe PDF 文件的安全和隱私。這項服務使用數位簽名和認證來確保只有預期的收件人才能變更文件。因為安全功能會套用至檔案本身，所以檔案在其整個生命週期中都會保持安全及受控。 當檔案離線下載以及將它送回您的組織時，防火牆外仍會保持安全。 您可以使用簽名API完成以下任務：

* 新增簽名欄位至PDF檔案。
* 在PDF檔案中簽署指定的簽名欄位。
* 認證PDF檔案

### 加密API

加密API可讓您加密和解密檔案。 檔案加密後，其內容會變得無法讀取。 授權的使用者可以解密檔案以取得內容的存取權。 如果PDF檔案已使用密碼加密，使用者必須先指定開啟的密碼，才能在Adobe Reader或Adobe Acrobat中檢視檔案。 同樣地，如果PDF檔案已使用憑證加密，使用者必須使用與用於加密PDF檔案的憑證（私密金鑰）相對應的公開金鑰來解密PDF檔案。

您可以使用加密API完成這些工作：

* 使用密碼加密PDF檔案。
* 從PDF檔案中移除密碼式加密。
* 擷取套用至PDF檔案的安全性型別。

簽名API和加密API都是 [同步API](#types-of-communications-apis-types).


## 通訊 API 類型 {#types}

通訊提供用於隨需和批次產生文件的 HTTP API：

* **[同步 API](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)** 適用於隨需、低延遲和單筆記錄文件產生案例。這些 API 更適合根據使用者動作的使用案例。例如，在使用者填寫完表單後產生文件。

* **[批次 API (非同步 API)](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)** 適用於已排程、高輸出量和多文件產生案例。這些 API 批次產生文件。例如，每月產生的電話帳單、信用卡報表和福利報表。

## 上線

通訊功能可作為獨立和附加模組供 Forms as a Cloud Service 使用者使用。您可以聯絡 Adobe Sales 團隊或您的 Adobe 代表，要求存取權。Adobe 為您的組織啟用存取權，並向您指定的組織管理員提供所需的權限。管理員可以將存取權授予您組織的 Forms as a Cloud Service 開發人員 (使用者) 以使用 API。

加入後，為您的 Forms as a Cloud Service 環境啟用通訊功能：

1. 登入 Cloud Manager 並開啟您的 AEM Forms as a Cloud Service 執行個體。

1. 開啟「編輯方案」選項，前往「解決方案和附加元件」索引標籤，然後選擇&#x200B;**[!UICONTROL Forms - 通訊]**&#x200B;選項。

   ![通訊](assets/communications.png)

   如果您已經啟用&#x200B;**[!UICONTROL Forms - 數位註冊]**&#x200B;選項，則選擇&#x200B;**[!UICONTROL Forms - 通訊附加元件]**&#x200B;選項。

   ![附加元件](assets/add-on.png)

1. 按一下&#x200B;**[!UICONTROL 更新]**。

1. 執行建置管道。建置管道成功後，將為您的環境啟用通訊 API。

>[!NOTE]
>
> 若要啟用和設定文件操控 API，請將以下規則新增至[Dispatcher 設定](setup-local-development-environment.md#forms-specific-rules-to-dispatcher)：
>
> `# Allow Forms Doc Generation requests`
> `/0062 { /type "allow" /method "POST" /url "/adobe/forms/assembler/*" }`

<!--

Communication help you combine a template and XML data to generate print documents in various formats. The service lets you generate documents in synchronous and batch modes. The APIs enables you to create applications that let you:

  * Generate documents by populating template files (PDF and XDP) with XML data.
  * Generate output forms in various formats, including non-interactive PDF print streams.

Consider a scenario where you have one or more templates and multiple records of XML data for each template. You can use Communications APIs to generate a print document for each record.  You can also combine the records into a single document.  The result is a non-interactive PDF document. A non-interactive PDF document does not let users enter data into its fields.

 There are two main Communications APIs. The _generatePDFOutput_ generates PDFs, while the _generatePrintedOutput_ generates PostScript, ZPL, and PCL formats. These APIs are available as REST endpoints on your environment, both on author and publish instances. Since the publish instances are configured to scale faster than the author instances, it is recommended use these APIs via publish instances.

The first parameter of both the operations accept the path and name of the template file (for example ExpenseClaim.xdp). You can specify a fully-qualified path, reference path of your AEM Repository, or path of a binary file. The second parameter accepts an XML document that is merged with the template while generating the output document.  

The [API reference documentation](https://documentcloud.adobe.com/link/track?uri=urn:aaid:scds:US:b1223732-ae0f-4921-bdc0-c31e48b56044) provides detailed information about all the parameters, authentication methods, and various services provided by APIs. The API reference documentation is also available in the .yaml format. You can download the .yaml for [Batch APIs](assets/batch-api.yaml) or [non-Batch API.yaml](assets/non-batch-api.yaml) file and upload it to postman to check functionality of APIs.

>[!VIDEO](https://video.tv.adobe.com/v/335771)

Uploading Communication APIs .yaml file to postman to check functionality of APIs.

## Using the Communications APIs {#workflows}

Typically, you create a template using [Designer](use-forms-designer.md) and use communications APIs ( generatePDFOutput and generatePrintedOutput) to:

* Convert these templates to various formats, including PDF, PostScript, ZPL, and PCL.
* Merge XML form data with a form design to generate a document.
* Generate a document without merging XML form data into the document. However, the primary workflow is merging data into the document.

Then, the output document is stored to a file. You can design custom workflows to send the file to a network printer, a local printer, or to a storage system for archival. A typical out of the box and custom workflows look like the following:

![Communications Workflow](assets/communicaions-workflow.png)

### Create PDF documents {#create-pdf-documents}

You can use the _generatePDFOutput_ API to create PDF document that is based on a form design and XML form data. The output is a non-interactive PDF document. That is, users cannot enter or modify form data. A basic workflow is to merge XML form data with a form design to create a PDF document. The following illustration shows the merging of a form design and XML form data to produce a PDF document.

![Create PDF Documents](assets/outPutPDF_popup.png)

### Create PostScript (PS), Printer Command Language (PCL), Zebra Printing Language (ZPL) document {#create-PS-PCL-ZPL-documents}

You can use Communications APIs to create PostScript (PS), Printer Command Language (PCL), and Zebra Printing Language (ZPL) document that are based on an XDP form design or PDF document. The _generatePrintedOutput_ API merges a form design with form data to generate a document. You can save the document to a file and develop a custom process to send it to a printer.

 ### Processing batch data to create multiple documents

Communications APIs can create separate documents for each record within an XML batch data source. The APIs can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you instruct the APIs to create a separate document for each record (for example, PDF documents). As a result, the APIs generate ten PDF documents.

The following illustration also shows Communications APIs processing an XML data file that contains multiple records. However, assume that you instruct the APIs to create a single PDF document that contains all data records. In this situation, the APIs generate one document that contains all the records.

The following illustration shows Communications APIs processing an XML data file that contains multiple records. Assume that you instruct the Communications APIs to create a separate PDF document for each data record. In this situation, the APIs generates a separate PDF document for each data record.

### Processing batch data to create multiple documents {#processing-batch-data-to-create-multiple-documents}

You create separate documents for each record within an XML batch data source. You can can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you have a requirement to create a separate document for each record (for example, PDF documents). You can use the Communication APIs to generate ten PDF documents.

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. However, assume that you instruct the Communication APIs to create a single PDF document that contains all data records. In this situation, the Communication APIs generate one document that contains all the records.

![Create PDF Documents](assets/ou_OutputBatchSingle_popup.png)

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. Assume that you instruct the Communication APIs to create a separate PDF document for each data record. In this situation, the Communication APIs generates a separate PDF document for each data record.

![Create PDF Documents](assets/ou_OutputBatchMany_popup.png)

For detailed information on using Batch APIs, see Communication APIs: Processing batch data to create multiple documents.

### Flatten interactive PDF documents {#flatten-interactive-pdf-documents}

You can use the Communications APIs to transform an interactive PDF document (for example, a form) to a non-interactive PDF document. An interactive PDF document lets users enter or modify data located in the PDF document fields. The process of transforming an interactive PDF document to a non-interactive PDF document is called flattening. When a PDF document is flattened, a user cannot modify the data located in the document's fields. One reason to flatten a PDF document is to ensure that data cannot be modified.

You can flatten the following types of PDF documents:

* Interactive PDF documents created in Designer (that contain XFA streams).

* Acrobat PDF forms

If you attempt to flatten a non-interactive PDF document, an exception occurs.

### Retain Form State {#retain-form-state}

An interactive PDF document contains various elements that constitute a form. These elements may include fields (to accept or display data), buttons (to trigger events), and scripts (commands to perform a specific action). Clicking a button may trigger an event that changes the state of a field. For example, choosing a gender option may change the color of a field or the appearance of the form. This is an example of a manual event causing the form state to change.

When such an interactive PDF document is flattened using the Communications APIs, the state of the form is not retained. To ensure that the state of the form is retained even after the form is flattened, set the Boolean value _retainFormState_ to True to save and retain the state of the form.  -->

## 另請參閱 {#see-also}

* [通訊處理 — 同步API](/help/forms/aem-forms-cloud-service-communications.md)
* [通訊處理 — 批次API](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)
* [最適化Forms的AEM Formsas a Cloud Service架構和通訊API](/help/forms/aem-forms-cloud-service-architecture.md)
