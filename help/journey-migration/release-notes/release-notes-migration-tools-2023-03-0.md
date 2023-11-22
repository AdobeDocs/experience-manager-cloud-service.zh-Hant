---
title: AEMas a Cloud Service版本2023.03.0中移轉工具的發行說明
description: AEMas a Cloud Service版本2023.03.0中移轉工具的發行說明
feature: Release Information
exl-id: cdc57cca-e10a-4b0d-b803-910ccc9350a6
source-git-commit: d7e5a14c2dfee41b4ab5af733218fe58d17871fa
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 5%

---

# AEMas a Cloud Service版本2023.03.0中移轉工具的發行說明 {#release-notes}

本頁面總覽AEMas a Cloud Service2023.03.0中移轉工具發行說明。

## 最佳做法分析工具 {#bpa-release}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.40的發行日期為2023年3月3日。

### 新增功能 {#what-is-new-bpa}

* BPA現在可以偵測並報告衝突的節點，也就是具有相同的節點 `jcr:uuid`. 這類發現會被標籤為嚴重，因為將內容移至AEMas a Cloud Service時，可能會導致內容擷取失敗。
* BPA現在可以偵測並報告事件接聽程式的使用情形。 建議在移至AEMas a Cloud Service時，將此型別的事件處理機制重構為Sling工作。

### 錯誤修正 {#bug-fixes-bpa}

* BPA回報的誤報 `grouprendercondition`. 此問題已修正。

## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt}

內容轉移工具v2.0.16的發行日期為2023年3月8日。

### 新增功能 {#what-is-new-ctt}

* 使用者對應已經過簡化，並整合至內容擷取步驟。 不需要任何設定，預設情況下，當使用者起始內容擷取時，會自動完成使用者對應。 如有需要，使用者可以選擇停用使用者對應。 瞭解更多 [此處。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/user-mapping-and-migration.html?lang=en#user-mapping-detail)
* 使用的預先複製步驟 [AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) 已與內容轉移工具整合，以大幅加快內容擷取速度。 安裝此CTT版本時，會自動設定並安裝預先複製。 根據預設，在起始擷取作業時，將會對大於200 GB的移轉集自動執行預先複製。 使用者可以選擇視需要將其停用。 瞭解更多 [此處。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en)
* CTT現在可用於Windows伺服器。

### 錯誤修正 {#bug-fixes-ctt}

* 多個錯誤修正，以改善內容擷取恢復能力。
