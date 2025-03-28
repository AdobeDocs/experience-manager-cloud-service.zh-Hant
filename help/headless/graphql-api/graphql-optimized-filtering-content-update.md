---
title: 更新您的內容片段，以達到最佳化 GraphQL 篩選
description: 了解如何更新您的內容片段，以便在 Adobe Experience Manager as a Cloud Service 中達到最佳化 GraphQL 篩選，並實現 Headless 內容傳遞。
exl-id: 211f079e-d129-4905-a56a-4fddc11551cc
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: 8d14936ad21dc5879c72383defc3db22ce9a24ef
workflow-type: ht
source-wordcount: '867'
ht-degree: 100%

---

# 更新您的內容片段，以達到最佳化 GraphQL 篩選 {#updating-content-fragments-for-optimized-graphql-filtering}

若要最佳化 GraphQL 篩選器的效能，可執行一個程序來更新您的內容片段。

>[!NOTE]
>
>更新內容片段後，您可以依照[最佳化 GraphQL 查詢](/help/headless/graphql-api/graphql-optimization.md)的建議進行。


## 先決條件 {#prerequisites}

此任務的必備條件：

1. 確保您至少擁有 2023.1.0 版本的 AEM as a Cloud Service。

1. 確保執行任務的使用者具有必要權限：

   * 至少要在 Cloud Manager 中具備 `Deployment Manager` 角色。

## 更新您的內容片段 {#updating-content-fragments}

1. 透過使用 Cloud Manager UI 為您的執行個體設定以下變數來啟用更新：

   ![Cloud Manager 環境設定](assets/cfm-graphql-update-01.png "Cloud Manager 環境設定")

   可用變數為：

   | | 名稱 | 值 | 預設值 | 服務 | 已應用 | 類型 | 附註 |
   |---|---|---|---|---|---|---|---|
   | 1 | `CF_MIGRATION_ENABLED` | `1` | `0` | 全部 | | 變數 | 啟用(!=0) 或停用 (0) 觸發內容片段遷移作業。 |
   | 2 | `CF_MIGRATION_ENFORCE` | `1` | `0` | 全部 | | 變數 | 執行 (!=0) 內容片段的重新遷移。將此標幟設定為 0 可執行 CF 的增量遷移。這表示，如果作業由於任何原因終止，則下一次執行作業會從作業被終止的那個點開始遷移。建議強制執行第一次遷移 (值=1)。 |
   | 3 | `CF_MIGRATION_BATCH` | `50` | `50` | 全部 | | 變數 | 遷移後用來儲存內容片段數量的批次大小。這與單批中多少個 CF 儲存到存放庫中有關，並且可以用來最佳化寫入存放庫的數量。 |
   | 4 | `CF_MIGRATION_LIMIT` | `1000` | `1000` | 全部 | | 變數 | 一次處理的最大數量的內容片段。另請參閱 `CF_MIGRATION_INTERVAL` 的說明。 |
   | 5 | `CF_MIGRATION_INTERVAL` | `60` | `600` | 全部 | | 變數 | 處理剩餘內容片段直到下一個限制的時間間隔 (秒)。這個間隔時間也視為開始作業前的等待時間，以及處理每個後續 CF_MIGRATION_LIMIT 數量的內容片段之間的延遲時間。(*) |

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
   >這只是完成作業所需的&#x200B;*最短*&#x200B;時間，不包括 I/O 時間。實際花費的時間可能超過這個估計。

1. 監控更新的進度和完成情況。

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

   使用 Splunk 啟用環境記錄存取權的客戶可以使用下面的範例查詢來監控升級程序。如需有關啟用 Splunk 記錄的詳細資訊，請參閱[偵錯生產和階段](/help/implementing/developing/introduction/logging.md#debugging-production-and-stage)。

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

   | | 名稱 | 值 | 預設值 | 服務 | 已應用 | 類型 | 附註 |
   |---|---|---|---|---|---|---|---|
   | | `CF_MIGRATION_ENABLED` | `0` | `0` | 全部 | | 變數 | 停用(0) (或啟用(!=0)) 觸發內容片段遷移作業。 |

   >[!NOTE]
   >
   >這對於發佈層很重要，因為內容更新僅在 golden-publish 上進行，並且在回收 pod 時，所有正常的 publish pod 都是以 golden-publish 為主。

1. 驗證更新程序的完成。

   您可以使用 Cloud Manager Developer Console 中的存放庫瀏覽器來驗證更新是否成功完成，以檢查內容片段資料。

   * 在第一次完整遷移之前，`cfGlobalVersion` 屬性不存在。
因此，該屬性 (在 JCR 節點 `/content/dam` 上且值為 `1`) 的存在可確認遷移完成。

   * 您還可以查看個別內容片段的以下屬性：

      * `_strucVersion` 應具有 `1` 的值
      * `indexedData` 結構必須存在

     >[!NOTE]
     >
     >該程序會更新作者和發佈執行個體上的內容片段。
     >
     >因此，Adobe 建議您經由存放庫瀏覽器對&#x200B;*至少*&#x200B;一位作者&#x200B;*和*&#x200B;一個發佈執個體進行驗證。

## 限制 {#limitations}

留意以下限制：

* GraphQL 篩選器的效能最佳化只有在完全更新所有內容片段後才有可能 (由 JCR 節點 `/content/dam` 的 `cfGlobalVersion` 屬性存在來表示)

* 如果在執行更新程序後從內容套組 (使用 `crx/de`) 匯入內容片段，則在再次執行更新程序之前，GraphQL 查詢結果中不會考慮這些內容片段。
