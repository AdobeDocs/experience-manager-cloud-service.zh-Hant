---
title: 參與工作流程
description: 工作流程通常包含要求人員在頁面或資產上執行活動的步驟。
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
workflow-type: tm+mt
source-wordcount: '1545'
ht-degree: 1%

---


# 參與工作流程 {#participating-in-workflows}

工作流程通常包含要求人員在頁面或資產上執行活動的步驟。 工作流選擇要執行活動的用戶或組，並將工作項目分配給該人員或組。 使用者會收到通知，然後可採取適當的動作：

* [檢視通知](#notifications-of-available-workflow-actions)
* [完成參與者步驟](#completing-a-participant-step)
* [委派參與者步驟](#delegating-a-participant-step)
* [對參與者步驟執行退一步](#performing-step-back-on-a-participant-step)
* [開啟工作流程項目以檢視詳細資訊（並採取動作）](#opening-a-workflow-item-to-view-details-and-take-actions)
* [檢視工作流程裝載（多個資源）](#viewing-the-workflow-payload-multiple-resources)

## 可用工作流程動作的通知 {#notifications-of-available-workflow-actions}

當您被指派工作項目時(例如「核准內 **容**」)，會出現各種警報和/或通知：

* 您的 [通知指示](/help/sites-cloud/authoring/getting-started/inbox.md) （工具列）將會增加：

   ![通知工具列](/help/sites-cloud/authoring/assets/workflows-notifications.png)

* 項目將列在通知收件箱 [中](/help/sites-cloud/authoring/getting-started/inbox.md):

   ![收件匣中的通知](/help/sites-cloud/authoring/assets/workflows-inbox.png)

* 當您使用頁面編輯器時，狀態列會顯示：
   * 應用於頁面的工作流的名稱； 例如，要求啟動。
   * 當前用戶在工作流的當前步驟中可以執行的任何操作； 例如，「完成」(Complete)、「委派」(Delegate)、「查看」(View)詳細資訊。
   * 頁面所受的工作流程數。 您可以：
      * 使用向左／向右箭頭來導覽各種工作流程的狀態資訊。
      * 按一下／點選實際數字，以開啟所有適用工作流程的下拉式清單，然後選取您要顯示在狀態列中的工作流程。

   ![具有多個工作流程的頁面](/help/sites-cloud/authoring/assets/workflows-multiple.png)

   >[!NOTE]
   >
   >狀態列僅對具有工作流權限的用戶可見； 例如，群組的成 `workflow-users` 員。
   >
   >
   >當目前的使用者直接參與工作流程的目前步驟時，會顯示動作。

* 為資 **源開啟** 「時間軸」時，將顯示工作流步驟。 當您按一下／點選警報橫幅時，也會顯示可用的動作：

   ![時間軸中的工作流程](/help/sites-cloud/authoring/assets/workflows-timeline.png)

### 完成參與者步驟 {#completing-a-participant-step}

您可以完成項目，讓工作流程繼續下一個步驟。

在此操作中，您可以指明：

* **下一步**: 下一步； 您可以從提供的清單中選擇
* **評論**: if freed

您可以從以下任一步驟中完成參與者步驟：

* [收件箱](#completing-a-participant-step-inbox)
* [頁面編輯器](#completing-a-participant-step-page-editor)
* [時間軸](#completing-a-participant-step-timeline)
* 開啟 [工作流項以查看詳細資訊時](#opening-a-workflow-item-to-view-details-and-take-actions)。

#### 完成參與者步驟——收件箱 {#completing-a-participant-step-inbox}

請按下列步驟完成工作項目：

1. 開啟 **[AEM收件匣](/help/sites-cloud/authoring/getting-started/inbox.md)**。
1. 選取您要對其採取動作的工作流程項目（點選／按一下縮圖）。
1. 從工 **具列中** ，選擇「完成」。
1. 將會 **開啟「完成工作項** 」對話框。 從下拉 **選取器中選取** 「下一步」，並視需要新增 **「注釋** 」。
1. 使用 **「確定** 」(OK)完成步驟(或使用「取 **消** 」(Cancel)中止操作)。

#### 完成參與者步驟——頁面編輯器 {#completing-a-participant-step-page-editor}

請按下列步驟完成工作項目：

1. 開啟頁 [面進行編輯](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing)。
1. 從頂 **端的** 「狀態列」中選擇「完成」。
1. 將會 **開啟「完成工作項** 」對話框。 從下拉 **選取器中選取** 「下一步」，並視需要新增 **「注釋** 」。
1. 使用 **「確定** 」(OK)完成步驟(或使用「取 **消** 」(Cancel)中止操作)。

#### 完成參與者步驟——時間表 {#completing-a-participant-step-timeline}

您也可以使用時間軸來完成並進行步驟：

1. 選擇所需頁面並開啟 **時間軸** (或開啟 **時間軸** ，然後選取頁面):

   ![完成步驟](/help/sites-cloud/authoring/assets/workflows-timeline-completing.png)

1. 按一下／點選警報橫幅以顯示可用動作。 選擇 **高級**:

   ![推進步驟](/help/sites-cloud/authoring/assets/workflows-timeline-advance.png)

1. 您可以根據工作流程來選擇下一個步驟：

   ![選擇下一步](/help/sites-cloud/authoring/assets/workflows-next-step.png)

1. 選擇「 **高級** 」(Advance)以確認操作。

### 委派參與者步驟 {#delegating-a-participant-step}

如果已指派步驟給您，但由於任何原因您無法採取動作，您可以將步驟委派給其他使用者或群組。

可進行委派的用戶取決於分配了工作項目的人員：

* 如果工作項目已指派給群組，則可使用群組成員。
* 如果工作項目已指派給某個組，然後委託給用戶，則可以使用組成員和組。
* 如果工作項目已指派給單一使用者，則無法委派工作項目。

在此操作中，您可以指明：

* **使用者**: 要委派給的用戶； 您可以從提供的清單中選擇
* **評論**: if freed

您可以從以下任一位置委派參與者步驟：

* [收件箱](#delegating-a-participant-step-inbox)
* [頁面編輯器](#delegating-a-participant-step-page-editor)
* [時間軸](#delegating-a-participant-step-timeline)
* 開啟 [工作流項以查看詳細資訊時](#opening-a-workflow-item-to-view-details-and-take-actions)。

#### 委派參與者步驟——收件箱 {#delegating-a-participant-step-inbox}

使用以下過程來委派工作項目：

1. 開啟 **[AEM收件匣](/help/sites-cloud/authoring/getting-started/inbox.md)**。
1. 選取您要對其採取動作的工作流程項目（點選／按一下縮圖）。
1. 從工 **具欄中** ，選擇「委派」。
1. 對話方塊將會開啟。 從下拉 **選取器** （這也可以是群組）中指定「使用者」，並視需要新 **增「注釋** 」。
1. 使用 **「確定** 」(OK)完成步驟(或使用「取 **消** 」(Cancel)中止操作)。

#### 委派參與者步驟——頁面編輯器 {#delegating-a-participant-step-page-editor}

使用以下過程來委派工作項目：

1. 開啟頁 [面進行編輯](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing)。
1. 從上 **方的狀態列選取** 「委派」。
1. 對話方塊將會開啟。 從下拉 **選取器** （這也可以是群組）中指定「使用者」，並視需要新 **增「注釋** 」。
1. 使用 **「確定** 」(OK)完成步驟(或使用「取 **消** 」(Cancel)中止操作)。

#### 委派參與者步驟——時間軸 {#delegating-a-participant-step-timeline}

您也可以使用時間軸來委派和／或指派步驟：

1. 選擇所需頁面並開啟 **時間軸** (或開啟 **時間軸** ，然後選取頁面)。
1. 按一下／點選警報橫幅以顯示可用動作。 選擇 **變更受託人**:

   ![委派步驟](/help/sites-cloud/authoring/assets/workflows-delegate.png)

1. 指定新的受託人：

   ![變更受託人](/help/sites-cloud/authoring/assets/workflows-assignee.png)

1. 選擇 **「指定** 」以確認操作。

### 對參與者步驟執行退一步 {#performing-step-back-on-a-participant-step}

如果您發現需要重複某個步驟或一系列步驟，則可退後一步。 這可讓您選取在工作流程中較早發生的步驟，以進行重新處理。 工作流程會返回您指定的步驟，然後繼續進行。

在此操作中，您可以指明：

* **上一步**: 返回的步驟； 您可以從提供的清單中選擇
* **評論**: if freed

您可以從以下任一位置對參與者執行退一步：

* [收件箱](#performing-step-back-on-a-participant-step-inbox)
* [頁面編輯器](#performing-step-back-on-a-participant-step-page-editor)
* [時間軸](#performing-step-back-on-a-participant-step-timeline)
* 開啟 [工作流項以查看詳細資訊時](#opening-a-workflow-item-to-view-details-and-take-actions)。

#### 對參與者步驟執行退回——收件箱 {#performing-step-back-on-a-participant-step-inbox}

請按下列步驟退一步：

1. 開啟 **[AEM收件匣](/help/sites-cloud/authoring/getting-started/inbox.md)**。
1. 選取您要對其採取動作的工作流程項目（點選／按一下縮圖）。
1. 選擇「 **後退** 」以開啟對話框。
1. 指定「上 **一個步驟** 」，並視需要 **新增「注釋** 」。
1. 使用 **「確定** 」(OK)完成步驟(或使用「取 **消** 」(Cancel)中止操作)。

#### 對參與者步驟執行退一步——頁面編輯器 {#performing-step-back-on-a-participant-step-page-editor}

請按下列步驟退一步：

1. 開啟頁 [面進行編輯](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing)。
1. 從頂 **部的狀態列選擇** 「後退」(Step Back)。
1. 指定「上 **一個步驟** 」，並視需要 **新增「注釋** 」。
1. 使用 **「確定** 」(OK)完成步驟(或使用「取 **消** 」(Cancel)中止操作)。

#### 對參與者步驟執行後退——時間軸 {#performing-step-back-on-a-participant-step-timeline}

您也可以使用時間軸來回滾（步驟）回到上一個步驟：

1. 選擇所需頁面並開啟 **時間軸** (或開啟 **時間軸** ，然後選取頁面)。
1. 按一下／點選警報橫幅以顯示可用動作。 選擇 **回滾**:

   ![回退步驟](/help/sites-cloud/authoring/assets/workflows-roll-back.png)

1. 指定工作流應返回的步驟：

   ![指定步驟](/help/sites-cloud/authoring/assets/workflows-roll-back-step.png)

1. 選擇「 **回滾** 」以確認操作。

### 開啟工作流項以查看詳細資訊（並採取操作） {#opening-a-workflow-item-to-view-details-and-take-actions}

查看工作流工作項目的詳細資訊並採取相應的操作。

工作流詳細資訊顯示在頁籤中，工具欄中提供了相應的操作：

* **「工作項目** 」頁籤：

   ![「工作項目」頁籤](/help/sites-cloud/authoring/assets/workflows-work-item.png)

* **「工作流資訊** 」頁籤：

   ![「工作流」頁籤](/help/sites-cloud/authoring/assets/workflows-workflow-info.png)

   如果已為模型配置了「工作流階段」，則可以根據以下內容查看進度： <!--If [Workflow Stages](/help/sites-developing/workflows.md#workflow-stages) have been configured for the model, you can view the progress according to these:-->

   ![工作流程階段](/help/sites-cloud/authoring/assets/workflows-workflow-stages.png)

* **「注釋** 」頁籤：

   ![「注釋」頁籤](/help/sites-cloud/authoring/assets/workflows-comments.png)

您可以從以下任一位置開啟工作項目詳細資訊：

* [收件箱](#performing-step-back-on-a-participant-step-inbox)
* [頁面編輯器](#performing-step-back-on-a-participant-step-page-editor)

#### 開啟工作流詳細資訊——收件箱 {#opening-workflow-details-inbox}

要開啟工作流項並查看詳細資訊，請執行以下操作：

1. 開啟 **[AEM收件匣](/help/sites-cloud/authoring/getting-started/inbox.md)**。
1. 選取您要對其採取動作的工作流程項目（點選／按一下縮圖）。
1. 選擇「 **開啟** 」以開啟資訊標籤。
1. 如果需要，請選擇相應的操作，提供任何詳細資訊，然後使用「確定」( **OK** )(或「取 **消」**)進行確認。
1. 使用 **「儲存** 」或「 **取消** 」退出。

#### 開啟工作流詳細資訊——頁面編輯器 {#opening-workflow-details-page-editor}

要開啟工作流項並查看詳細資訊，請執行以下操作：

1. 開啟頁 [面進行編輯](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing)。
1. 從狀 **態欄中選擇** 「查看詳細資訊」以開啟資訊頁籤。
1. 如果需要，請選擇相應的操作，提供任何詳細資訊，然後使用「確定」( **OK** )(或「取 **消」**)進行確認。
1. 使用 **「儲存** 」或「 **取消** 」退出。

### 檢視工作流程裝載（多個資源） {#viewing-the-workflow-payload-multiple-resources}

您可以檢視與工作流程例項相關聯之裝載的詳細資料。 一開始會顯示套件中的資源，然後您可以下鑽以顯示個別頁面。

要查看工作流實例的裝載和資源，請執行以下操作：

1. 開啟 **[AEM收件匣](/help/sites-cloud/authoring/getting-started/inbox.md)**。
1. 選取您要對其採取動作的工作流程項目（點選／按一下縮圖）。
1. 從工 **具列選擇** 「檢視裝載」，以開啟對話方塊。
   * 由於工作流包只是儲存庫中路徑的指針的集合，因此您可以在此處添加／刪除／修改條目以調整工作流包引用的內容。 使用「資 **源定義** 」元件添加新條目。
1. 這些連結可用來開啟個別頁面。
