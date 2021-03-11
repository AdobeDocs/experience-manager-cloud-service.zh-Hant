---
title: 交付Dynamic Media資產
description: 瞭解如何提供Dynamic Media資產。
translation-type: tm+mt
source-git-commit: a8eb6a88b889facca8518c05a80051fc17dd0617
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 1%

---


# 交付Dynamic Media資產{#delivering-dynamic-media-assets}

如何傳遞您的Dynamic Media資產（包括視訊和影像），取決於網站的實作方式。

有了Dynamic Media，你有幾種選擇：

* 如果您的網站是裝載AEM在上，則您要直接將Dynamic Media資產新增至您的頁面。
* 如果您的網站未AEM開啟，您可以選擇：

   * 將您的視訊或影像內嵌在您的網站上。
   * 將URL連結至您的Web應用程式。 當您想要將視訊播放器發佈為快顯視窗或強制視窗時，請使用連結。
   * 如果您的網站回應速度快，您可以[傳送最佳化的影像。](/help/assets/dynamic-media/responsive-site.md)

>[!NOTE]
>
>智慧型影像功能可與您現有的影像預設集搭配使用。 它使用傳送時最後一毫秒的智慧，根據瀏覽器或網路連線速度進一步降低影像檔案大小。 如需詳細資訊，請參閱[智慧型影像](/help/assets/dynamic-media/imaging-faq.md)。

如需詳細資訊，請參閱下列主題：

* [新增Dynamic Media資產至網頁](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)
* [將視訊或影像檢視器內嵌在網頁上](/help/assets/dynamic-media/embed-code.md)
* [在 Dynamic Media 中啟用超連結保護](/help/assets/dynamic-media/hotlink-protection.md)
* [將URL連結至您的Web應用程式](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)
* [為互動式網站提供最佳化影像](/help/assets/dynamic-media/responsive-site.md)
* [HTTP2內容傳送](/help/assets/dynamic-media/http2faq.md)
* [通過Dynamic Media使CDN快取失效](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)
* [利用Dynamic MediaClassic對CDN快取進行失效](/help/assets/dynamic-media/invalidate-cdn-cache-dm-classic.md)
* [使用規則集轉換URL](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md)

## HTTP/2交付Dynamic Media資產{#http-delivery-of-dynamic-media-assets}

現在AEM支援透過HTTP/2傳送所有Dynamic Media內容（影像和視訊）。 也就是說，影像或視訊的已發佈URL或內嵌程式碼可與任何接受代管資產的應用程式整合。 然後，該已發佈資產會透過HTTP/2通訊協定傳送。 這種傳送方式改善了瀏覽器和伺服器通訊的方式，讓所有Dynamic Media資產的回應和載入時間都更佳。

如需詳細資訊，請參閱[HTTP/2內容傳送常見問題](/help/assets/dynamic-media/http2faq.md)。
