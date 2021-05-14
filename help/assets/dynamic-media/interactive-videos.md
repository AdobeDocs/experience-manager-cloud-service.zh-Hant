---
title: 互動影片
description: 瞭解如何在Dynamic Media使用互動式視訊和可購買視訊。
feature: 互動影片
role: Business Practitioner
exl-id: e4859223-91de-47a1-a789-c2a9447e5f71
source-git-commit: d3ee23917eba4a2e4ae1f2bd44f5476d2ff7dce1
workflow-type: tm+mt
source-wordcount: '6051'
ht-degree: 3%

---

# 互動影片{#interactive-videos}


您可以輕鬆製作互動式視訊（也稱為可購買的視訊），直接從視訊推動轉換。 客戶與視訊的互動會與視訊播放器一起在面板中進行，視訊播放器會根據視訊中的功能捲動相關服務、資訊或產品縮圖。 客戶可以點選縮圖並直接連結至服務，或將項目新增至購物車以立即購買，或連結至網頁以取得詳細資訊。

當視訊結束時，會顯示所有方案的視覺化摘要，以推動行動要求。 客戶有另一個機會來點選他們想要的項目。 可操作且具體的體驗，例如這些可提升客戶參與度和轉化率。

另請參閱[互動式影像](/help/assets/dynamic-media/interactive-images.md)。

## 互動式視訊的實際運作{#interactive-video-in-action}

若要檢視互動式可購買視訊的實際運作，請按一下「 [Live Demos](https://landing.adobe.com/tw/na/dynamic-media/ctir-2755/live-demos.html)」 (即時展示)，捲動至頁面上的 **[!UICONTROL Shopbable Media]** 標題，然後按一下可購買視訊以開始播放。

* 在播放期間，當視訊中使用產品時，相同的產品會以縮圖影像的形式出現在右側。

* 若要暫停影片並開啟產品的「快速檢視」，請點選縮圖。 例如，點選影片中的KitchenAid縮圖影像，即可體驗混合器的360度旋轉檢視，或放大檢視混合器詳細資訊。

另請參閱[搭配使用互動式視訊與Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-interactive-video-feature-video-use.html?lang=en#dynamic-media)

<!-- 

There was a link here that showed the video frame of an interactive video and when the reader clicked the frame the video would play https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/AXIS/index.html. This now needs to call a new interactive video

-->

<!-- 

[A frame from an interactive, shoppable video](assets/chlimage_1-126.png) *A video frame capture from an interactive, shoppable video.*

-->

>[!NOTE]
>
>如果您建立互動式視訊，以在使用者點選縮圖影像時啟動網頁，有些裝置會封鎖快顯網頁。 在這種情況下，請變更裝置上的快顯封鎖程式設定。 例如，在Apple iPhone 6上，點選「設定> Safari >封鎖快顯視窗&#x200B;]**」，然後將控制項滑入「**[!UICONTROL &#x200B;關閉&#x200B;]**」。**[!UICONTROL &#x200B;現在，當您播放互動式視訊並按一下縮圖時，如果您要開啟快顯視窗，就會出現提示。 如果您接受，則會開啟網頁。

### 觀看互動式視訊的建立方式{#watch-how-interactive-videos-are-created}

觀看[如何建立互動式視訊的逐步說明](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveVideo)（7分30秒）。
(雖然視訊逐步解說已加上隨選資產的品牌，但原則和步驟仍適用於「Adobe Experience Manager資產」中的互動式視訊。)

### Adobe客戶成功網路研討會{#adobe-customer-success-webinar}

[在Experience Manager資產中使用互動式視訊、連結分享和YouTube分享](https://adobecustomersuccess.adobeconnect.com/p1yxzdo4aec/)網路研討會教您如何使用互動式視訊和其他功能，將轉換導向的活動連結至視訊行銷內容。

## 快速入門：互動式影片{#quick-start-interactive-videos}

下列逐步工作流程說明旨在協助您在Dynamic Media快速上手使用互動式視訊。

在某些快速入門任務中查找&#x200B;**Example**&#x200B;標題。 它包含一個簡短的教學課程，以此[開始的示範網頁為基礎，*尚未*&#x200B;新增互動功能至](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html)。

範例 **可協助您說明** ，如何將互動式視訊整合在您自己的網站上。

當您在最後一個範例區段中完成教學課程時，[您的完整整合互動式視訊最終示範網頁會以此方式顯示](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-3.html)。



互動式視訊步驟：

1. **（可選）識別快速檢視變數** -從識別現有快速檢視實作使用的動態變數開始。當您建立互動式視訊時，可使用變數將產品縮圖對應至其對應的產品快速檢視。 請參閱[（可選）識別快速檢視變數](#optional-identifying-quickview-variables)。
   **只有在以下所有條件都成立時，才需要此步驟：**
·您要透過觸發至「快速檢視」，為視訊新增互動功能。·您實作的Experience Manager 
*不* 要使用電子商務整合架構，將產品資料從任何電子商務解決方案（例如IBM® WebSphere® Commerce、Elastic Path、SAP Hybris或Intershop）拉入Experience Manager。

1. **（可選）建立互動式視訊檢視器預設集** -自訂各種元件的外觀和行為，這些元件是播放器的組成元件，例如視訊筆畫和互動式縮圖。如果您想要改用現成可用的互動式視訊檢視器預設集`Shoppable_Video_Light`或`Shoppable_Video_Dark`，則不需要建立您自己的互動式視訊檢視器預設集。
請參閱[建立新檢視器預設集](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset)（選用）和[建立互動檢視器預設集的特殊注意事項](/help/assets/dynamic-media/managing-viewer-presets.md#special-considerations-for-creating-an-interactive-viewer-preset)。

1. **上傳視訊及其相關影像資產** -上傳您要製作互動內容的視訊和相關影像。請參閱[上傳視訊及其相關縮圖資產](#uploading-a-video-and-its-associated-thumbnail-assets)。

1. **為您的視訊新增互動功能** -在視訊中新增一或多個時間區段。然後，在這些時間區段內建立影像縮圖的關聯。 將每個影像縮圖指派給動作，例如超連結、快速檢視或體驗片段。
(如果您的互動式內容具有相對URL的連結，尤其是連結至「Experience Manager網站」頁面，則無法使用以URL為基礎的連結方法。)
發佈互動式視訊資產以完成。 發佈會建立您最終複製並套用至網站登陸頁面的內嵌代碼或URL。 請參閱[新增視訊的互動功能](#adding-interactivity-to-your-video)。
請參閱[發佈資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

1. **將互動式視訊新增至您的網站或Experience Manager網站** -如果您使用Experience Manager網站或電子商務，或兩者皆使用，請將互動式視訊新增至Experience Manager的網頁。將互動式媒體元件拖曳至頁面上。 請參閱[將Dynamic Media資產新增至Pages](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)。
使用內嵌程式碼或URL，將您的互動式視訊與網站體驗整合。 請參閱[將互動式視訊與您的網站整合](#integrating-an-interactive-video-with-your-website)。
如果您使用協力廠商WCM(Web Content Manager)，您必須將新的互動式視訊與網站上使用的現有快速檢視實作整合。 請參閱[整合互動式視訊與現有的快速檢視](#integrating-an-interactive-video-with-an-existing-quickview)。
   [新增Dynamic Media資產至頁面](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

## （可選）識別快速檢視變數{#optional-identifying-quickview-variables}

>[!NOTE]
只有在以下情況下，才需要此任務：
* 您想要透過觸發至「快速檢視」，將互動功能加入視訊。
* 您的Experience Manager實作&#x200B;*not*&#x200B;會使用電子商務整合架構，將產品資料從任何電子商務解決方案（例如IBM® WebSphere® Commerce、Elastic Path、SAP Hybris或Intershop）拉入Experience Manager。<!-- See [eCommerce concepts in Experience Manager Assets](/help/sites-administering/concepts.md).-->

如果您的Experience Manager實作使用電子商務，則可略過此工作並繼續下一個工作。

首先，識別您現有的快速檢視實作所使用的動態變數，以便您在互動式視訊建立程式中，將產品縮圖對應至對應的產品快速檢視。

在視訊中新增時間區段時，您會指派SKU（庫存保留單位）和任何其他變數至您新增至區段的每個縮圖。 這些變數稍後會用來顯示正確的快速檢視產品。

請務必正確識別唯一觸發產品快速檢視所需的變數。

有時，與負責您現有快速檢視實作的IT專家諮詢就夠了。 他們可能知道識別系統中「快速檢視」的最小資料集。 不過，您也可以簡單分析前端程式碼的現有行為。

大部分的快速檢視實作都採用下列範例：

* 使用者在網站上啟動使用者介面元素。例如，按一下「快速檢視」按鈕。
* 如有需要，網站會傳送Ajax要求至後端以載入快速檢視資料或內容。
* 快速檢視資料會轉譯為內容，以準備在網頁上轉譯。
* 最後，前端程式碼會以視覺化方式在螢幕上呈現此類內容。

因此，方法是造訪您現有網站中實作快速檢視的不同區域。 然後觸發快速檢視，並取得網頁所傳送的Ajax URL，以載入快速檢視資料或內容。

通常您不需使用任何專用的除錯工具。 現代網頁瀏覽器採用Web檢視器，可讓您完成適當的工作。 以下是包含Web檢視程式的Web瀏覽器範例：

* 若要在Google Chrome中查看所有傳出的HTTP要求，請按&#x200B;**F12**(Windows®)或&#x200B;**Command+Options+I**(Mac)以開啟「開發人員工具」面板，然後按一下「網路」標籤。****

* 在Firefox中，您可以按&#x200B;**F12**(Windows®)或&#x200B;**Command+Option+I**(Mac)啟動Firebug外掛程式，並使用其&#x200B;**[!UICONTROL Net]**&#x200B;標籤，或使用內建的檢查工具及其網路標籤。

* 在Internet Explorer中，按&#x200B;**F12**&#x200B;啟動除錯工具。

在瀏覽器中開啟網路監視時，觸發頁面上的快速檢視。

現在，在網路記錄檔中尋找快速檢視Ajax URL，並複製已記錄的URL以供日後分析。 通常當您觸發快速檢視時，會有許多要求傳送至伺服器。 通常，快速檢視Ajax URL是清單中第一個檢視的URL。 它有複雜的查詢字串部分或路徑，其回應MIME類型為`text/html`、`text/xml`或`text/javascript`。

在此程式中，請務必造訪您網站的不同區域，以及不同的產品類別和類型。 原因是快速檢視URL有特定網站類別的共用部分，但只有在您造訪網站的不同區域時才會變更。

在最簡單的情況下，「快速檢視URL」中唯一的變數部分是產品SKU。 在這種情況下，產品SKU值是將縮圖新增至互動式視訊中Experience Manager時段所需的唯一資料片段。

但是，在複雜情況下，快速檢視URL除了產品SKU以外，還有不同的元素，例如類別ID和顏色代碼。 在這種情況下，每個此類元素都會變成Experience Manager中縮圖資料定義中的個別變數。

請考慮下列快速檢視URL的範例及其產生的縮圖變數：

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
    </ul> <p>URL中唯一的變數部分是<code>productId=</code>查詢字串參數的值，而它顯然是SKU值。 因此，縮圖只需填入<strong><code>866558</code></strong>、<strong><code>1196184</code></strong>、<strong><code>1081492</code></strong>、<strong><code>1898294</code></strong>等值的SKU欄位。</p> </td>
  </tr>
  <tr>
    <td><p>單一SKU，位於URL路徑中。</p> </td>
    <td><p>錄制的快速檢視URL包括：</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>變數部分位於路徑的最後一部分，它會變成Experience Manager縮圖的SKU值：<strong><code>6422350843</code></strong>、<strong><code>1607745002</code></strong>、<strong><code>0086724882</code></strong>。</p> </td>
  </tr>
  <tr>
    <td><p>查詢字串中的SKU和類別ID。</p> </td>
    <td><p>錄制的快速檢視URL包括：</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>在此例中，URL中有兩個不同的部分。 SKU會儲存在<code>prodId</code>參數中，而類別ID會儲存在<code>category=</code>參數中。</p> <p>因此，縮圖定義是成對的。 即SKU值和名為<code>categoryId</code>的額外變數。 產生的對如下：</p>
    <ul>
      <li>SKU為<code>305466</code>，而<code>categoryId</code>為 <code>1100004</code></li>
      <li>SKU為<code>310181</code>，而<code>categoryId</code>為 <code>1100004</code></li>
      <li>SKU為<code>308706</code>，而<code>categoryId</code>為 <code>1740148</code></li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**範例**

將上述方法套用至「範例」網站時，您的網頁會包含數個產品縮圖，每個產品縮圖都有一個「SEE MORE」按鈕：

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html)

啟動頁面上所有可用的產品快速檢視後，您會收到下列對後端提出的快速檢視要求清單：

* datafeed/candles-233396346.json
* datafeed/candles-233978050.json
* datafeed/candles-234024346.json
* datafeed/candles-234024356.json
* datafeed/candles-234024359.json
* datafeed/cushions-233939848.json
* datafeed/cushions-234019477.json
* datafeed/cushions-234019483.json
* datafeed/furniture-231747479.json
* datafeed/furniture-232625621.json
* datafeed/furniture-232625626.json
* datafeed/furniture-233939810.json
* datafeed/furniture-233939825.json
* datafeed/furniture-233939828.json
* datafeed/furniture-233939853.json
* datafeed/furniture-233940334.json
* datafeed/glassware-000064007.json
* datafeed/glassware-230722193.json
* datafeed/glassware-233916550.json
* datafeed/glassware-233916597.json

檢視伺服器呼叫，產品特定資訊只會出現在請求路徑中。 您也會注意到查詢字串完全未使用，並且涉及兩種不同的資料片段類型：

* 第一種是蠟燭，墊子，家具，玻璃器皿。 您可以將此稱為「產品類別」。
* 第二種類型是產品代碼，例如233916597。 您可以假設它是「產品SKU」。

有了這些資訊，整個快速檢視URL會有下列模式：

`/datafeed/$categoryId$-$SKU$.json`

根據此類分析，您可得出以下兩個變數用於縮圖：`categoryId`和`SKU`。

您現在可以上傳視訊及其相關的縮圖資產。

## （可選）建立互動式視訊檢視器預設集{#optional-creating-an-interactive-video-viewer-preset}

如果您要使用預設、現成可用的互動式視訊檢視器預設集類型`Shoppable_Video_dark`或`Shoppable_Video_light`，您可以略過此工作並繼續下一步。

在製作環境中點選縮圖時，會出現「快速檢視」對話方塊的預覽。

![chlimage_1-21](assets/chlimage_1-127.png)

您可以選擇建立自訂的互動式視訊檢視器預設集。 您可決定視訊播放器的樣式、互動式縮圖和視訊結尾的縮圖格線檢視。

互動式視訊檢視器預設集會正確呈現您新增的視訊和所有時間軸區段。 當您在「預覽」模式中按一下產品縮圖時，也會使用預設的「快速檢視」範例，讓您在發佈前先測試其互動性。

儲存檢視器預設集後，其狀態會在「檢視器預設集」頁面中自動設為**On **。此狀態表示在動態媒體元件中及您使用它預覽視訊時，都可看到它。請確定您也手動發佈新的檢視器預設集。

請參閱[建立新檢視器預設集](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset)以建立您自己的互動式視訊檢視器預設集。

## 上傳視訊及其相關縮圖資產 {#uploading-a-video-and-its-associated-thumbnail-assets}

如果您已上傳視訊和縮圖資產，請繼續[為視訊新增互動功能](#adding-interactivity-to-your-video)。

如果您上傳的視訊或影像不正確，或您想要刪除已上傳的視訊或影像，請參閱[刪除資產](/help/assets/manage-digital-assets.md#delete-assets)。

若要上傳視訊及其相關縮圖資產：

1. 將視訊和相關的縮圖資產上傳至您想要的檔案夾或檔案夾。

   請參閱[上傳資產](/help/assets/manage-digital-assets.md)。
請參閱[使用FTP工作排程來上傳資產](/help/assets/manage-digital-assets.md)。

   現在，為您的視訊加入互動功能。

## 將互動功能加入影片{#adding-interactivity-to-your-video}

您可使用「建立互動式視訊」頁面上的就地視覺編輯器，將時間軸區段新增至視訊。

新增時間軸區段後，您會在每個區段中新增縮圖影像。 針對您新增的每個縮圖，您都會套用動作。 例如，您可以套用快速檢視至縮圖，或指派超連結至縮圖，或指派體驗片段。

請參閱[體驗片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)。

>[!NOTE]
當您將檢視器內嵌在「體驗片段」時，不支援「互動式視訊」中的社交媒體分享工具。 您可以改用或建立沒有社交媒體分享工具的檢視器預設集。 這些檢視器預設集可讓您成功將它內嵌在「體驗片段」中。

>[!NOTE]
如果您的互動式內容具有相對URL的連結，尤其是「Experience Manager網站」頁面的連結，則無法使用以URL為基礎的連結方法。

在目前的建立／編輯作業階段中，支援在頁面右上角的「復原」和「重做」選項。

儲存互動式視訊後，視訊會立即開啟至「預覽」。 您可以從中選取互動式視訊檢視器預設集，並播放視訊，以大致呈現它對客戶的呈現方式。

**若要在視訊中加入互動功能：**

1. 在「資產」檢視中，導覽至您上傳並想要製作互動式影片。
1. 執行下列任一項作業：

   * 將滑鼠指標暫留在影像上，然後點選&#x200B;**[!UICONTROL 選擇]**（勾選圖示）。 在工具列上，點選&#x200B;**[!UICONTROL 編輯]**。

   * 將滑鼠指標暫留在影像上，然後點選「更多動作」]**（三點圖示）**[!UICONTROL >「編輯」]**。**[!UICONTROL 

   * 若要在「詳細資料檢視」頁面中開啟影像，請點選影像。 在工具列中，點選&#x200B;**[!UICONTROL 編輯]**。

1. 在「建立互動式視訊」頁面上，執行下列任一項作業：

   * 若要開始播放視訊，請點選&#x200B;**[!UICONTROL Play]**&#x200B;按鈕。 當您要反白顯示的特定產品、服務或詳細資訊出現在檢視中時，點選工具列上的「新增區段」。 ****&#x200B;重複，直到您到達視訊結束為止。

      您可以針對您新增的每個時段，指派一或多個縮圖影像給該時段。 然後，您可以將這些縮圖連結至「快速檢視」產品頁面，供客戶購買，或連結至網頁，以取得詳細資訊。

   * 若要開始播放視訊，請點選&#x200B;**[!UICONTROL Play]**&#x200B;按鈕。 當您要反白顯示的特定產品、服務或詳細資訊出現在檢視中時，點選&#x200B;**[!UICONTROL Pause]**。 點選&#x200B;**[!UICONTROL 新增區段]**。

      在您要新增區段的時間軸上，繼續播放和暫停視訊，直到視訊結束為止。

1. （可選）向左拖曳&#x200B;**[!UICONTROL 時間軸縮放滑桿]**&#x200B;上的橫條，以放大或向右縮小。 此動作可讓您控制您看到新增之區段的詳細程度。

   ![chlimage_1-22](assets/chlimage_1-128.png)

   視視訊的長度而定，「區段持續時間」預設值如下：

   <table>
      <tbody>
        <tr>
        <td><strong>如果視訊長度是……</strong></td>
        <td><strong>「區段持續時間」設定預設為……</strong></td>
        </tr>
        <tr>
        <td>3分鐘以上</td>
        <td>60秒</td>
        </tr>
        <tr>
        <td>2-3分鐘</td>
        <td>30秒</td>
        </tr>
        <tr>
        <td>1-2 分鐘</td>
        <td>20秒<br /> </td>
        </tr>
        <tr>
        <td>30-60秒</td>
        <td>10秒</td>
        </tr>
        <tr>
        <td>30秒或更短</td>
        <td>5秒</td>
        </tr>
      </tbody>
    </table>

   視訊時間軸使用的螢幕空間和可用的空間一樣多。 因此，當您調整瀏覽器大小時，您新增的區段會維持其正確寬度。

   為了說明，以下三個螢幕擷取畫面使用相同的影片。 請注意，每個區段的寬度會依時間軸縮放設定而改變。

   ![chlimage_1-23](assets/chlimage_1-129.png)

   螢幕擷取A

   以上螢幕擷取A顯示29秒產品視訊的預設檢視。 時間軸比例預設為5秒。

   ![chlimage_1-130](assets/chlimage_1-130.png)

   螢幕擷取B

   在上述的螢幕擷取B中，「時間軸縮放」滑桿從預設的5秒拖曳至3秒。 請注意，個別時間軸縮放時間戳記現在都是以3秒間隔設定。

   ![chlimage_1-25](assets/chlimage_1-131.png)

   螢幕擷取C

   在上述的螢幕擷取C中，「時間軸縮放」設定已移至8秒。 請注意，包含產品縮圖的區段已縮小。 如果您有長視訊，而且想要看到通常符合頁面寬度的更多區段的概述，以這種方式縮小影片會很有用。

1. （可選）執行下列任一項作業：

   * 調整區段的開始時間和結束時間。

      選取區段，然後分別拖曳前導或尾隨藍色橢圓以調整開始或結束時間。 顯示的視訊影格會根據您的調整，移至視訊中的適當時間。 時間軸段的移動基於時間軸中的任何相鄰段進行限制。 允許的最小區段時間為1秒。

      使用下列導覽捷徑，快速檢查並微調您的視訊區段：

      * 若要直接在該區段的開頭尋找視訊，請點選前導的藍色橢圓。
      * 若要直接在該區段的尾端尋找視訊，請點選結尾的藍色橢圓。
      * 若要將視訊播放傳回至該區段的開頭，請點選整個區段。

   ![chlimage_1-26](assets/chlimage_1-132.png)

   重新定位時間軸段的結尾

   * 若要刪除區段

      選取時間軸上的最後一個區段，然後在工具列上，點選「刪除區段」**[!UICONTROL 。]**&#x200B;如果選取了兩或多個區段，「刪除區段」功能會停用。

      您只能刪除最後一個區段。 例如，如果您想要刪除時間軸上的所有區段，您必須一律選取最後一個區段，然後點選「刪除區段」**[!UICONTROL 。]**


1. 選取您要關聯一或多個縮圖影像的時段。
1. 在視訊右側，點選「**[!UICONTROL Content]**」標籤。
1. 在「內容」標籤下，點選「**[!UICONTROL 選擇資產]**」，然後瀏覽並選取您要用於視訊的所有影像資產。 選取的資產會新增至「內容」索引標籤中的「資產選擇器」面板。

1. 在「內容」標籤下方的資產選擇器中，執行下列任一項作業：

   <table>
      <tbody>
        <tr>
        <td>將縮圖與所選時間軸段關聯</td>
        <td><p>在右側的資產選擇器面板中點選影像。</p> <p>您可以新增任意數量的縮圖至時間軸區段。 對於您選取的每個影像，資產選取器中的影像上會出現核取標籤。</p> </td>
        </tr>
        <tr>
        <td>要從所選時間軸段中刪除縮略圖，請執行以下操作：</td>
        <td><p>執行下列任一操作：</p>
          <ul>
          <li>在資產選擇器面板中，點選含有核取標籤的影像以取消選取它。 影像資產會從時間軸區段中移除。<br /> </li>
          <li>在選取的時間軸區段中，點選影像，然後在工具列上，點選「刪除產品」<strong>。</strong></li>
          </ul> </td>
        </tr>
      </tbody>
    </table>

   ![資產選擇器](assets/chlimage_1-133.png)

   點選資產選取器面板中的影像會將其新增至選取的時間軸區段。

1. 在其中一個時間軸區段中選取單一縮圖影像，然後點選「動作&#x200B;****」標籤。
1. 執行下列任一操作：
   <table> 
    <tbody> 
      <tr> 
      <td>將選取的縮圖影像與快速檢視建立關聯</td> 
      <td><p>在「Action Type（操作類型）」下，按一下「Quick view（快速查看）」 <strong>。</strong></p> <p>如果您是Experience Manager網站和電子商務客戶：</p> 
       <ul> 
       <li>請注意，「SKU值」文字欄位已預先填入所選產品的SKU（庫存保留單位）。 SKU是您提供之每個不同產品或服務的唯一識別碼。 當影像與Experience Manager商務中的產品相關聯時，會自動填入此欄位。</li> 
       <li>如果預先填入的SKU不正確，請點選或按一下「產品選擇器」圖示（放大鏡）以開啟「選擇產品」頁面。 點選您要使用的產品，然後點選頁面右上角的核取標籤。 您會返回互動式視訊編輯器。</li> 
       </ul> <p> 如果您<em>not</em>是Experience Manager網站或電子商務客戶</p> 
       <ul> 
       <li>請參閱<a href="/help/assets/dynamic-media/carousel-banners.md#identifying-hotspot-and-image-map-variables">識別熱點變數</a>。 必須定義這些變數。</li> 
       <li>依預設，此SKU欄位會使用影像資產的檔案名稱，但不含副檔名。 如果您根據SKU遵循檔案的標準命名慣例，則此欄位通常不需要進行任何其他編輯。 </li> 
       <li>否則，請編輯預設值並輸入正確的SKU值。 在「SKU值」文字欄位中，輸入產品的SKU（庫存保留單位），此為您提供之每個不同產品或服務的唯一識別碼。 輸入的SKU值會自動填入「快速檢視」範本的變數部分，讓系統知道將點選的影像與特定SKU的「快速檢視」產生關聯。</li> 
       </ul> <p>（可選）如果快速檢視中有其他變數必須用來進一步識別產品，請點選<strong>新增一般變數</strong>。 在文字欄位中，指定額外的變數。 例如，<code>category=Womens</code>是新增的變數。</p> <p> </p> </td> 
      </tr> 
      <tr> 
      <td>將選定的縮圖影像與超連結關聯</td> 
      <td><p>在「動作類型」下，點選「<strong>超連結</strong>」，然後執行下列其中一項作業：</p> 
       <ul> 
       <li>如果您是Experience Manager網站客戶，請點選網站選擇器圖示（資料夾）以導覽至網頁。 如果您的互動式內容具有相對URL的連結，尤其是「Experience Manager網站」頁面的連結，則無法使用以URL為基礎的連結方法。</li> 
       <li>如果您是獨立的Dynamic Media客戶，請在HREF文字欄位中，指定連結網頁的完整URL路徑。</li> 
       </ul> <p>請確定您要指定是在新瀏覽器標籤中或在目前標籤中開啟連結。</p> </td> 
      </tr> 
      <tr> 
      <td>將選取的縮圖影像與體驗片段建立關聯</td> 
      <td><p>在「動作類型」下，點選「體驗片段」，然後執行下列動作：<strong></strong><p> 
       <ul> 
       <li>如果您是Experience Manager網站客戶，請點選「搜尋」圖示（放大鏡）以開啟「體驗片段」頁面。 點選或按一下您要使用的體驗片段，然後點選<strong>若要返回上一頁的「動作」面板，請在頁面右上角選取</strong>。<br /> 請參閱 <a href="/help/sites-cloud/authoring/fundamentals/experience-fragments.md">體驗片段</a>。</li> 
      </ul> 
       <ul> 
       <li>指定「體驗片段」在視訊上顯示的寬度和高度。</li>
       </ul><strong>注意</strong>:當您將檢視器內嵌在「體驗片段」時，不支援「互動式視訊」中的社交媒體分享工具。您可以改用或建立沒有社交媒體分享工具的檢視器預設集。 這些檢視器預設集可讓您成功將它內嵌在「體驗片段」中。</p></tr>&lt;&gt; 
      <tr> 
      <td>若要編輯已指派給縮圖影像的動作</td> 
      <td>在時間軸區段中，點選文字標籤右側有連結的縮圖影像。 連結指示已為其指派操作。 若要進行變更，請點選<strong>動作</strong>標籤。</td> 
      </tr> 
      <tr> 
      <td>若要變更縮圖影像的文字標籤</td> 
      <td><p>依預設，文字標籤會使用縮圖影像的<code>Title</code>中繼資料欄位。 如果<code>Title</code>不存在，則會改用縮圖影像的檔案名稱，但不使用副檔名。</p> <p>若要變更縮圖影像的文字標籤，請在顯示影像資產正下方的<strong>動作</strong>標籤下，輸入所要的文字。 請參閱下圖。</p> <p>新文字標籤僅供視訊播放器本身及顯示在時間軸區段中的縮圖文字使用。 標籤變更不會影響縮圖影像的「標題」中繼資料欄位，也不會影響其檔案名稱。</p> </td> 
      </tr> 
      <tr> 
      <td>恢復更改</td> 
      <td>在頁面的右上角附近，點選「<strong>還原</strong>」或「<strong>重做</strong>」。</td> 
      </tr> 
    </tbody> 
   </table>

   ![experiencefragment_interactivevideos](assets/experiencefragment_interactivevideos.png)

   縮圖影像會新增一個文字標籤。

1. 執行下列任一項作業：

   * 重複步驟6-11，將更多縮圖影像新增至影片中的時間軸區段。
   * 繼續選擇步驟13。

1. （可選）執行下列任一項作業：

   * **[!UICONTROL 合併區段]** -您可以將兩個相鄰的區段（無論是否已指派產品縮圖）合併為一個區段。

      在時間軸上，點選兩或多個要合併為一個的連續區段。 在下方的影像中，兩個選取的區段上沒有藍色的橢圓形拖曳控點。

      點選工具列上的「合併區段」。****
   ![chlimage_1-134](assets/chlimage_1-134.png)

   將兩個選取的五秒區段合併為一個十秒區段。

   * **[!UICONTROL 分割區段]** -您可以將單一區段分割為兩個等時的區段。如果已將產品縮圖指派給區段，則縮圖會合併到左側區段。

      在時間軸上，點選您要分成兩半的區段，然後點選工具列上的「分割區段」。****

      選取兩個或多個區段會停用「分割區段」功能。****
   ![chlimage_1-135](assets/chlimage_1-135.png)

   將選取的10秒區段分割為兩個區段，每個區段5秒。

1. 在&#x200B;**[!UICONTROL 建立互動式視訊]**&#x200B;頁面的右上角，會顯示目前選取的與視訊搭配使用的檢視器預設集名稱。 若要選取不同的檢視器預設集，請點選名稱。

   例如，`Shoppable_Video_light`檢視器預設集可讓您播放視訊旁有白色顯示區域的視訊。 顯示區域是播放期間可點選縮圖影像的顯示區域。 `Shoppable_Video_dark`檢視器預設集可讓您在視訊旁以黑色顯示區域播放視訊。

   如果您建立了自己的互動式視訊檢視器預設集，您可以在預設集清單中看到它，您可以從中選擇。

   完成後，點選&#x200B;**[!UICONTROL Save]**。

   >[!NOTE]
   當您儲存互動式視訊時，會自動 `.vtt` 儲存相關的檔案。`.vtt`檔案會儲存至&#x200B;**[!UICONTROL Assets]**&#x200B;根目錄的`_VTT`檔案夾。 您的互動式視訊必須有檔案和資料夾才能在網站上正確播放。因此，請勿移動、編輯或刪除資料夾 `_VTT` 或其內容。

1. 發佈互動式視訊。 發佈會建立內嵌代碼或URL，您最終會將其複製並貼至您的網站體驗。

   如果您使用快速檢視新增互動功能，則只使用內嵌程式碼；如果您使用超連結網頁新增互動功能，也可以使用發佈的URL。 但請注意，如果您的互動式內容具有相對URL的連結，尤其是Experience Manager網站頁面的連結，則無法使用以URL為基礎的連結方法。

   請參閱[發佈資產](publishing-dynamicmedia-assets.md)。

   >[!NOTE]
   若要發佈具有快速檢視功能的可購物視訊，請確定您也會從您的商務區個別發佈視訊的相關影像資產。

   新增時間軸區段並發佈互動式視訊後，您就可將它新增至現有的網站登陸頁面。 請參閱[將互動式視訊與您的網站整合](#integrating-an-interactive-video-with-your-website)。

## 發佈互動式視訊資產{#publishing-interactive-video-assets}

如需如何發佈互動式視訊資產的詳細資訊，請參閱[發佈資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

## 將互動式視訊與您的網站{#integrating-an-interactive-video-with-your-website}整合

在您上傳視訊、新增時間軸區段至該視訊並發佈互動式視訊後，您現在可以將它新增至現有網站。

如果您是Experience Manager網站客戶，可將互動式媒體元件拖曳至您的頁面，以新增互動式視訊。 請參閱[將Dynamic Media資產新增至Pages](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)。

如果您是獨立的Experience Manager資產客戶，您可以依本節所述手動將互動式視訊新增至網站。

1. 複製已發佈的互動式視訊的內嵌程式碼或URL。
請參閱[將視訊或影像檢視器內嵌至網頁](/help/assets/dynamic-media/embed-code.md)。
如果您使用快速檢視新增互動功能，則只使用內嵌程式碼；如果您使用超連結網頁新增互動功能，也可以使用發佈的URL。 但請注意，如果您的互動式內容具有相對URL的連結，尤其是Experience Manager網站頁面的連結，則無法使用以URL為基礎的連結方法。

1. 在目標的網頁程式碼中，識別靜態視訊的位置。
1. 移除靜態視訊，並以您從「Experience Manager資產」複製的內嵌程式碼或URL取代程式碼。
複製的嵌入代碼被設定用於響應性環境，因此它自動適應先前由靜態視頻佔用的區域。

>[!NOTE]
此時，如果您只新增超連結網頁的互動功能，就完成了。
不過，如果您新增任何互動功能來觸發快速檢視，互動視訊旁的縮圖僅供顯示之用；它們尚未與您現有的快速檢視整合。 在這種情況下，您必須將互動式視訊與網站上現有的快速檢視整合。

**範例**

以示範網站為例：

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html)

請注意，視訊內嵌代碼是標準的：

```xml
<style type="text/css">
 #s7video_div.s7videoviewer{
   width:100%;
   height:auto;
 }
</style>

<script type="text/javascript" src="https://demos-pub.assetsadobe.com/etc/dam/viewers/s7viewers/html5/js/VideoViewer.js"></script>
<div id="s7video_div"></div>
<script type="text/javascript">
 var s7videoviewer = new s7viewers.VideoViewer({
  "containerId" : "s7video_div",
  "params" : {
   "serverurl" : "https://adobedemo62-h.assetsadobe.com/is/image",
   "contenturl" : "https://demos-pub.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Video",
   "config2": "/etc/dam/presets/analytics",
   "videoserverurl": "https://gateway-na.assetsadobe.com/DMGateway/public/demoCo",
   "posterimage": "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4",
   "asset" : "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4" }
 }).init();
</script>
```

整合就像移除視訊內嵌程式碼，並從Experience Manager中取代互動式視訊內嵌程式碼一樣簡單。 您可在下列URL中看到結果。 雖然它會在頁面上顯示互動式視訊，但尚未與現有的快速檢視整合：

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-1.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-1.html)

## 將互動式視訊與現有的快速檢視整合{#integrating-an-interactive-video-with-an-existing-quickview}

>[!NOTE]
此任務僅在您是獨立Experience Manager資產客戶時才適用。

此程式的最後一個步驟是將互動式視訊與網站上使用的現有快速檢視實施整合。 沒有適合所有情況的整合解決方案。 每個快速檢視實作都是獨一無二的。 因此，需要一種需要前端IT人員協助的具體方法。

現有的快速檢視實作通常代表一連串的相關動作，這些動作會依下列順序出現在網頁上：

1. 使用者會在您網站的使用者介面中觸發元素。
1. 前端程式碼會根據步驟1中觸發的使用者介面元素，取得快速檢視URL。
1. 前端程式碼會使用步驟2AJAX中取得的URL來傳送要求。
1. 後端邏輯會將對應的快速檢視資料或內容傳回前端程式碼。
1. 前端程式碼會載入快速檢視資料或內容。
1. 或者，前端程式碼會將載入的快速檢視資料轉換為HTML表示法。
1. 前端程式碼會顯示模式對話方塊或面板，並轉譯HTML內容給使用者。

這些呼叫不代表可由網頁邏輯從任意步驟呼叫的獨立公用API呼叫。 相反地，它是連結呼叫，在此連結呼叫中，前一個步驟的最後一個階段（回呼）中將隱藏下一個步驟。

在互動式視訊取代步驟1和部分步驟2的同時，當使用者點選互動式視訊中的縮圖時，檢視器會處理這些使用者互動。 檢視器會將事件傳回至網頁，其中包含先前新增至Experience Manager的所有縮圖資料。

在此類事件處理常式中，前端程式碼會執行下列動作：

* 監聽互動式視訊所發出的事件。
* 根據縮圖資料建構快速檢視URL。
* 觸發從後端載入快速檢視並在螢幕上顯示的程式。

此外，互動式視訊檢視器支援全螢幕作業模式。 一般使用者只要按一下縮圖，就會觸發「快速檢視」，而不需離開全螢幕。 若要實現此功能，請變更前端程式碼，讓「快速檢視」強制回應對話方塊附加至檢視器的容器。 請勿新增檢視器處於全螢幕模式時無法使用的檔案BODY或其他網頁元素。 執行此工作的程式碼會監聽在檢視器載入頁面後傳送的另一個檢視器回呼。

Experience Manager傳回的內嵌程式碼已有可供使用的事件處理常式。 如下列反白顯示的程式碼片段所示，會加上註解：

```xml
<style type="text/css">
 #s7interactivevideo_div.s7interactivevideoviewer{
   width:100%;
   height:auto;
 }
</style>
<script type="text/javascript" src="https://demos-pub.assetsadobe.com/etc/dam/viewers/s7viewers/html5/js/InteractiveVideoViewer.js"></script>

<div id="s7interactivevideo_div"></div>
<script type="text/javascript">
 var s7interactivevideoviewer = new s7viewers.InteractiveVideoViewer({
  "containerId" : "s7interactivevideo_div",
  "params" : {
   "serverurl" : "https://adobedemo62-h.assetsadobe.com/is/image",
   "contenturl" : "https://demos-pub.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Video_light",
   "config2": "/etc/dam/presets/analytics",
   "videoserverurl": "https://gateway-na.assetsadobe.com/DMGateway/public/demoCo",
   "interactivedata": "content/dam/_VTT/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4.svideo.vtt",
   "VideoPlayer.contenturl": "https://adobedemo62-h.assetsadobe.com/is/content",
   "asset" : "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4" }
 })
 /* // Example of interactive video event for quickview.
   s7interactivevideoviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku; //SKU for product ID
    //To pass other parameter from the hotspot, you need to add custom parameter during the hotspot setup as parameterName=value
    loadQuickView(sku); //Replace this call with your quickview plugin
    //Please refer to your quickviewer plugin for the quickview call
    },
"initComplete":function() {
    //--- Attach quickview popup to viewer container so popup will work in fullscreen mode ---
    var popup = document.getElementById('quickview_div'); // get custom quickview container
    popup.parentNode.removeChild(popup); // remove it from current DOM
    var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
    var inner_container = document.getElementById(sdkContainerId);
    inner_container.appendChild(popup); //Attach custom quickview container to viewer
    }
   });
 */
 s7interactivevideoviewer.init();
</script>
```

因此，只需取消上述反白顯示的程式碼片段的註解，並以特定網頁專用的程式碼取代虛擬處理常式主體即可。

標準內嵌程式碼中有兩個預設回呼處理常式：`quickViewActivate`和`initComplete`。 在檢視器中按一下縮圖時，會觸發`quickViewActivate`處理常式。 使用它將檢視器與快速檢視啟動邏輯整合。 當檢視器載入頁面時，`initComplete`處理常式只會觸發一次。 此處理常式可用來調整網頁DOM中的「快速檢視」對話方塊位置。

建立快速檢視URL的程式與識別本主題前面所涵蓋的縮圖變數的程式相反。 使用先前識別的快速檢視URL範例，您可以瞭解每種情況下如何建構快速檢視URL:

<table>
  <tbody>
  <tr>
    <td><p>單一SKU，可在查詢字串中找到</p> </td>
    <td><code class="code">s7interactivevideoviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/json?productId=" + inData.sku + "&amp;source=100";
      },
      });</code></td>
  </tr>
  <tr>
    <td>單一SKU，位於URL路徑中</td>
    <td><code class="code">s7interactivevideoviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/product/" + inData.sku;
      },
      });</code></td>
  </tr>
  <tr>
    <td><p>查詢字串中的SKU和類別ID</p> </td>
    <td><code class="code">s7interactivevideoviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;prodId=" + inData.sku;
      },
      });</code></td>
  </tr>
  </tbody>
</table>

觸發快速檢視URL並啟動快速檢視面板的最後一個步驟，很可能需要IT部門的前端IT人員協助。 他們具備最佳的知識，瞭解如何從正確的步驟精確觸發快速檢視實作，並擁有現成可用的快速檢視URL。

您可以瞭解這些步驟如何套用至示範網站，以將互動式視訊與快速檢視程式碼完全整合。 在本主題的前面，快速檢視URL的結構已識別為：

```xml
/datafeed/$CategoryId$-$SKU$.json
```

使用`categoryId`和`sku`物件中可用的欄位，透過檢視器程式碼傳遞至處理常式，輕鬆在`quickViewActivate`處理常式中重建此URL，如下所示：`inData`

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

示範網站會使用簡單的`loadQuickView()`函式呼叫來觸發「快速檢視」對話方塊。 此函式只使用一個引數，即快速檢視資料URL。 因此，整合互動式視訊的最後一個步驟是將下列程式碼行新增至`quickViewActivate`處理常式：

```xml
loadQuickView(quickViewUrl);
```

最後，請確定您的「快速檢視」對話方塊已附加至檢視器的容器元素。 內嵌程式碼預設值提供實現此功能的範例步驟。 若要取得檢視器容器元素的參考，您可以使用下列程式碼行：

```xml
var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
var inner_container = document.getElementById(sdkContainerId);
```

其中，`inner_container`是檢視器所管理之`DIV`元素的參考。 您希望該對話框是該`DIV`的子項。

實際定位模態對話框元素並將其附加到上述容器的步驟是按大小寫進行的。 同樣地，您也可以向熟悉您所需之快速檢視實作的前端開發人員尋求協助。

對於示例網站，「快速查看模式」對話框實施為`DIV`，其快速查看模式ID直接附加到文檔`BODY`。 因此，將該對話方塊移至檢視器容器的程式碼與下列程式碼一樣簡單：

```xml
var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
var inner_container = document.getElementById(sdkContainerId);
inner_container.appendChild(document.getElementById("quickview-modal"));
```

完整的原始碼如下：

```xml
<style type="text/css">
 #s7interactivevideo_div.s7interactivevideoviewer{
   width:100%;
   height:auto;
 }
</style>
<script type="text/javascript" src="https://demos-pub.assetsadobe.com/etc/dam/viewers/s7viewers/html5/js/InteractiveVideoViewer.js"></script>

<div id="s7interactivevideo_div"></div>
<script type="text/javascript">
 var s7interactivevideoviewer = new s7viewers.InteractiveVideoViewer({
  "containerId" : "s7interactivevideo_div",
  "params" : {
   "serverurl" : "https://adobedemo62-h.assetsadobe.com/is/image",
   "contenturl" : "https://demos-pub.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Video_light",
   "videoserverurl": "https://gateway-na.assetsadobe.com/DMGateway/public/demoCo",
   "interactivedata": "content/dam/_VTT/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4.svideo.vtt",
   "VideoPlayer.contenturl": "https://adobedemo62-h.assetsadobe.com/is/content",
   "asset" : "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4" }
 })
 // Example of interactive video event for quickview.
   s7interactivevideoviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku; //SKU for product ID
     var categoryId=inData.categoryId; //categoryId
    var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
    loadQuickView(quickViewUrl);
    },
   "initComplete":function() {
    //--- Attach quickview popup to viewer container so popup will work in fullscreen mode ---
    var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
    var inner_container = document.getElementById(sdkContainerId);
    inner_container.appendChild(document.getElementById("quickview-modal"));
    }
   });
 s7interactivevideoviewer.init();
</script>
```

完整整合互動式影片的最終示範網站如下所示：

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-3.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-3.html)

## 使用快速檢視建立自訂快顯視窗® {#using-quickviews-to-create-custom-pop-ups}

請參閱[使用快速檢視建立自訂快顯視窗Windows®](/help/assets/dynamic-media/custom-pop-ups.md)。
—>
