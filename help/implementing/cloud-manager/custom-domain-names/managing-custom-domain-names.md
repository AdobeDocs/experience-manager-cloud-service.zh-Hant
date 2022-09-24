---
title: 管理自訂網域名稱
description: 了解如何使用Cloud Manager檢視、更新、取代和刪除自訂網域名稱。
exl-id: 6cab8cf2-22c0-4f4b-9c54-a1425e74ddd0
source-git-commit: 955f4bb55434eeb1a429a1972714b71c5370de1e
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# 管理自訂網域名稱 {#managing-custom-domain-names}

Cloud Manager可讓您檢視、更新、取代和刪除自訂網域名稱。

## 檢視和更新 {#view-and-update}

使用 **檢視和更新** 功能表來檢視任何自訂網域名稱的詳細資訊。

1. 登入Cloud Manager，網址為 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇適當的組織和方案。

1. 導覽至 **環境** 螢幕 **概述** 頁面。

1. 標識要查看或更新的自定義域名的行。

1. 按一下行最右端的刪節號按鈕。

1. 選取 **檢視與更新** 選項。

## 更新自訂網域名稱的SSL憑證 {#update-cert}

您可以遵循 [檢視和更新自訂網域名稱的相同步驟](#view-and-update) 更新自訂網域名稱的SSL憑證。

>[!NOTE]
>
>SSL憑證必須有效， [已配置，](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) 並包含您正在更新的自訂網域名稱。

## 刪除自訂網域名稱 {#deleting}

使用 **業務負責人** 或 **部署管理員** 角色可以使用Cloud Manager刪除自訂網域名稱。

### 從所有關聯環境刪除自訂網域名稱 {#delete-cdn-all}

1. 登入Cloud Manager，網址為 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇適當的組織和方案。

1. 導覽至 **環境** 螢幕 **概述** 頁面。

1. 導覽至 **網域設定** 頁面 **環境** 螢幕。

1. 識別您要刪除的自訂網域名稱列。

1. 按一下行最右端的刪節號按鈕。

1. 選擇 **刪除**.

   ![刪除自定義域名](/help/implementing/cloud-manager/assets/cdn/cdn-delete.png)

1. 確認您的提交。

### 從特定環境刪除自訂網域名稱 {#delete-cdn-specific}

1. 登入Cloud Manager，網址為 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇適當的組織和方案。
1. 導覽至 **環境** 螢幕 **概述** 頁面。
1. 從 **環境** 頁面，導覽至感興趣環境的詳細資訊畫面。
1. 從域名表中，標識要刪除的自定義域名的行。
1. 按一下行最右端的刪節號按鈕。
1. 選擇 **刪除**.
1. 確認您的提交。
