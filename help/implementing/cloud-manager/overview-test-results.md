---
title: Cloud Manager測試概述
description: 概略了解Cloud Manager為確保自訂程式碼品質而自動執行的三種測試類型。
exl-id: 5f5c97b1-4180-4f49-af8b-257d4744766e
source-git-commit: a9303c659730022b7417fc9082dedd26d7cbccca
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---


# Cloud Manager測試概述 {#overview}

Cloud Manager支援的Cloud Services管道測試分為三類。

1. [程式碼品質測試](/help/implementing/cloud-manager/code-quality-testing.md)

   * 程式碼品質測試會評估應用程式程式碼的品質。
   * 在所有非生產和生產管道中，程式碼品質管道會在建置步驟後立即執行。
   * 此 [自訂程式碼品質規則](/help/implementing/cloud-manager/custom-code-quality-rules.md) 由Cloud Manager根據AEM Engineering的最佳實務而執行。

1. [功能測試](/help/implementing/cloud-manager/functional-testing.md)

   * 功能測試是生產管道階段測試階段的一部分。

1. [體驗稽核測試](/help/implementing/cloud-manager/experience-audit-testing.md)

   * 所有Cloud Manager生產管道中都會啟用體驗稽核測試，且無法略過。

這些測試可以是：

* 客戶撰寫
* Adobe寫入
* 使用開放原始碼工具建立

>[!NOTE]
>
> 客戶寫的測試和Adobe寫的測試都在為運行此類測試而設計的集裝箱化基礎架構中運行。
