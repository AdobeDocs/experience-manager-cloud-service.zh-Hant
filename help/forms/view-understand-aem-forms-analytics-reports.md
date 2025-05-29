---
title: 檢視並了解 Adaptive Forms 分析報告
description: 最適化表單可順暢地與 Adobe Analytics 整合，以擷取和追蹤已發佈表單和文件的效能量度。
keywords: 檢視和瞭解Adaptive Forms Analytics報表、Adobe Analytics報表、Forms Analytics報表
topic-tags: develop
feature: Adaptive Forms
role: Admin, User
level: Intermediate
exl-id: 756dee1f-4685-4783-961d-b172a5bd0692
source-git-commit: 56a3d50d7cc8db532097b97f0898f87fc6ba0b3d
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 97%

---

# 檢視並了解 Adaptive Forms 分析報告 {#viewing-and-understanding-aem-forms-analytics-reports}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | 本文章 |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/integrate-aem-forms-with-experience-cloud-solutions/view-understand-aem-forms-analytics-reports.html) |

在快速發展的數位分析領域，跟上全球趨勢對於做出明智的決策和優化數位體驗至關重要。為此，最適化表單可順暢地與 Adobe Analytics 整合，以擷取和追蹤已發佈表單和文件的效能量度。分析這些量度的目的是做出資料導向式決策，使用量度和分析來增強表單的可用性和有效性。

透過擷取和追蹤關鍵績效指標，企業可以確定需要改進的領域，優化使用者體驗，並最終推動更好的結果，創造卓越的客戶體驗。

## 將 Adobe Analytics 設定為最適化表單 {#setup-adobe-analytics-to-aem-forms}

對於 AEM Forms Analytics 報告，首先透過 Experience Cloud Setup Automation 將 Adobe Analytics 整合到 AEM Forms。最適化表單中的 Experience Cloud Setup Automation 需要 Adobe Analytics 授權、Data Collection (先前稱為 Adobe Launch) 來管理追蹤指令碼，並與 Experience Platform Launch API 整合以簡化資料彙總和深入見解生成作業。請造訪[使用 Experience Cloud Setup Automation 為最適化表單啟用 Adobe Analytics](/help/forms/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation.md)以獲得完整的設定資訊。

>[!CAUTION]
>
>Experience Cloud設定自動化功能已過時。

## 檢視最適化表單 Adobe Analytics 報告 {#view-adobe-analytics-report}

1. 在您的 AEM 執行個體上，前往 **[!UICONTROL Forms]** >> **[!UICONTROL 表單和文件]**。
1. 選取您的表單，您會看到  Adobe Analytics 已整合到為 Adobe Analytics 啟動的表單中，如左側所示。

   ![檢視報告](assets/activ-aa.png){width="100%"}

1. 按一下 **Adobe Analytics** 查看報告並分析效能資料。

## 了解最適化表單分析報告 {#understanding-aem-forms-analytics-reports}

Adobe Analytics 提供了一系列全面的最適化表單效能量度，旨在提供表單使用情況的寶貴深入見解。這些量度為：

### **最適化表單的效能如何？** {#how-your-adaptive-form-is-performing}

它具有「表單轉譯」、「表單提交」、「驗證錯誤」和「不重複訪客」量度，可讓您評估表單的使用情況和有效性。

* **表格轉譯**：表單轉譯顯示表單被轉譯或開啟的次數。

* **表格提交**：表單提交表示使用者成功完成並提交最適化表單的次數。

* **驗證錯誤**：驗證錯誤顯示表單欄位中與驗證相關的錯誤總數。

* **不重複訪客**：不重複訪客表示單一訪客轉譯表單的次數。如需不重複訪客的詳細資訊，請參閱[不重複訪客、造訪和客戶行為](https://experienceleague.adobe.com/docs/analytics/components/metrics/visits.html?lang=zh-Hant)。

  ![表單效能](assets/forms-performance.png){width="100%"}

### **表單訪客** {#visitors-to-your-forms}

可以協助您獲得有關訪客在表單上的活動的寶貴深入見解：

* **造訪和提交**：描述了在某個日期範圍內您的表單被造訪的頻率以及對應的表單提交次數，如需相關詳細資訊，請按一下[造訪次數](https://experienceleague.adobe.com/docs/analytics/components/metrics/visits.html?lang=zh-Hant)。
* **不重複訪客及其總造訪次數**：它可區別新使用者和回訪使用者。例如，某位訪客可能在一個月內每天造訪您的網站，但這仍會計為單一不重複訪客。造訪[不重複訪客](https://experienceleague.adobe.com/docs/analytics/components/metrics/unique-visitors.html)了解詳細資訊。

  ![表單訪客](assets/forms-visitors.png){width="100%"}

### **裝置類型** {#device-type}

裝置類型可協助您識別用於存取表單的裝置類型。它將裝置類型歸類為行動裝置類型。例如，在此範例中，其為「行動裝置類型：其他」和「行動裝置類型：行動電話」。各種類型的行動裝置包括行動電話、平板電腦、媒體播放器、遊戲主機等。

![裝置類型](assets/device-type.png){width="100%"}

### **地理劃分** {#geographical-breakdown}

它顯示存取表單的位置。它提供有關表單使用者的區域特定資訊，例如，您可以看到表單使用者的區域特定資訊是印度，如圖所示。

![地理劃分](assets/geographical-breakdown.png){width="100%"}

### **主要流量來源和熱門表單** {#top-sources-of-traffic-and-popular-forms}

這可協助您識別表單參考所在主要來源或連結。例如，在下圖中，您可以看到最適化表單的搜尋實例，其中 18.9% 是&#x200B;**分類/建立書籤**，70.49% 基於&#x200B;**搜尋引擎**，24%來自&#x200B;**其他網站**。您可以根據您的需求定義維度項目。此外，您還可以找出造訪次數最多或最受歡迎的表單。

![參考的網站](assets/referred-sites.png){width="100%"}

### **熱門表單的使用者活動** {#user-activity-on-top-forms}

全面呈現使用者參與度 (含欄位造訪次數)、表單轉譯、驗證錯誤、捨棄表單、表單提交，提供最活躍表單的深入見解。在下圖中，您可以看到根據表單事件量度，申請表單是最活躍的。

![使用者活動](assets/user-activity.png){width="100%"}

### **表單逗留時間表** {#timeline-for-time-spent-on-forms}

這是使用者在表單上逗留的時間，可以協助您識別參與模式。

![表單逗留時間](assets/time-spent-on-forms.png){width="100%"}

### **訪客需要協助填寫表單的區域** {#areas-requiring-assistance}

說明檢視、驗證錯誤和欄位造訪等量度顯示使用者裡需協助的地方或我們如何追蹤欄位中的錯誤。例如，在下圖中，您可以看到表單，包含的欄位有：**全名**、**電話號碼**、**DoB**。這&#x200B;**全名**&#x200B;欄位有 12 次造訪，在 12 次造訪中，有 8 次造訪出現驗證錯誤，1 次點擊說明圖示以取得該欄位的說明檢視。您可以查看其他表單欄位的量度資料。

![協助區域](assets/assisting-areas.png){width="100%"}

### **訪客在捨棄表單之前最後查看的表單欄位** {#last-form-field-that-visitors-viewed}

可以協助您分析使用者在捨棄表單之前花時間造訪的表單欄位。例如，在下圖中，5 個捨棄表格中，2 個停在&#x200B;**全名**&#x200B;欄位、2 個停在&#x200B;**電話號碼**&#x200B;欄位、1 個停在&#x200B;**文字輸入**&#x200B;欄位。

![欄位訪客](assets/field-visitors.png){width="100%"}

## 另請參閱 {#see-also}

* [使用 Experience Cloud Setup Automation 為最適化表單啟用 Adobe Analytics](/help/forms/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation.md)
* [新增自適應表單至 AEM Sites 頁面或體驗片段](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [將AEM Forms與Adobe Analytics整合](/help/forms/integrate-aem-forms-with-adobe-analytics.md)
