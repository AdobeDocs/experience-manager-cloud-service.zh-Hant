---
title: Cloud ManagerTest概述
description: 獲取Cloud Manager自動運行的三種test的概述，以確保自定義代碼的質量。
exl-id: 5f5c97b1-4180-4f49-af8b-257d4744766e
source-git-commit: a9303c659730022b7417fc9082dedd26d7cbccca
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---


# Cloud ManagerTest概述 {#overview}

Cloud Manager支援三種test，用於Cloud Services管道。

1. [代碼質量測試](/help/implementing/cloud-manager/code-quality-testing.md)

   * 代碼質量測試評估應用程式碼的質量。
   * 在所有非生產和生產管道中的生成步驟之後立即執行代碼質量管道。
   * 的 [自定義代碼質量規則](/help/implementing/cloud-manager/custom-code-quality-rules.md) 由Cloud Manager執行，基於工程部門的最佳實踐AEM建立。

1. [功能測試](/help/implementing/cloud-manager/functional-testing.md)

   * 功能測試是生產流水線階段測試階段的一部分。

1. [體驗審計測試](/help/implementing/cloud-manager/experience-audit-testing.md)

   * 在所有Cloud Manager生產管道中都啟用了體驗審核測試，因此無法跳過。

這些test可以是：

* 客戶編寫
* Adobe
* 使用開源工具建立

>[!NOTE]
>
> 客戶編寫的test和Adobe編寫的test都運行在為運行此類test而設計的集裝箱化基礎架構中。
