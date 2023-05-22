---
title: AEM as a Cloud Service 中的基礎結構和服務監視
description: AEM as a Cloud Service 中的基礎結構和服務監視
exl-id: 82432c11-37ec-48ac-a52b-487abdc859fa
source-git-commit: f55439552e253b8b71b40525454130c6f163e6d4
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 5%

---

# AEM as a Cloud Service 中的基礎結構和服務監視 {#monitoring-in-aem-as-a-cloud-service}

Adobe Experience Manager as a Cloud Service提供可觀察性和監控：基礎架構、服務和用戶體驗。 由於使用了各種解決方案，並且有多個監控層，因此本頁分為三部分：

* [外部可用性](#external-availability)
* [內部模組監控](#module-monitoring)
* [客戶可觀性](#customer-observability)

AEMas a Cloud Service使用數百個雲本地監視器連續報告每個環境的狀態(24/7)，每年365天。 監視器定義不是靜態的，它們會不斷被審查以改進早期檢測能力。 此外，Adobe還設定了響應警報的呼叫過程。

如果您需要有關其他類型的監視（如通過雲管理器進行日誌記錄或監視）的資訊，請參閱 [其他資源](#resources) 的子菜單。

## 外部可用性 {#external-availability}

外部可用性由兩部分組成：服務邊緣和自定義監視。

### 服務邊緣 {#service-edge}

您的所有AEMas a Cloud Service環境都受到可用性監控。 但是，服務邊緣監控僅針對生產環境設定，並且度量用於計算客戶的SLA。 它考慮了環境運行AEM時和as a Cloud ServiceCDN。 服務邊緣監控採用五個與您所選區域相鄰的不同位置，並定期檢查可用性。 站點的不可用將觸發警報，並會與Adobe的呼叫支援團隊和流程接洽。

### 自定義監視 {#custom-monitoring}

通過自定義監視，客戶可以選擇在以前最多提供五個不同的Web屬性URL [活](/help/journey-migration/go-live.md)。 這些URL應有效並返回HTTP 200響應代碼。 這些顯示器支援客戶 [自帶CDN](/help/implementing/dispatcher/cdn.md#point-to-point-CDN) 在AdobeCDN前面，以及在不受Adobe控制的AEMas a Cloud Service前面使用的任何外部流量路由。 自定義監控檢查產生的警報將與Adobe的支援團隊和流程接洽。

>[!NOTE]
>
> 此功能僅面向具有 [高級雲支援。](https://experienceleague.adobe.com/docs/support-resources/data-sheets/overview.html#support-add-ons) 如果您有任何問題，請通過管理控制台提出支援案例。

## 內部模組監視 {#module-monitoring}

雖然外部可用性側重於最終用戶監控，但內部模組監控會觀察體系結構子系統在名義上是否運行而沒有功能或效能降級。 在出現問題時，會觸發警報，以便可以自動或通過操作團隊的參與進行維修，以防止損壞的可用性。 監視器有多種類別，下面是一些示例檢查：

* CPUiowait百分比未超過某個閾值。
* 實例重新部署不超過特定頻率。
* 磁碟使用率低於某個閾值。
* 作者儲存庫大小在一定範圍內。
* 備份操作已成功完成。
* 監視資料庫運行狀況和效能。
* AEM雲服務的運行情況如預期，包括沒有阻止的複製隊列、一致的資料和效能查詢。

為Forms預配的環境添加了其他檢查。 請記住，檢查定義不是靜態的，會隨著更改和更新而改變。

## 客戶可觀性 {#customer-observability}

客戶可以 [New Relic應用程式效能監控](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic.html) 提供即時效能資料收集和圖表以便分析和故障排除的套件。 通過使用監控套件，客戶可以直接觀察各種指標，如：JVM效能度量、Java的事務時間、後台外部調用和資料庫調用。

## 其他資源 {#resources}

* [New Relic應用程式效能監控](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic.html)
* [記錄AEMas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/logging.html)
* [監視環境](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/monitoring-environments.html)
