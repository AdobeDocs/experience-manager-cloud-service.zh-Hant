---
title: 元件參考指南
description: 元件及其結構的詳細資訊開發人員參考指南
exl-id: 45e5265b-39d6-4a5c-be1a-e66bb7ea387d
source-git-commit: 421ad8506435e8538be9c83df0b78ad8f222df0c
workflow-type: tm+mt
source-wordcount: '3659'
ht-degree: 1%

---

# 元件參考指南 {#components-reference-guide}

元件是在AEM中建立體驗的核心。 此 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 和 [AEM專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) 透過一組現成的強大元件，讓您輕鬆開始使用。 此 [WKND教學課程](/help/implementing/developing/introduction/develop-wknd-tutorial.md) 引導開發人員了解如何使用這些工具，以及如何建立自訂元件以建立新的AEM網站。

>[!TIP]
>
>參考本檔案之前，請確定您已完成 [WKND教學課程](/help/implementing/developing/introduction/develop-wknd-tutorial.md) 因此對 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 和 [AEM專案原型。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)

由於WKND教學課程涵蓋大部分使用案例，本檔案旨在補充這些資源。 它提供有關如何在AEM中架構和設定元件的深入技術細節，而非快速入門手冊。

## 總覽 {#overview}

本節介紹開發您自己的元件時所需的詳細資訊，並說明重要概念和問題。

### 規劃 {#planning}

開始實際設定或編寫元件程式碼之前，您應先詢問：

* 您到底需要新元件做什麼？
* 您是否需要從頭建立元件，還是可以從現有元件繼承基本知識？
* 元件是否需要邏輯才能選取/操控內容？
   * 邏輯應與使用者介面層分開。 HTL的設計目的，是為了協助確保此情況發生。
* 元件是否需要CSS格式？
   * CSS格式應與元件定義分開。 定義命名HTML元素的慣例，以便透過外部CSS檔案修改它們。
* 您的新元件可能會帶來哪些安全性影響？

### 重複使用現有元件 {#reusing-components}

在您花時間建立全新元件之前，請考慮自訂或擴充現有元件。 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 提供一套靈活、強大且經過良好測試的生產就緒元件。

#### 擴充核心元件 {#extending-core-components}

核心元件也提供 [清除自訂模式](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html) 以便您根據自己專案的需求進行調整。

#### 覆蓋元件 {#overlying-components}

也可使用 [覆蓋](/help/implementing/developing/introduction/overlays.md) 根據搜尋路徑邏輯。 然而，在此情況下， [Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md) 不會觸發，且 `/apps` 必須定義整個覆蓋。

#### 擴展元件對話框 {#extending-component-dialogs}

您也可以使用Sling Resource Merger並定義屬性來覆寫元件對話方塊 `sling:resourceSuperType`.

這表示您只需重新定義所需的差異，而不需要重新定義整個對話框。

### 內容邏輯和呈現標籤  {#content-logic-and-rendering-markup}

元件將以呈現 [HTML。](https://www.w3schools.com/htmL/html_intro.asp) 您的元件需要定義取得必要內容所需的HTML，然後在製作和發佈環境中視需要呈現。

建議您將負責標籤和轉譯的程式碼與控制用來選取元件內容之邏輯的程式碼分開。

這一理念得到了支援 [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html)，故意限制為確保使用真實寫程式語言來定義基礎業務邏輯的模板語言。 此機制會反白標示為指定檢視所呼叫的程式碼，並視需要為相同元件的不同檢視允許特定邏輯。

此（選用）邏輯可以不同方式實作，並可透過特定命令從HTL叫用：

* 使用Java - [HTL Java Use-API](https://experienceleague.adobe.com/docs/experience-manager-htl/content/java-use-api.html) 可讓HTL檔案存取自訂Java類別中的Helper方法。 這可讓您使用Java程式碼來實作邏輯，以選取和設定元件內容。
* 使用JavaScript - [HTL JavaScript Use-API](https://experienceleague.adobe.com/docs/experience-manager-htl/using/htl/use-api-javascript.html) 可讓HTL檔案存取以JavaScript撰寫的協助程式碼。 這可讓您使用JavaScript程式碼來實作邏輯，以選取和設定元件內容。
* 使用用戶端資料庫 — 現代化網站嚴重依賴於由複雜JavaScript和CSS程式碼驅動的用戶端處理。 請參閱檔案 [在AEMas a Cloud Service上使用用戶端程式庫](/help/implementing/developing/introduction/clientlibs.md) 以取得更多資訊。

## 元件結構 {#structure}

AEM元件的結構既強大又靈活。 主要部分為：

* [資源類型](#resource-type)
* [元件定義](#component-definition)
* [元件的屬性和子節點](#properties-and-child-nodes-of-a-component)
* [對話方塊](#dialogs)
* [設計對話方塊](#design-dialogs)

### 資源類型 {#resource-type}

結構的一個關鍵元素是資源類型。

* 內容結構聲明意圖。
* 資源類型會實作它們。

這是抽象，有助於確保即使外觀和感覺隨時間而改變，意圖仍會維持。

### 元件定義 {#component-definition}

元件的定義可依下列方式劃分：

* AEM元件以 [Sling。](https://sling.apache.org/documentation.html)
* AEM元件位於 `/libs/core/wcm/components`.
* 項目/站點特定元件位於 `/apps/<myApp>/components`.
* AEM標準元件定義為 `cq:Component` 並有關鍵要素：
   * jcr屬性 — jcr屬性的清單。 這些是變數，有些可能是選用的，不過元件節點、其屬性和子節點的基本結構是由 `cq:Component` 定義。
   * 資源 — 這些定義元件使用的靜態元素。
   * 指令碼 — 這些指令碼用於實作元件之產生例項的行為。

#### 重要屬性 {#vital-properties}

* **根節點**:
   * `<mycomponent> (cq:Component)`  — 元件的階層節點。
* **重要屬性**:
   * `jcr:title`  — 元件標題；例如，當元件列於 [元件瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser) 和 [元件主控台](/help/sites-cloud/authoring/features/components-console.md)
   * `jcr:description`  — 元件的說明；在元件瀏覽器和元件主控台中，作為滑鼠移過提示使用
   * 請參閱 [元件圖示](#component-icon) 詳細資訊
* **重要子節點**:
   * `cq:editConfig (cq:EditConfig)`  — 定義元件的編輯屬性，並使元件顯示在「元件瀏覽器」中
      * 如果元件有對話方塊，則會自動顯示在「元件」瀏覽器或Sidekick中，即使cq:editConfig不存在亦然。
   * `cq:childEditConfig (cq:EditConfig)`  — 控制未定義子元件的製作UI方面 `cq:editConfig`.
   * `cq:dialog (nt:unstructured)`  — 此元件的對話框。 定義介面，讓使用者設定元件和/或編輯內容。
   * `cq:design_dialog (nt:unstructured)`  — 編輯此元件的設計

#### 元件圖示 {#component-icon}

當開發人員建立元件時，元件的圖示或縮寫會透過元件的JCR屬性定義。 這些屬性的計算順序如下，並使用找到的第一個有效屬性。

1. `cq:icon`  — 指向 [Coral UI程式庫](https://opensource.adobe.com/coral-spectrum/examples/#icon) 在元件瀏覽器中顯示
   * 使用Coral圖示的HTML屬性值。
1. `abbreviation`  — 字串屬性，可自訂元件瀏覽器中元件名稱的縮寫
   * 縮寫應限制為兩個字元。
   * 提供空白字串，將會從的前兩個字元建立縮寫 `jcr:title` 屬性。
      * 例如，「Im」代表「Image」
      * 本地化的標題將用於建立縮寫。
   * 僅當元件具有 `abbreviation_commentI18n` 屬性，然後會用作翻譯提示。
1. `cq:icon.png` 或 `cq:icon.svg`  — 此元件的圖示，顯示在元件瀏覽器中
   * 20 x 20像素是標準元件的圖示大小。
      * 較大的圖示會縮小（用戶端）。
   * 建議的顏色為rgb(112, 112, 112)> #707070
   * 標準元件圖示的背景是透明的。
   * 僅 `.png` 和 `.svg` 支援檔案。
   * 如果透過Eclipse外掛程式從檔案系統匯入，檔案名稱需逸出為 `_cq_icon.png` 或 `_cq_icon.svg` 例如，
   * `.png` 先例 `.svg` 如果兩者皆存在。

若沒有上述任何屬性(`cq:icon`, `abbreviation`, `cq:icon.png` 或 `cq:icon.svg`)位於元件上：

* 系統會在超級元件上搜尋相同的屬性，如下所示： `sling:resourceSuperType` 屬性。
* 如果在超級元件層級找不到任何縮寫或空白縮寫，則系統會從 `jcr:title` 屬性。

要取消超級元件的表徵圖繼承，請設定空 `abbreviation` 元件上的屬性將回復為預設行為。

此 [元件主控台](/help/sites-cloud/authoring/features/components-console.md#component-details) 顯示如何定義特定元件的圖示。

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

定義元件所需的許多節點/屬性在兩個UI中都很常見，差異仍獨立，因此您的元件可在兩個環境中運作。

元件是類型的節點 `cq:Component` 和具有以下屬性和子節點：

| 名稱 | 類型 | 說明 |
|---|---|---|
| `.` | `cq:Component` | 這代表目前的元件。 元件屬於節點類型 `cq:Component`. |
| `componentGroup` | `String` | 這表示可在中選取元件的群組 [元件瀏覽器。](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser) 開頭為的值 `.` 用於無法從UI中選擇的元件，如其他元件繼承的基礎元件。 |
| `cq:isContainer` | `Boolean` | 這表示元件是否為容器元件，因此可以包含段落系統等其他元件。 |
| `cq:dialog` | `nt:unstructured` | 這是元件的編輯對話框的定義。 |
| `cq:design_dialog` | `nt:unstructured` | 這是元件設計對話框的定義。 |
| `cq:editConfig` | `cq:EditConfig` | 這會定義 [編輯元件的設定。](#edit-behavior) |
| `cq:htmlTag` | `nt:unstructured` | 這會傳回新增至周圍HTML標籤的其他標籤屬性。 可將屬性新增至自動產生的div。 |
| `cq:noDecoration` | `Boolean` | 若為true，則不會以自動產生的div和css類別轉譯元件。 |
| `cq:template` | `nt:unstructured` | 如果找到，則從「元件瀏覽器」中新增元件時，此節點將作為內容範本使用。 |
| `jcr:created` | `Date` | 這是元件的建立日期。 |
| `jcr:description` | `String` | 此為元件的說明。 |
| `jcr:title` | `String` | 這是元件的標題。 |
| `sling:resourceSuperType` | `String` | 設定後，元件會從此元件繼承。 |
| `component.html` | `nt:file` | 這是元件的HTL指令碼檔案。 |
| `cq:icon` | `String` | 此值指向 [元件的圖示](#component-icon) 和會出現在「元件瀏覽器」中。 |

如果我們看 **文字** 元件，我們可以看到以下幾個元素：

![文字元件結構](assets/components-text.png)

特定權益物業包括：

* `jcr:title`  — 這是元件瀏覽器中用於識別元件的元件標題。
* `jcr:description`  — 此為元件的說明。
* `sling:resourceSuperType`  — 這表示延伸元件時（透過覆寫定義）的繼承路徑。

特別感興趣的子節點包括：

* `cq:editConfig`  — 這會在編輯時控制元件的視覺效果。
* `cq:dialog`  — 這會定義編輯此元件內容的對話方塊。
* `cq:design_dialog`  — 它指定此元件的設計編輯選項。

### 對話方塊 {#dialogs}

對話方塊是元件的關鍵元素，因為對話方塊提供介面，供作者在內容頁面上設定元件，並為該元件提供輸入。 請參閱 [編寫檔案](/help/sites-cloud/authoring/fundamentals/editing-content.md) 如需內容作者如何與元件互動的詳細資訊。

視元件的複雜性而定，您的對話方塊可能需要一或多個索引標籤。

AEM元件的對話方塊：

* 是 `cq:dialog` 類型節點 `nt:unstructured`.
* 位於 `cq:Component` 節點及其元件定義旁。
* 定義用於編輯此元件的內容的對話框。
* 是使用Granite UI元件來定義。
* 會根據其內容結構和 `sling:resourceType` 屬性。
* 包含描述對話框內欄位的節點結構
   * 這些節點是 `nt:unstructured` 和必要 `sling:resourceType` 屬性。

![標題元件的對話框定義](assets/components-title-dialog.png)

在對話方塊中，會定義個別欄位：

![標題元件對話框定義的欄位](assets/components-title-dialog-items.png)

### 設計對話方塊 {#design-dialogs}

設計對話方塊與用來編輯和設定內容的對話方塊類似，但提供範本作者的介面，以在頁面範本上預先設定並提供該元件的設計詳細資料。 內容作者接著會使用頁面範本來建立內容頁面。 請參閱 [範本檔案](/help/sites-cloud/authoring/features/templates.md) 以取得建立範本的詳細資訊。

[編輯頁面範本時會使用設計對話方塊](/help/sites-cloud/authoring/features/templates.md)，但並非所有元件都需要。 例如 **標題** 和 **影像元件** 都有設計對話，而 **社交媒體分享元件** 不會。

### Coral UI和Granite UI {#coral-and-granite}

Coral UI和Granite UI會定義AEM的外觀和風格。

* [Coral UI](https://opensource.adobe.com/coral-spectrum/documentation/) 在所有雲端解決方案中提供一致的UI。
* [Granite UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html) 提供包裝在Sling元件中的Coral UI標籤，以建立UI主控台和對話方塊。

Granite UI提供在製作環境中建立對話方塊所需的大量基本Widget。 如有必要，您可以擴充此選取範圍並建立您自己的介面工具集。

如需其他詳細資訊，請參閱下列資源：

* [AEM UI的結構](/help/implementing/developing/introduction/ui-structure.md)

### 自訂對話方塊欄位 {#customizing-dialog-fields}

<!--
Content not found

>[!TIP]
>
>See the [AEM Gems session](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html) on customizing dialog fields.
-->

若要建立新介面工具集以用於元件對話方塊，您必須建立新的Granite UI欄位元件。

如果您將對話方塊視為表單元素的簡單容器，則您也可以將對話方塊內容的主要內容視為表單欄位。 建立新表單欄位需要建立資源類型；這等同於建立新元件。 為協助您完成該工作，Granite UI提供要繼承的通用欄位元件(使用 `sling:resourceSuperType`):

`/libs/granite/ui/components/coral/foundation/form/field`

更具體來說，Granite UI提供一系列欄位元件，適合用於對話方塊，或更一般地適用於 [表單。](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/index.html)

建立資源類型後，您可以使用屬性在對話方塊中新增節點，以實例化欄位 `sling:resourceType` 指您剛引進的資源類型。

#### 對對話框欄位的訪問 {#access-to-dialog-fields}

您也可以使用演算條件(`rendercondition`)來控制誰有權存取對話方塊中的特定索引標籤/欄位；例如：

```text
+ mybutton
  - sling:resourceType = granite/ui/components/coral/foundation/button
  + rendercondition
    - sling:resourceType = myapp/components/renderconditions/group
    - groups = ["administrators"]
```

## 使用元件 {#using-components}

建立元件後，您必須啟用它，才能使用它。 使用它，可顯示元件的結構與儲存庫中產生內容的結構有何關係。

### 將元件新增至範本 {#adding-your-component-to-the-template}

定義元件後，必須將其提供使用。 要使元件在模板中可用，必須在模板的佈局容器的策略中啟用該元件。

請參閱 [範本檔案](/help/sites-cloud/authoring/features/templates.md) 以取得建立範本的詳細資訊。

### 元件及其建立的內容 {#components-and-the-content-they-create}

如果我們建立並設定 **標題** 元件： `/content/wknd/language-masters/en/adventures/extreme-ironing.html`

![標題編輯對話方塊](assets/components-title-dialog.png)

接著，我們便可查看在存放庫內建立的內容結構：

![標題元件節點結構](assets/components-title-content-nodes.png)

尤其是，如果您查看 **標題元件**:

* 內容包含 `jcr:title` 保有作者輸入標題的實際文本的屬性。
* 它也包含 `sling:resourceType` 參考元件定義。

定義的屬性取決於個別定義。 儘管它們可能比高一些，但它們仍遵循著同樣的基本原則。

## 元件階層和繼承 {#component-hierarchy-and-inheritance}

AEM中的元件受 **資源類型層次結構**. 這可用來使用屬性擴充元件 `sling:resourceSuperType`. 這可讓元件繼承其他元件。

請參閱 [重複使用元件](#reusing-components) 以取得更多資訊。

## 編輯行為 {#edit-behavior}

本節說明如何設定元件的編輯行為。 這包括可用於元件的動作、in.place編輯器的特性，以及與元件上的事件相關的監聽器等屬性。

元件的編輯行為是透過新增 `cq:editConfig` 類型節點 `cq:EditConfig` 元件節點下(類型 `cq:Component`)和新增特定屬性和子節點。 下列屬性和子節點可用：

* `cq:editConfig` 節點屬性
* [`cq:editConfig` 子節點](#configuring-with-cq-editconfig-child-nodes):
   * `cq:dropTargets` （節點類型） `nt:unstructured`):定義可接受內容尋找器資產中的刪除的刪除目標清單（允許單個刪除目標）
   * `cq:inplaceEditing` （節點類型） `cq:InplaceEditingConfig`):定義元件的就地編輯設定
   * `cq:listeners` （節點類型） `cq:EditListenersConfig`):定義元件上發生動作之前或之後發生的內容

AEM中有許多現有設定。 您可以使用以下位置中的「查詢」工具輕鬆搜索特定屬性或子節點： **CRXDE Lite**.

### 元件預留位置 {#component-placeholders}

元件必須一律呈現作者可看見的某些HTML，即使元件沒有內容亦然。 否則，它可能會從編輯器的介面中以視覺化方式消失，從技術上而言，它會呈現在頁面上，但在編輯器中則隱藏。 在這種情況下，作者將無法選取空白元件並與其互動。

因此，只要元件在頁面編輯器中轉譯頁面時(當WCM模式為 `edit` 或 `preview`)。
預留位置的典型HTML標籤如下：

```HTML
<div class="cq-placeholder" data-emptytext="Component Name"></div>
```

轉譯上述預留位置HTML的典型HTL指令碼如下：

```HTML
<div class="cq-placeholder" data-emptytext="${component.properties.jcr:title}"
     data-sly-test="${(wcmmode.edit || wcmmode.preview) && isEmpty}"></div>
```

在上一個範例中， `isEmpty` 為true的變數，唯有元件沒有內容，且作者無法看見。

為避免重複，Adobe建議元件實作者為這些預留位置使用HTL範本， [就像核心元件所提供的一樣。](https://github.com/adobe/aem-core-wcm-components/blob/master/content/src/content/jcr_root/apps/core/wcm/components/commons/v1/templates.html)

接著，您就可使用下列HTL行，在上一個連結中使用範本：

```HTML
<sly data-sly-use.template="core/wcm/components/commons/v1/templates.html"
     data-sly-call="${template.placeholder @ isEmpty=!model.text}"></sly>
```

在上一個範例中， `model.text` 是變數，只有在內容有且可見時，才會設為true。

您可以在核心元件中查看此範本的使用範例， [例如標題元件中。](https://github.com/adobe/aem-core-wcm-components/blob/master/content/src/content/jcr_root/apps/core/wcm/components/title/v2/title/title.html#L27)

### 使用cq:EditConfig子節點進行配置 {#configuring-with-cq-editconfig-child-nodes}

#### 將資產拖曳至對話方塊 — cq:dropTargets {#cq-droptargets}

此 `cq:dropTargets` 節點（節點類型） `nt:unstructured`)會定義放置目標，以接受從內容尋找器拖曳的資產中的放置。 它是類型的節點 `cq:DropTargetConfig`.

類型的子節點 `cq:DropTargetConfig` 定義元件中的放置目標。

### 就地編輯 — cq:inplaceEditing {#cq-inplaceediting}

就地編輯器可讓使用者直接編輯內容流程中的內容，而不需開啟對話方塊。 例如，標準 **文字** 和 **標題** 元件都有inp-lace編輯器。

就地編輯器對於每個元件類型並非必要/有意義的。

此 `cq:inplaceEditing` 節點（節點類型） `cq:InplaceEditingConfig`)會定義元件的就地編輯設定。 它可以有下列屬性：

| 屬性名稱 | 屬性類型 | 屬性值 |
|---|---|---|
| `active` | `Boolean` | `true` 啟用元件就地編輯。 |
| `configPath` | `String` | 編輯器配置的路徑，可由配置節點指定 |
| `editorType` | `String` | 可用類型包括： `plaintext` 針對非HTML內容， `title` 在開始編輯之前將圖形標題轉換為純文字， `text` 使用RTF編輯器 |

下列設定可啟用元件的內嵌編輯，並定義 `plaintext` 作為編輯器類型：

```text
    <cq:inplaceEditing
        jcr:primaryType="cq:InplaceEditingConfig"
        active="{Boolean}true"
        editorType="plaintext"/>
```

### 處理欄位事件 — cq:listeners {#cq-listeners}

處理對話欄位上事件的方法是使用自訂的接聽程式來完成 [用戶端程式庫。](/help/implementing/developing/introduction/clientlibs.md)

若要將邏輯插入欄位，您應：

* 將欄位標示為指定的CSS類別（連結）。
* 在用戶端程式庫中定義掛接該CSS類別名稱的JS接聽程式（這可確保您的自訂邏輯限定在您的欄位內，而不會影響相同類型的其他欄位）。

若要達成此目標，您必須了解您要與之互動的基礎Widget程式庫。 [請參閱Coral UI檔案](https://opensource.adobe.com/coral-spectrum/documentation/) 以識別您要對哪個事件做出反應。

此 `cq:listeners` 節點（節點類型） `cq:EditListenersConfig`)會定義元件上的動作之前或之後會發生什麼事。 下表定義了其可能的屬性。

| 屬性名稱 | 屬性值 |
|---|---|
| `beforedelete` | 處理常式會在元件移除前觸發。 |
| `beforeedit` | 在編輯元件之前會觸發處理常式。 |
| `beforecopy` | 處理常式會在複製元件之前觸發。 |
| `beforeremove` | 處理常式會在元件移動前觸發。 |
| `beforeinsert` | 處理常式會在插入元件之前觸發。 |
| `beforechildinsert` | 處理常式會在元件插入至其他元件（僅限容器）之前觸發。 |
| `afterdelete` | 移除元件後，就會觸發處理常式。 |
| `afteredit` | 編輯元件後，就會觸發處理常式。 |
| `aftercopy` | 在複製元件後會觸發處理常式。 |
| `afterinsert` | 插入元件後會觸發處理常式。 |
| `aftermove` | 移動元件後會觸發處理常式。 |
| `afterchildinsert` | 將元件插入另一個元件（僅限容器）後，就會觸發處理常式。 |

>[!NOTE]
>
>若是巢狀元件，對定義為上屬性的動作會有某些限制 `cq:listeners` 節點。 對於嵌套元件，以下屬性的值 **必須** be `REFRESH_PAGE`:
>
>* `aftermove`
>* `aftercopy`


事件處理常式可透過自訂實作來實作。 例如(其中 `project.customerAction` 是靜態方法):

`afteredit = "project.customerAction"`

下列範例等同於 `REFRESH_INSERTED` 配置：

`afterinsert="function(path, definition) { this.refreshCreated(path, definition); }"`

使用下列配置時，在元件被刪除、編輯、插入或移動後刷新頁面：

```text
    <cq:listeners
        jcr:primaryType="cq:EditListenersConfig"
        afterdelete="REFRESH_PAGE"
        afteredit="REFRESH_PAGE"
        afterinsert="REFRESH_PAGE"
        afterMove="REFRESH_PAGE"/>
```

### 欄位驗證 {#field-validation}

在Granite UI和Granite UI介面工具集中進行欄位驗證，方法是使用 `foundation-validation` API。 請參閱 [`foundation-valdiation` Granite檔案](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/clientlibs/foundation/js/validation/index.html) 以取得詳細資訊。

### 檢測對話框的可用性 {#dialog-ready}

如果您有自訂JavaScript，只需在對話方塊可用且準備就緒時執行，則應監聽 `dialog-ready` 事件。

每當對話方塊載入（或重新載入）且可供使用時，就會觸發此事件，這表示每當對話方塊的DOM中有變更（建立/更新）時。

`dialog-ready` 可用來在JavaScript自訂程式碼中連結，該程式碼會對對話方塊或類似工作中的欄位執行自訂。

## 預覽行為 {#preview-behavior}

此 [WCM模式](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/WCMMode.html) 切換至「預覽」模式時，即使未重新整理頁面，也會設定cookie。

對於呈現時對WCM模式敏感的元件，必須定義元件以明確重新整理元件，然後仰賴Cookie的值。

## 檔案元件 {#documenting-components}

身為開發人員，您需要輕鬆存取元件檔案，以便快速了解元件的：

* 說明
* 預期用途
* 內容結構和屬性
* 公開的API和擴充功能點
* 等

因此，很容易就能在元件本身內使用任何現有的檔案標籤。

你只需把 `README.md` 檔案。

![元件結構中的README.md](assets/components-documentation.png)

此標籤下拉式清單會顯示在 [元件主控台。](/help/sites-cloud/authoring/features/components-console.md)

![元件控制台中顯示的README.md](assets/components-documentation-console.png)

支援的Markdown與 [內容片段](/help/sites-cloud/administering/content-fragments/content-fragments.md).
