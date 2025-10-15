---
title: 影像品質最佳化的最佳做法
description: 瞭解可協助您使用Dynamic Media最佳化影像資產品質的最佳實務。
contentOwner: Rick Brough
feature: Asset Management, Best Practices
role: User
exl-id: 2efc4a27-01d7-427f-9701-393497314402
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '1648'
ht-degree: 1%

---

# 影像品質最佳化的最佳做法 {#best-practices-for-optimizing-the-quality-of-your-images}

{{work-with-dynamic-media}}

最佳化影像品質是一項耗時的程式，因為許多因素都會產生可接受的演算結果。 由於個人對影像品質的認知不同，所以最後的結果會有部分主觀性。 結構化的實驗是關鍵。

Adobe Experience Manager包含100多項Dynamic Media影像傳送命令，用於調整及最佳化影像和演算結果。 下列准則可協助您使用一些基本指令和最佳作法，簡化程式並快速取得良好的結果。

<!-- ADDED THE FOLLOWING TOPIC AS PER CQDOC-21594 -->

## 在Dynamic Media中啟用智慧型影像 {#bp-enable-smart-imaging}

**智慧型影像處理：**

* 在Dynamic Media中啟用智慧型影像可讓您根據使用者端瀏覽器功能，自動最佳化影像格式、大小和品質。
想要進一步瞭解嗎？ 移至[智慧型影像](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/assets/dynamicmedia/imaging-faq)。
* 它可動態調整這些引數，藉以強化影像傳送效能。
* 您可以使用自我評估工具[快照](https://snapshot.scene7.com/)來評估智慧型影像。

**影像格式：**

* 避免在URL中使用明確的`fmt=webp`或`fmt=avif`命令，除非使用案例特別需要。
* 智慧型影像會自動選取最佳格式，以獲得最佳的頻寬增益。

**預設行為：**

* 當URL中未指定格式命令，且智慧型影像未啟用時，Dynamic Media影像傳送預設為使用JPEG格式。

選擇適當的影像格式並啟用智慧型影像處理，可大幅影響效能和使用者體驗。


<!-- ADDED THE FOLLOWING TOPIC AS PER CQDOC-21594 -->

## 選取來源影像的最佳作法 {#bp-select-source-image}

使用來源影像的基本考量事項：

* **Source影像格式：**
   * 使用PNG、TIFF或PSD等無損格式可確保影像品質維持高品質，不會出現任何壓縮成品。
   * 這些格式會保留所有原始資料，因此非常適合編輯和進一步處理。
* **Source影像大小：**
   * 從高解析度影像開始，提供更多細節和彈性。
   * 當需要以不同大小（例如，跨裝置或熒幕解析度）顯示影像時，擁有較大的來源影像可提供更好的縮放。
   * 若是支援縮放的影像（例如產品像片），請將最大的一側尺寸設定為約2,000畫素或以上。
   * 不需要縮放的標誌或橫幅可以按照預期用途所需的最大尺寸上傳。

透過在來源層級進行這些謹慎的選擇，您可以對視覺內容的整體品質做出重大貢獻。

<!-- REMOVED TOPIC AS PER CQDOC-21594
## Best practices for image format (`&fmt=`) {#best-practices-for-image-format-fmt}

* JPG or PNG are the best choices to deliver images in good quality and with manageable size and weight.
* If no format command is supplied in the URL, Dynamic Media Image Delivery defaults to JPG for delivery.
* JPG compresses at a ratio of 10:1 and usually produces smaller image file sizes. PNG compresses at a ratio of about 2:1, except when images contain a white background. Typically though, PNG file sizes are larger than JPG files.
* JPG uses lossy compression, meaning that picture elements (pixels) are dropped during compression. PNG on the other hand uses lossless compression.
* JPG often compresses photographic images with better fidelity than synthetic images with sharp edges and contrast.
* If your images contain transparency, use PNG because JPG does not support transparency.

As a best practice for image format, start with the most common setting `&fmt=JPG`. -->

## 影像大小相關最佳實務 {#best-practices-for-image-size}

動態縮小影像大小是最常見的工作之一。 它涉及指定大小，以及（選擇性）用來縮減影像規模的縮減取樣模式。

* 若是調整影像大小，最好且最直接的方法是使用`&wid=<value>`和`&hei=<value>,`，或只使用`&hei=<value>`。 這些引數會根據外觀比例自動設定影像寬度。
* `&resMode=<value>`控制縮減取樣所使用的演演算法。 從`&resMode=sharp2`開始。 這個值可提供最佳的影像品質。 雖然使用縮減取樣`value =bilin`的速度較快，但通常會導致成品產生鋸齒。

如需調整影像大小的最佳作法，請使用`&wid=<value>&hei=<value>&resMode=sharp2`或`&hei=<value>&resMode=sharp2`

## 影像銳利化的最佳作法 {#best-practices-for-image-sharpening}

影像銳利化是控制網站上影像的最複雜方面，也會造成許多錯誤。 請參考下列實用資源，以花時間進一步瞭解銳利化和遮色片銳利化在Experience Manager中的運作方式：

* 最佳實務白皮書[Adobe Dynamic Media Classic影像品質和銳利化最佳實務](/help/assets/dynamic-media/assets/sharpening_images.pdf)也適用於Experience Manager。

* 觀看[搭配Experience Manager - Dynamic Media使用影像銳利化](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-image-sharpening-feature-video-use#dynamic-media)。

有了Experience Manager，您可以在內嵌和/或傳送時銳利化影像。 不過，通常最好只使用一種方法或另一種方法來銳利化影像，但不要同時使用兩者。 在URL上傳送影像時銳利化，通常能提供最佳結果。

您可以使用兩種影像銳利化方法：

* 簡單銳利化( `&op_sharpen`) — 類似於Photoshop中使用的銳利化濾鏡，簡單銳利化會在動態調整大小後，將基本銳利化套用至影像的最終檢視。 不過，此方法無法由使用者設定。 除非必要，否則最佳實務是避免使用`&op_sharpen`。
* 遮色片銳利化調整(`&op_USM`) — 遮色片銳利化調整是業界標準的銳利化濾鏡。 最佳作法是依照下列方針，使用遮色片銳利化來銳利化影像。 「不銳利化遮色片」可讓您控制下列三個引數：

   * `&op_sharpen=`金額，半徑，臨界值

      * **[!UICONTROL amount]** （0-5，效果強度）。
      * **[!UICONTROL 半徑]** (0-250，在銳利化物件周圍繪製的「銳利化線條」寬度（以畫素為單位）。

     請記住，引數半徑和數量彼此對應。 可以增加數量來補償縮小半徑。 「半徑」允許更細微的控制，因為較低的值只會銳利化邊緣畫素，而較高的值會銳利化較寬的畫素範圍。

      * **[!UICONTROL 臨界值]** （0-255，效果敏感度。）

     此引數會決定銳化畫素與周圍區域的差異程度，之後才會被視為邊緣畫素，濾鏡會銳化這些畫素。 **[!UICONTROL threshold]**&#x200B;引數有助於避免色彩相似的區域過度銳利化，例如膚色。 例如，閾值為12會忽略膚色亮度的微小變化，以避免加上「雜訊」，同時仍會加上邊緣對比度至高對比區域，例如睫毛與皮膚相遇的區域。

     如需如何設定這三個引數的詳細資訊，包括篩選使用的最佳實務，請參閱下列資源：

      * 最佳實務白皮書[Adobe Dynamic Media Classic影像品質和銳利化最佳實務](/help/assets/dynamic-media/assets/sharpening_images.pdf)也適用於Experience Manager。

      * 觀看[搭配Experience Manager - Dynamic Media使用影像銳利化](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-image-sharpening-feature-video-use#dynamic-media)。

      * Experience Manager也可讓您控制第四個引數：單色(0,1)。 此引數決定使用0值將遮色片銳利化調整分別套用至每個色彩元件，或是使用1值將影像亮度/強度套用至影像。

最佳作法是從「遮色片銳利化調整半徑」引數開始。 您可以開始使用的半徑設定如下：

* **[!UICONTROL 網站]**： 0.2-0.3畫素
* **[!UICONTROL 像片列印(250-300 ppi)]**： 0.3-0.5畫素
* **[!UICONTROL 膠印列印(266-300 ppi)]**： 0.7-1.0畫素
* **[!UICONTROL 畫布列印(150 ppi)]**： 1.5至2.0畫素

逐漸將數量從1.75增加到4。 如果銳利化仍不是您想要的方式，請將半徑增加小數點，然後再次從1.75到4執行量。 視需要重複。

將單色引數設定保留為0。

### JPEF壓縮(`&qlt=`)的最佳作法 {#best-practices-for-jpef-compression-qlt}

* 此引數會控制JPG編碼品質。 較高的值表示影像品質較高，但檔案大小較大；或者，較低的值表示影像品質較低，但檔案大小較小。 此引數的範圍為0至100。
* 若要最佳化品質，請勿將引數值設為100。 設定90或95與100之間的差異幾乎無法察覺。 然而100卻不必要地增加了影像檔案的大小。 因此，若要最佳化品質但避免影像檔案變得太大，請將`qlt= value`設為90或95。
* 若要針對較小的影像檔案大小進行最佳化，但將影像品質維持在可接受的等級，請將`qlt= value`設定為80。 值低於70到75會導致影像品質顯著下降。
* 若要保持中間，最佳做法是將`qlt= value`設為85以保持中間。
* 在`qlt=`中使用色度旗標

   * `qlt=`引數有第二個設定，可讓您使用值`,1`開啟RGB色度縮減取樣，或使用值`,0`關閉。
   * 若要保持簡單，請從RGB色度縮減取樣關閉(`,0`)開始。 此設定通常會產生更好的影像品質，尤其是對於具有大量銳利邊緣和對比的人工合成影像。

JPG壓縮的最佳作法是使用`&qlt=85,0`。

## JPEG大小調整的最佳實務(`&jpegSize=`) {#best-practices-for-jpeg-sizing-jpegsize}

如果您想要保證影像不會超過傳送至記憶體有限之裝置的某個大小，引數`jpegSize`就十分實用。

* 此引數設定為KB (`jpegSize=&lt;size_in_kilobytes&gt;`)。 它會定義影像傳送的允許大小上限。
* `&jpegSize=`會與JPG壓縮引數`&qlt=`互動。 如果具有指定JPG壓縮引數(`&qlt=`)的JPG回應未超過jpegSize值，則影像會依定義傳回`&qlt=`。 否則，`&qlt=`會逐漸減少，直到影像符合最大允許大小為止。 或者，直到系統判斷它無法容納並傳回錯誤為止。

如果您要將JPG影像傳遞至記憶體有限的裝置，最佳做法是設定`&jpegSize=`並新增引數`&qlt=`。

## 最佳實務摘要 {#best-practices-summary}

為了達到高影像品質和小檔案大小，最佳實務建議從下列參陣列合開始：

`fmt=jpg&qlt=85,0&resMode=sharp2&op_usm=1.75,0.3,2,0`

在大多數情況下，這種設定組合會產生卓越的結果。

如果影像需要進一步最佳化，請從半徑設定為0.2或0.3開始，逐步微調銳利化（不銳利化遮色片）引數。然後，逐漸將數量從1.75增加到最大值4 (相當於Photoshop中的400%)。 檢查是否達到所需結果。

如果銳利化結果仍然不令人滿意，請以小數點為增量增加半徑。 對於每個小數點增量，請在1.75處重新啟動該數量，並逐漸將其增加到4。 重複此程式，直到您達到想要的結果為止。 雖然上述值是經過創意工作室驗證的方法，但請記住，您可以從其他值開始，並遵循其他策略。 結果是否令您滿意是主觀問題，因此結構化的實驗是關鍵。

實驗時，以下一般建議有助於最佳化您的工作流程：

* 請直接在URL上即時嘗試並測試不同的引數。
* 如需參考最佳做法，請記得您可以將「動態媒體影像伺服」命令群組至影像預設集。 影像預設集基本上是含有自訂預設集名稱（例如`$thumb_low$`和`&product_high$`）的URL命令巨集。 URL路徑中的自訂預設集名稱會呼叫這些預設集。 這類功能可協助您針對網站上不同的影像使用模式管理命令和品質設定，並縮短URL的整體長度。
* Experience Manager也提供更進階的方式來調整影像品質，例如在擷取時套用銳利化影像。 若要調整並最佳化演算結果，[Adobe的諮詢服務](https://business.adobe.com/tw/customers/consulting-services/main.html)可協助您提供自訂的深入分析和最佳實務。
