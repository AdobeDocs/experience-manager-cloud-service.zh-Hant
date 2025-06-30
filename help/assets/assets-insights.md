---
title: Assets Insights
description: 追蹤協力廠商網站、行銷活動和Adobe創意解決方案中所使用影像的使用者評級和使用統計資料。
contentOwner: AG
feature: Asset Insights, Asset Reports
role: User, Leader
exl-id: e268453b-e7c0-4aa4-bd29-2686edb5f99a
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 13%

---

# Assets Insights {#asset-insights}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/asset-insights.html?lang=en) |
| AEM as a Cloud Service  | 本文章 |

Assets Insights功能可讓您追蹤用於協力廠商網站、行銷活動及Adobe創意解決方案之影像的使用者評分和使用情況統計資料。 它有助於提供影像效能和人氣的相關深入分析。

Assets Insights會擷取使用者活動詳細資訊，例如影像分級、點按和曝光次數（影像載入網站上的次數）。 系統會根據這些統計資料，將分數指派給影像。 您可以使用評分和效能統計資料來選取常用影像，以包含在目錄、行銷活動等中。 您甚至可以根據這些統計資料制定封存和授權更新政策。

若要讓Assets Insights從網站擷取影像的使用狀況統計資料，您必須在網站程式碼中包含影像的內嵌程式碼。

若要讓Assets Insights顯示資產的使用狀況統計資料，請先設定此功能以從[!DNL Adobe Analytics]擷取報表資料。 如需詳細資訊，請參閱[設定Assets Insights](#configure-asset-insights)。 若要使用此功能，請另外購買[!DNL Adobe Analytics]授權。

>[!NOTE]
>
>僅支援並提供影像的深入分析。

## 檢視影像的統計資料 {#viewing-statistics-for-an-image}

您可以從中繼資料頁面檢視Assets Insights分數。

1. 從Assets使用者介面中，選取影像，然後從工具列按一下&#x200B;**[!UICONTROL 屬性]**。
1. 在[屬性]頁面中，按一下&#x200B;**[!UICONTROL Insights]**。
1. 檢閱&#x200B;**[!UICONTROL Insights]**&#x200B;索引標籤中資產的使用狀況詳細資料。 **[!UICONTROL 分數]**&#x200B;區段說明資產的資產使用總計和效能差距。

   使用分數說明資產在各種解決方案中的使用次數。

   **[!UICONTROL 曝光次數]**&#x200B;分數是資產載入網站上的次數。 在&#x200B;**[!UICONTROL 點按]**&#x200B;下顯示的數字是資產的點按次數。

1. 請檢閱&#x200B;**[!UICONTROL 使用統計資料]**&#x200B;區段，瞭解資產所屬的實體，以及最近使用它的創意解決方案。 使用量越高，資產在使用者中受歡迎的可能性就越大。 使用情況資料會顯示在下列標題下：

   * **[!UICONTROL 資產]**：資產屬於集合或複合資產的次數。
   * **[!UICONTROL 網頁與行動裝置]**：資產屬於網站與應用程式一部分的次數。
   * **[!UICONTROL 社交]**：其他解決方案（例如[!DNL Adobe Campaign]）使用資產的次數。
   * **[!UICONTROL 電子郵件]**：在電子郵件行銷活動中使用資產的次數。

   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >由於Assets Insights功能通常會定期從[!DNL Adobe Analytics]擷取解決方案資料，因此解決方案區段可能不會顯示最新的資料。 資料顯示的時間長度取決於Assets Insights為擷取Analytics資料而執行的擷取作業排程。

1. 要以圖形方式查看某個時段內資產的效能統計資訊，請在「效能統計資訊」部分中 **[!UICONTROL 選擇該時段]** 。詳細資訊 (包括點按次數和印象) 會顯示為圖形的趨勢線。

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >與「解決方案」段落中的資料不同，「效能統計資料」段落會顯示最新的資料。

1. 若要取得您包含在網站中之資產的內嵌程式碼，以取得效能資料，請按一下資產縮圖下方的&#x200B;**[!UICONTROL 取得內嵌程式碼]**。<!-- For more information on how to include your Embed code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

   ![chlimage_1-98](assets/chlimage_1-98.png)

## 檢視影像的彙總統計資料 {#viewing-aggregate-statistics-for-images}

您可以使用前瞻分析檢視同時檢視資料夾內所有資產 **[!UICONTROL 的分數]**。

1. 在Assets使用者介面中，導覽至包含您要檢視其見解的資產的資料夾。
1. 按一下工具列中的&#x200B;**[!UICONTROL 配置]**&#x200B;選項，然後選擇&#x200B;**[!UICONTROL 前瞻分析檢視]**。
1. 頁面會顯示資產的使用情況分數。 比較各種資產的評等並得出深入見解。

<!-- TBD: Commenting as Web Console is not available. Document the appropriate OSGi config method if available in CS.

## Schedule background job {#scheduling-background-job}

Assets Insights fetches usage data for assets from Adobe Analytics report suites in a periodic manner. By default, Assets Insights runs a background job every 24 hours at 2 AM to the fetch data. However, you can modify both the frequency and the time by configuring the **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service from the web console.

1. Click the [!DNL Experience Manager] logo, and go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Open the **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service configuration.

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. Specify the desired scheduler frequency and the start time for the job in the property scheduler expression. Save the changes.
-->

## 設定Assets深入分析 {#configure-asset-insights}

[!DNL Experience Manager Assets]會從[!DNL Adobe Analytics]擷取協力廠商網站使用之數位資產的使用資料。 若要啟用Assets Insights以擷取此資料並產生深入分析，請先設定此功能以與[!DNL Adobe Analytics]整合。

>[!NOTE]
>
>僅支援並為影像提供深入分析。

1. 在[!DNL Experience Manager]中，按一下&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]**。

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. 按一下「 **[!UICONTROL 前瞻分析設定]** 」資訊卡。

1. 如需Analytics Web服務存取資訊，請移至&#x200B;**[!UICONTROL Analytics]** > **[!UICONTROL 管理員]** > **[!UICONTROL 管理工具]** > **[!UICONTROL 公司設定]** > **[!UICONTROL Web服務]**，並複製&#x200B;**[!UICONTROL 共用機密]**&#x200B;金鑰。

   在精靈中，選取&#x200B;**[!UICONTROL 資料中心]**，並提供&#x200B;**[!UICONTROL 公司]**、網站服務&#x200B;**[!UICONTROL 使用者名稱]**&#x200B;的顯示名稱，然後貼上&#x200B;**[!UICONTROL 共用機密]**&#x200B;金鑰。

   按一下&#x200B;**[!UICONTROL 驗證]**。

   ![在[!DNL Experience Manager]](assets/analytics-insight-config.png)中設定Adobe Analytics以進行Assets深入分析

   *圖：在[!DNL Experience Manager]*&#x200B;中設定Adobe Analytics以進行Assets深入分析

1. 驗證成功後，您會在下拉式清單中取得報表套裝清單。 選取您要Assets Insights擷取資料的Adobe Analytics **[!UICONTROL 報表套裝]**。 按一下&#x200B;**[!UICONTROL 新增]**。

1. 在[!DNL Experience Manager]設定您的報表套裝後，按一下&#x200B;**[!UICONTROL 完成]**。

如需詳細資訊，請參閱[Adobe Analytics網站服務](https://experienceleague.adobe.com/docs/analytics/admin/company-settings/web-services-admin.html#api-access-information)。

### 頁面追蹤器 {#page-tracker}

設定Adobe Analytics帳戶後，系統就會為您產生頁面追蹤器程式碼。 若要啟用Assets Insights以追蹤第三方網站中使用的[!DNL Experience Manager]資產，請在網站程式碼中包含頁面追蹤器程式碼。 使用Assets中的頁面追蹤器公用程式來產生頁面追蹤器程式碼。<!--  For more information on how to include your Page Tracker code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

1. 在[!DNL Experience Manager]中，按一下&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]**。

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. 在導覽頁 **[!UICONTROL 面中]** ，按一下 **** 前瞻分析頁面追蹤器卡片。
1. 按一下&#x200B;**[!UICONTROL 下載]**&#x200B;以下載頁面追蹤程式碼。

<!--
Add page tracker code, CQDOC-18045, 30/07/2021
-->
下列範常式式碼片段顯示範例網頁中包含的頁面追蹤器程式碼：

```xml
 <head>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/sitecatalyst/appmeasurement.js"></script>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/foundation/assetinsights/pagetracker.js"></script>
            <script type="text/javascript">
                                assetAnalytics.attrTrackable = 'trackable';
                assetAnalytics.defaultTrackable = false;
                assetAnalytics.attrAssetID = 'aem-asset-id';
                assetAnalytics.assetImpressionPollInterval = 200; // interval in millis
                assetAnalytics.charsLimitForGET = 2000; // bytes
                assetAnalytics.dispatcher.init("assetstesting","abc.net","bee","list1","eVar3","event8","event7");
            </script>

 </head>
```



<!--

## Using demo package for Assets Insights {#using-demo-package-for-asset-insights}

Using the demo package, you can enable Adobe Assets Insights to capture data from and generate insights for a sample web page.

1. Configure Assets Insights using the instructions in [Configure Assets Insights](#configure-asset-insights).
1. Download the sample [!DNL Experience Manager Assets] package from below and install the package from CRXDE package manager.

   [Get File](assets/insightsdemo.zip)

1. Download the ZIP file containing the sample web page from below and extract on your local file system.

   [Get File](assets/demosite.zip)

1. Click the web page to open it in the web browser.

   >[!CAUTION]
   >
   >Web Page is configured to load asset from the localhost server . In case your server is running somewhere else change server address from localhost to server address in the HTML content of the web page.

   >[!NOTE]
   >
   >The external web page can be in [!DNL Experience Manager] itself.

-->

**另請參閱**

* [翻譯資產](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [資產支援的檔案格式](file-format-support.md)
* [搜尋資產](search-assets.md)
* [連接的資產](use-assets-across-connected-assets-instances.md)
* [資產報表](asset-reports.md)
* [中繼資料結構描述](metadata-schemas.md)
* [下載資產](download-assets-from-aem.md)
* [管理中繼資料](manage-metadata.md)
* [搜尋 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [大量中繼資料匯入](metadata-import-export.md)
* [發佈資產至 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
