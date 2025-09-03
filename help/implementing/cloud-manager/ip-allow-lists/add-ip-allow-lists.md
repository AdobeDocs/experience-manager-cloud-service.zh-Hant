---
title: 新增IP允許清單
description: 瞭解如何使用Cloud Manager新增您自己的IP允許清單。
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 39af50d05fcbd22b3f4b4664f2c99590e7fb9da9
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 7%

---


# 新增 IP 允許清單 {#add-ip-allow-list}

瞭解如何使用Cloud Manager新增您自己的IP允許清單。

具有&#x200B;**業務負責人**&#x200B;或&#x200B;**部署管理員**&#x200B;角色的使用者可以按照以下步驟新增IP允許清單。

{{add-cm-allowlist-frontend-pipeline}}
{{ip-allow-lists-ue}}

**新增IP允許清單：**

1. 在[experience.adobe.com](https://experience.adobe.com/experiencemanager/)登入Cloud Manager。

1. 在左側功能表中按一下Cloud Manager，然後選取適當的組織。

1. 在「**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**」控制台中，選取程式。

1. 從&#x200B;**程式總覽**&#x200B;頁面，使用左側功能表（您可能需要按一下左上角的![顯示功能表圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)才能檢視功能表），按一下![工作清單圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_TaskList_18_N.svg) **IP允許清單**。

   左側功能表中的![IP允許清單選項](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. 在IP允許清單頁面的右上角附近，按一下&#x200B;**新增IP允許清單**。

   ![新增 IP 允許清單對話框](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. 在&#x200B;**新增IP允許清單**&#x200B;對話方塊的&#x200B;**IP允許清單名稱**&#x200B;欄位中，輸入您要用來參照IP允許清單的名稱。 此名稱僅供參考。 請確定其描述性足以協助您識別清單。

1. 在&#x200B;**IP位址/ CIDR**&#x200B;欄位中，輸入最多50個IP位址或CIDR區塊。 您可以透過下列其中一種方式新增它們：

   * 一次一個：輸入地址，然後按`Enter`。 對每個其他位址重複此步驟。
   * 一次多個：輸入以逗號(，)或定位字元分隔的地址，然後按`Enter`以個別辨識每個地址。

1. 完成輸入最後一個IP位址或CIDR區塊之後，請按`Enter`確認輸入。 只有在您按下`Enter`後，專案才會被確認，且&#x200B;**儲存**&#x200B;按鈕會變成使用中。

1. 按一下「**儲存**」。

儲存後，新建立的IP允許清單會在&#x200B;**IP允許清單**&#x200B;頁面的表格中顯示為一列。

