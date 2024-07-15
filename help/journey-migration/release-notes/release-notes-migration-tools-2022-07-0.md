---
title: AEM as a Cloud Service 2022.7.0版中移轉工具的發行說明
description: AEM as a Cloud Service 2022.7.0版中移轉工具的發行說明
feature: Release Information
exl-id: bc8f1a80-867e-423a-9c03-4a53b1ebc57c
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 5%

---

# AEM as a Cloud Service 2022.7.0版中移轉工具的發行說明 {#release-notes}

本頁面總覽AEM as a Cloud Service 2022.7.0中移轉工具的發行說明。

## 最佳做法分析工具 {#bpa-release}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.30的發行日期為2022年7月27日。

### 新增功能 {#what-is-new-bpa}

* BPA現在可以偵測和報告總計可移轉Lucene索引大小，也就是不包括`/oak:index/lucene`和`/oak:index/damAssetLucene`的總計Lucene索引。
* BPA新增了新模式，可偵測和報告自訂i18n字典的使用情況。 AEM as a Cloud Service中不提供Translator.html，且必須透過Cloud Manager CI/CD管道從Git部署自訂i18n字典。

### 錯誤修正 {#bug-fixes-bpa}

* BPA報告缺少內容片段的原始轉譯。 由於內容片段沒有轉譯，因此內容片段的這項檢查現已跳過。
* BPA UI中缺少篩選ACS Commons發現的選項。 此問題已修正。

## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt}

內容轉移工具v2.0.12的發行日期為2022年7月19日。

### 新增功能 {#what-is-new-ctt}

* 透過LDAP登入的使用者現在可以在CTT中執行「檢查大小」和「使用者對應」功能。
* 為協助在擷取期間偵錯SSL/TLS連線問題，使用者現在可以啟用SSL記錄。
* 為協助偵錯來源連線問題，當與Azure的連線失敗時，子網域名稱現在會列印在記錄中。
* 為協助偵錯預先複製期間的問題，現在當預先複製失敗時，AzCopy記錄會附加至擷取記錄。
* 為了避免過時的「檢查大小」結果，使用者只能在先前「檢查大小」完成後重新執行「檢查大小」。

### 錯誤修正 {#bug-fixes-ctt}

* 刪除並重新建立移轉集後出現先前的擷取記錄。 此問題已修正。
* 檢視進度動作按鈕不適用於狀態為「已停止」的移轉集。 此問題已修正。
* 刪除動作按鈕無法用於具有過期擷取金鑰的移轉集。 此問題已修正。
* 已修正多個UI錯誤。

## Cloud Acceleration Manager {#cam-release}

### 發行日期 {#release-date-cam}

Cloud Acceleration Manager的發行日期為2022年7月15日。

### 新增功能 {#what-is-new-cam}

* Cloud Acceleration Manager現在可讓使用者手動擷取移轉Token，以便在自動擷取失敗時開始內嵌。 如果客戶已設定封鎖CAM的IP允許清單，或如果非管理員使用者嘗試開始內嵌，則自動擷取可能會失敗。 如需詳細資訊，請參閱[疑難排解](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#troubleshooting)。
* 「移轉複雜性」頁面上的長表格現在可以摺疊，以方便使用。
