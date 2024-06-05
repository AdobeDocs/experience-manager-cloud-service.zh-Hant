---
title: 如何架構目標內容的多網站管理
description: 圖表顯示如何架構目標內容的多網站支援
exl-id: c6b05c2a-0897-4514-8937-e23bfcf757d5
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 8%

---

# 如何架構目標內容的多網站管理 {#how-multisite-management-for-targeted-content-is-structured}

下圖顯示如何架構目標內容的多網站支援。

區域會顯示在下方 **/content/campaigns/&lt;brand>** 依預設，每個品牌都有自動建立的主版區域。 每個區域都包含自身的一組活動、體驗和選件。

![多站台結構](/help/sites-cloud/authoring/assets/multisite-structure.png)

若要查詢目標內容，頁面或網站可以對應至某個區域。 如果沒有設定區域，AEM會退回此特定品牌的主區域。

下圖是該邏輯如何為三個網站（稱為site1、site2及site3）運作的範例。

![跨網站的多網站結構](/help/sites-cloud/authoring/assets/multisite-structure-2.png)

* 網站1會根據區域對應查詢myarea1以尋找brand1，並查詢otherarea2以尋找brand2。
* 網站2會查詢brand1的myarea1和brand2的主區域，因為只有brand1的區域對應已定義。
* 網站3會查詢brand1和brand2的主要區域，因為此網站完全沒有定義其他區域對應。
