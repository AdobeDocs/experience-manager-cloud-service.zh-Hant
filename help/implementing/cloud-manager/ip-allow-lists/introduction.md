---
title: 簡介 — Cloud Manager中的IP允許清單
description: 簡介 — Cloud Manager中的IP允許清單
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
source-git-commit: 3f282169b9ac2e2cf3e58277fd0c32cd97003de2
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# 簡介 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="管理IP允許清單"
>abstract="AEM as a cloud service可開放至網際網路，且安全性會透過使用者驗證和授權處理。 「IP允許清單」是Cloud Manager中的一項功能，用於限制和控制僅對受信任用戶的訪問。 此功能可讓擁有權限的使用者建立受信任IP位址的允許清單，讓其網站的使用者可從這些位址存取其AEM網域。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists.html" text="新增IP允許清單"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/view-update-ip-allow-list.html" text="檢視和更新IP允許清單"

AEM as a cloud service可開放至網際網路，且安全性會透過使用者驗證和授權處理。 「IP允許清單」是Cloud Manager中的一項功能，用於限制和控制僅對受信任用戶的訪問。 此功能可讓擁有權限的使用者建立受信任IP位址的允許清單，讓其網站的使用者可從這些位址存取其AEM網域。

>[!NOTE]
>您的計畫中最多可新增10個IP允許清單，而每個IP允許清單最多可新增50個IP/CIDR位址。

IP允許清單可以新增一次，並套用/取消套用多次，作為環境中的製作和/或發佈者服務的單位或實體。

>[!NOTE]
>Cloud Manager針對環境中的製作和/或發佈服務支援IP允許清單名稱。

擁有權限的使用者可使用Cloud Manager UI IP允許清單頁面或環境詳細資料頁面，執行數項工作以管理您環境的IP允許清單，包括：

* [新增IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md)
   >[!NOTE]
   > 您可以在程式中跨環境服務多次新增並重複使用或套用規則。
* [檢視或更新IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/view-update-ip-allow-list.md)
* [套用或取消套用IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)
* [刪除IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/delete-ip-allow-list.md)
