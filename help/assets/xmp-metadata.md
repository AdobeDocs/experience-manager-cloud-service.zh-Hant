---
title: XMP 中繼資料
description: 瞭解用於元XMP資料管理的（可擴展元資料平台）元資料標準。 它被Experience Manager用作元資料的建立、處理和交換的標準格式。
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: fd9af408-d2a3-4c7a-9423-c4b69166f873
source-git-commit: 4be76f19c27aeab84de388106a440434a99a738c
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 15%

---

# XMP 中繼資料 {#xmp-metadata}

(可XMP擴展元資料平台)是Experience Manager Assets用於所有元資料管理的元資料標準。 為XMP各種應用程式建立、處理和交換元資料提供了標準格式。

除了提供可嵌入到所有檔案格式的通用元資料編碼之外，還XMP提供了豐富的 [內容模型](#xmp-core-concepts) 和 [由Adobe支援](#advantages-of-xmp) 以及其他公司的用戶XMP, [!DNL Assets] 有一個強大的平台可以構建。

## XMP概述 {#xmp-ecosystem}

[!DNL Assets] 本機支援元XMP資料標準。 XMP是處理和儲存數字資產中標準化和專有元資料的標準。 設計XMP為允許多個應用程式有效地使用元資料的通用標準。

例如，生產專業人員使用Adobe應用程式內XMP的內置支援跨多種檔案格式傳遞資訊。 的 [!DNL Assets] 儲存庫提取XMP元資料並使用它來管理內容生命週期，並提供了建立自動化工作流的能力。

通XMP過提供資料模型、儲存模型和模式來標準化元資料的定義、建立和處理方式。 本節將介紹所有這些概念。

EXIF、ID3或Microsoft辦事處的所有舊元資料都會自動轉換為XMP，可以擴展為支援特定於客戶的元資料架構，如產品目錄。

中的元XMP資料由一組屬性組成。 這些屬性始終與稱為資源的特定實體相關聯；即，屬性是關於資源的。 在這種情況XMP下，資源始終是資產。

XMP定義了 [中繼資料](https://en.wikipedia.org/wiki/Metadata) 模型，可與任何已定義的中繼資料項目集搭配使用。XMP也定義了基本屬性的特定結構 [](https://en.wikipedia.org/wiki/XML_schema) ，這些基本屬性可用於記錄資源在經過多個處理步驟 (從被拍攝、掃描或創作為文字) 、通過照片編輯步驟(如 [](https://en.wikipedia.org/wiki/Image_scanner)[](https://en.wikipedia.org/wiki/Cropping_%28image%29) or color adjustment)到組合成最終影像時的歷史記錄。XMP可讓每個軟體程式或裝置沿途將其資訊新增至數位資源，然後再保留在最終數位檔案中。

XMP最常是使用 [W3C](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium)[Resource Description Framework](https://en.wikipedia.org/wiki/Resource_Description_Framework) (RDF)的子集進行序列化和儲存，該子集又以 [XML表示](https://en.wikipedia.org/wiki/XML)。

### 優XMP勢 {#advantages-of-xmp}

與其XMP他編碼標準和方案相比具有以下優點：

* 基XMP於元資料功能強大且細粒度。
* 可XMP以為一個屬性設定多個值。
* XMP具有標準化編碼，可輕鬆交換元資料。
* XMP可擴展。 您可以在資產中添加其他資訊。

該標XMP準設計為可擴展，允許您向資料中添加自定義類型的元XMP資料。 而EXIF則不是 — 它有一個無法擴展的固定屬性清單。

>[!NOTE]
>
>通XMP常不允許嵌入二進位資料類型。 要以縮略圖XMP像等形式傳送二進位資料，必須以XML友好格式(如 `Base64`。

### 核心概念 {#xmp-core-concepts}

**命名空間和架構**

架XMP構是包含資料類型和描述性資訊的公共XML命名空間中的一組屬性名稱。 架XMP構由其XML命名空間URI標識。 使用命名空間可防止名稱相同但含義不同的不同架構中的屬性之間發生衝突。

例如， **建立者** 兩個獨立設計方案中的屬性可能是指建立資產的人員，也可能是指建立資產的應用程式(例如，Adobe Photoshop)。

**XMP屬性和值**

可XMP以包括來自一個或多個架構的屬性。 例如，許多Adobe應用程式使用的典型子集可能包括以下內容：

* 都柏林核心架構： `dc:title`。 `dc:creator`。 `dc:subject`。 `dc:format`。 `dc:rights`
* XMP基本架構 `xmp:CreateDate`。 `xmp:CreatorTool`。 `xmp:ModifyDate`。 `xmp:metadataDate`
* XMP權限管理架構 `xmpRights:WebStatement`。 `xmpRights:Marked`
* XMP媒體管理架構 `xmpMM:DocumentID`

**語言替代**

提XMP供了 `xml:lang` 屬性到文本屬性以指定文本的語言。

## XMP回寫到格式副本 {#xmp-writeback-to-renditions}

中XMP的此寫回功能 [!DNL Adobe Experience Manager Assets] 將元資料更改複製到原始資產的格式副本。
當從內更改資產的元資料時 [!DNL Assets] 或在上載資產時，這些更改最初儲存在資產層次結構中的元資料節點中。 「寫回」功能允許您將元資料更改傳播到資產的所有或特定格式副本。 該功能僅回寫那些使用 `jcr` 命名空間，即名為 `dc:title` 寫回，但名為 `mytitle` 不。

例如，考慮修改 [!UICONTROL 標題] 標題為 `Classic Leather` 至 `Nylon`。

![中繼資料](assets/metadata.png)

在這個例子中， [!DNL Assets] 將更改保存到 **[!UICONTROL 標題]** 屬性 `dc:title` 資產層次結構中儲存的資產元資料的參數。

![儲存在儲存庫中資產節點中的元資料](assets/metadata_stored.png)

>[!IMPORTANT]
>
>預設情況下，在 [!DNL Assets]。 瞭解如何 [啟用元資料寫入](#enable-xmp-writeback)。 啟用元資料寫回時，數字資產的MSM不能工作。 寫回後，遺產就會斷。

### 啟用寫XMP回 {#enable-xmp-writeback}

[!UICONTROL DAM元資料寫回] 工作流用於寫回資產的元資料。 要啟用寫回，請執行以下三種方法之一：

* 使用啟動程式。
* 手動啟動 `DAM MetaData Writeback` 工作流。
* 將工作流配置為後處理的一部分。

要使用啟動器，請執行以下步驟：

1. 作為管理員，訪問 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 發射器]**。
1. 選擇 [!UICONTROL 啟動程式] 對於 **[!UICONTROL 工作流]** 列顯示 **[!UICONTROL DAM元資料寫回]**。 按一下 **[!UICONTROL 屬性]** 的子菜單。

   ![選擇DAM元資料寫回啟動程式以修改其屬性並激活它](assets/launcher-properties-metadata-writeback1.png)

1. 選擇 **[!UICONTROL 激活]** 的 **[!UICONTROL 啟動程式屬性]** 的子菜單。 按一下&#x200B;**[!UICONTROL 「儲存並關閉」]**。

要手動將工作流僅應用一次資產，請應用 [!UICONTROL DAM元資料寫回] 從左欄開始。

要將工作流應用於所有上載的資產，請將工作流添加到後處理配置檔案。

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
