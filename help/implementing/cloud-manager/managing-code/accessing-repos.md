---
title: 訪問儲存庫
description: 瞭解如何使用Cloud Manager的自助Git帳戶管理訪問和管理您的Git儲存庫。
exl-id: 0c0671a3-e400-46f3-ad86-166a6cfdd44b
source-git-commit: 4729574eb31e01077f0d2a35efcef6d134f6aa5c
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# 訪問儲存庫 {#accessing-repos}

瞭解如何使用Cloud Manager的自助Git帳戶管理訪問和管理您的Git儲存庫。

## 使用自助服務儲存庫帳戶管理 {#self-service-repos}

Cloud Manager使用 **訪問回購資訊** 按鈕。

1. 登錄到Cloud Manager(位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇相應的組織和程式。

1. 導航到 **管線** 卡 **計畫概述** 頁面並查找 **訪問回購資訊** 按鈕來訪問和管理git儲存庫。

   ![訪問環境卡上的「回購資訊」按鈕](/help/implementing/cloud-manager/assets/repos/access-repo1.png)

1. 按一下 **查看回購資訊** 按鈕開啟對話框以查看：

   * Cloud Manager Git儲存庫的URL。
   * Git用戶名。
   * git密碼，其值在 **生成密碼** 按鈕

   ![](/help/implementing/cloud-manager/assets/repos/access-repo-create.png)

使用這些憑據，用戶可以克隆儲存庫的本地副本，並在該本地儲存庫中進行更改，並且在準備就緒後，可以將任何代碼更改提交回雲管理器中的遠程代碼儲存庫。

的 **訪問回購資訊** 的上界 **非生產** 管道頁籤 **管線** 卡。

![訪問非生產標籤上的「回購資訊」按鈕](/help/implementing/cloud-manager/assets/repos/access-repo-nonprod.png)

>[!NOTE]
>
>的 **訪問回購資訊** 選項對具有 **開發人員** 或 **部署管理器** 角色。
