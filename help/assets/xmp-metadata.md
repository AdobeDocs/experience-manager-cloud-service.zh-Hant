---
title: XMP 中繼資料
description: 瞭解XMP（可擴充中繼資料平台）中繼資料管理標準。 AEM將它當做建立、處理和交換中繼資料的標準格式。
contentOwner: AG
translation-type: tm+mt
source-git-commit: b0436c74389ad0b3892d1258d993c00aa470c3ab
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 20%

---


# XMP 中繼資料 {#xmp-metadata}

XMP（可擴充中繼資料平台）是AEM Assets用於所有中繼資料管理的中繼資料標準。 XMP提供標準格式，讓您針對多種應用程式建立、處理和交換中繼資料。

除了提供可嵌入所有檔案格式的通用中繼資料編碼外，XMP還提供多樣化的 [內容模型](#xmp-core-concepts) ，並受 [Adobe](#advantages-of-xmp) 和其他公司的支援，讓XMP與AEM Assets的使用者擁有強大的平台可以建立。

## XMP概觀與生態系統 {#xmp-ecosystem}

AEM Assets原生支援XMP中繼資料標準。 XMP是處理和儲存數位資產中標準化和專屬中繼資料的標準。 XMP是通用的標準，可讓多個應用程式有效地處理中繼資料。

例如，生產專業人員可使用Adobe應用程式內建的XMP支援，跨多種檔案格式傳遞資訊。 AEM Assets儲存庫會擷取XMP中繼資料，並使用它來管理內容生命週期，並提供建立自動化工作流程的功能。

XMP透過提供資料模型、儲存模型和結構描述，標準化中繼資料的定義、建立和處理方式。 本節將介紹這些概念。

EXIF、ID3或Microsoft Office的所有舊式中繼資料都會自動轉譯為XMP,XMP可加以擴充，以支援客戶特定的中繼資料架構，例如產品型錄。

XMP中的中繼資料由一組屬性組成。 這些屬性始終與稱為資源的特定實體相關聯； 即，屬性是關於資源的。 對於XMP，資源永遠是資產。

XMP定義了 [中繼資料](https://en.wikipedia.org/wiki/Metadata) 模型，可與任何已定義的中繼資料項目集搭配使用。XMP也定義了基本屬性的特定結構 [](https://en.wikipedia.org/wiki/XML_schema) ，這些基本屬性可用於記錄資源在經過多個處理步驟 (從被拍攝、掃描或創作為文字) 、通過照片編輯步驟(如 [](https://en.wikipedia.org/wiki/Image_scanner)[](https://en.wikipedia.org/wiki/Cropping_%28image%29) or color adjustment)到組合成最終影像時的歷史記錄。XMP可讓每個軟體程式或裝置沿途將其資訊新增至數位資源，然後再保留在最終數位檔案中。

XMP最常是使用 [W3C](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium)[Resource Description Framework](https://en.wikipedia.org/wiki/Resource_Description_Framework) (RDF)的子集進行序列化和儲存，該子集又以 [XML表示](https://en.wikipedia.org/wiki/XML)。

### XMP的優點 {#advantages-of-xmp}

XMP比其他編碼標準和圖式具有以下優點：

* 以XMP為基礎的中繼資料功能強大，而且具備細緻的功能。
* XMP可讓您針對一個屬性擁有多個值。
* XMP具備標準化編碼，可讓您輕鬆交換中繼資料。
* XMP具有可擴充性。 您可以新增其他資訊至資產。

XMP標準可擴充，讓您在XMP資料中新增自訂的中繼資料類型。 而EXIF則否——它有固定的屬性清單，無法延伸。

>[!NOTE]
>
>XMP通常不允許嵌入二進位資料類型。 若要以XMP格式傳送二進位資料（例如縮圖影像），它們必須以XML友好格式編碼，例如 `Base64`。

### XMP核心概念 {#xmp-core-concepts}

**命名空間和圖式**

XMP架構是一組通用XML命名空間中的屬性名稱，其中包含資料類型和描述性資訊。 XMP架構由其XML命名空間URI來識別。 使用名稱空間可防止名稱相同但含義不同之不同結構中屬性之間的衝突。

例如，兩個獨立設計結構中的 **Creator** 屬性可能代表建立資產的人員，也可能代表建立資產的應用程式（例如Adobe Photoshop）。

**XMP屬性和值**

XMP可以包括來自一個或多個方案的屬性。 例如，許多Adobe應用程式使用的典型子集可能包括：

* 都柏林核心架構： `dc:title`, `dc:creator`, `dc:subject`, `dc:format`, `dc:rights`
* XMP基本架構： `xmp:CreateDate`, `xmp:CreatorTool`, `xmp:ModifyDate`, `xmp:metadataDate`
* XMP權限管理架構： `xmpRights:WebStatement`的 `xmpRights:Marked`
* XMP媒體管理架構： `xmpMM:DocumentID`

**替代語言**

XMP可讓您將屬性新增至 `xml:lang` 文字屬性，以指定文字的語言。

## XMP回寫至轉譯 {#xmp-writeback-to-renditions}

Adobe Experience Manager(AEM)Assets中的此XMP回寫功能可將資產中繼資料變更複製至資產的轉譯。

當您從AEM Assets中變更資產的中繼資料，或在上傳資產時，變更最初會儲存在CRXDE的資產節點中。

XMP回寫功能會將中繼資料變更傳播至資產的所有或特定轉譯。

請考慮您修改資產 [!UICONTROL 標題] (Title)屬性的 `Classic Leather` 藍本 `Nylon`。

![中繼資料](assets/metadata.png)

在此情況下，AEM Assets會將資產階層中儲存之資產中繼資料 **[!UICONTROL 的參數中對Title]**`dc:title` 屬性所做的變更儲存。

![metadata_stored](assets/metadata_stored.png)

不過，AEM Assets不會自動將任何中繼資料變更傳播至資產的轉譯。

XMP回寫功能可讓您將中繼資料變更傳播至資產的所有或特定轉譯。 不過，這些變更不會儲存在資產階層的中繼資料節點下。 此功能會在二進位檔案中內嵌轉譯的變更。

### 啟用XMP回寫 {#enable-xmp-writeback}

<!-- asgupta, Engg: Need attention here to update the configuration manager changes.
-->

若要啟用中繼資料變更在上傳資產時傳播至資產的轉譯，請在Configuration Manager中修改 **[!UICONTROL Adobe CQ DAM Rendition Maker]** configuration。

1. 要開啟配置管理器，請訪問 `https://[aem_server]:[port]/system/console/configMgr`。
1. 開啟 **[!UICONTROL Adobe CQ DAM Rendition Maker設定]** 。
1. 選擇「 **[!UICONTROL 傳播XMP]** 」選項，然後保存更改。

### 針對特定轉譯啟用XMP回寫 {#enable-xmp-writeback-for-specific-renditions}

若要讓XMP回寫功能將中繼資料變更傳播至選取的轉譯，請將這些轉譯指定至DAM中繼資料回寫工作流程的  XMP回寫程式工作流程步驟。 依預設，此步驟會以原始轉譯設定。

對於XMP回寫功能，將中繼資料傳播至轉譯縮圖140.100.png和319.319.png，請執行這些步驟。

1. 點選/按一下AEM標誌，然後導覽至「工 **[!UICONTROL 具]** >工 **[!UICONTROL 作流程]** >模 **[!UICONTROL 型]**」。
1. 從「模型」頁面，開啟「 **[!UICONTROL DAM中繼資料回寫]** 」工作流程模型。
1. 在「 **[!UICONTROL DAM中繼資料回寫]** 」屬性頁面中，開啟 **[!UICONTROL 「XMP回寫程式」步驟]** 。
1. 在「步 **[!UICONTROL 驟屬性]** 」對話方塊中，點選/按一下「 **[!UICONTROL 處理]** 」標籤。
1. 在「參 **[!UICONTROL 數]** 」方塊中，新增 `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`，然後點選／按一下「 **[!UICONTROL 確定」]**。

   ![step_properties](assets/step_properties.png)

1. 儲存變更。
1. 若要使用新屬性重新產生動態媒體影像的金字塔TIFF(PTIFF)轉譯，請將「動態媒體處理影像資產」步驟新增至「 **** DAM中繼資料回寫」工作流程。PTIFF轉譯只會在Dynamic Media Hybrid實作中建立並儲存在本機。

1. 儲存工作流程。

中繼資料變更會傳播至資產的轉譯縮圖140.100.png和thumbnail.319.319.png，而非其他。

<!--
>[!NOTE]
>
>For XMP writeback issues in 64 bit Linux, see [How to enable XMP write-back on 64-bit RedHat Linux](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).
>
>For more information about supported platforms, see [XMP metadata write-back prerequisites](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back).
-->

<!--
TBD: The method has changed in AEMaaCS. Find the new ones.

### Filter XMP metadata {#filtering-xmp-metadata}

AEM Assets supports filtering of properties/nodes for XMP metadata that is read from asset binaries and stored in JCR when assets are ingested. Filtering is possible via a blocked list and an allowed list.

Filtering using a blocked list lets you import all XMP metadata properties except the properties that are specified for exclusion. However, for asset types such as INDD files that have huge amounts of XMP metadata (for example 1000 nodes with 10,000 properties), the names of nodes to be filtered are not always known in advance. If filtering using a blocked list allows a large number of assets with numerous XMP metadata to be imported, the AEM instance/cluster can encounter stability issues, for example clogged observation queues.

Filtering of XMP metadata via allowed list resolves this issue by letting you define the XMP properties to be imported. This way, other/unknown XMP properties are ignored. For backward compatibility, you can add some of these properties to the filter that uses a blocked list.

>[!NOTE]
>
>Filtering works only for the properties derived from XMP sources in asset binaries. For the properties derived from non-XMP sources, such as EXIF and IPTC formats, the filtering does not work. For example, the date of asset creation is stored in property named `CreateDate` in EXIF TIFF. AEM stories this value in the metadata field named `exif:DateTimeOriginal`. As the source is a non-XMP source, filtering does not work on this property.

1. To open Configuration Manager, access `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL Adobe CQ DAM XmpFilter]** configuration.
1. To apply filtering via an allowed list, select **[!UICONTROL Apply Whitelist to XMP Properties]**, and specify the properties to be imported in the **[!UICONTROL Whitelisted XML Names for XMP filtering]** box.

1. To filter out blocked XMP properties after applying filtering via allowed list, specify them in the **[!UICONTROL Blacklisted XML Names for XMP filtering]** box.

   >[!NOTE]
   >
   >The **[!UICONTROL Apply Blacklist to XMP Properties]** option is selected by default. In other words, filtering using a blocked list is enabled by default. To disable such filtering, deselect the **[!UICONTROL Apply Blacklist to XMP Properties]** option.

1. Save the changes.
-->

>[!MORELIKETHIS]
>
>* [Adobe的XMP規格](https://www.adobe.com/devnet/xmp.html)

