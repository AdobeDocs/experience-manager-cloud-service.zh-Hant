---
title: Cloud Acceleration Manager的整備階段
description: 本頁概述Cloud Acceleration Manager的整備階段。
exl-id: 91a13cae-4934-42e8-9538-896fd72f5acb
source-git-commit: 7d67bdb5e0571d2bfee290ed47d2d7797a91e541
workflow-type: tm+mt
source-wordcount: '682'
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

1. 導覽至&#x200B;**Readiness**&#x200B;區段，如下圖所示。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-1.png)

   >[!NOTE]
   >如需詳細資訊，請參閱在Cloud Acceleration Manager中建立及管理專案。

## 使用最佳實務分析卡 {#best-practices-analysis}

請依照下列步驟，使用「最佳實務分析」卡：

1. 按一下&#x200B;**Best Practices Analysis**&#x200B;卡片中的&#x200B;**Review**&#x200B;按鈕。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-2.png)

1. 請依照下列步驟下載Best Practices Analyzer(BPA)。

   >[!NOTE]
   >為避免對業務關鍵例項造成影響，建議您在盡可能接近生產環境的製作環境中，對自訂、設定、內容和使用者應用程式等方面執行BPA。 或者，您可以在複製的生產製作環境中執行 CRA。

   1. 導覽至[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)入口網站，並以zip檔案形式下載Best Practices Analyzer。

      >[!NOTE]
      >查看[使用最佳做法分析器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en#imp-considerations)以了解如何運行BPA。

   1. 將報表匯出為CSV格式

1. 按一下「**上傳新報表**」以在CAM中上傳BPA報表。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-3.png)

   >[!IMPORTANT]
   >如果您處於瀏覽器的無痕模式，則無法上傳報表。

1. 上傳新報表後，您會看到「最佳實務分析」報表。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/cam-bpareport.png)

1. 查看並探索CAM中的「最佳做法分析」儀表板。 如需詳細資訊，請參閱以下的[檢閱最佳實務分析報表](#analysis-report)一節。

   >[!NOTE]
   >上傳新報表會重設所有評估。

### 檢閱最佳實務分析報表 {#analysis-report}

探索「最佳實務分析報表」頁面中可用的下列資訊卡：

![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/cam-bpareport.png)

>[!NOTE]
> 使用每張卡片，您可以：
>* 按一下每個卡片以開啟其關聯的標籤
>* 將所有報表標籤加入書籤（包括篩選），以便共用或日後擷取
>* 使用「詳細資料」圖示來檢視每個報表結果的詳細資料


#### 報表屬性 {#report-properties}

**報表屬性**&#x200B;卡片提供報表屬性的相關資訊，例如報表日期、持續時間、篩選器、上傳日期和Adobe Experience Manager(AEM)詳細資訊。

![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-properties.png)

#### 報表概述 {#report-overview}

此&#x200B;**報表概述**&#x200B;卡片提供評估是否準備好移至AEMas a Cloud Service時適用的報表結果和嚴重性層級，如下圖所示。

![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-overview.png)

按一下此報告會開啟&#x200B;**Report**&#x200B;標籤。

![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-overview2.png)

您可以根據重要性、子類型或計數來篩選報表。

![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-overview3.png)

>[!NOTE]
>請參閱[解譯Best Practices Analyzer報表](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en) ，了解調查結果類別和重要性層級。

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

1. 按一下&#x200B;**Planning And Setup**&#x200B;卡中的&#x200B;**View**&#x200B;按鈕。 此卡片提供所有相關內容，可協助您規劃及設定AEM移轉。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-view.png)

1. 內容輪播會顯示移轉歷程這個階段的所有相關資訊。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-5-planning.png)

## 下一步 {#whats-next}

學習如何登入Cloud Acceleration Manager及如何建立專案後，您現在可以繼續檢閱[實作階段](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-implementation-phase.html?lang=en)中的下一個步驟。
