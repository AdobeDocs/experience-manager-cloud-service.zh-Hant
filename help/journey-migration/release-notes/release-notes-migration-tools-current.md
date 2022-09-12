---
title: AEM as a Cloud Service2022.7.0版中移轉工具發行說明
description: AEM as a Cloud Service2022.7.0版中移轉工具發行說明
feature: Release Information
exl-id: 2f787321-f156-480d-bbe8-1a6d04f110c5
source-git-commit: ad9edf7bc164ea7e03496680dff8df6d1ebe266a
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 5%

---

# AEM as a Cloud Service2022.7.0版中移轉工具發行說明 {#release-notes}

此頁面概述AEM 2022.7.0中移轉工具的發行說明。

## Best Practices Analyzer {#bpa-release}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.30的發行日期為2022年7月27日。

### 新增功能 {#what-is-new-bpa}

* BPA現在可以檢測並報告可遷移的Lucene索引總大小，即Lucene索引總大小，不包括 `/oak:index/lucene` 和 `/oak:index/damAssetLucene`.
* BPA中新增的模式，可偵測自訂i18n字典的使用並製作報表。 AEMas a Cloud Service中無法使用Translator.html，且需透過Cloud Manager CI/CD管道從Git部署自訂i18n字典。

### 錯誤修正 {#bug-fixes-bpa}

* BPA回報內容片段遺失原始轉譯。 由於內容片段沒有轉譯，因此現在會針對內容片段略過此檢查。
* BPA UI中缺少篩選ACS公域結果的選項。 此問題已修正。

## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt}

內容轉移工具2.0.12版的發行日期為2022年7月19日。

### 新增功能 {#what-is-new-ctt}

* 透過LDAP登入的使用者現在可以執行CTT中的「檢查大小」和「使用者對應」功能。
* 為協助在擷取期間偵錯SSL/TLS連線問題，使用者現在可以啟用SSL記錄。
* 為協助偵錯來源連線問題，當連線至Azure失敗時，子網域名稱現在會列印在記錄中。
* 為了幫助在預複製期間調試問題，現在當預複製失敗時，AzCopy日誌會附加到提取日誌中。
* 為了避免過時的檢查大小結果，用戶只有在完成以前的檢查大小後才能重新運行檢查大小。

### 錯誤修正 {#bug-fixes-ctt}

* 刪除並重新建立移轉集後，會顯示先前的擷取記錄。 此問題已修正。
* 「查看進度」操作按鈕對於狀態為「已停止」的遷移集不可用。 此問題已修正。
* 提取金鑰過期的移轉集無法使用刪除動作按鈕。 此問題已修正。
* 修正多個UI錯誤。

## Cloud Acceleration Manager {#cam-release}

### 發行日期 {#release-date-cam}

Cloud Acceleration Manager的發行日期為2022年7月15日。

### 新增功能 {#what-is-new-cam}

* Cloud Acceleration Manager現在可讓使用者手動擷取移轉Token，以便在自動擷取失敗時開始擷取。 如果客戶已設定封鎖CAM的IP允許清單，或非管理員使用者嘗試開始擷取，自動擷取可能會失敗。 請參閱 [疑難排解](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#troubleshooting) 以取得更多資訊。
* 「移轉複雜性」頁面上的長表現在可以折疊，以方便使用。
