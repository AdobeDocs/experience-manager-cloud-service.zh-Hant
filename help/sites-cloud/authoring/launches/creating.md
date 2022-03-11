---
title: '建立啟動 '
description: 您可以建立啟動以啟用更新現有網頁的新版本，以便將來激活。
exl-id: 216ccb7a-1409-4f55-8be2-2b088f91a430
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 12%

---

# 建立啟動  {#creating-launches}

建立啟動以啟用更新現有網頁的新版本以供將來激活。 建立「啟動」時，可指定標題和源頁：

* 標題將出現在 [引用](/help/sites-cloud/authoring/fundamentals/environment-tools.md#references) 這裡是作者們可以接觸他們的地方。
* 預設情況下，源頁面的子頁面將包括在啟動中。 如果需要，只能使用源頁。
* 預設情況下， [即時拷貝](/help/sites-cloud/administering/msm/overview.md) 在源頁更改時自動更新啟動頁。 可以指定建立靜態副本以防止自動更改。

(可選) 您可以指定 **啟動日期**  (和時間)，以定義啟動頁面要升級和啟動的時間。不過，「 **啟動日期** 」只會搭配「生產就緒 **」旗標運作(請** 參閱編輯啟動設定 [](/help/sites-cloud/authoring/launches/editing.md#editing-a-launch-configuration));要讓動作實際自動發生，必須同時設定。

>[!NOTE]
>
>建立啟動時，層次結構中上方的頁面不是源頁面的副本。 它們是佔位符，使用模板建立：
>
>* `/libs/launches/templates/outofscope`
>
>無法編輯這些頁面。 您將看到以下消息：
>
>* **本頁不是啟動的一部分。轉到生產頁**


## 建立啟動 {#creating-a-launch}

您可以從「站點」或「啟動」控制台建立啟動：

1. 開啟 **站點** 或 **啟動** 控制台。

   >[!NOTE]
   >
   >使用 **站點** 控制台通常導航到源頁的位置，但這並非強制性，因為您可以在選擇 **啟動源** 的子菜單。

1. 根據您使用的控制台：
   * **啟動**:
      1. 選擇 **建立啟動** 的上界。
   * **網站**:
      1. 選擇 **建立** 的子菜單。
      1. 從此選擇 **建立啟動** 的子菜單。

   >[!NOTE]
   >
   >在Sites **** Console中，您也可以使用選 [擇模式](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) ，在選擇「建立」之前選擇 **頁面**。
   >
   >這將使用所選頁面作為初始源頁面。

1. 在 **選擇源** 走一步 **添加頁面**。 可以選擇多個頁，為每個頁指定路徑：
   * 導航到所需位置。
   * 選擇源頁並確認（複選標籤）。

   根據需要重複。

   ![選擇啟動源](/help/sites-cloud/authoring/assets/launches-select-source.png)

   >[!NOTE]
   >
   >要將頁面和/或分支添加到發佈中，它們必須位於站點內；即位於普通頂級根下面。
   >
   >如果站點包含頂層以下的語言根，則啟動的頁面和分支必須位於公共語言根下。

1. 對於每個條目，您可以指定是否：

   * **包含子頁面**:

      * 指定是否建立包含子頁的啟動。  預設情況下，此子頁包括在內。

   繼續 **下一個**。

   ![選擇啟動源](/help/sites-cloud/authoring/assets/launches-select-source-2.png)

1. 在 **屬性** 指定的嚮導步驟：

   * **啟動標題**:啟動的名稱。 該名稱對作者應有意義。
   * **現有內容**:原始內容將用於建立啟動。
   * **使用新模板替換頁面**:請參閱 [使用新模板建立啟動](#create-launch-with-new-template) 的子菜單。
   * **繼承源頁即時資料**:選擇此選項可在源頁面更改時自動更新啟動頁面的內容。 此選項通過使發佈 [即時拷貝](/help/sites-cloud/administering/msm/overview.md)。 預設情況下，此選項處於選中狀態。—>
   * **啟動日期**:激活啟動副本的日期和時間(取決於 **生產就緒** 標誌；見 [啟動 — 事件順序](/help/sites-cloud/authoring/launches/overview.md#launches-the-order-of-events))。

   ![啟動屬性](/help/sites-cloud/authoring/assets/launches-properties.png)

1. 使用 **建立** 完成該流程並建立新的啟動。 確認對話框將詢問您是否要立即開啟啟動。

   如果返回控制台( **完成**)您可以從以下任一位置查看(並訪問您的啟動：

   * 的 [**啟動** 控制台](/help/sites-cloud/authoring/launches/overview.md#the-launches-console)
   * 的 [**引用** 的 **站點** 控制台](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)

### 使用新模板建立啟動 {#create-launch-with-new-template}

建立啟動時，您可以選擇是否使用新模板：

>[!NOTE]
>
>此選項僅在從建立啟動時可用 **站點** 控制台。 在從建立啟動時不可用 **啟動** 控制台。

![使用新模板建立啟動](/help/sites-cloud/authoring/assets/launches-create-new-template.png)

選擇此項將：

* 更新其他可用選項，
* 包括一個新步驟，您可以在其中選擇所需的模板。

![選擇新模板](/help/sites-cloud/authoring/assets/launches-select-template.png)

>[!CAUTION]
>
>由於使用了其他模板，因此新頁面將為空。 由於頁面結構不同，不會複製任何內容。
>
>此機制可用於更改 [現有頁](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page)  — 但必須考慮內容的丟失。

### 建立嵌套啟動 {#creating-a-nested-launch}

建立嵌套啟動（在啟動中啟動）使您能夠從現有啟動建立啟動，以便作者可以利用已做的更改，而不必對每次啟動多次進行相同的更改。

>[!NOTE]
>
>另請參閱 [升級嵌套啟動](/help/sites-cloud/authoring/launches/promoting.md#promoting-a-nested-launch)。

#### 建立嵌套啟動 — 啟動控制台 {#creating-a-nested-launch-launches-console}

從 **啟動** 控制台基本上與建立任何其他形式的啟動相同，但您需要導航到啟動分支 `/content/launches`:

1. 在 **啟動** 控制台選擇 **建立**。
1. 選擇 **添加頁面**，然後通過指定 `/content/launches` 的 **篩選器** 鐵軌。 選擇所需的啟動並使用「選擇 **」確認**:

   ![建立嵌套啟動](/help/sites-cloud/authoring/assets/launches-create-nested.png)

1. 繼續 **下一個**。

1. 完成 **屬性** 和其他發射一樣。

1. 完成 **建立**。

#### 建立嵌套啟動 — 站點控制台 {#creating-a-nested-launch-sites-console}

從 **站點** 控制台 — 基於現有的啟動：

1. 訪問 [從引用啟動（站點控制台）](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) 按鈕。
1. 選 **擇「建立啟動** 」以開啟嚮導(由於已選擇源，因此它將跳過 **** 選擇源步驟)。
1. 輸入 **啟動標題** 以及任何其他所需細節（如正常發射）。
1. 使用 **建立** 完成該流程並建立新的啟動。 確認對話框將詢問您是否要立即開啟啟動。

如果您選 **取「完成**」，則會返回至Sites ******** Console的「參考」邊欄，如果您選取適當的頁面，則會顯示您的新啟動。

### 刪除啟動 {#deleting-a-launch}

可以從 [啟動控制台](/help/sites-cloud/authoring/launches/overview.md#the-launches-console):

* 按一下/按一下縮略圖，選擇啟動。
* 將出現工具欄 — 選擇刪除。
* 確認操作。

>[!CAUTION]
>
>刪除啟動將刪除啟動本身和所有子體嵌套啟動。
