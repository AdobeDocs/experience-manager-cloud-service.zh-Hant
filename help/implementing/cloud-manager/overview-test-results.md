---
title: Cloud Manager 測試總覽
description: 大致了解 Cloud Manager 自動執行的三種類型的測試，以確保您的自訂程式碼的品質。
exl-id: 5f5c97b1-4180-4f49-af8b-257d4744766e
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 85%

---


# Cloud Manager 測試總覽 {#overview}

Cloud Manager for Cloud Services 管道支援三類測試。

1. [程式碼品質測試](/help/implementing/cloud-manager/code-quality-testing.md)

   * 程式碼品質測試會評估應用程式程式碼的品質。
   * 在所有生產和非生產管道中的建構步驟之後立即執行。
   * Cloud Manager 根據 AEM Engineering 的最佳實務執行的[自訂程式碼品質規則](/help/implementing/cloud-manager/custom-code-quality-rules.md)。

1. [功能測試](/help/implementing/cloud-manager/functional-testing.md)

   * 功能測試是的階段測試階段的一部分 [生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) 並可選擇屬於測試階段的一部分 [非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md).

1. [體驗稽核測試](/help/implementing/cloud-manager/experience-audit-testing.md)

   * 體驗審計測試在所有 Cloud Manager 生產管道中啟用，並且不能跳過。

這些測試可以是：

* 客戶撰寫
* Adobe 編寫的
* 使用開源工具建立

>[!NOTE]
>
> 客戶編寫的測試和 Adobe 編寫的測試都在為執行此類測試而設計的容器化基礎架構中執行。
