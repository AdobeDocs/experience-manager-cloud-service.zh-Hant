---
title: AEM Formsas a Cloud Service — 通訊
description: 自動將資料與XDP和PDF模板合併，或以PCL、ZPL和PostScript格式生成輸出
exl-id: 9fa9959e-b4f2-43ac-9015-07f57485699f
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '2372'
ht-degree: 0%

---


# 使用AEM Formsas a Cloud Service通訊API {#frequently-asked-questions}

**通訊功能正在測試中。**

通信API可幫助您將XDP模板、基於XDP的PDF文檔和Acrobat Forms(AcroForm)與XML資料結合，以生成各種格式的打印文檔，並使您能夠建立應用程式，以便您：

- 使用XML資料填入範本檔案，以產生檔案。

- 以各種格式產生表單，包括非互動式PDF列印資料流。

- 從XFA表單PDF產生列印PDF。

- 將多組資料與源模板合併，以批量生成PDF、PostScript、PCL和ZPL文檔。

假設您有一或多個範本，以及每個範本的多個XML資料記錄。 您可以使用通信API為每條記錄生成打印文檔。 <!-- You can also combine the records into a single document. --> 結果是非互動式PDF檔案。 非互動式PDF檔案不會讓使用者在其欄位中輸入資料。

此 [API參考檔案](https://documentcloud.adobe.com/link/track?uri=urn:aaid:scds:US:b1223732-ae0f-4921-bdc0-c31e48b56044) 提供有關API所提供所有API、參數、驗證方法和各種服務的詳細資訊。 API參考檔案也提供.yaml格式。 您可以下載.yaml [批次API](assets/batch-api.yaml) 或 [非批次API.yaml](assets/non-batch-api.yaml) 檔案並上傳至postman以檢查API的功能。

>[!VIDEO](https://video.tv.adobe.com/v/335771)

將通訊API .yaml檔案上傳至postman以檢查API的功能。

>[!NOTE]
>
>只有表單使用者群組的成員才能存取通訊API。

## 啟用通訊

若要啟用Formsas a Cloud Service環境的通訊：

1. 登入Cloud Manager並開啟AEM Formsas a Cloud Service例項。

1. 開啟「編輯方案」選項，前往「解決方案與附加元件」標籤，然後選取 **[!UICONTROL Forms — 通訊]** 選項。

   <!-- ![Communications](assets\communications.png)

    If you have already enabled the **[!UICONTROL Forms - Digital Enrollment]** option, then select the **[!UICONTROL Forms - Communications Add-On]** option.  

    <!-- ![Addon](assets\add-on.png) -->

1. 按一下 **[!UICONTROL 更新]**.

1. 執行建置管道。

建置pipleine成功後，即會為您的環境啟用通訊API。

## 使用通訊API {#workflows}

通常，您使用 [設計工具](use-forms-designer.md) 和使用通訊API來：

- 將這些模板轉換為各種格式，包括PDF、PostScript、ZPL和PCL。
- 將XML表單資料與表單設計合併，以生成文檔。
- 生成文檔，而不將XML表單資料合併到文檔中。 但是，主要工作流正在將資料合併到文檔中。

然後，將輸出文檔儲存到檔案中。 您可以設計自定義工作流，將檔案發送到網路打印機、本地打印機或儲存系統進行存檔。 典型的現成可用和自訂工作流程如下所示：

![通訊工作流程](assets/communicaions-workflow.png)

### 建立PDF文檔 {#create-pdf-documents}

您可以使用 _generatePDFOutput_ API，以建立以表單設計和XML表單資料為基礎的PDF檔案。 輸出是非互動式PDF檔案。 也就是說，用戶不能輸入或修改表單資料。 基本的工作流是將XML表單資料與表單設計合併，以建立PDF文檔。 下圖顯示表單設計與XML表單資料的合併，以產生PDF檔案。

![建立PDF文檔](assets/outPutPDF_popup.png)

### 建立PostScript(PS)、打印機命令語言(PCL)、Zebra打印語言(ZPL)文檔 {#create-PS-PCL-ZPL-documents}

您可以使用通信API來建立基於XDP表單設計或PDF文檔的PostScript(PS)、打印機命令語言(PCL)和Zebra打印語言(ZPL)文檔。 此 _generatePrintedOutput_ API將表單設計與表單資料合併，以產生檔案。 您可以將檔案儲存至檔案，並開發自訂程式以將其傳送至印表機。

<!-- ### Processing batch data to create multiple documents

Communications APIs can create separate documents for each record within an XML batch data source. The APIs can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you instruct the APIs to create a separate document for each record (for example, PDF documents). As a result, the APIs generate ten PDF documents.

The following illustration also shows Communications APIs processing an XML data file that contains multiple records. However, assume that you instruct the APIs to create a single PDF document that contains all data records. In this situation, the APIs generate one document that contains all of the records.

The following illustration shows Communications APIs processing an XML data file that contains multiple records. Assume that you instruct the Communications APIs to create a separate PDF document for each data record. In this situation, the APIs generates a separate PDF document for each data record.

 -->

### 處理批資料以建立多個文檔 {#processing-batch-data-to-create-multiple-documents}

您可以為XML批資料源內的每個記錄建立單獨的文檔。 您可以以批量和非同步模式生成文檔。 您可以為轉換設定各種參數，然後開始批次處理。 <!-- You can can also create a single document that contains all records (this functionality is the default).  Assume that an XML data source contains ten records and you have a requirement to create a separate document for each record (for example, PDF documents). You can use the Communication APIs to generate ten PDF documents. -->

<!-- The following illustration shows the Communication APIs processing an XML data file that contains multiple records. However, assume that you instruct the Communication APIs to create a single PDF document that contains all data records. In this situation, the Communication APIs generate one document that contains all of the records.

![Create PDF Documents](assets/ou_OutputBatchSingle_popup.png)

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. Assume that you instruct the Communication APIs to create a separate PDF document for each data record. In this situation, the Communication APIs generates a separate PDF document for each data record.

![Create PDF Documents](assets/ou_OutputBatchMany_popup.png)

For detailed information on using Batch APIs, see Communication APIs: Processing batch data to create multiple documents. -->

### 平面化互動式PDF檔案 {#flatten-interactive-pdf-documents}

您可以使用通訊API將互動式PDF檔案（例如表單）轉換為非互動式PDF檔案。 互動式PDF檔案可讓使用者輸入或修改位於PDF檔案欄位中的資料。 將互動式PDF文檔轉換為非互動式PDF文檔的過程稱為拼合。 平面化PDF文檔時，用戶無法修改位於文檔欄位中的資料。 平面化PDF檔案的一個原因是為了確保資料無法修改。

您可以平面化下列類型的PDF檔案：

- 在Designer中建立的互動式PDF檔案（包含XFA資料流）。

- AcrobatPDF forms

如果您嘗試平面化非互動式PDF檔案，會發生例外狀況。

### 保留表單狀態 {#retain-form-state}

互動式PDF檔案包含構成表單的各種元素。 這些元素可以包括欄位（接受或顯示資料）、按鈕（觸發事件）和指令碼（執行特定操作的命令）。 按一下按鈕可觸發變更欄位狀態的事件。 例如，選擇性別選項可能會變更欄位的顏色或表單外觀。 這是導致表單狀態變更的手動事件範例。

使用通訊API扁平化此類互動式PDF檔案時，不會保留表單的狀態。 若要確保在表單平面化後仍會保留表單的狀態，請設定布林值 _retainFormState_ 設為True以儲存及保留表單的狀態。

### 通訊API的考量事項 {#considerations-for-communications-apis}

#### 表單資料 {#form-data}

通信API接受通常在設計工具中建立的表單設計和作為輸入的XML表單資料。 要用資料填充文檔，要填充的每個表單欄位的XML表單資料中必須存在XML元素。 XML元素名稱必須與欄位名稱相符。 如果XML元素與表單欄位不對應，或XML元素名稱與欄位名稱不匹配，則會忽略該元素。 不需要匹配XML元素的顯示順序。 重要因素是XML元素需指定相應的值。

請考量下列貸款申請表範例：

![貸款申請表](assets/loanFormData.png)

要將資料合併到此表單設計中，請建立與表單對應的XML資料源。 以下XML表示與抵押申請表示例對應的XML資料源。

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

若要完整存取通訊API的轉譯功能，建議您使用XDP檔案作為輸入。 在某些情況下，可使用PDF檔案。 不過，使用PDF檔案作為輸入有下列限制：

- 不包含XFA資料流的PDF文檔無法呈現為PostScript、PCL或ZPL。 通訊API可將具有XFA資料流（即在Designer中建立的表單）的PDF檔案轉譯為雷射和標籤格式。 如果PDF檔案經過簽署、認證或包含使用權限(使用AEM FormsReader擴充功能服務套用)，則無法以這些列印格式呈現。

<!-- * Run-time options such as PDF version and tagged PDF are not supported for Acrobat forms. They are valid for PDF forms that contain XFA streams; however, these forms cannot be signed or certified. 

#### Email support {#email-support}

For email functionality, you can create a process in AEM Workflows that uses the Email Step. A workflow represents a business process that you are automating. -->

#### 可列印區域 {#printable-areas}

標籤打印機的預設0.25英吋不可打印邊距不精確，因打印機和打印機而異，從標籤大小到標籤大小不等。 建議您保持0.25英吋的邊距或將其縮小。 不過，建議您不要增加不可列印的邊界。 否則，可打印區域中的資訊無法正確打印。

請務必為打印機使用正確的XDC檔案。 例如，請避免為300-dpi打印機選擇XDC檔案，並將文檔發送到200-dpi打印機。

#### 指令碼 {#scripts}

與通訊API搭配使用的表單設計可包含在伺服器上執行的指令碼。 確保表單設計不包含在用戶端上執行的指令碼。 有關建立表單設計指令碼的資訊，請參閱設計工具幫助。

<!-- #### Working with Fonts
 Document Considerations for Working with Fonts>> -->

#### 字型對應 {#font-mapping}

如果字型安裝在客戶端電腦上，該字型可在Designer的下拉清單中使用。 如果未安裝字型，則需要手動指定字型名稱。 Designer中的「永久替換不可用的字型」選項可以關閉。 否則，當XDP檔案保存在Designer中時，替代字型名稱將寫入XDP檔案。 這表示未使用打印機駐留字型。

要設計使用打印機駐留字型的表單，請在「設計器」中選擇與打印機上可用字型相匹配的字型名。 PCL或PostScript支援的字型清單位於相應的設備配置檔案（XDC檔案）中。 或者，可以建立字型映射以將非打印機駐留字型映射到不同字型名稱的打印機駐留字型。 例如，在PostScript方案中，對Arial®字型的引用可以映射到駐留在打印機上的Helvetica®字型。

有兩種OpenType®字型。 一種類型是PCL支援的TrueTypeOpenType®字型。 二是CFFOpenType®。 PDF和PostScript輸出支援嵌入的Type-1、TrueType和OpenType®字型。 PCL輸出支援嵌入的TrueType字型。

Type-1和OpenType®字型未嵌入到PCL輸出中。 使用Type-1和OpenType®字型格式化的內容被柵格化並生成為點陣圖影像，該影像可能大而慢而難以生成。

在生成PostScript、PCL或PDF輸出時，下載或嵌入的字型會自動替換。 這意味著，在生成的輸出中只包含正確呈現生成的文檔所需的字型字形子集。

#### 使用裝置設定檔檔案（XDC檔案） {#working-with-xdc-files}

設備配置檔案（XDC檔案）是XML格式的打印機描述檔案。 此檔案可讓通訊API以雷射或標籤打印機格式輸出文檔。 通訊API使用XDC檔案，包括：

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

不需要修改這些檔案來建立文檔。 但是，您可以修改它們以符合您的業務需求。

這些檔案是支援特定打印機功能的示例XDC檔案，如駐留字型、紙盤和訂書機。 這些示例旨在幫助您了解如何使用設備配置檔案來設定您自己的打印機。 這些樣本也是同一生產線中類似打印機的起點。

#### 使用XCI設定檔案 {#working-with-xci-files}

通訊API使用XCI設定檔案來執行工作，例如控制輸出是單一面板或編頁。 雖然此檔案包含可設定的設定，但修改此值並非典型值。 <!-- The default.xci file is located in the svcdata\XMLFormService folder. -->

您可以在使用通訊API時傳遞修改的XCI檔案。 執行此操作時，請建立預設檔案的副本，僅更改需要修改以滿足您的業務需求的值，然後使用修改的XCI檔案。

通訊API以預設XCI檔案（或修改的檔案）開頭。 然後會套用使用通訊API指定的值。 這些值會覆寫XCI設定。

下表指定XCI選項。

| XCI選項 | 說明 |
| ------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
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

### 已知問題

- 請確定範本和XCI組態檔的大小大於16KB。

- 確保資料xml檔案不包含XML聲明標頭。 例如， `<?xml version="1.0" encoding="UTF-8"?>`

- 對於批配置，只有一個實例，其中包含OutputType(PDF、打印)和RenderType（PostScript、PCL、IPL、ZPL等）值的組合 中指定的規則。

- 運行批處理時，請勿修改批處理配置中使用的資料源USC配置/Azure雲配置。 即使在執行後，如果需要任何更新，請建立配置副本，而不是更新現有批配置中使用的配置副本。

### 最佳作法

- Adobe建議將資料檔案blob容器存放在AEM Cloud Service使用的雲端地區。

<!-- Using API

 There are two main Communications APIs. The _generatePDFOutput_ generates PDFs, while the _generatePrintedOutput_ generates PostScript, ZPL, and PCL formats. These APIs are available as HTTP endpoints on your environment, both on author and publish instances. Since the publish instances are configured to scale faster than the author instances, it is recommended use these APIs via publish instances.

The first parameter of both the operations accept the path and name of the template file (for example ExpenseClaim.xdp). You can specify a fully qualified path, reference path of your AEM Repository, or path of a binary file. The second parameter accepts an XML document that is merged with the template while generating the output document. -->


