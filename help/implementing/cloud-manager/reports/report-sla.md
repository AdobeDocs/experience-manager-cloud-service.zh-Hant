---
title: SLA 報告
description: 瞭解如何檢視生產AEM環境相對於簽訂的Service level agreement的效能。
exl-id: 03932415-a029-4703-b44a-f86a87edb328
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 13%

---


# SLA報表 {#sla-reporting}

瞭解如何檢視生產AEM環境相對於簽訂的SLA (Service level agreement)的效能。

## 檢視SLA報表 {#introduction}

SLA報表資料會追蹤兩個生產階層的效能量度：製作階層和發佈階層。

所選年份的折線圖包含從1月至12月每個月的資料點。 會追蹤下列量度。

| 已追蹤的量度 | 線段色彩 | 說明 |
| --- | --- | --- |
| 作者層實際 | 淺綠色 | 對於由Adobe或Adobe的廠商引起的生產製作層級分解事故測量到的運作時間。 |
| 作者層合約 | 深藍色 | 您和Adobe的合約中為製作層級定義的SLA。 |
| 發佈層實際 | 橙色 | 測量的生產發佈層級運作時間，由Adobe或Adobe的廠商引起的客製化事件。 |
| 發佈層合約 | 紅色 | 您和Adobe的合約中為發佈層級定義的SLA。 |

**若要檢視SLA報告：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 在「**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**」控制台中，選取程式。

1. 從&#x200B;**計畫總覽**&#x200B;頁面，按一下左側功能表中的&#x200B;**報表**。

1. 按一下&#x200B;**SLA報表**。

   ![SLA報表折線圖](/help/implementing/cloud-manager/reports/assets/cm-sla-report2.png)

1. 按一下所需的年份，檢視SLA資料的線圖。

1. (選用) 執行以下任一操作：

   * 將游標捲動至折線圖的資料點上，以顯示該點的特定值。
   * 在折線圖的年份下方，按一下圖示&#x200B;**下載**&#x200B;以儲存折線圖的PNG影像檔案。
   * 按一下量度名稱即可檢視該量度的資料。 或者，在選取或取消選取一或多個量度名稱時，按鍵盤上的`Shift`。

## 事件分析 {#event-analysis}

在此圖表下的&#x200B;**事件分析**&#x200B;區段會顯示所選年度期間該方案發生的事故組合。

每個事故都有一個時間範圍、一個原因和一連串評論。

![事件分析範例](/help/implementing/cloud-manager/reports/assets/sla-reporting-c.png)

## 重新整理SLA報表的間隔 {#refresh}

SLA報告可讓您透過insight瞭解AEM生產環境的效能，且為最新狀態，但並非即時。 SLA報表產生每月進行，且會針對標示為`Production previous month`的新程式產生。 並非立即完成。 由於此延遲，檢閱SLA報表時請牢記下列事項：

* 報告的SLA是存在於月初的專案，即使SLA在該月有所變更。
* 如果月初沒有SLA因為方案不存在而存在，則會套用建立方案當日存在的SLA 。

## 預覽環境 {#preview}

預覽環境旨在作為內容作者在發佈之前驗證內容最終體驗的工具。 由於此功能，預覽環境在設計上並非採用高可用性，因此沒有相關聯的SLA。

