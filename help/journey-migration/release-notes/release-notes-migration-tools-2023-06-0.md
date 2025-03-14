---
title: AEM as a Cloud Service 2023.06.0版中移轉工具的發行說明
description: AEM as a Cloud Service 2023.06.0版中移轉工具的發行說明
feature: Release Information
exl-id: 021b7472-d1e4-4ef6-a040-c612fed8d3c3
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 3%

---

# AEM as a Cloud Service 2023.06.0版中移轉工具的發行說明 {#release-notes}

本頁面總覽AEM as a Cloud Service 2023.06.0中移轉工具的發行說明。

## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt}

內容轉移工具v2.0.20的發行日期為2023年6月8日。

### 新增功能 {#what-is-new-ctt}

* 新的移轉工具 — 內容轉換器(CT)已在此版本中整合內容轉移工具(CTT)。 在將內容從您目前的AEM實作(內部部署或Managed Services)移轉至AEM as a Cloud Service之前，內容轉換器可以自動偵測並修正[Best Practices Analyzer (BPA)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=zh-Hant)回報的內容相關問題。
內容轉換器提供的優點包括：
   * 防失敗：內容轉換器每次對存放庫進行修改以修正問題時，都會建立套件。 如有需要，您可以安裝套件以還原成先前的狀態。
   * 使用方便： Content Transformer已與Content Transfer Tool整合，並提供直覺式的簡單使用者介面。
   * 節省時間：當您的大量內容問題屬於一個模式類別時，您可以使用內容轉換器按幾下即可解決所有問題，大幅降低時間和移轉複雜性。
