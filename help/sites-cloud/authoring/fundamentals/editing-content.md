---
title: 編輯頁面內容
description: 建立頁面後，您可以編輯內容以進行所需的更新
exl-id: 8af0f621-14e8-4605-a51a-a3be21f19092
source-git-commit: 14671264f1605552b2262a3139d4005e6dd90cb5
workflow-type: tm+mt
source-wordcount: '2992'
ht-degree: 6%

---

# 編輯頁面內容{#editing-page-content}

建立頁面後（新頁面或作為啟動或即時副本的一部分），您可以編輯內容以進行所需的更新。

使用 [元件](/help/sites-cloud/authoring/features/components-console.md) （適合內容類型）拖曳至頁面上。 接著，您就可以就地編輯、移動或刪除這些項目。

>[!NOTE]
>
>您的帳戶需要適當的存取權限和權限才能編輯頁面。
>
>如果您遇到任何問題，建議您與系統管理員聯繫。
<!--
>Your account needs the [appropriate access rights](/help/sites-administering/security.md) and [permissions](/help/sites-administering/security.md#permissions) to edit pages.
-->

>[!NOTE]
>
>如果頁面和/或範本已適當設定，則您可以使用 [回應式版面](/help/sites-cloud/authoring/features/responsive-layout.md) 編輯。

>[!TIP]
>
>登入時 **編輯** 模式，則內容中的連結是可見的，但 **無法存取**. 使用 [預覽模式](#previewing-pages) 如果您想使用內容中的連結進行導覽。

## 頁面工具列 {#page-toolbar}

頁面工具列提供對適當功能的存取，視頁面設定而定。

![頁面工具列](/help/sites-cloud/authoring/assets/editing-page-toolbar.png)

工具列提供許多選項的存取權。 視您目前的內容和設定而定，某些選項可能無法使用。

* **切換側面板**

   這會開啟/關閉保持 [資產瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser), [元件瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)，和 [內容樹](/help/sites-cloud/authoring/fundamentals/environment-tools.md#content-tree).

   ![側面板切換](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

* **頁面資訊**

   提供 [頁面資訊](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) 功能表，包括頁面詳細資訊和可在頁面上採取的動作，包括檢視和編輯頁面資訊、檢視頁面屬性，以及發佈/取消發佈頁面。

   ![頁面資訊按鈕](/help/sites-cloud/authoring/assets/page-information-icon.png)

* **模擬器**

   切換 [模擬器工具列](/help/sites-cloud/authoring/features/responsive-layout.md#selecting-a-device-to-emulate)，可用來模擬其他裝置上頁面的外觀與風格。 這會在版面模式中自動切換。

   ![模擬器按鈕](/help/sites-cloud/authoring/assets/emulator.png)

* **ContextHub**

   開啟 [ContextHub](/help/sites-cloud/authoring/personalization/contexthub.md). 僅在「預覽」模式中可用。

   ![「內容中心」按鈕](/help/sites-cloud/authoring/assets/context-hub.png)

* **頁面標題**

   這純粹是資訊。

   ![頁面標題](/help/sites-cloud/authoring/assets/page-title.png)

* **模式選擇器**

   顯示當前 [模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) 和可讓您選取其他模式，例如編輯、版面、時間扭曲或鎖定目標。

   ![模式選擇器按鈕](/help/sites-cloud/authoring/assets/mode-selector.png)

* **預覽**

   啟用 [預覽模式](#preview-mode). 這會以發佈時的顯示方式顯示頁面。

   ![預覽按鈕](/help/sites-cloud/authoring/assets/preview.png)

* **注釋**

   可讓您新增 [註解](/help/sites-cloud/authoring/fundamentals/annotations.md) 檢視頁面時傳回至該頁面。 在第一個批注之後，表徵圖將切換到指示頁面上批注數的數字。

   ![註解按鈕](/help/sites-cloud/authoring/assets/annotations.png)

### 狀態通知 {#status-notification}

如果頁面是 [工作流程](/help/sites-cloud/authoring/workflows/overview.md) 或多個工作流程時，此資訊會在編輯頁面時顯示在畫面頂端的通知列中。

![工作流程通知](/help/sites-cloud/authoring/assets/editing-workflow-notification.png)

>[!NOTE]
>
>狀態欄僅對具有適當權限的使用者帳戶可見。

通知會列出針對頁面執行的工作流程。 如果使用者參與目前的工作流程步驟，則選項為 [影響工作流狀態](/help/sites-cloud/authoring/workflows/participating.md) 以及取得工作流程的詳細資訊，例如：

* **完成**  — 開啟 **完成工作項** 對話
* **委派**  — 開啟 **完成工作項** 對話
* **查看詳細資訊**  — 開啟 **詳細資料** 工作流窗口

透過通知列完成和委派工作流程步驟的運作方式與 [參與工作流程](/help/sites-cloud/authoring/workflows/participating.md) 從通知收件匣。

如果頁面受多個工作流程的規範，則通知的右端會顯示工作流程數，並附上箭頭按鈕，讓您捲動工作流程。

![多個工作流通知](/help/sites-cloud/authoring/assets/editing-workflow-notification-multiple.png)

## 元件預留位置 {#component-placeholder}

元件預留位置是一個指標，可在您放置元件時顯示元件的位置 — 位於目前暫留在的元件上方。

* 將新元件新增至頁面時（從元件瀏覽器拖曳）:

   ![將新元件新增至頁面時的預留位置](/help/sites-cloud/authoring/assets/editing-component-placeholder.png)

* 移動現有元件時：

   ![在頁面上移動現有元件時的預留位置](/help/sites-cloud/authoring/assets/editing-component-placeholder-existing.png)

## 插入元件 {#inserting-a-component}

### 從元件瀏覽器插入元件 {#inserting-a-component-from-the-components-browser}

您可以使用 [元件瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser). 此 [元件預留位置](#component-placeholder) 顯示元件的位置：

1. 確定您的頁面位於 [**編輯** 模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes).
1. 開啟 [元件瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser).
1. 將所需元件拖曳至 [必填職位](#component-placeholder).
1. [編輯](#edit-content) 元件。

>[!NOTE]
>
>在行動裝置上，元件瀏覽器會填入整個畫面。 開始拖曳元件後，瀏覽器會關閉再次顯示頁面，讓您放置元件。

### 從段落系統插入元件 {#inserting-a-component-from-the-paragraph-system}

您可以使用 **拖曳元件至此** 框：

1. 確定您的頁面位於 [**編輯** 模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes).
1. 從段落系統中選擇和添加新元件有兩種方式：

   * 選取 **插入元件** 選項(+)，可在現有元件的工具列或 **拖曳元件至此** 框。

      ![插入元件](/help/sites-cloud/authoring/assets/editing-insert-component.png)

   * 如果您位於桌上型電腦裝置上，可以連按兩下 **拖曳元件至此** 框。

   * 此 **插入新元件** 對話方塊將會開啟，供您選取所需元件：

      ![插入新元件對話框](/help/sites-cloud/authoring/assets/editing-insert-component-selection.png)

1. 選取的元件將新增至頁面底部。 [編輯](#edit-content) 元件（視需要）。

### 使用資產瀏覽器插入元件 {#inserting-a-component-using-the-assets-browser}

您也可以從 [資產瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser). 這會自動建立適當類型的新元件（並包含資產）。

您可以針對安裝設定此行為。 如需詳細資訊，請參閱設定段落系統，讓拖曳資產可建立元件例項。 <!--This behavior can be configured for your installation. See [Configuring a Paragraph System so that Dragging an Asset Creates a Component Instance](/help/sites-developing/developing-components.md#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance) for further details.-->

若要借由拖曳上述其中一個資產類型來建立元件：

1. 確定您的頁面位於 [**編輯** 模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes).
1. 開啟 [資產瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser).
1. 將所需資產拖曳至所需位置。 此 [元件預留位置](#component-placeholder) 顯示元件的位置。

   在所需位置建立與資產類型相適用的元件，其中會包含選取的資產。

1. [編輯](#edit-content) 元件（如有需要）。

>[!NOTE]
>
>在行動裝置上，資產瀏覽器會填滿整個畫面。 開始拖曳資產後，瀏覽器會關閉以再次顯示頁面，讓您放置資產。

如果瀏覽資產時發現您需要快速變更資產，可以啟動 [資產編輯器](/help/assets/manage-digital-assets.md) 按一下資產名稱旁的編輯圖示，即可直接從瀏覽器存取。

![資產編輯按鈕](/help/sites-cloud/authoring/assets/asset-edit-button.png)

## 元件工具列 {#component-toolbar}

選取元件會開啟工具列。 這可讓您存取可在元件上執行的各種動作。

使用者可用的實際動作會視情況顯示，並非此處會說明所有動作。

![元件工具列](/help/sites-cloud/authoring/assets/editing-component-toolbar.png)

* **編輯**

   [取決於元件類型](/help/sites-cloud/authoring/fundamentals/components.md) 這可讓您 [編輯元件的內容](#edit-content). 通常會提供工具列。

   ![編輯按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-edit.png)

* **設定**

   [取決於元件類型](/help/sites-cloud/authoring/fundamentals/components.md) 這可讓您編輯和設定元件的屬性。 通常會開啟對話。

   ![配置按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-configure.png)

* **複製**

   這會將元件複製到剪貼簿。 貼上動作後，原始元件將會保留。

   ![複製按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-copy.png)

* **剪下**

   這會將元件複製到剪貼簿。 貼上動作後，原始元件將會移除。

   ![剪下按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-cut.png)

* **刪除**

   這會從含有您確認的頁面中刪除元件。

   ![刪除按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-delete.png)

* **插入元件**

   這會開啟對話方塊 [新增元件](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component-from-the-paragraph-system).

   ![插入按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-insert.png)

* **貼上**

   這會將剪貼簿中的元件貼到頁面。 原始檔案是否保留，取決於您是使用複製還是剪切。

   * 您可以貼到相同的頁面或不同的頁面。
   * 貼上的項目會貼到您選取貼上動作的項目上方。
   * 只有剪貼簿上有內容時，才會顯示「貼上」動作。

   ![貼上按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-paste.png)

   >[!NOTE]
   >
   >如果您貼到剪下/復製作業前已開啟的其他頁面，則必須重新整理頁面才能查看貼上的內容。

* **群組**

   這可讓您一次選取多個元件。 在案頭裝置上，可透過 **按住Ctrl鍵並按一下** 或 **按住Command鍵並按一下**.

   ![「組」按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-group.png)

* **父級**

   這可讓您選取所選元件的父元件。

   ![父按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-parent.png)

* **配置**

   這可讓您修改 [配置](/help/sites-cloud/authoring/fundamentals/editing-content.md#edit-component-layout) 的子句。 這只會套用至選取的元件，不會啟動 [版面模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) 的URL。

   ![版面按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-layout.png)

* **轉換為體驗片段變數**

   這可讓您建立新 [體驗片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md) 從選取的元件，或將其新增至現有的體驗片段。

   ![轉換為體驗片段按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-xf.png)

## 編輯內容 {#edit-content}

在元件中新增和/或編輯內容有兩種方法：

* 開啟 [編輯元件對話方塊](#component-edit-dialog).
* [拖放資產](#drag-and-drop-assets-into-component) 從「資產」瀏覽器直接新增內容。

### 元件編輯對話方塊 {#component-edit-dialog}

您可以使用元件工具列的「編輯 (鉛筆) 」圖示， [開啟元件以編輯內容](#component-toolbar)。

確切的編輯選項取決於元件。 某些元件 [所有動作將僅可在全螢幕模式中使用](#edit-content-full-screen-mode). 例如：

* 文字元件

   ![文本元件的工具欄](/help/sites-cloud/authoring/assets/editing-text-component-toolbar.png)

* 影像元件

   ![影像元件的工具欄](/help/sites-cloud/authoring/assets/editing-image-component-toolbar.png)

   >[!NOTE]
   >
   >編輯在空白的影像元件上無法運作。
   >
   >您必須先將影像拖曳或上傳至元件，才能開始編輯影像。

* 影像元件 — 全螢幕

   [進入影像元件的全螢幕模式](#edit-content-full-screen-mode) ，可讓您有更多空間編輯影像，並顯示額外的編輯選項，例如「啟動地圖」和「重設縮放」 ********。此外，全螢幕還允許選取裁切預設集。

   ![影像元件的全螢幕模式](/help/sites-cloud/authoring/assets/editing-image-component-full-screen.png)

* 從多個基本元件構建的元件首先要求您確認需要的編輯選項集：

### 將資產拖放至元件 {#drag-and-drop-assets-into-component}

對於特定元件類型（例如影像），您可以直接將資產從資產瀏覽器拖放至元件中，以更新內容。

## 以全螢幕模式編輯內容 {#edit-content-full-screen-mode}

對於所有元件，可使用（並從中退出）存取全螢幕模式：

![全螢幕按鈕](/help/sites-cloud/authoring/assets/editing-full-screen.png)

例如， **文字** 元件：

![全螢幕文字元件](/help/sites-cloud/authoring/assets/editing-text-full-screen.png)

>[!NOTE]
>
>對於某些元件，全螢幕模式比基本就地編輯器有更多可用選項。

## 移動元件 {#moving-a-component}

要移動段落元件，請執行以下操作：

1. 選擇要用點選並按住或按住移動的段落。
1. 將段落拖動到新位置。 AEM表示可以將段落保存的位置。 將其放置在您想要的位置。

   ![移動元件](/help/sites-cloud/authoring/assets/editing-moving-component.png)

1. 您的段落被移動。

>[!TIP]
>
>您也可以使用 [剪下並貼上](#component-toolbar) 來移動元件。

## 編輯元件配置 {#edit-component-layout}

您可以選取元件的 [Layout](/help/sites-cloud/authoring/features/responsive-layout.md)****  (配置) 動作，以變更元件的配置，並節省時間，而不需離開編輯模式，而不需重複從編輯切換到配置模式來調整元件。

1. 登入時 **編輯** 在sites控制台的模式下，選擇元件會顯示元件的工具欄。

   ![頁面元件的元件工具列](/help/sites-cloud/authoring/assets/editing-layout-toolbar.png)

   按一下或點選 **版面** 動作來調整元件的版面。

   ![元件工具欄的「佈局」按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-layout.png)

1. 選取「配置」動作後：

   * 元件顯示的調整手柄大小。
   * 模擬器工具欄顯示在螢幕頂部。
   * 配置操作（而不是標準編輯操作）將顯示在元件工具欄上。

   ![佈局模式中的元件](/help/sites-cloud/authoring/assets/editing-layout-mode.png)

   您現在可以修改元件的版面，如同在 [配置模式](/help/sites-cloud/authoring/features/responsive-layout.md#defining-layouts-layout-mode).

1. 進行必要的配置變更後，按一下 **關閉** 按鈕，停止修改元件的佈局。 元件的工具列會恢復為正常編輯狀態。

   ![頁面元件的元件工具列](/help/sites-cloud/authoring/assets/editing-layout-exit.png)

>[!TIP]
>
>「佈局」(Layout)操作的範圍僅限於所選元件。 例如，如果編輯一個元件的佈局，然後按一下另一個元件，則新選元件的標準編輯工具欄（而不是佈局工具欄）將顯示，調整大小控制滑塊和模擬器工具欄將消失。
>
>如果您需要編輯頁面的整體版面，並影響到多個元件，請切換至 [配置模式](/help/sites-cloud/authoring/features/responsive-layout.md).

## 繼承的元件 {#inherited-components}

繼承是內容可從一個元件自動推送至另一個元件的機制。 繼承的元件可以是各種情況的產品，包括：

* [多網站管理](/help/sites-cloud/administering/msm/overview.md)
* [啟動](/help/sites-cloud/authoring/launches/overview.md) （根據即時副本時）。

您可以取消（然後重新啟用）繼承。 視元件而定，如果元件位於屬於即時副本或啟動的頁面上（根據即時副本），則可從元件工具列使用。

![顯示繼承關係的元件工具欄](/help/sites-cloud/authoring/assets/editing-component-toolbar-inheritance.png)

例如：

* 取消繼承

   ![取消繼承按鈕](/help/sites-cloud/authoring/assets/editing-cancel-inheritance.png)

* 重新啟用繼承（如果已取消繼承）

   ![重新啟用繼承按鈕](/help/sites-cloud/authoring/assets/editing-reenable-inheritance.png)

* Blueprint或Live Copy來源中也提供轉出動作

   ![轉出按鈕](/help/sites-cloud/authoring/assets/editing-rollout.png)

## 編輯頁面範本 {#editing-the-page-template}

您可以輕鬆切換至範本 [編輯器](/help/sites-cloud/authoring/features/templates.md#editing-templates-template-authors) ，方法是在「頁面資訊」選單中選取 **「編輯範本**」(Edit [Template](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) )。

在「欄檢視」或「清單檢視」中選取頁面時，您可輕鬆查看該頁 [面所依據](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view)[的範本](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view)。

## 即時副本狀態 {#live-copy-status}

此 [「即時副本狀態」頁面模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) 可讓您快速概述即時副本狀態，以及繼承/不繼承哪些元件：

* 綠色邊框：繼承
* 粉紅色邊框：已取消繼承

例如：

![顯示即時副本狀態的範例](/help/sites-cloud/authoring/assets/editing-live-copy-status.png)

## 新增註解 {#adding-annotations}

[註解](/help/sites-cloud/authoring/fundamentals/annotations.md) 可讓審核者和其他作者提供您內容的意見反應。 它們通常用於審核和驗證目的。

## 預覽頁面 {#previewing-pages}

預覽頁面有兩個選項：

* [預覽模式](#preview-mode)  — 快速就地預覽
* [檢視為已發佈](#view-as-published)  — 在新索引標籤中開啟頁面的完整預覽

>[!TIP]
>
>* 內容中的連結是可見的，但在「編輯」模式中無法存取。
>* 如果您想使用連結來導覽，請使用其中一個預覽選項。
>* 使用 [鍵盤快捷鍵](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) `Ctrl-Shift-M` 在預覽模式和上次選取模式之間切換。


>[!NOTE]
>
>已為兩個預覽選項設定WCM模式Cookie。

### 預覽模式 {#preview-mode}

編輯內容時，您可以使用預覽來預覽頁面 [模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes). 此模式：

* 隱藏各種編輯機制，讓您快速檢視頁面在發佈時的顯示方式。
* 可讓您使用連結進行導覽。
* 是 **not** 重新整理頁面內容。

編寫時，可使用頁面編輯器右上角的圖示來使用預覽模式：

![預覽按鈕](/help/sites-cloud/authoring/assets/preview.png)

### 以已發佈狀態檢視 {#view-as-published}

此 **檢視為已發佈** 選項 [頁面資訊](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) 功能表。 這會在新索引標籤中開啟頁面，重新整理內容，並依照發佈環境中的顯示方式顯示頁面。

## 鎖定頁面 {#locking-a-page}

AEM可讓您鎖定頁面，讓其他人都無法修改內容。 當您對特定頁面進行許多編輯，或需要將頁面凍結一段時間時，這個功能會很實用。

可從以下任一位置鎖定頁面：

* **網站** 主控台

   1. 選擇具有 [選擇模式](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
   1. 選取鎖定圖示。

      ![鎖定按鈕](/help/sites-cloud/authoring/assets/lock.png)

* **頁面編輯器**

   1. 選取 **頁面資訊** 圖示以開啟功能表。
   1. 選取 **鎖定頁面** 選項。

鎖定後，控制台視圖資訊會更新，編輯鎖定符號時，工具欄中會顯示。

![鎖定頁面的範例](/help/sites-cloud/authoring/assets/editing-locked-page.png)

>[!CAUTION]
>
>模擬使用者時，可執行鎖定頁面的作業。 不過，以此方式鎖定的頁面只能由模擬的使用者或具有管理員權限的使用者(AEM管理員IMS設定檔的成員)解除鎖定。
>
>無法通過模擬鎖定頁面的用戶來解除鎖定頁面。
<!--
>Locking a page can be performed when [impersonating a user](/help/sites-administering/security.md#impersonating-another-user). However a page locked in this way can only then be unlocked by the user who was impersonated or by the admin user.
-->

## 解鎖頁面 {#unlocking-a-page}

解鎖頁面非常類似 [鎖定頁面](#locking-a-page). 鎖定頁面後，鎖定選項會由解除鎖定動作取代。

「頁面資訊」功能表 **會列出** 「解除鎖定」為選項，而網站主控台中的「鎖定」圖示會以「解除鎖定」圖示 **** 取代。

![解除鎖定按鈕](/help/sites-cloud/authoring/assets/unlock.png)

>[!CAUTION]
>
>模擬使用者時，可執行鎖定頁面的作業。 不過，以此方式鎖定的頁面只能由模擬的使用者或具有管理員權限的使用者(AEM管理員IMS設定檔的成員)解除鎖定。
>
>無法通過模擬鎖定頁面的用戶來解除鎖定頁面。
<!--
>Locking a page can be performed when [impersonating a user](/help/sites-administering/security.md#impersonating-another-user). However a page locked in this way can only then be unlocked by the user who was impersonated or by the admin user.
-->

## 撤消和重新執行頁面編輯 {#undoing-and-redoing-page-edits}

下列圖示可讓您還原或重做動作。 這些在適當時會顯示在工具列中：

![還原和重做按鈕](/help/sites-cloud/authoring/assets/redo.png)

>[!TIP]
>
>* 此 [鍵盤快捷鍵](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) `Ctrl-Z` 也可用來還原頁面編輯動作。
>* 鍵盤快速鍵 `Ctrl-Y` 也可用於重做頁面編輯動作。


>[!NOTE]
>
>請參閱 [還原和重做頁面編輯 — 理論](#undoing-and-redoing-page-edits-the-theory) 以取得還原和重新執行頁面編輯時可能進行的完整詳細資訊。

## 還原和重做頁面編輯 — 理論 {#undoing-and-redoing-page-edits-the-theory}

AEM會儲存您所執行動作的歷史記錄，以及執行動作的順序，讓您可以依照執行動作的順序還原多個動作，並視需要重做以重新套用一或多個動作。

如果選取了內容頁面上的元素（例如文字元件），則還原和重做命令會套用至選取的項目。

撤消和重做命令的行為與其他軟體中類似。 在您決定內容時，可使用命令還原網頁的最近狀態。 例如，如果將文本段落移動到頁面上的其他位置，則可以使用撤消命令將段落移回。 如果您接著決定上一個位置較好，請使用重做命令來「還原」。

例如，您可以:

* 只要您自使用還原功能後未進行頁面編輯，就重做動作。
* 最多可還原20個編輯動作（預設設定）。
* 也使用 [鍵盤快速鍵](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) 以還原和重做。

您可以對下列類型的頁面變更使用還原和重做：

* 添加、編輯、刪除和移動段落
* 就地編輯段落內容
* 複製、剪下和貼上頁面中的項目

>[!NOTE]
>
>* 若要還原和重做檔案和影像的變更，需要特殊權限。
>* 檔案和影像的變更記錄至少會持續10小時。 但是，在此之後，變更的還是無法保證。 管理員可以更改10小時的預設時間。
>* 您的系統管理員可以根據您執行個體的需求，配置還原/重做功能的各個方面。

<!--* Your system administrator can [configure various aspects of the Undo/Redo features](/help/sites-administering/config-undo.md) according to the requirements for your instance.-->
