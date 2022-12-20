---
title: Formsas a Cloud Service通訊簡介
description: 自動將資料與XDP和PDF模板合併，或以PCL、ZPL和PostScript格式生成輸出
exl-id: b6f05b2f-5665-4992-8689-d566351d54f1
source-git-commit: 33e59ce272223e081710294a2e2508edb92eba52
workflow-type: tm+mt
source-wordcount: '1136'
ht-degree: 1%

---

# 使用AEM Formsas a Cloud Service通訊 {#frequently-asked-questions}

通信功能可幫助您建立品牌認可、個性化和標準化的文檔，如業務往來函、對帳單、報銷申請處理信函、福利通知、每月賬單或歡迎套件。

此功能提供API來產生和操控檔案。 您可以按需生成或操作文檔，或建立批處理作業以按定義的間隔生成多個文檔。 通訊API提供：

* 簡化隨需和批次檔案的產生功能。

* 按需組合、重新排列和驗證PDF文檔的功能。

* HTTP API可輕鬆與外部系統整合。 包括獨立的API，以用於隨選（低延遲）和批次作業（高吞吐量作業）。

* 安全存取資料。 通信API僅連接到客戶指定的資料儲存庫並訪問資料，因此通信高度安全。

![信用卡報表示例](assets/statement.png)
信用卡對帳單可使用Communications API來建立。 此示例對帳單使用相同的模板，但根據每個客戶的信用卡使用情況，為每個客戶分別提供資料。

## 檔案產生

通信文檔生成API有助於將模板(XFA或PDF)與客戶資料(XML)結合，以PDF和打印格式（如PS、PCL、DPL、IPL和ZPL格式）生成文檔。 這些API透過運用PDF和XFA範本 [XML資料](communications-known-issues-limitations.md#form-data) 使用批任務按需生成單個文檔或多個文檔。

通常，您使用 [設計工具](use-forms-designer.md) 和使用通訊API來合併資料與範本。 您的應用程式可以將輸出文檔發送到網路打印機、本地打印機或儲存系統進行存檔。 典型的現成可用和自訂工作流程如下所示：

![通信文檔生成工作流](assets/communicaions-workflow.png)

您也可以根據使用案例，透過您的網站或儲存伺服器下載這些檔案。

檔案產生API的一些範例如下：

### 建立PDF文檔 {#create-pdf-documents}

您可以使用文檔生成API來建立基於表單設計和XML表單資料的PDF文檔。 輸出是非互動式PDF檔案。 也就是說，使用者無法輸入或修改表單資料。 基本的工作流是將XML表單資料與表單設計合併，以建立PDF文檔。 下圖顯示表單設計與XML表單資料的合併，以產生PDF檔案。

![建立PDF文檔](assets/outPutPDF_popup.png)
圖：建立PDF文檔的典型工作流

### 建立PostScript(PS)、打印機命令語言(PCL)、Zebra打印語言(ZPL)文檔 {#create-PS-PCL-ZPL-documents}

您可以使用文檔生成API來建立基於XDP表單設計或PDF文檔的PostScript(PS)、打印機命令語言(PCL)和Zebra打印語言(ZPL)文檔。 這些API有助於將表單設計與表單資料合併，以產生檔案。 您可以將檔案儲存至檔案，並開發自訂程式以將其傳送至印表機。

<!-- ### Processing batch data to create multiple documents

Communications APIs can create separate documents for each record within an XML batch data source. The APIs can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you instruct the APIs to create a separate document for each record (for example, PDF documents). As a result, the APIs generate ten PDF documents.

The following illustration also shows Communications APIs processing an XML data file that contains multiple records. However, assume that you instruct the APIs to create a single PDF document that contains all data records. In this situation, the APIs generate one document that contains all of the records.

The following illustration shows Communications APIs processing an XML data file that con tains multiple records. Assume that you instruct the Communications APIs to create a separate PDF document for each data record. In this situation, the APIs generates a separate PDF document for each data record.

 -->

### 處理批資料以建立多個文檔 {#processing-batch-data-to-create-multiple-documents}

您可以使用文檔生成API為XML批資料源內的每個記錄建立單獨的文檔。 您可以以批量和非同步模式生成文檔。 您可以為轉換設定各種參數，然後開始批次處理。

![建立PDF文檔](assets/ou_OutputBatchMany_popup.png)

<!-- You can can also create a single document that contains all records (this functionality is the default).  Assume that an XML data source contains ten records and you have a requirement to create a separate document for each record (for example, PDF documents). You can use the Communication APIs to generate ten PDF documents. -->

<!-- The following illustration shows the Communication APIs processing an XML data file that contains multiple records. However, assume that you instruct the Communication APIs to create a single PDF document that contains all data records. In this situation, the Communication APIs generate one document that contains all of the records.

![Create PDF Documents](assets/ou_OutputBatchSingle_popup.png)

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. Assume that you instruct the Communication APIs to create a separate PDF document for each data record. In this situation, the Communication APIs generates a separate PDF document for each data record.

![Create PDF Documents](assets/ou_OutputBatchMany_popup.png)

For detailed information on using Batch APIs, see Communication APIs: Processing batch data to create multiple documents. 

### Flatten interactive PDF documents {#flatten-interactive-pdf-documents}

You can use document generation APIs to transform an interactive PDF document (for example, a form) to a non-interactive PDF document. An interactive PDF document lets users enter or modify data located in the PDF document fields. The process of transforming an interactive PDF document to a non-interactive PDF document is called flattening. When a PDF document is flattened, a user cannot modify the data located in the document’s fields. One reason to flatten a PDF document is to ensure that data cannot be modified.

You can flatten the following types of PDF documents:

* Interactive PDF documents created in Designer (that contain XFA streams).

* Acrobat PDF forms

If you attempt to flatten a non-interactive PDF document, an exception occurs.

### Retain Form State {#retain-form-state}

An interactive PDF document contains various elements that constitute a form. These elements may include fields (to accept or display data), buttons (to trigger events), and scripts (commands to perform a specific action). Clicking a button may trigger an event that changes the state of a field. For example, choosing a gender option may change the color of a field or the appearance of the form. This is an example of a manual event causing the form state to change.

When such an interactive PDF document is flattened using the Communications APIs, the state of the form is not retained. To ensure that the state of the form is retained even after the form is flattened, set the Boolean value _retainFormState_ to True to save and retain the state of the form. -->

## 檔案操作

通信文檔操作API有助於組合、重新排列和驗證PDF文檔。 通常，您會建立DDX並將其提交至檔案操作API，以組合或重新排列檔案。 此 [DDX文檔](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf) 提供了有關如何使用源文檔生成一組所需文檔的說明。 DDX參考檔案提供所有支援操作的詳細資訊。 文檔操作的一些示例包括：

### 匯編PDF文檔

您可以使用檔案操作API將兩個或多個PDF或XDP檔案組合為單一PDF檔案或PDFPortfolio。 以下是匯編PDF文檔的一些方法：

* 組合簡單的PDF文檔
* 建立PDFPortfolio
* 組合加密文檔
* 使用Bates編號來組合文檔
* 平面化和組合檔案

![從多個PDF文檔組裝簡單的PDF文檔](assets/as_document_assembly.png)
圖：從多個PDF文檔組裝簡單的PDF文檔

### 拆解PDF文檔

您可以使用文檔操作API來拆解PDF文檔。 API可從來源檔案擷取頁面，或根據書籤分割來源檔案。 通常，如果PDF文檔最初是從許多單個文檔（如語句集合）建立，則此任務非常有用。

* 從源文檔中提取頁面
* 根據書籤劃分源文檔

![將基於書籤的源文檔劃分為多個文檔](assets/as_intro_pdfsfrombookmarks.png)
圖：將基於書籤的源文檔劃分為多個文檔

### 轉換為並驗證PDF/A相容文檔

您可以使用文檔操作API將PDF文檔轉換為符合PDF/A的文檔，並確定PDF文檔是否符合PDF/A。 PDF/A是一種存檔格式，用於對文檔的內容進行長期保存。 這些字型嵌入到文檔中，並且該檔案被解壓縮。 因此，PDF/A文檔通常比標準PDF文檔大。 此外，PDF/檔案不包含音訊和視訊內容。

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

## 通訊API類型

通訊提供HTTP API，以供隨需和批次檔案產生：

* **[同步API](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)** 適用於按需、低延遲和單記錄文檔生成方案。 這些API更適合使用者動作的使用案例。 例如，在使用者填妥表單後產生檔案。

* **[批次API（非同步API）](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)** 適合於計畫、高吞吐量和多文檔生成方案。 這些API會以批次產生檔案。 例如，每月生成電話賬單、信用卡對帳單和福利對帳單。

## 上線

通訊功能是供Formsas a Cloud Service使用者使用的獨立附加模組。 您可以聯絡Adobe銷售團隊或您的Adobe代表以要求存取權。 Adobe 為您的組織啟用存取權限，並向您指定的組織管理員提供所需的特權。 管理員可授予您組織的Formsas a Cloud Service開發人員（使用者）使用API的存取權。

上線後，若要為您的Formsas a Cloud Service環境啟用通訊功能：

1. 登入Cloud Manager並開啟AEM Formsas a Cloud Service例項。

1. 開啟「編輯方案」選項，前往「解決方案與附加元件」標籤，然後選取 **[!UICONTROL Forms — 通訊]** 選項。

   ![通訊](assets/communications.png)

   如果您已啟用 **[!UICONTROL Forms — 數位註冊]** 選項，然後選取 **[!UICONTROL Forms — 通訊附加元件]** 選項。

   ![Addon](assets/add-on.png)

1. 按一下 **[!UICONTROL 更新]**.

1. 執行建置管道。 建置管道成功後，即會為您的環境啟用通訊API。

>[!NOTE]
>
> 若要啟用並設定檔案操作API，請新增下列規則至 [Dispatcher設定](setup-local-development-environment.md#forms-specific-rules-to-dispatcher):
>
> `# Allow Forms Doc Generation requests`
> `/0062 { /type "allow" /method "POST" /url "/adobe/forms/assembler/*" }`

<!--

Communication help you combine a template and XML data to generate print documents in various formats. The service allows you to generate documents in synchronous and batch modes. The APIs enables you to create applications that let you:

  * Generate documents by populating template files (PDF and XDP) with XML data.
  * Generate output forms in various formats, including non-interactive PDF print streams.

Consider a scenario where you have one or more templates and multiple records of XML data for each template. You can use Communications APIs to generate a print document for each record.  You can also combine the records into a single document.  The result is a non-interactive PDF document. A non-interactive PDF document does not let users enter data into its fields.

 There are two main Communications APIs. The _generatePDFOutput_ generates PDFs, while the _generatePrintedOutput_ generates PostScript, ZPL, and PCL formats. These APIs are available as REST endpoints on your environment, both on author and publish instances. Since the publish instances are configured to scale faster than the author instances, it is recommended use these APIs via publish instances.

The first parameter of both the operations accept the path and name of the template file (for example ExpenseClaim.xdp). You can specify a fully qualified path, reference path of your AEM Repository, or path of a binary file. The second parameter accepts an XML document that is merged with the template while generating the output document.  

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

You can use Communications APIs to create PostScript (PS), Printer Command Language (PCL), and Zebra Printing Language (ZPL) document that are based on a XDP form design or PDF document. The _generatePrintedOutput_ API merges a form design with form data to generate a document. You can save the document to a file and develop a custom process to send it to a printer.

 ### Processing batch data to create multiple documents

Communications APIs can create separate documents for each record within an XML batch data source. The APIs can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you instruct the APIs to create a separate document for each record (for example, PDF documents). As a result, the APIs generate ten PDF documents.

The following illustration also shows Communications APIs processing an XML data file that contains multiple records. However, assume that you instruct the APIs to create a single PDF document that contains all data records. In this situation, the APIs generate one document that contains all of the records.

The following illustration shows Communications APIs processing an XML data file that contains multiple records. Assume that you instruct the Communications APIs to create a separate PDF document for each data record. In this situation, the APIs generates a separate PDF document for each data record.

### Processing batch data to create multiple documents {#processing-batch-data-to-create-multiple-documents}

You create separate documents for each record within an XML batch data source. You can can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you have a requirement to create a separate document for each record (for example, PDF documents). You can use the Communication APIs to generate ten PDF documents.

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. However, assume that you instruct the Communication APIs to create a single PDF document that contains all data records. In this situation, the Communication APIs generate one document that contains all of the records.

![Create PDF Documents](assets/ou_OutputBatchSingle_popup.png)

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. Assume that you instruct the Communication APIs to create a separate PDF document for each data record. In this situation, the Communication APIs generates a separate PDF document for each data record.

![Create PDF Documents](assets/ou_OutputBatchMany_popup.png)

For detailed information on using Batch APIs, see Communication APIs: Processing batch data to create multiple documents.

### Flatten interactive PDF documents {#flatten-interactive-pdf-documents}

You can use the Communications APIs to transform an interactive PDF document (for example, a form) to a non-interactive PDF document. An interactive PDF document lets users enter or modify data located in the PDF document fields. The process of transforming an interactive PDF document to a non-interactive PDF document is called flattening. When a PDF document is flattened, a user cannot modify the data located in the document’s fields. One reason to flatten a PDF document is to ensure that data cannot be modified.

You can flatten the following types of PDF documents:

* Interactive PDF documents created in Designer (that contain XFA streams).

* Acrobat PDF forms

If you attempt to flatten a non-interactive PDF document, an exception occurs.

### Retain Form State {#retain-form-state}

An interactive PDF document contains various elements that constitute a form. These elements may include fields (to accept or display data), buttons (to trigger events), and scripts (commands to perform a specific action). Clicking a button may trigger an event that changes the state of a field. For example, choosing a gender option may change the color of a field or the appearance of the form. This is an example of a manual event causing the form state to change.

When such an interactive PDF document is flattened using the Communications APIs, the state of the form is not retained. To ensure that the state of the form is retained even after the form is flattened, set the Boolean value _retainFormState_ to True to save and retain the state of the form.  -->
