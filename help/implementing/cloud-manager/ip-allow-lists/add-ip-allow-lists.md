---
title: 新增IP允許清單
description: 瞭解如何使用Cloud Manager新增您自己的IP允許清單。
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: b9fb178760b74cb0e101506b6a9ff5ae30c18490
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 14%

---


# 新增 IP 允許清單 {#add-ip-allow-list}

瞭解如何使用Cloud Manager新增您自己的IP允許清單。

具有&#x200B;**業務負責人**&#x200B;或&#x200B;**部署管理員**&#x200B;角色的使用者可以按照以下步驟新增IP允許清單。

{{add-cm-allowlist-frontend-pipeline}}

**新增IP允許清單：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 在「**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**」控制台中，選取程式。

1. 從&#x200B;**程式總覽**&#x200B;頁面，使用側面板（您可能需要按一下左上角的![顯示功能表圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)來檢視面板），按一下![工作清單圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_TaskList_18_N.svg) **IP允許清單**。

   側面板中的![IP允許清單選項](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. 在IP允許清單頁面的右上角附近，按一下&#x200B;**新增IP允許清單**。

   ![新增 IP 允許清單對話框](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. 在&#x200B;**新增IP允許清單**&#x200B;對話方塊的&#x200B;**IP允許清單名稱**&#x200B;欄位中，輸入您要用來參照IP允許清單的名稱。 此名稱僅供參考。 請確定其描述性足以協助您識別清單。

1. 在&#x200B;**IP位址/ CIDR**&#x200B;欄位中，輸入IP或IP CIDR區塊。 請使用逗號或定位點分隔多個區塊。

1. 按一下「**儲存**」。

儲存後，新建立的IP允許清單會在&#x200B;**IP允許清單**&#x200B;頁面的表格中顯示為一列。

