---
title: XMP 中繼資料
description: 瞭解用於中繼資料管理的XMP （可延伸中繼資料平台）中繼資料標準。 Experience Manager將其用作建立、處理和交換中繼資料的標準化格式。
contentOwner: AG
feature: Metadata
role: Admin, User
exl-id: fd9af408-d2a3-4c7a-9423-c4b69166f873
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1033'
ht-degree: 17%

---

# XMP 中繼資料 {#xmp-metadata}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/xmp-writeback.html) |
| AEM as a Cloud Service  | 本文章 |

XMP （可延伸中繼資料平台）是Experience Manager Assets用於所有中繼資料管理的中繼資料標準。 XMP為各種應用程式的中繼資料的建立、處理和交換提供標準格式。

除了提供可內嵌至所有檔案格式的通用中繼資料編碼之外，XMP還提供豐富的[內容模型](#xmp-core-concepts)，並受到Adobe[&#128279;](#advantages-of-xmp)和其他公司的支援，因此XMP與[!DNL Assets]結合的使用者擁有可建置的強大平台。

## XMP概觀和生態系統 {#xmp-ecosystem}

[!DNL Assets]原生支援XMP中繼資料標準。 XMP是在數位資產中處理和儲存標準化和專屬中繼資料的標準。 XMP是專為允許多個應用程式有效使用中繼資料的通用標準而設計。

例如，專業製作人員可利用Adobe應用程式內建的XMP支援，以多種檔案格式傳遞資訊。 [!DNL Assets]儲存庫會擷取XMP中繼資料，並使用它來管理內容生命週期，並提供建立自動化工作流程的功能。

XMP透過提供資料模型、儲存模型和結構描述，將中繼資料的定義、建立和處理標準化。 本章節將介紹所有這些概念。

來自EXIF、ID3或Microsoft Office的所有舊版中繼資料會自動轉譯為XMP，可延伸以支援客戶特定的中繼資料結構，例如產品目錄。

XMP中的中繼資料包含一組屬性。 這些屬性一律與稱為資源的特定實體相關聯；也就是說，屬性是有關資源的。 在XMP中，資源一律為資產。

XMP定義了 [中繼資料](https://en.wikipedia.org/wiki/Metadata) 模型，可與任何已定義的中繼資料項目集搭配使用。XMP也定義了基本屬性的特定結構 [&#128279;](https://en.wikipedia.org/wiki/XML_schema) ，這些基本屬性可用於記錄資源在經過多個處理步驟 (從被拍攝、掃描或創作為文字) 、通過照片編輯步驟(如 [&#128279;](https://en.wikipedia.org/wiki/Image_scanner) [&#128279;](https://en.wikipedia.org/wiki/Cropping_%28image%29) or color adjustment)到組合成最終影像時的歷史記錄。XMP可讓每個軟體程式或裝置沿途將其資訊新增至數位資源，然後再保留在最終數位檔案中。

XMP最常是使用 [W3C](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://en.wikipedia.org/wiki/Resource_Description_Framework) (RDF)的子集進行序列化和儲存，該子集又以 [XML表示](https://en.wikipedia.org/wiki/XML)。

### XMP的優點 {#advantages-of-xmp}

與其他編碼標準和結構描述相比，XMP具有以下優勢：

* XMP中繼資料功能非常強大，而且相當精細化。
* XMP可讓您一個屬性有多個值。
* XMP已標準化編碼，讓您輕鬆交換中繼資料。
* XMP是可擴充的。 您可以將其他資訊新增至資產。

XMP標準可擴充，可讓您將自訂的中繼資料型別新增到XMP資料中。 另一方面，EXIF則不會 — 它具有無法擴充的固定屬性清單。

>[!NOTE]
>
>XMP通常不允許內嵌二進位資料型別。 若要在XMP中攜帶二進位資料（例如縮圖影像），必須以XML易記格式（例如`Base64`）進行編碼。

### XMP核心概念 {#xmp-core-concepts}

**名稱空間和結構描述**

XMP結構描述是通用XML名稱空間中的一組屬性名稱，包括
資料型別和描述性資訊。 XMP結構描述是由其XML名稱空間URI識別。 使用名稱空間可防止不同結構描述中名稱相同但含義不同的屬性之間發生衝突。

例如，兩個獨立設計的結構描述中的&#x200B;**建立者**&#x200B;屬性可能代表建立資產的人，也可能代表建立資產的應用程式(例如Adobe Photoshop)。

**XMP屬性和值**

XMP可能包含一或多個結構描述的屬性。 例如，許多Adobe應用程式所使用的典型子集可能包括以下專案：

* 都柏林核心結構描述： `dc:title`，`dc:creator`，`dc:subject`，`dc:format`，`dc:rights`
* XMP基本結構描述： `xmp:CreateDate`，`xmp:CreatorTool`，`xmp:ModifyDate`，`xmp:metadataDate`
* XMP許可權管理結構描述： `xmpRights:WebStatement`，`xmpRights:Marked`
* XMP媒體管理結構描述： `xmpMM:DocumentID`

**替代語言**

XMP可讓您新增`xml:lang`屬性至文字屬性，以指定文字的語言。

## XMP回寫至轉譯 {#xmp-writeback-to-renditions}

[!DNL Adobe Experience Manager Assets]中的這個XMP回寫功能會將中繼資料變更復寫至原始資產的轉譯。
當您從[!DNL Assets]內變更資產的中繼資料時，或上傳資產時，變更最初會儲存在資產階層中的中繼資料節點中。 回寫功能可讓您將中繼資料變更傳播到資產的所有或特定轉譯。 此功能只會回寫那些使用`jcr`名稱空間的中繼資料屬性，也就是回寫名為`dc:title`的屬性，但不回寫名為`mytitle`的屬性。

例如，假設您將`Classic Leather`標題為`Nylon`之資產的[!UICONTROL Title]屬性修改為案例。

![中繼資料](assets/metadata.png)

在此案例中，[!DNL Assets]會針對儲存在資產階層中的資產中繼資料，將變更儲存在`dc:title`引數中的&#x200B;**[!UICONTROL Title]**&#x200B;屬性。

![中繼資料儲存在儲存庫中的資產節點中](assets/metadata_stored.png)

>[!IMPORTANT]
>
>預設不會在[!DNL Assets]中啟用回寫功能。 瞭解如何[啟用中繼資料回寫](#enable-xmp-writeback)。 適用於數位資產的MSM無法搭配已啟用中繼資料回寫的功能運作。 回寫時，繼承中斷。

### 啟用XMP回寫 {#enable-xmp-writeback}

[!UICONTROL DAM中繼資料回寫]工作流程是用來回寫資產的中繼資料。 若要啟用回寫，請遵循下列三種方法之一：

* 使用啟動器。
* 手動啟動`DAM MetaData Writeback`工作流程。
* 將工作流程設定為後期處理的一部分。

若要使用啟動器，請遵循下列步驟：

1. 以系統管理員身分，存取&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 啟動器]**。
1. 選取&#x200B;**[!UICONTROL 工作流程]**&#x200B;欄顯示&#x200B;**[!UICONTROL DAM中繼資料回寫]**&#x200B;的[!UICONTROL 啟動器]。 按一下工具列中的&#x200B;**[!UICONTROL 屬性]**。

   ![選取DAM中繼資料回寫啟動器，以修改其屬性並加以啟用](assets/launcher-properties-metadata-writeback1.png)

1. 在&#x200B;**[!UICONTROL 啟動器屬性]**&#x200B;頁面上選取&#x200B;**[!UICONTROL 啟動]**。 按一下「**[!UICONTROL 儲存並關閉]**」。

若要僅手動將工作流程套用至資產一次，請從左側邊欄套用[!UICONTROL DAM中繼資料回寫]工作流程。

若要將工作流程套用至所有上傳的資產，請將工作流程新增至後期處理設定檔。

<!-- Commenting for now. Need to document how to enable metadata writeback. See CQDOC-17254.

### Enable XMP writeback {#enable-xmp-writeback}

To enable the metadata changes to be propagated to the renditions of the asset when uploading it, modify the **[!UICONTROL Adobe CQ DAM Rendition Maker]** configuration in Configuration Manager.

1. To open Configuration Manager, access `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL Adobe CQ DAM Rendition Maker]** configuration.
1. Select the **[!UICONTROL Propagate XMP]** option, and then save the changes.

### Enable XMP write-back for specific renditions {#enable-xmp-writeback-for-specific-renditions}

To let the XMP write-back feature propagate metadata changes to select renditions, specify these renditions to the [!UICONTROL XMP Writeback Process] workflow step of DAM Metadata WriteBack workflow. By default, this step is configured with the original rendition.

For the XMP write-back feature to propagate metadata to the rendition thumbnails 140.100.png and 319.319.png, perform these steps.

1. Select the Experience Manager logo, and then navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Workflow]** &gt; **[!UICONTROL Models]**.
1. From the Models page, open the **[!UICONTROL DAM Metadata Writeback]** workflow model.
1. In the **[!UICONTROL DAM Metadata Writeback]** properties page, open the **[!UICONTROL XMP Writeback Process]** step.
1. In the **[!UICONTROL Step Properties]** dialog box, select the **[!UICONTROL Process]** tab.
1. In the **[!UICONTROL Arguments]** box, add `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`, and then select **[!UICONTROL OK]**.

   ![step_properties](assets/step_properties.png)

1. Save the changes.
1. To regenerate the Pyramid TIFF (PTIFF) renditions for Dynamic Media images with the new attributes, add the **[!UICONTROL Dynamic Media Process Image Assets]** step to the DAM Metadata write-back workflow. PTIFF renditions are only created and stored locally in a Dynamic Media Hybrid implementation.

1. Save the workflow.

The metadata changes are propagated to the renditions renditions thumbnail.140.100.png and thumbnail.319.319.png of the asset, and not the others.
-->

**另請參閱**

* [翻譯資產](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [資產支援的檔案格式](file-format-support.md)
* [搜尋資產](search-assets.md)
* [連接的資產](use-assets-across-connected-assets-instances.md)
* [資產報表](asset-reports.md)
* [中繼資料結構描述](metadata-schemas.md)
* [下載資產](download-assets-from-aem.md)
* [管理中繼資料](manage-metadata.md)
* [搜尋 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [大量中繼資料匯入](metadata-import-export.md)
* [發佈資產至 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
