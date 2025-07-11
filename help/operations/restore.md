---
title: 在AEM as a Cloud Service中還原內容
description: 瞭解如何使用 Cloud Manager 從備份中還原 AEM as a Cloud Service 內容。
exl-id: 921d0c5d-5c29-4614-ad4b-187b96518d1f
feature: Operations
role: Admin
source-git-commit: 3aff6beda8bcafc884c46ffdc55c530d581543e4
workflow-type: tm+mt
source-wordcount: '1359'
ht-degree: 29%

---


# 在AEM as a Cloud Service中還原內容 {#content-restore}

您可以使用Cloud Manager從備份中還原AEM as a Cloud Service內容。

## 概觀 {#overview}

Cloud Manager 的自助還原程式會從 Adobe 系統備份中複製資料，並將其還原到其原始環境。 執行還原以將已遺失、損壞或意外刪除的資料恢復至其原始狀態。

還原程式只會影響內容，而不會變更您的程式碼和 AEM 版本。 您可以隨時啟動個別環境的還原操作。 （如果您需要以簡單快速的方式還原先前部署的原始程式碼，而不需要啟動新的管道執行，則可以使用[還原先前部署的程式碼](/help/operations/restore-previous-code-deployed.md)）。

Cloud Manager 提供兩種型別的備份，您可以從中還原內容。

* **時間點(PIT)：**&#x200B;此選項會還原過去24小時內擷取的連續備份。
* **上週：** 此型別在過去七天內從系統備份還原，但前 24 小 時除外。

在這兩種情況下，您的自訂程式碼版本和 AEM 版本會維持不變。

>[!TIP]
>
>也可以使用公用API[還原備份](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/)。

>[!WARNING]
>
>* 只有在程式碼或內容發生嚴重問題時，才應使用此功能。
>* 還原備份會刪除在該備份之後新增的任何資料。 測試環境也會回覆成先前的版本。
>* 在起始內容還原作業之前，請先考慮其他選擇性內容還原選項。

## 選擇性內容還原選項 {#selective-options}

在還原至完整內容還原之前，請考慮以下選項以更輕鬆地還原您的內容。

* 如果已刪除路徑的封裝可用，請使用[封裝管理員](/help/implementing/developing/tools/package-manager.md)再次安裝封裝。
* 如果刪除的路徑是Sites中的頁面，請使用[還原樹狀結構功能](/help/sites-cloud/authoring/sites-console/page-versions.md)。
* 如果刪除的路徑是資產資料夾，且原始檔案可供使用，請透過[Assets主控台](/help/assets/add-assets.md)重新上傳。
* 如果刪除內容為資產，請考慮還原[資產的舊版本](/help/assets/manage-digital-assets.md)。

如果上述選項都無法運作，且已刪除路徑的內容很重要，請依下列各節所述執行內容還原。

## 建立使用者角色 {#user-role}

依預設，沒有任何使用者擁有在開發、生產或測試環境中執行內容還原的許可權。 若要將此許可權委派給特定使用者或群組，請使用以下一般步驟。

1. 以表示式名稱建立產品描述檔，該名稱是指內容復原。
1. 提供必要程式的&#x200B;**程式存取**&#x200B;許可權。
1. 根據您的使用案例，提供程式所需環境或所有環境的&#x200B;**環境還原建立**&#x200B;許可權。
1. 將使用者指派給該設定檔。

如需管理許可權的詳細資訊，請參閱[自訂許可權](/help/implementing/cloud-manager/custom-permissions.md)。

## 還原環境的內容 {#restoring-content}

>[!NOTE]
>
>使用者必須有[適當的許可權](#user-role)，才能起始還原作業。

**若要還原環境的內容：**

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

1. 在「環境」表格中，在您要還原其內容的環境右側，按一下![更多圖示或省略符號選單圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)，然後按一下&#x200B;**還原內容**。

   ![從省略符號選單還原內容選項](/help/operations/assets/environments-ellipsis-menu.png)

1. 在環境頁面的&#x200B;**還原內容**&#x200B;標籤上，在&#x200B;**還原時間**&#x200B;下拉式清單中，選取還原的時間範圍。

   ![還原環境的內容標籤](/help/operations/assets/environments-content-restore-tab.png)

   * 如果您在相鄰的&#x200B;**時間**&#x200B;欄位中選擇&#x200B;**過去24小時**，請指定過去24小時內的確切時間來還原。
   * 如果您在相鄰的&#x200B;**天**&#x200B;欄位中選擇&#x200B;**上週**，請選取過去七天內的日期（不包括之前的24小時）。

1. 選取日期或指定時間後，以下&#x200B;**可用備份**&#x200B;部份會顯示可還原的可用備份清單

1. 按一下備份旁的![資訊圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg)，檢視其程式碼版本和AEM版本，然後在選取備份之前，先權衡還原的影響（請參閱[選擇正確的備份](#choosing-backup)）。

   ![備份資訊](assets/backup-info.png)

   針對還原選項顯示的時間戳記是以使用者的電腦時區為基礎。

1. 在代表您要還原之備份的資料列右端，按一下![旋轉CCW粗體，或按一下[還原]](https://spectrum.adobe.com/static/icons/workflow_18/Smock_RotateCCWBold_18_N.svg)以開始還原程式。

1. 檢閱&#x200B;**還原內容**&#x200B;對話方塊中的詳細資料，然後按一下&#x200B;**還原**。

   ![確認還原](assets/backup-restore.png)

備份程式已啟動。 您可以在&#x200B;**[還原活動](#restore-activity)**&#x200B;清單中檢視其狀態。 完成還原操作所需的時間取決於要還原的內容的大小和設定檔。

還原成功完成時，環境會執行下列動作：

* 執行與起始還原操作時相同的程式碼和AEM版本。
* 它具有所選快照的時間戳記中可用的相同內容，而且會重建索引以符合目前的程式碼。

## 選擇正確的備份 {#choosing-backup}

Cloud Manager 的自助式還原程式只會將內容還原到 AEM。 因此，您必須仔細考慮在所需的還原點與目前時間之間進行的程式碼變更。 檢閱目前認可ID與要還原之認可ID之間的認可歷史記錄。

有幾種情況。

* 環境自訂程式碼和還原位於相同的存放庫和相同分支。
* 環境自訂程式碼和還原會共用一個存放庫、使用單獨的分支，並源自共同認可。
* 環境自訂計畫碼和還原位於不同的存放庫中。
   * 在此情況下，不會顯示認可ID。
   * Adobe強烈建議您複製兩個存放庫，並使用差異工具來比較分支。

此外，請記住，還原可能會導致您的生產和測試環境失去同步。 還原內容的後果由您負責。

## 還原活動 {#restore-activity}

**還原活動**&#x200B;清單顯示最近十個還原要求的狀態，包括任何使用中的還原操作。

![還原活動](assets/backup-activity.png)

按一下![資訊圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg)進行備份，即可下載該備份的記錄檔，並檢查程式碼詳細資訊，包括啟動還原時快照集與資料之間的差異。

## 異地備份 {#offsite-backup}

定期備份涵蓋 AEM Cloud Service 中意外刪除或技術故障的風險，但區域故障可能會帶來其他風險。 除了可用性外，這類地區中斷的最大風險是資料遺失。

AEM as a Cloud Service可降低所有AEM生產環境的這項風險。 也就是說，它會持續將所有AEM內容複製到遠端區域。 此程式會讓內容在三個月內可用於復原。 此功能稱為異地備份。

AEM服務可靠性工程在資料區域中斷期間，從站外備份還原中繼和生產AEM Cloud Service環境。

## 限制 {#limitations}

自助還原機制的使用受下列限制。

* 還原作業限制為七天，這表示無法還原超過七天的快照。
* 每個日曆月，一個計畫中的所有環境最多允許 10 次成功還原。
* 環境建立後，需要六個小時才能建立第一個備份快照。 在建立此快照之前，無法對環境執行還原。
* 如果環境目前正在執行完整棧疊或Web層設定管道，則不會起始還原操作。
* 如果同一環境中已執行另一個還原，則無法啟動還原。
* 在極少數的情況下，由於備份時間限制為 24 小時/ 7 天選取的備份可能會因為選取備份到啟動還原之間的延遲而變得無法使用。
* 已刪除環境中的資料會永久遺失且無法復原。
