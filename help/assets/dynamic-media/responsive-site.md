---
title: 為互動式網站提供最佳化影像
description: 瞭解如何使用回應式程式碼功能來提供來自Dynamic Media的最佳化影像。
feature: 資產管理
topic: 業務從業人員
role: 業務從業人員
translation-type: tm+mt
source-git-commit: 497952b1b6679eca301839d1435924e16a2e2438
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 14%

---


# 為回應式網站傳送最佳化影像 {#delivering-optimized-images-for-a-responsive-site}

當您想要與網頁開發人員共用用於互動式服務的程式碼時，請使用「互動式程式碼」功能。 您可將回應式(**[!UICONTROL RESS]**)程式碼複製到剪貼簿，以便與網頁開發人員共用。

如果您的網站位於協力廠商WCM上，則使用此功能是合理的。 不過，若您的網站已開啟，AEM則Offsite影像伺服器會轉譯影像並提供給網頁。

另請參閱[將視訊檢視器內嵌在網頁上。](embed-code.md)

另請參閱[將URL連結到Web應用程式。](linking-urls-to-yourwebapplication.md)

**為互動式網站提供最佳化影像**:

1. 導覽至您要為其提供回應式程式碼的影像，然後在下拉式選單中，點選「轉譯」****。

   ![chlimage_1-408](assets/chlimage_1-408.png)

1. 選取回應式影像預設集。URL **[!UICONTROL 和]****[!UICONTROL RESS]** 按鈕出現。

   ![chlimage_1-409](assets/chlimage_1-409.png)

   >[!NOTE]
   >
   >必須發佈 *選取的資產* ，以及選取的影像預設集或檢視器預設集，才能使 **[!UICONTROL URL]** 或 **[!UICONTROL RESS]** 按鈕可用。
   >
   >影像預設集會自動發佈。

1. 點選&#x200B;**[!UICONTROL RESS]**。

   ![chlimage_1-410](assets/chlimage_1-410.png)

1. 在&#x200B;**[!UICONTROL 內嵌回應式影像]**&#x200B;對話方塊中，選取並複製回應式程式碼文字，並貼入您的網站以存取回應式資產。
1. 編輯內嵌程式碼中的預設中斷點，以直接比對程式碼中回應式網站的中斷點。 此外，測試在不同頁面中斷點處提供的不同影像解析度。

## 使用HTTP/2傳送您的Dynamic Media資產{#using-http-to-delivery-your-dynamic-media-assets}

HTTP/2是全新、更新的Web通訊協定，可改善瀏覽器和伺服器的通訊方式。 它提供更快速的資訊傳輸，並降低所需的處理能力。 使用HTTP/2支援傳送Dynamic Media資產，提供更佳的回應和載入時間。

如需開始使用HTTP/2與您的Dynamic Media帳戶的完整詳細資訊，請參閱[HTTP2內容傳送](http2faq.md)。
