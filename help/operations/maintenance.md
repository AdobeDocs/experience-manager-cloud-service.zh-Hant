---
title: AEM as a Cloud Service 中的維護任務
description: AEM as a Cloud Service 中的維護任務
exl-id: 5b114f94-be6e-4db4-bad3-d832e4e5a412
source-git-commit: 19a3ebd981a7a62fe78a9ec909547b6a70c55121
workflow-type: tm+mt
source-wordcount: '1107'
ht-degree: 13%

---

# AEM as a Cloud Service 中的維護任務 {#maintenance-tasks-in-aem-as-a-cloud-service}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_maintenance"
>title="維護任務"
>abstract="維護任務是依據排程執行以將存放庫最佳化的程序。使用 AEM as a Cloud Service，客戶設定維護任務的操作屬性的需求會降至最低。客戶可以將他們的資源集中在應用程式層級的問題上，將基礎結構的操作交由 Adobe 進行。"

維護任務是依據排程執行以將存放庫最佳化的程序。使用 AEM as a Cloud Service，客戶設定維護任務的操作屬性的需求會降至最低。客戶可以將他們的資源集中在應用程式層級的問題上，將基礎結構的操作交由 Adobe 進行。

## 設定維護任務 {#maintenance-tasks-configuring}

在舊版AEM中，您可以使用維護卡（「工具>作業>維護」）來設定維護任務。 對於AEMas a Cloud Service，維護卡不再可用，因此設定應認可到原始檔控制並使用Cloud Manager部署。 Adobe會管理具有客戶無法設定之設定的維護任務（例如，資料存放區垃圾收集、稽核記錄清除、版本清除）。 其他維護任務可由客戶設定，如下表所述。

>[!CAUTION]
>
>Adobe保留覆寫客戶維護任務組態設定的權利，以緩解效能降級等問題。

下表說明發行AEMas a Cloud Service時可用的維護工作。

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>維護任務</th>
    <th>擁有設定者</th>
    <th>如何設定（選擇性）</th>
  </tr>  
  <tr>
    <td>資料存放區垃圾收集</td>
    <td>Adobe</td>
    <td>不適用 — 完全Adobe擁有</td>
  </td> 
  </tr>
  <tr>
    <td>版本清除</td>
    <td>Adobe</td>
    <td>對於現有環境（在2023年9月1日之前建立的環境），清除功能會停用，且日後不會啟用，除非客戶明確啟用，且客戶當時可能也會使用自訂值設定該功能。<br><br> <!--Alexandru: leave the two line breaks in place, otherwise spacing won't render properly-->新環境（自2023年9月1日起建立的環境）預設會啟用清除，使用下列值，客戶可以設定自訂值。
     <ol>
       <li>超過30天的版本會被移除</li>
       <li>會保留過去30天內最新的5個版本</li>
       <li>無論上述規則為何，都會保留最新版本。</li>
       <br>建議有法規要求的客戶將網站頁面完全依照特定日期顯示，並整合專門的外部服務。
     </ol></td>
  </td>
  </tr>
  <tr>
    <td>稽核記錄清除</td>
    <td>Adobe</td>
    <td>對於現有環境（在2023年9月1日之前建立的環境），清除功能會停用，且日後不會啟用，除非客戶明確啟用，且客戶當時可能也會使用自訂值設定該功能。<br><br> <!-- See above for the two line breaks -->新環境（自2023年9月1日起建立的環境）將預設啟用「 」下的清除。 <code>/content</code> 存放庫的節點，根據下列行為：
     <ol>
       <li>針對復寫稽核，會移除超過3天的稽核記錄</li>
       <li>針對DAM （資產）稽核，會移除超過30天的稽核記錄</li>
       <li>若為頁面稽核，則會移除超過3天的記錄。</li>
       <br>建議有法規要求的客戶製作無法編輯的稽核記錄，並與專門的外部服務整合。
     </ol></td>
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
    <p>如需其他組態詳細資訊，請參閱下方的維護視窗表格。 在上面的節點底下新增另一個節點，以啟用維護任務。 將其命名 <code>granite_TaskPurgeTask</code>，具有屬性 <code>sling:resourceType</code> 設定為 <code>granite/operations/components/maintenance/task</code> 和屬性 <code>granite.maintenance.name</code> 設定為 <code>TaskPurge</code>. 設定OSGI屬性，請參閱 <code>com.adobe.granite.taskmanagement.impl.purge.TaskPurgeMaintenanceTask</code> 屬性清單。</p>
  </td>
  </tr>
    <tr>
    <td>工作流程清除</td>
    <td>客戶</td>
    <td>
    <p>必須在Git中完成。 覆寫下的現成維護視窗設定節點 <code>/libs</code> 在資料夾下建立屬性 <code>/apps/settings/granite/operations/maintenance/granite_weekly</code>， <code>granite_daily</code> 或 <code>granite_monthly</code>. 如需其他組態詳細資訊，請參閱下方的維護視窗表格。</p>
    <p>在上面的節點底下新增另一個節點（將其命名），以啟用維護任務 <code>granite_WorkflowPurgeTask</code>)，並具備適當的屬性。 設定OSGI屬性，請參閱 <a href="https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/workflows-administering.html#regular-purging-of-workflow-instances">AEM 6.5維護任務檔案</a>.</p>
  </td>
  </tr>
  <tr>
    <td>專案清除</td>
    <td>客戶</td>
    <td>
    <p>必須在Git中完成。 覆寫下的現成維護視窗設定節點 <code>/libs</code> 在資料夾下建立屬性 <code>/apps/settings/granite/operations/maintenance/granite_weekly</code>， <code>granite_daily</code> 或 <code>granite_monthly</code>. 如需其他組態詳細資訊，請參閱下方的維護視窗表格。</p>
    <p>在上面的節點底下新增另一個節點（將其命名），以啟用維護任務 <code>granite_ProjectPurgeTask</code>)，並具備適當的屬性。 請參閱「Adobe專案清除設定」底下的OSGI屬性清單。</p>
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
    <td>JCR節點定義</td>
  <td>
  <p><strong>windowSchedule=daily</strong> （此值不應變更）</p>
  <p><strong>windowStartTime=HH：MM</strong> 使用作為24小時時鐘。 定義與每日維護視窗相關聯的維護任務應何時開始執行。</p>
  <p><strong>windowEndTime=HH：MM</strong> 使用作為24小時時鐘。 定義與每日維護視窗關聯的維護任務在尚未完成時應何時停止執行。</p>
  <p>在此時間範圍內，維護任務不能執行超過一次。</p>
  </td> 
  </tr>
  <tr>
    <td>每週</td>
    <td>客戶</td>
    <td>JCR節點定義</td>
    <td>
    <p><strong>windowSchedule=weekly</strong> （此值不應變更）</p>
    <p><strong>windowStartTime=HH：MM</strong> 使用作為24小時時鐘。 定義與每週維護視窗相關聯的維護任務應何時開始執行。</p>
    <p><strong>windowEndTime=HH：MM</strong> 使用作為24小時時鐘。 定義與每週維護視窗關聯的維護任務在尚未完成時應何時停止執行。</p>
    <p>在此時間範圍內，維護任務不能執行超過一次。</p>
    <p><strong>windowScheduleWeekdays =介於1-7之間的兩個值的陣列（例如，[5,5]）</strong> 陣列的第一個值是排程工作的開始日期，第二個值是停止工作的結束日期。 開始和結束的確切時間分別由windowStartTime和windowEndTime控制。</p>
    </td>
  </tr>
  <tr>
    <td>每月</td>
    <td>客戶</td>
    <td>JCR節點定義</td>
    <td>
    <p><strong>windowSchedule=每月</strong> （此值不應變更）</p>
    <p><strong>windowStartTime=HH：MM</strong> 使用作為24小時時鐘。 定義與每月維護視窗關聯的維護任務應何時開始執行。</p>
    <p><strong>windowEndTime=HH：MM</strong> 使用作為24小時時鐘。 定義與每月維護視窗關聯的維護任務在尚未完成時應何時停止執行。</p>
    <p>在此時間範圍內，維護任務不能執行超過一次。</p>
    <p><strong>windowScheduleWeekdays =介於1-7之間的兩個值的陣列（例如，[5,5]）</strong> 陣列的第一個值是排程工作的開始日期，第二個值是停止工作的結束日期。 開始和結束的確切時間分別由windowStartTime和windowEndTime控制。</p>
    <p><strong>windowFirstLastStartDay= 0/1</strong> 0表示排程在每月的第一週，或1表示排程在每月的最後一週。 若沒有值，則會有效地將工作排程在windowScheduleWeekdays所管轄的日期（每月）。</p>
    </td>
    </tr>
    </tbody>
</table>

**位置**:

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
