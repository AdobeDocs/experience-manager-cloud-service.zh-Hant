---
title: 將動態媒體視訊或影像檢視器內嵌至網頁
description: 瞭解如何將動態媒體視訊或影像資產內嵌在網頁上。
translation-type: tm+mt
source-git-commit: 193201670e5e78235025885f52215cca730ce556
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 22%

---


# 將動態媒體視訊、影像檢視器或維度檢視器內嵌至網頁{#embedding-the-video-or-image-viewer-on-a-web-page}

當您想 **** 要播放視訊或檢視內嵌在網頁上的資產時，請使用「內嵌代碼」功能。您可將內嵌代碼複製到剪貼簿，以便貼到網頁中。「內嵌代碼」對話方塊中不允許編 **[!UICONTROL 輯代碼]** 。

只有當您&#x200B;_not_&#x200B;使用AEM做為WCM時，才內嵌URL。 如果您使用AEM做為WCM，則[會直接將資產新增至頁面。](adding-dynamic-media-assets-to-pages.md)

請參閱[將URL連結至您的Web應用程式。](linking-urls-to-yourwebapplication.md)

請參閱[為回應式網站提供最佳化影像。](responsive-site.md)

>[!NOTE]
>
>在您發佈所選資產之前，內嵌代碼無法複製。 此外，您也必須發佈檢視器預設集或影像預設集。
>
>請參閱[發佈資產](publishing-dynamicmedia-assets.md)。
>
>請參閱[Publishing Viewer Presets](managing-viewer-presets.md#publishing-viewer-presets)。
>
>請參閱[發佈影像預設集](managing-image-presets.md#publishing-image-presets)。

**將動態媒體視訊或影像檢視器內嵌在網頁上**

1. 導覽至您要複製其內嵌代碼的&#x200B;*published*&#x200B;視訊或影像資產。

   請記住，內嵌程式碼僅可在您首次 *發佈**資產後* 複製。此外，檢視器預設集或影像預設集也必須發佈。

   請參閱[發佈資產。](publishing-dynamicmedia-assets.md)

   請參閱[Publishing Viewer Presets](managing-viewer-presets.md#publishing-viewer-presets)。

   請參閱[發佈影像預設集](managing-image-presets.md#publishing-image-presets)。

1. 在左側導軌中，選擇下拉式清單並點選「**[!UICONTROL 檢視器]**」。
1. 在左側導軌中，點選檢視器預設集名稱。 檢視器預設會套用至資產。
1. 點選&#x200B;**[!UICONTROL Embed]**。
1. 在&#x200B;**[!UICONTROL 內嵌代碼]**&#x200B;對話方塊中，將整個代碼複製到剪貼簿，然後點選&#x200B;**[!UICONTROL 關閉]**。
1. 將內嵌代碼貼入您的網頁。

## 使用HTTP/2來傳送您的動態媒體資產{#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2是全新、更新的Web通訊協定，可改善瀏覽器和伺服器的通訊方式。 它提供更快速的資訊傳輸，並降低所需的處理能力。 動態媒體資產的傳送現在可透過HTTP/2，提供更佳的回應和載入時間。

如需開始使用HTTP/2與動態媒體帳戶的完整詳細資訊，請參閱[HTTP2內容傳送](http2faq.md)。
