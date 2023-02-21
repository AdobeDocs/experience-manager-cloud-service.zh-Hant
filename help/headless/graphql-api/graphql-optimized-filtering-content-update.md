---
title: 更新內容片段以最佳化GraphQL篩選
description: 了解如何更新內容片段，以便在Adobe Experience Manager as a Cloud Service中最佳化GraphQL篩選以傳送無頭式內容。
source-git-commit: 7c6dcf4548972740803d64e21a74e885caf8b487
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 6%

---


# 更新內容片段以最佳化GraphQL篩選 {#updating-content-fragments-for-optimized-graphql-filtering}

若要最佳化GraphQL篩選器的效能，您需執行程式來更新內容片段。

>[!NOTE]
>
>更新內容片段後，您可以遵循 [最佳化GraphQL查詢](/help/headless/graphql-api/graphql-optimization.md).


## 必備條件 {#prerequisites}

確保您至少擁有2023.1.0版AEMas a Cloud Service。

## 更新內容片段 {#updating-content-fragments}

要運行該過程，請執行以下步驟：

1. 使用Cloud Manager UI為您的執行個體設定下列變數，以啟用更新：

   ![Cloud Manager環境配置](assets/cfm-graphql-update-01.png "Cloud Manager環境配置")

   可用的變數包括：

   <table style="table-layout:auto">
    <tbody>
     <tr>
      <th> </th>
      <th>名稱</th>
      <th>值</th>
      <th>預設值</th>
      <th>服務</th>
      <th>已套用</th>
      <th>類型</th>
      <th>附註</th>
     </tr>
     <tr>
      <td>1</td>
      <td>'AEM_RELEASE_CHANNEL' </td>
      <td>'prerelease' </td>
      <td> </td>
      <td>全部 </td>
      <td> </td>
      <td>變數 </td>
      <td>啟用功能時需要。 </td>
     </tr>
     <tr>
      <td>2</td>
      <td>'CF_MIGRATION_ENABLED' </td>
      <td>`1` </td>
      <td>`0` </td>
      <td>全部 </td>
      <td> </td>
      <td>變數 </td>
      <td>啟用(!=0)或停用(0)觸發內容片段移轉作業。 </td>
     </tr>
     <tr>
      <td>3</td>
      <td>'CF_MIGRATION_ENFORCE' </td>
      <td>`1` </td>
      <td>`0` </td>
      <td>全部 </td>
      <td> </td>
      <td>變數 </td>
      <td>強制(!=0)重新移轉內容片段。<br>將此標幟設為0將執行CF的增量遷移。 這表示，如果作業因任何原因而終止，則下次運行該作業將從其終止的位置開始遷移。 請注意，我們建議強制執行第一次移轉（值=1）。 </td>
     </tr>
     <tr>
      <td>4</td>
      <td>'CF_MIGRATION_BATCH' </td>
      <td>`50` </td>
      <td>`50` </td>
      <td>全部 </td>
      <td> </td>
      <td>變數 </td>
      <td>移轉後儲存內容片段數的批次大小。<br>這與以一批方式將多少個CF保存到儲存庫有關，並且可用於優化寫入儲存庫的次數。 </td>
     </tr>
     <tr>
      <td>5</td>
      <td>'CF_MIGRATION_LIMIT' </td>
      <td>`1000` </td>
      <td>`1000` </td>
      <td>全部 </td>
      <td> </td>
      <td>變數 </td>
      <td>一次要處理的內容片段數目上限。<br>另請參閱「CF_MIGRATION_INTERVAL」的附註。 </td>
     </tr>
     <tr>
      <td>6</td>
      <td>'CF_MIGRATION_INTERVAL' </td>
      <td>`60` </td>
      <td>`600` </td>
      <td>全部 </td>
      <td> </td>
      <td>變數 </td>
      <td>處理剩餘內容片段直到下一個限制的間隔（秒）<br>此間隔也視為開始作業前的等待時間，以及後續每個CF_MIGRATION_LIMIT數的處理之間的延遲。<br>(*)</td>
     </tr>
    </tbody>
   </table>

   >[!NOTE]
   >
   >(*)
   >
   >的值 `CF_MIGRATION_INTERVAL` 也有助於估算移轉作業的總執行時間。
   >
   >例如：
   >
   >* 內容片段總數= 20,000
   >* CF_MIGRATION_LIMIT = 1000
   >* CF_MIGRATION_INTERNAL = 60（秒）
   >* 完成移轉所需的約略時間= 60 +(20,000/1000 * 60)= 1260秒= 21分鐘
      >  開始時新增的額外「60」秒是因為開始工作時的初始延遲。

   >
   >您也應注意，這只是 *最小* 完成作業所需的時間，不包括I/O時間。 實際花費的時間可能比這個估計要多得多。

1. 監視進度和更新完成。

   若要這麼做，請監控作者的記錄，並透過以下網址取得golden-publish:

   * `com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob`

      * 作者記錄；例如：

         ```shell
         23.01.2023 13:13:45.926 *INFO* [sling-threadpool-09cbdb47-4d99-4c4c-b6d5-781b635ee21b-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob This instance<dd9ffdc1-0c28-4d04-9a96-5d4d223e457e> is the leader, will schedule the upgrade schedule job.
         ...
         23.01.2023 13:13:45.941 *INFO* [sling-threadpool-09cbdb47-4d99-4c4c-b6d5-781b635ee21b-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Scheduling content fragments upgrade from version 0 to 1, slingJobId: 2023/1/23/13/13/50e1a575-4cd7-497b-adf0-62cb5768eedb_0, enforce: true, limit: 1000, batch: 50, interval: 60s
         
         23.01.2023 13:20:40.960 *INFO* [sling-threadpool-09cbdb47-4d99-4c4c-b6d5-781b635ee21b-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Finished content fragments upgrade in 6m, slingJobId: 2023/1/23/13/13/50e1a575-4cd7-497b-adf0-62cb5768eedb_0, status: MaintenanceJobStatus{jobState=SUCCEEDED, statusMessage='Upgrade to version '1' succeeded.', errors=[], successCount=3781, failedCount=0, skippedCount=0}
         ```
   * Golden-publish日誌；例如：

      ```shell
      23.01.2023 12:35:05.150 *INFO* [sling-threadpool-8abcc1bb-cdcb-46d4-8565-942ad8a73209-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob This instance<ad1b399e-77be-408e-bc3f-57097498fddb> is the leader, will schedule the upgrade schedule job.
      
      23.01.2023 12:35:05.161 *INFO* [sling-threadpool-8abcc1bb-cdcb-46d4-8565-942ad8a73209-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Scheduling content fragments upgrade from version 0 to 1, slingJobId: 2023/1/23/12/34/ad1b399e-77be-408e-bc3f-57097498fddb_0, enforce: true, limit: 1000, batch: 50, interval: 60s
      ...
      23.01.2023 12:40:45.180 *INFO* [sling-threadpool-8abcc1bb-cdcb-46d4-8565-942ad8a73209-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Finished content fragments upgrade in 5m, slingJobId: 2023/1/23/12/34/ad1b399e-77be-408e-bc3f-57097498fddb_0, status: MaintenanceJobStatus{jobState=SUCCEEDED, statusMessage='Upgrade to version '1' succeeded.', errors=[], successCount=3781, failedCount=0, skippedCount=0}
      ```


1. 禁用更新過程。

   >[!IMPORTANT]
   >
   >完成升級需要此步驟。

   執行更新程式後，重設雲端環境變數 `CF_MIGRATION_ENABLED` 為「0」，以觸發所有豆莢的回收。

   <table style="table-layout:auto">
    <tbody>
     <tr>
      <th> </th>
      <th>名稱</th>
      <th>值</th>
      <th>預設值</th>
      <th>服務</th>
      <th>已套用</th>
      <th>類型</th>
      <th>附註</th>
     </tr>
     <tr>
      <td></td>
      <td>'CF_MIGRATION_ENABLED' </td>
      <td>`0` </td>
      <td>`0` </td>
      <td>全部 </td>
      <td> </td>
      <td>變數 </td>
      <td>禁用(0)(或啟用(!=0))觸發內容片段移轉作業。 </td>
     </tr>
    </tbody>
   </table>

   >[!NOTE]
   >
   >這對發佈層級尤其重要，因為內容更新僅在golden-publish上完成，而在回收Pod時，所有一般的發佈Pod都是以golden-publish為基礎。

1. 驗證更新過程的完成。

   您可以在Cloud Manager開發人員控制台中使用存放庫瀏覽器，檢查內容片段資料，以確認更新是否成功完成。

   * 在首次完成移轉前， `cfGlobalVersion` 屬性將不存在。
因此，此屬性在JCR節點上的存在 `/content/dam` 值為 `1`，確認移轉完成。

   * 您也可以檢查個別內容片段的下列屬性：

      * `_strucVersion` 應具有 `1`
      * `indexedData` 必須存在

      >[!NOTE]
      >
      >程式會更新製作和發佈執行個體上的內容片段。
      >
      >因此，建議您透過存放庫瀏覽器，對 *至少* 一位作者 *和* 一個發佈例項。


## 限制 {#limitations}

請注意下列限制：

* 只有在完整更新所有內容片段後（以下列方式表示），才能最佳化GraphQL篩選器的效能 `cfGlobalVersion` JCR節點的屬性 `/content/dam`)

* 如果從內容套件匯入內容片段(使用 `crx/de`)，則在GraphQL查詢結果中不會考慮這些內容片段，直到再次執行更新程式為止。