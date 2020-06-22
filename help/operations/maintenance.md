---
title: AEM中的Maintenance Tasks as a Cloud Service
description: 'AEM中的Maintenance Tasks as a Cloud Service '
translation-type: tm+mt
source-git-commit: e9ee1064c5fa62b56c822a18ad6ca8cc4d09fa75
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 2%

---


# AEM中的Maintenance Tasks as a Cloud Service

維護任務是按計畫運行以優化儲存庫的進程。 將AEM視為雲端服務，客戶對維護工作的營運屬性設定的需求微乎其微。 客戶可將資源集中在應用程式層級的考量上，將基礎架構作業交給Adobe。

有關維護任務的其他資訊，請參見以下頁：

* [AEM維護指南](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html)
* [Operations Dashboard維護任務](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/operations-dashboard.html#AutomatedMaintenanceTasks)

## 配置維護任務

在舊版AEM中，您可以使用維護卡（「工具>作業>維護」）來設定維護工作。 對於AEM做為雲端服務，維護卡已不再提供，因此應使用Cloud Manager將設定提交至來源控制並部署。 Adobe將管理不需要客戶決策的維護工作（例如，Datastore Garbage Collection），而客戶可以設定其他維護工作（請參閱下表）。

>[!CAUTION]
>
>Adobe保留覆寫客戶維護工作組態設定的權利，以緩解效能降低等問題。

下表說明在AEM發行時可用的「雲端服務」維護工作。

| 維護任務 | 誰擁有配置 | 如何設定（選用） |
|---|---|---|
| 資料儲存廢棄項目收集 | Adobe | 不適用——完全由Adobe擁有 |
| 版本清除 | Adobe | Adobe完全擁有，但客戶日後將可設定特定參數。 |
| 審核日誌清除 | Adobe | Adobe完全擁有，但客戶日後將可設定特定參數。 |
| Lucene 二進位清理 | Adobe | 未使用，因此Adobe已停用。 |
| 臨機任務清除 | 客戶 | 必須用github完成。 <br> 通過在資料夾或下建立屬性，覆蓋下 `/libs` 的「現成維護」窗口配置節 `/apps/settings/granite/operations/maintenance/granite_weekly` 點 `granite_daily`。 有關其他配置詳細資訊，請參閱下面的維護窗口表。 <br> 通過在上述節點下添加另一個節點(命名該節點 `granite_TaskPurgeTask`)和相應屬性來啟用維護任務。 <br> 設定OSGI屬性，請參閱 [AEM 6.5維護工作檔案](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |
| 工作流程清除 | 客戶 | 必須用github完成。 <br> 通過在資料夾或下建立屬性，覆蓋下 `/libs` 的「現成維護」窗口配置節點`/apps/settings/granite/operations/maintenance/granite_weekly``granite_daily`。 有關其他配置詳細資訊，請參閱下面的維護窗口表。 <br> 通過在上述節點下添加另一個節點(命名該節點 `granite_WorkflowPurgeTask`)和相應屬性來啟用維護任務。 <br> 設定OSGI屬性，請參 [閱AEM 6.5維護工作檔案](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |
| 專案清除 | 客戶 | 必須用github完成。 <br> 通過在資料夾或下建立屬性，覆蓋下 `/libs` 的「現成維護」窗口配置節 `/apps/settings/granite/operations/maintenance/granite_weekly` 點 `granite_daily`。 有關其他配置詳細資訊，請參閱下面的維護窗口表。 <br> 通過在上面的節點下添加節點（將其命名）並添加相應的屬 `granite_ProjectPurgeTask`性來啟用維護任務。 <br> 設定OSGI屬性，請參 [閱AEM 6.5維護工作檔案](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |

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
    <td><code>/apps/settings/granite/operations/maintenance/granite_daily </code></td>
    <td>請參閱下方的程式碼範例1</td>
   <td>
    <ul>
    <li><strong>windowSchedule</strong> = daily（此值不應變更）</li>
    <li><strong>windowStartTime</strong> = HH:MM，用作24小時時鐘。 定義與Daily Maintenance Windows關聯的Maintenance Tasks何時應開始執行。</li>
    <li><strong>windowEndTime</strong> = HH:MM，用作24小時時鐘。 定義與「每日維護」窗口關聯的維護任務何時應停止執行（如果尚未完成）。</li>
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
    <li><strong>windowStartTime</strong> = HH:MM，用作24小時時鐘。 定義與每週維護窗口關聯的維護任務何時開始執行。</li>
    <li><strong>windowEndTime</strong> = HH:MM，用作24小時時鐘。 定義與「每週維護窗口」關聯的維護任務何時應停止執行（如果尚未完成）。</li>
    <li><strong>windowScheduleWekdays = 1-7之間的2個值陣列。 例如， [5,5]</strong> 陣列的第一個值是調度作業的開始日，第二個值是停止作業的結束日。 開始和結束的確切時間分別由windowStartTime和windowEndTime控制。</li>
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
    <li><strong>windowSchedule</strong> = daily（此值不應變更）</li>
    <li><strong>windowStartTime</strong> = HH:MM，用作24小時時鐘。 定義與「每月維護」窗口關聯的維護任務何時開始執行。</li>
    <li><strong>windowEndTime</strong> = HH:MM，用作24小時時鐘。 定義與「每月維護」窗口關聯的維護任務何時應停止執行（如果尚未完成）。</li>
    <li><strong>windowScheduleWekdays = 1-7之間的2個值陣列。 例如， [5,5]</strong> 陣列的第一個值是調度作業的開始日，第二個值是停止作業的結束日。 開始和結束的確切時間分別由windowStartTime和windowEndTime控制。</li>
    <li><strong>windowFirstLastStartDay - 0/1</strong> 0，以排程當月的第一週，或1，排程當月的最後一週。 如果缺少值，則有效地每天排程工作，並受每月windowScheduleWeekdays的管理。</li>
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

程式碼範例2

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
