---
title: 管理數字資產的元資料
description: 瞭解元資料的類型和方法 [!DNL Adobe Experience Manager Assets] 幫助管理資產的元資料，以便更輕鬆地對資產進行分類和組織。 [!DNL Experience Manager] 使能夠根據資產的元資料自動組織和處理資產。
contentOwner: AG
mini-toc-levels: 1
feature: Asset Management,Metadata
role: User,Architect,Admin
exl-id: 73a82bc2-1dda-4090-b7ee-29d1a632ba25
source-git-commit: 20d54ccdd116c3dbede8fb20f7169a17a223f7a1
workflow-type: tm+mt
source-wordcount: '1953'
ht-degree: 6%

---

# 管理數字資產的元資料 {#managing-metadata-for-digital-assets}

[!DNL Adobe Experience Manager Assets] 保留每個資產的元資料。 它使資產的分類和組織變得更容易，並幫助尋找特定資產的人。 能夠從上載到的檔案中提取元資料 [!DNL Experience Manager Assets]元資料管理與創意工作流整合。 通過能夠保留和管理與資產相關的元資料，您可以根據資產的元資料自動組織和處理資產。

<!-- 
* [Metadata Schemata Reference](meta-ref.md)
-->

## 為什麼我們需要元資料 {#why-metadata}

元資料是指有關資料的資料。 在這方面，資料是指數字資產，比如影像。 中繼資料是進行高效率資產管理的關鍵所在。

元資料是資產可用的所有資料的集合，但不一定包含在該映像中。 元資料的一些示例包括：

* 資產的名稱。
* 上次修改的時間和日期。
* 儲存在儲存庫中的資產大小。
* 包含在中的資料夾的名稱。
* 相關資產或應用的標籤。

以上是基本元資料屬性 [!DNL Experience Manager] 可以管理資產，這允許用戶查看所有資產。 例如，按上次修改日期對資產進行排序在嘗試發現最近添加或修改的資產時非常有用。

您可以向數字資產添加更多高級資料，例如：

* 資產類型（是影像、視頻、音頻剪輯還是文檔？）。
* 資產所有者。
* 資產的標題。
* 資產說明。
* 分配給資產的標籤。

更多元資料有助於您進一步對資產進行分類，並有助於隨著數字資訊量的增長。 僅根據檔案名可以管理幾百個檔案。 然而，此方法並不能調整規模。當涉案人數和受管理資產數量增加時，這個數字就不足。

隨著中繼資料增加，數位資產的價值也會成長，這是因為資產會變得

* 更易於存取 - 系統和使用者可以更輕鬆找到資產。
* 更易於管理 - 您可以更容易找到具有同一組屬性的資產，並將變更套用到這些資產。
* 完整 - 資產攜帶更多資訊和包含更多中繼資料的內容。

出於這些原因， [!DNL Assets] 為您提供了建立、管理和交換數字資產的元資料的正確方法。

## 元資料的類型 {#types-of-metadata}

元資料的兩種基本類型是技術元資料和描述元資料。

技術元資料對於處理數字資產且不應手動維護的軟體應用程式非常有用。 [!DNL Experience Manager Assets] 而其他軟體則自動確定技術元資料，當資產被修改時，元資料可能會改變。 資產的可用技術元資料在很大程度上取決於資產的檔案類型。 技術元資料的一些示例包括：

* 檔案大小。
* 影像的Dimension（高度和寬度）。
* 音頻或視頻檔案的比特率。
* 影像的解析度（詳細程度）。

描述性元資料是與應用程式域相關的元資料，例如資產來自的業務。 無法自動確定描述性元資料。 它是手動或半自動建立的。 例如，GPS攝像頭可以自動跟蹤經緯度，並添加地理標籤。

手動建立描述性元資料資訊的成本很高。 因此，制定標準以簡化跨軟體系統和組織的元資料交換。 [!DNL Experience Manager Assets] 支援元資料管理的所有相關標準。

## 元資料和上次修改 {#last-modification}

資產的上次修改日期反映了資產的原始檔案上次修改的時間。 因此，修改日期和用戶僅在以下情況下才會更改：

* 已上載資產的新版本
* 重新處理資產

上次修改日期和用戶不更改：

* 移動或更名資產時
* 當資產被簽出時，已簽出或版本
* 發佈或未發佈資產時
* 關於元資料更新
* 引用或集合更新

## 編碼標準 {#encoding-standards}

在檔案中嵌入元資料有多種方法。 支援編碼標準的選擇：

* XMP:使用 [!DNL Assets] 將提取的元資料儲存在儲存庫中。
* ID3:檔案。
* Exif:的子菜單。
* 其他/舊版：從 [!DNL Microsoft Word]。 [!DNL PowerPoint]。 [!DNL Excel]等等。

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP為一個公開標準，由 [!DNL Experience Manager Assets] 所有元資料管理。 該標準提供可嵌入所有檔案格式的通用元資料編碼。 Adobe和其他公司XMP支援標準，因為它提供了豐富的內容模型。 標準和XMP的用戶 [!DNL Experience Manager Assets] 有一個強大的平台可以構建。 有關詳細資訊，請參見 [XMP](https://www.adobe.com/products/xmp.html)。

### ID3 {#id}

在電腦或攜帶型MP3播放器上回放數字音頻檔案時，這些ID3標籤中儲存的資料會顯示。

ID3標籤是為MP3檔案格式設計的。 有關格式的其他資訊：

* ID3標籤在MP3和mp3PRO檔案中工作。
* WAV沒有標籤。
* WMA具有不允許開源實現的專有標籤。
* Ogg Vorbis使用Ogg容器中嵌入的Xiph注釋。
* AAC使用專有標籤格式。

### 艾希夫 {#exif}

可交換影像檔案格式(Exif)是數字攝影中最常用的元資料格式。 它提供了一種以多種檔案格式(如JPEG、TIFF、RIFF和WAV)嵌入固定的元資料屬性辭彙的方法。 Exif將元資料儲存為元資料名稱和元資料值的對。 這些元資料名稱 — 值對也稱為標籤，不要與中的標籤混淆 [!DNL Experience Manager]。 現代數位相機建立了Exif元資料，現代圖形軟體支援它。 Exif格式是元資料管理的最低公分母，尤其是映像。

Exif的一個主要限制是，一些常用的影像檔案格式(如BMP、GIF或PNG)不支援它。

Exif定義的元資料欄位通常是技術性的，在描述性元資料管理中使用有限。 因此， [!DNL Experience Manager Assets] 提供將Exif屬性映射到 [通用元資料架構](metadata-schemas.md) 然後進XMP入。

#### 其他元資料 {#other-metadata}

可以從檔案中嵌入的其他元資料包括 [!DNL Microsoft Word]。 [!DNL PowerPoint]。 [!DNL Excel]等等。

## 管理數字資產的元資料 {#manage-assets-metadata}

Enterprise Manager資產允許您同時編輯多個資產的元資料，以便可以將公共元資料更改快速批量傳播到資產。 使用 [!UICONTROL 屬性] 頁，以將元資料屬性更改為公用值或添加或修改標籤。 要自定義元資料「屬性」頁，包括添加、修改、刪除元資料屬性，請使用架構編輯器。

>[!NOTE]
>
>批量編輯方法適用於資料夾或集合中的可用資產。 對於跨資料夾可用或符合通用標準的資產， [搜索後批量更新元資料](/help/assets/search-assets.md#metadata-updates)。

1. 導航到要編輯的資產的位置。
1. 選擇要編輯其公用屬性的資產。
1. 在工具欄上，點擊/按一下 **[!UICONTROL 屬性]** 開啟 [!UICONTROL 屬性] 的子菜單。

   >[!NOTE]
   >
   >選擇多個資產時，將為資產選擇最低的公用父窗體。 換句話說， [!UICONTROL 屬性] 頁僅顯示在整個頁面上公用的元資料欄位 [!UICONTROL 屬性] 所有資產的頁數。

1. 修改各頁籤下選定資產的元資料屬性。
1. 要查看特定資產的元資料編輯器，請取消選擇清單中剩餘的資產。 元資料編輯器欄位被填充有特定資產的元資料。

   >[!NOTE]
   >
   >* 在 [!UICONTROL 屬性] 的子菜單。 預設情況下，資產清單會選擇所有資產。 不會更新從清單中刪除的資產的元資料。
   >* 在「資產」清單頂部，選中靠近 **[!UICONTROL 標題]** 在選擇資產和清除清單之間切換。


1. 要為資產選擇其他元資料架構，請點擊/按一下 **[!UICONTROL 設定]** ，然後選擇所需的架構。 儲存變更。
1. 若要在包含多個值的欄位中，將新中繼資料與現有中繼資料一起附加，請選取「附 **[!UICONTROL 加模式」]**。如果您未選取此選項，新的中繼資料會取代欄位中現有的中繼資料。點選/按一 **[!UICONTROL 下提交]**。

   >[!CAUTION]
   >
   >對於單值欄位，即使您選擇「附加模式」，新元資料也不會附加到欄位中的現 **[!UICONTROL 有值]**。

## 使用處理配置檔案的自定義元資料 {#metadata-compute-service}

資產作為 [!DNL Cloud Service] 可以使用雲本地服務為資產生成自定義元資料。 配置處理配置檔案以生成自定義元資料。 請參閱 [如何使用處理配置檔案](/help/assets/asset-microservices-configure-and-use.md#use-profiles)。

![處理配置檔案中的元資料格式副本](assets/processing-profile-metadata.png)

>[!TIP]
>
>只能將一個處理配置檔案應用於資料夾。 要將多個處理應用於資料夾中的資產，請向單個處理配置檔案添加更多選項。 例如，單個配置檔案可以生成格式副本、轉碼資產、生成自定義元資料等。 您可以為每個任務應用MIME類型篩選器，以便針對所需的檔案格式觸發相應的任務。

<!-- TBD: Commenting as Web Console is not available. Document the appropriate OSGi config method if available in CS.

## Configure limit for bulk metadata update {#configlimit}

To prevent DOS-like situation, [!DNL Experience Manager] limits the number of parameters supported in a Sling request. When updating metadata of many assets in one go, you may reach the limit and the metadata does not get updated for more assets. [!DNL Experience Manager] generates the following warning in the logs:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

To change the limit, access Web Console ( **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**) and change the value of **[!UICONTROL Maximum POST Parameters]** in **[!UICONTROL Apache Sling Request Parameter Handling]** OSGi configuration.
-->

## 元資料架構 {#metadata-schemata}

元資料方案是可在各種應用程式中使用的預定義元資料屬性定義集。 屬性始終與資產關聯，這意味著屬性是資源的「關於」。

如果不存在滿足您需要的元資料架構，您也可以設計自己的元資料架構。 不要複製現有資訊。 在組織內，分離模式使共用元資料更加容易。 [!DNL Experience Manager] 為您提供了最流行的元資料架構的預設清單。 該清單可幫助您快速啟動元資料策略並快速選擇所需的元資料屬性。

下面列出了支援的元資料架構。

### 標準元資料 {#standard-metadata}

* DC - [!DNL Dublin Core] 是一組重要且廣泛使用的元資料。
* DICOM — 醫學數字成像和通信。
* `Iptc4xmpCore` 和 `iptc4xmpExt`  — 國際新聞通訊標準包含許多特定主題的元資料。
* RDF — 資源說明框架 — 用於通用語義Web元資料。
* XMP [!DNL Extensible Metadata Platform]。
* `xmpBJ`  — 基本作業票務。

### 特定於應用程式的元資料 {#application-specific-metadata}

特定於應用程式的元資料包括技術和描述性元資料。 如果使用此類元資料，則其他應用程式可能無法使用元資料。 例如，其他影像呈現應用程式可能無法訪問 [!DNL Adobe Photoshop] 元資料。 您可以建立將特定於應用程式的屬性更改為標準屬性的工作流步驟。

* ACDSee — 由 [!DNL ACDSee] 的子菜單。 請參閱 [www.acdsee.com](https://www.acdsee.com/)。
* 相冊 —  [!DNL Adobe Photoshop Album]。
* CQ — 使用者 [!DNL Experience Manager Assets]。
* DAM — 使用者 [!DNL Experience Manager Assets]。
* DEX - [Optima SC說明瀏覽器](https://www.optimasc.com/products/dex/index.html) 是用於Windows作業系統元資料和檔案管理的工具的集合。
* CRS - [Adobe Photoshop Camera·勞](https://helpx.adobe.com/camera-raw/using/introduction-camera-raw.html)。
* LR - [!DNL Adobe Lightroom]。
* MediaPro - [iView媒體專業版](https://en.wikipedia.org/wiki/Phase_One_Media_Pro)。
* MicrosoftPhoto和MP -MicrosoftPhoto。
* PDF和PDF/X。
* Photoshop和普索。 [!DNL Adobe Photoshop]。

### Digital Rights Management元資料 {#digital-rights-management-metadata}

* CC - [!DNL Creative Commons].
* [!DNL XMPRights]。
* 加 —  [圖片許可通用系統](https://www.useplus.com)。
* 稜鏡 —  [發佈行業標準元資料要求](https://www.idealliance.org/prism-metadata)。
* PRL - PRISM權利語言。
* PUR - PRISM使用權。
* `xmpPlus`  — 將PLUS與整合XMP。

### 特定於攝影的元資料 {#photography-specific-metadata}

* Exif — 來自相機的技術資訊，包括GPS位置。
* CRS - [!DNL Camera Raw] 架構。
* `iptc4xmpCore` 和 `iptc4xmpExt`.
* TIFF — 映像元資料(不僅用於TIFF映像)。

### 特定於打印的元資料 {#print-specific-metadata}

* PDF和PDF/X -Adobe PDF和第三方應用程式。
* 稜鏡 —  [發佈行業標準元資料要求](https://www.idealliance.org/prism-metadata)。
* XMP [!DNL Extensible Metadata Platform]。
* `xmpPG`  — 頁面XMP文本的元資料。

### 多媒體特定元資料 {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media].
* `xmpMM`  — 介質管理。

## 元資料驅動的工作流 {#metadata-driven-workflows}

建立元資料驅動的工作流有助於您自動執行某些流程，從而提高效率。 在元資料驅動的工作流中，工作流管理系統讀取該工作流，並因此執行一些預定義的操作。 例如，您可以使用元資料驅動的工作流的一些方法：

* 工作流可以檢查影像是否具有標題。 如果沒有，系統會通知添加標題。
* 工作流可以檢查資產上的版權聲明是否允許分發。 因此，系統將資產發送到一台或另一台伺服器。
* 工作流可以檢查沒有預定義的強制元資料或具有 *無效* 元資料。

>[!MORELIKETHIS]
>
>* [XMP 中繼資料](xmp-metadata.md)
>* [如何編輯或添加元資料](meta-edit.md)

