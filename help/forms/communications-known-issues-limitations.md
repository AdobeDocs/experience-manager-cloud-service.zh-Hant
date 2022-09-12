---
title: 已知問題的考量事項和最佳實務
description: 通訊最佳實務、已知問題和限制
exl-id: e95615dd-e494-40cd-9cdf-6e9761ca3b3e
source-git-commit: 4b76fbbb1b58324065b39d6928027759b0897246
workflow-type: tm+mt
source-wordcount: '1707'
ht-degree: 0%

---

# 已知問題的考量事項和最佳實務 {#best-practices-known-issues-and-limitations}

開始使用通訊API之前，請先檢閱下列考量事項、已知問題和常見問題：

## 考量事項  {#considerations-for-communications-apis}

### 表單資料 {#form-data}

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

### 支援的文檔類型 {#supported-document-types}

若要完整存取通訊API的轉譯功能，建議您使用XDP檔案作為輸入。 有時可使用PDF檔案。 不過，使用PDF檔案作為輸入有以下限制：

不包含XFA資料流的PDF文檔無法呈現為PostScript、PCL或ZPL。 通訊API可將具有XFA資料流（即在Designer中建立的表單）的PDF檔案轉譯為雷射和標籤格式。 如果PDF檔案經過簽署、認證或包含使用權限(使用AEM FormsReader擴充功能服務套用)，則無法以這些列印格式呈現。


### 可列印區域 {#printable-areas}

標籤打印機的預設0.25英吋不可打印邊距不精確，因打印機、打印機、標籤大小和標籤大小而異，但建議您保持0.25英吋邊距或將其縮小。 不過，建議您不要增加不可列印的邊界。 否則，可打印區域中的資訊無法正確打印。

請務必為打印機使用正確的XDC檔案。 例如，請避免為300-dpi打印機選擇XDC檔案，並將文檔發送到200-dpi打印機。

### 僅限XFA表單(XDP/PDF)的指令碼 {#scripts}

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
<!-- It is not necessary to modify these files to create documents. However, you can modify them to meet your business requirements. -->

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


## 已知問題

* 打印選項清單中只能使用一次特定的渲染類型(PDF、打印)。 例如，不能有兩個PCL呈現類型的PRINT選項。

* 對於批配置，只有一個實例，其中包含OutputType(PDF、打印)和RenderType（PostScript、PCL、IPL、ZPL等）值的組合 中指定的規則。

* 對於非同步API（批次處理），預設記錄層級設為2。 您可以使用自訂XCI將記錄層級變更為1。

* 設定預設XCI時，其包含的路徑直到原始轉譯。 例如 `/content/dam/formsanddocuments/default.xci/jcr:content/renditions/original`



## 最佳作法

* Adobe建議將資料檔案blob容器存放在AEM Cloud Service使用的雲端地區。

## 常見問題 {#faq}

**我可以使用觀看的資料夾或其他儲存機制來儲存輸入和輸出嗎？**

目前，您可以使用Microsoft Azure Storage來儲存輸入資料和產生的檔案。 Microsoft Azure儲存提供 [自動化資料移動操作](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10).

**Microsoft Azure儲存帳戶是否隨Experience Manager FormsCloud Service授權包含？**

Microsoft Azure儲存帳戶獨立於Experience Manager FormsCloud Service授權。

**通訊API會將資料儲存在Experience Manager FormsCloud Service伺服器上嗎？**

輸入和輸出資料僅儲存在Microsoft Azure儲存上。

**通訊API是否僅適用於Experience Manager FormsCloud Service? 我可以在內部部署環境中取得類似的功能嗎？**

您可以使用AEM Forms輸出服務將範本(XFA或PDF)與客戶資料結合，以PDF、PS、PCL和ZPL格式產生檔案。

與內部部署環境相比，本Cloud Service可提供自動擴展和成本效益的額外優勢。

<!--**Where is data processed?**

**Who has access to data?**

**Is data encrypted?**

**Where is data hosted?** -->

**我可以同時執行多個批處理操作嗎？**
是的，您可以簡單地運行多個批處理操作。 請始終對每個操作使用不同的源資料夾和目標資料夾，以避免任何衝突。
