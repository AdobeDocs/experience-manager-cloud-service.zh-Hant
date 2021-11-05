---
title: 設定非生產管道
description: 請參照本頁面，了解如何在Cloud Manager中設定非生產管道
index: true
source-git-commit: 2ac65af4cf410491d1196b9e20f67647e0a1b4d1
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 0%

---


# 設定非生產管道 {#configure-non-production-pipeline}

除了部署至預備和生產的主要管道外，客戶還能設定額外的管道，稱為非生產管道。

非生產管道有兩種類型：

1. 程式碼品質：在Git分支的程式碼上執行程式碼品質掃描。 此管道會執行建置和程式碼品質步驟。
1. 部署：除了執行建置和程式碼品質步驟外，此管道還會將程式碼部署至選取的非生產環境至AEMas a Cloud Service環境。

## 新增非生產管道 {#adding-non-production-pipeline}

在主螢幕上，這些管道會列在新卡中：

1. 存取 **管道** Cloud Manager主畫面中的資訊卡。 按一下 **+添加** 選取 **新增非生產管道**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. **新增非生產管道**  對話框。 選取要建立的管線類型 **程式碼品質管道** 或 **部署管道**.

   >[!NOTE]
   >對於部署管道，必須選擇部署環境。

   此外，您也可以設定 **部署觸發程式** 和 **重要量度失敗行為** 從 **部署選項**. 按一下 **繼續**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add2.png)

   您可以定義下列部署觸發器以啟動管道。

   * **手動**  — 使用UI手動啟動管道。
   * **Git變更時**  — 每當有提交項新增至設定的git分支時，就會啟動CI/CD管道。 即使選取此選項，也始終可以手動啟動管道。

      在管道設定或編輯期間，部署管理器可以選擇在任何質量門中遇到重要故障時定義管道的行為。

      這對希望實現更自動化流程的客戶非常有用。 可用選項包括：
   您可以定義重要失敗量度行為以啟動管道。

   * **每次都問**  — 這是預設設定，需要手動干預任何「重要」故障。
   * **立即失敗**  — 如果選中，則每當出現「重要」(Important)故障時，管道將被取消。 這實質上是模擬用戶手動拒絕每個故障。
   * **立即繼續**  — 如果選中此選項，則每當出現「重要」故障時，管道將自動繼續。 這實際上是在模擬使用者手動核准每個失敗。


1. 選擇 **[完整堆疊程式碼](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline)** 或 **[前端代碼](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)**.

   如果您選取 **前端代碼**，您必須選取 **存放庫**, **Git分支** 和 **代碼位置**，如下圖所示：

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-confignew1.png)

   如果您選取 **完整堆疊程式碼**，您必須選取 **存放庫** 和 **Git分支**，如圖所示：
   ![](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-fullstack1.png)

   >[!IMPORTANT]
   >如果所選環境已存在完整堆棧代碼管道，則此選擇將被禁用。

   >[!NOTE]
   >開始配置前端管道之前，請參見 [AEM快速網站建立歷程](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites-journey/quick-site/overview.html) 透過簡單易用的AEM快速網站建立工具，提供端對端工作流程。 本檔案網站可協助您簡化AEM網站的前端開發，並在不具備AEM後端知識的情況下快速自訂網站。

1. 新建立的非生產管道現在會顯示在 **管道** 卡片。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-fullstack2.png)


   管道會顯示在主畫面的卡片上，包含四個動作，如下所示：

   * **新增**  — 允許添加新管道。
   * **全部顯示**  — 允許用戶查看所有管道。
   * **存取存放庫資訊**  — 可讓使用者取得存取Cloud Manager Git存放庫所需的資訊。
   * **更多詳情**  — 導覽至了解CI/CD管道檔案資源。