---
title: AEMas a Cloud Service2023.06.0版中移轉工具的發行說明
description: AEMas a Cloud Service2022.06.0版中移轉工具的發行說明
feature: Release Information
source-git-commit: 88227693b7dfc3cbd30751718dc85e55ee67bb96
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 2%

---

# AEMas a Cloud Service2023.06.0版中移轉工具的發行說明 {#release-notes}

本頁面總覽AEMas a Cloud Service2022.06.0中移轉工具發行說明。

## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt}

內容轉移工具v2.0.20的發行日期為2023年6月8日。

### 新增功能 {#what-is-new-ctt}

* 新的移轉工具 — 內容轉換工具(CT)已在此版本中與「內容轉移工具(CTT)」整合。 內容轉換工具可自動偵測並修正回報的相關內容問題。 [Best Practices Analyzer (BPA)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en) 將內容從您目前的AEM實作(內部部署或Managed Services)移轉至AEMas a Cloud Service之前。
內容轉換工具提供的優點包括：
   * 防故障：內容轉換器每次對存放庫進行修改以修復問題時，都會建立套件。 如有需要，您可以安裝套件以回覆成先前的狀態。
   * 易於使用： Content Transformer已與Content Transfer Tool整合，並提供直覺式的簡單使用者介面。
   * 節省時間：當大量內容問題屬於一個模式類別時，您只需使用內容轉換器按幾下即可解決所有問題，大幅降低時間和移轉複雜性。
