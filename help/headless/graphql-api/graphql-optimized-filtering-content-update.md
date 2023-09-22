---
title: 更新您的內容片段，以達到最佳化 GraphQL 篩選
description: 了解如何更新您的內容片段，以便在 Adobe Experience Manager as a Cloud Service 中達到最佳化 GraphQL 篩選，並實現 Headless 內容傳遞。
exl-id: 211f079e-d129-4905-a56a-4fddc11551cc
source-git-commit: 97a6a7865f696f4d61a1fb4e25619caac7b68b51
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 60%

---

# 更新您的內容片段，以達到最佳化 GraphQL 篩選 {#updating-content-fragments-for-optimized-graphql-filtering}

若要最佳化GraphQL篩選器的效能，請執行程式來更新您的內容片段。

>[!NOTE]
>
>更新您的內容片段後，您可以遵循的建議 [最佳化GraphQL查詢](/help/headless/graphql-api/graphql-optimization.md).


## 先決條件 {#prerequisites}

此任務的必備條件：

1. 確保您至少擁有 2023.1.0 版本的 AEM as a Cloud Service。

1. 確保執行任務的使用者具有必要權限：

   * 至少， `Deployment Manager` 需要Cloud Manager中的角色。

## 更新您的內容片段 {#updating-content-fragments}

1. 透過使用 Cloud Manager UI 為您的執行個體設定以下變數來啟用更新：

   ![Cloud Manager 環境設定](assets/cfm-graphql-update-01.png "Cloud Manager 環境設定")

   可用變數為：

   <table style="table-layout:auto">
    <tbody>
     <tr>
      <th> </th>
      <th>名稱</th>
      <th>值</th>
      <th>預設值</th>
      <th>服務</th>
      <th>已應用</th>
      <th>類型</th>
      <th>附註</th>
     </tr>

   <tr>
      <td>1</td>
      <td>`CF_MIGRATION_ENABLED` </td>
      <td>`1` </td>
      <td>`0` </td>
      <td>全部 </td>
      <td> </td>
      <td>變數 </td>
      <td>啟用(!=0) 或停用 (0) 觸發內容片段遷移作業。 </td>
     </tr>
     <tr>
      <td>2</td>
      <td>`CF_MIGRATION_ENFORCE` </td>
      <td>`1` </td>
      <td>`0` </td>
      <td>全部 </td>
      <td> </td>
      <td>變數 </td>
      <td>執行 (!=0)重新移轉內容片段。<br>將此標幟設為0會執行CF的遞增移轉。 這表示，如果工作因任何原因而終止，則工作的下次執行會從工作終止的點開始移轉。 建議執行第一次移轉（值=1）。 </td>
     </tr>
     <tr>
      <td>3</td>
      <td>`CF_MIGRATION_BATCH` </td>
      <td>`50` </td>
      <td>`50` </td>
      <td>全部 </td>
      <td> </td>
      <td>變數 </td>
      <td>用於儲存移轉後內容片段數的批次大小。<br>這與一次儲存至存放庫的CF數量相關，並可用於最佳化寫入存放庫的次數。 </td>
     </tr>
     <tr>
      <td>4</td>
      <td>`CF_MIGRATION_LIMIT` </td>
      <td>`1000` </td>
      <td>`1000` </td>
      <td>全部 </td>
      <td> </td>
      <td>變數 </td>
      <td>一次處理的最大數量的內容片段。<br>另請參閱 “CF_MIGRATION_INTERVAL” 的註釋。 </td>
     </tr>
     <tr>
      <td>5</td>
      <td>`CF_MIGRATION_INTERVAL` </td>
      <td>`60` </td>
      <td>`600` </td>
      <td>全部 </td>
      <td> </td>
      <td>變數 </td>
      <td>處理剩餘內容片段直到下一個限制的間隔（秒）<br>此間隔也會被視為啟動作業前的等待時間，以及處理每個後續CF_MIGRATION_LIMIT數目CF之間的延遲。<br>(*)</td>
     </tr>
    </tbody>
   </table>

   >[!NOTE]
   >
   >(*)
   >
   >`CF_MIGRATION_INTERVAL` 值還可以幫助估計遷移作業的總執行時間。
   >
   >例如：
   >
   >* 內容片段總數 = 20,000
   >* CF_MIGRATION_LIMIT = 1000
   >* CF_MIGRATION_INTERNAL = 60 (秒)
   >* 完成遷移所需的大約時間 = 60 + (20,000/1000 * 60) = 1260 秒 = 21 分鐘
   >  在開始時增加的額外「60」秒是由於開始作業時的初始延遲。
   >
   >這只是 *最小值* 完成工作所需的時間，但不包括I/O時間。 實際花費的時間可能超過此預估值。

1. 監視更新的進度和完成。

   為此，請從以下位置監控作者和 golden-publish 的記錄：

   * `com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob`

      * 作者記錄；例如：

        ```shell
        23.01.2023 13:13:45.926 *INFO* [sling-threadpool-09cbdb47-4d99-4c4c-b6d5-781b635ee21b-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob This instance<dd9ffdc1-0c28-4d04-9a96-5d4d223e457e> is the leader, will schedule the upgrade schedule job.
        ...
        23.01.2023 13:13:45.941 *INFO* [sling-threadpool-09cbdb47-4d99-4c4c-b6d5-781b635ee21b-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Scheduling content fragments upgrade from version 0 to 1, slingJobId: 2023/1/23/13/13/50e1a575-4cd7-497b-adf0-62cb5768eedb_0, enforce: true, limit: 1000, batch: 50, interval: 60s
        
        23.01.2023 13:20:40.960 *INFO* [sling-threadpool-09cbdb47-4d99-4c4c-b6d5-781b635ee21b-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Finished content fragments upgrade in 6m, slingJobId: 2023/1/23/13/13/50e1a575-4cd7-497b-adf0-62cb5768eedb_0, status: MaintenanceJobStatus{jobState=SUCCEEDED, statusMessage='Upgrade to version '1' succeeded.', errors=[], successCount=3781, failedCount=0, skippedCount=0}
        ```

      * Golden-publish 記錄；例如：

        ```shell
        23.01.2023 12:35:05.150 *INFO* [sling-threadpool-8abcc1bb-cdcb-46d4-8565-942ad8a73209-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob This instance<ad1b399e-77be-408e-bc3f-57097498fddb> is the leader, will schedule the upgrade schedule job.
        
        23.01.2023 12:35:05.161 *INFO* [sling-threadpool-8abcc1bb-cdcb-46d4-8565-942ad8a73209-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Scheduling content fragments upgrade from version 0 to 1, slingJobId: 2023/1/23/12/34/ad1b399e-77be-408e-bc3f-57097498fddb_0, enforce: true, limit: 1000, batch: 50, interval: 60s
        ...
        23.01.2023 12:40:45.180 *INFO* [sling-threadpool-8abcc1bb-cdcb-46d4-8565-942ad8a73209-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Finished content fragments upgrade in 5m, slingJobId: 2023/1/23/12/34/ad1b399e-77be-408e-bc3f-57097498fddb_0, status: MaintenanceJobStatus{jobState=SUCCEEDED, statusMessage='Upgrade to version '1' succeeded.', errors=[], successCount=3781, failedCount=0, skippedCount=0}
        ```

   使用 Splunk 啟用環境記錄存取權的客戶可以使用下面的範例查詢來監控升級程序。如需有關啟用Splunk記錄的詳細資訊，請參閱 [偵錯生產和中繼](/help/implementing/developing/introduction/logging.md#debugging-production-and-stage).

   ```splunk
   index=<indexName> sourcetype=aemerror aem_envId=<environmentId> msg="*com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Finished*" 
   (aem_tier=golden-publish OR aem_tier=author) | table _time aem_tier pod_name msg | sort -_time desc
   ```

   其中：

   * `environmentId`- 客戶環境識別碼；例如，`e1234`
   * `indexName`- 客戶索引名稱，收集 `aemerror` 事件

   輸出範例：

   <table style="table-layout:auto">
     <thead>
       <tr>
       <th>_time</th>
       <th>aem_tier</th>
       <th>pod_name</th>
       <th>msg</th>
       </tr>
     </thead> 
     <tbody>
       <tr>
         <td>2023-04-21 06:00:35.723</td>
         <td>作者</td>
         <td>cm-p1234-e1234-aem-author-76d6dc4b79-8lsb5</td>
         <td>[sling-threadpool-bb5da4dd-6b05-4230-93ea-1d5cd242e24f-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Finished content fragments upgrade in 391m, slingJobId: 2023/4/20/23/16/db7963df-e267-489b-b69a-5930b0dadb37_0, status: MaintenanceJobStatus{jobState=SUCCEEDED, statusMessage='Upgrade to version '1' succeeded.', errors=[], successCount=36756, failedCount=0, skippedCount=0}</td>
       </tr>
       <tr>
         <td>2023-04-21 06:05:48.207</td>
         <td>golden-publish</td>
         <td>cm-p1234-e1234-aem-golden-publish-644487c9c5-lvkv2</td>
         <td>[sling-threadpool-284b9a9a-8454-461e-9bdb-44866c6ddfb1-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Finished content fragments upgrade in 211m, slingJobId: 2023/4/20/23/15/66c1690a-cdb7-4e66-bc52-90f33394ddfc_0, status: MaintenanceJobStatus{jobState=SUCCEEDED, statusMessage='Upgrade to version '1' succeeded.', errors=[], successCount=19557, failedCount=0, skippedCount=0}</td>
       </tr>
     </tbody>
   <table>

1. 停用更新程序。

   >[!IMPORTANT]
   >
   >這是完成升級必要的步驟。

   執行更新程序後，將雲端環境變數 `CF_MIGRATION_ENABLED` 重設為 “0”，以觸發所有 pod 的回收。

   <table style="table-layout:auto">
    <tbody>
     <tr>
      <th> </th>
      <th>名稱</th>
      <th>值</th>
      <th>預設值</th>
      <th>服務</th>
      <th>已應用</th>
      <th>類型</th>
      <th>附註</th>
     </tr>
     <tr>
      <td></td>
      <td>`CF_MIGRATION_ENABLED` </td>
      <td>`0` </td>
      <td>`0` </td>
      <td>全部 </td>
      <td> </td>
      <td>變數 </td>
      <td>停用(0) (或啟用(!=0)) 觸發內容片段遷移作業。 </td>
     </tr>
    </tbody>
   </table>

   >[!NOTE]
   >
   >這對發佈層級很重要，因為內容更新只會在Golden-publish上完成，而且當回收Pod時，所有一般發佈Pod都會以Golden-publish為基礎。

1. 驗證更新程序的完成。

   您可以使用 Cloud Manager Developer Console 中的存放庫瀏覽器來驗證更新是否成功完成，以檢查內容片段資料。

   * 在第一次完整移轉前， `cfGlobalVersion` 屬性不存在。
因此，該屬性 (在 JCR 節點 `/content/dam` 上且值為 `1`) 的存在可確認遷移完成。

   * 您還可以查看個別內容片段的以下屬性：

      * `_strucVersion` 應具有 `1` 的值
      * `indexedData` 結構必須存在

     >[!NOTE]
     >
     >此程式會更新作者和發佈執行個體上的內容片段。
     >
     >因此，Adobe建議您透過以下專案的存放庫瀏覽器執行驗證： *至少* 一位作者 *和* 一個發佈執行個體。

## 限制 {#limitations}

留意以下限制：

* 只有在完成所有內容片段的更新後（以「 」的存在表示），GraphQL篩選器的效能才能最佳化。 `cfGlobalVersion` JCR節點的屬性 `/content/dam`)

* 如果內容片段是從內容套件匯入(使用 `crx/de`)後，則不會在GraphQL查詢結果中考慮這些內容片段，直到再次執行更新程式為止。
