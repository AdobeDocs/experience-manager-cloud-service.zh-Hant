---
title: AEM as a Cloud Service 中的維護任務
description: 瞭解AEM as a Cloud Service中的維護任務以及如何進行設定。
exl-id: 5b114f94-be6e-4db4-bad3-d832e4e5a412
feature: Operations
role: Admin
source-git-commit: f8ef7e36ad602af96c3a6055db31ac328da808e6
workflow-type: tm+mt
source-wordcount: '2106'
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
    <td>不適用 — 完全Adobe擁有</td>
  </td> 
  </tr>
  <tr>
    <td>版本清除</td>
    <td>客戶</td>
    <td>目前預設會停用版本清除，但可以設定原則，如以下所述 <a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/operations/maintenance#purge_tasks">版本永久刪除與稽核日誌永久刪除維護作業</a> 區段。<br/><br/>預設會立即啟用清除，且這些值可覆寫。<br>
   </td>
  </td>
  </tr>
  <tr>
    <td>稽核記錄清除</td>
    <td>客戶</td>
    <td>稽核記錄清除目前預設為停用，但您可以設定原則，如中所述 <a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/operations/maintenance#purge_tasks">版本永久刪除與稽核日誌永久刪除維護作業</a> 區段。<br/><br/>預設會立即啟用清除，且這些值可覆寫。<br>
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
    <p>必須在Git中完成。 覆寫下的現成維護視窗設定節點 <code>/libs</code> 在資料夾下建立屬性 <code>/apps/settings/granite/operations/maintenance/granite_weekly</code>， <code>granite_daily</code> 或 <code>granite_monthly</code>.</p>
    <p>如需其他組態詳細資訊，請參閱下方的維護期間表格。 在上述節點底下新增另一個節點，以啟用維護任務。 將其命名 <code>granite_TaskPurgeTask</code>，具有屬性 <code>sling:resourceType</code> 設為 <code>granite/operations/components/maintenance/task</code> 和屬性 <code>granite.maintenance.name</code> 設為 <code>TaskPurge</code>. 設定OSGI屬性，請參閱 <code>com.adobe.granite.taskmanagement.impl.purge.TaskPurgeMaintenanceTask</code> 屬性清單的資訊。</p>
  </td>
  </tr>
    <tr>
    <td>工作流程清除</td>
    <td>客戶</td>
    <td>
    <p>必須在Git中完成。 覆寫下的現成維護視窗設定節點 <code>/libs</code> 在資料夾下建立屬性 <code>/apps/settings/granite/operations/maintenance/granite_weekly</code>， <code>granite_daily</code> 或 <code>granite_monthly</code>. 如需其他組態詳細資訊，請參閱下方的維護期間表格。</p>
    <p>在上述節點底下新增另一個節點（將其命名），以啟用維護任務 <code>granite_WorkflowPurgeTask</code>)，並具備適當的屬性。 設定OSGI屬性，請參閱 <a href="https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/workflows-administering.html#regular-purging-of-workflow-instances">AEM 6.5維護任務檔案</a>.</p>
  </td>
  </tr>
  <tr>
    <td>專案清除</td>
    <td>客戶</td>
    <td>
    <p>必須在Git中完成。 覆寫下的現成維護視窗設定節點 <code>/libs</code> 在資料夾下建立屬性 <code>/apps/settings/granite/operations/maintenance/granite_weekly</code>， <code>granite_daily</code> 或 <code>granite_monthly</code>. 如需其他組態詳細資訊，請參閱下方的維護期間表格。</p>
    <p>在上述節點底下新增另一個節點（將其命名），以啟用維護任務 <code>granite_ProjectPurgeTask</code>)，並具備適當的屬性。 請參閱「Adobe專案清除設定」底下的OSGI屬性清單。</p>
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
  <p><strong>windowStartTime=HH：MM</strong> 使用作為24小時時鐘。 定義與每日維護期間相關的維護任務何時開始執行。</p>
  <p><strong>windowEndTime=HH：MM</strong> 使用作為24小時時鐘。 定義與每日維護視窗關聯的維護任務在尚未完成時應何時停止執行。</p>
  <p>在此時間範圍內，維護任務不能執行超過一次。</p>
  </td> 
  </tr>
  <tr>
    <td>每週</td>
    <td>客戶</td>
    <td>jcr節點定義</td>
    <td>
    <p><strong>windowSchedule=weekly</strong> （此值不應變更）</p>
    <p><strong>windowStartTime=HH：MM</strong> 使用作為24小時時鐘。 定義與每週維護期間關聯的維護任務應何時開始執行。</p>
    <p><strong>windowEndTime=HH：MM</strong> 使用作為24小時時鐘。 定義與每週維護視窗關聯的維護任務在尚未完成時應何時停止執行。</p>
    <p>在此時間範圍內，維護任務不能執行超過一次。</p>
    <p><strong>windowScheduleWeekdays =兩個值的陣列，從1到7 （例如，[5,5]）</strong> 陣列的第一個值是排程工作的開始日期，第二個值是停止工作的結束日期。 開始和結束的確切時間分別由windowStartTime和windowEndTime控制。</p>
    </td>
  </tr>
  <tr>
    <td>每月</td>
    <td>客戶</td>
    <td>jcr節點定義</td>
    <td>
    <p><strong>windowSchedule=每月</strong> （此值不應變更）</p>
    <p><strong>windowStartTime=HH：MM</strong> 使用作為24小時時鐘。 定義與每月維護視窗關聯的維護任務應何時開始執行。</p>
    <p><strong>windowEndTime=HH：MM</strong> 使用作為24小時時鐘。 定義與每月維護視窗關聯的維護任務在尚未完成時應何時停止執行。</p>
    <p>在此時間範圍內，維護任務不能執行超過一次。</p>
    <p><strong>windowScheduleWeekdays =介於1-7之間的兩個值陣列（例如，[5,5]）</strong> 陣列的第一個值是排程工作的開始日期，第二個值是停止工作的結束日期。 開始和結束的確切時間分別由windowStartTime和windowEndTime控制。</p>
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

**1**  — 在Git中專案的頂層資料夾中建立以下資料夾和檔案結構：

```
config/
     mt.yaml
```

**2**  — 在設定檔案中宣告屬性，包括：

* 值為「MaintenanceTasks」的「kind」屬性。
* 「版本」屬性（目前我們為版本1）。
* 具有屬性的選用「metadata」物件 `envTypes` 以逗號分隔此組態有效的環境型別(dev、stage、prod)清單。 如果未宣告任何中繼資料物件，則該設定對所有環境型別都有效。
* 同時具有兩者的資料物件 `versionPurge` 和 `auditLogPurge` 物件。

請參閱的定義與語法 `versionPurge` 和 `auditLogPurge` 物件。

您應建構類似於以下範例的設定：

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

>[!NOTE]
>您可以使用 `yq` 在本機驗證組態檔的YAML格式(例如， `yq mt.yaml`)。

**3**  — 設定非生產和生產設定管道。

快速開發環境(RDE)不支援清除。 對於生產（非沙箱）計畫中的其他環境型別，在Cloud Manager中建立目標部署設定管道。

另請參閱 [設定生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) 和 [設定非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) 以取得更多詳細資料。

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

此欄表示 *預設* 指定未來套用預設值時的預設值； *待定* 會反映仍未決定的環境ID。

| 屬性 | 環境>待定的未來預設值 | 環境&lt;=TBD的未來預設值 | 必要 | 類型 | 值 |
|-----------|--------------------------|-------------|-----------|---------------------|-------------|
| 路徑 | [「/content」] | [「/content」] | 是 | 字串陣列 | 指定建立新版本時要在哪一個路徑下清除版本。  客戶必須宣告此屬性，但唯一允許值為「/content」。 |
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

如果第23天有11個版本，則會在下次清除維護作業執行時清除最舊的版本，因為 `maximumVersions` 屬性設為10。

如果第31天有5個版本，則只會清除3個版本，因為 `minimumVersions` 屬性設為2。

範例：

```
maximumAgeDays = 30
maximumVersions = 0
minimumVersions = 1
```

由於30天以上的版本，將不會清除 `maximumVersions` 屬性設為0。

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

此欄表示 *預設* 指定未來套用預設值時的預設值； *待定* 會反映仍未決定的環境ID。


| 屬性 | 環境>待定的未來預設值 | 環境&lt;=TBD的未來預設值 | 必要 | 類型 | 值 |
|-----------|--------------------------|-------------|-----------|---------------------|-------------|
| 多項規則 | - | - | 是 | 物件 | 下列一或多個節點：復寫、頁面、dam。 這些節點中的每一個都會定義規則，其屬性如下。 所有屬性都必須宣告。 |
| maximumAgeDays | 7 天 | 2557年（7年以上2個閏日） | 是 | 整數 | 對於復寫、頁面或dam：稽核記錄的保留天數。 系統會清除早於設定值的稽核記錄。 |
| 內容路徑 | 「/content」 | 「/content」 | 是 | 字串 | 相關型別稽核記錄清除的路徑。 必須設定為「/content」。 |
| 型別 | 所有值 | 所有值 | 是 | 列舉陣列 | 的 **復寫**，列舉值為：啟用、停用、刪除、測試、反向、內部輪詢。 的 **頁面**，列舉值為： PageCreated、PageModified、PageMoved、PageDeleted、VersionCreated、PageRestored、PageRolled、PageValid、PageInvalid。 的 **dam**，列舉值為：ASSET_EXPIRING、METADATA_UPDATED、ASSET_EXPIRED、ASSET_REMOVED、RESTORED、ASSET_MOVED、ASSET_VIEWED、PROJECT_VIEWED、PUBLISHED_EXTERNAL、COLLECTION_VIEWED、VERSIONED、ADDED_COMMENT、RENDITION_UPDATED、ACCEPTED、DOWNLOADED、SUBASED、SUBASSET、ASSET_CREATED、ASSET_CREATED、CREATED、ASSEATED_ASSET、CREATED_CREATED_ASSET、CREATED_CREATED、ASSEATED_ASSET_CREATED_CREATED、ASSEATED_ASSEATED_ASSED_ASSEATED_ASSEATED_ASSEATED_ASSET REMOVED、ASSET_PUBLISHED、ORIGINAL_UPDATED、RENDITION_DOWNLOADED、已拒絕。 |
