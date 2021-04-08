---
title: 發佈Dynamic Media資產
description: 瞭解如何發佈Dynamic Media資產。
contentOwner: Rick Brough
feature: 資產管理
topic: 業務從業人員
role: Business Practitioner
exl-id: 8ee759dc-cb8f-4e80-8175-2c3ba06da862
translation-type: tm+mt
source-git-commit: 6b232ab512a6faaf075faa55c238dfb10c00b100
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 3%

---

# 發佈Dynamic Media資產{#publishing-dynamic-media-assets}

您可以選擇已上傳的資產，然後點選&#x200B;**[!UICONTROL Publish]**&#x200B;或&#x200B;**[!UICONTROL Quick Publish]**，以發佈您的Dynamic Media資產。 發佈您的Dynamic Media資產後，您就可透過URL或在頁面上內嵌程式碼，將其加入網頁。

您也可以立即發佈上傳的資產，不需任何使用者干預。 或者，您可以選擇性地發佈這些資產。 請參閱[配置Dynamic Media](config-dm.md)。 或者，您可以使用資料夾層級的&#x200B;**[!UICONTROL 選擇性發佈]**，選擇性地將資產發佈至彼此互斥的Dynamic Media或Adobe Experience Manager。 請參閱[在Dynamic Media使用選擇性發佈](/help/assets/dynamic-media/selective-publishing.md)。

在&#x200B;**[!UICONTROL 資訊卡檢視]**&#x200B;中，資產名稱正下方以及日期與時間左側會顯示一個小型全球圖示，以指出資產已發佈。 在「清 **[!UICONTROL 單檢視]**」中，「已發佈」 **** 欄會指出已發佈或未發佈的資產。

>[!NOTE]
>
>如果資產已發佈，則您會將資產移至另一個檔案夾，並從其新位置重新發佈，則原始已發佈的資產位置以及新重新發佈的資產仍然可用。 但是，原始發佈的資產「遺失」至Experience Manager，無法解除發佈。 因此，在將資產移至其他資料夾之前，請先解除發佈資產，這是最佳作法。

如果您想在編碼後立即發佈視訊資產，請確定已完成編碼。 當視訊正在編碼時，系統會讓您知道視訊處理工作流程正在進行中。 完成視訊編碼後，您就可以預覽視訊轉譯。 此時，您可以放心地發佈視訊，而不會發生任何發佈錯誤。

另請參閱[將URL連結到Web應用程式](linking-urls-to-yourwebapplication.md)。

另請參閱[將Dynamic Media視頻查看器或影像查看器嵌入網頁](embed-code.md)。

>[!NOTE]
>
>* 必須發佈資產才能使用URL。 如果資產未發佈，複製URL並貼至網頁瀏覽器將無法運作。
>* 必須啟用並發佈影像預設集和檢視器預設集，才能即時傳送。

>



如需發佈集合或資產的詳細資訊，請參閱[發佈資產](/help/assets/manage-digital-assets.md)。

## HTTP/2交付Dynamic Media資產{#http-delivery-of-dynamic-media-assets}

Experience Manager現在支援透過HTTP/2傳送所有Dynamic Media內容（影像和視訊）。 也就是說，影像或視訊的已發佈URL或內嵌程式碼可與任何接受代管資產的應用程式整合。 然後，該已發佈資產會透過HTTP/2通訊協定傳送。 這種傳送方式改善了瀏覽器和伺服器通訊的方式，讓所有Dynamic Media資產的回應和載入時間都更佳。

請參閱[HTTP/2內容傳送常見問題](/help/assets/dynamic-media/http2faq.md)。

<!--this md file used to reside under sites-administering-->
