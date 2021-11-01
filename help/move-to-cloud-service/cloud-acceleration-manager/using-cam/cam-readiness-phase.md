---
title: Cloud Acceleration Manager的整備階段
description: 本頁概述Cloud Acceleration Manager的整備階段。
exl-id: 91a13cae-4934-42e8-9538-896fd72f5acb
source-git-commit: d706f8229cbca27ece5faedbecc4d02f58d40fb2
workflow-type: tm+mt
source-wordcount: '1057'
ht-degree: 5%

---

# Cloud Acceleration Manager的整備階段 {#readiness-phase-cam}

在Cloud Acceleration Manager中建立專案後，您現在可以在整備階段中開始評估目前的AEM實作。

準備階段包括：

* [最佳實務分析](#best-practices-analysis)
* [規劃和設定](#planning-setup)

請依照下列步驟導覽至整備階段：

1. 按一下您的專案卡，開啟專案登陸頁面。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/cam-landing1.png)

1. 導覽至 **準備** 部分，如下圖所示。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-1.png)

   >[!NOTE]
   >如需詳細資訊，請參閱在Cloud Acceleration Manager中建立及管理專案。

## 使用最佳實務分析卡 {#best-practices-analysis}

請依照下列步驟，使用「最佳實務分析」卡：

1. 按一下 **檢閱** 按鈕 **最佳實務分析** 卡片。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-2.png)

1. 請依照下列步驟下載Best Practices Analyzer(BPA)。

   >[!NOTE]
   >為避免對業務關鍵例項造成影響，建議您在盡可能接近生產環境的製作環境中，對自訂、設定、內容和使用者應用程式等方面執行BPA。 或者，您可以在複製的生產製作環境中執行 CRA。

   1. 導覽至 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) 入口網站，並以zip檔案形式下載Best Practices Analyzer。

      >[!NOTE]
      >檢閱 [使用Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en#imp-considerations) 來學習如何運行BPA。

   1. 將報表匯出為CSV格式

1. 按一下 **上傳新報表** 在CAM中上傳BPA報表。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-3.png)

   >[!IMPORTANT]
   >如果您處於瀏覽器的無痕模式，則無法上傳報表。

1. 上傳新報表後，您會看到「最佳實務分析」報表。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/cam-bpareport.png)

1. 查看並探索CAM中的「最佳做法分析」儀表板。 請參閱下方的章節 [檢閱最佳實務分析報表](#analysis-report) 以取得更多詳細資訊。

   >[!NOTE]
   >上傳新報表會重設所有評估。

### 使用打印預覽 {#print-preview-cam}

您可以在Cloud Acceleration Manager中選取列印預覽選項，以便列印報表的預覽，或將報表列印為PDF格式，以方便共用。

請遵循下列步驟：

1. 按一下 **打印預覽** 圖示，如下所示。

   ![影像](/help/move-to-cloud-service/best-practices-analyzer/assets/bpa-printpreview1.png)

1. 按一下 **打印預覽** 開啟新索引標籤，其中報表顯示在可列印的預覽中。 按一下 **列印** 將報表打印為PDF格式。

   >[!IMPORTANT]
   >* 選項 **另存為PDF** 建議並支援上述功能。
   >* 如果使用瀏覽器的打印按鈕，則只打印一頁。


   ![影像](/help/move-to-cloud-service/best-practices-analyzer/assets/bpa-printpreview2.png)

### 使用檢視趨勢線 {#trendline-view-cam}

在專案中上傳多個最佳實務分析器(BPA)報表時，您可以選取 **檢視趨勢線** 選項，查看和比較舊BPA報表的結果。

請依照下列步驟，從趨勢線選項中檢視報表：

>[!NOTE]
>在專案中上傳多個BPA報表時，您會看到 **...** 表徵圖。

1. 導覽至您的專案，然後按一下 **檢閱** 從 **最佳實務分析** 卡片 **準備** 階段。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view1a.png)

1. 按一下 **...** 圖示來顯示下拉式清單。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view1.png)

   >[!IMPORTANT]
   >顯示的報表一律為具有最新報表日期的報表。

1. 按一下 **檢視趨勢線**，如下圖所示。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view2.png)

1. 按一下 **檢視趨勢線** 開啟報告的趨勢線檢視，如下圖所示。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view3.png)

   >[!NOTE]
   >趨勢線報表以圖形表示方式顯示歷史BPA報表的結果。
   >
   >您會看到兩個圖表，顯示趨勢：
   >1. **報告結果趨勢**
   >1. **自訂元件和範本趨勢**

   >
   >您可以透過下拉式清單新增或變更圖形檢視，如下圖所示：
   >![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view4.png)


### 檢閱最佳實務分析報表 {#analysis-report}

探索「最佳實務分析報表」頁面中可用的下列資訊卡：

![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/cam-bpareport.png)

>[!NOTE]
> 使用每張卡片，您可以：
>* 按一下每個卡片以開啟其關聯的標籤
>* 將所有報表標籤加入書籤（包括篩選），以便共用或日後擷取
>* 使用「詳細資料」圖示來檢視每個報表結果的詳細資料


#### 報表屬性 {#report-properties}

此 **報表屬性** 「 」卡片提供報表屬性的相關資訊，例如報表日期、持續時間、篩選器、上傳日期，以及Adobe Experience Manager(AEM)詳細資料。

![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-properties.png)

#### 報表概述 {#report-overview}

此 **報表概述** 卡片提供評估移至AEMas a Cloud Service的準備程度時適用的報表結果和嚴重性層級，如下圖所示。

![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-overview.png)

按一下此報告會開啟 **報表** 標籤。

![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-overview2.png)

您可以根據重要性、子類型或計數來篩選報表。

![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-overview3.png)

>[!NOTE]
>請參閱 [解譯Best Practices Analyzer報表](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en) 了解調查結果類別和重要性級別。

#### 最佳做法評估 {#best-practices-assessment}

最佳實務評估選項可評估您目前的AEM例項，並提供採用AEM最佳實務的後續步驟指引。 您可以從此索引標籤檢閱下列資訊：

* AEM例項概述
* 自訂元件和範本
* 其他調查結果
* 查詢緩慢
* 維護任務

#### 遷移複雜性評估 {#migration-complexity-assessment}

「移轉複雜性評估」選項可評估將現有AEM實作移轉至AEMas a Cloud Service的複雜性。

您可以從此索引標籤檢閱下列資訊：

* AEM例項概述
* 評估
* 內容移轉考量事項

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/migration-complexity-1.png)

## 使用計畫和設定卡 {#planning-setup}

請按照本節，探索「規劃和設定」活動卡。

1. 按一下 **檢視** 按鈕 **計畫和設定** 卡片。 此卡片提供所有相關內容，可協助您規劃及設定AEM移轉。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-view.png)

1. 內容輪播會顯示移轉歷程這個階段的所有相關資訊。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-5-planning.png)

### 刪除最佳實務分析報表 {#delete-trendline}

請依照下列步驟，從趨勢線檢視中刪除報表：

>[!IMPORTANT]
>只有在專案中上傳了多個報表時，才能刪除報表。

1. 導覽至您的專案，然後按一下 **檢閱** 從 **最佳實務分析** 卡片 **準備** 階段。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view1a.png)

1. 按一下 **...** 圖示來顯示下拉式清單。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view1.png)

1. 按一下 **檢視趨勢線**，如下圖所示。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view2.png)

1. 按一下 **趨勢線報表** 螢幕。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view5.png)

1. 按一下 **刪除** 以確認刪除。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view6.png)

## 下一步 {#whats-next}

學習如何登入Cloud Acceleration Manager及如何建立專案後，您現在可以繼續檢閱 [實作階段](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-implementation-phase.html?lang=en).
