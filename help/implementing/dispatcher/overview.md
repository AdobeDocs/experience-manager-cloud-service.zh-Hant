---
title: 內容傳遞流程概觀
description: 進一步了解關於內容傳送資料流量，以及發佈內容的方式
exl-id: fe42fb9e-cdf4-43e1-b688-7cecf4124fa5
feature: Dispatcher
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 93%

---

# 內容傳遞流程 {#content-delivery}

目前頁面詳細說明 AEM as a Cloud Service 中的發佈服務內容傳遞。發佈服務內容傳遞包括：

* CDN
* AEM Dispatcher
* AEM 發佈者

資料流如下所示：

1. 已在瀏覽器中新增 URL
1. 己要求 CDN，其在 DNS 中對應至該網域
1. 如果內容完全快取在 CDN 上，CDN 會將其提供給瀏覽器
1. 如果內容非完全快取，則 CDN 會呼叫 (反向 Proxy) Dispatcher
1. 如果內容完全快取在 Dispatcher 上，Dispatcher 會將其提供給 CDN
1. 如果內容非完全快取，則 Dispatcher 會呼叫 (反向 Proxy) AEM Publish
1. 內容由瀏覽器呈現，瀏覽器也可能快取它，視標頭而定

依預設，內容類型 HTML/文字設定為在 Dispatcher 層 300 秒 (5 分鐘) 後過期，這是 Dispatcher 快取和 CDN 都遵守的閾值。重新部署發佈服務期間，Dispatcher 快取被清空，然後在新發佈節點接受流量之前會做準備。

以下章節提供更多有關內容傳遞的詳細資訊：

* [CDN 設定](/help/implementing/dispatcher/cdn.md)
* [快取](/help/implementing/dispatcher/caching.md)

如需有關從作者服務復寫到發佈服務的資訊，請參閱[復寫](/help/operations/replication.md)。
