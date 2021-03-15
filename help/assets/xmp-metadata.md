---
title: XMP 中繼資料
description: 瞭解中繼資XMP料管理的（可擴充中繼資料平台）中繼資料標準。 它被用AEM作建立、處理和交換中繼資料的標準格式。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 46f5ffbdce0bf555e9576126acec61cdae0a1de0
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 16%

---


# XMP 中繼資料 {#xmp-metadata}

(可XMP擴充中繼資料平台)是AEM Assets用於所有中繼資料管理的中繼資料標準。 為XMP各種應用程式建立、處理和交換中繼資料提供標準格式。

除了提供可嵌入所有檔案格式的通用中繼資料編碼外XMP，還提供多樣化的[內容模型](#xmp-core-concepts)，並受Adobe](#advantages-of-xmp)等公司支援[，讓與AEM Assets合作的使用者擁有強大的平台來建立。

## XMP概觀與生態系統{#xmp-ecosystem}

AEM Assets本身支援XMP中繼資料標準。 XMP是處理和儲存數位資產中標準化和專屬中繼資料的標準。 設XMP計為通用標準，可讓多個應用程式有效地處理中繼資料。

例如，生產專業人員可使用Adobe應用程式內建XMP的支援，跨多種檔案格式傳遞資訊。 AEM Assets儲存庫提取元XMP資料並使用它管理內容生命週期，並提供建立自動化工作流的能力。

XMP透過提供資料模型、儲存模型和結構，標準化中繼資料的定義、建立和處理方式。 本節將介紹這些概念。

EXIF、ID3或Microsoft Office的所有舊式中繼資料都會自動轉譯為XMP，可加以擴充以支援客戶特定的中繼資料架構，例如產品型錄。

中的元XMP資料由一組屬性組成。 這些屬性始終與稱為資源的特定實體相關聯；即，屬性是關於資源的。 在這種情況XMP下，資源始終是資產。

XMP定義了 [中繼資料](https://en.wikipedia.org/wiki/Metadata) 模型，可與任何已定義的中繼資料項目集搭配使用。XMP也定義了基本屬性的特定結構 [](https://en.wikipedia.org/wiki/XML_schema) ，這些基本屬性可用於記錄資源在經過多個處理步驟 (從被拍攝、掃描或創作為文字) 、通過照片編輯步驟(如 [](https://en.wikipedia.org/wiki/Image_scanner)[](https://en.wikipedia.org/wiki/Cropping_%28image%29) or color adjustment)到組合成最終影像時的歷史記錄。XMP可讓每個軟體程式或裝置沿途將其資訊新增至數位資源，然後再保留在最終數位檔案中。

XMP最常是使用 [W3C](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium)[Resource Description Framework](https://en.wikipedia.org/wiki/Resource_Description_Framework) (RDF)的子集進行序列化和儲存，該子集又以 [XML表示](https://en.wikipedia.org/wiki/XML)。

### &lt;a0/XMP>的優點{#advantages-of-xmp}

與其XMP他編碼標準和模式相比，具有以下優勢：

* 基XMP於元資料的功能非常強大，而且細緻。
* 可讓XMP您對一個屬性有多個值。
* XMP有標準化編碼，讓您輕鬆交換中繼資料。
* 可XMP擴充。 您可以新增其他資訊至資產。

此標XMP準可擴充，讓您在資料中新增自訂的中繼資料類XMP型。 而EXIF則否——它有固定的屬性清單，無法延伸。

>[!NOTE]
>
>通XMP常不允許嵌入二進位資料類型。 若要將二進位資XMP料（例如縮圖影像）傳入，它們必須以XML友好格式編碼，例如`Base64`。

### XMP核心概念{#xmp-core-concepts}

**命名空間和圖式**

架XMP構是一組通用XML命名空間中的屬性名稱，其中包含
資料類型和描述性資訊。 架構XMP由其XML命名空間URI標識。 使用名稱空間可防止名稱相同但含義不同之不同結構中屬性之間的衝突。

例如，兩個獨立設計結構中的&#x200B;**Creator**&#x200B;屬性可能代表資產的建立者，也可能代表資產建立者的應用程式(例如Adobe Photoshop)。

**XMP屬性和值**

可XMP以包括來自一個或多個方案的屬性。 例如，許多Adobe應用程式使用的典型子集可能包括：

* 都柏林核心架構：`dc:title`、`dc:creator`、`dc:subject`、`dc:format`、`dc:rights`
* XMP基本架構：`xmp:CreateDate`、`xmp:CreatorTool`、`xmp:ModifyDate`、`xmp:metadataDate`
* XMP權限管理架構`xmpRights:WebStatement`, `xmpRights:Marked`
* XMP媒體管理架構`xmpMM:DocumentID`

**替代語言**

提XMP供將`xml:lang`屬性新增至文字屬性以指定文字語言的功能。

## XMP回寫至轉譯{#xmp-writeback-to-renditions}

&lt;a0/XMP>中的此回寫功能會將中繼資料變更複製到原始資產的轉譯。 [!DNL Adobe Experience Manager Assets]當您從[!DNL Assets]中變更資產的中繼資料，或在上傳資產時，這些變更最初會儲存在儲存庫的資產節點中。 不過，[!DNL Assets]不會自動將任何中繼資料變更傳播至資產的轉譯。 回寫功XMP能可讓您將中繼資料變更傳播至資產的所有或特定轉譯。 更新會儲存在資產階層的中繼資料節點中。 此功能也會將更新內嵌在轉譯的二進位檔案中。 此功能僅會回寫使用`jcr`命名空間的中繼資料屬性。

例如，假設您將`Classic Leather`資產的[!UICONTROL Title]屬性修改為`Nylon`的藍本。

![中繼資料](assets/metadata.png)

在這種情況下，[!DNL Assets]會針對資產階層中儲存的資產中繼資料，在`dc:title`參數中儲存對&#x200B;**[!UICONTROL Title]**&#x200B;屬性的變更。

![儲存在儲存庫中資產節點中的元資料](assets/metadata_stored.png)

>[!NOTE]
>
>在[!DNL Assets]中，預設未啟用回寫功能。 瞭解如何[啟用中繼資料回寫](#enable-xmp-writeback)。

### 啟XMP用回寫{#enable-xmp-writeback}

[!UICONTROL DAM中繼資] 料回寫工作流程可用來回寫資產的中繼資料。要啟用回寫，請執行以下步驟：

1. 作為管理員，訪問&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 啟動器]**。
1. 選擇[!UICONTROL Launcher]，其中&#x200B;**[!UICONTROL Workflow]**&#x200B;欄顯示&#x200B;**[!UICONTROL DAM MetaData Writeback]**。 按一下工具欄中的&#x200B;**[!UICONTROL 屬性]**。

   ![選擇DAM中繼資料回寫啟動程式以修改其屬性並加以啟用](assets/launcher-properties-metadata-writeback1.png)

1. 在&#x200B;**[!UICONTROL 啟動器屬性]**&#x200B;頁面上選擇&#x200B;**[!UICONTROL 激活]**。 按一下&#x200B;**[!UICONTROL 「儲存並關閉」]**。

若要將此工作流程只套用一次至資產，請從左側導軌套用工作流程[!UICONTROL DAM中繼資料回寫]。 若要將工作流程套用至所有已上傳的資產，請將工作流程新增至後處理設定檔。

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
