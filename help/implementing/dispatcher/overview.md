---
title: 內容交付流概述
description: 內容交付流概述
exl-id: fe42fb9e-cdf4-43e1-b688-7cecf4124fa5
source-git-commit: 60fc1b8f93c93ca427507dbe56511342f285e6bc
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 1%

---

# 內容傳遞流程 {#content-delivery}

當前頁面詳細資訊在as a Cloud Service中發佈服務內容AEM傳遞。 發佈服務內容傳遞包括：

* CDN
* 調度AEM員
* 發AEM布

資料流如下：

1. URL將添加到瀏覽器中
1. 在DNS中映射到該域的CDN請求
1. 如果內容在CDN上完全快取，則CDN會將其提供給瀏覽器
1. 如果內容未完全快取，則CDN將調用（反向代理）到調度程式
1. 如果內容在分發程式上完全快取，則分發程式將其提供給CDN
1. 如果內容未完全快取，則調度程式將調用（反向代理）到發AEM布
1. 該內容由瀏覽器呈現，該瀏覽器也可根據標題快取它

預設情況下，內容類型HTML/文本設定為在分發程式層300秒（5分鐘）後過期，該閾值是分發程式快取和CDN都尊重的。 在重新部署發佈服務期間，在新發佈節點接受通信量之前清除調度器快取並隨後預熱。

以下各節提供了有關內容交付的更詳細資訊：
* [CDN配置](/help/implementing/dispatcher/cdn.md)
* [快取](/help/implementing/dispatcher/caching.md)


有關從作者服務到發佈服務的複製的資訊可用 [這裡](/help/operations/replication.md)。
