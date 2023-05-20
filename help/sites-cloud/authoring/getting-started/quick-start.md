---
title: 編寫頁面的快速入門手冊
description: 快速、高級的指南，幫助您開始創作頁面內容
exl-id: d37c9b61-7382-4bf6-8b90-59726b871264
source-git-commit: 07702fbebc768ee877d68219eff5551b09c7ff3e
workflow-type: tm+mt
source-wordcount: '1585'
ht-degree: 6%

---

# 編寫頁面的快速入門手冊 {#quick-guide-to-authoring-pages}

本文檔旨在作為中關鍵頁面創作操作的高級快速入門指AEM南。 本文件:

* 不是全面覆蓋。
* 提供指向詳細文檔的連結。

有關創作的完整詳細資訊，請參AEM閱：

* [創作概念](/help/sites-cloud/authoring/getting-started/concepts.md)
* [基本處理](/help/sites-cloud/authoring/getting-started/basic-handling.md)

## 幾個簡短提示 {#a-few-quick-hints}

在開始快速入門手冊之前，這裡是一小組一般提示和提示，您應記住這些提示和提示，這些提示分為創作系統的各個區域。

### 在站點控制台中 {#sites-console}

* 建立按鈕

   * 此按鈕在許多控制台中都可用 — 所提供的選項是上下文相關的，因此可能因場景而異。

* 重新排序頁面

   * 可以在 [清單視圖](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view)。 將應用這些更改，並在其他視圖中可見。

### 頁面創作 {#page-authoring}

* 導航連結

   * **連結不可用於導航** 當您進入 **編輯** 的子菜單。 要使用需要的連結導航 [預覽頁面](/help/sites-cloud/authoring/fundamentals/editing-content.md#previewing-pages) 使用其中之一：

      * [預覽模式](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode)
      * [以已發佈狀態檢視](/help/sites-cloud/authoring/fundamentals/editing-content.md#view-as-published)

* 版本未從頁面編輯器啟動/建立。 現在從 **站點** 控制台(通過 **建立** 或 [時間軸](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline) )。

>[!NOTE]
>
>有許多鍵盤快捷方式可讓創作體驗更輕鬆。
>
>* [編輯頁面時的鍵盤快捷鍵](/help/sites-cloud/authoring/fundamentals/keyboard-shortcuts.md)
>* [控制台的鍵盤快捷鍵](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)


### 查找頁面 {#finding-your-page}

查找頁面有多方面；您可以導航和/或搜索：

1. 開啟 **站點** 控制台(使用 **站點** 的上界 [全局導航](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation)  — 當您選擇Adobe Experience Manager連結（左上）時，將觸發（下拉）該連結。

1. 按一下/按一下相應頁面，在樹下導航。 頁面資源的表示方式取決於您使用的視圖 —  [卡、清單或列](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources):

   ![「查看選擇」下拉清單](/help/sites-cloud/authoring/assets/views.png)

1. 使用 [標題中的breadcrumb](/help/sites-cloud/authoring/getting-started/basic-handling.md#the-header)，允許您返回到選定位置：

   ![Breadcrumb下拉清單](/help/sites-cloud/authoring/assets/breadcrumb.png)

1. 您也可以 [搜索](/help/sites-cloud/authoring/getting-started/search.md) 的雙曲餘切值。 您可以從顯示的結果中選擇頁面。

   ![搜索欄位](/help/sites-cloud/authoring/assets/search.png)

### 建立新頁面 {#creating-a-new-page}

至 [建立新頁面](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page):

1. [導航到位置](#finding-your-page) 建立新頁面的位置。
1. 使用 **建立** 表徵圖，然後選擇 **頁面** 清單中：

   ![「建立」按鈕](/help/sites-cloud/authoring/assets/create.png)

1. 這將開啟嚮導，該嚮導將指導您收集在 [建立新頁面](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page)。 按照螢幕上的說明進行操作。

### 選擇頁面以執行進一步操作 {#selecting-your-page-for-further-action}

您可以選擇頁面，以便對其執行操作。 選擇頁面將自動更新工具欄，以便顯示與該資源相關的操作。

如何選擇頁面取決於您在控制台中使用的視圖：

1. 欄檢視:

   * 點擊/按一下所需資源的縮略圖 — 縮略圖將覆蓋一個勾選項，以顯示其已被選中。

1. 清單檢視:

   * 點擊/按一下所需資源的縮略圖 — 縮略圖將覆蓋一個勾選項，以顯示其已被選中。

1. 卡片檢視:

   * 進入選擇模式 [選擇所需資源](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)。 如何執行此操作取決於設備：

      * 在移動設備上：點擊並握住卡
      * 在案頭設備上：使用 [快速操作](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions) 表徵圖表示：
   * 卡片將覆蓋一個勾號，以顯示已選擇頁面。

   ![示例卡](/help/sites-cloud/authoring/assets/card.png)

### 快速操作（僅限卡視圖/案頭） {#quick-actions-card-view-desktop-only}

[快速操作](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions) 可用：

1. [導航到該頁](#finding-your-page) 你想對它採取行動。
1. 將滑鼠指針懸停在表示所需資源的卡上。 將顯示快速操作：

   ![卡操作](/help/sites-cloud/authoring/assets/card-actions.png)

### 編輯頁面內容 {#editing-your-page-content}

要編輯頁面：

1. [導航到該頁](#finding-your-page) 編輯。
1. [開啟頁面進行編輯](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing) 使用「編輯（鉛筆）」表徵圖：

   ![「編輯」按鈕](/help/sites-cloud/authoring/assets/edit.png)

   可以從以下任一位置訪問此選項：

   * [快速操作（僅卡視圖/案頭）](#quick-actions-card-view-desktop-only) 的子目錄。
   * 工具欄 [已選擇頁面](#selecting-your-page-for-further-action)。

1. 開啟編輯器時，您可以：

   * [將新元件添加到頁面](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component) 按：

      * 開啟側面板
      * 選擇元件頁籤( [元件瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser))
      * 將所需元件拖到頁面上。

      側面板可開啟（和關閉），具有：

      ![側面板切換按鈕](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

   * [編輯現有元件的內容](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) 頁上：

      * 按一下或按一下開啟元件工具欄。 使用 **編輯** （鉛筆）表徵圖以開啟對話框。
      * 開啟元件的就地編輯器，按一下並按住或按兩下。 將顯示可用操作（對於某些元件，這將是有限的選擇）。
      * 要查看所有可用操作，請使用：

         ![全屏按鈕](/help/sites-cloud/authoring/assets/full-screen.png)
   * [配置現有元件的屬性](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-edit-dialog)

      * 按一下或按一下開啟元件工具欄。 使用 **配置** （扳手）表徵圖以開啟對話框。
   * [移動元件](/help/sites-cloud/authoring/fundamentals/editing-content.md#moving-a-component) 其中之一：

      * 將所需元件拖到其新位置。
      * 按一下或按一下開啟元件工具欄。 使用 **剪切** 然後 **貼上** 表徵圖。
   * [複製（並貼上）](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) 元件：

      * 按一下或按一下開啟元件工具欄。 使用 **複製** 然後 **貼上** 表徵圖。
   >[!NOTE]
   >
   >你可以 **貼上** 元件到同一頁或不同頁。 如果貼上到剪切/複製操作之前已開啟的其他頁面，則該頁面需要刷新頁面。

   * [刪除](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) 元件：

      * 使用點擊或按一下開啟元件工具欄，然後使用 **刪除** 表徵圖
   * [添加註釋](/help/sites-cloud/authoring/fundamentals/annotations.md#annotations) 到頁面：

      * 選擇 **注釋** 模式（語音氣泡表徵圖）。 使用 **添加註釋** 表徵圖。 使用右上角的X退出注釋模式。

         ![「注釋」按鈕](/help/sites-cloud/authoring/assets/annotations.png)
   * [預覽頁面](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode) （查看它在發佈環境中的顯示方式）

      * 選擇 **預覽** 的子菜單。
   * 使用 **編輯** 下拉選擇器。

   >[!NOTE]
   >
   >要使用必須使用的內容中的連結導航 [預覽模式](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode)。

### 編輯頁面屬性 {#editing-the-page-properties}

有兩種（主要）方法 [編輯頁面屬性](/help/sites-cloud/authoring/fundamentals/page-properties.md):

* 從 **站點** 控制台：

   1. [導航到該頁](#finding-your-page) 要發佈。
   1. 選擇 **屬性** 表徵圖：

      * [快速操作（僅限卡視圖/案頭）](#quick-actions-card-view-desktop-only) 的子目錄。
      * 工具欄 [已選擇頁面](#selecting-your-page-for-further-action)。

      ![「屬性」按鈕](/help/sites-cloud/authoring/assets/properties.png)

   1. 將顯示頁面屬性。 您可以根據需要進行更新，然後使用「保存」保留這些


* 當 [編輯頁面](#editing-your-page-content):

   1. 開啟 **頁面資訊** 的子菜單。
   1. 選擇 **開啟屬性** 開啟對話框以編輯屬性。

      ![「頁面資訊」按鈕](/help/sites-cloud/authoring/assets/page-information.png)

### 發佈頁面（或取消發佈） {#publishing-your-page-or-unpublishing}

有兩種主要方法 [發佈頁面](/help/sites-cloud/authoring/fundamentals/publishing-pages.md) （以及取消發佈）:

* 從 **站點** 控制台：

   1. [導航到該頁](#finding-your-page) 要發佈。
   1. 選擇 **快速發佈** 表徵圖：

      * [快速操作（僅限卡視圖/案頭）](#quick-actions-card-view-desktop-only) 的子目錄。
      * 工具欄 [已選擇頁面](#selecting-your-page-for-further-action) (還允許訪問 [稍後發佈](/help/sites-cloud/authoring/fundamentals/publishing-pages.md))。

      ![「快速發佈」按鈕](/help/sites-cloud/authoring/assets/quick-publish.png)


* 當 [編輯頁面](#editing-your-page-content):

   1. 開啟 **頁面資訊** 的子菜單。
   1. 選擇 **發佈頁面**。

* 從主控台取消發佈頁面只能透過「管理出版物 **** 」選項完成，此選項只能在工具列上使用 (不能透過快速動作)。

   ![「管理發布」按鈕](/help/sites-cloud/authoring/assets/manage-publication.png)

   的 **取消發佈頁面** 選項 **頁面資訊** 的子菜單。

   請參閱 [發佈頁面](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#unpublishing-pages) 的子菜單。

### 移動、複製和貼上或刪除頁面 {#move-copy-and-paste-or-delete-your-page}

這些操作都可通過以下方式觸發：

1. [導航到該頁](#finding-your-page) 要移動、複製和貼上或刪除。
1. 選擇複製 (然後貼上) 、移動或刪除圖示 (視需要)，使用下列任一項：

   * [快速操作（僅限卡視圖/案頭）](#quick-actions-card-view-desktop-only) 的下界。
   * 工具欄 [已選擇頁面](#selecting-your-page-for-further-action)。

   然後，取決於您的操作：

   * [複製](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#copying-and-pasting-a-page):

      * 然後，您需要導航到新位置並貼上。
   * [移動](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#moving-or-renaming-a-page):

      * 將開啟嚮導以收集移動頁面所需的資訊。 按照螢幕上的說明進行操作。
   * [刪除](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#deleting-a-page):

      * 系統將要求您確認操作。
   >[!NOTE]
   >
   >「刪除」不能作為「快速操作」使用。

### 鎖定頁面（然後解鎖） {#locking-your-page-then-unlocking}

[鎖定頁面](/help/sites-cloud/authoring/fundamentals/editing-content.md#locking-a-page) ，會使其他作者無法在您執行時使用頁面。您可以找到「鎖定 (和解除鎖定) 」圖示/按鈕：

* 工具欄 [已選擇頁面](#selecting-your-page-for-further-action)。
* 的 [「頁面資訊」下拉菜單](#editing-the-page-properties) 編輯頁面時。
* 編輯頁面時（當頁面被鎖定時），頁面工具欄

例如，鎖表徵圖如下所示：

![鎖定按鈕](/help/sites-cloud/authoring/assets/lock.png)

### 訪問頁面引用 {#accessing-page-references}

[快速訪問引用](/help/sites-cloud/authoring/fundamentals/environment-tools.md#references) 「參考」(References)導軌中提供「至」(to)/「自」(from)頁面。

1. 選擇 **引用** 使用工具欄表徵圖（之前或之後） [選擇頁面](#selecting-your-page-for-further-action)):

   ![「參照」視圖選項](/help/sites-cloud/authoring/assets/references.png)

   將顯示參考型別清單：

   ![引用視圖](/help/sites-cloud/authoring/assets/references-list.png)

1. 點擊/按一下所需的參考型別以顯示更多詳細資訊，並（在適當時）採取進一步的操作。

### 建立頁面版本 {#creating-a-version-of-your-page}

建立 [版本](/help/sites-cloud/authoring/features/page-versions.md) 頁面中：

1. 要開啟時間軸滑軌，請選擇 **[時間軸](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)** 使用工具欄表徵圖（之前或之後） [選擇頁面](#selecting-your-page-for-further-action)):

   ![時間線視圖選項](/help/sites-cloud/authoring/assets/timeline.png)

1. 點擊/按一下「時間軸」列右下角的省略號以顯示額外的按鈕，包括 **另存為版本**。

   ![時間軸視圖](/help/sites-cloud/authoring/assets/timeline-view.png)

1. 選擇 **另存為版本**，則 **建立**。

### 恢復/比較頁面版本 {#restoring-comparing-a-version-of-your-page}

恢復和/或比較頁面版本時使用的基本機制相同：

1. 選擇 **[時間軸](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)** 使用工具欄表徵圖（之前或之後） [選擇頁面](#selecting-your-page-for-further-action)):

   ![時間線視圖選項](/help/sites-cloud/authoring/assets/timeline.png)

   如果已保存頁面的版本，則會在時間軸中列出。

1. 點擊/按一下要恢復的版本 — 這將顯示其他操作按鈕：

   * **還原為此版本**

      * 版本將還原。
   * **顯示差異**

      * 將開啟頁面，並突出顯示兩個版本之間的差異。
