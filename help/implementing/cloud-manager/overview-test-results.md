---
title: Cloud Manager 測試總覽
description: 大致了解 Cloud Manager 自動執行的三種類型的測試，以確保您的自訂計劃碼的品質。
exl-id: 5f5c97b1-4180-4f49-af8b-257d4744766e
source-git-commit: a9303c659730022b7417fc9082dedd26d7cbccca
workflow-type: ht
source-wordcount: '154'
ht-degree: 100%

---


# Cloud Manager 測試總覽 {#overview}

Cloud Manager for Cloud Services 管道支援三類測試。

1. [計劃碼品質測試](/help/implementing/cloud-manager/code-quality-testing.md)

   * 計劃碼品質測試會評估應用計劃計劃碼的品質。
   * 在所有生產和非生產管道中的建構步驟之後立即執行。
   * Cloud Manager 根據 AEM Engineering 的最佳實務執行的[自訂計劃碼品質規則](/help/implementing/cloud-manager/custom-code-quality-rules.md)。

1. [功能測試](/help/implementing/cloud-manager/functional-testing.md)

   * 功能測試是生產管道測試階段的一部分。

1. [體驗稽核測試](/help/implementing/cloud-manager/experience-audit-testing.md)

   * 體驗審計測試在所有 Cloud Manager 生產管道中啟用，並且不能跳過。

這些測試可以是：

* 客戶撰寫
* Adobe 編寫的
* 使用開源工具建立

>[!NOTE]
>
> 客戶編寫的測試和 Adobe 編寫的測試都在為執行此類測試而設計的容器化基礎架構中執行。
