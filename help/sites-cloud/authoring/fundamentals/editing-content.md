---
title: 編輯頁面內容
description: 建立頁面後，您可以編輯內容以進行所需的更新
exl-id: 8af0f621-14e8-4605-a51a-a3be21f19092
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '2973'
ht-degree: 6%

---


# 編輯頁面內容{#editing-page-content}

建立頁面後（新頁面或作為啟動項或即時副本的一部分），您可以編輯內容以進行所需的更新。

內容新增方式： [元件](/help/sites-cloud/authoring/features/components-console.md) （適用於內容型別）可拖曳至頁面上的物件。 接著，您就可以就地編輯、移動或刪除這些專案。

>[!NOTE]
>
>您的帳戶需要適當的存取許可權才能編輯頁面。
>
>如果您遇到任何問題，我們建議您連絡系統管理員。
<!--
>Your account needs the [appropriate access rights](/help/sites-administering/security.md) and [permissions](/help/sites-administering/security.md#permissions) to edit pages.
-->

>[!NOTE]
>
>如果您的頁面和/或範本已正確設定，則您可以使用 [回應式版面](/help/sites-cloud/authoring/features/responsive-layout.md) 編輯時。

>[!TIP]
>
>當在 **編輯** 模式，會顯示內容中的連結，但 **無法存取**. 使用 [預覽模式](#previewing-pages) 如果您想使用內容中的連結進行導覽。

{{edge-delivery-authoring}}

## 頁面工具列 {#page-toolbar}

根據頁面設定，頁面工具列會提供適當功能的存取權。

![頁面工具列](/help/sites-cloud/authoring/assets/editing-page-toolbar.png)

工具列提供許多選項的存取權。 根據您目前的內容和組態，某些選項可能無法使用。

* **切換側面板**

  這將會開啟/關閉側面板，側面板會保留 [資產瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser)， [元件瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)、和 [內容樹狀結構](/help/sites-cloud/authoring/fundamentals/environment-tools.md#content-tree).

  ![側面板切換](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

* **頁面資訊**

  提供對的存取 [頁面資訊](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) 功能表包含頁面詳細資訊以及可在頁面上採取的動作，包括檢視和編輯頁面資訊、檢視頁面屬性以及發佈/取消發佈頁面。

  ![頁面資訊按鈕](/help/sites-cloud/authoring/assets/page-information-icon.png)

* **模擬器**

  切換 [模擬器工具列](/help/sites-cloud/authoring/features/responsive-layout.md#selecting-a-device-to-emulate)，用來模擬頁面在其他裝置上的外觀。 這會在版面模式中自動切換。

  ![「模擬器」按鈕](/help/sites-cloud/authoring/assets/emulator.png)

* **ContextHub**

  開啟 [ContextHub](/help/sites-cloud/authoring/personalization/contexthub.md). 僅適用於「預覽」模式。

  ![「內容中心」按鈕](/help/sites-cloud/authoring/assets/context-hub.png)

* **頁面標題**

  這僅供參考。

  ![頁面標題](/help/sites-cloud/authoring/assets/page-title.png)

* **模式選擇器**

  顯示目前的 [模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) 並可讓您選取其他模式，例如編輯、版面、時間扭曲或定位。

  ![模式選取器按鈕](/help/sites-cloud/authoring/assets/mode-selector.png)

* **預覽**

  啟用 [預覽模式](#preview-mode). 這會顯示發佈時所顯示的頁面。

  ![預覽按鈕](/help/sites-cloud/authoring/assets/preview.png)

* **注釋**

  讓您新增 [註解](/help/sites-cloud/authoring/fundamentals/annotations.md) 在檢閱頁面時移至頁面。 在第一個註解後，圖示會切換為指示頁面上註解數量的數字。

  ![註解按鈕](/help/sites-cloud/authoring/assets/annotations.png)

### 狀態通知 {#status-notification}

如果頁面是的一部分 [工作流程](/help/sites-cloud/authoring/workflows/overview.md) 或多個工作流程時，此資訊會在編輯頁面時顯示在畫面頂端的通知列中。

![工作流程通知](/help/sites-cloud/authoring/assets/editing-workflow-notification.png)

>[!NOTE]
>
>狀態列只對具有適當許可權的使用者帳戶可見。

通知會列出針對頁面執行的工作流程。 如果使用者涉及目前工作流程步驟，則選項為 [影響工作流程狀態](/help/sites-cloud/authoring/workflows/participating.md) 並取得更多工作流程的相關資訊，例如：

* **完成**  — 開啟 **完成工作專案** 對話方塊
* **委派**  — 開啟 **完成工作專案** 對話方塊
* **檢視詳細資料**  — 開啟 **詳細資料** 工作流程視窗

透過通知列完成及委派工作流程步驟的運作方式 [參與工作流程](/help/sites-cloud/authoring/workflows/participating.md) 從「通知」收件匣。

如果頁面受限於多個工作流程，則在通知的右端會顯示工作流程數量，並附上箭頭按鈕，讓您捲動瀏覽工作流程。

![多個工作流程通知](/help/sites-cloud/authoring/assets/editing-workflow-notification-multiple.png)

## 元件預留位置 {#component-placeholder}

元件預留位置是一個指示器，可顯示將元件放置於何處 — 位於目前暫留的元件上方。

* 將新元件新增至頁面時（從元件瀏覽器拖曳）：

  ![將新元件新增至頁面時的預留位置](/help/sites-cloud/authoring/assets/editing-component-placeholder.png)

* 移動現有元件時：

  ![在頁面上移動現有元件時的預留位置](/help/sites-cloud/authoring/assets/editing-component-placeholder-existing.png)

## 插入元件 {#inserting-a-component}

### 使用元件瀏覽器插入元件 {#inserting-a-component-from-the-components-browser}

您可以使用 [元件瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser). 此 [元件預留位置](#component-placeholder) 顯示元件的放置位置：

1. 確定您的頁面位於 [**編輯** 模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes).
1. 開啟 [元件瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser).
1. 將所需的元件拖曳至 [所需位置](#component-placeholder).
1. [編輯](#edit-content) 元件。

>[!NOTE]
>
>在行動裝置上，元件瀏覽器會填滿整個畫面。 開始拖曳元件後，瀏覽器將關閉並再次顯示頁面，以便您放置元件。

### 使用段落系統插入元件 {#inserting-a-component-from-the-paragraph-system}

您可以使用 **將元件拖曳到這裡** 段落系統的方塊：

1. 確定您的頁面位於 [**編輯** 模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes).
1. 有兩種方式可以從段落系統選取和新增元件：

   * 選取 **插入元件** 選項(+) (位於現有元件的工具列或 **將元件拖曳到這裡** 方塊。

     ![插入元件](/help/sites-cloud/authoring/assets/editing-insert-component.png)

   * 如果您使用桌上型裝置，可以按兩下 **將元件拖曳到這裡** 方塊。

   * 此 **插入新元件** 對話方塊會開啟，讓您選取所需的元件：

     ![插入新元件對話方塊](/help/sites-cloud/authoring/assets/editing-insert-component-selection.png)

1. 選取的元件會新增至頁面底部。 [編輯](#edit-content) 元件視需要。

### 使用「資產瀏覽器」插入元件 {#inserting-a-component-using-the-assets-browser}

您也可以拖曳以下專案的資產，將新元件新增至頁面： [資產瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser). 這會自動建立適當型別的元件（並包含資產）。

您可針對您的安裝設定此行為。 如需詳細資訊，請參閱設定段落系統好讓拖曳資產建立元件例項。 <!--This behavior can be configured for your installation. See [Configuring a Paragraph System so that Dragging an Asset Creates a Component Instance](/help/sites-developing/developing-components.md#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance) for further details.-->

若要拖曳上述任一資產型別來建立元件：

1. 確定您的頁面位於 [**編輯** 模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes).
1. 開啟 [資產瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser).
1. 將所需的資產拖曳至所需的位置。 此 [元件預留位置](#component-placeholder) 顯示元件的放置位置。

   適合資產型別的元件會在所需位置建立，其中包含所選資產。

1. [編輯](#edit-content) 元件（若有需要）。

>[!NOTE]
>
>在行動裝置上，資產瀏覽器會填滿整個畫面。 開始拖曳資產後，瀏覽器將關閉並再次顯示頁面，以便您放置資產。

如果您在瀏覽資產時發現需要對資產進行快速變更，可以開始 [資產編輯器](/help/assets/manage-digital-assets.md) 直接從瀏覽器按一下資產名稱旁的編輯圖示。

![資產編輯按鈕](/help/sites-cloud/authoring/assets/asset-edit-button.png)

## 元件工具列 {#component-toolbar}

選取元件會開啟工具列。 這可讓您存取可在元件上執行的各種動作。

使用者可用的實際動作會視情況顯示，並非所有動作皆可在此處說明。

![元件工具列](/help/sites-cloud/authoring/assets/editing-component-toolbar.png)

* **編輯**

  [取決於元件型別](/help/sites-cloud/authoring/fundamentals/components.md)，這可讓您 [編輯元件的內容](#edit-content). 通常會提供工具列。

  ![編輯按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-edit.png)

* **設定**

  [取決於元件型別](/help/sites-cloud/authoring/fundamentals/components.md)，即可編輯及設定元件的屬性。 通常會開啟一個對話方塊。

  ![設定按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-configure.png)

* **複製**

  這會將元件複製到剪貼簿。 貼上動作後，原始元件仍會保留。

  ![複製按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-copy.png)

* **剪下**

  這會將元件複製到剪貼簿。 貼上動作後，會移除原始元件。

  ![剪下按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-cut.png)

* **刪除**

  這將會從含有您確認的頁面中刪除元件。

  ![刪除按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-delete.png)

* **插入元件**

  這將開啟對話方塊，以 [新增元件](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component-from-the-paragraph-system).

  ![插入按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-insert.png)

* **貼上**

  這會將元件從剪貼簿貼到頁面上。 原始物件是否保留，取決於您是使用複製還是剪下。

   * 您可以貼至相同頁面或不同頁面。
   * 貼上的專案會貼在您選取貼上動作的專案上方。
   * 唯有剪貼簿上有內容時，才會顯示「貼上」動作。

  ![貼上按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-paste.png)

  >[!NOTE]
  >
  >如果您在剪下/復製作業前將頁面貼到已開啟的其他頁面，則必須重新整理頁面以檢視貼上的內容。

* **群組**

  這可讓您一次選取多個元件。 桌上型電腦裝置也可以透過以下步驟達到相同目的： **Control+按一下** 或 **Command+按一下**.

  ![群組按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-group.png)

* **父級**

  這可讓您選取所選元件的父元件。

  ![父按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-parent.png)

* **版面配置**

  這可讓您修改 [版面](/help/sites-cloud/authoring/fundamentals/editing-content.md#edit-component-layout) 所選元件的ID。 這僅適用於所選的元件，且不會啟動 [版面模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) 整個頁面。

  ![「配置」按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-layout.png)

* **轉換為體驗片段變數**

  這可讓您建立 [體驗片段](/help/sites-cloud/authoring/fundamentals/experience-fragments.md) 或是將其新增到現有的體驗片段中。

  ![「轉換為體驗片段」按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-xf.png)

## 編輯內容 {#edit-content}

在元件中新增及/或編輯內容的方法有兩種：

* 開啟 [用於編輯的元件對話方塊](#component-edit-dialog).
* [拖放資產](#drag-and-drop-assets-into-component) 以直接新增內容。

### 元件編輯對話方塊 {#component-edit-dialog}

您可以使用元件工具列的「編輯 (鉛筆) 」圖示， [開啟元件以編輯內容](#component-toolbar)。

確切的編輯選項取決於元件。 針對某些元件 [所有動作僅可在全熒幕模式中使用](#edit-content-full-screen-mode). 例如：

* 文字元件

  ![文字元件的工具列](/help/sites-cloud/authoring/assets/editing-text-component-toolbar.png)

* 影像元件

  ![影像元件的工具列](/help/sites-cloud/authoring/assets/editing-image-component-toolbar.png)

  >[!NOTE]
  >
  >無法編輯空白的影像元件。
  >
  >您必須先將影像拖曳或上傳至元件，才能開始編輯。

* 影像元件 — 全熒幕

  [進入全熒幕模式](#edit-content-full-screen-mode) 針對影像元件，可讓您有更多空間編輯影像，並顯示額外的編輯選項，例如 **啟動地圖** 和 **重設縮放**. 此外，全螢幕還允許選取裁切預設集。

  ![影像元件的全熒幕模式](/help/sites-cloud/authoring/assets/editing-image-component-full-screen.png)

* 由多個基本元件所建構的元件會先要求您確認所要的編輯選項集：

### 將資產拖放至元件中 {#drag-and-drop-assets-into-component}

對於特定元件型別（例如影像），您可以從資產瀏覽器直接將資產拖放至元件以更新內容。

## 以全熒幕模式編輯內容 {#edit-content-full-screen-mode}

對於所有元件，可使用（和退出）存取全熒幕模式：

![全熒幕按鈕](/help/sites-cloud/authoring/assets/editing-full-screen.png)

例如， **文字** 元件：

![全熒幕中的文字元件](/help/sites-cloud/authoring/assets/editing-text-full-screen.png)

>[!NOTE]
>
>對於某些元件，全熒幕模式比基本就地編輯器有更多可用選項。

## 移動元件 {#moving-a-component}

若要移動段落元件：

1. 使用點選並按住或點選並按住來選取要移動的段落。
1. 將段落拖曳到新位置。 AEM會指出段落可以儲存的位置。 將其拖曳至所需位置。

   ![移動元件](/help/sites-cloud/authoring/assets/editing-moving-component.png)

1. 此時會移動您的段落。

>[!TIP]
>
>您也可以使用 [剪下並貼上](#component-toolbar) 以移動元件。

## 編輯元件配置 {#edit-component-layout}

您可以選取元件的 [Layout](/help/sites-cloud/authoring/features/responsive-layout.md)****  (配置) 動作，以變更元件的配置，並節省時間，而不需離開編輯模式，而不需重複從編輯切換到配置模式來調整元件。

1. 當在 **編輯** 在Sites Console模式中，選取元件會顯示元件的工具列。

   ![頁面元件的元件工具列](/help/sites-cloud/authoring/assets/editing-layout-toolbar.png)

   選取 **版面** 調整元件版面的動作。

   ![元件工具列的「配置」按鈕](/help/sites-cloud/authoring/assets/editing-component-toolbar-layout.png)

1. 選取「配置」動作後：

   * 元件顯示的調整大小控點。
   * 模擬器工具列會顯示在畫面頂端。
   * 元件工具列上會顯示「配置」動作，而非標準編輯動作。

   ![配置模式中的元件](/help/sites-cloud/authoring/assets/editing-layout-mode.png)

   您現在可以修改元件的版面，就像在中一樣 [佈局模式](/help/sites-cloud/authoring/features/responsive-layout.md#defining-layouts-layout-mode).

1. 進行必要的版面變更後，按一下 **關閉** 按鈕來停止修改元件的版面。 元件的工具列會回到其正常的編輯狀態。

   ![頁面元件的元件工具列](/help/sites-cloud/authoring/assets/editing-layout-exit.png)

>[!TIP]
>
>「配置」動作僅限於選定元件的範圍。 例如，如果您正在編輯一個元件的版面，然後按一下另一個元件，則會為新選取的元件顯示標準編輯工具列（而非版面工具列），而調整大小操作框和模擬器工具列會消失。
>
>如果您需要編輯頁面的整體版面配置，並影響多個元件，請切換至 [佈局模式](/help/sites-cloud/authoring/features/responsive-layout.md).

## 繼承元件 {#inherited-components}

繼承是可自動將內容從一個元件推送到另一個元件的機制。 繼承的元件可能是各種情況的產物，包括：

* [多網站管理](/help/sites-cloud/administering/msm/overview.md)
* [啟動](/help/sites-cloud/authoring/launches/overview.md) （當以即時副本為基礎時）。

您可以取消（然後重新啟用）繼承。 根據元件的不同，如果元件位於即時副本或啟動的一部分（根據即時副本）頁面上，則可從元件工具列執行此操作。

![顯示繼承關係的元件工具列](/help/sites-cloud/authoring/assets/editing-component-toolbar-inheritance.png)

例如：

* 取消繼承

  ![取消繼承按鈕](/help/sites-cloud/authoring/assets/editing-cancel-inheritance.png)

* 重新啟用繼承（如果繼承已取消）

  ![「重新啟用繼承」按鈕](/help/sites-cloud/authoring/assets/editing-reenable-inheritance.png)

* 「轉出」動作也適用於Blueprint或即時副本來源

  ![轉出按鈕](/help/sites-cloud/authoring/assets/editing-rollout.png)

## 編輯頁面範本 {#editing-the-page-template}

您可以輕鬆切換至範本 [編輯器](/help/sites-cloud/authoring/features/templates.md#editing-templates-template-authors) ，方法是在「頁面資訊」選單中選取 **「編輯範本**」(Edit [Template](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) )。

在「欄檢視」或「清單檢視」中選取頁面時，您可輕鬆查看該頁 [面所依據](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view)[的範本](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view)。

## 即時副本狀態 {#live-copy-status}

此 [即時副本狀態頁面模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) 可讓您快速概略瞭解即時副本狀態以及不會繼承哪些元件：

* 綠色邊框：繼承
* 粉紅色邊框：繼承已取消

例如：

![顯示的即時副本狀態範例](/help/sites-cloud/authoring/assets/editing-live-copy-status.png)

## 新增註解 {#adding-annotations}

[註解](/help/sites-cloud/authoring/fundamentals/annotations.md) 允許檢閱者和其他作者針對您的內容提供意見回饋。 它們通常用於稽核和驗證目的。

## 預覽頁面 {#previewing-pages}

預覽頁面有兩個選項：

* [預覽模式](#preview-mode)  — 快速就地預覽
* [以發佈的形式檢視](#view-as-published)  — 在新標籤中開啟頁面的完整預覽

>[!TIP]
>
>* 內容中的連結可見，但在編輯模式中無法存取。
>* 如果您想要使用連結來導覽，請使用任一預覽選項。
>* 使用 [鍵盤快速鍵](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) `Ctrl-Shift-M` 在預覽和上次選取的模式之間切換。

>[!NOTE]
>
>這兩個預覽選項都會設定WCM模式Cookie。

### 預覽模式 {#preview-mode}

編輯內容時，您可以使用預覽來預覽頁面 [模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes). 此模式：

* 隱藏各種編輯機制，讓您快速檢視頁面在發佈時的顯示方式。
* 可讓您使用連結來導覽。
* 會 **非** 重新整理頁面內容。

製作時，使用頁面編輯器右上角的圖示即可使用預覽模式：

![預覽按鈕](/help/sites-cloud/authoring/assets/preview.png)

### 以已發佈狀態檢視 {#view-as-published}

此 **以發佈的形式檢視** 選項可從以下網址取得： [頁面資訊](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) 功能表。 這會在新索引標籤中開啟頁面、重新整理內容，並完全依照頁面在發佈環境中的顯示方式顯示頁面。

## 鎖定頁面 {#locking-a-page}

AEM可讓您鎖定頁面，不讓其他人編輯內容。 當您對某個特定頁面進行大量編輯，或需要凍結頁面一段時間時，此鎖定功能會很有用。

您可以透過下列任一方式鎖定頁面：

* **網站** 主控台

   1. 選擇頁面 [選擇模式](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
   1. 選取鎖定圖示。

      ![「鎖定」按鈕](/help/sites-cloud/authoring/assets/lock.png)

* **頁面編輯器**

   1. 選取 **頁面資訊** 圖示以開啟功能表。
   1. 選取 **鎖定頁面** 選項。

鎖定後，主控台檢視資訊會更新；編輯時，工具列會顯示鎖定符號。

![鎖定頁面的範例](/help/sites-cloud/authoring/assets/editing-locked-page.png)

>[!CAUTION]
>
>模擬使用者身份時可以執行鎖定頁面。 但是以這種方式鎖定的頁面只能由（客戶）使用被模擬的使用者來解鎖。
>
>無法透過模擬鎖定頁面的使用者來解鎖頁面。
>
>如果鎖定頁面的使用者無法解鎖頁面，請聯絡客戶支援評估移除鎖定的選項。

## 解鎖頁面 {#unlocking-a-page}

解鎖頁面的方法非常類似於 [鎖定頁面](#locking-a-page). 鎖定頁面後，鎖定選項會由解鎖動作取代。

「頁面資訊」功能表 **會列出** 「解除鎖定」為選項，而網站主控台中的「鎖定」圖示會以「解除鎖定」圖示 **** 取代。

![解鎖按鈕](/help/sites-cloud/authoring/assets/unlock.png)

>[!CAUTION]
>
>模擬使用者身份時可以執行鎖定頁面。 但是以這種方式鎖定的頁面只能由（客戶）使用被模擬的使用者解除鎖定。
>
>無法透過模擬鎖定頁面的使用者來解鎖頁面。
>
>如果鎖定頁面的使用者無法解鎖頁面，請聯絡客戶支援評估移除鎖定的選項。

<!--
>[!CAUTION]
>
>Locking a page can be performed when impersonating a user. However a page locked in this way can only then be unlocked by the user who was impersonated, or by a user with admin rights (a member of AEM Administrator IMS profile).
>
>Pages cannot be unlocked by impersonating the user who locked the page.
-->

<!--
>Locking a page can be performed when [impersonating a user](/help/sites-administering/security.md#impersonating-another-user). However a page locked in this way can only then be unlocked by the user who was impersonated or by the admin user.
-->

## 復原和重做頁面編輯 {#undoing-and-redoing-page-edits}

下列圖示可讓您還原或重做動作。 這些會在適當時顯示在工具列中：

![「復原」和「重做」按鈕](/help/sites-cloud/authoring/assets/redo.png)

>[!TIP]
>
>* 此 [鍵盤快速鍵](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) `Ctrl-Z` 也可用來還原頁面編輯動作。
>* 鍵盤快速鍵 `Ctrl-Y` 也可用來重做頁面編輯動作。

>[!NOTE]
>
>另請參閱 [還原和重做頁面編輯 — 理論](#undoing-and-redoing-page-edits-the-theory) 以取得復原和重做頁面編輯時可行功能的完整細節。

## 還原和重做頁面編輯 — 理論 {#undoing-and-redoing-page-edits-the-theory}

AEM會儲存您執行動作的歷史記錄，以及執行動作的順序，如此一來，您就可以依照執行動作的順序復原多個動作，並視需要重做這些動作，以重新套用一或多個動作。

如果選取了內容頁面上的元素（例如文字元件），則復原和重做命令會套用至選取的專案。

復原和重做命令的行為與其他軟體中的類似。 在您決定內容時，請使用命令來還原網頁的最近狀態。 例如，如果您將文欄位落移至頁面上的不同位置，您可以使用復原指令將段落移回。 如果之後您認為前一個位置較好，請使用重做指令「復原復原」。

例如，您可以：

* 只要您使用復原後尚未進行頁面編輯，就可以重做動作。
* 復原最多20個編輯動作（預設設定）。
* 也使用 [鍵盤快速鍵](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) 用於還原和重做。

您可以對下列型別的頁面變更使用還原和重做：

* 新增、編輯、移除和移動段落
* 就地編輯段落內容
* 在頁面中複製、剪下和貼上專案

>[!NOTE]
>
>* 需要特殊許可權才能復原和重做檔案與影像的變更。
>* 檔案和影像的變更記錄至少會持續10小時。 然而，在這段時間之後，變更的復原則無法保證。 您的管理員可以變更十小時的預設時間。
>* 您的系統管理員可以根據您執行個體的需求，設定「復原/重做」功能的各個方面。
<!--* Your system administrator can [configure various aspects of the Undo/Redo features](/help/sites-administering/config-undo.md) according to the requirements for your instance.-->
