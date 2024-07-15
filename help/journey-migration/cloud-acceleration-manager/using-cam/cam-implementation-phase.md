---
title: Cloud Acceleration Manager中的實作階段
description: 本頁提供Cloud Acceleration Manager實施階段的概觀。
exl-id: e6ac88f0-4b3f-43a1-98bc-8c6608713784
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 5%

---

# Cloud Acceleration Manager中的實作階段 {#implementation-phase-cam}

實作階段包括：

* [本機開發](#local-development)
* [程式碼重構](#code-refactoring)
* [AEM as a Cloud Service 部署](#aem-as-a-cloud-service-deployment)
* [內容轉移](#content-transfer)


按一下您的專案卡片，以便您可以開啟專案登入頁面，並導覽至&#x200B;**實作**&#x200B;區段，如下圖所示。

![影像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-1.png)

>[!NOTE]
>請參閱[在Cloud Acceleration Manager中建立和管理專案](getting-started-cam.md#create-project)以瞭解更多資訊。


## 使用本機開發卡 {#local-development}

本機開發卡片提供所有相關內容，可協助您在開始移轉歷程的實施階段時設定本機AEM開發環境。

請依照本區段操作，以便探索本機開發活動卡：

1. 從&#x200B;**本機開發**&#x200B;卡片按一下&#x200B;**檢視**。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-2.png)

1. 內容輪播會顯示移轉歷程這個階段的相關資訊。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-3.png)


## 使用程式碼重構卡 {#code-refactoring}

「程式碼重構」活動卡片會提供所有相關資訊，並反白標示在移至AEM as a Cloud Service時需檢視和解決的程式碼重構區域。

請詳閱本節，以探索「程式碼重構」活動卡：

1. 從&#x200B;**程式碼重構**&#x200B;活動卡中，按一下&#x200B;**檢閱**。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-4.png)

1. 頁面會顯示依嚴重性層級組織的程式碼重構活動清單。 您可以按一下兩個醒目提示的圖示以瞭解更多資訊。

   此頁面會在三個不同的標籤中顯示程式碼重構的考量事項：

   * 概觀
   * Dispatcher
   * 測試

>[!NOTE]
>檢閱這些標籤中的內容，瞭解Best Practices Analyzer未涵蓋的一些其他區域。

**Dispatcher**&#x200B;索引標籤提供如何建構AEM as a Cloud Service Apache和Dispatcher設定，以及如何在部署至雲端環境之前，先在本機驗證和執行設定的相關資訊。 同時也說明如何在雲端環境中進行除錯。

![影像](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-2.png)

**測試**&#x200B;索引標籤提供功能、體驗稽核和UI測試的資訊。

![影像](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-3.png)


## 使用AEM as a Cloud Service部署卡 {#aem-as-a-cloud-service-deployment}

AEM as a Cloud Service部署卡片提供所有相關內容，可協助您將程式碼部署至AEM as a Cloud Service。

請依照本章節所述，探索AEM as a Cloud Service部署卡片活動卡：

1. 從&#x200B;**AEM as a Cloud Service部署**&#x200B;活動卡中，按一下&#x200B;**檢視**。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-6.png)

1. 內容輪播會顯示移轉歷程這個階段的相關資訊。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/aem-deployment-card.png)


## 使用內容轉移卡 {#content-transfer}

「內容轉移」卡片可讓您開始並管理從目前AEM執行個體到AEM as a Cloud Service的內容轉移。

請依照本節，以便探索「內容轉移」活動卡：

1. 從&#x200B;**內容轉移**&#x200B;活動卡按一下&#x200B;**檢閱**。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-1.png)

1. 若要開始內容轉移，您必須建立移轉集。 按一下&#x200B;**建立移轉集**。 移轉集可讓內容傳輸至AEM as a Cloud Service。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-2.png)

   >[!NOTE]
   >移轉集會在長時間不活動後過期。 如需詳細資訊，請參閱[移轉集到期日](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry)。

   >[!NOTE]
   >使用「內容轉移工具」之前，請先參閱[必要條件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html)以及[最佳實務和指導方針](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html)。

1. 下載並安裝內容轉移工具以填入移轉集並完成內容轉移的提取階段。 檢閱[內容轉移工具快速入門](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=zh-Hant)以瞭解如何使用內容轉移工具。

1. 若要將內容從移轉集內嵌至AEM as a Cloud Service上的環境，您必須開始內嵌。 導覽至&#x200B;**擷取工作**，然後按一下&#x200B;**新增擷取**。 檢閱[將內容擷取至Target](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)，以瞭解如何完成內容轉移的擷取階段。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-3.png)

<!--### Estimating Content Transfer Time {#calculating}

A Content Transfer Tool calculator has been provided to estimate how long it could take to complete the content transfer activity. You can use the content repository size slider to select the size that applies to your project. The transfer times vary for the extraction and ingestion phases. 

   ![image](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-4.png)

   >[!NOTE]
   >These times are estimates only. Factor such as network speeds and time to scale up instances have not been accounted for in these estimates.

To estimate the size of the AEM Repository, you can run the Disk Usage report under `http://HOST:PORT/etc/reports/diskusage.html`. 

You can also estimate the size of specific repository paths by using the `path` parameter, for example, `http://HOST:PORT/etc/reports/diskusage.html?path=/content/dam`. -->

## 下一步 {#whats-next}

在您瞭解如何登入Cloud Acceleration Manager以及如何使用實作階段後，您就可以繼續檢閱[上線階段](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-golive-phase.html)的下一個步驟了。
