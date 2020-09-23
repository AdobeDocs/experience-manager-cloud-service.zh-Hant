---
title: 管理工作流實例
description: 瞭解如何管理工作流程例項
translation-type: tm+mt
source-git-commit: 85e4104c3c2dbe4b67005bab52edb7ab90767406
workflow-type: tm+mt
source-wordcount: '934'
ht-degree: 0%

---


# 管理工作流實例 {#administering-workflow-instances}

工作流控制台提供多種工具來管理工作流實例，以確保它們正如預期執行。

管理工作流程時可使用多種控制台。 使用全 [域導覽](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation) ，開啟「工具」窗格，然後選取「工 **作流程******」:

* **型號**:管理工作流程定義
* **例項**:檢視並管理執行中的工作流程例項
* **啟動器**:管理啟動工作流程的方式
* **封存**:檢視成功完成之工作流程的歷史記錄
* **失敗**:檢視已完成但有錯誤的工作流程記錄
* **自動指派**:設定範本的自動指派工作流程

## 監控工作流實例的狀態 {#monitoring-the-status-of-workflow-instances}

1. 使用導覽依序 **選擇工**&#x200B;具、工 **作流程**。
1. 選擇「 **例項** 」(Instances)以顯示當前正在進行的工作流實例清單。

   ![wf-97](/help/sites-cloud/administering/assets/wf-97.png)


## 搜尋工作流程例項 {#search-workflow-instances}

1. 使用導覽依序 **選擇工**&#x200B;具、工 **作流程**。
1. 選擇「 **例項** 」(Instances)以顯示當前正在進行的工作流實例清單。 在上邊欄的左角，選取「篩選 **器」**。 或者，您也可以使用按鍵按鍵alt+1。 將顯示以下對話框：

   ![wf-99-1](/help/sites-cloud/administering/assets/wf-99-1.png)

1. 在「篩選」對話方塊中，選取工作流程搜尋准則。 您可以根據以下輸入進行搜尋：

* 裝載路徑：選擇特定路徑
* 工作流程模型：選擇工作流模型
* 受託人：選擇工作流程受託人
* 類型：任務、工作流項或工作流失敗
* 任務狀態：活動、完成或終止
* 我身在何處：擁有者AND受託人，僅限擁有者，僅限受託人
* 開始日期：開始日期在指定日期之前或之後
* 結束日期：指定日期之前或之後的結束日期
* 到期日：指定日期之前或之後的到期日
* 更新日期：在指定日期之前或之後更新日期

## 暫停、繼續和終止工作流實例 {#suspending-resuming-and-terminating-a-workflow-instance}

1. 使用導覽依序 **選擇工**&#x200B;具、工 **作流程**。
1. 選擇「 **例項** 」(Instances)以顯示當前正在進行的工作流實例清單。

   ![wf-96-1](/help/sites-cloud/administering/assets/wf-96-1.png)

1. 選擇特定項目，然後視 **情況使用****Terminate**、 **Suspend**&#x200B;或Resume;確認及／或需要進一步詳細資訊：

   ![wf-97-1](/help/sites-cloud/administering/assets/wf-97-1.png)

## 檢視封存的工作流程 {#viewing-archived-workflows}

1. 使用導覽依序 **選擇工**&#x200B;具、工 **作流程**。
1. 選擇「 **封存** 」以顯示成功完成的工作流實例清單。

   ![wf-98](/help/sites-cloud/administering/assets/wf-98.png)

   >[!NOTE]
   >
   >中止狀態被視為由於用戶操作而成功終止；例如：
   >
   >* 終止動 **作的使用**
   >* 當受工作流約束的頁面被（強制）刪除時，工作流將被終止


1. 選擇特定項目，然後選 **擇開啟歷史記錄** ，以查看詳細資訊：

   ![wf-99](/help/sites-cloud/administering/assets/wf-99.png)

## 修正工作流程例項失敗 {#fixing-workflow-instance-failures}

當工作流程失敗時，AEM會提供「 **Failures** 」（失敗）主控台，讓您在處理原始原因後調查並採取適當動作：

* **Failure Details(失敗詳**&#x200B;細資料)開啟視窗以顯示 
**故障消息**、 **步驟** 和 **故障棧**。

* **開啟歷史**&#x200B;記錄顯示工作流程歷史記錄的詳細資訊。

* **重試步驟** ：再次執行指令碼步驟元件實例。 修正原始錯誤的原因後，請使用「重試步驟」命令。 例如，在修正「處理步驟」執行之指令碼中的錯誤後，請重試該步驟。
* **終止** ：如果錯誤導致工作流出現不可協調的情況，則終止工作流。 例如，工作流可以依賴於環境條件，如儲存庫中對工作流實例不再有效的資訊。
* **「終止和重試** 」類似於「 **** 終止」，但是使用原始裝載、標題和說明開始新的工作流實例。

若要調查失敗，然後在之後繼續或終止工作流程，請執行下列步驟：

1. 使用導覽依序 **選擇工**&#x200B;具、工 **作流程**。
1. 選擇 **失敗** ，以顯示未成功完成的工作流實例清單。
1. 選擇特定項目，然後選擇相應的操作：

   ![wf-47](/help/sites-cloud/administering/assets/wf-47.png)

## 定期清除工作流實例 {#regular-purging-of-workflow-instances}

最小化工作流實例數可提高工作流引擎的效能，因此您可以定期從儲存庫中清除已完成或正在運行的工作流實例。

設定 **Adobe Granite Workflow Purge Configuration** ，以根據工作流程例項的年齡和狀態來清除。 您也可以清除所有模型或特定模型的工作流實例。

您也可以建立服務的多個配置，以清除滿足不同標準的工作流實例。 例如，建立設定，當特定工作流程模型的執行時間比預期長時，會清除這些例項。 建立另一個配置，該配置在特定天數後清除所有已完成的工作流，以最小化儲存庫的大小。

要配置服務，可以配置OSGI配置檔案請參閱 [OSGi配置檔案](/help/implementing/deploying/configuring-osgi.md)。 下表說明了這兩種方法所需的屬性。

>[!NOTE]
>
>要將配置添加到儲存庫，服務PID為：
>
>`com.adobe.granite.workflow.purge.Scheduler`
>
>由於服務是工廠服務，因此節點的名 `sling:OsgiConfig` 稱需要標識符尾碼，例如：
>
>`com.adobe.granite.workflow.purge.Scheduler-myidentifier`

<table>
 <tbody>
  <tr>
   <th>屬性名稱（Web控制台）</th>
   <th>OSGi屬性名稱</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>工作名稱</td>
   <td>scheduledpurge.name</td>
   <td>計劃清除的描述性名稱。</td>
  </tr>
  <tr>
   <td>工作流程狀態</td>
   <td>scheduledpurge.workflowStatus</td>
   <td><p>要清除的工作流實例的狀態。 下列值有效：</p>
    <ul>
     <li>完成：已完成的工作流實例將被清除。</li>
     <li>正在運行：執行中的工作流程例項會被清除。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>要清除的模型</td>
   <td>scheduledpurge.modelIds</td>
   <td><p>要清除的工作流模型的ID。 ID是指向模型節點的路徑，例如：<br /> /conf/global/settings/workflow/models/dam/update_asset/jcr:content/model<br /> 指定無值可清除所有工作流程模型的例項。</p> <p>要指定多個型號，請按一下Web控制台中的+按鈕。 </p> </td>
  </tr>
  <tr>
   <td>工作流程時代</td>
   <td>scheduledpurge.daysold</td>
   <td>要清除的工作流實例的年齡（以天為單位）。</td>
  </tr>
 </tbody>
</table>

## 設定收件箱的最大大小 {#setting-the-maximum-size-of-the-inbox}

您可以設定 **Adobe Granite Workflow Service**，以設定收件匣的最大大小，請參 [閱將OSGi組態新增至儲存庫](/help/implementing/deploying/configuring-osgi.md)。 下表說明您所配置的屬性。

>[!NOTE]
>
>要將配置添加到儲存庫，服務PID為：
>
>`com.adobe.granite.workflow.core.WorkflowSessionFactory`。

| 屬性名稱（Web控制台） | OSGi屬性名稱 |
|---|---|
| 最大收件箱查詢大小 | granite.workflow.inboxQuerySize |

