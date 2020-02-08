---
title: 管理數位資產的中繼資料
description: 瞭解中繼資料的類型，以及AEM Assets如何協助管理資產的中繼資料，讓資產的分類和組織更輕鬆。 AEM Assets可讓您使用您的資產保留和管理任意中繼資料，因此能夠根據資產的中繼資料自動組織和處理資產。
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# 管理數位資產的中繼資料 {#managing-metadata-for-digital-assets}

Adobe Experience Manager(AEM)Assets會保留每個資產的中繼資料。 這可讓資產分類和組織更輕鬆，並協助尋找特定資產的人。 透過從上傳至AEM Assets的檔案擷取中繼資料的功能，中繼資料管理與創意工作流程整合。 AEM Assets可讓您使用您的資產保留和管理任意中繼資料，因此能夠根據資產的中繼資料自動組織和處理資產。

>[!MORELIKETHIS]
>
>* [XMP中繼資料](xmp-metadata.md)
>* [如何編輯或新增中繼資料](meta-edit.md)


<!-- 
* [Metadata Schemata Reference](meta-ref.md)
-->

## 為何選擇中繼資料 {#why-metadata}

中繼資料是指有關資料的資料。 在這方面，資料是指您所處理的資產，例如影像。 中繼資料很重要，因為它可讓使用者更有效率地管理資產。

中繼資料是此影像所有可用資料的集合，但不一定包含在該影像中，例如：

* 資產的名稱
* 上次修改的時間和日期
* 儲存在儲存庫中的映像大小
* 包含在

這些是AEM可為資產管理的基本中繼資料屬性，可讓使用者查看所有資產，例如，依其上次修改日期排序——在嘗試發現哪些資產最近新增至儲存庫時很實用。

您可以新增更多高階資料至數位資產，例如：

* 資產類型（是影像、視訊、音訊剪輯或檔案？）
* 資產的擁有者
* 資產的標題
* 資產說明
* 指派給資產的標籤

更多中繼資料可協助您進一步分類資產，並隨著數位資訊的增加而有所幫助。 雖然單一人員僅根據檔案名稱就可以管理數百個檔案的清單，但是當相關人員數量及所管理資產數量增加時，此方法就不適用。

當中繼資料新增至資產時，資產的價值會增加，因為資產會變成

* 更容易存取——人們更容易找到
* 更輕鬆管理——您可以更輕鬆地尋找具有相同屬性集的資產，並將變更套用至資產
* 更複雜——您新增至資產的中繼資料越多，管理中繼資料越重要

基於這些原因，AEM Assets提供您正確的方式，來建立、管理和交換數位資產的中繼資料。

## 中繼資料基礎 {#metadata-basics}

在匯入（收錄）資產時，會從資產中擷取中繼資料。 此外，新增中繼資料可協助您進一步分類資產。

本節涵蓋中繼資料和編碼標準的類型。

### 技術中繼資料 {#technical-metadata}

技術中繼資料對於處理數位資產且不應手動維護的軟體應用程式非常有用。 AEM Assets和其他軟體可自動判斷技術中繼資料，並可能在修改資產時變更。 資產的可用技術中繼資料主要取決於資產的檔案類型。 技術中繼資料的範例如下：

* 檔案大小
* 影像的尺寸（高度和寬度）
* 音訊或視訊檔案的位元速率
* 影像的解析度（詳細程度）

### 描述性中繼資料 {#descriptive-metadata}

描述性中繼資料是與應用程式網域相關的中繼資料，例如資產來自的業務。 無法自動確定描述性中繼資料。 必須手動或半自動建立。 例如，GPS攝影機可自動追蹤拍攝的影像經緯度，並將這項資訊加入影像的中繼資料。

由於建立描述性中繼資料資訊需要耗費大量人力，因此已制定標準，以簡化跨軟體系統和組織的中繼資料交換。

AEM Assets支援中繼資料管理的所有相關標準。

由於中繼資料的重要性以及建立中繼資料需要大量的人工參與，因此已建立標準，讓交換變得更輕鬆。

### 編碼標準 {#encoding-standards}

中繼資料可以以多種方式內嵌至檔案。 支援多種編碼標準：

* XMP:供AEM Assets用來在儲存庫中儲存擷取的中繼資料。
* ID3:音訊和視訊檔案。
* EXIF:的雙曲餘切值。
* 其他／舊版：從Microsoft Word、PowerPoint、Excel等。

#### XMP {#xmp}

XMP意指可擴充中繼資料平台，是AEM Assets用於所有中繼資料管理的中繼資料標準。 除了提供可嵌入所有檔案格式的通用中繼資料編碼外，XMP提供多樣化內容模型，並受Adobe和其他公司支援，讓XMP的使用者結合AEM Assets擁有強大的平台可以建立。

#### ID3 {#id}

當您在電腦或可攜式MP3播放器上播放數位音訊檔案時，會顯示儲存在這些ID3標籤中的資料。

ID3標籤是針對MP3檔案格式而設計。 有關格式的其他資訊：

* ID3標籤適用於MP3和MP3pro檔案。
* WAV沒有標籤。
* WMA具有不允許開放原始碼實作的專屬標籤。
* Ogg Vorbis使用嵌入在OGG容器中的Xiph注釋。
* AAC使用專屬的標籤格式。

#### EXIF {#exif}

EXIF是指可交換的影像檔案格式，是數位攝影中最常用的中繼資料格式。 它提供了一種將固定的元資料屬性辭彙嵌入多種檔案格式(如

* JPEG
* TIFF
* RIFF
* WAV

EXIF的主要限制是不支援其他常用的影像檔案格式，例如BMP、GIF或PNG。

EXIF將中繼資料儲存為中繼資料名稱與中繼資料值的配對。 這些中繼資料名稱——值配對也稱為標籤，不要與AEM中的標籤混淆。

由於EXIF是由現代數位相機自動建立，並透過現代圖形軟體提供支援，因此可視為中繼資料管理的最低共性。

EXIF定義的大部分中繼資料欄位都具有高度技術性，且對描述性中繼資料管理的使用有限。 因此，AEM Assets提供將EXIF屬性對應至通用中繼資料 [圖式](metadata-schemas.md) ，以及 [XMP](xmp-metadata.md)（AEM Assets用於中繼資料管理的強大中繼資料格式）的功能。

#### 其他中繼資料 {#other-metadata}

可從檔案內嵌的其他中繼資料包括Microsoft Word、PowerPoint、Excel等。

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


1. 若要為資產選取不同的中繼資料結構，請點選／按一 **[!UICONTROL 下工具列中]** 的「設定」，然後選取所要的結構。 儲存變更。
1. 若要在包含多個值的欄位中，將新中繼資料與現有中繼資料一起附加，請選取「附 **[!UICONTROL 加模式」]**。 如果您未選取此選項，新的中繼資料會取代欄位中現有的中繼資料。 點選／按一 **[!UICONTROL 下提交]**。

   >[!CAUTION]
   >
   >對於單值欄位，即使您選擇「附加模式」，新元資料也不會附加到欄位中的現 **[!UICONTROL 有值]**。

## 設定大量中繼資料更新的限制 {#configlimit}

為避免DOS狀況，AEM會限制Sling請求中支援的參數數。 一次更新許多資產的中繼資料時，您可能會達到限制，而且無法針對更多資產更新中繼資料。 AEM會在記錄檔中產生下列警告：

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

若要變更限制，請存取Web Console( **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**)並變更 **[!UICONTROL Apache Sling Parameters Request Apache Handling Osgi Configuration的]****** Maximum POST Parameters Praters Aremeters的值。

## 中繼資料圖式 {#metadata-schemata}

中繼資料結構是一組預先定義的中繼資料屬性定義，可用於多種應用程式。 屬性始終與資產相關聯，這表示屬性與資源「相關」。

如果沒有符合您需求的中繼資料架構，您也可以設計自己的中繼資料架構（但請小心，不要複製已存在的項目）。 在組織內，分離圖式資料可讓組織間共用中繼資料。

AEM提供您最熱門中繼資料架構的現成清單，讓您快速開始您的中繼資料策略，並從已定義的架構中挑選您需要的中繼資料屬性。

支援的中繼資料架構列於下節。

### 標準中繼資料 {#standard-metadata}

* dc - Dublin Core —— 最重要且廣泛使用的中繼資料集
* DICOM —— 數位影像與醫學通訊
* Iptc4xmpCore &amp; iptc4xmpExt —— 國際新聞通訊標準——大量特定主題的中繼資料
* rdf —— 資源描述框架——通用語義Web元資料
* xmp —— 可擴充的中繼資料平台
* xmpBJ —— 基本工作訂票

### 應用程式專用的中繼資料 {#application-specific-metadata}

>[!NOTE]
>
>應用程式專用的中繼資料包括技術和描述性中繼資料。 如果您使用這些功能，其他應用程式可能無法使用中繼資料。 例如，如果您有具有Adobe Photoshop中繼資料的資產，而另一個影像轉換應用程式則嘗試存取中繼資料，則可能無法存取。
>
>如果您發現資產中有許多應用程式特定的中繼資料，可以建立將應用程式特定屬性變更為標準屬性的工作流程步驟。

* acdsee —— 由ACDSee程式管理的元數 [據www.acdsee.com/](https://www.acdsee.com/)
* 相簿- Adobe Photoshop Album
* cq —— 由AEM Assets使用
* dam —— 由AEM Assets使用
* dex - Optima SC說明瀏覽器
* crs - Adobe Photoshop Camera Raw
* lr - Adobe Lightroom
* mediapro - iview mediaPro
* MicrosoftPhoto和MP - Microsoft Photo
* pdf &amp; pdfx
* photoshop &amp; psAux - Adobe Photoshop

### 數位版權管理中繼資料 {#digital-rights-management-metadata}

* cc —— 創意共用
* xmpRights
* plus —— 圖片授權通用系統- https://www.useplus.com/
* prism - https://www.idealliance.org/prism-metadata業界標準中繼資料的發佈需求
* prl —— 稜鏡版權語言
* pur —— 稜鏡使用權
* xmpPlus —— 整合PLUS與XMP

### 攝影專用中繼資料 {#photography-specific-metadata}

* exif —— 相機提供的大量技術資訊，包括GPS位置
* crs - photoshop相機原始資料
* Iptc4xmpCore和iptc4xmpExt
* TIFF —— 影像中繼資料（不僅適用於TIFF影像）

### 列印專用的中繼資料 {#print-specific-metadata}

* pdf和pdfx - Adobe PDF和協力廠商應用程式
* prism - [www.prismstandard.org業界標準中繼資料](https://www.prismstandard.org) （英文）的發佈需求
* xmp
* xmpPG —— 分頁文字的xmp

### 多媒體特定中繼資料 {#multimedia-specific-metadata}

* xmpDM —— 動態媒體
* xmpMM —— 媒體管理

## 中繼資料導向的工作流程 {#metadata-driven-workflows}

建立中繼資料導向的工作流程可協助您自動化某些程式，進而提高效率。 在元資料驅動的工作流中，工作流管理系統讀取該工作流並因此執行一些預定義的操作。

例如，您可使用中繼資料導向工作流程的一些方式：

* 工作流程可檢查影像是否有標題。 如果沒有，系統會通知特定使用者新增標題。
* 工作流程可以檢查資產上的版權聲明是否允許散發。 如果有，系統會將資產傳送至一個伺服器。 如果沒有，系統會將資產傳送至另一伺服器。
