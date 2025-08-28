---
title: IP 允許清單簡介
description: 瞭解IP允許清單如何限制使用者可以從哪些位址存取AEM as a Cloud Service中的網域。
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f1e9b76742c8d97f44ff974fb8686fdcb3d804e6
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 21%

---


# IP 允許清單簡介 {#introduction}

瞭解IP允許清單如何限制使用者可以從哪些位址存取AEM as a Cloud Service中的網域。

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="管理 IP 允許清單"
>abstract="AEM as a Cloud Service 可透過網際網路存取，並透過使用者驗證和授權來獲得保護。Cloud Manager 的 IP 允許清單僅能用來限制和控制對受信任 IP 位址的存取。具有適當權限的 Cloud Manager 使用者可以就受信任的 IP 位址建立允許清單，其網站的使用者可以從這些位址存取其 AEM 網域。"
>additional-url="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/cicd-pipelines/ip-allow-lists/add-ip-allow-lists" text="新增 IP 允許清單"
>additional-url="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/cicd-pipelines/ip-allow-lists/managing-ip-allow-lists" text="檢視和更新 IP 允許清單"

## 概觀 {#overview}

AEM as a cloud service預設可透過網際網路存取。 雖然安全性已透過使用者驗證和授權處理，但 IP 允許清單是一種將存取限制為僅受信任的 IP 位址的方法。

Cloud Manager的IP允許清單可用於限制和控制對此類受信任IP地址的存取。 具有適當許可權的Cloud Manager使用者可以[建立並新增受信任的IP位址的IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md)，其網站的使用者可以從這些位址存取其AEM網域。

新增之後，可以在環境中以單位或實體的形式，多次將[IP允許清單套用或取消套用](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)至作者服務或發佈者服務，或兩者皆套用。

>[!NOTE]
>
>如果未套用IP允許清單，則預設會允許所有IP位址。 套用IP允許清單時，除IP允許清單上的位址外，不允許任何IP位址。

## 使用說明 {#usage-notes}

* 最多可以將50個IP允許清單新增到您的程式。
* 每個IP允許清單最多可以新增50個IP/CIDR地址。
* Cloud Manager支援IP允許清單名稱用於環境中的作者服務或/及發佈服務。

### 前端管道和IP允許清單 {#front-end-pipeline}

如果您使用或打算使用[前端管道來開發網站](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md)，則必須預先新增下列Cloud Manager IP允許清單。

當您[新增IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md#add-cm-allowlist)，將其命名&#x200B;*`Cloud Manager`*，然後複製下列位址清單並將其貼到IP允許清單對話方塊中。

```text
52.254.106.192/28
20.186.185.181
52.254.106.240/28
52.254.107.128/28
52.254.105.192/28
52.254.106.176/28
20.186.185.227
52.254.106.144/28
52.254.107.64/28
20.186.185.239
20.22.83.112
52.254.107.80/28
52.254.107.144/28
52.254.106.224/28
20.14.241.153
52.254.107.0/28
52.254.107.32/28
52.254.106.208/28
40.70.154.136/29
52.254.106.160/28
52.254.107.16/28
52.254.106.0/28
4.152.211.251
```

為避免前端管道執行中斷，請確保新增此Cloud Manager IP允許清單。 然後，在啟用管道之前&#x200B;*將清單套用至作者環境*。

如需詳細資訊，請參閱[套用IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)和[啟用前端管道](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md)。

### 通用編輯器和IP允許清單 {#universal-editor}

如果您打算使用通用編輯器來編寫內容，您必須將通用編輯器服務使用的IP位址新增到允許清單並套用它。

1. 從下列API端點擷取Universal Editor服務使用的IP位址： `http://universal-editor-service.adobe.io/ip-ranges`。
1. 使用這些IP位址建立允許清單，將其命名為`Universal Editor Service`或類似名稱。
1. 套用`Universal Editor Service`允許清單。

Universal Editor服務使用的IP位址清單可能會有所變更，您必須據此更新允許清單。
