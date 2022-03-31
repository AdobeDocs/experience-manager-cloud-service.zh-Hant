---
title: IP允許清單簡介
description: 瞭解IP允許清單如何限制用戶可以從哪些地址訪問您AEM的as a Cloud Service域。
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
source-git-commit: 8d1680fa8dbaaefa297cf8c6698097b3c7acc48d
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---


# IP允許清單簡介 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="管理IP允許清單"
>abstract="因AEM為雲服務可通過網際網路訪問，並通過用戶驗證和授權進行安全保護。 Cloud Manager的IP允許清單可用於僅限制和控制對受信任IP地址的訪問。 具有適當權限的Cloud Manager用戶可以建立允許其站點用戶訪問其域的受信任IP地址AEM清單。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists.html" text="添加IP允許清單"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/view-update-ip-allow-list.html" text="查看和更新IP允許清單"

因AEM為雲服務可通過網際網路訪問，並通過用戶驗證和授權進行安全保護。 Cloud Manager的IP允許清單可用於僅限制和控制對受信任IP地址的訪問。 具有適當權限的Cloud Manager用戶可以建立允許其站點用戶訪問其域的受信任IP地址AEM清單。

IP允許清單可以添加一次，並作為單元或實體多次應用/取消應用到環境中的作者和/或發佈者服務。

## 限制 {#limitations}

IP的許多限制使清單必須記住。

* 您的程式中最多可添加50個IP允許清單
* 每個IP允許清單最多可添加50個IP/CIDR地址。
* IP允許清單名稱在雲管理器中受支援，用於建立和/或發佈環境中的服務。
