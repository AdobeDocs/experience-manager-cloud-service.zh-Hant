---
title: AEMas a Cloud Service版2021.11.0中的Cloud Manager發行說明
description: AEMas a Cloud Service版2021.11.0中的Cloud Manager發行說明
feature: Release Information
source-git-commit: d6aa3097e558d4e78f20493f214167db57f1a013
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 2%

---

# Adobe Experience Manager as a Cloud Service 2021.11.0中的Cloud Manager發行說明 {#release-notes}

本頁概述AEM 2021.11.0中Cloud Manager的發行說明。

>[!NOTE]
>若要查看最新的Adobe Experience Manager as a Cloud Service發行說明，請按一下 [此處](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=zh-Hant).

## 發行日期 {#release-date}

AEMas a Cloud Service的Cloud Manager發行日期2021.11.0為2021年11月4日。
下一版預計於2021年12月16日發行。

### 新增功能 {#what-is-new}

* 使用者現在可以運用新的前端管道，以加速方式專門部署前端程式碼。 請參閱 [Cloud Manager前端管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) 了解更多。

   >[!IMPORTANT]
   >您必須使用AEM版本 `2021.10.5933.20211012T154732Z` 以利用新的前端管道。

* 以更有效的方式執行程式碼分析，而不需要建立整個AEM影像，可大幅縮短程式碼品質管道持續時間。 此變更將在發行後的數週內逐步推出。

* Git提交ID現在會顯示在管道執行詳細資訊中，以便更輕鬆追蹤已建置的程式碼。

* 現在可透過公開的API建立方案。

* 現在可透過公開的API建立環境。

* 此 `x-request-id` 回應標題現在會顯示在 [www.adobe.io](https://www.adobe.io/). 提交客戶服務問題以進行疑難排解時，此標題相當實用。

* 身為使用者，我看到管道為零的管道卡為我提供適當的指引。

* 現在提供新的「活動頁面」，供檢視活動（例如管道和程式碼執行）及其相關詳細資訊之用。 隨著時間推移，此頁面所列的活動將會擴展範圍以及提供的詳細資料。

* 提供新的管道頁面，可在暫留時顯示狀態彈出視窗，方便您檢視詳細資訊摘要。 可檢視管道執行及其相關聯的詳細資訊。

* 「編輯管道API」現在支援變更部署階段所使用的環境。

* 已針對大型封裝導入OakPal掃描程式的最佳化。

* 品質問題CSV檔案現在會包含每個品質問題的時間戳記。

### 錯誤修正 {#bug-fixes}

* 某些非正統的組建設定會導致管道的Maven工件快取中儲存不必要的檔案，導致在啟動和停止組建容器時產生多餘的網路I/O。

* 如果部署階段不存在，管道PATCHAPI就會失敗。

* 此 `ClientlibProxyResourceCheck` 當有具有共同基本路徑的用戶端程式庫時，品質規則會產生誤判問題。

* 達到最大儲存庫數時，錯誤訊息未指定錯誤的原因。

* 在少數情況下，管道由於某些回應代碼的重試處理不當而失敗。

