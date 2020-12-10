---
title: 簡介- Could Manager中的IP允許清單
description: 簡介- Could Manager中的IP允許清單
translation-type: tm+mt
source-git-commit: 4635cb6360707d12cf512b0ee21f05169a153114
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 簡介 {#introduction}

AEM做為雲端服務可開放至網際網路，而安全性則透過使用者驗證和授權來處理。 「IP允許」清單是Cloud Manager中的一項功能，用於限制和控制僅對受信任用戶的訪問。 此功能可讓擁有權限的使用者建立受信任IP位址的「允許清單」，讓其網站的使用者可從中存取其AEM網域。

「IP允許」清單可以新增一次，並以單位或實體的身分多次套用／取消套用至環境中的「作者」和／或「發行者」服務。

>[!NOTE]
>IP允許清單名稱在環境中受Cloud Manager for Author和／或Publish服務支援。

使用Cloud Manager UI IP Allow List（允許清單）頁或Environment Details（環境詳細資訊）頁，具有權限的用戶可以執行數項任務來管理您環境的IP Allow Lists，包括：

* 添加IP允許清單
   >[!NOTE]
   > 您可以在程式中的環境服務中添加一次，然後重複使用或應用規則。
* 查看或更新IP允許清單
* 套用或取消套用IP允許清單
* 刪除IP允許清單