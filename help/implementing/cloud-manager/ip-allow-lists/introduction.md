---
title: 簡介 — 雲管理器中的IP允許清單
description: 簡介 — 雲管理器中的IP允許清單
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
source-git-commit: 1875920ae5180074dcad98fb5c10242b6baa76c7
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# 簡介 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="管理IP允許清單"
>abstract="AEM雲服務向網際網路開放，安全通過用戶認證和授權進行處理。 IP允許清單是雲管理器中的一項功能，用於限制和控制僅對受信任用戶的訪問。 此功能使具有權限的用戶能夠建立受信任IP地址的允許清單，其站點用戶可以從該清單訪問其AEM域。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists.html" text="添加IP允許清單"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/view-update-ip-allow-list.html" text="查看和更新IP允許清單"

AEM雲服務向網際網路開放，安全通過用戶認證和授權進行處理。 IP允許清單是雲管理器中的一項功能，用於限制和控制僅對受信任用戶的訪問。 此功能使具有權限的用戶能夠建立受信任IP地址的允許清單，其站點用戶可以從該清單訪問其AEM域。

>[!NOTE]
>程式中最多可添加50個IP允許清單，每個IP允許清單最多可添加50個IP/CIDR地址。

IP允許清單可以添加一次，並作為單位或實體多次應用/取消應用到環境中的作者和/或發佈者服務。

>[!NOTE]
>環境中的Cloud Manager for Author和/或Publish服務支援IP允許清單名稱。

使用Cloud Manager UI IP允許清單頁或「環境詳細資訊」頁，具有權限的用戶可以執行多項任務來管理您環境的IP允許清單，包括：

* [添加IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md)
   >[!NOTE]
   > 您可以在程式中跨環境服務添加一次並重複使用或應用規則任意次數。
* [查看或更新IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/view-update-ip-allow-list.md)
* [應用或取消應用IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)
* [刪除IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/delete-ip-allow-list.md)
