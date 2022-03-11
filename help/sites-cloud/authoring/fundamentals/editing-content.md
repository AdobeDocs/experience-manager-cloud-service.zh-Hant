---
title: 編輯頁面內容
description: 建立頁面後，您可以編輯內容以進行所需的更新
exl-id: 8af0f621-14e8-4605-a51a-a3be21f19092
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '2974'
ht-degree: 6%

---

# 編輯頁面內容{#editing-page-content}

建立頁面（新建或作為啟動或即時拷貝的一部分）後，您可以編輯內容以進行所需的更新。

內容是使用 [元件](/help/sites-cloud/authoring/features/components-console.md) （適用於內容類型），可以拖到頁面上。 然後可以就地編輯、移動或刪除這些內容。

>[!NOTE]
>
>您的帳戶需要適當的訪問權限和權限來編輯頁面。
>
>如果您遇到任何問題，我們建議您與系統管理員聯繫。
<!--
>Your account needs the [appropriate access rights](/help/sites-administering/security.md) and [permissions](/help/sites-administering/security.md#permissions) to edit pages.
-->

>[!NOTE]
>
>如果您的頁面和/或模板已正確設定，則可以使用 [響應佈局](/help/sites-cloud/authoring/features/responsive-layout.md) 的子菜單。

>[!TIP]
>
>在 **編輯** 模式，內容中的連結可見，但 **無法訪問**。 使用 [預覽模式](#previewing-pages) 的子菜單。

## 頁面工具欄 {#page-toolbar}

頁面工具欄提供對相應功能的訪問，這取決於頁面配置。

![頁面工具欄](/help/sites-cloud/authoring/assets/editing-page-toolbar.png)

工具欄提供對多種選項的訪問。 根據您當前的上下文和配置，某些選項可能不可用。

* **切換側面板**

   此操作將開啟/關閉側面板，該面板將 [資產瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser)。 [元件瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser), [內容樹](/help/sites-cloud/authoring/fundamentals/environment-tools.md#content-tree)。

   ![側面板切換](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

* **頁面資訊**

   提供對 [頁面資訊](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) 菜單，包括頁面詳細資訊和可在頁面上執行的操作，包括查看和編輯頁面資訊、查看頁面屬性以及發佈/取消發佈頁面。

   ![「頁面資訊」按鈕](/help/sites-cloud/authoring/assets/page-information-icon.png)

* **模擬器**

   切換 [模擬工具欄](/help/sites-cloud/authoring/features/responsive-layout.md#selecting-a-device-to-emulate)，用於模擬另一設備上頁面的外觀。 這將在佈局模式下自動切換。

   ![模擬器按鈕](/help/sites-cloud/authoring/assets/emulator.png)

* **ContextHub**

   開啟 [上下文中心](/help/sites-cloud/authoring/personalization/contexthub.md)。 僅在「預覽」模式下可用。

   ![「上下文中心」按鈕](/help/sites-cloud/authoring/assets/context-hub.png)

* **頁面標題**

   這純粹是資訊性的。

   ![頁面標題](/help/sites-cloud/authoring/assets/page-title.png)

* **模式選擇器**

   顯示當前 [模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) 並允許您選擇其他模式，如編輯、佈局、時間曲線或目標。

   ![「模式選擇器」按鈕](/help/sites-cloud/authoring/assets/mode-selector.png)

* **預覽**

   啟用 [預覽模式](#preview-mode)。 這將按發佈時的顯示方式顯示頁面。

   ![預覽按鈕](/help/sites-cloud/authoring/assets/preview.png)

* **注釋**

   允許您添加 [注釋](/help/sites-cloud/authoring/fundamentals/annotations.md) 查看頁面時顯示。 在第一個注釋之後，表徵圖將切換到指示頁面上注釋數的數字。

   ![「注釋」按鈕](/help/sites-cloud/authoring/assets/annotations.png)

### 狀態通知 {#status-notification}

如果頁面是 [工作流](/help/sites-cloud/authoring/workflows/overview.md) 或多個工作流，編輯頁面時，此資訊顯示在螢幕頂部的通知欄中。

![工作流通知](/help/sites-cloud/authoring/assets/editing-workflow-notification.png)

>[!NOTE]
>
>狀態欄僅對具有適當權限的用戶帳戶可見。

通知列出針對頁面運行的工作流。 如果用戶參與當前工作流步驟，則選項 [影響工作流狀態](/help/sites-cloud/authoring/workflows/participating.md) 並獲取有關工作流的詳細資訊，如：

* **完成**  — 開啟 **完成工作項** 對話
* **委託**  — 開啟 **完成工作項** 對話
* **查看詳細資訊**  — 開啟 **詳細資訊** 窗口

通過通知欄完成和委託工作流步驟與在 [參與工作流](/help/sites-cloud/authoring/workflows/participating.md) 從「通知」收件箱。

如果頁面受多個工作流的制約，則通知的右端將顯示工作流數以及箭頭按鈕，以允許您滾動查看工作流。

![多個工作流通知](/help/sites-cloud/authoring/assets/editing-workflow-notification-multiple.png)

## 元件佔位符 {#component-placeholder}

元件佔位符是一個指示器，用於顯示在您放置元件時元件的位置 — 位於當前懸停在元件上方。

* 向頁面添加新元件時（從元件瀏覽器拖動）:

   ![將新元件添加到頁面時的佔位符](/help/sites-cloud/authoring/assets/editing-component-placeholder.png)

* 移動現有元件時：

   ![在頁面上移動現有元件時的佔位符](/help/sites-cloud/authoring/assets/editing-component-placeholder-existing.png)

## 插入元件 {#inserting-a-component}

### 從元件瀏覽器插入元件 {#inserting-a-component-from-the-components-browser}

可以使用 [元件瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)。 的 [元件佔位符](#component-placeholder) 顯示元件的位置：

1. 確保您的頁面位於 [**編輯** 模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)。
1. 開啟 [元件瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)。
1. 將所需元件拖到 [必需職位](#component-placeholder)。
1. [編輯](#edit-content) 元件。

>[!NOTE]
>
>在移動設備上，元件瀏覽器將填充整個螢幕。 一旦開始拖動元件，瀏覽器將關閉以再次顯示頁面，以便您可以放置元件。

### 從段落系統插入元件 {#inserting-a-component-from-the-paragraph-system}

可以使用 **將元件拖動到此處** 框：

1. 確保您的頁面位於 [**編輯** 模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)。
1. 從段落系統中選擇和添加新元件有兩種方法：

   * 選擇 **插入元件** 選項(+) **將元件拖動到此處** 框。

      ![插入元件](/help/sites-cloud/authoring/assets/editing-insert-component.png)

   * 如果您在台式機設備上，可以按兩下 **將元件拖動到此處** 框。

   * 的 **插入新元件** 對話框將開啟，以允許您選擇所需的元件：

      ![「插入新元件」對話框](/help/sites-cloud/authoring/assets/editing-insert-component-selection.png)

1. 所選元件將添加到頁面底部。 [編輯](#edit-content) 元件。

### 使用資產瀏覽器插入元件 {#inserting-a-component-using-the-assets-browser}

也可以通過從 [資產瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser)。 這將自動建立相應類型（並包含資產）的新元件。

可以為安裝配置此行為。 有關詳細資訊，請參閱配置段落系統，以便拖動資產可建立元件實例。 <!--This behavior can be configured for your installation. See [Configuring a Paragraph System so that Dragging an Asset Creates a Component Instance](/help/sites-developing/developing-components.md#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance) for further details.-->

要通過拖動上述資產類型之一來建立元件：

1. 確保您的頁面位於 [**編輯** 模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)。
1. 開啟 [資產瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser)。
1. 將所需資產拖到所需位置。 的 [元件佔位符](#component-placeholder) 顯示元件的位置。

   將在所需位置建立與資產類型相適應的元件 — 該元件將包含所選資產。

1. [編輯](#edit-content) 元件（如果需要）。

>[!NOTE]
>
>在移動設備上，資產瀏覽器將填充整個螢幕。 一旦開始拖動資產，瀏覽器將關閉以再次顯示頁面，以便您可以放置資產。

如果在瀏覽資產時發現需要快速更改資產，則可以啟動 [資產編輯器](/help/assets/manage-digital-assets.md) 按一下資產名稱旁邊的編輯表徵圖，即可直接從瀏覽器中找到。

![資產編輯按鈕](/help/sites-cloud/authoring/assets/asset-edit-button.png)

## 元件工具欄 {#component-toolbar}

選擇元件將開啟工具欄。 這提供了對可對元件執行的各種操作的訪問權限。

用戶可用的實際操作將顯示為適當的，但此處不能描述所有操作。

![元件工具欄](/help/sites-cloud/authoring/assets/editing-component-toolbar.png)

* **編輯**

   [取決於元件類型](/help/sites-cloud/authoring/fundamentals/components.md) 這將允許您 [編輯元件的內容](#edit-content)。 通常會提供工具欄。

   ![「編輯」按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-edit.png)

* **設定**

   [取決於元件類型](/help/sites-cloud/authoring/fundamentals/components.md) 這將允許您編輯和配置元件的屬性。 通常會開啟對話框。

   ![「配置」按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-configure.png)

* **複製**

   這將將元件複製到剪貼簿。 貼上操作後，原始元件將保留。

   ![「複製」按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-copy.png)

* **剪下**

   這將將元件複製到剪貼簿。 貼上操作後，將刪除原始元件。

   ![剪切按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-cut.png)

* **刪除**

   這將從頁面中刪除元件並進行確認。

   ![刪除按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-delete.png)

* **插入元件**

   這將開啟對話框 [添加新元件](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component-from-the-paragraph-system)。

   ![「插入」按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-insert.png)

* **貼上**

   這將將元件從剪貼簿貼上到頁面。 原始檔案是否保留，取決於您是使用複製還是剪切。

   * 可以貼上到同一頁或另一頁。
   * 貼上的項目將貼上到您選擇貼上操作的項目上方。
   * 僅當剪貼簿上存在內容時，才會顯示「預處理」操作。

   ![貼上按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-paste.png)

   >[!NOTE]
   >
   >如果貼上到剪切/複製操作之前已開啟的其他頁面，則必須刷新該頁面才能查看貼上的內容。

* **群組**

   這允許您同時選擇多個元件。 在案頭設備上，可通過 **按住Ctrl鍵並按一下** 或 **按住Command鍵並按一下**。

   ![「組」按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-group.png)

* **父級**

   這允許您選擇所選元件的父元件。

   ![「父項」按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-parent.png)

* **配置**

   這允許您修改 [佈局](/help/sites-cloud/authoring/fundamentals/editing-content.md#edit-component-layout) 的子菜單。 這僅適用於選定元件，不激活 [佈局模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) 的下一頁。

   ![佈局按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-layout.png)

* **轉換為體驗片段變體**

   這允許您建立新 [體驗片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md) 或將其添加到現有體驗片段。

   ![「轉換為體驗片段」按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-xf.png)

## 編輯內容 {#edit-content}

在元件中添加和/或編輯內容有兩種方法：

* 開啟 [元件對話框](#component-edit-dialog)。
* [拖放資產](#drag-and-drop-assets-into-component) 直接添加內容。

### 元件編輯對話框 {#component-edit-dialog}

您可以使用元件工具列的「編輯 (鉛筆) 」圖示， [開啟元件以編輯內容](#component-toolbar)。

確切的編輯選項將取決於元件。 對於某些元件 [所有操作將僅在全屏模式下可用](#edit-content-full-screen-mode)。 例如：

* 文字元件

   ![文本元件的工具欄](/help/sites-cloud/authoring/assets/editing-text-component-toolbar.png)

* 影像元件

   ![影像元件的工具欄](/help/sites-cloud/authoring/assets/editing-image-component-toolbar.png)

   >[!NOTE]
   >
   >編輯在空影像元件上不起作用。
   >
   >必須先將影像拖動或上載到元件，然後才能開始編輯它。

* 影像元件 — 全屏

   [進入影像元件的全螢幕模式](#edit-content-full-screen-mode) ，可讓您有更多空間編輯影像，並顯示額外的編輯選項，例如「啟動地圖」和「重設縮放」 ********。此外，全螢幕還允許選取裁切預設集。

   ![影像元件的全屏模式](/help/sites-cloud/authoring/assets/editing-image-component-full-screen.png)

* 由多個基本元件構建的元件首先要求您確認您要的編輯選項集：

### 將資產拖放到元件中 {#drag-and-drop-assets-into-component}

對於特定的元件類型（如影像），您可以直接將資產從資產瀏覽器拖放到元件中以更新內容。

## 以全屏模式編輯內容 {#edit-content-full-screen-mode}

對於所有元件，可以使用（並退出）訪問全屏模式：

![全屏按鈕](/help/sites-cloud/authoring/assets/editing-full-screen.png)

例如， **文本** 元件：

![全屏文本元件](/help/sites-cloud/authoring/assets/editing-text-full-screen.png)

>[!NOTE]
>
>對於某些元件，全屏模式的可用選項將比基本就地編輯器更多。

## 移動元件 {#moving-a-component}

要移動段落元件，請執行以下操作：

1. 選擇要移動的段落，可按一下並按住或按一下並按住。
1. 將段落拖到新位置。 指AEM明可以存放段落的位置。 將其放在您所需的位置。

   ![移動元件](/help/sites-cloud/authoring/assets/editing-moving-component.png)

1. 您的段落已移動。

>[!TIP]
>
>您還可以使用 [剪切和貼上](#component-toolbar) 的子菜單。

## 編輯元件佈局 {#edit-component-layout}

您可以選取元件的 [Layout](/help/sites-cloud/authoring/features/responsive-layout.md)****  (配置) 動作，以變更元件的配置，並節省時間，而不需離開編輯模式，而不需重複從編輯切換到配置模式來調整元件。

1. 在 **編輯** 在站點控制台的模式下，選擇元件將顯示元件的工具欄。

   ![頁面元件的元件工具欄](/help/sites-cloud/authoring/assets/editing-layout-toolbar.png)

   按一下或點擊 **佈局** 操作以調整元件的佈局。

   ![元件工具欄的「佈局」按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-layout.png)

1. 選擇「佈局」(Layout)操作後：

   * 顯示元件的大小調整手柄。
   * 模擬器工具欄顯示在螢幕頂部。
   * 佈局操作而不是元件工具欄上顯示的標準編輯操作。

   ![佈局模式下的元件](/help/sites-cloud/authoring/assets/editing-layout-mode.png)

   現在，可以修改元件的佈局，如 [佈局模式](/help/sites-cloud/authoring/features/responsive-layout.md#defining-layouts-layout-mode)。

1. 進行必要的佈局更改後，按一下 **關閉** 按鈕停止修改元件的佈局。 元件的工具欄返回其正常編輯狀態。

   ![頁面元件的元件工具欄](/help/sites-cloud/authoring/assets/editing-layout-exit.png)

>[!TIP]
>
>「佈局」(Layout)操作在選定元件的範圍內受限。 例如，如果正在編輯一個元件的佈局，然後按一下另一個元件，則新選定元件的標準編輯工具欄（而不是佈局工具欄）將顯示，調整大小手柄以及模擬器工具欄將消失。
>
>如果需要編輯頁面的總體佈局，影響多個元件，請切換到 [佈局模式](/help/sites-cloud/authoring/features/responsive-layout.md)。

## 繼承的元件 {#inherited-components}

繼承是一種機制，在該機制中，內容可以自動從一個元件推送到另一個元件。 繼承的元件可以是各種方案的產物，包括：

* [多站點管理](/help/sites-cloud/administering/msm/overview.md)
* [啟動](/help/sites-cloud/authoring/launches/overview.md) （基於即時拷貝）。

可以取消（然後重新啟用）繼承。 根據元件的不同，如果元件位於作為即時拷貝或啟動一部分的頁面（基於即時拷貝），則可以從元件工具欄獲得此功能。

![顯示繼承關係的元件工具欄](/help/sites-cloud/authoring/assets/editing-component-toolbar-inheritance.png)

例如：

* 取消繼承

   ![「取消繼承」按鈕](/help/sites-cloud/authoring/assets/editing-cancel-inheritance.png)

* 重新啟用繼承（如果已取消繼承）

   ![「重新啟用繼承」按鈕](/help/sites-cloud/authoring/assets/editing-reenable-inheritance.png)

* 在藍圖或即時拷貝源中也提供了部署操作

   ![「推廣」按鈕](/help/sites-cloud/authoring/assets/editing-rollout.png)

## 編輯頁面模板 {#editing-the-page-template}

您可以輕鬆切換至範本 [編輯器](/help/sites-cloud/authoring/features/templates.md#editing-templates-template-authors) ，方法是在「頁面資訊」選單中選取 **「編輯範本**」(Edit [Template](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) )。

在「欄檢視」或「清單檢視」中選取頁面時，您可輕鬆查看該頁 [面所依據](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view)[的範本](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view)。

## 即時副本狀態 {#live-copy-status}

的 [「即時複製狀態」頁模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) 允許您快速概述即時拷貝狀態以及哪些元件是/不是繼承的：

* 綠色邊框：繼承
* 粉紅色邊框：已取消繼承

例如：

![顯示即時複製狀態的示例](/help/sites-cloud/authoring/assets/editing-live-copy-status.png)

## 添加註釋 {#adding-annotations}

[注釋](/help/sites-cloud/authoring/fundamentals/annotations.md) 允許審閱者和其他作者提供有關您內容的反饋。 它們通常用於審查和驗證目的。

## 預覽頁面 {#previewing-pages}

預覽頁面有兩個選項：

* [預覽模式](#preview-mode)  — 快速就地預覽
* [查看為已發佈](#view-as-published)  — 在新頁籤中開啟頁面的完整預覽

>[!TIP]
>
>* 內容中的連結是可見的，但在「編輯」模式下無法訪問。
>* 如果要使用連結導航，請使用其中一個預覽選項。
>* 使用 [鍵盤快捷鍵](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) `Ctrl-Shift-M` 以在預覽和上次選定模式之間切換。


>[!NOTE]
>
>WCM模式Cookie已設定為兩個預覽選項。

### 預覽模式 {#preview-mode}

編輯內容時，可以使用預覽來預覽頁面 [模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)。 此模式：

* 隱藏各種編輯機制，以快速查看頁面在發佈時的顯示方式。
* 允許您使用連結進行導航。
* 是 **不** 刷新頁面內容。

創作時，預覽模式可使用頁面編輯器右上角的表徵圖：

![預覽按鈕](/help/sites-cloud/authoring/assets/preview.png)

### 以已發佈狀態檢視 {#view-as-published}

的 **查看為已發佈** 的 [頁面資訊](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) 的子菜單。 這將在新頁籤中開啟頁面，刷新內容，並完全按照頁面在發佈環境中的顯示方式顯示頁面。

## 鎖定頁面 {#locking-a-page}

允AEM許您鎖定頁面，以便其他人不能修改內容。 當您對一個特定頁面進行大量編輯或需要將頁面凍結一段時間時，此功能非常有用。

可以從以下任一位置鎖定頁面：

* **站點** 控制台

   1. 選擇頁 [選擇模式](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)。
   1. 選擇鎖定表徵圖。

      ![鎖定按鈕](/help/sites-cloud/authoring/assets/lock.png)

* **頁面編輯器**

   1. 選擇 **頁面資訊** 按鈕。
   1. 選擇 **鎖定頁** 的雙曲餘切值。

一旦鎖定，控制台視圖資訊就會更新，編輯鎖定符號時，工具欄中會顯示該資訊。

![鎖定頁面的示例](/help/sites-cloud/authoring/assets/editing-locked-page.png)

>[!CAUTION]
>
>在模擬用戶時可以執行鎖定頁面。 但是，只有模擬用戶或管理員用戶才能解鎖以這種方式鎖定的頁面。
>
>無法通過模擬鎖定頁面的用戶來解鎖頁面。
<!--
>Locking a page can be performed when [impersonating a user](/help/sites-administering/security.md#impersonating-another-user). However a page locked in this way can only then be unlocked by the user who was impersonated or by the admin user.
-->

## 解鎖頁面 {#unlocking-a-page}

解鎖頁面與 [鎖定頁面](#locking-a-page)。 鎖定頁面後，鎖定選項將被解鎖操作替換。

「頁面資訊」功能表 **會列出** 「解除鎖定」為選項，而網站主控台中的「鎖定」圖示會以「解除鎖定」圖示 **** 取代。

![解鎖按鈕](/help/sites-cloud/authoring/assets/unlock.png)

>[!CAUTION]
>
>在模擬用戶時可以執行鎖定頁面。 但是，只有模擬用戶或管理員用戶才能解鎖以這種方式鎖定的頁面。
>
>無法通過模擬鎖定頁面的用戶來解鎖頁面。
<!--
>Locking a page can be performed when [impersonating a user](/help/sites-administering/security.md#impersonating-another-user). However a page locked in this way can only then be unlocked by the user who was impersonated or by the admin user.
-->

## 撤消和重做頁面編輯 {#undoing-and-redoing-page-edits}

以下表徵圖允許您撤消或重做操作。 這些內容在適當時顯示在工具欄中：

![撤消和重做按鈕](/help/sites-cloud/authoring/assets/redo.png)

>[!TIP]
>
>* 的 [鍵盤快捷鍵](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) `Ctrl-Z` 也可用於撤消頁面編輯操作。
>* 鍵盤快捷鍵 `Ctrl-Y` 也可用於重做頁面編輯操作。


>[!NOTE]
>
>請參閱 [撤消和重做頁面編輯 — 理論](#undoing-and-redoing-page-edits-the-theory) 的子菜單。

## 撤消和重做頁面編輯 — 理論 {#undoing-and-redoing-page-edits-the-theory}

AEM儲存所執行操作的歷史記錄以及執行操作的順序，以便您可以按執行操作的順序撤消多個操作，並重做這些操作以在必要時重新應用一個或多個操作。

如果選擇了內容頁面上的元素（如文本元件），則撤消和重做命令將應用於所選項目。

撤消和重做命令的行為與其他軟體中的行為類似。 在您對內容做出決策時，使用命令恢復網頁的最近狀態。 例如，如果將文本段落移動到頁面上的其他位置，則可以使用撤消命令將段落移回。 如果隨後確定上一個位置更好，請使用redo命令「撤消」。

例如，您可以:

* 只要自使用撤消後未進行頁面編輯，就重做操作。
* 撤消最多20個編輯操作（預設設定）。
* 還使用 [鍵盤快捷鍵](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) 撤消和重做。

可以對以下類型的頁面更改使用撤消和重做：

* 添加、編輯、刪除和移動段落
* 原地編輯段落內容
* 在頁面中複製、剪切和貼上項目

>[!NOTE]
>
>* 要撤消和重做對檔案和影像的更改，需要特殊權限。
>* 對檔案和影像的更改歷史至少持續10小時。 但是，在此之後，無法保證撤消更改。 管理員可以更改預設時間（10小時）。
>* 系統管理員可以根據實例的要求配置「撤消/重做」功能的各個方面。

<!--* Your system administrator can [configure various aspects of the Undo/Redo features](/help/sites-administering/config-undo.md) according to the requirements for your instance.-->
