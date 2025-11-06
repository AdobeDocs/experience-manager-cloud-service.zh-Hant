---
title: 套用和取消套用 IP 允許清單
description: 瞭解如何對Cloud Manager環境套用和取消套用IP允許清單。
exl-id: 7158496c-b0c4-4228-a306-71dc51003c57
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 14%

---


# 套用和取消套用IP允許清單 {#apply-allow-list}

套用IP允許清單時，清單定義中包含的所有IP範圍都與環境中的作者或發佈服務相關聯。 取消套用清單與此過程相反。

{{add-cm-allowlist-frontend-pipeline}}
{{ip-allow-lists-ue}}

## 套用IP允許清單 {#applying}

具有&#x200B;**業務負責人**&#x200B;或&#x200B;**部署管理員**&#x200B;角色的使用者可以按照以下步驟套用IP允許清單。

**套用IP允許清單：**

1. 在[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)登入Cloud Manager。
1. 選取適當的組織。
1. 在「**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**」控制台中，選取程式。
1. 從「**概觀**」頁面，瀏覽到「**環境**」畫面。
1. 在&#x200B;**環境**&#x200B;畫面上，瀏覽至特定環境詳細資訊頁面。
1. 瀏覽至&#x200B;**IP允許清單**&#x200B;資料表。
1. 使用表格頂端的輸入欄位，以便您可以選取IP允許清單以及要套用清單的作者、發佈或預覽服務。
IP允許清單必須已存在於Cloud Manager中才能套用它。 請參閱[新增IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md)。
1. 按一下「![新增」圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg)「**套用**」並確認您的訂閱。

## 取消套用IP允許清單 {#un-applying}

具有&#x200B;**業務負責人**&#x200B;或&#x200B;**部署管理員**&#x200B;角色的使用者可以按照以下步驟取消套用IP允許清單。

**要取消套用IP允許清單：**

1. 在[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)登入Cloud Manager。
1. 選取適當的組織。
1. 在「**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**」控制台中，選取程式。
1. 從&#x200B;**總覽**&#x200B;頁面，瀏覽至&#x200B;**環境**&#x200B;頁面。
1. 導覽至特定環境詳細資訊頁面。
1. 從[一般]索引標籤，捲動至&#x200B;**IP允許清單**&#x200B;表格。
1. 識別您要取消套用之IP允許清單的列。
1. 在已識別列的右側，按一下![更多圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。
1. 按一下&#x200B;**取消套用**。
1. 在&#x200B;**取消套用IP允許清單**&#x200B;對話方塊中，按一下&#x200B;**取消套用**。
