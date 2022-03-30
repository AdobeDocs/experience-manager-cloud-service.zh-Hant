---
title: 管理自定義域名
description: 瞭解如何使用雲管理器查看、更新、替換和刪除自定義域名。
source-git-commit: 4604b5fad59524a05dc7addf16c70246a14cfea1
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---


# 管理自定義域名 {#managing-custom-domain-names}

Cloud Manager允許您查看、更新、替換和刪除自定義域名。

## 查看和更新 {#view-and-update}

使用 **查看和更新** 的子菜單。

1. 登錄到Cloud Manager(位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇相應的組織和程式。

1. 導航到 **環境** 螢幕 **概述** 的子菜單。

1. 標識要查看或更新的自定義域名的行。

1. 按一下行最右端的省略號按鈕。

1. 選擇 **查看和更新** 的雙曲餘切值。

## 更新自定義域名的SSL證書 {#update-cert}

你可以 [查看和更新自定義域名的步驟相同](#view-and-update) 更新自定義域名的SSL證書。

>[!NOTE]
>
>SSL證書必須有效， [已配置，](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) 並包含您正在更新的自定義域名。

##  刪除自定義域名 {#deleting}

具有 **業務所有者** 或 **部署管理器** 角色可以使用雲管理器刪除自定義域名。

### 從所有關聯環境中刪除自定義域名 {#delete-cdn-all}

1. 登錄到Cloud Manager(位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇相應的組織和程式。

1. 導航到 **環境** 螢幕 **概述** 的子菜單。

1. 導航到 **域設定** 的 **環境** 的上界。

1. 標識要刪除的自定義域名的行。

1. 按一下行最右端的省略號按鈕。

1. 選擇 **刪除**。
   ![](/help/implementing/cloud-manager/assets/cdn/cdn-delete.png)

1. 確認提交。

### 從特定環境中刪除自定義域名 {#delete-cdn-specific}

1. 登錄到Cloud Manager(位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇相應的組織和程式。
1. 導航到 **環境** 螢幕 **概述** 的子菜單。
1. 從 **環境** 頁面，導航至感興趣環境的詳細資訊螢幕。
1. 從域名表中，標識要刪除的自定義域名的行。
1. 按一下行最右端的省略號按鈕。
1. 選擇 **刪除**。
1. 確認提交。
