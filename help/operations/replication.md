---
title: 複寫
description: 散佈 和疑難排解復寫。
exl-id: c84b4d29-d656-480a-a03a-fbeea16db4cd
source-git-commit: 1ba960a930e180f4114f78607a3eb4bd5ec3edaf
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 1%

---

# 複寫 {#replication}

Adobe Experience Manager as a Cloud Service使用[Sling Content Distribution](https://sling.apache.org/documentation/bundles/content-distribution.html)功能，將內容移動至在AEM執行階段以外Adobe I/O上執行的管道服務。

>[!NOTE]
>
>如需詳細資訊，請參閱[分送](/help/core-concepts/architecture.md#content-distribution) 。

## 發佈內容的方法{#methods-of-publishing-content}

### 快速取消發佈 — 計畫取消發佈{#publish-unpublish}

作者適用的這些標準AEM功能不會隨著AEMCloud Service而變更。

### 開啟和關閉時間 — 觸發配置{#on-and-off-times-trigger-configuration}

從「頁面屬性」的「[基本」頁簽中可以找到&#x200B;**「開啟時間」**&#x200B;和&#x200B;**「關閉時間」**&#x200B;的其他可能性。](/help/sites-cloud/authoring/fundamentals/page-properties.md#basic)

要實現自動複製，您需要在[OSGi配置](/help/implementing/deploying/configuring-osgi.md) **開啟關閉觸發配置**&#x200B;中啟用&#x200B;**自動複製**:

![OSGi On Off觸發器配置](/help/operations/assets/replication-on-off-trigger.png)

### 樹激活{#tree-activation}

要執行樹激活：

1. 從AEM「開始」功能表導覽至「**工具>部署>發佈**」
2. 選擇卡片&#x200B;**forwardPublisher**
3. 在forwardPublisher Web控制台UI中，選擇&#x200B;**Distribute**

   ![](assets/distribute.png "DistributeDistribute")
4. 在路徑瀏覽器中選擇路徑，根據需要選擇添加節點、樹或刪除，然後選擇&#x200B;**Submit**

### 發佈內容樹工作流{#publish-content-tree-workflow}

您可以選擇&#x200B;**工具 — 工作流 — 模型**&#x200B;並複製&#x200B;**發佈內容樹**&#x200B;現成可用的工作流模型，如下所示：

![](/help/operations/assets/publishcontenttreeworkflow.png)

請勿修改或調用原始模型。 請務必先複製模型，然後修改或叫用該復本。

如同所有工作流程，您也可以透過API叫用。 如需詳細資訊，請參閱以程式設計方式](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-program-interaction.html?lang=en#extending-aem)與工作流程互動。[

或者，您也可以建立使用`Publish Content Tree`流程步驟的「工作流模型」來實現此目標：

1. 從AEM as a Cloud Service首頁，前往&#x200B;**工具 — 工作流程 — 模型**
1. 在「工作流模型」頁面中，按螢幕右上角的&#x200B;**Create**
1. 新增標題和名稱至模型。 如需詳細資訊，請參閱[建立工作流模型](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html)
1. 從清單中選擇新建立的模型，然後按&#x200B;**Edit**
1. 在以下窗口中，將「處理步驟」(Process Step)拖放到當前模型流中：

   ![程序步驟](/help/operations/assets/processstep.png)

1. 按一下流量中的「處理」步驟，然後按扳手圖示選取&#x200B;**設定**
1. 按一下&#x200B;**Process**&#x200B;頁簽，然後從下拉清單中選擇`Publish Content Tree`

   ![樹狀激活](/help/operations/assets/newstep.png)

1. 在&#x200B;**參數**&#x200B;欄位中設定任何其他參數。 多個逗號分隔引數可以字串在一起。 例如：

   `enableVersion=true,agentId=publish`


   >[!NOTE]
   >
   >如需參數清單，請參閱下方的&#x200B;**參數**&#x200B;一節。

1. 按下&#x200B;**Done**&#x200B;以儲存工作流程模型。

**參數**

* `replicateAsParticipant` （布林值，預設值） `false`)。如果配置為`true`，則複製使用執行參與者步驟的主體的`userid`。
* `enableVersion` （布林值，預設值） `true`)。此參數會決定是否在復寫時建立新版本。
* `agentId` （字串值，預設值表示已使用所有啟用的代理）。建議您明確說明agentId;例如，設定它：發佈
* `filters` （字串值，預設值表示所有路徑皆已啟用）。可用值包括：
   * `onlyActivated`  — 只有未標示為已啟用的路徑才會啟用。
   * `onlyModified`  — 僅啟用已啟用且修改日期晚於啟用日期的路徑。
   * 上方可以用垂直號「|」來ORed。 例如， `onlyActivated|onlyModified`。

**記錄**

樹激活工作流步驟開始時，它將在INFO日誌級別上記錄其配置參數。 啟動路徑時，也會記錄INFO陳述式。

然後，在複製所有路徑後，將記錄最終的INFO語句。

此外，您可以將`com.day.cq.wcm.workflow.process.impl`以下記錄器的記錄層級增加為「除錯/TRACE」，以取得更多記錄資訊。

如果發生錯誤，工作流程步驟會以`WorkflowException`終止，其中會包含基礎的例外。

以下是範例發佈內容樹狀結構工作流程期間產生的記錄檔範例：

```
21.04.2021 19:14:55.566 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.treeactivation.TreeActivationWorkflowProcess TreeActivation options: replicateAsParticipant=false(userid=workflow-process-service), agentId=publish, chunkSize=100, filter=, enableVersion=false
```

```
21.04.2021 19:14:58.541 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.ChunkedReplicator closing chunkedReplication-VolatileWorkItem_node1_var_workflow_instances_server60_2021-04-20_brian-tree-replication-test-2_1, 17 paths replicated in 2971 ms
```

**繼續支援**

工作流程會以區塊處理內容，每個區塊代表要發佈之完整內容的子集。 如果由於任何原因，工作流被系統停止，它將重新啟動並處理尚未處理的區塊。 記錄陳述式會指出內容已從特定路徑繼續。

## 疑難排解 {#troubleshooting}

若要疑難排解復寫，請導覽至AEM製作服務Web UI中的復寫佇列：

1. 從AEM「開始」功能表導覽至「**工具>部署>發佈**」
2. 選擇卡片&#x200B;**forwardPublisher**
   ![](assets/status.png "StatusStatus")
3. 檢查應為綠色的隊列狀態
4. 您可以測試與復寫服務的連線
5. 選擇&#x200B;**Logs**&#x200B;頁簽，該頁簽顯示內容發佈的歷史記錄

![](assets/logs.png "LogsLogs")

如果無法發佈內容，則會從AEM發佈服務還原整個發佈。
在這種情況下，應審查隊列，以確定哪些項目導致取消發佈。 按一下顯示紅色狀態的佇列，就會顯示含有待處理項目的佇列，如有需要，可從中清除單一或所有項目。
