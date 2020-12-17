---
title: 元件參考指南
description: 元件及其結構詳細資訊的開發人員參考指南
translation-type: tm+mt
source-git-commit: a4805cd1c6ee3b32f064f258d4a2a0308bee99b1
workflow-type: tm+mt
source-wordcount: '3464'
ht-degree: 0%

---


# 元件參考指南{#components-reference-guide}

元件是建立AEM體驗的核心。 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)和[AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)讓您輕鬆開始使用一組現成、強穩的元件。 [WKND Tutorial](/help/implementing/developing/introduction/develop-wknd-tutorial.md)教學課程會引導開發人員瞭解如何使用這些工具以及如何建立自訂元件以建立新的AEM網站。

>[!TIP]
>
>在參考本檔案之前，請確定您已完成[WKND Tutorial](/help/implementing/developing/introduction/develop-wknd-tutorial.md)，因此熟悉[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)和[AEM Project Archetype。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)

由於WKND教學課程涵蓋大部分的使用案例，本檔案僅作為這些資源的補充。 它提供有關元件在AEM中如何結構化和設定的深入技術細節，並非做為快速入門手冊。

## 概覽 {#overview}

本節將介紹開發您自己的元件時所需的詳細資訊。

### 規劃 {#planning}

開始實際設定或編碼元件之前，您應詢問：

* 您到底需要新元件做什麼？
* 您需要從頭開始建立元件，還是可以從現有元件繼承基本功能？
* 您的元件是否需要邏輯來選取／控制內容？
   * 邏輯應與使用者介面層分開。 HTL的設計目的是協助確保這一點。
* 您的元件是否需要CSS格式？
   * CSS格式應與元件定義分開。 定義HTML元素命名的慣例，以便您透過外部CSS檔案修改這些元素。
* 您的新元件可能會帶來哪些安全性影響？

### 重複使用現有元件{#reusing-components}

在您投入時間建立全新元件之前，請考慮自訂或擴充現有元件。 [核心元](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 件提供一套靈活、強穩且經過良好測試的可立即生產使用的元件。

#### 擴展核心元件{#extending-core-components}

核心元件也提供[清除的自訂模式](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html)，您可使用這些模式來調整以符合您自己專案的需求。

#### 覆蓋元件{#overlying-components}

元件也可以根據搜尋路徑邏輯以[overlay](/help/implementing/developing/introduction/overlays.md)重新定義。 不過，在此情況下，[Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md)將不會觸發，而`/apps`必須定義整個覆蓋。

#### 擴展元件對話框{#extending-component-dialogs}

您也可以使用Sling Resource Merger並定義屬性`sling:resourceSuperType`來覆寫元件對話方塊。

這表示您只需要重新定義所需的差異，而不需要重新定義整個對話框。

### 內容邏輯與轉換標籤{#content-logic-and-rendering-markup}

將使用[HTML呈現您的元件。](https://www.w3schools.com/htmL/html_intro.asp) 您的元件需要定義需要的HTML，以取得必要的內容，然後在作者和發佈環境中視需要呈現。

建議將負責標籤和轉換的代碼與控制用於選擇元件內容的邏輯的代碼分開。

[HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html)支援此理念，該模板語言被特意限制以確保使用真正的寫程式語言來定義底層業務邏輯。 此機制會反白標示為特定檢視所呼叫的程式碼，並視需要允許相同元件不同檢視的特定邏輯。

此（選用）邏輯可以不同的方式實作，並可從HTL以特定命令叫用：

* 使用Java - [HTL Java Use-API](https://helpx.adobe.com/experience-manager/htl/using/use-api-java.html)可讓HTL檔案存取自訂Java類別中的輔助方法。 這可讓您使用Java程式碼來實作邏輯，以選取和設定元件內容。
* 使用JavaScript - [HTL JavaScript Use-API](https://experienceleague.adobe.com/docs/experience-manager-htl/using/htl/use-api-javascript.html)可讓HTL檔案存取以JavaScript編寫的輔助程式碼。 這可讓您使用JavaScript程式碼來實作邏輯，以選取和設定元件內容。
* 使用用戶端程式庫——現代網站嚴重依賴由複雜JavaScript和CSS程式碼驅動的用戶端處理。 如需詳細資訊，請參閱檔案[「在AEM上使用用戶端程式庫做為雲端服務」。](/help/implementing/developing/introduction/clientlibs.md)

## 元件結構{#structure}

AEM元件的結構強大而有彈性。 主要部分有：

* [資源類型](#resource-type)
* [元件定義](#component-definition)
* [元件的屬性和子節點](#properties-and-child-nodes-of-a-component)
* [對話方塊](#dialogs)
* [設計對話框](#design-dialogs)

### 資源類型 {#resource-type}

結構的關鍵要素是資源類型。

* 內容結構宣告意圖。
* 資源類型實施它們。

這種抽象化有助於確保即使外觀和感覺隨著時間而改變，意圖也會隨著時間而改變。

### 元件定義{#component-definition}

元件的定義可以按如下方式劃分：

* AEM元件是以[Sling.](https://sling.apache.org/documentation.html)為基礎
* AEM元件位於`/libs/core/wcm/components`下方。
* 項目／站點特定元件位於`/apps/<myApp>/components`下。
* AEM標準元件定義為`cq:Component`，並具有關鍵元素：
   * jcr屬性-jcr屬性的清單。 這些是變數，雖然元件節點的基本結構、其屬性和子節點由`cq:Component`定義定義，但有些是可選的。
   * 資源——這些定義元件使用的靜態元素。
   * 指令碼——這些指令碼用於實作元件產生例項的行為。

#### 重要屬性{#vital-properties}

* **根節點**:
   * `<mycomponent> (cq:Component)` -元件的層次節點。
* **重要屬性**:
   * `jcr:title` -元件標題；例如，當元件列在「元件瀏覽器」和「元件控制台」中時， [將](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser) 用作 [標籤](/help/sites-cloud/authoring/features/components-console.md)
   * `jcr:description` -元件說明；用作元件瀏覽器和元件主控台中的滑鼠移過提示
   * 如需詳細資訊，請參閱[元件圖示](#component-icon)一節
* **重要子節點**:
   * `cq:editConfig (cq:EditConfig)` -定義元件的編輯屬性，並使元件顯示在元件瀏覽器中
      * 如果元件有對話方塊，則會自動出現在「元件」瀏覽器或Sidekick中，即使cq:editConfig不存在亦然。
   * `cq:childEditConfig (cq:EditConfig)` -控制未定義子元件的作者UI方面 `cq:editConfig`。
   * `cq:dialog (nt:unstructured)` -此元件的對話框。定義允許用戶配置元件和／或編輯內容的介面。
   * `cq:design_dialog (nt:unstructured)` -此元件的設計編輯

#### 元件表徵圖{#component-icon}

當開發人員建立元件時，元件的圖示或縮寫會透過元件的JCR屬性來定義。 這些屬性依下列順序計算，並使用第一個找到的有效屬性。

1. `cq:icon` -指向 [Coral UI程式庫中標準圖示的字串屬](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html) 性，以顯示在元件瀏覽器中
   * 使用Coral圖示的HTML屬性值。
1. `abbreviation` -字串屬性，用於自定義元件瀏覽器中元件名稱的縮寫
   * 縮寫應限制為兩個字元。
   * 提供空字串將從`jcr:title`屬性的前兩個字元生成縮寫。
      * 例如，「Im」代表「Image」
      * 本地化的標題將用來建立縮寫。
   * 僅當元件具有`abbreviation_commentI18n`屬性時，縮寫才被翻譯，然後將其用作翻譯提示。
1. `cq:icon.png` 或 `cq:icon.svg` -此元件的表徵圖，如元件瀏覽器中所示
   * 20 x 20像素是標準元件的圖示大小。
      * 較大的圖示會縮小（用戶端）。
   * 建議的顏色是rgb(112、112、112)> #707070
   * 標準元件圖示的背景是透明的。
   * 僅支援`.png`和`.svg`檔案。
   * 如果透過Eclipse外掛程式從檔案系統匯入，檔案名稱需要逸出為`_cq_icon.png`或`_cq_icon.svg`。
   * `.png` 如果兩者都 `.svg` 存在，就先例。

如果元件上未找到上述屬性（`cq:icon`、`abbreviation`、`cq:icon.png`或`cq:icon.svg`）:

* 系統將在`sling:resourceSuperType`屬性後搜索超級元件上的相同屬性。
* 如果在超級元件級別中沒有發現縮寫或空縮寫，系統將從當前元件`jcr:title`屬性的第一個字母建立縮寫。

要取消超級元件中表徵圖的繼承，在元件上設定空`abbreviation`屬性將恢復為預設行為。

[元件控制台](/help/sites-cloud/authoring/features/components-console.md#component-details)顯示如何定義特定元件的表徵圖。

#### SVG表徵圖示例{#svg-icon-example}

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

### 元件{#properties-and-child-nodes-of-a-component}的屬性和子節點

定義元件所需的許多節點／屬性對兩個UI都很常見，差異仍獨立，因此您的元件可以在兩個環境中工作。

元件是`cq:Component`類型的節點，具有以下屬性和子節點：

| 名稱 | 類型 | 說明 |
|---|---|---|
| `.` | `cq:Component` | 這表示當前元件。 元件的節點類型為`cq:Component`。 |
| `componentGroup` | `String` | 這表示在[元件瀏覽器中可以選擇元件的組。](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser) 開頭為的值 `.` 用於無法從UI（如其他元件繼承的基本元件）中選擇的元件。 |
| `cq:isContainer` | `Boolean` | 這表示元件是否為容器元件，因此可包含其他元件，例如段落系統。 |
| `cq:dialog` | `nt:unstructured` | 這是元件的編輯對話框的定義。 |
| `cq:design_dialog` | `nt:unstructured` | 這是元件設計對話框的定義。 |
| `cq:editConfig` | `cq:EditConfig` | 這定義了元件的[編輯配置。](#edit-behavior) |
| `cq:htmlTag` | `nt:unstructured` | 這會傳回新增至周圍HTML標籤的其他標籤屬性。 可將屬性新增至自動產生的視訊。 |
| `cq:noDecoration` | `Boolean` | 如果為true，則不會使用自動產生的div和css類別來呈現元件。 |
| `cq:template` | `nt:unstructured` | 如果找到此節點，則當從「元件瀏覽器」添加元件時，該節點將用作內容模板。 |
| `jcr:created` | `Date` | 這是建立元件的日期。 |
| `jcr:description` | `String` | 這是元件的說明。 |
| `jcr:title` | `String` | 這是元件的標題。 |
| `sling:resourceSuperType` | `String` | 設定後，元件將繼承此元件。 |
| `component.html` | `nt:file` | 這是元件的HTL指令檔。 |
| `cq:icon` | `String` | 此值指向元件](#component-icon)的[表徵圖，並顯示在元件瀏覽器中。 |

如果我們查看&#x200B;**Text**&#x200B;元件，我們可以看到以下幾個元素：

![文字元件結構](assets/components-text.png)

特定權益物業包括：

* `jcr:title` -這是用於在元件瀏覽器中標識元件的元件的標題。
* `jcr:description` -這是元件的說明。
* `sling:resourceSuperType` -這表示擴展元件（通過覆蓋定義）時的繼承路徑。

特別感興趣的子節點包括：

* `cq:editConfig` -這可在編輯時控制元件的視覺化方面。
* `cq:dialog` -這定義了用於編輯此元件內容的對話框。
* `cq:design_dialog` -這指定此元件的設計編輯選項。

### 對話方塊 {#dialogs}

對話框是元件的關鍵元素，因為它們為作者提供了在內容頁面上配置元件並提供該元件的輸入的介面。 如需內容作者如何與元件互動的詳細資訊，請參閱[編寫檔案](/help/sites-cloud/authoring/fundamentals/editing-content.md)。

視元件的複雜性而定，您的對話方塊可能需要一個或多個標籤。

AEM元件的對話方塊：

* 是`cq:dialog`類型`nt:unstructured`的節點。
* 位於其`cq:Component`節點下方，並位於其元件定義旁。
* 定義用於編輯此元件內容的對話框。
* 是使用Granite UI元件定義。
* 會根據其內容結構和`sling:resourceType`屬性，轉譯為伺服器端（如Sling元件）。
* 包含描述對話框中欄位的節點結構
   * 這些節點是`nt:unstructured`，具有所需的`sling:resourceType`屬性。

![標題元件的對話框定義](assets/components-title-dialog.png)

在對話方塊中，會定義個別欄位：

![標題元件對話框定義的欄位](assets/components-title-dialog-items.png)

### 設計對話框{#design-dialogs}

設計對話框與用於編輯和配置內容的對話框類似，但它們為模板作者提供了介面，以便在頁面模板上為該元件進行專業配置並提供設計詳細資訊。 然後內容作者會使用頁面範本來建立內容頁面。 有關如何建立模板的詳細資訊，請參閱[模板文檔](/help/sites-cloud/authoring/features/templates.md)。

[編輯頁面範本時會使用設計對話方塊](/help/sites-cloud/authoring/features/templates.md)，但並非所有元件都需要這些對話方塊。例如，**Title**&#x200B;和&#x200B;**影像元件**&#x200B;都具有設計對話方塊，而&#x200B;**社交媒體分享元件**&#x200B;則沒有。

### Coral UI和Granite UI {#coral-and-granite}

Coral UI和Granite UI可定義AEM的外觀和感覺。

* [Coral ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html) UI在所有雲端解決方案中提供一致的UI。
* [Granite ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html) UI提供Coral UI標籤，並封裝在Sling元件中，以建立UI主控台和對話方塊。

Granite UI提供在製作環境上建立對話方塊所需的各種基本Widget。 如有需要，您可以延伸此選取範圍並建立您自己的介面工具集。

如需詳細資訊，請參閱下列資源：

* [Coral UI指南](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html)
* [Granite UI檔案](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)
* [AEM UI的結構](/help/implementing/developing/introduction/ui-structure.md)

### 自定義對話框欄位{#customizing-dialog-fields}

>[!TIP]
>
>請參閱「自訂對話方塊欄位」的[AEM Gems session](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html)。

若要建立新介面工具集以用於元件對話方塊，您必須建立新的Granite UI欄位元件。

如果您將對話方塊視為表單元素的簡單容器，則您也可以將對話方塊內容的主要內容視為表單欄位。 建立新表單域需要建立資源類型；這相當於建立新元件。 為協助您完成該任務，Granite UI提供了要繼承的通用欄位元件（使用`sling:resourceSuperType`）:

`/libs/granite/ui/components/coral/foundation/form/field`

更具體地說，Granite UI提供一系列欄位元件，適合用於對話方塊，或更一般地以[形式說。](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/index.html)

建立資源類型後，可以通過在對話框中添加新節點來實例化欄位，該節點的屬性`sling:resourceType`引用了剛剛引入的資源類型。

#### 對對話框欄位{#access-to-dialog-fields}的訪問

您也可以使用演算條件(`rendercondition`)來控制誰可以存取對話方塊中的特定標籤／欄位；例如：

```text
+ mybutton
  - sling:resourceType = granite/ui/components/coral/foundation/button
  + rendercondition
    - sling:resourceType = myapp/components/renderconditions/group
    - groups = ["administrators"]
```

## 使用元件{#using-components}

建立元件後，您必須啟用它才能使用它。 使用它可顯示元件結構與儲存庫中生成的內容結構之間的關係。

### 將元件添加到模板{#adding-your-component-to-the-template}

在定義元件後，它必須可供使用。 若要讓元件可供範本使用，您必須在範本版面容器的原則中啟用元件。

有關如何建立模板的詳細資訊，請參閱[模板文檔](/help/sites-cloud/authoring/features/templates.md)。

### 元件及其建立的內容{#components-and-the-content-they-create}

如果我們在頁面上建立並配置&#x200B;**Title**&#x200B;元件的實例：`/content/wknd/language-masters/en/adventures/extreme-ironing.html`

![標題編輯對話框](assets/components-title-dialog.png)

然後，我們可以看到在儲存庫中建立的內容的結構：

![標題元件節點結構](assets/components-title-content-nodes.png)

尤其是，如果您查看&#x200B;**標題元件**&#x200B;的實際文字：

* 內容包含`jcr:title`屬性，其中包含作者輸入之標題的實際文字。
* 它還包含對元件定義的`sling:resourceType`引用。

定義的屬性取決於各個定義。 雖然可能比高，但仍遵循相同的基本原則。

## 元件層次和繼承{#component-hierarchy-and-inheritance}

AEM中的元件受&#x200B;**資源類型階層**&#x200B;的規範。 這用於使用屬性`sling:resourceSuperType`擴展元件。 這可讓元件繼承其他元件。

如需詳細資訊，請參閱[重複使用元件](#reusing-components)一節。

## 編輯行為{#edit-behavior}

本節說明如何設定元件的編輯行為。 這包括一些屬性，如元件可用的操作、in.place編輯器的特性，以及與元件上的事件相關的監聽器。

元件的編輯行為是通過在元件節點（類型`cq:Component`）下添加`cq:editConfig`類型`cq:EditConfig`的節點，並添加特定屬性和子節點來配置的。 以下屬性和子節點可用：

* `cq:editConfig` 節點屬性
* [`cq:editConfig` 子節點](#configuring-with-cq-editconfig-child-nodes):
   * `cq:dropTargets` (節點類 `nt:unstructured`型):定義可接受內容搜尋器資產拖放的拖放目標清單（允許單一拖放目標）
   * `cq:inplaceEditing` (節點類 `cq:InplaceEditingConfig`型):定義元件的就地編輯配置
   * `cq:listeners` (節點類 `cq:EditListenersConfig`型):定義在元件上執行動作之前或之後發生的動作

AEM中有許多現有的設定。 使用&#x200B;**CRXDE Lite**&#x200B;中的查詢工具，可以輕鬆地搜索特定屬性或子節點。

### 使用cq進行配置：EditConfig子節點{#configuring-with-cq-editconfig-child-nodes}

#### 將資產拖放至對話方塊- cq:dropTargets {#cq-droptargets}

`cq:dropTargets`節點（節點類型`nt:unstructured`）定義可接受從內容查找器拖動的資產中刪除的刪除目標。 它是類型`cq:DropTargetConfig`的節點。

類型`cq:DropTargetConfig`的子節點定義元件中的放置目標。

### 就地編輯- cq:inplace編輯{#cq-inplaceediting}

就地編輯器可讓使用者直接在內容流程中編輯內容，而不需開啟對話方塊。 例如，標準&#x200B;**Text**&#x200B;和&#x200B;**Title**&#x200B;元件都具有內嵌編輯器。

對於每個元件類型，就地編輯器並非必要／有意義。

`cq:inplaceEditing`節點（節點類型`cq:InplaceEditingConfig`）定義元件的就地編輯配置。 它可以具有以下屬性：

| 屬性名稱 | 屬性類型 | 屬性值 |
|---|---|---|
| `active` | `Boolean` | `true` 以啟用元件的就地編輯。 |
| `configPath` | `String` | 可由配置節點指定的編輯器配置路徑 |
| `editorType` | `String` | 可用類型包括：`plaintext`對於非HTML內容，`title`在開始編輯前將圖形標題轉換為明文，而`text`使用Rich Text Editor |

以下配置啟用元件的輸入編輯，並將`plaintext`定義為編輯器類型：

```text
    <cq:inplaceEditing
        jcr:primaryType="cq:InplaceEditingConfig"
        active="{Boolean}true"
        editorType="plaintext"/>
```

### 處理欄位事件- cq:listeners {#cq-listeners}

處理對話欄位上事件的方法是使用自訂[用戶端程式庫中的聆聽器來完成。](/help/implementing/developing/introduction/clientlibs.md)

若要將邏輯插入您的欄位，您應：

* 將您的欄位標示為指定的CSS類別（勾選）。
* 在用戶端程式庫中定義連結該CSS類別名稱的JS接聽程式（這可確保您的自訂邏輯僅限於您的欄位，而不會影響同類型的其他欄位）。

若要達成此目的，您必須瞭解您要與之互動的基礎Widget程式庫。 [請參閱Coral UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html) 檔案，以識別您要回應的事件。

`cq:listeners`節點（節點類型`cq:EditListenersConfig`）定義在元件上執行操作之前或之後會發生什麼。 下表定義了其可能的屬性。

| 屬性名稱 | 屬性值 |
|---|---|
| `beforedelete` | 在刪除元件之前觸發處理程式。 |
| `beforeedit` | 在編輯元件之前觸發處理程式。 |
| `beforecopy` | 在複製元件之前觸發處理程式。 |
| `beforeremove` | 在移動元件之前觸發處理程式。 |
| `beforeinsert` | 在插入元件之前觸發處理程式。 |
| `beforechildinsert` | 處理常式會在元件插入至其他元件之前觸發（僅限容器）。 |
| `afterdelete` | 移除元件後，就會觸發處理常式。 |
| `afteredit` | 編輯元件後，就會觸發處理常式。 |
| `aftercopy` | 在複製元件後觸發處理程式。 |
| `afterinsert` | 在插入元件後觸發處理程式。 |
| `aftermove` | 在移動元件後觸發處理程式。 |
| `afterchildinsert` | 在將元件插入其他元件（僅限容器）後，就會觸發處理常式。 |

>[!NOTE]
>
>對於嵌套元件，在`cq:listeners`節點上定義為屬性的操作有某些限制。 對於嵌套元件，以下屬性的值&#x200B;**必須**&#x200B;為`REFRESH_PAGE`:
>
>* `aftermove`
>* `aftercopy`


事件處理常式可與自訂實作一起實作。 例如（其中`project.customerAction`是靜態方法）:

`afteredit = "project.customerAction"`

以下示例等效於`REFRESH_INSERTED`配置：

`afterinsert="function(path, definition) { this.refreshCreated(path, definition); }"`

使用下列配置，在刪除、編輯、插入或移動元件後刷新頁面：

```text
    <cq:listeners
        jcr:primaryType="cq:EditListenersConfig"
        afterdelete="REFRESH_PAGE"
        afteredit="REFRESH_PAGE"
        afterinsert="REFRESH_PAGE"
        afterMove="REFRESH_PAGE"/>
```

### 欄位驗證{#field-validation}

在Granite UI和Granite UI Widget中進行欄位驗證的方法是使用`foundation-validation` API。 如需詳細資訊，請參閱[`foundation-valdiation` Granite檔案](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/clientlibs/foundation/js/validation/index.html)。

### 檢測對話框的可用性{#dialog-ready}

如果您有自訂JavaScript，而且只有在對話方塊可用且準備就緒時才需要執行，則應監聽`dialog-ready`事件。

每當對話方塊載入（或重新載入）並準備使用時，就會觸發此事件，這表示每當對話方塊的DOM中有變更（建立／更新）時。

`dialog-ready` 可用來在JavaScript自訂程式碼中掛接，以對對話方塊內的欄位或類似工作執行自訂。

## 預覽行為{#preview-behavior}

在切換至「預覽」模式時，即使頁面未重新整理，也會設定[WCM模式](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) Cookie。

對於具有對WCM模式敏感的轉譯元件，需要定義這些元件，以明確重新整理它們，然後依賴Cookie的值。

## 文檔元件{#documenting-components}

身為開發人員，您想要輕鬆存取元件檔案，以便快速瞭解元件：

* 說明
* 預定用途
* 內容結構與屬性
* 公開的API和擴充點
* 等等。

因此，很容易就能在元件本身使用任何現有的檔案標籤。

您只需將`README.md`檔案置於元件結構中。

![元件結構中的README.md](assets/components-documentation.png)

然後，此標籤將顯示在[元件控制台中。](/help/sites-cloud/authoring/features/components-console.md)

![README.md在元件控制台中可見](assets/components-documentation-console.png)

支援的標籤與[內容片段的標籤相同。](/help/assets/content-fragments/content-fragments.md)