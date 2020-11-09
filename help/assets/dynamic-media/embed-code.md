---
title: 將動態媒體視訊或影像檢視器內嵌至網頁
description: 瞭解如何將動態媒體視訊或影像內嵌在網頁上
translation-type: tm+mt
source-git-commit: 7dae5c0ed82687415719cd2d72f98028cf0a8e64
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 22%

---


# 將動態媒體視訊、影像檢視器或維度檢視器內嵌在網頁上 {#embedding-the-video-or-image-viewer-on-a-web-page}

當您想 **** 要播放視訊或檢視內嵌在網頁上的資產時，請使用「內嵌代碼」功能。您可將內嵌代碼複製到剪貼簿，以便貼到網頁中。「內嵌代碼」對話方塊中不允許編 **[!UICONTROL 輯代碼]** 。

只有當您未將AEM用 _作_ WCM時，才內嵌URL。 如果您使用AEM做為WCM，則 [直接在頁面上新增資產。](adding-dynamic-media-assets-to-pages.md)

See [Linking URLs to your Web Application.](linking-urls-to-yourwebapplication.md)

See [Delivering Optimized Images for a Responsive Site.](responsive-site.md)

>[!NOTE]
>
>在您發佈所選資產之前，內嵌代碼無法複製。 此外，您也必須發佈檢視器預設集或影像預設集。
>
>請參閱 [發佈資產](publishing-dynamicmedia-assets.md)。
>
>請參 [閱Publishing Viewer預設集](managing-viewer-presets.md#publishing-viewer-presets)。
>
>請參閱 [發佈影像預設集](managing-image-presets.md#publishing-image-presets)。

**將動態媒體視訊或影像檢視器內嵌在網頁上**

1. 導覽至您要 *複製其內嵌* 、已發佈的視訊或影像資產。

   請記住，內嵌程式碼僅可在您首次 *發佈**資產後* 複製。此外，檢視器預設集或影像預設集也必須發佈。

   請參閱 [發佈資產。](publishing-dynamicmedia-assets.md)

   請參 [閱Publishing Viewer預設集](managing-viewer-presets.md#publishing-viewer-presets)。

   請參閱 [發佈影像預設集](managing-image-presets.md#publishing-image-presets)。

1. 在左側導軌中，選取下拉式選單並點選「檢 **[!UICONTROL 視器]**」。
1. 在左側導軌中，點選檢視器預設集名稱。 檢視器預設會套用至資產。
1. 點選「 **[!UICONTROL 內嵌]**」。
1. 在「內 **[!UICONTROL 嵌代碼]** 」對話方塊中，將整個代碼複製到剪貼簿，然後點選「 **[!UICONTROL 關閉」]**。
1. 將內嵌代碼貼入您的網頁。

## 使用HTTP/2來傳送您的動態媒體資產 {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2是全新、更新的Web通訊協定，可改善瀏覽器和伺服器的通訊方式。 它提供更快速的資訊傳輸，並降低所需的處理能力。 動態媒體資產的傳送現在可透過HTTP/2，提供更佳的回應和載入時間。

如需 [您的動態媒體帳戶開始使用HTTP/2的完整詳細資訊，請參閱HTTP2內容傳送](http2faq.md) 。
