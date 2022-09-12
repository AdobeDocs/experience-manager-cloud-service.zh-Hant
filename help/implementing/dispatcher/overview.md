---
title: 內容傳遞流程概觀
description: 內容傳遞流程概觀
exl-id: fe42fb9e-cdf4-43e1-b688-7cecf4124fa5
source-git-commit: 60fc1b8f93c93ca427507dbe56511342f285e6bc
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 1%

---

# 內容傳遞流程 {#content-delivery}

目前頁面詳細說明AEMas a Cloud Service中的發佈服務內容傳送。 發佈服務內容傳送包括：

* CDN
* AEM dispatcher
* AEM發佈

資料流程如下：

1. URL會新增至瀏覽器
1. 向DNS中對應至該網域的CDN提出請求
1. 如果CDN已完全快取內容，CDN會將內容提供給瀏覽器
1. 如果未完全快取內容，CDN會呼叫（反向代理）給Dispatcher
1. 如果Dispatcher已完全快取內容，Dispatcher會將內容提供給CDN
1. 如果未完全快取內容，則Dispatcher會呼叫（反向Proxy）至AEM發佈
1. 內容由瀏覽器轉譯，瀏覽器也可根據標題快取

依預設，內容類型HTML/文字會設為在Dispatcher層300秒（5分鐘）後過期，此臨界值會同時受到Dispatcher快取和CDN的尊重。 在重新部署發佈服務期間，會清除Dispatcher快取，然後在新的發佈節點接受流量之前加熱。

以下章節提供內容傳送的更詳細資訊：
* [CDN設定](/help/implementing/dispatcher/cdn.md)
* [快取](/help/implementing/dispatcher/caching.md)


有關從作者服務復寫至發佈服務的資訊可供使用 [此處](/help/operations/replication.md).
