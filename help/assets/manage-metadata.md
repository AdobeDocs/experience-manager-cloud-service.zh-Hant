---
title: 管理數位資產的中繼資料
description: 瞭解中繼資料的型別以及 [!DNL Adobe Experience Manager Assets] 如何協助管理資產的中繼資料，以便更輕鬆地分類及組織資產。 [!DNL Experience Manager] 可讓您根據資產的中繼資料自動整理及處理資產。
contentOwner: AG
mini-toc-levels: 1
feature: Asset Management, Metadata
role: User, Developer, Admin
exl-id: 73a82bc2-1dda-4090-b7ee-29d1a632ba25
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1944'
ht-degree: 9%

---

# 管理數位資產的中繼資料 {#managing-metadata-for-digital-assets}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/metadata.html?lang=zh-Hant) |
| AEM as a Cloud Service  | 本文章 |

[!DNL Adobe Experience Manager Assets]保留每個資產的中繼資料。 它可讓您更輕鬆地分類及組織資產，並協助尋找特定資產的人。 中繼資料管理可透過從上傳至[!DNL Experience Manager Assets]的檔案擷取中繼資料，與創意工作流程整合。 有了使用資產保留和管理中繼資料的功能，您可以根據資產的中繼資料自動組織和處理資產。

<!-- 
* [Metadata Schemata Reference](meta-ref.md)
-->

## 為什麼我們需要中繼資料 {#why-metadata}

中繼資料是指資料的相關資料。 就此而言，資料是指您的數位資產，例如影像。 中繼資料是進行高效率資產管理的關鍵所在。

中繼資料是資產所有可用資料的集合，但不一定包含在該影像中。 中繼資料的一些範例包括：

* 資產名稱。
* 上次修改的時間和日期。
* 資產儲存在存放庫中的大小。
* 包含在其中的資料夾名稱。
* 相關資產或套用的標籤。

以上是[!DNL Experience Manager]可以管理資產的基本中繼資料屬性，可讓使用者檢視所有資產。 例如，嘗試探索最近新增或修改的資產時，依上次修改日期排序資產會很有用。

例如，您可以將高階資料新增至數位資產：

* 資產型別（是影像、視訊、音訊剪輯或檔案？）。
* 資產擁有者。
* 資產標題。
* 資產的說明。
* 指派給資產的標籤。

更多中繼資料可協助您進一步將資產分類，且隨著數位資訊量成長，將有所幫助。 您可以僅根據檔案名稱管理數百個檔案。 然而，此方法並不能調整規模。隨著相關人數和管理的資產數量增加，此方法尚嫌不足。

隨著中繼資料增加，數位資產的價值也會成長，這是因為資產會變得

* 更易於存取 - 系統和使用者可以更輕鬆找到資產。
* 更易於管理 - 您可以更容易找到具有同一組屬性的資產，並將變更套用到這些資產。
* 完整 - 資產攜帶更多資訊和包含更多中繼資料的內容。

基於這些原因，[!DNL Assets]為您提供建立、管理和交換數位資產的中繼資料的正確方式。

## 中繼資料的型別 {#types-of-metadata}

中繼資料分為技術、資訊和管理中繼資料。

### 技術中繼資料

技術中繼資料專注於數位資產的技術方面，提供與下列相關的重要資訊：

* 檔案大小
* 格式
* 解決方法
* 尺寸
* 色彩模式

這類中繼資料可協助使用者瞭解並有效使用數位資產。

### 資訊性中繼資料

資訊性中繼資料提供描述性資訊，可增進內容瞭解、協助內容探索和可搜尋性。 其中包含關鍵字、註解及說明。 <br>例如，在Experience Manager Assets中管理視訊時，我們可以包含下列資訊中繼資料：

* **關鍵字**：行銷、產品發佈、促銷
* **Caption**：介紹我們最新產品，以及令人興奮的功能
* **描述**：視訊內容的詳細概觀。

### 管理中繼資料

管理中繼資料會處理數位資產的管理方面。 它可確儲存取控制、法規遵循，以及管理數位資產管理系統中資產的整體生命週期。 其中包含下列相關資訊：

* 資產所有權
* 使用許可權
* 權限
* 其他管理詳細資料

此中繼資料型別可確保有效的資產管理、存取控制和法規遵循。

<!-- Learn more about [metadata best practices](metadata-best-practices.md) to manage your digital assets effectively. -->

<!-- The two basic types of metadata are technical metadata and descriptive metadata.

Technical metadata is useful for software applications that are dealing with digital assets and should not be maintained manually. [!DNL Experience Manager Assets] and other software automatically determine technical metadata and the metadata may change when the asset is modified. The available technical metadata of an asset depends largely on the file type of the asset. Some examples of technical metadata are:

* Size of a file.
* Dimensions (height and width) of an image.
* Bit rate of an audio or video file.
* Resolution (level of detail) of an image.

Descriptive metadata is metadata concerned with the application domain, for example, the business that an asset is coming from. Descriptive metadata cannot be determined automatically. It is created manually or semi-automatically. For example, a GPS-enabled camera can automatically track the latitude and longitude and add geotag the image.

The cost of manually creating descriptive metadata information is high. So, standards are established to ease the exchange of metadata across software systems and organizations. [!DNL Experience Manager Assets] supports all relevant standards for metadata management. -->

## 中繼資料和上次修改 {#last-modification}

資產的最後修改日期反映上次修改資產原始檔案的時間。 因此，修改日期和使用者僅在以下情況下變更：

* 已上傳資產的新版本
* 已重新處理資產

上次修改日期和使用者不會變更：

* 資產移動或重新命名時
* 將資產簽出、簽入或版本時
* 發佈或取消發佈資產時
* 關於中繼資料更新
* 參考或集合更新

## 編碼標準 {#encoding-standards}

有多種方式可將中繼資料內嵌在檔案中。 支援一系列編碼標準：

* XMP： [!DNL Assets]用來將擷取的中繼資料儲存在存放庫中。
* ID3：適用於音訊和視訊檔案。
* Exif：適用於影像檔案。
* 其他/舊版：來自[!DNL Microsoft Word]、[!DNL PowerPoint]、[!DNL Excel]等。

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP)是[!DNL Experience Manager Assets]用於所有中繼資料管理的開放標準。 此標準提供通用中繼資料編碼，可嵌入至所有檔案格式。 Adobe和其他公司支援XMP標準，因為它提供豐富的內容模型。 XMP標準版和[!DNL Experience Manager Assets]版的使用者擁有強大的平台可建置。 如需詳細資訊，請參閱[XMP](https://www.adobe.com/products/xmp.html)。

### ID3 {#id}

當您在電腦或可攜式MP3播放器上播放數位音訊檔案時，會顯示儲存在這些ID3標籤中的資料。

ID3標籤是專為MP3檔案格式所設計。 格式的其他資訊：

* ID3標籤可用於MP3和mp3PRO檔案。
* WAV沒有標籤。
* WMA擁有不允許開放原始碼實作的專屬標籤。
* Ogg Vorbis使用內嵌於Ogg容器中的Xiph註解。
* AAC使用專屬標籤格式。

### Exif {#exif}

可交換影像檔案格式(Exif)是數位攝影中最常用的中繼資料格式。 它提供一種以多種檔案格式(例如JPEG、TIFF、RIFF和WAV)內嵌中繼資料屬性的固定辭彙的方法。 Exif會將中繼資料儲存為中繼資料名稱和中繼資料值的配對。 這些中繼資料名稱 — 值組也稱為標籤，不要與[!DNL Experience Manager]中的標籤混淆。 現代數位相機可建立Exif中繼資料，而現代圖形軟體則支援這些中繼資料。 Exif格式是中繼資料管理（尤其是影像）的最低通用分母。

Exif的一個主要限制是一些常見的影像檔案格式(例如BMP、GIF或PNG)不支援它。

Exif定義的中繼資料欄位通常屬於技術性質，在描述性中繼資料管理中的用途有限。 因此，[!DNL Experience Manager Assets]提供Exif屬性到[通用中繼資料結構描述](metadata-schemas.md)和XMP的對應。

#### 其他中繼資料 {#other-metadata}

可從檔案嵌入的其他中繼資料包括[!DNL Microsoft Word]、[!DNL PowerPoint]、[!DNL Excel]等。

## 管理數位資產的中繼資料 {#manage-assets-metadata}

Enterprise Manager Assets可讓您同時編輯多個資產的中繼資料，以便快速將常見的中繼資料變更大量傳播至資產。 使用[!UICONTROL 屬性]頁面將中繼資料屬性變更為通用值，或新增或修改標籤。 若要自訂中繼資料「屬性」頁面，包括新增、修改、刪除中繼資料屬性，請使用「架構」編輯器。

>[!NOTE]
>
>大量編輯方法適用於資料夾或集合中可用的資產。 對於跨資料夾可用的資產，或符合共同條件的資產，可在搜尋[後](/help/assets/search-assets.md#metadata-updates)大量更新中繼資料。

1. 導覽至您要編輯的資產位置。
1. 選取您要編輯其一般屬性的資產。
1. 從工具列中選取&#x200B;**[!UICONTROL 屬性]**&#x200B;以開啟所選資產的[!UICONTROL 屬性]頁面。

   >[!NOTE]
   >
   >當您選取多個資產時，系統會為資產選取最低的一般父級表單。 換句話說，[!UICONTROL 屬性]頁面只顯示所有個別資產的[!UICONTROL 屬性]頁面所共有的中繼資料欄位。

1. 修改各種標籤下所選資產的中繼資料屬性。
1. 若要檢視特定資產的中繼資料編輯器，請取消選取清單中剩餘的資產。 中繼資料編輯器欄位會填入特定資產的中繼資料。

   >[!NOTE]
   >
   >* 在[!UICONTROL 屬性]頁面中，您可以取消選取範圍以從資產清單移除資產。 資產清單預設會選取所有資產。 您從清單中移除的資產中繼資料不會更新。
   >* 在資產清單頂端，選取&#x200B;**[!UICONTROL 標題]**&#x200B;附近的核取方塊，以在選取資產和清除清單之間切換。

1. 若要為資產選取不同的中繼資料結構，請從工具列選取&#x200B;**[!UICONTROL 設定]**，然後選取所需的結構。 儲存變更。
1. 若要在包含多個值的欄位中，將新中繼資料與現有中繼資料一起附加，請選取「附 **[!UICONTROL 加模式」]**。如果您未選取此選項，新的中繼資料會取代欄位中現有的中繼資料。選取&#x200B;**[!UICONTROL 提交]**。

   >[!CAUTION]
   >
   >對於單值欄位，即使您選擇「附加模式」，新元資料也不會附加到欄位中的現 **[!UICONTROL 有值]**。

## 使用處理設定檔的自訂中繼資料 {#metadata-compute-service}

作為[!DNL Cloud Service]的Assets可以使用雲端原生服務產生資產的自訂中繼資料。 設定處理設定檔以產生自訂中繼資料。 請參閱[如何使用處理設定檔](/help/assets/asset-microservices-configure-and-use.md#use-profiles)。

![中繼資料轉譯正在處理設定檔](assets/processing-profile-metadata.png)

>[!TIP]
>
>一個資料夾只能套用一個處理設定檔。 若要將多個處理套用至資料夾中的資產，請將更多選項新增至單一處理設定檔。 例如，單一設定檔可以產生轉譯、轉碼資產、產生自訂中繼資料等。 您可以對每個任務套用MIME型別篩選器，這樣就能針對所需的檔案格式觸發適當的任務。

<!-- TBD: Commenting as Web Console is not available. Document the appropriate OSGi config method if available in CS.

## Configure limit for bulk metadata update {#configlimit}

To prevent DOS-like situation, [!DNL Experience Manager] limits the number of parameters supported in a Sling request. When updating metadata of many assets in one go, you may reach the limit and the metadata does not get updated for more assets. [!DNL Experience Manager] generates the following warning in the logs:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

To change the limit, access Web Console ( **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**) and change the value of **[!UICONTROL Maximum POST Parameters]** in **[!UICONTROL Apache Sling Request Parameter Handling]** OSGi configuration.
-->

## 中繼資料結構 {#metadata-schemata}

中繼資料結構是一組預先定義的中繼資料屬性定義，可用於各種應用程式。 屬性一律與資產相關聯，這表示屬性與資源「相關」。

如果沒有符合您需求的中繼資料結構，您也可以自行設計中繼資料結構。 不要複製現有的資訊。 在組織內，分隔結構描述可讓您更輕鬆地共用中繼資料。 [!DNL Experience Manager]為您提供最受歡迎中繼資料結構的預設清單。 清單可協助您快速啟動中繼資料策略，並快速挑選所需的中繼資料屬性。

支援的中繼資料結構描述如下所列。

### 標準中繼資料 {#standard-metadata}

* DC - [!DNL Dublin Core]是重要且廣泛使用的中繼資料集。
* DICOM — 醫學的數位影像與通訊。
* `Iptc4xmpCore`和`iptc4xmpExt` — 國際新聞通訊標準包含許多特定主題的中繼資料。
* RDF — 資源說明架構 — 用於一般語意Web中繼資料。
* XMP - [!DNL Extensible Metadata Platform]。
* `xmpBJ` — 基本工作票證。

### 應用程式專屬中繼資料 {#application-specific-metadata}

應用程式專屬中繼資料包括技術和描述性中繼資料。 如果您使用這類中繼資料，其他應用程式可能無法使用中繼資料。 例如，不同的影像演算應用程式可能無法存取[!DNL Adobe Photoshop]中繼資料。 您可以建立工作流程步驟，將應用程式特定屬性變更為標準屬性。

* ACDSee - [!DNL ACDSee]程式管理的中繼資料。 請參閱[www.acdsee.com/](https://www.acdsee.com/)。
* 相簿 — [!DNL Adobe Photoshop Album]。
* CQ — 由[!DNL Experience Manager Assets]使用。
* DAM - [!DNL Experience Manager Assets]使用。
* DEX - [Optima SC Description Explorer](https://www.optimasc.com/products/dex/index.html)是Windows作業系統中繼資料和檔案管理工具的集合。
* CRS - [Adobe Photoshop Camera Raw](https://helpx.adobe.com/tw/camera-raw/using/introduction-camera-raw.html)。
* LR - [!DNL Adobe Lightroom]。
* MediaPro - [iView MediaPro](https://en.wikipedia.org/wiki/Phase_One_Media_Pro)。
* MicrosoftPhoto和MP - Microsoft像片。
* PDF和PDF/X。
* Photoshop和psAux - [!DNL Adobe Photoshop]。

### Digital Rights Management中繼資料 {#digital-rights-management-metadata}

* 副本 — [!DNL Creative Commons]。
* [!DNL XMPRights]。
* PLUS - [Picture Licensing Universal System](https://www.useplus.com)。
<!--THIS LINK IS 404 WITH NO SUITABLE REPLACEMENT * PRISM - [Publishing Requirements for Industry Standard Metadata](https://www.idealliance.org/prism-metadata). -->
* PRL — 稜鏡許可權語言。
* PUR - PRISM使用許可權。
* `xmpPlus` - PLUS與XMP整合。

### 攝影專用中繼資料 {#photography-specific-metadata}

* Exif — 攝影機的技術資訊，包括GPS位置。
* CRS - [!DNL Camera Raw]結構描述。
* `iptc4xmpCore`和`iptc4xmpExt`。
* TIFF — 影像中繼資料(不僅適用於TIFF影像)。

### 列印特定中繼資料 {#print-specific-metadata}

* PDF和PDF/X - Adobe PDF和協力廠商應用程式。
<!--THIS LINK IS 404 WITH NO SUITABLE REPLACEMENT * PRISM - [Publishing Requirements for Industry Standard Metadata](https://www.idealliance.org/prism-metadata). -->
* XMP - [!DNL Extensible Metadata Platform]。
* `xmpPG` — 分頁文字的XMP中繼資料。

### 多媒體專屬中繼資料 {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media]。
* `xmpMM` — 媒體管理。

## 中繼資料導向的工作流程 {#metadata-driven-workflows}

建立中繼資料導向工作流程可協助您自動化部分流程，進而提高效率。 在中繼資料驅動的工作流程中，工作流程管理系統會讀取工作流程，並因此執行一些預先定義的動作。 例如，部分使用中繼資料導向工作流程的方式：

* 工作流程可檢查影像是否具有標題。 如果不適用，系統會通知以新增標題。
* 工作流程可檢查資產上的版權宣告是否允許發佈。 因此，系統會將資產傳送至一台或多台伺服器。
* 工作流程可以檢查未預先定義、強制中繼資料的資產，或含有&#x200B;*無效*&#x200B;中繼資料的資產。

**另請參閱**

* [翻譯資產](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [資產支援的檔案格式](file-format-support.md)
* [搜尋資產](search-assets.md)
* [連接的資產](use-assets-across-connected-assets-instances.md)
* [資產報表](asset-reports.md)
* [中繼資料結構描述](metadata-schemas.md)
* [下載資產](download-assets-from-aem.md)
* [搜尋 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [大量中繼資料匯入](metadata-import-export.md)
* [發佈資產至 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [XMP 中繼資料](xmp-metadata.md)
>* [如何編輯或新增中繼資料](meta-edit.md)
