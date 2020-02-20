---
title: 提供動態媒體資產
description: 瞭解如何提供動態媒體資產
translation-type: tm+mt
source-git-commit: 218afb360ec3a13f2f4562a703ca3184083fa7f6

---


# 提供動態媒體資產{#delivering-dynamic-media-assets}

如何提供動態媒體資產（視訊和影像）取決於網站的實作方式。

使用動態媒體時，您有數個選項：

* 如果您的網站是由AEM代管，則您想要直接將動態媒體資產新增至您的頁面。
* 如果您的網站未在AEM上，您可以選擇：

   * 將您的視訊或影像內嵌在您的網站上。
   * 將URL連結至您的Web應用程式。 當您想要將視訊播放器發佈為快顯視窗或強制視窗時，請使用連結。
   * 如果您的網站回應速度快，您就可以提 [供最佳化影像。](/help/assets/dynamic-media/responsive-site.md)

>[!NOTE]
>
>智慧型影像功能可與您現有的影像預設集搭配使用，並在傳送時的最後一毫秒使用智慧功能，根據瀏覽器或網路連線速度進一步降低影像檔案大小。 如需詳 [細資訊](/help/assets/dynamic-media/imaging-faq.md) ，請參閱智慧型影像。

如需詳細資訊，請參閱下列主題：

* [新增動態媒體資產至網頁](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)
* [將視訊或影像檢視器內嵌在網頁上](/help/assets/dynamic-media/embed-code.md)
* [在動態媒體中啟用熱連結保護](/help/assets/dynamic-media/hotlink-protection.md)
* [將URL連結至您的Web應用程式](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)
* [為互動式網站提供最佳化影像](/help/assets/dynamic-media/responsive-site.md)
* [HTTP2內容傳送](/help/assets/dynamic-media/http2faq.md)
* [使CDN快取內容無效](/help/assets/dynamic-media/invalidate-cdn-cached-content.md)
* [使用規則集轉換URL](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md)

## HTTP/2傳送動態媒體資產 {#http-delivery-of-dynamic-media-assets}

AEM現在支援透過HTTP/2傳送所有動態媒體內容（影像和視訊）。 也就是說，影像或視訊的已發佈URL或內嵌程式碼可與任何接受代管資產的應用程式整合。 然後，該已發佈資產會透過HTTP/2通訊協定傳送。 此傳送方式改善了瀏覽器和伺服器通訊的方式，讓您的所有動態媒體資產都能獲得較佳的回應和載入時間。

如需 [詳細資訊，請參閱HTTP/2內容傳送常見問題](/help/assets/dynamic-media/http2faq.md) 。
