---
title: 使用內容傳輸工具的准則和最佳做法（舊版）
description: 使用內容傳輸工具的指導原則和最佳做法
hide: true
hidefromtoc: true
exl-id: 03449606-0fb4-4a9f-9abb-6b17c27a6046
source-git-commit: eadcf71aa96298383b05e61251dfeb5f345df6b9
workflow-type: tm+mt
source-wordcount: '1476'
ht-degree: 13%

---

# 使用內容傳輸工具的准則和最佳做法（舊版） {#guidelines}

## 准則與最佳作法 {#best-practices}

請依照以下章節了解使用「內容轉移工具」的准則與最佳作法：

* 運行 [修訂版清除](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html) 和 [資料儲存一致性檢查](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16550.html?lang=en) 的 **源** 儲存庫，以發現潛在問題並減少儲存庫的大小。

* 如果AEM將雲作者內容分發網路(CDN)配置配置為具有IP的允許清單，請確保源環境IP也添加到允許清單中。 這樣可確保源環境和AEM雲環境能夠相互通信。

* 使用 *擦* 模式啟用，其中將刪除目標AEM Cloud Service環境中的現有儲存庫（作者或發佈），然後使用遷移集資料進行更新。 此模式比非擦去模式快速許多，因為在非擦去模式中，移轉集會套用在目前內容的頂端。

* 內容轉移活動完成後，雲端服務環境將需要正確的專案結構，以確保內容在雲端服務環境中成功轉譯。

* 在執行「內容轉移工具」之前，您必須確定來源 AEM 例項的 `crx-quickstart` 子目錄中有足夠的磁碟空間。這是因為「內容轉移工具」會建立存放庫的本機副本，且該副本稍後將上傳至移轉集。計算所需可用磁碟空間的一般公式如下：
   `data store size + node store size * 1.5`

   * *資料存放區大小*：「內容轉移工具」會使用 64GB，即使實際資料存放區較大亦然。
   * *節點存放區大小*：區段存放區目錄大小或 MongoDB 資料庫大小。因此，若區段存放區的大小為 20GB，則需要的可用磁碟空間為 94GB。

* 必須在整個內容傳輸活動中維護遷移集以支援內容補充。 由於在內容傳輸活動期間一次最多可以建立和維護十個遷移集，因此建議相應地分拆內容儲存庫。 這樣做可確保不會用完遷移集。

## 使用內容傳輸工具之前的重要注意事項 {#important-considerations}

請跟隨以下章節，了解執行「內容轉移工具」時的重要考量：

* 內容傳輸工具的最低系統AEM要求是6.3 +和Java™ 8。 如果您的版AEM本較低，則需要將內容儲存庫升級AEM到6.5以使用內容傳輸工具。

* 必須在環境上配AEM置Java™, `java` 命令可由啟動的用戶執AEM行。

* 在安裝1.3.0版時卸載舊版內容傳輸工具，因為該工具中存在重大體系結構更改。 使用1.3.0，您還應建立遷移集，並對新遷移集重新運行提取和接收。

* 內容傳輸工具可用於以下類型的資料儲存：檔案資料儲存、S3資料儲存、共用的S3資料儲存和Azure Blob儲存資料儲存。

* 如果使用 *沙盒環境*，確保您的環境是最新的，並已升級到最新版本。 如果您使用&#x200B;*生產環境*，則會自動更新。

* 要使用內容傳輸工具，您需要是源實例上的管理員用戶，並且屬於本AEM地 **管理員** Cloud Service實例中的組。 無權限用戶無法檢索訪問令牌以使用內容傳輸工具。

* 如果設定 **在接收之前擦除雲實例上的現有內容** 選項，它將刪除整個現有儲存庫，並建立一個儲存庫以將內容插入其中。 此工作流表示它重置所有設定，包括目標Cloud Service實例的權限。 此結果即使對添加到 **管理員** 組。 必須將用戶讀入 **管理員** 以檢索內容傳輸工具的訪問令牌。

* 如果將來自兩個源的內容移動到目標上的相同路徑，則內容傳輸工具不支援將來自多個源的內容合併到目標Cloud Service實例。 要將內容從多個源移動到單個目標Cloud Service實例，您需要確保源的內容路徑不重疊。

* 訪問令牌可以在特定時間段之後或在升級Cloud Service環境之後定期過期。 如果訪問令牌已過期，則無法連接到Cloud Service實例。 在這種情況下，您需要檢索新的訪問令牌。 與現有遷移集關聯的狀態表徵圖將更改為紅色雲，並在懸停在紅色雲上時顯示一條消息。

* 內容傳輸工具(CTT)在將內容從源實例傳輸到目標實例之前不執行任何類型的內容分析。 例如， CTT在將內容插入發佈環境時不會區分已發佈和未發佈的內容。 在遷移集中指定的任何內容都會被引入所選目標實例。 用戶可以將遷移集插入Author實例或Publish實例或兩者。 將內容移動到生產實例時，在源Author實例上安裝CTT以將內容移動到目標Author實例。 同樣，在源發佈實例上安裝CTT以將內容移動到目標發佈實例。 請參閱 [在發佈實例上運行內容傳輸工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en#running-tool) 的子菜單。

* 內容傳輸工具傳輸的用戶和組僅是內容滿足權限所需的用戶和組。 的 *提取* 進程拷貝整個 `/home` 遷移集和 *攝取* 進程複製遷移內容ACL中引用的所有用戶和組。 要自動將現有用戶和組映射到其IMS ID，請參閱 [使用用戶映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/legacy-user-mapping-tool/using-user-mapping-tool-legacy.html?lang=en)。

* 在提取階段中，「內容轉移工具」會在作用中的 AEM 來源例項上執行。

* 完成 *提取* 內容傳輸過程的階段和開始之前 *攝取階段* 將內容錄入AEMas a Cloud Service *舞台* 或 *生產* 實例，記錄支援票證。 通知Adobe您打算運行 *攝取* 以便Adobe能夠確保在 *攝取* 處理。 在計畫前一週記錄支援票證 *攝取* 日期。 在您提交支援票證後，支援團隊將提供有關後續步驟的指導。 記錄支援票證，具有以下詳細資訊：

   * 計畫啟動時的確切日期和估計時間（與時區） *攝取* 。
   * 您計畫將資料插入的環境類型（階段或生產）。
   * 程式ID。

* 的 *攝取階段* 因為作者縮小了整個作者部署。 此過程意味著在整個AEM攝取過程中，作者不可用。 還請確保在運行雲管理器 *攝取* 。

* 使用時 `Amazon S3` 或 `Azure` 作為源系統上的數AEM據儲存，應配置資料儲存，以便無法刪除儲存的blob（垃圾收集）。 這確保了索引資料的完整性，如果無法配置這種方式，則可能由於此索引資料的完整性不足而導致提取失敗。

* 如果使用自定義索引，則必須確保使用 `tika` 節點，然後運行內容傳輸工具。 請參閱 [準備新索引定義](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html?lang=en#preparing-the-new-index-definition) 的子菜單。

* 如果要執行頂層提取，請確保從初始提取到運行頂層提取時，不更改現有內容的內容結構。 無法對自初始提取後結構已更改的內容運行頂層。 確保在遷移過程中限制此操作。

* 如果您打算將版本作為遷移集的一部分包括，並且正在執行 `wipe=false`，則由於內容傳輸工具中的當前限制，您必須禁用版本清除。 如果您希望啟用版本清除功能，並在遷移集中執行頂置操作，則必須將接收操作執行為 `wipe=true`。

## 下一步 {#whats-next}

一旦您瞭解了使用內容傳輸工具的指導原則、最佳做法和重要注意事項，現在您就可以安裝和使用該工具了，從建立遷移集開始。 請參閱 [內容傳輸工具入門](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en) 來瞭解更多資訊。
