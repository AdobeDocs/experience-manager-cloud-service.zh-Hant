---
title: AEM Forms中有哪些考量事項、已知問題和最佳實務？
description: AEM Forms Communication API的考量事項已知問題和最佳實務。
exl-id: e95615dd-e494-40cd-9cdf-6e9761ca3b3e
source-git-commit: 0f8aed76af4d2640094a76f2805f73a0a619e33f
workflow-type: tm+mt
source-wordcount: '1748'
ht-degree: 0%

---

# 考量已知問題和最佳實務 {#best-practices-known-issues-and-limitations}

開始使用通訊API之前，請檢閱下列考量事項、已知問題和常見問題：

## 考量事項  {#considerations-for-communications-apis}

### 表單資料 {#form-data}

Communications API接受通常以設計工具建立的表單設計和XML表單資料作為輸入。 若要在檔案中填入資料，XML元素必須存在於您要填入的每個表單欄位的XML表單資料中。 XML元素名稱必須符合欄位名稱。 如果XML元素未對應至表單欄位，或XML元素名稱不符合欄位名稱，則會忽略該元素。 不需要比對XML元素的顯示順序。 重要因素是XML元素是以對應的值指定的。

請考量下列範例貸款申請表單：

![貸款申請表](assets/loanFormData.png)

若要將資料合併至此表單設計，請建立與表單相對應的XML資料來源。 下列XML代表與範例抵押應用程式表單相對應的XML資料來源。

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

### 支援的檔案型別 {#supported-document-types}

若要完整存取Communications API的轉譯功能，建議您使用XDP檔案作為輸入。 有時可以使用PDF檔案。 不過，使用PDF檔案作為輸入有限制：

不包含XFA資料流的PDF檔案無法轉譯為PostScript、PCL或ZPL。 Communications API可將具有XFA串流（即在Designer中建立的表單）的PDF檔案轉譯為雷射影像和標籤格式。 如果PDF檔案經過簽署、認證或包含使用許可權(使用AEM FormsReader擴充功能服務套用)，將無法轉譯為上述列印格式。


### 可列印區域 {#printable-areas}

標籤印表機的預設0.25英吋不可列印邊界並不精確，而且會因印表機與印表機以及標籤大小而異，不過，建議您保留0.25英吋邊界或縮小邊界。 不過，建議您不要增加不可列印的邊界。 否則，可列印區域中的資訊無法正確列印。

請務必確保您使用印表機正確的XDC檔案。 例如，請避免為300 dpi印表機選擇XDC檔案，並將檔案傳送到200 dpi印表機。

### 僅適用於XFA表單的指令碼(XDP/PDF) {#scripts}

搭配Communications API使用的表單設計可以包含伺服器上執行的指令碼。 確認表單設計不包含在使用者端上執行的指令碼。 如需建立表單設計指令集的相關資訊，請參閱 [Designer說明](use-forms-designer.md).

<!-- #### Working with Fonts
 Document Considerations for Working with Fonts>> -->

### 字型對應 {#font-mapping}

若要設計使用印表機內建字型的表單，請在Designer中選擇符合印表機可用字型的字型名稱。 PCL或PostScript支援的字型清單位於對應的裝置設定檔（XDC檔案）中。 或者，也可以建立字型對映來將非印表機駐留字型對應到印表機駐留字型的不同字型名稱。 例如，在PostScript案例中，對Arial®字型的參照可以對應到印表機所在的Helvetica®字型。

如果字型已安裝在使用者端電腦上，則可在Designer的下拉式清單中找到它。 如果未安裝字型，則必須手動指定字型名稱。 Designer中的「永久取代無法使用的字型」選項可以關閉。 否則，當XDP檔案儲存在Designer中時，替代字型名稱會寫入XDP檔案。 這表示不使用印表機內建的字型。

OpenType有兩種型別®字型。 一種型別是PCL支援的TrueTypeOpenType®字型。 另一個是CFFOpenType®。 PDF和PostScript輸出支援內嵌Type-1、TrueType和OpenType®字型。 PCL輸出支援內嵌的TrueType字型。

Type-1和OpenType®字型未內嵌在PCL輸出中。 使用Type-1和OpenType®字型格式化的內容會點陣化並產生為點陣圖影像，其大小可能較大，產生速度可能較慢。

產生PostScript、PCL或PDF輸出時，下載或內嵌的字型會自動被取代。 這表示產生的輸出中只包含正確轉譯產生檔案所需的字型字元子集。

### 使用裝置設定檔（XDC檔案） {#working-with-xdc-files}

裝置設定檔（XDC檔案）是XML格式的印表機描述檔。 此檔案可讓Communications API以雷射或標籤印表機格式輸出檔案。 通訊API使用XDC檔案，包括下列專案：

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

您可以使用提供的XDC檔案來產生列印檔案，或依您的需求加以修改。
<!-- It is not necessary to modify these files to create documents. However, you can modify them to meet your business requirements. -->

這些檔案是支援特定印表機功能的參考XDC檔案，例如常駐字型、紙匣和裝訂器。 這些參考資料的目的是協助您瞭解如何使用裝置設定檔來設定您自己的印表機。 此參考也是相同產品線中類似印表機的起點。

### 使用XCI設定檔案 {#working-with-xci-files}

通訊API使用XCI設定檔案來執行工作，例如控制輸出是單一面板還是分頁。 雖然此檔案包含可設定的設定，但通常不會修改此值。 <!-- The default.xci file is located in the svcdata\XMLFormService folder. -->

您可以在使用Communications API時傳遞修改過的XCI檔案。 這樣做時，請建立預設檔案的副本，僅變更需要修改的值以滿足您的業務需求，並使用修改過的XCI檔案。

通訊API會以預設的XCI檔案（或修改的檔案）開始。 然後它會套用使用Communications API指定的值。 這些值會覆寫XCI設定。

下表指定XCI選項。

| XCI選項 | 說明 |
| ------------------------------------| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| config/present/pdf/creator | 使用檔案資訊字典中的建立者專案來識別檔案建立者。 如需此字典的相關資訊，請參閱PDF參考指南。 |
| config/present/pdf/producer | 使用檔案資訊字典中的製作者專案來識別檔案製作者。 如需此字典的相關資訊，請參閱PDF參考指南。 |
| config/present/layout | 控制輸出是單一面板還是分頁。 |
| config/present/pdf/compression/level | 指定產生PDF檔案時要使用的壓縮程度。 |
| config/present/pdf/scriptModel | 控制輸出PDF檔案中是否包含XFA特定資訊。 |
| config/present/common/data/adjustData | 控制XFA應用程式是否會在合併後調整資料。 |
| config/present/pdf/renderPolicy | 控制頁面內容的產生是在伺服器上完成，還是延後至使用者端。 |
| config/present/common/locale | 指定輸出檔案中使用的預設地區設定。 |
| config/present/destination | 當由目前元素包含時，指定輸出格式。 當由openAction元素包含時，會指定在互動式使用者端中開啟檔案時要執行的動作。 |
| config/present/output/type | 指定要套用至檔案的壓縮型別，或是要產生的輸出型別。 |
| config/present/common/temp/uri | 指定表單URI。 |
| config/present/common/template/base | 提供表單設計中基本的URI位置。 當此元素不存在或空白時，會使用表單設計的位置作為基礎。 |
| config/present/common/log/to | 控制記錄資料或輸出資料寫入的位置。 |
| config/present/output/to | 控制記錄資料或輸出資料寫入的位置。 |
| config/present/script/currentPage | 指定開啟檔案時的初始頁面。 |
| config/present/script/exclude | 通知AEM Forms伺服器/通訊API要忽略哪些事件。 |
| config/present/pdf/linearized | 控制是否將輸出PDF檔案線性化。 |
| config/present/script/runScripts | 控制AEM Forms要執行哪一組指令碼。 |
| config/present/pdf/tagged | 控制標籤在輸出PDF檔案中是否包含。 在PDF的內容中，標籤是包含在檔案中的其他資訊，用於公開檔案的邏輯結構。 標籤有助於協助協助工具及重新格式化。 例如，頁碼可能會被標籤為成品，這樣熒幕閱讀器就不會在文字中間朗讀它。 雖然標籤讓檔案變得更實用，但它們也會增加檔案的大小，以及建立檔案的處理時間。 |
| config/present/pdf/version | 指定要產生的PDF檔案版本。 |


## 已知問題

* 您只能在列印選項清單中使用一次特定的轉譯型別(PDF、列印)。 例如，不能有兩個PRINT選項，每個選項都指定PCL演算型別。

* 對於批次設定，只允許一個OutputType (PDF、列印)和RenderType （PostScript、PCL、IPL、ZPL等）值組合的執行個體。

* 對於非同步API （批次處理），預設記錄層級設定為2。 您可以使用自訂XCI將記錄層級變更為1。

* 設定預設的XCI時，會包含直到原始轉譯的路徑。 例如 `/content/dam/formsanddocuments/default.xci/jcr:content/renditions/original`



## 最佳做法

* Adobe建議將資料檔案blob容器存放區託管在AEM Cloud Service使用的雲端區域。

## 常見問題 {#faq}

**我可以使用watched資料夾或其他儲存機制來儲存輸入和輸出嗎？**

目前，您可以使用Microsoft Azure Storage來儲存輸入資料和產生的檔案。 Microsoft Azure儲存體提供各種選項來 [自動化資料移動作業](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10).

**Experience Manager FormsCloud Service授權是否包含Microsoft Azure儲存體帳戶？**

Microsoft Azure儲存體帳戶獨立於Experience Manager FormsCloud Service授權。

**通訊API會將資料儲存在Experience Manager FormsCloud Service伺服器上嗎？**

輸入和輸出資料僅儲存在Microsoft Azure Storage上。

**通訊API是否僅適用於Experience Manager FormsCloud Service？ 我可以在內部部署環境中取得類似功能嗎？**

您可以使用AEM Forms Output服務將範本(XFA或PDF)與客戶資料結合，以產生PDF、PS、PCL和ZPL格式的檔案。

相較於內部部署環境，該Cloud Service提供自動擴充及成本效益的額外優點。

<!--**Where is data processed?**

**Who has access to data?**

**Is data encrypted?**

**Where is data hosted?** -->

**我可以同時執行多個批次作業嗎？**
可以，您可以同時執行多個批次作業。 每次作業一律使用不同的來源和目的地資料夾，以避免任何衝突。

>[!MORELIKETHIS]
>
>* [AEM Formsas a Cloud Service通訊簡介](/help/forms/aem-forms-cloud-service-communications-introduction.md)
>* [最適化Forms的AEM Formsas a Cloud Service架構和通訊API](/help/forms/aem-forms-cloud-service-architecture.md)
>* [通訊處理 — 同步API](/help/forms/aem-forms-cloud-service-communications.md)
>* [通訊處理 — 批次API](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)

