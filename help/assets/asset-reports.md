---
title: 關於使用與共用的報告
description: ' [!DNL Adobe Experience Manager Assets] 中有關您資產的報表，可協助您瞭解數位資產的使用、活動和共用。'
contentOwner: AG
translation-type: tm+mt
source-git-commit: 6586dfeeef1732ae115eea433a665191773ed283
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 4%

---


# 資產報表{#asset-reports}

資產報表可讓您評估[!DNL Adobe Experience Manager Assets]部署的公用程式。 使用[!DNL Assets]，您可以產生各種數位資產的報表。 這些報表提供您系統使用情況、使用者與資產的互動方式，以及哪些資產被下載和共用的實用資訊。

使用報表中的資訊衍生關鍵成功度量，以測量企業內部及客戶對[!DNL Assets]的接受度。

[!DNL Assets]報告框架使用[!DNL Sling]作業以有序方式非同步處理報告請求。 它適用於大型儲存庫。 非同步報表處理可提高報表產生的效率和速度。

報表管理介面是直覺式的，包含存取已封存報表及檢視報表執行狀態（成功、失敗和佇列）的精細選項和控制項。

產生報告時，會透過<!-- through an email (optional) and -->收件匣通知您。 您可以從報表清單頁面檢視、下載或刪除報表，其中會顯示所有先前產生的報表。

## 產生報告{#generate-reports}

[!DNL Experience Manager Assets] 為您生成以下標準報表：

* 上傳
* 下載
* 過期
* 修改
* 發佈
* [!DNL Brand Portal] 發佈
* 磁碟使用情況
* 檔案
* 連結共用

[!DNL Adobe Experience Manager] 管理員可輕鬆產生和自訂這些報表，以供您的實作使用。管理員可依照下列步驟產生報表：

1. 在[!DNL Experience Manager]介面中，按一下「工具&#x200B;**** > **[!UICONTROL 資產]** > **[!UICONTROL 報表]**」。

   ![「工具」頁面，以導覽資產報表](assets/navigation.png)

1. 在[!UICONTROL 資產報表]頁面上，從工具列按一下&#x200B;**[!UICONTROL 建立]**。
1. 從&#x200B;**[!UICONTROL 建立報表]**&#x200B;頁面中，選擇您要建立的報表，然後按一下&#x200B;**[!UICONTROL 下一步]**。

   ![選擇報表類型](assets/choose_report.png)

<!-- TBD: How do enable this in CS now? Is it done using some OSGi config now?
   >[!NOTE]
   >
   >Before you can generate an **[!UICONTROL Asset Downloaded]** report, ensure that the Asset Download service is enabled. From the web console (`https://[aem_server]:[port]/system/console/configMgr`), open the **[!UICONTROL Day CQ DAM Event Recorder]** configuration, and select the **[!UICONTROL Asset Downloaded (DOWNLOADED)]** option in Event Types if not already selected.
-->

>[!NOTE]
>
>依預設，「內容片段」和連結分享會包含在資產[!UICONTROL Download]報表中。 選取適當的選項，以建立連結共用的報表，或從下載報表中排除內容片段。

>[!NOTE]
>
>[!UICONTROL Download]報表只會顯示在個別選取後下載或使用快速動作下載的資產詳細資訊。 但是，它不包含已下載資料夾中資產的詳細資料。

1. 在儲存報表的CRX儲存庫中設定報表詳細資訊，例如標題、說明、縮圖和資料夾路徑。 預設情況下，資料夾路徑為`/content/dam`。 您可以指定不同的路徑。

   ![新增報表詳細資訊的頁面](assets/report_configuration.png)

   選擇報表的日期範圍。 您可以選擇立即產生報表，或在未來的日期和時間產生報表。

   >[!NOTE]
   >
   >如果您選擇稍後排程報表，請確定您在「日期和時間」欄位中指定日期和時間。 如果您未指定任何值，報表引擎會將其視為要立即產生的報表。

   設定欄位可能會因您建立的報表類型而異。 例如，**[!UICONTROL 「磁碟使用狀況」報表提供選項，可在計算資產使用的磁碟空間時包含資產轉譯。]**&#x200B;您可以選擇在子資料夾中包含或排除資產，以便計算磁碟使用情況。

   >[!NOTE]
   >
   >「磁 **[!UICONTROL 碟使用情況]** 」報表不包含日期範圍欄位，因為它僅表示目前的磁碟空間使用情況。

   ![「 Disk Usage 」報告的詳細資訊頁](assets/disk_usage_configuration.png)

   建立&#x200B;**[!UICONTROL 檔案]**&#x200B;報告時，可以包含／排除子資料夾。 不過，您無法為此報表包含資產轉譯。

   ![「檔案」報表的詳細資訊頁面](assets/files_report.png)

   **[!UICONTROL 連結共用]**&#x200B;報表會顯示從[!DNL Assets]內與外部使用者共用之資產的URL。 <!-- It includes email ids of the user who shared the assets, emails ids of users with which the assets are shared, share date, and expiration date for the link. -->欄無法自訂。

   **[!UICONTROL 連結共用]**&#x200B;報表不包含子資料夾和轉譯的選項，因為它只會發佈顯示在`/var/dam/share`下方的共用URL。

   ![「連結共用」報表的詳細資訊頁面](assets/link_share.png)

1. 從工具列按一下「下一步」。****

1. 在&#x200B;**[!UICONTROL 設定欄]**&#x200B;頁面中，依預設會選取某些欄以顯示在報表中。 您可以選取更多欄。 取消選取選取的欄，將其排除在報表中。

   ![選取或取消選取報表欄](assets/configure_columns.png)

   要顯示自定義列名或屬性路徑，請在CRX的`jcr:content`節點下配置資產二進位檔案的屬性。 或者，透過屬性路徑選擇器加入。

   ![選取或取消選取報表欄](assets/custom_columns.png)

1. 從工具列按一下「建立」。 ****&#x200B;訊息會通知報表產生已開始。
1. 在[!UICONTROL 資產報表]頁面上，報表產生狀態是根據報表作業的目前狀態，例如[!UICONTROL Success]、[!UICONTROL Failed]、[!UICONTROL Queued]或[!UICONTROL Scheduled]。 通知收件箱中會顯示相同的狀態。要查看報告頁，請按一下報告連結。 或者，選擇報告，然後從工具欄中按一下&#x200B;**[!UICONTROL View]**。

   ![產生的報表](assets/report_page.png)

   按一下工具列中的&#x200B;**[!UICONTROL 下載]**，以下載CSV格式的報表。

## 新增自訂欄至報表{#add-custom-columns}

您可以新增自訂欄至下列報表，以顯示更多符合自訂需求的資料：

* 上傳
* 下載
* 過期
* 修改
* 發佈
* [!DNL Brand Portal] 發佈
* 檔案

若要新增自訂欄至這些報表，請依照下列步驟進行：

1. 在[!DNL Manager interface]中，按一下「工具&#x200B;**** > **[!UICONTROL 資產]** > **[!UICONTROL 報表]**」。
1. 在[!UICONTROL 資產報表]頁面上，從工具列按一下&#x200B;**[!UICONTROL 建立]**。

1. 從&#x200B;**[!UICONTROL 建立報表]**&#x200B;頁面，選擇要建立的報表。 按一下&#x200B;**[!UICONTROL 下一步]**。

1. 視需要設定報表詳細資訊，例如標題、說明、縮圖、資料夾路徑和日期範圍。 按一下&#x200B;**[!UICONTROL 下一步]**。

1. 從&#x200B;**[!UICONTROL 預設列]**&#x200B;清單中選擇適用資訊。 要顯示自定義列，請在&#x200B;**[!UICONTROL 自定義列]**&#x200B;下指定列的名稱。

   ![指定報表的自訂欄名稱](assets/custom_columns-1.png)

1. 使用屬性路徑選擇器在CRXDE的`jcr:content`節點下添加屬性路徑。 或者，在屬性路徑欄位中鍵入路徑。

   ![從jcr:content中的路徑映射屬性路徑](assets/property_picker.png)

   若要新增更多自訂欄，請按一下「新增&#x200B;****」，然後重複上述步驟。

1. 從工具列按一下「建立」。 ****&#x200B;訊息會通知報表產生已開始。

<!-- TBD: How to configure purge now? Is it using OSGi configurations?

## Configure purging service {#configure-purging-service}

To remove reports that you no longer require, configure the DAM Report Purge service from the web console to purge existing reports based on their quantity and age.

1. Access the web console (configuration manager) from `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL DAM Report Purge Service]** configuration.
1. Specify the frequency (time interval) for the purging service in the `scheduler.expression.name` field. You can also configure the age and the quantity threshold for reports.
1. Save the changes.
-->

## 疑難排解資訊與提示{#tips-troubleshoot}

* 如果[!UICONTROL 磁碟使用狀況報表]未產生，且您使用[!DNL Dynamic Media]，請確定所有資產都正確進行。 若要解決，請重新處理資產並重新產生報表。
