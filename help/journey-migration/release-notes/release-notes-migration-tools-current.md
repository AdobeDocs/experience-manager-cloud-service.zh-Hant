---
title: AEMas a Cloud Service版2023.03.0中移轉工具發行說明
description: AEMas a Cloud Service版2022.03.0中移轉工具發行說明
feature: Release Information
exl-id: 2f787321-f156-480d-bbe8-1a6d04f110c5
source-git-commit: b2681113f5565e4f63c76abeaf46d5f4b1a8a8ea
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 5%

---

# AEMas a Cloud Service版2023.03.0中移轉工具發行說明 {#release-notes}

此頁面概述AEM 2022.03.0中移轉工具的發行說明。

## 最佳做法分析工具 {#bpa-release}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.40的發行日期為2023年3月3日。

### 新增功能 {#what-is-new-bpa}

* BPA現在可以檢測並報告發生衝突的節點 — 具有相同的節點 `jcr:uuid`. 這類發現被標為重要，因為在將內容移至AEMas a Cloud Service時，這可能導致內容擷取失敗。
* BPA現在可以偵測事件接聽程式的使用情況並製作報表。 建議您在移至AEM as a Cloud Service時，將此類型的事件處理機制重新調整為sling工作。

### 錯誤修正 {#bug-fixes-bpa}

* BPA報告誤判 `grouprendercondition`. 此問題已修正。

## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt}

內容轉移工具2.0.16版的發行日期為2022年3月8日。

### 新增功能 {#what-is-new-ctt}

* 使用者對應已簡化並整合至內容擷取步驟。 不需要任何設定，預設情況下，當使用者起始內容擷取時，會自動完成使用者對應。 如有需要，使用者可以選擇停用使用者對應。 深入了解 [這裡。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/user-mapping-and-migration.html?lang=en#user-mapping-detail)
* 預復步驟使用 [AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) 已與「內容轉移工具」整合，大幅加快內容擷取。 安裝此版本的CTT時，會自動設定並安裝Precopy。 預設情況下，提取開始時，會為大於200GB的遷移集自動運行預復。 使用者有權視需要停用。 深入了解 [這裡。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en)
* CTT現在可用於Windows伺服器。

### 錯誤修正 {#bug-fixes-ctt}

* 多項錯誤修正以改善內容擷取的彈性。
