---
title: Dynamic Media 無障礙內容
description: 瞭解Dynamic Media和Dynamic Media檢視器的協助功能。
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
topic: 業務從業人員
feature: 協助工具
role: 管理員，業務從業人員
translation-type: tm+mt
source-git-commit: 8093f6cec446223af58515fd8c91afa5940f9402
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 1%

---


# Dynamic Media 無障礙內容 {#accessibility-in-dm}

Dynamic Media支援鍵盤控制和輔助技術，例如JAWS和NVDA螢幕閱讀程式，可跨製作使用者介面使用。

## Dynamic Media{#keyboard-support-in-dm}的鍵盤協助功能支援

由於Dynamic Media是Experience Manager資產的外掛程式，因此大部份的鍵盤控制行為都與Experience Manager資產相同。 例如，Dynamic Media的`Cancel`按鈕與「Experience Manager資產」中的焦點反白顯示相同。 它也會對`Spacebar`鍵產生反應，如Experience Manager資產中。 請參閱Assets](/help/assets/accessibility.md#keyboard-shortcuts)中的[鍵盤快速鍵。

在大多數情況下，由Dynamic Media的單個用戶介面元素支援的按鍵操作是顯而易見的，而且易於查找。 Dynamic Media的鍵盤控制項如下：

* 能夠使用`Tab`和`Shift+Tab`鍵擊，在頁面上的互動元素之間導航。
使用`Tab`將輸入焦點提前到Tabbing順序中的下一個用戶介面元素；使用`Shift+Tab`將輸入焦點重新帶回先前的使用者介面元素。
焦點遍歷會遵循畫面上自然的使用者介面元素位置，並依從左至右、從上至下的順序移動。 此外，如果有欄位有錯誤，您可以按`Tab`將焦點移至該欄位。
* 能夠使用`Spacebar`和`Enter`鍵來啟動標準的使用者介面元素，例如按鈕和下拉式清單。
* 能夠查看活動元素上的鍵盤焦點反白顯示。 具有輸入焦點的用戶介面元件接收視覺焦點指示，作為圍繞用戶介面元件呈現的邊框。
* 在熱點編輯器中，您可以使用一些自定義的按鍵操作（如箭頭鍵）來與複雜的用戶介面元素交互以重新定位熱點。
* 在「互動式視訊」編輯器中，您可以使用`Spacebar`來選取影像，並將它新增至區段。 此外，您還可以使用`Backspace`鍵從&#x200B;**[!UICONTROL Content]**&#x200B;標籤中刪除所選項目。 此外，按`Tab`可視需要在頁面上的互動式元素之間導覽。
* 在「影像裁切／智慧型裁切」編輯器中，您可以執行下列動作：
   * 使用方向鍵裁切影格大小，或重新放置影像，或兩者。
   * 第一個`Tab`停止會反白顯示整個影像影格。 然後，您可以使用鍵盤上的箭頭鍵來重新定位框架。
   * 後面四個`Tab`停位是影格的四角。 將焦點放在框架拐角上時，該拐角會加亮。 同樣地，您可以使用鍵盤上的箭頭鍵來移動焦點轉角。
請參閱[編輯單一影像的智慧裁切或智慧色票](/help/assets/dynamic-media/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Dynamic Media的輔助技術支援{#assistive-technology=support-for-dm}

Dynamic Media的使用者介面元素可與輔助技術搭配使用，例如螢幕閱讀器。 例如，當您使用鍵盤快速鍵`D`導覽標誌時，它會識別頁面上的標誌，或使用鍵盤快速鍵`R`導覽區域。 它也會在使用標題鍵盤快速鍵`H`導覽時旁白標題。

## Dynamic Media查看器的鍵盤輔助功能支援{#keyboard-accessibility-for-dm-viewers}

所有現成可用的Dynamic Media檢視器元件都支援為客戶提供鍵盤協助功能。

請參閱《Dynamic Media檢視器參考指南》中的[鍵盤協助功能和導覽](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html)。

## Dynamic Media檢視器中的輔助技術支援{#assistive-technology=support-for-dm-viewers}

所有Dynamic Media檢視器元件都支援ARIA（可存取的Rich Internet Applications）角色和屬性，以改善與輔助技術（例如螢幕閱讀器）的整合。
請參閱《Dynamic Media檢視器參考指南》中任何自訂檢視器主題的**輔助技術支援**&#x200B;說明主題。 例如，請參閱視頻查看器的[輔助技術支援](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html)或互動式影像查看器的[輔助技術支援](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html?lang=en#viewers-for-aem-assets-only)。

>[!MORELIKETHIS]
>
>* [Adobe解決方案的協助功能](https://www.adobe.com/accessibility.html)
>* [Experience Manager資產中的協助功能](/help/assets/dynamic-media/accessibility-dm.md)

