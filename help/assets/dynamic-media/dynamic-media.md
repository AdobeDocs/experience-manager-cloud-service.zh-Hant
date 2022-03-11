---
title: 與Dynamic Media合作
description: 瞭解如何使用Dynamic Media來在Web、移動和社交站點上為消費提供資產。
role: Admin,User
exl-id: 3ec3cb85-88ce-4277-a45c-30e52c75ed42
source-git-commit: fa6de4e383b4de628938fce455f321911cad452c
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 4%

---

# 與Dynamic Media合作 {#working-with-dynamic-media}

[Dynamic Media](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) 幫助按需提供豐富的視覺商品銷售和營銷資產，並自動擴展以在Web、移動和社交網站上消費。 使用一組主要源資產，Dynamic Media通過其全球、可擴展、效能優化的網路即時生成並提供多種豐富內容的變體。

Dynamic Media提供互動式觀看體驗，包括縮放、360°旋轉和視頻。 Dynamic Media獨一無二地納入了Adobe Experience Manager數字資產管理（資產）解決方案的工作流程，以簡化和簡化數字市場活動管理流程。

<!-- >[!NOTE]
>
>A Community article is available on [Working with Adobe Experience Manager and Dynamic Media](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html). -->

## 用Dynamic Media做什麼 {#what-you-can-do-with-dynamic-media}

Dynamic Media允許您在發佈資產之前管理資產。 如何處理一般資產，將在 [使用數字資產](/help/assets/manage-digital-assets.md)。 一般主題包括上載，下載，編輯和發佈資產；查看和編輯屬性，以及搜索資產。

僅Dynamic Media功能包括：

* [輪播橫幅](carousel-banners.md)
* [影像集](image-sets.md)
* [互動影像](interactive-images.md)
* [互動影片](interactive-videos.md)
* [混合媒體集](mixed-media-sets.md)
* [全景影像](panoramic-images.md)

* [迴轉集](spin-sets.md)
* [影片](video.md)
* [交付Dynamic Media資產](delivering-dynamic-media-assets.md)
* [管理資產](managing-assets.md)
* [使用快速視圖建立自定義彈出式Windows®](custom-pop-ups.md)

另請參閱 [設定Dynamic Media](administering-dynamic-media.md)。

<!-- 

OBSOLETE UNTIL INTEGRATING SCENE7 TOPIC GETS A MAJOR UPDATE
>[!NOTE]
>
>To understand the differences between using Dynamic Media and integrating Dynamic Media Classic with AEM, see [Dynamic Media Classic integration versus Dynamic Media](/help/sites-cloud/administering/integrating-scene7.md#aem-scene-integration-versus-dynamic-media).

-->

## Dynamic Media啟用與Dynamic Media禁用 {#dynamic-media-on-versus-dynamic-media-off}

您可以通過以下特徵來判斷是否啟用（開啟）Dynamic Media:

* 在下載或預覽資產時，動態格式副本可用。
* 映像集、旋轉集、混合媒體集可用。
* 建立PTIFF格式副本。

按一下影像資產時，資產的視圖與啟用Dynamic Media時不同。 Dynamic Media用的是點播HTML5觀眾。

### 動態格式副本 {#dynamic-renditions}

動態格式副本（如影像和查看器預設）（下） **[!UICONTROL 動態]**)時可用。

![chlimage_1-358](assets/chlimage_1-358.png)

### 影像集、旋轉集、混合媒體集 {#image-sets-spins-sets-mixed-media-sets}

如果啟用了Dynamic Media，則映像集、旋轉集和混合媒體集可用。

![chlimage_1-359](assets/chlimage_1-359.png)

### PTIFF格式副本 {#ptiff-renditions}

Dynamic Media啟用的資產包括 `pyramid.tiffs`。

![chlimage_1-360](assets/chlimage_1-360.png)

### 資產視圖更改 {#asset-views-change}

啟用Dynamic Media後，可通過按一下 `+` 和 `-` 按鈕。 也可按一下/點擊以放大特定區域。 還原將使您進入原始版本，您可以通過按一下對角線箭頭使影像全屏。 Dynamic Media啟用後，如下所示：

![chlimage_1-361](assets/chlimage_1-361.png)

禁用Dynamic Media後，可放大和縮小並恢復為原始大小：

![chlimage_1-362](assets/chlimage_1-362.png)
