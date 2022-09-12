---
title: IP允許清單簡介
description: 了解IP允許清單如何限制使用者可存取您AEMas a Cloud Service網域的位址。
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
>abstract="AEM雲端服務可透過網際網路存取，並透過使用者驗證和授權加以保護。 Cloud Manager的IP允許清單可用來限制和控制僅對受信任IP位址的存取。 具有適當權限的Cloud Manager使用者可建立允許清單，列出受信任的IP位址，讓其網站的使用者可從這些位址存取其AEM網域。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists.html" text="新增IP允許清單"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/view-update-ip-allow-list.html" text="檢視和更新IP允許清單"

AEM雲端服務可透過網際網路存取，並透過使用者驗證和授權加以保護。 Cloud Manager的IP允許清單可用來限制和控制僅對受信任IP位址的存取。 具有適當權限的Cloud Manager使用者可建立允許清單，列出受信任的IP位址，讓其網站的使用者可從這些位址存取其AEM網域。

IP允許清單可以新增一次，並套用/取消套用多次，作為環境中的製作和/或發佈者服務的單位或實體。

## 限制 {#limitations}

IP有許多限制可讓清單記住。

* 您的程式中最多可新增50個IP允許清單
* 每個IP允許清單最多可新增50個IP/CIDR位址。
* Cloud Manager支援在環境中製作和/或發佈服務使用IP允許清單名稱。
