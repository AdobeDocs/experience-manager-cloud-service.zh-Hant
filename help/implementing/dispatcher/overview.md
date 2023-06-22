---
title: 內容傳遞流程概觀
description: 內容傳遞流程概觀
exl-id: fe42fb9e-cdf4-43e1-b688-7cecf4124fa5
source-git-commit: f0edd0e3deeba89dcbd2dc1a07859138b24e2220
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 48%

---

# 內容傳遞流程 {#content-delivery}

目前頁面詳細說明 AEM as a Cloud Service 中的發佈服務內容傳遞。發佈服務內容傳遞包括：

* CDN
* AEM傳送器
* AEM發行者

資料流如下所示：

1. 已在瀏覽器中新增 URL
1. 己要求 CDN，其在 DNS 中對應至該網域
1. 如果內容完全快取在 CDN 上，CDN 會將其提供給瀏覽器
1. 如果內容未完全快取，CDN會呼叫Dispatcher （反向Proxy）
1. 如果Dispatcher已完全快取內容，Dispatcher會將其提供給CDN
1. 如果內容未完全快取，Dispatcher會呼叫（反向Proxy）到AEM發佈
1. 內容由瀏覽器呈現，瀏覽器也可能快取它，視標頭而定

根據預設，內容型別HTML/文字會設定為Dispatcher層級300秒（5分鐘）後過期，這是Dispatcher快取和CDN都遵循的臨界值。 在重新部署發佈服務期間，Dispatcher快取會遭到清除，並在新發佈節點接受流量之前暖和。

以下章節提供有關內容傳送的更多詳細資料：
* [CDN 設定](/help/implementing/dispatcher/cdn.md)
* [快取](/help/implementing/dispatcher/caching.md)


關於從作者服務複製至發佈服務的資訊位於[此處](/help/operations/replication.md)。
