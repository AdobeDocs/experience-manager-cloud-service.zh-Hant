---
title: AEM as aCloud Service中Cloud Manager的發行說明2021.8.0版
description: AEM as aCloud Service中Cloud Manager的發行說明2021.8.0版
feature: Release Information
source-git-commit: f9f24fb4cdf1a98aeb08248f027e2df40d844337
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 4%

---

# Adobe Experience Manager as aCloud Service2021.8.0中的Cloud Manager發行說明 {#release-notes}

本頁概述AEM as a 2021.8.0Cloud Service中Cloud Manager的發行說明。

>[!NOTE]
>若要查看Adobe Experience Manager as aCloud Service的最新發行說明，請按一下[here](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=zh-Hant)。

## 發行日期 {#release-date}

AEM as aCloud Service2021.8.0中的Cloud Manager發行日期為2021年8月12日。
下一版預計於2021年9月9日發行。

### 新增功能 {#what-is-new}

* Cloud Service客戶現在可以在Cloud Manager中檢視「服務等級協定(SLA)」報表。 這將在今後幾個月內逐步提供。
請參閱[SLA報告](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sla-reporting.html)以了解更多資訊。

* IndexType和`IndexDamAssetLucene`質量規則的類型和嚴重性已更改。 這兩個都是Blocker *serverity*&#x200B;的錯誤。

* 已引入新的Oak索引品質規則，涵蓋非同步和tika設定。

* 將每個程式的SSL憑證上限提高至50個。

* 自助服務功能可讓使用者透過Cloud Manager UI建立和管理多個存放庫。

* SonarQube在不必要地閱讀Git歷史資料。 在大型程式碼基底中，這可能會導致不必要的組建效能損失。

* 現在有API可用來使每個管道的Maven相依性快取失效。

* Cloud Manager使用的AEM專案原型版本已更新為29版。

### 錯誤修正 {#bug-fixes}

* 最新版本小於目前版本時，不應顯示更新可用狀態。

* 名稱很長的新組織無法首次上線。

* 有時，當管道因某些原因觸發兩次時，會導致其中一個執行失敗，並出現&#x200B;*無法更新管道執行狀態*&#x200B;錯誤。
