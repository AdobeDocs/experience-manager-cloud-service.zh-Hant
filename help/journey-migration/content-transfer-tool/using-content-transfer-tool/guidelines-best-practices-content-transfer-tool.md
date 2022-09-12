---
title: 使用內容轉移工具的准則和最佳作法
description: 使用內容轉移工具的准則和最佳作法
exl-id: d1975c34-85d4-42e0-bb1a-968bdb3bf85d
source-git-commit: 98b81d918d60722ddb3f1c7736bc5b3506e05f6f
workflow-type: tm+mt
source-wordcount: '1654'
ht-degree: 21%

---

# 使用內容轉移工具的准則和最佳作法 {#guidelines}

## 准則與最佳作法 {#best-practices}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_guidelines"
>title="准則與最佳作法"
>abstract="檢閱使用「內容轉移」工具的准則和最佳實務，包括修訂清除任務、磁碟空間考量事項等。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#pre-reqs" text="使用內容轉移工具的重要考量"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="使用使用者對應工具的重要考量"

新版「內容轉移工具」已推出，其整合了內容轉移程式與Cloud Acceleration Manager。 強烈建議您切換至此新版本，以運用其提供的所有優點：

* 自助式方式，只需擷取一次移轉集，並同時內嵌至多個環境
* 透過更好的載入狀態、護欄和錯誤處理改善使用者體驗
* 擷取記錄會持續存在，且一律可用於疑難排解

若要開始使用新版本(v2.0.10)，您需要解除安裝舊版「內容轉移工具」。 這是必需的，因為新版本具有重大的體系結構更改。 若使用v2.0.10，您將需要建立新的移轉集，並對新移轉集重新執行提取和擷取。 如果移轉已進行中，您可以繼續使用舊版CTT，直到移轉完成為止。

下列准則和最佳實務適用於新版的「內容轉移工具」：

* 建議您對&#x200B;**來源**&#x200B;存放庫執行[修訂清理](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html)和[資料存放區一致性檢查](https://helpx.adobe.com/tw/experience-manager/kb/How-to-run-a-datastore-consistency-check-via-oak-run-AEM.html)，以找出潛在問題並降低存放庫大小。

* 如果 AEM 雲端製作內容傳遞網路 (CDN) 已設定好 IP 白名單，則應確實將來源環境 IP 也新增至允許清單中。讓來源環境和 AEM 雲端環境可互相通訊。

* 在擷取階段中，建議使用&#x200B;*擦去*&#x200B;模式來執行擷取，讓目標 AEM 雲端服務環境中的現有存放庫 (製作或發佈) 被完全刪除，然後以移轉集資料更新。此模式比非擦去模式快速許多，因為在非擦去模式中，移轉集會套用在目前內容的頂端。

* 內容轉移活動完成後，雲端服務環境將需要正確的專案結構，以確保內容在雲端服務環境中成功轉譯。

* 在執行「內容轉移工具」之前，您必須確定來源 AEM 例項的 `crx-quickstart` 子目錄中有足夠的磁碟空間。這是因為「內容轉移工具」會建立存放庫的本機副本，且該副本稍後將上傳至移轉集。計算所需可用磁碟空間的一般公式如下：
   `data store size + node store size * 1.5`

   * *資料存放區大小*：「內容轉移工具」會使用 64GB，即使實際資料存放區較大亦然。
   * *節點存放區大小*：區段存放區目錄大小或 MongoDB 資料庫大小。因此，若區段存放區的大小為 20GB，則需要的可用磁碟空間為 94GB。

* 需要在整個內容轉移活動中維護移轉集，以支援追加內容。 在內容轉移活動期間，每個Cloud Acceleration Manager專案最多可一次建立和維護5個移轉集。 如果需要5個以上的移轉集，您需要在Cloud Acceleration Manager中建立第二個專案。 不過，這需要額外的專案管理和產品外控管理，以避免多名使用者覆寫目標上的內容。

## 使用內容轉移工具前的重要考量 {#important-considerations}

請跟隨以下章節，了解執行「內容轉移工具」時的重要考量：

* 「內容轉移工具」的最低系統需求為 AEM 6.3 + 和 JAVA 8。如果您使用較低的AEM版本，您需要將內容存放庫升級至AEM 6.5，才能使用「內容轉移工具」。

* 必須在AEM環境上設定Java，以便 `java` 命令可由啟動AEM的使用者執行。

* 「內容轉移工具」可搭配下列類型的資料存放區使用：檔案資料儲存、S3資料儲存、共用S3資料儲存和Azure Blob儲存資料儲存。

* 如果您使用 *沙箱環境*，請確定您的環境為最新版本，並升級至最新版本。 如果您使用&#x200B;*生產環境*，則會自動更新。

* 若要使用「內容轉移工具」，您必須是來源例項的管理員使用者，且屬於本機AEM **管理員** 群組(在您要將內容傳送至的Cloud Service例項中)。 沒有權限的使用者將無法開始擷取。

* 若設定 **擷取前先擦去雲端例項上的現有內容** 選項，該選項將刪除整個現有儲存庫並建立新儲存庫以將內容嵌入。 這表示會重設所有設定，包括目標Cloud Service例項的權限。 對於新增至 **管理員** 群組。 必須將使用者重新新增至 **管理員** 群組，以擷取「內容轉移工具」的存取權杖。

* 如果來自兩個來源的內容移至目標上的相同路徑，「內容轉移工具」不支援將來自多個來源的內容合併至目標Cloud Service例項。 若要將多個來源的內容移入單一目標Cloud Service例項，您必須確保來自來源的內容路徑沒有重疊。

* 提取金鑰自建立/續訂起14天內有效。 可隨時更新。 如果提取金鑰已過期，您將無法執行提取。

* 內容轉移工具(CTT)在將內容從來源例項轉移至目標例項之前，不會執行任何類型的內容分析。 例如，CTT不會在將內容擷取至發佈環境時，區分已發佈和未發佈的內容。 無論移轉集中指定什麼內容，都會擷取至選取的目標例項。 使用者能將移轉集內嵌至製作例項、發佈例項或兩者。 建議將內容移至生產執行個體時，應在來源製作執行個體上安裝CTT，以將內容移至目標製作執行個體，同樣地，請在來源發佈執行個體上安裝CTT，將內容移至目標發佈執行個體。 請參閱 [在發佈執行個體上執行內容轉移工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#running-ctt-on-publish) 以取得更多詳細資訊。

* 「內容轉移工具」轉移的「使用者」和「群組」只是內容滿足權限所需的使用者和群組。 此 *提取* 進程複製整個 `/home` 移轉集和 *擷取* 進程會複製遷移內容ACL中引用的所有用戶和組。 若要自動將現有的使用者和群組對應至其IMS ID，請參閱 [使用使用者對應工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration).

* 在提取階段中，「內容轉移工具」會在作用中的 AEM 來源例項上執行。

* 完成 *提取* 內容轉移過程的階段，以及開始 *擷取階段* 將內容內嵌至AEMas a Cloud Service *階段* 或 *生產* 例項中，您需要記錄支援票證，以通知Adobe您有意執行 *擷取* 以便Adobe可確保在 *擷取* 程式。 您需要在計畫前1週登錄支援票證 *擷取* 日期。 一旦您提交了支援票證，支援團隊就會提供後續步驟的指引。 您可以記錄支援票證，並提供下列詳細資訊：

   * 您計劃開始時的確切日期和預計時間（搭配您的時區） *擷取* 階段。
   * 您打算將資料內嵌至的環境類型（預備或生產）。
   * 方案ID。

* 此 *擷取階段* 針對作者縮小整個製作部署。 這表示在整段擷取程序中，將無法使用製作 AEM。此外，請確定在執行 *擷取* 階段。

* 使用時 `Amazon S3` 或 `Azure` 作為源AEM系統上的資料儲存，應配置資料儲存，以便無法刪除儲存的blob（垃圾收集）。 這樣可確保索引資料的完整性，並且如果未能配置此方式，則可能由於此索引資料的完整性不完整而導致提取失敗。

* 如果您使用自訂索引，則必須確保使用 `tika` 節點。 請參閱 [準備新索引定義](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#preparing-the-new-index-definition) 以取得更多詳細資訊。

* 如果您要追加提取，則必須不要變更現有內容的內容結構，從進行初始提取到執行追加提取的時間皆然。 自初始擷取後，結構已變更的內容無法執行追加。 請務必在移轉程式期間加以限制。

* 如果您打算將版本納入移轉集，且要以 `wipe=false`，則您必須停用版本清除，因為「內容轉移工具」中目前有限制。 如果您偏好保持已啟用版本清除功能，並在移轉集中執行追加，則您必須以 `wipe=true`.

## 下一步 {#whats-next}

了解使用「內容轉移工具」的准則、最佳作法和重要考量後，您現在就可以安裝及使用此工具，從建立移轉集開始。 請參閱 [內容轉移工具快速入門](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en) 了解更多。
