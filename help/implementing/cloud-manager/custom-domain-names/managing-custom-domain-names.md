---
title: 管理自訂網域名稱
description: 了解如何使用 Cloud Manager 查看、更新、取代和刪除自訂網域名稱。
exl-id: 6cab8cf2-22c0-4f4b-9c54-a1425e74ddd0
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 4e887b753eaf09e104c68484792f00dcb08ee304
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 60%

---


# 管理自訂網域名稱 {#managing-custom-domain-names}

Cloud Manager 可讓您檢視、更新、取代和刪除自訂網域名稱。

## 檢視和更新自訂網域名稱 {#view-and-update}

使用&#x200B;**檢視和更新**&#x200B;選單來檢視任何自訂網域名稱的詳細資訊。

**若要檢視和更新自訂網域名稱：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 在「**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**」控制台中，選取程式。

1. 從&#x200B;**概觀**&#x200B;頁面，瀏覽到&#x200B;**環境**&#x200B;畫面。

1. 識別您要檢視或更新之自訂網域名稱的列。

1. 按一下該列最右端的省略符號按鈕。

1. 選擇&#x200B;**檢視和更新**&#x200B;選項。

## 更新自訂網域名稱的SSL憑證 {#update-cert}

你可以遵循[與檢視和更新自訂網域名稱的相同步驟](#view-and-update)來更新自訂網域名稱的 SSL 憑證。

>[!NOTE]
>
>SSL憑證必須有效，[已設定](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)，並包含您要更新的自訂網域名稱。

## 刪除自訂網域名稱 {#deleting}

具有&#x200B;**業務負責人**&#x200B;或&#x200B;**部署管理員**&#x200B;角色的使用者可以使用 Cloud Manager 刪除自訂網域名稱。

### 從所有關聯環境刪除自訂網域名稱 {#delete-cdn-all}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和方案。

1. 從&#x200B;**總覽**&#x200B;畫面瀏覽至&#x200B;**網域設定**&#x200B;頁面。

1. 識別要刪除自訂網域名稱的列。

1. 按一下該列最右端的省略符號按鈕。

1. 選取&#x200B;**刪除**。

1. 確認您的提交。

### 從特定環境刪除自訂網域名稱 {#delete-cdn-specific}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和計畫。
1. 從&#x200B;**概觀**&#x200B;頁面，瀏覽到&#x200B;**環境**&#x200B;畫面。
1. 從&#x200B;**環境**&#x200B;頁面，瀏覽至感興趣環境的詳細資訊畫面。
1. 從網域名稱表格中，識別要刪除自訂網域名稱的列。
1. 按一下該列最右端的省略符號按鈕。
1. 選取&#x200B;**刪除**。
1. 確認您的提交。
