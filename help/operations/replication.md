---
title: 複製
description: 分發和排除複製故障。
exl-id: c84b4d29-d656-480a-a03a-fbeea16db4cd
source-git-commit: 91a13f8b23136298e0ccf494e51fccf94fa1e0b4
workflow-type: tm+mt
source-wordcount: '1335'
ht-degree: 1%

---

# 複製 {#replication}

Adobe Experience Manager as a Cloud Service使用 [Sling內容分發](https://sling.apache.org/documentation/bundles/content-distribution.html) 將要複製的內容移動到運行時之外的Adobe Developer上的管道服AEM務。

>[!NOTE]
>
>閱讀 [分佈](/help/overview/architecture.md#content-distribution) 的子菜單。

## 發佈內容的方法 {#methods-of-publishing-content}

>[!NOTE]
>
>如果您對批量發佈內容感興趣，請使用 [發佈內容樹工作流](#publish-content-tree-workflow)。
>此工作流步驟專門為Cloud Service而構建，並可以高效地處理大負載。
>建議不要構建您自己的批量發佈自定義代碼。
>如果必須出於任何原因進行自定義，則可以使用現有的工作流API觸發此工作流/工作流步驟。
>只發佈必須發佈的內容始終是一種良好做法。 而且，如果沒有必要，也要小心不要試圖發佈大量內容。 但是，通過「發佈內容樹工作流」可以發送多少內容沒有限制。

### 快速取消/發佈 — 計畫取消/發佈 {#publish-unpublish}

此功能允許您立即發佈選定的頁面，而無需通過「管理發布」方法提供其他選項。

有關詳細資訊，請參見 [管理發布](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#manage-publication)。

### 開啟和關閉時間 — 觸發器配置 {#on-and-off-times-trigger-configuration}

其他可能性 **準時** 和 **關機時間** 可從 [「頁面屬性」的「基本」頁籤](/help/sites-cloud/authoring/fundamentals/page-properties.md#basic)。

要實現此功能的自動複製，請啟用 **自動複製** 的 [OSGi配置](/help/implementing/deploying/configuring-osgi.md) **開關觸發器配置**:

![OSGi開關觸發器配置](/help/operations/assets/replication-on-off-trigger.png)

### 管理發佈 {#manage-publication}

「管理發布」提供的選項比「快速發佈」更多，允許包含子頁、自定義引用、啟動任何適用的工作流以及提供以後發佈的選項。

為「以後發佈」選項包括資料夾的子項會調用「發佈內容樹」工作流，本文對此進行了介紹。

您可以在 [發佈基礎文檔](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#manage-publication)。

### 發佈內容樹狀工作流程 {#publish-content-tree-workflow}

通過選擇 **工具 — 工作流 — 模型** 複製 **發佈內容樹** 現成工作流模型，如下所示：

![](/help/operations/assets/publishcontenttreeworkflow.png)

不要修改或調用原始模型。 相反，請確保首先複製模型，然後修改或調用該副本。

與所有工作流一樣，它也可以通過API調用。 有關詳細資訊，請參見 [以寫程式方式與工作流交互](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-program-interaction.html?lang=en#extending-aem)。

或者，可以建立使用 `Publish Content Tree` 流程步驟：

1. 從AEMas a Cloud Service首頁 **工具 — 工作流 — 模型**。
1. 在「工作流模型」頁中，按 **建立** 的下界。
1. 將標題和名稱添加到模型。 有關詳細資訊，請參見 [建立工作流模型](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html)。
1. 從清單中選擇新建立的模型，然後按 **編輯**
1. 在以下窗口中，將「處理步驟」拖放到當前模型流中：

   ![程序步驟](/help/operations/assets/processstep.png)

1. 在流中選擇「處理」步驟並選擇 **配置** 按扳手錶徵圖。
1. 選擇 **進程** 頁籤 `Publish Content Tree` 從下拉清單中，檢查 **處理程式高級** 複選框

   ![樹激活](/help/operations/assets/newstep.png)

1. 在 **參數** 的子菜單。 可將多個逗號分隔的參數串在一起。 例如：

   `enableVersion=true,agentId=publish,includeChildren=true`


   >[!NOTE]
   >
   >有關參數清單，請參見 **參數** 的下界。

1. 按 **完成** 的子菜單。

**參數**

* `includeChildren` (布爾值，預設值： `false`)。 值 `false` 即只發佈路徑； `true` 意味著孩子也會被出版。
* `replicateAsParticipant` (布爾值，預設值： `false`)。 如果配置為 `true`，複製正在使用 `userid` 參與者步驟的主體。
* `enableVersion` (布爾值，預設值： `true`)。 此參數確定複製時是否建立了新版本。
* `agentId` （字串值，預設表示只使用發佈代理）。 建議對agentId進行顯式；例如，設定該值：發佈。 將代理設定為 `preview` 發佈到預覽服務。
* `filters` （字串值，預設表示已激活所有路徑）。 可用值包括：
   * `onlyActivated`  — 僅激活已（已）激活的頁面。 充當一種重新激活的形式。
   * `onlyModified`  — 僅激活已激活且修改日期晚於激活日期的路徑。
   * 上面可以用管道「|」來對齊。 比如說， `onlyActivated|onlyModified`。

**記錄**

樹激活工作流步驟啟動時，它會在INFO日誌級別上記錄其配置參數。 激活路徑後，還會記錄INFO語句。

工作流步驟複製所有路徑後，將記錄最終的INFO語句。

此外，您還可以提高以下伐木者的伐木水準 `com.day.cq.wcm.workflow.process.impl` 到DEBUG/TRACE以獲取更多日誌資訊。

如果存在錯誤，則工作流步驟將終止， `WorkflowException`，它包含基礎異常。

以下是示例發佈內容樹工作流期間生成的日誌示例：

```
21.04.2021 19:14:55.566 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.treeactivation.TreeActivationWorkflowProcess TreeActivation options: replicateAsParticipant=false(userid=workflow-process-service), agentId=publish, chunkSize=100, filter=, enableVersion=false
```

```
21.04.2021 19:14:58.541 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.ChunkedReplicator closing chunkedReplication-VolatileWorkItem_node1_var_workflow_instances_server60_2021-04-20_brian-tree-replication-test-2_1, 17 paths replicated in 2971 ms
```

**恢復支援**

工作流以塊的形式處理內容，每個塊都表示要發佈的完整內容的子集。 如果系統停止了工作流，它將重新啟動並處理尚未處理的塊。 日誌語句聲明內容已從特定路徑恢復。

### 複製API {#replication-api}

您可以使用as a Cloud Service中提供的複製API發佈AEM內容。

有關詳細資訊，請參見 [API文檔](https://javadoc.io/doc/com.adobe.aem/aem-sdk-api/latest/com/day/cq/replication/package-summary.html)。

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

**使用特定代理進行複製**

複製資源時（如上例所示），僅使用預設處於活動狀態的代理。 在AEMas a Cloud Service中，它只表示名為「publish」的代理，將作者連接到發佈層。

為支援預覽功能，已添加名為「預覽」的新代理，預設情況下該代理不處於活動狀態。 此代理用於將作者連接到預覽層。 如果僅希望通過預覽代理進行複製，則必須通過 `AgentFilter`。

請參閱以下示例：

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

如果您未提供此類篩選器並且僅使用「發佈」代理，則不使用「預覽」代理，並且複製操作不會影響預覽層。

整體 `ReplicationStatus` 僅當複製操作包括至少一個預設處於活動狀態的代理時，才修改資源的。 在上面的示例中，此流不是。 複製僅使用「預覽」代理。 因此，必須使用 `getStatusForAgent()` 方法，它允許查詢特定代理的狀態。 此方法也適用於「發佈」代理。 如果使用提供的代理執行了任何複製操作，則返回非空值。

### 使內容無效的方法 {#invalidating-content}

您可以直接使內容失效，方法是使用作者的Sling Content Invalidation(SCD)（首選方法），或使用複製API調用發佈Dispatcher刷新複製代理。 請參閱 [快取](/help/implementing/dispatcher/caching.md) 的子菜單。

**複製API容量限制**

一次複製少於100條路徑，其中500條為限制。 超過限度， `ReplicationException` 。
如果您的應用程式邏輯不需要原子複製，則可以通過設定 `ReplicationOptions.setUseAtomicCalls` to false，它接受任意數目的路徑，但在內部建立儲存段以保持在此限制以下。

每個複製調用所傳輸的內容的大小不得超過 `10 MB`。 此規則包括節點和屬性，但不包括任何二進位檔案（工作流包和內容包被視為二進位檔案）。


## 疑難排解 {#troubleshooting}

要排除複製故障，請導航至AEM Author Service Web UI中的「複製隊列」：

1. 從「開始」AEM菜單，導航到 **工具>部署>分發**
2. 選擇卡 **發佈**
   ![狀態](assets/publish-status.png "狀態")
3. 檢查應為綠色的隊列狀態
4. 您可以test到複製服務的連接
5. 選擇 **日誌** 頁籤，其中顯示內容發佈的歷史記錄

![日誌](assets/publish-logs.png "日誌")

如果無法發佈內容，則從AEM發佈服務還原整個發佈。
在這種情況下，主可編輯隊列顯示紅色狀態，應檢查該隊列，以確定哪些項目導致取消發佈。 通過按一下該隊列，將顯示其掛起項，如果需要，可以從該隊列清除單個項或所有項。
