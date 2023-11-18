---
title: 製作環境和工具
description: AEM的製作環境提供各種機制來組織和編輯您的內容
exl-id: cc3bd4cf-93bd-429d-9a2a-4a02a7b42f7c
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '2161'
ht-degree: 10%

---


# 製作環境和工具 {#authoring-the-environment-and-tools}

AEM的製作環境提供各種機制來組織和編輯您的內容。 提供的工具可從各種主控台和頁面編輯器存取。

{{edge-delivery-authoring}}

## 管理您的網站 {#managing-your-site}

此 **網站** console可讓您使用標題列、工具列、動作圖示（適用於選取的資源） 、導覽路徑標示，以及選取時的輔助導軌（例如時間軸和參考），來導覽和管理您的網站。

例如，欄檢視：

![欄檢視](/help/sites-cloud/authoring/assets/column-view.png)

## 編輯頁面內容 {#editing-page-content}

您可以使用頁面編輯器編輯頁面。 例如：

`http://<host>:<port>/editor.html/content/wknd/en/sports/la-skateparks.html`

![頁面編輯器](/help/sites-cloud/authoring/assets/page-editor.png)

>[!NOTE]
>
>第一次開啟頁面進行編輯時，一連串幻燈片會提供您功能導覽。
>
>您可以視需要略過導覽，並隨時透過選擇 **頁面資訊** 功能表。

## 存取說明 {#accessing-help}

編輯頁面時， **說明** 可從以下位置存取：

* 此 [**頁面資訊**](/help/sites-cloud/authoring/fundamentals/page-properties.md#page-properties) 選擇器，會顯示簡介幻燈片（在您第一次存取編輯器時顯示）
* 此 [設定](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) 特定元件的對話方塊(使用？ 圖示)，其中會顯示相關內容說明

進一步的 [可以從主控台取得說明相關資源](/help/sites-cloud/authoring/getting-started/basic-handling.md#accessing-help).

## 元件瀏覽器 {#components-browser}

元件是AEM內容的建置組塊。 您可以在頁面上放置多個元件，並設定其選項，以使用AEM建置您的內容頁面。

元件瀏覽器會顯示目前頁面上可用的所有元件。 這些檔案可以拖曳至適當位置，然後編輯以新增您的內容。

元件瀏覽器是側面板中的標籤(連同資產 [瀏覽器](#assets-browser)[和內容樹](#content-tree))。要開啟 (或關閉) 側面板，請使用工具欄左上角的表徵圖：

![側面板切換](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

當您開啟側面板時，它會從左側滑開(選取 **元件** 標籤（如有需要）。 開啟時，您可以瀏覽頁面可用的所有元件。

實際外觀和處理方式取決於您使用的裝置型別：

* **行動裝置(例如iPad)**

  元件瀏覽器會完整涵蓋正在編輯的頁面。

  若要將元件新增至頁面，請按住所需元件並向右移動，元件瀏覽器會關閉並重新顯示頁面 — 您可以在此處放置元件。

  ![行動裝置上的元件瀏覽器](/help/sites-cloud/authoring/assets/component-browser-mobile.png)

* **案頭裝置**

  元件瀏覽器會在視窗左側開啟。

  若要將元件新增至頁面，請按一下所需元件，並將其拖曳至所需位置。

  ![案頭上的元件瀏覽器](/help/sites-cloud/authoring/assets/component-browser-desktop.png)

  元件由表示

   * 元件名稱
   * 元件群組（灰色）
   * 圖示或縮寫
      * 標準元件的圖示為單色。
      * 縮寫一律為元件名稱的前兩個字元。

  從頂部的工具列 **元件** 瀏覽器您可以：

   * 依名稱篩選元件。
   * 使用下拉式選取範圍，將顯示限製為特定群組。

  如需元件的詳細說明，您可以選取中元件旁的資訊圖示 **元件** 瀏覽器（如果有的話）。 例如，對於 **內容片段**：

  ![元件瀏覽器資訊](/help/sites-cloud/authoring/assets/component-browser-information.png)

  如需有關可用元件的詳細資訊，請參閱 [元件主控台](/help/sites-cloud/authoring/features/components-console.md).

>[!NOTE]
>
>當寬度小於1024畫素時會偵測到行動裝置。 小型案頭視窗亦可如此。

## 資產瀏覽器 {#assets-browser}

資產瀏覽器會顯示全部 [資產](/help/assets/home.md) 這些檔案可直接在您目前頁面上使用。

資產瀏覽器是側面板中的標籤，以及元件瀏 [覽器](#components-browser)[和內容樹](#content-tree)。要開啟或關閉側面板，請使用工具欄左上角的表徵圖：

![側面板切換](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

當您開啟側面板時，它將會從左側滑開。 選取 **資產** 標籤（如有需要）。

![資產瀏覽器按鈕](/help/sites-cloud/authoring/assets/assets-browser-button.png)

當資產瀏覽器開啟時，您可以瀏覽頁面可用的所有資產。 如有需要，可使用無限捲動來展開清單。

![資產瀏覽器](/help/sites-cloud/authoring/assets/assets-browser.png)

若要將資產新增至頁面，請選取並拖曳至所需位置。 這可以是：

* 適當型別的現有元件。
   * 例如，您可以將影像型別的資產拖曳至影像元件上。
* A [預留位置](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-placeholder) 在段落系統中建立適當型別的元件。
   * 例如，您可以將影像型別的資產拖曳至段落系統，以建立「影像」元件。

>[!NOTE]
>
>這適用於特定資產和元件型別。 另請參閱 [使用「資產瀏覽器」插入元件](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component-using-the-assets-browser) 以取得更多詳細資料。

從資產瀏覽器頂端的工具列，您可以依以下方式篩選資產：

* 名稱
* 路徑
* 資產型別，例如，影像、影片、檔案、段落、內容片段和體驗片段
* 資產特性，例如方向與樣式
   * 僅適用於特定資產型別

實際外觀和處理方式取決於您使用的裝置型別：

* **行動裝置**

  資產瀏覽器會完整涵蓋正在編輯的頁面。

  若要將資產新增至頁面，請觸控並按住所需資產，然後將其向右移動，資產瀏覽器會關閉並重新顯示頁面，您可在此將資產新增至所需元件。

  ![行動裝置上的資產瀏覽器](/help/sites-cloud/authoring/assets/assets-browser-mobile.png)

* **案頭裝置**

  資產瀏覽器會在視窗左側開啟。

  若要將資產新增至頁面，請按一下所需資產，並將其拖曳至所需元件或位置。

  ![案頭上的資產瀏覽器](/help/sites-cloud/authoring/assets/assets-browser-desktop.png)

>[!NOTE]
>
>當寬度小於1024畫素時會偵測到行動裝置；也就是在小型案頭視窗中。

如果您需要快速變更資產，可以開始 [資產編輯器](/help/assets/manage-digital-assets.md) 按一下資產名稱旁顯示的編輯圖示，即可直接從資產瀏覽器中存取。

![資產編輯按鈕](/help/sites-cloud/authoring/assets/asset-edit-button.png)

## 內容樹 {#content-tree}

此 **內容樹狀結構** 會提供階層中頁面所有元件的概觀，讓您一眼即可檢視頁面的構成方式。

內容樹是側面板中的標籤（連同元件和資產瀏覽器）。 要開啟 (或關閉) 側面板，請使用工具欄左上角的表徵圖：

![內容樹按鈕](/help/sites-cloud/authoring/assets/content-tree-button.png)

當您開啟側面板時，它將滑開（從左側）。 選取 **內容樹狀結構** 標籤（如有需要）。 開啟時，您可以看到頁面或範本的樹狀檢視表示法，因此更容易瞭解其內容如何階層架構。 此外，在複雜頁面上，它可讓您更輕鬆地在頁面元件之間跳轉。

![內容樹](/help/sites-cloud/authoring/assets/content-tree-editor.png)

頁面可以輕鬆地由許多相同型別的元件組成，因此內容（元件）樹狀結構會在元件型別名稱（黑色）後面顯示描述性文字（灰色）。 描述性文字來自元件的常見屬性，例如標題或文字。

元件型別會以使用者語言顯示，而元件說明文字則來自頁面語言。

按一下元件旁的>形箭號將會收合或展開該層級。

![內容樹V形展開](/help/sites-cloud/authoring/assets/content-tree-chevron.png)

按一下元件即可在頁面編輯器中醒目顯示元件。 可執行的動作取決於頁面狀態：

* 例如，基本頁面：

  ![醒目提示的內容樹狀結構](/help/sites-cloud/authoring/assets/content-tree-highlighted.png)

  基本頁面的元件會有常用選項。

  如果按一下樹狀結構中的元件可編輯，則名稱右側會出現扳手圖示。 按一下此圖示會啟動元件的編輯對話方塊。

  ![內容樹編輯按鈕](/help/sites-cloud/authoring/assets/content-tree-edit.png)

* 屬於的頁面 [即時副本](/help/sites-cloud/administering/msm/overview.md)，其中元件繼承自其他頁面。

>[!NOTE]
>
>如果您在行動裝置上編輯頁面（如果瀏覽器寬度小於1024畫素），則無法使用內容樹。

## 片段 — 相關聯的內容瀏覽器 {#fragments-associated-content-browser}

如果您的頁面包含內容片段，那麼您也可以存取 [關聯內容的瀏覽器](/help/sites-cloud/authoring/fundamentals/content-fragments.md#using-associated-content).

## 參考 {#references}

**引用** 顯示所選頁面的連線：

* BluePrint
* 啟動
* 即時副本
* 語言副本
* 導入連結
* 參考元件的使用：借入和借出的內容

開啟所需的主控台，然後導覽至所需的資源並開啟 **引用** 使用：

![引用選項](/help/sites-cloud/authoring/assets/references.png)

[選取您需要的資源](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) 若要顯示與該資源相關的參照型別清單：

![參考詳細資料](/help/sites-cloud/authoring/assets/references-detail.png)

選取適當的參照型別以取得詳細資訊。 在某些情況下，當您選取特定參照時，可使用進一步的動作，包括：

* **傳入連結**，提供參照頁面的頁面清單，並可直接存取 **編輯** 其中一個頁面。

   * 這只能顯示靜態連結，而不能顯示動態產生的連結；例如來自清單元件的連結。

* 借入和借出內容的例項，使用 **參考** 元件，您可從此處導覽至參照/參照頁面
* [啟動](/help/sites-cloud/authoring/launches/overview.md)，提供相關啟動項的存取權
* [即時副本](/help/sites-cloud/administering/msm/overview.md) 顯示以所選資源為基礎之所有即時副本的路徑。
* [Blueprint](/help/sites-cloud/administering/msm/best-practices.md)，提供詳細資訊和各種動作
* [語言副本](/help/sites-cloud/administering/translation/managing-projects.md#creating-translation-projects-using-the-references-panel)，提供詳細資訊和各種動作

## 事件 — 時間表 {#events-timeline}

針對適當的資源(例如 **網站** 控制檯或資產 **資產** console) [時間軸可用來顯示任何選取專案上的最近活動](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline).

開啟所需的主控台，然後導覽至所需的資源並開啟 **時間表**，使用：

![時間軸選項](/help/sites-cloud/authoring/assets/timeline.png)

[選取您需要的資源](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)，然後 **全部顯示** 或 **活動** 若要列出所選資源上任何最近的動作：

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
* [提升啟動](/help/sites-cloud/authoring/launches/promoting.md) （僅限頁面為啟動時）

此外， **頁面資訊** 適時提供對analytics和建議的存取權。

## 頁面模式 {#page-modes}

編輯頁面時，有多種模式可允許不同的動作：

* [編輯](/help/sites-cloud/authoring/fundamentals/editing-content.md)  — 編輯頁面內容時所使用的模式。
* [版面](/help/sites-cloud/authoring/features/responsive-layout.md)  — 可讓您根據裝置建立及編輯回應式版面（如果頁面以版面容器為基礎）
* [目標定位](/help/sites-cloud/authoring/personalization/targeted-content.md)  — 透過所有管道的目標定位和測量，提高內容關聯性。
* [時間扭曲](/help/sites-cloud/authoring/features/page-versions.md#timewarp)  — 可讓您檢視特定時間點的頁面狀態。
* [即時副本狀態](/help/sites-cloud/authoring/fundamentals/editing-content.md#live-copy-status)  — 可讓您快速概略瞭解即時副本狀態以及不會繼承哪些元件。
* [開發人員模式](/help/implementing/developing/tools/developer-mode.md)
* [預覽](/help/sites-cloud/authoring/fundamentals/editing-content.md#previewing-pages)  — 用於檢視在發佈環境中顯示的頁面；或使用內容中的連結進行導覽。
* [註解](/help/sites-cloud/authoring/fundamentals/annotations.md)  — 用於在頁面上新增或檢視註解。

您可以使用右上角的圖示來存取這些專案。 實際圖示會變更，以反映您目前使用的模式：

![頁面模式](/help/sites-cloud/authoring/assets/page-modes.png)

>[!NOTE]
>
>* 視頁面的特性而定，某些模式可能無法使用。
>* 存取某些模式需要適當的許可權。
>* 由於空間限制，開發人員模式不適用於行動裝置。
>* 有一個 [鍵盤快速鍵](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) ( `Ctrl-Shift-M`)以在 **預覽** 和目前選取的模式(例如， **編輯**， **版面**、等等)。
>

## 路徑選擇 {#path-selection}

通常在製作時，必須選取另一個資源，例如定義另一個頁面或資源的連結，或選取影像時。 若要輕鬆選取路徑， [路徑欄位](#path-fields) 優惠自動完成和 [路徑瀏覽器](#path-browser) 允許更強大的選取範圍。

### 路徑欄位 {#path-fields}

此處用來說明的範例是影像元件。 如需使用和編輯元件的詳細資訊，請參閱 [用於頁面編寫的元件](/help/sites-cloud/authoring/fundamentals/components.md).

路徑欄位現在具有自動完成和先行等功能，可更輕鬆找到資源。

按一下 **開啟選取範圍對話方塊** 路徑欄位中的按鈕會開啟 [路徑瀏覽器](#path-browser) 對話方塊，以允許更詳細的選取選項。

![開啟選取範圍對話方塊按鈕](/help/sites-cloud/authoring/assets/open-selection-dialog-button.png)

或者，您可以開始在路徑欄位中輸入，AEM會在您輸入時提供相符的路徑。

![開啟選取範圍對話方塊按鈕](/help/sites-cloud/authoring/assets/path-selection-completion.png)

### 路徑瀏覽器 {#path-browser}

路徑瀏覽器的組織方式如下 [欄檢視](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view) ，以供您更詳細地選取資源。

![路徑瀏覽器](/help/sites-cloud/authoring/assets/path-browser.png)

* 選取資源後， **選取** 對話方塊右上角的按鈕會變成使用中按鈕。 選取以確認選取範圍或 **取消** 以中止。
* 如果上下文允許選擇多個資源，則選擇資源也會激活「選擇 **** 」按鈕，但也會向窗口的右上角添加選定資源的計數。按一下 **數字旁** 的X，取消選取全部。
* 當您瀏覽樹狀結構時，您的位置會反映在對話方塊頂端的階層連結中。 這些階層連結也可用來在資源階層內快速跳轉。
* 您隨時可以使用對話方塊頂端的搜尋欄位。 按一下 **X** ，以清除搜尋。
* 若要縮小搜尋範圍，您可以顯示篩選選項，並根據特定路徑篩選結果。

  ![篩選器選項](/help/sites-cloud/authoring/assets/filters-option.png)

## 鍵盤快速鍵 {#keyboard-shortcuts}

各種 [鍵盤快速鍵](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) 可用。
