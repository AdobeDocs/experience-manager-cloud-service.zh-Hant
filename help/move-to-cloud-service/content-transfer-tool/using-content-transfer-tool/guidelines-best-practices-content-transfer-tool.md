---
title: 使用內容轉移工具的指引和最佳實務
description: 使用內容轉移工具的指引和最佳實務
source-git-commit: bdcc5cfc229fd5b1fd1f70e37c7231ed3f727e72
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 使用內容轉移工具的指引和最佳實務 {#guidelines}

## 准則與最佳作法 {#best-practices}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_guidelines"
>title="准則與最佳作法"
>abstract="檢閱使用「內容轉移」工具的准則和最佳實務，包括修訂清除任務、磁碟空間考量事項等。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#pre-reqs" text="使用內容轉移工具的重要考量"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="使用使用者對應工具的重要考量"

請依照以下章節了解使用「內容轉移工具」的准則與最佳作法：

* 建議您對&#x200B;**來源**&#x200B;存放庫執行[修訂清理](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html)和[資料存放區一致性檢查](https://helpx.adobe.com/tw/experience-manager/kb/How-to-run-a-datastore-consistency-check-via-oak-run-AEM.html)，以找出潛在問題並降低存放庫大小。

* 如果 AEM 雲端製作內容傳遞網路 (CDN) 已設定好 IP 白名單，則應確實將來源環境 IP 也新增至允許清單中。讓來源環境和 AEM 雲端環境可互相通訊。

* 在擷取階段中，建議使用&#x200B;*擦去*&#x200B;模式來執行擷取，讓目標 AEM 雲端服務環境中的現有存放庫 (製作或發佈) 被完全刪除，然後以移轉集資料更新。此模式比非擦去模式快速許多，因為在非擦去模式中，移轉集會套用在目前內容的頂端。

* 內容轉移活動完成後，雲端服務環境將需要正確的專案結構，以確保內容在雲端服務環境中成功轉譯。

* 在執行「內容轉移工具」之前，您必須確定來源 AEM 例項的 `crx-quickstart` 子目錄中有足夠的磁碟空間。這是因為「內容轉移工具」會建立存放庫的本機副本，且該副本稍後將上傳至移轉集。計算所需可用磁碟空間的一般公式如下：
   `data store size + node store size * 1.5`

   * *資料存放區大小*：「內容轉移工具」會使用 64GB，即使實際資料存放區較大亦然。
   * *節點存放區大小*：區段存放區目錄大小或 MongoDB 資料庫大小。因此，若區段存放區的大小為 20GB，則需要的可用磁碟空間為 94GB。

* 需要在整個內容轉移活動中維護移轉集，以支援追加內容。 由於在內容轉移活動期間，一次最多可建立並維護10個移轉集，因此建議您據以劃分內容存放庫，以確保移轉集不會用完。

## 使用內容轉移工具前的重要考量 {#important-considerations}

請跟隨以下章節，了解執行「內容轉移工具」時的重要考量：

* 「內容轉移工具」的最低系統需求為 AEM 6.3 + 和 JAVA 8。如果您使用較低的AEM版本，您需要將內容存放庫升級至AEM 6.5，才能使用「內容轉移工具」。

* 必須在AEM環境上配置Java，以便啟動AEM的用戶可以執行`java`命令。

* 安裝1.3.0版時，建議解除安裝舊版「內容轉移工具」，因為工具的架構有重大變更。 使用1.3.0時，您也應建立新的移轉集，並對新移轉集重新執行提取和擷取。

* 「內容轉移工具」可搭配下列類型的資料存放區使用：檔案資料儲存、S3資料儲存、共用S3資料儲存和Azure Blob儲存資料儲存。

* 如果您使用&#x200B;*沙箱環境*，請確定您的環境為最新版本，並升級至最新版本。 如果您使用&#x200B;*生產環境*，則會自動更新。

* 若要使用「內容轉移工具」，您必須是來源例項的管理員使用者，且屬於要轉移內容的Cloud Service例項中的本機AEM **administrators**&#x200B;群組。 無權限的使用者將無法擷取能使用「內容轉移工具」的存取 Token。

* 如果啟用「在擷取&#x200B;**之前擦去雲端例項上的現有內容」選項，則會刪除整個現有存放庫並建立新存放庫，以將內容擷取至中。**&#x200B;這表示會重設所有設定，包括目標Cloud Service例項的權限。 對於新增至&#x200B;**administrators**&#x200B;群組的管理員使用者，也是如此。 必須將用戶重新添加到&#x200B;**administrators**&#x200B;組中，才能檢索CTT的訪問令牌。

* 存取權杖可能會在特定時段之後或Cloud Service環境升級後定期過期。 如果存取權杖已過期，您將無法連線至Cloud Service執行個體，因此您需要擷取新的存取權杖。 與現有移轉集相關聯的狀態圖示會變更為紅色雲端，當您將游標暫留在紅色雲端上時，會顯示訊息。

* 內容轉移工具(CTT)在將內容從來源例項轉移至目標例項之前，不會執行任何類型的內容分析。 例如，CTT不會在將內容擷取至發佈環境時，區分已發佈和未發佈的內容。 無論移轉集中指定什麼內容，都會擷取至選取的目標例項。 使用者能將移轉集內嵌至製作例項、發佈例項或兩者。 建議將內容移至生產執行個體時，應在來源製作執行個體上安裝CTT，以將內容移至目標製作執行個體，同樣地，請在來源發佈執行個體上安裝CTT，將內容移至目標發佈執行個體。 如需詳細資訊，請參閱在發佈執行個體](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#running-ctt-on-publish)上執行內容轉移工具。[

* 「內容轉移工具」轉移的「使用者」和「群組」只是內容滿足權限所需的使用者和群組。 *提取*&#x200B;程式將整個`/home`複製到遷移集中，而&#x200B;*獲取*&#x200B;程式複製遷移內容ACL中引用的所有用戶和組。 若要自動將現有使用者和群組對應至其IMS ID，請參閱[使用使用者對應工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration)。

* 在提取階段中，「內容轉移工具」會在作用中的 AEM 來源例項上執行。

* 完成內容傳輸程式的&#x200B;*提取*&#x200B;階段之後，以及開始&#x200B;*擷取階段*&#x200B;將內容內嵌至您的AEMas a Cloud Service *階段*&#x200B;或&#x200B;*生產*&#x200B;例項之前，您需要記錄支援票證，以通知Adobe有意執行&#x200B;*擷取*，讓Adobe可確保在&#x200B;*擷取*&#x200B;過程期間不會發生中斷。 您需要在計畫的&#x200B;*擷取*&#x200B;日期前1週記錄支援票證。 一旦您提交了支援票證，支援團隊就會提供後續步驟的指引。 您可以記錄支援票證，並提供下列詳細資訊：

   * 計劃開始&#x200B;*擷取*&#x200B;階段時，確切的日期和估計時間（搭配您的時區）。
   * 您打算將資料內嵌至的環境類型（預備或生產）。
   * 方案ID。

* 製作的&#x200B;*擷取階段*&#x200B;會縮小整個製作部署。 這表示在整段擷取程序中，將無法使用製作 AEM。另外，請確定在您執行&#x200B;*擷取*&#x200B;階段時，不會執行任何Cloud Manager管道。

* 將`Amazon S3`或`Azure`用作源AEM系統上的資料儲存時，應配置資料儲存，以便無法刪除儲存的Blob（垃圾收集）。 這樣可確保索引資料的完整性，並且如果未能配置此方式，則可能由於此索引資料的完整性不完整而導致提取失敗。

* 如果您使用自訂索引，則在執行「內容轉移工具」之前，必須確保以`tika`節點配置自訂索引。 有關詳細資訊，請參閱[準備新索引定義](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#preparing-the-new-index-definition)。

* 如果您要追加提取，則必須不要變更現有內容的內容結構，從進行初始提取到執行追加提取的時間皆然。 自初始擷取後，結構已變更的內容無法執行追加。 請務必在移轉程式期間加以限制。

* 如果您要將版本納入移轉集，並要使用`wipe=false`執行追加，則必須由於「內容轉移工具」中的目前限制而停用版本清除。 如果您偏好保持版本清除已啟用，並在遷移集中執行追加，則必須以`wipe=true`的形式執行擷取。
