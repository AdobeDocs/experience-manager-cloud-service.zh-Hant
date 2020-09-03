---
title: 測試結果概觀——雲端服務
description: 測試結果概觀——雲端服務
translation-type: tm+mt
source-git-commit: d03ef0afe91760e35ef4e8fb3e3f2c833cbf945c
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---


# 概覽 {#overview}

Cloud Manager for Cloud Services Pipeline支援的測試有三大類：

1. [程式碼品質測試](/help/implementing/cloud-manager/code-quality-testing.md)

   「程式碼品質測試」會評估您的應用程式碼的品質。 在所有非生產和生產管線中，在構建步驟之後立即執行代碼質量管線。

   Cloud Manager [所執行的「自訂程式碼品質規則](/help/implementing/cloud-manager/custom-code-quality-rules.md) 」是根據AEM Engineering的最佳實務建立。

1. [功能測試](/help/implementing/cloud-manager/functional-testing.md)

   功能測試是生產管道階段測試階段的一部分。

1. [體驗審核測試](/help/implementing/cloud-manager/experience-audit-testing.md)

   所有Cloud Manager生產管道中都啟用了「體驗審核測試」，不能跳過。

這些測試可以是：

* 客戶撰寫
* Adobe編寫
* 開放原始碼工具

   >[!NOTE]
   > 客戶撰寫的測試和Adobe撰寫的測試都可在專為執行這些類型測試而設計的容器化基礎架構中執行。

