---
title: Assets Insights
description: 追蹤在協力廠商網站、行銷活動和Adobe創意解決方案中使用的影像的使用者評等和使用統計資料。
contentOwner: AG
feature: Asset Insights,Asset Reports
role: User,Leader
exl-id: e268453b-e7c0-4aa4-bd29-2686edb5f99a
source-git-commit: 0df4d40cb37ced97dcffaf20adc2132eaadae524
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 7%

---

# Assets Insights {#asset-insights}

「資產前瞻分析」功能可讓您追蹤使用者評等，以及第三方網站、行銷活動和Adobe創意解決方案所使用影像的使用統計資料。 有助於深入分析影像的效能和受歡迎程度。

Assets Insights會擷取使用者活動詳細資料，例如影像的分級、點按和曝光次數（影像在網站上載入的次數）。 它會根據這些統計資料來指派分數給影像。 您可以使用分數和效能統計資料來選取要納入目錄、行銷活動等的熱門影像。 您甚至可以根據這些統計資料制定存檔和許可證更新策略。

若要讓「資產分析」擷取網站影像的使用量統計資料，您必須在網站程式碼中包含影像的內嵌程式碼。

若要讓「資產分析」顯示資產的使用統計資料，請先設定功能以從中擷取報表資料 [!DNL Adobe Analytics]. 如需詳細資訊，請參閱 [設定Assets Insights](#configure-asset-insights). 若要使用此功能，請購買 [!DNL Adobe Analytics] 單獨授權。

>[!NOTE]
>
>深入分析受支援，僅針對影像提供。

## 查看影像的統計資訊 {#viewing-statistics-for-an-image}

您可以從中繼資料頁面檢視「資產前瞻分析」分數。

1. 從「資產」使用者介面中，選取影像，然後按一下 **[!UICONTROL 屬性]** 的上界。
1. 在「屬性」頁面中，按一下 **[!UICONTROL 前瞻分析]**.
1. 檢閱 **[!UICONTROL 前瞻分析]** 標籤。 此 **[!UICONTROL 分數]** 一節說明資產的資產使用總量和效能分數。

   使用分數說明資產在各種解決方案中的使用次數。

   此 **[!UICONTROL 曝光數]** score是網站上載入資產的次數。 顯示在 **[!UICONTROL 點按次數]** 是資產的點按次數。

1. 檢閱 **[!UICONTROL 使用情況統計資料]** 區段來了解資產所屬的實體，以及最近使用哪些創意解決方案。 使用率越高，資產在使用者中受歡迎的機率就越大。 使用資料顯示在以下標題下：

   * **[!UICONTROL 資產]**:資產屬於集合或複合資產的次數。
   * **[!UICONTROL 網頁與行動]**:資產加入網站和應用程式的次數。
   * **[!UICONTROL 社交]**:資產用於其他解決方案(例如 [!DNL Adobe Campaign].
   * **[!UICONTROL 電子郵件]**:資產用於電子郵件促銷活動的次數。

   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >因為「資產分析」功能通常會從 [!DNL Adobe Analytics] 「解決方案」區段可能不會定期顯示最新資料。 顯示資料的時段取決於Assets Insights執行擷取Analytics資料的擷取作業排程。

1. 要以圖形方式查看某個時段內資產的效能統計資訊，請在「效能統計資訊」部分中 **[!UICONTROL 選擇該時段]** 。詳細資訊 (包括點按次數和印象) 會顯示為圖形的趨勢線。

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >與「解決方案」區段中的資料不同，「效能統計資料」區段會顯示最新的資料。

1. 若要取得您納入網站之資產的內嵌程式碼，以取得效能資料，請按一下 **[!UICONTROL 取得內嵌程式碼]** 在資產縮圖下方。 <!-- For more information on how to include your Embed code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

   ![chlimage_1-98](assets/chlimage_1-98.png)

## 查看映像的聚合統計資訊 {#viewing-aggregate-statistics-for-images}

您可以使用前瞻分析檢視同時檢視資料夾內所有資產 **[!UICONTROL 的分數]**。

1. 在「資產」使用者介面中，導覽至包含您要檢視深入分析之資產的資料夾。
1. 按一下 **[!UICONTROL 版面]** 選項，然後選擇 **[!UICONTROL 前瞻分析檢視]**.
1. 頁面會顯示資產的使用分數。 比較各種資產的評等並得出深入分析。

<!-- TBD: Commenting as Web Console is not available. Document the appropriate OSGi config method if available in CS.

## Schedule background job {#scheduling-background-job}

Assets Insights fetches usage data for assets from Adobe Analytics report suites in a periodic manner. By default, Assets Insights runs a background job every 24 hours at 2 AM to the fetch data. However, you can modify both the frequency and the time by configuring the **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service from the web console.

1. Click the [!DNL Experience Manager] logo, and go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Open the **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service configuration.

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. Specify the desired scheduler frequency and the start time for the job in the property scheduler expression. Save the changes.
-->

## 設定Assets Insights {#configure-asset-insights}

[!DNL Experience Manager Assets] 從擷取協力廠商網站所使用數位資產的使用資料 [!DNL Adobe Analytics]. 若要讓Assets Insights擷取此資料並產生深入分析，請先設定功能以與 [!DNL Adobe Analytics].

>[!NOTE]
>
>僅支援並提供影像見解。

1. 在 [!DNL Experience Manager]，按一下 **[!UICONTROL 工具]** > **[!UICONTROL 資產]**.

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. 按一下「 **[!UICONTROL 前瞻分析設定]** 」資訊卡。

1. 如需Analytics網站服務存取資訊，請前往 **[!UICONTROL Analytics]** > **[!UICONTROL 管理]** > **[!UICONTROL 管理工具]** > **[!UICONTROL 公司設定]** > **[!UICONTROL 網站服務]** 並複製 **[!UICONTROL 共用機密]** 鍵。

   在精靈中，選取 **[!UICONTROL 資料中心]**，並提供 **[!UICONTROL 公司]**，網站服務 **[!UICONTROL 使用者名稱]**，並貼上 **[!UICONTROL 共用機密]** 鍵。

   按一下 **[!UICONTROL 驗證]**.

   ![在中設定Adobe Analytics for Assets Insights [!DNL Experience Manager]](assets/analytics-insight-config.png)

   *圖：在中設定Adobe Analytics for Assets Insights[!DNL Experience Manager]*

1. 成功驗證時，下拉式清單中會列出報表套裝。 選取Adobe Analytics **[!UICONTROL 報表套裝]** 您希望Assets Insights擷取資料的位置。 按一下&#x200B;**[!UICONTROL 「新增」]**。

1. 之後 [!DNL Experience Manager] 設定您的報表套裝，按一下 **[!UICONTROL 完成]**.

如需詳細資訊，請參閱 [Adobe Analytics網站服務](https://experienceleague.adobe.com/docs/analytics/admin/company-settings/web-services-admin.html#api-access-information).

### 頁面追蹤器 {#page-tracker}

設定Adobe Analytics帳戶後，系統會為您產生頁面追蹤器程式碼。 啟用Assets Insights以追蹤 [!DNL Experience Manager] 協力廠商網站中使用的資產，請在網站程式碼中加入頁面追蹤器程式碼。 使用資產中的頁面追蹤器公用程式來產生頁面追蹤器程式碼。 <!--  For more information on how to include your Page Tracker code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

1. 在 [!DNL Experience Manager]，按一下 **[!UICONTROL 工具]** > **[!UICONTROL 資產]**.

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. 在導覽頁 **[!UICONTROL 面中]** ，按一下 **** 前瞻分析頁面追蹤器卡片。
1. 按一下 **[!UICONTROL 下載]** 下載頁面追蹤器程式碼。

<!--
Add page tracker code, CQDOC-18045, 30/07/2021
-->
下列范常式式碼片段顯示範例網頁中包含的頁面追蹤器程式碼：

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
