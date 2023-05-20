---
title: 如何架構目標內容的多網站管理
description: 圖表顯示了如何構建對目標內容的多站點支援
exl-id: c6b05c2a-0897-4514-8937-e23bfcf757d5
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 8%

---

# 如何架構目標內容的多網站管理 {#how-multisite-management-for-targeted-content-is-structured}

下圖顯示了如何構建對目標內容的多站點支援。

下面顯示區域 **/內容/活動/&lt;brand>** 預設情況下，每個品牌都有一個主區域，該主區域會自動建立。 每個區域都有自己的活動、經驗和優惠。

![多站點結構](/help/sites-cloud/authoring/assets/multisite-structure.png)

要查找目標內容，頁面或站點可以映射到區域。 如果未配置區域，AEM則返回到此特定品牌的主區域。

下圖是邏輯在三個站點（稱為site1 、 site2和site3）中如何工作的示例。

![跨站點的多站點結構](/help/sites-cloud/authoring/assets/multisite-structure-2.png)

* site1根據區域映射查找brand1的myarea1和brand2的其它區域2。
* site2查找brand1的myarea1和brand2的主區域，因為只定義了brand1的區域映射。
* site3查找brand1和brand2的主區域，因為根本沒有為此站點定義其他區域映射。
