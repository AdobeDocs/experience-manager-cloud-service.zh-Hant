---
title: AEM as a Cloud Service2022.5.0版中移轉工具發行說明
description: AEM as a Cloud Service2022.5.0版中移轉工具發行說明
feature: Release Information
exl-id: 1aa49e85-1914-44d9-bcf7-0a1b03926df0
source-git-commit: 8b7427ff99343741f62c7d0f42a6c4b3ea19bcb3
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 5%

---

# AEM as a Cloud Service2022.5.0版中移轉工具發行說明 {#release-notes}

此頁面概述AEM 2022.5.0中移轉工具的發行說明。

## Best Practices Analyzer {#bpa-release}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.30的發行日期為2022年6月1日。

### 新增功能 {#what-is-new-bpa}

* 可使用CoralUI和Classic對話介面工具集偵測自訂對話介面工具集的使用情況並製作報表。 建議將自訂的傳統對話Widget從ExtJS轉換為CoralUI。 自訂Coral Dialog Widget應更新至CoralUI3。
* 能夠偵測資產共用公域的使用情形和版本並製作報表。 AEMas a Cloud Service不支援Asset Share Commons 1.x，且必須升級至2.x。
* 能夠偵測並報告來自版本的節點數。
* 能夠檢測並報告已修改的自定義複製代理或現成可用的複製代理。

### 錯誤修正 {#bug-fixes-bpa}

* BPA報告了NCC（不相容的更改）、UMI（升級錯誤配置問題）和PCX（頁面複雜性）發現，這些結果是誤判的。 這些已修正。
* 當任何節點名稱長度超過150位元組時，BPA報告失敗。 此問題已經修正，僅當節點父路徑等於或大於350個位元組時，才會偵測到此類失敗。

## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt}

內容轉移工具2.0.10版的發行日期為2022年6月2日。

### 新增功能 {#what-is-new-ctt}

* 內容轉移工具(CTT)已改良為與Cloud Acceleration Manager搭配使用，以簡化整個內容轉移流程。 CTT現在著重於執行內容擷取。 CTT擷取服務現已整合至Cloud Acceleration Manager。 透過此演變提供的優點包括：
   * 自助式方式，只需擷取一次移轉集，並同時內嵌至多個環境。
   * 透過更佳的載入狀態、護欄和錯誤處理改善使用者體驗。
   * 擷取記錄會持續存在，且一律可供疑難排解。

## Cloud Acceleration Manager {#cam-release}

### 發行日期 {#release-date-cam}

Cloud Acceleration Manager的發行日期為2022年6月2日。

### 新增功能 {#what-is-new-cam}

* Cloud Acceleration Manager現在可讓使用者開始和管理內容傳輸，將內容從客戶的AEM例項（內部部署或Adobe Managed Services）移至AEMas a Cloud Service，作為移轉專案的一部分。 請參閱 [使用內容轉移卡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-implementation-phase.html#content-transfer) 以取得更多詳細資訊。
