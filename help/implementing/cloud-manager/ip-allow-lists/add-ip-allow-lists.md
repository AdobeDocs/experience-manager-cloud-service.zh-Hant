---
title: 新增IP允許清單
description: 瞭解如何使用Cloud Manager新增您自己的IP允許清單。
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 1415d07235641262814e81362c806572bcf582ba
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 12%

---


# 新增 IP 允許清單 {#add-ip-allow-list}

瞭解如何使用Cloud Manager新增您自己的IP允許清單。

具有&#x200B;**業務負責人**&#x200B;或&#x200B;**部署管理員**&#x200B;角色的使用者可以按照以下步驟新增IP允許清單。

{{add-cm-allowlist-frontend-pipeline}}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 在「**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**」控制台中，選取程式。

1. 從&#x200B;**計畫總覽**&#x200B;頁面，使用左側的側面板（您可能需要按一下左上角的漢堡圖示才能看到面板），按一下&#x200B;**IP允許清單**。

   側面板中的![IP允許清單選項](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. 在IP允許清單頁面的右上角附近，按一下&#x200B;**新增IP允許清單**。

   ![新增 IP 允許清單對話框](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. 在&#x200B;**新增IP允許清單**&#x200B;對話方塊的&#x200B;**IP允許清單名稱**&#x200B;欄位中，輸入您要用來參照IP允許清單的名稱。 此名稱僅供參考。 請確定其描述性足以協助您識別清單。

1. 在&#x200B;**IP位址/ CIDR**&#x200B;欄位中，輸入IP或IP CIDR區塊。 請使用逗號或定位點分隔多個區塊。

1. 按一下&#x200B;**儲存**。

儲存後，新建立的IP允許清單會在&#x200B;**IP允許清單**&#x200B;頁面的表格中顯示為一列。

## 新增Cloud Manager IP允許清單 {#add-cm-allowlist}

前端管道要求預先新增以下Cloud Manager IP允許清單。

**Cloud Manager IP允許清單**

`52.254.106.192/28,20.186.185.181,52.254.106.240/28,52.254.107.128/28,52.254.105.192/28,52.254.106.176/28,20.186.185.227,52.254.106.144/28,52.254.107.64/28,20.186.185.239,20.22.83.112,52.254.107.80/28,52.254.107.144/28,52.254.106.224/28,20.14.241.153,52.254.107.0/28,52.254.107.32/28,52.254.106.208/28,40.70.154.136/29,52.254.106.160/28,52.254.107.16/28,52.254.106.0/28,4.152.211.251`

為避免前端管道執行中斷，請確保在啟用管道之前&#x200B;*新增此Cloud Manager IP允許清單，然後將其套用至環境*&#x200B;的作者服務。

**若要新增Cloud Manager IP允許清單：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 在「**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**」控制台中，選取程式。

1. 從&#x200B;**計畫總覽**&#x200B;頁面，使用左側的側面板（您可能需要按一下左上角的漢堡圖示才能看到面板），按一下&#x200B;**IP允許清單**。

1. 在IP允許清單頁面的右上角附近，按一下&#x200B;**新增IP允許清單**。

1. 在&#x200B;**新增IP允許清單**&#x200B;對話方塊的&#x200B;**IP允許清單名稱**&#x200B;欄位中，輸入&#x200B;*`Cloud Manager`*。

1. 複製上述Cloud Manager IP允許清單位址的區塊。 每個位址已用逗號分隔。

1. 在&#x200B;**新增IP允許清單**&#x200B;對話方塊中，將區塊貼到&#x200B;**IP位址/ CIDR**&#x200B;欄位中。

1. 將游標放在位址清單中的第一個逗號之後，然後按&#x200B;**Enter**。

1. 按一下&#x200B;**儲存**。

現在，[將Cloud Manager IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)套用至您的程式環境。



