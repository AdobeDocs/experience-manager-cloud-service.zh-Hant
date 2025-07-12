---
title: 還原先前部署的Source程式碼
description: 瞭解如何將環境還原至其上次成功建置的&amp；ndash；不需要執行管道。
feature: Operations
role: Admin
badge: label="英文字母" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket"
source-git-commit: ae90f527d398af40cf9e6963d2e27de3368f2e8f
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 4%

---

# 還原先前在AEM as a Cloud Service中部署的原始程式碼 {#restore-previous-code-deployed}

>[!NOTE]
>
>&#x200B;>本文所述的功能只能透過早期採用者Alpha程式取得。 若要註冊Alpha，請參閱管道部署的[一鍵回覆](/help/implementing/cloud-manager/release-notes/current.md##one-click-rollback)。

使用&#x200B;**還原先前部署的程式碼**，將環境立即復原到其上次成功的組建 — 不需要執行管道。

您只要開啟所選環境的![更多圖示或省略符號選單圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)選單，並選擇&#x200B;**還原** > **先前部署程式碼**&#x200B;即可回覆最近部署的原始程式碼（以秒為單位）。

>[!TIP]
>
>您可以在&#x200B;**一般**&#x200B;標籤下方的環境詳細資料檢視中，檢視使用中的原始程式碼版本。 檢視[檢視環境的詳細資料](/help/implementing/cloud-manager/manage-environments.md#viewing-environment)。
>
>![使用中的Source程式碼版本](/help/operations/assets/environments-view-details-sourcecodeversion.png)

**還原先前部署的程式碼**&#x200B;功能只有在以下&#x200B;**every**&#x200B;條件為true時才可供使用：

* 您擁有&#x200B;**環境還原建立**&#x200B;許可權。 如需管理許可權的詳細資訊，請參閱[自訂許可權](/help/implementing/cloud-manager/custom-permissions.md)。
* 您的組織已註冊早期採用者計畫，且功能標幟已開啟。
* 程式會在&#x200B;**AEM as a Cloud Service**&#x200B;上執行。
* 選擇的環境是&#x200B;**開發**&#x200B;環境(暫時的Alpha限制)。
* 該環境的最後一個管道已於&#x200B;**成功**&#x200B;完成，並在&#x200B;**少於10天**&#x200B;前執行。
* 環境狀態為&#x200B;**正在執行**，而且沒有管道正在進行中。
* 您要還原的目標原始程式碼版本已在30天內&#x200B;**部署**。

如果任何檢查失敗，Cloud Manager會開啟下列對話方塊，其中列出一或多個未滿足的條件，並停用&#x200B;**Confirm**，以防止還原。

![還原先前程式碼部署失敗對話方塊](/help/operations/assets/restore-previous-code-deployment-not-allowed.png)。

如果您只想將已遺失、損壞或意外刪除的資料還原至其原始狀態，您可以使用[在AEM as a Cloud Service中還原內容](/help/operations/restore.md)。 此還原程式只會影響內容，而不會變更您的原始程式碼和AEM版本。

**若要還原先前部署的程式碼：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 按一下要啟動還原的程式。

1. 透過執行下列操作之一，列出該計畫的所有環境：

   * 從左側功能表的&#x200B;**服務**&#x200B;下方，按一下![資料圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **環境**。

     ![「環境」索引標籤](assets/environments-1.png)

   * 從左側功能表的&#x200B;**程式**&#x200B;下方，按一下&#x200B;**總覽**，然後從&#x200B;**環境**&#x200B;卡片，按一下![工作流程圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) **全部顯示**。

     ![顯示全部選項](assets/environments-2.png)

     >[!NOTE]
     >
     >**環境**&#x200B;卡僅列出三個環境。 按一下卡片中的[顯示全部&#x200B;**]以檢視程式的**&#x200B;全部&#x200B;*環境。*

1. 在「環境」表格中，在您要還原其原始程式碼的環境右側，按一下![更多圖示或省略符號選單圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)，然後按一下&#x200B;**還原** > **先前已部署程式碼**。

   ![從省略符號選單還原先前部署的程式碼選項](/help/operations/assets/restore-previous-code-deployed-menu.png)

1. 在&#x200B;**還原先前部署的程式碼**&#x200B;對話方塊中，檢閱目前部署的版本以及您要還原的版本，然後按一下&#x200B;**確認**。

   ![還原先前部署的程式碼對話方塊](/help/operations/assets/restore-previous-code-deployed-dialogbox.png)

1. Cloud Manager將環境復原到先前的組建、保持內容和設定不變，並在環境頁面上標示環境&#x200B;**正在還原**，直到部署完成。

   ![正在還原啟用](/help/operations/assets/restore-previous-code-deployed-restoring.png)
