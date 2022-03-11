---
title: 有關使用和共用的報告
description: 有關中的資產的報告 [!DNL Adobe Experience Manager Assets] 幫助您瞭解數字資產的使用、活動和共用。
contentOwner: AG
feature: Asset Reports,Asset Management
role: Admin,User
exl-id: ef617b01-0019-4379-8d58-c03215d7e28f
source-git-commit: a2c2a1f4ef4a8f0cf1afbba001d24782a6a2a24e
workflow-type: tm+mt
source-wordcount: '868'
ht-degree: 5%

---

# 資產報表 {#asset-reports}

資產報告允許您評估 [!DNL Adobe Experience Manager Assets] 部署。 與 [!DNL Assets]，您可以為數字資產生成各種報告。 這些報告提供有關係統使用情況、用戶如何與資產交互以及哪些資產的有用資訊 <!-- downloaded and --> 共用。

使用報告中的資訊來獲取關鍵成功度量，以衡量採用 [!DNL Assets] 企業內部和客戶之間。

的 [!DNL Assets] 報告框架使用 [!DNL Sling] 作業以按順序非同步處理報表請求。 它可用於大型儲存庫。 非同步報告處理提高了報告生成的效率和速度。

報表管理介面是直觀的，包括用於訪問已存檔的報表和查看報表運行狀態（成功、失敗和排隊）的細粒度選項和控制。

生成報告時，您將通過 <!-- through an email (optional) and --> 收件箱通知。 您可以從報告清單頁查看、下載或刪除報告，其中顯示所有先前生成的報告。

## 生成報告 {#generate-reports}

[!DNL Experience Manager Assets] 為您生成以下標準報表：

* 上傳
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

[!DNL Adobe Experience Manager] 管理員可以輕鬆生成和自定義這些報告以用於您的實施。 管理員可以按照以下步驟生成報告：

1. 在 [!DNL Experience Manager] 介面，按一下 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 報告]**。

   ![「工具」頁，用於定位資產報表](assets/navigation.png)

1. 在 [!UICONTROL 資產報表] 的 **[!UICONTROL 建立]** 的子菜單。
1. 從 **[!UICONTROL 建立報告]** 的子菜單。 **[!UICONTROL 下一個]**。

   ![選擇報告類型](assets/choose_report.png)

1. 在儲存報告的CRX儲存庫中配置報告詳細資訊，如標題、說明、縮略圖和資料夾路徑。 預設情況下，資料夾路徑為 `/content/dam`。 可以指定其他路徑。

   ![要添加報告詳細資訊的頁](assets/report_configuration.png)

   選擇報表的日期範圍。 您可以選擇立即或在將來的日期和時間生成報表。

   >[!NOTE]
   >
   >如果您選擇稍後計畫報表，請確保在「日期和時間」欄位中指定日期和時間。 如果未指定任何值，則報告引擎會將其視為要立即生成的報告。

   配置欄位可能因您建立的報告類型而異。 例如， **[!UICONTROL 磁碟使用情況]** report提供了在計算資產使用的磁碟空間時包括資產格式副本的選項。 您可以選擇在子資料夾中包括或排除資產以計算磁碟使用率。

   >[!NOTE]
   >
   >「磁 **[!UICONTROL 碟使用情況]** 」報表不包含日期範圍欄位，因為它僅表示目前的磁碟空間使用情況。

   ![「 Disk Usage 」報告的「 Details 」頁](assets/disk_usage_configuration.png)

   建立 **[!UICONTROL 檔案]** 報表中，您可以包括/排除子資料夾。 但是，您不能為此報表包括資產格式副本。

   ![「Files」報告的詳細資訊頁面](assets/files_report.png)

   的 **[!UICONTROL 連結共用]** 報表顯示與外部用戶共用的資產的URL，這些資產來自 [!DNL Assets]。 <!-- It includes email ids of the user who shared the assets, emails ids of users with which the assets are shared, share date, and expiration date for the link. -->欄無法自訂。

   的 **[!UICONTROL 連結共用]** 不包括子資料夾和格式副本的選項，因為它只發佈顯示在 `/var/dam/share`。

   ![「連結共用」報告的詳細資訊頁面](assets/link_share.png)

1. 按一下 **[!UICONTROL 下一個]** 的子菜單。

1. 在 **[!UICONTROL 配置列]** 的子菜單。 可以選擇更多列。 取消選擇列以將其排除在報表中。

   ![選擇或取消選擇報表列](assets/configure_columns.png)

   要顯示自定義列名或屬性路徑，請在 `jcr:content` 的子目錄。 或者，通過屬性路徑選取器添加它。

   ![選擇或取消選擇報表列](assets/custom_columns.png)

1. 按一下 **[!UICONTROL 建立]** 的子菜單。 消息通知已啟動報告生成。
1. 在 [!UICONTROL 資產報表] 頁，報表生成狀態基於報表作業的當前狀態，例如 [!UICONTROL 成功]。 [!UICONTROL 失敗]。 [!UICONTROL 已排隊]或 [!UICONTROL 計畫]。 通知收件箱中顯示相同的狀態。要查看報告頁，請按一下報告連結。 或者，選擇報告，然後按一下 **[!UICONTROL 視圖]** 的子菜單。

   ![生成的報告](assets/report_page.png)

   按一下 **[!UICONTROL 下載]** 的子菜單。

## 將自定義列添加到報表 {#add-custom-columns}

您可以向以下報表添加自定義列，以根據自定義要求顯示更多資料：

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

要向這些報表添加自定義列，請執行以下步驟：

1. 在 [!DNL Manager interface]按一下 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 報告]**。
1. 在 [!UICONTROL 資產報表] 的 **[!UICONTROL 建立]** 的子菜單。

1. 從 **[!UICONTROL 建立報告]** 的子菜單。 按一下&#x200B;**[!UICONTROL 下一步]**。

1. 根據需要配置報告詳細資訊，如標題、說明、縮略圖、資料夾路徑和日期範圍。 按一下&#x200B;**[!UICONTROL 下一步]**。

1. 從清單中選擇適用資訊 **[!UICONTROL 預設列]**。 要顯示自定義列，請在 **[!UICONTROL 自定義列]**。

   ![指定報表的自定義列的名稱](assets/custom_columns-1.png)

1. 在 `jcr:content` 使用屬性路徑選取器的節點。 或者，在屬性路徑欄位中鍵入路徑。

   ![從jcr:content中的路徑映射屬性路徑](assets/property_picker.png)

   要添加更多自定義列，請按一下 **[!UICONTROL 添加]** 重複上述步驟。

1. 按一下 **[!UICONTROL 建立]** 的子菜單。 消息通知報表生成已啟動。

<!-- TBD: How to configure purge now? Is it using OSGi configurations?

## Configure purging service {#configure-purging-service}

To remove reports that you no longer require, configure the DAM Report Purge service from the web console to purge existing reports based on their quantity and age.

1. Access the web console (configuration manager) from `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL DAM Report Purge Service]** configuration.
1. Specify the frequency (time interval) for the purging service in the `scheduler.expression.name` field. You can also configure the age and the quantity threshold for reports.
1. Save the changes.
-->

## 故障排除資訊 {#tips-troubleshoot}

* 如果 [!UICONTROL 磁碟使用情況報告] 未生成，如果您正在使用 [!DNL Dynamic Media]，確保所有資產都正確運行。 要解決問題，請重新處理資產並再次生成報告。

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
