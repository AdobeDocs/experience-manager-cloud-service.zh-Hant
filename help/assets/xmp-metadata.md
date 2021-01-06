---
title: XMP 中繼資料
description: 瞭解XMP（可擴充中繼資料平台）中繼資料管理標準。 AEM將它當做建立、處理和交換中繼資料的標準格式。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 8110259a910c891a5bcf7507cfa9897603a45c91
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 17%

---


# XMP 中繼資料 {#xmp-metadata}

XMP（可擴充中繼資料平台）是AEM Assets用於所有中繼資料管理的中繼資料標準。 XMP提供標準格式，讓您針對多種應用程式建立、處理和交換中繼資料。

除了提供可嵌入所有檔案格式的通用中繼資料編碼外，XMP還提供多樣化的[內容模型](#xmp-core-concepts)，並受Adobe](#advantages-of-xmp)和其他公司支援[，讓XMP的使用者結合AEM Assets擁有強大的平台來建立內容。

## XMP概觀和生態系統{#xmp-ecosystem}

AEM Assets原生支援XMP中繼資料標準。 XMP是處理和儲存數位資產中標準化和專屬中繼資料的標準。 XMP是通用的標準，可讓多個應用程式有效地處理中繼資料。

例如，生產專業人員可使用Adobe應用程式內建的XMP支援，跨多種檔案格式傳遞資訊。 AEM Assets儲存庫會擷取XMP中繼資料，並使用它來管理內容生命週期，並提供建立自動化工作流程的功能。

XMP透過提供資料模型、儲存模型和結構描述，標準化中繼資料的定義、建立和處理方式。 本節將介紹這些概念。

EXIF、ID3或Microsoft Office的所有舊式中繼資料都會自動轉譯為XMP,XMP可加以擴充，以支援客戶特定的中繼資料架構，例如產品型錄。

XMP中的中繼資料由一組屬性組成。 這些屬性始終與稱為資源的特定實體相關聯；即，屬性是關於資源的。 對於XMP，資源永遠是資產。

XMP定義了 [中繼資料](https://en.wikipedia.org/wiki/Metadata) 模型，可與任何已定義的中繼資料項目集搭配使用。XMP也定義了基本屬性的特定結構 [](https://en.wikipedia.org/wiki/XML_schema) ，這些基本屬性可用於記錄資源在經過多個處理步驟 (從被拍攝、掃描或創作為文字) 、通過照片編輯步驟(如 [](https://en.wikipedia.org/wiki/Image_scanner)[](https://en.wikipedia.org/wiki/Cropping_%28image%29) or color adjustment)到組合成最終影像時的歷史記錄。XMP可讓每個軟體程式或裝置沿途將其資訊新增至數位資源，然後再保留在最終數位檔案中。

XMP最常是使用 [W3C](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium)[Resource Description Framework](https://en.wikipedia.org/wiki/Resource_Description_Framework) (RDF)的子集進行序列化和儲存，該子集又以 [XML表示](https://en.wikipedia.org/wiki/XML)。

### XMP {#advantages-of-xmp}的優點

XMP比其他編碼標準和圖式具有以下優點：

* 以XMP為基礎的中繼資料功能強大，而且具備細緻的功能。
* XMP可讓您針對一個屬性擁有多個值。
* XMP具備標準化編碼，可讓您輕鬆交換中繼資料。
* XMP具有可擴充性。 您可以新增其他資訊至資產。

XMP標準可擴充，讓您在XMP資料中新增自訂的中繼資料類型。 而EXIF則否——它有固定的屬性清單，無法延伸。

>[!NOTE]
>
>XMP通常不允許嵌入二進位資料類型。 若要以XMP格式傳送二進位資料（例如縮圖影像），必須以XML友好格式（例如`Base64`）加以編碼。

### XMP核心概念{#xmp-core-concepts}

**命名空間和圖式**

XMP架構是一組通用XML命名空間中的屬性名稱，其中包含
資料類型和描述性資訊。 XMP架構由其XML命名空間URI來識別。 使用名稱空間可防止名稱相同但含義不同之不同結構中屬性之間的衝突。

例如，兩個獨立設計結構中的&#x200B;**Creator**&#x200B;屬性可能代表建立資產的人員，也可能代表建立資產的應用程式（例如Adobe Photoshop）。

**XMP屬性和值**

XMP可以包括來自一個或多個方案的屬性。 例如，許多Adobe應用程式使用的典型子集可能包括：

* 都柏林核心架構：`dc:title`、`dc:creator`、`dc:subject`、`dc:format`、`dc:rights`
* XMP基本架構：`xmp:CreateDate`、`xmp:CreatorTool`、`xmp:ModifyDate`、`xmp:metadataDate`
* XMP權限管理架構：`xmpRights:WebStatement`, `xmpRights:Marked`
* XMP媒體管理架構：`xmpMM:DocumentID`

**替代語言**

XMP可讓您將`xml:lang`屬性新增至文字屬性，以指定文字的語言。

## XMP回寫到轉譯{#xmp-writeback-to-renditions}

Adobe Experience Manager(AEM)Assets中的此XMP回寫功能會將資產中繼資料變更複製至資產的轉譯。

當您從AEM Assets中變更資產的中繼資料，或在上傳資產時，變更最初會儲存在CRXDE的資產節點中。

XMP回寫功能會將中繼資料變更傳播至資產的所有或特定轉譯。

考慮將`Classic Leather`資產[!UICONTROL Title]屬性修改為`Nylon`的藍本。

![中繼資料](assets/metadata.png)

在此情況下，AEM Assets會針對儲存在資產階層中的資產中繼資料，在`dc:title`參數中儲存對&#x200B;**[!UICONTROL Title]**&#x200B;屬性的變更。

![metadata_stored](assets/metadata_stored.png)

不過，AEM Assets不會自動將任何中繼資料變更傳播至資產的轉譯。

XMP回寫功能可讓您將中繼資料變更傳播至資產的所有或特定轉譯。 不過，這些變更不會儲存在資產階層的中繼資料節點下。 此功能會在二進位檔案中內嵌轉譯的變更。

<!-- Commenting for now. Need to document how to enable metadata writeback. See CQDOC-17254.

### Enable XMP writeback {#enable-xmp-writeback}
-->

<!-- asgupta, Engg: Need attention here to update the configuration manager changes. -->

<!-- 
To enable the metadata changes to be propagated to the renditions of the asset when uploading it, modify the **[!UICONTROL Adobe CQ DAM Rendition Maker]** configuration in Configuration Manager.

1. To open Configuration Manager, access `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL Adobe CQ DAM Rendition Maker]** configuration.
1. Select the **[!UICONTROL Propagate XMP]** option, and then save the changes.

### Enable XMP write-back for specific renditions {#enable-xmp-writeback-for-specific-renditions}

To let the XMP write-back feature propagate metadata changes to select renditions, specify these renditions to the [!UICONTROL XMP Writeback Process] workflow step of DAM Metadata WriteBack workflow. By default, this step is configured with the original rendition.

For the XMP write-back feature to propagate metadata to the rendition thumbnails 140.100.png and 319.319.png, perform these steps.

1. Tap/click the AEM logo, and then navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Workflow]** &gt; **[!UICONTROL Models]**.
1. From the Models page, open the **[!UICONTROL DAM Metadata Writeback]** workflow model.
1. In the **[!UICONTROL DAM Metadata Writeback]** properties page, open the **[!UICONTROL XMP Writeback Process]** step.
1. In the **[!UICONTROL Step Properties]** dialog box, tap/click the **[!UICONTROL Process]** tab.
1. In the **[!UICONTROL Arguments]** box, add `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`, and then tap/click **[!UICONTROL OK]**.

   ![step_properties](assets/step_properties.png)

1. Save the changes.
1. To regenerate the Pyramid TIFF (PTIFF) renditions for Dynamic Media images with the new attributes, add the **[!UICONTROL Dynamic Media Process Image Assets]** step to the DAM Metadata write-back workflow. PTIFF renditions are only created and stored locally in a Dynamic Media Hybrid implementation.

1. Save the workflow.

The metadata changes are propagated to the renditions renditions thumbnail.140.100.png and thumbnail.319.319.png of the asset, and not the others.
-->

>[!MORELIKETHIS]
>
>* [Adobe的XMP規格](https://www.adobe.com/devnet/xmp.html)

