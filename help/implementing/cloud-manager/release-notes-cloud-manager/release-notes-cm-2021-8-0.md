---
title: AEM as a Cloud Service 版本 2021.8.0 中 Cloud Manager 的發行說明
description: AEM as a Cloud Service 版本 2021.8.0 中 Cloud Manager 的發行說明
feature: Release Information
exl-id: cf1d5c4f-404a-4ced-90f2-273c710adc0f
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 2021.8.0 中 Cloud Manager 的發行說明 {#release-notes}

本頁面總覽 AEM as a Cloud Service 2021.8.0 中 Cloud Manager 的發行說明

>[!NOTE]
>若要閱讀 Adobe Experience Manager as a Cloud Service 的目前發行說明，請按一下[此處](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=zh-Hant)。

## 發行日期 {#release-date}

AEM as a Cloud Service 2021.8.0 中的 Cloud Manager 發行日期是 2021 年 8 月 12 日。

### 新增功能 {#what-is-new}

* Cloud Service 客戶現在可以在 Cloud Manager 中檢視服務等級協定 (SLA) 報告。我們即將在未來幾個月以漸進方式推出這項功能。
如需了解更多，請參閱 [SLA 報告](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sla-reporting.html?lang=zh-Hant)。

* IndexType 和 `IndexDamAssetLucene` 品質規則的類型和嚴重性已變更。這兩個規則現在都歸類於「阻斷錯誤」*嚴重性*。

* 我們引進了新的 Oak 索引品質規則來涵蓋非同步和 Tika 設定。

* 將每個計劃的 SSL 憑證數上限增加到 50。

* 可讓使用者透過 Cloud Manager UI 建立及管理多個存放庫的自助式功能。

* SonarQube 之前會讀取 Git 記錄資料，這是不必要的。在大型計劃碼基底中，這可能會導致不必要的建置效能損失。

* 現在有一個 API 可讓每個管道的 Maven 相依性快取失效。

* Cloud Manager 使用的 AEM 專案原型版本已更新至版本 29。

### 錯誤修正 {#bug-fixes}

* 當最新版本低於目前版本時，不應顯示更新可用狀態。

* 名稱很長的新組織於初始入門時失敗。

* 有時，當管道由於某種原因被觸發兩次時，會導致其中一次執行失敗，並出現&#x200B;*無法更新管道執行狀態*&#x200B;錯誤。
