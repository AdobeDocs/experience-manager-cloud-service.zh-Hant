---
title: 互動式影像
description: 瞭解如何在Dynamic Media使用互動式影像。
feature: 互動影像
topic: 業務從業人員
role: Business Practitioner
exl-id: 89eef5e6-d508-4f33-b54e-24d4df49f8c3
translation-type: tm+mt
source-git-commit: 6b232ab512a6faaf075faa55c238dfb10c00b100
workflow-type: tm+mt
source-wordcount: '4249'
ht-degree: 1%

---

# 互動式影像{#interactive-images}

將「可購買」的熱點拖放至影像上，即可輕鬆為客戶製作豐富、吸引人的靜態影像。 可購物熱點結合了有關產品或服務的其他資訊以及直接、銷售點「新增至購物車」或「購買」功能。 客戶可以點選這些直接連結至產品或服務的熱點、將其新增至購物車，或連結至網頁。 此類直接體驗可提高客戶在網站上的參與度和轉化率。

以下是具有「快速檢視」快顯視窗的可購物橫幅。 用戶通過點選模型上的圓或「熱點」來激活「快速」視圖。

![chlimage_1-152](assets/chlimage_1-368.png)

請參閱上圖所示網頁上的[互動式影像實際運作](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html)。

## 觀看互動式影像橫幅的建立方式{#watch-how-interactive-image-banners-are-created}

觀看[如何建立互動式影像橫幅的10分鐘33秒逐步說明](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner)。 您也會學習如何預覽、編輯和傳遞互動式影像橫幅。

## 快速入門：互動式影像{#quick-start-interactive-images}

下列逐步工作流程說明旨在協助您在AEM Assets快速上手使用互動式影像。

在某些快速入門任務中查找&#x200B;**Example**&#x200B;標題。 它包含以[網頁範例為基礎的簡短教學課程，該範例尚未新增互動式影像至](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html)。



本教學課程可協助您說明將互動式影像整合在您自己的網站上的步驟。

互動式影像步驟：

1. **（可選）識別熱點變數**。如果您使用Adobe Experience Manager資產和Dynamic Media獨立版，請識別用於現有快速檢視實作的動態變數。 如此可確保在建立互動式影像時輸入熱點資料。 請參閱[（可選）識別熱點變數](#optional-identifying-hotspot-variables)。
不過，如果您使用AEM Sites或AEM電子商務或兩者，則不需要此步驟。

1. **（可選）建立互動式影像檢視器預設集**。自訂用於表示熱點的圖形影像。 如果您想要改用名為`Shoppable_Banner`的現成可用的互動式影像檢視器預設集，則不需要建立您自己的互動式影像檢視器預設集。
請參閱[（可選）建立互動式影像檢視器預設集](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset)。

1. **上傳影像橫幅**。上傳您要製作互動式影像橫幅。
請參閱[上傳影像橫幅](#uploading-an-image-banner)。

1. **將熱點添加到影像橫幅**。將一個或多個熱點添加到影像橫幅。 將每個動作與超連結、快速檢視或體驗片段等動作產生關聯。 添加熱點後，將通過發佈互動式影像完成此任務。
請參閱[將熱點添加到影像橫幅](#adding-hotspots-to-an-image-banner)。
請參閱[預覽互動式影像](#optional-previewing-interactive-images) —— 選用。 視需要，您可以檢視可購買橫幅的呈現方式，並測試其互動性。
如需如何發佈互動式影像資產的詳細資訊，請參閱[發佈資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

1. **將互動式影像新增至您的網站或以Experience Manager新增至網站**。如果您使用網站、電子商務或兩者，則可直接將互動影像新增至Experience Manager的網頁。 將互動式媒體元件拖曳至頁面上。 請參閱[將Dynamic Media資產新增至Pages](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)。
如果您單獨使用Experience Manager資產和Dynamic Media，請複製網站上的內嵌代碼。 然後，將它與您現有的快速檢視整合。 請參閱[整合互動式影像與您的網站](#integrating-an-interactive-image-with-your-website)。
如果您使用協力廠商的WCM(Web Content Manager)，請將新的互動式視訊與網站上使用的現有快速檢視整合。 請參閱[整合互動式影像與現有的快速檢視](#integrating-an-interactive-image-with-an-existing-quickview)。

## （可選）識別熱點變數{#optional-identifying-hotspot-variables}

>[!NOTE]
>
>只有在以下情況下，才需要此任務：
>
>* 您想要透過觸發至快速檢視，將互動功能加入影像。
>* 您的Experience Manager實作&#x200B;*not*&#x200B;會使用電子商務整合架構，從任何電子商務解決方案將產品資料拉入Experience Manager。 此類解決方案包括IBM WebSphere® Commerce、Elastic Path、hybris或Intershop。

>
>
如果您的實AEM作使用電子商務，您可以略過此工作，繼續下一個工作。

首先，識別您現有快速檢視實作所使用的動態變數，以便輸入熱點資料以建立互動式影像。

在「Experience Manager資產」中將熱點新增至橫幅影像時，請指派SKU（庫存保留單位）。 SKU是您提供之每個不同產品或服務的唯一識別碼。 此外，還可新增任何額外的可選變數至每個熱點。 這些熱點變數稍後會用來比對熱點與快速檢視內容。

請務必正確識別要與熱點資料關聯的變數數目和類型。 每個新增至橫幅影像的熱點都必須包含足夠的資訊，以明確識別現有後端系統中的產品。

有不同的方法可識別一組要用於熱點資料的變數。

有時，與負責現有快速檢視實作的IT專家諮詢就夠了。 這些人可能知道在系統中識別「快速檢視」所需的最低資料集。 不過，您也可以簡單分析前端程式碼的現有行為。

大部分的快速檢視實作都採用下列範例：

* 使用者在網站上啟動使用者介面元素。例如，按一下「快速檢視」按鈕。
* 如有需要，網站會傳送Ajax要求至後端以載入快速檢視資料或內容。
* 快速檢視資料會轉譯為內容，以準備在網頁上轉譯。
* 最後，前端程式碼會以視覺化方式在螢幕上呈現此類內容。

然後，方法是造訪實施快速檢視功能的現有網站的不同區域。 然後觸發快速檢視並擷取網頁所傳送的Ajax URL，以載入快速檢視資料或內容。

通常您不需使用任何專用的除錯工具。 現代網頁瀏覽器採用Web檢視器，可讓您完成適當的工作。 以下是包含Web檢視程式的Web瀏覽器範例：

* 若要在Google Chrome中查看所有傳出的HTTP要求，請按F12以開啟「開發人員工具」面板，然後按一下「網路」標籤。
在Mac上，按Command+Option+I以開啟「開發人員工具」面板，然後按一下「網路」標籤。

* 在Firefox中，您可以按F12並使用其網頁標籤來啟動Firebug外掛程式。 或者，您也可以使用內建的「檢查器」工具及其「網路」頁籤。
在Mac上，按Command+Option+I以開啟「開發人員工具」面板，然後按一下「偵測器」標籤。

在瀏覽器中開啟網路監視時，觸發頁面上的快速檢視。

現在，在網路記錄檔中尋找快速檢視Ajax URL，並複製已記錄的URL以供日後分析。 通常當您觸發快速檢視時，會有許多要求傳送至伺服器。 通常，快速檢視Ajax URL是清單中第一個檢視的URL。 它有複雜的查詢字串部分或路徑，其回應MIME類型為`text/html`、`text/xml`或`text/javascript`。

在此程式中，請務必造訪您網站的不同區域，以及不同的產品類別和類型。 原因是快速檢視URL可能包含特定網站類別的常用部分。 不過，只有當您造訪網站的不同區域時，這些變數才會變更。

在最簡單的情況下，「快速檢視URL」中唯一的變數部分是產品SKU。 在這種情況下，SKU值是您在橫幅影像中新增熱點所需的唯一資料片段。

但是，在複雜情況下，快速檢視URL除了SKU以外，還有不同的元素。 例如，變更的元素可能包括類別ID、顏色代碼和大小代碼。 在這種情況下，每個元素都是Experience Manager資產中可購物互動影像功能中熱點資料定義中的個別變數。

請考慮下列快速檢視URL的範例及其產生的熱點變數：

<table>
  <tbody>
  <tr>
    <td><p>單一SKU，可在查詢字串中找到。</p> </td>
    <td><p>錄制的快速檢視URL包括：</p>
    <ul>
      <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>URL中唯一的變數部分是productId=查詢字串參數的值，而它顯然是SKU值。 因此，熱點只需要填入<strong><code>866558</code></strong>、<strong><code>1196184</code></strong>、<strong><code>1081492</code></strong>、<strong><code>1898294</code></strong>等值的SKU欄位。</p> </td>
  </tr>
  <tr>
    <td><p>單一SKU，位於URL路徑中。</p> </td>
    <td><p>錄制的快速檢視URL包括：</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>變數部分位於路徑的最後一部分，並成為熱點的SKU值：<strong><code>6422350843</code></strong>、<strong><code>1607745002</code></strong>、<strong><code>0086724882</code></strong>。</p> </td>
  </tr>
  <tr>
    <td><p>查詢字串中的SKU和類別ID。</p> </td>
    <td><p>錄制的快速檢視URL包括：</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>在此例中，URL中有兩個不同的部分。 SKU儲存在<code>prodId</code>參數中，類別ID<code></code>儲存在<code>category=</code>參數中。</p> <p>因此，熱點定義是對。 即SKU值和名為<code>categoryId</code>的額外變數。 產生的對如下：</p>
    <ul>
      <li><p>SKU為<strong><code>305466</code></strong>,<code>categoryId</code>為<code>1100004</code>。</p> </li>
      <li><p>SKU為<strong><code>310181</code></strong>,<code>categoryId</code>為<strong><code>1100004</code></strong>。</p> </li>
      <li><p>SKU為<strong><code>308706</code></strong>,<code>categoryId</code>為<strong><code>1740148</code></strong>。</p> </li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**範例**

您可以將上述三個範例中使用的相同方法套用至[示範網頁](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html)。

示範網頁包含數個產品縮圖，每個產品縮圖都有標示為「檢視更多」的「快速檢視」按鈕。 在您網頁瀏覽器的除錯工具仍處於啟用狀態時，按一下每個按鈕並記下錄制的快速檢視URL。 在您啟動頁面上所有4種產品快速檢視後，您會有下列對後端提出的快速檢視要求清單：

* `/datafeed/Men-Windbreaker.json`
* `/datafeed/Men-SimpleHenley.json`
* `/datafeed/Men-CamoPullover.json`
* `/datafeed/Women-QuiltedDownJacket.json`

檢視伺服器呼叫，您可以看到產品特定資訊只存在於請求路徑中。 您也注意到查詢字串完全未使用，並且涉及兩種不同的資料片段類型：

* 第一種是「男」或「女」。 您可以將此稱為「產品類別」。
* 第二種類型是產品名稱，例如CamoPullover，可能是產品SKU。

有了這些資訊，整個快速檢視URL會有下列模式：

`/datafeed/$categoryId$-$SKU$.json`

基於此類分析，您應使用`categoryId`和`SKU`作為熱點。

您現在可以使用AEM Assets的可購買互動影像功能，上傳影像橫幅並新增熱點。

## （可選）建立互動式影像檢視器預設集{#optional-creating-an-interactive-image-viewer-preset}

您可以選擇使用隨附於AEM Assets的預設、現成可用的互動式影像檢視器預設集，稱為`Shoppable_Banner`。 或者，您也可以建立您自己的自訂檢視器預設集，以便用於互動式影像。

當您建立自訂的互動式影像檢視器預設集時，可以決定影像橫幅上熱點的外觀。 在建立檢視器預設集時，您可以選擇使用預先定義影像收藏館中的熱點圖形。

儲存檢視器預設集後，它會自動在AEM Assets的「檢視器預設集」清單頁面上啟動（開啟）。 此功能表示它可在互動式媒體元件中顯示，且在您檢視資產時也可顯示。 不過，若要使用此檢視器預設集傳送&#x200B;*互動式橫幅，* publish *您的檢視器預設集。*&#x200B;此規則適用於自訂或現成可用的檢視器預設集。

**若要建立互動式影像檢視器預設集**

1. 在左側導軌中，點選「**[!UICONTROL 工具>資產>檢視器預設集]**」。
1. 在頁面的右上角附近，點選&#x200B;**[!UICONTROL Create]**。
1. 在「新建檢視器預設集」對話方塊中，輸入名稱以說明互動式橫幅檢視器預設集。

   儲存後，此標題會出現在「檢視器預設集」清單頁面中。

1. 在「豐富型媒體類型」下拉式功能表中，選取「互動 **[!UICONTROL 式影像」]**。
1. 點選&#x200B;**[!UICONTROL Create]**。
1. 在「編輯檢視器預設集」頁面上，點選「**[!UICONTROL 外觀]**」標籤。
1. 執行下列任一項作業：

   * 若要上傳您要用於影像的自己熱點影像，請點選「資產選擇器」圖示。 在「選擇內容」頁中，導航到要使用的熱點影像並選擇它。 點選右上角的「勾選標籤」圖示。
   * 若要選取預先定義的熱點影像，請點選「熱點圖庫」圖示。 在熱點圖庫浮動視窗上，點選您要使用的熱點影像。

1. 在頁面的右上角附近，點選&#x200B;**[!UICONTROL Save]**。

   請確定您已發佈新的檢視器預設集。

   請參閱[Publishing Viewer Presets](/help/assets/dynamic-media/managing-viewer-presets.md#publishing-viewer-presets)。

   您現在已準備好上傳影像橫幅。

## 上傳影像橫幅{#uploading-an-image-banner}

如果您已上傳您要使用的影像，請進入下一步[「新增熱點至影像橫幅](#adding-hotspots-to-an-image-banner)」。

**若要上傳影像橫幅**

1. 上傳您要製作互動式影像橫幅。

   請參閱[上傳資產](/help/assets/manage-digital-assets.md#uploading-assets)。

   您現在可以在影像橫幅中加入熱點；請參閱下面的下一項工作。

## 將熱點添加到影像橫幅{#adding-hotspots-to-an-image-banner}

您可以使用「熱點管理」頁上的編輯器將熱點添加到影像橫幅。

新增熱點時，您可將其定義為「快速檢視」快顯顯示、超連結或「體驗片段」。

請參閱[體驗片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)。

>[!NOTE]
>
>當您將檢視器內嵌在體驗片段時，不支援互動式影像中的社交媒體分享工具。 請改用或建立沒有社交媒體分享工具的檢視器預設集。 這些檢視器預設集可讓您成功將它內嵌在「體驗片段」中。

在目前的建立／編輯作業階段中，支援在頁面右上角的「復原」和「重做」選項。

當您完成互動影像的建立後，您可以使用「預覽」來呈現您的互動影像對客戶的呈現方式。

請參閱[（可選）預覽互動式影像](#optional-previewing-interactive-images)。

>[!NOTE]
>
>當您在「互動式影像」或「轉盤橫幅」中新增熱點至影像時，熱點資訊會儲存在相同的中繼資料位置。 此位置是相對於影像的位置，不論是互動式影像或轉盤橫幅。 這項功能表示，您可以在任一檢視器中，輕鬆地重複使用相同的影像及其定義的熱點資料。
但是，請注意，轉盤橫幅支援影像上的影像地圖，這些影像也可能包含熱點；互動式影像則否。 如果您想要建立使用相同影像的互動式影像或轉盤橫幅，請記住這個想法。 您可以改用相同影像的個別復本來建立互動式影像和轉盤橫幅。
另請參閱[轉盤橫幅](/help/assets/dynamic-media/carousel-banners.md)。

>[!NOTE]
如果您正在編輯具有熱點的互動式影像並裁剪影像，則會刪除熱點。

**向影像橫幅添加熱點**

1. 在「資產」檢視中，導覽至您要建立互動功能的影像橫幅。
1. 執行下列任一項作業：

   * 將滑鼠指標暫留在影像上，然後點選&#x200B;**[!UICONTROL 選擇]**（勾選圖示）。 在工具列上，點選&#x200B;**[!UICONTROL 編輯]**。

   * 將滑鼠指標暫留在影像上，然後點選「更多動作」]**（三點圖示）**[!UICONTROL >「編輯」]**。**[!UICONTROL 

   * 若要在「詳細資料檢視」頁面中開啟影像，請點選影像。 在工具列中，點選&#x200B;**[!UICONTROL 編輯]**。

1. 在頁面的左上角附近，點選「新增熱點」( **[!UICONTROL 手指點選圖示]** )以開啟「熱點」管理頁面。
1. 在頁面的左上角附近，點選&#x200B;**[!UICONTROL 熱點]**。

   1. 在「熱點管理」頁的左上角附近，按一下&#x200B;**[!UICONTROL 熱點]**。
   1. 在影像上，點選您要熱點出現的位置。如有必要，請拖動熱點以調整其位置。或者，使用鍵盤箭頭鍵控制所選熱點的位置。
   1. 通過重複步驟a和b，根據需要添加更多熱點。
   1. （可選）若要刪除熱點，請在影像上選取它，然後點選&#x200B;**[!UICONTROL 熱點]**&#x200B;標題下的&#x200B;**[!UICONTROL 刪除]**（垃圾筒圖示）。

1. 在「名稱」文本欄位中，鍵入熱點的名稱。 此名稱也會出現在「選定熱點」下拉清單中。
1. 執行下列任一項作業：

   * 點選&#x200B;**[!UICONTROL 快速檢視]**。

      * 如果您是AEM Sites或電子商務客戶，請點選或按一下「產品選擇器」圖示（放大鏡）以開啟「選擇產品」頁面。 點選您要使用的產品，然後點選頁面右上角的&#x200B;**Select**。 您將返回熱點管理頁。
      * 如果您&#x200B;*not*&#x200B;是Experience Manager網站或電子商務客戶

         * 請參閱[識別熱點變數](#optional-identifying-hotspot-variables);您必須定義這些變數。
         * 然後，手動輸入SKU值。 在「SKU值」文字欄位中，輸入產品的SKU。 輸入的SKU值會自動填入「快速檢視」範本的變數部分。 它可確保系統知道將點選熱點與特定SKU的「快速」檢視建立關聯。
         * （可選）如果快速檢視中有其他變數可用來進一步識別產品，請點選&#x200B;**[!UICONTROL 新增一般變數]**。 在文字欄位中，指定額外的變數。 例如，`category=Mens`是新增的變數。
   * 點選&#x200B;**[!UICONTROL 超連結]**。

      * 如果您是Experience Manager網站客戶，請點選網站選擇器圖示（資料夾）。 導覽至URL。 如果您的互動式內容具有相對URL的連結，尤其是「Experience Manager網站」頁面的連結，則無法使用以URL為基礎的連結方法。
      * 如果您是獨立客戶，請在HREF文字欄位中，指定連結網頁的完整URL路徑。

   請確定您要指定是在新的瀏覽器標籤（建議預設值）或相同的標籤中開啟連結。

   如需詳細資訊，請參閱[使用選擇器](/help/assets/dynamic-media/working-with-selectors.md)。

   * 點選&#x200B;**[!UICONTROL 體驗片段]**。

      * 如果您是AEM Sites客戶，請點選或按一下「搜尋」圖示（放大鏡）以開啟「體驗片段」頁面。 點選您要使用的體驗片段。 然後點選頁面右上角的&#x200B;**[!UICONTROL Select]**。 您將返回熱點管理頁。
請參閱[體驗片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)。

      * 指定體驗片段在橫幅上顯示的寬度和高度。

         >[!NOTE]
         當您將檢視器內嵌在體驗片段時，不支援互動式影像中的社交媒體分享工具。 請改用或建立沒有社交媒體分享工具的檢視器預設集。 這些檢視器預設集可讓您成功將它內嵌在「體驗片段」中。



1. 點選「**[!UICONTROL 儲存]**」以儲存您的作品並返回「瀏覽頁」。
1. 發佈互動式影像。 發佈會透過雲端傳送橫幅，並產生內嵌代碼，讓您與協力廠商網站整合。

   請參閱[發佈資產](/help/assets/manage-digital-assets.md#publish-assets)。

   新增熱點並發佈互動式影像後，您現在可以將它新增至現有的網站。

   請參閱[整合互動式影像與您的網站](#integrating-an-interactive-image-with-your-website)。

   >[!NOTE]
   如果您正在編輯具有熱點的互動式影像並裁剪影像，則會刪除熱點。

### （選擇性）預覽互動式影像{#optional-previewing-interactive-images}

您可以使用「預覽」來呈現您的互動式影像對客戶的外觀。 預覽功能也可讓您測試影像的熱點，以確保它們如預期般運作。

當您對互動式影像感到滿意時，就可以發佈它。
請參閱[將視訊或影像檢視器內嵌至網頁](/help/assets/dynamic-media/embed-code.md)。
請參閱[將URL連結至您的Web應用程式](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)。 如果您的互動式內容具有相對URL的連結，尤其是連結至AEM Sites頁面，則無法使用以URL為基礎的連結方法。
請參閱[將Dynamic Media資產新增至Pages](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)。

**若要預覽互動式影像**

1. 在「資產」檢視中，導覽至您已建立的現有互動影像，然後點選以在「預覽」中開啟它。
1. 在「預覽」頁面的左上角附近，在「內容」下拉式清單中，點選「檢視器」****。
1. 在「檢視器」清單中，點選&#x200B;**[!UICONTROL Shopbable_Banner]**&#x200B;或您所建立的互動式影像檢視器預設集的名稱。
1. 要測試熱點的相關操作，請在影像上點選熱點。

## 發佈互動式影像資產{#publishing-interactive-image-assets}

如需如何發佈互動式影像資產的詳細資訊，請參閱[發佈資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

## 將互動式影像與您的網站{#integrating-an-interactive-image-with-your-website}整合

上傳橫幅影像、新增熱點並發佈互動式影像後，您就可以將它新增至網站頁面。

如果您是AEM Sites的客戶，可將互動式媒體元件拖曳至頁面上，以新增互動式影像。 請參閱[將Dynamic Media資產新增至Pages](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)。

如果您是獨立的AEM Assets客戶，您可以依本節所述手動將互動式影像新增至您的網站。

1. 複製已發佈的互動式影像的內嵌程式碼。
請參閱[將視訊或影像檢視器內嵌至網頁](/help/assets/dynamic-media/embed-code.md)。

1. 將複製的內嵌程式碼新增至網頁中所需的位置。
複製的嵌入代碼被設定用於響應性環境，以便自動適合所分配的區域。

**範例**

以[示範網站為範例](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html)，請注意，這三個人的圖片是靜態`IMG`標籤：

```xml
<img class="img-responsive" width="100%" title="Hero Image 2" alt="Hero Image 2" src="images/shoppable-banner.jpg">
```

整合就像移除`IMG`標籤，並從AEM Assets以複製的內嵌代碼取代它一樣簡單。 您可以看到結果[顯示頁面上具有三個圓形熱點](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-1.html)的可購物互動影像。

>[!NOTE]
因此，展示網站的可購物互動影像上的熱點僅供顯示之用。 它們尚未與現有的快速檢視整合。

若要針對回應式環境將「裁切」套用至可購買的互動式影像，請將「互動式影像」設定屬性`ZoomView.iscommand`納入路徑。 在這種情況下，會呼叫`ZoomView`元件，而`iscommand`是您套用的「裁切」影像伺服命令。

請參閱[ZoomView.iscommand](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/command-reference-configuration-attributes-interactive-images/r-html5-aem-interactive-image-config-attrib-zoomview-iscommand.html)組態屬性。

請參閱[crop](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-crop.html)影像伺服命令。

您現在可以將互動式影像與網站上現有的快速檢視整合。

## 將互動式影像與現有的快速檢視整合{#integrating-an-interactive-image-with-an-existing-quickview}

>[!NOTE]
此任務僅在您是獨立的AEM Assets客戶時才適用。

此程式的最後一個步驟是將互動式影像與網站上現有的快速檢視實施整合。 沒有適合所有情況的整合解決方案。 每個快速檢視實作都是獨一無二的，而且需要特定的方法。 因此，在前端IT人員的協助下提供協助是有益的。

現有的快速檢視實作通常代表一連串的相關動作，這些動作會依下列順序出現在網頁上：

1. 使用者會在您網站的使用者介面中觸發元素。
1. 前端程式碼會根據步驟1中觸發的使用者介面元素，取得快速檢視URL。
1. 前端程式碼會使用步驟2中取得的URL來傳送Ajax要求。
1. 後端邏輯會將對應的快速檢視資料或內容傳回前端程式碼。
1. 前端程式碼會載入快速檢視資料或內容。
1. 或者，前端程式碼會將載入的快速檢視資料轉換為HTML表示法。
1. 前端程式碼會顯示模式對話方塊或面板，並轉譯HTML內容給使用者。

這些呼叫不一定代表由網頁邏輯從任意步驟呼叫的獨立公用API呼叫。 相反地，它是連結呼叫，在此連結呼叫中，前一個步驟的最後一個階段（回呼）中將隱藏下一個步驟。

當可購物互動影像取代步驟1和部分步驟2時，使用者會在可購物影像中點選熱點。 此類使用者互動由檢視器處理。 檢視器會傳回事件至網頁，其中包含先前新增至AEM Assets的所有熱點資料。

在此類事件處理常式中，前端程式碼會執行下列動作：

* 監聽由可購買互動影像發出的事件。
* 根據熱點資料建構快速檢視URL。
* 觸發從後端載入快速檢視並在螢幕上顯示的程式。

「Experience Manager資產」傳回的內嵌程式碼具有可供使用的事件處理常式，已加上註解，如下列反白顯示的程式碼片段所示：

```xml
        var s7interactiveimageviewer = new s7viewers.InteractiveImage({
            "containerId" : "s7interactiveimage_div",
            "params" : {
                "serverurl" : "https://aodmarketingna.assetsadobe.com/is/image",
                "contenturl" : "https://aodmarketingna.assetsadobe.com/",
                "config" : "/etc/dam/presets/viewer/Shoppable_Media",
                "asset" : "/content/dam/mac/aodmarketingna/shoppable-banner/shoppable-banner.jpg" }
        })
        /* // Example of interactive image event for Quickview.
             s7interactiveimageviewer.setHandlers({
                "quickViewActivate": function(inData) {
                    var sku=inData.sku; //SKU for product ID
                    //To pass other parameter from the hotspot, you will need to add custom parameter during the hotspot setup as parameterName=value
                    loadQuickView(sku); //Replace this call with your Quickview plugin
                    //Please refer to your Quickviewer plugin for the Quickview call
                 },
             });
        */
        s7interactiveimageviewer.init();
```

因此，只需取消程式碼的註解，並以特定網頁專用的程式碼取代虛擬處理常式主體即可。

建立快速檢視URL的程式與用來識別先前涵蓋的熱點變數的程式相反。

請參閱[識別熱點變數](#optional-identifying-hotspot-variables)。

使用先前的快速檢視URL範例，您可在下列範例中查看如何建構快速檢視URL:

<table>
 <tbody>
  <tr>
   <td><p>單一SKU，可在查詢字串中找到</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/json?productId=" + inData.sku + "&amp;amp;source=100";
      },
      });</code></td>
  </tr>
  <tr>
   <td><p>單一SKU，位於URL路徑中</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/product/" + inData.sku;
      },
      });</code></td>
  </tr>
  <tr>
   <td><p>查詢字串中的SKU和類別ID</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;amp;prodId=" + inData.sku;
      },
      });</code></td>
  </tr>
 </tbody>
</table>

觸發快速檢視URL並啟動快速檢視面板的最後一個步驟，需要企業前端IT人員的協助。 他們具備最佳的知識，瞭解如何從正確的步驟精確觸發快速檢視實作，並擁有現成可用的快速檢視URL。

您可以瞭解這些步驟如何套用至示範網站，以便將可購買的互動式影像與快速檢視程式碼完全整合。 之前，快速檢視URL的結構已識別為：

```xml
/datafeed/$categoryId$-$SKU$.json
```

若要在`quickViewActivate`處理常式中重建此URL，您可以使用`categoryId`和`SKU`欄位。 在`inData`物件中，這些欄位可供檢視器程式碼傳遞至處理常式：

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

示範網站會使用簡單的`loadQuickView()`函式呼叫來觸發「快速檢視」對話方塊。 此函式只使用一個引數，即快速檢視資料URL。 因此，整合可購物互動影像的最後一個步驟是將下列程式碼行新增至`quickViewActivate`處理常式：

```xml
loadQuickView(quickViewUrl);
```

以下是完整的原始碼：

```xml
 var s7interactiveimageviewer = new s7viewers.InteractiveImage({
  "containerId" : "s7interactiveimage_div",
  "params" : {
   "serverurl" : "https://aodmarketingna.assetsadobe.com/is/image",
   "contenturl" : "https://aodmarketingna.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Media",
   "asset" : "/content/dam/mac/aodmarketingna/shoppable-banner/shoppable-banner.jpg" }
 })
   s7interactiveimageviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku;
     var categoryId=inData.categoryId;
    var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
    loadQuickView(quickViewUrl);
    },
   });
 s7interactiveimageviewer.init();
```

具備完全整合的互動式影像](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-3.html)的[最終示範網站。

## 使用快速檢視建立自訂快顯視窗{#using-quickviews-to-create-custom-pop-ups}

請參閱[使用快速檢視建立自訂快顯視窗](/help/assets/dynamic-media/custom-pop-ups.md)。
