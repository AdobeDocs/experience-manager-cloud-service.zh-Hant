---
title: 維護任AEM務作為Cloud Service
description: 維護任AEM務作為Cloud Service
exl-id: 5b114f94-be6e-4db4-bad3-d832e4e5a412
translation-type: tm+mt
source-git-commit: d53d34e86b5e5bac6a66be8d288cf4ab8fb00ac4
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 2%

---

# 維護任AEM務作為Cloud Service

維護任務是按計畫運行以優化儲存庫的進程。 作為AEMCloud Service，客戶對於配置維護任務的操作屬性的需求非常小。 客戶可將資源集中在應用程式級別上，讓基礎架構操作與Adobe。

有關維護任務的其他資訊，請參見以下頁：

* [維AEM護指南](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html)
* [Operations Dashboard維護任務](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/operations-dashboard.html#AutomatedMaintenanceTasks)

## 配置維護任務

在舊版中，您可AEM以使用維護卡（「工具」>「操作」>「維護」）來設定維護工作。 作為AEMCloud Service，維護卡已不再可用，因此應使用Cloud Manager將配置提交到源控制並部署。 Adobe將管理不需要客戶決策的維護任務（例如，資料儲存廢棄項收集），而客戶可以配置其他維護任務（請參見下表）。

>[!CAUTION]
>
>Adobe保留覆寫客戶維護任務配置設定的權利，以緩解效能降低等問題。

下表說明了作為Cloud Service在發行時可用的維AEM護任務。

| 維護任務 | 誰擁有配置 | 如何設定（選用） |
|---|---|---|
| 資料儲存廢棄項目收集 | Adobe | N/A —— 完全擁有Adobe |
| 版本清除 | Adobe | 完全歸Adobe所有，但是在未來，客戶將能夠設定特定參數。 |
| 審核日誌清除 | Adobe | 完全歸Adobe所有，但是在未來，客戶將能夠設定特定參數。 |
| Lucene 二進位清理 | Adobe | 未使用，因此被Adobe禁用。 |
| 臨機任務清除 | 客戶 | 必須用github完成。 <br> 通過在資料夾或下建立屬性，覆蓋下 `/libs` 的「現成維護」窗口配 `/apps/settings/granite/operations/maintenance/granite_weekly` 置節點 `granite_daily`。有關其他配置詳細資訊，請參閱下面的維護窗口表。 <br> 通過在上述節點下添加另一個節點(命名該節點 `granite_TaskPurgeTask`)和相應屬性來啟用維護任務。<br> 配置OSGI屬性，請參 [閱AEM6.5維護任務文檔](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |
| 工作流程清除 | 客戶 | 必須用github完成。 <br> 通過在資料夾下建立屬性，覆蓋下的「現成維護」 `/libs` 窗口配置節`/apps/settings/granite/operations/maintenance/granite_weekly` 點 `granite_daily`。有關其他配置詳細資訊，請參閱下面的維護窗口表。 <br> 通過在上述節點下添加另一個節點(命名該節點 `granite_WorkflowPurgeTask`)和相應屬性來啟用維護任務。<br> 配置OSGI屬性，請參 [閱AEM6.5維護任務文檔](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |
| 專案清除 | 客戶 | 必須用github完成。 <br> 通過在資料夾或下建立屬性，覆蓋下 `/libs` 的「現成維護」窗口配 `/apps/settings/granite/operations/maintenance/granite_weekly` 置節點 `granite_daily`。有關其他配置詳細資訊，請參閱下面的維護窗口表。 <br> 通過在上面的節點下添加節點（將其命名）並添加相應的屬 `granite_ProjectPurgeTask`性來啟用維護任務。<br> 配置OSGI屬性，請 [參AEM閱6.5維護任務文檔](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |

客戶可以計畫在每日、每週或每月維護窗口期間執行的每個工作流清除、臨機任務清除和項目清除維護任務。 這些配置應直接在原始碼控制中編輯。 下表說明每個窗口可用的配置參數。

<table>
  <tr>
    <th>維護窗口配置</th>
    <th>誰擁有配置</th>
    <th>配置類型</th>
    <th>位置</th>
    <th>範例</th>
    <th>參數</th>
  </tr>
  <tr>
    <td>每日</td>
    <td>客戶</td>
    <td>JCR節點定義</td>
    <td>/apps/settings/granite/operations/maintenance/granite_daily</td>
    <td>請參閱程式碼範例1標籤</td>
   <td>
    <ul>
    <li><strong>windowSchedule</strong> = daily（此值不應更改）</li>
    <li><strong>windowStartTime</strong> = HH:MM，用作24小時時鐘。定義與Daily Maintenance Windows關聯的Maintenance Tasks何時應開始執行。</li>
    <li><strong>windowEndTime</strong> = HH:MM，用作24小時時鐘。定義與「每日維護」窗口關聯的維護任務何時應停止執行（如果尚未完成）。</li>
    </ul> </td> 
  </tr>
  <tr>
    <td>每週</td>
    <td>客戶</td>
    <td>JCR節點定義</td>
    <td><code>/apps/settings/granite/operations/maintenance/granite_weekly</code></td>
    <td>請參閱下方的程式碼範例2</td>
     <td>
    <ul>
    <li><strong>windowSchedule</strong> = weekly（此值不應變更）</li>
    <li><strong>windowStartTime</strong> = HH:MM，用作24小時時鐘。定義與每週維護窗口關聯的維護任務何時開始執行。</li>
    <li><strong>windowEndTime</strong> = HH:MM，用作24小時時鐘。定義與「每週維護窗口」關聯的維護任務何時應停止執行（如果尚未完成）。</li>
    <li><strong>windowScheduleWekdays = 1-7之間的2個值陣列。例如，[5,5]</strong> 陣列的第一個值是調度作業的開始日，第二個值是停止作業的結束日。開始和結束的確切時間分別由windowStartTime和windowEndTime控制。</li>
    </ul> </td> 
  </tr>
  <tr>
    <td>每月</td>
    <td>客戶</td>
    <td>JCR節點定義</td>
    <td><code>/apps/settings/granite/operations/maintenance/granite_monthly</code></td>
    <td>請參閱下方的程式碼範例3</td>
     <td>
    <ul>
    <li><strong>windowSchedule</strong> = daily（此值不應更改）</li>
    <li><strong>windowStartTime</strong> = HH:MM，用作24小時時鐘。定義與「每月維護」窗口關聯的維護任務何時開始執行。</li>
    <li><strong>windowEndTime</strong> = HH:MM，用作24小時時鐘。定義與「每月維護」窗口關聯的維護任務何時應停止執行（如果尚未完成）。</li>
    <li><strong>windowScheduleWekdays = 1-7之間的2個值陣列。例如，[5,5]</strong> 陣列的第一個值是調度作業的開始日，第二個值是停止作業的結束日。開始和結束的確切時間分別由windowStartTime和windowEndTime控制。</li>
    <li><strong>windowFirstLastStartDay - 0/1</strong> 0，排程每月的第一週，或排程每月的最後一週。如果缺少值，則有效地每天排程工作，並受每月windowScheduleWeekdays的管理。</li>
    </ul> </td> 
  </tr>
</table>

程式碼範例1

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

程式碼範例2

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

程式碼範例3

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
