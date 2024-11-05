---
title: 在資產檢視中管理報告
description: 存取資產檢視之報告區段的資料，評估產品和功能使用情況，並得出關鍵成功量度的見解。
exl-id: 26d0289e-445a-4b8e-a5a1-b02beedbc3f1
feature: Asset Insights, Asset Reports
role: User, Admin, Developer
source-git-commit: 5ff36490c4d9a6f61255ad06ffab984f18c1823b
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 31%

---

# 管理報告 {#manage-reports}

| [搜尋最佳實務](/help/assets/search-best-practices.md) | [中繼資料最佳實務](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [具有 OpenAPI 功能的 Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開發人員文件](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

資產報告可讓管理員檢視Adobe Experience Manager Assets檢視環境的活動。 此資料提供有關使用者如何與內容和產品互動的有用資訊。所有使用者可以存取「深入分析」儀表板，且獲指派至管理員產品設定檔的使用者可以建立使用者定義的報告。

## 存取報告 {#access-reports}

指派至資產檢視管理員產品設定檔的所有使用者可以在資產檢視中存取 Insights 儀表板或建立使用者定義的報告。

若要存取報告，請導覽至「**[!UICONTROL 設定]**」下的「**[!UICONTROL 報告]**」。

![報告](assets/reports.png)

<!--
In the **[!UICONTROL Reports]** screen, various components are shown in the tabular format which includes the following:

* **Title**: Title of the report
* **Type**: Determines whether the report is uploaded or downloaded to the repository
* **Description**: Provide details of the report that was given during uploading/downloading the report
* **Status**: Determines whether the report is completed, under progress, or deleted.
* **Author**: Provides email of the author who has uploaded/downloaded the report.
* **Created**: Gives information of the date when the report was generated.
-->

## 建立報表 {#create-report}

AEM Assets檢視環境可透過報表控制面板提供全面的報告功能。 此功能可讓使用者產生和下載CSV報告，詳細說明指定時間段內的資產上傳和下載，範圍從一次到每日、每週、每月或每年間隔。

**若要建立報告：**

1. 瀏覽至&#x200B;**報表**，然後按一下&#x200B;**建立報表** （從右上方）。 **建立報告**對話方塊會顯示下列欄位：
   ![建立報告](/help/assets/assets/executed-reports1.svg)

   **在設定索引標籤中：**

   1. **報表型別：**&#x200B;在上傳和下載型別之間選取。
   1. **標題：**&#x200B;新增標題至報表。
   1. **描述：**&#x200B;新增選擇性描述至報表。
   1. **選取資料夾路徑：**&#x200B;選取資料夾路徑，以產生該特定資料夾中已上傳和已下載資產的報表。 例如，如果您需要上傳至資料夾的資產報表，請指定該資料夾的路徑。
   1. **選取日期間隔：**&#x200B;選取檢視資料夾內上傳或下載活動的日期範圍。
   <br>

   >[!NOTE]
   >
   > 資產檢視會將所有本地時區轉換為世界協調時間 (UTC)。

   **在資料行索引標籤中：**&#x200B;選取要在報告中顯示的資料行名稱。 下表說明所有欄的使用：

   <table>
    <tbody>
     <tr>
      <th><strong>資料行名稱</strong></th>
      <th><strong>說明</strong></th>
      <th><strong>報告型別</strong></th>
     </tr>
     <tr>
      <td>標題</td>
      <td>輸入資產的標題。</td>
      <td>上傳和下載</td>
     </tr>
     <tr>
      <td>路徑</td>
      <td>資產檢視中可用資產的資料夾路徑。</td>
      <td>上傳和下載</td>
     </tr>
     <tr>
      <td>MIME 類型</td>
      <td>資產的 MIME 類型。</td>
      <td>上傳和下載</td>
     </tr>
     <tr>
      <td>大小</td>
      <td>資產位元組的大小。</td>
      <td>上傳和下載</td>
     </tr>
     <tr>
      <td>下載者</td>
      <td>下載資產的使用者的電子郵件ID。</td>
      <td>下載</td>
     </tr>
     <tr>
      <td>下載日期</td>
      <td>執行資產下載動作的日期。</td>
      <td>下載</td>
     </tr>
     <tr>
      <td>作者</td>
      <td>資產的作者。</td>
      <td>上傳和下載</td>
     </tr>
     <tr>
      <td>建立日期</td>
      <td>資產上載到資產檢視的日期。</td>
      <td>上傳和下載</td>
     </tr>
     <tr>
      <td>修改日期</td>
      <td>上次修改資產的日期。</td>
      <td>上傳和下載</td>
     </tr>
     <tr>
      <td>過期</td>
      <td>資產的到期狀態。</td>
      <td>上傳和下載</td>
     </tr>
     <tr>
      <td>按使用者名稱下載</td>
      <td>下載資產的使用者的名稱。</td>
      <td>下載</td>
     </tr>           
    </tbody>
   </table>

## 檢視和下載現有報表 {#View-and-download-existing-report}

現有報告會顯示在&#x200B;**已執行報告**&#x200B;標籤下。 按一下「**報表**」並選取「**已執行報表**」以檢視所有建立且狀態為「**已完成**」的報表，表示它們已可供下載。 若要下載CSV格式的報表或刪除報表，請選取報表列。 然後選取&#x200B;**下載CSV**&#x200B;或&#x200B;**刪除**。
![檢視及下載現有報告](/help/assets/assets/view-download-existing-report.png)

## 排程報表 {#schedule-report}

在AEM Assets檢視UI中，**排程報表**&#x200B;會設定在指定的未來間隔（例如每日、每週、每月或每年）自動生成報表。 此功能有助於簡化週期性報表需求，並確保及時更新資料。 同時&#x200B;**建立報告**&#x200B;會產生過去日期的報告。 已完成的報告列在&#x200B;**已執行的報告**&#x200B;下，而即將產生的報告列在&#x200B;**排程報告**&#x200B;下。

若要排程報表，請遵循下列步驟：

1. 從左窗格按一下「報表」 ，然後從右上方按一下「建立報表」 。
1. 報告對話方塊會顯示下列資訊：
   1. **報表型別：**&#x200B;在上傳和下載型別之間選取。
   1. **標題：**&#x200B;新增標題至報表。
   1. **描述**：新增選擇性描述至報表。
   1. **選取資料夾路徑：**&#x200B;選取資料夾路徑，以針對未來將上傳至該特定資料夾或從該特定資料夾下載的資產產生報表。
   1. 切換&#x200B;**排程報告：**切換可排程報告在稍後執行，或重複執行。
      ![排程報告](/help/assets/assets/schedule-reports1.svg)

   1. **選擇頻率：**&#x200B;指定產生報告的間隔（例如，每日、每週、每月、每年或一次），並設定執行報告的日期和時間，以及週期結束日期。 對於一次性報表，請在AEM環境中選取活動型別，並選取報表的日期範圍。 例如，如果您需要特定月份從10日到29日（未來日期）的已下載資產報表，請在&#x200B;**選取日期間隔**&#x200B;欄位中選取這些日期。

   >[!NOTE]
   >
   > 資產檢視會將所有本地時區轉換為世界協調時間 (UTC)。

## 檢視排程報告 {#view-scheduled-reports}

排程報告會以系統整理的方式顯示在&#x200B;**排程報告**&#x200B;標籤下。 每個排程報告的所有已完成報告都儲存在單一報告資料夾中。 按一下![展開摺疊](/help/assets/assets/expand-icon1.svg)以檢視完成的報表。 例如，如果您已排程每日報表，則所有完成的報表會分組到一個資料夾中。 這個組織可簡化報表的導覽和可發現性。 若要檢視排程報告，請按一下&#x200B;**報告**，然後按一下&#x200B;**排程報告**。 所有排程報告都會顯示，其狀態為進行中或完成。 已完成的報告可供下載。\
![排程報告](/help/assets/assets/scheduled-reports-tab.png)

## 編輯和取消排程報告 {#edit-cancel-scheduled-reports}

1. 瀏覽至&#x200B;**排程報告**&#x200B;索引標籤。
1. 選取報表列。
1. 按一下&#x200B;**編輯**。
1. 按一下&#x200B;**取消排程**，然後按一下&#x200B;**確認**，以取消排程報告。 對於已取消的報告，下次執行時間會變成空白，且狀態會顯示為已取消。
   ![編輯和取消排程報告](/help/assets/assets/cancel-edit-scheduled-reports.png)

### 恢復排程 {#resume-schedule}

若要繼續取消的排程，請選取報表列，然後按一下&#x200B;**繼續排程**。 恢復後，下一個執行階段專案會再次顯示，且狀態會顯示為進行中。
![繼續排程](/help/assets/assets/resume-schedule.png)

>[!NOTE]
>
> 如果您在排定的結束日期之前恢復取消的報表，則會自動產生從取消日期到恢復日期的報表。

## 檢視 Insights {#view-live-statistics}

資產檢視使您能夠使用 Insights 儀表板查看資產檢視環境的即時資料。您可以查看過去 30 天或過去 12 個月的即時事件度量。

<!--![Toolbar options when you select an asset](assets/assets-view-live-statistics.png)-->

按一下左側導覽窗格中可用的「**[!UICONTROL 深入分析]**」以檢視以下自動產生的圖表：

* **下載**：使用折線圖表示過去30天或12個月內從Assets檢視環境下載的資產數量。
  ![深入分析 — 下載](/help/assets/assets/insights-downloads2341.svg)

* **上傳**：使用折線圖表示過去30天或12個月內上傳至Assets檢視環境的資產數量。
  ![分析 — 上傳](/help/assets/assets/insights-uplods2.svg)
  <!--* **Asset Count by Size**: The division of count of assets based on their range of various sizes from 0 MB to 100 GB.-->

* **儲存空間使用量**：使用長條圖表示的Assets檢視環境儲存空間使用量（位元組）。
  ![分析 — 上傳](/help/assets/assets/insights-storage-usage1.svg)
  <!--* **Delivery**: The graph depicts the count of assets as the delivery dates.-->

<!--* **Asset Count by Asset Type**: Represents count of various MIME types of the available assets. For example, application/zip, image/png, video/mp4, application/postscripte.-->

* **熱門搜尋**：以表格格式檢視過去 30 天或 12 個月內，在資產檢視環境中熱門搜尋詞彙以及這些詞彙的搜尋次數。
  ![分析 — 上傳](/help/assets/assets/insights-top-search.svg)
  <!--
   ![Insights](assets/insights1.png)
   ![Insights](assets/insights2.png)
   -->
* **依大小劃分的資產計數：**將資產視圖環境中的總資產計數劃分為不同的大小範圍，突出顯示每個大小範圍內的資產數量和百分比，以圓環圖表示。
  ![依大小劃分的資產計數深入解析](/help/assets/assets/insights-assets-count-by-size.svg)
* **依資產型別區分的資產計數：**區段Assets檢視環境中的資產總計計數，根據資產的檔案型別反白顯示資產的計數和百分比，以環形圖表示。
  ![依大小劃分的資產計數深入解析](/help/assets/assets/insights-assest-count-by-asset-type1.svg)