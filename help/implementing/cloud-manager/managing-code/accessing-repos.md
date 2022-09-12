---
title: 存取儲存庫
description: 了解如何使用Cloud Manager的自助Git帳戶管理功能存取及管理您的Git存放庫。
exl-id: 0c0671a3-e400-46f3-ad86-166a6cfdd44b
source-git-commit: 4729574eb31e01077f0d2a35efcef6d134f6aa5c
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# 存取儲存庫 {#accessing-repos}

了解如何使用Cloud Manager的自助Git帳戶管理功能存取及管理您的Git存放庫。

## 使用自助服務儲存庫帳戶管理 {#self-service-repos}

Cloud Manager可讓您輕鬆使用 **存取存放庫資訊** 按鈕可顯示在管道卡上。

1. 登入Cloud Manager，網址為 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇適當的組織和方案。

1. 導覽至 **管道** 卡片 **計畫概述** 頁面，並尋找 **存取存放庫資訊** 按鈕來存取和管理您的git存放庫。

   ![「環境」卡上的「存取存放庫資訊」按鈕](/help/implementing/cloud-manager/assets/repos/access-repo1.png)

1. 按一下 **檢視存放庫資訊** 按鈕以開啟要檢視的對話方塊：

   * Cloud Manager Git存放庫的URL。
   * Git使用者名稱。
   * git密碼，其值會在 **生成密碼** 按鈕。

   ![](/help/implementing/cloud-manager/assets/repos/access-repo-create.png)

使用這些憑證，使用者可以複製存放庫的本機副本，並在該本機存放庫中進行變更，在準備就緒時，即可將任何程式碼變更提交回Cloud Manager的遠端程式碼存放庫。

此 **存取存放庫資訊** 選項 **非生產** 管道標籤 **管道** 卡片。

![在非生產索引標籤上存取存放庫資訊按鈕](/help/implementing/cloud-manager/assets/repos/access-repo-nonprod.png)

>[!NOTE]
>
>此 **存取存放庫資訊** 選項對具有 **開發人員** 或 **部署管理員** 角色。
