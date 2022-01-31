---
title: '已知問題 '
description: 通信最佳做法、已知問題和限制
source-git-commit: c38a34519822449ff2577a9474b1294d5d45d3ae
workflow-type: tm+mt
source-wordcount: '1666'
ht-degree: 0%

---


# 考慮已知問題和最佳做法 {#best-practices-known-issues-and-limitations}

在開始使用通信API之前，請查看以下注意事項、已知問題和常見問題：

## 注意事項  {#considerations-for-communications-apis}

### 表單資料 {#form-data}

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

### 支援的文檔類型 {#supported-document-types}

要完全訪問通信API的呈現功能，建議使用XDP檔案作為輸入。 有時，可以使用PDF檔案。 但是，將PDF檔案用作輸入有以下限制：

不包含XFA流的PDF文檔不能呈現為PostScript、PCL或ZPL。 通信API可以將具有XFA流（即在設計器中建立的表單）的PDF文檔呈現為雷射和標籤格式。 如果PDF文檔已簽名、認證或包含使用權限(使用AEM FormsReader擴展服務應用)，則無法將其呈現為這些打印格式。


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


## 已知問題

* 在打印選項清單中，只能使用一次特定的渲染類型(PDF、打印)。 例如，不能有兩個PRINT選項，每個選項都指定PCL呈現類型。

* 對於批配置，只有OutputType(PDF、打印)和RenderType（PostScript、PCL、IPL、ZPL等）值組合的一個實例 的子菜單。

## 最佳作法

* Adobe建議在AEM Cloud Service使用的雲區域中托管資料檔案blob容器儲存。

## 常見問題 {#faq}

**是否可以使用監視資料夾或其他儲存機制來儲存輸入和輸出？**

目前，您可以使用MicrosoftAzure儲存來保存輸入資料和生成的文檔。 MicrosoftAzure儲存提供多種選項 [自動化資料移動操作](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10)。

**是否包含MicrosoftAzure儲存帳戶與Experience Manager FormsCloud Service許可證？**

MicrosoftAzure儲存帳戶獨立於Experience Manager FormsCloud Service許可證。

**通信API是否在Experience Manager FormsCloud Service伺服器上儲存資料？**

輸入和輸出資料僅保存在MicrosoftAzure儲存上。

**通信API是否僅可用於Experience Manager FormsCloud Service? 是否可以在內部環境中獲得類似的功能？**

您可以使用AEM Forms輸出服務將模板(XFA或PDF)與客戶資料組合，以PDF、PS、PCL和ZPL格式生成文檔。

與現場環境相比，該Cloud Service還提供了自動擴展和成本效益的額外優勢。

<!--**Where is data processed?**

**Who has access to data?**

**Is data encrypted?**

**Where is data hosted?** -->

**是否可以同時運行多個批處理操作？**
是，您可以簡單地運行多個批處理工序。 始終對每個操作使用不同的源資料夾和目標資料夾以避免任何衝突。
