---
title: AEM as a Cloud Service 中的維護任務
description: 瞭解AEM as a Cloud Service中的維護任務以及如何進行設定。
exl-id: 5b114f94-be6e-4db4-bad3-d832e4e5a412
feature: Operations
role: Admin
source-git-commit: f6e8066ecdfdbd0c7e79c2557dc19eec81657047
workflow-type: tm+mt
source-wordcount: '2042'
ht-degree: 8%

---


# AEM as a Cloud Service 中的維護任務 {#maintenance-tasks-in-aem-as-a-cloud-service}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_maintenance"
>title="維護任務"
>abstract="維護任務是依據排程執行以將存放庫最佳化的程序。使用 AEM as a Cloud Service，客戶設定維護任務的操作屬性的需求會降至最低。客戶可以將他們的資源集中在應用程式層級的問題上，將基礎結構的操作交由 Adobe 進行。"

維護任務是依據排程執行以將存放庫最佳化的程序。使用 AEM as a Cloud Service，客戶設定維護任務的操作屬性的需求會降至最低。客戶可以將他們的資源集中在應用程式層級的問題上，將基礎結構的操作交由 Adobe 進行。

## 設定維護任務 {#maintenance-tasks-configuring}

在舊版AEM中，您可以使用維護卡（「工具>作業>維護」）來設定維護任務。 AEM as a Cloud Service的維護卡已無法使用，因此設定應認可至原始檔控制，並使用Cloud Manager進行部署。 Adobe會管理具有客戶無法設定之設定（例如資料存放區記憶體回收）的維護任務。 其他維護任務可由客戶設定，如下表所述。

>[!CAUTION]
>
>Adobe保留覆寫客戶維護任務組態設定的權利，以緩解效能降級等問題。

下表說明可用的維護任務。

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>維護任務</th>
    <th>擁有設定者</th>
    <th>如何設定（選擇性）</th>
  </tr>  
  <tr>
    <td>資料存放區記憶體回收</td>
    <td>Adobe</td>
    <td>不適用 — 完全由Adobe擁有</td>
  </td> 
  </tr>
  <tr>
    <td>版本清除</td>
    <td>客戶</td>
    <td>目前預設會停用版本清除，但可以設定原則，如<a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/operations/maintenance#purge_tasks">版本清除和稽核記錄清除維護工作</a>區段中所述。<br/><br/>預設即將啟用清除，這些值可覆寫。<br>
   </td>
  </td>
  </tr>
  <tr>
    <td>稽核記錄清除</td>
    <td>客戶</td>
    <td>稽核記錄清除目前預設為停用，但可以設定原則，如<a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/operations/maintenance#purge_tasks">版本清除和稽核記錄清除維護任務</a>一節中所述。<br/><br/>預設即將啟用清除，這些值可覆寫。<br>
   </td>
   </td>
  </tr>
  <tr>
    <td>Lucene 二進位清理</td>
    <td>Adobe</td>
    <td>未使用，因此被Adobe停用。</td>
  </td>
  </tr>
  <tr>
    <td>臨時任務清除</td>
    <td>客戶</td>
    <td>
    <p>必須在Git中完成。 覆寫<code>/libs</code>下的現成維護視窗設定節點，方法是在資料夾<code>/apps/settings/granite/operations/maintenance/granite_weekly</code>、<code>granite_daily</code>或<code>granite_monthly</code>下建立屬性。</p>
    <p>如需其他組態詳細資訊，請參閱下方的維護期間表格。 在上述節點底下新增另一個節點，以啟用維護任務。 將其命名為<code>granite_TaskPurgeTask</code>，屬性<code>sling:resourceType</code>設為<code>granite/operations/components/maintenance/task</code>，屬性<code>granite.maintenance.name</code>設為<code>TaskPurge</code>。 設定OSGI屬性，請參閱<code>com.adobe.granite.taskmanagement.impl.purge.TaskPurgeMaintenanceTask</code>以取得屬性清單。</p>
  </td>
  </tr>
    <tr>
    <td>工作流程清除</td>
    <td>客戶</td>
    <td>
    <p>必須在Git中完成。 覆寫<code>/libs</code>下的現成維護視窗設定節點，方法是在資料夾<code>/apps/settings/granite/operations/maintenance/granite_weekly</code>、<code>granite_daily</code>或<code>granite_monthly</code>下建立屬性。 如需其他組態詳細資訊，請參閱下方的維護期間表格。</p>
    <p>透過在上面的節點底下新增另一個具有適當屬性的節點（將其命名為<code>granite_WorkflowPurgeTask</code>）來啟用維護任務。 設定OSGI屬性，請參閱<a href="/help/sites-cloud/administering/workflows-administering.md#regular-purging-of-workflow-instances">定期清除工作流程執行個體</a>。</p>
  </td>
  </tr>
  <tr>
    <td>專案清除</td>
    <td>客戶</td>
    <td>
    <p>必須在Git中完成。 覆寫<code>/libs</code>下的現成維護視窗設定節點，方法是在資料夾<code>/apps/settings/granite/operations/maintenance/granite_weekly</code>、<code>granite_daily</code>或<code>granite_monthly</code>下建立屬性。 如需其他組態詳細資訊，請參閱下方的維護期間表格。</p>
    <p>透過在上面的節點底下新增另一個具有適當屬性的節點（將其命名為<code>granite_ProjectPurgeTask</code>）來啟用維護任務。 檢視<a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi">Adobe專案清除設定</a>的<b>OSGi屬性</b>清單。</p>
  </td>
  </tr>
  </tbody>
</table>

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>維護時段設定</th>
    <th>擁有設定者</th>
    <th>設定型別</th>
    <th>參數</th>
  </tr>
  <tr>
    <td>每日</td>
    <td>客戶</td>
    <td>jcr節點定義</td>
  <td>
  <p><strong>windowSchedule=daily</strong> （此值不應變更）</p>
  <p><strong>windowStartTime=HH：MM</strong>用作24小時時鐘。 定義與每日維護期間相關的維護任務何時開始執行。</p>
  <p><strong>windowEndTime=HH：MM</strong>用作24小時時鐘。 定義與每日維護視窗關聯的維護任務在尚未完成時應何時停止執行。</p>
  <p>在此時間範圍內，維護任務不能執行超過一次。</p>
  </td> 
  </tr>
  <tr>
    <td>每週</td>
    <td>客戶</td>
    <td>jcr節點定義</td>
    <td>
    <p><strong>windowSchedule=weekly</strong> （此值不應變更）</p>
    <p><strong>windowStartTime=HH：MM</strong>用作24小時時鐘。 定義與每週維護期間關聯的維護任務應何時開始執行。</p>
    <p><strong>windowEndTime=HH：MM</strong>用作24小時時鐘。 定義與每週維護視窗關聯的維護任務在尚未完成時應何時停止執行。</p>
    <p>在此時間範圍內，維護任務不能執行超過一次。</p>
    <p><strong>windowScheduleWeekdays =由1-7 （例如[5,5]）的兩個值組成的陣列</strong>陣列的第一個值是排程工作的開始日期，第二個值是停止工作的結束日期。 開始和結束的確切時間分別由windowStartTime和windowEndTime控制。</p>
    </td>
  </tr>
  <tr>
    <td>每月</td>
    <td>客戶</td>
    <td>jcr節點定義</td>
    <td>
    <p><strong>windowSchedule=monthly</strong> （此值不應變更）</p>
    <p><strong>windowStartTime=HH：MM</strong>用作24小時時鐘。 定義與每月維護視窗關聯的維護任務應何時開始執行。</p>
    <p><strong>windowEndTime=HH：MM</strong>用作24小時時鐘。 定義與每月維護視窗關聯的維護任務在尚未完成時應何時停止執行。</p>
    <p>在此時間範圍內，維護任務不能執行超過一次。</p>
    <p><strong>windowScheduleWeekdays=由1-7 （例如[5,5]）的兩個值組成的陣列</strong>陣列的第一個值是排程工作的開始日期，第二個值是停止工作的結束日期。 開始和結束的確切時間分別由windowStartTime和windowEndTime控制。</p>
    <p><strong>windowFirstLastStartDay= 0/1</strong> 0表示排程在每月的第一週，或1表示排程在每月最後一週。 若沒有值，則會有效地在受windowScheduleWeekdays （每月）控制的當天排程工作。</p>
    </td>
    </tr>
    </tbody>
</table>

**位置**：

* 每日 — /apps/settings/granite/operations/maintenance/granite_daily
* 每週 — /apps/settings/granite/operations/maintenance/granite_weekly
* 每月 — /apps/settings/granite/operations/maintenance/granite_monthly

**程式碼範例**：

程式碼範例1 （每日）

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" 
  xmlns:jcr="http://www.jcp.org/jcr/1.0" 
  jcr:primaryType="sling:Folder"
  sling:configCollectionInherit="true"
  sling:configPropertyInherit="true"
  windowSchedule="daily"
  windowStartTime="03:00"
  windowEndTime="05:00"
 />
```

程式碼範例2 （每週）

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" 
   xmlns:jcr="http://www.jcp.org/jcr/1.0"
   jcr:primaryType="sling:Folder"
   sling:configCollectionInherit="true"
   sling:configPropertyInherit="true"
   windowEndTime="15:30"
   windowSchedule="weekly"
   windowScheduleWeekdays="[5,5]"
   windowStartTime="14:30"/>
```

程式碼範例3 （每月）

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" 
   xmlns:jcr="http://www.jcp.org/jcr/1.0"
   jcr:primaryType="sling:Folder"
   sling:configCollectionInherit="true"
   sling:configPropertyInherit="true"
   windowEndTime="15:30"
   windowSchedule="monthly"
   windowFirstLastStartDay=0
   windowScheduleWeekdays="[5,5]"
   windowStartTime="14:30"/>
```

## 版本永久刪除與稽核日誌永久刪除維護作業 {#purge-tasks}

永久刪除版本和稽核記錄會減少存放庫的大小，在某些情況下，可以改善效能。

>[!NOTE]
>
>AEM Guides客戶不應設定「版本清除」。

### 預設值 {#defaults}

目前預設不會啟用清除，但未來將會變更。 在啟用預設清除之前建立的環境會有較保守的臨界值，因此清除不會意外發生。 如需有關預設永久刪除原則的詳細資訊，請參閱下方的「版本永久刪除」和「稽核日誌永久刪除」段落。
<!-- Version purging and audit log purging are on by default, with different default values for environments with ids higher than **TBD** versus those with ids lower than that value. -->

<!-- ### Overriding the default values with a new configuration {#override} -->

您可以宣告組態檔並將其部署（如下所述），來覆寫預設的清除值。

<!-- The reason for this behavior is to clarify the ambiguity over whether the default purge values would take effect once you remove the declaration. -->

### 套用設定 {#configure-purge}

宣告組態檔並部署，如下列步驟所述。

>[!NOTE]
>在組態檔案中部署版本清除節點後，您必須將其保持宣告狀態，且不得將其移除。 如果您嘗試這麼做，設定管道將會失敗。
> 
>同樣地，在組態檔中部署稽核記錄清除節點後，必須將其保持宣告狀態，不得將其移除。

**1**&#x200B;建立名為`mt.yaml`或類似的檔案。

**2**&#x200B;將檔案放置在名為`config`或類似名稱的頂層資料夾下，如[使用設定管道](/help/operations/config-pipeline.md#folder-structure)中所述。

**3** — 在組態檔中宣告屬性，包括：

* 資料節點上方的一些屬性 — 如需相關說明，請參閱[使用設定管道](/help/operations/config-pipeline.md#common-syntax)。 `kind`屬性值應該是&#x200B;*MaintenanceTasks*，而且版本應該設定為&#x200B;*1*。

* 同時具有`versionPurge`和`auditLogPurge`物件的資料物件。

請參閱下列`versionPurge`與`auditLogPurge`物件的定義與語法。

建構類似於以下範例的設定：

```
kind: "MaintenanceTasks"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  versionPurge:
    maximumVersions: 15
    maximumAgeDays: 20
    paths: ["/content"]
    minimumVersions: 1
    retainLabelledVersions: false
  auditLogPurge:
    rules:
      - replication:
          maximumAgeDays: 15
          contentPath: "/content"
          types: ["Activate", "Deactivate", "Delete", "Test", "Reverse", "Internal Poll"]
      - pages:
          maximumAgeDays: 15
          contentPath: "/content"
          types: ["PageCreated", "PageModified", "PageMoved", "PageDeleted", "VersionCreated", "PageRestored", "PageValid", "PageInvalid"]
      - dam:
          maximumAgeDays: 15
          contentPath: "/content"
          types: ["ASSET_EXPIRING", "METADATA_UPDATED", "ASSET_EXPIRED", "ASSET_REMOVED", "RESTORED", "ASSET_MOVED", "ASSET_VIEWED", "PROJECT_VIEWED", "PUBLISHED_EXTERNAL", "COLLECTION_VIEWED", "VERSIONED", "ADDED_COMMENT", "RENDITION_UPDATED", "ACCEPTED", "DOWNLOADED", "SUBASSET_UPDATED", "SUBASSET_REMOVED", "ASSET_CREATED", "ASSET_SHARED", "RENDITION_REMOVED", "ASSET_PUBLISHED", "ORIGINAL_UPDATED", "RENDITION_DOWNLOADED", "REJECTED"]
```

請記住，為了讓設定有效：

* 必須定義所有屬性。 沒有繼承的預設值。
* 下方屬性表格中的型別（整數、字串、布林值等）必須遵守。

**4** — 在Cloud Manager中建立設定管道，如[設定管道文章](/help/operations/config-pipeline.md#managing-in-cloud-manager)所述。

### 版本清除 {#version-purge}

>[!NOTE]
>
>AEM Guides客戶不應設定「版本清除」。

#### 版本清除預設值 {#version-purge-defaults}

<!-- For version purging, environments with an id higher than **TBD** have the following default values: -->

目前預設不會啟用清除，但未來將會變更。

啟用預設清除後建立的環境會有以下預設值：

* 超過30天的版本會被移除。
* 會保留過去30天內最近的五個版本。
* 無論上述規則為何，都會保留最新版本（以及目前的檔案）。

<!-- Environments with an id equal or lower than **TBD** will have the following default values: -->

在啟用預設清除之前建立的環境，其預設值會列於下方，但建議您降低這些值，以最佳化效能。

* 超過7年的版本會被移除。
* 會保留過去7年的所有版本。
* 7年後，最新版本以外的版本（除了目前的檔案）會被移除。

#### 版本清除屬性 {#version-purge-properties}

允許的屬性列於下方。

指示&#x200B;*預設*&#x200B;的資料行指示未來套用預設時的預設值；*待定*&#x200B;反映尚未確定的環境ID。

| 屬性 | 環境>待定的未來預設值 | 環境&lt;=TBD的未來預設值 | 必要 | 類型 | 值 |
|-----------|--------------------------|-------------|-----------|---------------------|-------------|
| 路徑 | [&quot;/content&quot;] | [&quot;/content&quot;] | 是 | 字串陣列 | 指定建立新版本時要在哪一個路徑下清除版本。  客戶必須宣告此屬性，但唯一允許值為「/content」。 |
| maximumAgeDays | 30 | 2557 （7年以上2個閏日） | 是 | 整數 | 系統會移除設定值之前的任何版本。 如果值為0，則不會根據版本的存留期執行永久刪除。 |
| maximumVersions | 5 | 0 （無限制） | 是 | 整數 | 第n個最新版本之前的任何版本都會被移除。 如果值為0，則不會根據版本數執行永久刪除。 |
| minimumVersions | 1 | 1 | 是 | 整數 | 無論年齡為何，保留的最低版本數量。 請注意，一律會保留至少1個版本；其值必須為1或更高。 |
| retainLabelledVersioned | false | false | 是 | 布林值 | 決定是否從清除中排除明確標籤的版本。 為求較佳的存放庫最佳化，建議將此值設為false。 |


**屬性互動**

下列範例說明屬性在結合時如何互動。

範例：

```
maximumAgeDays = 30
maximumVersions = 10
minimumVersions = 2
```

如果第23天有11個版本，則會在下次清除維護工作執行時清除最舊的版本，因為`maximumVersions`屬性設定為10。

如果第31天有5個版本，則只會清除3個，因為`minimumVersions`屬性設定為2。

範例：

```
maximumAgeDays = 30
maximumVersions = 0
minimumVersions = 1
```

由於`maximumVersions`屬性設為0，因此不會清除任何超過30天的版本。

將保留一個超過30天的版本。

### 稽核記錄清除 {#audit-purge}

#### 稽核記錄清除預設值 {#audit-purge-defaults}

<!-- For audit log purging, environments with an id higher than **TBD** have the following default values: -->

目前預設不會啟用清除，但未來將會變更。

啟用預設清除後建立的環境會有以下預設值：

* 會移除超過7天的復寫、DAM和頁面稽核記錄。
* 所有可能的事件都會記錄下來。

<!-- Environments with an id equal or lower than **TBD** will have the following default values: -->

在啟用預設清除之前建立的環境，其預設值會列於下方，但建議您降低這些值，以最佳化效能。

* 系統會移除超過7年的復寫、DAM和頁面稽核記錄。
* 所有可能的事件都會記錄下來。

>[!NOTE]
>建議符合法規要求，必須產生無法編輯之稽核記錄的客戶整合專門的外部服務。

#### 稽核記錄清除屬性 {#audit-purge-properties}

允許的屬性列於下方。

指示&#x200B;*預設*&#x200B;的資料行指示未來套用預設時的預設值；*待定*&#x200B;反映尚未確定的環境ID。


| 屬性 | 環境>待定的未來預設值 | 環境&lt;=TBD的未來預設值 | 必要 | 類型 | 值 |
|-----------|--------------------------|-------------|-----------|---------------------|-------------|
| 多項規則 | - | - | 是 | 物件 | 下列一或多個節點：復寫、頁面、dam。 這些節點中的每一個都會定義規則，其屬性如下。 所有屬性都必須宣告。 |
| maximumAgeDays | 7 天 | 2557年（7年以上2個閏日） | 是 | 整數 | 對於復寫、頁面或dam：稽核記錄的保留天數。 系統會清除早於設定值的稽核記錄。 |
| 內容路徑 | 「/content」 | 「/content」 | 是 | 字串 | 相關型別稽核記錄清除的路徑。 必須設定為「/content」。 |
| 型別 | 所有值 | 所有值 | 是 | 列舉陣列 | 針對&#x200B;**復寫**，列舉值為：啟用、停用、刪除、測試、反向、內部輪詢。 對於&#x200B;**頁面**，列舉值為： PageCreated、PageModified、PageMoved、PageDeleted、VersionCreated、PageRestored、PageRolled、PageValid、PageInvalid。 對於&#x200B;**dam**，列舉值為：ASSET_EXPIRING、METADATA_UPDATED、ASSET_EXPIRED、ASSET_REMOVED、RESTORED、ASSET_MOVED、ASSET_VIEWED、PROJECT_VIEWED、PUBLISHED_EXTERNAL、COLLECTION_VIEWED、VERSIONED、ADDED_COMMENT、RENDITION_UPDATED、ACCEPTED、DOWNATED、DOWNATED、DOWNATED、DOWNATED、SUBONED、SUBASSET、SUBASSET_UPDATED、RATED、RATED、RATED、ASSET_RATED、RATED_RATED、ASSET_RATED Shared、RENDITION_REMOVED、ASSET_PUBLISHED、ORIGINAL_UPDATED、RENDITION_DOWNLOADED、REJECTED。 |
