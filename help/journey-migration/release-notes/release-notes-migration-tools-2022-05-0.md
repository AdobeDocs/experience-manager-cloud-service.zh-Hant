---
title: 《 2022.5.0版中遷移工具AEM發行說明》
description: 《 2022.5.0版中遷移工具AEM發行說明》
feature: Release Information
source-git-commit: 6196f3fc67dbcfe03a71bb6a0796dd5d1d0f8546
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 5%

---

# 《 2022.5.0版中遷移工具AEM發行說明》 {#release-notes}

本頁概述了as a Cloud Service2022.5.0中遷移工具的AEM發行說明。

## 最佳做法分析器 {#bpa-release}

### 發行日期 {#release-date-bpa}

最佳做法分析器2.1.30版的發佈日期為2022年6月1日。

### 新增功能 {#what-is-new-bpa}

* 能夠使用CoralUI和Classic對話框小部件檢測並報告自定義對話框小部件的使用情況。 建議將自定義經典對話框小部件從ExtJS轉換為CoralUI。 應將自定義Coral對話框小部件更新為CoralUI3。
* 能夠檢測並報告資產共用公域的使用和版本。 as a Cloud Service不支援資產共用公AEM域1.x，必須升級到2.x。
* 能夠檢測和報告版本中的節點數。
* 能夠檢測並報告已修改的自定義複製代理或出廠預裝的複製代理。

### 錯誤修正 {#bug-fixes-bpa}

* BPA正在報告誤報的NCC（非相容更改）、 UMI（升級錯誤配置問題）和PCX（頁面複雜性）發現。 這些都修好了。
* 當任何節點名稱長度超過150位元組時，BPA報告失敗。 這已被修復，只有當節點父路徑等於或大於350位元組時，才能檢測此類故障。

## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt}

內容傳輸工具v2.0.10的發佈日期為2022年6月2日。

### 新增功能 {#what-is-new-ctt}

* 內容傳輸工具(CTT)已經改進為與Cloud Acceleration Manager協作，以簡化整個內容傳輸過程。 CTT現在側重於執行內容提取。 CTT接收服務現已整合到Cloud Acceleration Manager中。 通過此演變提供的好處包括：
   * 一種自助式方法，可以一次提取遷移集，並將其並行地接收到多個環境中。
   * 通過更好的載入狀態、護欄和錯誤處理改善用戶體驗。
   * 攝取日誌被保留，並且始終可用於故障排除。

## Cloud Acceleration Manager {#cam-release}

### 發行日期 {#release-date-cam}

Cloud Acceleration Manager的發佈日期為2022年6月2日。

### 新增功能 {#what-is-new-cam}

* Cloud Acceleration Manager現在為用戶提供了啟動和管理內容傳輸的功能，以將內容從客戶實例AEM（本地或Adobe托管服務）移動到as a Cloud Service，作為遷移項AEM目的一部分。 請參閱 [使用內容傳輸卡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-implementation-phase.html#content-transfer) 的子菜單。
