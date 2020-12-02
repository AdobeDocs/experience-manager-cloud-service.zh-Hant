---
title: AEM UI的結構
description: AEM UI包含數個基本原則，並由數個關鍵元素組成
translation-type: tm+mt
source-git-commit: 0799a817095558edd49b53ddc915c9474181fef7
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 2%

---


# AEM UI {#structure-of-the-aem-ui}的結構

AEM UI包含數個基本原則，由數個關鍵元素組成：

## 控制台{#consoles}

### 基本版面配置和調整大小{#basic-layout-and-resizing}

AEM適用於行動與桌上型裝置，但並非建立兩種樣式，而是使用一種樣式，適用於所有螢幕和裝置。

所有模組都使用相同的基本版面，在AEM中，這可以看成：

![AEM Sites主控台](assets/ui-sites-console.png)

版面符合回應式設計樣式，並可配合您使用的裝置／視窗大小。

例如，當解析度低於1024像素（如行動裝置）時，顯示器會隨之調整：

![網站主控台行動檢視](assets/ui-sites-mobile.png)

### 標題列 {#header-bar}

![AEM標題列](assets/ui-header-bar.png)

標題列顯示全域元素，包括：

* 標誌和您目前使用的特定產品／解決方案；對於AEM，這也會形成全域導覽的連結
* 搜尋
* 用於訪問幫助資源的表徵圖
* 用於訪問其他解決方案的表徵圖
* 指示（並訪問）等待您的任何警報或收件箱項目的指示符
* 使用者圖示，以及您的描述檔管理連結

### 工具列 {#toolbar}

工具列與您的位置相關，並呈現與控制頁面中的檢視或資產相關的工具。 工具列是特定於產品的，但是這些元素有一些通用性。

在任何位置，工具列都會顯示目前可用的動作：

![AEM Sites工具列](assets/ui-sites-toolbar.png)

還取決於當前是否選擇了資源：

![已選取AEM Sites工具列](assets/ui-sites-toolbar-selected.png)

### 左側邊欄 {#left-rail}

左側邊欄可視需要開啟／隱藏，以顯示：

* **僅限內容**
* **內容樹**
* **時間軸**
* **引用**
* **篩選**

預設值為&#x200B;**僅內容**（隱藏邊欄）。

![左側邊欄](assets/ui-left-rail.png)

## 頁面編寫{#page-authoring}

編寫頁面時，結構區域如下。

### 內容影格{#content-frame}

頁面內容會在內容影格中呈現。 內容影格完全獨立於編輯器——以確保不會因CSS或javascript而產生衝突。

內容影格位於視窗的右側區段、工具列下方。

![內容影格](assets/ui-content-frame.png)

### 編輯器幀{#editor-frame}

編輯器框架可啟用編輯功能。

編輯器框架是所有頁面製作元素的容器（抽象）。 它位於內容框架之上，並包含：

* 頂端工具列
* 側面板
* 所有覆蓋
* 任何其他頁面製作元素；例如，元件工具列

![編輯器框架](assets/ui-editor-frame.png)

### 側面板{#side-panel}

這包含三個預設標籤。 **Assets**&#x200B;和&#x200B;**Components**&#x200B;標籤可讓您選取這些元素，並從面板拖曳這些元素並拖曳至頁面。 使用&#x200B;**內容樹**&#x200B;頁籤可以檢查頁面上的內容層次。

側面板預設為隱藏。 當選取時，會顯示在左側，或當視窗大小低於1024像素寬度時，會滑過以覆蓋整個視窗；例如，在行動裝置上。

![側面板](assets/ui-side-panel.png)

### 側面板——資產{#side-panel-assets}

在「資產」索引標籤中，您可以從資產範圍中選取。 您也可以篩選特定詞語，或選取群組。

![資產標籤](assets/ui-side-panel-assets.png)

### 側面板——資產群組{#side-panel-asset-groups}

在「資產」標籤中，有一個下拉式清單可供您用來選取特定資產群組。

![資產群組](assets/ui-side-panel-asset-groups.png)

### 側面板——元件{#side-panel-components}

在「元件」索引標籤中，您可以從元件範圍中選取。 您也可以篩選特定詞語，或選取群組。

![「元件」頁籤](assets/ui-side-panel-components.png)

### 側面板——內容樹{#side-panel-content-tree}

在「內容樹」索引標籤中，您可以檢視頁面上的內容階層。 按一下標籤中的項目會跳至編輯器中的頁面上，並選取項目。

![內容樹](assets/ui-side-panel-content-tree.png)

### 覆蓋{#overlays}

這些內容覆蓋內容影格，並由[圖層](#layer)使用，以瞭解如何（完全透明）與元件及其內容互動的機制。

覆蓋會在編輯器影格中顯示（與所有其他頁面製作元素一起顯示），不過實際覆蓋內容影格中的適當元件。

![覆蓋](assets/ui-overlays.png)

### 層{#layer}

圖層是一組獨立的功能，可以激活它以：

* 提供頁面的不同檢視
* 可讓您控制和／或與頁面互動

這些圖層可為整個頁面提供複雜的功能，而不是個別元件上的特定動作。

AEM隨附數個已建置用於頁面製作的圖層；例如，編輯、預覽和註解圖層。

>[!NOTE]
>
>圖層是強大的概念，會影響使用者對頁面內容的檢視和互動。 在開發您自己的圖層時，您需要確保該圖層在退出時清理乾淨。

### 圖層切換器{#layer-switcher}

圖層切換器可讓您選擇要使用的圖層。 關閉時，它表示當前正在使用的層。

圖層切換器可從工具列（位於視窗頂部，位於編輯器框架內）下拉式清單中取用。

![圖層切換器](assets/ui-layer-switcher.png)

### 元件工具欄{#component-toolbar}

每個元件例項都會在按下時顯示其工具列（按一下一次或按兩下慢速）。 工具列包含頁面上元件實例可用的特定操作（例如複製、貼上、開啟編輯器）。

視可用空間而定，元件工具欄位於相應元件的右上角或右下角。

![元件工具列](assets/ui-component-toolbar.png)

## 更多資訊 {#further-information}

<!--For more details about the concepts around the touch-enabled UI, continue to the article [Concepts of the AEM Touch-Enabled UI](/help/sites-developing/touch-ui-concepts.md).-->

如需詳細的技術資訊，請參閱頁面編輯器的[JS檔案集](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html)。
