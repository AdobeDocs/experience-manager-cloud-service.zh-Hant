---
title: 使用任務
description: 任務表示在內容上要完成的工作專案，並用於專案中以決定目前任務的完整度等級
exl-id: 66f95a1f-34d0-4e2e-aa8c-addc2029a1d9
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 10%

---

# 使用任務 {#working-with-tasks}

任務表示要在內容上完成的工作專案。 當您被指派任務時，它會顯示在「工作流程收件匣」中。 任務專案在型別欄中有任務的值。

任務也會用於專案中，以判斷目前任務（包括工作流程任務）的完整程度。

## 追蹤專案進度 {#tracking-project-progress}

您可以透過檢視由&#x200B;**任務**&#x200B;圖磚表示的專案內的作用中/已完成任務來追蹤專案進度。 專案進度可由下列專案決定：

* **&#x200B;**&#x200B;任務表徵圖：項目詳細資訊頁面上的「任務表徵圖」(Task Tile)中描述了項目的整體進度。

* **&#x200B;**&#x200B;任務清單：按一下「任務」表徵圖時，將顯示任務清單。此清單包含與項目相關的所有任務的詳細資訊。

兩者都會列出工作流程任務和您直接在&#x200B;**任務**&#x200B;圖磚中建立的任務。

### 任務拼貼 {#task-tile}

如果專案有任何相關任務，專案內會顯示任務表徵圖。 「任務表徵圖」顯示專案的目前狀態。 這是以工作流程內的現有任務為基礎，不包括未來在工作流程進行時將產生的任何任務。 下列資訊會顯示在「工作」表徵圖中：

* 已完成任務的百分比
* 作用中任務的百分比
* 逾期任務的百分比

![任務拼貼](/help/sites-cloud/authoring/assets/projects-tasks-breakdown.png)

### 檢視或修改專案中的任務 {#viewing-or-modifying-the-tasks-in-a-project}

除了追蹤進度以外，您也可能想要檢視專案的詳細資訊或修改專案。

#### 任務清單 {#task-list}

按一下「任務」方塊中的省略符號(...)，即可顯示與專案相關的任務清單。 任務會依父工作流程劃分。 任務詳細資訊會與中繼資料一起顯示，例如到期日、受指派人、優先順序和狀態。

![工作清單](/help/sites-cloud/authoring/assets/projects-task-list.png)

#### 工作詳細資訊 {#task-details}

如需特定工作的詳細資訊，請在工作清單中，選取工作並&#x200B;**開啟**。

![任務詳細資料](/help/sites-cloud/authoring/assets/projects-task-details.png)

### 檢視和修改工作註解 {#viewing-and-modifying-task-comments}

在「任務」詳細資訊中，您可以編輯或新增註解。 此外，專案中的所有註解都會顯示在「註解」區域中。

![對任務的評論](/help/sites-cloud/authoring/assets/projects-tasks-comments.png)

### 新增任務 {#adding-tasks}

您可以將新任務新增至專案。 然後，這些任務會出現在「任務」表徵圖中，並可在通知收件匣中對其執行操作。

若要新增任務：

1. 在專案中，在&#x200B;**任務**&#x200B;圖磚中，選取+圖示。 將打 **開「添加任務** 」窗口。
1. 輸入工作的相關資訊。 任務的標題及指派給哪個群組是必填欄位。 內容路徑、說明、工作優先順序及到期日等其他資訊為選用。 此外，您可以選取&#x200B;**進階**&#x200B;標籤以輸入工作的名稱，此名稱可用來命名URL。

   ![新增工作](/help/sites-cloud/authoring/assets/projects-add-task.png)

1. 選取「**建立**」。

## 使用收件匣中的任務 {#working-with-tasks-in-the-inbox}

存取任務的另一種方式是從「收件匣」。 從收件匣中，您可以開啟內容以實施必要的變更。 完成後，您會將任務狀態設定為「已完成」。 當任務指派給您所屬的使用者群組時，也會顯示在您的收件匣中。 在這種情況下，群組的所有成員都可以執行工作並完成任務。

收件匣中的![任務](/help/sites-cloud/authoring/assets/projects-task-inbox.png)

若要完成工作，請選取工作並按一下[完成]。**&#x200B;** 新增資訊至工作，然後按一下[完成]。**&#x200B;** 如需詳細資訊，請參閱[您的收件匣](/help/sites-cloud/authoring/inbox.md)。

![任務通知](/help/sites-cloud/authoring/assets/projects-task-notifications.png)
