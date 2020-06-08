---
title: 使用 Dynamic Media
description: 瞭解如何使用動態媒體來提供資產，以便在網頁、行動裝置和社交網站上使用。
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 7%

---


# 使用 Dynamic Media {#working-with-dynamic-media}

[動態媒體](https://www.adobe.com/solutions/web-experience-management/dynamic-media.html) ，可協助您隨選提供豐富的視覺化銷售和行銷資產，並自動調整規模，以便在網頁、行動裝置和社交網站上消費。 Dynamic Media使用一組主資產，透過其全球、可擴充、最佳化效能的網路，即時產生並提供多種多樣化內容變化。

動態媒體提供互動式檢視體驗，包括縮放、360度旋轉和視訊。 動態媒體獨一無二地整合了Adobe Experience Manager數位資產管理(Assets)解決方案的工作流程，以簡化數位宣傳管理流程。

>[!NOTE]
>
>有關使用Adobe Experience Manager和動態媒 [體的資訊，請參閱社群文章](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html)。

## Dynamic Media的功能 {#what-you-can-do-with-dynamic-media}

動態媒體可讓您在發佈資產之前先管理資產。 使用數位資產中會詳細說明如何使用 [資產](/help/assets/manage-digital-assets.md)。 一般主題包括上傳、下載、編輯和發佈資產； 檢視和編輯屬性，以及搜尋資產。

僅限動態媒體的功能包括：

* [輪播橫幅](carousel-banners.md)
* [影像集](image-sets.md)
* [互動影像](interactive-images.md)
* [互動影片](interactive-videos.md)
* [混合媒體集](mixed-media-sets.md)
* [全景影像](panoramic-images.md)

* [迴轉集](spin-sets.md)
* [影片](video.md)
* [提供動態媒體資產](delivering-dynamic-media-assets.md)
* [管理資產](managing-assets.md)
* [使用「快速檢視」建立自訂快顯視窗](custom-pop-ups.md)

另請參閱 [設定動態媒體](administering-dynamic-media.md)。

<!-- 

OBSOLETE UNTIL INTEGRATING SCENE7 TOPIC GETS A MAJOR UPDATE
>[!NOTE]
>
>To understand the differences between using Dynamic Media and integrating Dynamic Media Classic with AEM, see [Dynamic Media Classic integration versus Dynamic Media](/help/sites-cloud/administering/integrating-scene7.md#aem-scene-integration-versus-dynamic-media).

-->

## 啟用動態媒體與停用動態媒體 {#dynamic-media-on-versus-dynamic-media-off}

您可以透過下列特性來判斷動態媒體是否已啟用（開啟）:

* 動態轉譯可在下載或預覽資產時使用。
* 影像集、回轉集、混合媒體集皆可使用。
* 會建立PTIFF轉譯。

當您按一下影像資產時，資產的檢視會與啟用動態媒體時不同。 動態媒體使用隨選HTML5檢視器。

### 動態轉譯 {#dynamic-renditions}

啟用「動態媒體」時，動態轉譯(例如影像和檢視器預 **[!UICONTROL 設集]**，在「動態媒體」下)可用。

![chlimage_1-358](assets/chlimage_1-358.png)

### 影像集、旋轉集、混合媒體集 {#image-sets-spins-sets-mixed-media-sets}

啟用動態媒體時，影像集、回轉集和混合媒體集都可用。

![chlimage_1-359](assets/chlimage_1-359.png)

### PTIFF轉譯 {#ptiff-renditions}

啟用動態媒體的資產包括 `pyramid.tiffs`。

![chlimage_1-360](assets/chlimage_1-360.png)

### 資產檢視變更 {#asset-views-change}

啟用「動態媒體」後，您可以按一下和按鈕來放大 `+` 和縮 `-` 小。 您也可以按一下／點選以放大檢視特定區域。 Revert會將您帶到原始版本，您可以按一下對角線箭頭，使影像成為全螢幕。 啟用動態媒體的外觀如下：

![chlimage_1-361](assets/chlimage_1-361.png)

停用「動態媒體」後，您可以放大和縮小並回復為原始大小：

![chlimage_1-362](assets/chlimage_1-362.png)
