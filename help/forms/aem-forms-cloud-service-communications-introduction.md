---
title: Formsas a Cloud Service通訊
description: 自動將資料與XDP和PDF模板合併，或以PCL、ZPL和PostScript格式生成輸出
exl-id: b6f05b2f-5665-4992-8689-d566351d54f1
source-git-commit: a6b6a190a59d1c2f0001fe1f28d8d7bc8353d464
workflow-type: tm+mt
source-wordcount: '1144'
ht-degree: 1%

---

# 使用AEM Formsas a Cloud Service通信 {#frequently-asked-questions}

**文檔操作API處於預發佈階段，在實際發佈之前可能會發生更改。**

通信功能可幫助您建立品牌認可、個性化和標準化的文檔，如業務信函、報表、理賠信函、福利通知、每月帳單或歡迎套件。

該功能提供API來生成和操作文檔。 您可以按需生成或操作文檔或建立批處理作業以按定義的間隔生成多個文檔。 通信API提供：

* 簡化的按需和批處理文檔生成功能。

* 可按需組合、重新排列和驗證PDF文檔。

* HTTP API可更輕鬆地與外部系統整合。 包括用於按需（低延遲）和批處理操作（高吞吐量操作）的單獨API。

* 安全訪問資料。 通信API僅連接到客戶指定的資料儲存庫並從其訪問資料，使通信高度安全。

![信用卡對帳單樣本](assets/statement.png)
可以使用通信API建立信用卡對帳單。 此示例對帳單使用相同的模板，但根據每個客戶信用卡的使用情況分別使用資料。

## 文檔生成

通信文檔生成API幫助將模板(XFA或PDF)與客戶資料([XML資料](#form-data))以PDF和打印格式（如PS、PCL、DPL、IPL和ZPL格式）生成文檔。 這些API利用 [PDF和XFA模板](#supported-document-types) 與 [XML資料](communications-known-issues-limitations.md#form-data) 使用批處理作業生成單個單據按需或多個單據。

通常，您使用 [設計師](use-forms-designer.md) 並使用Communications API將資料與模板合併。 您的應用程式可以將輸出文檔發送到網路打印機、本地打印機或儲存系統進行存檔。 典型的開箱即用工作流和自定義工作流如下所示：

![通信文檔生成工作流](assets/communicaions-workflow.png)

根據使用案例，您還可以通過網站或儲存伺服器下載這些文檔。

文檔生成API的一些示例包括：

### 建立PDF文檔 {#create-pdf-documents}

可以使用文檔生成API建立基於表單設計和XML表單資料的PDF文檔。 輸出是非互動式PDF文檔。 即用戶不能輸入或修改表單資料。 基本工作流是將XML表單資料與表單設計合併，以建立PDF文檔。 下圖顯示了表單設計與XML表單資料的合併，以生成PDF文檔。

![建立PDF文檔](assets/outPutPDF_popup.png)
圖：建立PDF文檔的典型工作流

### 建立PostScript(PS)、打印機命令語言(PCL)、Zebra打印語言(ZPL)文檔 {#create-PS-PCL-ZPL-documents}

可以使用文檔生成API建立基於XDP表單設計或PDF文檔的PostScript(PS)、打印機命令語言(PCL)和Zebra打印語言(ZPL)文檔。 這些API有助於將表單設計與表單資料合併以生成文檔。 您可以將文檔保存到檔案中，並開發自定義流程以將其發送到打印機。

<!-- ### Processing batch data to create multiple documents

Communications APIs can create separate documents for each record within an XML batch data source. The APIs can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you instruct the APIs to create a separate document for each record (for example, PDF documents). As a result, the APIs generate ten PDF documents.

The following illustration also shows Communications APIs processing an XML data file that contains multiple records. However, assume that you instruct the APIs to create a single PDF document that contains all data records. In this situation, the APIs generate one document that contains all of the records.

The following illustration shows Communications APIs processing an XML data file that con tains multiple records. Assume that you instruct the Communications APIs to create a separate PDF document for each data record. In this situation, the APIs generates a separate PDF document for each data record.

 -->

### 處理批處理資料以建立多個文檔 {#processing-batch-data-to-create-multiple-documents}

您可以使用文檔生成API為XML批資料源中的每個記錄建立單獨的文檔。 您可以在批量和非同步模式下生成文檔。 您可以為轉換配置各種參數，然後啟動批處理。

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


## （預發佈）文檔處理

通信文檔處理API有助於組合、重新排列和驗證PDF文檔。 通常，您會建立DDX並將其提交到文檔處理API以匯編或重新排列文檔。 DDX文檔提供了有關如何使用源文檔生成一組所需文檔的說明。 DDX參考文檔提供了有關所有支援操作的詳細資訊。 文檔處理的一些示例包括：

### 匯編PDF文檔

您可以使用文檔製造API將兩個或多個PDF或XDP文檔匯編為單個PDF文檔或PDFPortfolio。 以下是匯編PDF文檔的一些方法：

* 匯編簡單PDF文檔
* 建立PDFPortfolio
* 匯編加密文檔
* 使用Bates編號來匯編文檔
* 拼合和匯編文檔

![從多個PDF文檔中組裝簡單PDF文檔](assets/as_document_assembly.png)
圖：從多個PDF文檔中組裝簡單PDF文檔

### 拆卸PDF文檔

您可以使用文檔製造API來拆解PDF文檔。 API可以從源文檔中提取頁面或基於書籤劃分源文檔。 通常，如果PDF文檔最初是從許多單個文檔（如語句集合）建立的，則此任務非常有用。

* 從源文檔中提取頁面
* 基於書籤劃分源文檔

![將基於書籤的源文檔劃分為多個文檔](assets/as_intro_pdfsfrombookmarks.png)
圖：將基於書籤的源文檔劃分為多個文檔

### 轉換為並驗證符合PDF/A的文檔

您可以使用文檔PDFAPI將PDF文檔轉換為符合PDF/A的文檔，並確定PDF文檔是否符合/A。 PDF/A是一種存檔格式，旨在長期保存文檔的內容。 字型嵌入到文檔中，檔案未壓縮。 因此，PDF/A文檔通常比標準PDF文檔大。 此外，PDF/文檔不包含音頻和視頻內容。

>[!NOTE]
>
> 要啟用和配置文檔處理API，請將以下規則添加到 [調度程式配置](setup-local-development-environment.md#forms-specific-rules-to-dispatcher):
>
> `# Allow Forms Doc Generation requests`
> `/0062 { /type "allow" /method "POST" /url "/adobe/forms/assembler/*" }`


## 通信API的類型

通信為按需和批處理文檔生成提供HTTP API:

* **[同步API](https://www.adobe.io/experience-manager-forms-cloud-service-developer-reference/)** 適用於按需、低延遲和單記錄文檔生成情形。 這些API更適合基於用戶操作的使用案例。 例如，在用戶完成填寫表單後生成文檔。

* **[批處理API（非同步API）](https://www.adobe.io/experience-manager-forms-cloud-service-developer-reference/)** 適用於計畫、高吞吐量和多個文檔生成方案。 這些API以批次形式生成文檔。 例如，每月生成電話單、信用卡對帳單和福利對帳單。

## 入門

通信功能可作為Formsas a Cloud Service用戶的獨立和附加模組使用。 您可以聯繫Adobe銷售團隊或Adobe代表以請求訪問權限。 Adobe 為您的組織啟用存取權限，並向您指定的組織管理員提供所需的特權。 管理員可授予您組織的Formsas a Cloud Service開發人員（用戶）使用API的權限。

登機後，要為您的Formsas a Cloud Service環境啟用通信功能：

1. 登錄到Cloud Manager並開啟您的AEM Formsas a Cloud Service實例。

1. 開啟「編輯程式」選項，轉到「解決方案和載入項」頁籤，然後選擇 **[!UICONTROL Forms — 通信]** 的雙曲餘切值。

   ![通信](assets/communications.png)

   如果已啟用 **[!UICONTROL Forms — 數字註冊]** ，然後選擇 **[!UICONTROL Forms — 通信插件]** 的雙曲餘切值。

   ![阿登](assets/add-on.png)

1. 按一下 **[!UICONTROL 更新]**。

1. 運行生成管道。 生成管道成功後，將為您的環境啟用Communications API。


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
