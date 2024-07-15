---
title: AEM as a Cloud Service 2022.5.0版中移轉工具的發行說明
description: AEM as a Cloud Service 2022.5.0版中移轉工具的發行說明
feature: Release Information
exl-id: 1aa49e85-1914-44d9-bcf7-0a1b03926df0
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 5%

---

# AEM as a Cloud Service 2022.5.0版中移轉工具的發行說明 {#release-notes}

本頁面總覽AEM as a Cloud Service 2022.5.0中移轉工具的發行說明。

## 最佳做法分析工具 {#bpa-release}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.30的發行日期為2022年6月1日。

### 新增功能 {#what-is-new-bpa}

* 能夠使用CoralUI和Classic對話方塊Widget偵測及報告自訂對話方塊Widget的使用情況。 建議您將自訂Classic對話方塊Widget從ExtJS轉換為CoralUI。 自訂Coral對話方塊Widget應更新為CoralUI3。
* 能夠偵測並報告Assets Share Commons的使用情況和版本。 AEM as a Cloud Service不支援Asset Share Commons 1.x，且必須升級至2.x。
* 能夠偵測和報告版本中的節點數量。
* 能夠偵測和報告自訂復寫代理程式或已修改的現成復寫代理。

### 錯誤修正 {#bug-fixes-bpa}

* BPA報告誤報的NCC （不相容變更）、UMI （升級設定錯誤問題）和PCX （頁面複雜性）發現。 這些問題已修正。
* 當任何節點名稱長度超過150個位元組時，BPA會報告失敗。 這已修正為僅當節點父路徑等於或大於350位元組時偵測此類失敗。

## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt}

內容轉移工具v2.0.10的發行日期為2022年6月2日。

### 新增功能 {#what-is-new-ctt}

* 內容轉移工具(CTT)已經過改良，可與Cloud Acceleration Manager搭配使用，以精簡整個內容轉移程式。 CTT現在專注於執行內容擷取。 CTT擷取服務現在已整合至Cloud Acceleration Manager。 透過此演化提供的優點包括：
   * 自助式方式擷取一次移轉集，並同時將其擷取至多個環境中。
   * 透過更好的載入狀態、護欄和錯誤處理，改善使用者體驗。
   * 內嵌記錄會持續存在，並隨時可用於疑難排解。

## Cloud Acceleration Manager {#cam-release}

### 發行日期 {#release-date-cam}

Cloud Acceleration Manager的發行日期為2022年6月2日。

### 新增功能 {#what-is-new-cam}

* Cloud Acceleration Manager現在可讓使用者開始和管理內容轉移，以將內容從客戶的AEM例項(內部部署或AdobeManaged Services)移至AEM as a Cloud Service，作為移轉專案的一部分。 如需詳細資訊，請參閱[使用內容轉移卡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-implementation-phase.html#content-transfer)。
