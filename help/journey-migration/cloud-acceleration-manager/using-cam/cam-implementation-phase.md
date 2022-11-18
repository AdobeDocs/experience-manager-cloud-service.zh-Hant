---
title: Cloud Acceleration Manager中的實作階段
description: 本頁概述Cloud Acceleration Manager的實作階段。
exl-id: e6ac88f0-4b3f-43a1-98bc-8c6608713784
source-git-commit: dbf01e5bd9ee83e378b4297d2f3d341d548f9238
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 2%

---

# Cloud Acceleration Manager中的實作階段 {#implementation-phase-cam}

實作階段包括：

* [地方開發](#local-development)
* [程式碼重構](#code-refactoring)
* [AEMas a Cloud Service部署](#aem-as-a-cloud-service-deployment)
* [內容轉移](#content-transfer)


按一下您的專案卡，開啟專案登陸頁面並導覽至 **實作** 部分，如下圖所示。

![影像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-1.png)

>[!NOTE]
>請參閱 [在Cloud Acceleration Manager中建立和管理專案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/getting-started-cam.html?lang=en#create-project) 了解更多。


## 使用本機開發卡 {#local-development}

「本機開發」卡提供所有相關內容，可協助您在開始移轉歷程的「實作」階段時，設定本機AEM開發環境。

請依照本節，探索「本機開發」活動卡：

1. 按一下 **檢視** 按鈕 **地方開發** 卡片。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-2.png)

1. 內容輪播會顯示移轉歷程這個階段的相關資訊。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-3.png)


## 使用程式碼重構卡 {#code-refactoring}

「程式碼重構」活動卡片提供所有相關資訊，並反白顯示移至AEM as a Cloud Service時，您需要檢閱和解決的程式碼重構區域。

請依照以下小節來探索「程式碼重構」活動卡：

1. 按一下 **檢閱** 按鈕 **程式碼重構** 活動卡。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-4.png)

1. 頁面顯示依嚴重性層級組織的程式碼重構活動清單。 您可以按一下兩個醒目提示的圖示，以深入了解。

   頁面會在三個不同的標籤中顯示程式碼重構考量事項：

   * 概觀
   * Dispatcher
   * 測試

>[!NOTE]
>請查看這些頁簽中的內容，了解Best Practices Analyzer未涵蓋的其他部分。

此 **Dispatcher** 標籤提供如何構建AEMas a Cloud ServiceApache和Dispatcher設定的資訊，以及如何在部署至雲端環境之前，在本機驗證和執行設定。 此外，也說明在雲端環境中進行除錯的方式。

![影像](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-2.png)

此 **測試** 索引標籤提供功能、體驗稽核和UI測試的相關資訊。

![影像](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-3.png)


## 使用AEMas a Cloud Service部署卡 {#aem-as-a-cloud-service-deployment}

AEMas a Cloud Service部署卡提供所有相關內容，可協助您將程式碼部署至AEMas a Cloud Service。

請依照本節所述，探索AEMas a Cloud Service部署卡活動卡：

1. 按一下 **檢視** 按鈕 **AEMas a Cloud Service部署** 活動卡。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-6.png)

1. 內容輪播會顯示移轉歷程這個階段的相關資訊。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/aem-deployment-card.png)


## 使用內容轉移卡 {#content-transfer}

「內容轉移」卡片可讓您開始及管理從目前的AEM例項到AEMas a Cloud Service的內容轉移。

請依照以下章節，探索「內容轉移」活動卡：

1. 按一下 **檢閱** 按鈕 **內容轉移** 活動卡。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-1.png)

1. 若要開始內容轉移，您需要建立移轉集。 按一下 **建立移轉集**. 移轉集可讓內容轉移至AEMas a Cloud Service。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-2.png)

   >[!NOTE]
   >請查看 [必要條件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=en) 和 [最佳實務與准則](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en) 內容轉移工具前，請先確認。

1. 您需要下載並安裝「內容轉移工具」，以填入移轉集並完成內容轉移的提取階段。 檢閱 [內容轉移工具快速入門](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en) 了解如何使用「內容轉移工具」。

1. 若要從AEMas a Cloud Service的移轉集擷取內容至環境，您需要開始擷取。 導覽至 **擷取工作** 按一下 **新擷取**. 檢閱 [將內容擷取至Target](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content.html?lang=en) 了解如何完成內容轉移的擷取階段。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-3.png)

<!--### Estimating Content Transfer Time {#calculating}

A Content Transfer Tool calculator has been provided to estimate how long it could take to complete the content transfer activity. You can use the content repository size slider to select the size that applies to your project. The transfer times vary for the extraction and ingestion phases. 

   ![image](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-4.png)

   >[!NOTE]
   >These times are estimates only. Factor such as network speeds and time to scale up instances have not been accounted for in these estimates.

To estimate the size of the AEM Repository, you can run the Disk Usage report under `http://HOST:PORT/etc/reports/diskusage.html`. 

You can also estimate the size of specific repository paths by using the `path` parameter, for example, `http://HOST:PORT/etc/reports/diskusage.html?path=/content/dam`. -->

## 下一步 {#whats-next}

一旦您了解如何登入Cloud Acceleration Manager以及如何運用實作階段，現在就可以開始檢閱 [上線階段](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-golive-phase.html?lang=en).
