---
title: 測試結果概覽 — Cloud Services
description: 測試結果概覽 — Cloud Services
exl-id: 5f5c97b1-4180-4f49-af8b-257d4744766e
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# 概覽 {#overview}

Cloud Manager支援的Cloud Services管道測試有三大類別：

1. [程式碼品質測試](/help/implementing/cloud-manager/code-quality-testing.md)

   程式碼品質測試會評估應用程式程式碼的品質。 程式碼品質管道會在所有非生產和生產管道中，於建置步驟後立即執行。

   由Cloud Manager執行的[自訂程式碼品質規則](/help/implementing/cloud-manager/custom-code-quality-rules.md)是根據AEM Engineering的最佳實務所建立。

1. [功能測試](/help/implementing/cloud-manager/functional-testing.md)

   功能測試是生產管道階段測試階段的一部分。

1. [體驗稽核測試](/help/implementing/cloud-manager/experience-audit-testing.md)

   所有Cloud Manager生產管道都會啟用Experience Audit Testing，且無法略過。

這些測試可以是：

* 客戶撰寫
* Adobe寫入
* 開放原始碼工具

   >[!NOTE]
   > 客戶寫的測試和Adobe寫的測試都運行在專為運行這些類型的測試而設計的集裝箱基礎架構中。
