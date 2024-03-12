---
title: 為 Edge Delivery Services 發佈內容
description: 了解內容發佈如何與 Edge Delivery Services 搭配使用，以及如何使用 Edge Delivery Services 發佈 AEM 內容。
feature: Edge Delivery Services
exl-id: 32fbb144-9175-47a9-bb5a-ca15f3fcd2d8
source-git-commit: 3ee1ba83518c3d4fba59b0c98b31e5c63a2eb6ab
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 66%

---


# 為 Edge Delivery Services 發佈內容 {#publishing-edge}

使用 Edge Delivery Services 時，無論內容來源為何，都可以流暢地發佈內容：

* 文件型內容 - 請參閱 Edge Delivery Services 文件的[「發佈」區段](/help/edge/docs/authoring.md) 。
* AEM 內容 - 請參閱下面的詳細資訊。

## AEM 的發佈流程 {#publishing-flow}

使用 Universal Editor 編輯 AEM 內容時，發佈內容如同在 Universal Editor 點擊「**發佈**」按鈕一樣簡單。請參閱文件：[使用 Universal Editor 發佈內容。](/help/sites-cloud/authoring/universal-editor/publishing.md)

在發佈時的資訊流程如下。一旦作者開始發佈，此流程就會自動進行，且此處有說明可供資訊參考。

>[!NOTE]
>
>每天最多允許從製作 UI 或按工作流程發佈 5000 個路徑。不支援建立大量發佈工作負載的整合。

![從 AEM 發佈至 Edge Delivery Services 時的資訊流程](assets/publishing-flow.png)

1. 內容作者在 Universal Editor 中發布 AEM 內容。
1. 發佈事件會推送至Adobe管道佇列。
1. Edge Delivery Services發佈服務會將相關事件轉送至Edge Delivery Services管理員API。
1. Edge傳送從AEM作者提取及擷取語意HTML。
1. AEM 已更新發佈狀態。

>[!NOTE]
>
>依預設，Edge Delivery Services管理員API不受保護，並且可用於發佈或取消發佈檔案而無需驗證。 為了設定管理員API的驗證，如中所述： [設定作者的驗證](https://www.aem.live/docs/authentication-setup-authoring)，您的專案必須布建API_KEY，以授與發佈服務的存取權。 [請聯絡Adobe團隊以瞭解Slack](/help/edge/docs/slack.md) 以取得指引。

## 如何開始使用 {#how-to-get-started}

請聯絡您的 Adob&#x200B;&#x200B;e 代表，要求使用此功能的存取權。
