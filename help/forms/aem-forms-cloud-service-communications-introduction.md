---
title: Formsas a Cloud Service通訊
description: 自動將資料與XDP和PDF模板合併，或以PCL、ZPL和PostScript格式生成輸出
exl-id: b6f05b2f-5665-4992-8689-d566351d54f1
source-git-commit: d4372e7f5766c6fadea6ca25edc7bfa2aeba10b9
workflow-type: tm+mt
source-wordcount: '1026'
ht-degree: 1%

---

# 使用AEM Formsas a Cloud Service通信 {#frequently-asked-questions}

**AEM Formsas a Cloud Service通信功能為beta。**

通信功能可幫助您建立面向品牌、個性化和標準化的文檔，如業務信函、報表、理賠信函、福利通知、每月帳單或歡迎套件。


您可以按需生成文檔或建立批處理作業，以按定義的間隔生成多個文檔。 通信API提供：

* 簡化的按需和批處理文檔生成功能。

* HTTP API可更輕鬆地與外部系統整合。 包括用於按需（低延遲）和批處理操作（高吞吐量操作）的單獨API。 它使文檔生成成為一項高效的任務。

* 安全訪問資料。 通信API僅連接到客戶指定的資料儲存庫並從其訪問資料，不製作資料的本地副本，使通信具有高度安全性。

![信用卡對帳單樣本](assets/statement.png)
可以使用通信API建立信用卡對帳單。 此示例對帳單使用相同的模板，但根據每個客戶的信用卡使用情況將資料分開。

## 它是怎麼運作的？

通信利用 [PDF和XFA模板](#supported-document-types) 與 [XML資料](#form-data) 按需生成單個文檔或使用按定義間隔的批處理作業生成多個文檔。

通信API可幫助將模板(XFA或PDF)與客戶資料([XML資料](#form-data))以PDF和打印格式（如PS、PCL、DPL、IPL和ZPL格式）生成文檔。

通常，您使用 [設計師](use-forms-designer.md) 並使用Communications API將資料與模板合併。 您的應用程式可以將輸出文檔發送到網路打印機、本地打印機或儲存系統進行存檔。 典型的開箱即用工作流和自定義工作流如下所示：

![通信工作流](assets/communicaions-workflow.png)

根據使用案例，您還可以通過網站或儲存伺服器下載這些文檔。

## 通信API

通信為按需和批處理文檔生成提供HTTP API:

* **[同步API](https://www.adobe.io/experience-manager-forms-cloud-service-developer-reference/)** 適用於按需、低延遲和單記錄文檔生成情形。 這些API更適合基於用戶操作的使用案例。 例如，在用戶完成填寫表單後生成文檔。

* **[批處理API（非同步API）](https://www.adobe.io/experience-manager-forms-cloud-service-developer-reference/)** 適用於計畫、高吞吐量和多個文檔生成方案。 這些API以批次形式生成文檔。 例如，每月生成電話單、信用卡對帳單和福利對帳單。

通信API的一些主要用途是：

### 建立PDF文檔 {#create-pdf-documents}

可以使用通信API建立基於表單設計和XML表單資料的PDF文檔。 輸出是非互動式PDF文檔。 即用戶不能輸入或修改表單資料。 基本工作流是將XML表單資料與表單設計合併，以建立PDF文檔。 下圖顯示了表單設計與XML表單資料的合併，以生成PDF文檔。

![建立PDF文檔](assets/outPutPDF_popup.png)

### 建立PostScript(PS)、打印機命令語言(PCL)、Zebra打印語言(ZPL)文檔 {#create-PS-PCL-ZPL-documents}

您可以使用Communications API建立基於XDP表單設計或PDF文檔的PostScript(PS)、打印機命令語言(PCL)和Zebra打印語言(ZPL)文檔。 這些API有助於將表單設計與表單資料合併以生成文檔。 您可以將文檔保存到檔案中，並開發自定義流程以將其發送到打印機。

<!-- ### Processing batch data to create multiple documents

Communications APIs can create separate documents for each record within an XML batch data source. The APIs can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you instruct the APIs to create a separate document for each record (for example, PDF documents). As a result, the APIs generate ten PDF documents.

The following illustration also shows Communications APIs processing an XML data file that contains multiple records. However, assume that you instruct the APIs to create a single PDF document that contains all data records. In this situation, the APIs generate one document that contains all of the records.

The following illustration shows Communications APIs processing an XML data file that contains multiple records. Assume that you instruct the Communications APIs to create a separate PDF document for each data record. In this situation, the APIs generates a separate PDF document for each data record.

 -->

### 處理批處理資料以建立多個文檔 {#processing-batch-data-to-create-multiple-documents}

您可以為XML批資料源中的每個記錄建立單獨的文檔。 您可以在批量和非同步模式下生成文檔。 您可以為轉換配置各種參數，然後啟動批處理。 <!-- You can can also create a single document that contains all records (this functionality is the default).  Assume that an XML data source contains ten records and you have a requirement to create a separate document for each record (for example, PDF documents). You can use the Communication APIs to generate ten PDF documents. -->

<!-- The following illustration shows the Communication APIs processing an XML data file that contains multiple records. However, assume that you instruct the Communication APIs to create a single PDF document that contains all data records. In this situation, the Communication APIs generate one document that contains all of the records.

![Create PDF Documents](assets/ou_OutputBatchSingle_popup.png)

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. Assume that you instruct the Communication APIs to create a separate PDF document for each data record. In this situation, the Communication APIs generates a separate PDF document for each data record.

![Create PDF Documents](assets/ou_OutputBatchMany_popup.png)

For detailed information on using Batch APIs, see Communication APIs: Processing batch data to create multiple documents. -->

### 拼合互動式PDF文檔 {#flatten-interactive-pdf-documents}

您可以使用Communications API將互動式PDF文檔（例如，表單）轉換為非互動式PDF文檔。 互動式PDF文檔允許用戶輸入或修改位於PDF文檔欄位中的資料。 將互動式PDF文檔轉換為非互動式PDF文檔的過程稱為拼合。 當PDF文檔展平時，用戶無法修改位於文檔欄位中的資料。 展平PDF文檔的一個原因是確保資料無法修改。

可以拼合以下類型的PDF文檔：

* 互動式PDF文檔在設計器中建立（包含XFA流）。

* AcrobatPDF forms

如果嘗試拼合非互動式PDF文檔，則會發生異常。

### 保留窗體狀態 {#retain-form-state}

互動式PDF文檔包含構成表單的各種元素。 這些元素可包括欄位（接受或顯示資料）、按鈕（觸發事件）和指令碼（執行特定操作的命令）。 按一下按鈕可觸發更改欄位狀態的事件。 例如，選擇性別選項可能會更改欄位的顏色或表單的外觀。 這是導致窗體狀態更改的手動事件的示例。

當使用通信API平展這種互動式PDF文檔時，不保留表單的狀態。 要確保即使在平展表單後仍保留表單的狀態，請設定布爾值 _retainFormState_ 為True以保存和保留窗體的狀態。

## 入門

通信可作為Formsas a Cloud Service用戶的獨立和附加模組使用。 您可以聯繫Adobe銷售團隊或Adobe代表以請求訪問權限。

Adobe 為您的組織啟用存取權限，並向您指定的組織管理員提供所需的特權。 管理員可以授予您組織的AEM Forms開發人員（用戶）使用API的權限。

在結束後，為您的Formsas a Cloud Service環境啟用通信：

1. 登錄到雲管理器並開啟您的AEM Formsas a Cloud Service實例。

1. 開啟「編輯程式」選項，轉到「解決方案和載入項」頁籤，然後選擇 **[!UICONTROL Forms — 通信]** 的雙曲餘切值。

   ![通信](assets/communications.png)

   如果已啟用 **[!UICONTROL Forms — 數字註冊]** ，然後選擇 **[!UICONTROL Forms — 通信插件]** 的雙曲餘切值。

   ![阿登](assets/add-on.png)

1. 按一下 **[!UICONTROL 更新]**。

1. 運行生成管道。

生成管道成功後，將為您的環境啟用通信API。


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
