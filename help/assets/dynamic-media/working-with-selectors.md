---
title: 使用選取器
description: 瞭解在Dynamic Media中可用來選取互動式影像、互動式視訊和轉盤橫幅之資產的方法。
contentOwner: Rick Brough
feature: Selectors,Interactive Images,Interactive Videos,Carousel Banners
role: User
exl-id: a6f366ab-41b8-4909-b815-e6c4b938bf77
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 7%

---

# 在Dynamic Media中使用選取器 {#working-with-selectors}

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

使用互動式影像、互動式視訊或轉盤橫幅時，您會選取資產，並選取要連結至熱點與影像地圖的網站和產品。 使用影像集、迴轉集和多媒體集時，您也可以使用「資產選取器」選取資產。

本主題涵蓋如何使用產品、網站和資產選取器，包括在選取器中瀏覽、篩選和排序的功能。

您在建立轉盤集、新增熱點和影像地圖，以及建立互動式視訊和影像時存取選擇器。

例如，在此輪播橫幅中，如果您要將熱點或影像地圖連結至快速檢視頁面，請使用產品選擇器。 如果要將熱點或影像地圖連結至超連結，請使用網站選擇器；在建立幻燈片時使用資產選擇器。

![chlimage_1-520](assets/chlimage_1-520.png)

當您選取（而不是手動輸入）連結區或影像地圖的目標位置時，您使用的是選取器。 只有當您是[!DNL Adobe Experience Manager Sites]客戶時，網站選擇器才能運作。 產品選擇器還需要[!DNL Experience Manager Commerce]。

## 在Dynamic Media中選取產品 {#selecting-products}

當您想要讓熱點或影像地圖提供產品目錄中特定產品的快速檢視，請使用產品選擇器來選擇產品。

1. 導覽至「轉盤集」、「互動式影像」或「互動式視訊」，然後選取「**[!UICONTROL 動作]**」標籤（僅在您已定義熱點或影像地圖時可用）。

   產品選擇器位於&#x200B;**[!UICONTROL 動作型別]**&#x200B;區域。

   ![chlimage_1-521](assets/chlimage_1-521.png)

1. 選取&#x200B;**[!UICONTROL 產品選擇器]**&#x200B;圖示（放大鏡）並導覽至目錄中的產品。

   ![chlimage_1-522](assets/chlimage_1-522.png)

   您可以點選&#x200B;**[!UICONTROL 篩選器]**&#x200B;並輸入關鍵字，或選取標籤，或兩者同時進行，依關鍵字或標籤來篩選。

   ![chlimage_1-523](assets/chlimage_1-523.png)

   您可以點選「**[!UICONTROL 瀏覽]**」並導覽至其他資料夾，以變更[!DNL Experience Manager]瀏覽產品資料的位置。

   ![chlimage_1-524](assets/chlimage_1-524.png)

   選取&#x200B;**[!UICONTROL 依]**&#x200B;排序，以變更[!DNL Experience Manager]是依最新到最舊還是最舊到最新排序。

   ![chlimage_1-525](assets/chlimage_1-525.png)

   選取&#x200B;**[!UICONTROL 以]**&#x200B;檢視，以變更您檢視產品的方式 — **[!UICONTROL 清單檢視]**&#x200B;或&#x200B;**[!UICONTROL 卡片檢視]**。

   ![chlimage_1-526](assets/chlimage_1-526.png)

1. 選取產品後，欄位會填入產品縮圖和名稱。

   ![chlimage_1-527](assets/chlimage_1-527.png)

1. 在&#x200B;**[!UICONTROL 預覽]**&#x200B;模式中時，您可以選取熱點或影像地圖，並檢視快速檢視的顯示方式。

   ![chlimage_1-528](assets/chlimage_1-528.png)

## 在Dynamic Media中選取網站 {#selecting-sites}

當您想要將熱點或影像地圖連結至[!DNL Experience Manager]個網站內管理的網頁時，請使用網站選擇器來選擇網頁。

1. 導覽至「轉盤集」、「互動式影像」或「互動式視訊」，然後選取「**[!UICONTROL 動作]**」標籤（僅在您已定義熱點或影像地圖時可用）。

   「網站選擇器」位於「動 **[!UICONTROL 作類型]** 」區。

   ![chlimage_1-529](assets/chlimage_1-529.png)

1. 選取&#x200B;**[!UICONTROL 網站選擇器]**&#x200B;圖示（含放大鏡的資料夾），並導覽至您[!DNL Experience Manager]網站中要連結熱點或影像地圖的頁面。

   ![chlimage_1-530](assets/chlimage_1-530.png)

1. 選取網站後，欄位會填入路徑。

   ![chlimage_1-531](assets/chlimage_1-531.png)

1. 當您在&#x200B;**[!UICONTROL 預覽]**&#x200B;模式中選取熱點或影像地圖時，您可以導覽至您指定的[!DNL Experience Manager]網站頁面。

## 在Dynamic Media中選取資產 {#selecting-assets}

使用此選取器來選擇要用於轉盤橫幅、互動式視訊、影像集、混合媒體集和迴轉集的影像。 在互動式視訊中，當您在「**[!UICONTROL 內容]**」索引標籤中選取「**[!UICONTROL 選取Assets]**」時，資產選取器即可使用。 在「轉盤集」中，建立幻燈片時可使用資產選取器。 在「影像集」、「混合媒體集」和「迴轉集」中，當您分別建立「影像集」、「混合媒體集」或「迴轉集」時，可使用資產選取器。

另請參閱[資產選取器](/help/assets/search-assets.md#asset-selector)以取得詳細資訊。

1. 導覽至轉盤集並建立幻燈片。 或者，導覽至互動式視訊，前往「**[!UICONTROL 內容]**」標籤，然後選取資產。 或者，建立混合媒體集、影像集或迴轉集。
1. 選取&#x200B;**[!UICONTROL 資產選擇器]**&#x200B;圖示（含放大鏡的資料夾）並導覽至資產。

   ![chlimage_1-532](assets/chlimage_1-532.png)

   點選&#x200B;**[!UICONTROL 篩選器]**&#x200B;並輸入關鍵字、新增條件或兩者，依關鍵字或標籤篩選。

   ![chlimage_1-533](assets/chlimage_1-533.png)

   您可以導覽至&#x200B;**[!UICONTROL 路徑]**&#x200B;欄位中的其他資料夾，以變更[!DNL Experience Manager]瀏覽資產的位置。

   選取&#x200B;**[!UICONTROL 集合]**&#x200B;以僅搜尋集合中的資產。

   ![chlimage_1-534](assets/chlimage_1-534.png)

   選取&#x200B;**[!UICONTROL 以]**&#x200B;檢視，以變更您檢視產品的方式 — **[!UICONTROL 清單檢視]**、**[!UICONTROL 欄檢視]**&#x200B;或&#x200B;**[!UICONTROL 卡片檢視]**。

   ![chlimage_1-535](assets/chlimage_1-535.png)

1. 若要選取資產，請選取核取記號。 資產隨即顯示。

   ![chlimage_1-536](assets/chlimage_1-536.png)
—>
