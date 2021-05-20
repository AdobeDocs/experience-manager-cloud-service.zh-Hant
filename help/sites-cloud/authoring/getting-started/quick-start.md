---
title: 製作頁面的快速入門手冊
description: 快速的高階指南，協助您開始編寫頁面內容
exl-id: d37c9b61-7382-4bf6-8b90-59726b871264
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '1585'
ht-degree: 5%

---

# 製作頁面的快速入門手冊 {#quick-guide-to-authoring-pages}

本檔案旨在提供AEM中關鍵頁面編寫動作的高階快速入門手冊。 本文檔：

* 不是全面涵蓋。
* 提供指向詳細文檔的連結。

如需使用AEM製作的完整詳細資訊，請參閱：

* [製作概念](/help/sites-cloud/authoring/getting-started/concepts.md)
* [基本處理](/help/sites-cloud/authoring/getting-started/basic-handling.md)

## 一些快速提示{#a-few-quick-hints}

開始快速入門手冊之前，以下是一小組一般提示和提示，您應謹記這些提示，並分為編寫系統的各個區域。

### 在站點控制台{#sites-console}中

* 建立按鈕

   * 此按鈕在許多主控台中都可用 — 所呈現的選項是內容相關的，因此可能會根據情境而有所不同。

* 重新排序頁面

   * 這可在[清單檢視](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view)中完成。 將應用這些更改，並在其他視圖中可見。

### 頁面編寫{#page-authoring}

* 導覽連結

   * **處於「編輯」模** 式時，無法導覽 **** 連結。若要導覽至連結，您需使用下列任一項來預覽頁面](/help/sites-cloud/authoring/fundamentals/editing-content.md#previewing-pages):[

      * [預覽模式](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode)
      * [以已發佈狀態檢視](/help/sites-cloud/authoring/fundamentals/editing-content.md#view-as-published)

* 版本不會從頁面編輯器啟動/建立。 現在可從&#x200B;**Sites**&#x200B;控制台（透過&#x200B;**Create**&#x200B;或[Timeline](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)選取資源完成）執行此操作。

>[!NOTE]
>
>有許多鍵盤快速鍵可讓編寫體驗更輕鬆。
>
>* [編輯頁面時的鍵盤快速鍵](/help/sites-cloud/authoring/fundamentals/keyboard-shortcuts.md)
* [控制台的鍵盤快速鍵](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)


### 查找頁面{#finding-your-page}

尋找頁面有各種方面；您可以導覽及/或搜尋：

1. 開啟&#x200B;**Sites**&#x200B;主控台(使用[全域導覽](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation)中的&#x200B;**Sites**&#x200B;選項 — 當您選取Adobe Experience Manager連結（左上角）時，就會觸發（下拉式）。

1. 點選/按一下適當的頁面，以向下導覽樹狀結構。 頁面資源的呈現方式取決於您使用的檢視 — [卡片、清單或欄](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources):

   ![檢視選取範圍下拉式清單](/help/sites-cloud/authoring/assets/views.png)

1. 使用標題](/help/sites-cloud/authoring/getting-started/basic-handling.md#the-header)中的[階層連結向上導覽樹狀結構，讓您返回至選取的位置：

   ![階層連結下拉式清單](/help/sites-cloud/authoring/assets/breadcrumb.png)

1. 您也可以[搜尋](/help/sites-cloud/authoring/getting-started/search.md)以取得頁面。 您可以從顯示的結果中選取您的頁面。

   ![搜尋欄位](/help/sites-cloud/authoring/assets/search.png)

### 建立新頁面{#creating-a-new-page}

若要[建立新頁面](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page):

1. [導覽至](#finding-your-page) 您要建立新頁面的位置。
1. 使用&#x200B;**Create**&#x200B;圖示，然後從清單中選取&#x200B;**Page**:

   ![建立按鈕](/help/sites-cloud/authoring/assets/create.png)

1. 這會開啟精靈，引導您收集建立新頁面[時所需的資訊。 ](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page)按照螢幕說明操作。

### 選擇您的頁面以執行進一步操作{#selecting-your-page-for-further-action}

您可以選取頁面，以便對其採取動作。 選取頁面會自動更新工具列，以顯示與該資源相關的動作。

如何選取頁面取決於您在主控台中使用的檢視：

1. 欄檢視:

   * 點選/按一下所需資源的縮圖 — 縮圖將會與勾號重疊，以顯示其已選取。

1. 清單檢視:

   * 點選/按一下所需資源的縮圖 — 縮圖將會與勾號重疊，以顯示其已選取。

1. 卡片檢視:

   * 通過[選擇所需資源](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)進入選擇模式。 具體操作方式取決於您的設備：

      * 在行動裝置上：點選並按住卡片
      * 在桌上型電腦上：使用刻度表表徵圖表示的[快速操作](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions):
   * 卡片將覆蓋上勾號，以顯示已選取頁面。

   ![範例卡片](/help/sites-cloud/authoring/assets/card.png)

### 快速操作（僅卡片視圖/案頭）{#quick-actions-card-view-desktop-only}

[提供](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions) 快速操作：

1. [導覽至](#finding-your-page) 您要對其採取動作的頁面。
1. 將滑鼠指標暫留在代表您所需資源的資訊卡上。 將顯示快速操作：

   ![卡片動作](/help/sites-cloud/authoring/assets/card-actions.png)

### 編輯頁面內容{#editing-your-page-content}

若要編輯頁面：

1. [導覽至](#finding-your-page) 您要編輯的頁面。
1. [使用「編輯」(](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing) 鉛筆)圖示開啟頁面進行編輯：

   ![編輯按鈕](/help/sites-cloud/authoring/assets/edit.png)

   這可透過下列任一項存取：

   * [適當資源的快速動作（僅限卡片檢視/案頭）](#quick-actions-card-view-desktop-only) 。
   * 選取[頁面時的工具列](#selecting-your-page-for-further-action)。

1. 編輯器開啟時，您可以：

   * [將新元件新增至您的](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component) 頁面：

      * 開啟側面板
      * 選擇元件頁簽（[元件瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)）
      * 將所需元件拖曳至頁面上。

      側面板可開啟（和關閉），具有：

      ![側面板切換按鈕](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

   * [編輯頁面上現有元](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) 件的內容：

      * 開啟元件工具列，點選或按一下。 使用&#x200B;**Edit**（鉛筆）圖示開啟對話方塊。
      * 使用點選並按住或按兩下，開啟元件的就地編輯器。 將顯示可用的動作（對於某些元件，這是有限的選取項目）。
      * 若要查看所有可用動作，請使用以下項目進入全螢幕模式：

         ![全螢幕按鈕](/help/sites-cloud/authoring/assets/full-screen.png)
   * [配置現有元件的屬性](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-edit-dialog)

      * 開啟元件工具列，點選或按一下。 使用&#x200B;**Configure**（扳手）圖示開啟對話方塊。
   * [移動元](/help/sites-cloud/authoring/fundamentals/editing-content.md#moving-a-component) 件：

      * 將所需元件拖曳至其新位置。
      * 開啟元件工具列，點選或按一下。 視需要使用&#x200B;**Cut**&#x200B;然後使用&#x200B;**Paste**&#x200B;圖示。
   * [複製（並貼上）](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) 元件：

      * 開啟元件工具列，點選或按一下。 視需要使用&#x200B;**Copy**&#x200B;然後使用&#x200B;**Paste**&#x200B;圖示。
   >[!NOTE]
   您可以將&#x200B;**貼上**&#x200B;元件至相同頁面或不同頁面。 如果貼到剪下/復製作業前已開啟的不同頁面，則該頁面需要重新整理頁面。

   * [](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) 刪除元件：

      * 開啟元件工具列並點選或按一下，然後使用&#x200B;**Delete**&#x200B;圖示。
   * [將注](/help/sites-cloud/authoring/fundamentals/annotations.md#annotations) 釋新增至頁面：

      * 選擇&#x200B;**注釋**&#x200B;模式（語音氣泡圖示）。 使用&#x200B;**Add annotation**（加號）圖示添加註釋。 使用右上角的X退出注釋模式。

         ![註解按鈕](/help/sites-cloud/authoring/assets/annotations.png)
   * [預覽頁面](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode) （以查看頁面在發佈環境中的顯示方式）

      * 從工具欄中選擇&#x200B;**預覽**。
   * 使用&#x200B;**Edit**&#x200B;下拉選擇器返回到編輯模式（或選擇其他模式）。

   >[!NOTE]
   若要在內容中使用連結進行導覽，您必須使用[預覽模式](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode)。

### 編輯頁面屬性{#editing-the-page-properties}

[編輯頁面屬性](/help/sites-cloud/authoring/fundamentals/page-properties.md)有兩種（主要）方法：

* 從&#x200B;**Sites**&#x200B;控制台：

   1. [導覽至](#finding-your-page) 您要發佈的頁面。
   1. 從以下任一項中選擇&#x200B;**屬性**&#x200B;表徵圖：

      * [適當資源的快速動作（僅限卡片檢視/案頭）](#quick-actions-card-view-desktop-only) 。
      * 選取[頁面時的工具列](#selecting-your-page-for-further-action)。

      ![「屬性」按鈕](/help/sites-cloud/authoring/assets/properties.png)

   1. 將顯示頁面屬性。 您可以視需要進行更新，然後使用「儲存」來保留這些


* 當[編輯頁面](#editing-your-page-content)時：

   1. 開啟&#x200B;**頁面資訊**&#x200B;功能表。
   1. 選擇&#x200B;**開啟屬性**&#x200B;以開啟用於編輯屬性的對話框。

      ![頁面資訊按鈕](/help/sites-cloud/authoring/assets/page-information.png)

### 發佈您的頁面（或取消發佈）{#publishing-your-page-or-unpublishing}

[發佈頁面](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)的主要方法有兩種（以及取消發佈）:

* 從&#x200B;**Sites**&#x200B;控制台：

   1. [導覽至](#finding-your-page) 您要發佈的頁面。
   1. 從以下任一項中選擇&#x200B;**快速發佈**&#x200B;表徵圖：

      * [適當資源的快速動作（僅限卡片檢視/案頭）](#quick-actions-card-view-desktop-only) 。
      * 選取[頁面時的工具列](#selecting-your-page-for-further-action)（也提供[稍後發佈](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)的存取權）。

      ![快速發佈按鈕](/help/sites-cloud/authoring/assets/quick-publish.png)


* 當[編輯頁面](#editing-your-page-content)時：

   1. 開啟&#x200B;**頁面資訊**&#x200B;功能表。
   1. 選擇&#x200B;**發佈頁面**。

* 從主控台取消發佈頁面只能透過「管理出版物 **** 」選項完成，此選項只能在工具列上使用 (不能透過快速動作)。

   ![「管理出版物」按鈕](/help/sites-cloud/authoring/assets/manage-publication.png)

   仍可透過編輯器中的&#x200B;**頁面資訊**&#x200B;功能表使用&#x200B;**取消發佈頁面**&#x200B;選項。

   如需詳細資訊，請參閱[發佈頁面](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#unpublishing-pages) 。

### 移動、複製和貼上或刪除您的頁面{#move-copy-and-paste-or-delete-your-page}

這些動作皆可由下列項目觸發：

1. [導覽至](#finding-your-page) 您要移動、複製和貼上或刪除的頁面。
1. 選擇複製 (然後貼上) 、移動或刪除圖示 (視需要)，使用下列任一項：

   * [所需資源的快速動作（僅限卡片檢視/案頭）](#quick-actions-card-view-desktop-only) 。
   * 選取[頁面時的工具列](#selecting-your-page-for-further-action)。

   然後，根據您的動作：

   * 複製:

      * 然後，您需要導覽至新位置並貼上。
   * 移動:

      * 將會開啟精靈，以收集移動頁面所需的資訊。 按照螢幕上的說明操作。
   * 刪除:

      * 系統會要求您確認動作。
   >[!NOTE]
   刪除不作為快速操作。

### 鎖定頁面（然後解鎖）{#locking-your-page-then-unlocking}

[鎖定頁面](/help/sites-cloud/authoring/fundamentals/editing-content.md#locking-a-page) ，會使其他作者無法在您執行時使用頁面。您可以找到「鎖定 (和解除鎖定) 」圖示/按鈕：

* 選取[頁面時的工具列](#selecting-your-page-for-further-action)。
* 編輯頁面時，「頁面資訊」下拉式功能表](#editing-the-page-properties)。[
* 編輯頁面時（頁面鎖定時），頁面工具列

例如，鎖表徵圖如下所示：

![鎖定按鈕](/help/sites-cloud/authoring/assets/lock.png)

### 存取頁面參考{#accessing-page-references}

[可在「參](/help/sites-cloud/authoring/fundamentals/environment-tools.md#references) 考」邊欄中快速存取參考/參考頁面。

1. 使用工具欄表徵圖選擇&#x200B;**引用**（在[選擇您的頁面](#selecting-your-page-for-further-action)之前或之後）:

   ![參考視圖選項](/help/sites-cloud/authoring/assets/references.png)

   將顯示參考類型清單：

   ![參考檢視](/help/sites-cloud/authoring/assets/references-list.png)

1. 點選/按一下所需的參照類型，以顯示更多詳細資訊，並（若適用）採取進一步動作。

### 建立頁面版本{#creating-a-version-of-your-page}

若要建立頁面的[version](/help/sites-cloud/authoring/features/page-versions.md):

1. 若要開啟「時間軸」邊欄，請使用工具列圖示（在[選取您的頁面](#selecting-your-page-for-further-action)之前或之後）選取&#x200B;**[時間軸](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)**:

   ![時間軸視圖選項](/help/sites-cloud/authoring/assets/timeline.png)

1. 點選/按一下「時間軸」欄右下方的省略號，以顯示額外的按鈕，包括&#x200B;**另存為版本**。

   ![時間軸檢視](/help/sites-cloud/authoring/assets/timeline-view.png)

1. 選擇&#x200B;**另存為版本**，然後選擇&#x200B;**建立**。

### 還原/比較頁面版本{#restoring-comparing-a-version-of-your-page}

還原和/或比較頁面版本時，會使用相同的基本機制：

1. 使用工具欄表徵圖選擇&#x200B;**[時間軸](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)**（在[選擇您的頁面](#selecting-your-page-for-further-action)之前或之後）:

   ![時間軸視圖選項](/help/sites-cloud/authoring/assets/timeline.png)

   如果已儲存您的頁面版本，則時間軸會列出此版本。

1. 點選/按一下您要還原的版本 — 這將顯示其他動作按鈕：

   * **還原為此版本**

      * 版本將會還原。
   * **顯示差異**

      * 將會開啟頁面，並強調顯示差異（兩個版本之間）。
