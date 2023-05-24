---
title: 管理工作流程例項
description: 瞭解如何管理工作流程例項
feature: Administering
role: Admin
exl-id: d2adb5e8-3f0e-4a3b-b7d0-dbbc5450e45f
source-git-commit: 0a87842923298be1a801a85519ac85fae5ef7933
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 0%

---

# 管理工作流程例項 {#administering-workflow-instances}

工作流程主控台提供了幾個用於管理工作流程執行個體的工具，以確保它們按預期執行。

有一系列主控台可用來管理您的工作流程。 使用 [全域導覽](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation) 以開啟 **工具** 窗格，然後選取 **工作流程**：

* **模型**：管理工作流程定義
* **執行個體**：檢視和管理執行中的工作流程例項
* **啟動器**：管理工作流程的啟動方式
* **封存**：檢視成功完成的工作流程歷史記錄
* **失敗**：檢視已完成但發生錯誤的工作流程歷史記錄
* **自動指派**：設定範本的自動指派工作流程

## 監控工作流程例項狀態 {#monitoring-the-status-of-workflow-instances}

1. 使用導覽選取 **工具**，則 **工作流程**.
1. 選取 **執行個體** 以顯示目前進行中的工作流程例項清單。

   ![wf-97](/help/sites-cloud/administering/assets/wf-97.png)


## 搜尋工作流程例項 {#search-workflow-instances}

1. 使用導覽選取 **工具**，則 **工作流程**.
1. 選取 **執行個體** 以顯示目前進行中的工作流程例項清單。 在頂端欄的左角，選取 **篩選器**. 或者，您也可以使用alt+1鍵。 下列對話方塊隨即顯示：

   ![wf-99-1](/help/sites-cloud/administering/assets/wf-99-1.png)

1. 在「篩選」對話方塊中，選取工作流程搜尋條件。 您可以根據下列輸入進行搜尋：

   * 裝載路徑：選取特定路徑
   * 工作流程模型：選取工作流程模型
   * 受指派人：選取工作流程受指派人
   * 型別：任務、工作流程專案或工作流程失敗
   * 工作狀態：作用中、完成或已終止
   * 我的位置：擁有者和受指派人、僅限擁有者、僅限受指派人
   * 開始日期：指定日期之前或之後的開始日期
   * 結束日期：指定日期之前或之後的結束日期
   * 到期日：指定日期之前或之後的到期日
   * 更新日期：指定日期之前或之後的更新日期

## 暫停、恢復和終止工作流程例項 {#suspending-resuming-and-terminating-a-workflow-instance}

1. 使用導覽選取 **工具**，則 **工作流程**.
1. 選取 **執行個體** 以顯示目前進行中的工作流程例項清單。

   ![wf-96-1](/help/sites-cloud/administering/assets/wf-96-1.png)

1. 選取特定專案，然後使用 **終止**， **暫停**，或 **繼續**，視情況而定；需要確認和/或進一步細節：

   ![wf-97-1](/help/sites-cloud/administering/assets/wf-97-1.png)

   >[!NOTE]
   >
   >
   >為了終止或中止工作流程，工作流程必須處於等待使用者介入的狀態，例如在「參與者步驟」中。 嘗試中止目前正在執行工作的工作流程（執行中的作用中執行緒）可能不會產生預期的結果。


## 檢視已封存的工作流程 {#viewing-archived-workflows}

1. 使用導覽選取 **工具**，則 **工作流程**.

1. 選取 **封存** 顯示成功完成的工作流程例項清單。

   ![wf-98](/help/sites-cloud/administering/assets/wf-98.png)

   >[!NOTE]
   >中止狀態會被視為成功終止，因為它是使用者動作的結果；例如：
   >
   >* 使用 **終止** 動作
   >* 當受工作流程約束的頁面被（強制）刪除時，工作流程將終止



1. 選取特定專案，然後 **開啟歷史記錄** 若要檢視更多詳細資料：

   ![wf-99](/help/sites-cloud/administering/assets/wf-99.png)

## 修正工作流程執行個體失敗 {#fixing-workflow-instance-failures}

當工作流程失敗時，AEM會提供 **失敗** 主控台，可讓您在原始原因處理完畢後，立即進行調查並採取適當的動作：

* **失敗詳細資料**
開啟視窗以顯示 
**失敗訊息**， **步驟** 和 **失敗棧疊**.

* **開啟歷史記錄**
顯示工作流程記錄的詳細資訊。

* **重試步驟** 再次執行指令碼步驟元件例項。 修正原始錯誤的原因後，請使用「重試步驟」指令。 例如，在您修正「程式步驟」所執行指令碼中的錯誤後，請重試該步驟。
* **終止** 如果錯誤導致工作流程出現不可調和的情況，則終止工作流程。 例如，工作流程可以依賴環境條件，例如存放庫中對工作流程例項不再有效的資訊。
* **終止並重試** 類似於 **終止** 但新工作流程例項是使用原始裝載、標題和說明啟動。

若要調查失敗，然後繼續或終止工作流程，請使用下列步驟：

1. 使用導覽選取 **工具**，則 **工作流程**.

1. 選取 **失敗** 以顯示未成功完成的工作流程例項清單。
1. 選取特定專案，然後選取適當的動作：

   ![wf-47](/help/sites-cloud/administering/assets/wf-47.png)

## 定期清除工作流程例項 {#regular-purging-of-workflow-instances}

將工作流程例項的數目降至最低會提升工作流程引擎的效能，因此您可以定期從儲存庫中清除已完成或執行中的工作流程例項。

設定 **AdobeGranite工作流程清除設定** 若要根據工作流程執行個體的年齡和狀態來永久刪除工作流程執行個體，請執行下列步驟： 您也可以清除所有模型或特定模型的工作流程例項。

您也可以建立服務的多個組態，以清除滿足不同條件的工作流程執行個體。 例如，建立一個設定，當特定工作流程模型的執行個體執行時間比預期時間長很多時，清除這些執行個體。 建立另一個設定，在特定天數後清除所有已完成的工作流程，以將存放庫的大小降至最低。

若要設定服務，您可以設定OSGi組態檔，請參閱 [OSGi設定檔案](/help/implementing/deploying/configuring-osgi.md). 下表說明這兩種方法所需的特性。

>[!NOTE]
>若要將設定新增至存放庫，服務PID為：
>`com.adobe.granite.workflow.purge.Scheduler`
>因為服務是工廠服務，所以服務名稱 `sling:OsgiConfig` 節點需要識別碼尾碼，例如：
>`com.adobe.granite.workflow.purge.Scheduler-myidentifier`

<table>
 <tbody>
  <tr>
   <th>屬性名稱（Web主控台）</th>
   <th>OSGi屬性名稱</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>工作名稱</td>
   <td>scheduledpurge.name</td>
   <td>排定永久刪除的描述性名稱。</td>
  </tr>
  <tr>
   <td>工作流程狀態</td>
   <td>scheduledpurge.workflowStatus</td>
   <td><p>要清除的工作流程執行個體的狀態。 下列值有效：</p>
    <ul>
     <li>已完成：已清除已完成的工作流程執行個體。</li>
     <li>執行中：清除執行中的工作流程執行個體。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>要永久刪除的模型</td>
   <td>scheduledpurge.modelIds</td>
   <td><p>要清除的工作流程模型的ID。 ID是模型節點的路徑，例如：<br /> /conf/global/settings/workflow/models/dam/update_asset/jcr：content/model<br /> 不指定任何值以清除所有工作流程模型的執行個體。</p> <p>若要指定多個模型，請按一下Web主控台中的+按鈕。 </p> </td>
  </tr>
  <tr>
   <td>工作流程年齡</td>
   <td>scheduledpurge.daysold</td>
   <td>要清除的工作流程例項期限（以天為單位）。</td>
  </tr>
 </tbody>
</table>

## 設定收件匣大小上限 {#setting-the-maximum-size-of-the-inbox}

您可以透過設定 **AdobeGranite工作流程服務**，請參閱 [將OSGi設定新增至存放庫](/help/implementing/deploying/configuring-osgi.md). 下表說明您設定的屬性。

>[!NOTE]
>若要將設定新增至存放庫，服務PID為：
>`com.adobe.granite.workflow.core.WorkflowSessionFactory`.

| 屬性名稱（Web主控台） | OSGi屬性名稱 |
|---|---|
| 收件匣查詢大小上限 | granite.workflow.inboxQuerySize |

## 對客戶擁有的資料存放區使用工作流程變數 {#using-workflow-variables-customer-datastore}

工作流程處理的資料會儲存在Adobe提供的儲存空間(JCR)中。 此資料本質上可能是敏感資料。 您可能想要將所有使用者定義的中繼資料/資料儲存在您自己的受管理存放區中，而非Adobe提供的存放區。 以下各節說明如何為外部儲存設定這些變數。

### 設定模型以使用中繼資料的外部儲存 {#set-model-for-external-storage}

在工作流程模型的層級，會提供一個旗標，指出模型（及其執行階段執行個體）具有中繼資料的外部儲存。 針對標籤為外部儲存的模型的工作流程例項，工作流程變數不會儲存在JCR中。

屬性 *userMetadataPersistenceEnabled* 將會儲存在 *jcr：content節點* 工作流程模型的URL。 此標幟將持續保留在工作流程中繼資料中為 *cq：userMetaDataCustomPersistenceEnabled*.

下圖顯示必須在工作流程上設定標幟。

![workflow-externalize-config](/help/sites-cloud/administering/assets/workflow-externalize-config.png)

### 外部儲存空間中中繼資料的API {#apis-for-metadata-external-storage}

若要在外部儲存變數，您必須實作工作流程公開的API。

UserMetaDataPersistenceContext

以下範例說明如何使用API。

```
@ProviderType
public interface UserMetaDataPersistenceContext {
 
    /**
     * Gets the workflow for persistence
     * @return workflow
     */
    Workflow getWorkflow();
 
    /**
     * Gets the workflow id for persistence
     * @return workflowId
     */
    String getWorkflowId();
 
    /**
     * Gets the user metadata persistence id
     * @return userDataId
     */
    String getUserDataId();
}
```

UserMetaDataPersistenceProvider

```
/**
 * This provider can be implemented to store the user defined workflow-data metadata in a custom storage location
 */
@ConsumerType
public interface UserMetaDataPersistenceProvider {
 
   /**
    * Retrieves the metadata using a unique identifier
    * @param userMetaDataPersistenceContext
    * @param metaDataMap of user defined workflow data metaData
    * @throws WorkflowException
    */
   void get(UserMetaDataPersistenceContext userMetaDataPersistenceContext, MetaDataMap metaDataMap) throws WorkflowException;
 
   /**
    * Stores the given metadata to the custom storage location
    * @param userMetaDataPersistenceContext
    * @param metaDataMap metadata map
    * @return the unique identifier that can be used to retrieve metadata. If null is returned, then workflowId is used.
    * @throws WorkflowException
    */
   String put(UserMetaDataPersistenceContext userMetaDataPersistenceContext, MetaDataMap metaDataMap) throws WorkflowException;
 
} 
```


