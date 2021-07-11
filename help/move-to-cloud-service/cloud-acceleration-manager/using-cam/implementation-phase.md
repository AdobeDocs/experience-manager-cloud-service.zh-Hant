---
title: Cloud Acceleration Manager中的實作階段
description: 本頁概述Cloud Acceleration Manager的實作階段。
hide: true
hidefromtoc: true
index: false
source-git-commit: 8063afa2df9f5007f686afcc4162abde56c188ef
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 2%

---


# Cloud Acceleration Manager中的實作階段 {#implementation-phase-cam}

實作階段包括：

* [地方開發](#local-development)
* [程式碼重構](#code-refactoring)
* [AEM as a Cloud Service部署](#aem-as-a-cloud-service-deployment)
* [內容轉移](#content-transfer)


按一下您的專案卡片以開啟專案登錄頁面，並導覽至&#x200B;**實作**&#x200B;區段，如下圖所示。

![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-1.png)

>[!NOTE]
>請參考[在Cloud Acceleration Manager](/help/move-to-cloud-service/cloud-acceleration-manager/using-cam/getting-started-cam.md)中建立和管理專案以深入了解。


## 使用本機開發卡 {#local-development}

「本機開發」卡提供所有相關內容，可協助您在開始移轉歷程的「實作」階段時，設定本機AEM開發環境。

請依照本節，探索「本機開發」活動卡：

1. 按一下&#x200B;**Local Development**&#x200B;卡片中的&#x200B;**View**&#x200B;按鈕。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-2.png)

1. 隨即顯示內容輪播，其中包含移轉歷程這個階段的相關資訊。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-3.png)


## 使用程式碼重構卡 {#code-refactoring}

「程式碼重構」活動卡片提供所有相關資訊，並反白顯示移至AEM as aCloud Service時需要檢閱的程式碼重構區域。

請依照以下小節來探索「程式碼重構」活動卡：

1. 按一下&#x200B;**程式碼重構**&#x200B;活動卡片中的&#x200B;**檢閱**&#x200B;按鈕。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-4.png)

1. 頁面顯示依嚴重性層級組織的程式碼重構活動清單。 您可以按一下兩個醒目提示的圖示，以深入了解。

   >[!NOTE]
   >此外，請查看頁面標籤中的內容，了解Best Practices Analyzer未涵蓋的其他部分。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-5.png)


## 使用AEM作為Cloud Service部署卡 {#aem-as-a-cloud-service-deployment}

AEM as a Cloud Service部署卡提供所有相關內容，可協助您將程式碼部署至AEM as aCloud Service。

請依照以下小節，探索AEM as a Cloud Service部署卡活動卡：

1. 按一下&#x200B;**AEM as a Cloud Service部署**&#x200B;活動卡中的&#x200B;**View**&#x200B;按鈕。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-6.png)

1. 隨即顯示內容輪播，其中包含移轉歷程這個階段的相關資訊。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/aem-deployment-card.png)


## 使用內容轉移卡 {#content-transfer}

「內容轉移」活動卡片提供使用「內容轉移工具」將內容從您目前的AEM例項移至AEM作為Cloud Service時，應審閱的指引和考量事項。

請依照以下章節，探索「內容轉移」活動卡：

1. 按一下&#x200B;**內容轉移**&#x200B;活動卡上的&#x200B;**檢視**&#x200B;按鈕。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-8.png)

1. 隨即顯示內容輪播，其中包含移轉歷程這個階段的相關資訊。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/content-transfertool-card.png)

   >[!NOTE]
   >使用內容轉移工具之前，請先檢閱[必要條件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=en)及[最佳作法和准則](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en)。

### 預估內容轉移工具活動 {#calculating}

提供全新的內容轉移工具電腦，可估計完成內容轉移活動可能需要多久的時間。 您可以使用內容存放庫大小滑桿來選取套用至專案的大小。 提取和擷取階段的傳輸時間會有所不同。

要估計AEM儲存庫的大小，可以運行`http://HOST:PORT/etc/reports/diskusage.html`下的「磁碟使用情況」報告。

您也可以使用`path`參數（例如`http://HOST:PORT/etc/reports/diskusage.html?path=/content/dam`）來估計特定存放庫路徑的大小。

## 下一步 {#whats-next}

一旦您了解如何登入Cloud Acceleration Manager及如何運用「實作」階段，您現在就可以繼續檢閱下一個步驟：使用「GoLive」階段。
