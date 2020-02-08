---
title: 資產分析
description: 瞭解「資產前瞻分析」功能如何讓您追蹤第三方網站、行銷宣傳和Adobe創意解決方案所使用影像的使用者評分和使用統計資料。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# 資產分析{#asset-insights}

<!-- TBD: Add uicontrol tags  -->

「資產前瞻分析」功能可讓您追蹤使用者評分和使用統計資料，這些資料用於協力廠商網站、行銷活動和Adobe的創意解決方案。 它有助於獲得有關其效能與人氣的見解。

Assets Insights會擷取使用者活動詳細資訊，例如影像被評等、點按和曝光（影像在網站上載入的次數）。 它會根據這些統計資料來指派分數給影像。 您可以使用分數和績效統計資料來選取要納入目錄、行銷活動等的熱門影像。 您甚至可以根據這些統計資料來制定封存和授權續約政策。

若是「資產前瞻分析」，以從網站擷取影像的使用統計資料，您必須將影像的內嵌代碼加入網站代碼中。

若要讓「資產前瞻分析」顯示資產的使用統計資料，請先設定功能，從Adobe Analytics擷取報告資料。 如需詳細資訊，請參 [閱設定資產分析](#configure-asset-insights)。

>[!NOTE]
>
>只有影像才支援並提供見解。

## 檢視影像的統計資料 {#viewing-statistics-for-an-image}

您可以從中繼資料頁面檢視「資產前瞻分析」分數。

1. 從「資產」使用者介面(UI)中，選取影像，然後從工具列點選「 **[!UICONTROL 屬性]** 」。
1. 從「屬性」頁面，點選「 **[!UICONTROL 前瞻分析」]**。
1. 在「前瞻分析」索引標籤中檢閱資產的使 **[!UICONTROL 用詳細]** 資訊。 「分 **[!UICONTROL 數]** 」區段說明資產的資產使用和績效分數總計。

   使用分數說明資產在各種解決方案中的使用次數。

   「 **[!UICONTROL 印象]** 」分數是資產在網站上載入的次數。 「點按次數」 **[!UICONTROL 下方]** ，顯示的數字是資產被點按的次數。

1. 檢閱「使 **[!UICONTROL 用統計資料]** 」區段，瞭解資產所屬的實體以及最近使用該資產的創意解決方案。 使用率越高，資產在使用者中受歡迎的機率就越高。 使用資料會顯示在下列標題下：

   * **資產**:資產屬於系列或複合資產的次數
   * **網頁與行動裝置**:資產加入網站和應用程式的次數
   * **Social**:資產在解決方案（例如Adobe Social和Adobe Campaign）中使用的次數
   * **電子郵件**:資產用於電子郵件促銷活動的次數
   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >由於「資產前瞻分析」功能通常會定期從Adobe Analytics擷取「解決方案」資料，因此「解決方案」區段可能不會顯示最新資料。 顯示資料的時段取決於「資產分析」執行以擷取Analytics資料的擷取作業排程。

1. 要以圖形方式查看某個時段內資產的效能統計資訊，請在「效能統計資訊」部分中 **[!UICONTROL 選擇該時段]** 。 詳細資訊（包括點按次數和印象）會顯示為圖形的趨勢線。

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >與「解決方案」區段中的資料不同，「效能統計資料」區段會顯示最新的資料。

1. 若要取得您包含在網站中之資產的內嵌代碼以取得效能資料，請點選／按一下資產縮圖 **[!UICONTROL 下方的「取得內嵌代碼]** 」。 <!-- For more information on how to include your Embed code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

   ![chlimage_1-98](assets/chlimage_1-98.png)

## 檢視影像的匯總統計資料 {#viewing-aggregate-statistics-for-images}

您可以使用前瞻分析檢視同時檢視資料夾內所有資產 **[!UICONTROL 的分數]**。

1. 在「資產」使用者介面中，導覽至包含您要檢視其見解之資產的檔案夾。
1. 點選／按一下工具列中的「版面」圖示，然後選擇「 **[!UICONTROL 前瞻分析檢視」]**。
1. 頁面會顯示資產的使用分數。 比較各種資產的評分並獲取見解。

## 排程背景工作 {#scheduling-background-job}

「資產前瞻分析」會定期從Adobe Analytics報表套裝擷取資產的使用資料。 根據預設，資產前瞻分析會每24小時在2 AM執行一次背景工作，以擷取資料。 不過，您可以透過Web主控台設定 **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** Service，來修改頻率和時間。

1. 點選AEM標誌，並前往「工 **[!UICONTROL 具]** > **[!UICONTROL 作業]** > **[!UICONTROL Web Console]**」。
1. 開啟 **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service組態。

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. 在屬性調度器表達式中指定所需的調度器頻率和作業的啟動時間。 儲存變更。

## 設定資產分析 {#configure-asset-insights}

Adobe Experience Manager(AEM)Assets會從Adobe Analytics擷取協力廠商網站所使用之AEM資產的使用資料。 若要讓「資產前瞻分析」擷取此資料並產生前瞻分析，請先設定功能以與Adobe Analytics整合。

>[!NOTE]
>
>只有影像才支援並提供見解。

1. 在AEM中，按一下「 **[!UICONTROL 工具]** > **[!UICONTROL 資產]**」。

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. 按一下「 **[!UICONTROL 前瞻分析設定]** 」資訊卡。
1. 在精靈中，選取資料中心並提供您的認證，包括您的組織名稱、使用者名稱和共用密碼。

   ![在AEM中設定Adobe Analytics的資產見解](assets/insights_config2.png)
   *圖：在AEM中設定Adobe Analytics的資產見解*

1. 按一下／點選「 **[!UICONTROL 驗證]**」。 在AEM驗證您的認證後，從「報表套裝」清單 **[!UICONTROL 中]** ，選擇Adobe Analytics報表套裝，讓您從中擷取資產分析。 按一下&#x200B;**[!UICONTROL 「新增」]**。
1. AEM設定您的報表套裝後，請點選「完 **[!UICONTROL 成]**」。

### 頁面追蹤器 {#page-tracker}

在您設定Adobe Analytics帳戶後，就會產生頁面追蹤器代碼。 若要啟用「資產前瞻分析」來追蹤協力廠商網站中使用的AEM資產，請在網站程式碼中加入頁面追蹤器程式碼。 使用AEM Assets中的「頁面追蹤器」公用程式來產生頁面追蹤器代碼。 <!--  For more information on how to include your Page Tracker code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

1. 在AEM中，按一下「 **[!UICONTROL 工具]** > **[!UICONTROL 資產]**」。

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. 在導覽頁 **[!UICONTROL 面中]** ，按一下 **** 前瞻分析頁面追蹤器卡片。
1. 按一 **[!UICONTROL 下「下載]** 」以下載頁面追蹤器代碼。

<!--

## Using demo package for Asset Insights {#using-demo-package-for-asset-insights}

Using the demo package, you can enable Adobe Asset Insights to capture data from and generate insights for a sample web page.

1. Configure Asset Insights using the instructions in [Configure Asset Insights](#configure-asset-insights).
1. Download the sample AEM Assets package from below and install the package from CRXDE package manager.

   [Get File](assets/insightsdemo.zip)

1. Download the ZIP file containing the sample web page from below and extract on your local file system.

   [Get File](assets/demosite.zip)

1. Click the web page to open it in the web browser.

   >[!CAUTION]
   >
   >Web Page is configured to load asset from the localhost server . In case your server is running somewhere else change server address from localhost to server address in the HTML content of the web page.

   >[!NOTE]
   >
   >The external web page can be in AEM itself.

-->
