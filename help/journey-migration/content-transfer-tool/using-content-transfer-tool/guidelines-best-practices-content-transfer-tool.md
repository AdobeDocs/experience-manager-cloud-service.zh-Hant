---
title: 使用內容轉移工具的准則和最佳實務
description: 使用內容轉移工具的准則和最佳實務
exl-id: d1975c34-85d4-42e0-bb1a-968bdb3bf85d
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1544'
ht-degree: 15%

---

# 使用內容轉移工具的准則和最佳實務 {#guidelines}

## 准則與最佳作法 {#best-practices}

<!-- Alexandru: hiding for now

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_guidelines"
>title="Guidelines and Best Practices"
>abstract="Review guidelines and best practices to use the Content Transfer tool including revision cleanup tasks, Disk space considerations and more."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html" text="Important Considerations for using Content Transfer Tool"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/user-mapping-and-migration.md#important-considerations" text="Important Considerations when Mapping and Migrating Users" 

-->

提供新版內容轉移工具，整合了內容轉移程式與Cloud Acceleration Manager。 強烈建議切換至此新版本，以使用它提供的所有優點：

* 自助式方式擷取一次移轉集，並同時將其擷取至多個環境中
* 透過更好的載入狀態、護欄和錯誤處理，改善使用者體驗
* 內嵌記錄會持續存在，且隨時可用於疑難排解

若要開始使用新版本，您必須解除安裝舊版的「內容轉移工具」。 此為必要操作，因為新版本具有重大的架構變更。 若使用2.x版，您需要建立新的移轉集，並重新執行新移轉集的擷取和擷取。
不再支援2.0.0之前的版本，建議您使用最新版本。

以下准則和最佳實務適用於新版的「內容轉移工具」：

* 建議您對&#x200B;**來源**&#x200B;存放庫執行[修訂清理](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html)和[資料存放區一致性檢查](https://helpx.adobe.com/tw/experience-manager/kb/How-to-run-a-datastore-consistency-check-via-oak-run-AEM.html)，以找出潛在問題並降低存放庫大小。

* 在擷取階段中，建議使用以下專案執行擷取： *擦去* 啟用模式，讓目標AEM Cloud Service環境中的現有存放庫（製作或發佈）完全刪除，然後使用移轉集資料更新。 此模式比非擦去模式快速許多，因為在非擦去模式中，移轉集會套用在目前內容的頂端。

* 內容轉移活動完成後，雲端服務環境將需要正確的專案結構，以確保內容在雲端服務環境中成功轉譯。

* 在執行「內容轉移工具」之前，您必須確定來源 AEM 例項的 `crx-quickstart` 子目錄中有足夠的磁碟空間。這是因為「內容轉移工具」會建立存放庫的本機副本，且該副本稍後將上傳至移轉集。計算所需可用磁碟空間的一般公式如下：
  `data store size + node store size * 1.5`

   * *資料存放區大小*：「內容轉移工具」會使用 64GB，即使實際資料存放區較大亦然。
   * *節點存放區大小*：區段存放區目錄大小或 MongoDB 資料庫大小。因此，若區段存放區的大小為 20GB，則需要的可用磁碟空間為 94GB。

* 在整個內容轉移活動中都需要維護移轉集，以支援追加內容。 在內容轉移活動期間，Cloud Acceleration Manager中一次最多可以為每個專案建立5個移轉集。 如果需要超過五個移轉集，您將需要在Cloud Acceleration Manager中建立第二個專案。 但是，這需要額外的專案管理和產品外控管，以避免多個使用者覆寫目標上的內容。

## 使用內容轉移工具前的重要考量 {#important-considerations}

請跟隨以下章節，了解執行「內容轉移工具」時的重要考量：

* 「內容轉移工具」的最低系統需求為 AEM 6.3 + 和 JAVA 8。如果您使用較舊的AEM版本，您必須將內容存放庫升級至AEM 6.5才能使用內容轉移工具。

* 必須在AEM環境中設定Java，以便 `java` 命令可由啟動AEM的使用者執行。

* 內容轉移工具可與下列型別的資料存放區一起使用：檔案資料存放區、S3資料存放區、共用的S3資料存放區和Azure Blob存放區資料存放區。

* 如果您使用 *沙箱環境*，確定您的環境為最新版本且已升級至最新版本。 如果您使用&#x200B;*生產環境*，則會自動更新。

* 若要開始內嵌，您必須屬於本機AEM **管理員** 群組(在您要轉移內容的Cloud Service例項中)。 若未手動提供移轉權杖，未獲授權的使用者將無法開始內嵌。

* 如果設定 **在內嵌之前擦除雲端例項上的現有內容** 選項已啟用，則會刪除整個現有存放庫並建立新存放庫以內嵌內容。 這表示它會重設所有設定，包括目標Cloud Service執行個體的許可權。 對於新增至的管理員使用者也是如此 **管理員** 群組。 必須將使用者重新新增至 **管理員** 群組以擷取內容轉移工具的存取權杖。

* 如果來自兩個來源的內容移動到目標上的相同路徑，則內嵌不支援將來自多個來源的內容合併到目標Cloud Service例項中。 若要將多個來源的內容移至單一目標Cloud Service例項，您需要確保來源的內容路徑沒有重疊。

* 擷取金鑰的有效期為建立/更新後的14天。 可隨時續約。 如果擷取金鑰已過期，您將無法執行擷取。

* 內容轉移工具(CTT)在將內容從來源例項轉移到目標例項之前，不會執行任何型別的內容分析。 例如，將內容擷取至發佈環境時，CTT不會區分已發佈和未發佈的內容。 移轉集中指定的任何內容都會擷取到所選的目標例項。 使用者能將移轉集內嵌至「作者」執行個體或「發佈」執行個體（或兩者）。 建議在將內容移至生產執行個體時，在來源製作執行個體上安裝CTT以將內容移至目標製作執行個體，同樣地，在來源發佈執行個體上安裝CTT以將內容移至目標發佈執行個體。 另請參閱 [在發佈執行個體上執行內容轉移工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html#running-tool) 以取得更多詳細資料。

* 「內容轉移工具」轉移的「使用者與群組」只是內容滿足許可權所需的使用者與群組。 此 _摘取_ 程式會複製整個 `/home` 並新增從每位使用者的電子郵件地址建立的欄位，以進行使用者對應。 如需詳細資訊，請參閱 [使用者對應和主體移轉](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md). 此 _內嵌_ 程式會複製已移轉內容ACL中參照的所有使用者和群組。

* 在提取階段中，「內容轉移工具」會在作用中的 AEM 來源例項上執行。

* 完成 *摘取* 內容轉移程式階段及開始 *擷取階段* 將內容內嵌至您的AEMas a Cloud Service *階段* 或 *生產* 執行個體，您需要記錄支援票證以通知Adobe您打算執行 *內嵌* 以便Adobe可確保在 *內嵌* 程式。 您需要於計畫的1週前記錄支援票證 *內嵌* 日期。 在您提交支援票證後，支援團隊會提供後續步驟的指引。 您可以記錄支援票證，其詳細資料如下：

   * 計劃開始的確切日期和估計時間（以您的時區表示） *內嵌* 階段。
   * 您打算將資料內嵌到的環境型別（中繼或生產）。
   * 方案ID。

* 此 *擷取階段* 對於作者，會縮小整個作者部署。 這表示在整段擷取程式中，無法使用製作AEM。 也請確定當您執行 *內嵌* 階段。

* 使用時 `Amazon S3` 或 `Azure` 做為來源AEM系統上的資料存放區，資料存放區應進行設定，以便無法刪除已儲存的blob （垃圾收集）。 這樣可確保索引資料的完整性，如果無法以這種方式設定，可能會導致擷取失敗，因為此索引資料缺乏完整性。

* 如果您使用自訂索引，您必須確保設定自訂索引時具有 `tika` 節點（在執行內容轉移工具之前）。 另請參閱 [準備新的索引定義](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html#preparing-the-new-index-definition) 以取得更多詳細資料。

* 如果您打算執行追加提取，則必須確保現有內容的內容結構不會從初次提取時間變更為執行追加提取時間。 追加無法針對自初始擷取以來結構已變更的內容執行。 請務必在移轉程式期間限制此專案。

* 如果您打算將版本納入移轉集，並使用執行追加功能 `wipe=false`，則由於「內容轉移工具」的目前限制，您必須停用版本清除。 如果您偏好啟用版本整個清除，並且要在移轉集中執行追加作業，則必須依照以下方式執行內嵌 `wipe=true`.

* 移轉集將在長時間不活動後過期，之後其資料將不再可用。 檢閱 [移轉集到期](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html#migration-set-expiry) 以取得更多詳細資料。

## 下一步 {#whats-next}

瞭解使用內容轉移工具的准則、最佳實務和重要考量後，您就可以開始安裝和使用工具，從建立移轉集開始。 另請參閱 [內容轉移工具快速入門](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md) 以深入瞭解。
