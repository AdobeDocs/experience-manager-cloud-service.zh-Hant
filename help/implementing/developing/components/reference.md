---
title: 元件參考指南
description: 開發人員參考指南，瞭解元件及其結構的詳細資訊
exl-id: 45e5265b-39d6-4a5c-be1a-e66bb7ea387d
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '3642'
ht-degree: 1%

---

# 元件參考指南 {#components-reference-guide}

元件是在AEM中建立體驗的核心。 此 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 和 [AEM專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hant) 以一組現成的強大元件輕鬆開始使用。 此 [WKND教學課程](/help/implementing/developing/introduction/develop-wknd-tutorial.md) 帶領開發人員瞭解如何使用這些工具，以及如何建置自訂元件以建立AEM網站。

>[!TIP]
>
>在參考此檔案之前，請確定您已完成 [WKND教學課程](/help/implementing/developing/introduction/develop-wknd-tutorial.md) 因此熟悉 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 和 [AEM專案原型。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hant)

由於WKND教學課程涵蓋大部分的使用案例，本檔案旨在補充這些資源。 它提供了有關如何在AEM中建構和設定元件的深入技術細節，並非旨在作為快速入門手冊。

## 概觀 {#overview}

本節說明開發您自己的元件時，所需詳細資訊的主要概念和問題。

### 規劃 {#planning}

開始實際設定元件或為元件編寫程式碼之前，您應該先詢問：

* 您到底需要新元件做什麼？
* 您是否需要從頭開始建立元件，或可從現有元件繼承基本知識？
* 您的元件需要邏輯才能選取/操控內容嗎？
   * 邏輯應與使用者介面層分開。 HTL的設計目的是協助確保做到這一點。
* 您的元件是否需要CSS格式？
   * CSS格式應與元件定義分開。 定義命名HTML元素的慣例，以便您可以透過外部CSS檔案來修改它們。
* 您的新元件可能會引入哪些安全性影響？

### 重複使用現有元件 {#reusing-components}

在您花時間建立全新元件之前，請考慮自訂或擴充現有元件。 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 提供一套彈性、強大且經過充分測試的生產就緒元件。

#### 擴充核心元件 {#extending-core-components}

核心元件也提供 [清除自訂模式](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html) 以根據您自己的專案需求進行調整。

#### 覆蓋元件 {#overlying-components}

元件也可以使用重新定義 [覆蓋](/help/implementing/developing/introduction/overlays.md) 根據搜尋路徑邏輯。 但在這種情況下， [Sling資源合併](/help/implementing/developing/introduction/sling-resource-merger.md) 將不會觸發，而且 `/apps` 必須定義整個覆蓋。

#### 延伸元件對話方塊 {#extending-component-dialogs}

也可以使用Sling Resource Merger並定義屬性來覆寫元件對話方塊 `sling:resourceSuperType`.

這表示您只需要重新定義所需的差異，而不必重新定義整個對話方塊。

### 內容邏輯和轉譯標籤  {#content-logic-and-rendering-markup}

您的元件呈現方式 [HTML](https://www.w3schools.com/htmL/html_intro.asp). 您的元件必須定義取得所需內容所需的HTML，然後視需要在製作和發佈環境中轉譯。

建議將負責標示和轉譯的程式碼，與控制用來選取元件內容的邏輯的程式碼分開。

支援此理念的有 [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html)，特意限制以確保使用實際程式語言來定義基礎商業邏輯的範本化語言。 此機制會醒目顯示呼叫特定檢視的程式碼，並在必要時允許同一元件的不同檢視使用特定邏輯。

此（選用）邏輯可透過不同方式實作，並使用特定命令從HTL叫用：

* 使用Java - [HTL Java Use-API](https://experienceleague.adobe.com/docs/experience-manager-htl/content/java-use-api.html) 讓HTL檔案能夠存取自訂Java類別中的Helper方法。 這可讓您使用Java程式碼來實作選取和設定元件內容的邏輯。
* 使用JavaScript - [HTL JavaScript Use-API](https://experienceleague.adobe.com/docs/experience-manager-htl/using/htl/use-api-javascript.html) 會讓HTL檔案存取以JavaScript撰寫的協助程式碼。 這可讓您使用JavaScript程式碼來實作選取和設定元件內容的邏輯。
* 使用使用者端資料庫 — 現代網站重度依賴由複雜JavaScript和CSS程式碼驅動的使用者端處理。 檢視檔案 [在AEMas a Cloud Service上使用使用者端資料庫](/help/implementing/developing/introduction/clientlibs.md) 以取得詳細資訊。

## 元件結構 {#structure}

AEM元件的結構既強大又靈活。 主要部分為：

* [資源類型](#resource-type)
* [元件定義](#component-definition)
* [元件的屬性和子節點](#properties-and-child-nodes-of-a-component)
* [對話方塊](#dialogs)
* [設計對話方塊](#design-dialogs)

### 資源類型 {#resource-type}

結構的一個關鍵元素是資源型別。

* 內容結構會宣告意圖。
* 資源型別會實作它們。

這是一項抽象，有助於確保即使表觀和感覺隨著時間而改變，意圖仍會維持在時間上。

### 元件定義 {#component-definition}

元件的定義可劃分如下：

* AEM元件是根據 [Sling.](https://sling.apache.org/documentation.html)
* AEM元件位於 `/libs/core/wcm/components`.
* 專案/網站特定元件位於 `/apps/<myApp>/components`.
* AEM標準元件的定義為 `cq:Component` 並具備關鍵元素：
   * jcr屬性 — jcr屬性的清單。 雖然元件節點的基本結構、其屬性和子節點由定義，但這些是變數，有些可能是選用的。 `cq:Component` 定義。
   * 資源 — 這些會定義元件使用的靜態元素。
   * 指令碼 — 這些用於實作元件結果例項的行為。

#### 重要屬性 {#vital-properties}

* **根節點**：
   * `<mycomponent> (cq:Component)`  — 元件的階層節點。
* **重要屬性**：
   * `jcr:title`  — 元件標題；例如，當元件列在 [元件瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser) 和 [元件主控台](/help/sites-cloud/authoring/features/components-console.md)
   * `jcr:description`  — 元件的說明，在元件瀏覽器和元件主控台中作為滑鼠懸停的提示
   * 請參閱區段 [元件圖示](#component-icon) 以取得詳細資訊
* **重要子節點**：
   * `cq:editConfig (cq:EditConfig)`  — 定義元件的編輯屬性，並讓元件出現在元件瀏覽器中
      * 如果元件有對話方塊，即使cq：editConfig不存在，它也會自動出現在「元件」瀏覽器或Sidekick中。
   * `cq:childEditConfig (cq:EditConfig)`  — 控制未定義其本身的子元件的作者UI方面 `cq:editConfig`.
   * `cq:dialog (nt:unstructured)`  — 此元件的對話方塊。 定義允許使用者設定元件及/或編輯內容的介面。
   * `cq:design_dialog (nt:unstructured)`  — 此元件的設計編輯

#### 元件圖示 {#component-icon}

元件的圖示或縮寫可在開發人員建立元件時，透過元件的JCR屬性來定義。 系統會依下列順序評估這些屬性，並使用找到的第一個有效屬性。

1. `cq:icon`  — 字串屬性，指向 [Coral UI程式庫](https://opensource.adobe.com/coral-spectrum/examples/#icon) 以在元件瀏覽器中顯示
   * 使用Coral圖示的HTML屬性值。
1. `abbreviation`  — 字串屬性，用於自訂元件瀏覽器中元件名稱的縮寫
   * 縮寫應限製為兩個字元。
   * 提供空字串將會建置的縮寫（從開頭兩個字元） `jcr:title` 屬性。
      * 例如，「Image」的「Im」
      * 使用當地語系化的標題來建置縮寫。
   * 只有元件具備以下條件時，才會轉譯縮寫： `abbreviation_commentI18n` 屬性，然後用作翻譯提示。
1. `cq:icon.png` 或 `cq:icon.svg`  — 此元件的圖示，會顯示在元件瀏覽器中
   * 20 x 20畫素是標準元件的圖示大小。
      * 較大的圖示會縮小（使用者端）。
   * 建議的色彩為rgb(112， 112， 112) > #707070
   * 標準元件圖示的背景是透明的。
   * 僅限 `.png` 和 `.svg` 支援檔案。
   * 如果透過Eclipse外掛程式從檔案系統匯入，檔案名稱需要逸出為 `_cq_icon.png` 或 `_cq_icon.svg` 例如。
   * `.png` 先決條件優先 `.svg` 如果兩者都存在。

如果以上屬性均非(`cq:icon`， `abbreviation`， `cq:icon.png` 或 `cq:icon.svg`)，可以在元件上找到：

* 系統會在超級元件上搜尋下列專案後的相同屬性 `sling:resourceSuperType` 屬性。
* 如果在超級元件層級找不到任何專案或空白縮寫，系統會從 `jcr:title` 目前元件的屬性。

若要取消從超級元件繼承圖示，請將設定為空白 `abbreviation` 元件上的屬性將還原為預設行為。

此 [元件主控台](/help/sites-cloud/authoring/features/components-console.md#component-details) 顯示特定元件圖示的定義方式。

#### SVG圖示範例 {#svg-icon-example}

```xml
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "https://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
<svg version="1.1" id="Layer_1" xmlns="https://www.w3.org/2000/svg" xmlns:xlink="https://www.w3.org/1999/xlink" x="0px" y="0px"
     width="20px" height="20px" viewBox="0 0 20 20" enable-background="new 0 0 20 20" xml:space="preserve">
    <ellipse cx="5" cy="5" rx="3" ry="3" fill="#707070"/>
    <ellipse cx="15" cy="5" rx="4" ry="4" fill="#707070"/>
    <ellipse cx="5" cy="15" rx="5" ry="5" fill="#707070"/>
    <ellipse cx="15" cy="15" rx="4" ry="4" fill="#707070"/>
</svg>
```

### 元件的屬性和子節點 {#properties-and-child-nodes-of-a-component}

定義元件所需的許多節點/屬性對這兩個UI都是通用的，差異保持獨立，以便您的元件可以在兩個環境中運作。

元件是型別的節點 `cq:Component` 和有下列屬性和子節點：

| 名稱 | 類型 | 說明 |
|---|---|---|
| `.` | `cq:Component` | 這表示目前的元件。 元件屬於節點型別 `cq:Component`. |
| `componentGroup` | `String` | 這表示可在其中選取元件的群組 [元件瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser). 以開頭的值 `.` 用於無法從UI選取的元件，例如其他元件繼承自的基本元件。 |
| `cq:isContainer` | `Boolean` | 這表示元件是否為容器元件，因此可包含其他元件，例如段落系統。 |
| `cq:dialog` | `nt:unstructured` | 這是元件之「編輯」對話方塊的定義。 |
| `cq:design_dialog` | `nt:unstructured` | 這是元件之「設計」對話方塊的定義。 |
| `cq:editConfig` | `cq:EditConfig` | 這會定義 [編輯元件的設定。](#edit-behavior) |
| `cq:htmlTag` | `nt:unstructured` | 這會傳回新增至周圍HTML標籤的其他標籤屬性。 啟用向自動產生的div新增屬性。 |
| `cq:noDecoration` | `Boolean` | 如果為true，則元件不會使用自動產生的div和css類別轉譯。 |
| `cq:template` | `nt:unstructured` | 如果找到，從元件瀏覽器新增元件時，會將此節點作為內容範本使用。 |
| `jcr:created` | `Date` | 這是建立元件的日期。 |
| `jcr:description` | `String` | 這是元件的說明。 |
| `jcr:title` | `String` | 這是元件的標題。 |
| `sling:resourceSuperType` | `String` | 設定後，元件會繼承自此元件。 |
| `component.html` | `nt:file` | 這是元件的HTL指令碼檔案。 |
| `cq:icon` | `String` | 此值指向 [元件的圖示](#component-icon) 和會顯示在「元件瀏覽器」中。 |

如果您檢視 **文字** 元件中，您可以看到幾個元素：

![文字元件結構](assets/components-text.png)

特別感興趣的屬性包括：

* `jcr:title`  — 這是元件瀏覽器的元件標題，用於識別元件。
* `jcr:description`  — 這是元件的說明。
* `sling:resourceSuperType`  — 這表示擴充元件時的繼承路徑（透過覆寫定義）。

特別感興趣的子節點包括：

* `cq:editConfig`  — 這控制了編輯時元件的視覺方面。
* `cq:dialog`  — 這會定義用於編輯此元件內容的對話方塊。
* `cq:design_dialog`  — 這會指定此元件的設計編輯選項。

### 對話方塊 {#dialogs}

對話方塊是元件的關鍵元素，因為對話方塊為作者提供介面，讓作者可在內容頁面上設定元件，並提供該元件的輸入。 請參閱 [製作檔案](/help/sites-cloud/authoring/fundamentals/editing-content.md) 以取得內容作者如何與元件互動的詳細資訊。

根據元件的複雜性，您的對話方塊可能需要一或多個標籤。

AEM元件的對話方塊：

* 為 `cq:dialog` 型別的節點 `nt:unstructured`.
* 位在其 `cq:Component` 節點及其元件定義旁邊。
* 定義用於編輯此元件內容的對話方塊。
* 是使用Granite UI元件來定義。
* 根據其內容結構和 `sling:resourceType` 屬性。
* 包含描述對話方塊內欄位的節點結構
   * 這些節點為 `nt:unstructured` 具有必要的 `sling:resourceType` 屬性。

![標題元件的對話方塊定義](assets/components-title-dialog.png)

在對話方塊中，會定義個別欄位：

![標題元件的對話方塊定義欄位](assets/components-title-dialog-items.png)

### 設計對話方塊 {#design-dialogs}

「設計」對話方塊類似於用來編輯和設定內容的對話方塊，但它們為範本作者提供了介面，讓他們可以預先設定，並為頁面範本上的該元件提供設計詳細資訊。 然後，內容作者會使用頁面範本來建立內容頁面。 請參閱 [範本檔案](/help/sites-cloud/authoring/features/templates.md) 有關如何建立範本的詳細資訊。

[編輯頁面範本時會使用「設計」對話方塊](/help/sites-cloud/authoring/features/templates.md)，但並非所有元件都需要。 例如， **標題** 和 **影像元件** 兩者都有設計對話方塊，而 **社群媒體分享元件** 不會。

### Coral UI和Granite UI {#coral-and-granite}

Coral UI和Granite UI定義了AEM的外觀和風格。

* [Coral UI](https://opensource.adobe.com/coral-spectrum/documentation/) 跨所有雲端解決方案提供一致的UI。
* [Granite UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html) 提供包在Sling元件中的Coral UI標籤，用於建置UI主控台和對話方塊。

Granite UI提供在製作環境中建立對話方塊所需的大量基本Widget。 必要時，您可以擴充此選取範圍並建立您自己的Widget。

如需其他詳細資訊，請參閱下列資源：

* [AEM UI 的結構](/help/implementing/developing/introduction/ui-structure.md)

### 自訂對話方塊欄位 {#customizing-dialog-fields}

<!--
Content not found

>[!TIP]
>
>See the [AEM Gems session](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html) on customizing dialog fields.
-->

若要建立Widget以用於元件對話方塊，需要您建立Granite UI欄位元件。

如果您將對話方塊視為表單元素的簡單容器，則也可以將對話方塊內容的主要內容視為表單欄位。 建立新表單欄位需要您建立資源型別；這等同於建立元件。 為協助您完成該工作，Granite UI提供了可供繼承的通用欄位元件(使用 `sling:resourceSuperType`)：

`/libs/granite/ui/components/coral/foundation/form/field`

更具體來說，Granite UI提供了一系列適合用於對話方塊的欄位元件，或者更一般地說 [表單。](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/index.html)

建立資源型別後，您可以在對話方塊中使用屬性新增節點，將欄位例項化 `sling:resourceType` 請參閱您剛才介紹的資源型別。

#### 對話方塊欄位的存取權 {#access-to-dialog-fields}

您也可以使用演算條件(`rendercondition`)來控制誰可以存取您對話方塊中的特定索引標籤/欄位，例如：

```text
+ mybutton
  - sling:resourceType = granite/ui/components/coral/foundation/button
  + rendercondition
    - sling:resourceType = myapp/components/renderconditions/group
    - groups = ["administrators"]
```

## 使用元件 {#using-components}

建立元件後，必須啟用它才能使用。 使用它會顯示元件結構如何與存放庫中結果內容的結構相關聯。

### 將元件新增至範本 {#adding-your-component-to-the-template}

定義元件後，該元件必須可供使用。 若要讓元件可在範本中使用，您必須在範本的版面配置容器原則中啟用該元件。

請參閱 [範本檔案](/help/sites-cloud/authoring/features/templates.md) 有關如何建立範本的詳細資訊。

### 元件及其建立的內容 {#components-and-the-content-they-create}

如果我們建立並設定 **標題** 頁面上的元件： `/content/wknd/language-masters/en/adventures/extreme-ironing.html`

![標題編輯對話方塊](assets/components-title-dialog.png)

接著，我們就能檢視存放庫中建立的內容結構：

![標題元件節點結構](assets/components-title-content-nodes.png)

特別是，如果您檢視實際文字 **標題元件**：

* 內容包含 `jcr:title` 保留作者輸入之標題的實際文字的屬性。
* 其中也包含 `sling:resourceType` 元件定義的參照。

定義的屬性取決於個別定義。 雖然這些規則可能比上述規則更複雜，但仍遵循相同的基本原則。

## 元件階層與繼承 {#component-hierarchy-and-inheritance}

AEM中的元件須遵守 **資源型別階層**. 這是用來使用屬性擴充元件 `sling:resourceSuperType`. 這可讓元件繼承自其他元件。

請參閱區段 [重複使用元件](#reusing-components) 以取得詳細資訊。

## 編輯行為 {#edit-behavior}

本節說明如何設定元件的編輯行為。 這包括元件可用的動作、in.place編輯器的特性，以及與元件事件相關的接聽程式等屬性。

元件的編輯行為可透過新增 `cq:editConfig` 型別節點 `cq:EditConfig` 在元件節點（型別）下方 `cq:Component`)，並新增特定屬性和子節點。 下列屬性和子節點可供使用：

* `cq:editConfig` 節點屬性
* [`cq:editConfig` 子節點](#configuring-with-cq-editconfig-child-nodes)：
   * `cq:dropTargets` (節點型別 `nt:unstructured`)：定義可以從內容尋找器的資產接受放置的放置目標清單（允許單一放置目標）
   * `cq:inplaceEditing` (節點型別 `cq:InplaceEditingConfig`)：定義元件的就地編輯設定
   * `cq:listeners` (節點型別 `cq:EditListenersConfig`)：定義元件上發生動作之前或之後所發生的事件

AEM中有許多現有設定。 您可以使用中的查詢工具輕鬆搜尋特定屬性或子節點 **CRXDE Lite**.

### 元件預留位置 {#component-placeholders}

元件必須一律呈現某些作者可見的HTML，即使元件沒有內容亦然。 否則，編輯器介面中可能會看不到它，從技術上講它會出現，但不會顯示在頁面和編輯器中。 在這種情況下，作者將無法選取空白元件並與之互動。

因此，只要元件在頁面編輯器中轉譯頁面時(當WCM模式為 `edit` 或 `preview`)。
預留位置的一般HTML標示如下：

```HTML
<div class="cq-placeholder" data-emptytext="Component Name"></div>
```

轉譯上述預留位置HTML的典型HTL指令碼如下：

```HTML
<div class="cq-placeholder" data-emptytext="${component.properties.jcr:title}"
     data-sly-test="${(wcmmode.edit || wcmmode.preview) && isEmpty}"></div>
```

在上一個範例中， `isEmpty` 是一個變數，只有在元件沒有內容且作者看不到時才會成立。

為避免重複，Adobe建議元件的實作人員對這些預留位置使用HTL範本， [如核心元件所提供的那種。](https://github.com/adobe/aem-core-wcm-components/blob/master/content/src/content/jcr_root/apps/core/wcm/components/commons/v1/templates.html)

接著，使用先前連結中的範本並使用下列HTL行：

```HTML
<sly data-sly-use.template="core/wcm/components/commons/v1/templates.html"
     data-sly-call="${template.placeholder @ isEmpty=!model.text}"></sly>
```

在上一個範例中， `model.text` 是變數，只有在內容具有內容且可見時才會成立。

此範本的範例使用可在核心元件中檢視， [例如，在標題元件中。](https://github.com/adobe/aem-core-wcm-components/blob/master/content/src/content/jcr_root/apps/core/wcm/components/title/v2/title/title.html#L27)

### 使用cq：EditConfig子節點進行配置 {#configuring-with-cq-editconfig-child-nodes}

#### 將資產拖放至對話方塊 — cq：dropTargets {#cq-droptargets}

此 `cq:dropTargets` 節點（節點型別） `nt:unstructured`)會定義放置目標，可接受從內容尋找器拖曳之資產的放置。 它是型別節點 `cq:DropTargetConfig`.

型別的子節點 `cq:DropTargetConfig` 會定義元件中的放置目標。

### 就地編輯 — cq：inplaceEditing {#cq-inplaceediting}

就地編輯器可讓使用者直接在內容流程中編輯內容，而不需要開啟對話方塊。 例如，標準 **文字** 和 **標題** 元件都有就地編輯器。

就地編輯器並非每個元件型別的必要/有意義。

此 `cq:inplaceEditing` 節點（節點型別） `cq:InplaceEditingConfig`)會為元件定義就地編輯設定。 它可以有以下屬性：

| 屬性名稱 | 屬性型別 | 屬性值 |
|---|---|---|
| `active` | `Boolean` | `true` 以啟用就地編輯元件。 |
| `configPath` | `String` | 編輯器設定的路徑，可由設定節點指定 |
| `editorType` | `String` | 可用的型別包括： `plaintext` 對於非HTML內容， `title` 在編輯開始之前，將圖形標題轉換為純文字，並且 `text` 使用RTF編輯器 |

下列組態可讓您就地編輯元件並定義 `plaintext` 作為編輯器型別：

```text
    <cq:inplaceEditing
        jcr:primaryType="cq:InplaceEditingConfig"
        active="{Boolean}true"
        editorType="plaintext"/>
```

### 處理欄位事件 — cq：listeners {#cq-listeners}

處理對話方塊欄位上的事件的方法，是使用自訂中的接聽程式來完成 [使用者端資料庫](/help/implementing/developing/introduction/clientlibs.md).

若要將邏輯插入欄位，您應該：

* 讓您的欄位標示為指定的CSS類別（勾點）。
* 在您的使用者端程式庫中定義連結至該CSS類別名稱的JS接聽程式（這可確保您的自訂邏輯僅限定在欄位範圍內，不會影響相同型別的其他欄位）。

若要完成此操作，您需要瞭解您要與之互動的基礎Widget程式庫。 [請參閱Coral UI檔案](https://opensource.adobe.com/coral-spectrum/documentation/) 以識別您要回應的事件。

此 `cq:listeners` 節點（節點型別） `cq:EditListenersConfig`)會定義元件動作之前或之後所發生的事件。 下表定義其可能的屬性。

| 屬性名稱 | 屬性值 |
|---|---|
| `beforedelete` | 處理常式會在移除元件之前觸發。 |
| `beforeedit` | 處理常式會在編輯元件之前觸發。 |
| `beforecopy` | 處理常式會在複製元件之前觸發。 |
| `beforeremove` | 處理常式會在移動元件之前觸發。 |
| `beforeinsert` | 處理常式會在插入元件之前觸發。 |
| `beforechildinsert` | 處理常式會在元件插入另一個元件（僅限容器）之前觸發。 |
| `afterdelete` | 處理常式會在移除元件後觸發。 |
| `afteredit` | 處理常式會在編輯元件後觸發。 |
| `aftercopy` | 處理常式會在元件複製後觸發。 |
| `afterinsert` | 處理常式會在插入元件後觸發。 |
| `aftermove` | 處理常式會在元件移動後觸發。 |
| `afterchildinsert` | 將元件插入另一個元件（僅限容器）後，就會觸發處理常式。 |

>[!NOTE]
>
>對於巢狀元件，定義為 `cq:listeners` 節點。 對於巢狀元件，下列屬性的值 **必須** 是 `REFRESH_PAGE`：
>
>* `aftermove`
>* `aftercopy`

事件處理常式可使用自訂實施來實施。 例如，(其中 `project.customerAction` 是靜態方法)：

`afteredit = "project.customerAction"`

下列範例等同於 `REFRESH_INSERTED` 設定：

`afterinsert="function(path, definition) { this.refreshCreated(path, definition); }"`

使用下列設定時，頁面會在刪除、編輯、插入或移動元件後重新整理：

```text
    <cq:listeners
        jcr:primaryType="cq:EditListenersConfig"
        afterdelete="REFRESH_PAGE"
        afteredit="REFRESH_PAGE"
        afterinsert="REFRESH_PAGE"
        afterMove="REFRESH_PAGE"/>
```

### 欄位驗證 {#field-validation}

Granite UI和Granite UI Widget中的欄位驗證已透過使用 `foundation-validation` API。 請參閱 [`foundation-valdiation` Granite檔案](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/clientlibs/foundation/js/validation/index.html) 以取得詳細資訊。

### 偵測對話方塊的可用性 {#dialog-ready}

如果您有自訂JavaScript，只有在對話方塊可用且準備就緒時才必須執行，則應接聽 `dialog-ready` 事件。

每當對話方塊載入（或重新載入）並準備就緒可供使用時，即代表每當對話方塊的DOM中有變更（建立/更新）時，就會觸發此事件。

`dialog-ready` 可用於掛接JavaScript自訂程式碼，以在對話方塊或類似工作內的欄位上執行自訂。

## 預覽行為 {#preview-behavior}

此 [WCM模式](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/WCMMode.html) 即使頁面未重新整理，切換至預覽模式時也會設定Cookie。

對於具有對WCM模式敏感的轉譯之元件，需要定義它們以專門重新整理自身，然後依賴Cookie的值。

## 記錄元件 {#documenting-components}

身為開發人員，您想要輕鬆存取元件檔案，以便快速瞭解元件的以下內容：

* 說明
* 預期用途
* 內容結構和屬性
* 公開的API和擴充功能點
* 等等

因此，很容易讓元件本身隨附任何現有的檔案Markdown 。

您只需放置 `README.md` 檔案。

![元件結構中的README.md](assets/components-documentation.png)

然後，此Markdown會顯示在 [元件主控台](/help/sites-cloud/authoring/features/components-console.md).

![元件主控台中的README.md可見專案](assets/components-documentation-console.png)

支援的Markdown與相同 [內容片段](/help/sites-cloud/administering/content-fragments/overview.md).
