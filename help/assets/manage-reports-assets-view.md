---
title: 在「資產」檢視中管理報表
description: 存取Assets檢視的報表區段中的資料，以評估產品和功能使用情況並取得關鍵成功量度的深入分析。
exl-id: c7155459-05d9-4a95-a91f-a1fa6ae9d9a4
source-git-commit: df82681338f8ca1a34df6118cbddc6642aa8d4b5
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 71%

---

# 管理報告 {#manage-reports}

>[!CONTEXTUALHELP]
>id="assets_reports"
>title="報告"
>abstract="資產報告可讓管理員檢視Adobe Experience Manager Assets檢視環境的活動。 此資料提供有關使用者如何與內容和產品互動的有用資訊。指派至管理員產品設定檔的所有使用者可以存取 Insights 儀表板或建立使用者定義的報告。"

資產報告可讓管理員檢視Adobe Experience Manager Assets檢視環境的活動。 此資料提供有關使用者如何與內容和產品互動的有用資訊。

## 訪問報告 {#access-reports}

指派給Assets檢視管理員產品設定檔的所有使用者都可以存取Insights儀表板或在Assets檢視中建立使用者定義的報告。

## 檢視 Insights {#view-live-statistics}

「資產」檢視可讓您使用「見解」儀表板檢視「資產」檢視環境的即時資料。 您可以查看過去 30 天或過去 12 個月的即時事件度量。

![選取資產時可用的工具列選項](assets/assets-essentials-live-statistics.png)

按一下左側導覽窗格中可用的「**[!UICONTROL Insights]**」以檢視以下自動產生的圖表：

* **下載**：使用折線圖表示過去30天或12個月內從資產檢視環境下載的資產數量。

* **上傳**：使用折線圖表示過去30天或12個月內上傳至「資產」檢視環境的資產數量。

* **熱門搜尋**：以表格格式顯示過去30天或12個月內，在「資產」檢視環境中檢視熱門搜尋詞語及其搜尋次數。

<!--

* **Storage usage**: The storage usage, in gigabytes (GB), for the Assets view environment, for the last 30 days or 12 months represented using a bar chart.

-->

## 建立下載報告 {#create-download-report}

若要建立下載報告：

1. 瀏覽到 **[!UICONTROL 設定]** > **[!UICONTROL 報告]** 按一下 **[!UICONTROL 建立報告]**。

1. 在[!UICONTROL 配置]頁籤，將報表類型指定為&#x200B;**[!UICONTROL 下載]**。

1. 指定報告的標題和說明 (選用)。

1. 使用 **[!UICONTROL 選擇資料夾路徑]** 的子選單。

1. 選擇報告的日期間隔。

   >[!NOTE]
   >
   > 「資產」檢視將所有當地時區轉換為世界協調時間(UTC)。

1. 在 [!UICONTROL 列] 頁籤，選擇需要在報告中顯示的列名。

1. 按一下&#x200B;**[!UICONTROL 建立]**。

   ![下載報告](assets/download-reports-config.png)

下表說明了可添加到報告的所有列的使用：

<table>
    <tbody>
     <tr>
      <th><strong>資料行名稱</strong></th>
      <th><strong>說明</strong></th>
     </tr>
     <tr>
      <td>標題</td>
      <td>輸入資產的標題。</td>
     </tr>
     <tr>
      <td>路徑</td>
      <td>資產在「資產」檢視中可用的資料夾路徑。</td>
     </tr>
     <tr>
      <td>MIME 類型</td>
      <td>資產的 MIME 類型。</td>
     </tr>
     <tr>
      <td>大小</td>
      <td>資產位元組的大小。</td>
     </tr>
     <tr>
      <td>下載者</td>
      <td>下載資產的使用者的電子郵件ID。</td>
     </tr>
     <tr>
      <td>下載日期</td>
      <td>執行資產下載操作的日期。</td>
     </tr>
     <tr>
      <td>作者</td>
      <td>資產的作者。</td>
     </tr>
     <tr>
      <td>建立日期</td>
      <td>資產上傳至「資產」檢視的日期。</td>
     </tr>
     <tr>
      <td>修改日期</td>
      <td>上次修改資產的日期。</td>
     </tr>
     <tr>
      <td>過期</td>
      <td>資產的到期狀態。</td>
     </tr>
     <tr>
      <td>按使用者名稱下載</td>
      <td>下載資產的使用者的名稱。</td>
     </tr>           
    </tbody>
   </table>

## 建立上傳報告 {#create-upload-report}

若要建立上傳報告：

1. 瀏覽到 **[!UICONTROL 設定]** > **[!UICONTROL 報告]** 按一下 **[!UICONTROL 建立報告]**。

1. 在[!UICONTROL 配置]頁籤，將報表類型指定為&#x200B;**[!UICONTROL 上傳]**。

1. 指定報告的標題和說明 (選用)。

1. 使用 **[!UICONTROL 選擇資料夾路徑]** 的子選單。

1. 選擇報告的日期間隔。

1. 在 [!UICONTROL 列] 頁籤，選擇需要在報告中顯示的列名。

1. 按一下&#x200B;**[!UICONTROL 建立]**。

   ![上傳報告](assets/upload-reports-config.png)

下表說明了可添加到報告的所有列的使用：

<table>
    <tbody>
     <tr>
      <th><strong>資料行名稱</strong></th>
      <th><strong>說明</strong></th>
     </tr>
     <tr>
      <td>標題</td>
      <td>輸入資產的標題。</td>
     </tr>
     <tr>
      <td>路徑</td>
      <td>資產在「資產」檢視中可用的資料夾路徑。</td>
     </tr>
     <tr>
      <td>MIME 類型</td>
      <td>資產的 MIME 類型。</td>
     </tr>
     <tr>
      <td>大小</td>
      <td>資產的大小。</td>
     </tr>
     <tr>
      <td>作者</td>
      <td>資產的作者。</td>
     </tr>
     <tr>
      <td>建立日期</td>
      <td>資產上傳至「資產」檢視的日期。</td>
     </tr>
     <tr>
      <td>修改日期</td>
      <td>上次修改資產的日期。</td>
     </tr>
     <tr>
      <td>過期</td>
      <td>資產的到期狀態。</td>
     </tr>              
    </tbody>
   </table>

## 查看現有報告 {#view-report-list}

[建立報告](#create-download-report)之後，您可以查看現有報告的清單並選擇以 CSV 格式下載或刪除它們。

要查看報告清單，請瀏覽至 **[!UICONTROL 設定]** > **[!UICONTROL 報告]**。

對於每個報告，您都可以查看報告標題、報告類型、建立報告時指定的說明、報告狀態、建立報告的作者的電子郵件識別碼以及報告建立日期。

`Completed ` 報告的狀態表示報告已準備好下載。

![報告清單](assets/list-of-reports.png)


## 下載 CSV 報告 {#download-csv-report}

要以 CSV 格式下載的報告：

1. 瀏覽到 **[!UICONTROL 設定]** > **[!UICONTROL 報告]**。

1. 選擇報告並按一下 **[!UICONTROL 下載 CSV]**。

所選報告以 CSV 格式下載。CSV 報告中顯示的列取決於您在選擇[建立報告](#create-download-report)時選擇的資料行。

## 刪除報告 {#delete-report}

若要刪除報告：

1. 瀏覽到 **[!UICONTROL 設定]** > **[!UICONTROL 報告]**。

1. 選擇報告並按一下 **[!UICONTROL 刪除]**。

1. 再按一次「**[!UICONTROL 刪除]**」以進行確認。
