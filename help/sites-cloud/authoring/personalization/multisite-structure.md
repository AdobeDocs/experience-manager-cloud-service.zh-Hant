---
title: 如何架構目標內容的多網站管理
description: 圖表顯示如何架構目標內容的多網站支援
exl-id: c6b05c2a-0897-4514-8937-e23bfcf757d5
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 8%

---

# 如何架構目標內容的多網站管理 {#how-multisite-management-for-targeted-content-is-structured}

下圖顯示如何架構目標內容的多網站支援。

區域顯示在下方 **/content/campaigns/&lt;brand>** 預設情況下，每個品牌都有自動建立的主版區域。 每個區域都包含其專屬的活動、體驗和選件集。

![多站點結構](/help/sites-cloud/authoring/assets/multisite-structure.png)

若要尋找目標內容，頁面或網站可對應至某個區域。 如果未設定任何區域，AEM會回復至此特定品牌的主版區域。

下圖為邏輯在三個網站（稱為site1、site2和site3）中如何運作的範例。

![跨網站的多網站結構](/help/sites-cloud/authoring/assets/multisite-structure-2.png)

* site1會根據區域對應，為brand1尋找myarea1，為brand2尋找otherarea2。
* site2會針對brand1查詢myarea1，並針對brand2查詢主版區域，因為只定義brand1的區域對應。
* site3會查找brand1和brand2的主版區域，因為此網站完全未定義其他區域對應。
