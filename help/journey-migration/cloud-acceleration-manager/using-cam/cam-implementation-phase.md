---
title: 雲加速管理器的實施階段
description: 本頁概述了Cloud Acceleration Manager中的實施階段。
exl-id: e6ac88f0-4b3f-43a1-98bc-8c6608713784
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 2%

---

# 雲加速管理器的實施階段 {#implementation-phase-cam}

實施階段包括：

* [地方發展](#local-development)
* [程式碼重構](#code-refactoring)
* [AEMas a Cloud Service部署](#aem-as-a-cloud-service-deployment)
* [內容轉移](#content-transfer)


按一下項目卡以開啟項目登錄頁並導航到 **實施** 的下界。

![影像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-1.png)

>[!NOTE]
>請參閱 [在雲加速管理器中建立和管理項目](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/getting-started-cam.html?lang=en#create-project) 來瞭解更多資訊。


## 使用本地開發卡 {#local-development}

「本地開發」卡提供所有相關內容，這些內容將幫助您AEM在開始遷移過程的「實施」階段時設定本地開發環境。

按照本節介紹「本地開發」活動卡：

1. 按一下 **視圖** 按鈕 **地方發展** 卡。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-2.png)

1. 內容傳送器顯示遷移過程的這一階段的相關資訊。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-3.png)


## 使用代碼重構卡 {#code-refactoring}

「代碼重構」活動卡提供了所有相關資訊，並突出顯示了在轉到AEMas a Cloud Service時需要檢查和解決的代碼重構區域。

按照本節瀏覽「代碼重構」活動卡：

1. 按一下 **審閱** 按鈕 **代碼重構** 活動卡。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-4.png)

1. 此頁顯示按嚴重性級別組織的代碼重構活動的清單。 按一下兩個突出顯示的表徵圖可瞭解更多資訊。

   該頁在三個不同的頁籤中顯示代碼重構注意事項：

   * 概覽
   * Dispatcher
   * 測試

>[!NOTE]
>請查看這些頁籤中的內容，瞭解最佳做法分析器未涵蓋的其他部分。

的 **調度程式** 頁籤提供有關如何構AEM造as a Cloud ServiceApache和Dispatcher配置的資訊，以及在部署到雲環境之前如何在本地驗證和運行它。 還介紹了在雲環境中的調試。

![影像](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-2.png)

的 **測試** 頁籤提供有關功能、體驗審核和UI測試的資訊。

![影像](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-3.png)


## 使用AEMas a Cloud Service部署卡 {#aem-as-a-cloud-service-deployment}

AEMas a Cloud Service部署卡提供所有相關內容，幫助您將代碼部署到AEMas a Cloud Service。

按照本部分瀏覽AEMas a Cloud Service部署卡活動卡：

1. 按一下 **視圖** 按鈕 **AEMas a Cloud Service部署** 活動卡。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-6.png)

1. 內容傳送器顯示遷移過程的這一階段的相關資訊。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/aem-deployment-card.png)


## 使用內容傳輸卡 {#content-transfer}

「內容傳輸」活動卡提供了使用內容傳輸工具將內容從當前實例移動到as a Cloud Service時應檢查AEM的指導AEM和注意事項。

按照本節來瀏覽內容傳輸活動卡：

1. 按一下 **視圖** 按鈕 **內容傳輸** 活動卡。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-8.png)

1. 內容傳送器顯示遷移過程的這一階段的相關資訊。

   ![影像](/help/journey-migration/cloud-acceleration-manager/assets/content-transfertool-card.png)

   >[!NOTE]
   >請查看 [先決條件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=en) 和 [最佳做法和准則](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en) 使用內容傳輸工具之前。

### 估計內容傳輸時間 {#calculating}

已提供一個新的內容傳輸工具計算器，用於估計完成內容傳輸活動可能需要多長時間。 可以使用內容儲存庫大小滑塊選擇適用於項目的大小。 對於提取和攝取階段，轉移時間不同。

>[!NOTE]
>這些時代只是估算。 這些估計中沒有考慮網路速度和擴展實例的時間等因素。

要估計儲存庫的大AEM小，可以在 `http://HOST:PORT/etc/reports/diskusage.html`。

您還可以使用 `path` 參數，例如 `http://HOST:PORT/etc/reports/diskusage.html?path=/content/dam`。

## 下一步是什麼 {#whats-next}

一旦您學會了如何登錄到Cloud Acceleration Manager以及如何利用實施階段，您現在就可以繼續查看中的下一步 [上線階段](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-golive-phase.html?lang=en)。
