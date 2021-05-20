---
title: 資產 Insights
description: 追蹤使用者評分和影像使用統計資料，這些資料用於協力廠商網站、行銷宣傳和Adobe的創意解決方案。
contentOwner: AG
feature: 資產分析，資產報表
role: Business Practitioner,Leader
exl-id: e268453b-e7c0-4aa4-bd29-2686edb5f99a
source-git-commit: 212e4e7cfb93d5765f80003c42ba6afb9af45c13
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 8%

---

# 資產 Insights {#asset-insights}

「資產前瞻分析」功能可讓您追蹤使用者評分，以及協力廠商網站、行銷宣傳和Adobe創意解決方案所使用影像的使用統計資料。 它可協助您深入瞭解影像的效能與人氣。

Assets Insights會擷取使用者活動詳細資訊，例如影像被評等、點按和曝光（影像在網站上載入的次數）。 它會根據這些統計資料來指派分數給影像。 您可以使用分數和績效統計資料來選取要納入目錄、行銷活動等的熱門影像。 您甚至可以根據這些統計資料來制定封存和授權續約政策。

若是「資產前瞻分析」，以從網站擷取影像的使用統計資料，您必須將影像的內嵌代碼加入網站代碼中。

若要讓「資產前瞻分析」顯示資產的使用統計資料，請先設定功能，從[!DNL Adobe Analytics]擷取報告資料。 如需詳細資訊，請參閱[設定資產前瞻分析](#configure-asset-insights)。 若要使用此功能，請個別購買[!DNL Adobe Analytics]授權。

>[!NOTE]
>
>我們僅支援影像的深入資訊。

## 檢視影像{#viewing-statistics-for-an-image}的統計資料

您可以從中繼資料頁面檢視「資產前瞻分析」分數。

1. 從「資產」使用者介面中，選取影像，然後從工具列按一下「屬性」**[!UICONTROL 。]**
1. 在「屬性」頁面中，按一下&#x200B;**[!UICONTROL Insights]**。
1. 在&#x200B;**[!UICONTROL Insights]**&#x200B;標籤中檢閱資產的使用詳細資訊。 **[!UICONTROL Score]**&#x200B;區段說明資產的資產使用總數和績效儲存。

   使用分數說明資產在各種解決方案中的使用次數。

   **[!UICONTROL 印象]**&#x200B;分數是資產在網站上載入的次數。 顯示在&#x200B;**[!UICONTROL Clicks]**&#x200B;下方的數字是資產被點按的次數。

1. 請檢閱&#x200B;**[!UICONTROL 使用統計資料]**&#x200B;一節，以瞭解資產屬於哪些實體以及最近使用該資產的創意解決方案。 使用率越高，資產在使用者中受歡迎的機率就越高。 使用資料會顯示在下列標題下：

   * **[!UICONTROL 資產]**:資產屬於系列或複合資產的次數。
   * **[!UICONTROL 網頁與行動裝置]**:資產加入網站和應用程式的次數。
   * **[!UICONTROL Social]**:資產用於其他解決方案（例如a）的次數 [!DNL Adobe Campaign]。
   * **[!UICONTROL 電子郵件]**:資產用於電子郵件促銷活動的次數。

   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >由於「資產前瞻分析」功能通常會定期從[!DNL Adobe Analytics]中擷取解決方案資料，因此「解決方案」區段可能不會顯示最新的資料。 顯示資料的時段取決於「資產分析」執行以擷取Analytics資料的擷取作業排程。

1. 要以圖形方式查看某個時段內資產的效能統計資訊，請在「效能統計資訊」部分中 **[!UICONTROL 選擇該時段]** 。詳細資訊 (包括點按次數和印象) 會顯示為圖形的趨勢線。

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >與「解決方案」區段中的資料不同，「效能統計資料」區段會顯示最新的資料。

1. 若要取得您包含在網站中的資產的內嵌代碼，以取得效能資料，請按一下資產縮圖下方的「取得內嵌代碼」。<!-- For more information on how to include your Embed code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->****

   ![chlimage_1-98](assets/chlimage_1-98.png)

## 檢視影像{#viewing-aggregate-statistics-for-images}的匯總統計資料

您可以使用前瞻分析檢視同時檢視資料夾內所有資產 **[!UICONTROL 的分數]**。

1. 在「資產」使用者介面中，導覽至包含您要檢視其見解之資產的檔案夾。
1. 按一下工具列中的「版面」選項，然後選擇&#x200B;**[!UICONTROL 前瞻分析檢視]**。
1. 頁面會顯示資產的使用分數。 比較各種資產的評分並獲取見解。

<!-- TBD: Commenting as Web Console is not available. Document the appropriate OSGi config method if available in CS.

## Schedule background job {#scheduling-background-job}

Asset Insights fetches usage data for assets from Adobe Analytics report suites in a periodic manner. By default, Asset Insights runs a background job every 24 hours at 2 AM to the fetch data. However, you can modify both the frequency and the time by configuring the **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service from the web console.

1. Click the [!DNL Experience Manager] logo, and go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Open the **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service configuration.

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. Specify the desired scheduler frequency and the start time for the job in the property scheduler expression. Save the changes.
-->

## 設定資產分析{#configure-asset-insights}

[!DNL Experience Manager Assets] 從中擷取協力廠商網站使用之數位資產的使用資料 [!DNL Adobe Analytics]。若要讓「資產前瞻分析」擷取此資料並產生前瞻分析，請先設定功能以與[!DNL Adobe Analytics]整合。

>[!NOTE]
>
>只有影像才支援並提供見解。

1. 在[!DNL Experience Manager]中，按一下&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 資產]**。

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. 按一下「 **[!UICONTROL 前瞻分析設定]** 」資訊卡。
1. 在精靈中，選取資料中心並提供您的認證，包括您的組織名稱、使用者名稱和共用密碼。

   ![設定Adobe Analytics的資產分析  [!DNL Experience Manager]](assets/insights_config2.png)

   *圖：設定Adobe Analytics的資產分析[!DNL Experience Manager]*

1. 按一下&#x200B;**[!UICONTROL Authenticate]**。 在[!DNL Experience Manager]驗證您的認證後，從&#x200B;**[!UICONTROL 報表套裝]**&#x200B;清單中，選擇您要從中擷取資產分析的Adobe Analytics報表套裝。 按一下&#x200B;**[!UICONTROL 「新增」]**。
1. 在[!DNL Experience Manager]設定報表套裝後，按一下&#x200B;**[!UICONTROL Done]**。

### 頁面追蹤器{#page-tracker}

在您設定Adobe Analytics帳戶後，會為您產生頁面追蹤器代碼。 若要啟用「資產前瞻分析」來追蹤第三方網站中使用的[!DNL Experience Manager]資產，請在網站程式碼中加入頁面追蹤器程式碼。 使用資產中的頁面追蹤器公用程式，產生頁面追蹤器代碼。<!--  For more information on how to include your Page Tracker code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

1. 在[!DNL Experience Manager]中，按一下&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 資產]**。

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. 在導覽頁 **[!UICONTROL 面中]** ，按一下 **** 前瞻分析頁面追蹤器卡片。
1. 按一下&#x200B;**[!UICONTROL 下載]**&#x200B;以下載頁面追蹤器代碼。

<!--

## Using demo package for Asset Insights {#using-demo-package-for-asset-insights}

Using the demo package, you can enable Adobe Asset Insights to capture data from and generate insights for a sample web page.

1. Configure Asset Insights using the instructions in [Configure Asset Insights](#configure-asset-insights).
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
