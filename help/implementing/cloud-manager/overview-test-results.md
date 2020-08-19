---
title: 測試結果概觀——雲端服務
description: 測試結果概觀——雲端服務
translation-type: tm+mt
source-git-commit: 25ba5798de175b71be442d909ee5c9c37dcf10d4
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 16%

---


# 概覽 {#overview}

使用 Cloud Manager 進行雲端服務管線執行時，會支援針對預備環境執行的測試。這與在「建立和裝置測試」步驟中執行的測試相反，這些測試會離線執行，而且無法存取任何執行中的AEM環境。

Cloud Manager for Cloud Services Pipeline支援的測試有三大類：

1. [程式碼品質測試](/help/implementing/cloud-manager/code-quality-testing.md)
1. [功能測試](/help/implementing/cloud-manager/functional-testing.md)
1. [內容審核測試](/help/implementing/cloud-manager/content-audit-testing.md)

這些測試可以是：

* 客戶撰寫
* Adobe編寫
* 開放原始碼工具（由Google的Lighthouse提供支援）

   >[!NOTE]
   > 客戶撰寫的測試和Adobe撰寫的測試都可在專為執行這些類型測試而設計的容器化基礎架構中執行。

