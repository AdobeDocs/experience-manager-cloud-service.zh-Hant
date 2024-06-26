---
title: 發佈頁面
description: 瞭解如何使用AEM中的各種機制來發佈和取消發佈頁面。
exl-id: 89f2363c-7922-4ca5-92cb-cbee6a393ee3
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '1927'
ht-degree: 5%

---

# 發佈頁面 {#publishing-pages}

在作者環境中建立並檢閱您的內容後，目標為 [使其可在您的公用網站上使用](/help/sites-cloud/authoring/getting-started/concepts.md) （您的發佈環境）。

這稱為發佈頁面。 從發佈環境中移除頁面時，系統會將其稱為取消發佈。 發佈和取消發佈頁面時，作者環境仍會提供進一步的變更，直到您刪除它為止。

您可以立即發佈/取消發佈頁面，或在預先定義的未來日期/時間發佈/取消發佈頁面。

>[!NOTE]
>
>發佈體驗片段的程式基本上與發佈頁面的程式相同，不過是從體驗片段控制檯或編輯器中進行。

## 術語 {#terminology}

當您使用Adobe Experience Manager (AEM)時，可能會遇到as a Cloud Service的與發佈相關的詞語。

* **發佈/取消發佈**
   * 這些是讓您的內容在發佈環境中公開使用（或不公開使用）的動作主要詞語。
   * 這些是AEM檔案中使用的術語。
* **啟用/停用**
   * 這些辭彙與發佈/取消發佈同義。
   * 這些詞語在舊版AEM中使用。
* **復寫/複製**
   * 這些是技術術語，說明發佈頁面時資料（例如頁面內容、檔案、程式碼、使用者評論）從一個環境移動到另一個環境。
   * 這些詞語主要由開發人員使用。

## 發佈頁面 {#publishing-pages-1}

根據您的位置，您可以發佈：

* [從頁面編輯器](#publishing-from-the-editor)
* [從網站主控台](#publishing-from-the-console)

>[!NOTE]
>
>如果您沒有發佈特定頁面所需的許可權：
>
>* 系統會觸發工作流程，將您要發佈的請求通知給適當人員。
>* 您的開發團隊可能已自訂此工作流程。
>* 系統會顯示簡短的訊息，通知您工作流程已觸發。

>[!NOTE]
>
>如果要保留頁面順序，您必須使用 [管理發布](#manage-publication) 以單一動作同時發佈父頁面和任何子頁面。
>
>無法保證頁面順序：
>* 若僅選取子頁面以供發佈（因為訂單資訊會保留在父頁面上）
>* 如果父頁面和子頁面是以不同動作發佈

>[!NOTE]
>
> 如需其他可能性，請參閱 **準時** 和 **關閉時間** 在 [頁面屬性的基本索引標籤](/help/sites-cloud/authoring/fundamentals/page-properties.md#basic)

### 從編輯器發佈 {#publishing-from-the-editor}

如果您正在編輯頁面，可以直接從編輯器發佈頁面。

1. 選取 **頁面資訊** 圖示以開啟功能表，然後 **發佈頁面** 選項。

   ![透過頁面選項發佈頁面](/help/sites-cloud/authoring/assets/publishing-page-options.png)

1. 視頁面是否有需要發佈的參照而定：

   * 如果沒有要發佈的引用，則會直接發佈頁面。
   * 如果頁面含有需要發佈的參照，這些參照會列在 **發佈** 精靈，您可在其中執行以下其中一項作業：
      * 指定您要與頁面一起發佈的資產或標籤等，然後使用 **發佈** 以完成程式。
      * 使用 **取消** 以中止動作。

   ![使用頁面發佈參考](/help/sites-cloud/authoring/assets/publishing-references.png)

1. 選取 **發佈** 會將頁面復寫至發佈環境。 在頁面編輯器中，會顯示確認發佈動作的資訊橫幅。

   ![發佈狀態資訊橫幅](/help/sites-cloud/authoring/assets/publishing-info.png)

   在主控台中檢視相同頁面時，會顯示更新的發佈狀態。

   ![網站主控台欄檢視中的頁面發佈狀態](/help/sites-cloud/authoring/assets/publishing-status-console-column.png)

>[!NOTE]
>
>從編輯器發佈是淺層發佈，也就是說，只會發佈選取的頁面，而不會發佈任何子頁面。

>[!NOTE]
>
>頁面存取者： [別名](/help/sites-cloud/authoring/fundamentals/page-properties.md#advanced) 在編輯器中無法發佈。 編輯器中的發佈選項僅適用於透過實際路徑存取的頁面。

### 從主控台發佈 {#publishing-from-the-console}

在網站主控台中，有兩個發佈選項：

* [快速發佈](#quick-publish)
* [管理發佈](#manage-publication)

#### 快速發佈 {#quick-publish}

**快速發佈** 適用於簡單案例，並立即發佈所選頁面，無需進行任何進一步互動。 因此，任何未發佈的參考也會自動發佈。

若要使用「快速發佈」功能發佈頁面：

1. 在網站主控台中選取一個或多個頁面，然後按一下 **快速發佈** 按鈕。

   ![選取要發佈的頁面](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. 在「快速發佈」對話方塊中，按一下以確認發佈 **發佈** 或按一下以取消 **取消**. 請記住，任何未發佈的參考也會自動發佈。

   ![快速發佈確認](/help/sites-cloud/authoring/assets/publishing-quick-publish.png)

1. 發佈頁面時，畫面會顯示確認發佈的警報。

>[!NOTE]
>
>快速發佈是淺層發佈，也就是說，只會發佈選取的頁面，而不會發佈任何子頁面。

#### 管理發佈 {#manage-publication}

**管理發布** 提供的選項多於 **快速發佈**，允許包含子頁面、自訂參照和啟動任何適用的工作流程，並提供在以後發佈的選項。

>[!NOTE]
>
>如果要保留頁面順序，您必須使用 **管理發布** 以透過單一動作將父頁面與任何子頁面一起發佈。
>
>無法保證頁面順序：
>* 若僅選取子頁面以供發佈（因為訂單資訊會保留在父頁面上）
>* 如果父頁面和子頁面是以不同動作發佈

若要使用「管理發布」來發佈或取消發佈頁面：

1. 在網站主控台中選取一個或多個頁面，然後按一下 **管理發布** 按鈕。

   ![選取要發佈的頁面](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. 「管 **理出版物** 」嚮導將啟動。第一步， **選項**，可讓您：

   * **動作**

     選擇發佈或取消發佈選取的頁面。

   * **正在排程**

     選擇現在或稍後採取該動作。

     稍後發佈會啟動工作流程，以在指定時間發佈選取的一或多個頁面。 相反地，稍後取消發佈會啟動工作流程，以在特定時間取消發佈選取的一個或多個頁面。

     >[!NOTE]
     >
     >如果您想稍後再取消發佈/取消發佈，請前往 [工作流程主控台](/help/sites-cloud/administering/workflows-administering.md#suspending-resuming-and-terminating-a-workflow-instance) 以終止對應的工作流程。

   ![管理發布選項](/help/sites-cloud/authoring/assets/publishing-manage-publication-options.png)

1. 按一下 **下一個** 以繼續。

1. 在管理出版物精靈的下一個步驟中， **範圍**，您可以定義發佈/取消發佈的範圍，例如包含以包含子頁面和/或包含參照。

   ![管理發布範圍](/help/sites-cloud/authoring/assets/publishing-manage-publication-scope.png)

   **新增內容**

   您可以使用「新 **增內容** 」按鈕，在要發佈的頁面清單中新增其他頁面，以防您在啟動「管理出版物」精靈之前未選取其中一個頁面。

   選取 **新增內容** 按鈕會啟動 [路徑瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#path-browser) 以允許選擇內容。

   選取所需頁面，然後按一下 **選取** 將內容新增至精靈或 **取消** 以取消選取範圍並返回精靈。

   **移除選取專案**

   回到精靈中，您可以在清單中選取一個專案，將其從選取範圍中移除。

   ![管理出版物選取頁面](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

   **已發佈引用**

   選取頁面，然後按一下「 」，即可檢視及修改該頁面要發佈或取消發佈的引用 **已發佈引用** 按鈕。

   ![管理發布選項](/help/sites-cloud/authoring/assets/publishing-manage-publication-references.png)

   此 **已發佈引用** 對話方塊會顯示所選內容的參照。 依預設，這些量度會全部選取並發佈/取消發佈，但您可以取消勾選以取消選取，這樣它們就不會包含在動作中。

   按一下 **完成** 儲存變更或 **取消** 以取消選取範圍並返回精靈。

   回到精靈中， **引用** 欄會更新，以反映您選取的要發佈或取消發佈的引用。

   ![管理出版物選取頁面](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

   **包含子項**

   >[!NOTE]
   >
   >另請參閱 [發佈和取消發佈樹狀結構](#publishing-and-unpublishing-a-tree)

   按一下 **包含子項** 開啟對話方塊，讓您：

   * **包含子項**
   * **僅包含直接子項**
   * **僅包含已修改的頁面**
   * **僅包含已發佈的頁面**

   啟用必要選項並確認 **確定** 根據選取選項，將子頁面新增至要發佈或取消發佈的頁面清單中。 按一下 **取消** 以取消選取範圍並返回精靈。

   ![管理發布（包括子項）](/help/sites-cloud/authoring/assets/publishing-include-children.png)

1. 按一下 **發佈** 完成。

   回到網站主控台，系統會傳送通知訊息確認發佈。

1. 如果發佈的頁面與工作流程相關聯，它們可能會顯示在最終版本中 **工作流程** 發佈精靈的步驟。

   ![管理出版物選取頁面](/help/sites-cloud/authoring/assets/publishing-manage-publication-workflow.png)

   >[!NOTE]
   >
   >此 **工作流程** 根據使用者可能擁有也可能沒有的許可權顯示步驟。 請參閱本頁先前關於發佈許可權和管理工作流程存取權的附註，以及 [將工作流程套用至頁面](/help/sites-cloud/authoring/workflows/applying.md) 以取得詳細資訊。

   資源會依觸發的工作流程分組，每個指定選項用於：

   * 定義工作流程的標題。
   * 保留工作流程封裝，前提是工作流程具有多資源支援。
   * 如果已選擇保留工作流程封裝的選項，則定義工作流程封裝的標題。

1. 按一 **下「發佈** 」或「 **稍後發佈** 」以完成出版。

## 取消發佈頁面 {#unpublishing-pages}

取消發佈頁面會將它從您的發佈中移除，或者 [預覽](/help/sites-cloud/authoring/fundamentals/previewing-content.md)，因此不再開放給您的讀者使用。

在 [發佈方式](#publishing-pages)，您可從想要的目的地取消發佈一或多個頁面：

* [從頁面編輯器](#unpublishing-from-the-editor)
* [從網站主控台](#unpublishing-from-the-console)

### 從編輯器中取消發佈 {#unpublishing-from-the-editor}

編輯頁面時，如果您要取消發佈該頁面，請選取「 」 **取消發佈頁面** 在 **頁面資訊** 功能表，視需要而定 [發佈頁面](#publishing-from-the-editor).

>[!NOTE]
>
>頁面存取者： [別名](/help/sites-cloud/authoring/fundamentals/page-properties.md#advanced) 無法取消發佈編輯器中的。 編輯器中的發佈選項僅適用於透過實際路徑存取的頁面。

### 從主控台取消發佈 {#unpublishing-from-the-console}

就像您一樣 [使用「管理出版物」選項進行發佈](#manage-publication)，您也可以用它來取消發佈。

1. 在網站主控台中選取一個或多個頁面，然後按一下 **管理發布** 按鈕。
1. 「管 **理出版物** 」嚮導將啟動。在第一個步驟中， **選項**，選擇「取消發佈」(Unpublish **)，而非「發佈」(Publish)的預設** 選項 ****。

   ![取消發佈 — 選項](/help/sites-cloud/authoring/assets/publishing-unpublish.png)

   正如稍後發佈會啟動工作流程，以在指定時間發佈此版本的頁面一樣，稍後停用也會啟動工作流程，以在指定時間取消發佈選取的一或多個頁面。

   >[!NOTE]
   >
   >如果您想稍後再取消發佈/取消發佈，請前往 [工作流程主控台](/help/sites-cloud/administering/workflows-administering.md#suspending-resuming-and-terminating-a-workflow-instance) 以終止對應的工作流程。

   >[!NOTE]
   >如果您擁有 [預覽](/help/sites-cloud/authoring/fundamentals/previewing-content.md) 環境您可以選取 **目的地** 在管理發布期間。

1. 若要完成取消發佈，請依照您想要的方式繼續完成精靈 [發佈頁面](#manage-publication).

   ![取消發佈 — 範圍](/help/sites-cloud/authoring/assets/publishing-unpublish-scope.png)

## 發佈和取消發佈樹狀結構 {#publishing-and-unpublishing-a-tree}

當您輸入或更新了相當數量的內容頁面時 — 所有這些頁面都位於同一個根頁面下 — 在一個動作中發佈整個樹狀結構會比較容易。

您可以使用 [管理發布](#manage-publication) 選項，執行此操作。

1. 在網站主控台中，選取您要發佈或取消發佈之樹狀結構的根頁面，然後選取 **管理發布**.
1. 「管 **理出版物** 」嚮導將啟動。選擇發佈或取消發佈的時機，然後選取 **下一個** 以繼續。
1. 在 **範圍** 步驟，選取根頁面並選取 **包含子項**.

   ![管理出版物選取頁面](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

1. 在 **包含子項** 對話方塊：

   * 選取 **包含子項**
   * 取消選取 **僅包含直接子項**
   * 取消選取 **僅包含已發佈的頁面**
   * 設定 **僅包含已修改的頁面** 視需要

   這些選項預設為選取，因此您必須記得加以設定。 確認選擇，透過 **確定** 將內容新增到發佈/取消發佈。

   ![包含樹狀結構發佈的子系](/help/sites-cloud/authoring/assets/publishing-include-children-tree.png)

1. 在 **管理發布** 精靈您可以新增其他頁面或移除選取的頁面，以進一步自訂選取專案。

   請記住，您也可以透過以下方式檢閱要發佈的引用： **已發佈引用** 選項。

1. [照常繼續管理發布精靈](#manage-publication) 完成發佈或取消發佈樹狀結構。

## 決定發佈狀態 {#determining-publication-status}

您可以決定頁面的發佈狀態：

* 在 [sites console上的資源概觀資訊](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)

  ![卡片檢視中的發佈狀態](/help/sites-cloud/authoring/assets/publishing-status-console-card.png)

  發佈狀態會顯示在 [網站主控台](/help/sites-cloud/authoring/getting-started/basic-handling.md#card-view)[的卡片](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view)、欄和 [清單檢視中](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view) 。

* 在 [時間表](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)

  ![時間軸檢視中的發佈狀態](/help/sites-cloud/authoring/assets/publishing-status-timeline.png)

* 在 [頁面資訊功能表](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) 編輯頁面時

  ![「頁面資訊」選單中的發佈狀態](/help/sites-cloud/authoring/assets/publishing-status-page-information.png)
