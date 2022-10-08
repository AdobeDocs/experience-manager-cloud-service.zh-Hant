---
title: 發佈頁面
description: 如何使用AEM發佈和取消發佈頁面
exl-id: 89f2363c-7922-4ca5-92cb-cbee6a393ee3
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '1812'
ht-degree: 6%

---

# 發佈頁面 {#publishing-pages}

在製作環境中建立並檢閱內容後，目標是 [在你的公共網站上公佈](/help/sites-cloud/authoring/getting-started/concepts.md) （您的發佈環境）。

這稱為發佈頁面。 如果您想從發佈環境中移除頁面，即為取消發佈。 發佈和取消發佈頁面時，製作環境仍可供進一步變更，直到您刪除為止。

您可以立即發佈/取消發佈頁面，或在日後預先定義的日期/時間發佈。

>[!NOTE]
>
>發佈體驗片段基本上遵循與發佈頁面相同的程式，不過可從體驗片段主控台或編輯器進行。

## 術語 {#terminology}

使用Adobe Experience Manager(AEM)as a Cloud Service時，您可能會遇到與發佈相關的不同辭彙。

* **發佈/取消發佈**
   * 這些是可讓您的內容在您的發佈環境（或不可）上公開的動作的主要辭彙。
   * 這些是AEM檔案中使用的辭彙。
* **啟用/停用**
   * 這些詞語等同於發佈/取消發佈。
   * 這些詞語用於舊版AEM。
* **複製/複製**
   * 這些技術術語說明在您發佈頁面時，資料（例如頁面內容、檔案、程式碼、使用者註解）從一個環境移動至另一個環境。
   * 這些術語主要由開發人員使用。

## 發佈頁面 {#publishing-pages-1}

您可以根據您的位置發佈：

* [從頁面編輯器](#publishing-from-the-editor)
* [從網站主控台](#publishing-from-the-console)

>[!NOTE]
>
>如果您沒有發佈特定頁面所需的權限：
>
>* 系統會觸發工作流程，通知您發佈請求的適當人員。
>* 您的開發團隊可能已自訂此工作流程。
>* 系統會短暫顯示訊息，通知您工作流程已觸發。


>[!NOTE]
>
> 如需其他可能性，請參閱 **準時** 和 **關閉時間** 在 [頁面屬性的基本索引標籤](/help/sites-cloud/authoring/fundamentals/page-properties.md#basic)

### 從編輯器發佈 {#publishing-from-the-editor}

如果您正在編輯頁面，則可直接從編輯器發佈頁面。

1. 選取 **頁面資訊** 圖示來開啟功能表，然後 **發佈頁面** 選項。

   ![透過頁面選項發佈頁面](/help/sites-cloud/authoring/assets/publishing-page-options.png)

1. 視頁面是否有需要發佈的參考而定：

   * 如果沒有要發佈的參考，則會直接發佈頁面。
   * 如果頁面有需要發佈的參考，這些將列在 **發佈** 嚮導中，您可以在其中：
      * 指定哪些資產/標籤/等等 您想要與頁面一起發佈，然後使用 **發佈** 來完成此程式。
      * 使用 **取消** 中止動作。

   ![使用頁面發佈參考](/help/sites-cloud/authoring/assets/publishing-references.png)

1. 選取 **發佈** 會將頁面複製到發佈環境。 在頁面編輯器中，會顯示資訊橫幅以確認發佈動作。

   ![發佈狀態資訊橫幅](/help/sites-cloud/authoring/assets/publishing-info.png)

   在主控台中檢視相同頁面時，更新的發佈狀態會顯示。

   ![網站主控台欄檢視中的頁面發佈狀態](/help/sites-cloud/authoring/assets/publishing-status-console-column.png)

>[!NOTE]
>
>從編輯器發佈是淺層發佈，亦即只會發佈/發佈選取的頁面/頁面，而不會發佈任何子頁面。

>[!NOTE]
>
>由存取的頁面 [別名](/help/sites-cloud/authoring/fundamentals/page-properties.md#advanced) 無法發佈。 編輯器中的發佈選項僅適用於透過其實際路徑存取的頁面。

### 從主控台發佈 {#publishing-from-the-console}

在網站主控台中，有兩個發佈選項：

* [快速發佈](#quick-publish)
* [管理發佈](#manage-publication)

#### 快速發佈 {#quick-publish}

**快速發佈** 是供簡單的案例使用，且會立即發佈選取的頁面，而不需進行任何進一步互動。 因此，任何未發佈的參考也會自動發佈。

若要使用快速發佈來發佈頁面：

1. 在網站主控台中選取頁面，然後按一下 **快速發佈** 按鈕。

   ![選擇要發佈的頁面](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. 在快速發佈對話方塊中，按一下 **發佈** 或按一下「 **取消**. 請記住，所有未發佈的參考也會自動發佈。

   ![快速發佈確認](/help/sites-cloud/authoring/assets/publishing-quick-publish.png)

1. 發佈頁面時，會顯示確認發佈的警報。

>[!NOTE]
>
>「快速發佈」是淺層發佈，亦即只會發佈/發佈選取的頁面/頁面，而不會發佈任何子頁面。

#### 管理發佈 {#manage-publication}

**管理出版物** 選項多於 **快速發佈**，可包含子頁面、自訂參考、啟動任何適用的工作流程，以及提供以後發佈的選項。

若要使用管理出版物來發佈或取消發佈頁面：

1. 在網站主控台中選取頁面，然後按一下 **管理出版物** 按鈕。

   ![選擇要發佈的頁面](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. 「管 **理出版物** 」嚮導將啟動。第一步， **選項**，可讓您：

   * **動作**

      選擇發佈或取消發佈所選頁面。

   * **排程**

      選擇立即或稍後執行該操作。

      稍後發佈會啟動工作流程，以在指定時間發佈選取的頁面。 反之，稍後取消發佈會開始工作流程，以在特定時間取消發佈選取的頁面。

      >[!NOTE]
      >
      >如果您想要取消稍後發佈/取消發佈，請前往 [工作流程主控台](/help/sites-cloud/administering/workflows-administering.md#suspending-resuming-and-terminating-a-workflow-instance) 終止相應的工作流。
   ![管理出版物選項](/help/sites-cloud/authoring/assets/publishing-manage-publication-options.png)

1. 按一下 **下一個** 繼續。

1. 在「管理出版物」精靈的下一個步驟中， **範圍**，您可以定義發佈/取消發佈的範圍，例如包含以包含子頁面和/或包含參考。

   ![管理發布範圍](/help/sites-cloud/authoring/assets/publishing-manage-publication-scope.png)

   **新增內容**

   您可以使用「新 **增內容** 」按鈕，在要發佈的頁面清單中新增其他頁面，以防您在啟動「管理出版物」精靈之前未選取其中一個頁面。

   選取 **新增內容** 按鈕會啟動 [路徑瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#path-browser) 允許選取內容。

   選取所需頁面，然後按一下 **選擇** 將內容添加到嚮導或 **取消** 取消選擇並返回嚮導。

   **移除選取項目**

   返回精靈，您可以在清單中選取項目，以從選取項目中移除項目。

   ![管理出版物選擇頁面](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

   **已發佈引用**

   您可以查看和修改要為頁面發佈或取消發佈的參照，方法是選取該參照，然後按一下 **發佈的參考** 按鈕。

   ![管理出版物選項](/help/sites-cloud/authoring/assets/publishing-manage-publication-references.png)

   此 **發佈的參考** 對話框顯示所選內容的參考。 依預設，系統會選取所有欄位，且會發佈/取消發佈，但您可以取消勾選，取消選取這些欄位，以便不會納入動作中。

   按一下 **完成** 儲存變更或 **取消** 取消選擇並返回嚮導。

   回到精靈里， **參考** 欄將會更新，以反映您要發佈或取消發佈的參考選項。

   ![管理出版物選擇頁面](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

   **包含子項**

   >[!NOTE]
   >
   >請參閱 [發佈和取消發佈樹](#publishing-and-unpublishing-a-tree)

   按一下 **包括子項** 開啟對話框，允許您：

   * **包含子系**
   * **僅包含直接子項**
   * **僅包含修改過的頁面**
   * **僅包含已發佈的頁面**

   啟動所需選項並使用確認 **確定** 根據選擇選項將子頁添加到要發佈或取消發佈的頁清單中。 按一下 **取消** 取消選擇並返回嚮導。

   ![管理出版物，包括子項](/help/sites-cloud/authoring/assets/publishing-include-children.png)

1. 按一下 **發佈** 完成。

   在網站主控台中，通知訊息會確認發佈。

1. 如果發佈的頁面與工作流程相關聯，最後可能會顯示 **工作流程** 發佈精靈的步驟。

   ![管理出版物選擇頁面](/help/sites-cloud/authoring/assets/publishing-manage-publication-workflow.png)

   >[!NOTE]
   >
   >此 **工作流程** 步驟將根據您的使用者可能擁有或可能沒有的權限顯示。 請參閱此頁面上有關發佈權限以及管理工作流程存取權限的上一個備注，以及 [將工作流程套用至頁面](/help/sites-cloud/authoring/workflows/applying.md) 以取得詳細資訊。

   資源會依觸發的工作流程分組，而每個指定選項可：

   * 定義工作流程的標題。
   * 保留工作流程套件，前提是工作流程具有多資源支援。
   * 如果選擇了保留工作流包的選項，則定義工作流包的標題。

1. 按一 **下「發佈** 」或「 **稍後發佈** 」以完成出版。

## 取消發佈頁面 {#unpublishing-pages}

取消發佈頁面會從您的發佈中移除該頁面，或 [預覽](/help/sites-cloud/authoring/fundamentals/previewing-content.md)，讓讀者不再能使用。

在 [發佈方式類似](#publishing-pages)，您可以從所需目的地取消發佈一或多個頁面：

* [從頁面編輯器](#unpublishing-from-the-editor)
* [從網站主控台](#unpublishing-from-the-console)

### 從編輯器取消發佈 {#unpublishing-from-the-editor}

編輯頁面時，如果要取消發佈該頁面，請選取 **取消發佈頁面** 在 **頁面資訊** 菜單，就像你 [發佈頁面](#publishing-from-the-editor).

>[!NOTE]
>
>由存取的頁面 [別名](/help/sites-cloud/authoring/fundamentals/page-properties.md#advanced) 無法取消發佈編輯器中的。 編輯器中的發佈選項僅適用於透過其實際路徑存取的頁面。

### 從主控台取消發佈 {#unpublishing-from-the-console}

和你一樣 [使用管理出版物選項進行發佈](#manage-publication)，您也可以使用它來取消發佈。

1. 在網站主控台中選取頁面，然後按一下 **管理出版物** 按鈕。
1. 「管 **理出版物** 」嚮導將啟動。在第一個步驟中， **選項**，選擇「取消發佈」(Unpublish **)，而非「發佈」(Publish)的預設** 選項 ****。

   ![取消發佈 — 選項](/help/sites-cloud/authoring/assets/publishing-unpublish.png)

   就像稍後發佈會啟動工作流程以在指定時間發佈此版本的頁面一樣，稍後停用會啟動工作流程以在特定時間取消發佈選取的頁面或頁面。

   >[!NOTE]
   >
   >如果您想要取消稍後發佈/取消發佈，請前往 [工作流程主控台](/help/sites-cloud/administering/workflows-administering.md#suspending-resuming-and-terminating-a-workflow-instance) 終止相應的工作流。

   >[!NOTE]
   >如果您有 [預覽](/help/sites-cloud/authoring/fundamentals/previewing-content.md) 環境 **目的地** 管理發布期間。

1. 要完成取消發佈，請按照要完成的操作繼續通過嚮導 [發佈頁面](#manage-publication).

   ![取消發佈 — 範圍](/help/sites-cloud/authoring/assets/publishing-unpublish-scope.png)

## 發佈和取消發佈樹 {#publishing-and-unpublishing-a-tree}

當您輸入或更新相當多的內容頁面時（所有頁面都位於相同的根頁面下），在一個動作中發佈整個樹狀結構會較為容易。

您可以使用 [管理出版物](#manage-publication) 選項，以執行此操作。

1. 在網站主控台中，選取您要發佈或取消發佈之樹狀結構的根頁面，然後選取 **管理出版物**.
1. 「管 **理出版物** 」嚮導將啟動。選擇要發佈或取消發佈，以及何時發生，然後選取 **下一個** 繼續。
1. 在 **範圍** 步驟，選取根頁面並選取 **包括子項**.

   ![管理出版物選擇頁面](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

1. 在 **包括子項** 對話框：

   * 選取 **包括子項**
   * 取消選取 **僅包括直系子女**
   * 取消選取 **僅包含已發佈的頁面**
   * 設定 **僅包含已修改的頁面** 必填

   預設會選取這些選項，因此您必須記得加以設定。 使用確認選取項目 **確定** 將內容新增至發佈/取消發佈。

   ![包括用於樹發佈的子項](/help/sites-cloud/authoring/assets/publishing-include-children-tree.png)

1. 在 **管理出版物** 嚮導，您可以通過添加其他頁面或刪除那些選定頁面來進一步自定義選擇。

   請記住，您也可以檢閱要透過 **發佈的參考** 選項。

1. [正常地繼續管理出版物嚮導](#manage-publication) 完成樹的發佈或取消發佈。

## 確定發佈狀態 {#determining-publication-status}

您可以決定頁面的發佈狀態：

* 在 [sites console上的資源概觀資訊](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)

   ![卡片檢視中的發佈狀態](/help/sites-cloud/authoring/assets/publishing-status-console-card.png)

   發佈狀態會顯示在 [網站主控台](/help/sites-cloud/authoring/getting-started/basic-handling.md#card-view)[的卡片](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view)、欄和 [清單檢視中](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view) 。

* 在 [時間表](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)

   ![時間軸視圖中的發佈狀態](/help/sites-cloud/authoring/assets/publishing-status-timeline.png)

* 在 [頁面資訊功能表](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) 編輯頁面時

   ![「頁面資訊」功能表中的發佈狀態](/help/sites-cloud/authoring/assets/publishing-status-page-information.png)
