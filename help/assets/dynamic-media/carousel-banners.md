---
title: 輪播橫幅
description: 瞭解如何在Dynamic Media中使用轉盤橫幅。
contentOwner: Rick Brough
feature: Carousel Banners
role: User
exl-id: 34541302-6610-4f5e-af93-c95328dda910
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '4492'
ht-degree: 1%

---

# 輪播橫幅{#carousel-banners}

輪播橫幅可讓行銷人員輕鬆建立互動式輪播促銷內容，並將內容傳送至任何畫面，藉此促進轉換。

建立和修改促銷橫幅中的主要內容可能很耗時，這會限制您快速發佈新內容或使其更具針對性的能力。 輪播橫幅可讓您快速建立或修改旋轉橫幅，並新增互動功能，例如連結至產品詳細資料或相關資源的熱點。 您可以在任何熒幕上提供這些內容，讓您更快將新的促銷內容推向市場。

轉盤橫幅是由具有單字&#x200B;**[!UICONTROL CAROUSELSET]**&#x200B;的橫幅指定：

![chlimage_1-438](assets/chlimage_1-438.png)

在您的網站上，輪播橫幅看起來可能如下所示：

![chlimage_1-439](assets/chlimage_1-439.png)

您可以在此選取數字來瀏覽影像。 此外，幻燈片會根據您可以自訂的時間間隔自動旋轉。 轉盤橫幅中的影像同時支援熱點與影像地圖。 使用者可以選取或前往超連結或存取快速檢視視窗。

在此範例中，使用者已選取影像地圖並存取手套的快速檢視視窗：

![chlimage_1-440](assets/chlimage_1-440.png)

## 觀看輪播橫幅的建立方式 {#watch-how-carousel-banners-are-created}

觀看如何建立[輪播橫幅的逐步解說](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&emailurl=https://s7d5.scene7.com/s7/emailFriend&serverUrl=https://s7d5.scene7.com/is/image/&config=Scene7SharedAssets/Universal_HTML5_Video_social&contenturl=https://s7d5.scene7.com/skins/&asset=S7tutorials/InteractiveCarouselBanner) （持續時間： 10分33秒）。 您也會瞭解如何預覽、編輯及傳遞輪播橫幅。

>[!NOTE]
>
>必須將非管理使用者新增到&#x200B;**[!UICONTROL dam-users]**&#x200B;群組，才能建立或編輯輪播橫幅。 如果您在建立或編輯時遇到問題，請洽詢系統管理員，以便將您新增至&#x200B;**d[!UICONTROL am-users]**&#x200B;群組。

## 快速入門：輪播橫幅 {#quick-start-carousel-banners}

快速上手並執行：

1. [識別熱點和影像地圖變數](#identifying-hotspot-and-image-map-variables) (僅適用於使用Adobe Experience Manager Assets + Dynamic Media的客戶)

   首先，識別現有快速檢視實施所使用的動態變數。 這麼做可協助您在Experience Manager Assets中的轉盤橫幅建立程式期間，正確輸入熱點和影像地圖資料。

<!-- LEAVE; COMMERCE BEING ADDED AGAIN IN THE FUTURE

   >[!NOTE]
   >
   >If you are an Experience Manager Sites or Ecommerce customer, you can use the built-in feature to navigate to product pages and lookup the existing skus in the product catalog. You do not need to manually enter hotspot or image map variables.
   >
   >
   >If you are an Experience ManagerAssets and Dynamic Media customer, you will manually enter data for hotspots and image maps, and then integrate the published URL or Embed code with your third-party content management system.

-->

1. 可選：視需 [要建立轉盤集檢視器預設](/help/assets/dynamic-media/managing-viewer-presets.md)。

   如果您是管理員，可以透過建立自己的轉盤檢視器預設集來自訂轉盤的行為和外觀。 主要優點在於您可以對多個輪播重複使用此自訂檢視器預設集。 不過，使用者可以選擇在編寫轉盤時直接自訂轉盤的行為和外觀。 如果您想要為特定輪播提供特定設計，建議使用此方法。

1. [上傳影像橫幅](#uploading-image-banners)。

   上傳您想要互動的影像橫幅。

1. [建立轉盤集](#creating-carousel-sets)。

   在輪播集中，使用者會瀏覽橫幅影像，並選取熱點或影像地圖以存取相關內容。

   若要在Assets中建立轉盤集，請選取&#x200B;**[!UICONTROL 建立]**，然後選取&#x200B;**[!UICONTROL 轉盤集]**。 將資產新增至投影片並選取&#x200B;**[!UICONTROL 儲存]**。 您也可以直接在編輯器中編輯轉盤的外觀和行為。

1. [新增熱點或影像地圖至影像橫幅](#adding-hotspots-or-image-maps-to-an-image-banner)。

   新增一或多個熱點或影像地圖至影像橫幅。 然後，將每個專案與連結、快速檢視或體驗片段等動作建立關聯。 新增熱點或影像地圖後，您可以發佈轉盤集來完成此工作。 發佈作業會建立內嵌程式碼，您可將其用於複製並套用至網站登陸頁面。

   請參閱[&#x200B; （選擇性）預覽轉盤橫幅](#optional-previewing-carousel-banners) — 選擇性。 如有需要，您可以檢視轉盤集的表示方式，並測試其互動性。

1. [發佈轉盤橫幅](#publishing-carousel-banners)。

   您可以像發佈任何資產一樣發佈轉盤集。 在Assets中，導覽至轉盤集並加以選取，然後選取「**[!UICONTROL 發佈]**」。 發佈轉盤集時會啟用URL和內嵌字串。

1. 執行下列任一項作業：

   * [新增轉盤橫幅至您的網站頁面](#adding-a-carousel-banner-to-your-website-page)您可以新增轉盤橫幅URL或內嵌程式碼（您已複製至網站頁面）。

      * [將輪播橫幅與現有的快速檢視整合](#integrating-the-carousel-banner-with-an-existing-quickview)。 如果您使用協力廠商Web內容管理系統，則必須將新的轉盤橫幅與網站上現有的快速檢視實作整合。

   * [在Experience Manager中新增輪播橫幅至您的網站](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)。 如果您是Experience Manager Sites客戶，則可以使用互動媒體元件，將轉盤集直接新增至頁面。

如果您必須編輯轉盤集，請參閱[編輯轉盤集](#editing-carousel-sets)。 此外，您也可以檢視及編輯[轉盤集屬性](/help/assets/manage-digital-assets.md#editing-properties)。

## 識別熱點和影像地圖變數 {#identifying-hotspot-and-image-map-variables}

首先，識別現有快速檢視實施所使用的動態變數。 此方法可協助您在Experience Manager Assets中的轉盤集建立程式期間正確輸入熱點或影像地圖資料。

當您將熱點或影像地圖新增至橫幅影像時，您會指派SKU （庫存單位）。 您也可以將選用的額外變數指派給每個熱點或影像地圖。 這類變數稍後會用於比對熱點或影像地圖與快速檢視內容。

<!-- LEAVE; COMMERCE BEING ADDED LATER

>[!NOTE]
>
>If you are an Experience Manager Sites and/or Experience Manager Ecommerce customer, skip this step. You do not need to manually identify hotspot or image map variables; you can use the integration with Ecommerce for product integration. See information on [setting up eCommerce](/help/sites-cloud/administering/generic.md). In addition, you can use the Interactive component and add it to your web page.
>
>If you are an Experience Manager Assets or Media customer, you publish the URL or Embed code and then integrate with your third-party content management system and identify hotspots and image maps manually.

-->

請務必正確識別要與熱點或影像地圖資料相關聯的變數數量和型別。 新增至橫幅影像的每個熱點或影像地圖都必須包含足夠的資訊，以明確識別現有後端系統中的產品。 同時，請確定每個熱點或影像地圖未包含超過必要的資料。 原因是這會使資料輸入流程過於複雜且進行中的熱點或影像地圖管理更容易出錯。

有不同的方式可識別要用於熱點或影像地圖資料的一組變數。

有時候，諮詢負責現有Quickview實作的IT專家就足夠了。 他們可能會知道系統中用於識別快速檢視的最小資料集為何。 但是，也可以只分析前端計畫碼的現有行為。

大部分的「快速檢視」實作都使用下列範例：

* 使用者在網站上啟動使用者介面元素。例如，選取&#x200B;**[!UICONTROL 快速檢視]**&#x200B;按鈕。
* 如有需要，網站會傳送Ajax要求至後端以載入Quickview資料或內容。
* 快速檢視資料會轉譯成內容，以備在網頁上轉譯。
* 最後，前端程式碼會在畫面上以視覺化方式呈現此類內容。

接著，方法就是瀏覽已實作「快速檢視」功能的現有網站的不同區域。 然後觸發Quickview並取得網頁傳送的Ajax URL，以載入Quickview資料或內容。

通常您不需要使用任何專門的偵錯工具。 現代的網頁瀏覽器配備能夠執行適當工作的網頁檢查器。 以下是一些包含網頁檢查器的網頁瀏覽器範例：

* 若要在Google Chrome中檢視所有傳出的HTTP要求，請按下F12 (Windows®)或Command-Option-I (Mac)以開啟開發人員工具面板。 選取「網路」標籤。
* 在Firefox中，您可以按F12 (Windows®)或Command-Option-I (Mac)來啟動Firebug外掛程式。 使用其「網路」標籤，或使用內建的「偵測器」工具及其「網路」標籤。

在瀏覽器中開啟網路監視時，會觸發頁面上的快速檢視。

現在，您可以在網路記錄中找到快速檢視Ajax URL，並複製紀錄的URL以供日後分析。 通常當您觸發「快速檢視」時，會有許多要求傳送至伺服器。 通常，快速檢視Ajax URL是清單中的第一個專案。 它具有複雜的查詢字串部分或路徑，而且其回應MIME型別是`text/html`、`text/xml`或`text/javascript`。

在此過程中，請務必使用不同的產品類別和型別，造訪您網站的不同區域。 原因是快速檢視URL具有指定網站類別的共同部分，但只有在您造訪網站的其他區域時才會變更。

最簡單的情況是，快速檢視URL中的唯一變數部分是產品SKU。 在此情況下，將「熱點」或「影像地圖」新增至橫幅影像時，SKU值是您唯一需要的資料片段。

不過，在複雜的情況下，除了SKU之外，快速檢視URL還有不同的變數元素。 其中一些元素包括類別ID、顏色代碼、大小代碼等。 在這種情況下，每個元素都是您熱點中的獨立變數，或是輪播橫幅功能中的影像地圖資料定義。

請考量下列快速檢視URL範例及其產生的熱點或影像地圖變數：

<table>
 <tbody>
  <tr>
   <td>在查詢字串中找到單一SKU。</td>
   <td><p>錄製的快速檢視URL包含以下專案：</p>
    <ul>
     <li><p><code>https://server/json?productId=866558&source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1196184&source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1081492&source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1898294&source=100</code></p> </li>
    </ul> <p>URL中唯一的變數部分是<code>productId=</code>查詢字串引數的值，而且它顯然是SKU值。 因此，熱點或影像地圖只需要填入如下值的SKU欄位 <code>866558,</code> <code>1196184,</code> <code>1081492,</code> <code>1898294.</code></p> </td>
  </tr>
  <tr>
   <td>在URL路徑中找到單一SKU。</td>
   <td><p>錄製的快速檢視URL包含以下專案：</p>
    <ul>
     <li><p><code>https://server/product/6422350843</code></p> </li>
     <li><p><code>https://server/product/1607745002</code></p> </li>
     <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>變數部分位於路徑的最後一部分，並且變成熱點/影像地圖的SKU值： <strong><code>6422350843</code>，<code>1607745002,</code> </strong><code>0086724882.</code></p> </td>
  </tr>
  <tr>
   <td>查詢字串中的SKU和類別ID。</td>
   <td><p>錄製的快速檢視URL包含以下專案：</p>
    <ul>
     <li><p><code>https://server/quickView/product/?category=1100004&prodId=305466</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1100004&prodId=310181</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1740148&prodId=308706</code></p> </li>
    </ul> <p>在這種情況下，URL中有兩個不同的部分。 SKU儲存在<code>prodId</code>引數中，而類別識別碼儲存在<code>category=</code>引數中。</p> <p>因此，熱點/影像地圖定義是配對。 即SKU值和稱為<code>categoryId</code>的額外變數。 產生的配對如下：</p>
    <ul>
     <li><p>SKU是<strong><code>305466</code></strong>，<code>categoryId</code>是<code>1100004</code>。</p> </li>
     <li><p>SKU是<strong><code>310181</code></strong>，<code>categoryId</code>是<strong><code>1100004</code></strong>。</p> </li>
     <li><p>SKU是<strong><code>308706</code></strong>，<code>categoryId</code>是<strong><code>1740148</code></strong>。</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 上傳影像橫幅 {#uploading-image-banners}

如果您已上傳要使用的影像，請繼續進行下一個步驟： [建立轉盤集](#creating-carousel-sets)。 Dynamic Media啟用後，必須上傳轉盤中使用的影像。

若要上傳影像橫幅，請參閱[上傳資產](/help/assets/manage-digital-assets.md)。

## 建立轉盤集 {#creating-carousel-sets}

>[!NOTE]
>
>必須將非管理使用者新增到&#x200B;**[!UICONTROL dam-users]**&#x200B;群組，才能建立或編輯輪播橫幅。 如果您在建立或編輯時遇到問題，請洽詢系統管理員，以便將您新增至&#x200B;**[!UICONTROL dam-users]**&#x200B;群組。

**若要建立轉盤集：**

1. 在Assets中，導覽至您要建立轉盤集的資料夾，然後前往&#x200B;**[!UICONTROL 建立>轉盤集]**。
1. 在「轉盤橫幅編輯器」頁面上，選取&#x200B;**[!UICONTROL 點選以開啟「資產選取器」]**&#x200B;以選取您第一張幻燈片的影像。

   在「輪播橫幅編輯器」頁面上，執行下列任一項作業：

   * 在頁面的左上角附近，選取&#x200B;**[!UICONTROL 新增投影片]**&#x200B;圖示。

   * 在頁面中間附近，選取&#x200B;**[!UICONTROL 點選以開啟「資產選取器」]**。

   選取以選取您要納入轉盤集的資產。 選取的資產上面有勾號圖示。 完成後，在頁面的右上角附近，選取&#x200B;**[!UICONTROL 選取]**。

   使用「資產選擇器」，您可以輸入關鍵字並選取&#x200B;**[!UICONTROL 退貨]**&#x200B;來搜尋資產。 您也可以套用篩選條件來調整搜尋結果。您可以依路徑、系列、檔案類型和標籤來篩選。選取篩選，然後在工具列中選取&#x200B;**[!UICONTROL 篩選]**&#x200B;圖示。 選取[檢視]圖示並選取&#x200B;**[!UICONTROL 資料行檢視]**、**[!UICONTROL 卡片檢視]**&#x200B;或&#x200B;**[!UICONTROL 清單檢視]**，以變更檢視。

   如需詳細資訊，請參閱[使用選取器](/help/assets/dynamic-media/working-with-selectors.md)。

1. 繼續新增投影片，直到在轉盤集內新增所有要旋轉的影像為止。
1. (選用) 執行以下任一操作：

   * 如有必要，請拖曳投影片以重新排序集合清單中的影像。
   * 若要刪除影像，請選取影像，然後在工具列中選取&#x200B;**[!UICONTROL 刪除投影片]**。

   * 若要套用預設集，在頁面右上角附近，選取預設集下拉式清單，然後選取要一次套用至預設集的預設集。

   若要刪除幻燈片，請選取幻燈片。 在工具列上，選取工具列上的&#x200B;**[!UICONTROL 刪除投影片]**。 若要移動投影片，請選取重新排序圖示並移至所需位置。

1. 在幻燈片中新增影像後，您可以在影像中新增熱點、影像地圖或兩者。 請參閱[將熱點或影像地圖新增至影像橫幅](#adding-hotspots-or-image-maps-to-an-image-banner)。
1. 您可以變更轉盤集的視覺設計和行為。 若要調整轉盤橫幅的顯示方式或特定元件的行為，請選取&#x200B;**[!UICONTROL 行為]**&#x200B;和&#x200B;**[!UICONTROL 外觀]**&#x200B;標籤。 如需如何使用檢視器編輯器的詳細資訊，請參閱[管理檢視器預設集](/help/assets/dynamic-media/viewer-presets.md)。

   >[!NOTE]
   >
   >對於輪播橫幅，您可以調整下列專案：
   >
   >* 影像顯示的持續時間。 依預設，每個影像會顯示9秒。
   >* 動畫。 依預設，每個幻燈片切換都是淡化。 您可以將其變更為幻燈片切換。
   >* 按鈕的樣式。 使用者可以選取每個點或數字，旋轉橫幅。 您可以變更設定指示器按鈕出現的位置（如果是數值或虛線樣式），以及大小。
   >* 變更影像地圖的醒目提示樣式或用於連結區的圖示。
   >* 編輯檢視器預設集之前，請先選擇要作為預設集基礎的樣式。 如果您未選擇樣式，當您開始編輯檢視器預設集時，如果您變更為其他預設集，則會遺失所有變更。

   您也可以預覽轉盤橫幅的外觀。 請參閱[&#x200B; （選擇性）預覽轉盤橫幅](#optional-previewing-carousel-banners)。

1. 完成時選取&#x200B;**[!UICONTROL 儲存]**。

## 將熱點或影像地圖新增至影像橫幅 {#adding-hotspots-or-image-maps-to-an-image-banner}

您可以使用轉盤集編輯器，將熱點或影像地圖新增至橫幅。

當您新增熱點或影像地圖時，可以將它們定義為快速檢視快顯顯示、超連結或體驗片段。

請參閱[體驗片段](/help/sites-cloud/authoring/fragments/content-fragments.md)。

>[!NOTE]
>
>將檢視器嵌入體驗片段時，不支援轉盤橫幅中的社群媒體分享工具。
>
>若要解決此問題，您可以使用或建立沒有社群媒體分享工具的檢視器預設集。 這類檢視器預設集可讓您成功將其嵌入體驗片段中。

將熱點或影像地圖新增至影像時，請記得儲存作業。 在您目前的建立/編輯作業階段期間，支援頁面右上角附近的「復原」和「重做」選項。

當您完成建立轉盤橫幅時，可以選擇性使用預覽，檢視轉盤橫幅向客戶呈現的呈現方式。

請參閱[&#x200B; （選擇性）預覽轉盤橫幅](#optional-previewing-carousel-banners)。

>[!NOTE]
>
>當您將熱點新增至影像橫幅時，熱點資訊會儲存在相同的中繼資料位置（相對於影像的位置）。 無論是否為互動式影像或輪播橫幅，這點皆為正確。 這項功能表示您可以在任一檢視器中輕鬆重複使用相同的影像，以及其定義的熱點資料。
>
>但是請注意，轉盤橫幅支援也可能包含熱點的影像上的影像地圖，互動式影像則否。 如果您打算建立使用相同影像的互動式影像或轉盤橫幅，請記住此秘訣。 請考慮改用相同影像的個別復本來建立互動式影像和輪播橫幅。

>[!NOTE]
>
>如果您使用熱點編輯互動式影像並裁切影像，則會移除您的熱點。

<!-- See also [Adding Image Maps](/help/assets/image-maps.md). -->

**若要新增熱點或影像地圖至影像橫幅：**

1. 在Assets中，導覽至您想要產生互動式的轉盤集。
1. 選取輪播集並選取&#x200B;**[!UICONTROL 編輯]**。 「轉盤檢視器編輯器」隨即開啟。
1. 選取您要讓幻燈片互動的幻燈片。
1. 在頁面的左上角附近，選取&#x200B;**[!UICONTROL 熱點]**&#x200B;或&#x200B;**[!UICONTROL 影像地圖]**。
1. 執行下列任一項作業：

   * 連結區：在影像上，選取您要顯示連結區的位置。
   * 針對影像地圖：在影像上，從左上角拖曳至右下角以建立影像地圖區域。 您可以拖曳邊角來調整影像地圖的大小。

   如有必要，請將熱點或影像地圖拖曳到新位置。 或者，使用鍵盤方向鍵來控制所選連結區的位置。 視需要新增更多熱點或影像地圖。

   若要刪除熱點或影像地圖，請選取&#x200B;**[!UICONTROL 動作]**&#x200B;標籤。 在&#x200B;**[!UICONTROL 地圖與熱點]**&#x200B;標題下，從&#x200B;**[!UICONTROL 選取的型別]**&#x200B;下拉式清單中，選取您要移除的熱點或影像對映的名稱。 選取功能表旁的&#x200B;**[!UICONTROL 垃圾桶]**&#x200B;圖示，然後選取&#x200B;**[!UICONTROL 刪除]**。

1. 在「名稱」文字欄位中，輸入熱點或影像對映的名稱。 此名稱也會出現在&#x200B;**[!UICONTROL 地圖與熱點]**&#x200B;下拉式清單中。 提供名稱可讓您日後決定變更熱點或影像地圖時，輕鬆識別熱點或影像地圖。
1. 在&#x200B;**[!UICONTROL 動作]**&#x200B;索引標籤中執行下列任一項動作：

   * 選取&#x200B;**[!UICONTROL 快速檢視]**。

      * 如果您是Experience Manager Sites <!-- and Ecommerce-->客戶，請選取「產品挑選器」圖示（放大鏡）以開啟「選取產品」頁面。 若要返回「轉盤橫幅編輯器」，請選取您要使用的產品，然後選取頁面右上角的核取記號。
      * 如果您不是Experience Manager Sites <!-- or Ecommerce -->客戶：

         * 定義變數。 請參閱[識別熱點變數](#identifying-hotspot-and-image-map-variables)。
         * 然後，手動輸入SKU值。 在「SKU值」文字欄位中，輸入產品的SKU （庫存單位），這是您提供的每個不同產品或服務的唯一識別碼。 輸入的SKU值會自動填入快速檢視範本的變數部分。 系統現在知道要將選取的熱點與特定SKU的快速檢視建立關聯。
         * （選擇性）如果快速檢視中有其他變數您必須用來進一步識別產品，請選取&#x200B;**[!UICONTROL 新增一般變數]**。 在文字欄位中，指定額外的變數。 例如， category=Mens是新增的變數。

         * 如需詳細資訊，請參閱[使用選取器](/help/assets/dynamic-media/working-with-selectors.md)。

   * 選取&#x200B;**[!UICONTROL 超連結]**。

      * 如果您是Experience Manager Sites客戶，請選取「網站選擇器」圖示（資料夾）以導覽至URL。

        >[!NOTE]
        >
        >如果您的互動式內容有具有相對URL的連結，尤其是指向Experience Manager Sites頁面的連結，則無法採用URL型連結方法。

      * 如果您是獨立客戶，請在href文字欄位中指定連結網頁的完整URL路徑。

   請務必指定要在新的瀏覽器分頁（建議的預設值）或相同的分頁中開啟連結。

   如需詳細資訊，請參閱[使用選取器](/help/assets/dynamic-media/working-with-selectors.md)。

   * 選取&#x200B;**[!UICONTROL 體驗片段]**。

      * 如果您是Experience Manager Sites客戶，請選取「搜尋」圖示（放大鏡）以開啟「體驗片段」頁面。 若要返回熱點管理頁面，請選取您要使用的體驗片段，然後在頁面的右上角，選取&#x200B;**[!UICONTROL 選取]**。
請參閱[體驗片段](/help/sites-cloud/authoring/fragments/content-fragments.md)。

      * 指定體驗片段在橫幅上顯示的寬度和高度。

        >[!NOTE]
        >
        >將檢視器嵌入體驗片段時，不支援轉盤橫幅中的社群媒體分享工具。
        >
        >若要解決此問題，您可以使用或建立沒有社群媒體分享工具的檢視器預設集。 這類檢視器預設集可讓您成功將其嵌入體驗片段中。

   ![experience_fragment-carouselbanner](assets/experience_fragment-carouselbanner.png)

   您也可以預覽轉盤橫幅的外觀。 請參閱[&#x200B; （選擇性）預覽轉盤橫幅](#optional-previewing-carousel-banners)。

1. 選取「**[!UICONTROL 儲存]**」。
1. 發佈轉盤集。 發佈作業會建立可在網站頁面上使用的內嵌程式碼或URL。 如果您是Experience Manager Sites客戶，請直接將輪播集新增至您的網頁。

   請參閱[發佈資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

   請參閱[將轉盤集新增至您的網站登陸頁面](#adding-a-carousel-banner-to-your-website-page)

## 編輯轉盤集 {#editing-carousel-sets}

>[!NOTE]
>
>必須將非管理使用者新增到&#x200B;**[!UICONTROL dam-users]**&#x200B;群組，才能建立或編輯輪播橫幅。 如果您在建立或編輯時遇到問題，請洽詢系統管理員，以便將您新增至&#x200B;**[!UICONTROL dam-users]**&#x200B;群組。

您可以對轉盤集執行各種編輯任務，如下所示：

* 將幻燈片新增至輪播集。 另請參閱[使用選取器](/help/assets/dynamic-media/working-with-selectors.md)。
* 重新排序轉盤集中的幻燈片。
* 刪除轉盤集中的資產。
* 套用檢視器預設集。
* 刪除轉盤集。
* 新增或編輯熱點及影像地圖。 另請參閱[使用選取器](/help/assets/dynamic-media/working-with-selectors.md)。

**若要編輯轉盤集：**

1. 執行下列任一項作業：

   * 將游標暫留在轉盤集資產上，然後選取「**[!UICONTROL 編輯]**」（鉛筆圖示）。
   * 將游標暫留在轉盤集資產上，選取&#x200B;**[!UICONTROL 選取]** （勾選圖示），然後在工具列上選取&#x200B;**[!UICONTROL 編輯]**。

   * 選取轉盤集資產，然後在頁面的左上角選取&#x200B;**[!UICONTROL 編輯]** （鉛筆圖示）。

1. 若要編輯轉盤集，請執行下列任一項作業：

   * 若要新增幻燈片，請選取&#x200B;**[!UICONTROL 新增幻燈片]**&#x200B;圖示。 導覽至您要新增至該幻燈片的資產，然後選取核取標籤。
   * 若要重新排列投影片，請將投影片拖曳至新的位置（選取重新排列圖示以移動專案）。
   * 若要新增熱點或影像地圖，請選取熱點或影像地圖圖示，並參閱[新增熱點和影像地圖至影像橫幅](#adding-hotspots-or-image-maps-to-an-image-banner)。
   * 若要編輯轉盤集的外觀或行為，請選取&#x200B;**[!UICONTROL 外觀]**&#x200B;索引標籤或&#x200B;**[!UICONTROL 行為]**&#x200B;索引標籤，然後設定您想要的選項。
   * 若要編輯熱點或影像地圖，請在適當的幻燈片上選取熱點或影像地圖。 在&#x200B;**[!UICONTROL 動作]**&#x200B;標籤下，進行變更。
   * 若要刪除投影片，請選取該投影片，然後在工具列中選取&#x200B;**[!UICONTROL 刪除投影片]**。
   * 若要套用預設集，在頁面右上角附近，選取&#x200B;**[!UICONTROL 預設集]**&#x200B;下拉式清單，然後選取檢視器預設集。
   * 若要刪除整個轉盤集，請導覽至轉盤集，選取該轉盤集，然後選取&#x200B;**[!UICONTROL 刪除]**。

   >[!NOTE]
   >
   >如果您使用熱點編輯互動式影像並裁切影像，則會移除您的熱點。

## （選用）預覽轉盤橫幅 {#optional-previewing-carousel-banners}

您可以使用「預覽」來檢視傳送橫幅給客戶的顯示方式。 使用預覽也可讓您測試轉盤橫幅的熱點和影像地圖，以確保它們如預期般運作。

當您對輪播橫幅感到滿意時，可以將其發佈。
請參閱[將視訊或影像檢視器嵌入網頁](/help/assets/dynamic-media/embed-code.md)。
檢視[將URL連結至您的網頁應用程式](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)。 如果您的互動式內容有具有相對URL的連結，尤其是指向Experience Manager Sites頁面的連結，則無法採用URL型連結方法。
請參閱[將Dynamic Media Assets新增至頁面](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)。

您可以從轉盤編輯器（偏好方法）或&#x200B;**[!UICONTROL 檢視器]**&#x200B;清單預覽轉盤橫幅。

**若要選擇性預覽轉盤橫幅：**

1. 在&#x200B;**[!UICONTROL Assets]**&#x200B;中，導覽至您已建立的現有轉盤橫幅，並選取以開啟。
1. 選取&#x200B;**[!UICONTROL 編輯]**。
1. 在工具列右角的檢視器預設集清單中，選取檢視器以預覽輪播橫幅。

   ![experience_fragment-carouselbanner-viewerdropdown](assets/experience_fragment-carouselbanner-viewerdropdown.png)

1. 選取&#x200B;**[!UICONTROL 預覽]**。
1. 若要測試其相關動作，請選取影像上的熱點或影像地圖。

**若要從檢視器清單預覽輪播橫幅：**

1. 在&#x200B;**[!UICONTROL Assets]**&#x200B;中，導覽至您已建立的現有轉盤橫幅，並選取以開啟。
1. 在「預覽」頁面的左上角附近，選取「內容」圖示。
1. 在頁面左側面板中的&#x200B;**[!UICONTROL 檢視器]**&#x200B;清單中，選取您要使用的輪播橫幅檢視器預設集名稱。
1. 若要測試其相關動作，請選取影像上的熱點或影像地圖。

## 發佈輪播橫幅 {#publishing-carousel-banners}

若要使用輪播，您必須將其發佈。 發佈轉盤集時會啟用URL和內嵌程式碼。 它也會將轉盤發佈至Dynamic Media雲端，此雲端已與CDN整合，以便提供可擴充且高效能的傳送方式。

>[!NOTE]
>
>如果您使用具有傳送橫幅之熱點的現有互動式影像，則必須在發佈傳送橫幅後個別發佈互動式影像。
>
>此外，如果您修改轉盤橫幅中預先存在的已發佈互動影像，請發佈互動影像，以便這些變更會反映在轉盤橫幅中。

如需如何發佈轉盤橫幅的詳細資訊，請參閱[發佈Dynamic Media Assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

## 將輪播橫幅新增至您的網站頁面 {#adding-a-carousel-banner-to-your-website-page}

上傳橫幅影像以建立轉盤後，新增熱點或影像地圖（或兩者）至橫幅。 已發佈傳送集。 您現在已準備好將其新增到您現有的網站頁面。

>[!NOTE]
>
>如果您是Experience Manager Sites客戶，可以將互動媒體元件拖曳至頁面，直接將輪播橫幅新增至頁面。 請參閱[將Dynamic Media Assets新增至頁面](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)。

不過，如果您是獨立的Experience Manager Assets客戶，可以手動將輪播橫幅新增至您的網站登陸頁面。

1. 複製已發佈轉盤集的內嵌程式碼。
請參閱[將視訊或影像檢視器嵌入網頁](/help/assets/dynamic-media/embed-code.md)。

1. 將您從Experience Manager Assets複製的內嵌程式碼新增至網頁。
複製的內嵌程式碼會回應，因此會自動符合頁面的內嵌區域。

## 將輪播橫幅與現有的快速檢視整合 {#integrating-the-carousel-banner-with-an-existing-quickview}

注意：此步驟僅適用於獨立Experience Manager Assets客戶。

此程式的最後一步是將轉盤橫幅與網站上現有的快速檢視實作整合。 每個快速檢視實作都是獨一無二，而且需要特定方法，通常需要前端IT人員的協助。

現有的快速檢視實施通常代表一連串在網頁上發生的相互關聯動作，其順序如下：

1. 使用者會在您網站的使用者介面中觸發元素。
1. 前端程式碼會根據步驟1所觸發的使用者介面元素來取得快速檢視URL。
1. 前端程式碼會使用在步驟2中取得的URL傳送Ajax要求。
1. 後端邏輯會將對應的快速檢視資料或內容傳回前端程式碼。
1. 前端程式碼會載入快速檢視資料或內容。
1. 前端程式碼可選擇性將載入的快速檢視資料轉換為HTML呈現。
1. 前端程式碼會顯示模型對話方塊或面板，並在畫面上為使用者呈現HTML內容。

這些呼叫不代表網頁邏輯可從任意步驟呼叫的獨立公用API呼叫。 相反地，這是一種鏈結呼叫，下個步驟的每一個都會隱藏在上一個步驟的最後一個階段（回撥）。

在輪播橫幅取代步驟1和部分步驟2的同時，當使用者選取熱點或影像地圖時，此類互動由檢視器處理。 檢視器會將事件傳回至包含先前新增之所有熱點或影像地圖資料的網頁。

在此類事件處理常式中，前端程式碼會執行下列動作：

* 聆聽轉盤橫幅所發出的事件。
* 根據熱點或影像地圖資料建構快速檢視URL。
* 觸發從後端載入快速檢視並在畫面上呈現以供顯示的程式。

Experience Manager Assets傳回的內嵌程式碼已備有備註的現成事件處理常式。

因此，只需取消註解程式碼，並將虛擬處理常式本文取代為特定網頁專用的程式碼。

建構快速檢視URL的程式與用來識別先前涵蓋的熱點和影像地圖變數的程式相反。

請參閱[識別熱點和影像對映變數](#identifying-hotspot-and-image-map-variables)。

觸發快速檢視URL及啟動快速檢視面板的最後一個步驟，極有可能需要您IT部門的前端IT人員協助。 他們深知如何透過適當的步驟準確觸發快速檢視實施，並擁有現成的快速檢視URL。

## 使用Quickview建立自訂快顯視窗® {#using-quickviews-to-create-custom-pop-ups}

請參閱[使用Quickview建立自訂快顯視窗®](/help/assets/dynamic-media/custom-pop-ups.md)。
