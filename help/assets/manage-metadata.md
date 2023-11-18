---
title: 管理數位資產的中繼資料
description: 瞭解中繼資料的型別和方式 [!DNL Adobe Experience Manager Assets] 協助管理資產的中繼資料，讓資產更輕鬆分類及組織。 [!DNL Experience Manager] 可讓您根據資產的中繼資料自動整理和處理資產。
contentOwner: AG
mini-toc-levels: 1
feature: Asset Management,Metadata
role: User,Architect,Admin
exl-id: 73a82bc2-1dda-4090-b7ee-29d1a632ba25
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '2000'
ht-degree: 8%

---

# 管理數位資產的中繼資料 {#managing-metadata-for-digital-assets}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/metadata.html?lang=en) |
| AEM as a Cloud Service  | 本文章 |

[!DNL Adobe Experience Manager Assets] 保留每個資產的中繼資料。 它可讓您更輕鬆地分類及組織資產，並協助尋找特定資產的人。 能夠自上傳至的檔案擷取中繼資料 [!DNL Experience Manager Assets]，中繼資料管理與創意工作流程整合。 有了使用資產保留和管理中繼資料的功能，您可以根據資產的中繼資料自動組織和處理資產。

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

以上是基本的中繼資料屬性， [!DNL Experience Manager] 可管理資產，讓使用者檢視所有資產。 例如，嘗試探索最近新增或修改的資產時，依上次修改日期排序資產會很有用。

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

基於這些原因， [!DNL Assets] 提供建立、管理和交換數位資產中繼資料的合適方式。

## 中繼資料的型別 {#types-of-metadata}

兩種基本的中繼資料型別是技術中繼資料和描述性中繼資料。

技術中繼資料適用於處理數位資產的軟體應用程式，且不應手動維護。 [!DNL Experience Manager Assets] 和其他軟體會自動決定技術中繼資料，而中繼資料可能會在資產修改時變更。 資產可用的技術中繼資料主要取決於資產的檔案型別。 技術中繼資料的一些範例包括：

* 檔案的大小。
* 影像的Dimension（高度和寬度）。
* 音訊或視訊檔案的位元速率。
* 影像的解析度（詳細程度）。

描述性中繼資料是與應用程式網域相關的中繼資料，例如資產來自的業務。 描述性中繼資料無法自動判斷。 它是手動或半自動建立的。 例如，啟用GPS的相機可以自動追蹤經緯度，並在影像中新增地理標籤。

手動建立描述性中繼資料資訊的成本很高。 因此，我們建立了各種標準，以便於在軟體系統和組織之間交換中繼資料。 [!DNL Experience Manager Assets] 支援中繼資料管理的所有相關標準。

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

* XMP：使用者 [!DNL Assets] 將擷取的中繼資料儲存在存放庫中。
* ID3：適用於音訊和視訊檔案。
* Exif：適用於影像檔案。
* 其他/舊版：從 [!DNL Microsoft Word]， [!DNL PowerPoint]， [!DNL Excel]、等等。

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP)是一種開放標準，用於 [!DNL Experience Manager Assets] 用於所有中繼資料管理。 此標準提供通用中繼資料編碼，可嵌入至所有檔案格式。 Adobe和其他公司支援XMP標準，因為它提供豐富的內容模型。 XMP標準的使用者和 [!DNL Experience Manager Assets] 擁有強大的平台作為建置基礎。 如需詳細資訊，請參閱 [XMP](https://www.adobe.com/products/xmp.html).

### ID3 {#id}

當您在電腦或可攜式MP3播放器上播放數位音訊檔案時，會顯示儲存在這些ID3標籤中的資料。

ID3標籤是專為MP3檔案格式所設計。 格式的其他資訊：

* ID3標籤可用於MP3和mp3PRO檔案。
* WAV沒有標籤。
* WMA擁有不允許開放原始碼實作的專屬標籤。
* Ogg Vorbis使用內嵌於Ogg容器中的Xiph註解。
* AAC使用專屬標籤格式。

### Exif {#exif}

可交換影像檔案格式(Exif)是數位攝影中最常用的中繼資料格式。 它提供一種以多種檔案格式(例如JPEG、TIFF、RIFF和WAV)內嵌中繼資料屬性的固定辭彙的方法。 Exif會將中繼資料儲存為中繼資料名稱和中繼資料值的配對。 這些中繼資料名稱 — 值組也稱為標籤，切勿與中的標籤混淆 [!DNL Experience Manager]. 現代數位相機可建立Exif中繼資料，而現代圖形軟體則支援這些中繼資料。 Exif格式是中繼資料管理（尤其是影像）的最低通用分母。

Exif的一個主要限制是一些常見的影像檔案格式(例如BMP、GIF或PNG)不支援它。

Exif定義的中繼資料欄位通常屬於技術性質，在描述性中繼資料管理中的用途有限。 基於這個原因， [!DNL Experience Manager Assets] 提供Exif屬性對映至 [常見中繼資料結構](metadata-schemas.md) 並進入XMP。

#### 其他中繼資料 {#other-metadata}

其他可從檔案嵌入的中繼資料包括 [!DNL Microsoft Word]， [!DNL PowerPoint]， [!DNL Excel]、等等。

## 管理數位資產的中繼資料 {#manage-assets-metadata}

Enterprise Manager Assets可讓您同時編輯多個資產的中繼資料，以便快速將常見的中繼資料變更大量傳播至資產。 使用 [!UICONTROL 屬性] 頁面，將中繼資料屬性變更為通用值或新增或修改標籤。 若要自訂中繼資料「屬性」頁面，包括新增、修改、刪除中繼資料屬性，請使用「架構」編輯器。

>[!NOTE]
>
>大量編輯方法適用於資料夾或集合中可用的資產。 對於跨資料夾可用的資產或符合共同條件的資產，可以 [搜尋後大量更新中繼資料](/help/assets/search-assets.md#metadata-updates).

1. 導覽至您要編輯的資產位置。
1. 選取您要編輯其一般屬性的資產。
1. 從工具列中選取 **[!UICONTROL 屬性]** 以開啟 [!UICONTROL 屬性] 所選資產的頁面。

   >[!NOTE]
   >
   >當您選取多個資產時，系統會為資產選取最低的一般父級表單。 換言之， [!UICONTROL 屬性] 頁面只會顯示跨頁面共用的中繼資料欄位 [!UICONTROL 屬性] 所有個別資產的頁面。

1. 修改各種標籤下所選資產的中繼資料屬性。
1. 若要檢視特定資產的中繼資料編輯器，請取消選取清單中剩餘的資產。 中繼資料編輯器欄位會填入特定資產的中繼資料。

   >[!NOTE]
   >
   >* 在 [!UICONTROL 屬性] 頁面上，您可以取消選取範圍，從資產清單中移除資產。 資產清單預設會選取所有資產。 您從清單中移除的資產中繼資料不會更新。
   >* 在資產清單頂端，選取附近的核取方塊 **[!UICONTROL 標題]** 以在選取資產和清除清單之間切換。

1. 若要為資產選取不同的中繼資料結構，請選取 **[!UICONTROL 設定]** 從工具列中，並選取所需的結構描述。 儲存變更。
1. 若要在包含多個值的欄位中，將新中繼資料與現有中繼資料一起附加，請選取「附 **[!UICONTROL 加模式」]**。如果您未選取此選項，新的中繼資料會取代欄位中現有的中繼資料。選取 **[!UICONTROL 提交]**.

   >[!CAUTION]
   >
   >對於單值欄位，即使您選擇「附加模式」，新元資料也不會附加到欄位中的現 **[!UICONTROL 有值]**。

## 使用處理設定檔的自訂中繼資料 {#metadata-compute-service}

Assets as a [!DNL Cloud Service] 可使用雲端原生服務為資產產生自訂中繼資料。 設定處理設定檔以產生自訂中繼資料。 另請參閱 [如何使用處理設定檔](/help/assets/asset-microservices-configure-and-use.md#use-profiles).

![處理設定檔中的中繼資料轉譯](assets/processing-profile-metadata.png)

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

如果沒有符合您需求的中繼資料結構，您也可以自行設計中繼資料結構。 不要複製現有的資訊。 在組織內，分隔結構描述可讓您更輕鬆地共用中繼資料。 [!DNL Experience Manager] 為您提供最受歡迎中繼資料結構的預設清單。 清單可協助您快速啟動中繼資料策略，並快速挑選所需的中繼資料屬性。

支援的中繼資料結構描述如下所列。

### 標準中繼資料 {#standard-metadata}

* DC - [!DNL Dublin Core] 是一組重要且廣泛使用的中繼資料。
* DICOM — 醫學的數位影像與通訊。
* `Iptc4xmpCore` 和 `iptc4xmpExt`  — 國際新聞通訊標準包含許多特定主題的中繼資料。
* RDF — 資源說明架構 — 用於一般語意Web中繼資料。
* XMP - [!DNL Extensible Metadata Platform].
* `xmpBJ`  — 基本工作票證。

### 應用程式專屬中繼資料 {#application-specific-metadata}

應用程式專屬中繼資料包括技術和描述性中繼資料。 如果您使用這類中繼資料，其他應用程式可能無法使用中繼資料。 例如，不同的影像演算應用程式可能無法存取 [!DNL Adobe Photoshop] 中繼資料。 您可以建立工作流程步驟，將應用程式特定屬性變更為標準屬性。

* ACDSee — 由管理的中繼資料 [!DNL ACDSee] 程式。 另請參閱 [www.acdsee.com/](https://www.acdsee.com/).
* 相簿 —  [!DNL Adobe Photoshop Album].
* CQ — 使用者 [!DNL Experience Manager Assets].
* DAM — 使用者 [!DNL Experience Manager Assets].
* DEX - [Optima SC說明總管](https://www.optimasc.com/products/dex/index.html) 是Windows作業系統中繼資料和檔案管理的工具集合。
* CRS - [Adobe Photoshop Camera Raw](https://helpx.adobe.com/camera-raw/using/introduction-camera-raw.html).
* LR - [!DNL Adobe Lightroom].
* MediaPro - [iView MediaPro](https://en.wikipedia.org/wiki/Phase_One_Media_Pro).
* MicrosoftPhoto和MP - Microsoft像片。
* PDF和PDF/X。
* Photoshop和psAux - [!DNL Adobe Photoshop].

### Digital Rights Management中繼資料 {#digital-rights-management-metadata}

* CC - [!DNL Creative Commons].
* [!DNL XMPRights]。
* 加 —  [圖片授權通用系統](https://www.useplus.com).
* 稜鏡 —  [發佈產業標準中繼資料的需求](https://www.idealliance.org/prism-metadata).
* PRL — 稜鏡許可權語言。
* PUR - PRISM使用許可權。
* `xmpPlus` - PLUS與XMP整合。

### 攝影專用中繼資料 {#photography-specific-metadata}

* Exif — 攝影機的技術資訊，包括GPS位置。
* CRS - [!DNL Camera Raw] 綱要。
* `iptc4xmpCore` 和 `iptc4xmpExt`.
* TIFF — 影像中繼資料(不僅適用於TIFF影像)。

### 列印特定中繼資料 {#print-specific-metadata}

* PDF與PDF/X - Adobe PDF和協力廠商應用程式。
* 稜鏡 —  [發佈產業標準中繼資料的需求](https://www.idealliance.org/prism-metadata).
* XMP - [!DNL Extensible Metadata Platform].
* `xmpPG`  — 分頁文字的XMP中繼資料。

### 多媒體專屬中繼資料 {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media].
* `xmpMM`  — 媒體管理。

## 中繼資料導向的工作流程 {#metadata-driven-workflows}

建立中繼資料導向工作流程可協助您自動化部分流程，進而提高效率。 在中繼資料驅動的工作流程中，工作流程管理系統會讀取工作流程，並因此執行一些預先定義的動作。 例如，部分使用中繼資料導向工作流程的方式：

* 工作流程可檢查影像是否具有標題。 如果不適用，系統會通知以新增標題。
* 工作流程可檢查資產上的版權宣告是否允許發佈。 因此，系統會將資產傳送至一台或多台伺服器。
* 工作流程可以檢查沒有預先定義、強制中繼資料的資產，或具有 *無效* 中繼資料。

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

>[!MORELIKETHIS]
>
>* [XMP 中繼資料](xmp-metadata.md)
>* [如何編輯或新增中繼資料](meta-edit.md)
