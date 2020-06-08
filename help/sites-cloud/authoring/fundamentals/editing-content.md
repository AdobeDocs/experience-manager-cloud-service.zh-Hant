---
title: 編輯頁面內容
description: 建立頁面後，您就可以編輯內容以進行所需的更新
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
workflow-type: tm+mt
source-wordcount: '2974'
ht-degree: 6%

---


# 編輯頁面內容{#editing-page-content}

建立您的頁面後（新增或作為啟動或即時副本的一部分），您就可以編輯內容以進行所需的更新。

使用可拖曳至 [頁面的元件](/help/sites-cloud/authoring/features/components-console.md) （適合內容類型）來新增內容。 然後，您就可以就地編輯、移動或刪除這些項目。

>[!NOTE]
>
>您的帳戶需要適當的存取權限和權限才能編輯頁面。
>
>如果您遇到任何問題，我們建議您與系統管理員聯繫。
<!--
>Your account needs the [appropriate access rights](/help/sites-administering/security.md) and [permissions](/help/sites-administering/security.md#permissions) to edit pages.
-->

>[!NOTE]
>
>如果您的頁面和／或範本已正確設定，則可在編輯時使 [用互動式版](/help/sites-cloud/authoring/features/responsive-layout.md) 面。

>[!TIP]
>
>在「編 **輯** 」模式下，您的內容中的連結是可見的，但是無 **法存取**。 如果您 [想要使用內容中的連結來導覽](#previewing-pages) ，請使用「預覽」模式。

## 頁面工具列 {#page-toolbar}

頁面工具列提供對適當功能的存取，視頁面設定而定。

![頁面工具列](/help/sites-cloud/authoring/assets/editing-page-toolbar.png)

工具列提供多種選項的存取權。 根據您目前的上下文和設定，某些選項可能無法使用。

* **切換側面板**

   這會開啟／關閉側面板，此面板會保 [存「資產瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser)」、「元 [件瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)」和「 [內容樹」](/help/sites-cloud/authoring/fundamentals/environment-tools.md#content-tree)。

   ![側面板切換](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

* **頁面資訊**

   提供對「頁面資 [訊](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) 」選單的存取，包括頁面詳細資料和可在頁面上執行的動作，包括檢視和編輯頁面資訊、檢視頁面屬性，以及發佈／取消發佈頁面。

   ![「頁面資訊」按鈕](/help/sites-cloud/authoring/assets/page-information-icon.png)

* **模擬器**

   切換模 [擬器工具列](/help/sites-cloud/authoring/features/responsive-layout.md#selecting-a-device-to-emulate)，該工具列用於模擬其他裝置上頁面的外觀和感覺。 這會在版面模式中自動切換。

   ![模擬器按鈕](/help/sites-cloud/authoring/assets/emulator.png)

* **ContextHub**

   開啟 [ContextHub](/help/sites-cloud/authoring/personalization/contexthub.md)。 僅在「預覽」模式中可用。

   ![「上下文中樞」按鈕](/help/sites-cloud/authoring/assets/context-hub.png)

* **頁面標題**

   這純粹是資訊性的。

   ![頁面標題](/help/sites-cloud/authoring/assets/page-title.png)

* **模式選擇器**

   顯示目前 [模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) ，並可讓您選取其他模式，例如編輯、版面、時間彎曲或定位。

   ![模式選擇器按鈕](/help/sites-cloud/authoring/assets/mode-selector.png)

* **預覽**

   啟用 [預覽模式](#preview-mode)。 如此會顯示發佈時的頁面。

   ![預覽按鈕](/help/sites-cloud/authoring/assets/preview.png)

* **注釋**

   可讓您在檢 [視頁面](/help/sites-cloud/authoring/fundamentals/annotations.md) 時，新增註解至頁面。 在第一個注釋之後，表徵圖將切換到一個數字，指示頁面上的注釋數。

   ![「注釋」按鈕](/help/sites-cloud/authoring/assets/annotations.png)

### 狀態通知 {#status-notification}

如果頁面是工作流程或 [多個工作流程](/help/sites-cloud/authoring/workflows/overview.md) ，則編輯頁面時，此資訊會顯示在畫面頂端的通知列中。

![工作流程通知](/help/sites-cloud/authoring/assets/editing-workflow-notification.png)

>[!NOTE]
>
>狀態列僅對具有適當權限的用戶帳戶可見。

通知會列出針對頁面執行的工作流程。 如果用戶參與當前工作流步驟，則還可 [以選擇影響工作流狀態](/help/sites-cloud/authoring/workflows/participating.md) ，並獲取有關工作流的詳細資訊，例如：

* **完成** -開啟「完 **成工作項目」對話框**
* **委派** -開啟「完 **整工作項目」對話方** 塊
* **查看詳細資訊** -開啟工作流 **的** 「詳細資訊」窗口

從「通知」收件匣參與工作流程時，透過通知列完成和委派工 [作流程步驟](/help/sites-cloud/authoring/workflows/participating.md) ，其運作方式相同。

如果頁面受多個工作流程的約束，則通知的右端會顯示工作流程數目，並附上箭頭按鈕，讓您捲動整個工作流程。

![多個工作流程通知](/help/sites-cloud/authoring/assets/editing-workflow-notification-multiple.png)

## 元件預留位置 {#component-placeholder}

元件預留位置是指示器，可顯示當您放置元件時元件的位置——位於目前暫留在元件上方。

* 將新元件新增至頁面時（從元件瀏覽器拖曳）:

   ![新增元件至頁面時的預留位置](/help/sites-cloud/authoring/assets/editing-component-placeholder.png)

* 移動現有元件時：

   ![在頁面上移動現有元件時的預留位置](/help/sites-cloud/authoring/assets/editing-component-placeholder-existing.png)

## 插入元件 {#inserting-a-component}

### 從元件瀏覽器插入元件 {#inserting-a-component-from-the-components-browser}

您可以使用元件瀏覽器來新增 [元件](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)。 元 [件預留位置](#component-placeholder) (Component placeholder)顯示元件的位置：

1. 請確定您的頁面處於「編 [**輯&#x200B;**」模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)。
1. 開啟元 [件瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)。
1. 將所需元件拖曳至 [所需位置](#component-placeholder)。
1. [編輯元件](#edit-content) 。

>[!NOTE]
>
>在行動裝置上，元件瀏覽器會填滿整個螢幕。 當您開始拖曳元件後，瀏覽器會關閉以再次顯示頁面，好讓您放置元件。

### 從段落系統中插入元件 {#inserting-a-component-from-the-paragraph-system}

可以使用段落系統的「將元件拖 **曳到此處** 」框添加新元件：

1. 請確定您的頁面處於「編 [**輯&#x200B;**」模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)。
1. 從段落系統中選擇和添加新元件有兩種方法：

   * Select the **Insert Component** option (+) from either the toolbar of an existing component or the **Drag components here** box.

      ![插入元件](/help/sites-cloud/authoring/assets/editing-insert-component.png)

   * 如果您使用桌上型裝置，可以按兩下「拖曳元件至 **此處** 」方塊。

   * The **Insert New Component** dialog will open to allow you to select your required component:

      ![「插入新元件」對話框](/help/sites-cloud/authoring/assets/editing-insert-component-selection.png)

1. 所選元件將添加到頁面底部。 [視需要編輯元件](#edit-content) 。

### 使用資產瀏覽器插入元件 {#inserting-a-component-using-the-assets-browser}

您也可以從資產瀏覽器拖曳資產，將新元件新增至 [頁面](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser)。 這會自動建立適當類型的新元件（並包含資產）。

此行為可針對您的安裝進行設定。 如需詳細資訊，請參閱設定段落系統，讓拖曳資產可建立元件例項。 <!--This behavior can be configured for your installation. See [Configuring a Paragraph System so that Dragging an Asset Creates a Component Instance](/help/sites-developing/developing-components.md#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance) for further details.-->

要通過拖動上述資產類型之一來建立元件，請執行以下操作：

1. 請確定您的頁面處於「編 [**輯&#x200B;**」模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)。
1. 開啟資 [產瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser)。
1. 將所需資產拖曳至所需位置。 元件 [預留位置](#component-placeholder) ，會顯示元件的位置。

   將在所需位置建立一個適合資產類型的元件——它將包含選定的資產。

1. [視需要編輯元件](#edit-content) 。

>[!NOTE]
>
>在行動裝置上，資產瀏覽器會填滿整個螢幕。 當您開始拖曳資產後，瀏覽器會關閉以再次顯示頁面，好讓您放置資產。

如果瀏覽資產時發現您需要快速變更資產，您可以按一下資產名稱旁的編輯圖示，直接從瀏覽器啟動資產編輯器。 <!--If when browsing the assets you find that you need to make a quick change to an asset, you can start the [asset editor](/help/assets/manage-digital-assets.md) directly from the browser by clicking the edit icon next to the asset's name.-->

![資產編輯按鈕](/help/sites-cloud/authoring/assets/asset-edit-button.png)

## 元件工具列 {#component-toolbar}

選取元件將會開啟工具列。 這可讓您存取可在元件上執行的各種動作。

使用者可使用的實際動作會視需要顯示，並非所有動作都可在此處說明。

![元件工具列](/help/sites-cloud/authoring/assets/editing-component-toolbar.png)

* **編輯**

   [根據元件類型](/help/sites-cloud/authoring/fundamentals/components.md) ，這將允許您 [編輯元件的內容](#edit-content)。 通常會提供工具列。

   ![編輯按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-edit.png)

* **設定**

   [根據元件類型](/help/sites-cloud/authoring/fundamentals/components.md) ，這將允許您編輯和配置元件的屬性。 通常會開啟對話方塊。

   ![「配置」按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-configure.png)

* **複製**

   這會將元件複製到剪貼簿。 貼上動作後，原始元件將保留。

   ![「複製」按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-copy.png)

* **剪下**

   這會將元件複製到剪貼簿。 貼上動作後，原始元件將會移除。

   ![剪下按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-cut.png)

* **刪除**

   這會從含有您確認的頁面刪除元件。

   ![刪除按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-delete.png)

* **插入元件**

   這會開啟對話方塊， [以新增元件](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component-from-the-paragraph-system)。

   ![插入按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-insert.png)

* **貼上**

   這會將元件從剪貼簿貼到頁面。 原稿是否保留，取決於您是使用復本還是剪下。

   * 您可以貼到相同的頁面或不同的頁面。
   * 貼上的項目會貼至您選取貼上動作的項目上方。
   * 只有剪貼簿上有內容時，才會顯示「平移」動作。
   ![貼上按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-paste.png)

   >[!NOTE]
   >
   >如果您貼到在剪下／復製作業之前已開啟的其他頁面，您必須重新整理頁面，才能查看貼上的內容。

* **群組**

   這可讓您一次選取多個元件。 在案頭裝置上，您也可以使用 **Control+Click** 或 **Command+Click**。

   ![「組」按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-group.png)

* **父代**

   這允許您選擇所選元件的父元件。

   ![父按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-parent.png)

* **配置**

   這允許您修改選 [定組](/help/sites-cloud/authoring/fundamentals/editing-content.md#edit-component-layout) 件的佈局。 這僅適用於選取的元件，而不會啟動整個 [頁面的](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) 「版面」模式。

   ![版面按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-layout.png)

* **轉換為體驗片段變數**

   這可讓您從選取的元件 [建立新的體驗片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md) ，或將其新增至現有的體驗片段。

   ![轉換為體驗片段按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-xf.png)

## Edit Content {#edit-content}

在元件中新增和／或編輯內容有兩種方法：

* 開啟元 [件對話方塊進行編輯](#component-edit-dialog)。
* [從資產瀏覽器拖放資產](#drag-and-drop-assets-into-component) ，以直接新增內容。

### 元件編輯對話框 {#component-edit-dialog}

您可以使用元件工具列的「編輯 (鉛筆) 」圖示， [開啟元件以編輯內容](#component-toolbar)。

確切的編輯選項將取決於元件。 對於某些元 [件，所有動作只能在全螢幕模式下使用](#edit-content-full-screen-mode)。 例如：

* 文字元件

   ![文字元件的工具列](/help/sites-cloud/authoring/assets/editing-text-component-toolbar.png)

* 影像元件

   ![影像元件的工具列](/help/sites-cloud/authoring/assets/editing-image-component-toolbar.png)

   >[!NOTE]
   >
   >編輯無法用於空的影像元件。
   >
   >您必須先將影像拖曳或上傳至元件，才能開始編輯它。

* 影像元件——全螢幕

   [進入影像元件的全螢幕模式](#edit-content-full-screen-mode) ，可讓您有更多空間編輯影像，並顯示額外的編輯選項，例如「啟動地圖」和「重設縮放」 ********。此外，全螢幕還允許選取裁切預設集。

   ![影像元件的全螢幕模式](/help/sites-cloud/authoring/assets/editing-image-component-full-screen.png)

* 從多個基本元件建構的元件會先要求您確認您要編輯的一組選項：

### 將資產拖放至元件 {#drag-and-drop-assets-into-component}

對於特定元件類型（例如影像），您可以直接將資產從資產瀏覽器拖放至元件中，以更新內容。

## 以全螢幕模式編輯內容 {#edit-content-full-screen-mode}

對於所有元件，全屏模式可以通過（並退出）訪問：

![全螢幕按鈕](/help/sites-cloud/authoring/assets/editing-full-screen.png)

例如， **Text元件** :

![全螢幕文字元件](/help/sites-cloud/authoring/assets/editing-text-full-screen.png)

>[!NOTE]
>
>對於某些元件，全螢幕模式會比基本就地編輯器有更多可用的選項。

## 移動元件 {#moving-a-component}

要移動段落元件，請執行以下操作：

1. 選擇要使用點選並按住或按一下並按住移動的段落。
1. 將段落拖曳至新位置。 AEM會指出可將段落存放在何處。 將它拖放至您所要的位置。

   ![移動元件](/help/sites-cloud/authoring/assets/editing-moving-component.png)

1. 您的段落會被移動。

>[!TIP]
>
>也可以使用「剪 [下並貼上](#component-toolbar) 」(Cut and Paste)移動元件。

## 編輯元件配置 {#edit-component-layout}

您可以選取元件的 [Layout](/help/sites-cloud/authoring/features/responsive-layout.md)****  (配置) 動作，以變更元件的配置，並節省時間，而不需離開編輯模式，而不需重複從編輯切換到配置模式來調整元件。

1. 在站點控 **制台的** 「編輯」模式下，選擇元件會顯示元件的工具欄。

   ![頁面元件的元件工具列](/help/sites-cloud/authoring/assets/editing-layout-toolbar.png)

   按一下或點選「 **版面** 」動作，以調整元件的版面。

   ![元件工具欄的「佈局」按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-layout.png)

1. 選取「版面」動作後：

   * 元件顯示的調整大小控制點。
   * 模擬器工具欄顯示在螢幕頂部。
   * 元件工具列上會顯示版面動作，而非標準編輯動作。
   ![版面模式中的元件](/help/sites-cloud/authoring/assets/editing-layout-mode.png)

   您現在可以像在版面模式中一樣修改元件的 [版面](/help/sites-cloud/authoring/features/responsive-layout.md#defining-layouts-layout-mode)。

1. 在進行必要的版面變更後，按一下元件動作選單中的 **Close** （關閉）按鈕，以停止修改元件的版面。 元件的工具欄返回其正常編輯狀態。

   ![頁面元件的元件工具列](/help/sites-cloud/authoring/assets/editing-layout-exit.png)

>[!TIP]
>
>「佈局」(Layout)操作的範圍僅限於所選元件。 例如，如果編輯某個元件的佈局，然後按一下另一個元件，則新選元件將顯示標準編輯工具欄（而非佈局工具欄），並且調整控制滑塊大小和模擬器工具欄將消失。
>
>如果您需要編輯頁面的整體版面配置，並影響多個元件，請切換至版 [面模式](/help/sites-cloud/authoring/features/responsive-layout.md)。

## 繼承的元件 {#inherited-components}

繼承是一種機制，可自動將內容從一個元件推送到另一個元件。 繼承的元件可以是各種情況的產品，包括：

* 多網站管理 <!--[Multi site management](/help/sites-administering/msm.md)-->
* [啟動](/help/sites-cloud/authoring/launches/overview.md) （根據即時副本）。

您可以取消（然後重新啟用）繼承。 視元件而定，如果元件位於即時副本或啟動的頁面上（根據即時副本），則可從元件工具列取得此功能。

![顯示繼承關係的元件工具欄](/help/sites-cloud/authoring/assets/editing-component-toolbar-inheritance.png)

例如：

* 取消繼承

   ![取消繼承按鈕](/help/sites-cloud/authoring/assets/editing-cancel-inheritance.png)

* 重新啟用繼承（如果繼承已取消）

   ![重新啟用繼承按鈕](/help/sites-cloud/authoring/assets/editing-reenable-inheritance.png)

* Blueprint或即時副本來源中也提供轉出動作

   ![轉出按鈕](/help/sites-cloud/authoring/assets/editing-rollout.png)

## 編輯頁面範本 {#editing-the-page-template}

您可以輕鬆切換至範本 [編輯器](/help/sites-cloud/authoring/features/templates.md#editing-templates-template-authors) ，方法是在「頁面資訊」選單中選取 **「編輯範本**」(Edit [Template](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) )。

在「欄檢視」或「清單檢視」中選取頁面時，您可輕鬆查看該頁 [面所依據](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view)[的範本](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view)。

## 即時副本狀態 {#live-copy-status}

「即 [時副本狀態」頁面模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) ，可讓您快速概述即時副本狀態，以及哪些元件已繼承／未繼承：

* 綠色邊框： 繼承
* 粉色邊框： 繼承已取消

例如：

![顯示即時副本狀態的範例](/help/sites-cloud/authoring/assets/editing-live-copy-status.png)

## 添加註釋 {#adding-annotations}

[註解](/help/sites-cloud/authoring/fundamentals/annotations.md) ，可讓審核者和其他作者提供您內容的意見回應。 它們通常用於審閱和驗證目的。

## 預覽頁面 {#previewing-pages}

預覽頁面有兩個選項：

* [預覽模式](#preview-mode) -快速就地預覽
* [檢視為已發佈](#view-as-published) -在新標籤中開啟頁面的完整預覽

>[!TIP]
>
>* 內容中的連結是可見的，但在「編輯」模式中無法存取。
>* 如果您想使用連結進行導覽，請使用其中一個預覽選項。
>* 使用鍵 [盤快速鍵](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)`Ctrl-Shift-M` ，在預覽和上次選取的模式之間切換。


>[!NOTE]
>
>WCM模式Cookie已針對兩個預覽選項設定。

### 預覽模式 {#preview-mode}

在編輯內容時，您可以使用預覽模式來預覽 [頁面](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)。 此模式：

* 隱藏各種編輯機制，讓您快速檢視頁面在發佈時的顯示方式。
* 可讓您使用連結進行導覽。
* 不 **會重新整** 理頁面內容。

編寫時，預覽模式可使用頁面編輯器右上角的表徵圖：

![預覽按鈕](/help/sites-cloud/authoring/assets/preview.png)

### 以已發佈狀態檢視 {#view-as-published}

「頁 **面資訊」功能表中** ，提供「檢視為已發 [布」選項](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) 。 如此會在新標籤中開啟頁面，重新整理內容，並完全顯示頁面在發佈環境中的顯示效果。

## 鎖定頁面 {#locking-a-page}

AEM可讓您鎖定頁面，讓其他人無法修改內容。 當您對特定頁面進行大量編輯或需要將頁面凍結一段時間時，這項功能會很有用。

頁面可從以下任一位置鎖定：

* **Sites** Console

   1. 選擇具有選擇模 [式的頁面](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)。
   1. 選擇鎖定表徵圖。

      ![鎖定按鈕](/help/sites-cloud/authoring/assets/lock.png)

* **頁面編輯器**

   1. 選取「頁 **面資訊** 」圖示以開啟功能表。
   1. Select the **Lock Page** option.

鎖定後，控制台視圖資訊將更新，編輯鎖定符號時，工具欄中將顯示該資訊。

![鎖定頁面的範例](/help/sites-cloud/authoring/assets/editing-locked-page.png)

>[!CAUTION]
>
>在模擬使用者時可以執行鎖定頁面。 不過，以此方式鎖定的頁面只能由模擬或管理員使用者解除鎖定。
>
>無法模擬鎖定頁面的使用者來解除鎖定頁面。
<!--
>Locking a page can be performed when [impersonating a user](/help/sites-administering/security.md#impersonating-another-user). However a page locked in this way can only then be unlocked by the user who was impersonated or by the admin user.
-->

## 解除鎖定頁面 {#unlocking-a-page}

解除鎖定頁面與鎖定頁 [面非常相似](#locking-a-page)。 鎖定頁面後，鎖定選項將被解鎖操作替換。

「頁面資訊」功能表 **會列出** 「解除鎖定」為選項，而網站主控台中的「鎖定」圖示會以「解除鎖定」圖示 **** 取代。

![解除鎖定按鈕](/help/sites-cloud/authoring/assets/unlock.png)

>[!CAUTION]
>
>在模擬使用者時可以執行鎖定頁面。 不過，以此方式鎖定的頁面只能由模擬或管理員使用者解除鎖定。
>
>無法模擬鎖定頁面的使用者來解除鎖定頁面。
<!--
>Locking a page can be performed when [impersonating a user](/help/sites-administering/security.md#impersonating-another-user). However a page locked in this way can only then be unlocked by the user who was impersonated or by the admin user.
-->

## 復原和重做頁面編輯 {#undoing-and-redoing-page-edits}

下列圖示可讓您還原或重做動作。 如果適用，這些項目會顯示在工具列中：

![「還原」和「重做」按鈕](/help/sites-cloud/authoring/assets/redo.png)

>[!TIP]
>
>* 也可 [以使用鍵](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)`Ctrl-Z` 盤快速鍵來還原頁面編輯動作。
>* 鍵盤快速鍵 `Ctrl-Y` 也可用於重做頁面編輯操作。


>[!NOTE]
>
>如需 [](#undoing-and-redoing-page-edits-the-theory) 復原和重做頁面編輯時可能做到的完整詳細資訊，請參閱復原和重做頁面編輯——理論。

## 還原和重做頁面編輯——理論 {#undoing-and-redoing-page-edits-the-theory}

AEM會儲存您執行之動作的記錄和執行動作的順序，如此您就可以依執行動作的順序還原多個動作，並視需要重做以重新套用一或多個動作。

如果選取內容頁面上的元素（例如文字元件），則還原和重做命令會套用至選取的項目。

撤消命令和重做命令的行為與其他軟體中類似。 在您決定內容時，使用命令來還原網頁的最近狀態。 例如，如果將文本段落移動到頁面上的不同位置，則可以使用撤消命令將段落移回。 如果您接著決定先前的位置較佳，請使用redo命令來「復原」。

例如，您可以：

* 只要您自使用還原後未進行頁面編輯，就可重做動作。
* 最多可還原20個編輯動作（預設設定）。
* 此外，您也可 [以使用鍵盤快速鍵](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) ，來還原和重做。

您可以對下列類型的頁面變更使用還原和重做：

* 新增、編輯、移除和移動段落
* 就地編輯段落內容
* 在頁面中複製、剪下和貼上項目

>[!NOTE]
>
>* 還原和重做檔案和影像的變更需要特殊權限。
>* 檔案和影像的變更記錄至少會持續10小時。 但是，在此之後，不保證會取消變更。 您的管理員可以變更預設時間10小時。
>* 系統管理員可以根據實例的要求配置「撤消／重做」功能的各個方面。

<!--* Your system administrator can [configure various aspects of the Undo/Redo features](/help/sites-administering/config-undo.md) according to the requirements for your instance.-->
