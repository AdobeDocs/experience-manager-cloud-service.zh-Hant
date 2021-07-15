---
title: Cloud Acceleration Manager中的實作階段
description: 本頁概述Cloud Acceleration Manager的實作階段。
source-git-commit: 83da3b647e47022a41160f2007d90dc7b23db671
workflow-type: tm+mt
source-wordcount: '689'
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
>請參考[在Cloud Acceleration Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/getting-started-cam.html?lang=en#create-project)中建立和管理專案以深入了解。


## 使用本機開發卡 {#local-development}

「本機開發」卡提供所有相關內容，可協助您在開始移轉歷程的「實作」階段時，設定本機AEM開發環境。

請依照本節，探索「本機開發」活動卡：

1. 按一下&#x200B;**Local Development**&#x200B;卡片中的&#x200B;**View**&#x200B;按鈕。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-2.png)

1. 內容輪播會顯示移轉歷程這個階段的相關資訊。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-3.png)


## 使用程式碼重構卡 {#code-refactoring}

「程式碼重構」活動卡片提供所有相關資訊，並反白顯示移至AEM as aCloud Service時，您需要檢閱和解決的程式碼重構區域。

請依照以下小節來探索「程式碼重構」活動卡：

1. 按一下&#x200B;**程式碼重構**&#x200B;活動卡片中的&#x200B;**檢閱**&#x200B;按鈕。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-4.png)

1. 頁面顯示依嚴重性層級組織的程式碼重構活動清單。 您可以按一下兩個醒目提示的圖示，以深入了解。

   頁面會在三個不同的標籤中顯示程式碼重構考量事項。

   * 概覽:
   * Dispatcher
   * 測試

   **概述**&#x200B;標籤會顯示程式碼重構活動的清單。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/coderefactoring-1.png)

   **Dispatcher**&#x200B;標籤提供如何將AEM建構為Cloud ServiceApache和Dispatcher設定的資訊，以及如何在部署至雲端環境之前，在本機驗證和執行它。 此外，也說明在雲端環境中進行除錯的方式。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/coderefactoring-2.png)

   **Testing**&#x200B;標籤提供功能、體驗稽核和UI測試的相關資訊。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/coderefactoring-3.png)


   >[!NOTE]
   >此外，請查看頁面標籤中的內容，了解Best Practices Analyzer未涵蓋的其他部分。


## 使用AEM作為Cloud Service部署卡 {#aem-as-a-cloud-service-deployment}

AEM as a Cloud Service部署卡提供所有相關內容，可協助您將程式碼部署至AEM as aCloud Service。

請依照以下小節，探索AEM as a Cloud Service部署卡活動卡：

1. 按一下&#x200B;**AEM as a Cloud Service部署**&#x200B;活動卡中的&#x200B;**View**&#x200B;按鈕。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-6.png)

1. 內容輪播會顯示移轉歷程這個階段的相關資訊。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/aem-deployment-card.png)


## 使用內容轉移卡 {#content-transfer}

「內容轉移」活動卡片提供使用「內容轉移工具」將內容從您目前的AEM例項移至AEM作為Cloud Service時，應審閱的指引和考量事項。

請依照以下章節，探索「內容轉移」活動卡：

1. 按一下&#x200B;**內容轉移**&#x200B;活動卡上的&#x200B;**檢視**&#x200B;按鈕。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-8.png)

1. 內容輪播會顯示移轉歷程這個階段的相關資訊。

   ![影像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/content-transfertool-card.png)

   >[!NOTE]
   >使用內容轉移工具之前，請先檢閱[必要條件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=en)及[最佳作法和准則](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en)。

### 預估內容轉移時間 {#calculating}

提供全新的內容轉移工具電腦，可估計完成內容轉移活動可能需要多久的時間。 您可以使用內容存放庫大小滑桿來選取套用至專案的大小。 提取和擷取階段的傳輸時間會有所不同。

>[!NOTE]
>這些時候只是估計。 這些估計沒有考慮網路速度和擴展實例的時間等因素。

要估計AEM儲存庫的大小，可以運行`http://HOST:PORT/etc/reports/diskusage.html`下的「磁碟使用情況」報告。

您也可以使用`path`參數（例如`http://HOST:PORT/etc/reports/diskusage.html?path=/content/dam`）來估計特定存放庫路徑的大小。

## 下一步 {#whats-next}

學習如何登入Cloud Acceleration Manager及如何運用實作階段後，您現在可以繼續檢閱[上線階段](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-golive-phase.html?lang=en)中的下一個步驟。
