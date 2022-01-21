---
title: Formsas a Cloud Service通訊
description: 自動將資料與XDP和PDF模板合併，或以PCL、ZPL和PostScript格式生成輸出
exl-id: b6f05b2f-5665-4992-8689-d566351d54f1
source-git-commit: d136062ed0851b89f954e5485c2cfac64afeda2d
workflow-type: tm+mt
source-wordcount: '1869'
ht-degree: 1%

---

# 使用AEM Formsas a Cloud Service通信 {#frequently-asked-questions}

**AEM Formsas a Cloud Service通信功能為beta。**

通信功能可幫助您建立面向品牌、個性化和標準化的文檔，如業務信函、報表、理賠信函、福利通知、每月帳單或歡迎套件。


您可以按需生成文檔或建立批處理作業，以按定義的間隔生成多個文檔。 通信API提供：

* 簡化的按需和批量文檔生成功能

* HTTP API可更輕鬆地與現有系統整合。 包括用於按需（低延遲）和批處理操作（高吞吐量操作）的單獨API。 它使文檔生成成為一項高效的任務。

* 安全訪問資料。 通信API僅連接到客戶指定的資料儲存庫並從其訪問資料，不製作資料的本地副本，使通信具有高度安全性。

![信用卡對帳單樣本](assets/statement.png)
可以使用通信API建立信用卡對帳單。 此示例對帳單使用相同的模板，但根據每個客戶的信用卡使用情況將資料分開。

## 它是怎麼運作的？

通信利用 [PDF和XFA模板](#supported-document-types) 與 [XML資料](#form-data) 按需生成單個文檔或使用按定義間隔的批處理作業生成多個文檔。

通信API有助於將模板(XFA或PDF)與客戶資料([XML資料](#form-data))以PDF和打印格式（如PS、PCL、DPL、IPL和ZPL格式）生成文檔。

通常，您使用 [設計師](use-forms-designer.md) 並使用Communications API將資料與模板合併。 您的應用程式可以將輸出文檔發送到網路打印機、本地打印機或儲存系統進行存檔。 典型的開箱即用工作流和自定義工作流如下所示：

![通信工作流](assets/communicaions-workflow.png)

根據使用案例，您還可以通過網站或儲存伺服器下載這些文檔。

## 通信API

通信為按需和批處理文檔生成提供HTTP API:

* **[同步API](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/api/sync/)** 適用於按需、低延遲和單記錄文檔生成情形。 這些API更適合基於用戶操作的使用案例。 例如，在用戶完成填寫表單後生成文檔。

* **[批處理API（非同步API）](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/api/batch/)** 適用於計畫、高吞吐量和多個文檔生成方案。 這些API以批次形式生成文檔。 例如，每月生成電話單、信用卡對帳單和福利對帳單。

## 入門

通信可作為Formsas a Cloud Service用戶的獨立和附加模組使用。 您可以聯繫Adobe銷售團隊或Adobe代表以請求訪問權限。

Adobe 為您的組織啟用存取權限，並向您指定的組織管理員提供所需的特權。 管理員可以授予您組織的AEM Forms開發人員（用戶）使用API的權限。

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

## 注意事項 {#considerations-for-communications-apis}

在開始使用通信API生成文檔之前，請考慮以下事項：

### 表單資料 {#form-data}

通信API接受通常在 [設計師](use-forms-designer.md) 和XML表單資料作為輸入。 要用資料填充文檔，XML元素必須存在於要填充的每個表單域的XML表單資料中。 XML元素名稱必須與欄位名稱匹配。 如果XML元素與表單域不對應，或者XML元素名稱與欄位名稱不匹配，則忽略XML元素。 不必與XML元素的顯示順序匹配。 重要因素是XML元素是用相應的值指定的。

請考慮以下貸款申請表示例：

![貸款申請表](assets/loanFormData.png)

要將資料合併到此表單設計中，請建立與表單層次結構、欄位命名和資料類型對應的XML資料源。 以下XML表示與示例抵押申請表單對應的XML資料源。

```XML
* <xfa:datasets xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/">
* <xfa:data>
* <data>
    * <Layer>
        <closeDate>1/26/2007</closeDate>
        <lastName>Johnson</lastName>
        <firstName>Jerry</firstName>
        <mailingAddress>JJohnson@NoMailServer.com</mailingAddress>
        <city>New York</city>
        <zipCode>00501</zipCode>
        <state>NY</state>
        <dateBirth>26/08/1973</dateBirth>
        <middleInitials>D</middleInitials>
        <socialSecurityNumber>(555) 555-5555</socialSecurityNumber>
        <phoneNumber>5555550000</phoneNumber>
    </Layer>
    * <Mortgage>
        <mortgageAmount>295000.00</mortgageAmount>
        <monthlyMortgagePayment>1724.54</monthlyMortgagePayment>
        <purchasePrice>300000</purchasePrice>
        <downPayment>5000</downPayment>
        <term>25</term>
        <interestRate>5.00</interestRate>
    </Mortgage>
</data>
</xfa:data>
</xfa:datasets>
```

### 支援的文檔類型 {#supported-document-types}

要完全訪問通信API的呈現功能，建議使用XDP檔案作為輸入。 有時，可以使用PDF檔案。 但是，將PDF檔案用作輸入具有以下限制：

不包含XFA流的PDF文檔不能呈現為PostScript、PCL或ZPL。 通信API可以使用XFA流呈現PDF文檔(即，在 [設計師](use-forms-designer.md))和標籤格式。 如果PDF文檔已簽名、認證或包含使用權限(使用AEM FormsReader擴展服務應用)，則無法將其呈現為這些打印格式。

<!-- Run-time options such as PDF version and tagged PDF are not supported for Acrobat forms. They are valid for PDF forms that contain XFA streams; however, these forms cannot be signed or certified. 

### Email support {#email-support}

For email functionality, you can create a process in Experience Manager Workflows that uses the Email Step. A workflow represents a business process that you are automating. -->

### 可打印區域 {#printable-areas}

預設的0.25英吋不可打印邊距對於標籤打印機不準確，並且因打印機和打印機而異，因標籤大小和標籤大小而異，但建議您保留0.25英吋邊距或縮小它。 但是，建議不要增加不可打印的邊距。 否則，可打印區域中的資訊無法正確打印。

始終確保為打印機使用正確的XDC檔案。 例如，請避免為300 dpi打印機選擇XDC檔案，並將文檔發送到200 dpi打印機。

### 僅用於XFA表單(XDP/PDF)的指令碼 {#scripts}

與Communications API一起使用的表單設計可以包含在伺服器上運行的指令碼。 確保表單設計不包含在客戶端上運行的指令碼。 有關建立表單設計指令碼的資訊，請參見 [設計器幫助](use-forms-designer.md)。

<!-- #### Working with Fonts
 Document Considerations for Working with Fonts>> -->

### 字型映射 {#font-mapping}

要設計使用打印機駐留字型的表單，請在設計器中選擇與打印機上可用字型匹配的字型名稱。 PCL或PostScript支援的字型清單位於相應的設備配置檔案（XDC檔案）中。 或者，可以建立字型映射以將非打印機駐留字型映射到不同字型名稱的打印機駐留字型。 例如，在PostScript方案中，對Arial®字型的引用可以映射到駐留在打印機上的Helvetica®字型。

如果在客戶端電腦上安裝了字型，則字型可在設計器的下拉清單中使用。 如果未安裝字型，則需要手動指定字型名稱。 Designer中的「永久替換不可用字型」選項可關閉。 否則，當XDP檔案保存在Designer中時，替代字型名稱將寫入XDP檔案。 它表示不使用打印機駐留字型。

存在兩種類型的OpenType®字型。 一種類型是PCL支援的TrueTypeOpenType®字型。 另一個是CFFOpenType®。 PDF和PostScript輸出支援嵌入的Type-1、TrueType和OpenType®字型。 PCL輸出支援嵌入式TrueType字型。

Type-1和OpenType®字型未嵌入PCL輸出。 使用Type-1和OpenType®字型格式化的內容將被柵格化並生成為點陣圖影像，該點陣圖影像可以大而慢，以便生成。

生成PostScript、PCL或PDF輸出時，下載或嵌入的字型將自動替換。 它意味著只有正確呈現所生成文檔所需的字型字形的子集才包含在所生成的輸出中。

### 使用設備配置檔案（XDC檔案） {#working-with-xdc-files}

設備配置檔案（XDC檔案）是XML格式的打印機描述檔案。 此檔案使Communications API能夠將文檔輸出為雷射或標籤打印機格式。 通信API使用XDC檔案，包括：

* hppcl5c.xdc

* hppcl5e.xdc

* ps_plain_level3.xdc

* ps_plain.xdc

* zpl300.xdc

* zpl600.xdc

* zpl300.xdc

* ipl300.xdc

* ipl400.xdc

* tpcl600.xdc

* dpl300.xdc

* dpl406.xdc

* dpl600.xdc

您可以使用提供的XDC檔案生成打印文檔或根據您的要求修改它們。
<!-- It is not necessary to modify these files to create documents. However, you can modify them to meet your business requirements. -->

這些檔案是支援特定打印機功能的XDC檔案，如駐留字型、紙盒和訂書機。 這些參考的目的是幫助您瞭解如何使用設備配置檔案來設定自己的打印機。 參考也是同一產品系列中類似打印機的起點。

### 使用XCI配置檔案 {#working-with-xci-files}

通信API使用XCI配置檔案來執行任務，例如控制輸出是單個面板還是分頁。 儘管此檔案包含可設定的設定，但修改此值並非典型情況。 <!-- The default.xci file is located in the svcdata\XMLFormService folder. -->

可以使用Communications API傳遞修改的XCI檔案。 執行此操作時，建立預設檔案的副本，僅更改需要修改以滿足業務要求的值，並使用修改的XCI檔案。

通信API以預設XCI檔案（或修改的檔案）開頭。 然後，它應用使用通信API指定的值。 這些值會覆蓋XCI設定。

下表指定了XCI選項。

| XCI選項 | 說明 |
| ------------------------------------| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 配置/呈現/pdf/建立者 | 使用「文檔資訊」字典中的「建立者」條目標識文檔建立者。 有關此詞典的資訊，請參閱《PDF參考指南》。 |
| 配置/存在/pdf/製作者 | 使用「文檔資訊」字典中的「製作者」條目標識文檔製作者。 有關此詞典的資訊，請參閱《PDF參考指南》。 |
| 配置/現在/佈局 | 控制輸出是單個面板還是分頁。 |
| 配置/存在/pdf/壓縮/級別 | 指定生成PDF文檔時要使用的壓縮程度。 |
| config/present/pdf/script模型 | 控制是否將XFA特定資訊包含在輸出PDF文檔中。 |
| config/present/common/data/adjustData | 控制XFA應用程式是否在合併後調整資料。 |
| config/present/pdf/renderPolicy | 控制頁面內容的生成是在伺服器上完成還是延遲到客戶端。 |
| 配置/現在/常用/區域設定 | 指定在輸出文檔中使用的預設區域設定。 |
| 配置/存在/目標 | 當當前元素包含時，指定輸出格式。 當openAction元素包含時，指定在互動式客戶端中開啟文檔時要執行的操作。 |
| 配置/存在/輸出/類型 | 指定要應用於檔案的壓縮類型或要生成的輸出類型。 |
| 配置/當前/常/溫/uri | 指定窗體URI。 |
| 配置/現在/常用/模板/基本 | 為窗體設計中的URI提供基本位置。 當此元素不存在或為空時，窗體設計的位置將用作基礎。 |
| 配置/存在/公用/日誌/收件人 | 控制日誌資料或輸出資料寫入的位置。 |
| 配置/提供/輸出/到 | 控制日誌資料或輸出資料寫入的位置。 |
| config/present/script/currentPage | 指定開啟文檔時的初始頁面。 |
| 配置/現在/指令碼/排除 | 通知AEM Forms伺服器/通信API要忽略哪些事件。 |
| 配置/現在/pdf/線性化 | 控制輸出PDF文檔是否線性化。 |
| config/present/script/runScripts | 控制執行哪組指令碼AEM Forms。 |
| 配置/呈現/pdf/加標籤 | 控制將標籤包含到輸出PDF文檔中。 在PDF的上下文中，標籤是文檔中包含的用於公開文檔邏輯結構的附加資訊。 標籤有助於輔助輔助工具和重新格式化。 例如，頁碼可以被標籤為項目，以便螢幕閱讀器不會在文本的中間清晰它。 儘管標籤使文檔更有用，但它們也增加了文檔的大小和建立文檔的處理時間。 |
| 配置/提供/pdf/版本 | 指定要生成的PDF文檔的版本。 |
