---
title: 使用「內容轉移工具」的准則與最佳作法
description: 瞭解使用「內容轉移工具」的准則與最佳實務。
exl-id: d1975c34-85d4-42e0-bb1a-968bdb3bf85d
feature: Migration
role: Admin
source-git-commit: 943685ed9c33ba42c4dd1cb941b2eca1cce8bfe8
workflow-type: tm+mt
source-wordcount: '1389'
ht-degree: 12%

---


# 使用內容轉移工具的准則和最佳實務 {#guidelines}

## 準則和最佳做法 {#best-practices}

<!-- Alexandru: hiding for now

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_guidelines"
>title="Guidelines and Best Practices"
>abstract="Review guidelines and best practices to use the Content Transfer tool including revision cleanup tasks, Disk space considerations and more."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=zh-Hant" text="Important Considerations for using Content Transfer Tool"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/group-migration.md#important-considerations" text="Important Considerations when Migrating Groups" 

-->

「內容轉移工具」整合了內容轉移程式與Cloud Acceleration Manager。 您必須使用此版本（2.0或更新版本，但現在建議使用3.0版本）才能獲得其提供的所有優點：

* 自助式方式擷取一次移轉集，並同時將其擷取至多個環境中
* 透過更好的載入狀態、護欄和錯誤處理，改善使用者體驗
* 內嵌記錄檔會持續存在，且隨時可用於疑難排解

若要開始使用最新版本，請解除安裝舊版的「內容轉移工具」。 若使用2.0版或更新版本，您可以建立移轉集，並在集上重新執行擷取和擷取。
不支援2.0.0之前的版本，建議您使用最新版本。

下列准則和最佳實務適用於新版「內容轉移工具」：

* 對&#x200B;**來源**&#x200B;存放庫執行[修訂清理](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html?lang=zh-Hant)和[資料存放區一致性檢查](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16550.html?lang=zh-Hant)，以便識別潛在問題並降低存放庫大小。

* 在擷取階段中，Adobe建議您使用已啟用的&#x200B;*擦去*&#x200B;模式來執行擷取，並刪除目標Adobe Experience Manager (AEM)Cloud Service環境中的現有存放庫(Author或Publish)。 然後，以移轉集資料更新。 此模式比非擦去模式更快，因為在非擦去模式中，移轉集會套用在目前內容的頂端。

* 內容轉移活動完成後，雲端服務環境將需要正確的專案結構，以確保內容在雲端服務環境中成功轉譯。

* 在執行「內容轉移工具」之前，您必須確定來源 AEM 例項的 `crx-quickstart` 子目錄中有足夠的磁碟空間。這是因為「內容轉移工具」會建立存放庫的本機副本，且該副本稍後將上傳至移轉集。計算所需可用磁碟空間的一般公式如下：
  `data store size + node store size * 1.5`

* *資料存放區大小*：「內容轉移工具」會使用 64GB，即使實際資料存放區較大亦然。
* *節點存放區大小*：區段存放區目錄大小或 MongoDB 資料庫大小。因此，若區段存放區的大小為 20 GB，則需要的可用磁碟空間為 94 GB。

* 必須在整個內容轉移活動中維護移轉集，以支援內容追加。 在內容轉移活動期間，Cloud Acceleration Manager中一次最多可以建立和維護每個專案10個移轉集。 如果需要超過10個移轉集，請在Cloud Acceleration Manager中建立第二個專案。 但是，這需要額外的專案管理和產品外控管，以避免多個使用者覆寫目標上的內容。

* 請避免變更CTT工具的安裝目錄。 依預設，安裝會在crx-quickstart/cloud-migration路徑中進行。 此特定位置會由其他程式庫在內部使用。 修改此路徑可能會導致擷取問題。

## 使用內容轉移工具前的重要考量 {#important-considerations}

請跟隨以下章節，了解執行「內容轉移工具」時的重要考量：

* 「內容轉移工具」的最低系統需求為AEM 6.3 +和Java™ 8。 如果您使用較舊版本的AEM，請將內容存放庫升級至AEM 6.5以使用「內容轉移工具」。

* 必須在AEM環境中設定Java™，以便`java`命令可由啟動AEM的使用者執行。

* 內容轉移工具可用於下列型別的資料存放區：檔案資料存放區、S3資料存放區、共用的S3資料存放區和Azure Blob存放區資料存放區。

* 如果您使用&#x200B;*沙箱環境*，請確定您的環境為最新版本，並升級至最新版本。 如果您使用&#x200B;*生產環境*，則會自動更新。

* 若要開始內嵌，您必須屬於要傳輸內容的Cloud Service執行個體中的本機AEM **管理員**&#x200B;群組。 未獲授權的使用者若未手動提供移轉權杖，就無法開始內嵌。

* 如果設定&#x200B;**在擷取之前擦除雲端執行個體上的現有內容**&#x200B;選項已啟用，它會刪除整個現有存放庫並建立新的存放庫以將內容擷取到。 這表示它會重設所有設定，包括目標Cloud Service執行個體的許可權。 對於新增到&#x200B;**管理員**&#x200B;群組的管理員使用者也是這樣。 必須將該使用者讀入&#x200B;**管理員**&#x200B;群組，才能擷取「內容轉移工具」的存取權杖。

* 擷取金鑰的有效期為從建立或更新後的14天。 可隨時續約。 如果擷取金鑰已過期，您將無法執行擷取。

* 在將內容從來源例項轉移至目標例項之前，內容轉移工具(CTT)不會執行任何型別的內容分析。 例如，將內容擷取至Publish環境時，CTT不會區分已發佈和未發佈的內容。 移轉集中指定的任何內容都會擷取到所選的目標例項。 使用者可以將移轉集內嵌至「作者」例項或「Publish」例項，或兩者皆內嵌。 Adobe建議，將內容移動至生產執行個體時，CTT應安裝在來源製作執行個體上，以將內容移動至目標製作執行個體。 同樣地，請在來源Publish例項上安裝CTT，將內容移至目標Publish例項。 如需詳細資訊，請參閱[在Publish執行個體上執行內容轉移工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=zh-Hant#running-tool)。

* 「內容轉移工具」所轉移的群組只是內容滿足許可權所需的群組。 _擷取_&#x200B;程式會將整個`/home/groups`複製到移轉集。 如需詳細資訊，請參閱[群組移轉](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md)。 _內嵌_&#x200B;程式會複製已移轉內容ACL中參考的所有群組。 請參閱[移轉封閉式使用者群組](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md)，以了解封閉式使用者群組(CUG)原則中所使用群組的額外考量事項。

* 在提取階段中，「內容轉移工具」會在作用中的 AEM 來源例項上執行。

* 製作的&#x200B;*擷取階段*&#x200B;縮小了整個製作部署。 這表示在整段擷取程式中，無法使用製作AEM。 也請確定在您執行&#x200B;*內嵌*&#x200B;階段時沒有執行Cloud Manager管道。

* 使用`Amazon S3`或`Azure`做為來源AEM系統上的資料存放區時，資料存放區應設定為無法刪除已儲存的Blob （記憶體回收）。 這可確保索引資料的完整性，如果無法以這種方式設定，可能會導致擷取失敗，因為此索引資料缺乏完整性。

* 如果您使用自訂索引，您必須確定在執行「內容轉移工具」之前使用`tika`節點設定自訂索引。 如需詳細資訊，請參閱[準備新的索引定義](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html?lang=zh-Hant#preparing-the-new-index-definition)。

* 如果您打算進行追加提取，則現有內容的內容結構決不能從初次提取的時間變更為執行追加提取的時間。 追加無法針對自初始擷取以來結構已變更的內容執行。 請務必在移轉程式期間限制此專案。

* 如果您打算將版本納入移轉集，並使用`wipe=false`執行追加作業，則由於「內容轉移工具」目前的限制，您必須停用版本清除功能。 如果您偏好啟用版本清除，並且正在移轉集中執行追加作業，則必須以`wipe=true`身分執行內嵌。

* 內容轉移工具(CTT)不支援合併擷取。 若要將來自多個系統的內容整合至單一Cloud Service例項，只能移轉來自單一來源系統的版本。 此程式需要使用具有wipe=false引數的移轉，由於作業的增量性質，這可能會導致擷取時間延長。 可能的話，請在開始移轉前將內容整合至單一來源系統，免除合併內容的必要。

* 移轉集會在長時間不活動後過期，之後其資料就無法再使用。 檢閱[移轉集到期日](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=zh-Hant#migration-set-expiry)以取得詳細資料。

## 下一步 {#whats-next}

瞭解使用內容轉移工具的准則、最佳實務和重要考量後，您就可以開始安裝和使用工具，從建立移轉集開始。 請參閱[內容轉移工具快速入門](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md)。
