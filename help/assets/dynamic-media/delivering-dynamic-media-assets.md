---
title: 傳送Dynamic Media Assets
description: 了解如何傳送Dynamic Media資產。
feature: Asset Management
role: User
exl-id: 4557b561-b3c4-4d6f-8044-2069bda41613
source-git-commit: 6933f053e11320d8201922723879983084c52209
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# 傳送Dynamic Media Assets{#delivering-dynamic-media-assets}

如何傳送Dynamic Media資產（包括視訊和影像）取決於網站的實作方式。

有了Dynamic Media，您有數個選項：

* 如果您的網站托管於Adobe Experience Manager，則您想要直接將Dynamic Media資產新增至頁面。
* 如果您的網站未Experience Manager，您可以選擇：

   * 將您的視訊或影像嵌入網站。
   * 將URL連結至您的Web應用程式。 當您想要以快顯視窗或強制回應視窗的形式傳送視訊播放器時，請使用連結。
   * 如果您的網站回應式，您可以 [傳遞最佳化的影像](/help/assets/dynamic-media/responsive-site.md).

>[!NOTE]
>
>智慧型影像處理可與您現有的影像預設集搭配使用。 它會在傳送的最後毫秒使用智慧，根據瀏覽器或網路連線速度進一步縮小影像檔案大小。 請參閱 [智慧型影像](/help/assets/dynamic-media/imaging-faq.md) 以取得更多資訊。

如需詳細資訊，請參閱下列主題：

* [將Dynamic Media Assets新增至網頁](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)
* [將視訊或影像檢視器內嵌在網頁上](/help/assets/dynamic-media/embed-code.md)
* [在Dynamic Media中啟用快速連結保護](/help/assets/dynamic-media/hotlink-protection.md)
* [將URL連結至您的Web應用程式](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)
* [為回應式網站提供最佳化的影像](/help/assets/dynamic-media/responsive-site.md)
* [HTTP2內容傳送](/help/assets/dynamic-media/http2faq.md)
* [透過Dynamic Media使CDN快取失效](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)
* [透過Dynamic Media Classic使CDN快取失效](/help/assets/dynamic-media/invalidate-cdn-cache-dm-classic.md)
* [使用規則集轉換URL](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md)

## HTTP/2傳送Dynamic Media資產 {#http-delivery-of-dynamic-media-assets}

Experience Manager現在支援透過HTTP/2傳送所有Dynamic Media內容（影像和影片）。 也就是說，影像或視訊的已發佈URL或內嵌程式碼可與接受託管資產的任何應用程式整合。 然後會透過HTTP/2通訊協定來傳送已發佈的資產。 此傳遞方法可改善瀏覽器和伺服器通訊的方式，讓所有Dynamic Media資產的回應和載入時間都更佳。

若要進一步了解，請參閱 [HTTP/2傳送內容常見問題](/help/assets/dynamic-media/http2faq.md).
