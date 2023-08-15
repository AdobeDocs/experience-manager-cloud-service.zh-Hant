---
title: Cloud Acceleration Manager中的實作階段
description: 本頁提供Cloud Acceleration Manager實作階段的概觀。
exl-id: e6ac88f0-4b3f-43a1-98bc-8c6608713784
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 7%

---

# Cloud Acceleration Manager中的實作階段 {#implementation-phase-cam}

實作階段包括：

* [本機開發](#local-development)
* [程式碼重構](#code-refactoring)
* [AEMas a Cloud Service部署](#aem-as-a-cloud-service-deployment)
* [內容轉移](#content-transfer)


按一下您的專案卡片，以便開啟專案登入頁面並導覽至 **實施** 部分，如下圖所示。

![影像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-1.png)

>[!NOTE]
>另請參閱 [在Cloud Acceleration Manager中建立和管理專案](getting-started-cam.md#create-project) 以進一步瞭解。


## 使用本機開發卡 {#local-development}

本機開發卡片提供所有相關內容，可協助您在開始移轉歷程的實施階段時設定本機AEM開發環境。

請依照本區段操作，以便探索本機開發活動卡：

1. 按一下 **檢視** 從 **本機開發** 卡片。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-2.png)

1. 內容輪播會顯示移轉歷程這個階段的相關資訊。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-3.png)


## 使用程式碼重構卡 {#code-refactoring}

「程式碼重構」活動卡片會提供所有相關資訊，並反白標示在移至AEMas a Cloud Service時要檢視和解決的程式碼重構區域。

請詳閱本節，以探索「程式碼重構」活動卡：

1. 按一下 **檢閱** 從 **程式碼重構** 活動卡片。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-4.png)

1. 頁面會顯示依嚴重性層級組織的程式碼重構活動清單。 您可以按一下兩個醒目提示的圖示以瞭解更多資訊。

   此頁面會在三個不同的標籤中顯示程式碼重構的考量事項：

   * 概觀
   * Dispatcher
   * 測試

>[!NOTE]
>檢閱這些標籤中的內容，瞭解Best Practices Analyzer未涵蓋的一些其他區域。

此 **Dispatcher** 索引標籤提供有關如何構建AEMas a Cloud Service的Apache和Dispatcher設定，以及如何在部署到雲端環境之前在本地驗證和執行它的資訊。 同時也說明如何在雲端環境中進行除錯。

![影像](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-2.png)

此 **測試** 索引標籤提供有關功能、體驗稽核和UI測試的資訊。

![影像](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-3.png)


## 使用AEMas a Cloud Service部署卡 {#aem-as-a-cloud-service-deployment}

AEMas a Cloud Service部署卡會提供所有相關內容，協助您將程式碼部署至AEMas a Cloud Service。

請依照本章節所述，以探索AEMas a Cloud Service部署卡活動卡：

1. 按一下 **檢視** 從 **AEMas a Cloud Service部署** 活動卡片。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-6.png)

1. 內容輪播會顯示移轉歷程這個階段的相關資訊。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/aem-deployment-card.png)


## 使用內容轉移卡 {#content-transfer}

「內容轉移」卡片可讓您開始並管理從目前AEM執行個體到AEMas a Cloud Service的內容轉移。

請依照本節，以便探索「內容轉移」活動卡：

1. 按一下 **檢閱** 從 **內容轉移** 活動卡片。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-1.png)

1. 若要開始內容轉移，您必須建立移轉集。 按一下 **建立移轉集**. 移轉集可讓內容傳輸至AEMas a Cloud Service。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-2.png)

   >[!NOTE]
   >移轉集會在長時間不活動後過期。 另請參閱 [移轉集到期](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) 以取得詳細資訊。

   >[!NOTE]
   >另請參閱 [必備條件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=zh-Hant) 和 [最佳作法和准則](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) 開始使用「內容轉移工具」。

1. 下載並安裝內容轉移工具以填入移轉集並完成內容轉移的提取階段。 檢閱 [內容轉移工具快速入門](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=zh-Hant) 以瞭解如何使用內容轉移工具。

1. 若要將內容從移轉集擷取至AEMas a Cloud Service上的環境，您必須開始擷取。 瀏覽至 **內嵌工作** 並按一下 **新內嵌**. 檢閱 [將內容內嵌至目標](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content.html) 以便您瞭解如何完成內容轉移的擷取階段。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-3.png)

<!--### Estimating Content Transfer Time {#calculating}

A Content Transfer Tool calculator has been provided to estimate how long it could take to complete the content transfer activity. You can use the content repository size slider to select the size that applies to your project. The transfer times vary for the extraction and ingestion phases. 

   ![image](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-4.png)

   >[!NOTE]
   >These times are estimates only. Factor such as network speeds and time to scale up instances have not been accounted for in these estimates.

To estimate the size of the AEM Repository, you can run the Disk Usage report under `http://HOST:PORT/etc/reports/diskusage.html`. 

You can also estimate the size of specific repository paths by using the `path` parameter, for example, `http://HOST:PORT/etc/reports/diskusage.html?path=/content/dam`. -->

## 下一步 {#whats-next}

在您瞭解如何登入Cloud Acceleration Manager以及如何使用實作階段後，您就可以開始檢視中的下一個步驟了 [上線階段](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-golive-phase.html).
