---
title: 傳遞Dynamic Media資產
description: 瞭解如何透過內嵌視訊和影像，或將URL連結至您的網路應用程式，將Dynamic Media資產傳送至您的網頁。
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 4557b561-b3c4-4d6f-8044-2069bda41613
source-git-commit: 0e452bd94d75609ecc3c20ab6b56ded968ed0a70
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 9%

---

# 傳遞Dynamic Media資產{#delivering-dynamic-media-assets}

如何傳送Dynamic Media資產（包括影片和影像）取決於網站的實作方式。

Dynamic Media提供幾個選項：

* 如果您的網站託管於Adobe Experience Manager，那麼您想要直接將Dynamic Media資產新增至您的頁面。
* 如果您的網站不在Experience Manager上，您可以選擇以下任一選項：

   * 將您的影片或影像內嵌在網站上。
   * 將 URL 連結至您的網頁應用程式. 當您想要以快顯視窗或強制回應視窗的形式傳送視訊播放器時，請使用連結。
   * 如果您的網站有回應，您可以 [傳遞最佳化的影像](/help/assets/dynamic-media/responsive-site.md).

>[!NOTE]
>
>智慧型影像可與您現有的影像預設集搭配使用。 它會在傳送的最後一毫秒內運用智慧，根據瀏覽器或網路連線速度進一步縮小影像檔案大小。 另請參閱 [智慧型影像](/help/assets/dynamic-media/imaging-faq.md) 以取得詳細資訊。

如需詳細資訊，請參閱下列主題：

* [將Dynamic Media資產新增至網頁](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)
* [將視訊或影像檢視器內嵌在網頁上](/help/assets/dynamic-media/embed-code.md)
* [在 Dynamic Media 中啟動直接連結保護](/help/assets/dynamic-media/hotlink-protection.md)
* [將URL連結至您的網頁應用程式](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)
* [為回應式網站傳送最佳化影像](/help/assets/dynamic-media/responsive-site.md)
* [HTTP2傳送內容](/help/assets/dynamic-media/http2faq.md)
* [透過 Dynamic Media 使 CDN 快取失效](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)
* [透過 Dynamic Media Classic 使 CDN 快取失效](/help/assets/dynamic-media/invalidate-cdn-cache-dm-classic.md)
* [使用規則集轉換URL](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md)

## Dynamic Media資產的HTTP/2傳送 {#http-delivery-of-dynamic-media-assets}

Experience Manager現在支援透過HTTP/2傳送所有Dynamic Media內容（影像和視訊）。 也就是說，影像或視訊的已發佈URL或內嵌程式碼可整合至任何接受託管資產的應用程式。 該已發佈資產隨後會透過HTTP/2通訊協定傳送。 此傳送方式可改善瀏覽器和伺服器的通訊方式，讓您的所有Dynamic Media資產獲得更好的回應和載入時間。

若要深入瞭解，請參閱 [HTTP/2內容傳送常見問答](/help/assets/dynamic-media/http2faq.md).
