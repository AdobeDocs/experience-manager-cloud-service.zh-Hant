---
title: Cloud Acceleration Manager的整備階段
description: 本頁提供Cloud Acceleration Manager整備階段的概觀。
exl-id: 2583985b-0358-433c-9d31-38e2c60dc3dc
feature: Migration
role: Admin
source-git-commit: 3a0576e62518240b89290a75752386128b1ab082
workflow-type: tm+mt
source-wordcount: '1096'
ht-degree: 7%

---

# Cloud Acceleration Manager的整備階段 {#readiness-phase-cam}

在Cloud Acceleration Manager (CAM)中建立專案後，您現在可以在「整備」階段開始評估目前的Adobe Experience Manager (AEM)實作。

整備階段包括：

* [最佳實務分析](#best-practices-analysis)
* [規劃與設定](#planning-setup)

請依照下列步驟，導覽至「整備階段」：

1. 按一下您的專案卡。

   ![專案卡](/help/journey-migration/cloud-acceleration-manager/assets/cam-landing1.png)

1. 在專案登陸頁面上，導覽至「**整備**」區段，如下圖所示。

   ![整備](/help/journey-migration/cloud-acceleration-manager/assets/readiness-1.png)

   >[!NOTE]
   >如需瞭解詳細資訊，請參閱在Cloud Acceleration Manager中建立和管理專案。

## 使用最佳做法分析工具卡 {#best-practices-analysis}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_bpa"
>title="最佳做法分析工具報告"
>abstract="BPA 報告可以上傳到 CAM，以提供有關移轉到 AEM as a Cloud Service 的分析。"
>additional-url="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer" text="使用最佳做法分析工具"

1. 從&#x200B;**最佳實務分析**&#x200B;卡片按一下&#x200B;**檢閱**。

   ![最佳實務分析 — 檢閱](/help/journey-migration/cloud-acceleration-manager/assets/readiness-2.png)

1. 下載Best Practices Analyzer (BPA)。

   >[!NOTE]
   >為避免對業務關鍵例項造成影響，Adobe建議您在Author環境中執行BPA。 在自訂、設定、內容和使用者應用程式方面，環境應儘可能接近生產環境。 或者，您可以在複製的生產製作環境中執行CRA。

   1. 導覽至[軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?fulltext=best*)入口網站，並下載Best Practices Analyzer做為ZIP檔。

      >[!NOTE]
      >檢閱[使用Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=zh-Hant#imp-considerations)以瞭解如何執行BPA。

1. 在CAM中，按一下&#x200B;**取得上傳金鑰**，以便取得用來設定系統以直接將BPA報告自動上傳至CAM的金鑰。

   ![取得上傳金鑰](/help/journey-migration/cloud-acceleration-manager/assets/readiness-3b.png)

   >[!IMPORTANT]
   >報表仍可手動上傳，但使用上傳金鑰可簡化作業。 請注意，如果報表大小約為200MB或更大，則無法手動上傳報表。 也無法使用瀏覽器的無痕模式上傳報告。

1. 上傳新報告後，您可以在CAM中看到「最佳實務分析」報告。

   ![最佳實務分析報告](/help/journey-migration/cloud-acceleration-manager/assets/cam-bpareport.png)

   >[!NOTE]
   >如果上傳了多個不同的報告，則詳細顯示的報告總是具有最近的建立日期（不是上傳日期）的報告。

1. 檢閱並探索CAM中的「最佳實務分析」儀表板。 如需詳細資訊，請參閱[檢閱最佳實務分析報告](#analysis-report)。

   >[!NOTE]
   >如果新報告比先前載入的報告新，上傳新報告會重設所有評估。

### 使用列印預覽 {#print-preview-cam}

您可以在Cloud Acceleration Manager中選取「列印預覽」選項，以列印報表預覽，或以PDF格式列印報表，以方便共用。

請遵循下列步驟：

1. 按一下&#x200B;**列印預覽**&#x200B;動作。

   ![列印預覽](/help/journey-migration/best-practices-analyzer/assets/bpa-printpreview1b.png)

1. 在可列印預覽中顯示報告的新標籤上，按一下&#x200B;**列印**&#x200B;以將報告列印成PDF格式。

   >[!IMPORTANT]
   >
   >* 上述功能建議並支援選項&#x200B;**另存為PDF**。
   >* 如果使用瀏覽器的列印按鈕，則只會列印一頁。

   ![列印](/help/journey-migration/best-practices-analyzer/assets/bpa-printpreview2.png)

### 使用檢視趨勢線 {#trendline-view-cam}

當您在專案中上傳多個不同的Best Practices Analyzer (BPA)報告時，可以選取&#x200B;**檢視趨勢線**&#x200B;選項來檢視和比較歷史BPA報告的結果。

請依照下列步驟，從趨勢線選項檢視報表：

>[!NOTE]
>當您在專案中上傳多個不同的BPA報告時，您會看到&#x200B;**...**&#x200B;圖示。 如果報表的主機和建立時間相同，則會將報表視為相同（非不同）。

1. 導覽至您的專案，然後從&#x200B;**整備**&#x200B;階段的&#x200B;**最佳實務分析**&#x200B;卡中，按一下&#x200B;**檢閱**。

   ![最佳實務分析 — 檢閱](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1a.png)

1. 從&#x200B;**檢視**&#x200B;下拉式清單中，按一下&#x200B;**趨勢線報告**，如下圖所示。

   ![趨勢線報告](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1b.png)

1. 按一下&#x200B;**趨勢線報告**&#x200B;開啟報告的趨勢線檢視。

   ![趨勢線檢視](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view3a.png)


   >[!NOTE]
   >趨勢線報告會以圖形呈現方式顯示歷史BPA報告的結果。
   >
   >您會看到兩個顯示下列趨勢的圖表：
   > 
   >1. **報告發現趨勢**
   >1. **自訂元件與範本趨勢**
   >
   >您可以透過下拉式清單新增或變更圖形檢視，如下圖所示：
   >![選取圖形檢視](/help/journey-migration/cloud-acceleration-manager/assets/reports-bpa1.png)


### 檢閱最佳做法分析報表 {#analysis-report}

探索最佳實務分析報告頁面中可用的卡片：

![最佳實務分析報告](/help/journey-migration/cloud-acceleration-manager/assets/cam-bpareport.png)

>[!NOTE]
> 您可以使用每張卡片：
>
>* 開啟其相關聯的標籤
>* 將所有報表標籤（包括篩選）加入書籤，以便共用或未來擷取
>* 使用詳細資訊圖示可檢視每個報告發現的詳細資訊

#### 報告屬性 {#report-properties}

**報告屬性**&#x200B;卡片提供報告屬性的相關資訊，例如報告日期、持續時間、篩選器、上傳日期和Adobe Experience Manager (AEM)詳細資料。

![報告屬性](/help/journey-migration/cloud-acceleration-manager/assets/report-properties.png)

#### 報告總覽 {#report-overview}

此&#x200B;**報告總覽**&#x200B;卡片提供評估移至AEM as a Cloud Service的整備程度時適用的報告發現和嚴重性層級，如下圖所示。

![報告總覽](/help/journey-migration/cloud-acceleration-manager/assets/report-overview.png)

按一下此報表可開啟&#x200B;**報表**&#x200B;標籤。

![報告標籤](/help/journey-migration/cloud-acceleration-manager/assets/report-overview2.png)

您可以根據重要性、子型別或計數來篩選報表。

![報告篩選器](/help/journey-migration/cloud-acceleration-manager/assets/report-overview3.png)

>[!NOTE]
>請參閱[解譯Best Practices Analyzer報告](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=zh-Hant)，瞭解發現專案類別和重要性層級。

#### 最佳實務評估 {#best-practices-assessment}

最佳實務評估選項可評估您目前的AEM執行個體，並提供採用AEM最佳實務之後續步驟的指引。 您可以從此標籤檢閱下列資訊：

* AEM 執行個體總覽
* 自訂元件與範本
* 其他發現
* 緩慢查詢
* 維護任務

#### 移轉複雜性評估 {#migration-complexity-assessment}

「移轉複雜性評估」選項可評估將現有AEM實作移轉到AEM as a Cloud Service的複雜性。

您可以從此標籤檢閱下列資訊：

* AEM 執行個體總覽
* 評估
* 內容移轉考量事項

  ![移轉複雜性評估](/help/journey-migration/cloud-acceleration-manager/assets/migration-complexity-1.png)

## 使用Planning and Setup卡 {#planning-setup}

1. 從&#x200B;**規劃與設定**&#x200B;卡片，按一下&#x200B;**檢視**。 此卡片提供所有相關內容，可協助您規劃和設定AEM移轉。

   ![規劃與設定 — 檢視](/help/journey-migration/cloud-acceleration-manager/assets/readiness-view.png)

1. 內容輪播會顯示移轉歷程這個階段的所有相關資訊。

   ![規劃及設定輪播](/help/journey-migration/cloud-acceleration-manager/assets/readiness-5-planning.png)

### 從趨勢線檢視刪除最佳實務分析報告 {#delete-trendline}

>[!IMPORTANT]
>一個專案已上傳多個報告時，才能刪除報告。

1. 導覽至您的專案，然後從&#x200B;**整備**&#x200B;階段的&#x200B;**最佳實務分析**&#x200B;卡中，按一下&#x200B;**檢閱**。

   ![最佳實務分析 — 檢閱](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1a.png)

1. 按一下&#x200B;**...**。

   ![橢圓](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1.png)

1. 在下拉式清單中，按一下&#x200B;**檢視趨勢線**，如下圖所示。

   ![檢視趨勢線](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1b.png)

1. 從&#x200B;**趨勢線報告**&#x200B;畫面按一下刪除圖示。

   ![趨勢線報告 — 刪除](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view5a.png)

1. 按一下&#x200B;**刪除**&#x200B;以確認刪除。

   ![刪除](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view6a.png)

## 後續步驟 {#whats-next}

瞭解如何登入Cloud Acceleration Manager以及如何建立專案後，您現在已準備好繼續檢閱[實作階段](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-implementation-phase.html?lang=zh-Hant)的下一個步驟。
