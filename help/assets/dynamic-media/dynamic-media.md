---
title: 使用 Dynamic Media
description: 瞭解什麼是動態媒體，並且您可以使用Dynamic Media來傳遞資產，以便在網頁、行動裝置和社交網站上消耗。
contentOwner: Rick Brough
feature: Dynamic Media,Asset Management
role: Admin,User
exl-id: 3ec3cb85-88ce-4277-a45c-30e52c75ed42
source-git-commit: bc422429d4a57bbbf89b7af2283b537a1f516ab5
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 5%

---

# 使用 Dynamic Media {#working-with-dynamic-media}

[Dynamic Media](https://business.adobe.com/tw/products/experience-manager/assets/dynamic-media.html)可協助提供豐富的視覺銷售和行銷資產（隨選即用），並根據網路、行動及社交網站的消費自動調整。 Dynamic Media使用一組主要來源資產，透過其可擴充且效能最佳化的全域網路即時產生並傳送多種多樣的豐富內容。

Dynamic Media提供互動式檢視體驗，包括縮放、360度旋轉和視訊。 Dynamic Media以獨特方式整合Adobe Experience Manager數位資產管理(Assets)解決方案的工作流程，以簡化及簡化數位行銷活動管理程式。

<!-- 
>[!NOTE]
>
>A Community article is available on [Working with Adobe Experience Manager and Dynamic Media](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html). 
-->

## 什麼是Dynamic Media？

Adobe Experience Manager (AEM) as a Cloud Service中的Dynamic Media是功能強大的解決方案，旨在協助您跨數位平台管理、傳送及最佳化豐富媒體資產，例如影像和視訊。 它允許即時修改，例如調整大小、裁切及根據使用者的裝置或熒幕大小調整品質，從而將靜態媒體轉換為動態、吸引人的體驗。 有了Dynamic Media，無論使用者在桌上型電腦、行動裝置或平板電腦上，您的資產都會自動調整以提供最佳視覺體驗。

Dynamic Media的主要優點在於其能簡化媒體管理。 您不需要建立多個版本的影像或影片，Dynamic Media會針對各種情況提供最適合的格式來處理所有內容。 例如，電子商務企業可利用360度產品檢視或可縮放影像來建立互動式體驗，而內容豐富的網站則可確保快速、高品質的視訊串流。 這可加快載入時間並帶來更吸引人的使用者體驗，最終帶來更高的客戶滿意度和更好的轉換率。

Dynamic Media與AEM的數位資產管理(DAM)系統緊密整合，為您提供儲存、組織及部署媒體的單一平台。 這種集中式方法可簡化跨團隊的協同合作，並即時提供資產效能的深入分析。 無論您是專注於提供吸引人的視覺效果，還是增強媒體驅動的使用者互動，Dynamic Media都能協助您針對任何管道最佳化內容，使其成為企業提升其數位影響力的必要工具。

## 您可以使用Dynamic Media做什麼 {#what-you-can-do-with-dynamic-media}

Dynamic Media可讓您在發佈資產之前先管理資產。 [使用數位Assets](/help/assets/manage-digital-assets.md)中會詳細說明如何使用一般資產。 一般主題包括上傳、下載、編輯和發佈資產；檢視和編輯屬性以及搜尋資產。

僅限Dynamic Media的功能包括：

* [輪播橫幅](carousel-banners.md)
* [影像集](image-sets.md)
* [互動式影像](interactive-images.md)
* [互動式影片](interactive-videos.md)
* [混合媒體集](mixed-media-sets.md)
* [全景影像](panoramic-images.md)
* [迴轉集](spin-sets.md)
* [影片](video.md)
* [傳送Dynamic Media Assets](delivering-dynamic-media-assets.md)
* [管理Assets](managing-assets.md)
* [使用快速檢視建立自訂快顯視窗](custom-pop-ups.md)

另請參閱[設定Dynamic Media](administering-dynamic-media.md)。

<!-- 

OBSOLETE UNTIL INTEGRATING SCENE7 TOPIC GETS A MAJOR UPDATE
>[!NOTE]
>
>To understand the differences between using Dynamic Media and integrating Dynamic Media Classic with AEM, see [Dynamic Media Classic integration versus Dynamic Media](/help/sites-cloud/administering/integrating-scene7.md#aem-scene-integration-versus-dynamic-media).

-->

## Dynamic Media已啟用與Dynamic Media停用 {#dynamic-media-on-versus-dynamic-media-off}

您可以透過下列特性來判斷動態媒體是否已啟用（開啟）：

* 下載或預覽資產時，可使用動態轉譯。
* 影像集、迴轉集、混合媒體集可供使用。
* 已建立PTIFF轉譯。

當您按一下影像資產時，啟用動態媒體後，資產的檢視會不同。 Dynamic Media使用隨選HTML5檢視器。

### 動態轉譯 {#dynamic-renditions}

啟用Dynamic Media時，可以使用動態轉譯，例如影像和檢視器預設集（在&#x200B;**[!UICONTROL Dynamic]**&#x200B;下）。

![chlimage_1-358](assets/chlimage_1-358.png)

### Dynamic Media影像集、旋轉集、混合媒體集 {#image-sets-spins-sets-mixed-media-sets}

啟用Dynamic Media時，可以使用影像集、迴轉集及混合媒體集。

![chlimage_1-359](assets/chlimage_1-359.png)

### 啟用Dynamic Media的PTIFF轉譯 {#ptiff-renditions}

啟用Dynamic Media的資產包含`pyramid.tiffs`。

![chlimage_1-360](assets/chlimage_1-360.png)

### Dynamic Media資產檢視變更 {#asset-views-change}

啟用Dynamic Media後，按一下`+`和`-`按鈕即可放大和縮小。 您也可以選取放大特定區域。 「回覆」會將您帶至原始版本，而且您可以按一下對角線箭頭，讓影像變成全熒幕。 啟用的Dynamic Media如下所示：

![chlimage_1-361](assets/chlimage_1-361.png)

停用Dynamic Media後，您就可以放大和縮小並回覆成原始大小：

![chlimage_1-362](assets/chlimage_1-362.png)
