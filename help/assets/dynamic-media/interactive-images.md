---
title: 互動式影像
description: 瞭解如何使用Dynamic Media的互動式影像。
feature: Interactive Images
role: User
exl-id: 89eef5e6-d508-4f33-b54e-24d4df49f8c3
source-git-commit: 77f1b744dabd72fc26d3b0607db9561e6cb7fa66
workflow-type: tm+mt
source-wordcount: '4176'
ht-degree: 1%

---

# 互動式影像{#interactive-images}

通過將「可購物」熱點拖放到影像上，您可以輕鬆地使靜態影像豐富、吸引客戶。 可購物熱點將有關產品或服務的附加資訊與直接的銷售點「添加到購物車」或「購買」功能結合起來。 客戶可以點擊這些直接連結到產品或服務的熱點、將其添加到購物車或連結到網頁。 直接體驗（如這些）可增加您網站上的客戶參與和轉換。

以下是帶有Quickview彈出窗口的可購買橫幅。 用戶通過在模型上點擊圓或「熱點」來激活Quickview。

![chlimage_1-152](assets/chlimage_1-368.png)

請參閱 [互動式影像](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html) 上圖的網頁上。

## 觀看如何建立互動式影像條幅 {#watch-how-interactive-image-banners-are-created}

觀看上的漫步 [如何建立互動式影像條幅](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner) （10分33秒）。 您還將學習如何預覽、編輯和傳遞互動式影像橫幅。

## 快速啟動：互動式影像 {#quick-start-interactive-images}

以下逐步工作流說明旨在幫助您快速啟動並運行Adobe Experience Manager資產中的互動式映像。

查找 **示例** 標題。 它包含一個基於 [網頁示例尚未添加互動式影像](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html)。



本教程有助於說明在您自己的網站上整合互動式影像的步驟。

交互映像步驟：

1. **（可選）標識熱點變數**。 如果您使用Adobe Experience Manager資產和Dynamic Media獨立版，請確定現有Quickview實現中使用的動態變數。 這樣可確保在建立互動式影像時可以輸入熱點資料。 請參閱 [（可選）標識熱點變數](#optional-identifying-hotspot-variables)。
但是，如果您使用Experience Manager Sites或Experience Manager電子商務，或同時使用兩者，則無需執行此步驟。

1. **（可選）建立互動式影像查看器預設**。 定制用於表示熱點的圖形影像。 如果要使用名為的現成互動式影像查看器預設，則不需要建立您自己的互動式影像查看器預設 `Shoppable_Banner` 的雙曲餘切值。
請參閱 [（可選）建立互動式影像查看器預設](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset)。

1. **上載影像標題**。 上載要進行交互的影像橫幅。
請參閱 [正在上載影像標題](#uploading-an-image-banner)。

1. **將熱點添加到影像標題**。 將一個或多個熱點添加到影像標題。 將每個操作與操作（如超連結、Quickview或體驗片段）關聯。 添加熱點後，將通過發佈互動式影像來完成此任務。
請參閱 [向影像標題添加熱點](#adding-hotspots-to-an-image-banner)。
請參閱 [預覽互動式影像](#optional-previewing-interactive-images)  — 可選。 如果需要，可以查看可購物橫幅的表示形式並test其交互性。
請參閱 [發佈資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) 的子菜單。

1. **將互動式影像添加到您的網站或您的網站，以Experience Manager**。 如果您使用網站或電子商務，或兩者都使用，則可以直接將互動式影像添加到Experience Manager中的網頁。 將互動式媒體元件拖到頁面上。 請參閱 [將Dynamic Media資產添加到頁面](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)。
如果您使用Experience Manager資產和Dynamic Media獨立版，請將嵌入代碼複製到您的網站上。 然後，將其與現有Quickview整合。 請參閱 [將互動式影像與您的網站整合](#integrating-an-interactive-image-with-your-website)。
如果您使用第三方WCM（Web內容管理器），請將新的互動式視頻與網站上使用的現有Quickview整合。 請參閱 [將互動式影像與現有Quickview整合](#integrating-an-interactive-image-with-an-existing-quickview)。

## （可選）標識熱點變數 {#optional-identifying-hotspot-variables}

>[!NOTE]
>
>僅當以下情況為真時，才需要此任務：
>
>* 要通過觸發到「快速」視圖將交互性添加到影像。
>* 您實施Experience Manager *不* 使用電子商務整合框架將產品資料從任何電子商務解決方案拉入Experience Manager。 此類解決方案包括IBM® WebSphere® Commerce、Elastic Path、SAP Hybris或Intershop。
>
>如果您的Experience Manager實施使用電子商務，則可以跳過此任務並繼續執行下一個任務。

首先確定現有Quickview實現使用的動態變數，以便您可以輸入熱點資料以建立互動式影像。

將熱點添加到Experience Manager Assets的標題影像時，請分配SKU（庫存單位）。 SKU是您提供的每個不同產品或服務的唯一標識符。 並且，向每個熱點添加任何額外的可選變數。 此熱點變數稍後用於將熱點與Quickview內容匹配。

正確識別要與熱點資料關聯的變數的數量和類型非常重要。 添加到橫幅影像的每個熱點都必須攜帶足夠的資訊，以明確標識現有後端系統中的產品。

識別一組用於熱點資料的變數的方法不同。

有時，與負責現有Quickview實施的IT專家進行咨詢就足夠了。 此類人員可能知道在系統中標識Quickview所需的最少一組資料。 但是，也可以簡單地分析前端代碼的現有行為。

大多數Quickview實現都使用以下範例：

* 使用者在網站上啟動使用者介面元素。例如，選擇「快速視圖」按鈕。
* 如果需要，網站會向後端發送Ajax請求以載入Quickview資料或內容。
* Quickview資料被翻譯成內容以準備在網頁上呈現。
* 最後，前端代碼在螢幕上直觀地呈現這些內容。

然後，方法是訪問現有網站中實施Quickview功能的不同區域。 然後觸發Quickview並獲取網頁發送的Ajax URL，以載入Quickview資料或內容。

通常，您不需要使用任何專用的調試工具。 現代Web瀏覽器具有能夠完成充分工作的Web檢查器。 以下是包括Web檢查器的Web瀏覽器的幾個示例：

* 要在GoogleChrome中查看所有傳出HTTP請求，請按F12開啟「開發人員工具」面板，然後選擇「網路」頁籤。
在Mac上，按Command+Option+I以開啟「開發人員工具」面板，然後選擇「網路」頁籤。

* 在Firefox中，您可以通過按F12並使用其「Net」頁籤來激活Firebug插件。 或者，可以使用內置的「檢查器」工具及其「網路」頁籤。
在Mac上，按Command+Option+I以開啟「開發人員工具」面板，然後選擇「檢查器」頁籤。

在瀏覽器中開啟網路監視時，在頁面上觸發Quickview。

現在，在網路日誌中查找Quickview Ajax URL，並複製記錄的URL以供將來分析。 通常，在觸發Quickview時，會向伺服器發送大量請求。 通常，Quickview Ajax URL是清單中的第一個URL之一。 它具有複雜的查詢字串部分或路徑，其響應MIME類型為 `text/html`。 `text/xml`或 `text/javascript`。

在此過程中，訪問您網站的不同區域、不同的產品類別和類型非常重要。 原因是Quickview URL可以包含指定網站類別的公用部件。 但是，只有訪問網站的其他區域，它們才會改變。

在最簡單的情況下，Quickview URL中唯一的變數部分是產品SKU。 在這種情況下，SKU值是向橫幅影像添加熱點所需的唯一資料段。

但是，在複雜情況下，Quickview URL除了SKU之外還有不同的元素。 例如，變化元素可能包括類別ID、顏色代碼和大小代碼。 在這種情況下，在Experience Manager Assets的可購物互動式影像功能中，每個元素都是熱點資料定義中的一個單獨變數。

請考慮以下Quickview URL及其產生的熱點變數示例：

<table>
  <tbody>
  <tr>
    <td><p>在查詢字串中找到的單個SKU。</p> </td>
    <td><p>錄制的Quickview URL包括以下內容：</p>
    <ul>
      <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>URL中唯一的變數部分是productId=查詢字串參數的值，它顯然是SKU值。 因此，熱點只需要填充SKU欄位，如 <strong><code>866558</code></strong>。 <strong><code>1196184</code></strong>。 <strong><code>1081492</code></strong>。 <strong><code>1898294</code></strong>。</p> </td>
  </tr>
  <tr>
    <td><p>單SKU，在URL路徑中找到。</p> </td>
    <td><p>錄制的Quickview URL包括以下內容：</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>變數部分位於路徑的最後一部分，它成為熱點的SKU值： <strong><code>6422350843</code></strong>。 <strong><code>1607745002</code></strong>。 <strong><code>0086724882</code></strong>。</p> </td>
  </tr>
  <tr>
    <td><p>查詢字串中的SKU和類別ID。</p> </td>
    <td><p>錄制的Quickview URL包括以下內容：</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>在這種情況下，URL中有兩個不同的部分。 SKU儲存在 <code>prodId</code> 參數和類別ID<code></code> 儲存在 <code>category=</code> 的下界。</p> <p>因此，熱點定義是對。 即，SKU值和一個稱為 <code>categoryId</code>。 結果對如下：</p>
    <ul>
      <li><p>SKU是 <strong><code>305466</code></strong> 和 <code>categoryId</code> 是 <code>1100004</code>。</p> </li>
      <li><p>SKU是 <strong><code>310181</code></strong> 和 <code>categoryId</code> 是 <strong><code>1100004</code></strong>。</p> </li>
      <li><p>SKU是 <strong><code>308706</code></strong> 和 <code>categoryId</code> 是 <strong><code>1740148</code></strong>。</p> </li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**範例**

可將上述三個示例中使用的相同方法應用於 [演示網頁](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html)。

演示網頁有幾個產品縮略圖，每個產品縮略圖都有一個標有「查看更多」的Quickview按鈕。 在Web瀏覽器的調試工具仍處於激活狀態時，選擇每個按鈕並記下錄制的Quickview URL。 激活該頁上所有四個產品快速視圖後，您將擁有向後端發出的Quickview請求清單：

* `/datafeed/Male-Windbreaker.json`
* `/datafeed/Male-SimpleHenley.json`
* `/datafeed/Male-CamoPullover.json`
* `/datafeed/Female-QuiltedDownJacket.json`

查看伺服器呼叫時，您可以看到特定於產品的資訊僅存在於請求路徑中。 您還注意到查詢字串根本未使用，並且涉及兩種不同類型的資料段：

* 第一種類型為「Male」（男性）或「Meture」（女性）。 您可以將此稱為「產品類別」。
* 第二種類型是產品名稱，如CamoPullover，它可能是產品SKU。

根據此資訊，整個Quickview URL具有以下模式：

`/datafeed/$categoryId$-$SKU$.json`

根據這種分析， `categoryId` 和 `SKU` 按鈕。

現在，您已準備好使用Experience Manager Assets的可購物互動式影像功能上載影像橫幅並向其添加熱點。

## （可選）建立互動式影像查看器預設 {#optional-creating-an-interactive-image-viewer-preset}

您可以選擇使用預設的現成互動式影像查看器預設，該預設稱為 `Shoppable_Banner` 是Experience Manager Assets。 或者，您可以建立您自己的自定義查看器預設，以用於互動式影像。

建立自定義互動式影像查看器預設時，可確定影像標題上熱點的外觀。 作為建立查看器預設的一部分，您可以選擇使用預定義影像庫中的熱點圖形。

保存查看器預設後，它將在Experience Manager Assets的「查看器預設」清單頁面上自動激活（開啟）。 此功能意味著它在交互媒體元件中以及在您查看資產時都可見。 但是， *送* 與此查看器預設的互動式橫幅， *發佈* 您的查看器預設。 此規則對於自定義或現成查看器預設為true。

**要建立互動式影像查看器預設：**

1. 在左欄中，轉到 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 查看器預設]**。
1. 在頁面的右上角，點擊 **[!UICONTROL 建立]**。
1. 在「新建查看器預設」對話框中，鍵入一個名稱來描述互動式橫幅查看器預設。

   保存後，此標題將顯示在「查看器預設」清單頁中。

1. 在「豐富型媒體類型」下拉式功能表中，選取「互動 **[!UICONTROL 式影像」]**。
1. 選擇 **[!UICONTROL 建立]**。
1. 在「編輯查看器預設」頁面，按一下 **[!UICONTROL 外觀]** 頁籤。
1. 執行下列操作之一：

   * 要上載您想要在影像上使用的自己的熱點影像，請點擊「資產選取器」表徵圖。 在「選擇內容」頁中，導航到要使用的熱點影像並選擇它。 選擇右上角的「複選標籤」表徵圖。
   * 要選擇預定義的熱點影像，請按一下「熱點庫」表徵圖。 在熱點庫調色板上，點擊要使用的熱點影像。

1. 在頁面的右上角，點擊 **[!UICONTROL 保存]**。

   確保發佈新查看器預設。

   請參閱 [發佈查看器預設](/help/assets/dynamic-media/managing-viewer-presets.md#publishing-viewer-presets)。

   您現在已準備好上載影像標題。

## 上載影像標題 {#uploading-an-image-banner}

如果您已上傳了要使用的影像，請進入下一步， [向影像標題添加熱點](#adding-hotspots-to-an-image-banner)。

**要上載影像標題：**

1. 上載要進行交互的影像橫幅。

   請參閱 [正在上載資產](/help/assets/manage-digital-assets.md#uploading-assets)。

   您現在已準備好將熱點添加到影像標題中；請參閱下面的下一個任務。

## 將熱點添加到影像標題 {#adding-hotspots-to-an-image-banner}

可以使用「熱點管理」頁上的編輯器將熱點添加到影像標題。

添加熱點時，可以將其定義為Quickview彈出式顯示、超連結或體驗片段。

請參閱 [體驗片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)。

>[!NOTE]
>
>當您將查看器嵌入體驗片段時，不支援互動式影像中的社交媒體共用工具。 而是使用或建立沒有社交媒體共用工具的查看器預設。 這樣的查看器預設使您能夠成功將其嵌入「體驗片段」中。

在當前建立/編輯會話期間，支援在頁面右上角附近的「撤消」和「重做」選項。

建立完互動式影像後，可以使用「預覽」查看互動式影像對客戶的顯示方式。

請參閱 [（可選）預覽互動式影像](#optional-previewing-interactive-images)。

>[!NOTE]
>
>將熱點添加到交互影像或旋轉傳送條幅中的影像時，熱點資訊將儲存在同一元資料位置。 此位置相對於影像的位置，而不管它是互動式影像還是旋轉木馬橫幅。 此功能意味著您可以在任意一個查看器中輕鬆地重複使用同一影像及其定義的熱點資料。
但是，請注意，Carousel Banters支援影像上的影像映射，這些影像中也包含熱點；互動式映像不會。 如果要建立使用相同影像的互動式影像或旋轉木馬橫幅，請記住此思想。 您可以使用同一影像的單獨副本建立互動式影像和旋轉傳送條幅。
另請參閱 [旋轉木馬旗幟](/help/assets/dynamic-media/carousel-banners.md)。

>[!NOTE]
如果您正在編輯具有熱點的交互影像並裁剪影像，則您的熱點將被刪除。

**要將熱點添加到影像標題：**

1. 在「資產」視圖中，導航到要進行交互的影像標題。
1. 執行下列操作之一：

   * 懸停在影像上，然後點擊 **[!UICONTROL 選擇]** （複選標籤表徵圖）。 在工具欄上，點擊 **[!UICONTROL 編輯]**。

   * 懸停在影像上，然後點擊 **[!UICONTROL 更多操作]** （三點表徵圖） **[!UICONTROL >編輯]**。

   * 要在「詳細視圖」頁面中開啟它，請點擊影像。 在工具欄中，點擊 **[!UICONTROL 編輯]**。

1. 在頁面的左上角附近，點選「新增熱點」( **[!UICONTROL 手指點選圖示]** )以開啟「熱點」管理頁面。
1. 在頁面左上角附近，點擊 **[!UICONTROL 熱點]**。

   1. 在「熱點管理」頁的左上角附近，點擊 **[!UICONTROL 熱點]**。
   1. 在影像上，點選您要熱點出現的位置。如有必要，請拖動熱點以調整其位置。或者，使用鍵盤箭頭鍵控制選定熱點的位置。
   1. 重複步驟a和b，根據需要添加更多熱點。
   1. （可選）要刪除熱點，請在影像上選擇它，然後點擊 **[!UICONTROL 刪除]** （垃圾表徵圖） **[!UICONTROL 熱點]** 的子菜單。

1. 在「名稱」文本欄位中，鍵入熱點的名稱。 此名稱也出現在「選定熱點」下拉清單中。
1. 執行下列操作之一：

   * 選擇 **[!UICONTROL 快速視圖]**。

      * 如果您是Experience Manager Sites或電子商務客戶，請選擇「產品選取器」表徵圖（放大鏡）以開啟「選擇產品」頁。 選擇要使用的產品，然後點擊 **選擇** 在右上角。 您將返回熱點管理頁。
      * 如果 *不* Experience Manager Sites或電子商務客戶

         * 請參閱 [識別熱點變數](#optional-identifying-hotspot-variables);必須定義這些變數。
         * 然後，手動輸入SKU值。 在「SKU值」文本欄位中，鍵入產品的SKU。 輸入的SKU值會自動填充Quickview模板的可變部分。 它確保系統知道將點擊的熱點與特定SKU的Quickview關聯。
         * （可選）如果Quickview中有其他用於進一步標識產品的變數，請點擊 **[!UICONTROL 添加泛型變數]**。 在文本欄位中，指定一個額外變數。 比如說， `category=Mens` 是已添加的變數。
   * 選擇 **[!UICONTROL 超連結]**。

      * 如果您是Experience Manager Sites客戶，請按一下「站點選擇器」表徵圖（資料夾）。 導航到URL。 如果您的交互內容具有與相對URL的連結，特別是與Experience Manager Sites頁面的連結，則無法使用基於URL的連結方法。
      * 如果您是獨立客戶，請在HREF文本欄位中指定連結網頁的完整URL路徑。

   請確保指定是在新瀏覽器頁籤（推薦的預設頁籤）或同一頁籤中開啟連結。

   請參閱 [使用選擇器](/help/assets/dynamic-media/working-with-selectors.md) 的子菜單。

   * 選擇 **[!UICONTROL 體驗片段]**。

      * 如果您是Experience Manager Sites客戶，請選擇「搜索」表徵圖（放大鏡）以開啟「體驗片段」頁。 選擇要使用的體驗片段。 然後點擊 **[!UICONTROL 選擇]** 在右上角。 您將返回熱點管理頁。
請參閱 [體驗片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)。

      * 指定希望在橫幅上顯示體驗片段的寬度和高度。

         >[!NOTE]
         當您將查看器嵌入體驗片段時，不支援互動式影像中的社交媒體共用工具。 而是使用或建立沒有社交媒體共用工具的查看器預設。 這樣的查看器預設使您能夠成功將其嵌入「體驗片段」中。



1. 選擇 **[!UICONTROL 保存]** 保存您的工作並返回「瀏覽」頁。
1. 發佈互動式影像。 發佈通過雲傳遞標題，還生成嵌入代碼，使您能夠與第三方網站整合。

   請參閱 [發佈資產](/help/assets/manage-digital-assets.md#publish-assets)。

   添加熱點並發佈互動式影像後，您現在可以將其添加到現有網站。

   請參閱 [將互動式影像與您的網站整合](#integrating-an-interactive-image-with-your-website)。

   >[!NOTE]
   如果您正在編輯具有熱點的互動式影像並裁剪影像，則您的熱點將被刪除。

### （可選）預覽互動式影像 {#optional-previewing-interactive-images}

您可以使用「預覽」查看互動式影像對客戶的顯示方式。 預覽還允許您test影像的熱點，以確保它們按預期的方式運行。

當您對互動式影像感到滿意時，可以發佈它。
請參閱 [將視頻或影像查看器嵌入網頁](/help/assets/dynamic-media/embed-code.md)。
請參閱 [將URL連結到Web應用程式](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)。 如果您的交互內容具有與相對URL的連結，特別是與Experience Manager Sites頁面的連結，則無法使用基於URL的連結方法。
請參閱 [將Dynamic Media資產添加到頁面](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)。

**要預覽互動式影像：**

1. 在「資產」視圖中，導航到已建立的現有互動式影像，然後點擊以在「預覽」中開啟它。
1. 在「預覽」頁面的左上角附近，在「內容」下拉清單中，按一下 **[!UICONTROL 查看者]**。
1. 在「查看者」清單中，點擊 **[!UICONTROL 可購物橫幅]** 或您建立的互動式影像查看器預設的名稱。
1. 要test熱點的關聯操作，請點擊影像上的熱點。

## 發佈互動式影像資產 {#publishing-interactive-image-assets}

請參閱 [發佈資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) 的子菜單。

## 將互動式影像與您的網站整合 {#integrating-an-interactive-image-with-your-website}

上載橫幅影像、向其添加熱點並發佈互動式影像後，您就可以將其添加到網站頁面。

如果您是Experience Manager Sites客戶，則可以通過將互動式媒體元件拖到頁面上來添加互動式影像。 請參閱 [將Dynamic Media資產添加到頁面](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)。

如果您是Experience Manager Assets的獨立客戶，則可以按本節所述手動將互動式映像添加到您的網站。

1. 複製已發佈的互動式影像的嵌入代碼。
請參閱 [將視頻或影像查看器嵌入網頁](/help/assets/dynamic-media/embed-code.md)。

1. 將複製的嵌入代碼添加到網頁中所需的位置。
所複製的嵌入代碼被設定用於響應環境，以便它自動適應所分配的區域。

**範例**

使用 [示例演示網站](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html)注意，這三個人的照片是靜態的 `IMG` 標籤：

```xml {.line-numbers}
<img class="img-responsive" width="100%" title="Hero Image 2" alt="Hero Image 2" src="images/shoppable-banner.jpg">
```

整合與刪除 `IMG` 標籤並用從Experience Manager Assets複製的嵌入代碼替換。 你可以看到 [顯示具有三個圓形熱點的頁面上的可購物互動式影像](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-1.html)。

>[!NOTE]
因此，演示網站的可購物互動式影像上的熱點僅用於顯示。 它們尚未與現有的快速視圖整合。

要將「裁剪」應用到響應環境的可購物互動式影像，請包括互動式影像配置屬性 `ZoomView.iscommand` 到路上。 在這個例子中， `ZoomView` 元件調用和 `iscommand` 是您應用的「裁剪」影像服務命令。

請參閱 [ZoomView.iscommand](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/command-reference-configuration-attributes-interactive-images/r-html5-aem-interactive-image-config-attrib-zoomview-iscommand.html) 配置屬性。

請參閱 [作物](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-crop.html) 影像服務命令。

現在，您已準備好將互動式影像與網站上的現有Quickview整合。

## 將互動式影像與現有Quickview整合 {#integrating-an-interactive-image-with-an-existing-quickview}

>[!NOTE]
僅當您是獨立的Experience Manager Assets客戶時，此任務才適用。

此過程中的最後一個步驟是將互動式影像與網站上現有的Quickview實現整合。 對於適用於所有案例的整合，沒有解決方案。 每個Quickview實施都是獨特的，需要一種特定的方法。 因此，讓前端IT人員提供幫助是有益的。

現有的Quickview實現通常表示網頁上發生的一系列相互關聯的操作，其順序如下：

1. 用戶在網站的用戶介面中觸發元素。
1. 前端代碼根據步驟1中觸發的用戶介面元素獲取Quickview URL。
1. 前端代碼使用步驟2中獲得的URL發送Ajax請求。
1. 後端邏輯將相應的Quickview資料或內容返回到前端代碼。
1. 前端代碼載入Quickview資料或內容。
1. 或者，前端代碼將載入的Quickview資料轉換為HTML表示。
1. 前端代碼顯示一個模式對話框或面板，並在螢幕上為最終用戶呈現HTML內容。

這些調用不一定代表由網頁邏輯從任意步驟調用的獨立公共API調用。 相反，它是連結調用，在上一步的最後階段（回叫）中，每個下一步都被隱藏。

當該可購物互動式影像正在替換步驟1和部分步驟2時，用戶在該可購物影像內抽取熱點。 這種用戶交互由查看器處理。 查看器將事件返回至包含先前添加到Experience Manager Assets的所有熱點資料的網頁。

在此類事件處理程式中，前端代碼執行以下操作：

* 偵聽由可購買交互映像發出的事件。
* 基於熱點資料構建Quickview URL。
* 觸發從後端載入Quickview並將其呈現在螢幕上以供顯示的過程。

Experience Manager Assets返回的嵌入代碼具有一個可供使用的事件處理程式，該事件處理程式被注釋出來，如以下突出顯示的代碼段所示：

```xml {.line-numbers}
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

因此，只需取消注釋代碼，用特定網頁的代碼替換虛擬處理程式主體即可。

構造Quickview URL的過程與用於識別先前覆蓋的熱點變數的過程相反。

請參閱 [識別熱點變數](#optional-identifying-hotspot-variables)。

使用前面的Quickview URL示例，您可以在以下示例中查看如何在每種情況下構建Quickview URL:

<table>
 <tbody>
  <tr>
   <td><p>在查詢字串中找到的單一SKU</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/json?productId=" + inData.sku + "&amp;amp;source=100";
      },
      });</code></td>
  </tr>
  <tr>
   <td><p>單SKU，在URL路徑中找到</p> </td>
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

觸發Quickview URL並激活Quickview面板的最後一步需要前端IT人員在您的工作中提供幫助。 他們知道如何從正確的步驟準確觸發Quickview實現，並擁有可供使用的Quickview URL。

您可以看到這些步驟如何應用到演示網站，以將可購買的互動式影像與Quickview代碼完全整合。 以前，Quickview URL的結構標識如下：

```xml {.line-numbers}
/datafeed/$categoryId$-$SKU$.json
```

在 `quickViewActivate` handler，你可以 `categoryId` 和 `SKU` 的子菜單。 這些欄位在 `inData` 通過查看器代碼傳遞給處理程式的對象：

```xml {.line-numbers}
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

演示網站正在使用一個簡單的 `loadQuickView()` 函式。 此函式只採用一個參數，即Quickview資料URL。 因此，整合可購物互動式影像的最後一步是將以下代碼行添加到 `quickViewActivate` 處理程式：

```xml {.line-numbers}
loadQuickView(quickViewUrl);
```

以下是完整的原始碼：

```xml {.line-numbers}
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

的 [最後一個演示網站，其中包含完全整合的互動式影像](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-3.html)。

## 使用Quickview建立自定義彈出窗口 {#using-quickviews-to-create-custom-pop-ups}

請參閱 [使用Quickview建立自定義彈出式Windows®](/help/assets/dynamic-media/custom-pop-ups.md)。
