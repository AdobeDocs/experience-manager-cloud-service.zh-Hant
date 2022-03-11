---
title: 交付Dynamic Media資產
description: 瞭解如何交付Dynamic Media資產。
feature: Asset Management
role: User
exl-id: 4557b561-b3c4-4d6f-8044-2069bda41613
source-git-commit: 6933f053e11320d8201922723879983084c52209
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# 交付Dynamic Media資產{#delivering-dynamic-media-assets}

您如何交付您的Dynamic Media資產 — 包括視頻和影像 — 取決於您網站的實施方式。

對於Dynamic Media，你有幾種選擇：

* 如果您的網站位於Adobe Experience Manager，則您希望將Dynamic Media資產直接添加到您的頁面。
* 如果您的網站未Experience Manager，則您可以選擇：

   * 將視頻或影像嵌入到您的網站。
   * 將URL連結到Web應用程式。 當要將視頻播放器作為彈出窗口或模式窗口傳送時，請使用連結。
   * 如果您的站點響應迅速，您可以 [提供優化的映像](/help/assets/dynamic-media/responsive-site.md)。

>[!NOTE]
>
>智慧成像可與現有影像預設配合使用。 它使用在傳送的最後一毫秒時的智慧，根據瀏覽器或網路連接速度進一步減小影像檔案大小。 請參閱 [智慧映像](/help/assets/dynamic-media/imaging-faq.md) 的子菜單。

有關詳細資訊，請參閱以下主題：

* [將Dynamic Media資產添加到網頁](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)
* [將視頻或影像查看器嵌入網頁](/help/assets/dynamic-media/embed-code.md)
* [在Dynamic Media激活熱鏈路保護](/help/assets/dynamic-media/hotlink-protection.md)
* [將URL連結到Web應用程式](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)
* [為響應性站點提供優化的映像](/help/assets/dynamic-media/responsive-site.md)
* [HTTP2內容傳遞](/help/assets/dynamic-media/http2faq.md)
* [通過Dynamic Media使CDN快取無效](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)
* [通過Dynamic Media Classic使CDN快取無效](/help/assets/dynamic-media/invalidate-cdn-cache-dm-classic.md)
* [使用規則集轉換URL](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md)

## HTTP/2交付Dynamic Media資產 {#http-delivery-of-dynamic-media-assets}

Experience Manager現在支援通過HTTP/2傳遞所有Dynamic Media內容（影像和視頻）。 即，可將影像或視頻的已發佈URL或嵌入代碼與接受託管資產的任何應用程式整合。 然後，該已發佈資產將通過HTTP/2協定交付。 這種傳送方法改進了瀏覽器和伺服器之間的通信方式，使您的所有Dynamic Media資產都能得到更好的響應和載入時間。

要瞭解更多資訊，請參閱 [HTTP/2內容傳遞常見問題](/help/assets/dynamic-media/http2faq.md)。
