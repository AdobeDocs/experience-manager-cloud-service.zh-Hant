---
title: 製作環境和工具
description: AEM的製作環境提供多種機制，可組織及編輯您的內容
exl-id: cc3bd4cf-93bd-429d-9a2a-4a02a7b42f7c
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '2152'
ht-degree: 13%

---

# 製作環境和工具{#authoring-the-environment-and-tools}

AEM的製作環境提供多種組織及編輯內容的機制。 提供的工具可從各種主控台和頁面編輯器存取。

## 管理您的站點{#managing-your-site}

Sites **** Console可讓您使用標題列、工具列、動作圖示 (適用於選取的資源) 、導覽路徑標示，以及選取時的輔助導軌 (例如時間軸和參考)，來導覽和管理您的網站。

例如，欄檢視：

![欄檢視](/help/sites-cloud/authoring/assets/column-view.png)

## 編輯頁面內容 {#editing-page-content}

您可以使用頁面編輯器編輯頁面。 例如：

`http://<host>:<port>/editor.html/content/wknd/en/sports/la-skateparks.html`

![頁面編輯器](/help/sites-cloud/authoring/assets/page-editor.png)

>[!NOTE]
>
>第一次開啟頁面進行編輯時，您會看到一系列投影片，為您帶來功能導覽。
>
>您可以視需要略過導覽，並隨時透過從&#x200B;**頁面資訊**&#x200B;選單中選取來重複。

## 訪問幫助{#accessing-help}

編輯頁面時，可從以下位置存取&#x200B;**Help**:

* 顯示介紹性投影片的&#x200B;[**頁面資訊**](/help/sites-cloud/authoring/fundamentals/page-properties.md#page-properties)&#x200B;選取器（如您第一次存取編輯器時所顯示）
* 特定元件的[configuration](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar)對話方塊(使用？ 圖示)，其中顯示上下文相關幫助

控制台](/help/sites-cloud/authoring/getting-started/basic-handling.md#accessing-help)還提供[幫助相關資源。

## 元件瀏覽器{#components-browser}

元件是AEM內容的基礎要素。 您可將多個元件放在頁面上並設定其選項，以便使用AEM建立您的內容頁面。

元件瀏覽器會顯示目前頁面上可用的所有元件。 可將這些資料拖曳至適當位置，然後加以編輯以新增您的內容。

元件瀏覽器是側面板中的標籤(連同資產 [瀏覽器](#assets-browser)[和內容樹](#content-tree))。要開啟 (或關閉) 側面板，請使用工具欄左上角的表徵圖：

![側面板切換](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

當您開啟側面板時，它將從左側滑動開啟（如果需要，請選擇&#x200B;**元件**&#x200B;頁簽）。 開啟後，您可以瀏覽頁面所有可用的元件。

實際外觀和處理取決於您使用的設備類型：

* **行動裝置（例如iPad）**

   元件瀏覽器會完全覆蓋正在編輯的頁面。

   若要新增元件至頁面，並按住所需元件，然後將其移至右側，元件瀏覽器會關閉並再次顯示頁面，您可在此放置元件。

   ![行動裝置上的元件瀏覽器](/help/sites-cloud/authoring/assets/component-browser-mobile.png)

* **桌上型裝置**

   元件瀏覽器會在視窗左側開啟。

   若要將元件新增至頁面，請按一下所需元件，並將其拖曳至所需位置。

   ![案頭上的元件瀏覽器](/help/sites-cloud/authoring/assets/component-browser-desktop.png)

   元件由

   * 元件名稱
   * 元件組（以灰色表示）
   * 表徵圖或縮寫
      * 標準元件的表徵圖為單色。
      * 縮寫一律為元件名稱的前兩個字元。

   從&#x200B;**Components**&#x200B;瀏覽器的頂端工具列，您可以：

   * 依名稱篩選元件。
   * 使用下拉式選取項目，將顯示限制為特定群組。

   如需元件的詳細說明，您可以在「元件」瀏覽器中按一下或點選元件旁的資訊圖示(如果 **有** )。例如，對於&#x200B;**內容片段**:

   ![元件瀏覽器資訊](/help/sites-cloud/authoring/assets/component-browser-information.png)

   有關可用元件的詳細資訊，請參見[元件控制台](/help/sites-cloud/authoring/features/components-console.md)。

>[!NOTE]
>
>當寬度小於1024px時檢測到移動設備。 小型案頭窗口也可以這樣。

## 資產瀏覽器{#assets-browser}

資產瀏覽器會顯示目前頁面上可直接使用的所有[資產](/help/assets/home.md)。

資產瀏覽器是側面板中的標籤，以及元件瀏 [覽器](#components-browser)[和內容樹](#content-tree)。要開啟或關閉側面板，請使用工具欄左上角的表徵圖：

![側面板切換](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

開啟側面板時，它將從左側滑動開啟。 視需要選取&#x200B;**Assets**&#x200B;標籤。

![「資產瀏覽器」按鈕](/help/sites-cloud/authoring/assets/assets-browser-button.png)

當資產瀏覽器開啟時，您可以瀏覽頁面上所有可用的資產。 需要時，可使用無限滾動展開清單。

![資產瀏覽器](/help/sites-cloud/authoring/assets/assets-browser.png)

若要將資產新增至頁面，請選取並拖曳至所需位置。 這可以是：

* 適當類型的現有元件。
   * 例如，您可以將影像類型的資產拖曳至影像元件上。
* 段落系統中的[佔位符](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-placeholder)以建立相應類型的新元件。
   * 例如，您可以將影像類型的資產拖曳至段落系統以建立影像元件。

>[!NOTE]
>
>這適用於特定資產和元件類型。 如需詳細資訊，請參閱[使用資產瀏覽器插入元件](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component-using-the-assets-browser) 。

從資產瀏覽器的頂端工具列，您可以依下列方式篩選資產：

* 名稱
* 路徑
* 資產類型，例如影像、影片、檔案、段落、內容片段和體驗片段
* 方向和樣式等資產特性
   * 僅適用於特定資產類型

實際外觀和處理取決於您使用的設備類型：

* **行動裝置**

   資產瀏覽器會完全覆蓋正在編輯的頁面。

   若要新增資產至您的頁面觸控並按住所需資產，然後將其移至右側：資產瀏覽器會關閉，再次顯示頁面，讓您將資產新增至所需元件。

   ![行動裝置上的資產瀏覽器](/help/sites-cloud/authoring/assets/assets-browser-mobile.png)

* **案頭裝置**

   資產瀏覽器會在視窗左側開啟。

   若要新增資產至您的頁面，請按一下所需資產，然後將其拖曳至所需元件或位置。

   ![案頭上的Assets瀏覽器](/help/sites-cloud/authoring/assets/assets-browser-desktop.png)

>[!NOTE]
>
>當寬度小於1024px時，檢測到移動設備；即，也可在小型案頭視窗上。

如果您需要快速變更資產，可以按一下資產名稱旁顯示的編輯圖示，直接從資產瀏覽器啟動[資產編輯器](/help/assets/manage-digital-assets.md)。

![資產編輯按鈕](/help/sites-cloud/authoring/assets/asset-edit-button.png)

## 內容樹 {#content-tree}

**內容樹**&#x200B;提供階層中頁面上所有元件的概觀，讓您一目瞭然地了解頁面的構成方式。

「內容樹」是側面板中的標籤（連同元件和資產瀏覽器）。 要開啟 (或關閉) 側面板，請使用工具欄左上角的表徵圖：

![內容樹按鈕](/help/sites-cloud/authoring/assets/content-tree-button.png)

開啟側面板時，它將滑動開啟（從左側）。 如有必要，請選取「**內容樹**」頁簽。 開啟後，您會看到頁面或範本的樹狀檢視表示，以便更輕鬆了解其內容的階層結構。 此外，在複雜的頁面上，可更輕鬆地在頁面的元件之間跳轉。

![內容樹](/help/sites-cloud/authoring/assets/content-tree-editor.png)

頁面可以輕鬆由許多相同類型的元件組成，因此內容（元件）樹會在元件類型名稱（黑色）後顯示描述性文字（灰色）。 描述性文字來自元件的一般屬性，例如標題或文字。

元件類型將以使用者語言顯示，而元件說明文字則來自頁面語言。

按一下元件旁的>形箭號會收合或展開該層級。

![內容樹>形擴展](/help/sites-cloud/authoring/assets/content-tree-chevron.png)

按一下元件會反白顯示頁面編輯器中的元件。 可用的動作取決於頁面狀態：

* 例如，基本頁面：

   ![反白顯示內容樹](/help/sites-cloud/authoring/assets/content-tree-highlighted.png)

   基本頁面的元件會有慣用選項。

   如果您在樹狀結構中按一下的元件可編輯，則名稱右側會顯示扳手圖示。 按一下此圖示會直接啟動元件的編輯對話方塊。

   ![內容樹編輯按鈕](/help/sites-cloud/authoring/assets/content-tree-edit.png)

* 屬於[livecopy](/help/sites-cloud/administering/msm/overview.md)的頁面，元件繼承自其他頁面。

>[!NOTE]
>
>如果您在行動裝置上編輯頁面（如果瀏覽器寬度小於1024px），則無法使用內容樹。

## 片段 — 關聯內容瀏覽器{#fragments-associated-content-browser}

如果您的頁面包含內容片段，則您也可以存取[瀏覽器的關聯內容](/help/sites-cloud/authoring/fundamentals/content-fragments.md#using-associated-content)。

## 引用 {#references}

**** 參考會顯示與所選頁面的連線：

* BluePrint
* 啟動
* 即時副本
* 語言副本
* 導入連結
* 參考元件的使用：借入和借出內容

開啟所需的主控台，然後導覽至所需資源，並使用下列方式開啟&#x200B;**References**:

![參考選項](/help/sites-cloud/authoring/assets/references.png)

[選擇所需](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) 資源以顯示與該資源相關的參考類型清單：

![參考詳細資料](/help/sites-cloud/authoring/assets/references-detail.png)

選擇適當的參考類型以了解詳細資訊。 在某些情況下，當您選擇特定參照時，可以執行進一步的操作，包括：

* **傳入連結**，提供參考頁面的頁面清單，以及當您選取特定連結時，可直 **** 接存取這些頁面的編輯項目
* 使用&#x200B;**Reference**&#x200B;元件借入和借出內容的例項，您可從此處導覽至參考/參考頁面
* [啟動](/help/sites-cloud/authoring/launches/overview.md)，提供相關啟動的存取權
* [「即](/help/sites-cloud/administering/msm/overview.md) 時副本」會顯示根據所選資源的所有即時副本路徑。
* [Blueprint](/help/sites-cloud/administering/msm/best-practices.md)，提供詳細資訊和各種動作
* [語言副本](/help/sites-cloud/administering/translation/managing-projects.md#creating-translation-projects-using-the-references-panel)，提供詳細資訊和各種動作

## 事件 — 時間軸{#events-timeline}

對於適當的資源（例如，來自&#x200B;**Sites**&#x200B;控制台的頁面，或來自&#x200B;**Assets**&#x200B;控制台的資產）,[時間軸可用於顯示任何選定項目](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)上的最近活動。

開啟所需的控制台，然後導覽至所需資源並開啟&#x200B;**時間軸**，使用：

![時間軸選項](/help/sites-cloud/authoring/assets/timeline.png)

[選取您所需的資源](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)，然後選擇「 **顯示** 全部」 **** 活動，以列出所選資源上任何最近的操作：

![時間表詳細資訊](/help/sites-cloud/authoring/assets/timeline-detail.png)

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
* [促銷啟動](/help/sites-cloud/authoring/launches/promoting.md) （僅限頁面為啟動時）

此外，**頁面資訊**&#x200B;可在適當時提供對分析和建議的存取。

## 頁面模式{#page-modes}

編輯頁面時有多種模式，可執行不同的動作：

* [編輯](/help/sites-cloud/authoring/fundamentals/editing-content.md)  — 編輯頁面內容時要使用的模式。
* [配置](/help/sites-cloud/authoring/features/responsive-layout.md)  — 可讓您根據裝置建立和編輯回應式配置（如果頁面是根據配置容器）
* [鎖定目標](/help/sites-cloud/authoring/personalization/targeted-content.md)  — 透過鎖定目標和測量所有管道，提高內容關聯性。
* [時間扭曲](/help/sites-cloud/authoring/features/page-versions.md#timewarp)  — 可讓您在特定時間點檢視頁面狀態。
* [即時副本狀態](/help/sites-cloud/authoring/fundamentals/editing-content.md#live-copy-status)  — 可快速概述即時副本狀態，以及繼承/不繼承哪些元件。
* [預覽](/help/sites-cloud/authoring/fundamentals/editing-content.md#previewing-pages)  — 用來檢視頁面在發佈環境中的顯示效果；或在內容中使用連結導覽。
* [注釋](/help/sites-cloud/authoring/fundamentals/annotations.md)  — 用於在頁面上新增或檢視註解。

您可以使用右上角的圖示來存取這些項目。 實際圖示會變更，以反映您目前使用的模式：

![頁面模式](/help/sites-cloud/authoring/assets/page-modes.png)

>[!NOTE]
>
>* 根據頁面的特性，某些模式可能無法使用。
>* 存取某些模式需要適當的權限/權限。
>* 由於空間限制，行動裝置上無法使用開發人員模式。
>* 有一個鍵 [盤](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) ( `Ctrl-Shift-M`可切換 **)，在「預覽」和目前選取的模式之間切換(例如，「編輯」、「排版**********」等)。

>



## 路徑選擇{#path-selection}

編寫時，通常需要選取其他資源，例如定義其他頁面或資源的連結或選取影像時。 為了輕鬆選擇路徑，[path fields](#path-fields)提供自動完成，而[path browser](#path-browser)允許更強健的選擇。

### 路徑欄位{#path-fields}

此處用於說明的範例是影像元件。 如需使用和編輯元件的詳細資訊，請參閱[頁面編寫的元件](/help/sites-cloud/authoring/fundamentals/components.md)。

路徑欄位現在具有自動完成和前瞻功能，可更輕鬆找到資源。

按一下路徑欄位中的&#x200B;**開啟選擇對話框**&#x200B;按鈕可開啟[路徑瀏覽器](#path-browser)對話框，以提供更詳細的選擇選項。

![開啟選擇對話框按鈕](/help/sites-cloud/authoring/assets/open-selection-dialog-button.png)

或者，您也可以開始在路徑欄位中輸入內容，AEM會在您輸入內容時提供相符的路徑。

![開啟選擇對話框按鈕](/help/sites-cloud/authoring/assets/path-selection-completion.png)

### 路徑瀏覽器 {#path-browser}

路徑瀏覽器的組織方式與網站控制台的[欄檢視](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view)類似，可提供更詳細的資源選擇。

![路徑瀏覽器](/help/sites-cloud/authoring/assets/path-browser.png)

* 選取資源後，對話方塊右上角的&#x200B;**Select**&#x200B;按鈕就會變為作用中。 按一下或點選以確認選取項目，或按一下「取消」以中止。****
* 如果上下文允許選擇多個資源，則選擇資源也會激活「選擇 **** 」按鈕，但也會向窗口的右上角添加選定資源的計數。按一下 **數字旁** 的X，取消選取全部。
* 瀏覽樹狀結構時，您的位置會反映在對話方塊頂端的階層連結中。 這些階層連結也可用來快速跳入資源階層。
* 您隨時都可以使用對話方塊頂端的搜尋欄位。 按一下搜尋欄位中的&#x200B;**X**&#x200B;以清除搜尋。
* 若要縮小搜尋範圍，您可以顯示篩選選項並根據特定路徑篩選結果。

   ![篩選器選項](/help/sites-cloud/authoring/assets/filters-option.png)

## 鍵盤快速鍵 {#keyboard-shortcuts}

有各種[鍵盤快速鍵](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)可用。
