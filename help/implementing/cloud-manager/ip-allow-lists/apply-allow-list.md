---
title: 套用和套用IP允許清單
description: 瞭解如何在 Cloud Manager 環境中套用和取消套用 IP 允許清單。
exl-id: 7158496c-b0c4-4228-a306-71dc51003c57
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 328ae6d1866a7089fb291d4872d27dc5fa1d4caa
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 12%

---


# 套用和取消套用IP允許清單 {#apply-allow-list}

應用 IP 允許列表時，清單定義中包含的所有 IP 範圍都與環境中的作者或發佈服務相關聯。 取消套用清單與此過程相反。

{{add-cm-allowlist-frontend-pipeline}}

## 套用IP允許清單 {#applying}

企業擁有者&#x200B;**或**&#x200B;部署管理器&#x200B;**中的**&#x200B;用戶角色可以追隨這些步驟來應用 IP 允許列表。

**要應用IP允許清單，請執行以下作：**

1. ](https://my.cloudmanager.adobe.com/) my.cloudmanager.adobe.com 時登[入 Cloud Manager。
1. 選擇適當的組織。
1. 在「**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**」控制台中，選取程式。
1. 從「**概觀**」頁面，瀏覽到「**環境**」畫面。
1. 在「環境」****&#x200B;畫面上，流覽至特定環境詳細信息頁面。
1. 導航到「 **IP 允許清單」** 表。
1. 使用表頂部的輸入字段，以便您可以選擇 IP 允許清單以及要應用該列表的作者、Publish或預覽服務。IP 允許清單必須已存在於 Cloud Manager 中才能套用。 請參閱 [添加IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md)。
1. 按一下![新增圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg)**套用**&#x200B;並確認提交。

## 取消套用IP允許清單 {#un-applying}

企業擁有者&#x200B;**或**&#x200B;部署管理器&#x200B;**中的**&#x200B;用戶角色可以追隨這些步驟來取消應用 IP 允許列表。

**要取消應用 IP 允許清單，請執行以下作：**

1. ](https://my.cloudmanager.adobe.com/) my.cloudmanager.adobe.com 時登[入 Cloud Manager。
1. 選取適當的組織。
1. 在「**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**」控制台中，選取程式。
1. 從「概述&#x200B;**」**&#x200B;頁面中，導航到「**環境**」頁面。
1. 導航到特定環境詳細信息頁面。
1. 從常規標籤中，滾動到 **IP 允許列表** 表。
1. 確定要取消應用的IP允許清單行。
1. 在標識行的右側，按兩下 ![更多圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。
1. 按兩下 **取消套用**。
1. 在「 **取消應用IP允許清單** 」對話框中，按兩下取消 **應用**。
