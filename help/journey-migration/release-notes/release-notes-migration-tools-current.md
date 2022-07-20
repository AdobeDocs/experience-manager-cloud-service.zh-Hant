---
title: 《 2022.7.0版中遷移工具AEM發行說明》
description: 《 2022.7.0版中遷移工具AEM發行說明》
feature: Release Information
source-git-commit: f84327096951772e1bed8656334841e1292d6bcf
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 4%

---

# 《 2022.7.0版中遷移工具AEM發行說明》 {#release-notes}

本頁概述了as a Cloud Service2022.7.0中遷移工具的AEM發行說明。

## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt}

內容傳輸工具v2.0.12的發佈日期為2022年7月19日。

### 新增功能 {#what-is-new-ctt}

* 通過LDAP登錄的用戶現在可以在CTT中運行「檢查大小」和「用戶映射」功能。
* 為幫助調試提取期間的SSL/TLS連接問題，用戶現在可以啟用SSL日誌記錄。
* 為幫助調試源連接問題，當連接到Azure失敗時，子域名現在將打印在日誌中。
* 為幫助調試預複製期間的問題，當預複製失敗時，AzCopy日誌現在會附加到抽取日誌中。
* 為避免過時的「檢查大小」結果，只有在完成以前的「檢查大小」後，用戶才能重新運行「檢查大小」。

### 錯誤修正 {#bug-fixes-ctt}

* 刪除並重新建立遷移集後，將出現以前的提取日誌。 這個已經修復了。
* 「查看進度」操作按鈕對於狀態為「已停止」的遷移集不可用。 這個已經修復了。
* 刪除操作按鈕對於具有過期提取鍵的遷移集不可用。 這個已經修復了。
* 修復了多個UI錯誤。

## 雲加速管理器 {#cam-release}

### 發行日期 {#release-date-cam}

Cloud Acceleration Manager的發佈日期為2022年7月15日。

### 新增功能 {#what-is-new-cam}

* Cloud Acceleration Manager現在允許用戶手動檢索遷移令牌，以便在自動檢索失敗時能夠啟動攝取。 如果客戶設定了阻止CAM的IP允許清單，或非管理員用戶嘗試啟動攝取，自動檢索可能會失敗。 請參閱 [故障排除](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#troubleshooting) 的子菜單。
* 「遷移複雜性」頁上的長表現在可折疊，以方便使用。

