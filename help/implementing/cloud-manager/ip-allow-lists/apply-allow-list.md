---
title: 套用和取消套用 IP 允許清單
description: 了解如何對環境套用和取消套用 IP 允許清單。
exl-id: 7158496c-b0c4-4228-a306-71dc51003c57
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 84%

---


# 套用和取消套用 IP 允許清單 {#apply-allow-list}

應用 IP 允許清單時，清單定義中包含的所有 IP 範圍都與環境中的作者或發布服務相關聯。取消套用清單與此過程相反。

## 套用 IP 允許清單 {#applying}

具有&#x200B;**業務負責人**&#x200B;或&#x200B;**部署管理員**&#x200B;角色的使用者可以按照以下步驟套用 IP 允許清單。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 在「**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**」控制台中，選取程式。
1. 從&#x200B;**概觀**&#x200B;頁面瀏覽到&#x200B;**環境**&#x200B;畫面。
1. 從計畫概觀畫面的&#x200B;**環境**&#x200B;瀏覽到特定環境，然後瀏覽到 **IP 允許清單**&#x200B;資料表。
1. 使用表格頂端的輸入欄位，以便您可以選取IP允許清單以及要套用清單的作者或發佈服務。
   * IP 允許清單必須存在於 Cloud Manager 中才能將其套用。
1. 按一下&#x200B;**套用**，然後確認您的訂閱。

## 取消套用允許清單 {#un-applying}

具有&#x200B;**業務負責人**&#x200B;或&#x200B;**部署管理員**&#x200B;角色的使用者可以按照以下步驟取消套用 IP 允許清單。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和計畫。
1. 從&#x200B;**概觀**&#x200B;頁面瀏覽到&#x200B;**環境**&#x200B;畫面。
1. 從計畫概觀畫面的&#x200B;**環境**&#x200B;瀏覽到特定環境，然後瀏覽到 **IP 允許清單**&#x200B;資料表。
1. 識別您要取消套用之IP允許清單的列。
1. 選擇該列最右端的省略符號按鈕。
1. 選取&#x200B;**取消套用**&#x200B;選項，然後確認您的訂閱。
