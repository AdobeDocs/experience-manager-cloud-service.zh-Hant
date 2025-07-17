---
title: HTML5 forms簡介
description: HTML5 forms是Adobe Experience Manager 6.0 (AEM 6.0)軟體中的新功能，可以轉譯HTML5格式的XFA表單範本。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: 0facca18-ffa1-420c-859a-6f1f2c449d71
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---

# HTML5 forms簡介{#introduction-to-html-forms}

<span class="preview"> HTML5 Forms功能屬於Early Access方案的一部分。 若要要求存取權，請將您的正式（工作）電子郵件ID傳送電子郵件至aem-forms-ea@adobe.com。
</span>

HTML5 forms是Adobe Experience Manager 6.0 (AEM 6.0)軟體中的新功能，可以轉譯HTML5格式的XFA表單範本。 此功能可讓您在不支援XFA型PDF的行動裝置和桌上型瀏覽器上轉譯表單。 HTML5表單不僅支援XFA表單範本的現有功能，也新增了適用於行動裝置的新功能，例如手寫簽名。

HTML5 forms會根據標準HTML5建構產生檔案。 您可以在支援HTML5的所有新式瀏覽器中檢視HTML5表單。 它不需要為瀏覽器安裝任何其他瀏覽器外掛程式。 如需支援瀏覽器的詳細資訊，請參閱[支援的使用者端平台](https://adobe.com/go/learn_aemforms_supportedplatforms_63)。

![HTML5表單預覽](assets/mobile_form_on_an_ipad_date_14.png)

## HTML5 Forms的主要功能 {#key-capabilities-of-html-forms-br}

* 在所有相容的瀏覽器上支援HTML5中轉譯現有的XFA表單。
* 運用標準XFA表單設計功能，為行動裝置鎖定表單。
* 使用HTML5格式的動態XFA功能。
* 使用高精確度的SVG文字版面(SVG 1.1)，以符合PDF文字版面。
* 提供對JavaScript和FormCalc的支援。
* 根據資料驅動事件或使用者輸入，以動態方式將片段組合為互動式表單。
* 提供自訂CSS的支援，以根據您的企業標準符合表單的外觀。
* 啟用自訂Widget以提供豐富的資料擷取體驗。
* 提供與網頁應用程式整合的支援。

### 多頻道發佈 {#multichannel-publishing}

表單開發人員可使用XFA範本轉譯PDF和HTML5格式的表單。 若您有大量XFA表單需要最少的變更來適應HTML5表單設計實務，此功能將有所助益。 您可以將現有的XFA表單轉譯為HTML5，以鎖定尚不支援XFA型PDF的各種裝置。

## 管理HTML5表單 {#manage-html-forms}

AEM也提供統一的檢視，以便使用AEM Forms UI列出和管理所有表單範本。 您可以啟用、停用、發佈及預覽表單。<!--For more information, see [Introduction to managing forms](../../forms/using/introduction-managing-forms.md).-->

### Forms自訂 {#forms-customization}

HTML5表單會使用標準HTML5建構來轉譯表單範本。 這可讓您使用網頁技術(主要是CSS和JavaScript)輕鬆自訂和擴充HTML5格式的表單。 您可以輕鬆自訂現有Widget的外觀、建立您自己的自訂Widget，或在表單中使用自訂樣式。 如需建立自訂Widget以及自訂現有Widget的詳細資訊，請參閱[使用HTML5表單插入自訂Widget](/help/forms/custom-widgets.md)。
