---
title: IP 允許清單簡介
description: 瞭解IP允許清單如何限制使用者可以從哪些位址存取AEMas a Cloud Service上的網域。
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
source-git-commit: f0edd0e3deeba89dcbd2dc1a07859138b24e2220
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 18%

---


# IP 允許清單簡介 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="管理IP允許清單"
>abstract="AEM as a cloud service可透過網際網路存取，並透過使用者驗證和授權受到保護。 Cloud Manager的IP允許清單可用於限制和控制對受信任IP地址的訪問。 具有適當許可權的Cloud Manager使用者可以建立受信任IP地址的允許清單，其網站的使用者可以從這些地址存取其AEM網域。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists.html" text="新增 IP 允許清單"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/managing-ip-allow-lists.html" text="檢視和更新 IP 允許清單"

AEM as a cloud service 預設可透過網際網路存取。雖然安全性已透過使用者驗證和授權處理，但 IP 允許清單是一種將存取限制為僅受信任的 IP 位址的方法。

Cloud Manager的IP允許清單可用於限制和控制對此類受信任IP地址的訪問。 具有適當許可權的Cloud Manager使用者可以 [建立允許清單](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) 受信任的IP位址數量，其網站的使用者可以從這些位址存取其AEM網域。

新增之後， [可以套用/取消套用IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) 以單位或實體的身分多次前往環境中的作者和/或發佈者服務。

>[!NOTE]
>
>如果未套用IP允許清單，則預設會允許所有IP位址。 套用IP允許清單時，除IP允許清單上的位址外，不允許任何IP位址。

## 限制 {#limitations}

請記住IP允許清單有幾項限制。

* 最多可以在您的程式中新增50個IP允許清單
* 每個IP允許清單最多可以新增50個IP/CIDR位址。
* Cloud Manager中支援IP允許清單名稱用於環境中的作者或/及發佈服務。
