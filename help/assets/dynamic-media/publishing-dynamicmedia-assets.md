---
title: 發佈 Dynamic Media 資產
description: 瞭解如何發佈Dynamic Media資產。
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 8ee759dc-cb8f-4e80-8175-2c3ba06da862
source-git-commit: a11529886d4b158c19a97ccbcb7d004cf814178d
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 5%

---

# 發佈 Dynamic Media 資產 {#publishing-dynamic-media-assets}

通過選擇已上載的資產並選擇 **[!UICONTROL 發佈]** 或 **[!UICONTROL 快速發佈]**。 在您的Dynamic Media資產發佈後，您可以通過URL或在頁面上嵌入代碼的方式將其包含在網頁中。

您還可以立即發佈上傳的資產 — 無需任何用戶干預。 或者，你可以有選擇地發佈這些資產。 請參閱 [配置Dynamic Media](config-dm.md)。 或者，你可以有選擇地向Dynamic Media或Adobe Experience Manager公佈資產，相互排斥，使用 **[!UICONTROL 選擇性發佈]** 在資料夾級別。 請參閱 [與選擇性出版合作在Dynamic Media](/help/assets/dynamic-media/selective-publishing.md)。

在 **[!UICONTROL 卡視圖]**，一個小型全球表徵圖將出現在資產名稱的正下方，並顯示在日期和時間的左側，以指示已發佈該資產。 在「清 **[!UICONTROL 單檢視]**」中，「已發佈」 **** 欄會指出已發佈或未發佈的資產。

>[!NOTE]
>
>如果資產已發佈，則您會將資產移動到另一個資料夾，並從其新位置重新發佈，則原始發佈的資產位置以及新重新發佈的資產仍然可用。 但是，原始已發佈的資產被Experience Manager&quot;丟失&quot;，無法取消發佈。 因此，作為最佳做法，在將資產移動到其他資料夾之前，請先取消發佈資產。

如果要在對視頻資源進行編碼後立即發佈它們，請確保編碼已完成。 當對視頻進行編碼時，系統會讓您知道視頻處理工作流正在進行中。 完成視頻編碼後，可以預覽視頻格式副本。 此時，您可以安全地發佈視頻，而不會發生任何發佈錯誤。

另請參閱 [將URL連結到Web應用程式](linking-urls-to-yourwebapplication.md)。

另請參閱 [將Dynamic Media視頻查看器或影像查看器嵌入網頁](embed-code.md)。

>[!NOTE]
>
>* 必須發佈資產才能使用URL。 如果資產未發佈，則複製URL並將其貼上到Web瀏覽器將不起作用。
>* 必須激活和發佈影像預設和查看器預設以便即時交付。
>


有關發佈集或資產的詳細資訊，請參閱 [發佈資產](/help/assets/manage-digital-assets.md)。

## HTTP/2交付Dynamic Media資產 {#http-delivery-of-dynamic-media-assets}

Experience Manager現在支援通過HTTP/2傳遞所有Dynamic Media內容（影像和視頻）。 即，可將影像或視頻的已發佈URL或嵌入代碼與接受託管資產的任何應用程式整合。 然後，該已發佈資產將通過HTTP/2協定交付。 這種傳送方法改進了瀏覽器和伺服器之間的通信方式，使您的所有Dynamic Media資產都能得到更好的響應和載入時間。

請參閱 [HTTP/2傳遞內容常見問題](/help/assets/dynamic-media/http2faq.md)。

<!--this md file used to reside under sites-administering-->
