---
title: Dynamic Media 無障礙內容
description: 了解Dynamic Media和Dynamic Media檢視器中的協助工具。
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
feature: Accessibility
role: Admin,User
source-git-commit: 0d0a3247e42e0f4a9b2965104814fe6bcd8e6128
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 1%

---


# Dynamic Media 無障礙內容 {#accessibility-in-dm}

Dynamic Media支援製作使用者介面的鍵盤控制和輔助技術，例如JAWS和NVDA螢幕閱讀器。

## Dynamic Media的鍵盤協助工具支援 {#keyboard-support-in-dm}

由於Dynamic Media是[!DNL Experience Manager Assets]的外掛程式，因此大部分的鍵盤控制行為與[!DNL Experience Manager Assets]中相同。 例如，Dynamic Media中的`Cancel`按鈕與[!DNL Experience Manager Assets]中的按鈕焦點醒目提示相同。 它也會回應`Spacebar`鍵，如[!DNL Experience Manager Assets]中。 請參閱Assets](/help/assets/accessibility.md#keyboard-shortcuts)中的[鍵盤快速鍵。

Dynamic Media中個別使用者介面元素支援的鍵擊，在大多數情況下都顯而易見且易於找到。 Dynamic Media中的鍵盤控制項關於下列項目：

* 能夠使用`Tab`和`Shift+Tab`鍵擊在頁面上的互動元素之間導航。
使用`Tab`將輸入焦點按Tab鍵順序提前到下一個用戶介面元素；使用`Shift+Tab`將輸入焦點重新移回上一個使用者介面元素。
焦點周遊會遵循畫面上的自然使用者介面元素位置，並依從左至右、由上至下的順序移動。 此外，如果有欄位有錯誤，您可以按`Tab`將焦點移至該欄位。
* 能夠使用`Spacebar`和`Enter`鍵來激活標準用戶介面元素，如按鈕和下拉清單。
* 可在使用中元素上查看鍵盤焦點醒目提示。 具有輸入焦點的用戶介面元素接收視覺焦點指示，作為圍繞用戶介面元素呈現的邊框。
* 在熱點編輯器中，可以使用一些自定義鍵擊（如箭頭鍵）與複雜的用戶介面元素交互，以重新定位熱點。
* 在互動式視訊編輯器中，您可以使用`Spacebar`來選取影像，並將其新增至區段。 此外，還可以使用`Backspace`鍵從&#x200B;**[!UICONTROL Content]**&#x200B;頁簽中刪除選定項。 此外，按`Tab`可視需要運作，以在頁面上的互動式元素之間導覽。
* 在影像裁切/智慧型裁切編輯器中，您可以執行下列操作：
   * 使用箭頭鍵裁切幀大小，或重新定位影像，或兩者。
   * 第一個`Tab`停止將突出顯示整個影像幀。 然後，可以使用鍵盤上的箭頭鍵來重新定位框架。
   * 接下來的四個`Tab`停止是框架的四個角。 將焦點置於框架拐角時，該拐角將加亮。 同樣地，您可以使用鍵盤上的箭頭鍵來移動聚焦的角。
請參閱[編輯單個影像的智慧型裁切或智慧型色票](/help/assets/dynamic-media/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (Experience Manager 6.5) or Coral Spectrum (in Skyline)) as entire Experience Manager Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Dynamic Media中的輔助技術支援{#assistive-technology=support-for-dm}

Dynamic Media使用者介面元素可搭配輔助技術使用，例如螢幕閱讀器。 例如，當您使用鍵盤快捷鍵`D`導航地標時，它可識別頁面上的地標，或使用鍵盤快捷鍵`R`的區域。 它也會提供使用標題鍵盤快速鍵`H`導覽時的標題旁白。

## Dynamic Media檢視器中的鍵盤協助工具支援 {#keyboard-accessibility-for-dm-viewers}

所有現成可用的Dynamic Media檢視器元件都支援客戶的鍵盤協助工具。

請參閱Dynamic Media檢視器參考指南中的[鍵盤協助工具和導覽](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html)。

## Dynamic Media檢視器中的輔助技術支援{#assistive-technology=support-for-dm-viewers}

所有Dynamic Media檢視器元件都支援ARIA（可存取的豐富網際網路應用程式）角色和屬性，以改善與輔助技術（例如螢幕閱讀器）的整合。
請參閱Dynamic Media檢視器參考指南中任何自訂檢視器主題的**輔助技術支援**&#x200B;說明主題。 例如，請參閱視訊檢視器的[輔助技術支援](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html)，或互動式影像檢視器的[輔助技術支援](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html#viewers-for-aem-assets-only)。

>[!MORELIKETHIS]
>
>* [Adobe解決方案的協助工具](https://www.adobe.com/accessibility.html)
>* [Experience Manager資產中的協助工具](/help/assets/dynamic-media/accessibility-dm.md)

