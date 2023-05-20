---
title: 《 2023.03.0版中遷移工具AEM發行說明》
description: 《 2022.03.0版中遷移工具AEM發行說明》
feature: Release Information
exl-id: 2f787321-f156-480d-bbe8-1a6d04f110c5
source-git-commit: b2681113f5565e4f63c76abeaf46d5f4b1a8a8ea
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 5%

---

# 《 2023.03.0版中遷移工具AEM發行說明》 {#release-notes}

本頁概述了as a Cloud Service2022.03.0中遷移工具的AEM發行說明。

## 最佳做法分析工具 {#bpa-release}

### 發行日期 {#release-date-bpa}

最佳做法分析器2.1.40版的發佈日期為2023年3月3日。

### 新增功能 {#what-is-new-bpa}

* BPA現在可以檢測並報告衝突節點 — 具有相同的節點 `jcr:uuid`。 此類發現被標籤為關鍵，因為當將內容移動到as a Cloud Service時，它可能導致內容攝取AEM失敗。
* BPA現在可以檢測並報告事件偵聽器的使用情況。 建議將這種事件處理機制重新考慮為在移至AEMas a Cloud Service時吊掛作業。

### 錯誤修正 {#bug-fixes-bpa}

* BPA報告誤報 `grouprendercondition`。 這個已經修復了。

## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt}

內容傳輸工具v2.0.16的發佈日期為2022年3月8日。

### 新增功能 {#what-is-new-ctt}

* 用戶映射已簡化並整合到內容提取步驟中。 不需要設定，預設情況下，當用戶啟動內容提取時將自動完成用戶映射。 如果需要，用戶可以選擇禁用用戶映射。 瞭解更多資訊 [給。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/user-mapping-and-migration.html?lang=en#user-mapping-detail)
* 預複製步驟使用 [可用區複製](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) 已與內容傳輸工具整合，以顯著加快內容提取。 安裝此版本的CTT時，會自動配置並安裝預拷貝。 預設情況下，在啟動提取時，預拷貝將自動為大於200GB的遷移集運行。 用戶可以根據需要禁用它。 瞭解更多資訊 [給。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en)
* CTT現在可在Windows伺服器上使用。

### 錯誤修正 {#bug-fixes-ctt}

* 多個錯誤修復程式，可提高內容提取恢復能力。
