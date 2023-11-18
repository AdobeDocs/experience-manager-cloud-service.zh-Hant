---
title: 基本處理
description: 輕鬆瀏覽AEM及其基本用法
exl-id: ae87a63a-c6d3-4220-ab3d-07a20b21b93b
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '2943'
ht-degree: 6%

---


# 基本處理 {#basic-handling}

本檔案旨在概述使用AEM製作環境時的基本處理方式。 它會使用 **網站** 以主控台為基礎。

>[!NOTE]
>
>* 部分功能並非在所有主控台中提供，部分主控台可能提供其他功能。 有關個別主控台及其相關功能的特定資訊，請參閱其他頁面上的詳細說明。
>* 在整個AEM環境中都可以使用鍵盤快速鍵。 尤其是當 [使用主控台](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) 和 [編輯頁面](/help/sites-cloud/authoring/fundamentals/keyboard-shortcuts.md).

{{edge-delivery-authoring}}

## 觸控式UI {#a-touch-enabled-ui}

AEM使用者介面已啟用觸控功能。 觸控式介面可讓您使用觸控功能，透過點選、觸控並按住及輕掃之類的手勢與軟體互動。 由於AEM UI支援觸控功能，因此您可以在手機或平板電腦等觸控裝置上使用觸控手勢。 不過，您也可以使用傳統案頭裝置上的滑鼠動作，靈活選擇內容撰寫方式。

## 首要步驟 {#first-steps}

登入後立即到達 [導覽面板](#navigation-panel). 選取其中一個選項會開啟個別主控台。

![導覽面板](/help/sites-cloud/authoring/assets/navigation.png)

為了更清楚瞭解AEM的基本用法，本檔案根據 **網站** 主控台。 選擇於 **網站** 以開始使用。

## 產品導覽 {#product-navigation}

每當使用者首次存取主控台時，就會啟動產品導覽教學課程。 請花上一分鐘時間選取，以取得AEM基本處理的良好概觀。

![導覽教學課程](/help/sites-cloud/authoring/assets/tutorial.png)

選取 **下一個** 以進入概覽的下一頁。 選取 **關閉** 或在「概述」對話方塊外部選取以關閉。

除非您檢視所有投影片或核取選項，否則概觀將會在您下次存取主控台時重新啟動 **不要再顯示**.

## 全域導覽 {#global-navigation}

您可以使用全域導覽面板在主控台之間導覽。 當您選取畫面左上方的Adobe Experience Manager連結時，就會以全熒幕下拉式清單的形式觸發此動作。

您可以按一下或點選以關閉全域導覽面板 **關閉** 以返回您之前的位置。

![導覽面板頂列](/help/sites-cloud/authoring/assets/navigation-bar.png)

全域導覽有兩個面板，由畫面左側的圖示表示：

* **[導覽](#navigation-panel)**  — 當您登入AEM時，以指南針和預設面板表示
* **[工具](#tools-panel)**  — 以槌子表示

這些面板上可用的選項說明如下。

### 導覽面板 {#navigation-panel}

「導覽」面板：

![導覽面板](/help/sites-cloud/authoring/assets/navigation.png)

當您瀏覽控制檯和內容時，瀏覽器索引標籤的標題將會更新以反映您的位置。

在「導覽」中，可用的主控台有：

| 主控台 | 用途 |
|---|---|
| 專案 | 「專案」主控台可讓您直接存取專案。 [專案是虛擬儀表板](/help/sites-cloud/authoring/projects/overview.md) 可用來建立團隊的資訊。 然後，您可以授予該團隊存取資源、工作流程和任務的許可權，從而讓人們朝著共同目標努力。 |
| Sites | Sites主控台可讓您 [建立、檢視及管理網站](/help/sites-cloud/authoring/fundamentals/organizing-pages.md) 在您的AEM執行個體上執行。 透過此主控台，您可以建立、編輯、複製、移動和刪除頁面、啟動工作流程以及發佈頁面。 |
| 體驗片段 | 一個 [體驗片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md) 是獨立的體驗，可以跨管道重複使用，也可以具有變數，省去重複複製和貼上體驗或體驗片段的麻煩。 |
| Assets | 「資產」主控台可讓您匯入及管理 [數位資產，例如影像、影片、檔案和音訊檔案](/help/assets/overview.md). 這些資產隨後便可由同一AEM例項上執行的任何網站使用。 您也可以建立和管理 [內容片段](/help/assets/content-fragments/content-fragments.md) 從「資產」主控台。 |
| 個人化 | 此主控台提供工具的架構，適用於 [編寫鎖定內容及呈現個人化體驗](/help/sites-cloud/authoring/personalization/overview.md). |
| 內容片段 | [內容片段](/help/sites-cloud/administering/content-fragments/overview.md) 可讓您設計、建立、策劃和發佈不受頁面影響的內容。 它們可讓您準備結構化內容，以準備用於多個位置/多個管道，並適用於頁面製作和headless傳送。 |

## 「工具」面板 {#tools-panel}

在「工具」面板中，有一個側面板，其中包含一系列類別，這些類別將類似的「工具」主控台組合在一起。 「工具」主控台可供存取數個專用工具與主控台，協助您管理網站、數位資產及內容存放庫的其他方面。 <!--The [Tools consoles](/help/sites-administering/tools-consoles.md) provide access to several specialized tools and consoles that help you administer your websites, digital assets, and other aspects of your content repository.-->

![「工具」面板](/help/sites-cloud/authoring/assets/tools-panel.png)

## 標頭 {#the-header}

 標頭會始終顯示在畫面頂端。雖然無論您在系統中的何處，標題中的大部分選項都保持不變，但有些選項是上下文特定的。

![導覽標頭](/help/sites-cloud/authoring/assets/navigation-bar.png)

* [全域導覽](#global-navigation)

  選取 **Adobe Experience Manager** 連結可在主控台之間導覽。

  ![全域導覽](/help/sites-cloud/authoring/assets/global-navigation.png)

* [搜尋](/help/sites-cloud/authoring/getting-started/search.md)

  ![搜尋圖示](/help/sites-cloud/authoring/assets/search-icon.png)

  您也可以使用 [快速鍵](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) `/` （正斜線）從任何主控台叫用搜尋。

* [解決方案](https://www.adobe.com/experience-cloud.html)

  ![「解決方案」按鈕](/help/sites-cloud/authoring/assets/solutions.png)

* [說明](#accessing-help)

  ![說明按鈕](/help/sites-cloud/authoring/assets/help.png)

* [通知](/help/sites-cloud/authoring/getting-started/inbox.md)

  ![「通知」按鈕](/help/sites-cloud/authoring/assets/notifications.png)

  此圖示會標有目前已指派之未完成的通知數量。

* [使用者屬性](/help/sites-cloud/authoring/getting-started/account-environment.md)

  ![使用者屬性按鈕](/help/sites-cloud/authoring/assets/user-properties.png)

* [邊欄選擇器](#rail-selector)

  ![邊欄選擇器按鈕](/help/sites-cloud/authoring/assets/rail-selector.png)

  顯示的選項取決於您目前的主控台。 例如，在 **網站** 您可以選取「僅限內容」(Content only) （預設）、「時間軸」(Timeline)、「參照」(references)或「濾鏡」(filter)側面板。

  ![邊欄選擇器的範例](/help/sites-cloud/authoring/assets/rail-selector-example.png)

* 階層連結

  ![導覽列中的階層連結](/help/sites-cloud/authoring/assets/breadcrumbs-navigation.png)

  階層連結位於邊欄中間，且一律顯示目前所選專案的說明，可讓您在特定主控台內導覽。 在 **網站** 主控台，您可以瀏覽網站的各個層級。

  只要按一下階層連結文字，就會顯示一個下拉式清單，列出目前所選專案的階層層次。 按一下專案以跳至該位置。

  ![展開的階層連結範例](/help/sites-cloud/authoring/assets/breadcrumbs-example.png)

* **建立** 按鈕

  ![建立按鈕](/help/sites-cloud/authoring/assets/create.png)

  按一下後，顯示的選項即適用於主控台/前後關聯。

* [檢視](#viewing-and-selecting-resources)

  檢檢視示位於AEM工具列的最右側。 它也會指出目前的檢視，因此會變更。 例如在預設檢視中， **欄檢視** 它顯示：

  ![檢視按鈕](/help/sites-cloud/authoring/assets/views-button.png)

  您可以在欄檢視、卡片檢視和清單檢視之間切換。 在清單檢視中，它也會顯示檢視設定。

  ![檢視](/help/sites-cloud/authoring/assets/view.png)

  >[!NOTE]
  >
  >「 **檢視設定** 」選項僅在「清單檢視」 **模式中可用** 。

* 鍵盤導覽

  您僅能使用鍵盤導覽網站。 這會使用的標準瀏覽器功能 **標籤** 金鑰(或 **OPT+TAB**)，將您移動至頁面上可聚焦的元素之間。

  在 **網站** 主控台新增選項至 **跳至主要內容**. 當您以Tab鍵瀏覽頁首選項時，這個選項就會顯示，而且可讓您略過（產品）工具列中的標準元素，並直接前往主要內容，加速導覽速度。

  ![跳至主要內容](/help/sites-cloud/authoring/assets/skip-to-main-content.png)

## 存取說明 {#accessing-help}

有多種可用的說明資源：

* **主控台工具列**

  根據您的位置， **說明** 圖示會開啟適當的資源：

  ![說明圖示](/help/sites-cloud/authoring/assets/help-console.png)

* **導覽**

  第一次瀏覽系統時， [一連串投影片介紹AEM導覽](#product-navigation).

  ![教學課程](/help/sites-cloud/authoring/assets/tutorial.png)

* **頁面編輯器**

  第一次編輯頁面時，系統會以一系列幻燈片來介紹頁面編輯器。

  ![編輯器教學課程](/help/sites-cloud/authoring/assets/editor-tutorial.png)

  瀏覽此概觀，如同操作 [產品導覽概觀](#product-navigation) 首次存取任何主控台時。

  從 [**頁面資訊** 功能表您可以選取 **說明**](/help/sites-cloud/authoring/fundamentals/environment-tools.md#accessing-help) 以隨時再次顯示。

* **工具主控台**

  從 **工具** 主控台您也可以存取外部 **資源**：

   * **檔案**  — 檢視網站體驗管理檔案
   * **開發人員資源**  — 開發人員資源和下載

  >[!NOTE]
  >
  >您可以隨時使用快速鍵來存取可用快速鍵的概觀 `?` （問號）。
  >
  >如需所有鍵盤快速鍵的概觀，請參閱下列檔案：
  >
  >* [用於編輯頁面的鍵盤快速鍵](/help/sites-cloud/authoring/fundamentals/keyboard-shortcuts.md)
  >* [主控台的鍵盤快速鍵](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)

## 動作工具列 {#actions-toolbar}

每當選取資源（例如頁面或資產）時，工具列中都會有包含說明文字的圖示來指示各種動作。 這些動作相依於：

* 目前的主控台
* 目前內容
* 無論您是否在 [選擇模式](#viewing-and-selecting-resources)

工具列中可用的動作會變更，以反映您可對所選特定專案執行的動作。

您如何 [選取資源](#viewing-and-selecting-resources) 視檢視而定。

由於某些視窗的空間限制，工具列可能會很快變得比可用的空間長。發生此情況時，會出現其他選項。按一下或點選省略符號(三個點或 **...**)會開啟一個下拉式選取器，其中包含所有剩餘的動作。 例如，在Sites主控台中選取頁面 **後** :

![其他選項](/help/sites-cloud/authoring/assets/additional-options.png)

>[!NOTE]
>
>可用的個別圖示會根據適當的主控台/功能/案例進行記錄。

## 快速動作 {#quick-actions}

在 [卡片檢視](#card-view) 某些動作會以快速動作圖示的形式呈現，並位於工具列上。 快速動作圖示一次只適用於一個專案，您不需要預先選取。

當您將滑鼠懸停在資源卡上（案頭裝置）時，可以看到快速動作。 可用的快速動作取決於主控台和內容。 例如，以下是中頁面的快速動作 **網站** 主控台：

![其他選項](/help/sites-cloud/authoring/assets/quick-actions.png)

## 檢視和選擇資源 {#viewing-and-selecting-resources}

從概念上講，所有檢視中的檢視、導覽和選取操作都相同，只是處理方式根據您使用的檢視而略有差異。

您可以使用任何可用檢視來檢視、導覽及選取（進行進一步動作）您的資源，您可透過右上角的圖示選取每個檢視：

* [欄檢視](#column-view)
* [卡片檢視](#card-view)
* [清單檢視](#list-view)

>[!NOTE]
>
>依預設，AEM Assets不會在任何檢視中將資產的原始轉譯顯示為縮圖。 如果您是管理員，則可以使用覆蓋圖將AEM Assets設定為將原始轉譯顯示為縮圖。

### 選取資源 {#selecting-resources}

選取特定資源取決於檢視和裝置的組合：

| 檢視 | 選取觸控 | 選取案頭 | 取消選取觸控 | 取消選取案頭 |
|---|---|---|---|---|
| 欄 | 點選縮圖 | 按一下縮圖 | 點選縮圖 | 按一下縮圖 |
| 卡片 | 點選並按住卡片 | 將滑鼠移到上方，然後使用核取記號快速動作 | 點選卡片 | 按一下卡片 |
| 清單 | 點選縮圖 | 按一下縮圖 | 點選縮圖 | 按一下縮圖 |

#### 全選 {#select-all}

您可以按一下 **全選** 控制檯右上角的選項。

* 在 **卡片檢視** 已選取所有卡片。
* 在 **清單檢視** 會選取清單中的所有專案。
* 在 **欄檢視** 會選取最左欄中的所有專案。

![全選](/help/sites-cloud/authoring/assets/select-all.png)

#### 取消全選 {#deselecting-all}

在任何情況下，當您選取專案時，所選專案的計數都會顯示在工具列的右上方。

您可以取消選取所有專案並結束選取模式，方法如下：

* 按一下或點選 **X** 在計數旁邊
* 使用 **逸出** key

![取消全選](/help/sites-cloud/authoring/assets/deselect-all.png)

在所有檢視中，如果您使用案頭裝置，點選鍵盤上的Esc鍵即可取消選取所有專案。

#### 選取範例 {#selecting-example}

1. 例如在卡片檢視中：

   ![卡片檢視選取](/help/sites-cloud/authoring/assets/card-view-select.png)

1. 選取資源後，頂端標題會由 [動作工具列](#actions-toolbar) 可讓您存取目前適用於所選資源的動作。

   若要結束選取模式，請選取 **X** 右上方，或使用 **逸出**.

### 欄檢視 {#column-view}

![欄檢視](/help/sites-cloud/authoring/assets/column-view.png)

欄檢視允許透過一系列階層式欄對內容樹進行視覺導覽。 此檢視可讓您視覺化並周遊網站的樹狀結構。

在最左邊的欄中選取資源，會在右邊的欄中顯示子資源。 在右側欄中選取資源，會在右側另一欄中顯示子資源，依此類推。

* 您可以點選或按一下資源名稱或資源名稱右側的>形箭號，在樹狀結構中向上和向下導覽。

   * 點選或按一下時，資源名稱和>形箭號會反白顯示。
   * 已點按/已點按資源的子項會顯示在已點按/已點按資源右側的欄中。
   * 如果您選取沒有子系的資源名稱，其詳細資訊會顯示在最後一欄。

* 點選或按一下縮圖會選取資源。

   * 選取時，縮圖上會覆蓋勾號，資源名稱也會反白顯示。
   * 所選資源的詳細資訊會顯示在最後一欄。
   * 動作工具列隨即可用。

  在欄檢視中選取頁面時，選取的頁面會連同下列詳細資料顯示在最終欄中：

   * 頁面標題
   * 頁面名稱（頁面URL的一部分）
   * 頁面所依據的範本
   * 修改詳細資料
   * 頁面語言
   * 發佈和預覽詳細資料

### 卡片檢視 {#card-view}

![卡片檢視](/help/sites-cloud/authoring/assets/card-view.png)

* 卡片檢視會顯示目前層級中每個專案的資訊卡片。 這些會提供下列資訊：

   * 頁面內容的視覺化表示法
   * 頁面標題
   * 重要日期（例如上次編輯、上次發佈）
   * 如果頁面已鎖定、隱藏或屬於即時副本的一部分
   * 適當時，亦即需要您擔任工作流程一部分的時間
      * 指出所需動作的標籤，可能與 [收件匣](/help/sites-cloud/authoring/getting-started/inbox.md).

* [快速動作](#quick-actions) 也可以在此檢視中使用，例如選取和常見動作，例如編輯。

  ![快速動作](/help/sites-cloud/authoring/assets/quick-actions.png)

* 您可以點選/按一下卡片來向下瀏覽樹狀結構（注意避免快速動作），或使用 [標題中的階層連結](#the-header).

### 清單檢視 {#list-view}

![清單檢視](/help/sites-cloud/authoring/assets/list-view.png)

* 清單檢視會列出目前層級中每個資源的資訊。
* 您可以點選/按一下資源名稱，在樹狀結構中向下導覽，並使用 [標題中的階層連結](#the-header).
* 若要輕鬆選取清單中的所有專案，請使用清單左上方的核取方塊。

  ![清單檢視選取全部](/help/sites-cloud/authoring/assets/list-view-select-all.png)

   * 當選取清單中的所有專案時，此核取方塊會顯示為已核取。

      * 選取核取方塊以取消選取全部。

   * 僅選取部分專案時，其顯示會帶有減號。

      * 勾選核取方塊以選取全部。
      * 再次選取核取方塊以取消選取全部。

* 選擇要顯示的欄，使用 **檢視設定** 選項位於「檢視」按鈕下。 下列欄可供顯示：

   * **名稱**  — 頁面名稱，在多語言撰寫環境中相當實用，因為它是頁面URL的一部分，無論使用何種語言，都不會變更
   * **已修改**  — 上次修改日期和上次修改的使用者
   * **已發佈**  — 發佈狀態
   * **預覽**  — 預覽狀態
   * **範本**  — 頁面所在的範本
   * **工作流程**  — 目前套用至頁面的工作流程。 當您滑鼠懸停或開啟時間軸時，會提供詳細資訊。
   * **頁面分析**
   * **不重複訪客**
   * **頁面逗留時間**

     ![選取欄](/help/sites-cloud/authoring/assets/select-columns.png)

  根據預設 **名稱** 欄隨即顯示，它構成了頁面URL的一部分。 在某些情況下，作者可能需要存取不同語言的頁面，如果作者不知道頁面的語言，檢視頁面名稱（通常不會變更）會很有幫助。

* 使用清單中每個專案最右側的點狀垂直列，變更專案的順序。

  >[!NOTE]
  >
  >變更順序僅適用於具有下列條件的已排序資料夾： `jcr:primaryType` 值為 `sling:OrderedFolder`.

  ![欄順序](/help/sites-cloud/authoring/assets/column-order.png)

  選取垂直選取列並將專案拖曳到清單中的新位置。

  ![訂單清單](/help/sites-cloud/authoring/assets/order-list.png)

## 邊欄選擇器 {#rail-selector}

此 **邊欄選擇器** 可在視窗左上方取得，並依據您目前的主控台顯示選項。

![展開的邊欄選擇器](/help/sites-cloud/authoring/assets/rail-selector-expanded.png)

例如，在 **網站** 控制檯您可以選取「僅限內容」（預設值）、「內容樹」、「時間軸」、「參照」、「場地詳細資訊」或「篩選器」側面板。

如果選取「僅限內容」，則只會出現邊欄圖示。 選取任何其他選項時，選項名稱會出現在邊欄圖示旁。

>[!NOTE]
>
>[鍵盤快速鍵](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) 可用來快速切換邊欄顯示選項。

### 內容樹 {#content-tree}

內容樹可用來快速導覽側面板中的網站階層，並檢視目前資料夾中頁面的許多相關資訊。

使用內容樹側面板搭配清單檢視或卡片檢視，使用者可以輕鬆檢視專案的階層結構，並使用內容樹側面板在內容結構中輕鬆導覽，並在清單檢視中檢視詳細的頁面資訊。

![內容樹](/help/sites-cloud/authoring/assets/content-tree.png)

>[!NOTE]
>
>選取階層檢視中的專案後，可使用方向鍵來快速瀏覽階層。
>
>另請參閱 [鍵盤快速鍵](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) 以取得詳細資訊。

### 時間軸 {#timeline}

時間軸可用於檢視和/或啟動所選資源上已發生的事件。 若要開啟時間軸欄，請使用邊欄選取器：

![時間軸樹狀結構](/help/sites-cloud/authoring/assets/timeline.png)

時間軸欄可讓您：

* 檢視與選取專案相關的各種事件。

   * 您可從下拉式清單中選取事件型別：

      * 評論
      * [註解](/help/sites-cloud/authoring/fundamentals/annotations.md)
      * [活動](/help/sites-cloud/authoring/personalization/activities.md)
      * [啟動](/help/sites-cloud/authoring/launches/overview.md)
      * [版本](/help/sites-cloud/authoring/features/page-versions.md)
      * [工作流程](/help/sites-cloud/authoring/workflows/overview.md)
         * 暫時性工作流程除外，因為系統不會儲存這些工作流程的歷程記錄資訊 <!--With the exception of [transient workflows](/help/sites-developing/workflows.md#transient-workflows) as no history information is saved for these-->
      * 顯示全部

* 新增/檢視有關所選項目的註解。「注 **釋** 」方塊會顯示在事件清單的底部。鍵入注釋後跟Return將註冊注釋。當選取「注 **釋** 」或「 **全部顯示** 」時顯示。

* 特定的主控台具有其他功能。 例如，在Sites主控台中，您可以：

   * [儲存版本](/help/sites-cloud/authoring/features/page-versions.md)
   * [啟動工作流程](/help/sites-cloud/authoring/workflows/applying.md)

這些選項可透過 **註解** 欄位。

![評論欄位](/help/sites-cloud/authoring/assets/comments.png)

### 參考 {#references}

**引用** 顯示與所選資源的任何連線。 例如，在 **網站** 主控台 [引用](/help/sites-cloud/authoring/fundamentals/environment-tools.md#references) 若為頁面，則顯示：

* [啟動](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)
* [即時副本](/help/sites-cloud/administering/msm/overview.md#openingthelivecopyoverviewfromreferences)
* [語言副本](/help/sites-cloud/administering/translation/preparation.md#seeing-the-status-of-language-roots)
* 內容參照：

   * 從其他頁面連結至所選頁面
   * 參考元件在所選頁面中借用的內容和/或借出的內容

![引用範例](/help/sites-cloud/authoring/assets/references-example.png)

### 網站 {#site}

**網站** 顯示網站的詳細資料 [使用網站範本建立](/help/sites-cloud/administering/site-creation/create-site.md).

![網站邊欄](../assets/site-rail.png)

檢視檔案 [使用網站邊欄管理您的網站主題](/help/sites-cloud/administering/site-creation/site-rail.md) 以進一步瞭解如何使用邊欄管理 [您的網站主題](/help/sites-cloud/administering/site-creation/site-themes.md).

>[!TIP]
>
>從範本建立網站並自訂其主題的程式的端對端說明可在以下連結中找到： [快速網站建立歷程](/help/journey-sites/quick-site/overview.md).

### 篩選 {#filter}

這會開啟一個面板，類似於 [搜尋](/help/sites-cloud/authoring/getting-started/search.md) 並設定適當的位置篩選器，讓您進一步篩選想要檢視的內容。

![篩選器範例](/help/sites-cloud/authoring/assets/filter.png)
