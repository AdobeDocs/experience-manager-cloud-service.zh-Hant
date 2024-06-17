---
title: 使用與共用報表
description: 有關您在中之資產的報表 [!DNL Adobe Experience Manager Assets] 可協助您瞭解數位資產的使用、活動和共用。
contentOwner: AG
feature: Asset Reports, Asset Management
role: Admin, User
exl-id: ef617b01-0019-4379-8d58-c03215d7e28f
source-git-commit: ab2cf8007546f538ce54ff3e0b92bb0ef399c758
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 9%

---

# 資產報表 {#asset-reports}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/asset-reports.html?lang=en) |
| AEM as a Cloud Service  | 本文章 |

資產報告可讓您評估 [!DNL Adobe Experience Manager Assets] 部署。 替換為 [!DNL Assets]，您可為數位資產產生各種報表。 這些報表提供關於您系統使用情況、使用者如何與資產互動以及哪些資產的有用資訊 <!-- downloaded and --> 共用。

使用報告中的資訊取得關鍵成功度量，以測量採用程度 [!DNL Assets] 企業內部和客戶。

此 [!DNL Assets] 報告框架使用 [!DNL Sling] 非同步處理報表請求的作業。 其可擴展至大型存放庫。 非同步報表處理可提高報表產生的效率和速度。

報表管理介面是直覺式的，並包含存取已封存報表和檢視報表執行狀態（成功、失敗和已排入佇列）的細微選項和控制項。

產生報表時，系統會透過以下方式通知您 <!-- through an email (optional) and --> 收件匣通知。 您可以從報告清單頁面檢視、下載或刪除報告，該頁面會顯示所有先前產生的報告。

## 產生報表 {#generate-reports}

[!DNL Experience Manager Assets] 會為您產生下列標準報表：

* 上傳
* 下載
* 過期
* 修改
* 發佈
* [!DNL Brand Portal] 發佈
* 磁碟使用情況
* 檔案
* 連結共用

<!-- Removed download report.
* Upload
* Download
* Expiration
* Modification
* Publish
* [!DNL Brand Portal] publish
* Disk Usage
* Files
* Link Share
-->

[!DNL Adobe Experience Manager] 管理員可輕鬆地產生和自訂這些報表，以供您實作。 管理員可以依照下列步驟產生報表：

1. 在 [!DNL Experience Manager] 介面，按一下 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 報表]**.

   ![用於導覽資產報表的「工具」頁面](assets/navigation.png)

1. 在 [!UICONTROL 資產報表] 頁面，按一下 **[!UICONTROL 建立]** 工具列中的。
1. 從 **[!UICONTROL 建立報告]** 頁面上，選擇要建立的報表，然後按一下 **[!UICONTROL 下一個]**.

   ![選取報表型別](assets/choose_report.png)

1. 設定標題、說明、縮圖和資料夾路徑等報表詳細資訊。 依預設，資料夾路徑為 `/content/dam`. 您可以指定不同的路徑，以在特定資料夾上執行報表。

   ![新增報告詳細資料的頁面](assets/report_configuration.png)

   選擇報表的日期範圍。 您可以選擇現在產生報表，或在未來的日期和時間產生報表。

   >[!NOTE]
   >
   >如果您選擇稍後排程報表，請務必在「日期」和「時間」欄位中指定日期和時間。 如果您未指定任何值，報表引擎會將其視為要立即產生的報表。

   設定欄位可能會因您建立的報告型別而異。 例如， **[!UICONTROL 磁碟使用量]** 報表提供計算資產使用的磁碟空間時，包含資產轉譯的選項。 您可以選擇在子資料夾中包含或排除資產以計算磁碟使用量。

   >[!NOTE]
   >
   >「磁 **[!UICONTROL 碟使用情況]** 」報表不包含日期範圍欄位，因為它僅表示目前的磁碟空間使用情況。

   ![「磁碟使用情況」報告的「詳細資訊」頁面](assets/disk_usage_configuration.png)

   當您建立 **[!UICONTROL 檔案]** 報告，您可以包含/排除子資料夾。 不過，您無法包含此報表的資產轉譯。

   ![檔案報告的詳細資訊頁面](assets/files_report.png)

   此 **[!UICONTROL 連結共用]** 報表會顯示資產的URL，這些資產是從中與外部使用者共用的 [!DNL Assets]. <!-- It includes email ids of the user who shared the assets, emails ids of users with which the assets are shared, share date, and expiration date for the link. --> 欄無法自訂。

   此 **[!UICONTROL 連結共用]** 不包含子資料夾和轉譯的選項，因為它只會發佈顯示在下的共用URL `/var/dam/share`.

   ![連結共用報告的詳細資訊頁面](assets/link_share.png)

1. 按一下 **[!UICONTROL 下一個]** 工具列中的。

1. 在 **[!UICONTROL 設定欄]** 頁面中，某些欄會依預設選取顯示在報表中。 您可以選取更多欄。 取消選取欄以在報告中將其排除。

   ![選取或取消選取報表欄](assets/configure_columns.png)

   若要顯示自訂欄名稱或屬性路徑，請在 `jcr:content` CRX中的節點。 或者，透過屬性路徑選擇器新增路徑。

   ![選取或取消選取報表欄](assets/custom_columns.png)

1. 按一下 **[!UICONTROL 建立]** 工具列中的。 訊息會通知已啟動報表產生作業。
1. 在 [!UICONTROL 資產報表] 頁面時，報表產生狀態會根據報表工作的目前狀態，例如 [!UICONTROL 成功]， [!UICONTROL 已失敗]， [!UICONTROL 已排入佇列]，或 [!UICONTROL 已排程]. 相同的狀態會顯示在通知收件匣中。若要檢視報告頁面，請按一下報告連結。 或者，選取報告，然後按一下 **[!UICONTROL 檢視]** 工具列中的。

   <!--![A generated report](assets/report_page.png)-->
   ![產生的報告狀態](assets/report-status.JPG)

   按一下 **[!UICONTROL 下載]** 從工具列下載CSV格式的報表。

   >[!NOTE]
   >
   >您可以根據過去360天內產生的事件產生報表。 Experience Manager會將使用者ID資料保留30天。

## 新增自訂欄至報表 {#add-custom-columns}

您可以將自訂欄新增到以下報表，以顯示更多符合自訂需求的資料：

<!-- Remove download report.
* Upload
* Download
* Expiration
* Modification
* Publish
* [!DNL Brand Portal] publish
* Files
-->

* 上傳
* 過期
* 修改
* 發佈
* [!DNL Brand Portal] 發佈
* 檔案

若要新增自訂欄到這些報表，請執行下列步驟：

1. 在 [!DNL Manager interface]，按一下 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 報表]**.
1. 在 [!UICONTROL 資產報表] 頁面，按一下 **[!UICONTROL 建立]** 工具列中的。

1. 從 **[!UICONTROL 建立報告]** 頁面上，選擇要建立的報表。 按一下「**[!UICONTROL 下一步]**」。

1. 視適用情況設定報表詳細資訊，例如，標題、說明、縮圖、資料夾路徑和日期範圍。 按一下「**[!UICONTROL 下一步]**」。

1. 從清單中選取適用的資訊 **[!UICONTROL 預設欄]**. 若要顯示自訂欄，請指定下方的欄名稱 **[!UICONTROL 自訂欄]**.

   ![指定報表自訂欄的名稱](assets/custom_columns-1.png)

1. 將屬性路徑新增至 `jcr:content` CRXDE中的節點（使用屬性路徑選擇器）。 或者，在屬性路徑欄位中輸入路徑。

   ![從jcr：content中的路徑對應屬性路徑](assets/property_picker.png)

   若要新增更多自訂欄，請按一下 **[!UICONTROL 新增]** 並重複上述步驟。

1. 按一下 **[!UICONTROL 建立]** 工具列中的。 訊息會通知您報表產生作業已啟動。

<!-- TBD: How to configure purge now? Is it using OSGi configurations?

## Configure purging service {#configure-purging-service}

To remove reports that you no longer require, configure the DAM Report Purge service from the web console to purge existing reports based on their quantity and age.

1. Access the web console (configuration manager) from `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL DAM Report Purge Service]** configuration.
1. Specify the frequency (time interval) for the purging service in the `scheduler.expression.name` field. You can also configure the age and the quantity threshold for reports.
1. Save the changes.
-->

## 疑難排解資訊 {#tips-troubleshoot}

* 如果 [!UICONTROL 磁碟使用情況報表] 不會產生，而且如果您使用 [!DNL Dynamic Media]，確認所有資產皆已正確處理。 若要解決，請重新處理資產並再次產生報表。

<!-- These notes were present in generate report section above. Removing commented text from in between the instructions to preserve the numbering of the ordered list.

TBD: How do enable this in CS now? Is it done using some OSGi config now?
   >[!NOTE]
   >
   >Before you can generate an **[!UICONTROL Asset Downloaded]** report, ensure that the Asset Download service is enabled. From the web console (`https://[aem_server]:[port]/system/console/configMgr`), open the **[!UICONTROL Day CQ DAM Event Recorder]** configuration, and select the **[!UICONTROL Asset Downloaded (DOWNLOADED)]** option in Event Types if not already selected.
-->

<!-- Removed download report.
   >[!NOTE]
   >
   >By default, the Content Fragments and link shares are included in the asset [!UICONTROL Download] report. Select the appropriate option to create a report of link shares or to exclude Content Fragments from the download report.

   >[!NOTE]
   >
   >The [!UICONTROL Download] report displays details of only those assets which are downloaded after selecting individually or are downloaded using Quick Action. However, it does not include the details of the assets that are inside a downloaded folder.
-->

**另請參閱**

* [翻譯資產](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [資產支援的檔案格式](file-format-support.md)
* [搜尋資產](search-assets.md)
* [連接的資產](use-assets-across-connected-assets-instances.md)
* [中繼資料結構描述](metadata-schemas.md)
* [下載資產](download-assets-from-aem.md)
* [管理中繼資料](manage-metadata.md)
* [搜尋 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [大量中繼資料匯入](metadata-import-export.md)
* [發佈資產至 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
