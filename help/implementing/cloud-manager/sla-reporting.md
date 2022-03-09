---
title: SLA報告
description: 瞭解如何查看您的生產環AEM境相對於合同服務級別協定(SLA)的效能。
exl-id: 03932415-a029-4703-b44a-f86a87edb328
source-git-commit: 6cf164093cc543fe4847859b248e70efd86efbb1
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# SLA報告 {#sla-reporting}

瞭解如何查看您的生產環AEM境相對於合同服務級別協定(SLA)的效能。

## 簡介 {#introduction}

SLA報告資料可通過 **報告** 頁籤。 按照以下步驟訪問。

1. 登錄到Cloud Manager(位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇相應的組織和程式。

1. 導航到 **報告** 的 **概述** 的子菜單。

1. 按一下所需年份，查看SLA資料圖表。

![SLA圖示例](assets/sla-reporting-1.png)

將游標置於資料點上，以顯示該點的特定值。

![顯示詳細資料](assets/sla-reporting-b.png)

## SLA度量 {#sla-metrics}

所選年份的圖形包括多個資料集。

* **發佈層合同**  — 這是您的合同中為發佈層定義的AdobeSLA。

* **發佈層實際**  — 這是由Adobe或Adobe供應商引起的生產發佈層代理事件的正常運行時間。

* **作者層合同**  — 這是您在合同中為作者層定義的AdobeSLA。

* **作者層實際**  — 這是由Adobe或Adobe供應商引起的生產作者層代理事件的正常運行時間。

## 事件分析 {#event-analysis}

的 **事件分析** 圖表下的部分顯示了在選定年份中為程式發生的事件集。

每個事件都有一個時間範圍、一個原因和一組注釋。

![事件分析示例](assets/sla-reporting-c.png)
