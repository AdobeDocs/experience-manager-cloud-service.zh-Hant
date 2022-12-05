---
title: 進入Dynamic Media，第二部分
description: Dynamic Media歷程涵蓋Dynamic Media的基本概念、運作方式、可為您做什麼，以及為您的工作和客戶帶來哪些價值。
contentOwner: Rick Brough
products: Experience Manager as a Cloud Service
topic-tags: introduction,administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
hide: false
hidefromtoc: false
exl-id: cdca41ad-a2cd-4f68-aaa4-5eec33c30f0b
source-git-commit: 9e425601c493740050d61e8025ea3f9e3dbdc4d8
workflow-type: tm+mt
source-wordcount: '2902'
ht-degree: 0%

---

# Dynamic Media歷程：基本知識，第二部分  {#dm-journey-part2}

歡迎使用Dynamic Media歷程：基本知識，第二部分，您可以期望了解以下內容：

* Dynamic Media URL及Dynamic Media如何傳遞內容的解剖
* 建立影像預設集以轉譯資產的基本知識
* 影像集、回轉集和混合媒體集

另請參閱 [Dynamic Media歷程；基本知識，第一部分](/help/assets/dynamic-media/dm-journey-part1.md).

>[!TIP]
>
>為獲得最佳結果，Adobe建議您在桌上型電腦上閱讀並檢視此Dynamic Media歷程。

## Dynamic Media URL及Dynamic Media如何傳遞內容的解剖 {#dm-journey-d}

上傳和發佈Dynamic Media資產後，您可以複製資產產生的URL，並貼到瀏覽器中，以查看資產對客戶的呈現方式。 以下監看影像的複製URL會依顏色劃分，以方便閱讀和理解。

![Dynamic Media URL解剖](/help/assets/dynamic-media/assets/dm-colored-url.png)
_Dynamic Media URL的解剖。_

紅色URL的第一部分是參考伺服器網域本身。 在此情況下，Dynamic Media會在一般伺服器網域上執行， `https://s7d1.scene7.com/is/image/`. 只要查看伺服器網域，您就能輕鬆查看一組影像，並了解這些影像是否是由Dynamic Media提供。 URL會相當一致。 不過，有些Dynamic Media客戶已切換至專用的伺服器網域，而可能是 `name-of-your-company.scene7.com`. 智慧映像需要專用的伺服器域。

帳戶名稱是紫色的部分。 在此情況下，帳戶稱為 `jpearldemo`.

資產ID或名稱， `AdobeStock_28563982` 為綠色。 請注意，資產已 _no_ 檔案副檔名，例如 `.png` 或 `.jpg`. 將資產擷取至Dynamic Media時，會移除副檔名，並建立不同類型的檔案：金字塔TIFF檔案。 吡唑TIFF可讓Dynamic Media快速建立轉譯。

最後，還有一些影像處理參數， `?wid=1000&fmt=jpeg&qlt=85`，在結尾以黃色顯示。

整個URL路徑為即時狀態。 [試試看](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982?wid=1000&amp;fmt=jpeg&amp;qlt=85){target=&quot;_blank&quot;}。

在您的瀏覽器視窗仍開啟至Dynamic Media URL和監看影像時，我們將進一步了解您如何只變更URL即可建立影像轉譯。

### 透過URL轉譯監看影像

首先，請僅手動刪除URL路徑中的影像處理規則；保留伺服器名稱、帳戶名稱，以及資產ID或影像名稱。 [試試看](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982){target=&quot;_blank&quot;}。

現在將影像處理參數新增至URL的結尾。 在URL欄位中，在影像名稱的右側，輸入 `?wid=500`，然後按 **[!UICONTROL 輸入]**. [試試看](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=500){target=&quot;_blank&quot;}。

請注意，手錶的新轉譯已產生。 要從這個改變影像寬度的簡單練習中了解這一點，關鍵在於所看到的影像是動態100%產生的。

現在變更的寬度值 `500` 像素到 `1000` 像素，然後按 **[!UICONTROL 輸入]**. [試試看](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000){target=&quot;_blank}。
你按下 **[!UICONTROL 輸入]**，則瀏覽器會返回Dynamic Media Image Server。 它會根據您剛輸入的新寬度值，產生全新的手錶轉譯，然後將新影像傳回瀏覽器並快取。

Dynamic Media有許多影像處理參數，您可以用來微調網頁上的影像資產。 您可以 [在這裡看到一份清單](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html?lang=en).

現在，請嘗試將旋轉參數新增至監看影像。 URL路徑的結尾，緊接在後 `wid=1000`，類型 `&rotate=90`，然後按 **[!UICONTROL 輸入]**. [試試看](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000&amp;rotate=90){target=&quot;_blank&quot;}。

手錶的左邊還有點偏。 變更 `90` to `92`，然後按 **[!UICONTROL 輸入]**. [試試看](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000&amp;rotate=9){target=&quot;_blank&quot;}。

再說一遍，當你按下 **[!UICONTROL 輸入]**，手錶的新轉譯幾乎會即時產生。 您可以看到您獲得的效能，這說明為何Dynamic Media可以傳送超過800,000個影像要求， _每秒_，在繁忙的週末或大節日。

雖然您可以逐一影像在URL中變更影像處理參數，但這並非有效的方法，尤其是如果您的網站上有數萬個影像時。 使用影像預設集是更好的方法。

## 建立影像預設集以轉譯資產的基本知識 {#dm-journey-e}

您想要建立影像或讓影像可供使用的位置和方式有多種。 傳統上，創意素材會進入Adobe Photoshop，並將每個不同的轉譯儲存為靜態影像。

![靜態影像](/help/assets/dynamic-media/assets/dm-static-images.png)
_很好：靜態影像，每個影像都手動建立。_

想像一下創意Director看著照片說，

_「我真的想拍這張表，這樣大手指向四，小手指向1，讓手錶錶盤更容易看。」_

創意人員必須重新拍攝所有這些新的靜態影像。

但是，透過Dynamic Media，如果您有不同的影像預設集，則可以在需要時使用這些影像。 影像預設集強制執行標準。

![主要檔案方法](/help/assets/dynamic-media/assets/dm-onefile.png)
_最佳：使用影像預設集即時建立一個檔案，其中包含多個轉譯，例如 `Search_Grid` 和 `Thumbnail`._

| **為何使用影像預設集？** |  |
|---|---|
| 標準 | 影像預設集會對隨請求的任何影像強制執行標準影像處理。 |
| 變更管理 | 如果您必須變更影像處理，只需編輯現有影像預設集的參數即可。 更新的定義會自動傳播至所有請求。 |

您需要特定影像類型的每個位置，例如，

* 產品詳細資訊頁面，
* 搜索網格，
* 縮圖，
* 購物卡，或
* 主圖影像

無論影像要使用的位置，您都希望以相同的參數傳送該影像。

現在來看看影像預設集在Dynamic Media中的建立方式。

![從「基本」標籤開始建立影像預設集](/help/assets/dynamic-media/assets/dm-image-preset-basictab.png)
_從「基本」標籤開始建立影像預設集。_

在上例中，您可以看到已使用名稱建立新的影像預設集 _中_. Dynamic Media使用現成可用的影像（背包）範例，協助您在建立影像預設集時查看影像特性。

此 _中_ 影像預設集的寬度為500像素，高度為800像素。 在此歷程的第一部分，您閱讀了有關以不同格式傳送資產的資訊。 從 **[!UICONTROL 格式]** 下拉式選單中，您可以選擇以JPEG、PNG、TIFF或數種其他格式傳送資產。 您在這裡有彈性。

選取 **[!UICONTROL 進階]** 索引標籤會提供資產的色域選項。 視您在 **[!UICONTROL 基本]** 標籤 — 在上例中，已選取「JPEG」 — 您可以以「RGB」、「灰階」或「CMYK」來傳送資產。 從 **[!UICONTROL 色彩描述檔]** 下拉菜單中，您可以選擇如何傳送要用於打印的CMYK影像資產。 另請注意，您可以套用其他參數來銳利化影像。 在這種情況下， **[!UICONTROL 不銳利化遮色片]** 已套用。

![從「進階」標籤選取選項，建立影像預設集](/help/assets/dynamic-media/assets/dm-image-preset-advancedtab.png)
_從「進階」標籤選取選項，建立影像預設集。_

你還記得 [Dynamic Media URL解剖](#dm-journey-d) 之前，您已閱讀Dynamic Media URL及其建置方式的相關資訊。 此 **[!UICONTROL 影像修飾元]** 文字方塊是您可以輸入任何其他影像處理參數的位置。 使用預設集傳送影像時，參數會包含在URL的預設集名稱中。 在上方的螢幕擷取中，參數 `bgc=451B15` 已新增。 即增加了深棕色背景顏色。

您可以將影像預設集視為影像的配方。 它會每次傳送使用預設集的影像，一致；會一樣的。 參數 `&op_brightness=+10` 也增加以稍微增加亮度。

完成後，您會儲存預設集，現在它可供您擁有的所有影像使用。 在此情況下，我們要套用 _中_ 一碗液態巧克力的影像。

![套用影像預設集 *中* 生成影像的格式副本](/help/assets/dynamic-media/assets/dm-medium-image-preset.png)
_應用影像預設集「介質」以生成影像的轉譯。_

您可以複製URL，然後貼到瀏覽器中以檢查影像外觀。 [試試看](http://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_74043302?$Medium$){target=&quot;_blank&quot;}。

在您的瀏覽器中，注意影像預設集的名稱 _中_ 填入完整URL路徑。

您可以看到影像中顯示的清晰度。 這種品質部分是因為一碗巧克力的拍攝方式。 另外，部分原因是使用Dynamic Media時，您可儲存比傳送至數位頻道更大的影像。

如果一碗巧克力的東西看起來都不錯，您就會將URL貼到您的網頁中，讓影像顯示在您的網站上。

如果您再次查看下方的監看影像，您會看到 `Cart` 影像預設集，a `Grid` 預設集，a `Large` 預設集，a `PDP-page` （產品詳細資料頁面）預設集，以及其他幾個預設集。

![靜態和動態影像預設集](/help/assets/dynamic-media/assets/dm-image-presets.png)
_靜態和動態影像預設集。 已使用 `PDP-page` 影像預設集。_

但是，如果您必須在網站上變更影像呢？ 例如，假設您已完成某些測試，發現影像為120 x 120( `Cart` 影像預設集)未如您所想般收到。 您必須將寬度增加為175像素，並將高度增加為175像素，以使影像更大。 傳統上，您必須前往Adobe Photoshop並重新建立所有這些購物車影像。 但使用Dynamic Media時，您只需將「寬度」和「高度」值更新為175即可編輯影像預設集，並儲存您的預設集，如下列範例所示。

![編輯影像預設集](/help/assets/dynamic-media/assets/dm-edit-image-preset.png)
_編輯寬度和高度 `Cart` 影像預設集。_

在您變更影像預設集並排清快取後，所有影像都會更新，以及該預設集使用的所有URL，請執行 _not_ 隨處皆可變更。 這表示不需要中斷的連結，也不需要網頁重新導向。

## 影像集、回轉集和混合媒體集 {#dm-journey-f}

Dynamic Media較常使用的功能包括建立影像集、回轉集和混合媒體集。

影像集通常由一系列影像資產組成，並以單一實體呈現。 這些類型的集合可為使用者提供整合的檢視體驗，讓使用者按一下縮圖影像即可看見項目的不同檢視。 影像集可讓您呈現某個項目的替代檢視，而檢視器提供縮放工具，供您仔細檢查影像。 [檢視使用彈出檢視器且稱為「執行中」的影像集](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running).

在Dynamic Media內，您會看到跑鞋的數個影像。 這是一個產品系列，銷售和營銷部門希望客戶將其視為單個演示文稿；影像集。

![建立影像集](/help/assets/dynamic-media/assets/dm-create-image-set.png)
_建立影像集的開始。_

要建立影像集，請選擇 **[!UICONTROL 影像集]** 從 **[!UICONTROL 建立]** 下拉式功能表。 注意功能表上也有建立 **[!UICONTROL 混合媒體集]**, **[!UICONTROL 回轉集]**&#x200B;和 **[!UICONTROL 轉盤集]**. 您建立這些集的方式與影像集的方式大致相同。

混合媒體集可包含影像、色票集、回轉集、視訊和最適化視訊集。 [試試看](https://s7d9.scene7.com/s7viewers/html5/MixedMediaViewer.html?asset=Scene7SharedAssets/Mixed_Media_Set_Sample). 回轉集模擬轉動物件的真實行為，以檢查物件。 回轉集可讓您從任何角度檢視關鍵視覺詳細資訊。 [試試看](https://s7d9.scene7.com/s7viewers/html5/SpinViewer.html?asset=Scene7SharedAssets/SpinSet_Sample&amp;stagesize=500,400){target=&quot;_blank&quot;}。

建立影像集是簡單明瞭的。 您只需新增要納入集合的影像資產。

![建立影像集](/help/assets/dynamic-media/assets/dm-create-image-set-add-assets.png)
_影像集編輯器可讓您新增影像資產，並重新排序其在集中的外觀。_

您必須為設定命名。 請謹慎選擇名稱，因為您以後無法編輯它！ 在上述範例中，此集稱為 `Running`. 完成後，會儲存集合。

這是 `Running` 影像集於Experience Manager Assets。

![在Experience Manager Assets中設定的執行中影像，卡片檢視](/help/assets/dynamic-media/assets/dm-image-set.png)
_此 `Running` 影像在Experience Manager Assets中設定，卡片檢視。_

無論您是已建立影像集、混合媒體集、回轉集或任何其他互動式媒體，在建立影像集後，您都想要了解該影像集對客戶的顯示和行為。 Dynamic Media有許多內建的檢視器，可讓您執行此操作。

首先，選取建置的影像集，以在預覽中開啟它，如以下範例所示。

![在預覽中設定的「正在運行」影像，並選擇「查看器」選項](/help/assets/dynamic-media/assets/dm-image-set-viewer.png)
_此 `Running` 在預覽中設定的影像已選取「檢視器」選項。_

請注意，在預覽中，您可以選取跑鞋色板，並在鞋上放大和縮小。 若要將檢視器套用至該集，請選取 **[!UICONTROL 檢視器]** 從下拉式功能表。

![已套用彈出檢視器的執行中影像集](/help/assets/dynamic-media/assets/dm-image-set-flyout-viewer.png)
_此 `Running` 已套用彈出檢視器的影像集。_

在此情況下， `Flyout` 已選取檢視器。 此時，您可以在檢視器中預覽影像集。 但是，最好在您的瀏覽器中查看，即客戶如何看到。 您選取 **[!UICONTROL URL]** 在左下方，複製URL並貼到您的瀏覽器中。 [試試看](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running&amp;config=jpearldemo/Flyout){target=&quot;_blank&quot;}。

單一URL可讓您使用網站上您需要的影像集和檢視器。 您可能已注意到上一個範例 **[!UICONTROL 內嵌]** 位於URL按鈕的右側。 選取 **[!UICONTROL 內嵌]**，您可以複製此影像集/檢視器的程式碼，然後將其新增至網頁或Experience Manager Sites元件。

Flyout檢視器是預設的現成檢視器，您可以編輯其屬性。 或者，就像建立影像預設集一樣，您可以建立自己的自訂檢視器。

假設您的銷售和行銷團隊不喜歡Flyout檢視器。 他們喜歡縮放功能，但希望客戶直接在鞋子上看到縮放效果。 在這種情況下，您只需將InlineZoom查看器應用到影像集，並複製其URL並貼到瀏覽器中，以了解其工作方式。 [試試看](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running&amp;config=jpearldemo/InlineZoom){target=&quot;_blank&quot;}。

當你將滑鼠指針移到鞋子上時，你放大到該影像，你可以看到更多細節，同時你移動指針。 原因只是影像的大小，最初上傳到Dynamic Media。

當你考慮作為消費者生活，或者當你在日常工作中工作，當你去不同的網站時，你會看到這樣的東西。 想想這是如何實現的，以及如何在你自己的工作和公司網站上運用Dynamic Media的力量。

你只是讀了一點關於影像集和觀眾。 讓我們看幾個其他檢視器，並在單一資產上試用。 若要重設檢視器，請按一下 **[!UICONTROL 重新整理]** 按鈕。

<!-- LEAVE THIS HIDDEN PATH IN THE DOCUMENTATION FOR DEMO PURPOSES [Flyout viewer with image set](http://www.partycity.com/girls-little-old-lady-costume-P750948.html) -->

* `ZoomVertical_dark` 檢視器已套用至影像資產。 [試試看](https://s7d1.scene7.com/s7viewers/html5/ZoomVerticalViewer.html?asset=jpearldemo/AdobeStock_96311480&amp;config=jpearldemo/ZoomVertical_dark){target=&quot;_blank&quot;}。
* `Zoom_light` 檢視器已套用至影像。 [試試看](https://s7d1.scene7.com/s7viewers/html5/BasicZoomViewer.html?asset=jpearldemo/AdobeStock_38827423&amp;config=jpearldemo/Zoom_light){target=&quot;_blank&quot;}。

## 選用 — 深入了解

如果您想要進一步了解剛才閱讀的內容，請使用下列材料，更詳細地探索概念。 否則，您的Dynamic Media歷程就會完成！

_Dynamic Media說明主題_

* [如何建立影像預設集](/help/assets/dynamic-media/image-presets.md)
* 清單 [影像處理參數](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html) 在建立影像預設集時，可在「影像修飾詞」欄位中使用
* [如何預覽資產](/help/assets/dynamic-media/previewing-assets.md)
* [如何預覽3D資產](/help/assets/dynamic-media/previewing-3d-assets.md)
* [如何建立影像集](/help/assets/dynamic-media/image-sets.md)
* [如何建立回轉集](/help/assets/dynamic-media/spin-sets.md)
* [如何建立混合媒體集](/help/assets/dynamic-media/mixed-media-sets.md)

_Dynamic Media教學課程_

* [將Dynamic Media與Experience Manager Assets搭配使用](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-overview-feature-video-use.html)
* [Adobe Experience Manager內容庫](https://experienceleague.adobe.com/?lang=en#recommended/solutions/experience-manager) (搜尋 _Dynamic Media_)

_Dynamic Media檢視器_

* [即時演示](https://landing.adobe.com/tw/na/dynamic-media/ctir-2755/live-demos.html) 每個檢視者

<!-- Live as of April 28 2022. LEAVE IN HERE https://landing.adobe.com/en/na/dynamic-media/ctir-2755/index.html -->