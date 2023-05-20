---
title: 使用內容傳輸工具的指導原則和最佳做法
description: 使用內容傳輸工具的指導原則和最佳做法
exl-id: d1975c34-85d4-42e0-bb1a-968bdb3bf85d
source-git-commit: 5475f9995513d09e61bd8f52242b3e74b8d4694c
workflow-type: tm+mt
source-wordcount: '1552'
ht-degree: 19%

---

# 使用內容傳輸工具的指導原則和最佳做法 {#guidelines}

## 准則與最佳作法 {#best-practices}

<!-- Alexandru: hiding for now

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_guidelines"
>title="Guidelines and Best Practices"
>abstract="Review guidelines and best practices to use the Content Transfer tool including revision cleanup tasks, Disk space considerations and more."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html" text="Important Considerations for using Content Transfer Tool"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/user-mapping-and-migration.md#important-considerations" text="Important Considerations when Mapping and Migrating Users" 

-->

新版內容傳輸工具可將內容傳輸過程與Cloud Acceleration Manager整合。 強烈建議切換到此新版本，以利用它提供的所有好處：

* 自助式方法，一次提取遷移集並將其並行接收到多個環境中
* 通過更好的載入狀態、護欄和錯誤處理改進用戶體驗
* 攝取日誌被保留，始終可用於故障排除

要開始使用新版本，您需要卸載舊版本的內容傳輸工具。 這是必需的，因為新版本具有重大的體系結構更改。 使用2.x版，您需要建立新的遷移集，並對新遷移集重新運行提取和接收。
不再支援2.0.0之前的版本，建議使用最新版本。

以下准則和最佳做法適用於新版的內容傳輸工具：

* 建議您對&#x200B;**來源**&#x200B;存放庫執行[修訂清理](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html)和[資料存放區一致性檢查](https://helpx.adobe.com/tw/experience-manager/kb/How-to-run-a-datastore-consistency-check-via-oak-run-AEM.html)，以找出潛在問題並降低存放庫大小。

* 在擷取階段中，建議使用&#x200B;*擦去*&#x200B;模式來執行擷取，讓目標 AEM 雲端服務環境中的現有存放庫 (製作或發佈) 被完全刪除，然後以移轉集資料更新。此模式比非擦去模式快速許多，因為在非擦去模式中，移轉集會套用在目前內容的頂端。

* 內容轉移活動完成後，雲端服務環境將需要正確的專案結構，以確保內容在雲端服務環境中成功轉譯。

* 在執行「內容轉移工具」之前，您必須確定來源 AEM 例項的 `crx-quickstart` 子目錄中有足夠的磁碟空間。這是因為「內容轉移工具」會建立存放庫的本機副本，且該副本稍後將上傳至移轉集。計算所需可用磁碟空間的一般公式如下：
   `data store size + node store size * 1.5`

   * *資料存放區大小*：「內容轉移工具」會使用 64GB，即使實際資料存放區較大亦然。
   * *節點存放區大小*：區段存放區目錄大小或 MongoDB 資料庫大小。因此，若區段存放區的大小為 20GB，則需要的可用磁碟空間為 94GB。

* 需要在整個內容傳輸活動中維護遷移集以支援內容補充。 在內容傳輸活動期間，每次最多可以建立和維護雲加速管理器中每個項目的5個遷移集。 如果需要5個以上的遷移集，您需要在雲加速管理器中建立第二個項目。 但是，這將需要額外的項目管理和產品外治理，以避免多個用戶覆蓋目標上的內容。

## 使用內容傳輸工具之前的重要注意事項 {#important-considerations}

請跟隨以下章節，了解執行「內容轉移工具」時的重要考量：

* 「內容轉移工具」的最低系統需求為 AEM 6.3 + 和 JAVA 8。如果您的版AEM本較低，則需要將內容儲存庫升級AEM到6.5以使用內容傳輸工具。

* 必須在環境上配AEM置Java，以便 `java` 命令可由啟動的用戶執AEM行。

* 內容傳輸工具可用於以下類型的資料儲存：檔案資料儲存、S3資料儲存、共用的S3資料儲存和Azure Blob儲存資料儲存。

* 如果使用 *沙盒環境*，確保您的環境是最新的，並已升級到最新版本。 如果您使用&#x200B;*生產環境*，則會自動更新。

* 要開始攝取，您需要屬於本AEM地 **管理員** Cloud Service實例中的組。 未授權用戶將無法在不手動提供遷移令牌的情況下啟動接收。

* 如果設定 **在接收之前擦除雲實例上的現有內容** 選項，它將刪除整個現有儲存庫並建立新儲存庫以將內容插入。 這意味著它會重置所有設定，包括對目標Cloud Service實例的權限。 對於添加到 **管理員** 組。 必須將用戶重新添加到 **管理員** 以檢索內容傳輸工具的訪問令牌。

* 如果將來自兩個源的內容移動到目標上的相同路徑，則接收不支援將來自多個源的內容合併到目標Cloud Service實例。 要將內容從多個源移動到單個目標Cloud Service實例，您需要確保源的內容路徑不重疊。

* 提取密鑰自建立/續訂之日起有效14天。 它可以隨時更新。 如果提取密鑰已過期，您將無法執行提取。

* 內容傳輸工具(CTT)在將內容從源實例傳輸到目標實例之前不執行任何類型的內容分析。 例如， CTT在將內容插入發佈環境時不會區分已發佈和未發佈的內容。 遷移集中指定的任何內容都將被引入所選目標實例。 用戶能夠將遷移集插入Author實例或Publish實例或兩者。 建議在將內容移動到生產實例時，在源Author實例上安裝CTT以將內容移動到目標Author實例，同樣，在源Publish實例上安裝CTT以將內容移動到目標Publish實例。 請參閱 [在發佈實例上運行內容傳輸工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html#running-tool) 的子菜單。

* 內容傳輸工具傳輸的用戶和組僅是內容滿足權限所需的用戶和組。 的 _提取_ 進程拷貝整個 `/home` 在遷移集中，它通過添加每個用戶電子郵件地址中的欄位來執行用戶映射。 有關詳細資訊，請參見 [用戶映射和主遷移](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md)。 的 _攝取_ 進程複製遷移內容ACL中引用的所有用戶和組。

* 在提取階段中，「內容轉移工具」會在作用中的 AEM 來源例項上執行。

* 完成 *提取* 內容傳輸過程的階段和開始之前 *攝取階段* 將內容錄入AEMas a Cloud Service *舞台* 或 *生產* 實例，您需要記錄支援票證以通知Adobe您打算運行 *攝取* 以便Adobe能夠確保在 *攝取* 處理。 您需要在計畫前1週記錄支援票證 *攝取* 日期。 一旦您提交了支援票證，支援團隊將提供有關後續步驟的指導。 您可以記錄支援票證，具有以下詳細資訊：

   * 計畫啟動時的確切日期和估計時間（與時區） *攝取* 。
   * 您計畫將資料插入的環境類型（階段或生產）。
   * 程式ID。

* 的 *攝取階段* 因為作者縮小了整個作者部署。 這表示在整段擷取程序中，將無法使用製作 AEM。還請確保在運行雲管理器 *攝取* 。

* 使用時 `Amazon S3` 或 `Azure` 作為源系統上的數AEM據儲存，應配置資料儲存，以便無法刪除儲存的blob（垃圾收集）。 這確保了索引資料的完整性，如果無法配置這種方式，則可能由於此索引資料的完整性不足而導致提取失敗。

* 如果使用自定義索引，則必須確保使用 `tika` 節點，然後運行內容傳輸工具。 請參閱 [準備新索引定義](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html#preparing-the-new-index-definition) 的子菜單。

* 如果要執行頂層提取，則必須不更改現有內容的內容結構，從初始提取到運行頂層提取。 無法對自初始提取後結構已更改的內容運行頂層。 請確保在遷移過程中限制此操作。

* 如果您打算將版本作為遷移集的一部分包括，並且正在執行 `wipe=false`，則由於內容傳輸工具中的當前限制，您必須禁用版本清除。 如果您希望啟用版本清除功能，並在遷移集中執行頂置操作，則必須將接收操作執行為 `wipe=true`。

* 遷移集將在長時間不活動後過期，此後其資料將不再可用。 請查看 [遷移集到期](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html#migration-set-expiry) 的子菜單。

## 下一步 {#whats-next}

一旦您瞭解了使用內容傳輸工具的指導原則、最佳做法和重要注意事項，現在您就可以安裝和使用該工具了，從建立遷移集開始。 請參閱 [內容傳輸工具入門](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md) 來瞭解更多資訊。
