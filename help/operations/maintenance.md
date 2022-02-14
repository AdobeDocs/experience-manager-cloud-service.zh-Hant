---
title: 維護任AEM務as a Cloud Service
description: 維護任AEM務as a Cloud Service
exl-id: 5b114f94-be6e-4db4-bad3-d832e4e5a412
source-git-commit: 83fe5c7b3a30f2444cddd982e9cc14a07c410530
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 2%

---

# 維護任AEM務as a Cloud Service

>[!CONTEXTUALHELP]
>id="aemcloud_golive_maintenance"
>title="維護任務"
>abstract="維護任務是按計畫運行以優化儲存庫的進程。 隨著AEMas a Cloud Service，客戶配置維護任務的操作屬性的需求非常小。 客戶可以將資源集中在應用程式級別的問題上，從而讓基礎架構操作保持Adobe。"

維護任務是按計畫運行以優化儲存庫的進程。 隨著AEMas a Cloud Service，客戶配置維護任務的操作屬性的需求非常小。 客戶可以將資源集中在應用程式級別的問題上，從而讓基礎架構操作保持Adobe。

## 配置維護任務

在以前的版本AEM中，您可以使用維護卡（「工具」>「操作」>「維護」）配置維護任務。 對於AEMas a Cloud Service，維護卡不再可用，因此應提交配置以使用雲管理器進行原始碼控制和部署。 Adobe將管理不需要客戶決策的維護任務（例如，資料儲存垃圾收集），而客戶可以配置其他維護任務（請參閱下表）。

>[!CAUTION]
>
>Adobe保留覆蓋客戶維護任務配置設定以緩解效能降級等問題的權利。

下表說明了在as a Cloud Service發佈時可用的維護任AEM務。

| 維護任務 | 誰擁有配置 | 如何配置（可選） |
|---|---|---|
| 資料儲存垃圾收集 | Adobe | N/A — 完全Adobe |
| 版本清除 | Adobe | 完全歸Adobe所有，但在將來，客戶將能夠配置某些參數。 |
| 審核日誌清除 | Adobe | 完全歸Adobe所有，但在將來，客戶將能夠配置某些參數。 |
| Lucene 二進位清理 | Adobe | 未使用，因此被Adobe禁用。 |
| 即席任務清除 | 客戶 | 必須用github完成。 <br> 覆蓋「現成維護」窗口配置節點 `/libs` 在資料夾下建立屬性 `/apps/settings/granite/operations/maintenance/granite_weekly` 或 `granite_daily`。 有關其他配置詳細資訊，請參閱下面的「維護窗口」表。 <br> 通過在上面的節點下添加另一個節點（將其命名為）來啟用維護任務 `granite_TaskPurgeTask`)。 <br> 配置OSGI屬性，請參閱 [AEM6.5維護任務文檔](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |
| 工作流程清除 | 客戶 | 必須用github完成。 <br> 覆蓋「現成維護」窗口配置節點 `/libs` 在資料夾下建立屬性`/apps/settings/granite/operations/maintenance/granite_weekly` 或 `granite_daily`。 有關其他配置詳細資訊，請參閱下面的「維護窗口」表。 <br> 通過在上面的節點下添加另一個節點（將其命名為）來啟用維護任務 `granite_WorkflowPurgeTask`)。 <br> 配置OSGI屬性，請參見 [AEM6.5維護任務文檔](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |
| 專案清除 | 客戶 | 必須用github完成。 <br> 覆蓋「現成維護」窗口配置節點 `/libs` 在資料夾下建立屬性 `/apps/settings/granite/operations/maintenance/granite_weekly` 或 `granite_daily`。 有關其他配置詳細資訊，請參閱下面的「維護窗口」表。 <br> 通過在上面的節點下添加節點（將其命名為）來啟用維護任務 `granite_ProjectPurgeTask`)。 <br> 配置OSGI屬性，請參見 [AEM6.5維護任務文檔](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |

客戶可以計畫在每日、每週或每月維護窗口中執行的工作流清除、即席任務清除和項目清除維護任務。 應直接在原始碼管理中編輯這些配置。 下表說明了每個窗口可用的配置參數。 另請參見表後提供的位置和代碼示例。

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>維護窗口配置</th>
    <th>誰擁有配置</th>
    <th>配置類型</th>
    <th>參數</th>
  </tr>
  <tr>
    <td>每日</td>
    <td>客戶</td>
    <td>JCR節點定義</td>
  <td>
  <p><strong>windowSchedule=daily</strong> （不應更改此值）</p>
  <p><strong>windowStartTime=HH:MM</strong> 24小時鐘。 定義與「每日維護」窗口關聯的維護任務應何時開始執行。</p>
  <p><strong>windowEndTime=HH:MM</strong> 24小時鐘。 定義與「每日維護」窗口關聯的維護任務在尚未完成時應停止執行的時間。</p>
  </td> 
  </tr>
  <tr>
    <td>每週</td>
    <td>客戶</td>
    <td>JCR節點定義</td>
    <td>
    <p><strong>windowSchedule=weekly</strong> （不應更改此值）</p>
    <p><strong>windowStartTime=HH:MM</strong> 24小時鐘。 定義與每週維護窗口關聯的維護任務何時開始執行。</p>
    <p><strong>windowEndTime=HH:MM</strong> 24小時鐘。 定義與「每週維護」窗口關聯的維護任務在尚未完成時應停止執行的時間。</p>
    <p><strong>windowScheduleWeekdays=1-7之間的2個值的陣列(例如[5,5])</strong> 陣列的第一個值是調度作業的開始日，第二個值是停止作業的結束日。 開始和結束的確切時間分別由windowStartTime和windowEndTime控制。</p>
    </td>
  </tr>
  <tr>
    <td>每月</td>
    <td>客戶</td>
    <td>JCR節點定義</td>
    <td>
    <p><strong>windowSchedule=daily</strong> （不應更改此值）</p>
    <p><strong>windowStartTime=HH:MM</strong> 24小時鐘。 定義與「每月維護」窗口關聯的維護任務何時開始執行。</p>
    <p><strong>windowEndTime=HH:MM</strong> 24小時鐘。 定義與「每月維護」窗口關聯的維護任務在尚未完成時停止執行的時間。</p>
    <p><strong>windowScheduleWeekdays=1-7之間的2個值的陣列(例如[5,5])</strong> 陣列的第一個值是調度作業的開始日，第二個值是停止作業的結束日。 開始和結束的確切時間分別由windowStartTime和windowEndTime控制。</p>
    <p><strong>windowFirstLastStartDay= 0/1</strong> 0：計畫本月的第一週，1：計畫本月的最後一週。 如果缺少值，則有效地將每天的作業安排在windowScheduleWeekdays的管轄範圍內。</p>
    </td> 
    </tr>
    </tbody>
</table>

**位置**:

* 每日 — /apps/settings/granite/operations/maintenance/granite_daily
* 每週 — /apps/settings/granite/operations/maintenance/granite_weekl
* 每月 — /apps/settings/granite/operations/maintenance/granite_monthly

**代碼示例**:

代碼示例1（每日）

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

代碼示例2（每週）

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

代碼示例3（每月）

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
