---
title: 複寫
description: 散佈 和複製故障排除。
exl-id: c84b4d29-d656-480a-a03a-fbeea16db4cd
translation-type: tm+mt
source-git-commit: eb92c66f2b9e8e6ec859114da2de049747ec251e
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 1%

---

# 複寫 {#replication}

Adobe Experience Manager作為Cloud Service使用[Sling Content Distribution](https://sling.apache.org/documentation/bundles/content-distribution.html)功能，將要複製的內容移至執行階段以外Adobe I/O上執行的管道服AEM務。

>[!NOTE]
>
>如需詳細資訊，請閱讀[Distribution](/help/core-concepts/architecture.md#content-distribution)。

## 發佈內容{#methods-of-publishing-content}的方法

### 快速取消／發佈——計畫取消／發佈{#publish-unpublish}

作者的AEM這些標準功能不會隨Cloud Service而AEM改變。

### 開啟和關閉時間——觸發器配置{#on-and-off-times-trigger-configuration}

從「頁面屬性」的「基本」標籤中可以找到&#x200B;**On Time**&#x200B;和&#x200B;**Off Time**&#x200B;的其他可能性。[](/help/sites-cloud/authoring/fundamentals/page-properties.md#basic)

要實現自動複製，您需要在[OSGi配置](/help/implementing/deploying/configuring-osgi.md)**開關觸發器配置**&#x200B;中啟用&#x200B;**自動複製**:

![OSGi On Off觸發器配置](/help/operations/assets/replication-on-off-trigger.png)

### 樹激活{#tree-activation}

要執行樹狀結構激活：

1. 從「開AEM始」功能表導覽至「**工具>部署>散發」**
2. 選擇卡片&#x200B;**forwardPublisher**
3. 進入forwardPublisher Web控制台UI後，**選擇Distribute**

   ![散](assets/distribute.png "發")
4. 在路徑瀏覽器中選擇路徑，選擇根據需要添加節點、樹或刪除，然後選擇&#x200B;**提交**

### 發佈內容樹工作流程{#publish-content-tree-workflow}

通過選擇&#x200B;**工具——工作流——模型**&#x200B;並複製&#x200B;**發佈內容樹**&#x200B;現成可用的工作流模型，可以觸發樹複製，如下所示：

![](/help/operations/assets/publishcontenttreeworkflow.png)

請勿修改或叫用原始模型。 請務必先複製模型，然後修改或叫用該副本。

和所有工作流程一樣，您也可以透過API叫用它。 如需詳細資訊，請參閱[程式化與工作流程互動](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-program-interaction.html?lang=en#extending-aem)。

或者，也可以通過建立使用`Publish Content Tree`進程步驟的「工作流模型」來實現此目的：

1. 從作AEM為Cloud Service首頁，轉至&#x200B;**工具——工作流——模型**
1. 在「工作流模型」頁面中，按螢幕右上角的&#x200B;**Create**&#x200B;鍵
1. 新增標題和名稱至模型。 如需詳細資訊，請參閱[建立工作流程模型](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html)
1. 從清單中選擇新建立的模型，然後按&#x200B;**Edit**&#x200B;鍵
1. 在以下窗口中，將「流程步驟」(Process Step)拖放到當前模型流中：

   ![程序步驟](/help/operations/assets/processstep.png)

1. 按一下流程中的「處理」步驟，然後按扳手圖示，選擇「**設定**」
1. 按一下&#x200B;**Process**&#x200B;頁籤，然後從下拉清單中選擇`Publish Content Tree`

   ![樹狀啟動](/help/operations/assets/newstep.png)

1. 在&#x200B;**參數**&#x200B;欄位中設定任何其它參數。 多個逗號分隔引數可以一併串連。 例如：

   `enableVersion=true,agentId=publish`


   >[!NOTE]
   >
   >有關參數清單，請參見下面的&#x200B;**Parameters**&#x200B;部分。

1. 按&#x200B;**Done**&#x200B;保存工作流模型。

**參數**

* `replicateAsParticipant` （布林值，預設值） `false`)。如果配置為`true`，則複製使用執行參與者步驟的承擔者的`userid`。
* `enableVersion` （布林值，預設值） `true`)。此參數確定複製時是否建立了新版本。
* `agentId` （字串值，預設值表示使用所有已啟用的代理）。
* `filters` （字串值，預設值表示所有路徑都已啟用）。可用值包括：
   * `onlyActivated` -只有未標示為已啟用的路徑才會啟用。
   * `onlyModified` -僅啟用已啟動且修改日期晚於啟動日期的路徑。
   * 上述可以用垂直號&quot;|&quot;進行ORed。 例如，`onlyActivated|onlyModified`。

**記錄**

當樹狀結構啟動工作流程步驟啟動時，它會在INFO記錄層級上記錄其設定參數。 在激活路徑時，也會記錄INFO語句。

然後，工作流步驟複製所有路徑後，將記錄最終的INFO語句。

此外，您可以將`com.day.cq.wcm.workflow.process.impl`以下記錄程式的記錄級別提高為DEBUG/TRACE，以獲取更多日誌資訊。

如果出現錯誤，工作流步驟將以`WorkflowException`終止，該將包住基礎的例外。

以下是範例發佈內容樹狀結構工作流程中產生的記錄檔範例：

```
21.04.2021 19:14:55.566 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.treeactivation.TreeActivationWorkflowProcess TreeActivation options: replicateAsParticipant=false(userid=workflow-process-service), agentId=publish, chunkSize=100, filter=, enableVersion=false
```

```
21.04.2021 19:14:58.541 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.ChunkedReplicator closing chunkedReplication-VolatileWorkItem_node1_var_workflow_instances_server60_2021-04-20_brian-tree-replication-test-2_1, 17 paths replicated in 2971 ms
```

**繼續支援**

工作流程會以區塊處理內容，每個區塊代表要發佈的完整內容的子集。 如果由於任何原因工作流被系統停止，它將重新啟動並處理尚未處理的塊。 日誌語句將聲明內容已從特定路徑恢復。

## 疑難排解 {#troubleshooting}

若要疑難排解複製問題，請導覽至AEM Author Service Web UI中的「複製佇列」:

1. 從「開AEM始」功能表導覽至「**工具>部署>散發」**
2. 選擇卡片&#x200B;**forwardPublisher**
   ![狀](assets/status.png "態")
3. 檢查應為綠色的隊列狀態
4. 您可以測試到複製服務的連接
5. 選擇&#x200B;**日誌**&#x200B;頁籤，該頁籤顯示內容發佈的歷史記錄

![日](assets/logs.png "志")

如果內容無法發佈，則整個出版物會從AEM Publish Service回復。
在這種情況下，應審查隊列，以確定哪些項目導致出版物取消。 按一下顯示紅色狀態的佇列，即會顯示包含待審項目的佇列，視需要可清除單一或所有項目。
