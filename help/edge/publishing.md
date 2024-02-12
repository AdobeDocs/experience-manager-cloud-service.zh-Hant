---
title: 為 Edge Delivery Services 發佈內容
description: 了解內容發佈如何與 Edge Delivery Services 搭配使用，以及如何使用 Edge Delivery Services 發佈 AEM 內容。
feature: Edge Delivery Services
exl-id: 32fbb144-9175-47a9-bb5a-ca15f3fcd2d8
source-git-commit: daad30dd74d389c631131a77655c9fabf4ff2967
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 87%

---

# 為 Edge Delivery Services 發佈內容 {#publishing-edge}

使用 Edge Delivery Services 時，無論內容來源為何，都可以流暢地發佈內容：

* 文件型內容 - 請參閱 Edge Delivery Services 文件的[「發佈」區段](/help/edge/docs/authoring.md) 。
* AEM 內容 - 請參閱下面的詳細資訊。

## AEM 的發佈流程 {#publishing-flow}

使用 Universal Editor 編輯 AEM 內容時，發佈內容如同在 Universal Editor 點擊「**發佈**」按鈕一樣簡單。請參閱文件：[使用 Universal Editor 發佈內容。](/help/implementing/universal-editor/publishing.md)

在發佈時的資訊流程如下。一旦作者開始發佈，此流程就會自動進行，且此處有說明可供資訊參考。

>[!NOTE]
>
>每天最多允許從編寫UI或工作流程發佈5000個路徑。 不支援建立大量發佈工作載入的整合。

![從 AEM 發佈至 Edge Delivery Services 時的資訊流程](assets/publishing-flow.png)

1. 內容作者在 Universal Editor 中發布 AEM 內容。
1. 發布事件會被推送到 Adob&#x200B;&#x200B;e Pipeline 佇列。
1. Edge Delivery 發佈服務會將相關事件轉送到 Edge Delivery 管理 API。
1. Edge Delivery 會從 AEM Author 提取並擷取語義 HTML。
1. AEM 已更新發佈狀態。

## 如何開始使用 {#how-to-get-started}

請聯絡您的 Adob&#x200B;&#x200B;e 代表，要求使用此功能的存取權。
