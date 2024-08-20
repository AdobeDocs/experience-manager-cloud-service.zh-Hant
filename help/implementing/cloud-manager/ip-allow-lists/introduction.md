---
title: IP 允許清單簡介
description: 瞭解IP允許清單如何限制使用者可以從哪些位址存取AEM as a Cloud Service中的網域。
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f4c6331491bb08e81964476ad58065c1ee022967
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 20%

---


# IP 允許清單簡介 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="管理 IP 允許清單"
>abstract="AEM as a Cloud Service可透過網際網路存取，並透過使用者驗證和授權得到保護。 Cloud Manager的IP允許清單可用於限制和控制對受信任IP地址的存取。 具有適當權限的 Cloud Manager 使用者可以就受信任的 IP 位址建立允許清單，其網站的使用者可以從這些位址存取其 AEM 網域。"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists" text="新增 IP 允許清單"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/managing-ip-allow-lists" text="檢視和更新IP允許清單"

AEM as a cloud service預設可透過網際網路存取。 雖然安全性已透過使用者驗證和授權處理，但 IP 允許清單是一種將存取限制為僅受信任的 IP 位址的方法。

Cloud Manager的IP允許清單可用於限制和控制對此類受信任IP地址的存取。 具有適當許可權的Cloud Manager使用者可以[建立受信任的IP位址的IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md)，其網站的使用者可以從這些位址存取其AEM網域。

新增之後，可以在環境中以單位或實體的形式，多次將[IP允許清單套用或取消套用](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)至作者服務或發佈者服務，或兩者皆套用。

>[!NOTE]
>
>如果未套用IP允許清單，則預設會允許所有IP位址。 套用IP允許清單時，除IP允許清單上的位址外，不允許任何IP位址。

## 限制 {#limitations}

記住IP允許清單有幾項限制。

* 最多可以在您的程式中新增50個IP允許清單。
* 每個IP允許清單最多可以新增50個IP/CIDR地址。
* Cloud Manager支援IP允許清單名稱用於環境中的作者服務或/及發佈服務。
