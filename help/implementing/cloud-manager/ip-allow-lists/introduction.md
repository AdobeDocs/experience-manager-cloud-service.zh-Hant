---
title: IP 允許清單簡介
description: 了解 IP 允許清單如何限制使用者可以從哪些地址存取您的 AEM as a Cloud Service 網域。
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
source-git-commit: 8d1680fa8dbaaefa297cf8c6698097b3c7acc48d
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 100%

---


# IP 允許清單簡介 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="管理 IP 允許清單"
>abstract="AEM as a Cloud Service 可透過網際網路存取，並透過使用者身份驗證和授權得到保護。Cloud Manager 的 IP 允許清單可用於限制和控制對受信任 IP 地址的存取。具有適當權限的 Cloud Manager 使用者可以建立受信任的 IP 地址允許清單，其網站的使用者可以從這些地址存取其 AEM 域。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists.html?lang=zh-Hant" text="新增 IP 允許清單"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/view-update-ip-allow-list.html?lang=zh-Hant" text="檢視和更新 IP 允許清單"

AEM as a Cloud Service 可透過網際網路存取，並透過使用者身份驗證和授權得到保護。Cloud Manager 的 IP 允許清單可用於限制和控制對受信任 IP 地址的存取。具有適當權限的 Cloud Manager 使用者可以建立受信任的 IP 地址允許清單，其網站的使用者可以從這些地址存取其 AEM 域。

IP 允許清單可以作為一個單元或實體多次新增和應用/取消應用到環境中的作者和/或出版商服務。

## 限制 {#limitations}

記住 IP 允許清單有許多限制。

* 最多可以在您的程序中新增 50 個 IP 允許清單
* 每個 IP 允許清單最多可以新增 50 個 IP/CIDR 地址。
* Cloud Manager 中支援 IP 允許清單名稱用於環境中的創作和/或發布服務。
