---
title: AEM as a Cloud Service 中的維護任務
description: AEM as a Cloud Service 中的維護任務
exl-id: 5b114f94-be6e-4db4-bad3-d832e4e5a412
source-git-commit: 8bd001f6f70ce1aa9a63623b3ad68793fa355c9a
workflow-type: tm+mt
source-wordcount: '999'
ht-degree: 4%

---

# AEM as a Cloud Service 中的維護任務 {#maintenance-tasks-in-aem-as-a-cloud-service}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_maintenance"
>title="維護任務"
>abstract="維護任務是按計畫運行以優化儲存庫的進程。 隨著AEMas a Cloud Service，客戶配置維護任務的操作屬性的需求非常小。 客戶可以將資源集中在應用程式級別的問題上，從而讓基礎架構操作保持Adobe。"

維護任務是按計畫運行以優化儲存庫的進程。 隨著AEMas a Cloud Service，客戶配置維護任務的操作屬性的需求非常小。 客戶可以將資源集中在應用程式級別的問題上，從而讓基礎架構操作保持Adobe。

## 配置維護任務

在以前的版本AEM中，您可以使用維護卡（「工具」>「操作」>「維護」）配置維護任務。 對於AEMas a Cloud Service，維護卡不再可用，因此應提交配置以使用雲管理器進行原始碼控制和部署。 Adobe管理那些具有客戶無法配置的設定的維護任務（例如，資料儲存垃圾收集、審核日誌清除、版本清除）。 其他維護任務可由客戶配置，如下表所述。

>[!CAUTION]
>
>Adobe保留覆蓋客戶維護任務配置設定以緩解效能降級等問題的權利。

下表說明了在as a Cloud Service發佈時可用的維護任AEM務。

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>維護任務</th>
    <th>誰擁有配置</th>
    <th>如何配置（可選）</th>
  </tr>  
  <tr>
    <td>資料儲存垃圾收集</td>
    <td>Adobe</td>
    <td>N/A — 完全Adobe</td>
  </td> 
  </tr>
  <tr>
    <td>版本清除</td>
    <td>Adobe</td>
    <td>為了使作者層保持效能，在 <code>/content</code> 根據以下行為清除儲存庫的節點：<br><br> <!--Alexandru: please leave the two line breaks in place, otherwise spacing won't render properly-->
     <ol>
       <li>刪除30天以上的版本</li>
       <li>最近30天中的5個版本保留</li>
       <li>不論上述規則如何，最新版本都將保留。</li>
     </ol><br>注：對於2022年3月14日之後建立的新環境，預設情況下會強制執行上述行為。 如果您需要不同的設定，請提交客戶支援票證。</td>
  </td>
  </tr>
  <tr>
    <td>審核日誌清除</td>
    <td>Adobe</td>
    <td>為了使作者層保持效能， <code>/content</code> 根據以下行為清除儲存庫的節點：<br><br> <!-- See above for the two line breaks -->
     <ol>
       <li>對於複製審核，刪除3天以上的審核日誌</li>
       <li>對於DAM（資產）審核，刪除30天以上的審核日誌</li>
       <li>對於頁面審核，刪除3天以上的日誌。</li>
     </ol><br>注：對於2022年3月14日之後建立的新環境，預設情況下會強制執行上述行為。 如果您需要不同的設定，請提交客戶支援票證。</td>
   </td>
  </tr>
  <tr>
    <td>Lucene 二進位清理</td>
    <td>Adobe</td>
    <td>未使用，因此被Adobe禁用。</td>
  </td>
  </tr>
  <tr>
    <td>即席任務清除</td>
    <td>客戶</td>
    <td>
    <p>必須用Git完成。 覆蓋「現成維護」窗口配置節點 <code>/libs</code> 在資料夾下建立屬性 <code>/apps/settings/granite/operations/maintenance/granite_weekly</code> 或 <code>granite_daily</code>。</p>
    <p>有關其他配置詳細資訊，請參閱下面的「維護窗口」表。 通過在上面的節點下添加另一個節點（將其命名為）來啟用維護任務 <code>granite_TaskPurgeTask</code>)。 配置OSGI屬性。</p>
  </td>
  </tr>
    <tr>
    <td>工作流程清除</td>
    <td>客戶</td>
    <td>
    <p>必須用Git完成。 覆蓋「現成維護」窗口配置節點 <code>/libs</code> 在資料夾下建立屬性 <code>/apps/settings/granite/operations/maintenance/granite_weekly</code> 或 <code>granite_daily</code>。 有關其他配置詳細資訊，請參閱下面的「維護窗口」表。</p>
    <p>通過在上面的節點下添加另一個節點（將其命名為）來啟用維護任務 <code>granite_WorkflowPurgeTask</code>)。 配置OSGI屬性，請參見 <a href="https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/workflows-administering.html#regular-purging-of-workflow-instances">AEM6.5維護任務文檔</a>。</p>
  </td>
  </tr>
  <tr>
    <td>專案清除</td>
    <td>客戶</td>
    <td>
    <p>必須用Git完成。 覆蓋「現成維護」窗口配置節點 <code>/libs</code> 在資料夾下建立屬性 <code>/apps/settings/granite/operations/maintenance/granite_weekly</code> 或 <code>granite_daily</code>。 有關其他配置詳細資訊，請參閱下面的「維護窗口」表。</p>
    <p>通過在上面的節點下添加另一個節點（將其命名為）來啟用維護任務 <code>granite_ProjectPurgeTask</code>)。 配置OSGI屬性。</p>
  </td>
  </tr>
  </tbody>
</table>

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
