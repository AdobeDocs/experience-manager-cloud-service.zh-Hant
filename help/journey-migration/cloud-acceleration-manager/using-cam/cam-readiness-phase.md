---
title: 雲加速管理器中的就緒性階段
description: 本頁概述了Cloud Acceleration Manager中的就緒階段。
exl-id: 2583985b-0358-433c-9d31-38e2c60dc3dc
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1057'
ht-degree: 5%

---

# 雲加速管理器中的就緒性階段 {#readiness-phase-cam}

在雲加速管理器中建立項目後，您現在可以開始評估當前實施AEM的就緒性階段。

準備階段包括：

* [最佳做法分析](#best-practices-analysis)
* [計畫和設定](#planning-setup)

按照以下步驟導航至準備階段：

1. 按一下項目卡開啟項目登錄頁。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/cam-landing1.png)

1. 導航到 **就緒** 的下界。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/readiness-1.png)

   >[!NOTE]
   >請參閱在Cloud Acceleration Manager中建立和管理項目以瞭解詳細資訊。

## 使用最佳做法分析卡 {#best-practices-analysis}

按照以下步驟使用最佳做法分析卡：

1. 按一下 **審閱** 按鈕 **最佳做法分析** 卡。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/readiness-2.png)

1. 按照以下步驟下載最佳做法分析器(BPA)。

   >[!NOTE]
   >為避免對業務關鍵型實例產生影響，建議在定制、配置、內容和用戶應用程式方面盡可能接近生產環境的「作者」環境上運行BPA。 或者，您可以在複製的生產製作環境中執行 CRA。

   1. 導航到 [軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) 將最佳做法分析器作為zip檔案下載。

      >[!NOTE]
      >審閱 [使用最佳做法分析器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en#imp-considerations) 學習如何運行BPA。

   1. 以CSV格式導出報告

1. 按一下 **上載新報表** 在CAM中上載BPA報告。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/readiness-3.png)

   >[!IMPORTANT]
   >如果您處於瀏覽器的Incognito模式，則無法上載報表。

1. 上載新報告後，您將看到「最佳實踐分析」報告。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/cam-bpareport.png)

1. 查看並瀏覽CAM中的「最佳實踐分析」操控板。 請參閱下面的部分 [複查最佳做法分析報告](#analysis-report) 的子菜單。

   >[!NOTE]
   >上載新報告會重置所有評估。

### 使用打印預覽 {#print-preview-cam}

您可以在Cloud Acceleration Manager中選擇打印預覽選項，以便進行報表的可打印預覽，或將報表打印為PDF格式，以便於共用。

請遵循下列步驟：

1. 按一下 **打印預覽** 表徵圖，如下所示。

   ![影像](/help/journey-migration/best-practices-analyzer/assets/bpa-printpreview1.png)

1. 按一下 **打印預覽** 開啟一個新頁籤，其中報告顯示在可打印的預覽中。 按一下 **打印** 打印報表到PDF。

   >[!IMPORTANT]
   >* 選項 **另存為PDF** 建議並支援上述功能。
   >* 如果使用瀏覽器的打印按鈕，則只打印一頁。


   ![影像](/help/journey-migration/best-practices-analyzer/assets/bpa-printpreview2.png)

### 使用查看趨勢線 {#trendline-view-cam}

在項目中上載多個最佳做法分析器(BPA)報告時，可以選擇 **查看趨勢線** 選項，查看和比較歷史BPA報告的結果。

按照以下步驟從趨勢線選項查看報告：

>[!NOTE]
>在項目中上載多個BPA報告時，您將看到 **...** 表徵圖

1. 導航到項目並按一下 **審閱** 從 **最佳做法分析** 卡 **就緒** 。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1a.png)

1. 按一下 **...** 表徵圖。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1.png)

   >[!IMPORTANT]
   >顯示的報告始終是具有最新報告日期的報告。

1. 按一下 **查看趨勢線**，如下圖所示。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view2.png)

1. 按一下 **查看趨勢線** 開啟報告的趨勢線視圖，如下圖所示。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view3a.png)


   >[!NOTE]
   >趨勢線報告以圖形表示形式顯示歷史BPA報告的結果。
   >
   >您將看到兩個圖表，其中顯示了以下趨勢：
   >1. **報告發現趨勢**
   >1. **自定義元件和模板趨勢**

   >
   >您可以通過下拉菜單添加或更改圖形視圖，如下圖所示：
   >![影像](/help/journey-migration/cloud-acceleration-manager/assets/reports-bpa1.png)


### 複查最佳做法分析報告 {#analysis-report}

瀏覽「最佳實踐分析報告」頁中提供的以下卡：

![影像](/help/journey-migration/cloud-acceleration-manager/assets/cam-bpareport.png)

>[!NOTE]
> 使用每張卡，您可以：
>* 按一下每張卡以開啟其關聯的頁籤
>* 將所有報表頁籤（包括篩選）書籤以用於共用或將來檢索
>* 使用詳細資訊表徵圖查看每個報表查找結果的詳細資訊


#### 報表屬性 {#report-properties}

的 **報表屬性** card提供有關報告屬性的資訊，如報告日期、持續時間、篩選器、上載日期和Adobe Experience Manager(AEM)詳細資訊。

![影像](/help/journey-migration/cloud-acceleration-manager/assets/report-properties.png)

#### 報告概述 {#report-overview}

此 **報告概述** card提供在評估是否準備遷移到as a Cloud Service時適用的報告發現AEM和嚴重性級別，如下圖所示。

![影像](/help/journey-migration/cloud-acceleration-manager/assets/report-overview.png)

按一下此報告將開啟 **報告** 頁籤。

![影像](/help/journey-migration/cloud-acceleration-manager/assets/report-overview2.png)

您可以根據重要性、子類型或計數來篩選報表。

![影像](/help/journey-migration/cloud-acceleration-manager/assets/report-overview3.png)

>[!NOTE]
>請參閱 [解釋最佳做法分析器報告](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en) 瞭解調查結果類別和重要性級別。

#### 最佳做法評估 {#best-practices-assessment}

「最佳做法評估」選項可評估您當前AEM的實例，並指導採用最佳做AEM法的後續步驟。 您可以從此頁籤查看以下資訊：

* 實AEM例概述
* 自定義元件和模板
* 其他發現
* 查詢緩慢
* 維護任務

#### 遷移複雜性評估 {#migration-complexity-assessment}

「遷移複雜性評估」選項可評估將現有實施遷移到as a Cloud Service的AEM複雜AEM性。

您可以從此頁籤查看以下資訊：

* 實AEM例概述
* 評估
* 內容遷移注意事項

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/migration-complexity-1.png)

## 使用計畫和設定卡 {#planning-setup}

按照本節來瀏覽Planning和Setup活動卡。

1. 按一下 **視圖** 按鈕 **計畫和設定** 卡。 此卡提供所有相關內容，幫助您規劃和設定遷移AEM。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/readiness-view.png)

1. 內容傳送器顯示遷移過程的這一階段的所有相關資訊。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/readiness-5-planning.png)

### 刪除最佳做法分析報告 {#delete-trendline}

按照以下步驟從趨勢線視圖中刪除報表：

>[!IMPORTANT]
>只有在項目中上載了多個報表時，才能刪除報表。

1. 導航到項目並按一下 **審閱** 從 **最佳做法分析** 卡 **就緒** 。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1a.png)

1. 按一下 **...** 表徵圖。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1.png)

1. 按一下 **查看趨勢線**，如下圖所示。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view2.png)

1. 按一下 **趨勢線報告** 的上界。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view5a.png)

1. 按一下 **刪除** 確認刪除。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view6a.png)

## 下一步是什麼 {#whats-next}

一旦您學會了如何登錄到Cloud Acceleration Manager以及如何建立項目，您現在就可以繼續查看中的下一步 [實施階段](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-implementation-phase.html?lang=en)。
