---
title: AEM as a Cloud Service2021.8.0版中Cloud Manager發行說明
description: AEM as a Cloud Service2021.8.0版中Cloud Manager發行說明
feature: Release Information
exl-id: cf1d5c4f-404a-4ced-90f2-273c710adc0f
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 4%

---

# Adobe Experience Manager as a Cloud Service 2021.8.0中的Cloud Manager發行說明 {#release-notes}

本頁概述AEM 2021.8.0as a Cloud Service版中Cloud Manager的發行說明。

>[!NOTE]
>若要查看最新的Adobe Experience Manager as a Cloud Service發行說明，請按一下 [此處](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html).

## 發行日期 {#release-date}

AEM 2021.8.0中的Cloud Manageras a Cloud Service日期為2021年8月12日。

### 新增功能 {#what-is-new}

* Cloud Service客戶現在可以在Cloud Manager中檢視「服務等級協定(SLA)」報表。 這將在今後幾個月內逐步提供。
請參閱 [SLA報告](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sla-reporting.html) 了解更多。

* IndexType和的類型和嚴重性 `IndexDamAssetLucene` 品質規則已變更。 這兩個都是Blocker的錯誤 *伺服器*.

* 已引入新的Oak索引品質規則，涵蓋非同步和tika設定。

* 將每個程式的SSL憑證上限提高至50個。

* 自助服務功能可讓使用者透過Cloud Manager UI建立和管理多個存放庫。

* SonarQube在不必要地閱讀Git歷史資料。 在大型程式碼基底中，這可能會導致不必要的組建效能損失。

* 現在有API可用來使每個管道的Maven相依性快取失效。

* Cloud Manager使用的AEM專案原型版本已更新為29版。

### 錯誤修正 {#bug-fixes}

* 最新版本小於目前版本時，不應顯示更新可用狀態。

* 名稱很長的新組織無法首次上線。

* 有時候，當管道因某些原因而觸發兩次時，會導致其中一個執行失敗 *無法更新管道執行狀態* 錯誤。
