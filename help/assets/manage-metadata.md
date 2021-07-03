---
title: 管理數位資產的中繼資料
description: 了解中繼資料的類型，並了解如何 [!DNL Adobe Experience Manager Assets] helps manage metadata for assets to allow easier categorization and organization of assets. [!DNL Experience Manager] 根據資產的中繼資料自動組織和處理資產。
contentOwner: AG
mini-toc-levels: 1
feature: 資產管理，元資料
role: User,Architect,Admin
exl-id: 73a82bc2-1dda-4090-b7ee-29d1a632ba25
source-git-commit: a2c2a1f4ef4a8f0cf1afbba001d24782a6a2a24e
workflow-type: tm+mt
source-wordcount: '1857'
ht-degree: 3%

---

# 管理數位資產的中繼資料 {#managing-metadata-for-digital-assets}

[!DNL Adobe Experience Manager Assets] 保留每個資產的中繼資料。它可讓資產分類和組織更輕鬆，並協助尋找特定資產的人。 能夠從上傳至[!DNL Experience Manager Assets]的檔案中擷取中繼資料，中繼資料管理與創意工作流程整合。 您可以使用資產保留和管理中繼資料，並根據資產的中繼資料自動組織和處理資產。

<!-- 
* [Metadata Schemata Reference](meta-ref.md)
-->

## 為什麼我們需要元資料 {#why-metadata}

中繼資料是指資料的相關資料。 在這方面，資料是指您的數位資產，例如影像。 中繼資料對於有效管理資產至關重要。

中繼資料是資產可用之所有資料的集合，但不一定包含在該影像中。 中繼資料的一些範例為：

* 資產名稱。
* 上次修改的時間和日期。
* 儲存在存放庫中的資產大小。
* 資料夾的名稱。
* 相關資產或套用的標籤。

以上是[!DNL Experience Manager]可針對資產管理的基本中繼資料屬性，可讓使用者查看所有資產。 例如，在嘗試探索最近新增的資產時，依上次修改日期排序資產很實用。

您可以新增更多高階資料至數位資產，例如：

* 資產的類型（是影像、視訊、音訊剪輯或檔案？）。
* 資產擁有者。
* 資產的標題。
* 資產說明。
* 指派給資產的標籤。

更多中繼資料可協助您進一步分類資產，並隨著數位資訊量增加而有所幫助。 僅根據檔案名稱即可管理數百個檔案。 不過，此方法無法擴充。 當參與人數和管理的資產數量增加時，這個數字就不夠。

隨著中繼資料的增加，數位資產的值會隨著資產的增加而增加，

* 更容易訪問 — 系統和用戶可以輕鬆找到它。
* 易於管理 — 您可以更輕鬆找到具有相同屬性集的資產，並套用變更。
* 完整 — 資產包含更多資訊和內容，並包含更多中繼資料。

基於這些原因，[!DNL Assets]提供您建立、管理和交換數位資產中繼資料的正確方式。

## 中繼資料的類型 {#types-of-metadata}

兩種基本的中繼資料類型是技術中繼資料和描述性中繼資料。

技術中繼資料對於處理數位資產且不應手動維護的軟體應用程式非常有用。 [!DNL Experience Manager Assets] 而其他軟體則自動確定技術元資料，當資產被修改時，元資料可能會改變。資產的可用技術中繼資料主要取決於資產的檔案類型。 技術中繼資料的一些範例為：

* 檔案大小。
* Dimension（高度和寬度）。
* 音訊或視訊檔案的位元速率。
* 影像的解析度（詳細程度）。

描述性中繼資料是與應用程式網域相關的中繼資料，例如資產來自的業務。 無法自動確定描述性中繼資料。 系統會手動或半自動建立。 例如，啟用GPS的相機可自動追蹤經緯度，並新增地理標籤影像。

手動建立描述性中繼資料資訊的成本很高。 因此，制定標準是為了方便跨軟體系統和組織交換元資料。 [!DNL Experience Manager Assets] 支援元資料管理的所有相關標準。

## 編碼標準 {#encoding-standards}

在檔案中內嵌中繼資料有多種方式。 支援一系列編碼標準：

* XMP:由[!DNL Assets]用來在儲存庫中儲存擷取的中繼資料。
* ID3:用於音頻和視頻檔案。
* 例如：（適用於影像檔案）。
* 其他/舊版：從[!DNL Microsoft Word]、[!DNL PowerPoint]、[!DNL Excel]等。

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP)是開放標準，用於所有中 [!DNL Experience Manager Assets] 繼資料管理。此標準提供通用中繼資料編碼，可嵌入到所有檔案格式中。 Adobe和其他公司支援XMP standard，因為它提供豐富的內容模型。 XMP standard和[!DNL Experience Manager Assets]的使用者擁有強大的平台可以建立。 如需詳細資訊，請參閱[XMP](https://www.adobe.com/products/xmp.html)。

### ID3 {#id}

當您在電腦或筆記型電腦MP3播放器上播放數位音訊檔案時，儲存在這些ID3標籤中的資料會顯示。

ID3標籤是為MP3檔案格式而設計。 格式的其他資訊：

* ID3標籤適用於MP3和mp3PRO檔案。
* WAV沒有標籤。
* WMA具有不允許開放原始碼實作的專屬標籤。
* Ogg Vorbis使用嵌入在Ogg容器中的Xiph注釋。
* AAC使用專屬標籤格式。

### Exif {#exif}

可交換影像檔案格式(Exif)是數位攝影中最常用的中繼資料格式。 它提供了以多種檔案格式（如JPEG、TIFF、RIFF和WAV）嵌入元資料屬性的固定辭匯的方法。 Exif將中繼資料儲存為中繼資料名稱和中繼資料值的配對。 這些元資料名稱值配對也稱為標籤，請勿與[!DNL Experience Manager]中的標籤混淆。 現代數位相機可建立Exif元資料，現代圖形軟體可支援它。 Exif格式是中繼資料管理的最低公分母，尤其是影像。

Exif的一個主要限制是一些常見的影像檔案格式（如BMP、GIF或PNG）不支援它。

Exif定義的中繼資料欄位通常屬於技術性質，在描述性中繼資料管理中的使用有限。 因此，[!DNL Experience Manager Assets]提供Exif屬性到[通用元資料結構](metadata-schemas.md)和XMP的映射。

#### 其他中繼資料 {#other-metadata}

可從檔案嵌入的其他元資料包括[!DNL Microsoft Word]、[!DNL PowerPoint]、[!DNL Excel]等。

## 管理數位資產的中繼資料 {#manage-assets-metadata}

Enterprise Manager Assets可讓您同時編輯多個資產的中繼資料，以便快速將通用中繼資料變更大量傳播至資產。 使用[!UICONTROL 屬性]頁可將元資料屬性更改為公共值，或添加或修改標籤。 要自定義元資料屬性頁，包括添加、修改、刪除元資料屬性，請使用結構編輯器。

>[!NOTE]
>
>大量編輯方法適用於資料夾或集合中的可用資產。 對於可跨資料夾使用或符合通用條件的資產，可以在搜尋](/help/assets/search-assets.md#metadata-updates)後，大量更新中繼資料。[

1. 導覽至您要編輯的資產所在位置。
1. 選取您要編輯公用屬性的資產。
1. 從工具列中，點選/按一下「屬性」**[!UICONTROL 「屬性」]**&#x200B;以開啟所選資產的「屬性」[!UICONTROL 「屬性」]頁面。

   >[!NOTE]
   >
   >選取多個資產時，系統會為資產選取最低的共同父表單。 換言之，「[!UICONTROL 屬性]」頁面只會顯示所有個別資產之「[!UICONTROL 屬性]」頁面中共有的中繼資料欄位。

1. 修改各種標籤下所選資產的中繼資料屬性。
1. 若要檢視特定資產的中繼資料編輯器，請取消在清單中選取剩餘資產。 中繼資料編輯器欄位會填入特定資產的中繼資料。

   >[!NOTE]
   >
   >* 在[!UICONTROL 屬性]頁面中，您可以取消選取項目，從資產清單中移除資產。 資產清單預設會選取所有資產。 您從清單中移除的資產中繼資料不會更新。
   >* 在資產清單頂端，選取&#x200B;**[!UICONTROL Title]**&#x200B;附近的核取方塊，在選取資產和清除清單之間切換。


1. 若要為資產選取不同的中繼資料結構，請從工具列點選/按一下「**[!UICONTROL 設定]**」，然後選取所需的結構。 儲存變更。
1. 若要在包含多個值的欄位中，將新中繼資料與現有中繼資料一起附加，請選取「附 **[!UICONTROL 加模式」]**。如果您未選取此選項，新的中繼資料會取代欄位中現有的中繼資料。點選/按一 **[!UICONTROL 下提交]**。

   >[!CAUTION]
   >
   >對於單值欄位，即使您選擇「附加模式」，新元資料也不會附加到欄位中的現 **[!UICONTROL 有值]**。

## 使用處理設定檔的自訂中繼資料 {#metadata-compute-service}

作為[!DNL Cloud Service]的資產可以使用雲端原生服務為資產產生自訂中繼資料。 設定處理設定檔以產生自訂中繼資料。 請參閱[如何使用處理設定檔](/help/assets/asset-microservices-configure-and-use.md#use-profiles)。

![處理設定檔中的中繼資料轉譯](assets/processing-profile-metadata.png)

>[!TIP]
>
>只能將一個處理設定檔套用至資料夾。 若要對資料夾中的資產套用多個處理，請新增更多選項至單一處理設定檔。 例如，單一設定檔可產生轉譯、轉碼資產、產生自訂中繼資料等。 您可以為每個任務應用MIME類型篩選器，以便根據所需的檔案格式觸發相應的任務。

<!-- TBD: Commenting as Web Console is not available. Document the appropriate OSGi config method if available in CS.

## Configure limit for bulk metadata update {#configlimit}

To prevent DOS-like situation, [!DNL Experience Manager] limits the number of parameters supported in a Sling request. When updating metadata of many assets in one go, you may reach the limit and the metadata does not get updated for more assets. [!DNL Experience Manager] generates the following warning in the logs:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

To change the limit, access Web Console ( **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**) and change the value of **[!UICONTROL Maximum POST Parameters]** in **[!UICONTROL Apache Sling Request Parameter Handling]** OSGi configuration.
-->

## 中繼資料結構 {#metadata-schemata}

中繼資料結構是可用於各種應用程式的一組預先定義的中繼資料屬性定義。 屬性一律與資產相關聯，這表示屬性是資源的「關於」。

如果沒有符合您需求的中繼資料結構，您也可以設計您自己的中繼資料結構。 請勿複製現有資訊。 在組織內，區隔架構可讓您更輕鬆共用中繼資料。 [!DNL Experience Manager] 提供最受歡迎中繼資料結構的預設清單。此清單可協助您快速啟動中繼資料策略，並快速挑選您需要的中繼資料屬性。

支援的中繼資料結構列於下方。

### 標準中繼資料 {#standard-metadata}

* DC - [!DNL Dublin Core]是一組重要且廣泛使用的元資料。
* DICOM — 醫學中的數字影像和通信。
* `Iptc4xmpCore` 和 —  `iptc4xmpExt` 《國際新聞通訊標準》包含許多主題特定的元資料。
* RDF — 資源描述框架 — 用於通用語義Web元資料。
* XMP - [!DNL Extensible Metadata Platform]。
* `xmpBJ`  — 基本工作票證。

### 應用程式專屬中繼資料 {#application-specific-metadata}

應用程式專用中繼資料包含技術和描述性中繼資料。 如果您使用此類中繼資料，其他應用程式可能無法使用中繼資料。 例如，不同的影像呈現應用程式可能無法訪問[!DNL Adobe Photoshop]元資料。 您可以建立將應用程式特定屬性變更為標準屬性的工作流程步驟。

* ACDSee — 由[!DNL ACDSee]程式管理的元資料。 請參閱[www.acdsee.com/](https://www.acdsee.com/)。
* 專輯 — [!DNL Adobe Photoshop Album]。
* CQ — 由[!DNL Experience Manager Assets]使用。
* DAM — 由[!DNL Experience Manager Assets]使用。
* DEX - [Optima SC Description explorer](http://www.optimasc.com/products/dex/index.html)是用於Windows作業系統元資料和檔案管理的工具的集合。
* CRS - [Adobe Photoshop Camera Raw](https://helpx.adobe.com/camera-raw/using/introduction-camera-raw.html)。
* LR - [!DNL Adobe Lightroom]。
* MediaPro - [iView MediaPro](https://en.wikipedia.org/wiki/Phase_One_Media_Pro)。
* MicrosoftPhoto和MP - Microsoft Photo。
* PDF和PDF/X。
* Photoshop和psAux - [!DNL Adobe Photoshop]。

### Digital Rights Management中繼資料 {#digital-rights-management-metadata}

* CC - [!DNL Creative Commons].
* [!DNL XMPRights]。
* PLUS - [圖片許可通用系統](https://www.useplus.com)。
* PRISM - [發佈行業標準元資料的要求](https://www.idealliance.org/prism-metadata)。
* PRL — 稜鏡版權語言。
* PUR — 稜鏡使用權。
* `xmpPlus` - PLUS與XMP整合。

### 攝影專用中繼資料 {#photography-specific-metadata}

* Exif — 相機的技術資訊，包括GPS位置。
* CRS - [!DNL Camera Raw]架構。
* `iptc4xmpCore` 和 `iptc4xmpExt`.
* TIFF — 影像中繼資料（不僅適用於TIFF影像）。

### 特定於打印的元資料 {#print-specific-metadata}

* PDF和PDF/X - Adobe PDF和協力廠商應用程式。
* PRISM - [發佈行業標準元資料的要求](https://www.idealliance.org/prism-metadata)。
* XMP - [!DNL Extensible Metadata Platform]。
* `xmpPG`  — 分頁文字的XMP中繼資料。

### 多媒體特定中繼資料 {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media].
* `xmpMM`  — 媒體管理。

## 中繼資料導向的工作流程 {#metadata-driven-workflows}

建立中繼資料導向的工作流程可協助您自動執行某些程式，進而提高效率。 在元資料驅動的工作流中，工作流管理系統讀取該工作流，並因此執行一些預定義的操作。 例如，您可以使用中繼資料導向工作流程的一些方式：

* 工作流程可檢查影像是否具有標題。 若未這麼做，系統會通知您新增標題。
* 工作流程可以檢查資產上的版權聲明是否允許發佈。 因此，系統會將資產傳送至一部或另一部伺服器。
* 工作流程可以檢查沒有預先定義的強制中繼資料的資產，或具有&#x200B;*invalid*&#x200B;中繼資料的資產。

>[!MORELIKETHIS]
>
>* [XMP 中繼資料](xmp-metadata.md)
* [如何編輯或新增中繼資料](meta-edit.md)

