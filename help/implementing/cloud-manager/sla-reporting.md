---
title: SLA 報告
description: 了解如何查看生產 AEM 環境相對於簽訂的服務水平協議 (SLA) 的效能。
exl-id: 03932415-a029-4703-b44a-f86a87edb328
source-git-commit: f037f47f0b131c87301faf4458658224d1d62a43
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 55%

---


# SLA 報告 {#sla-reporting}

了解如何查看生產 AEM 環境相對於簽訂的服務水平協議 (SLA) 的效能。

## 簡介 {#introduction}

SLA 報告數據可透過&#x200B;**報告**&#x200B;標籤。請依照下列步驟進行存取。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 在 **[我的計畫](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)** 畫面選取程式。

1. 從&#x200B;**總覽**&#x200B;頁面瀏覽到&#x200B;**報告**&#x200B;索引標籤。

1. 按一下所需的年份以檢視繪製的SLA資料。

![SLA 圖案範例](assets/sla-reporting-1.png)

將滑鼠捲動到資料點上以顯示該點的特定值。

![顯示詳細資料](assets/sla-reporting-b.png)

## SLA 量度 {#sla-metrics}

所選年份的圖表包括數個資料集。

* **發布層級合約** - 這是您和 Adobe 的合約中為發佈層級定義的 SLA。

* **發布層級實際** - 這是對於由 Adobe 或 Adobe 的廠商引起的生產發佈層級分解事故測量到的運作時間。

* **作者層級合約**：這是您和 Adobe 的合約中為作者層級定義的 SLA。

* **作者層級實際** - 這是對於由 Adobe 或 Adobe 的廠商引起的生產作者層級分解事故測量到的運作時間。

## 事件分析 {#event-analysis}

在此圖表下的&#x200B;**事件分析**&#x200B;區段會顯示在選定年度期間該方案發生的事故組合。

每個事故都有一個時間範圍、一個原因和一連串評論。

![事件分析範例](assets/sla-reporting-c.png)

## 重新整理間隔 {#refresh}

SLA報告可讓您深入瞭解AEM生產環境的效能，並且是最新狀態，但不是即時的。 SLA報告產生每月進行，並且為上個月標籤為生產的新計畫產生。 並非立即完成。 由於此延遲，當您檢視SLA報告時，請牢記以下事項：

* 報告的SLA將是當月開始時存在的SLA，即使SLA在該月內有所變更。
* 如果月初沒有SLA，因為當時沒有程式，則會套用建立程式之日存在的SLA。

## 預覽環境 {#preview}

預覽環境旨在作為內容作者在發佈之前驗證內容最終體驗的工具。 因此，預覽環境在設計上沒有高可用性，也沒有相關聯的SLA。
