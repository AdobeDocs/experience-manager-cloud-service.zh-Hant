---
title: 發佈 Dynamic Media 資產
description: 瞭解如何發佈Dynamic Media影片和影像資產，以便透過URL或內嵌程式碼至網頁中。
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 8ee759dc-cb8f-4e80-8175-2c3ba06da862
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 7%

---

# 發佈 Dynamic Media 資產 {#publishing-dynamic-media-assets}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime和Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets與Edge Delivery Services整合</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI擴充性</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>啟用Dynamic Media Prime和Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>搜尋最佳實務</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>中繼資料最佳實務</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>具有 OpenAPI 功能的 Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開發人員文件</b></a>
        </td>
    </tr>
</table>

選取您已上傳的資產，並選取&#x200B;**[!UICONTROL 發佈]**&#x200B;或&#x200B;**[!UICONTROL 快速發佈]**，即可發佈您的Dynamic Media資產。 發佈Dynamic Media資產後，您就能透過URL或內嵌程式碼的方式，將資產納入網頁中。

您也可立即發佈您上傳的資產，無需任何使用者介入。 或者，您可以選擇發佈這些資產。 請參閱[設定Dynamic Media](config-dm.md)。 或者，您可以在資料夾層級使用&#x200B;**[!UICONTROL 選擇性發佈]**，選擇性地將資產發佈至Dynamic Media或Adobe Experience Manager （互斥）。 請參閱[在Dynamic Media中使用選擇性發佈](/help/assets/dynamic-media/selective-publishing.md)。

在&#x200B;**[!UICONTROL 卡片檢視]**&#x200B;中，資產名稱正下方以及日期和時間左側會顯示一個小型全球圖示，以指出資產已發佈。 在「清 **[!UICONTROL 單檢視]**」中，「已發佈」 **** 欄會指出已發佈或未發佈的資產。

>[!NOTE]
>
>如果資產已發佈，然後您將資產移動到另一個檔案夾，並從其新位置重新發佈，則仍然可以使用原始已發佈資產位置以及新重新發佈的資產。 然而，原始發佈的資產會「遺失」給Experience Manager，且無法取消發佈。 因此，最佳做法是先取消發佈資產，然後再將其移至其他資料夾。

如果您打算在編碼視訊資產後立即發佈，請務必完成編碼。 當視訊編碼時，系統會告知您視訊處理工作流程正在進行中。 視訊編碼完成後，您可以預覽視訊轉譯。 如此一來，您就可以安全地發佈影片，而不會發生任何發佈錯誤。

另請參閱[將URL連結至您的網頁應用程式](linking-urls-to-yourwebapplication.md)。

另請參閱[將Dynamic Media視訊檢視器或影像檢視器內嵌在網頁上](embed-code.md)。

>[!NOTE]
>
>* 必須發佈Assets才能使用該URL。 如果資產未發佈，將無法將URL複製並貼到網頁瀏覽器。
>* 影像預設集和檢視器預設集必須啟動並發佈，才能即時傳送。
>

如需發佈集合或資產的詳細資訊，請參閱[發佈Assets](/help/assets/manage-digital-assets.md)。

## Dynamic Media資產的HTTP/2傳送 {#http-delivery-of-dynamic-media-assets}

Experience Manager現在支援透過HTTP/2傳送所有Dynamic Media內容（影像和影片）。 也就是說，影像或視訊的已發佈URL或內嵌程式碼可整合至任何接受託管資產的應用程式。 該已發佈資產隨後會透過HTTP/2通訊協定傳送。 此傳送方式可改善瀏覽器和伺服器的通訊方式，讓您的所有Dynamic Media資產獲得更好的回應和載入時間。

請參閱[HTTP/2內容傳遞常見問題](/help/assets/dynamic-media/http2faq.md)。

<!--this md file used to reside under sites-administering-->
