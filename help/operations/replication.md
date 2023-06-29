---
title: 複製
description: 散佈和疑難排解復寫。
exl-id: c84b4d29-d656-480a-a03a-fbeea16db4cd
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1339'
ht-degree: 1%

---

# 複製 {#replication}

Adobe Experience Manager as a Cloud Service使用 [Sling內容發佈](https://sling.apache.org/documentation/bundles/content-distribution.html) 將內容移動到復寫至AEM執行階段以外的Adobe Developer上執行的管道服務的功能。

>[!NOTE]
>
>讀取 [分佈](/help/overview/architecture.md#content-distribution) 以取得詳細資訊。

## 發佈內容的方法 {#methods-of-publishing-content}

>[!NOTE]
>
>如果您有興趣大量發佈內容，請使用 [發佈內容樹狀工作流程](#publish-content-tree-workflow).
>此工作流程步驟是專為Cloud Service而建置，可有效處理大型裝載。
>不建議建置您自己的大量發佈自訂程式碼。
>如果您因任何原因必須自訂，則可以使用現有的工作流程API來觸發此工作流程/工作流程步驟。
>只發佈必須發佈的內容永遠都是不錯的做法。 如果不需要的話，也請謹慎行事，不要嘗試發佈大量內容。 不過，您可以透過發佈內容樹狀工作流程傳送多少內容並無限制。

### 快速取消/發佈 — 計畫取消/發佈 {#publish-unpublish}

此功能可讓您立即發佈所選頁面，而不需透過「管理發布」方法額外選擇選項。

如需詳細資訊，請參閱 [管理發布](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#manage-publication).

### 開啟和關閉時間 — 觸發器設定 {#on-and-off-times-trigger-configuration}

的其他可能性 **準時** 和 **關閉時間** 可從以下網址取得： [頁面屬性的基本索引標籤](/help/sites-cloud/authoring/fundamentals/page-properties.md#basic).

若要為此功能實現自動複製，請啟用 **自動復寫** 在 [OSGi設定](/help/implementing/deploying/configuring-osgi.md) **開啟關閉觸發器設定**：

![OSGi開啟關閉觸發器設定](/help/operations/assets/replication-on-off-trigger.png)

### 管理發佈 {#manage-publication}

「管理發布」比「快速發佈」提供更多的選項，允許包含子頁面、自訂參照和啟動任何適用的工作流程，並提供稍後發佈的選項。

為「稍後發佈」選項包含資料夾的子項時，會叫用發佈內容樹狀工作流程，如本文所述。

您可以在以下網址找到有關管理發布的詳細資訊： [出版基礎檔案](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#manage-publication).

### 發佈內容樹狀工作流程 {#publish-content-tree-workflow}

您可以透過選擇來觸發樹狀結構復寫 **工具 — 工作流程 — 模型** 並複製 **發佈內容樹狀結構** 現成的工作流程模型，如下所示：

![發佈內容樹狀工作流程卡片](/help/operations/assets/publishcontenttreeworkflow.png)

請勿修改或叫用原始模型。 相反，請確保先複製模型，然後修改或呼叫該副本。

如同所有工作流程，您也可以透過API叫用。 如需詳細資訊，請參閱 [以程式設計方式與工作流程互動](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-program-interaction.html?lang=en#extending-aem).

或者，您也可以建立工作流程模型，此模型使用 `Publish Content Tree` 程式步驟：

1. 從AEMas a Cloud Service首頁，前往 **工具 — 工作流程 — 模型**.
1. 在「工作流程模型」頁面中，按 **建立** 在熒幕的右上角。
1. 新增標題和名稱至您的模型。 如需詳細資訊，請參閱 [建立工作流程模型](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html).
1. 從清單中選取新建立的模型，然後按 **編輯**
1. 在下列視窗中，將「處理步驟」拖放至目前的模型流程：

   ![程序步驟](/help/operations/assets/processstep.png)

1. 選取流程中的「處理」步驟，然後選取 **設定** 按一下扳手圖示。
1. 選取 **程式** 標籤並選取 `Publish Content Tree` 從下拉式清單中，然後檢查 **處理常式前進** 核取方塊

   ![樹啟動](/help/operations/assets/newstep.png)

1. 在中設定任何其他引數 **引數** 欄位。 多個以逗號分隔的引數可串連在一起。 例如：

   `enableVersion=true,agentId=publish,includeChildren=true`


   >[!NOTE]
   >
   >如需引數清單，請參閱 **引數** 區段底下。

1. 按下 **完成** 以儲存「工作流程」模型。

**參數**

* `includeChildren` (布林值，預設： `false`)。 值 `false` 表示只會發佈路徑； `true` 表示也會發佈子項。
* `replicateAsParticipant` (布林值，預設： `false`)。 若設定為 `true`，復寫正在使用 `userid` 執行參與者步驟的主參與者。
* `enableVersion` (布林值，預設： `true`)。 此引數會決定複製時是否建立新版本。
* `agentId` （字串值，預設值表示僅使用發佈代理）。 建議清楚說明agentId；例如，將其設定為值： publish。 將代理程式設定為 `preview` 發佈至預覽服務。
* `filters` （字串值，預設值代表所有路徑都已啟動）。 可用的值包括：
   * `onlyActivated`  — 僅啟動（已）已啟動的頁面。 作為重新啟用的一種形式。
   * `onlyModified`  — 僅啟動已啟動且修改日期晚於啟動日期的路徑。
   * 以上可以用垂直號「|」進行「或」操作。 例如， `onlyActivated|onlyModified`.

**記錄**

樹狀結構啟動工作流程步驟啟動時，會在INFO記錄層級上記錄其設定引數。 啟動路徑時，也會記錄INFO陳述式。

在工作流程步驟已複製所有路徑之後，會記錄最終的INFO陳述式。

此外，您也可以增加以下記錄器的記錄層級 `com.day.cq.wcm.workflow.process.impl` 偵錯/TRACE以取得更多記錄資訊。

如果有錯誤，工作流程步驟會以 `WorkflowException`，會包裝基礎的例外狀況。

以下是在範例發佈內容樹狀工作流程期間產生的記錄範例：

```
21.04.2021 19:14:55.566 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.treeactivation.TreeActivationWorkflowProcess TreeActivation options: replicateAsParticipant=false(userid=workflow-process-service), agentId=publish, chunkSize=100, filter=, enableVersion=false
```

```
21.04.2021 19:14:58.541 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.ChunkedReplicator closing chunkedReplication-VolatileWorkItem_node1_var_workflow_instances_server60_2021-04-20_brian-tree-replication-test-2_1, 17 paths replicated in 2971 ms
```

**繼續支援**

工作流程會以區塊處理內容，每個區塊都代表要發佈的完整內容子集。 如果系統停止工作流程，它會重新啟動並處理尚未處理的區塊。 記錄陳述式指出內容已從特定路徑恢復。

### 復寫API {#replication-api}

您可以使用AEMas a Cloud Service提供的復寫API發佈內容。

如需詳細資訊，請參閱 [API檔案](https://javadoc.io/doc/com.adobe.aem/aem-sdk-api/latest/com/day/cq/replication/package-summary.html).

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

如上例所示，複製資源時，只會使用預設為作用中的代理程式。 在AEMas a Cloud Service中，這僅代表稱為「發佈」的代理程式，此代理程式會將作者連線到發佈層級。

為了支援預覽功能，已新增名為「預覽」的新代理程式，預設為不啟用。 此代理程式用於將作者連線到預覽層。 如果您只想透過預覽代理程式進行復寫，您必須透過 `AgentFilter`.

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

如果您未提供此類篩選器，且僅使用「發佈」代理程式，則不會使用「預覽」代理程式，且復寫動作不會影響預覽階層。

整體 `ReplicationStatus` 只有當復寫動作包含至少一個預設為作用中的代理程式時，才會修改資源的復寫動作。 在上述範例中，此流程並不適用。 復寫只是使用「預覽」代理程式。 因此，您必須使用 `getStatusForAgent()` 方法，允許查詢特定代理程式的狀態。 此方法也適用於「發佈」代理。 如果已使用提供的代理程式完成任何復寫動作，則會傳回非Null值。

### 讓內容失效的方法 {#invalidating-content}

您可以使用作者的Sling內容失效(SCD) （偏好方法）或使用復寫API叫用發佈Dispatcher Flush復寫代理程式，直接讓內容失效。 另請參閱 [快取](/help/implementing/dispatcher/caching.md) 頁面，以取得更多詳細資料。

**復寫API容量限制**

一次復寫少於100個路徑，以500為上限。 超過限制，a `ReplicationException` 擲回。
如果您的應用程式邏輯不需要原子複製，可透過設定 `ReplicationOptions.setUseAtomicCalls` 為false，可接受任何數量的路徑，但在內部建立貯體以保持在此限制以下。

每個復寫呼叫所傳輸的內容大小不得超過 `10 MB`. 此規則包含節點和屬性，但不包含任何二進位檔（工作流程套件和內容套件被視為二進位檔）。


## 疑難排解 {#troubleshooting}

若要疑難排解復寫，請導覽至AEM作者服務Web UI中的復寫佇列：

1. 從AEM「開始」功能表，瀏覽至 **「工具」>「部署」>「發佈」**
2. 選取卡片 **發佈**
   ![狀態](assets/publish-status.png "狀態")
3. 檢查應為綠色的佇列狀態
4. 您可以測試復寫服務的連線
5. 選取 **記錄檔** 索引標籤，顯示內容發佈的歷史記錄

![記錄檔](assets/publish-logs.png "記錄檔")

如果內容無法發佈，則整個發佈將從AEM Publish Service還原。
在這種情況下，可編輯的主要佇列會顯示紅色狀態，並應加以檢閱以識別哪些專案導致取消發佈。 按一下該佇列會顯示其暫止專案，視需要可從中清除單一專案或所有專案。
