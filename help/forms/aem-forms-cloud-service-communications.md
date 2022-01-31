---
title: AEM Formsas a Cloud Service — 通信
description: 自動將資料與XDP和PDF模板合併，或以PCL、ZPL和PostScript格式生成輸出
exl-id: 9fa9959e-b4f2-43ac-9015-07f57485699f
source-git-commit: ed46b0be25dabcea69be29e54000a4eab55e2836
workflow-type: tm+mt
source-wordcount: '2250'
ht-degree: 0%

---


# 使用AEM Formsas a Cloud Service通信API {#frequently-asked-questions}

**通信功能為beta。**

通信API可幫助您將XDP模板、基於XDP的PDF文檔和Acrobat·Forms(AcroForm)與XML資料相結合，以生成各種格式的打印文檔，並使您能夠建立應用程式，以便您：

- 使用 XML 資料填寫範本檔案來產生文件。

- 以各種格式生成表單，包括非互動式PDF打印流。

- 從 XFA 表單 PDF 產生列印 PDF。

- 通過將多組資料與源模板合併，批量生成PDF、PostScript、PCL和ZPL文檔。

請考慮一個方案，其中每個模板有一個或多個模板和多個XML資料記錄。 可以使用Communications API為每條記錄生成打印文檔。 <!-- You can also combine the records into a single document. --> 結果是非互動式PDF文檔。 非互動式PDF文檔不允許用戶在其欄位中輸入資料。

的 [API參考文檔](https://documentcloud.adobe.com/link/track?uri=urn:aaid:scds:US:b1223732-ae0f-4921-bdc0-c31e48b56044) 提供了有關所有API、參數、驗證方法以及API提供的各種服務的詳細資訊。 API參考文檔也以.yaml格式提供。 您可以下載.yaml [批處理API](assets/batch-api.yaml) 或 [非批處理API.yaml](assets/non-batch-api.yaml) 檔案並上傳給郵遞員，以檢查API的功能。

>[!VIDEO](https://video.tv.adobe.com/v/335771)

將通信API .yaml檔案上載到郵遞員以檢查API的功能。

>[!NOTE]
>
>只有表單用戶組的成員才能訪問通信API。

## 啟用通信

要為您的Formsas a Cloud Service環境啟用通信：

1. 登錄到雲管理器並開啟您的AEM Formsas a Cloud Service實例。

1. 開啟「編輯程式」選項，轉到「解決方案和載入項」頁籤，然後選擇 **[!UICONTROL Forms — 通信]** 的雙曲餘切值。

   <!-- ![Communications](assets\communications.png)

    If you have already enabled the **[!UICONTROL Forms - Digital Enrollment]** option, then select the **[!UICONTROL Forms - Communications Add-On]** option.  

    <!-- ![Addon](assets\add-on.png) -->

1. 按一下 **[!UICONTROL 更新]**。

1. 運行生成管道。

生成管道成功後，將為您的環境啟用通信API。

## 使用通信API {#workflows}

通常，您使用 [設計師](use-forms-designer.md) 並使用通信API:

- 將這些模板轉換為各種格式，包括PDF、PostScript、ZPL和PCL。
- 將XML表單資料與表單設計合併以生成文檔。
- 生成文檔，而不將XML表單資料合併到文檔中。 但是，主工作流正在將資料合併到文檔中。

然後，將輸出文檔儲存到檔案。 您可以設計自定義工作流，將檔案發送到網路打印機、本地打印機或儲存系統進行存檔。 典型的開箱即用工作流和自定義工作流如下所示：

![通信工作流](assets/communicaions-workflow.png)

### 建立PDF文檔 {#create-pdf-documents}

您可以使用 _生成PDFOutput_ API，用於建立基於表單設計和XML表單資料的PDF文檔。 輸出是非互動式PDF文檔。 即用戶不能輸入或修改表單資料。 基本工作流是將XML表單資料與表單設計合併，以建立PDF文檔。 下圖顯示了表單設計與XML表單資料的合併，以生成PDF文檔。

![建立PDF文檔](assets/outPutPDF_popup.png)

### 建立PostScript(PS)、打印機命令語言(PCL)、Zebra打印語言(ZPL)文檔 {#create-PS-PCL-ZPL-documents}

您可以使用Communications API建立基於XDP表單設計或PDF文檔的PostScript(PS)、打印機命令語言(PCL)和Zebra打印語言(ZPL)文檔。 的 _generatePrintedOutput_ API將表單設計與表單資料合併以生成文檔。 您可以將文檔保存到檔案中，並開發自定義流程以將其發送到打印機。

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

- 互動式PDF文檔在設計器中建立（包含XFA流）。

- AcrobatPDF forms

如果嘗試拼合非互動式PDF文檔，則會發生異常。

### 保留窗體狀態 {#retain-form-state}

互動式PDF文檔包含構成表單的各種元素。 這些元素可包括欄位（接受或顯示資料）、按鈕（觸發事件）和指令碼（執行特定操作的命令）。 按一下按鈕可觸發更改欄位狀態的事件。 例如，選擇性別選項可能會更改欄位的顏色或表單的外觀。 這是導致窗體狀態更改的手動事件的示例。

當使用通信API平展這種互動式PDF文檔時，不保留表單的狀態。 要確保即使在平展表單後仍保留表單的狀態，請設定布爾值 _retainFormState_ 為True以保存和保留窗體的狀態。

### 通信API的注意事項 {#considerations-for-communications-apis}

#### 表單資料 {#form-data}

通信API接受通常在設計器中建立的表單設計和作為輸入的XML表單資料。 要用資料填充文檔，XML元素必須存在於要填充的每個表單域的XML表單資料中。 XML元素名稱必須與欄位名稱匹配。 如果XML元素與表單域不對應，或XML元素名稱與欄位名稱不匹配，則忽略該元素。 不必與XML元素的顯示順序匹配。 重要因素是XML元素是用相應的值指定的。

請考慮以下貸款申請表示例：

![貸款申請表](assets/loanFormData.png)

要將資料合併到此表單設計中，請建立與表單對應的XML資料源。 以下XML表示與示例抵押申請表單對應的XML資料源。

```XML
<?xml version="1.0" encoding="UTF-8" ?>
- <xfa:datasets xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/">
- <xfa:data>
- <data>
    - <Layer>
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
    - <Mortgage>
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

#### 支援的文檔類型 {#supported-document-types}

要完全訪問通信API的呈現功能，建議使用XDP檔案作為輸入。 在某些情況下，可以使用PDF檔案。 但是，將PDF檔案用作輸入具有以下限制：

- 不包含XFA流的PDF文檔不能呈現為PostScript、PCL或ZPL。 通信API可以將具有XFA流（即在設計器中建立的表單）的PDF文檔呈現為雷射和標籤格式。 如果PDF文檔已簽名、認證或包含使用權限(使用AEM FormsReader擴展服務應用)，則無法將其呈現為這些打印格式。

<!-- * Run-time options such as PDF version and tagged PDF are not supported for Acrobat forms. They are valid for PDF forms that contain XFA streams; however, these forms cannot be signed or certified. 

#### Email support {#email-support}

For email functionality, you can create a process in AEM Workflows that uses the Email Step. A workflow represents a business process that you are automating. -->

#### 可打印區域 {#printable-areas}

預設的0.25英吋不可打印邊距對於標籤打印機不準確，因打印機和打印機以及標籤大小和標籤大小而異。 建議您保持0.25英吋的邊距或減小它。 但是，建議不要增加不可打印的邊距。 否則，可打印區域中的資訊無法正確打印。

始終確保為打印機使用正確的XDC檔案。 例如，請避免為300 dpi打印機選擇XDC檔案，並將文檔發送到200 dpi打印機。

#### 指令碼 {#scripts}

與Communications API一起使用的表單設計可以包含在伺服器上運行的指令碼。 確保表單設計不包含在客戶端上運行的指令碼。 有關建立表單設計指令碼的資訊，請參閱設計器幫助。

<!-- #### Working with Fonts
 Document Considerations for Working with Fonts>> -->

#### 字型映射 {#font-mapping}

如果在客戶端電腦上安裝了字型，則字型可在設計器的下拉清單中使用。 如果未安裝字型，則需要手動指定字型名稱。 Designer中的「永久替換不可用字型」選項可關閉。 否則，當XDP檔案保存在Designer中時，替代字型名稱將寫入XDP檔案。 這表示不使用打印機駐留字型。

要設計使用打印機駐留字型的表單，請在設計器中選擇與打印機上可用字型匹配的字型名稱。 PCL或PostScript支援的字型清單位於相應的設備配置檔案（XDC檔案）中。 或者，可以建立字型映射以將非打印機駐留字型映射到不同字型名稱的打印機駐留字型。 例如，在PostScript方案中，對Arial®字型的引用可以映射到駐留在打印機上的Helvetica®字型。

存在兩種類型的OpenType®字型。 一種類型是PCL支援的TrueTypeOpenType®字型。 另一個是CFFOpenType®。 PDF和PostScript輸出支援嵌入的Type-1、TrueType和OpenType®字型。 PCL輸出支援嵌入式TrueType字型。

Type-1和OpenType®字型未嵌入PCL輸出。 使用Type-1和OpenType®字型格式化的內容將被柵格化並生成為點陣圖影像，該點陣圖影像可以大而慢，以便生成。

生成PostScript、PCL或PDF輸出時，下載或嵌入的字型將自動替換。 這意味著只有正確呈現生成的文檔所需的字型字形子集才會包含在生成的輸出中。

#### 使用設備配置檔案（XDC檔案） {#working-with-xdc-files}

設備配置檔案（XDC檔案）是XML格式的打印機描述檔案。 此檔案使Communications API能夠將文檔輸出為雷射或標籤打印機格式。 通信API使用XDC檔案，包括：

- hppcl5c.xdc

- hppcl5e.xdc

- ps_plain_level3.xdc

- ps_plain.xdc

- zpl300.xdc

- zpl600.xdc

- zpl300.xdc

- ipl300.xdc

- ipl400.xdc

- tpcl600.xdc

- dpl300.xdc

- dpl406.xdc

- dpl600.xdc

無需修改這些檔案即可建立文檔。 但是，您可以修改它們以滿足您的業務要求。

這些檔案是支援特定打印機功能的XDC檔案示例，如駐留字型、紙盒和訂書機。 這些示例的目的是幫助您瞭解如何使用設備配置檔案設定自己的打印機。 這些示例也是同一產品系列中類似打印機的起點。

#### 使用XCI配置檔案 {#working-with-xci-files}

通信API使用XCI配置檔案來執行任務，例如控制輸出是單個面板還是分頁。 儘管此檔案包含可設定的設定，但修改此值並非典型情況。 <!-- The default.xci file is located in the svcdata\XMLFormService folder. -->

可以使用Communications API傳遞修改的XCI檔案。 執行此操作時，建立預設檔案的副本，僅更改需要修改以滿足業務要求的值，並使用修改的XCI檔案。

通信API以預設XCI檔案（或修改的檔案）開頭。 然後，它應用使用通信API指定的值。 這些值會覆蓋XCI設定。

下表指定了XCI選項。

| XCI選項 | 說明 |
| ------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
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

<!-- Using API

 There are two main Communications APIs. The _generatePDFOutput_ generates PDFs, while the _generatePrintedOutput_ generates PostScript, ZPL, and PCL formats. These APIs are available as HTTP endpoints on your environment, both on author and publish instances. Since the publish instances are configured to scale faster than the author instances, it is recommended use these APIs via publish instances.

The first parameter of both the operations accept the path and name of the template file (for example ExpenseClaim.xdp). You can specify a fully qualified path, reference path of your AEM Repository, or path of a binary file. The second parameter accepts an XML document that is merged with the template while generating the output document. -->
