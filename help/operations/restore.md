---
title: 將內容還原為 AEM 的雲端服務
description: 瞭解如何使用 Cloud Manager 從備份中還原 AEM as a Cloud Service 內容。
exl-id: 921d0c5d-5c29-4614-ad4b-187b96518d1f
feature: Operations
role: Admin
source-git-commit: e6bd71cc56db766fcbab3a925baabb5901c97ee8
workflow-type: tm+mt
source-wordcount: '1610'
ht-degree: 25%

---


# 在 AEM 中還原內容作為雲端服務 {#content-restore}

你可以使用 Cloud Manager 從備份還原 AEM as a Cloud Service 的內容。



Cloud Manager 的自助還原程式會從 Adobe 系統備份中複製資料，並將其還原到其原始環境。 執行還原以將已遺失、損壞或意外刪除的資料恢復至其原始狀態。

還原程式只會影響內容，而不會變更您的程式碼和 AEM 版本。 您可以隨時啟動個別環境的還原操作。

如果你需要以簡單快速的方式還原先前部署的原始碼，且不需要重新執行管線，可以使用 [「還原先前部署](/help/operations/restore-previous-code-deployed.md)的程式碼」。

Cloud Manager 提供兩種型別的備份，您可以從中還原內容。

* **時間點（Point-In-Time，PIT）：** 此選項可恢復過去 24 小時內擷取的連續備份。
* **上週：** 此型別在過去七天內從系統備份還原，但前 24 小 時除外。

在這兩種情況下，您的自訂程式碼版本和 AEM 版本會維持不變。

>[!TIP]
>
>也可以使用公開 API[&#x200B; 還原備份](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/)。

>[!WARNING]
>
>* 此功能僅在程式碼或內容出現嚴重問題時使用。
>* 還原備份會刪除備份後新增的資料。 舞台設定也會回復到之前的版本。
>* 在啟動內容恢復前，請考慮其他選擇性的內容恢復選項。

## 選擇性內容還原選項 {#selective-options}

在進行完整內容還原前，請考慮以下選項，讓內容更輕鬆地恢復。

* 如果有已刪除路徑的套件可用，請使用 [套件管理器](/help/implementing/developing/tools/package-manager.md)重新安裝該套件。
* 如果刪除的路徑是網站中的頁面，請使用 [還原樹功能](/help/sites-cloud/authoring/sites-console/page-versions.md)。
* 如果刪除的路徑是資產資料夾，且原始檔案還在，請透過 [資產主控台](/help/assets/add-assets.md)重新上傳。
* 如果刪除的內容是資產，考慮 [還原資產的舊版本](/help/assets/manage-digital-assets.md)。

如果上述選項都無效，且刪除路徑的內容重要，請依以下章節詳細進行內容還原。

## 建立使用者角色 {#user-role}

預設情況下，沒有使用者有權限在開發、生產或暫存環境中執行內容還原。 若要將此權限委派給特定使用者或群組，請遵循以下一般步驟。

1. 建立一個帶有表達性名稱的產品檔案，並以內容修復為主題。
1. 提供 **所需程式存取** 權限。
1. 根據你的使用情境，提供 **所需的環境或程式所有環境的環境還原建立** 權限。
1. 將使用者分配到該設定檔。

有關權限管理的詳細資訊，請參見 [自訂權限](/help/implementing/cloud-manager/custom-permissions.md)。

## 恢復環境內容 {#restoring-content}

>[!NOTE]
>
>使用者必須擁有 [適當的權限](#user-role) 才能啟動還原操作。

**要恢復環境內容：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 點擊你想要啟動還原的程式。

1. 請透過以下其中一項方式列出所有程式環境：

   * 在左側選單中，在服務&#x200B;**區**&#x200B;點選![「資料圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg)**環境**」。

     ![「環境」索引標籤](assets/environments-1.png)

   * 從左側選單，在程式下方&#x200B;**點選**&#x200B;總覽&#x200B;**，然後從**&#x200B;環境&#x200B;**卡點選**&#x200B;工作流程圖示![](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg)「全部顯示」。**&#x200B;**

     ![顯示全部選項](assets/environments-2.png)

     >[!NOTE]
     >
     >**環境**&#x200B;卡只列出三個環境。點擊 **卡片中的「** 全部顯示」即可查看 *程式的所有* 環境。

1. 在 Environments 表格中，在你想還原內容的環境右側，點選 ![更多圖示或省略號選單圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)，然後點選 **還原內容**。

   ![從省略號選單中還原內容的選項](/help/operations/assets/environments-ellipsis-menu.png)

1. 在 **環境頁面的「還原內容** 」標籤中，「 **還原** 時間」下拉選單，選擇還原的時間範圍。

   ![環境的還原內容標籤](/help/operations/assets/environments-content-restore-tab.png)

   * 如果你選擇 **了「過去24小時**」，在旁邊 **的時間** 欄位中，請指定過去24小時內需要恢復的確切時間。
   * 如果您選擇了 **「上週**」，在相鄰的 **「日子** 」欄位中，請選擇過去七天內的日期，不包括過去24小時。

1. 選取日期或指定時間後，以下&#x200B;**可用備份**&#x200B;部份會顯示可還原的可用備份清單

1. 點選 ![備份旁的資訊圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) ，查看其程式碼版本與 AEM 版本，然後在選擇備份前權衡還原影響（參見 [選擇正確的備份](#choosing-backup)）。

   ![備份資訊](assets/backup-info.png)

   還原選項顯示的時間戳是根據使用者電腦的時區來決定的。

1. 在代表你想還原備份的那一列右端，點選 ![「旋轉 CCW 粗體」或「還原](https://spectrum.adobe.com/static/icons/workflow_18/Smock_RotateCCWBold_18_N.svg) 」以開始還原流程。

1. 在還原內容&#x200B;**對話框中查看詳細資訊**，然後點擊&#x200B;**還原**。

   ![確認還原](assets/backup-restore.png)

備份程序啟動。 你可以在 **[還原活動](#restore-activity)** 清單中查看它的狀態。 完成還原操作所需的時間取決於要還原的內容的大小和設定檔。

當還原成功完成後，環境會執行以下動作：

* 執行與還原操作時相同的程式碼和 AEM 版本。
* 它的內容與所選快照的時間戳相同，索引則重新建立以符合當前程式碼。

## 選擇合適的備份 {#choosing-backup}

Cloud Manager 的自助式還原程式只會將內容還原到 AEM。 因此，您必須仔細考慮在您期望還原點與目前時間之間所做的程式碼變更。 檢視目前提交 ID 與被還原的 ID 之間的提交歷史。

有幾種情況。

* 環境自訂程式碼和還原都在同一個倉庫和同一個分支上。
* 環境自訂程式碼與還原共用一個儲存庫，使用獨立分支，並從共同提交發起。
* 環境自訂程式碼和還原則分別在不同的倉庫裡。
   * 此時不會顯示提交 ID。
   * Adobe 強烈建議你複製兩個倉庫，並使用差異工具來比較分支。

另外，請記得還原可能會導致你的生產環境和預備環境不同步。 還原內容的後果由您負責。

## 恢復活動 {#restore-activity}

**還原活動**&#x200B;清單顯示最近十個還原要求的狀態，包括任何使用中的還原操作。

![還原活動](assets/backup-activity.png)

點擊 ![「資訊」圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) 以建立備份，您可以下載該備份的日誌，並檢查程式碼細節，包括快照與還原啟動時資料之間的差異。

## 異地備份 {#offsite-backup}

定期備份涵蓋 AEM Cloud Service 中意外刪除或技術故障的風險，但區域故障可能會帶來其他風險。 除了可用性外，這類地區中斷的最大風險是資料遺失。

AEM 作為雲端服務可降低所有 AEM 生產環境的風險。 也就是說，它會持續將所有 AEM 內容複製到遠端區域。 此過程可讓內容在三個月內可供復原。 這項功能稱為異地備份。

AEM 服務可靠性工程在資料區域中斷期間，從異地備份恢復 AEM 雲端服務的暫存與生產環境。

## 資料區域映射原則 {#data-region-mapping-principles}

Adobe 遵循一套內部指引來確定 AEM 作為雲端服務&#x200B;**的資料區域映射**。這些指引旨在支持營運效率，確保符合區域法規要求，並提供全球市場一致的客戶體驗。

### 區域映射透明度 {#region-mapping-transparency}

Adobe 不會公開詳細的區域到區域地圖資訊。\
若客戶對區域部署、資料駐留或合規影響有具體或合理疑問，建議直接透過官方支援或帳號管道聯繫 Adobe。

### 資料區域映射的核心原則 {#core-principles}

在決定合適的資料區域映射時，Adobe 會採用幾個優先排序的標準：

1. **不要離開全球區域**\
   部署仍集中於主要全球區域之一： **亞太**、 **EMEA**&#x200B;及 **美洲**&#x200B;地區。

2. **不要離開大陸**\
   在可能的情況下，資料複製與故障轉移保持在同一大陸上。

3. **不要離開這個國家**\
   如果技術上可行，資料會保持在同一國界內。

### 處理例外 {#handling-exceptions}

當因技術或基礎設施限制無法符合上述條件時，Adobe 會額外考量：

* **歐洲特定指引**\
  備用或次要區域不應設於非歐盟國家。\
  （反過來——使用歐盟國家作為非歐盟初選的備選——如果沒有更好的同國選擇，則可能被接受。）

* **避免進入某些區域**\
  應避免將資料政策限制或法規風險較高的地區作為備用或故障轉移地點。

若客戶需要釐清或有合規需求，Adobe 建議聯繫 Adobe 帳戶團隊或支援組織，以獲得針對其特定情況的指導。

## 限制 {#limitations}

自助還原機制的使用受下列限制。

* 還原作業限制為七天，這表示無法還原超過七天的快照。
* 每個日曆月，一個計畫中的所有環境最多允許 10 次成功還原。
* 環境建立後，需要六個小時才能建立第一個備份快照。 在建立此快照之前，無法對環境執行還原。
* 若環境目前有全端或網頁層組態管線在運行，則不會啟動還原操作。
* 如果同一環境中已執行另一個還原，則無法啟動還原。
* 在極少數的情況下，由於備份時間限制為 24 小時/ 7 天選取的備份可能會因為選取備份到啟動還原之間的延遲而變得無法使用。
* 已刪除環境中的資料會永久遺失且無法復原。
