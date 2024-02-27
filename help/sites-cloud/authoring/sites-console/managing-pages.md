---
title: 管理頁面
description: 瞭解如何在AEM中管理您的網站頁面，包括移動、複製和刪除。
source-git-commit: faac7c803a5145f4207154bfb3c9aa06274bbb86
workflow-type: tm+mt
source-wordcount: '1271'
ht-degree: 0%

---


# 管理頁面 {#managing-pages}

瞭解如何在AEM中管理您的網站頁面，包括移動、複製和刪除。

>[!TIP]
>
>開始管理頁面之前，請先熟悉 [AEM中頁面的組織方式。](/help/sites-cloud/authoring/sites-console/organizing-pages.md)

>[!TIP]
>
>有好幾個 [鍵盤快速鍵](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md) 您可從網站主控台使用，以便更有效率地組織頁面。

## 存取許可權 {#access-privileges}

您的帳戶需要適當的存取許可權才能在頁面上執行動作，例如建立、複製、移動、編輯和刪除。

如果您遇到任何問題，我們建議您連絡系統管理員。

## 開啟頁面進行編輯 {#opening-a-page-for-editing}

晚於 [建立頁面](/help/sites-cloud/authoring/sites-console/creating-pages.md) 或使用導覽至現有頁面 [此 **網站** 主控台，](/help/sites-cloud/authoring/sites-console/introduction.md) 您可以開啟它進行編輯。

1. 開啟 [此 **網站** 主控台。](/help/sites-cloud/authoring/sites-console/introduction.md)
1. 導覽以尋找您要編輯的頁面。
1. 使用下列任一專案選取您的頁面：

   * [快速動作](/help/sites-cloud/authoring/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-cloud/authoring/basic-handling.md#selecting-resources) 和工具列

1. 點選或按一下 **編輯** 圖示。

   ![編輯按鈕](/help/sites-cloud/authoring/assets/edit.png)

1. 頁面隨即開啟，您可以視需要編輯頁面。 根據所選頁面的建立方式， **編輯** 動作會開啟適當的編輯器。
   * [頁面編輯器](/help/sites-cloud/authoring/page-editor/introduction.md)  — 適用於使用AEM頁面編輯器建立的頁面
   * [通用編輯器](/help/sites-cloud/authoring/universal-editor/authoring.md)  — 適用於使用通用編輯器建立的頁面

## 複製和貼上頁面 {#copying-and-pasting-a-page}

您可以將頁面及其所有子頁面複製到新位置：

1. 開啟 [此 **網站** 主控台。](/help/sites-cloud/authoring/sites-console/introduction.md)
1. 導覽以尋找您要複製的頁面。
1. 使用以下其中一種方式選取您的頁面：

   * [快速動作](/help/sites-cloud/authoring/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-cloud/authoring/basic-handling.md#selecting-resources) 和工具列

1. 點選或按一下 **複製** 頁面圖示。

   ![複製](/help/sites-cloud/authoring/assets/copy.png)

1. 導覽至頁面新復本的位置。
1. 選取 **貼上** 圖示可用。

   ![貼上](/help/sites-cloud/authoring/assets/paste.png)

1. 「貼上」對話方塊會顯示貼上交易的摘要，以及執行下列功能的功能：
   * **新網站名稱：** 變更已貼上頁面的名稱
   * **貼上（不含子系）：** 貼上時省略所選頁面的子頁面（預設會貼上子頁面）

   ![貼上對話方塊](/help/sites-cloud/authoring/assets/paste-dialog.png)

1. 選取 **貼上** 按鈕以確認貼上交易並建立新頁面。

>[!NOTE]
>
>如果您將頁面複製到某個位置，而該位置已經存在名稱與原始名稱相同的頁面，則系統將藉由附加一個編號來自動產生名稱的變體。 例如，如果 `beach` 已存在，已存在名稱為的新頁面 `beach` 變為 `beach1`.

>[!NOTE]
>
>如果您在選擇模式中啟動貼上動作，這會在頁面複製後立即自動結束。

## 移動或重新命名頁面 {#moving-or-renaming-a-page}

移動或重新命名頁面的程式基本相同，這兩個動作都由「移動頁面」精靈處理。 使用此精靈，您可以：

* 重新命名頁面而不移動頁面。
* 移動頁面而不重新命名。
* 同時移動和重新命名。

AEM提供可更新任何內部連結的功能，這些連結會參照正在重新命名/移動的頁面。 您可以逐頁進行，提供完整的彈性。

1. 開啟 [此 **網站** 主控台。](/help/sites-cloud/authoring/sites-console/introduction.md)
1. 導覽以尋找您要移動的頁面。
1. 使用以下其中一種方式選取您的頁面：

   * [快速動作](/help/sites-cloud/authoring/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-cloud/authoring/basic-handling.md#selecting-resources) 和工具列

1. 點選或按一下 **移動** 頁面圖示以開啟「移動頁面」精靈。

   ![移動按鈕](/help/sites-cloud/authoring/assets/move.png)

1. 從 **重新命名** 精靈的步驟您可以：

   * 指定移動頁面後您希望頁面使用的名稱，然後選取「 」 **下一個** 以繼續進行。
   * **取消** 以中止程式。

   ![移動和重新命名頁面](/help/sites-cloud/authoring/assets/move-page-rename.png)

   * 如果您只移動頁面，頁面名稱可以維持不變。

   >[!NOTE]
   >
   >如果您將頁面移至相同名稱的頁面已經存在的位置，系統將藉由附加編號來自動產生名稱的變體。 例如，如果 `beach` 已存在，已存在名稱為的新頁面 `beach` 變為 `beach1`.

1. 從 **選取目的地** 精靈的步驟您可以：

   * 使用 [欄檢視](/help/sites-cloud/authoring/basic-handling.md#column-view) 若要導覽至頁面的新位置：

      * 按一下目的地的縮圖，以選取目的地。
      * 按一下 **下一個** 以繼續。

   * 使用 **返回** 以返回頁面名稱規格。

   >[!NOTE]
   >
   >依照預設，您正在移動或重新命名的頁面的父頁面會選取為目的地。

   ![選取頁面移動目的地](/help/sites-cloud/authoring/assets/move-page-destination.png)

   >[!NOTE]
   >
   >如果您將頁面移至相同名稱的頁面已經存在的位置，系統將藉由附加編號來自動產生名稱的變體。 例如，如果 `winter` 已存在， `winter` 變為 `winter1`.

1. 如果頁面已連結至或參考，或已發佈，則詳細資訊會列在 **調整/重新發佈** 步驟。

   * 您可以指出哪些頁面應適當地調整及/或重新發佈。

   >[!NOTE]
   >
   >如果頁面既未連結也未參考，則無法使用此步驟。

   ![移動時重新發佈頁面](/help/sites-cloud/authoring/assets/move-page-republish.png)

1. 點選或按一下 **移動** 以定義移動動作應該何時發生。

   * **現在** 將觸發 [非同步作業](#asynchronous-actions) 以立即移動頁面。
   * **稍後** 可讓您排程處理移動的日期。

   ![定義移動時間](assets/managing-pages-move-page-now-later.png)

1. 點選或按一下 **繼續** 以完成頁面移動。

>[!NOTE]
>
>如果頁面已發佈，移動頁面會自動將其取消發佈。 依預設，移動完成時會重新發佈它，但取消勾選即可變更此設定。 **重新發佈** 中的欄位 **調整/重新發佈** 步驟。

>[!NOTE]
>
>重新命名頁面也必須遵循 [頁面命名慣例](#page-naming-conventions) 指定新頁面名稱時。

>[!NOTE]
>
>只能將頁面移至允許該頁面所依據的範本位置。 另請參閱 [範本可用性](/help/implementing/developing/components/templates.md#template-availability) 以取得詳細資訊。

### 非同步動作 {#asynchronous-actions}

頁面移動動作一律會以非同步方式處理，讓使用者能不受阻礙地繼續在UI中編寫。

您可在以下位置檢查非同步作業的狀態： [**非同步工作狀態** 儀表板](/help/operations/asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations) 在 **全域導覽** > **工具** > **作業** > **工作**

>[!TIP]
>
>如需有關非同步作業處理以及如何設定頁面移動/重新命名動作限制的詳細資訊，請參閱 [非同步作業](/help/operations/asynchronous-jobs.md) 檔案。

### 刪除頁面 {#deleting-a-page}

1. 開啟 [此 **網站** 主控台。](/help/sites-cloud/authoring/sites-console/introduction.md)
1. 導覽至您要刪除的頁面。
1. 使用 [選擇模式](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources) 以選取所需頁面，然後使用 **刪除** 從工具列：

   ![刪除按鈕](/help/sites-cloud/authoring/assets/delete.png)

1. 對話方塊將會要求確認。

   ![刪除對話方塊](/help/sites-cloud/authoring/assets/delete-page.png)

   * **您要在刪除前封存頁面嗎？**  — 如果勾選，刪除時會建立選取要刪除之頁面的版本。
      * [日後可以還原這些版本](/help/sites-cloud/authoring/sites-console/page-versions.md).
      * 沒有舊版刪除的頁面無法還原。
1. 點選或按一下 **取消** 中止動作或 **刪除** 以確認動作。
   * 如果頁面沒有參考，則會刪除頁面。
   * 如果頁面含有參考，則會出現訊息方塊通知您 **一個或多個頁面被引用。** 您可以選取 **強制刪除** 或 **取消**.

>[!NOTE]
>
>如果頁面已發佈，則在刪除前會自動取消發佈。

### 鎖定頁面 {#locking-a-page}

您可以 [鎖定/解鎖頁面](/help/sites-cloud/authoring/page-editor/edit-content.md#locking-a-page) 從主控台或編輯個別頁面時。 有關頁面是否已鎖定的資訊也會顯示在這兩個位置。

![「鎖定」按鈕](/help/sites-cloud/authoring/assets/lock.png)
![解鎖按鈕](/help/sites-cloud/authoring/assets/unlock.png)

### 建立新資料夾 {#creating-a-new-folder}

您可以建立資料夾來協助組織您的檔案和頁面。

1. 開啟 [此 **網站** 主控台。](/help/sites-cloud/authoring/sites-console/introduction.md)
1. 導覽至所需位置。
1. 若要開啟選項清單，請選取 **建立** 從工具列
1. 選取 **資料夾** 以開啟對話方塊。 您可在此輸入 **名稱** 和 **標題**：

   ![建立資料夾](/help/sites-cloud/authoring/assets/organizing-create-folder.png)

1. 選取 **建立** 以建立資料夾。

>[!NOTE]
>
>* 資料夾也必須遵守 [頁面命名慣例](#page-naming-conventions) 指定新資料夾名稱時。
>* 資料夾只能直接建立在 **網站** 或位於其他資料夾下。 無法在頁面下建立縮圖。
>* 您可以在資料夾上執行移動、複製、貼上、刪除、發佈、取消發佈和檢視/編輯屬性的標準動作。
>* 無法在即時副本中選取資料夾。
