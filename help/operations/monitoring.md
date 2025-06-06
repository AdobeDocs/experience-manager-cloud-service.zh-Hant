---
title: AEM as a Cloud Service 中的基礎結構和服務監視
description: AEM as a Cloud Service 中的基礎結構和服務監視
exl-id: 82432c11-37ec-48ac-a52b-487abdc859fa
feature: Operations
role: Admin
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 5%

---

# AEM as a Cloud Service 中的基礎結構和服務監視 {#monitoring-in-aem-as-a-cloud-service}

Adobe Experience Manager as a Cloud Service提供基礎架構、服務和使用者體驗的可觀察性和監控。 由於使用了各種解決方案，且監控有數個層次，因此本頁面分為三個區段：

* [外部可用性](#external-availability)
* [內部模組監控](#module-monitoring)
* [客戶可觀察性](#customer-observability)

AEM as a Cloud Service使用數百台雲端原生監視器，一年365天持續報告每個環境的狀態(24/7)。 監視器定義不是靜態的，會持續檢閱以改進早期偵測功能。 此外，Adobe已設定隨叫隨到的程式來回應警示。

如果您需要其他監視型別(例如透過Cloud Manager的記錄或監視)的相關資訊，請參閱[其他資源](#resources)。

## 外部可用性 {#external-availability}

外部可用性由兩部分組成：服務Edge和自訂監視。

### 服務Edge {#service-edge}

您的所有AEM as a Cloud Service環境都會受到可用性監控。 不過，「服務Edge監控」僅針對生產環境設定，且量度會用於計算客戶的SLA。 這會考量到環境執行階段和AEM as a Cloud Service CDN。 服務Edge監控會採用離您所選地區較近的五個不同位置，並定期檢查可用性。 網站的不可用性會觸發警報，並讓Adobe的隨叫隨到支援團隊和程式參與互動。

### 自訂監視 {#custom-monitoring}

透過自訂監視，客戶可選擇在[上線](/help/journey-migration/go-live.md)之前提供最多五個不同的Web屬性URL。 這些URL應有效並傳回HTTP 200回應代碼。 這些監視器可支援以下客戶：[將自己的CDN](/help/implementing/dispatcher/cdn.md#point-to-point-CDN)帶到Adobe CDN前，以及在AEM as a Cloud Service前採用且未受Adobe控制的任何外部流量路由。 自訂監控檢查產生的警報會與Adobe的支援團隊和流程互動。

>[!NOTE]
>
> 此功能僅提供給具有[進階雲端支援](https://experienceleague.adobe.com/docs/support-resources/data-sheets/overview.html?lang=zh-Hant#support-add-ons)的生產環境和客戶。 如有任何問題，請聯絡您的Adobe客戶團隊。

## 內部模組監控 {#module-monitoring}

雖然外部可用性側重於使用者監控，但內部模組監控可觀察架構子系統是否名義上運作且功能或效能未降低。 如果發生問題，就會觸發警示，因此可自動進行修復，或透過作業團隊的參與進行修復，以防止可用性受損。 監視器有各種類別，下面顯示一些範例檢查：

* CPU iowait百分比不會超過特定臨界值。
* 執行個體重新部署不會超過特定頻率。
* 磁碟使用量低於某個臨界值。
* 作者存放庫大小在特定範圍內。
* 已成功完成備份作業。
* 資料庫健康狀況和效能受到監視。
* AEM雲端服務的運作如預期，包括沒有封鎖的復寫佇列、一致的資料和效能查詢。

為Forms布建的環境會新增其他檢查。 檢查定義不是靜態的，可能會變更和更新。

## 客戶可觀察性 {#customer-observability}

客戶可以使用[New Relic應用程式效能監視](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic.html?lang=zh-Hant)套裝，提供即時效能資料，收集並繪製圖表以供分析和疑難排解。 透過使用監控套件，客戶可以直接觀察各種量度，例如：JVM效能量度、Java™的交易時間、背景外部呼叫和資料庫呼叫。

## 其他資源 {#resources}

* [New Relic應用程式效能監視](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic.html?lang=zh-Hant)
* [正在記錄AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/logging.html?lang=zh-Hant)
* [監視環境](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/monitoring-environments.html?lang=zh-Hant)
