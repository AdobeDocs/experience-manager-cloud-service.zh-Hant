---
title: 發佈頁面
description: 如何使用
exl-id: 89f2363c-7922-4ca5-92cb-cbee6a393ee3
source-git-commit: 66bc262b35f69b7877e4a01df9ab26395afd604d
workflow-type: tm+mt
source-wordcount: '1791'
ht-degree: 7%

---

# 發佈頁面 {#publishing-pages}

在建立和審閱有關作者環境的內容後，目標是 [在你的公共網站上公佈](/help/sites-cloud/authoring/getting-started/concepts.md) （您的發佈環境）。

這稱為發佈頁面。 當要從發佈環境中刪除頁面時，稱為取消發佈。 在發佈和取消發佈頁面時，該頁面在作者環境中仍然可用，以便進行進一步更改，直到您將其刪除。

您可以立即發佈/取消發佈頁面，也可以在將來的預定義日期/時間發佈/取消發佈頁面。

>[!NOTE]
>
>發佈體驗片段與發佈頁面的過程基本相同，但是從體驗片段控制台或編輯器發佈。

## 術語 {#terminology}

在與Adobe Experience Manager()as a Cloud Service合作時，您可能會遇到與發佈相關的AEM不同術語。

* **發佈/取消發佈**
   * 這些是使您的內容在發佈環境中（或不在發佈環境中）公開可用的操作的主要條款。
   * 這些是文檔中使用的AEM術語。
* **激活/停用**
   * 這些術語與發佈/取消發佈是同義的。
   * 這些術語在以前版本中使AEM用。
* **複製/複製**
   * 這些技術術語描述了在發佈頁面時資料從一個環境到另一個環境的移動（如頁面內容、檔案、代碼、用戶注釋）。
   * 這些術語主要供開發商使用。

## 發佈頁面 {#publishing-pages-1}

根據您的位置，您可以發佈：

* [從頁面編輯器](#publishing-from-the-editor)
* [從站點控制台](#publishing-from-the-console)

>[!NOTE]
>
>如果您沒有發佈特定頁面所需的權限：
>
>* 將觸發一個工作流以通知相應人員您的發佈請求。
>* 此工作流可能已由您的開發團隊自定義。
>* 將短暫顯示一條消息，通知您工作流已觸發。


>[!NOTE]
>
> 有關其他可能性，請參見 **準時** 和 **關機時間** 的 [「頁面屬性」的「基本」頁籤](/help/sites-cloud/authoring/fundamentals/page-properties.md#basic)

### 從編輯器發佈 {#publishing-from-the-editor}

如果正在編輯頁面，則可以直接從編輯器發佈該頁面。

1. 選擇 **頁面資訊** 表徵圖，然後 **發佈頁面** 的雙曲餘切值。

   ![通過頁面選項發佈頁面](/help/sites-cloud/authoring/assets/publishing-page-options.png)

1. 根據頁面是否具有需要發佈的引用：

   * 如果沒有要發佈的引用，將直接發佈該頁面。
   * 如果頁面有需要發佈的引用，則這些引用將列在 **發佈** 中，您可以執行以下操作：
      * 指定哪些資產/標籤/等。 要與頁面一起發佈，然後使用 **發佈** 來完成此過程。
      * 使用 **取消** 中止操作。

   ![發佈與頁面的引用](/help/sites-cloud/authoring/assets/publishing-references.png)

1. 選擇 **發佈** 將該頁面複製到發佈環境。 在頁面編輯器中，將顯示確認發佈操作的資訊標題。

   ![發佈狀態資訊標題](/help/sites-cloud/authoring/assets/publishing-info.png)

   在控制台中查看同一頁時，更新的發佈狀態可見。

   ![站點控制台列視圖中的頁面發佈狀態](/help/sites-cloud/authoring/assets/publishing-status-console-column.png)

>[!NOTE]
>
>從編輯器發佈是淺層發佈，即僅發佈/未發佈選定的頁面/頁面和任何子頁面。

>[!NOTE]
>
>訪問者 [別名](/help/sites-cloud/authoring/fundamentals/page-properties.md#advanced) 無法發佈。 編輯器中的發佈選項僅可用於通過實際路徑訪問的頁面。

### 從控制台發佈 {#publishing-from-the-console}

在站點控制台中，有兩個發佈選項：

* [快速發佈](#quick-publish)
* [管理發佈](#manage-publication)

#### 快速發佈 {#quick-publish}

**快速發佈** 是針對簡單情況，並立即發佈所選頁面，而不需要進行任何進一步的交互。 因此，任何未發佈的引用也將自動發佈。

要發佈具有「快速發佈」的頁面：

1. 在站點控制台中選擇頁面，然後按一下 **快速發佈** 按鈕

   ![選擇發佈頁面](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. 在「快速發佈」對話框中，按一下 **發佈** 或按一下取消 **取消**。 請記住，所有未發佈的引用都將自動發佈。

   ![快速發佈確認](/help/sites-cloud/authoring/assets/publishing-quick-publish.png)

1. 在發佈頁面時，將顯示確認發佈的警報。

>[!NOTE]
>
>「快速發佈」是淺層發佈，即僅發佈/發佈選定的頁面/頁面，而任何子頁面均未發佈。

#### 管理發佈 {#manage-publication}

**管理發布** 提供了更多選項 **快速發佈**，允許包含子頁、自定義引用、啟動任何適用的工作流以及提供以後發佈的選項。

要使用「管理發布」發佈或取消發佈頁面：

1. 在站點控制台中選擇頁面，然後按一下 **管理發布** 按鈕

   ![選擇發佈頁面](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. 「管 **理出版物** 」嚮導將啟動。第一步， **選項**，允許您：

   * **動作**

      選擇以發佈或取消發佈所選頁面。

   * **排程**

      選擇立即或稍後執行該操作。

      稍後發佈將啟動工作流，以在指定時間發佈所選頁或頁。 相反，稍後取消發佈會啟動工作流以在特定時間取消發佈所選頁面。

      >[!NOTE]
      >
      >如果要在以後取消發佈/取消發佈，請轉到 [工作流控制台](/help/sites-cloud/administering/workflows-administering.md#suspending-resuming-and-terminating-a-workflow-instance) 以終止相應的工作流。
   ![管理發布選項](/help/sites-cloud/authoring/assets/publishing-manage-publication-options.png)

1. 按一下 **下一個** 繼續。

1. 在「管理發布」嚮導的下一步中， **範圍**，可以定義發佈/取消發佈的範圍，例如包括以包括子頁和/或包括引用。

   ![管理發布範圍](/help/sites-cloud/authoring/assets/publishing-manage-publication-scope.png)

   **新增內容**

   您可以使用「新 **增內容** 」按鈕，在要發佈的頁面清單中新增其他頁面，以防您在啟動「管理出版物」精靈之前未選取其中一個頁面。

   選擇 **添加內容** 按鈕啟動 [路徑瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#path-browser) 允許內容選擇。

   選擇所需的頁面，然後按一下 **選擇** 向嚮導或 **取消** 的子菜單。

   **移除選取項目**

   返回嚮導中，您可以在清單中選擇一個項目，以將其從選定項中刪除。

   ![管理發布選擇頁](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

   **已發佈引用**

   通過選擇頁面，然後按一下 **已發佈引用** 按鈕

   ![管理發布選項](/help/sites-cloud/authoring/assets/publishing-manage-publication-references.png)

   的 **已發佈引用** 對話框顯示所選內容的引用。 預設情況下，它們都被選中並將被發佈/未發佈，但您可以取消選中以取消選擇它們，以便它們不包括在操作中。

   按一下 **完成** 保存更改或 **取消** 的子菜單。

   回到嚮導中， **引用** 將更新列以反映您選擇的要發佈或未發佈的引用。

   ![管理發布選擇頁](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

   **包含子項**

   >[!NOTE]
   >
   >請參閱 [發佈和取消發佈樹](#publishing-and-unpublishing-a-tree)

   按一下 **包括子項** 開啟對話框，您可以：

   * **包含子系**
   * **僅包含直接子項**
   * **僅包含修改過的頁面**
   * **僅包含已發佈的頁面**

   激活所需選項並確認 **確定** 將子頁面添加到要發佈或未發佈的頁面清單中。 按一下 **取消** 的子菜單。

   ![管理出版物（包括子出版物）](/help/sites-cloud/authoring/assets/publishing-include-children.png)

1. 按一下 **發佈** 完成。

   在站點控制台中，一條通知消息將確認發佈。

1. 如果已發佈頁面與工作流關聯，則它們可能會在最終檔案中顯示 **工作流** 的子菜單。

   ![管理發布選擇頁](/help/sites-cloud/authoring/assets/publishing-manage-publication-workflow.png)

   >[!NOTE]
   >
   >的 **工作流** 步驟將根據用戶可能擁有或不擁有的權限顯示。 有關發佈權限以及管理對工作流的訪問和 [將工作流應用於頁面](/help/sites-cloud/authoring/workflows/applying.md) 的雙曲餘切值。

   資源按觸發的工作流和每個給定選項分組，以：

   * 定義工作流的標題。
   * 保留工作流包，前提是工作流具有多資源支援。
   * 如果選擇了保留工作流包的選項，則定義工作流包的標題。

1. 按一 **下「發佈** 」或「 **稍後發佈** 」以完成出版。

## 取消發佈頁面 {#unpublishing-pages}

取消發佈頁面將從您的發佈環境中刪除它，這樣讀者就無法再使用它了。

在 [與出版類似](#publishing-pages)，可以取消發佈一個或多個頁面：

* [從頁面編輯器](#unpublishing-from-the-editor)
* [從站點控制台](#unpublishing-from-the-console)

### 從編輯器取消發佈 {#unpublishing-from-the-editor}

編輯頁面時，如果要取消發佈該頁面，請選擇 **取消發佈頁面** 的 **頁面資訊** 菜單，就像你 [發佈頁面](#publishing-from-the-editor)。

>[!NOTE]
>
>訪問者 [別名](/help/sites-cloud/authoring/fundamentals/page-properties.md#advanced) 不能取消發佈。 編輯器中的發佈選項僅可用於通過實際路徑訪問的頁面。

### 從控制台取消發佈 {#unpublishing-from-the-console}

就像你 [使用「管理發布」選項發佈](#manage-publication)，也可以使用它取消發佈。

1. 在站點控制台中選擇頁面，然後按一下 **管理發布** 按鈕
1. 「管 **理出版物** 」嚮導將啟動。在第一個步驟中， **選項**，選擇「取消發佈」(Unpublish **)，而非「發佈」(Publish)的預設** 選項 ****。

   ![取消發佈 — 選項](/help/sites-cloud/authoring/assets/publishing-unpublish.png)

   正如稍後發佈啟動工作流以在指定時間發佈此版本的頁面一樣，稍後停用將啟動工作流以在特定時間取消發佈所選頁面或頁面。

   >[!NOTE]
   >
   >如果要在以後取消發佈/取消發佈，請轉到 [工作流控制台](/help/sites-cloud/administering/workflows-administering.md#suspending-resuming-and-terminating-a-workflow-instance) 以終止相應的工作流。

1. 要完成取消發佈，請按您希望的方式繼續嚮導 [發佈頁面](#manage-publication)。

   ![取消發佈 — 範圍](/help/sites-cloud/authoring/assets/publishing-unpublish-scope.png)

## 發佈和取消發佈樹 {#publishing-and-unpublishing-a-tree}

當您輸入或更新了大量內容頁面（所有內容都駐留在同一根頁面下）時，在一個操作中發佈整個樹會更容易。

您可以使用 [管理發布](#manage-publication) 選項。

1. 在站點控制台中，選擇要發佈或取消發佈的樹的根頁，然後選擇 **管理發布**。
1. 「管 **理出版物** 」嚮導將啟動。選擇發佈或取消發佈，並選擇何時發佈 **下一個** 繼續。
1. 在 **範圍** 步驟，選擇根頁並選擇 **包括子項**。

   ![管理發布選擇頁](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

1. 在 **包括子項** 對話框：

   * 選擇 **包括子項**
   * 取消選擇 **僅包括直接子項**
   * 取消選擇 **僅包括已發佈的頁面**
   * 配置 **僅包括已修改的頁面** 按要求

   預設情況下，這些選項處於選中狀態，因此必須記住要配置它們。 確認選擇 **確定** 將內容添加到發佈/取消發佈。

   ![包括用於樹發佈的子項](/help/sites-cloud/authoring/assets/publishing-include-children-tree.png)

1. 在 **管理發布** 嚮導，您可以通過添加其他頁面或刪除那些選定的頁面來進一步自定義選定內容。

   請記住，您也可以通過 **已發佈引用** 的雙曲餘切值。

1. [繼續正常管理發布嚮導](#manage-publication) 完成樹的發佈或取消發佈。

## 確定發佈狀態 {#determining-publication-status}

您可以確定頁面的發佈狀態：

* 在 [站點控制台上的資源概述資訊](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)

   ![卡視圖中的發佈狀態](/help/sites-cloud/authoring/assets/publishing-status-console-card.png)

   發佈狀態會顯示在 [網站主控台](/help/sites-cloud/authoring/getting-started/basic-handling.md#card-view)[的卡片](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view)、欄和 [清單檢視中](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view) 。

* 在 [時間](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)

   ![時間軸視圖中的發佈狀態](/help/sites-cloud/authoring/assets/publishing-status-timeline.png)

* 在 [頁面資訊菜單](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) 編輯頁面時

   ![「頁面資訊」菜單中的發佈狀態](/help/sites-cloud/authoring/assets/publishing-status-page-information.png)
