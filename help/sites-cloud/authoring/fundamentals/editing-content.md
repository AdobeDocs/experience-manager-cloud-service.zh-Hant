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

建立頁面後（新頁面或作為啟動或即時副本的一部分），您可以編輯內容以進行所需的更新。

使用可拖曳至頁面的[元件](/help/sites-cloud/authoring/features/components-console.md)（適合內容類型）來新增內容。 接著，您就可以就地編輯、移動或刪除這些項目。

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
>如果您的頁面和/或範本已適當設定，則您可以在編輯時使用[回應式版面](/help/sites-cloud/authoring/features/responsive-layout.md)。

>[!TIP]
>
>在&#x200B;**編輯**&#x200B;模式中時，內容中的連結可見，但&#x200B;**無法存取**。 如果您想使用內容中的連結來導覽，請使用[預覽模式](#previewing-pages)。

## 頁面工具欄{#page-toolbar}

頁面工具列可依頁面設定提供對適當功能的存取。

![頁面工具列](/help/sites-cloud/authoring/assets/editing-page-toolbar.png)

工具列提供許多選項的存取權。 視您目前的內容和設定而定，某些選項可能無法使用。

* **切換側面板**

   這會開啟/關閉側面板，該面板保存[資產瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser)、[元件瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)和[內容樹](/help/sites-cloud/authoring/fundamentals/environment-tools.md#content-tree)。

   ![側面板切換](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

* **頁面資訊**

   提供對[頁面資訊](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information)菜單的訪問，該菜單包括頁面詳細資訊和可以在頁面上採取的操作，包括查看和編輯頁面資訊、查看頁面屬性以及發佈/取消發佈頁面。

   ![頁面資訊按鈕](/help/sites-cloud/authoring/assets/page-information-icon.png)

* **模擬器**

   切換[模擬器工具列](/help/sites-cloud/authoring/features/responsive-layout.md#selecting-a-device-to-emulate)，該工具列用於模擬其他裝置上頁面的外觀和風格。 這會在版面模式中自動切換。

   ![模擬器按鈕](/help/sites-cloud/authoring/assets/emulator.png)

* **ContextHub**

   開啟[ContextHub](/help/sites-cloud/authoring/personalization/contexthub.md)。 僅在「預覽」模式中可用。

   ![「內容中心」按鈕](/help/sites-cloud/authoring/assets/context-hub.png)

* **頁面標題**

   這純粹是資訊。

   ![頁面標題](/help/sites-cloud/authoring/assets/page-title.png)

* **模式選擇器**

   顯示當前的[mode](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)，並允許您選擇其他模式，如編輯、佈局、時間扭曲或定位。

   ![模式選擇器按鈕](/help/sites-cloud/authoring/assets/mode-selector.png)

* **預覽**

   啟用[預覽模式](#preview-mode)。 這會以發佈時的顯示方式顯示頁面。

   ![預覽按鈕](/help/sites-cloud/authoring/assets/preview.png)

* **注釋**

   可讓您在檢閱頁面時，將[註解](/help/sites-cloud/authoring/fundamentals/annotations.md)新增至頁面。 在第一個批注之後，表徵圖將切換到指示頁面上批注數的數字。

   ![註解按鈕](/help/sites-cloud/authoring/assets/annotations.png)

### 狀態通知{#status-notification}

如果頁面是[工作流程](/help/sites-cloud/authoring/workflows/overview.md)或多個工作流程的一部分，則編輯頁面時，此資訊會顯示在螢幕頂端的通知列中。

![工作流程通知](/help/sites-cloud/authoring/assets/editing-workflow-notification.png)

>[!NOTE]
>
>狀態欄僅對具有適當權限的使用者帳戶可見。

通知會列出針對頁面執行的工作流程。 如果用戶參與當前工作流步驟，[的選項將影響工作流狀態](/help/sites-cloud/authoring/workflows/participating.md)並獲取有關工作流的詳細資訊，例如：

* **完成**  — 開啟完 **成工作項** 對話框
* **委派**  — 開啟「完 **成工作項** 目」對話
* **查看詳細資** 訊 — 開啟工 **** 作流的「詳細資訊」窗口

從通知收件匣[參與工作流程](/help/sites-cloud/authoring/workflows/participating.md)時，透過通知列完成和委派工作流程步驟的運作方式與相同。

如果頁面受多個工作流程的規範，則通知的右端會顯示工作流程數，並附上箭頭按鈕，讓您捲動工作流程。

![多個工作流通知](/help/sites-cloud/authoring/assets/editing-workflow-notification-multiple.png)

## 元件佔位符{#component-placeholder}

元件預留位置是一個指標，可在您放置元件時顯示元件的位置 — 位於目前暫留在的元件上方。

* 將新元件新增至頁面時（從元件瀏覽器拖曳）:

   ![將新元件新增至頁面時的預留位置](/help/sites-cloud/authoring/assets/editing-component-placeholder.png)

* 移動現有元件時：

   ![在頁面上移動現有元件時的預留位置](/help/sites-cloud/authoring/assets/editing-component-placeholder-existing.png)

## 插入元件{#inserting-a-component}

### 從元件瀏覽器{#inserting-a-component-from-the-components-browser}插入元件

您可以使用[元件瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)來新增元件。 [元件佔位符](#component-placeholder)顯示元件的位置：

1. 請確定您的頁面處於&#x200B;[**Edit**&#x200B;模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)。
1. 開啟[元件瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)。
1. 將所需元件拖曳至[必要位置](#component-placeholder)。
1. [](#edit-content) 編輯元件。

>[!NOTE]
>
>在行動裝置上，元件瀏覽器會填入整個畫面。 開始拖曳元件後，瀏覽器會關閉再次顯示頁面，讓您放置元件。

### 從段落系統{#inserting-a-component-from-the-paragraph-system}中插入元件

您可以使用段落系統的&#x200B;**將元件拖曳到此處**&#x200B;方塊來新增元件：

1. 請確定您的頁面處於&#x200B;[**Edit**&#x200B;模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)。
1. 從段落系統中選擇和添加新元件有兩種方式：

   * 從現有元件的工具欄或&#x200B;**將元件拖曳到此處**&#x200B;框中，選擇&#x200B;**插入元件**&#x200B;選項(+)。

      ![插入元件](/help/sites-cloud/authoring/assets/editing-insert-component.png)

   * 如果您在案頭設備上，可以按兩下&#x200B;**將元件拖曳到此處**&#x200B;框。

   * 將會開啟&#x200B;**插入新元件**&#x200B;對話框，允許您選擇所需元件：

      ![插入新元件對話框](/help/sites-cloud/authoring/assets/editing-insert-component-selection.png)

1. 選取的元件將新增至頁面底部。 [](#edit-content) 視需要編輯元件。

### 使用資產瀏覽器{#inserting-a-component-using-the-assets-browser}插入元件

您也可以從[assets瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser)拖曳資產，將新元件新增至頁面。 這會自動建立適當類型的新元件（並包含資產）。

您可以針對安裝設定此行為。 如需詳細資訊，請參閱設定段落系統，讓拖曳資產可建立元件例項。<!--This behavior can be configured for your installation. See [Configuring a Paragraph System so that Dragging an Asset Creates a Component Instance](/help/sites-developing/developing-components.md#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance) for further details.-->

若要借由拖曳上述其中一個資產類型來建立元件：

1. 請確定您的頁面處於&#x200B;[**Edit**&#x200B;模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)。
1. 開啟[資產瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser)。
1. 將所需資產拖曳至所需位置。 [元件佔位符](#component-placeholder)顯示元件的位置。

   在所需位置建立與資產類型相適用的元件，其中會包含選取的資產。

1. [](#edit-content) 視需要編輯元件。

>[!NOTE]
>
>在行動裝置上，資產瀏覽器會填滿整個畫面。 開始拖曳資產後，瀏覽器會關閉以再次顯示頁面，讓您放置資產。

如果瀏覽資產時發現您需要快速變更資產，您可以按一下資產名稱旁的編輯圖示，直接從瀏覽器啟動[資產編輯器](/help/assets/manage-digital-assets.md)。

![資產編輯按鈕](/help/sites-cloud/authoring/assets/asset-edit-button.png)

## 元件工具欄{#component-toolbar}

選取元件會開啟工具列。 這可讓您存取可在元件上執行的各種動作。

使用者可用的實際動作會視情況顯示，並非此處會說明所有動作。

![元件工具列](/help/sites-cloud/authoring/assets/editing-component-toolbar.png)

* **編輯**

   [根據元件](/help/sites-cloud/authoring/fundamentals/components.md) 類型，這可讓您 [編輯元件的內容](#edit-content)。通常會提供工具列。

   ![編輯按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-edit.png)

* **設定**

   [根據元件](/help/sites-cloud/authoring/fundamentals/components.md) 類型，這允許您編輯和配置元件的屬性。通常會開啟對話。

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

   這會開啟對話方塊，前往[新增新元件](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component-from-the-paragraph-system)。

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

   這可讓您一次選取多個元件。 在案頭設備上也可以通過&#x200B;**Control+Click**&#x200B;或&#x200B;**Command+Click**&#x200B;實現。

   ![「組」按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-group.png)

* **父級**

   這可讓您選取所選元件的父元件。

   ![父按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-parent.png)

* **配置**

   這可讓您修改所選元件的[layout](/help/sites-cloud/authoring/fundamentals/editing-content.md#edit-component-layout)。 這只會套用至選取的元件，不會為整個頁面啟用[配置模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)。

   ![版面按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-layout.png)

* **轉換為體驗片段變數**

   這可讓您從選取的元件建立新的[體驗片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)，或將其新增至現有的體驗片段。

   ![轉換為體驗片段按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-xf.png)

## 編輯內容{#edit-content}

在元件中新增和/或編輯內容有兩種方法：

* 開啟[元件對話框以進行編輯](#component-edit-dialog)。
* [從資產瀏覽器](#drag-and-drop-assets-into-component) 拖放資產，以直接新增內容。

### 元件編輯對話框{#component-edit-dialog}

您可以使用元件工具列的「編輯 (鉛筆) 」圖示， [開啟元件以編輯內容](#component-toolbar)。

確切的編輯選項取決於元件。 對於某些元件[，所有動作將僅以全螢幕模式](#edit-content-full-screen-mode)提供。 例如：

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

### 將資產拖放至元件{#drag-and-drop-assets-into-component}

對於特定元件類型（例如影像），您可以直接將資產從資產瀏覽器拖放至元件中，以更新內容。

## 以全螢幕模式編輯內容{#edit-content-full-screen-mode}

對於所有元件，可使用（並從中退出）存取全螢幕模式：

![全螢幕按鈕](/help/sites-cloud/authoring/assets/editing-full-screen.png)

例如， **Text**&#x200B;元件：

![全螢幕文字元件](/help/sites-cloud/authoring/assets/editing-text-full-screen.png)

>[!NOTE]
>
>對於某些元件，全螢幕模式比基本就地編輯器有更多可用選項。

## 移動元件{#moving-a-component}

要移動段落元件，請執行以下操作：

1. 選擇要用點選並按住或按住移動的段落。
1. 將段落拖動到新位置。 AEM表示可以將段落保存的位置。 將其放置在您想要的位置。

   ![移動元件](/help/sites-cloud/authoring/assets/editing-moving-component.png)

1. 您的段落被移動。

>[!TIP]
>
>您也可以使用[剪下並貼上](#component-toolbar)來移動元件。

## 編輯元件佈局{#edit-component-layout}

您可以選取元件的 [Layout](/help/sites-cloud/authoring/features/responsive-layout.md)****  (配置) 動作，以變更元件的配置，並節省時間，而不需離開編輯模式，而不需重複從編輯切換到配置模式來調整元件。

1. 在站點控制台的&#x200B;**編輯**&#x200B;模式下，選擇元件將顯示元件的工具欄。

   ![頁面元件的元件工具列](/help/sites-cloud/authoring/assets/editing-layout-toolbar.png)

   按一下或點選「**配置**」動作，以調整元件的配置。

   ![元件工具欄的「佈局」按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-layout.png)

1. 選取「配置」動作後：

   * 元件顯示的調整手柄大小。
   * 模擬器工具欄顯示在螢幕頂部。
   * 配置操作（而不是標準編輯操作）將顯示在元件工具欄上。

   ![佈局模式中的元件](/help/sites-cloud/authoring/assets/editing-layout-mode.png)

   您現在可以像在[layout mode](/help/sites-cloud/authoring/features/responsive-layout.md#defining-layouts-layout-mode)中一樣修改元件的佈局。

1. 進行必要的配置更改後，按一下元件操作菜單中的&#x200B;**關閉**&#x200B;按鈕，停止修改元件的配置。 元件的工具列會恢復為正常編輯狀態。

   ![頁面元件的元件工具列](/help/sites-cloud/authoring/assets/editing-layout-exit.png)

>[!TIP]
>
>「佈局」(Layout)操作的範圍僅限於所選元件。 例如，如果編輯一個元件的佈局，然後按一下另一個元件，則新選元件的標準編輯工具欄（而不是佈局工具欄）將顯示，調整大小控制滑塊和模擬器工具欄將消失。
>
>如果您需要編輯頁面的整體版面，並影響到多個元件，請切換至[版面模式](/help/sites-cloud/authoring/features/responsive-layout.md)。

## 繼承的元件{#inherited-components}

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

## 編輯頁面範本{#editing-the-page-template}

您可以輕鬆切換至範本 [編輯器](/help/sites-cloud/authoring/features/templates.md#editing-templates-template-authors) ，方法是在「頁面資訊」選單中選取 **「編輯範本**」(Edit [Template](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) )。

在「欄檢視」或「清單檢視」中選取頁面時，您可輕鬆查看該頁 [面所依據](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view)[的範本](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view)。

## 即時副本狀態 {#live-copy-status}

[即時副本狀態頁面模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)可讓您快速概述即時副本狀態，以及繼承/不繼承哪些元件：

* 綠色邊框：繼承
* 粉紅色邊框：已取消繼承

例如：

![顯示即時副本狀態的範例](/help/sites-cloud/authoring/assets/editing-live-copy-status.png)

## 添加註釋{#adding-annotations}

[](/help/sites-cloud/authoring/fundamentals/annotations.md) 注釋、審核者和其他作者，提供您內容的意見反應。它們通常用於審核和驗證目的。

## 預覽頁面{#previewing-pages}

預覽頁面有兩個選項：

* [預覽模式](#preview-mode)  — 快速就地預覽
* [檢視為已發佈](#view-as-published)  — 可在新索引標籤中開啟頁面的完整預覽

>[!TIP]
>
>* 內容中的連結是可見的，但在「編輯」模式中無法存取。
>* 如果您想使用連結來導覽，請使用其中一個預覽選項。
>* 使用[鍵盤快速鍵](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) `Ctrl-Shift-M`在預覽模式和上次選擇的模式之間切換。


>[!NOTE]
>
>已為兩個預覽選項設定WCM模式Cookie。

### 預覽模式{#preview-mode}

編輯內容時，您可以使用預覽[mode](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)預覽頁面。 此模式：

* 隱藏各種編輯機制，讓您快速檢視頁面在發佈時的顯示方式。
* 可讓您使用連結進行導覽。
* **not**&#x200B;會重新整理頁面內容嗎？

編寫時，可使用頁面編輯器右上角的圖示來使用預覽模式：

![預覽按鈕](/help/sites-cloud/authoring/assets/preview.png)

### 以已發佈狀態檢視 {#view-as-published}

從[Page Information](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information)功能表中可以使用&#x200B;**View as Published**&#x200B;選項。 這會在新索引標籤中開啟頁面，重新整理內容，並依照發佈環境中的顯示方式顯示頁面。

## 鎖定頁面{#locking-a-page}

AEM可讓您鎖定頁面，讓其他人都無法修改內容。 當您對特定頁面進行許多編輯，或需要將頁面凍結一段時間時，這個功能會很實用。

可從以下任一位置鎖定頁面：

* **** Siteconsole

   1. 選擇具有[選擇模式](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)的頁。
   1. 選取鎖定圖示。

      ![鎖定按鈕](/help/sites-cloud/authoring/assets/lock.png)

* **頁面編輯器**

   1. 選取&#x200B;**頁面資訊**&#x200B;圖示以開啟功能表。
   1. 選擇&#x200B;**鎖定頁面**&#x200B;選項。

鎖定後，控制台視圖資訊會更新，編輯鎖定符號時，工具欄中會顯示。

![鎖定頁面的範例](/help/sites-cloud/authoring/assets/editing-locked-page.png)

>[!CAUTION]
>
>模擬使用者時，可執行鎖定頁面的作業。 不過，以此方式鎖定的頁面，只能由模擬的使用者或管理員使用者解除鎖定。
>
>無法通過模擬鎖定頁面的用戶來解除鎖定頁面。
<!--
>Locking a page can be performed when [impersonating a user](/help/sites-administering/security.md#impersonating-another-user). However a page locked in this way can only then be unlocked by the user who was impersonated or by the admin user.
-->

## 解鎖頁面{#unlocking-a-page}

解鎖頁面與鎖定頁面[非常類似。 ](#locking-a-page)鎖定頁面後，鎖定選項會由解除鎖定動作取代。

「頁面資訊」功能表 **會列出** 「解除鎖定」為選項，而網站主控台中的「鎖定」圖示會以「解除鎖定」圖示 **** 取代。

![解除鎖定按鈕](/help/sites-cloud/authoring/assets/unlock.png)

>[!CAUTION]
>
>模擬使用者時，可執行鎖定頁面的作業。 不過，以此方式鎖定的頁面，只能由模擬的使用者或管理員使用者解除鎖定。
>
>無法通過模擬鎖定頁面的用戶來解除鎖定頁面。
<!--
>Locking a page can be performed when [impersonating a user](/help/sites-administering/security.md#impersonating-another-user). However a page locked in this way can only then be unlocked by the user who was impersonated or by the admin user.
-->

## 撤消和重新執行頁面編輯{#undoing-and-redoing-page-edits}

下列圖示可讓您還原或重做動作。 這些在適當時會顯示在工具列中：

![還原和重做按鈕](/help/sites-cloud/authoring/assets/redo.png)

>[!TIP]
>
>* [鍵盤快速鍵](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) `Ctrl-Z`也可用於還原頁面編輯動作。
>* 鍵盤快速鍵`Ctrl-Y`也可用於重做頁面編輯動作。


>[!NOTE]
>
>請參閱[還原和重新執行頁面編輯 — 理論](#undoing-and-redoing-page-edits-the-theory) ，以取得還原和重新執行頁面編輯時可能採取的完整詳細資訊。

## 撤消和重新執行頁面編輯 — 理論{#undoing-and-redoing-page-edits-the-theory}

AEM會儲存您執行之動作的歷史記錄，以及執行動作的順序，讓您可以依照執行動作的順序還原多個動作，並視需要重做以重新套用一或多個動作。

如果選取了內容頁面上的元素（例如文字元件），則還原和重做命令會套用至選取的項目。

撤消和重做命令的行為與其他軟體中類似。 在您決定內容時，可使用命令還原網頁的最近狀態。 例如，如果將文本段落移動到頁面上的其他位置，則可以使用撤消命令將段落移回。 如果您接著決定上一個位置較好，請使用重做命令來「還原」。

例如，您可以：

* 只要您自使用還原功能後未進行頁面編輯，就重做動作。
* 最多可還原20個編輯動作（預設設定）。
* 也可使用[鍵盤快速鍵](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)撤消和重做。

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
