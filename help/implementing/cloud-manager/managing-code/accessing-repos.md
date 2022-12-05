---
title: 存取存放庫
description: 了解如何使用 Cloud Manager 中的自助 Git 帳戶管理存取和管理您的 Git 存放庫。
exl-id: 0c0671a3-e400-46f3-ad86-166a6cfdd44b
source-git-commit: 4729574eb31e01077f0d2a35efcef6d134f6aa5c
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 100%

---

# 存取存放庫 {#accessing-repos}

了解如何使用 Cloud Manager 中的自助 Git 帳戶管理存取和管理您的 Git 存放庫。

## 使用自助服務存放庫帳戶管理 {#self-service-repos}

Cloud Manager 可以使用管道卡上顯眼的&#x200B;**存取存放庫資訊**&#x200B;按鈕輕鬆擷取您的存放庫資訊。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和方案。

1. 從&#x200B;**計劃總覽**&#x200B;頁面瀏覽至&#x200B;**管道**&#x200B;卡，尋找&#x200B;**存取存放庫資訊**&#x200B;按鈕，以存取和管理您的 Git 存放庫。

   ![環境卡上的存取存放庫資訊按鈕](/help/implementing/cloud-manager/assets/repos/access-repo1.png)

1. 按一下&#x200B;**檢視存放庫資訊**&#x200B;按鈕，即可開啟對話框以檢視：

   * Cloud Manager Git 存放庫的 URL。
   * Git 使用者名稱。
   * Git 密碼，其值在按一下&#x200B;**產生密碼**&#x200B;按鈕時顯示。

   ![](/help/implementing/cloud-manager/assets/repos/access-repo-create.png)

使用這些憑證，使用者可以複製存放庫的本機副本，並在該本機存放庫中進行變更，且在準備好後可以將任何計劃碼變更提交回 Cloud Manager 中的遠端計劃碼存放庫。

**管道**&#x200B;卡的&#x200B;**非生產**&#x200B;管道索引標籤上也提供了&#x200B;**存取存放庫資訊**。

![非生產索引標籤上的存取存放庫資訊按鈕](/help/implementing/cloud-manager/assets/repos/access-repo-nonprod.png)

>[!NOTE]
>
>擁有&#x200B;**開發人員**&#x200B;或&#x200B;**部署管理員**&#x200B;角色的使用者可看見該&#x200B;**存取存放庫資訊**&#x200B;選項。
