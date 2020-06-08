---
title: 發佈頁面
description: 如何使用AEM發佈和取消發佈頁面
translation-type: tm+mt
source-git-commit: f04dd39a5a22f44f976f2e473689780099f10f9a
workflow-type: tm+mt
source-wordcount: '1694'
ht-degree: 7%

---


# 發佈頁面 {#publishing-pages}

在您建立並檢視內容至作者環境後，其目的 [是讓內容可在您的公開網站](/help/sites-cloud/authoring/getting-started/concepts.md) （您的發佈環境）上使用。

這稱為發佈頁面。 當您想從發佈環境中移除頁面時，稱為取消發佈。 發佈和取消發佈頁面時，在作者環境中仍可使用頁面進行進一步變更，直到您刪除為止。

您可以立即發佈／取消發佈頁面，或在未來的預先定義日期／時間發佈／取消發佈頁面。

## 術語 {#terminology}

當您使用AEM時，可能會遇到與發佈相關的不同詞語。

* **發佈／取消發佈**
   * 這些是讓您的內容在發佈環境（或非）上公開提供之動作的主要條款。
   * 這些是AEM檔案中使用的詞語。
* **啟用／停用**
   * 這些詞語與publish/unpublish同義。
   * 這些詞語已用於舊版AEM。
* **複製／複製**
   * 這些技術術語描述了在您發佈頁面時，資料在一個環境之間的移動（例如頁面內容、檔案、程式碼、使用者註解）。
   * 這些術語主要供開發人員使用。

## 發佈頁面 {#publishing-pages-1}

視您的位置而定，您可以發佈：

* [從頁面編輯器](#publishing-from-the-editor)
* [從站點控制台](#publishing-from-the-console)

>[!NOTE]
>
>如果您沒有發佈特定頁面的必要權限：
>
>* 系統會觸發工作流程，通知您發佈請求的適當人員。
>* 您的開發團隊可能已自訂此工作流程。
>* 系統會短暫顯示訊息，通知您工作流程已觸發。


<!--
>* This [workflow may have been customized](/help/sites-developing/workflows-models.md#main-pars-procedure-6fe6) by your development team.
>* A message will be displayed briefly to notify you that the workflow was triggered.
-->

### 從編輯器發佈 {#publishing-from-the-editor}

如果您正在編輯頁面，則可直接從編輯器發佈頁面。

1. 選取「 **頁面資訊** 」圖示以開啟功能表，然後選 **取「發佈頁面** 」選項。

   ![透過頁面選項發佈頁面](/help/sites-cloud/authoring/assets/publishing-page-options.png)

1. 視頁面是否有需要發佈的參考而定：

   * 如果沒有要發佈的參考，頁面將直接發佈。
   * 如果頁面有需要發佈的參考，這些參考將列在「發 **布** 」精靈中，您可以在其中：
      * 指定哪些資產／標籤／等。 您想要與頁面一起發佈，然後使用「 **發佈** 」完成程式。
      * Use **Cancel** to abort the action.
   ![發佈頁面的參考](/help/sites-cloud/authoring/assets/publishing-references.png)

1. 選取 **「發佈** 」會將頁面複製至發佈環境。 在頁面編輯器中，會顯示確認發佈動作的資訊橫幅。

   ![發佈狀態資訊橫幅](/help/sites-cloud/authoring/assets/publishing-info.png)

   在控制台中查看相同頁面時，更新的發佈狀態可見。

   ![站點控制台中列視圖中的頁面發佈狀態](/help/sites-cloud/authoring/assets/publishing-status-console-column.png)

>[!NOTE]
>
>從編輯器發佈是淺層發佈，即僅發佈選定的頁面／頁面，而任何子頁面是／不是。

### 從主控台發佈 {#publishing-from-the-console}

在網站主控台中，有兩種發佈選項：

* [快速發佈](#quick-publish)
* [管理發佈](#manage-publication)

#### 快速發佈 {#quick-publish}

**「快速發佈** 」適用於簡單的情況，並立即發佈選取的頁面，而不需進行任何進一步的互動。 因此，任何未發佈的參考也會自動發佈。

若要使用「快速發佈」來發佈頁面：

1. 在網站主控台中選取頁面或頁面，然後按一下「快速 **發佈** 」按鈕。

   ![選擇發佈頁面](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. 在「快速發佈」對話方塊中，按一下「發佈」以確認出版物，或按一 **下** 「取消」以 **取消出版物**。 請記住，任何未發佈的參考也會自動發佈。

   ![快速發佈確認](/help/sites-cloud/authoring/assets/publishing-quick-publish.png)

1. 發佈頁面時，會顯示確認發佈的警報。

>[!NOTE]
>
>「快速發佈」是淺層發佈，即僅會發佈所選頁面／頁面，且未發佈任何子頁面。

#### 管理發佈 {#manage-publication}

**「管理出版物** 」提供的選項比「快速發佈」更多，允許包含子頁面、自訂參照、啟動任何適用的工作流程，以及提供稍後發佈的選項。

若要使用「管理出版物」來發佈或取消發佈頁面：

1. 在站點控制台中選擇頁或頁，然後按一下「管理 **出版物** 」按鈕。

   ![選擇發佈頁面](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. 「管 **理出版物** 」嚮導將啟動。第一個步驟 **Options**&#x200B;可讓您：

   * 選擇發佈或取消發佈所選頁面。
   * 選擇立即或稍後採取該動作。
   稍後發佈會啟動工作流程，以在指定時間發佈選取的頁面。 相反地，稍後取消發佈會啟動工作流程，在特定時間取消發佈選取的頁面。

   如果您想稍後取消發佈／取消發佈，請前往「工作流程控制台」以終止對應的工作流程。 <!--If you want to cancel a publish/unpublish later, go to the [Workflow Console](/help/sites-administering/workflows.md) to terminate the corresponding workflow.-->

   ![管理出版物選項](/help/sites-cloud/authoring/assets/publishing-manage-publication-options.png)

   按一 **下** 「下一步」繼續。

1. 在「管理出版物」嚮導的下一個步驟 **Scope**，您可以定義出版物／取消出版物的範圍，例如包含子頁面和／或包含引用。

   ![管理出版物範圍](/help/sites-cloud/authoring/assets/publishing-manage-publication-scope.png)

   您可以使用「新 **增內容** 」按鈕，在要發佈的頁面清單中新增其他頁面，以防您在啟動「管理出版物」精靈之前未選取其中一個頁面。

   按一下「新增內容」按鈕會啟動路 [徑瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#path-browser) ，以允許選取內容。

   選擇所需頁面，然後按一下「 **Select** （選擇）」將內容添加到嚮導中，或按一下「**Cancel **」取消選擇並返回嚮導。

   回到精靈中，您可以選取清單中的項目，以設定其他選項，例如：

   * 包括其子系。
   * 從選取範圍中移除它。
   * 管理其已發佈的參考。
   ![管理出版物選擇頁面](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

   按一下 **「包括子項** 」(Include Children)將開啟一個對話框，允許您：

   * 僅包含直接子項.
   * 僅包含修改過的頁面.
   * 僅包含已發佈的頁面.
   按一 **下「新增** 」，根據選取選項，將子頁面新增至要發佈或未發佈的頁面清單。 按一下 **取消** ，取消選擇並返回嚮導。

   ![管理出版物，包括子系](/help/sites-cloud/authoring/assets/publishing-include-children.png)

   返回到嚮導時，您會根據您在「包含子項」對話框中選擇的選項看到添加的頁。

   您可以通過選擇某個頁面，然後按一下「已發佈參照」(Published References)按鈕，來查看和修改要發佈或未發佈該頁面 **的參照** 。

   ![管理出版物選項](/help/sites-cloud/authoring/assets/publishing-manage-publication-references.png)

   「發 **布參照** 」(Published References)對話框顯示所選內容的參照。 依預設，這些檔案都已選取，而且會發佈／取消發佈，但您可以取消勾選以取消選取這些檔案，以便不包含在動作中。

   單 **擊「完成** 」保存更改，或按一下「取 **消** 」取消選擇並返回嚮導。

   回到精靈中，「參 **考」欄將會更新** ，以反映您選取要發佈或未發佈的參考。

   ![管理出版物選擇頁面](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

1. 按一 **下「發佈** 」以完成。

   在站點控制台中，通知消息將確認發佈。

1. 如果已發佈頁面與工作流程相關聯，則可能會顯示在出版物精靈的最 **後「工作流** 」步驟中。

   >[!NOTE]
   >
   >「工 **作流程** 」步驟將根據您的使用者可能擁有或可能沒有的權限顯示。 如需詳細資訊，請參閱本頁上面的有關發佈權限以及管理工作流程存取權 [和套用工作流程](/help/sites-cloud/authoring/workflows/applying.md) 。
   <!--
   >The **Workflows** step will be shown based on what rights your user may or may not have. See the previous note on this page regarding publishing privileges as well as [Managing Access to Workflows](/help/sites-administering/workflows-managing.md) and [Applying Workflows to Pages](/help/sites-cloud/authoring/workflows/applying.md) for details.
   -->

   資源會依觸發的工作流程和每個指定選項分組，以：

   * 定義工作流的標題。
   * 保留工作流包，前提是工作流支援多資源。
   <!--Keep the workflow package, provided that the workflow has [multi-resource support](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support).
    -->

   * 如果選擇了保留工作流包的選項，則定義工作流包的標題。
   按一 **下「發佈** 」或「 **稍後發佈** 」以完成出版。

## 取消發佈頁面 {#unpublishing-pages}

取消發佈頁面會將其從您的發佈環境中移除，如此讀者就無法再使用它。

以類 [似發佈的方式](#publishing-pages)，可以取消發佈一或多個頁面：

* [從頁面編輯器](#unpublishing-from-the-editor)
* [從站點控制台](#unpublishing-from-the-console)

### 從編輯器取消發佈 {#unpublishing-from-the-editor}

編輯頁面時，如果您想要解除發佈該頁面，請在「頁面資訊」功能表中選取「解除發佈頁面 **」(Unpublish Page** )，就像您發 **布頁面一樣**[](#publishing-from-the-editor)。

### 從主控台取消發佈 {#unpublishing-from-the-console}

就像您使 [用「管理出版物」選項發佈](#manage-publication)，您也可以使用它取消發佈。

1. 在站點控制台中選擇頁或頁，然後按一下「管理 **出版物** 」按鈕。
1. 「管 **理出版物** 」嚮導將啟動。在第一個步驟中， **選項**，選擇「取消發佈」(Unpublish **)，而非「發佈」(Publish)的預設** 選項 ****。

   ![取消發佈](/help/sites-cloud/authoring/assets/publishing-unpublish.png)

   就像稍後發佈會啟動工作流程以在指定時間發佈此版本的頁面一樣，稍後停用會啟動工作流程以在特定時間解除發佈選取的頁面。

   如果您想稍後取消發佈／取消發佈，請前往「工作流程控制台」以終止對應的工作流程。 <!--If you want to cancel a publish/unpublish later, go to the [Workflow Console](/help/sites-administering/workflows.md) to terminate the corresponding workflow.-->

1. 要完成取消發佈，請繼續執行嚮導，如同發 [布頁面一樣](#manage-publication)。

## 發佈和取消發佈樹狀結構 {#publishing-and-unpublishing-a-tree}

當您輸入或更新大量內容頁面（所有頁面都位於相同的根頁面下）時，在單一動作中發佈整個樹狀結構會比較容易。

您可以使用站 [點控制台上的](#manage-publication) 「管理出版物」選項來執行此操作。

1. 在站點控制台中，選擇要發佈或取消發佈的樹的根頁面，然後選擇「管 **理出版物」**。
1. 「管 **理出版物** 」嚮導將啟動。選擇發佈或取消發佈，並選擇「下一步」以繼 **續** 。
1. 在「范 **圍** 」步驟中，選擇根頁面，然後選擇「包 **含子項」**。

   ![管理出版物選擇頁面](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

1. 在「包 **含子項** 」對話方塊中，取消勾選選項：

   * 僅包含直接子項
   * 僅包含已發佈的頁面
   這些選項預設為選取，因此您必須記得取消選取。 按一 **下「新增** 」以確認內容並將內容新增至出版物／取消出版物。

   ![取消發佈時包含子項](/help/sites-cloud/authoring/assets/publishing-tree-children.png)

1. 「管 **理出版物** 」嚮導列出要查看的樹的內容。 您可以新增其他頁面或移除選取的頁面，進一步自訂選取範圍。

   ![管理出版物選項](/help/sites-cloud/authoring/assets/publishing-tree-select.png)

   請記住，您也可以查看要通過「已發佈參照」(Published References)選項發 **布的參照** 。

1. [按正常方式繼續「管理出版物」嚮導](#manage-publication) ，以完成樹的出版物或取消出版物。

## 確定發佈狀態 {#determining-publication-status}

您可以決定頁面的發佈狀態：

* 在站點 [控制台上的資源概述資訊中](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)

   ![卡片檢視中的出版物狀態](/help/sites-cloud/authoring/assets/publishing-status-console-card.png)

   發佈狀態會顯示在 [網站主控台](/help/sites-cloud/authoring/getting-started/basic-handling.md#card-view)[的卡片](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view)、欄和 [清單檢視中](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view) 。

* 在時間軸 [中](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)

   ![時間軸檢視中的出版物狀態](/help/sites-cloud/authoring/assets/publishing-status-timeline.png)

* 編輯頁 [面時在「頁面資訊](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) 」功能表中

   ![「頁面資訊」功能表中的出版物狀態](/help/sites-cloud/authoring/assets/publishing-status-page-information.png)
