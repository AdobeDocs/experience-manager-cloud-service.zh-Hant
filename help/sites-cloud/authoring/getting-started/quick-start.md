---
title: 製作頁面的快速入門手冊
description: 快速高階指南，協助您開始編寫頁面內容
exl-id: d37c9b61-7382-4bf6-8b90-59726b871264
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '1541'
ht-degree: 5%

---


# 製作頁面的快速入門手冊 {#quick-guide-to-authoring-pages}

本檔案旨在作為AEM中重要頁面製作動作的高層級快速入門手冊。 本檔案：

* 不是為了提供完整的涵蓋範圍。
* 提供詳細檔案的連結。

如需使用AEM編寫的完整詳細資訊，請參閱：

* [製作概念](/help/sites-cloud/authoring/getting-started/concepts.md)
* [基本處理](/help/sites-cloud/authoring/getting-started/basic-handling.md)

{{edge-delivery-authoring}}

## 一些快速提示 {#a-few-quick-hints}

在開始快速入門手冊之前，請謹記以下小部分的一般秘訣和提示，並依撰寫系統的區域加以劃分。

### 在網站主控台中 {#sites-console}

* 建立按鈕

   * 此按鈕在許多主控台中都有提供 — 顯示的選項與內容相關，因此會根據情況而有所不同。

* 重新排序頁面

   * 這可以在[清單檢視](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view)中完成。 變更會套用並顯示在其他檢視中。

### 頁面製作 {#page-authoring}

* 導覽連結

   * 當您處於&#x200B;**編輯**&#x200B;模式時，**連結無法用於導覽**。 若要使用連結導覽，您需要使用以下其中一種方式[預覽頁面](/help/sites-cloud/authoring/fundamentals/editing-content.md#previewing-pages)：

      * [預覽模式](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode)
      * [以已發佈狀態檢視](/help/sites-cloud/authoring/fundamentals/editing-content.md#view-as-published)

* 系統不會從頁面編輯器啟動/建立版本。 現在可以從&#x200B;**網站**&#x200B;主控台完成這項作業（針對選取的資源透過&#x200B;**建立**&#x200B;或[時間表](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)）。

>[!NOTE]
>
>有數種鍵盤快速鍵可讓您更輕鬆進行撰寫體驗。
>
>* 編輯頁面時[鍵盤快速鍵](/help/sites-cloud/authoring/fundamentals/keyboard-shortcuts.md)
>* 主控台的[鍵盤快速鍵](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)

### 尋找您的頁面 {#finding-your-page}

尋找頁面有許多方面；您可以導覽及/或搜尋：

1. 開啟&#x200B;**網站**&#x200B;主控台(使用[全域導覽](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation)中的&#x200B;**網站**&#x200B;選項 — 這會在您選取Adobe Experience Manager連結（左上方）時觸發（下拉式清單）。

1. 點選/按一下適當的頁面，在樹狀結構中向下導覽。 頁面資源的呈現方式取決於您使用的檢視 — [卡片、清單或欄](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)：

   ![檢視選取下拉式清單](/help/sites-cloud/authoring/assets/views.png)

1. 使用[標頭](/help/sites-cloud/authoring/getting-started/basic-handling.md#the-header)中的階層連結來向上導覽樹狀結構，可讓您返回選取的位置：

   ![階層連結下拉式清單](/help/sites-cloud/authoring/assets/breadcrumb.png)

1. 您也可以[搜尋](/help/sites-cloud/authoring/getting-started/search.md)頁面。 您可以從顯示的結果中選取您的頁面。

   ![搜尋欄位](/help/sites-cloud/authoring/assets/search.png)

### 建立新頁面 {#creating-a-new-page}

若要[建立頁面](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page)：

1. [導覽至您要建立新頁面的位置](#finding-your-page)。
1. 使用&#x200B;**建立**&#x200B;圖示，然後從清單中選取&#x200B;**頁面**：

   ![建立按鈕](/help/sites-cloud/authoring/assets/create.png)

1. 這會開啟精靈，引導您收集在[建立新頁面](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page)時所需的資訊。 請依照熒幕上的指示操作。

### 選取您的頁面以採取進一步動作 {#selecting-your-page-for-further-action}

您可以選取頁面以便對其執行動作。 選取頁面會自動更新工具列，以便顯示該資源相關的動作。

如何選取頁面取決於您在主控台中使用的檢視：

1. 欄檢視：

   * 選取所需資源的縮圖 — 縮圖上覆蓋有勾號，表示已選取該縮圖。

1. 清單檢視：

   * 選取所需資源的縮圖 — 縮圖上覆蓋有勾號，表示已選取該縮圖。

1. 卡片檢視：

   * 透過[選取所需的資源](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)進入選取模式。 如何執行此動作取決於您的裝置：

      * 在行動裝置上：選取並按住卡片
      * 在案頭裝置上：使用勾號圖示表示的[快速動作](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)：

   * 卡片上覆蓋有一個勾號，表示已選取頁面。

   ![範例卡片](/help/sites-cloud/authoring/assets/card.png)

### 快速動作（僅限卡片檢視/案頭） {#quick-actions-card-view-desktop-only}

[快速動作](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)可用：

1. [導覽至您要採取動作的頁面](#finding-your-page)。
1. 將滑鼠指標停留在代表所需資源的卡片上。 隨即顯示快速動作：

   ![卡片動作](/help/sites-cloud/authoring/assets/card-actions.png)

### 編輯您的頁面內容 {#editing-your-page-content}

若要編輯您的頁面：

1. [瀏覽至您要編輯的頁面](#finding-your-page)。
1. [使用「編輯」（鉛筆）圖示開啟頁面以進行編輯](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing)：

   ![編輯按鈕](/help/sites-cloud/authoring/assets/edit.png)

   您可透過下列任一方式存取此專案：

   * 適當資源的[快速動作（僅限卡片檢視/案頭）](#quick-actions-card-view-desktop-only)。
   * 選取[頁面時的工具列](#selecting-your-page-for-further-action)。

1. 編輯器開啟時，您可以：

   * [新增元件至您的頁面](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component)，方法如下：

      * 開啟側面板
      * 選取元件索引標籤（[元件瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)）
      * 將必要的元件拖曳到頁面上。

     側面板的開啟（和關閉）方式：

     ![側面板切換按鈕](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

   * [編輯頁面上現有元件](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar)的內容：

      * 選取「 」以開啟元件工具列。 使用&#x200B;**編輯** （鉛筆）圖示開啟對話方塊。
      * 使用select-and-hold或按兩下滑鼠鍵開啟元件的就地編輯器。 會顯示可用的動作（對於某些元件而言，為有限的選取範圍）。
      * 若要檢視所有可用動作，請使用以下方法進入全熒幕模式：

        ![全熒幕按鈕](/help/sites-cloud/authoring/assets/full-screen.png)

   * [設定現有元件的屬性](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-edit-dialog)

      * 選取「 」以開啟元件工具列。 使用&#x200B;**設定** （扳手）圖示開啟對話方塊。

   * [移動元件](/help/sites-cloud/authoring/fundamentals/editing-content.md#moving-a-component)：

      * 將所需元件拖曳至其新位置。
      * 選取「 」以開啟元件工具列。 必要時使用&#x200B;**剪下**&#x200B;再使用&#x200B;**貼上**&#x200B;圖示。

   * [複製（並貼上）](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar)元件：

      * 選取「 」以開啟元件工具列。 視需要使用&#x200B;**複製**&#x200B;然後&#x200B;**貼上**&#x200B;圖示。

   >[!NOTE]
   >
   >您可以&#x200B;**貼上**&#x200B;元件至相同頁面或其他頁面。 如果貼上至剪下/復製作業前已開啟的其他頁面，該頁面需要重新整理。

   * [刪除](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar)元件：

      * 使用select開啟元件工具列，然後使用&#x200B;**刪除**&#x200B;圖示。

   * [新增註解](/help/sites-cloud/authoring/fundamentals/annotations.md#annotations)至頁面：

      * 選取&#x200B;**註釋**&#x200B;模式（語音泡泡圖示）。 使用&#x200B;**新增註釋** （加號）圖示新增註釋。 使用右上方的X退出附註模式。

        ![註解按鈕](/help/sites-cloud/authoring/assets/annotations.png)

   * [預覽頁面](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode) （檢視該頁面在發佈環境中的顯示方式）

      * 從工具列選取&#x200B;**預覽**。

   * 使用&#x200B;**編輯**&#x200B;下拉式選取器返回編輯模式（或選取其他模式）。

   >[!NOTE]
   >
   >若要使用內容中的連結進行瀏覽，您必須使用[預覽模式](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode)。

### 編輯頁面屬性 {#editing-the-page-properties}

有兩個（主要）方法[編輯頁面屬性](/help/sites-cloud/authoring/fundamentals/page-properties.md)：

* 從&#x200B;**網站**&#x200B;主控台：

   1. [瀏覽至您要發佈的頁面](#finding-your-page)。
   1. 選取&#x200B;**屬性**&#x200B;圖示，其來源為：

      * 適當資源的[快速動作（僅限卡片檢視/案頭）](#quick-actions-card-view-desktop-only)。
      * 選取[頁面時的工具列](#selecting-your-page-for-further-action)。

      ![屬性按鈕](/help/sites-cloud/authoring/assets/properties.png)

   1. 畫面隨即顯示頁面屬性。 您可以視需要進行更新，然後使用「儲存」來儲存這些專案

* 當[編輯您的頁面](#editing-your-page-content)時：

   1. 開啟&#x200B;**頁面資訊**&#x200B;功能表。
   1. 選取&#x200B;**開啟屬性**&#x200B;以開啟用於編輯屬性的對話方塊。

      ![頁面資訊按鈕](/help/sites-cloud/authoring/assets/page-information.png)

### 發佈頁面（或取消發佈） {#publishing-your-page-or-unpublishing}

有兩種主要方法[發佈您的頁面](/help/sites-cloud/authoring/fundamentals/publishing-pages.md) （以及取消發佈）：

* 從&#x200B;**網站**&#x200B;主控台：

   1. [瀏覽至您要發佈的頁面](#finding-your-page)。
   1. 從下列任一位置選取&#x200B;**快速Publish**&#x200B;圖示：

      * 適當資源的[快速動作（僅限卡片檢視/案頭）](#quick-actions-card-view-desktop-only)。
      * 已選取您的[頁面時的工具列](#selecting-your-page-for-further-action) (也可讓您稍後存取[Publish](/help/sites-cloud/authoring/fundamentals/publishing-pages.md))。

      ![快速Publish按鈕](/help/sites-cloud/authoring/assets/quick-publish.png)

* 當[編輯您的頁面](#editing-your-page-content)時：

   1. 開啟&#x200B;**頁面資訊**&#x200B;功能表。
   1. 選取&#x200B;**Publish頁面**。

* 從主控台取消發佈頁面只能透過「管理出版物 **** 」選項完成，此選項只能在工具列上使用 (不能透過快速動作)。

  ![管理出版物按鈕](/help/sites-cloud/authoring/assets/manage-publication.png)

  編輯器中仍可透過&#x200B;**頁面資訊**&#x200B;功能表使用&#x200B;**取消發佈頁面**&#x200B;選項。

  如需詳細資訊，請參閱[發佈頁面](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#unpublishing-pages)。

### 移動、複製並貼上或刪除您的頁面 {#move-copy-and-paste-or-delete-your-page}

這些動作都可由以下動作觸發：

1. [瀏覽至您要移動、複製和貼上或刪除的頁面](#finding-your-page)。
1. 選擇複製 (然後貼上) 、移動或刪除圖示 (視需要)，使用下列任一項：

   * 所需資源的[快速動作（僅限卡片檢視/案頭）](#quick-actions-card-view-desktop-only)。
   * 選取[頁面時的工具列](#selecting-your-page-for-further-action)。

   接著，視您的動作而定：

   * [副本](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#copying-and-pasting-a-page)：

      * 然後，您需要導覽至新位置並貼上。

   * [移動](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#moving-or-renaming-a-page)：

      * 精靈會開啟，以收集移動頁面所需的資訊。 請依照熒幕上的指示操作。

   * [刪除](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#deleting-a-page)：

      * 系統會要求您確認動作。

   >[!NOTE]
   >
   >「刪除」不適用於「快速動作」。

### 鎖定頁面（然後解鎖） {#locking-your-page-then-unlocking}

[鎖定頁面](/help/sites-cloud/authoring/fundamentals/editing-content.md#locking-a-page) ，會使其他作者無法在您執行時使用頁面。您可以找到「鎖定 (和解除鎖定) 」圖示/按鈕：

* 選取[頁面時的工具列](#selecting-your-page-for-further-action)。
* 編輯頁面時，[頁面資訊下拉式功能表](#editing-the-page-properties)。
* 編輯頁面（頁面已鎖定）時的頁面工具列

例如，鎖定圖示看起來像這樣：

![鎖定按鈕](/help/sites-cloud/authoring/assets/lock.png)

### 存取頁面參照 {#accessing-page-references}

[在「參考」邊欄中，可以快速存取](/help/sites-cloud/authoring/fundamentals/environment-tools.md#references)頁面上的參考。

1. 使用工具列圖示選取&#x200B;**參考** （在[選取您的頁面](#selecting-your-page-for-further-action)之前或之後）：

   ![參考檢視選項](/help/sites-cloud/authoring/assets/references.png)

   此時會顯示參考型別清單：

   ![參考檢視](/help/sites-cloud/authoring/assets/references-list.png)

1. 選取所需的參照型別以顯示更多詳細資訊，並（在適當時）採取進一步動作。

### 建立頁面的版本 {#creating-a-version-of-your-page}

若要建立頁面的[版本](/help/sites-cloud/authoring/features/page-versions.md)：

1. 若要開啟[時間表]邊欄，請使用工具列圖示選取&#x200B;**[時間表](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)** （在[選取您的頁面](#selecting-your-page-for-further-action)之前或之後）：

   ![時間表檢視選項](/help/sites-cloud/authoring/assets/timeline.png)

1. 選取[時間表]欄右下方的省略符號以顯示額外的按鈕，包括&#x200B;**另存為版本**。

   ![時間表檢視](/help/sites-cloud/authoring/assets/timeline-view.png)

1. 選取&#x200B;**另存為版本**，然後選取&#x200B;**建立**。

### 還原/比較頁面版本 {#restoring-comparing-a-version-of-your-page}

還原及/或比較頁面版本時，會使用相同的基本機制：

1. 使用工具列圖示選取&#x200B;**[時間表](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)** （在[選取您的頁面](#selecting-your-page-for-further-action)之前或之後）：

   ![時間表檢視選項](/help/sites-cloud/authoring/assets/timeline.png)

   如果頁面的某個版本已儲存，則會列在時間軸中。

1. 選取您要還原的版本 — 這會顯示其他動作按鈕：

   * **還原為此版本**

      * 版本已還原。

   * **顯示差異**

      * 頁面開啟時會反白顯示兩個版本之間的差異。
