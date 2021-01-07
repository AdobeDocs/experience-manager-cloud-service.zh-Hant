---
title: 簡介- Cloud Manager中的IP允許清單
description: 簡介- Cloud Manager中的IP允許清單
translation-type: tm+mt
source-git-commit: 1304a0cfa67c38943b1a36c105fbd5eafb3f8c4f
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# 簡介 {#introduction}

AEM做為雲端服務可開放至網際網路，而安全性則透過使用者驗證和授權來處理。 「IP允許」清單是Cloud Manager中的一項功能，用於限制和控制僅對受信任用戶的訪問。 此功能可讓擁有權限的使用者建立受信任IP位址的「允許清單」，讓其網站的使用者可從中存取其AEM網域。

「IP允許」清單可以新增一次，並以單位或實體的身分多次套用／取消套用至環境中的「作者」和／或「發行者」服務。

>[!NOTE]
>IP允許清單名稱在環境中受Cloud Manager for Author和／或Publish服務支援。

使用Cloud Manager UI IP Allow List（允許清單）頁或Environment Details（環境詳細資訊）頁，具有權限的用戶可以執行數項任務來管理您環境的IP Allow Lists，包括：

* [新增IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md)
   >[!NOTE]
   > 您可以在程式中的環境服務中添加一次，然後重複使用或應用規則。
* [查看或更新IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/view-update-ip-allow-list.md)
* [應用或取消應用IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)
* [刪除IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/delete-ip-allow-list.md)