---
title: Dynamic Media歷程，第二部分
description: Dynamic Media歷程涵蓋Dynamic Media的基礎知識、運作方式、可為您做的事情，以及可為您的工作和客戶帶來的價值。
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
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '2870'
ht-degree: 0%

---

# Dynamic Media歷程：基礎知識，第二部分  {#dm-journey-part2}

歡迎使用Dynamic Media歷程：基礎知識，第II部分，您將可在此學習下列內容：

* Dynamic Media URL剖析，以及Dynamic Media如何提供內容
* 建立影像預設集以轉譯資產的基礎知識
* 影像集、迴轉集及混合媒體集

另請參閱 [Dynamic Media歷程；基礎知識，第一部分](/help/assets/dynamic-media/dm-journey-part1.md).

>[!TIP]
>
>為達到最佳效果，Adobe建議您透過桌上型電腦閱讀及檢視此Dynamic Media歷程。

## Dynamic Media URL剖析，以及Dynamic Media如何提供內容 {#dm-journey-d}

上傳和發佈Dynamic Media資產後，您可以複製資產產生的URL，並將其貼到瀏覽器中，以檢視向客戶呈現資產的方式。 下列鐘錶影像的複製URL會依顏色劃分，以便於閱讀和理解。

![Dynamic Media URL剖析](/help/assets/dynamic-media/assets/dm-colored-url.png)
_Dynamic Media URL剖析。_

URL紅色的第一部分是參照伺服器網域本身。 在此案例中，Dynamic Media是在一般伺服器網域上執行，也就是 `https://s7d1.scene7.com/is/image/`. 只要檢視伺服器網域，就能輕鬆檢視一組影像，並瞭解Dynamic Media是否提供這些影像。 URL將相當一致。 不過，有些Dynamic Media客戶已切換至專屬伺服器網域，網域可能設在 `name-of-your-company.scene7.com`. 智慧型影像需要專用的伺服器網域。

帳戶名稱是紫色的部分。 在此案例中，帳戶稱為 `jpearldemo`.

資產ID或名稱， `AdobeStock_28563982` 為綠色。 請注意，該資產已 _否_ 副檔名，例如 `.png` 或 `.jpg`. 將資產內嵌至Dynamic Media時，會移除副檔名，並建立其他型別的檔案：金字塔TIFF檔案。 金字塔TIFF可讓Dynamic Media即時快速建立轉譯。

最後，還有一些影像處理引數， `?wid=1000&fmt=jpeg&qlt=85`，結尾以黃色顯示。

整個URL路徑都是即時的。 [試試看](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982?wid=1000&amp;fmt=jpeg&amp;qlt=85){target="_blank"}.

在瀏覽器視窗仍開啟至Dynamic Media URL和監看影像的情況下，讓我們進一步瞭解您如何僅透過變更URL來建立影像的轉譯。

### 透過URL呈現監視影像

首先，請僅手動刪除URL路徑中的影像處理規則；保留伺服器名稱、帳戶名稱，以及資產ID或影像名稱。 [試試看](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982){target="_blank"}.

現在將影像處理引數新增至URL結尾。 在URL欄位中的影像名稱右側，輸入 `?wid=500`，然後按下 **[!UICONTROL 輸入]**. [試試看](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=500){target="_blank"}.

請注意，已產生新的手錶轉譯。 要瞭解這項變更影像寬度簡易練習，關鍵是要注意，看到的影像是100%以動態方式產生。

現在變更寬度值 `500` 畫素至 `1000` 畫素，然後按下 **[!UICONTROL 輸入]**. [試試看](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000){target="_blank}.
按下此鍵時 **[!UICONTROL 輸入]**，瀏覽器會返回Dynamic Media影像伺服器。 它會根據您剛輸入的新寬度值，產生全新的手錶轉譯，然後將新影像傳回瀏覽器，並加以快取。

Dynamic Media有許多影像處理引數，可用來微調網頁上的影像資產。 您可以 [在這裡檢視清單](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html?lang=en).

現在嘗試將旋轉引數新增到觀看影像。 和URL路徑的結尾，緊接在 `wid=1000`，型別 `&rotate=90`，然後按鍵 **[!UICONTROL 輸入]**. [試試看](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000&amp;rotate=90){target="_blank"}.

手錶還是稍微向左偏斜。 變更旋轉值 `90` 至 `92`，然後按鍵 **[!UICONTROL 輸入]**. [試試看](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000&amp;rotate=9){target="_blank"}.

同樣，當您按下 **[!UICONTROL 輸入]**，則會近乎即刻產生手錶的新轉譯。 您可以看到獲得的效能種類，因此說明Dynamic Media可以提供超過800,000個影像要求的原因， _每秒_、忙碌的週末或重大假日。

雖然您可以逐個影像變更URL中的影像處理引數，但這並非有效率的方法，尤其是如果您的網站包含數萬張影像時。 更好的方式是使用影像預設集。

## 建立影像預設集以轉譯資產的基礎知識 {#dm-journey-e}

有多種方法和位置可讓您建立影像或讓影像可供使用。 傳統上，創意會進入Adobe Photoshop，並將每個不同的轉譯儲存為靜態影像。

![靜態影像](/help/assets/dynamic-media/assets/dm-static-images.png)
_好：靜態影像，每個影像都是手動建立。_

現在，想像Creative Director看著影像說，

_「我真的很想要這個鏡頭，好讓大手指向四個，小手指向1，好讓錶盤更容易看見。」_

創意人員必須再次重新排列所有新的靜態影像。

但透過Dynamic Media，如果您有不同的影像預設集，您就可以隨處使用這些影像。 影像預設集會強制實施標準。

![主要檔案方法](/help/assets/dynamic-media/assets/dm-onefile.png)
_最佳：使用影像預設集即時建立具有多個轉譯的一個檔案，例如 `Search_Grid` 和 `Thumbnail`._

| **為何要使用影像預設集？** | |
|---|---|
| 標準 | 影像預設集會強制對其請求的任何影像執行標準影像處理處理。 |
| 變更管理 | 如果您必須變更影像處理，只要編輯現有影像預設集的引數即可。 更新的定義會自動傳播到所有請求。 |

您需要有特定影像型別的每個地方，例如：

* 產品詳細資料頁面，
* 搜尋格線，
* 縮圖，
* 購物卡，或
* 主圖影像

您想要在任何使用影像的地方，以相同的引數傳送影像。

讓我們先看看如何在Dynamic Media中建立影像預設集。

![從基本標籤開始建立影像預設集](/help/assets/dynamic-media/assets/dm-image-preset-basictab.png)
_從基本標籤開始建立影像預設集。_

在上述範例中，您可以看到已使用名稱建立新的影像預設集 _Medium_. Dynamic Media使用現成可用的影像（揹包）範例，協助您在建立影像預設集時檢視其特性。

此 _Medium_ 影像預設集的寬度為500畫素，高度為800畫素。 在此歷程的第一部分中，您已閱讀有關以不同格式傳送資產的資訊。 從 **[!UICONTROL 格式]** 從下拉式選單中，您可以選擇以JPEG、PNG、TIFF或數種其他格式傳送資產。 您可以靈活處理。

選取 **[!UICONTROL 進階]** 索引標籤會提供資產色域的選項。 根據您在 **[!UICONTROL 基本]** 標籤 — 在上述範例中，已選取JPEG — 您可以以RGB、灰階或CMYK傳送資產。 從 **[!UICONTROL 色彩設定檔]** 從下拉式選單中，您可以選取如何傳送要用於列印的CMYK影像資產。 也請注意，您可以套用其他引數來銳利化影像。 在這種情況下， **[!UICONTROL 不銳利化遮色片]** 中所有規則的URL區段。

![從「進階」標籤中選取選項，以建立影像預設集](/help/assets/dynamic-media/assets/dm-image-preset-advancedtab.png)
_從「進階」標籤中選取選項，以建立影像預設集。_

您記得在 [Dynamic Media URL剖析](#dm-journey-d) 先前版本，讓您瞭解有關Dynamic Media URL及其建置方式。 此 **[!UICONTROL 影像修飾元]** 您可以在此文字方塊中輸入任何其他所需的影像處理引數。 使用預設集傳送影像時，引數會包含在URL的預設集名稱中。 在上面的熒幕擷圖中，引數 `bgc=451B15` 「 」已新增。 也就是說，已新增深棕色背景顏色。

您可以將影像預設集視為影像的配方。 它將每次都持續傳送使用預設集的任何影像；都會一樣。 引數 `&op_brightness=+10` 也增加以稍微增加亮度。

完成後，您儲存了預設集，現在它可用於您擁有的所有影像。 在此案例中，我們要套用 _Medium_ 將影像預設為液體巧克力碗的影像。

![套用影像預設集 *Medium* 產生影像轉譯](/help/assets/dynamic-media/assets/dm-medium-image-preset.png)
_套用影像預設集「媒體」以產生影像的轉譯。_

複製URL，然後貼到瀏覽器中檢查影像的外觀。 [試試看](http://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_74043302?$Medium$){target="_blank"}.

在您的瀏覽器中，注意影像預設集的名稱 _Medium_ 在完整URL路徑中。

您可以看到影像中顯示的清晰度。 這種品質部分是由於這碗巧克力的拍攝方式。 此外，部分原因是因為使用Dynamic Media，您可以儲存比傳送至數位頻道更大的影像。

如果您的巧克力碗看起來一切正常，您就會將URL貼到您想讓影像出現在網站上的網頁。

如果您再看下方的手錶影像，可以看出有一個 `Cart` 影像預設集， a `Grid` 預設集， a `Large` 預設集， a `PDP-page` （產品詳細資料頁面）預設集和其他數個預設集。

![靜態和動態影像預設集](/help/assets/dynamic-media/assets/dm-image-presets.png)
_靜態和動態影像預設集。 已使用呈現監視影像 `PDP-page` 影像預設集。_

但如果您必須變更網站上的影像，該怎麼做？ 例如，假設您已進行一些測試，發現影像為120 x 120 (例如 `Cart` 影像預設集)，並未如您預期收到。 您必須將寬度增加至175畫素並將高度增加至175畫素，讓影像變大。 傳統上，您必須進入Adobe Photoshop並重新建立所有這些購物車影像。 但若使用Dynamic Media，只要將「寬度」和「高度」值更新為175，並儲存預設集即可編輯影像預設集，如下列範例所示。

![編輯影像預設集](/help/assets/dynamic-media/assets/dm-edit-image-preset.png)
_編輯的寬度和高度 `Cart` 影像預設集。_

在您變更影像預設集並清除快取後，所有影像都會更新，且與該預設集搭配使用的所有URL都會 _非_ 隨處變更。 這表示不需要中斷連結和網頁重新導向。

## 影像集、迴轉集及混合媒體集 {#dm-journey-f}

Dynamic Media一些較常見的用途是可讓您建立影像集、迴轉集和混合媒體集。

影像集通常由一系列以單一實體呈現的影像資產組成。 這些型別的設定可為使用者提供整合式檢視體驗，使用者可按一下縮圖影像來檢視專案的不同檢視。 影像集可讓您呈現某些專案的替代檢視，而檢視器則提供縮放工具，讓您更密切地檢查影像。 [檢視名為「執行中」且使用彈出式檢視器的影像集](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running).

在Dynamic Media內部，您可以看到幾張跑步鞋的影像。 這是銷售和行銷希望客戶檢視為單一簡報的產品線系列；影像集。

![建立影像集](/help/assets/dynamic-media/assets/dm-create-image-set.png)
_建立影像集的開始。_

若要建立影像集，請選擇 **[!UICONTROL 影像集]** 從 **[!UICONTROL 建立]** 下拉式功能表。 請注意，功能表上也有可建立 **[!UICONTROL 混合媒體集]**， a **[!UICONTROL 迴轉集]**，和 **[!UICONTROL 傳送集]**. 您建立這些集合的方式與影像集大致相同。

混合媒體集可包含影像、色票集、迴轉集、視訊和自我調整視訊集。 [試試看](https://s7d9.scene7.com/s7viewers/html5/MixedMediaViewer.html?asset=Scene7SharedAssets/Mixed_Media_Set_Sample). 「迴轉集」會模擬實際動作，即轉動物件來檢查它。 迴轉集可讓您從任何角度檢視重要的視覺細節。 [試試看](https://s7d9.scene7.com/s7viewers/html5/SpinViewer.html?asset=Scene7SharedAssets/SpinSet_Sample&amp;stagesize=500,400){target="_blank"}.

直接建立影像集。 您只需新增要納入集合的影像資產即可。

![建立影像集](/help/assets/dynamic-media/assets/dm-create-image-set-add-assets.png)
_「影像集編輯器」可讓您新增影像資產，以及重新排序影像資產在集中的外觀。_

您必須為集命名。 請謹慎選擇名稱，因為您稍後無法編輯！ 在上述範例中，集合稱為 `Running`. 完成後，您會儲存集合。

以下是 `Running` Experience Manager Assets中的影像集。

![Experience Manager Assets中的執行中影像集，卡片檢視](/help/assets/dynamic-media/assets/dm-image-set.png)
_此 `Running` Experience Manager Assets中的影像集，卡片檢視。_

無論您是否已建立影像集、混合媒體集、迴轉集或任何其他互動式媒體，當您建立該集後，都可以檢視它對於客戶的顯示和行為方式。 Dynamic Media有許多內建檢視器，可讓您這麼做。

首先，請選取建置的影像集，以在預覽中開啟該影像集，如下列範例所示。

![已選取「檢視器」選項時，在預覽中設定的「執行中的影像」](/help/assets/dynamic-media/assets/dm-image-set-viewer.png)
_此 `Running` 已選取「檢視器」選項，在預覽中設定影像。_

請注意，在預覽中，您可以選取跑步鞋色票，並放大和縮小鞋子。 若要將檢視器套用至集合，請選取 **[!UICONTROL 檢視者]** 從下拉式功能表。

![套用彈出式檢視器的「執行中」影像集](/help/assets/dynamic-media/assets/dm-image-set-flyout-viewer.png)
_此 `Running` 套用彈出式檢視器的影像集。_

在此案例中， `Flyout` 已選取檢視器。 此時，您可以預覽檢視器中設定的影像。 不過，最好還是透過瀏覽器檢視，也就是客戶如何檢視。 您選取 **[!UICONTROL URL]** 然後複製URL並貼到瀏覽器中。 [試試看](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running&amp;config=jpearldemo/Flyout){target="_blank"}.

單一URL可讓您在網站上所需的位置使用影像集和檢視器。 您在前一個範例中可能已注意到 **[!UICONTROL 內嵌]** 位於URL按鈕的右側。 藉由選取 **[!UICONTROL 內嵌]**，您可以複製此影像集/檢視器的程式碼，並將其新增至網頁或Experience Manager Sites元件中。

彈出式檢視器是預設的現成檢視器，您可以編輯其屬性。 或者，就像建立影像預設集一樣，您可以建立自己的自訂檢視器。

現在，假設您的銷售和行銷團隊不喜歡彈出式檢視器。 他們喜歡縮放功能，但他們希望客戶能在鞋子上直接看到縮放效果。 在這種情況下，您只需將InlineZoom檢視器套用至影像集，並在瀏覽器中複製並貼上其URL以檢視其行為。 [試試看](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running&amp;config=jpearldemo/InlineZoom){target="_blank"}.

當您將滑鼠指標移到鞋上時，您會放大該影像，而且當您移動指標時，可以看到更多細節。 原因很簡單，就是最初上傳至Dynamic Media的影像大小。

當您考慮以消費者身分生活，或從事日常工作時，以及前往不同網站時，您會看到類似情況。 想想這是如何做到的，以及如何在您自己的工作和您公司的網站上使用Dynamic Media的強大功能。

您剛剛閱讀了影像集和檢視器的相關資訊。 讓我們看看其他幾個檢視器，並在單一資產上試用。 若要重設檢視器，請按一下 **[!UICONTROL 重新整理]** 按鈕。

<!-- LEAVE THIS HIDDEN PATH IN THE DOCUMENTATION FOR DEMO PURPOSES [Flyout viewer with image set](http://www.partycity.com/girls-little-old-lady-costume-P750948.html) -->

* `ZoomVertical_dark` 檢視器套用到影像資產。 [試試看](https://s7d1.scene7.com/s7viewers/html5/ZoomVerticalViewer.html?asset=jpearldemo/AdobeStock_96311480&amp;config=jpearldemo/ZoomVertical_dark){target="_blank"}.
* `Zoom_light` 檢視器套用到影像。 [試試看](https://s7d1.scene7.com/s7viewers/html5/BasicZoomViewer.html?asset=jpearldemo/AdobeStock_38827423&amp;config=jpearldemo/Zoom_light){target="_blank"}.

## 選擇性 — 瞭解更多

如果您想進一步瞭解您剛剛閱讀的內容，請使用以下資料更詳細地探索概念。 否則，您的Dynamic Media歷程已完成！

_Dynamic Media說明主題_

* [如何建立影像預設集](/help/assets/dynamic-media/image-presets.md)
* 清單 [影像處理引數](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html) 當您建立影像預設集時，可在「影像修飾元」欄位中使用的選項
* [如何預覽資產](/help/assets/dynamic-media/previewing-assets.md)
* [如何預覽3D資產](/help/assets/dynamic-media/previewing-3d-assets.md)
* [如何建立影像集](/help/assets/dynamic-media/image-sets.md)
* [如何建立迴轉集](/help/assets/dynamic-media/spin-sets.md)
* [如何建立混合媒體集](/help/assets/dynamic-media/mixed-media-sets.md)

_Dynamic Media教學課程_

* [搭配Experience Manager Assets使用Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-overview-feature-video-use.html)
* [Adobe Experience Manager內容庫](https://experienceleague.adobe.com/?lang=en#recommended/solutions/experience-manager) (搜尋 _Dynamic Media_)

_Dynamic Media檢視器_

* [即時示範](https://landing.adobe.com/tw/na/dynamic-media/ctir-2755/live-demos.html) 每個檢視者

<!-- Live as of April 28 2022. LEAVE IN HERE https://landing.adobe.com/en/na/dynamic-media/ctir-2755/index.html -->