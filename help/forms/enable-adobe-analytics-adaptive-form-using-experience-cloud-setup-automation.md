---
title: 如何為最適化表單啟用Adobe Analytics？
description: Experience Cloud Setup Automation 可協助將 Adobe Analytics 連接到最適化表單，以追蹤關於訪客互動和參與度的深入見解。
keywords: 使用 Experience Cloud Setup Automation 為最適化表單啟用 Adobe Analytics，啟用Forms中的Adobe Analytics、Adaptive Forms中的Adobe Analytics、Forms Analytics整合、Forms和Adobe Analytics
exl-id: 0e1aa040-08b4-4c1a-b247-ad6fff410187
source-git-commit: 7a65aa82792500616f971df52b8ddb6d893ab89d
workflow-type: tm+mt
source-wordcount: '1593'
ht-degree: 59%

---

# 使用 Experience Cloud Setup Automation 為最適化表單啟用 Adobe Analytics {#integrate-adobe-analytics-to-aem-forms-with-experience-cloud-setup-automation}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | 本文章 |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/integrate-aem-forms-with-experience-cloud-solutions/configure-analytics-forms-documents.html) |

Experience Cloud Setup Automation 可協助將 Adobe Analytics 連接到最適化表單，這有助於追蹤和分析使用者與表單的互動，並提供關於訪客互動和參與度的深入見解。Experience Cloud Setup Automation 也可協助監控表單效能，其中涉及評估像是完成時間和退出點等量度。此分析有助於優化表單以提供更好的使用者體驗，同時根據登入狀態 (例如匿名使用者) 區分使用者行為，以識別整體趨勢和模式。

## 將 Adobe Analytics 整合至最適化表單的優勢 {#advantages-of-integrating-adobe-analytics-with-aem-forms}

* **深入分析一般使用者的行為**：Adobe Analytics 有助於深入分析一般使用者行為，顯示使用者動作、使用者退出和完成率，從而更深入了解個人如何使用表單。
* **使非技術商務使用者能夠獲得深入見解**：Adobe Analytics 透過其易於使用的介面，即使是非技術使用者也能存取和解釋表單使用數據，從而做出資料導向決策，可增強註冊體驗。
* **根據使用情況優化資料擷取體驗**：組織可以輕鬆識別資料擷取的痛點，進行有目標的改進，從而增強表單可用性並增加成功提交數量。

## 最適化表單使用情況量度的範圍 {#scope-of-adaptive-forms-usage-metrics}

Adobe Analytics 提供了一系列全面的最適化表單效能量度，旨在提供表單使用情況的寶貴深入見解。這些量度為：

* **表單轉譯、表單提交、驗證錯誤、不重複訪客**，可讓您評估表單的使用情況和有效性。

* **訪客深入見解**，其中包括造訪和提交頻率以及不重複訪客計數，提供表單對象的全面檢視。

* **裝置類型**&#x200B;資料告知您使用者用來存取表單之裝置的資料。

* **地理劃分**&#x200B;顯示表單使用者的區域分佈。

* **流量來源**&#x200B;和&#x200B;**熱門表單**&#x200B;量度，其包含最常使用的反向連結網域和最常被造訪的表單，可協助您了解流量來源和最受歡迎的表單。

* **熱門表單的使用者活動**，提供關於欄位造訪、表單轉譯、驗證錯誤、捨棄表單和表單提交的深入見解，使您能夠分析使用者行為。

* **表單逗留時間表**，其以時間表檢視的形式，提供表單的使用者參與度。

* **需提供訪客協助的區域**&#x200B;量度，其包括說明檢視、驗證錯誤實例和欄位造訪頻率，用於凸顯使用者在填寫表單時可能需要協助的地方。

![Analytics 報告](assets/analytics-report.png){width="100%"}


如需每個量度的詳細資訊，請造訪[檢視並了解 AEM Forms Analytics 分析報告](/help/forms/view-understand-aem-forms-analytics-reports.md)

## 先決條件 {#prerequisites}

<!--
Analytics, Data Collection (Formerly Adobe Launch), and Experience Manager (experience.adobe.com)
-->

Experience Cloud設定自動化需要 **Adobe Analytics授權**， **資料收集(先前稱為Adobe Launch)** 管理追蹤指令碼，以及 **Experience Manager Forms授權** 以簡化資料彙總和洞察力產生作業。

如果您擁有的有效授權 **Adobe Analytics** 和 **Experience Manager Forms**，而且您已與整合 **資料收集(先前稱為Adobe Launch)**，您應該在開發人員主控台中驗證其可用性。

若要確認上述功能是否適用於您的Formsas a Cloud Service環境，請造訪 [開發人員主控台](https://developer.adobe.com/console/projects)，瀏覽至專案並使用方案id — 環境id搜尋您的專案，例如，使用URL的環境 `https://author-p45913-e175111-cmstg.adobeaemcloud.com/index.html`，方案id — 環境id為 `p45913-e175111`. 確保有列出 Experience Cloud Setup Automation、Adobe Analytics 和 Experience Platform Launch API。如果都有列出，您可以為您的最適化表單啟用 Adobe Analytics。

![先決條件表單分析整合](assets/analytics-aem.png){width="100%"}

<!-- 
>[!NOTE]
> If you have an active licenses for Experience Cloud Setup Automation, Adobe Analytics, and Experience Platform Launch API, you should verify their availability within your developer console.
-->

<!-- For more information about your available integrations, see [troubleshooting Adaptive Forms with Analytics Integration](https://experienceleague.adobe.com/docs/experience-manager-65/forms/integrate-aem-forms-with-experience-cloud-solutions/view-understand-aem-forms-analytics-reports.html)
-->

## 設定 Adobe Analytics {#configure-adobe-analytics}

執行下列步驟，為您的最適化表單啟用和設定 Adobe Analytics：

* [為以基礎元件為主的最適化表單啟用 Adobe Analytics](#integrate-adobe-analytics-with-aem-forms-for-foundation-component)
* [為以核心元件為主的最適化表單啟用 Adobe Analytics](#integrate-adobe-analytics-with-aem-forms-for-core-components)

>[!VIDEO](https://video.tv.adobe.com/v/3424577/enable-adobe-analytics/?quality=12&learn=on)


<!--
>[!NOTE]
>
> This is the demo video for **Foundation Component**. In **Core Component** you are required to perform similar steps but the container is not chosen for forms.
-->

### 針對基礎元件為最適化表單啟用 Adobe Analytics {#integrate-adobe-analytics-with-aem-forms-for-foundation-component}

1. 建立雲端服務的設定容器：
   1. 前往&#x200B;**[!UICONTROL 工具 > 一般 > 設定瀏覽器]**。
   1. 選取或建立設定容器，並啟用&#x200B;**[!UICONTROL 雲端設定]**&#x200B;資料夾。
   1. 點選&#x200B;**[!UICONTROL 儲存並關閉]**&#x200B;以儲存設定並退出對話框。
1. 在您的 AEM 執行個體上，前往 **[Forms]** >> **[表單和文件]**。
1. 選取您的&#x200B;**[!UICONTROL 表單]** >> **[!UICONTROL 屬性]**，在&#x200B;**[!UICONTROL 設定容器]**&#x200B;中，選取您在步驟 1 於&#x200B;**[!UICONTROL 設定瀏覽器]** 建立或選取的設定容器。
1. 選取左邊欄的任務面板，然後按一下&#x200B;**設定 Analytics** 和&#x200B;**啟動 Adobe Analytics**。
1. 提供您偏好的報告套裝名稱，然後按一下&#x200B;**[!UICONTROL 下一步]**&#x200B;和&#x200B;**[!UICONTROL 儲存]**。
1. 儲存專案後，設定程序會執行一段時間，直到 Adobe Analytics 整合至您的最適化表單，您也可以查看&#x200B;**整合狀態**。

   >[!NOTE]
   >
   >如果設定程序超過 15 分鐘，請重新嘗試為您的表單啟用分析功能。

1. 在您的 AEM 執行個體上，前往 **[!UICONTROL Forms]** >> **[表單和文件]**，並選取您的&#x200B;**[!UICONTROL 表單]**，您會看到 Adobe Analytics 已整合至您的表單，如下圖所示。
1. 現在您可以檢視您的[最適化表單 Adobe Analytics 報告](#view-adobe-analytics-report)。

![整合的 AEM Analytics](assets/analytics-aem-integrated.png){width="100%"}


### 針對核心元件為最適化表單啟用 Adobe Analytics {#integrate-adobe-analytics-with-aem-forms-for-core-components}

1. 在您的 AEM 執行個體上，前往 **[!UICONTROL Forms]** >> **[!UICONTROL 表單和文件]**&#x200B;並選取您的&#x200B;**[!UICONTROL 表單]**。
1. 選取左側的任務面板，然後按一下&#x200B;**設定 Analytics** 和&#x200B;**啟動 Adobe Analytics**。
1. 提供您偏好的報告套裝名稱，然後按一下&#x200B;**[!UICONTROL 下一步]**&#x200B;和&#x200B;**[!UICONTROL 儲存]**。
1. 儲存專案後，設定程序會執行一段時間，直到 Adobe Analytics 整合至您的最適化表單，您也可以查看&#x200B;**整合狀態**。

   >[!NOTE]
   >
   >如果設定程序超過 15 分鐘，請重新嘗試為您的表單啟用分析功能。

1. 在您的 AEM 執行個體上，前往 **[!UICONTROL Forms]** >> **[!UICONTROL 表單和文件]**，並選取您的&#x200B;**[!UICONTROL 表單]**，您會看到 Adobe Analytics 已整合至您的表單。
1. 現在您可以檢視您的[最適化表單 Adobe Analytics 報告](#view-adobe-analytics-report)。

## 檢視最適化表單 Adobe Analytics 報告 {#view-adobe-analytics-report}

1. 在您的 AEM 執行個體上，前往 **[!UICONTROL Forms]** >> **[!UICONTROL 表單和文件]**。
1. 選取您的表單，您會看到  Adobe Analytics 已整合到為 Adobe Analytics 啟動的表單中，如左側所示。

   ![檢視報告](assets/activ-aa.png){width="100%"}

1. 按一下 **Adobe Analytics** 查看報告並分析效能資料。

若要使用手動方法將最適化表單與 Adobe Analytics 連接，請造訪[將 AEM Forms 與 Adobe Analytics 整合](/help/forms/integrate-aem-forms-with-adobe-analytics.md)。

## 啟用Analytics以在Sites中自適應Forms {#Connect-Analytics-to-Adaptive-Forms-in-Sites}

在AEM Sites中為您的Adaptive Form設定Analytics可協助您追蹤使用者互動以及您在Sites頁面中的Form上提交的表單。 透過在您的Sites Forms中緊密整合分析，您可獲得有關使用者行為、轉換率和表單中需改善領域的寶貴見解。

### 先決條件 {#Prerequisites-to-connect-forms-analytics-to-sites}

若要在適用於AEM Sites的Adaptive Forms中連線並啟用分析，您必須確保您的AEM Sites具備作用中的Adobe Analytics。

### 在Sites中連線最適化Forms以啟用Analytics {#Connect-analytics-to-adaptive-forms}

若要在AEM Sites頁面中連線最適化表單以啟用Analytics，請包含 `customfooterlibs` 使用AEM原型/Git存放庫和部署管道將使用者端程式庫移至AEM Sites頁面。

1. 開啟您的 [AEM Forms原型或複製的Git存放庫](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) 在文字編輯器中專案。 例如，Visual Studio Code。

1. 導覽至您最適化表單所在的網站頁面，例如，在此示範專案中，我們有 `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`.

1. 複製值 `sling:resourceSuperType`. 例如，值為 `core/wcm/components/page/v3/page`.

   ![Sling 資源](/help/forms/assets/slingresource.png){width="100%"}

1. 在該位置建立類似的結構 `ui.apps/src/main/content/jcr_root/apps` 與 `core/wcm/components/page/v3/page`.

   ![覆蓋結構](/help/forms/assets/overlaystructure.png){width="100%"}

1. 新增 `customfooterlibs.html` 檔案。

       ```
       // customheaderlibs.html
       &lt;sly data-sly-use.page=&quot;com.adobe.cq.wcm.core.components.models.Page&quot;>
       &lt;sly data-sly-test=&quot;${page.data &amp;&amp; page.dataLayerClientlibIncluded}&quot; data-sly-call=&quot;${clientlib.js @ categories=&amp;#39;core.forms.components.commons.v1.datalayer&amp;#39;, async=true}&quot;>&lt;/sly>
       &lt;/sly>
       
       ```
   
   此 `customfooterlibs.html` 用於JavaScript。

1. [執行管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) 以部署變更。

### 啟用表單分析規則至網站中的Forms {#bind-forms-analytics-rules-to-forms-in-sites}

1. 造訪 **Adobe Experience Platform資料彙集**.
1. 按一下 **標籤** 位於左側。
1. 使用計畫ID （如下圖所示）搜尋您的專案，例如，搜尋具有URL的環境 `https://author-p45921-e175111-cmstg.adobeaemcloud.com/index.html`，方案id為 `45921`.

   ![搜尋 — your-form-in-data-collection](/help/forms/assets/aep-data-collection.png){width="100%"}

1. 新增以下專案的設定： **表單規則** 和 **資料元素** 如下所示：

#### 新增表單規則 {#form-rules}

1. 選擇您的表單並新增 **新增屬性** 位於右上角，或按一下您的表單。
1. 在屬性頁面上，按一下 **規則** 並為您的表單選取事件，在下方的範例影像中，它是 **表單事件**.

   ![搜尋 — your-form-in-data-collection](/help/forms/assets/aep-form-event-properties.png){width="100%"}

1. 選取表單中的所有事件並 **複製** 位在右上邊欄的位置。
1. 一旦複製， **複製規則** 會出現快顯視窗，讓您使用project-id搜尋Sites頁面，以貼上「表單規則」。

   ![複製 — 表單 — 規則](/help/forms/assets/copy-form-rules.png){width="100%"}

1. 按一下 **複製** 將表單規則貼到Sites頁面。

#### 新增資料元素 {#data-elements}

1. 選擇您的表單並新增 **新增屬性** 位於右上角，或按一下您的表單。
1. 在屬性頁面上，按一下 **資料元素** 並為您的表單選取事件。
1. 選取表單中的所有事件並 **複製** 位於右上邊欄中。
1. 一旦複製， **複製規則** 會出現快顯視窗，讓您使用project-id搜尋Sites頁面，以貼上「表單規則」。
1. 按一下 **複製** 將表單規則貼到Sites頁面。

   ![Form-data-element](/help/forms/assets/form-data-elements.png){width="100%"}

透過上述步驟繫結Form和Sites規則後，請執行以下步驟以啟用Analytics至Sites頁面中的調適型表單：

1. 按一下 **發佈流程** 左側。
1. 按一下 **新增程式庫** 並輸入您偏好的名稱。
1. 在 **環境** 從右側的下拉式清單中選取 **開發**.
1. 按一下 **新增所有變更的資源**.
1. 按一下 **儲存並建置到開發環境**.

![發佈至開發](/help/forms/assets/publish-to-dev.png){width="100%"}


<!--

## Best Practices

1.    Verify that Adobe Analytics is enabled on all the forms activated for Adobe Analytics.

1.    Check the Adobe Analytics report periodically to gain insights into user behavior and form performance. For instance, you may set the cadence to 15 days or the period you prefer to choose for report analysis. This enables you to improve the forms enrollment experience.

1.    Enable Analytics for all or most of your forms for tracking and analyzing user interaction with your forms and to gain insights into visitor interactions and engagement.

1. Check your forms performance after you update your form fields or components.

1.    Share Analytics report with your peer groups for review, you can schedule your report for a later time.

-->

## 另請參閱 {#see-also}

* [檢視和瞭解最適化Forms分析報表](/help/forms/view-understand-aem-forms-analytics-reports.md)
* [新增最適化表單至 AEM Sites 頁面或體驗片段](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [將AEM Forms與Adobe Analytics整合](/help/forms/integrate-aem-forms-with-adobe-analytics.md)
