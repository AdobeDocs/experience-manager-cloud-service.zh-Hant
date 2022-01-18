---
title: Formsas a Cloud Service通訊簡介
description: 自動將資料與XDP和PDF模板合併，或以PCL、ZPL和PostScript格式生成輸出
exl-id: b6f05b2f-5665-4992-8689-d566351d54f1
source-git-commit: 8e20383a03f157f01da66bab930a3eccf674dde7
workflow-type: tm+mt
source-wordcount: '1840'
ht-degree: 1%

---

# 使用AEM Formsas a Cloud Service通訊 {#frequently-asked-questions}

**AEM Formsas a Cloud Service通訊功能正在測試中。**

通信功能可幫助您建立面向品牌、個性化和標準化的文檔，如業務往來函、對帳單、報銷申請處理信函、福利通知、每月賬單或歡迎套件。


您可以按需生成單據，也可以建立批任務以按定義的間隔生成多個文檔。 通訊API提供：

* 簡化的隨需和批次檔案產生功能

* 提供HTTP API，以便與現有系統輕鬆整合

* 安全存取資料。 通信API僅連接到客戶指定的資料儲存庫並從中訪問資料，不建立資料的本地副本，使通信高度安全。

* 針對低延遲和高吞吐量操作而單獨使用的API，使文檔生成成為一項高效的任務。

![信用卡報表示例](assets/statement.png)

## 如何運作？

通信利用 [PDF和XFA範本](#supported-document-types) with [XML資料](#form-data) 按需生成單個單據，或使用定義間隔的批任務生成多個單據。

通訊API可協助將範本(XFA或PDF)與客戶資料([XML資料](#form-data))，以生成PDF和打印格式的文檔，如PS、PCL、DPL、IPL和ZPL格式。

通常，您使用 [設計工具](use-forms-designer.md) 和使用通訊API來合併資料與範本。 您的應用程式可以將輸出文檔發送到網路打印機、本地打印機或儲存系統進行存檔。 典型的現成可用和自訂工作流程如下所示：

![通訊工作流程](assets/communicaions-workflow.png)

您也可以根據使用案例，透過您的網站或儲存伺服器下載這些檔案。

## 通訊API

通訊提供HTTP API，以供隨需和批次檔案產生：

* **[同步API](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/api/sync/)** 適用於按需、低延遲和單記錄文檔生成方案。 這些API更適合使用者動作的使用案例。 例如，在使用者填妥表單後產生檔案。

* **[批次API（非同步API）](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/api/batch/)** 適合於計畫、高吞吐量和多文檔生成方案。 這些API會以批次產生檔案。 例如，每月生成電話賬單、信用卡對帳單和福利對帳單。

## 入門

通訊是供Formsas a Cloud Service使用者使用的獨立附加模組。 您可以聯絡Adobe銷售團隊或您的Adobe代表以要求存取權。

Adobe 為您的組織啟用存取權限，並向您指定的組織管理員提供所需的特權。 管理員可授予您組織的AEM Forms開發人員（使用者）使用API的存取權。

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

## 考量事項 {#considerations-for-communications-apis}

開始使用通訊API產生檔案之前，請先考慮下列事項：

### 表單資料 {#form-data}

通訊API會接受通常於 [設計工具](use-forms-designer.md) 和XML表單資料作為輸入。 要用資料填充文檔，要填充的每個表單欄位的XML表單資料中必須存在XML元素。 XML元素名稱必須與欄位名稱相符。 如果XML元素與表單欄位不對應，或XML元素名稱與欄位名稱不匹配，則會忽略該元素。 不需要匹配XML元素的顯示順序。 重要因素是XML元素需指定相應的值。

請考量下列貸款申請表範例：

![貸款申請表](assets/loanFormData.png)

要將資料合併到此表單設計中，請建立與表單對應的XML資料源。 以下XML表示與抵押申請表示例對應的XML資料源。

```XML
<?xml version="1.0" encoding="UTF-8" ?>
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

若要完整存取通訊API的轉譯功能，建議您使用XDP檔案作為輸入。 有時可使用PDF檔案。 不過，使用PDF檔案作為輸入有下列限制：

不包含XFA資料流的PDF文檔無法呈現為PostScript、PCL或ZPL。 通訊API可以使用XFA資料流(即在 [設計工具](use-forms-designer.md))轉換為雷射和標籤格式。 如果PDF檔案經過簽署、認證或包含使用權限(使用AEM FormsReader擴充功能服務套用)，則無法以這些列印格式呈現。

<!-- Run-time options such as PDF version and tagged PDF are not supported for Acrobat forms. They are valid for PDF forms that contain XFA streams; however, these forms cannot be signed or certified. 

### Email support {#email-support}

For email functionality, you can create a process in Experience Manager Workflows that uses the Email Step. A workflow represents a business process that you are automating. -->

### 可列印區域 {#printable-areas}

標籤打印機的預設0.25英吋不可打印邊距不精確，因打印機和打印機而異，從標籤大小到標籤大小不等。 建議您保持0.25英吋的邊距或將其縮小。 不過，建議您不要增加不可列印的邊界。 否則，可打印區域中的資訊無法正確打印。

請務必為打印機使用正確的XDC檔案。 例如，請避免為300-dpi打印機選擇XDC檔案，並將文檔發送到200-dpi打印機。

### 指令碼 {#scripts}

與通訊API搭配使用的表單設計可包含在伺服器上執行的指令碼。 確保表單設計不包含在用戶端上執行的指令碼。 如需建立表單設計指令碼的相關資訊，請參閱 [設計工具說明](use-forms-designer.md).

<!-- #### Working with Fonts
 Document Considerations for Working with Fonts>> -->

### 字型對應 {#font-mapping}

要設計使用打印機駐留字型的表單，請在「設計器」中選擇與打印機上可用字型相匹配的字型名。 PCL或PostScript支援的字型清單位於相應的設備配置檔案（XDC檔案）中。 或者，可以建立字型映射以將非打印機駐留字型映射到不同字型名稱的打印機駐留字型。 例如，在PostScript方案中，對Arial®字型的引用可以映射到駐留在打印機上的Helvetica®字型。

如果字型安裝在客戶端電腦上，該字型可在Designer的下拉清單中使用。 如果未安裝字型，則需要手動指定字型名稱。 Designer中的「永久替換不可用的字型」選項可以關閉。 否則，當XDP檔案保存在Designer中時，替代字型名稱將寫入XDP檔案。 這表示未使用打印機駐留字型。

有兩種OpenType®字型。 一種類型是PCL支援的TrueTypeOpenType®字型。 二是CFFOpenType®。 PDF和PostScript輸出支援嵌入的Type-1、TrueType和OpenType®字型。 PCL輸出支援嵌入的TrueType字型。

Type-1和OpenType®字型未嵌入到PCL輸出中。 使用Type-1和OpenType®字型格式化的內容被柵格化並生成為點陣圖影像，該影像可能大而慢而難以生成。

在生成PostScript、PCL或PDF輸出時，下載或嵌入的字型會自動替換。 這意味著只有正確渲染生成的文檔所需的字型字形子集才包含在生成的輸出中。

### 使用裝置設定檔檔案（XDC檔案） {#working-with-xdc-files}

設備配置檔案（XDC檔案）是XML格式的打印機描述檔案。 此檔案可讓通訊API以雷射或標籤打印機格式輸出文檔。 通訊API使用XDC檔案，包含下列項目：

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

您可以使用提供的XDC檔案來生成打印文檔或根據您的要求修改它們。
&lt;!-*不需要修改這些檔案來建立文檔。 但是，您可以修改它們以符合您的業務需求。 —>

這些檔案是支援特定打印機功能的參考XDC檔案，如駐留字型、紙盤和訂書機。 這些參考的用途是幫助您了解如何使用設備配置檔案來設定自己的打印機。 參考也是同一生產線中類似打印機的起點。

### 使用XCI設定檔案 {#working-with-xci-files}

通訊API使用XCI設定檔案來執行工作，例如控制輸出是單一面板或編頁。 雖然此檔案包含可設定的設定，但修改此值並非典型值。 <!-- The default.xci file is located in the svcdata\XMLFormService folder. -->

您可以在使用通訊API時傳遞修改的XCI檔案。 執行此操作時，請建立預設檔案的副本，僅更改需要修改以滿足您的業務需求的值，然後使用修改的XCI檔案。

通訊API以預設XCI檔案（或修改的檔案）開頭。 然後會套用使用通訊API指定的值。 這些值會覆寫XCI設定。

下表指定XCI選項。

| XCI選項 | 說明 |
| ------------------------------------| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| config/present/pdf/creator | 使用「文檔資訊」字典中的「建立者」條目標識文檔建立者。 如需此字典的相關資訊，請參閱PDF參考指南。 |
| config/present/pdf/producer | 使用「文檔資訊」字典中的「生成者」條目標識文檔生成者。 如需此字典的相關資訊，請參閱PDF參考指南。 |
| 配置/存在/佈局 | 控制輸出是單一面板還是編頁。 |
| config/present/pdf/compression/level | 指定生成PDF文檔時要使用的壓縮程度。 |
| config/present/pdf/scriptModel | 控制輸出PDF文檔中是否包含XFA特定資訊。 |
| config/present/common/data/adjustData | 控制XFA應用程式在合併後是否調整資料。 |
| config/present/pdf/renderPolicy | 控制頁面內容的產生是在伺服器上完成，還是延遲至用戶端。 |
| config/present/common/locale | 指定輸出文檔中使用的預設區域設定。 |
| 設定/存在/目的地 | 當包含在當前元素中時，指定輸出格式。 當openAction元素包含時，指定在互動式客戶端中開啟文檔時要執行的操作。 |
| config/present/output/type | 指定要應用於檔案的壓縮類型或要生成的輸出類型。 |
| config/present/common/temp/uri | 指定表單URI。 |
| config/present/common/template/base | 在表單設計中為URI提供基本位置。 當此元素不存在或為空時，表單設計的位置將用作基礎。 |
| config/present/common/log/to | 控制日誌資料或輸出資料寫入的位置。 |
| config/present/output/to | 控制日誌資料或輸出資料寫入的位置。 |
| config/present/script/currentPage | 指定開啟文檔時的初始頁。 |
| config/present/script/exclude | 通知AEM Forms伺服器/通訊API要忽略哪些事件。 |
| config/present/pdf/line化 | 控制輸出PDF文檔是否被線性化。 |
| config/present/script/runScripts | 控制AEM Forms執行的指令碼集。 |
| config/present/pdf/tagged | 控制在輸出PDF文檔中包含標籤。 在PDF的上下文中，標籤是文檔中包含的用於公開文檔的邏輯結構的附加資訊。 標籤有助於輔助工具和重新格式化。 例如，頁碼可以被標籤為工件，這樣螢幕閱讀器就不會在文本的中間發出它。 雖然標籤使文檔更有用，但它們也會增加文檔的大小和處理時間以建立文檔。 |
| config/present/pdf/version | 指定要生成的PDF文檔的版本。 |
