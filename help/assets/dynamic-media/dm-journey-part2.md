---
title: Dynamic Media之旅，第二部
description: 《Dynamic Media之旅》介紹了Dynamic Media的基本知識、工作原理、能為您做什麼，以及它給您的工作和客戶帶來什麼價值。
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
source-git-commit: 94d77e08e5df82f9bb432bb06c4f05301d119f9e
workflow-type: tm+mt
source-wordcount: '2817'
ht-degree: 0%

---

# Dynamic Media之旅：《基礎》，第二部  {#dm-journey-part2}

歡迎來到Dynamic Media之旅：Basics（基本），第II部分，您可以在其中學習以下內容：

* Dynamic MediaURL的剖析及Dynamic Media如何提供內容
* 建立影像預設以呈現資產的基礎
* 映像集、旋轉集和混合媒體集

另請參閱 [Dynamic Media之旅；《基礎》，第一部分](/help/assets/dynamic-media/dm-journey-part1.md)。

>[!TIP]
>
>為獲得最佳效果，Adobe建議您在台式電腦上閱讀和查看Dynamic Media之旅。

## Dynamic MediaURL的剖析及Dynamic Media如何提供內容 {#dm-journey-d}

在上載和發佈您的Dynamic Media資產後，您可以複製資產生成的URL並將其貼上到瀏覽器中，以查看資產對客戶的顯示方式。 監視影像的以下複製URL按顏色細分，以便更容易閱讀和理解。

![Dynamic MediaURL的剖析](/help/assets/dynamic-media/assets/dm-colored-url.png)
_Dynamic MediaURL的解剖。_

紅色URL的第一部分引用伺服器域本身。 在本例中，Dynamic Media運行在通用伺服器域上， `https://s7d1.scene7.com/is/image/`。 只需查看伺服器域，您就可以輕鬆查看一組影像，並瞭解Dynamic Media是否在提供這些影像。 URL將是相當一致的。 但是，有些Dynamic Media客戶已切換到專用伺服器域 `name-of-your-company.scene7.com`。 智慧映像需要專用伺服器域。

帳戶名是紫色部分。 在這種情況下，該帳戶稱為 `jpearldemo`。

資產ID或名稱， `AdobeStock_28563982` 是綠色的。 注意資產已 *不* 檔案副檔名(如 `.png` 或 `.jpg`。 當將資產放入Dynamic Media時，將刪除檔案副檔名並建立另一種檔案：金字塔TIFF檔案。 吡唑TIFF允許Dynamic Media快速建立格式副本。

最後，還有一些影像處理參數， `?wid=1000&fmt=jpeg&qlt=85`，以黃色顯示。

整個URL路徑是即時的。 [試試看](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982?wid=1000&amp;fmt=jpeg&amp;qlt=85)。

您的瀏覽器窗口仍開啟到Dynamic MediaURL和監視影像，讓我們更仔細地看看您如何僅通過更改URL來建立影像的格式副本。

### 通過URL呈現監視影像

首先，僅手動刪除URL路徑中的影像處理規則；保留伺服器名、帳戶名和資產ID或映像名。 [試試看](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982)。

現在，將影像處理參數添加到URL的末尾。 在URL欄位中，在影像名稱右側鍵入 `?wid=500`按 **[!UICONTROL 輸入]**。 [試試看](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=500)。

請注意，將生成手錶的新格式副本。 要從改變影像寬度這一簡單練習中瞭解這一點，關鍵是所看到的影像是100%動態生成的。

現在更改的寬度值 `500` 像素到 `1000` 像素，然後按 **[!UICONTROL 輸入]**。 [試試看](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000)。
你一按 **[!UICONTROL 輸入]**，瀏覽器返回到Dynamic Media映像伺服器。 它會根據您剛剛輸入的新寬度值生成手錶的全新格式副本，然後將新影像返回瀏覽器並快取。

Dynamic Media有許多影像處理參數，您可以使用這些參數來微調網頁上的影像資產。 你可以 [在這裡看到他們的清單](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html?lang=en)。

現在，嘗試向監視影像添加旋轉參數。 URL路徑的結尾，緊跟在 `wid=1000`鍵 `&rotate=90`，然後按 **[!UICONTROL 輸入]**。 [試試看](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000&amp;rotate=90)。

手錶仍略向左傾斜。 更改的旋轉值 `90` 至 `92`，然後按 **[!UICONTROL 輸入]**。 [試試看](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000&amp;rotate=9)

再說一遍，當你按 **[!UICONTROL 輸入]**&#x200B;這款手錶幾乎在瞬間產生了新的再現。 您可以看到您獲得的效能，這就解釋了為什麼Dynamic Media可以提供800,000多個映像請求， *每秒*&#x200B;在忙碌的週末或主要的假期。

雖然可以逐張影像地更改URL中的影像處理參數，但這不是一種有效的方法，尤其是如果您的網站有成千上萬張影像。 一種更好的方法是使用影像預設。

## 建立影像預設以呈現資產的基礎 {#dm-journey-e}

要建立映像或使映像可用的方式和位置有多種。 傳統上， Creative會進入Adobe Photoshop，並將每個不同的呈現形式保存為靜態影像。

![靜態影像](/help/assets/dynamic-media/assets/dm-static-images.png)
_好：靜態映像，每個映像都是手動建立的。_

想像一下創意Director看著這些圖片說，

_「我真的想拍這張表，這樣大手就指向四，小手就指向1，讓手錶錶盤更容易看。」_

創意人員必須重新拍攝所有這些新的靜態影像。

但是，對於Dynamic Media，如果您有不同的影像預設，則可以隨時隨地使用這些影像。 影像預設強制執行標準。

![主檔案方法](/help/assets/dynamic-media/assets/dm-onefile.png)
_最佳：使用影像預設建立一個具有多個即時呈現的檔案，如 `Search_Grid` 和 `Thumbnail`。_

| **為什麼使用影像預設？** |  |
|---|---|
| 標準 | 影像預設對請求的影像強制執行標準影像處理處理。 |
| 更改管理 | 如果必須更改影像處理，則只需編輯現有影像預設的參數。 更新的定義會自動傳播到所有請求。 |

每個需要特定影像類型的地方，例如，

* 產品詳細資訊頁面，
* 搜索網格，
* 縮略圖，
* 購物卡，或
* 英雄形象

您希望將影像提供到與使用影像的參數相同的位置。

讓我們看一下在Dynamic Media如何建立影像預設。

![從「基本」頁籤開始建立影像預設](/help/assets/dynamic-media/assets/dm-image-preset-basictab.png)
_從「基本」頁籤開始建立影像預設。_

在上面的示例中，您可以看到已使用名稱建立了新影像預設 _中_。 Dynamic Media使用一個示例，即現成影像 — 背包 — 來幫助您查看建立影像預設時的特徵。

的 _中_ 影像預設的寬度為500像素，高度為800像素。 在《旅程》的第一部分，你讀到了關於以不同格式交付資產的內容。 從 **[!UICONTROL 格式]** 下拉菜單，您可以選擇將資產作為JPEG、PNG、TIFF或幾種其它格式傳送。 您在這裡有靈活性。

選擇 **[!UICONTROL 高級]** 頁籤。 根據您在 **[!UICONTROL 基本]** 頁籤 — 在上例中，選擇了「JPEG」 — 您可以以RGB、灰度或CMYK格式傳送資產。 從 **[!UICONTROL 顏色配置檔案]** 下拉菜單，您可以選擇如何傳送要用於打印的CMYK影像資產。 還請注意，您可以應用其他參數來銳化影像。 在這個例子中， **[!UICONTROL 非銳化蒙版]** 。

![通過從「高級」頁籤中選擇選項建立影像預設](/help/assets/dynamic-media/assets/dm-image-preset-advancedtab.png)
_通過從「高級」頁籤中選擇選項來建立影像預設。_

你還記得 [Dynamic MediaURL的剖析](#dm-journey-d) 之前，你讀到了Dynamic MediaURL，以及它是如何構建的。 的 **[!UICONTROL 影像修飾符]** 框中，您可以在其中鍵入所需的任何附加影像處理參數。 當使用預設傳送影像時，這些參數將包含在URL的預設名稱中。 在上面的螢幕快照中， `bgc=451B15` 。 就是加了一種深棕色的背景色。

您可以將影像預設視為影像的配方。 它將每次都提供使用預設的、一致的影像；會一樣的。 參數 `&op_brightness=+10` 還增加了亮度。

完成後，將保存預設，現在它可用於您擁有的所有影像。 在這種情況下，我們希望 _中_ 影像被預設為一碗液態巧克力的影像。

![應用影像預設 *中* 生成影像的格式副本](/help/assets/dynamic-media/assets/dm-medium-image-preset.png)
_應用影像預設介質以生成影像的再現。_

複製URL，然後將其貼上到瀏覽器中以檢查影像外觀。 [試試看](http://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_74043302?$Medium$)。 在瀏覽器中，注意影像預設的名稱 _中_ 的子菜單。

您可以看到在影像中顯示的清晰度。 這種質量在一定程度上是因為那碗巧克力的拍攝方式。 另外，這部分是因為在Dynamic Media，你可以儲存比傳輸到數字頻道的影像更大的影像。

如果一碗巧克力看起來一切都令人滿意，您就將URL貼上到您的網頁中，以便在您的網站上顯示影像。

如果你再看下面的手錶影像，你可以看到 `Cart` 影像預設，a `Grid` 預設，a `Large` 預設，a `PDP-page` （產品詳細資訊頁面）預設及其他幾個預設。

![靜態和動態影像預設](/help/assets/dynamic-media/assets/dm-image-presets.png)
_靜態和動態影像預設。 已使用 `PDP-page` 影像預設。_

但是，如果你不得不在你的網站上改變一個影像呢？ 例如，假設您已經執行了一些測試，並發現影像為120 x 120( `Cart` 影像預設)未像您想的那樣被接收。 必須將寬度增加到175像素，將高度增加到175像素，使影像變大。 傳統上，你必須進入Adobe Photoshop並重新建立所有這些購物車影像。 但是，使用Dynamic Media，您只需將「寬度」和「高度」值更新為175來編輯影像預設，然後保存您的預設，如下例所示。

![編輯影像預設](/help/assets/dynamic-media/assets/dm-edit-image-preset.png)
_編輯的寬度和高度 `Cart` 影像預設。_

更改影像預設並清除快取後，將更新所有影像，並執行與該預設一起使用的所有URL _不_ 隨處更改。 這意味著不需要斷開連結和網頁重定向。

## 映像集、旋轉集和混合媒體集 {#dm-journey-f}

Dynamic Media的一些更常用用途是您能夠建立映像集、旋轉集和混合媒體集。

影像集通常由作為單個實體呈現的一系列影像資產組成。 這些類型的集為用戶提供了綜合的查看體驗，用戶可以通過按一下縮略圖來查看項目的不同視圖。 影像集允許您顯示某些內容的替代視圖，而查看器提供了用於仔細檢查影像的縮放工具。 [查看使用Flyout查看器的名為「運行」的影像集](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running)。

在Dynamic Media里，你可以看到幾幅跑步鞋的圖片。 這是一個產品系列，銷售和營銷部門希望客戶將其視為單一演示；影像集。

![建立影像集](/help/assets/dynamic-media/assets/dm-create-image-set.png)
_建立映像集的開始。_

要建立映像集，請選擇 **[!UICONTROL 影像集]** 從 **[!UICONTROL 建立]** 下拉菜單。 菜單上的注意，還有建立 **[!UICONTROL 混合媒體集]**&#x200B;的 **[!UICONTROL 旋轉集]**&#x200B;的 **[!UICONTROL 旋轉木馬集]**。 建立這些集的方式與建立影像集的方式大致相同。

混合媒體集可以包含影像、色板集、旋轉集、視頻和自適應視頻集。 [試試看](https://s7d9.scene7.com/s7viewers/html5/MixedMediaViewer.html?asset=Scene7SharedAssets/Mixed_Media_Set_Sample)。 「旋轉」(Spin)集模擬轉動對象以檢查對象的真實行為。 旋轉集可從任何角度查看關鍵可視詳細資訊。 [試試看](https://s7d9.scene7.com/s7viewers/html5/SpinViewer.html?asset=Scene7SharedAssets/SpinSet_Sample&amp;stagesize=500,400)。

建立映像集非常簡單。 只需添加要包含在集中的映像資產。

![建立影像集](/help/assets/dynamic-media/assets/dm-create-image-set-add-assets.png)
_「影像集編輯器」(Image Set Editor)允許您添加影像資產並重新排序其在集中的外觀。_

需要您為集指定名稱。 請仔細選擇名稱，因為以後無法編輯它！ 在上例中，該集稱為 `Running`。 完成後，將保存該集。

這是 `Running` 在Experience Manager Assets。

![Experience Manager Assets卡視圖中的運行映像集](/help/assets/dynamic-media/assets/dm-image-set.png)
_的 `Running` 影像在Experience Manager Assets設定，卡視圖。_

無論您是建立了映像集、混合媒體集、旋轉集還是任何其他互動式媒體，在建立該集後，您都希望瞭解它對客戶的顯示和行為方式。 Dynamic Media有很多內置的觀眾，讓你可以做到。

首先，選擇生成的「影像」集，以在預覽中將其開啟，如下例所示。

![選中「查看器」選項時，在預覽中設定「正在運行」影像](/help/assets/dynamic-media/assets/dm-image-set-viewer.png)
_的 `Running` 選中「查看器」選項時在預覽中設定的影像。_

請注意，在預覽中，您可以選擇正在運行的鞋色板並放大和縮小鞋。 要將查看器應用於集，請選擇 **[!UICONTROL 查看者]** 的下界。

![應用了浮動查看器的「運行」影像集](/help/assets/dynamic-media/assets/dm-image-set-flyout-viewer.png)
_的 `Running` 應用了浮動查看器的影像集。_

在這個例子中， `Flyout` 已選擇查看器。 此時，您可以在查看器中預覽影像集。 但是，最好在瀏覽器中看到它，只要客戶看到它。 您選擇 **[!UICONTROL URL]** 在左下角，複製URL並將其貼上到瀏覽器中。 [試試看](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running&amp;config=jpearldemo/Flyout)。

單個URL允許您使用網站上需要的影像集和查看器。 您可能在上一個示例中注意到 **[!UICONTROL 嵌入]** 按鈕的子菜單。 通過選擇 **[!UICONTROL 嵌入]**，您可以複製此影像集/查看器的代碼，並將其添加到網頁或Experience Manager Sites元件中。

Flyout查看器是預設的開箱查看器，可編輯其屬性。 或者，就像建立影像預設一樣，您也可以建立自己的自定義查看器。

假設你的銷售和營銷團隊不喜歡Flyout觀眾。 他們喜歡縮放功能，但希望顧客能直接看到鞋子上的縮放效果。 在這種情況下，只需將InlineZoom查看器應用於影像集，並在瀏覽器中複製和貼上其URL，以查看其行為。 [試試看](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running&amp;config=jpearldemo/InlineZoom)。

當你將滑鼠指針移到鞋上時，你會放大到那幅影像，當你移動指針時，你可以看到更多細節。 原因僅僅是最初上傳到Dynamic Media的影像的大小

當你考慮以消費者身份生活，或者當你在日常工作中工作，當你訪問不同的網站時，你會看到像這樣的事情。 想想這是如何實現的，以及如何在你自己的工作和公司網站上利用Dynamic Media的力量。

你只是讀了一點關於影像集和觀眾的資訊。 我們再來看看另外幾個觀眾，在單一資產上試一試。 要重置查看器，請按一下 **[!UICONTROL 刷新]** 按鈕。

<!-- LEAVE THIS HIDDEN PATH IN THE DOCUMENTATION FOR DEMO PURPOSES [Flyout viewer with image set](http://www.partycity.com/girls-little-old-lady-costume-P750948.html) -->

* `ZoomVertical_dark` 應用於影像資產的查看器。 [試試看](https://s7d1.scene7.com/s7viewers/html5/ZoomVerticalViewer.html?asset=jpearldemo/AdobeStock_96311480&amp;config=jpearldemo/ZoomVertical_dark)。
* `Zoom_light` 應用於影像的查看器。 [試試看](https://s7d1.scene7.com/s7viewers/html5/BasicZoomViewer.html?asset=jpearldemo/AdobeStock_38827423&amp;config=jpearldemo/Zoom_light)。

## 了解更多

_Dynamic Media話題_

* [建立影像預設](/help/assets/dynamic-media/image-presets.md)
* 清單 [影像處理參數](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html) 在建立影像預設時可在「影像修改量」欄位中使用的
* [預覽資產](/help/assets/dynamic-media/previewing-assets.md)
* [預覽3D資產](/help/assets/dynamic-media/previewing-3d-assets.md)
* [影像集](/help/assets/dynamic-media/image-sets.md)
* [旋轉集](/help/assets/dynamic-media/spin-sets.md)
* [混合媒體集](/help/assets/dynamic-media/mixed-media-sets.md)

_Dynamic Media教程_

* [將Dynamic Media與Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-overview-feature-video-use.html)
* [Adobe Experience Manager內容庫](https://experienceleague.adobe.com/?lang=en#recommended/solutions/experience-manager) （搜索） _Dynamic Media_)