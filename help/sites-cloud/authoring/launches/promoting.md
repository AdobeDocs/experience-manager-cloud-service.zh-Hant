---
title: 提升啟動
description: 在發佈之前，您需要升級啟動頁面，以將內容移回源（生產）。
exl-id: 5f5ed17c-43db-4ef6-ab79-c491326fa01c
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '817'
ht-degree: 5%

---

# 提升啟動 {#promoting-launches}

在發佈之前，您需要升級啟動頁面，以將內容移回源（生產）。 當啟動頁面被升級時，源頁面的相應頁面被升級頁面的內容替換。 升級啟動頁時可使用以下選項：

* 是僅升級當前頁面還是整個啟動。
* 是否提升當前頁的子頁。
* 是升級完整啟動，還是僅升級已更改的頁面。
* 是否在升級後刪除啟動。

>[!NOTE]
>
>將啟動頁提升到目標(**生產**)，您可以激活 **生產** 頁面作為實體（以加快流程）。 將頁面添加到工作流包，並將其用作激活頁麵包的工作流的負載。 在升級啟動之前，需要建立工作流包。 請參閱 [使用工作流處理已升級AEM頁](#processing-promoted-pages-using-aem-workflow)。

>[!CAUTION]
>
>不能同時升級單個啟動。 這意味著在同一次啟動上同時執行兩個升級操作可能導致錯誤 —  `Launch could not be promoted` （以及日誌中的衝突錯誤）。

>[!CAUTION]
>
>在為 *修改* 頁面，將考慮源分支和啟動分支中的修改。

## 升級啟動頁 {#promoting-launch-pages}

>[!NOTE]
>
>這包括在只有一個發射級別時升級發射頁面的手動操作。 請參閱：
>
>* [升級嵌套啟動](#promoting-a-nested-launch) 當結構中有多個發射時。
>* [啟動 — 事件順序](/help/sites-cloud/authoring/launches/overview.md#launches-the-order-of-events) 的子菜單。
>


您可以從以下任一 **站點** 控制台或 **啟動** 控制台：

1. 開啟:
   * 的 **站點** 控制台在瀏覽源頁時：
      1. 開啟 [參考軌](/help/sites-cloud/authoring/fundamentals/environment-tools.md#references) 並使用 [選擇模式](/help/sites-cloud/authoring/getting-started/basic-handling.md) （或選擇並開啟參照滑軌，訂單不重要）。 將顯示所有引用。
      1. 選擇 **啟動** (例如，啟動(1))，以顯示特定啟動的清單。
      1. 選擇特定啟動以顯示可用操作。
      1. 選擇 **促進啟動** 的子菜單。
   * 的 **站點** 導航啟動頁時控制台：
      1. 使用 [選擇模式](/help/sites-cloud/authoring/getting-started/basic-handling.md)。
      1. 的 **提升** 操作將在工具欄中可用。
   * 的 **啟動** 控制台：
      1. 選擇啟動（點擊/按一下縮略圖）。
      1. 選擇 **提升**。
1. 在第一步中，您可以指定：
   * **目標**
      * **刪除促銷活動後啟動**
   * **範圍**
      * **提升完整啟動項**
      * **提升已修改頁面**
      * **升級已批准的頁面**  — 取決於啟動審批工作流
      * **升級目前頁面**
      * **升級目前頁面與子頁面**

      例如，當選擇僅升級修改的頁面時：

      ![啟動促銷](/help/sites-cloud/authoring/assets/launches-promote.png)

      >[!NOTE]
      >
      >這包括單次啟動，如果已嵌套啟動，請參閱 [升級嵌套啟動](#promoting-a-nested-launch)。
1. 選擇 **下一個** 繼續。
1. 您可以查看要升級的頁面；這取決於您選擇的頁面範圍：

   ![審查促銷](/help/sites-cloud/authoring/assets/launches-promote-review.png)

1. 選擇 **提升**。

## 編輯時升級啟動頁面 {#promoting-launch-pages-when-editing}

編輯啟動頁面時， **升級啟動** 操作也可從 **頁面資訊**。 這將開啟嚮導以收集所需資訊。

![從站點資訊升級啟動](/help/sites-cloud/authoring/assets/launches-promote-page-info.png)

>[!NOTE]
>
>這適用於單個和 [嵌套啟動](#promoting-a-nested-launch)。

## 升級嵌套啟動 {#promoting-a-nested-launch}

建立嵌套啟動後，您可以將其升級回任何源，包括根源（生產）。

![嵌套啟動](/help/sites-cloud/authoring/assets/launches-promoting-nested.png)

1. 與建立嵌套啟動一樣，導航到並選擇 **啟動** 控制台或 **引用** 鐵軌。
1. 選擇 **促進啟動** 的子菜單。
1. 輸入所需的詳細資訊：
   * **目標**
      * **升級目標**  — 您可以向任何來源提升。
      * **升級後刪除啟動**  — 升級後，將刪除選定的啟動以及嵌套在其中的任何啟動。
   * **範圍**  — 在此，您可以選擇是升級整個啟動，還是僅升級實際已編輯的頁面。 如果是後者，則可以選擇包括/排除子頁。 預設配置是僅升級當前頁面的頁面更改：
      * **提升完整啟動項**
      * **提升已修改頁面**
      * **升級已批准的頁面**  — 取決於啟動審批工作流
      * **升級目前頁面**
      * **升級目前頁面與子頁面**

   ![升級啟動設定](/help/sites-cloud/authoring/assets/launches-promote-settings.png)

1. 選擇 **下一個**。
1. 在選擇之前查看升級詳細資訊 **提升**:

   ![查看升級設定](/help/sites-cloud/authoring/assets/launches-promote-review-2.png)

   >[!NOTE]
   >
   >列出的頁面將取決於 **範圍** 已定義，可能是已實際編輯的頁面。

1. 您的更改將在 **啟動** 控制台：

   ![在啟動控制台](/help/sites-cloud/authoring/assets/launches-console.png)

## 使用 AEM 工作流程處理提升頁面 {#processing-promoted-pages-using-aem-workflow}

使用工作流模型對已升級的「啟動」頁執行批量處理：

1. 建立工作流包。
1. 當作者升級「啟動」頁面時，他們會將其儲存在工作流包中。
1. 使用包作為負載啟動工作流模型。

要在升級頁面時自動啟動工作流，請為包節點配置工作流啟動程式。 <!--To start a workflow automatically when pages are promoted, [configure a workflow launcher](/help/sites-administering/workflows-starting.md#workflows-launchers) for the package node.-->

例如，當作者提升「啟動」頁面時，可以自動生成頁面激活請求。 配置工作流啟動程式以在修改包節點時啟動請求激活工作流。

![升級工作流](/help/sites-cloud/authoring/assets/launches-create-workflow.png)
