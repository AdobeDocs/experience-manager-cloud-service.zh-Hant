---
title: 基本處理
description: 輕鬆瀏覽AEM及其基本用法
exl-id: ae87a63a-c6d3-4220-ab3d-07a20b21b93b
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '2943'
ht-degree: 5%

---


# 基本處理 {#basic-handling}

本檔案旨在概述使用AEM製作環境時的基本處理方式。 它使用&#x200B;**Sites**&#x200B;主控台作為基礎。

>[!NOTE]
>
>* 部分功能並非在所有主控台中提供，部分主控台可能提供其他功能。 有關個別主控台及其相關功能的特定資訊，請參閱其他頁面上的詳細說明。
>* 在整個AEM環境中都可以使用鍵盤快速鍵。 特別是當[使用主控台](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)和[編輯頁面](/help/sites-cloud/authoring/fundamentals/keyboard-shortcuts.md)時。

{{edge-delivery-authoring}}

## 觸控式UI {#a-touch-enabled-ui}

AEM的使用者介面已啟用觸控功能。 觸控式介面可讓您使用觸控功能，透過選擇、觸控並按住及撥動等手勢與軟體互動。 由於AEM UI支援觸控功能，因此您可以在手機或平板電腦等觸控裝置上使用觸控手勢。 不過，您也可以使用傳統案頭裝置上的滑鼠動作，靈活選擇內容撰寫方式。

## 首要步驟 {#first-steps}

登入後立即進入[導覽面板](#navigation-panel)。 選取其中一個選項會開啟個別主控台。

![導覽面板](/help/sites-cloud/authoring/assets/navigation.png)

為了深入瞭解AEM的基本用法，本檔案是以&#x200B;**網站**&#x200B;主控台為基礎的。 在&#x200B;**網站**&#x200B;上選取以開始。

## 產品導覽 {#product-navigation}

每當使用者首次存取主控台時，就會啟動產品導覽教學課程。 請花上一分鐘時間選取，以取得AEM基本處理的良好概觀。

![導覽教學課程](/help/sites-cloud/authoring/assets/tutorial.png)

選取「**下一步**」以前往概覽的下一頁。 選取&#x200B;**關閉**&#x200B;或在總覽對話方塊之外選取以關閉。

除非您檢視所有投影片或勾選&#x200B;**不要再顯示這個專案**，否則概觀將會在您下次存取主控台時重新啟動。

## 全域導覽 {#global-navigation}

您可以使用全域導覽面板在主控台之間導覽。 當您選取畫面左上方的Adobe Experience Manager連結時，就會以全熒幕下拉式清單的形式觸發此動作。

您可以按一下或點選「**關閉**」來關閉全域導覽面板，以返回您之前的位置。

![導覽面板頂列](/help/sites-cloud/authoring/assets/navigation-bar.png)

全域導覽有兩個面板，由畫面左側的圖示表示：

* **[導覽](#navigation-panel)** — 在您登入AEM時，以指南針和預設面板表示
* **[工具](#tools-panel)** — 以錘子表示

這些面板上可用的選項說明如下。

### 導覽面板 {#navigation-panel}

「導覽」面板：

![導覽面板](/help/sites-cloud/authoring/assets/navigation.png)

當您瀏覽控制檯和內容時，瀏覽器索引標籤的標題將會更新以反映您的位置。

在「導覽」中，可用的主控台有：

| 主控台 | 用途 |
|---|---|
| 專案 | 「專案」主控台可讓您直接存取專案。 [專案是虛擬儀表板](/help/sites-cloud/authoring/projects/overview.md)，可用來建立團隊。 然後，您可以授予該團隊存取資源、工作流程和任務的許可權，從而讓人們朝著共同目標努力。 |
| Sites | Sites主控台可讓您[建立、檢視及管理在您的AEM執行個體上執行的網站](/help/sites-cloud/authoring/fundamentals/organizing-pages.md)。 透過此主控台，您可以建立、編輯、複製、移動和刪除頁面、啟動工作流程以及發佈頁面。 |
| 體驗片段 | [體驗片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)是獨立的體驗，可以跨管道重複使用，也可以有變數，省去重複複製和貼上體驗或體驗片段的麻煩。 |
| Assets | Assets主控台可讓您匯入及管理[數位資產，例如影像、影片、檔案和音訊檔案](/help/assets/overview.md)。 這些資產隨後便可由同一AEM例項上執行的任何網站使用。 您也可以從Assets主控台建立和管理[內容片段](/help/assets/content-fragments/content-fragments.md)。 |
| 個人化 | 此主控台提供[製作目標內容與呈現個人化體驗的工具架構](/help/sites-cloud/authoring/personalization/overview.md)。 |
| 內容片段 | [內容片段](/help/sites-cloud/administering/content-fragments/overview.md)可讓您設計、建立、組織及發佈獨立於頁面的內容。 它們可讓您準備結構化內容，以準備用於多個位置/多個管道，並適用於頁面製作和headless傳送。 |

## 「工具」面板 {#tools-panel}

在「工具」面板中，有一個側面板，其中包含一系列類別，這些類別將類似的「工具」主控台組合在一起。 「工具」主控台可供存取數個專用工具與主控台，協助您管理網站、數位資產及內容存放庫的其他方面。<!--The [Tools consoles](/help/sites-administering/tools-consoles.md) provide access to several specialized tools and consoles that help you administer your websites, digital assets, and other aspects of your content repository.-->

![工具面板](/help/sites-cloud/authoring/assets/tools-panel.png)

## 標頭 {#the-header}

標題一律會顯示在畫面頂端。 雖然無論您在系統中的何處，標題中的大部分選項都保持不變，但有些選項是上下文特定的。

![導覽標頭](/help/sites-cloud/authoring/assets/navigation-bar.png)

* [全域導覽](#global-navigation)

  選取&#x200B;**Adobe Experience Manager**&#x200B;連結以在主控台之間導覽。

  ![全域導覽](/help/sites-cloud/authoring/assets/global-navigation.png)

* [搜尋](/help/sites-cloud/authoring/getting-started/search.md)

  ![搜尋圖示](/help/sites-cloud/authoring/assets/search-icon.png)

  您也可以使用[捷徑鍵](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) `/` （正斜線）從任何主控台叫用搜尋。

* [解決方案](https://www.adobe.com/experience-cloud.html)

  ![解決方案按鈕](/help/sites-cloud/authoring/assets/solutions.png)

* [說明](#accessing-help)

  ![說明按鈕](/help/sites-cloud/authoring/assets/help.png)

* [通知](/help/sites-cloud/authoring/getting-started/inbox.md)

  ![通知按鈕](/help/sites-cloud/authoring/assets/notifications.png)

  此圖示會加上目前指派的未完成通知數目。

* [使用者屬性](/help/sites-cloud/authoring/getting-started/account-environment.md)

  ![使用者屬性按鈕](/help/sites-cloud/authoring/assets/user-properties.png)

* [邊欄選擇器](#rail-selector)

  ![邊欄選擇器按鈕](/help/sites-cloud/authoring/assets/rail-selector.png)

  顯示的選項取決於您目前的主控台。 例如，在&#x200B;**Sites**&#x200B;中，您可以選取僅限內容（預設）、時間軸、參照或篩選器側面板。

  ![邊欄選擇器範例](/help/sites-cloud/authoring/assets/rail-selector-example.png)

* 導覽列

  導覽列中的![階層連結](/help/sites-cloud/authoring/assets/breadcrumbs-navigation.png)

  階層連結位於邊欄中間，且一律顯示目前所選專案的說明，可讓您在特定主控台內導覽。 在&#x200B;**網站**&#x200B;主控台中，您可以瀏覽網站的各個層級。

  只要按一下階層連結文字，就會顯示一個下拉式清單，列出目前所選專案的階層層次。 按一下專案以跳至該位置。

  ![展開的階層連結範例](/help/sites-cloud/authoring/assets/breadcrumbs-example.png)

* **建立**&#x200B;按鈕

  ![建立按鈕](/help/sites-cloud/authoring/assets/create.png)

  按一下後，顯示的選項即適用於主控台/前後關聯。

* [檢視](#viewing-and-selecting-resources)

  檢檢視示位於AEM工具列的最右側。 它也會指出目前的檢視，因此會變更。 例如，在預設檢視&#x200B;**欄檢視**&#x200B;中顯示：

  ![檢視按鈕](/help/sites-cloud/authoring/assets/views-button.png)

  您可以在欄檢視、卡片檢視和清單檢視之間切換。 在清單檢視中，它也會顯示檢視設定。

  ![個檢視](/help/sites-cloud/authoring/assets/view.png)

  >[!NOTE]
  >
  >「 **檢視設定** 」選項僅在「清單檢視」 **模式中可用** 。

* 鍵盤導覽

  您僅能使用鍵盤導覽網站。 這會使用&#x200B;**TAB**&#x200B;索引鍵（或&#x200B;**OPT+TAB**）的標準瀏覽器功能，在頁面上可聚焦的元素之間移動您。

  在&#x200B;**網站**&#x200B;主控台中，**跳至主要內容**&#x200B;的選項已新增。 當您以Tab鍵瀏覽頁首選項時，這個選項就會顯示，而且可讓您略過（產品）工具列中的標準元素，並直接前往主要內容，加速導覽速度。

  ![跳至主要內容](/help/sites-cloud/authoring/assets/skip-to-main-content.png)

## 存取說明 {#accessing-help}

有多種可用的說明資源：

* **主控台工具列**

  根據您的位置，**說明**&#x200B;圖示會開啟適當的資源：

  ![說明圖示](/help/sites-cloud/authoring/assets/help-console.png)

* **導覽**

  第一次導覽系統時，[一連串幻燈片會介紹AEM導覽](#product-navigation)。

  ![教學課程](/help/sites-cloud/authoring/assets/tutorial.png)

* **頁面編輯器**

  第一次編輯頁面時，系統會以一系列幻燈片來介紹頁面編輯器。

  ![編輯器教學課程](/help/sites-cloud/authoring/assets/editor-tutorial.png)

  第一次存取任何主控台時，瀏覽這個概觀，就像瀏覽[產品瀏覽概觀](#product-navigation)一樣。

  從&#x200B;[**頁面資訊**&#x200B;功能表，您可以隨時選取&#x200B;**說明**](/help/sites-cloud/authoring/fundamentals/environment-tools.md#accessing-help)&#x200B;來再次顯示這個專案。

* **工具主控台**

  您也可以從&#x200B;**工具**&#x200B;主控台存取外部&#x200B;**資源**：

   * **檔案** — 檢視Web體驗管理檔案
   * **開發人員資源** — 開發人員資源和下載

  >[!NOTE]
  >
  >在主控台中，您可以隨時使用快速鍵`?` （問號）存取可用的快速鍵概觀。
  >
  >如需所有鍵盤快速鍵的概觀，請參閱下列檔案：
  >
  >* [編輯頁面的鍵盤快速鍵](/help/sites-cloud/authoring/fundamentals/keyboard-shortcuts.md)
  >* [主控台的鍵盤快速鍵](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)

## 動作工具列 {#actions-toolbar}

每當選取資源（例如頁面或資產）時，工具列中都會有包含說明文字的圖示來指示各種動作。 這些動作相依於：

* 目前的主控台
* 目前內容
* 您是否處於[選取模式](#viewing-and-selecting-resources)

工具列中可用的動作會變更，以反映您可對所選特定專案執行的動作。

您如何[選取資源](#viewing-and-selecting-resources)取決於檢視。

由於某些視窗的空間限制，工具列可能會很快變得比可用的空間長。發生此情況時，會出現其他選項。按一下或點選省略符號（三個點或&#x200B;**...**）會開啟一個下拉式選取器，其中包含所有剩餘的動作。 例如，在Sites主控台中選取頁面 **後** :

![其他選項](/help/sites-cloud/authoring/assets/additional-options.png)

>[!NOTE]
>
>可用的個別圖示會根據適當的主控台/功能/案例進行記錄。

## 快速動作 {#quick-actions}

在[卡片檢視](#card-view)中，某些動作會以快速動作圖示的形式呈現，並顯示在工具列上。 快速動作圖示一次只適用於一個專案，您不需要預先選取。

當您將滑鼠移至（桌上型裝置）資源卡上時，可以看到快速動作。 可用的快速動作取決於主控台和內容。 例如，以下是&#x200B;**Sites**&#x200B;主控台中頁面的快速動作：

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
| 欄 | 選取縮圖 | 按一下縮圖 | 選取縮圖 | 按一下縮圖 |
| 卡片 | 選取並按住卡片 | 將滑鼠移到上方，然後使用核取記號快速動作 | 選取卡片 | 按一下卡片 |
| 清單 | 選取縮圖 | 按一下縮圖 | 選取縮圖 | 按一下縮圖 |

#### 全選 {#select-all}

您可以按一下主控台右上角的&#x200B;**全選**&#x200B;選項，選取任何檢視中的所有專案。

* 在&#x200B;**卡片檢視**&#x200B;中，已選取所有卡片。
* 在&#x200B;**清單檢視**&#x200B;中，已選取清單中的所有專案。
* 在&#x200B;**欄檢視**&#x200B;中，選取最左欄中的所有專案。

![全選](/help/sites-cloud/authoring/assets/select-all.png)

#### 取消全選 {#deselecting-all}

在任何情況下，當您選取專案時，所選專案的計數都會顯示在工具列的右上方。

您可以取消選取所有專案並結束選取模式，方法如下：

* 按一下或點選計數旁的&#x200B;**X**
* 使用&#x200B;**ESC**&#x200B;金鑰

![全部取消選取](/help/sites-cloud/authoring/assets/deselect-all.png)

在所有檢視中，如果您使用案頭裝置，點選鍵盤上的Esc鍵即可取消選取所有專案。

#### 選取範例 {#selecting-example}

1. 例如在卡片檢視中：

   ![卡片檢視選擇](/help/sites-cloud/authoring/assets/card-view-select.png)

1. 選取資源後，[動作工具列](#actions-toolbar)會覆蓋頂端標頭，提供目前適用於選取資源的動作存取權。

   若要結束選取模式，請選取右上方的&#x200B;**X**，或使用&#x200B;**ESCAPE**。

### 欄檢視 {#column-view}

![欄視圖](/help/sites-cloud/authoring/assets/column-view.png)

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
      * 表示所需動作的標籤可能與[收件匣](/help/sites-cloud/authoring/getting-started/inbox.md)中的專案有關。

* [此檢視中也提供快速動作](#quick-actions)，例如選取範圍以及常見的動作，例如編輯。

  ![快速動作](/help/sites-cloud/authoring/assets/quick-actions.png)

* 您可以點選/按一下卡片來向下瀏覽樹狀結構（注意避免快速動作），或使用標頭](#the-header)中的[階層連結來再次向上瀏覽。

### 清單檢視 {#list-view}

![清單檢視](/help/sites-cloud/authoring/assets/list-view.png)

* 清單檢視會列出目前層級中每個資源的資訊。
* 您可以點選/按一下資源名稱，在樹狀結構中向下導覽，並使用標頭](#the-header)中的[階層連結進行備份。
* 若要輕鬆選取清單中的所有專案，請使用清單左上方的核取方塊。

  ![清單檢視選取全部](/help/sites-cloud/authoring/assets/list-view-select-all.png)

   * 當選取清單中的所有專案時，此核取方塊會顯示為已核取。

      * 選取核取方塊以取消選取全部。

   * 僅選取部分專案時，其顯示會帶有減號。

      * 勾選核取方塊以選取全部。
      * 再次選取核取方塊以取消選取全部。

* 使用位於[檢視]按鈕下方的&#x200B;**檢視設定**&#x200B;選項來選取要顯示的欄。 下列欄可供顯示：

   * **名稱** — 頁面名稱，在多語言撰寫環境中很有用，因為它是頁面URL的一部分，無論使用何種語言，都不會變更
   * **修改日期** — 上次修改日期和上次修改的使用者
   * **已發佈** — 發佈狀態
   * **預覽** — 預覽狀態
   * **範本** — 頁面所依據的範本
   * **工作流程** — 目前已套用至頁面的工作流程。 將滑鼠移至上方或開啟「時間軸」時，可以取得更多資訊。
   * **頁面分析**
   * **不重複訪客**
   * 第&#x200B;**頁上的**&#x200B;時間

     ![選取資料行](/help/sites-cloud/authoring/assets/select-columns.png)

  預設會顯示&#x200B;**Name**&#x200B;欄，它構成了頁面URL的一部分。 在某些情況下，作者可能需要存取不同語言的頁面，如果作者不知道頁面的語言，檢視頁面名稱（通常不會變更）會很有幫助。

* 使用清單中每個專案最右側的點狀垂直列，變更專案的順序。

  >[!NOTE]
  >
  >變更順序僅適用於具有`jcr:primaryType`值為`sling:OrderedFolder`的已排序資料夾。

  ![欄順序](/help/sites-cloud/authoring/assets/column-order.png)

  選取垂直選取列並將專案拖曳到清單中的新位置。

  ![訂單清單](/help/sites-cloud/authoring/assets/order-list.png)

## 邊欄選擇器 {#rail-selector}

**邊欄選取器**&#x200B;會顯示在視窗左上角，並根據您目前的主控台顯示選項。

已展開![邊欄選擇器](/help/sites-cloud/authoring/assets/rail-selector-expanded.png)

例如，在&#x200B;**網站**&#x200B;主控台中，您可以選取僅限內容（預設）、內容樹狀結構、時間軸、參考、網站詳細資訊或篩選器側面板。

如果選取「僅限內容」，則只會出現邊欄圖示。 選取任何其他選項時，選項名稱會出現在邊欄圖示旁。

>[!NOTE]
>
>[鍵盤快速鍵](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)可用來快速切換邊欄顯示選項。

### 內容樹狀結構 {#content-tree}

內容樹可用來快速導覽側面板中的網站階層，並檢視目前資料夾中頁面的許多相關資訊。

使用內容樹側面板搭配清單檢視或卡片檢視，使用者可以輕鬆檢視專案的階層結構，並使用內容樹側面板在內容結構中輕鬆導覽，並在清單檢視中檢視詳細的頁面資訊。

![內容樹](/help/sites-cloud/authoring/assets/content-tree.png)

>[!NOTE]
>
>選取階層檢視中的專案後，可使用方向鍵來快速瀏覽階層。
>
>如需詳細資訊，請參閱[鍵盤快速鍵](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)。

### 時間表 {#timeline}

時間軸可用於檢視和/或啟動所選資源上已發生的事件。 若要開啟時間軸欄，請使用邊欄選取器：

![時間表樹狀結構](/help/sites-cloud/authoring/assets/timeline.png)

時間軸欄可讓您：

* 檢視與選取專案相關的各種事件。

   * 您可從下拉式清單中選取事件型別：

      * 評論
      * [註解](/help/sites-cloud/authoring/fundamentals/annotations.md)
      * [活動](/help/sites-cloud/authoring/personalization/activities.md)
      * [啟動](/help/sites-cloud/authoring/launches/overview.md)
      * [版本](/help/sites-cloud/authoring/features/page-versions.md)
      * [工作流程](/help/sites-cloud/authoring/workflows/overview.md)
         * 暫時性工作流程除外，因為沒有儲存這些<!--With the exception of [transient workflows](/help/sites-developing/workflows.md#transient-workflows) as no history information is saved for these-->的歷史記錄資訊
      * 顯示全部

* 新增/檢視有關所選項目的註解。「注 **釋** 」方塊會顯示在事件清單的底部。鍵入注釋後跟Return將註冊注釋。當選取「注 **釋** 」或「 **全部顯示** 」時顯示。

* 特定的主控台具有其他功能。 例如，在Sites主控台中，您可以：

   * [儲存版本](/help/sites-cloud/authoring/features/page-versions.md)
   * [啟動工作流程](/help/sites-cloud/authoring/workflows/applying.md)

這些選項可透過&#x200B;**註解**&#x200B;欄位旁的>形箭號存取。

![註解欄位](/help/sites-cloud/authoring/assets/comments.png)

### 參考 {#references}

**參考**&#x200B;顯示與所選資源的任何連線。 例如，在&#x200B;**Sites**&#x200B;主控台中，[頁面的引用](/help/sites-cloud/authoring/fundamentals/environment-tools.md#references)會顯示：

* [啟動](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)
* [即時副本](/help/sites-cloud/administering/msm/overview.md#openingthelivecopyoverviewfromreferences)
* [語言副本](/help/sites-cloud/administering/translation/preparation.md#seeing-the-status-of-language-roots)
* 內容參照：

   * 從其他頁面連結至所選頁面
   * 參考元件在所選頁面中借用的內容和/或借出的內容

![參考範例](/help/sites-cloud/authoring/assets/references-example.png)

### 網站 {#site}

**網站**&#x200B;顯示使用網站範本](/help/sites-cloud/administering/site-creation/create-site.md)建立的網站[的詳細資料。

![網站邊欄](../assets/site-rail.png)

請參閱檔案[使用網站邊欄管理您的網站主題](/help/sites-cloud/administering/site-creation/site-rail.md)，以取得有關如何使用邊欄管理網站[主題](/help/sites-cloud/administering/site-creation/site-themes.md)的詳細資訊。

>[!TIP]
>
>您可以在[快速網站建立歷程](/help/journey-sites/quick-site/overview.md)中找到從範本建立網站並自訂其主題的程式的端對端說明。

### 篩選條件 {#filter}

這會開啟類似於[搜尋](/help/sites-cloud/authoring/getting-started/search.md)的面板，並已設定適當的位置篩選器，可讓您進一步篩選您要檢視的內容。

![篩選器範例](/help/sites-cloud/authoring/assets/filter.png)
