---
title: Cloud Acceleration Manager中的實作階段
description: This page provides an overview on the implementation phase in Cloud Acceleration Manager.
source-git-commit: a6d225943c5d23ebd960fda0b0912a81f1f80014
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 2%

---

# Cloud Acceleration Manager中的實作階段 {#implementation-phase-cam}

The Implementation Phase includes:

* [地方開發](#local-development)
* [程式碼重構](#code-refactoring)
* [AEM as a Cloud Service Deployment](#aem-as-a-cloud-service-deployment)
* [內容轉移](#content-transfer)


按一下您的專案卡，開啟專案登陸頁面並導覽至 **實作** 部分，如下圖所示。

![影像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-1.png)

>[!NOTE]
>請參閱 [在Cloud Acceleration Manager中建立和管理專案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/getting-started-cam.html?lang=en#create-project) 了解更多。


## 使用本機開發卡 {#local-development}

The Local Development card provides all the relevant content that will help you setup your local AEM development environment as you start the Implementation phase of your migration journey.

請依照本節，探索「本機開發」活動卡：

1. Click on the **View** button from the **Local Development** card.

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-2.png)

1. 內容輪播會顯示移轉歷程這個階段的相關資訊。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-3.png)


## 使用程式碼重構卡 {#code-refactoring}

「程式碼重構」活動卡片提供所有相關資訊，並反白顯示移至AEMas a Cloud Service時，您需要檢閱和解決的程式碼重構區域。

請依照以下小節來探索「程式碼重構」活動卡：

1. 按一下 **檢閱** 按鈕 **程式碼重構** 活動卡。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-4.png)

1. The page displays the list of code refactoring activities organized by the severity level. You can learn more by clicking on the two highlighted icons.

   頁面會在三個不同的標籤中顯示程式碼重構考量事項：

   * 概覽
   * Dispatcher
   * 測試

>[!NOTE]
>請查看這些頁簽中的內容，了解Best Practices Analyzer未涵蓋的其他部分。

此 **Dispatcher** 標籤提供如何構建AEMas a Cloud ServiceApache和Dispatcher設定的資訊，以及如何在部署至雲端環境之前，在本機驗證和執行設定。 此外，也說明在雲端環境中進行除錯的方式。

![影像](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-2.png)

此 **測試** 索引標籤提供功能、體驗稽核和UI測試的相關資訊。

![影像](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-3.png)


## 使用AEMas a Cloud Service部署卡 {#aem-as-a-cloud-service-deployment}

AEM as a Cloud Service Deployment card provides all the relevant content that will help you deploy your code to AEM as a Cloud Service.

Follow this section to explore AEM as a Cloud Service Deployment Card activity card:

1. Click on the **View** button from the **AEM as a Cloud Service Deployment** activity card.

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-6.png)

1. A content carousel displays the relevant information for this phase of the migration journey.

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/aem-deployment-card.png)


## 使用內容轉移卡 {#content-transfer}

「內容轉移」活動卡片提供使用「內容轉移工具」將內容從您目前的AEM例項移至AEMas a Cloud Service時應審閱的指引和考量事項。

請依照以下章節，探索「內容轉移」活動卡：

1. 按一下 **檢視** 按鈕 **內容轉移** 活動卡。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-8.png)

1. 內容輪播會顯示移轉歷程這個階段的相關資訊。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/content-transfertool-card.png)

   >[!NOTE]
   >請查看 [必要條件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=en) 和 [最佳實務與准則](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en) 內容轉移工具前，請先確認。

### 預估內容轉移時間 {#calculating}

A new Content Transfer Tool calculator has been provided to estimate how long it could take to complete the content transfer activity. You can use the content repository size slider to select the size that applies to your project. 提取和擷取階段的傳輸時間會有所不同。

>[!NOTE]
>這些時候只是估計。 這些估計沒有考慮網路速度和擴展實例的時間等因素。

若要預估AEM存放庫的大小，您可以在 `http://HOST:PORT/etc/reports/diskusage.html`.

You can also estimate the size of specific repository paths by using the `path` parameter, for example, `http://HOST:PORT/etc/reports/diskusage.html?path=/content/dam`.

## 下一步 {#whats-next}

一旦您了解如何登入Cloud Acceleration Manager以及如何運用實作階段，現在就可以開始檢閱 [上線階段](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-golive-phase.html?lang=en).
