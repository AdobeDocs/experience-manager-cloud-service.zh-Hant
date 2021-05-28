---
title: AEM as aCloud Service中的維護任務
description: AEM as aCloud Service中的維護任務
exl-id: 5b114f94-be6e-4db4-bad3-d832e4e5a412
source-git-commit: 22228ebfbc754551f93907502c53427ba43983b3
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 2%

---

# AEM as aCloud Service中的維護任務

>[!CONTEXTUALHELP]
>id="aemcloud_golive_maintenance"
>title="維護任務"
>abstract="維護任務是按計畫運行以優化儲存庫的進程。 以AEM為Cloud Service，客戶配置維護任務的操作屬性的需求極低。 客戶可以將資源集中在應用程式級別的問題上，使基礎架構操作留待Adobe。"
>additional-url="https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html" text="AEM維護指南"
>additional-url="https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/operations-dashboard.html#AutomatedMaintenanceTasks" text="操作儀表板維護任務"

維護任務是按計畫運行以優化儲存庫的進程。 以AEM為Cloud Service，客戶配置維護任務的操作屬性的需求極低。 客戶可以將資源集中在應用程式級別的問題上，使基礎架構操作留待Adobe。

有關維護任務的其他資訊，請參閱以下頁面：

* [AEM維護指南](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html)
* [操作儀表板維護任務](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/operations-dashboard.html#AutomatedMaintenanceTasks)

## 配置維護任務

在舊版AEM中，您可以使用維護卡（工具>操作>維護）來設定維護任務。 對於AEM as aCloud Service，維護卡已不再提供，因此應使用Cloud Manager將設定提交至原始碼控制並部署。 Adobe將管理不需要客戶決策的維護任務（例如，資料儲存垃圾回收），而客戶可以配置其他維護任務（請參閱下表）。

>[!CAUTION]
>
>Adobe保留覆寫客戶維護任務配置設定的權利，以緩解效能降低等問題。

下表說明AEM as aCloud Service發行時可用的維護任務。

| 維護任務 | 誰擁有配置 | 如何配置（可選） |
|---|---|---|
| 資料儲存垃圾收集 | Adobe | 不適用 — 完全擁有Adobe |
| 版本清除 | Adobe | 完全歸Adobe所有，但日後客戶將能設定特定參數。 |
| 審核日誌清除 | Adobe | 完全歸Adobe所有，但日後客戶將能設定特定參數。 |
| Lucene 二進位清理 | Adobe | 未使用，因此由Adobe禁用。 |
| 臨機任務清除 | 客戶 | 必須使用github完成。 <br> 在資料夾或下方建立屬性，以覆寫底下 `/libs` 的現成維護視窗設 `/apps/settings/granite/operations/maintenance/granite_weekly` 定節 `granite_daily`點。有關其他配置詳細資訊，請參閱下面的「維護窗口」表。 <br> 通過在上面的節點下添加另一個節點（將其命名為）並 `granite_TaskPurgeTask`使用相應的屬性來啟用維護任務。<br> 設定OSGI屬性，請參閱 [AEM 6.5維護工作檔案](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |
| 工作流程清除 | 客戶 | 必須使用github完成。 <br> 在資料夾下建立屬性，以覆寫底下 `/libs` 的現成維護視窗`/apps/settings/granite/operations/maintenance/granite_weekly` 設定節 `granite_daily`點。有關其他配置詳細資訊，請參閱下面的「維護窗口」表。 <br> 通過在上面的節點下添加另一個節點（將其命名為）並 `granite_WorkflowPurgeTask`使用相應的屬性來啟用維護任務。<br> 設定OSGI屬性，請參閱 [AEM 6.5維護工作檔案](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |
| 專案清除 | 客戶 | 必須使用github完成。 <br> 在資料夾或下方建立屬性，以覆寫底下 `/libs` 的現成維護視窗設 `/apps/settings/granite/operations/maintenance/granite_weekly` 定節 `granite_daily`點。有關其他配置詳細資訊，請參閱下面的「維護窗口」表。 <br> 通過在上面的節點下添加節點（將其命名為）以及相應的 `granite_ProjectPurgeTask`屬性來啟用維護任務。<br> 設定OSGI屬性請參閱 [AEM 6.5維護工作檔案](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |

客戶可以計畫在每日、每週或每月維護窗口中執行的每個「工作流清除」、「臨機任務清除」和「項目清除維護」任務。 應直接在原始碼控制項中編輯這些配置。 下表說明了每個窗口可用的配置參數。 另請參閱表格後提供的位置和程式碼範例。

<table>
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
  <p><strong>windowSchedule=daily</strong> （此值不應變更）</p>
  <p><strong>windowStartTime=HH:</strong> 使用為24小時時鐘。定義與「每日維護」窗口關聯的維護任務何時開始執行。</p>
  <p><strong>windowEndTime=HH:</strong> 使用為24小時時鐘。定義與每日維護窗口關聯的維護任務何時應停止執行（如果它們尚未完成）。</p>
  </td> 
  </tr>
  <tr>
    <td>每週</td>
    <td>客戶</td>
    <td>JCR節點定義</td>
    <td>
    <p><strong>windowSchedule=weekly</strong> （不應變更此值）</p>
    <p><strong>windowStartTime=HH:</strong> 使用為24小時時鐘。定義與每週維護窗口關聯的維護任務何時開始執行。</p>
    <p><strong>windowEndTime=HH:</strong> 使用為24小時時鐘。定義與每週維護窗口關聯的維護任務何時應停止執行（如果它們尚未完成）。</p>
    <p><strong>windowScheduleWeekdays=從1到7的2個值的陣列(例如[5,5])</strong> 陣列的第一個值是排程作業的開始日，第二個值是作業停止的結束日。開始和結束的確切時間分別由windowStartTime和windowEndTime控制。</p>
    </td>
  </tr>
  <tr>
    <td>每月</td>
    <td>客戶</td>
    <td>JCR節點定義</td>
    <td>
    <p><strong>windowSchedule=daily</strong> （此值不應變更）</p>
    <p><strong>windowStartTime=HH:</strong> 使用為24小時時鐘。定義與每月維護窗口關聯的維護任務何時開始執行。</p>
    <p><strong>windowEndTime=HH:</strong> 使用為24小時時鐘。定義與每月維護窗口關聯的維護任務何時應停止執行（如果它們尚未完成）。</p>
    <p><strong>windowScheduleWeekdays=從1到7的2個值的陣列(例如[5,5])</strong> 陣列的第一個值是排程作業的開始日，第二個值是作業停止的結束日。開始和結束的確切時間分別由windowStartTime和windowEndTime控制。</p>
    <p><strong>windowFirstLastStartDay= 0/1 </strong> 0，在月的第一週排程，或在月的最後一週排程1。如果缺少值，則有效地每天安排由windowScheduleWeekdays管理的作業。</p>
    </td> 
    </tr>
    </tbody>
</table>

**位置**:

* 每日 — /apps/settings/granite/operations/maintenance/granite_daily
* 每週 — /apps/settings/granite/operations/maintenance/granite_weekly
* 每月 — /apps/settings/granite/operations/maintenance/granite_monthly

**程式碼範例**:

程式碼範例1（每日）

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

程式碼範例2（每週）

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

程式碼範例3（每月）

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
