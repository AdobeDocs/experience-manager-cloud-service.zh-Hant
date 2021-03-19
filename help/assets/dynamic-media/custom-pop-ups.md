---
title: 使用快速檢視建立自訂快顯視窗
description: 「瞭解電子商務體驗中如何使用預設的快速檢視，從而顯示包含產品資訊的快顯視窗來推動購買。 您可以觸發自訂內容，以便在快顯視窗中顯示。」
topic: 「開發人員、管理員、商業從業人員」
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 0%

---


# 使用快速檢視建立自訂快顯視窗{#using-quickviews-to-create-custom-pop-ups}

電子商務體驗會使用預設的快速檢視，以便顯示含產品資訊的快顯視窗來推動購買。 不過，您可以觸發自訂內容以顯示在快顯視窗中。 根據您使用的檢視器，客戶可以點選熱點、縮圖影像或影像地圖來查看資訊或相關內容。

Dynamic Media的下列檢視器支援快速檢視：

* 互動式影像（可點選的熱點）
* 互動式視訊（視訊播放時可點選的縮圖影像）
* 轉盤橫幅（可點選的熱點或影像地圖）

雖然每個檢視器的功能不同，但建立快速檢視的程式在所有三個支援的檢視器上都相同。

**使用快速檢視來建立自訂快顯視窗**

1. 建立已上傳資產的快速檢視。

   您通常會在編輯資產時建立快速檢視，以便與您使用的檢視器搭配使用。

   <table>
    <tbody>
    <tr>
    <td><strong>您使用的檢視器</strong></td>
    <td><strong>若要建立快速檢視，請完成下列步驟</strong></td>
    </tr>
    <tr>
    <td>互動影像</td>
    <td><a href="/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner" target="_blank">將熱點添加到影像橫幅</a>。</td>
    </tr>
    <tr>
    <td>互動影片</td>
    <td><a href="/help/assets/dynamic-media/interactive-videos.md#adding-interactivity-to-your-video" target="_blank">為視訊新增互動功能</a>。</td>
    </tr>
    <tr>
    <td>輪播橫幅</td>
    <td><a href="/help/assets/dynamic-media/carousel-banners.md#adding-hotspots-or-image-maps-to-an-image-banner" target="_blank">將熱點或影像映射添加到橫幅</a>。<br /> </td>
    </tr>
    </tbody>
   </table>

1. 取得檢視器內嵌程式碼，將檢視器整合在您的網站中。

   <table>
    <tbody>
    <tr>
    <td><strong>您使用的檢視器</strong><br /> </td>
    <td><strong>若要將檢視器與您的網站整合，請完成下列步驟</strong></td>
    </tr>
    <tr>
    <td>互動式影像</td>
    <td><a href="/help/assets/dynamic-media/interactive-images.md#integrating-an-interactive-image-with-your-website" target="_blank">將互動式影像與您的網站整合</a>。<br /> </td>
    </tr>
    <tr>
    <td>互動式視訊<br /> </td>
    <td><a href="/help/assets/dynamic-media/interactive-videos.md#integrating-an-interactive-video-with-your-website" target="_blank">將互動式視訊與您的網站整合</a>。<br /> </td>
    </tr>
    <tr>
    <td>轉盤橫幅</td>
    <td><a href="/help/assets/dynamic-media/carousel-banners.md#adding-a-carousel-banner-to-your-website-page" target="_blank">新增轉盤橫幅至您的網站頁面</a>。<br /> </td>
    </tr>
    </tbody>
   </table>

1. 您使用的檢視器必須知道如何使用快速檢視。

   檢視器使用名為`QuickViewActive`的處理常式。

   **范**
例假設您在網頁上使用下列互動式影像的範例內嵌程式碼：

   ![chlimage_1-291](assets/chlimage_1-291.png)

   處理常式會使用`setHandlers`載入檢視器：

   `*viewerInstance*.setHandlers({ *handler 1*, *handler 2*}, ...`

   **使用上述範例內嵌程式碼範例，您有下列程式碼：**

   ```xml
   s7interactiveimageviewer.setHandlers({
       quickViewActivate": function(inData) {
           var sku=inData.sku;
           var genericVariable1=inData.genericVariable1;
           var genericVariable2=inData.genericVariable2;
          loadQuickView(sku,genericVariable1,genericVariable2);
       }
   })
   ```

   如需`setHandlers()`方法的詳細資訊，請參閱：

   * 互動式影像檢視器：[sethandlers](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-sethandlers.html)
   * 互動式視訊檢視器：[sethandlers](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-sethandlers.html)

1. 現在，請設定`quickViewActivate`處理常式。

   `quickViewActivate`處理常式控制檢視器中的「快速檢視」。 處理常式包含變數清單和函式呼叫，以便與「快速檢視」搭配使用。 內嵌代碼提供「快速檢視」中SKU變數集的對應。 它還調用了示例`loadQuickView`函式。

   **變**
數mappingMap變數，用於您的網頁中，以至「快速檢視」中包含的SKU值和一般變數：

   `var *variable1*= inData.*quickviewVariable*`

   提供的內嵌代碼具有SKU變數的範例對應：

   `var sku=inData.sku`

   從「快速檢視」中映射其他變數，如下所示：

   ```
   var <i>variable2</i>= inData.<i>quickviewVariable2</i>
    var <i>variable3</i>= inData.<i>quickviewVariable3</i>
   ```

   **函式**
呼叫處理常式也需要函式呼叫，才能使快速檢視運作。您的主機頁面會假設該函式可存取。 內嵌代碼提供範例函式呼叫：

   `loadQuickView(sku)`

   示例函式調用假定函式`loadQuickView()`存在且可訪問。

   如需`quickViewActivate`方法的詳細資訊，請參閱：

   * 互動式影像檢視器- [事件回呼](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-event-callbacks.html)
   * 互動式視訊檢視器- [事件回呼](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-event-callbacks.html)
   * 互動式視訊檢視器中的互動式資料支援- [互動式資料支援](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-int-data-support.html)

1. 請執行下列動作：

   * 取消對embed代碼的setHandlers部分的注釋。
   * 映射快速檢視中包含的任何其他變數。

      * 如果新增更多變數，請更新`loadQuickView(sku,*var1*,*var2*)`呼叫。
   * 在檢視器外部的頁面上建立簡單的`loadQuickView`()函式。

      例如，下列程式碼會將SKU值寫入瀏覽器主控台：

   ```xml
   function loadQuickView(sku){
       console.log ("quickview sku value is " + sku);
   }
   ```

   * 將測試HTML頁面上傳至網頁伺服器並開啟。

      快速檢視中的變數會被映射。 函式呼叫就位。 瀏覽器主控台會將變數值寫入瀏覽器主控台。 它使用提供的樣例函式來執行此操作。



1. 您現在可以使用函式來叫用「快速檢視」中的簡單快顯視窗。 下列範例會針對快顯視窗使用`DIV`。
1. 按以下方式設定彈出式菜單`DIV`的樣式。 視需要新增額外的樣式。

   ```xml
   <style type="text/css">
       #quickview_div{
           position: absolute;
           z-index: 99999999;
           display: none;
       }
   </style>
   ```

1. 將快顯視窗`DIV`置於HTML頁面的正文中。

   其中一個元素會以ID設定，當使用者叫用「快速檢視」時，ID會以SKU值更新。 此範例也包含一個簡單按鈕，可在快顯視窗顯示後再次隱藏。

   ```xml
   <div id="quickview_div" >
       <table>
           <tr><td><input id="btnClosePopup" type="button" value="Close"        onclick='document.getElementById("quickview_div").style.display="none"' /><br /></td></tr>
           <tr><td>SKU</td><td><input type="text" id="txtSku" name="txtSku"></td></tr>
       </table>
   </div>
   ```

1. 若要在快顯視窗中更新SKU值，請新增函式。 將步驟5中建立的簡單函式取代為下列項目，讓快顯視窗可見：

   ```xml
   <script type="text/javascript">
       function loadQuickView(sku){
           document.getElementById("txtSku").setAttribute("value",sku); // write sku value
           document.getElementById("quickview_div").style.display="block"; // show popup
       }
   </script>
   ```

1. 將測試HTML頁面上傳至您的網站伺服器並開啟。 當使用者叫用「快速檢視」時，檢視器會顯示快顯視窗`DIV`。
1. **如何以全螢幕模式顯示自訂快顯視窗**

   有些檢視器（例如互動式視訊檢視器）支援全螢幕模式顯示。 不過，如前述步驟所述，使用快顯功能會使它在全螢幕模式下顯示在檢視器後方。

   若要讓快顯視窗以標準和全螢幕模式顯示，請將快顯視窗附加至檢視器容器。 在此例中，請使用第二個處理常式方法`initComplete`。

   在初始化檢視器後，會呼叫`initComplete`處理常式。

   ```xml
   "initComplete":function() { code block }
   ```

   如需`init()`方法的詳細資訊，請參閱：

   * 互動式影像檢視器- [init](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-init.html)
   * 互動式視訊檢視器- [init](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-init.html)

1. 若要將快顯視窗（如前述步驟所述）附加至檢視器，請使用下列程式碼：

   ```xml
   "initComplete":function() {
       var popup = document.getElementById('quickview_div');
       popup.parentNode.removeChild(popup);
       var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId();
       var inner_container = document.getElementById(sdkContainerId);
       inner_container.appendChild(popup);
   }
   ```

   在上述程式碼中，您已執行下列作業：

   * 已識別您的自訂快顯視窗。
   * 從DOM中移除。
   * 已識別檢視器容器。
   * 已將快顯視窗連接至檢視器容器。

1. 您的整個setHandlers程式碼類似於下列程式碼（使用互動式視訊檢視器）:

   ```xml
   s7interactivevideoviewer.setHandlers({
       "quickViewActivate": function(inData) {
           var sku=inData.sku;
           loadQuickView(sku);
   
       },
       "initComplete":function() {
           var popup = document.getElementById('quickview_div'); // get custom quick view container
           popup.parentNode.removeChild(popup); // remove it from current DOM
           var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId();
           var inner_container = document.getElementById(sdkContainerId);
           inner_container.appendChild(popup);
       }
   });
   ```

1. 載入處理常式後，您就會初始化檢視器：

   `*viewerInstance.*init()`

   **范**
例此範例使用互動式影像檢視器。

   `s7interactiveimageviewer.init()`

   將檢視器內嵌至主機頁面後，請確定已建立檢視器例項。 此外，請確定在使用`init()`呼叫檢視器之前已載入處理常式。

