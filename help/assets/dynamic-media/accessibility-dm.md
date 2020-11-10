---
title: 無障礙環境支援 [!DNL Dynamic Media]
description: 瞭解如何在動態媒體中使用3D資產
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
translation-type: tm+mt
source-git-commit: 7af8ddda4aee093b22147db9be9f65cd0c131c04
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 0%

---


# 動態媒體中的協助功能 {#working-with-three-d-assets-dm}

Dynamic Media跨製作使用者介面支援鍵盤控制和輔助技術，例如JAWS和NVDA螢幕閱讀程式。



## 動態媒體中的鍵盤協助功能支援

個別使用者介面元素支援的按鍵輸入，在大多數情況下都十分明顯，而且易於發現。 動態媒體中的鍵盤控制項如下：

* 能夠使用 `Tab` 和按 `Shift+Tab` 鍵來導覽頁面上的互動元素。
使用 `Tab` 將輸入焦點提前到Tabbing順序下一個用戶介面元素；使用 `Shift+Tab` 可將輸入焦點重新放回先前的使用者介面元素。
焦點遍歷會遵循畫面上自然的使用者介面元素位置，並依從左至右、從上至下的順序移動。
* 能夠使用和 `Spacebar` 鍵 `Enter` 來啟動標準使用者介面元素，例如按鈕、下拉式清單等。
* 能夠查看活動元素上的鍵盤焦點反白顯示。 具有輸入焦點的用戶介面元件可接收視覺焦點指示，作為圍繞用戶介面元件呈現的邊框。
* 能夠使用一些自訂的按鍵操作來與複雜的UI元素互動，例如作用點編輯器中的箭頭鍵。 在「影像裁切／智慧型裁切」編輯器中，您可以使用方向鍵來裁切影格大小，或重新定位影像，或兩者皆可。

由於Dynamic Media是AEM Assets的外掛程式，因此大部份的鍵盤控制行為都與AEM Assets中完全相同。 例如，「動態媒 `Cancel` 體」中的按鈕與「AEM資產」中的對焦反白顯示相同，而且會 `Spacebar` 像「AEM資產」中的按鍵反應。 請參 [閱「資產」中的鍵盤快速鍵](/help/assets/accessibility.md#keyboard-shortcuts)。 熱點編輯器和影像裁切／智慧裁切編輯器除外。

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

在熱點編輯器中，動態媒體可讓您使用方向鍵來控製作用點的位置。 請參閱 [轉盤橫幅](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) 或互 [動式影像](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)

在「影像裁切／智慧型裁切」編輯器中，使用方向鍵裁切影格大小，或重新定位影像，或兩者。 請參 [閱編輯單一影像的智慧裁切或智慧色票](/help/assets/dynamic-media/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## 動態媒體檢視器的鍵盤協助功能支援 {#keyboard-accessibility-for-dm-viewers}

所有現成可用的動態媒體檢視器元件都支援為客戶提供鍵盤協助功能。

請參 [閱動態媒體檢視器參考指南](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) 中的鍵盤存取和導覽。

## 動態媒體檢視器的輔助技術支援 {#assistive-technology=support-for-dm-viewers}

Dynamic Media中的所有檢視器元件都支援ARIA（可存取的Rich Internet Applications）角色和屬性，以改善與輔助技術（例如螢幕閱讀器）的整合。

請參閱動 **態媒體檢視器參考指南中自訂檢視器主題中的** 「輔助技術支援說明」主題。 例如，請參 [閱視訊檢視器的輔助技術支援](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) ，或互動式影像檢視器 [的輔助技術支援](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html?lang=en#viewers-for-aem-assets-only) 。

>[!MORELIKETHIS]
>
>* [Adobe解決方案的協助功能](https://www.adobe.com/accessibility.html)
>* [Experience Manager Assets中的協助功能](/help/assets/dynamic-media/accessibility-dm.md)

