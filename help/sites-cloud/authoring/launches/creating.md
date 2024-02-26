---
title: 建立啟動
description: 您可以建立啟動項，以更新現有網頁的新版本，以供日後啟用。
exl-id: 216ccb7a-1409-4f55-8be2-2b088f91a430
source-git-commit: bbd845079cb688dc3e62e2cf6b1a63c49a92f6b4
workflow-type: tm+mt
source-wordcount: '1042'
ht-degree: 13%

---

# 建立啟動 {#creating-launches}

建立啟動項，以更新現有網頁的新版本，以供日後啟用。 建立啟動項時，您可以指定標題和來源頁面：

* 標題會顯示在 [引用](/help/sites-cloud/authoring/sites-console/console-side-panel.md#references) 邊欄，作者可從中存取縮圖，進而加以處理。
* 預設情況下，啟動會包含來源頁面的子頁面。 您可以視需要使用來源頁面。
* 根據預設， [即時副本](/help/sites-cloud/administering/msm/overview.md) 當來源頁面變更時，會自動更新啟動頁面。 您可以指定建立靜態副本，以防止自動變更。

(可選) 您可以指定 **啟動日期**  (和時間)，以定義啟動頁面要升級和啟動的時間。不過，「 **啟動日期** 」只會搭配「生產就緒 **」旗標運作(請** 參閱編輯啟動設定 [](/help/sites-cloud/authoring/launches/editing.md#editing-a-launch-configuration));要讓動作實際自動發生，必須同時設定。

>[!NOTE]
>
>當您建立啟動項時，階層中較高位置的頁面不是來源頁面的復本。 它們是使用範本建立的預留位置：
>
>* `/libs/launches/templates/outofscope`
>
>無法編輯這些頁面。 您會看到訊息：
>
>* **此頁面不是啟動項的一部分。 前往生產頁面**

## 建立啟動項 {#creating-a-launch}

您可以從「網站」或「啟動」主控台建立啟動：

1. 開啟 **網站** 或 **啟動** 主控台。

   >[!NOTE]
   >
   >使用時 **網站** console通常會導覽至來源頁面的位置，但這並非必要操作，因為當您選取 **啟動來源** 在精靈中。

1. 根據您使用的主控台：
   * **啟動**：
      1. 選取 **建立啟動項** 以開啟精靈。
   * **網站**：
      1. 選取 **建立** 以開啟選取方塊。
      1. 從此選取 **建立啟動項** 以開啟精靈。

   >[!NOTE]
   >
   >在Sites **** Console中，您也可以使用選 [擇模式](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources) ，在選擇「建立」之前選擇 **頁面**。
   >
   >這會使用選取的頁面作為初始來源頁面。

1. 在 **選取來源** 您需要執行的步驟 **新增頁面**. 您可以選取多個頁面，指定每個頁面的路徑：
   * 導覽至所需位置。
   * 選取來源頁面並確認（核取記號）。

   視需要重複。

   ![選取啟動來源](/help/sites-cloud/authoring/assets/launches-select-source.png)

   >[!NOTE]
   >
   >若要將頁面和/或分支新增至啟動，這些頁面和/或分支必須位於網站內（即在通用頂層根目錄下）。
   >
   >如果網站在頂層底下包含語言根，則啟動項的頁面和分支必須在共同語言根底下。

1. 對於每個專案，您可以指定是否：

   * **包含子頁面**：

      * 指定您是否要建立具有或不具有子頁面的啟動。  預設會包含此子頁面。

   繼續進行 **下一個**.

   ![選取啟動來源](/help/sites-cloud/authoring/assets/launches-select-source-2.png)

1. 在 **屬性** 您可以指定的精靈步驟：

   * **啟動項標題**：啟動項的名稱。 這個名稱應該對作者有意義。
   * **使用現有內容**：原始內容會用於建立啟動。
   * **使用新範本取代頁面**：請參閱 [使用新範本建立啟動項](#create-launch-with-new-template) 以取得更多詳細資料。
   * **繼承來源頁面即時資料**：選取此選項，可在來源頁面變更時自動更新啟動頁面的內容。 此選項會將啟動設為 [即時副本](/help/sites-cloud/administering/msm/overview.md). 依預設，會選取此選項。—>
   * **啟動日期**：啟動副本的啟動日期和時間(取決於 **生產就緒** 標幟；請參閱 [啟動 — 事件順序](/help/sites-cloud/authoring/launches/overview.md#launches-the-order-of-events))。

   ![啟動項屬性](/help/sites-cloud/authoring/assets/launches-properties.png)

1. 使用 **建立** 以完成程式並建立您的新啟動項。 確認對話方塊會詢問您是否要立即開啟啟動項。

   如果您傳回主控台(包含 **完成**)您可以透過以下其中一種方式來檢視（及存取）您的啟動項：

   * 此 [**啟動** 主控台](/help/sites-cloud/authoring/launches/overview.md#the-launches-console)
   * 此 [**引用** 在 **網站** 主控台](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)

### 使用新範本建立啟動項 {#create-launch-with-new-template}

建立啟動項時，您可以選擇是否使用新範本：

>[!NOTE]
>
>此選項僅適用於從建立啟動項 **網站** 主控台。 從建立啟動時，此選項無法使用 **啟動** 主控台。

![使用新範本建立啟動](/help/sites-cloud/authoring/assets/launches-create-new-template.png)

選取此選項將：

* 更新其他可用選項，
* 包括一個新步驟，您可在其中選取所需的範本。

![選取新範本](/help/sites-cloud/authoring/assets/launches-select-template.png)

>[!CAUTION]
>
>當使用不同的範本時，新頁面會是空的。 由於頁面結構不同，因此不會複製任何內容。
>
>此機制可用來變更的範本 [現有頁面](/help/sites-cloud/authoring/sites-console/creating-pages.md#creating-a-new-page)  — 雖然必須考量內容遺失。

### 建立巢狀啟動 {#creating-a-nested-launch}

建立巢狀啟動（在啟動內啟動）可讓您從現有的啟動建立啟動，讓作者能夠利用已進行的變更，而不必針對每個啟動多次進行相同的變更。

>[!NOTE]
>
>另請參閱 [提升巢狀啟動](/help/sites-cloud/authoring/launches/promoting.md#promoting-a-nested-launch).

#### 建立巢狀啟動 — 啟動主控台 {#creating-a-nested-launch-launches-console}

從建立巢狀啟動 **啟動** console基本上與建立任何其他形式的啟動相同，唯一例外是您必須導覽至啟動分支 `/content/launches`：

1. 在 **啟動** 主控台選取 **建立**.
1. 選取 **新增頁面**，然後指定以導覽至啟動分支 `/content/launches` 在 **篩選器** 邊欄。 選擇所需的啟動並使用「選擇 **」確認**:

   ![建立巢狀啟動](/help/sites-cloud/authoring/assets/launches-create-nested.png)

1. 繼續進行 **下一個**.

1. 完成 **屬性** 和任何其他啟動項一樣。

1. 完成並提供 **建立**.

#### 建立巢狀啟動 — Sites主控台 {#creating-a-nested-launch-sites-console}

若要從以下位置建立巢狀啟動： **網站** 主控台 — 根據現有的啟動：

1. 存取 [從「引用」（網站主控台）啟動](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) 以顯示可用的動作。
1. 選 **擇「建立啟動** 」以開啟嚮導(由於已選擇源，因此它將跳過 **** 選擇源步驟)。
1. 輸入 **啟動項標題** 以及任何其他必要的詳細資料（與一般啟動一樣）。
1. 使用 **建立** 以完成程式並建立您的新啟動項。 確認對話方塊會詢問您是否要立即開啟啟動項。

如果您選 **取「完成**」，則會返回至Sites ******** Console的「參考」邊欄，如果您選取適當的頁面，則會顯示您的新啟動。

### 刪除啟動項 {#deleting-a-launch}

您可以從以下位置刪除啟動項： [啟動主控台](/help/sites-cloud/authoring/launches/overview.md#the-launches-console)：

* 點選/按一下縮圖，以選取啟動。
* 工具列隨即顯示 — 選取「刪除」。
* 確認動作。

>[!CAUTION]
>
>刪除啟動將移除啟動本身和所有子系巢狀啟動。
