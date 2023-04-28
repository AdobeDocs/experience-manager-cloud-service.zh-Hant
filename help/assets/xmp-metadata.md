---
title: XMP 中繼資料
description: 了解用於中繼資料管理的XMP（可擴充中繼資料平台）中繼資料標準。 它被Experience Manager用作建立、處理和交換元資料的標準格式。
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: fd9af408-d2a3-4c7a-9423-c4b69166f873
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1041'
ht-degree: 17%

---

# XMP 中繼資料 {#xmp-metadata}

XMP（可擴充中繼資料平台）是Experience Manager Assets用於所有中繼資料管理的中繼資料標準。 XMP提供標準格式，供多種應用程式建立、處理和交換中繼資料。

除了提供可內嵌於所有檔案格式的通用中繼資料編碼外，XMP還提供豐富的 [內容模型](#xmp-core-concepts) 和 [支援Adobe](#advantages-of-xmp) 和其他公司，讓XMP的使用者 [!DNL Assets] 有一個強大的平台可以建立。

## XMP概述與生態系統 {#xmp-ecosystem}

[!DNL Assets] 原生支援XMP中繼資料標準。 XMP是處理和儲存數位資產中標準化和專屬中繼資料的標準。 XMP的設計是通用標準，可讓多個應用程式有效處理中繼資料。

例如，生產專業人員可在Adobe的應用程式中使用內建的XMP支援，以傳遞多種檔案格式的資訊。 此 [!DNL Assets] 存放庫會擷取XMP中繼資料，並使用它來管理內容生命週期，並提供建立自動化工作流程的功能。

XMP借由提供資料模型、儲存模型和結構，標準化中繼資料的定義、建立和處理方式。 本節將介紹所有這些概念。

來自EXIF、ID3或Microsoft Office的所有舊版中繼資料都會自動轉譯為XMP，以延伸支援客戶專屬的中繼資料結構，例如產品目錄。

XMP中的中繼資料包含一組屬性。 這些屬性始終與稱為資源的特定實體相關聯；也就是說，屬性是關於資源。 在XMP的情況下，資源一律為資產。

XMP定義了 [中繼資料](https://en.wikipedia.org/wiki/Metadata) 模型，可與任何已定義的中繼資料項目集搭配使用。XMP也定義了基本屬性的特定結構 [](https://en.wikipedia.org/wiki/XML_schema) ，這些基本屬性可用於記錄資源在經過多個處理步驟 (從被拍攝、掃描或創作為文字) 、通過照片編輯步驟(如 [](https://en.wikipedia.org/wiki/Image_scanner)[](https://en.wikipedia.org/wiki/Cropping_%28image%29) or color adjustment)到組合成最終影像時的歷史記錄。XMP可讓每個軟體程式或裝置沿途將其資訊新增至數位資源，然後再保留在最終數位檔案中。

XMP最常是使用 [W3C](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium)[Resource Description Framework](https://en.wikipedia.org/wiki/Resource_Description_Framework) (RDF)的子集進行序列化和儲存，該子集又以 [XML表示](https://en.wikipedia.org/wiki/XML)。

### XMP的優點 {#advantages-of-xmp}

XMP比其他編碼標準和架構有下列優點：

* XMP型中繼資料功能強大且微調。
* XMP可讓您擁有一個屬性的多個值。
* XMP具有標準化編碼，可讓您輕鬆交換中繼資料。
* XMP可擴充。 您可以新增其他資訊至資產。

XMP標準的設計可擴充，可讓您將自訂中繼資料類型新增至XMP資料。 EXIF則否 — 它有無法擴充的固定屬性清單。

>[!NOTE]
>
>XMP通常不允許嵌入二進位資料類型。 若要在XMP中傳送二進位資料（例如縮圖影像），必須以適合XML的格式編碼，例如 `Base64`.

### XMP核心概念 {#xmp-core-concepts}

**命名空間和架構**

XMP架構是通用XML命名空間中的一組屬性名稱，包含資料類型和描述性資訊。 XMP架構由其XML命名空間URI標識。 使用命名空間可避免名稱相同但含義不同之不同結構中的屬性之間產生衝突。

例如， **建立者** 兩個獨立設計結構中的屬性可能代表建立資產的人員，或可能代表建立資產的應用程式(例如Adobe Photoshop)。

**XMP屬性和值**

XMP可包含一或多個結構中的屬性。 例如，許多Adobe應用程式使用的典型子集可能包括：

* 都柏林核心架構： `dc:title`, `dc:creator`, `dc:subject`, `dc:format`, `dc:rights`
* XMP基本結構： `xmp:CreateDate`, `xmp:CreatorTool`, `xmp:ModifyDate`, `xmp:metadataDate`
* XMP權限管理結構： `xmpRights:WebStatement`, `xmpRights:Marked`
* XMP媒體管理結構： `xmpMM:DocumentID`

**替代語言**

XMP可讓您新增 `xml:lang` 屬性來指定文字的語言。

## XMP回寫至轉譯 {#xmp-writeback-to-renditions}

此XMP回寫功能位於 [!DNL Adobe Experience Manager Assets] 會將中繼資料變更複製至原始資產的轉譯。
從內變更資產的中繼資料時 [!DNL Assets] 或是在上傳資產時，變更最初儲存在資產階層的中繼資料節點中。 回寫功能可讓您將中繼資料變更傳播至資產的所有或特定轉譯。 功能只會回寫使用的中繼資料屬性 `jcr` 命名空間，即名為 `dc:title` 被寫回了，但被命名為 `mytitle` 不是。

例如，假設您修改 [!UICONTROL 標題] 資產的屬性(標題為 `Classic Leather` to `Nylon`.

![中繼資料](assets/metadata.png)

在這種情況下， [!DNL Assets] 將變更儲存至 **[!UICONTROL 標題]** 屬性 `dc:title` 資產階層中儲存的資產中繼資料的參數。

![儲存在存放庫中資產節點的中繼資料](assets/metadata_stored.png)

>[!IMPORTANT]
>
>預設不會啟用回寫功能，位於 [!DNL Assets]. 了解如何 [啟用中繼資料回寫](#enable-xmp-writeback). 數位資產的MSM無法搭配啟用中繼資料回寫運作。 回寫時，繼承會中斷。

### 啟用XMP回寫 {#enable-xmp-writeback}

[!UICONTROL DAM中繼資料回寫] 工作流程可用來回寫資產的中繼資料。 要啟用回寫，請遵循以下三種方法之一：

* 使用啟動器。
* 手動啟動 `DAM MetaData Writeback` 工作流程。
* 將工作流程設為後置處理的一部分。

要使用啟動器，請執行以下步驟：

1. 身為管理員，可存取 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 啟動器]**.
1. 選取 [!UICONTROL 啟動器] 對於 **[!UICONTROL 工作流程]** 欄顯示 **[!UICONTROL DAM中繼資料回寫]**. 按一下 **[!UICONTROL 屬性]** 的上界。

   ![選取DAM中繼資料回寫啟動器，以修改其屬性並啟用它](assets/launcher-properties-metadata-writeback1.png)

1. 選擇 **[!UICONTROL 啟動]** 在 **[!UICONTROL 啟動器屬性]** 頁面。 按一下&#x200B;**[!UICONTROL 「儲存並關閉」]**。

若要手動將工作流程套用至資產一次，請套用 [!UICONTROL DAM中繼資料回寫] 工作流程。

若要將工作流程套用至所有上傳的資產，請將工作流程新增至後置處理設定檔。

<!-- Commenting for now. Need to document how to enable metadata writeback. See CQDOC-17254.

### Enable XMP writeback {#enable-xmp-writeback}

To enable the metadata changes to be propagated to the renditions of the asset when uploading it, modify the **[!UICONTROL Adobe CQ DAM Rendition Maker]** configuration in Configuration Manager.

1. To open Configuration Manager, access `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL Adobe CQ DAM Rendition Maker]** configuration.
1. Select the **[!UICONTROL Propagate XMP]** option, and then save the changes.

### Enable XMP write-back for specific renditions {#enable-xmp-writeback-for-specific-renditions}

To let the XMP write-back feature propagate metadata changes to select renditions, specify these renditions to the [!UICONTROL XMP Writeback Process] workflow step of DAM Metadata WriteBack workflow. By default, this step is configured with the original rendition.

For the XMP write-back feature to propagate metadata to the rendition thumbnails 140.100.png and 319.319.png, perform these steps.

1. Tap/click the Experience Manager logo, and then navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Workflow]** &gt; **[!UICONTROL Models]**.
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

**另請參閱**

* [翻譯資產](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [Assets支援的檔案格式](file-format-support.md)
* [搜尋資產](search-assets.md)
* [連線資產](use-assets-across-connected-assets-instances.md)
* [資產報表](asset-reports.md)
* [中繼資料結構](metadata-schemas.md)
* [下載資產](download-assets-from-aem.md)
* [管理中繼資料](manage-metadata.md)
* [搜尋 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [大量中繼資料匯入](metadata-import-export.md)
