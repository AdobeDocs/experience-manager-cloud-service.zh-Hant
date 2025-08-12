---
title: 複製
description: 瞭解AEM as a Cloud Service中的散佈和疑難排解復寫問題。
exl-id: c84b4d29-d656-480a-a03a-fbeea16db4cd
feature: Operations
role: Admin
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '1711'
ht-degree: 1%

---

# 複製 {#replication}

Adobe Experience Manager as a Cloud Service使用[Sling內容發佈](https://sling.apache.org/documentation/bundles/content-distribution.html)功能將內容移動至復寫至AEM執行階段以外的Adobe Developer上執行的管道服務。

>[!NOTE]
>
>閱讀[發佈](/help/overview/architecture.md#content-distribution)以取得詳細資訊。

## 發佈內容的方法 {#methods-of-publishing-content}

>[!NOTE]
>
>如果您有興趣大量發佈內容，請使用[樹狀啟動工作流程步驟](#tree-activation)建立工作流程，以有效處理大量負載。
>&#x200B;>不建議建置您自己的大量發佈自訂程式碼。
>&#x200B;>如果您因任何原因必須自訂，則可使用現有的工作流程API，透過此步驟觸發工作流程。
>&#x200B;>只發佈必須發佈的內容永遠是好的做法。 如果不需要的話，也不要嘗試發佈大量內容。 不過，您可以使用樹狀啟動工作流程步驟在工作流程中傳送的內容數量並無限制。

### 快速取消/發佈 — 計畫取消/發佈 {#publish-unpublish}

此功能可讓您立即發佈所選頁面，無需透過「管理發布」方法選擇其他選項。

如需詳細資訊，請參閱[管理出版物](/help/sites-cloud/authoring/sites-console/publishing-pages.md#manage-publication)。

### 開啟和關閉時間 — 觸發器設定 {#on-and-off-times-trigger-configuration}

**開啟時間**&#x200B;和&#x200B;**關閉時間**&#x200B;的其他可能性可從頁面屬性[的](/help/sites-cloud/authoring/sites-console/page-properties.md#basic)基本索引標籤取得。

若要實現此功能的自動復寫，請在&#x200B;**OSGi設定** [開啟關閉觸發程式設定](/help/implementing/deploying/configuring-osgi.md)中啟用&#x200B;**自動復寫**：

![OSGi開啟關閉觸發器組態](/help/operations/assets/replication-on-off-trigger.png)

### 管理發佈 {#manage-publication}

管理發布提供比「快速發佈」更多的選項，允許包含子頁面、自訂參照和啟動任何適用的工作流程，並提供稍後發佈的選項。

為「稍後發佈」選項包含資料夾的子項時，會叫用發佈內容樹狀工作流程，如本文所述。

您可以在[出版基礎檔案](/help/sites-cloud/authoring/sites-console/publishing-pages.md#manage-publication)中找到有關管理出版的詳細資訊。

### 樹狀結構啟動工作流程步驟 {#tree-activation}

「樹啟動」工作流程步驟旨在有效複製內容節點的深層階層。 當佇列變得太大時，它會自動暫停，以允許其他複製以最小的延遲並行進行。

建立使用`TreeActivation`程式步驟的工作流程模型：

1. 從AEM as a Cloud Service首頁，移至&#x200B;**工具 — 工作流程 — 模型**。
1. 在「工作流程模型」頁面中，按畫面右上角的&#x200B;**建立**。
1. 新增標題和名稱至您的模型。 如需詳細資訊，請參閱[建立工作流程模型](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=zh-Hant)。
1. 從清單中選取建立的模型，然後按&#x200B;**編輯**
1. 在下列視窗中，刪除預設顯示的「步驟」
1. 將「處理步驟」拖放至目前的模型流程：

   ![處理步驟](/help/operations/assets/processstep.png)

1. 在流程中選取「處理」步驟，並按扳手圖示選取&#x200B;**設定**。
1. 選取「**處理序**」標籤，並從下拉式清單中選取「`Publish Content Tree`」，然後核取「**處理常式進階**」核取方塊

   ![樹狀結構啟動](/help/operations/assets/new-treeactivationstep.png)

1. 在&#x200B;**引數**&#x200B;欄位中設定任何其他引數。 多個以逗號分隔的引數可串連在一起。 例如：

   `enableVersion=false,agentId=publish,chunkSize=50,maxTreeSize=500000,dryRun=false,filters=onlyModified,maxQueueSize=10`

   >[!NOTE]
   >
   >如需引數清單，請參閱下方的&#x200B;**引數**&#x200B;區段。

1. 按下&#x200B;**完成**&#x200B;以儲存工作流程模型。

**引數**

| 名稱 | 預設 | 說明 |
| -------------- | ------- | --------------------------------------------------------------- |
| 路徑 |         | 要開始的根路徑 |
| agentId | 發佈 | 要使用的復寫代理程式名稱 |
| chunkSize | 50 | 要繫結到單一復寫中的路徑數量 |
| maxTreeSize | 500000 | 樹狀結構可視為小型的最大節點數 |
| maxQueueSize | 10 | 復寫佇列中的專案數上限 |
| enableVersion | false | 啟用版本設定 |
| 練習版 | false | 設定為true時，實際上不會呼叫復寫 |
| userId |         | 僅適用於工作。 在工作流程中，會使用呼叫工作流程的使用者 |
| 個篩選條件 |         | 節點篩選器名稱清單。 請參閱下方支援的篩選器 |

**支援篩選器**

| 名稱 | 說明 |
| ------------- | ------------------------------------------- |
| onlyModified | 節點：自上次發佈後已修改的新節點和預先存在的節點 |
| onlyActivated | 節點：上次發佈前已發佈的節點 |


**繼續支援**

工作流程會以區塊處理內容，每個區塊代表要發佈的完整內容子集。  如果系統停止工作流程，則會從中斷處繼續。

**監視工作流程進度**

1. 從AEM as a Cloud Service首頁，移至&#x200B;**工具 — 一般 — 工作**。
1. 檢視與工作流程對應的列。 *progress*&#x200B;資料行會顯示復寫進度。 例如，它可能會顯示41/564，而在重新整理時，它可能會更新為52/564。

   ![樹狀啟動進度](/help/operations/assets/treeactivation-progress.png)


1. 選取列並開啟它可提供工作流程執行狀態的更多詳細資訊。

   ![樹狀啟動狀態詳細資料](/help/operations/assets/treeactivation-progress-details.png)



### 發佈內容樹狀工作流程 {#publish-content-tree-workflow}

>[!NOTE]
>
>此功能已淘汰，以支援更高效能的樹狀結構啟動步驟（可包含在自訂工作流程中）。

+++ 按一下這裡以深入瞭解這項已棄用的功能。

您可以選擇&#x200B;**工具 — 工作流程 — 模型**&#x200B;並複製&#x200B;**發佈內容樹狀結構**&#x200B;現成的工作流程模型，以觸發樹狀結構復寫，如下所示：

![發佈內容樹狀工作流程卡](/help/operations/assets/publishcontenttreeworkflow.png)

請勿叫用原始模型。 相反，請務必先複製模型並叫用該副本。

如同所有工作流程，您也可以透過API叫用。 如需詳細資訊，請參閱[以程式設計方式與工作流程互動](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-program-interaction.html?lang=zh-Hant#extending-aem)。

或者，您也可以建立使用`Publish Content Tree`處理步驟的工作流程模型。

1. 從AEM as a Cloud Service首頁，移至&#x200B;**工具 — 工作流程 — 模型**。
1. 在「工作流程模型」頁面中，按畫面右上角的&#x200B;**建立**。
1. 新增標題和名稱至您的模型。 如需詳細資訊，請參閱[建立工作流程模型](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=zh-Hant)。
1. 從清單中選取建立的模型，然後按&#x200B;**編輯**
1. 在下列視窗中，將「處理步驟」拖放至目前的模型流程：

   ![處理步驟](/help/operations/assets/processstep.png)

1. 在流程中選取「處理」步驟，並按扳手圖示選取&#x200B;**設定**。
1. 選取「**處理序**」標籤，並從下拉式清單中選取「`Publish Content Tree`」，然後核取「**處理常式進階**」核取方塊

   ![樹狀結構啟動](/help/operations/assets/newstep.png)

1. 在&#x200B;**引數**&#x200B;欄位中設定任何其他引數。 多個以逗號分隔的引數可串連在一起。 例如：

   `enableVersion=true,agentId=publish,includeChildren=true`


   >[!NOTE]
   >
   >如需引數清單，請參閱下方的&#x200B;**引數**&#x200B;區段。

1. 按下&#x200B;**完成**&#x200B;以儲存工作流程模型。

**引數**

* `includeChildren` （布林值，預設： `false`）。 值`false`表示僅發佈路徑；`true`表示也發佈子項。
* `replicateAsParticipant` （布林值，預設： `false`）。 如果設定為`true`，則復寫使用執行參與者步驟的主體`userid`。
* `enableVersion` （布林值，預設： `false`）。 此引數會決定複製時是否建立新版本。
* `agentId` （字串值，預設值表示僅使用發佈代理程式）。 建議您清楚說明agentId，例如設定值： publish。 正在將代理程式設定為`preview`發佈到預覽服務。
* `filters` （字串值，預設值代表所有路徑都已啟動）。 可用的值包括：
   * `onlyActivated` — 僅啟動已（已）啟動的頁面。 作為重新啟用的一種形式。
   * `onlyModified` — 僅啟動已啟動且修改日期晚於啟動日期的路徑。
   * 以上可以用垂直號「|」進行「或」操作。 例如，`onlyActivated|onlyModified`。

**記錄**

樹狀結構啟動工作流程步驟啟動時，會在「資訊」記錄層級記錄其設定引數。 啟動路徑時，也會記錄INFO陳述式。

在工作流程步驟已複製所有路徑之後，會記錄最終的INFO陳述式。

此外，您也可以將記錄器的記錄層級增加到`com.day.cq.wcm.workflow.process.impl`以下的DEBUG/TRACE，以取得更多記錄資訊。

如果有錯誤，工作流程步驟會以`WorkflowException`結束，這會包裝基礎例外狀況。

以下是在範例發佈內容樹狀工作流程期間產生的記錄範例：

```
21.04.2021 19:14:55.566 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.treeactivation.TreeActivationWorkflowProcess TreeActivation options: replicateAsParticipant=false(userid=workflow-process-service), agentId=publish, chunkSize=100, filter=, enableVersion=false
```

```
21.04.2021 19:14:58.541 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.ChunkedReplicator closing chunkedReplication-VolatileWorkItem_node1_var_workflow_instances_server60_2021-04-20_brian-tree-replication-test-2_1, 17 paths replicated in 2971 ms
```

+++

### 復寫API {#replication-api}

您可以使用AEM as a Cloud Service提供的復寫API發佈內容。

如需詳細資訊，請參閱[API檔案](https://javadoc.io/doc/com.adobe.aem/aem-sdk-api/latest/com/day/cq/replication/package-summary.html)。

**API的基本用法**

```
@Reference
Replicator replicator;
@Reference
ReplicationStatusProvider replicationStatusProvider;

....
Session session = ...
// Activate a single page to all agents, which are active by default
replicator.replicate(session,ReplicationActionType.ACTIVATE,"/content/we-retail/en");
// Activate multiple pages (but try to limit it to approx 100 at max)
replicator.replicate(session,ReplicationActionType.ACTIVATE, new String[]{"/content/we-retail/en","/content/we-retail/de"});

// ways to get the replication status
Resource enResource = resourceResolver.getResource("/content/we-retail/en");
Resource deResource = resourceResolver.getResource("/content/we-retail/de");
ReplicationStatus enStatus = enResource.adaptTo(ReplicationStatus.class);
// if you need to get the status for more more than 1 resource at once, this approach is more performant
Map<String,ReplicationStatus> allStatus = replicationStatusProvider.getBatchReplicationStatus(enResource,deResource);
```

**使用特定代理程式復寫**

如上例所示，複製資源時，只會使用預設為作用中的代理程式。 在AEM as a Cloud Service中，這僅表示稱為「發佈」的代理程式，其會將作者連線到發佈層級。

為了支援預覽功能，已新增名為「預覽」的新代理程式，預設為不啟用。 此代理程式用於將作者連線到預覽層。 如果您只想透過預覽代理程式復寫，您必須透過`AgentFilter`明確選取此預覽代理程式。

請參閱下列範例：

```
private static final String PREVIEW_AGENT = "preview";

ReplicationStatus beforeStatus = enResource.adaptTo(ReplicationStatus.class); // beforeStatus.isActivated == false

ReplicationOptions options = new ReplicationOptions();
options.setFilter(new AgentFilter() {
  @Override
  public boolean isIncluded (Agent agent) {
    return agent.getId().equals(PREVIEW_AGENT);
  }
});
// will replicate only to preview
replicator.replicate(session,ReplicationActionType.ACTIVATE,"/content/we-retail/en", options);

ReplicationStatus afterStatus = enResource.adaptTo(ReplicationStatus.class); // afterStatus.isActivated == false
ReplicationStatus previewStatus = afterStatus.getStatusForAgent(PREVIEW_AGENT); // previewStatus.isActivated == true
```

如果您未提供這類篩選器，且只使用「發佈」代理程式，則不會使用「預覽」代理程式，且復寫動作不會影響預覽階層。

只有當復寫動作包含至少一個預設為作用中的代理程式時，才會修改資源的整體`ReplicationStatus`。 在上述範例中，此流程並非真實情況。 復寫只是使用「預覽」代理程式。 因此，您必須使用新的`getStatusForAgent()`方法，允許查詢特定代理程式的狀態。 此方法也適用於「發佈」代理。 如果已使用提供的代理程式完成任何復寫動作，則會傳回非null值。

### 讓內容失效的方法 {#invalidating-content}

您可以使用作者的Sling內容失效(SCD) （偏好方法）或使用復寫API叫用發佈Dispatcher Flush復寫代理程式，直接讓內容失效。 如需詳細資訊，請參閱[快取](/help/implementing/dispatcher/caching.md)頁面。

**復寫API容量限制**

一次複製少於100個路徑，以500為限制。 超過限制，擲回`ReplicationException`。
如果您的應用程式邏輯不需要原子式復寫，您可以將`ReplicationOptions.setUseAtomicCalls`設定為false，這會接受任何數量的路徑，但在內部建立儲存貯體以保持在此限制以下。

每個復寫呼叫所傳輸的內容大小不得超過`10 MB`。 此規則包含節點和屬性，但不包含任何二進位檔（工作流程套件和內容套件會視為二進位檔）。


## 疑難排解 {#troubleshooting}

若要進行復寫疑難排解，請導覽至AEM作者服務Web UI中的復寫佇列：

1. 從AEM [全域導覽](/help/sites-cloud/authoring/basic-handling.md#global-navigation)，導覽至&#x200B;**工具** > **部署** > **發佈**
1. 選取卡片&#x200B;**發佈**

   ![狀態](assets/publish-status.png "狀態")

1. 檢查應為綠色的佇列狀態
1. 您可以測試復寫服務的連線
1. 選取&#x200B;**記錄檔**&#x200B;標籤，顯示內容發佈的歷史記錄

![個記錄檔](assets/publish-logs.png "個記錄檔")

如果內容無法發佈，則整個發佈將從AEM發佈服務中還原。

在這種情況下，可編輯的主要佇列會顯示紅色狀態，應該加以檢閱以識別哪些專案導致取消發佈。 按一下該佇列，會顯示其暫止專案，如有需要，可從中清除單一專案或所有專案。
