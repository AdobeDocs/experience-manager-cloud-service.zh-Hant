---
title: AEM as a Cloud Service 中的維護任務
description: AEM as a Cloud Service 中的維護任務
exl-id: 5b114f94-be6e-4db4-bad3-d832e4e5a412
source-git-commit: 4e820caa043eeba22d14894d6943c957ea0bf80a
workflow-type: tm+mt
source-wordcount: '1013'
ht-degree: 4%

---

# AEM as a Cloud Service 中的維護任務 {#maintenance-tasks-in-aem-as-a-cloud-service}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_maintenance"
>title="維護任務"
>abstract="維護任務是按計畫運行以優化儲存庫的進程。 使用AEMas a Cloud Service，客戶配置維護任務的操作屬性的需求非常小。 客戶可以將資源集中在應用程式級別的問題上，使基礎架構操作留待Adobe。"

維護任務是按計畫運行以優化儲存庫的進程。 使用AEMas a Cloud Service，客戶配置維護任務的操作屬性的需求非常小。 客戶可以將資源集中在應用程式級別的問題上，使基礎架構操作留待Adobe。

## 配置維護任務 {#maintenance-tasks-configuring}

在舊版AEM中，您可以使用維護卡（工具>操作>維護）來設定維護任務。 若為AEMas a Cloud Service，維護卡將不再提供，因此應使用Cloud Manager將設定提交至原始碼控制並部署。 Adobe管理那些具有客戶無法配置的設定的維護任務（例如，資料儲存垃圾收集、審核日誌清除、版本清除）。 客戶可以配置其他維護任務，如下表所述。

>[!CAUTION]
>
>Adobe保留覆寫客戶維護任務配置設定的權利，以緩解效能降低等問題。

下表說明AEM as a Cloud Service發行時可用的維護任務。

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
    <td>不適用 — 完全擁有Adobe</td>
  </td> 
  </tr>
  <tr>
    <td>版本清除</td>
    <td>Adobe</td>
    <td>對於現有環境（在2023年3月1日之前建立的環境），清除會停用，且除非客戶明確啟用，否則將來不會啟用，屆時客戶也可以使用自訂值來設定清除。<br><br> <!--Alexandru: please leave the two line breaks in place, otherwise spacing won't render properly-->新環境（從2023年3月1日開始建立的環境）預設會啟用清除，並包含下列值，讓客戶能夠使用自訂值進行設定。
     <ol>
       <li>30天以前的版本會遭移除</li>
       <li>會保留過去30天內的最新5個版本</li>
       <li>不論上述規則為何，都會保留最新版本。</li>
     </ol></td>
  </td>
  </tr>
  <tr>
    <td>審核日誌清除</td>
    <td>Adobe</td>
    <td>對於現有環境（在2023年3月1日之前建立的環境），清除會停用，且除非客戶明確啟用，否則將來不會啟用，屆時客戶也可以使用自訂值來設定清除。<br><br> <!-- See above for the two line breaks -->新環境（從2023年3月1日開始建立的環境）將依預設在 <code>/content</code> 儲存庫的節點，依下列行為進行：
     <ol>
       <li>對於複製審核，將刪除3天以前的審核日誌</li>
       <li>若是DAM(Assets)稽核，超過30天的稽核記錄會遭到移除</li>
       <li>對於頁面稽核，會移除3天以前的記錄檔。</li>
     </ol></td>
   </td>
  </tr>
  <tr>
    <td>Lucene 二進位清理</td>
    <td>Adobe</td>
    <td>未使用，因此由Adobe禁用。</td>
  </td>
  </tr>
  <tr>
    <td>臨機任務清除</td>
    <td>客戶</td>
    <td>
    <p>必須以Git完成。 覆蓋下的現成維護窗口配置節點 <code>/libs</code> 在資料夾下建立屬性 <code>/apps/settings/granite/operations/maintenance/granite_weekly</code> 或 <code>granite_daily</code>.</p>
    <p>有關其他配置詳細資訊，請參閱下面的「維護窗口」表。 通過在上面的節點下添加其他節點（將其命名為）來啟用維護任務 <code>granite_TaskPurgeTask</code>)和適當的屬性。 設定OSGI屬性。</p>
  </td>
  </tr>
    <tr>
    <td>工作流程清除</td>
    <td>客戶</td>
    <td>
    <p>必須以Git完成。 覆蓋下的現成維護窗口配置節點 <code>/libs</code> 在資料夾下建立屬性 <code>/apps/settings/granite/operations/maintenance/granite_weekly</code> 或 <code>granite_daily</code>. 有關其他配置詳細資訊，請參閱下面的「維護窗口」表。</p>
    <p>通過在上面的節點下添加其他節點（將其命名為）來啟用維護任務 <code>granite_WorkflowPurgeTask</code>)和適當的屬性。 設定OSGI屬性請參閱 <a href="https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/workflows-administering.html#regular-purging-of-workflow-instances">AEM 6.5維護任務檔案</a>.</p>
  </td>
  </tr>
  <tr>
    <td>專案清除</td>
    <td>客戶</td>
    <td>
    <p>必須以Git完成。 覆蓋下的現成維護窗口配置節點 <code>/libs</code> 在資料夾下建立屬性 <code>/apps/settings/granite/operations/maintenance/granite_weekly</code> 或 <code>granite_daily</code>. 有關其他配置詳細資訊，請參閱下面的「維護窗口」表。</p>
    <p>通過在上面的節點下添加其他節點（將其命名為）來啟用維護任務 <code>granite_ProjectPurgeTask</code>)和適當的屬性。 設定OSGI屬性。</p>
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
  <p><strong>windowSchedule=daily</strong> （此值不應變更）</p>
  <p><strong>windowStartTime=HH:MM</strong> 24小時。 定義與「每日維護」窗口關聯的維護任務何時開始執行。</p>
  <p><strong>windowEndTime=HH:MM</strong> 24小時。 定義與每日維護窗口關聯的維護任務何時應停止執行（如果它們尚未完成）。</p>
  </td> 
  </tr>
  <tr>
    <td>每週</td>
    <td>客戶</td>
    <td>JCR節點定義</td>
    <td>
    <p><strong>windowSchedule=weekly</strong> （此值不應變更）</p>
    <p><strong>windowStartTime=HH:MM</strong> 24小時。 定義與每週維護窗口關聯的維護任務何時開始執行。</p>
    <p><strong>windowEndTime=HH:MM</strong> 24小時。 定義與每週維護窗口關聯的維護任務何時應停止執行（如果它們尚未完成）。</p>
    <p><strong>windowScheduleWekdays=從1到7的2個值的陣列（例如[5,5]）</strong> 陣列的第一個值是排程作業的開始日，第二個值是作業停止的結束日。 開始和結束的確切時間分別由windowStartTime和windowEndTime控制。</p>
    </td>
  </tr>
  <tr>
    <td>每月</td>
    <td>客戶</td>
    <td>JCR節點定義</td>
    <td>
    <p><strong>windowSchedule=daily</strong> （此值不應變更）</p>
    <p><strong>windowStartTime=HH:MM</strong> 24小時。 定義與每月維護窗口關聯的維護任務何時開始執行。</p>
    <p><strong>windowEndTime=HH:MM</strong> 24小時。 定義與每月維護窗口關聯的維護任務何時應停止執行（如果它們尚未完成）。</p>
    <p><strong>windowScheduleWeekdays=從1到7的2個值的陣列（例如[5,5]）</strong> 陣列的第一個值是排程作業的開始日，第二個值是作業停止的結束日。 開始和結束的確切時間分別由windowStartTime和windowEndTime控制。</p>
    <p><strong>windowFirstLastStartDay= 0/1</strong> 0：在月的第一週排程，或1：在月的最後一週排程。 如果缺少值，則有效地每天安排由windowScheduleWeekdays管理的作業。</p>
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
