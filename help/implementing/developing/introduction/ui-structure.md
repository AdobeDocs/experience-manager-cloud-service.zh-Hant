---
title: AEM UI 的結構
description: AEM UI具有數項基礎原則，並由數項關鍵元素組成
exl-id: ac211716-d699-4fdb-a286-a0a1122c86c5
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 3%

---

# AEM UI 的結構 {#structure-of-the-aem-ui}

AEM UI具有幾項基礎原則，而且由數個關鍵元素組成：

## 主控台 {#consoles}

### 基本版面與調整大小 {#basic-layout-and-resizing}

UI同時適用於行動裝置和桌上型裝置，不過AEM並非建立兩種樣式，而是使用一種適用於所有熒幕和裝置的樣式。

所有模組都使用相同的基本版面配置：

![AEM Sites主控台](assets/ui-sites-console.png)

此版面會遵循回應式設計樣式，並符合您所使用的裝置、視窗或兩者的大小。

例如，當解析度低於1024畫素時（如同在行動裝置上），畫面會據此調整：

![網站主控台行動裝置檢視](assets/ui-sites-mobile.png)

### 標題列 {#header-bar}

![AEM標頭列](assets/ui-header-bar.png)

標題列會顯示全域元素，包括：

* 標誌與您目前使用的特定產品/解決方案。 若為AEM，此元素也會形成全域導覽的連結
* 搜尋
* 用於存取說明資源的圖示
* 存取其他解決方案的圖示
* 任何警示或收件匣專案正在等待您的指示器 — 以及對其的存取權
* 使用者圖示，以及設定檔管理的連結

### 工具列 {#toolbar}

工具列會與您的位置及表面工具相關，與控制以下頁面中的檢視或資產相關。 工具列是產品專屬的，但這些元素有一些共同之處。

在任何位置，工具列都會顯示目前可用的動作：

![AEM Sites工具列](assets/ui-sites-toolbar.png)

也取決於是否選取資源：

已選取![AEM Sites工具列](assets/ui-sites-toolbar-selected.png)

### 左側邊欄 {#left-rail}

您可以視需要開啟/隱藏左側邊欄，以顯示：

* **僅內容**
* **內容樹**
* **時間表**
* **參照**
* **篩選器**

預設值為&#x200B;**僅內容** （隱藏邊欄）。

![左側邊欄](assets/ui-left-rail.png)

## 頁面製作 {#page-authoring}

編寫頁面時，結構區域如下。

### 內容框架 {#content-frame}

頁面內容會在內容框架中呈現。 內容框架獨立於編輯器 — 以確保不會因CSS或JavaScript而發生衝突。

內容框架位於視窗的右側區段（在工具列下）。

![內容框架](assets/ui-content-frame.png)

### 編輯器框架 {#editor-frame}

編輯器框架會啟用編輯功能。

編輯器框架是所有頁面製作元素的容器（摘要）。 它位在內容框架頂端，包括：

* 頂端工具列
* 側面板
* 所有覆蓋
* 任何其他頁面製作元素；例如，元件工具列

![編輯器框架](assets/ui-editor-frame.png)

### 側面板 {#side-panel}

包含三個預設標籤。 **Assets**&#x200B;和&#x200B;**元件**&#x200B;索引標籤可讓您選取這類元素，並將它們從面板拖放到頁面上。 **內容樹狀結構**&#x200B;索引標籤可讓您檢查頁面上內容的階層。

側面板預設為隱藏。 選取時，該視窗會顯示在左側，或當視窗寬度小於1024畫素時，它會滑過以覆蓋整個視窗，例如在行動裝置上。

![側面板](assets/ui-side-panel.png)

### 側面板 — Assets {#side-panel-assets}

在Assets標籤中，您可以從資產範圍中選取。 您也可以篩選特定字詞，或選取群組。

![Assets索引標籤](assets/ui-side-panel-assets.png)

### 側面板 — 資產群組 {#side-panel-asset-groups}

在Assets索引標籤中，有一個下拉式清單可用來選取特定資產群組。

![資產群組](assets/ui-side-panel-asset-groups.png)

### 側面板 — 元件 {#side-panel-components}

在「元件」標籤中，您可以從元件範圍中選取。 您也可以篩選特定字詞，或選取群組。

![元件標籤](assets/ui-side-panel-components.png)

### 側面板 — 內容樹 {#side-panel-content-tree}

在「內容樹狀結構」標籤中，您可以檢視頁面上內容的階層。 按一下索引標籤中的專案會跳至，並在編輯器內選取頁面上的專案。

![內容樹](assets/ui-side-panel-content-tree.png)

### 覆蓋 {#overlays}

覆蓋內容框架，並由[圖層](#layer)使用，以達成與元件及其內容透明互動的機制。

這些覆蓋圖會在編輯器框架中呈現（包含所有其他頁面製作元素），不過實際上會在內容框架中覆蓋適當的元件。

![重疊](assets/ui-overlays.png)

### 圖層 {#layer}

圖層是獨立的功能組合，可以啟動為：

* 提供頁面的不同檢視
* 允許您操控和/或與頁面互動

這些圖層提供整個頁面的複雜功能，而非個別元件上的特定動作。

AEM隨附數個已實作用於頁面製作的圖層；例如包括編輯、預覽和註釋圖層。

>[!NOTE]
>
>圖層是一個強大的概念，可影響使用者對頁面內容的檢視以及與頁面內容的互動。 開發您自己的圖層時，請確定圖層在退出時進行清除。

### 圖層切換器 {#layer-switcher}

圖層切換器可讓您選擇要使用的圖層。 關閉時，它會指出目前使用的圖層。

圖層切換器可從工具列（在視窗頂端、編輯器框架中）以下拉式清單形式提供。

![圖層切換器](assets/ui-layer-switcher.png)

### 元件工具列 {#component-toolbar}

元件的每個例項在按一下（一次或緩慢按兩下）時都會顯示其工具列。 工具列包含頁面上元件執行個體可用的特定動作（例如，複製、貼上、開啟編輯器）。

根據可用的空間，元件工具列會放置在適當元件的右上角或右下角。

![元件工具列](assets/ui-component-toolbar.png)

## 更多資訊 {#further-information}

<!--For more details about the concepts around the touch-enabled UI, continue to the article [Concepts of the AEM Touch-Enabled UI](/help/sites-developing/touch-ui-concepts.md).-->

如需更多技術資訊，請參閱頁面編輯器的[JS檔案集](https://developer.adobe.com/experience-manager/reference-materials/6-5/jsdoc/ui-touch/editor-core/index.html)。

### Unified Shell {#unified-shell}

如果您使用Unified Shell做為AEM UI，請參閱[Unified Shell上的AEM as a Cloud Service](/help/overview/aem-cloud-service-on-unified-shell.md)。

如果您需要進行任何自訂，或已經進行任何自訂，則可停用「統一」：

* [從UI](/help/overview/aem-cloud-service-on-unified-shell.md#disabling-unified-shell)

* 從您的專案程式碼，依：

   * 於`/conf/global/setting/unifiedshell`

      * 將`Boolean`屬性`enable`設定為`false`
