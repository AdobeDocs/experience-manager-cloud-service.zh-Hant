---
title: 管理您的數位資產的中繼資料 [!DNL Adobe Experience Manager]。
description: 瞭解中繼資料的類型， [!DNL Adobe Experience Manager Assets] helps manage metadata for assets to allow easier categorization and organization of assets. [!DNL Experience Manager] 以及如何根據資產的中繼資料自動組織和處理資產。
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: d6a0848547a6dcbb058576827d3cacbc8045ae79
workflow-type: tm+mt
source-wordcount: '1933'
ht-degree: 4%

---


# 管理數位資產的中繼資料 {#managing-metadata-for-digital-assets}

[!DNL Adobe Experience Manager Assets] 保留每個資產的中繼資料。 它可讓資產的分類和組織更輕鬆，並協助尋找特定資產的人。 中繼資料管理可從上傳至的檔案擷取中繼資 [!DNL Experience Manager Assets]料，與創意工作流程整合。 透過使用資產保留和管理中繼資料的能力，您可以根據資產的中繼資料自動組織及處理資產。

>[!MORELIKETHIS]
>
>* [XMP 中繼資料](xmp-metadata.md)
>* [如何編輯或新增中繼資料](meta-edit.md)


<!-- 
* [Metadata Schemata Reference](meta-ref.md)
-->

## 為什麼我們需要中繼資料 {#why-metadata}

中繼資料是指有關資料的資料。 在這方面，資料是指您的數位資產，例如影像。 中繼資料對於有效率的資產管理至關重要。

中繼資料是資產所有可用資料的集合，但不一定包含在該影像中。 中繼資料的一些範例包括：

* 資產的名稱。
* 上次修改的時間和日期。
* 資產儲存在儲存庫中時的大小。
* 包含在中的資料夾的名稱。
* 相關資產或套用的標籤。

以上是可管理資產的基本中繼資 [!DNL Experience Manager] 料屬性，可讓使用者查看所有資產。 例如，在嘗試尋找最近新增的資產時，可使用上次修改日期來排序資產。

您可以新增更多高階資料至數位資產，例如：

* 資產類型（是影像、視訊、音訊剪輯或檔案？）。
* 資產的擁有者。
* 資產的標題。
* 資產的說明。
* 指派給資產的標籤。

更多中繼資料可協助您進一步分類資產，並隨著數位資訊的增加而有所幫助。 僅根據檔名管理幾百個檔案是可能的。 但是，這種方法不具可擴充性。 當涉案人數和管理的資產數量增加時，這個數字就不夠。

隨著中繼資料的增加，數位資產的價值會增加，因為資產會變成，

* 更容易存取——系統和使用者可輕鬆找到。
* 管理起來更輕鬆——您可以更輕鬆地尋找具有相同屬性集的資產，並套用變更。
* 完整——資產包含更多資訊和內容，以及更多中繼資料。

基於這些原因， [!DNL Assets] 您可以為數位資產提供建立、管理和交換中繼資料的適當方式。

## 中繼資料類型 {#types-of-metadata}

兩種基本的中繼資料類型是技術中繼資料和描述性中繼資料。

技術中繼資料對於處理數位資產且不應手動維護的軟體應用程式非常有用。 [!DNL Experience Manager Assets] 而其他軟體會自動決定技術中繼資料，而當資產修改時，中繼資料可能會變更。 資產的可用技術中繼資料主要取決於資產的檔案類型。 技術中繼資料的一些範例包括：

* 檔案大小。
* 影像的尺寸（高度和寬度）。
* 音訊或視訊檔案的位元速率。
* 影像的解析度（詳細程度）。

描述性中繼資料是與應用程式網域相關的中繼資料，例如資產來自的業務。 無法自動確定描述性中繼資料。 系統會手動或半自動建立。 例如，可使用GPS的相機可自動追蹤經緯度，並新增地理標籤影像。

手動建立描述性中繼資料資訊的成本很高。 因此，建立標準是為了簡化跨軟體系統和組織的中繼資料交換。 [!DNL Experience Manager Assets] 支援中繼資料管理的所有相關標準。

## 編碼標準 {#encoding-standards}

在檔案中內嵌中繼資料有多種方式。 支援多種編碼標準：

* XMP:用於將提 [!DNL Assets] 取的元資料儲存在儲存庫中。
* ID3:音訊和視訊檔案。
* 例如：的雙曲餘切值。
* 其他／舊版：從 [!DNL Microsoft Word]、 [!DNL PowerPoint][!DNL Excel]等。

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP)是開放標準，供所有中繼資料 [!DNL Experience Manager Assets] 管理使用。 此標準提供通用中繼資料編碼，可嵌入所有檔案格式。 Adobe和其他公司支援XMP標準，因為它提供多樣化內容模型。 使用XMP標準和XMP標準的 [!DNL Experience Manager Assets] 使用者擁有強大的平台。 如需詳細資訊，請參 [閱XMP](https://www.adobe.com/products/xmp.html)。

### ID3 {#id}

當您在電腦或可攜式MP3播放器上播放數位音訊檔案時，會顯示儲存在這些ID3標籤中的資料。

ID3標籤是針對MP3檔案格式而設計。 有關格式的其他資訊：

* ID3標籤適用於MP3和mp3PRO檔案。
* WAV沒有標籤。
* WMA有不允許開放原始碼實作的專屬標籤。
* Ogg Vorbis使用內嵌在Ogg容器中的Xiph Comments。
* AAC使用專屬的標籤格式。

### Exif {#exif}

可交換的影像檔案格式(Exif)是數位攝影中最常用的中繼資料格式。 它提供以多種檔案格式（例如JPEG、TIFF、RIFF和WAV）嵌入固定的中繼資料屬性辭彙的方式。 Exif將中繼資料儲存為中繼資料名稱與中繼資料值的配對。 這些中繼資料名稱——值配對也稱為標籤，不要與中的標籤混淆 [!DNL Experience Manager]。 現代數位相機可建立Exif中繼資料，而現代圖形軟體也支援它。 Exif格式是中繼資料管理的最低公分母，尤其是影像。

Exif的主要限制是不支援一些常用的影像檔案格式，例如BMP、GIF或PNG。

Exif定義的中繼資料欄位通常具有技術性，在描述性中繼資料管理中使用有限。 因此，提供 [!DNL Experience Manager Assets] Exif屬性對應至常用中 [繼資料架構](metadata-schemas.md) ，以及XMP。

#### 其他中繼資料 {#other-metadata}

可從檔案內嵌的其他中繼資 [!DNL Microsoft Word]料 [!DNL PowerPoint]包括 [!DNL Excel]、、等等。

## 管理數位資產的中繼資料 {#manage-assets-metadata}

Enterprise Manager Assets可讓您同時編輯多個資產的中繼資料，以便快速將一般中繼資料變更大量傳播至資產。 使用「 [!UICONTROL 屬性] 」頁可以將元資料屬性更改為公用值，或添加或修改標籤。 要自定義元資料屬性頁，包括添加、修改、刪除元資料屬性，請使用方案編輯器。

>[!NOTE]
>
>大量編輯方法適用於資料夾或系列中的可用資產。 對於跨資料夾可用或符合一般准則的資產，可在搜尋後 [大量更新中繼資料](/help/assets/search-assets.md#metadataupdates)。

1. 導覽至您要編輯的資產所在的位置。
1. 選取您要編輯其常用屬性的資產。
1. 在工具列中點選／按一 **[!UICONTROL 下「屬性]** 」，以開啟選 [!UICONTROL 取資產的「屬性] 」頁面。

   >[!NOTE]
   >
   >當您選取多個資產時，會為資產選取最低的共同父級表單。 換言之，「屬 [!UICONTROL 性] 」頁面只會顯示所有個別資產的「屬性  」頁面上共有的中繼資料欄位。

1. 修改各種標籤下所選資產的中繼資料屬性。
1. 若要檢視特定資產的中繼資料編輯器，請取消選取清單中的其餘資產。 中繼資料編輯器欄位會填入特定資產的中繼資料。

   >[!NOTE]
   >
   >* 在「屬 [!UICONTROL 性] 」頁面中，您可以取消選取資產，從資產清單中移除資產。 資產清單預設會選取所有資產。 您從清單中移除的資產的中繼資料不會更新。
   >* 在資產清單頂端，選取「標題」旁的核取方塊 **** ，以在選取資產和清除清單之間切換。


1. 若要為資產選取不同的中繼資料結構，請點選／按一 **[!UICONTROL 下工具列中的]** 「設定」，然後選取所要的結構。 儲存變更。
1. 若要在包含多個值的欄位中，將新中繼資料與現有中繼資料一起附加，請選取「附 **[!UICONTROL 加模式」]**。如果您未選取此選項，新的中繼資料會取代欄位中現有的中繼資料。點選/按一 **[!UICONTROL 下提交]**。

   >[!CAUTION]
   >
   >對於單值欄位，即使您選擇「附加模式」，新元資料也不會附加到欄位中的現 **[!UICONTROL 有值]**。

## 使用處理設定檔自訂中繼資料 {#metadata-compute-service}

資產做為雲端服務，可使用雲端原生服務為資產產生自訂中繼資料。 設定處理設定檔以產生自訂中繼資料。 瞭解 [如何使用處理設定檔](/help/assets/asset-microservices-configure-and-use.md#use-profiles)。

![處理描述檔中的中繼資料轉譯](assets/processing-profile-metadata.png)

>[!TIP]
>
>只能將一個處理設定檔套用至資料夾。 若要對資料夾中的資產套用多個處理，請新增更多選項至單一處理設定檔。 例如，單一描述檔可產生轉譯、轉碼資產、產生自訂中繼資料等。 您可以對每個任務應用MIME類型篩選器，以便根據所需的檔案格式觸發相應的任務。

## 設定大量中繼資料更新的限制 {#configlimit}

為避免DOS狀況，AEM會限制Sling請求中支援的參數數。 一次更新許多資產的中繼資料時，您可能會達到限制，而且無法針對更多資產更新中繼資料。 AEM會在記錄檔中產生下列警告：

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

若要變更限制，請存取Web Console( **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**)並變更 **[!UICONTROL Apache Sling Parameters Request Apache Handling Osgi Configuration的]****** Maximum POST Parameters Praters Aremeters的值。

## 中繼資料圖式 {#metadata-schemata}

中繼資料結構是一組預先定義的中繼資料屬性定義，可用於各種應用程式。 屬性始終與資產相關聯，這表示屬性與資源「相關」。

如果沒有符合您需求的中繼資料架構，您也可以設計您自己的中繼資料架構。 請勿複製現有資訊。 在組織內，分離圖式資料可讓共用中繼資料更輕鬆。 [!DNL Experience Manager] 提供您最常用中繼資料架構的預設清單。 此清單可協助您快速開始中繼資料策略，並快速挑選您需要的中繼資料屬性。

支援的中繼資料架構列於下方。

### 標準中繼資料 {#standard-metadata}

* DC —— 是 [!DNL Dublin Core] 一組重要且廣泛使用的元資料。
* DICOM —— 數位影像與醫學通訊。
* `Iptc4xmpCore` 和 `iptc4xmpExt` - International Press Communications Standard包含許多特定主題的中繼資料。
* RDF —— 資源描述框架——通用語義Web元資料。
* XMP - [!DNL Extensible Metadata Platform].
* `xmpBJ` -基本工作訂票。

### 應用程式專用的中繼資料 {#application-specific-metadata}

應用程式專用的中繼資料包含技術和描述性中繼資料。 如果您使用此類中繼資料，其他應用程式可能無法使用中繼資料。 例如，不同的影像轉換應用程式可能無法存取中繼 [!DNL Adobe Photoshop] 資料。 您可以建立工作流程步驟，將應用程式特定屬性變更為標準屬性。

* ACDSee —— 由程式管理的元 [!DNL ACDSee] 資料。 請參 [閱www.acdsee.com/](https://www.acdsee.com/)。
* 相簿- [!DNL Adobe Photoshop Album].
* CQ —— 使用者 [!DNL Experience Manager Assets]。
* DAM —— 用於 [!DNL Experience Manager Assets]。
* DEX - [Optima SC描述檔案總管](http://www.optimasc.com/products/dex/index.html) ，是Windows作業系統中中繼資料和檔案管理工具的集合。
* CRS - [Adobe Photoshop Camera Raw](https://helpx.adobe.com/camera-raw/using/introduction-camera-raw.html)。
* LR - [!DNL Adobe Lightroom].
* MediaPro - [iView MediaPro](https://en.wikipedia.org/wiki/Phase_One_Media_Pro)。
* MicrosoftPhoto和MP - Microsoft Photo。
* PDF和PDF/X。
* Photoshop和psAux - [!DNL Adobe Photoshop].

### 數位版權管理中繼資料 {#digital-rights-management-metadata}

* CC - [!DNL Creative Commons].
* [!DNL XMPRights]。
* PLUS —— 圖 [片授權通用系統](https://www.useplus.com)。
* PRISM —— 發佈 [業界標準中繼資料的需求](https://www.idealliance.org/prism-metadata)。
* PRL —— 稜鏡版權語言。
* PUR —— 稜鏡使用權。
* `xmpPlus` -將PLUS與XMP整合。

### 攝影專用中繼資料 {#photography-specific-metadata}

* Exif —— 相機的技術資訊，包括GPS位置。
* CRS —— 方 [!DNL Camera Raw] 案。
* `iptc4xmpCore` 和 `iptc4xmpExt`.
* TIFF —— 影像中繼資料（不僅適用於TIFF影像）。

### 列印專用的中繼資料 {#print-specific-metadata}

* PDF和PDF/X - Adobe PDF和協力廠商應用程式。
* PRISM —— 發佈 [業界標準中繼資料的需求](https://www.prismstandard.org)。
* XMP - [!DNL Extensible Metadata Platform].
* `xmpPG` -分頁文字的XMP中繼資料。

### 多媒體特定中繼資料 {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media].
* `xmpMM` -媒體管理。

## 中繼資料導向的工作流程 {#metadata-driven-workflows}

建立中繼資料導向的工作流程可協助您自動化某些程式，進而提高效率。 在元資料驅動的工作流中，工作流管理系統讀取該工作流並因此執行一些預定義的操作。 例如，您可使用中繼資料導向工作流程的一些方式：

* 工作流程可以檢查影像是否有標題。 如果沒有，系統會通知您新增標題。
* 工作流程可以檢查資產上的版權聲明是否允許散發。 因此，系統會將資產傳送至一或另一伺服器。
* 工作流程可以檢查資產是否沒有預先定義的強制中繼資料，或是包含無效中繼資料 *的資* 產。
