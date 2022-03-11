---
title: Cloud Manager在as a Cloud Service版AEM2021.8.0中的發行說明
description: Cloud Manager在as a Cloud Service版AEM2021.8.0中的發行說明
feature: Release Information
exl-id: cf1d5c4f-404a-4ced-90f2-273c710adc0f
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 4%

---

# Adobe Experience Manager as a Cloud ServiceCloud Manager發行說明2021.8.0 {#release-notes}

本頁概述了as a Cloud Service2021.8.0中Cloud Manager的發行說明AEM。

>[!NOTE]
>要查看Adobe Experience Manager as a Cloud Service的當前發行說明，請按一下 [這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=zh-Hant)。

## 發行日期 {#release-date}

Cloud Manager在as a Cloud Service中的AEM發佈日期為2021年8月12日。

### 新增功能 {#what-is-new}

* Cloud Service客戶現在可以在雲管理器中查看服務級別協定(SLA)報告。 今後幾個月將逐步提供這種服務。
請參閱 [SLA報告](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sla-reporting.html) 來瞭解更多資訊。

* IndexType和的類型和嚴重性 `IndexDamAssetLucene` 質量規則已更改。 這兩個都是Blocker的錯誤 *服務*。

* 新的Oak指數質量規則已經引入，涵蓋非同步和tika配置。

* 將每個程式的最大SSL證書數增加到50。

* 自助服務功能，允許用戶通過Cloud Manager UI建立和管理多個儲存庫。

* SonarQube在不必要地讀取Git歷史資料。 在大代碼庫中，這可能導致不必要的生成效能損失。

* 現在有一個API可用於使每個管道的Maven依賴性快取無效。

* Cloud Manager使用的AEM項目原型版本已更新為版本29。

### 錯誤修正 {#bug-fixes}

* 當最新版本小於當前版本時，不應顯示「更新可用」狀態。

* 對於名字很長的新組織來說，最初的入職失敗。

* 有時，當管道由於某種原因被觸發兩次時，會導致其中一個執行失敗 *無法更新管道執行狀態* 錯誤。
