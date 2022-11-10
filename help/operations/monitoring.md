---
title: AEMas a Cloud Service的基礎架構與服務監控
description: AEMas a Cloud Service的基礎架構與服務監控
source-git-commit: 8121d2e9cd98b4cc6e848f6cd6c3fa4359988053
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 0%

---


# AEMas a Cloud Service的基礎架構與服務監控 {#monitoring-in-aem-as-a-cloud-service}

Adobe Experience Manager as a Cloud Service提供可觀察性和監控：基礎架構、服務和使用者體驗。 由於使用了各種解決方案，而且有數個監控層，因此本頁面會組織為三個區段：

* [外部可用性](#external-availability)
* [內部模組監控](#module-monitoring)
* [客戶可觀察性](#customer-observability)

AEM as a Cloud Service每年會使用數百個雲端原生監視器，持續報告每(24/7)環境的狀態365天。 監視器定義不是靜態的，會持續審查，以改善早期偵測功能。 此外，Adobe還設定了應對警報的呼叫過程。

如果您需要其他監視類型的相關資訊，例如透過Cloud Manager進行記錄或監視，請參閱 [其他資源](#resources) 區段。

## 外部可用性 {#external-availability}

外部可用性由兩部分組成：服務邊緣和自訂監控。

### 服務邊緣 {#service-edge}

所有AEMas a Cloud Service環境都會受到監控以取得可用性。 不過，服務邊緣監控僅針對生產環境設定，而量度則用於計算客戶的SLA。 這會考量環境執行階段和AEMas a Cloud ServiceCDN。 「服務邊緣監控」採用五個與您所選區域相鄰的不同位置，並定期檢查可用性。 網站無法使用會觸發警報，並吸引Adobe的電話支援團隊和流程。

### 自訂監視 {#custom-monitoring}

透過自訂監控，客戶可以選擇在之前提供最多五個不同的Web屬性URL [正式啟用](/help/journey-migration/go-live.md). 這些URL應有效，並傳回HTTP 200回應代碼。 這些監視器可支援 [自攜CDN](/help/implementing/dispatcher/cdn.md#point-to-point-CDN) 在AdobeCDN之前，以及AEMas a Cloud Service之前採用且不受Adobe控制的任何外部流量路由。 自訂監控檢查產生的警報將吸引Adobe的支援團隊和程式。

## 內部模組監控 {#module-monitoring}

雖然外部可用性主要集中在最終用戶監控上，但內部模組監控會觀察體系結構子系統是否在名義上運行，而沒有功能或效能降低。 在出現問題時，會觸發警報，以便自動或通過運營團隊的參與進行修復，以防止損壞的可用性。 監視器有不同類別，以下是一些示例檢查：

* CPU超時百分比未超過某個閾值。
* 執行個體重新部署不會超過特定頻率。
* 磁碟使用量低於某個閾值。
* 製作存放庫大小在特定範圍內。
* 備份操作已成功完成。
* 監控資料庫運行狀況和效能。
* AEM雲端服務的運作如預期，包括未封鎖的復寫佇列、一致的資料和效能查詢。

已新增其他檢查至針對Forms布建的環境。 請記住，檢查定義不是靜態的，且可能會有所變更和更新。

## 客戶可觀察性 {#customer-observability}

客戶可使用 [新的Relic應用程式效能監控](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic.html) 提供即時效能資料的套裝，可收集資料並繪製圖表以進行分析和疑難排解。 透過使用監控套裝，客戶可以直接觀察各種量度，例如：JVM效能度量、Java的事務時間、後台外部調用和資料庫調用。

## 其他資源 {#resources}

* [新的Relic應用程式效能監控](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic.html)
* [記錄AEMas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/logging.html)
* [監視環境](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/monitoring-environments.html)
