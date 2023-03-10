---
title: 使用內容轉移工具的准則和最佳實務（舊版）
description: 使用內容轉移工具的准則和最佳作法
hide: true
hidefromtoc: true
exl-id: 03449606-0fb4-4a9f-9abb-6b17c27a6046
source-git-commit: eadcf71aa96298383b05e61251dfeb5f345df6b9
workflow-type: tm+mt
source-wordcount: '1476'
ht-degree: 13%

---

# 使用內容轉移工具的准則和最佳實務（舊版） {#guidelines}

## 准則與最佳作法 {#best-practices}

請依照以下章節了解使用「內容轉移工具」的准則與最佳作法：

* 執行 [修訂清除](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html) 和 [資料儲存一致性檢查](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16550.html?lang=en) 在 **來源** 存放庫，以找出潛在問題並縮小存放庫大小。

* 如果AEM雲端製作內容傳遞網路(CDN)設定設定為有允許清單的IP，請確定來源環境IP也新增至允許清單。 這麼做可確保來源環境與AEM雲端環境能彼此通訊。

* 使用 *擦* 啟用模式，將刪除target AEM Cloud Service環境中的現有存放庫（製作或發佈），然後使用移轉集資料更新。 此模式比非擦去模式快速許多，因為在非擦去模式中，移轉集會套用在目前內容的頂端。

* 內容轉移活動完成後，雲端服務環境將需要正確的專案結構，以確保內容在雲端服務環境中成功轉譯。

* 在執行「內容轉移工具」之前，您必須確定來源 AEM 例項的 `crx-quickstart` 子目錄中有足夠的磁碟空間。這是因為「內容轉移工具」會建立存放庫的本機副本，且該副本稍後將上傳至移轉集。計算所需可用磁碟空間的一般公式如下：
   `data store size + node store size * 1.5`

   * *資料存放區大小*：「內容轉移工具」會使用 64GB，即使實際資料存放區較大亦然。
   * *節點存放區大小*：區段存放區目錄大小或 MongoDB 資料庫大小。因此，若區段存放區的大小為 20GB，則需要的可用磁碟空間為 94GB。

* 必須在整個內容轉移活動中維護移轉集，以支援追加內容。 因為在內容轉移活動期間，一次最多可建立並維護10個移轉集，因此建議據以分解內容存放庫。 這樣可確保移轉集不會用完。

## 使用內容轉移工具前的重要考量 {#important-considerations}

請跟隨以下章節，了解執行「內容轉移工具」時的重要考量：

* 「內容轉移工具」的最低系統需求為AEM 6.3 +和Java™ 8。 如果您使用較低的AEM版本，您需要將內容存放庫升級至AEM 6.5，才能使用「內容轉移工具」。

* 必須在AEM環境中設定Java™，以便 `java` 命令可由啟動AEM的使用者執行。

* 安裝1.3.0版時，請解除安裝舊版「內容轉移工具」，因為工具的架構有重大變更。 使用1.3.0時，您也應建立移轉集，並對新移轉集重新執行提取和擷取。

* 「內容轉移工具」可搭配下列類型的資料存放區使用：檔案資料儲存、S3資料儲存、共用S3資料儲存和Azure Blob儲存資料儲存。

* 如果您使用 *沙箱環境*，請確定您的環境為最新版本，並升級至最新版本。 如果您使用&#x200B;*生產環境*，則會自動更新。

* 若要使用「內容轉移工具」，您必須是來源例項的管理員使用者，且屬於本機AEM **管理員** 群組(在您要將內容傳送至的Cloud Service例項中)。 無權限的使用者無法擷取使用「內容轉移工具」的存取權杖。

* 若設定 **擷取前先擦去雲端例項上的現有內容** 選項，該選項會刪除整個現有儲存庫並建立儲存庫以將內容內嵌到中。 此工作流程表示會重設所有設定，包括目標Cloud Service例項的權限。 即使是新增至 **管理員** 群組。 必須將使用者讀入 **管理員** 群組，以擷取「內容轉移工具」的存取權杖。

* 如果來自兩個來源的內容移至目標上的相同路徑，「內容轉移工具」不支援將來自多個來源的內容合併至目標Cloud Service例項。 若要將多個來源的內容移入單一目標Cloud Service例項，您必須確保來自來源的內容路徑沒有重疊。

* 存取權杖可能會在特定時段之後或Cloud Service環境升級後定期過期。 如果存取權杖已過期，則無法連線至Cloud Service例項。 在這種情況下，您需要擷取新的存取權杖。 與現有移轉集相關聯的狀態圖示會變更為紅色雲端，當您將游標暫留在紅色雲端時會顯示訊息。

* 內容轉移工具(CTT)在將內容從來源例項轉移至目標例項之前，不會執行任何類型的內容分析。 例如，CTT不會在將內容擷取至發佈環境時，區分已發佈和未發佈的內容。 移轉集中指定的任何內容都會擷取至選取的目標例項。 使用者可將移轉集內嵌至製作例項、發佈例項或兩者。 將內容移至生產執行個體時，請在來源製作執行個體上安裝CTT，以將內容移至目標製作執行個體。 同樣地，請在來源發佈例項上安裝CTT，將內容移至目標發佈例項。 請參閱 [在發佈執行個體上執行內容轉移工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en#running-tool) 以取得更多詳細資訊。

* 「內容轉移工具」轉移的「使用者」和「群組」只是內容滿足權限所需的使用者和群組。 此 *提取* 進程複製整個 `/home` 移轉集和 *擷取* 進程會複製遷移內容ACL中引用的所有用戶和組。 若要自動將現有的使用者和群組對應至其IMS ID，請參閱 [使用使用者對應工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/legacy-user-mapping-tool/using-user-mapping-tool-legacy.html?lang=en).

* 在提取階段中，「內容轉移工具」會在作用中的 AEM 來源例項上執行。

* 完成 *提取* 內容轉移過程的階段，以及開始 *擷取階段* 將內容內嵌至AEMas a Cloud Service *階段* 或 *生產* 例項，記錄支援票證。 通知Adobe您打算執行 *擷取* 以便Adobe可確保在 *擷取* 程式。 在計畫前一週登錄支援票證 *擷取* 日期。 在您提交支援票證後，支援團隊會提供後續步驟的指導。 使用以下詳細資訊記錄支援票證：

   * 您計劃開始時的確切日期和預計時間（搭配您的時區） *擷取* 階段。
   * 您打算將資料內嵌至的環境類型（預備或生產）。
   * 方案ID。

* 此 *擷取階段* 針對作者縮小整個製作部署。 此程式表示製作AEM在整個擷取程式期間無法使用。 此外，請確定在執行 *擷取* 階段。

* 使用時 `Amazon S3` 或 `Azure` 作為源AEM系統上的資料儲存，應配置資料儲存，以便無法刪除儲存的blob（垃圾收集）。 這樣可確保索引資料的完整性，並且如果未能配置此方式，則可能由於此索引資料的完整性不完整而導致提取失敗。

* 如果您使用自訂索引，則必須確保使用 `tika` 節點。 請參閱 [準備新索引定義](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html?lang=en#preparing-the-new-index-definition) 以取得更多詳細資訊。

* 如果您要追加提取，請確定從進行初始提取到執行追加提取期間，現有內容的內容結構未變更。 自初始擷取後，無法對結構已變更的內容執行追加。 請務必在移轉程式期間加以限制。

* 如果您打算將版本納入移轉集，且要以 `wipe=false`，則您必須停用版本清除，因為「內容轉移工具」中目前有限制。 如果您偏好保持已啟用版本清除功能，並在移轉集中執行追加，則您必須以 `wipe=true`.

## 下一步 {#whats-next}

了解使用「內容轉移工具」的准則、最佳作法和重要考量後，您現在就可以安裝及使用此工具，從建立移轉集開始。 請參閱 [內容轉移工具快速入門](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en) 了解更多。
