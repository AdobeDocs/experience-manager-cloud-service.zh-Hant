---
title: 製作環境與工具
description: 的製作環境提AEM供多種機制來組織和編輯您的內容
translation-type: tm+mt
source-git-commit: 95ac5e5f6c49d5a2d7aef5dcf30d8298fd459457
workflow-type: tm+mt
source-wordcount: '2152'
ht-degree: 13%

---


# 製作環境與工具{#authoring-the-environment-and-tools}

的製作環境提AEM供多種機制來組織和編輯您的內容。 提供的工具可從各種控制台和頁面編輯器中存取。

## 管理您的網站{#managing-your-site}

Sites **** Console可讓您使用標題列、工具列、動作圖示 (適用於選取的資源) 、導覽路徑標示，以及選取時的輔助導軌 (例如時間軸和參考)，來導覽和管理您的網站。

例如，列視圖：

![欄檢視](/help/sites-cloud/authoring/assets/column-view.png)

## 編輯頁面內容 {#editing-page-content}

您可以使用頁面編輯器編輯頁面。 例如：

`http://<host>:<port>/editor.html/content/wknd/en/sports/la-skateparks.html`

![頁面編輯器](/help/sites-cloud/authoring/assets/page-editor.png)

>[!NOTE]
>
>當您第一次開啟頁面進行編輯時，一連串的投影片會提供您功能指南。
>
>您可以視需要略過導覽，並隨時從&#x200B;**頁面資訊**&#x200B;選單中選取以重複。

## 訪問幫助{#accessing-help}

編輯頁面時，可從以下位置訪問&#x200B;**Help**:

* [**頁面資訊**](/help/sites-cloud/authoring/fundamentals/page-properties.md#page-properties)&#x200B;選擇器，顯示簡介投影片（如您第一次存取編輯器時所顯示）
* 特定元件的[configuration](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar)對話方塊(使用？ 表徵圖)，顯示上下文相關幫助

控制台](/help/sites-cloud/authoring/getting-started/basic-handling.md#accessing-help)還提供與幫助相關的其他資源。[

## 元件瀏覽器{#components-browser}

元件是內容的建AEM構區塊。 您可以在頁面上放置多個元件並設定其選項，以便使用來建立內容頁面AEM。

元件瀏覽器會顯示目前頁面上可用的所有元件。 這些內容可拖曳至適當位置，然後進行編輯以新增內容。

元件瀏覽器是側面板中的標籤(連同資產 [瀏覽器](#assets-browser)[和內容樹](#content-tree))。要開啟 (或關閉) 側面板，請使用工具欄左上角的表徵圖：

![側面板切換](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

當您開啟側面板時，它會從左側滑動開啟（如有必要，請選取「**元件**」標籤）。 開啟時，您可以瀏覽頁面的所有可用元件。

實際外觀和處理方式取決於您使用的設備類型：

* **行動裝置（例如iPad）**

   元件瀏覽器完全涵蓋正在編輯的頁面。

   若要將元件新增至頁面，並按住所需的元件並向右移動——元件瀏覽器會關閉，再次顯示頁面——您可在此處放置元件。

   ![行動裝置上的元件瀏覽器](/help/sites-cloud/authoring/assets/component-browser-mobile.png)

* **案頭裝置**

   元件瀏覽器在窗口的左側開啟。

   若要將元件新增至您的頁面，請按一下所需元件，並將其拖曳至所需位置。

   ![案頭上的元件瀏覽器](/help/sites-cloud/authoring/assets/component-browser-desktop.png)

   元件由

   * 元件名稱
   * 元件群組（以灰色顯示）
   * 圖示或縮寫
      * 標準元件的圖示為單色。
      * 縮寫永遠是元件名稱的前兩個字元。

   從&#x200B;**Components**&#x200B;瀏覽器的頂部工具欄，您可以：

   * 依名稱篩選元件。
   * 使用下拉式選取範圍，將顯示限制在特定群組。

   如需元件的詳細說明，您可以在「元件」瀏覽器中按一下或點選元件旁的資訊圖示(如果 **有** )。例如，對於&#x200B;**內容片段**:

   ![元件瀏覽器資訊](/help/sites-cloud/authoring/assets/component-browser-information.png)

   有關可用元件的更多資訊，請參閱[元件控制台](/help/sites-cloud/authoring/features/components-console.md)。

>[!NOTE]
>
>當寬度小於1024px時檢測到移動設備。 此外，小型案頭視窗也可能適用。

## 資產瀏覽器{#assets-browser}

資產瀏覽器會顯示目前頁面上所有可直接使用的[資產](/help/assets/home.md)。

資產瀏覽器是側面板中的標籤，以及元件瀏 [覽器](#components-browser)[和內容樹](#content-tree)。要開啟或關閉側面板，請使用工具欄左上角的表徵圖：

![側面板切換](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

當您開啟側面板時，它會從左側滑動開啟。 如有必要，請選擇&#x200B;**Assets**&#x200B;標籤。

![資產瀏覽器按鈕](/help/sites-cloud/authoring/assets/assets-browser-button.png)

當資產瀏覽器開啟時，您可以瀏覽頁面的所有可用資產。 視需要使用無限捲動來展開清單。

![資產瀏覽器](/help/sites-cloud/authoring/assets/assets-browser.png)

若要將資產新增至頁面，請選取並拖曳至所需位置。 這可以是：

* 適當類型的現有元件。
   * 例如，您可以將文字影像的資產拖曳至影像元件上。
* 段落系統中的[佔位符](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-placeholder)可建立適當類型的新元件。
   * 例如，您可以將文字影像的資產拖曳至段落系統，以建立影像元件。

>[!NOTE]
>
>這適用於特定資產和元件類型。 如需詳細資訊，請參閱[使用資產瀏覽器插入元件](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component-using-the-assets-browser)。

從資產瀏覽器的頂端工具列，您可以依下列方式篩選資產：

* 名稱
* 路徑
* 資產類型，例如影像、視訊、檔案、段落、內容片段和體驗片段
* 資產特性，例如方向和樣式
   * 僅適用於特定資產類型

實際外觀和處理方式取決於您使用的設備類型：

* **行動裝置**

   資產瀏覽器會完全涵蓋正在編輯的頁面。

   若要將資產新增至頁面並按住必要的資產，然後將其向右移動——資產瀏覽器會關閉以再次顯示頁面，您可在其中將資產新增至所需元件。

   ![行動裝置上的資產瀏覽器](/help/sites-cloud/authoring/assets/assets-browser-mobile.png)

* **案頭裝置**

   資產瀏覽器會在視窗左側開啟。

   若要將資產新增至頁面，請按一下所需資產，然後拖曳至所需元件或位置。

   ![案頭上的資產瀏覽器](/help/sites-cloud/authoring/assets/assets-browser-desktop.png)

>[!NOTE]
>
>當移動設備寬度小於1024px時，檢測到移動設備；例如，也可在小型案頭視窗上。

如果您需要快速變更資產，可以按一下資產名稱旁的編輯圖示，直接從資產瀏覽器啟動[資產編輯器](/help/assets/manage-digital-assets.md)。

![資產編輯按鈕](/help/sites-cloud/authoring/assets/asset-edit-button.png)

## 內容樹 {#content-tree}

**內容樹**&#x200B;概述了分層結構中頁面上的所有元件，讓您一目瞭然地瞭解頁面的構成方式。

「內容樹」是側面板（連同元件和資產瀏覽器）中的標籤。 要開啟 (或關閉) 側面板，請使用工具欄左上角的表徵圖：

![內容樹按鈕](/help/sites-cloud/authoring/assets/content-tree-button.png)

當您開啟側面板時，它會滑開（從左側）。 如有必要，請選擇&#x200B;**內容樹**&#x200B;頁籤。 當開啟時，您可以看到頁面或範本的樹狀檢視表示，以便更輕鬆地瞭解其內容的階層式結構。 此外，在複雜的頁面上，可更輕鬆地在頁面的元件之間跳轉。

![內容樹](/help/sites-cloud/authoring/assets/content-tree-editor.png)

頁面可輕鬆由許多相同類型的元件組成，因此內容（元件）樹狀結構會在元件類型名稱（黑色）後顯示描述性文字（以灰色顯示）。 描述性文字來自元件的常用屬性，例如標題或文字。

元件類型將以用戶語言顯示，而元件說明文本則來自頁面語言。

按一下元件旁邊的雪佛龍將折疊或展開該級別。

![Content Tree擴充雪佛龍](/help/sites-cloud/authoring/assets/content-tree-chevron.png)

按一下元件會在頁面編輯器中反白顯示元件。 可用的動作將視頁面狀態而定：

* 例如，基本頁面：

   ![反白顯示內容樹狀結構](/help/sites-cloud/authoring/assets/content-tree-highlighted.png)

   基本頁面的元件將具有一般選項。

   如果您在樹狀結構中按一下的元件是可編輯的，則名稱右側會出現扳手圖示。 按一下此表徵圖將直接啟動元件的編輯對話框。

   ![內容樹編輯按鈕](/help/sites-cloud/authoring/assets/content-tree-edit.png)

* 屬於[livecopy](/help/sites-cloud/administering/msm/overview.md)一部分的頁面，其中元件繼承自其他頁面。

>[!NOTE]
>
>如果您在行動裝置上編輯頁面（如果瀏覽器寬度小於1024像素），則無法使用「內容樹」。

## 片段——關聯的內容瀏覽器{#fragments-associated-content-browser}

如果您的頁面包含內容片段，則您也可以存取[瀏覽器以取得關聯的內容](/help/sites-cloud/authoring/fundamentals/content-fragments.md#using-associated-content)。

## 引用 {#references}

**參** 考顯示到選定頁的連接：

* BluePrint
* 啟動
* 即時副本
* 語言副本
* 導入連結
* 使用參考元件：借閱和借閱內容

開啟所需的控制台，然後導航到所需資源，並使用以下方式開啟&#x200B;**引用**:

![參考選項](/help/sites-cloud/authoring/assets/references.png)

[選擇所需](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) 資源以顯示與該資源相關的參考型別清單：

![參考詳細資料](/help/sites-cloud/authoring/assets/references-detail.png)

選擇適當的參考類型以瞭解詳細資訊。 在某些情況下，當您選擇特定參照時，可以執行其他操作，包括：

* **傳入連結**，提供參考頁面的頁面清單，以及當您選取特定連結時，可直接存取這些頁 **** 面的「編輯」功能
* 使用&#x200B;**Reference**&#x200B;元件借閱和借閱內容的例項，您可從這裡導覽至參考／參考頁面
* [啟動](/help/sites-cloud/authoring/launches/overview.md)，提供相關啟動的存取權
* [即時](/help/sites-cloud/administering/msm/overview.md) 副本顯示所有基於所選資源的即時副本的路徑。
* [Blueprint](/help/sites-cloud/administering/msm/best-practices.md)，提供詳細資訊和各種動作
* [語言復本](/help/sites-cloud/administering/translation/managing-projects.md#creating-translation-projects-using-the-references-panel)，提供詳細資訊和各種動作

## 事件——時間軸{#events-timeline}

對於適當的資源（例如&#x200B;**Sites**&#x200B;控制台中的頁面，或&#x200B;**Assets**&#x200B;控制台中的資產）,[時間軸可用於顯示任何選定項目上的最近活動](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)。

開啟必要的主控台，然後導覽至所需的資源，並開啟&#x200B;**時間軸**，使用：

![時間軸選項](/help/sites-cloud/authoring/assets/timeline.png)

[選擇所需資源](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)，然後選擇 **顯示** 所有活 **** 動以列出所選資源上的任何最近操作：

![時間軸詳細資訊](/help/sites-cloud/authoring/assets/timeline-detail.png)

## 頁面資訊 {#page-information}

「頁面資訊 (均衡器圖示) 」會開啟一個功能表，其中也提供上次編輯和上次發佈的詳細資訊。視頁面、其網站和您的例項的特性而定，可能有更多或更少的選項可用：

![頁面資訊選項](/help/sites-cloud/authoring/assets/page-information.png)

* [開啟屬性](/help/sites-cloud/authoring/fundamentals/page-properties.md)
* [轉出頁面](/help/sites-cloud/administering/msm/overview.md#msm-from-the-ui)
* [啟動工作流程](/help/sites-cloud/authoring/workflows/applying.md#starting-a-workflow-from-the-page-editor)
* [鎖定頁面](/help/sites-cloud/authoring/fundamentals/editing-content.md#locking-a-page)
* [發佈頁面](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#publishing-pages-1)
* [取消發佈頁面](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#unpublishing-pages)
* [編輯範本](/help/sites-cloud/authoring/features/templates.md)
* [以已發佈狀態檢視](/help/sites-cloud/authoring/fundamentals/editing-content.md#view-as-published)
* [在 Admin 中檢視](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)
* [說明](/help/sites-cloud/authoring/getting-started/basic-handling.md#accessing-help)
* [促銷啟動](/help/sites-cloud/authoring/launches/promoting.md) （僅在頁面為啟動時）

此外，**頁面資訊**&#x200B;可在適當時提供分析和建議的存取權。

## 頁面模式{#page-modes}

編輯頁面時有多種模式，允許執行不同的動作：

* [編輯](/help/sites-cloud/authoring/fundamentals/editing-content.md) -編輯頁面內容時使用的模式。
* [版面](/help/sites-cloud/authoring/features/responsive-layout.md) -可讓您根據裝置建立和編輯互動式版面（如果頁面是以版面容器為基礎）
* [定位](/help/sites-cloud/authoring/personalization/targeted-content.md) -透過跨所有通道的定位和測量來提高內容相關性。
* [時間彎曲](/help/sites-cloud/authoring/features/page-versions.md#timewarp) -可讓您在特定時間點檢視頁面狀態。
* [即時副本狀態](/help/sites-cloud/authoring/fundamentals/editing-content.md#live-copy-status) -可快速概述即時副本狀態，以及哪些元件是／未繼承的。
* [預覽](/help/sites-cloud/authoring/fundamentals/editing-content.md#previewing-pages) -用於檢視頁面在發佈環境中的顯示效果；或在內容中使用連結進行導覽。
* [Annotate](/help/sites-cloud/authoring/fundamentals/annotations.md)  —— 用於在頁面上添加或查看批注。

您可以使用右上角的圖示來存取這些圖示。 實際圖示會變更，以反映您目前使用的模式：

![頁面模式](/help/sites-cloud/authoring/assets/page-modes.png)

>[!NOTE]
>
>* 根據頁面的特性，某些模式可能無法使用。
>* 存取某些模式需要適當的權限／權限。
>* 由於空間限制，行動裝置無法使用開發人員模式。
>* 有一個鍵 [盤](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) ( `Ctrl-Shift-M`可切換 **)，在「預覽」和目前選取的模式之間切換(例如，「編輯」、「排版**********」等)。

>



## 路徑選擇{#path-selection}

通常在編寫時，需要選擇其他資源，例如定義到其他頁面或資源的連結或選擇映像。 為了輕鬆選擇路徑，[路徑欄位](#path-fields)提供自動完成功能，而[路徑瀏覽器](#path-browser)則提供更強穩的選擇。

### 路徑欄位{#path-fields}

這裡用來說明的範例是影像元件。 有關使用和編輯元件的詳細資訊，請參閱[ Components for Page Authoring](/help/sites-cloud/authoring/fundamentals/components.md)。

路徑欄位現在具備自動完成和前瞻功能，讓尋找資源變得更輕鬆。

按一下路徑欄位中的&#x200B;**開啟選擇對話框**&#x200B;按鈕可開啟路徑瀏覽器](#path-browser)對話框，以提供更詳細的選擇選項。[

![「開啟選擇對話框」按鈕](/help/sites-cloud/authoring/assets/open-selection-dialog-button.png)

或者，您可以開始在路徑欄位中輸入，AEM並在輸入時提供相符的路徑。

![「開啟選擇對話框」按鈕](/help/sites-cloud/authoring/assets/path-selection-completion.png)

### 路徑瀏覽器 {#path-browser}

路徑瀏覽器的組織方式與站點控制台的[列視圖](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view)類似，允許更詳細地選擇資源。

![路徑瀏覽器](/help/sites-cloud/authoring/assets/path-browser.png)

* 在選擇資源後，對話框右上方的&#x200B;**選擇**&#x200B;按鈕將變為活動狀態。 按一下或點選以確認選擇，或&#x200B;**取消**&#x200B;中止。
* 如果上下文允許選擇多個資源，則選擇資源也會激活「選擇 **** 」按鈕，但也會向窗口的右上角添加選定資源的計數。按一下 **數字旁** 的X，取消選取全部。
* 在樹狀結構中導覽時，您的位置會反映在對話方塊頂端的階層連結中。 這些網站導覽路徑標示也可用來快速跳入資源階層。
* 您隨時都可以使用對話方塊頂端的搜尋欄位。 按一下搜尋欄位中的&#x200B;**X**&#x200B;以清除搜尋。
* 若要縮小搜尋範圍，您可以顯示篩選選項並根據特定路徑篩選結果。

   ![濾鏡選項](/help/sites-cloud/authoring/assets/filters-option.png)

## 鍵盤快速鍵 {#keyboard-shortcuts}

有各種[鍵盤快速鍵](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)可供使用。
