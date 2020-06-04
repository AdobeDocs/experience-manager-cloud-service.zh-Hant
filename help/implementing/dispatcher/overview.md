---
title: 內容傳送流程概觀
description: 內容傳送流程概觀
translation-type: tm+mt
source-git-commit: 0080ace746f4a7212180d2404b356176d5f2d72c
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---


# 內容傳送流程 {#content-delivery}

目前的頁面詳細資訊會在AEM中以Cloud Service的形式發佈服務內容傳送。 發佈服務內容傳送包括：

* CDN
* AEM Dispatcher
* AEM發佈

資料流程如下：

1. URL會新增至瀏覽器
1. 對DNS中對應至該網域的CDN提出請求
1. 如果內容已完全快取到CDN,CDN會將內容提供給瀏覽器
1. 如果內容未完全快取，CDN會呼叫（反向proxy）給分派程式
1. 如果內容已完全快取在Dispatcher上，則Dispatcher會將內容提供給CDN
1. 如果內容未完全快取，則分派程式會呼叫（反向proxy）至AEM發佈
1. 內容由瀏覽器轉譯，瀏覽器也會快取內容，視標題而定

依預設，內容類型HTML/text會設為在分派程式層的300秒（5分鐘）後過期，而分派程式快取和CDN都會遵守此臨界值。 在重新部署發佈服務期間，會清除調度器快取，然後在新的發佈節點接受通信之前預熱。

以下各節提供內容傳送的更詳細資訊，包括CDN設定和快取。

有關從作者服務複製到發佈服務的資訊，請參 [閱](/help/operations/replication.md)。
