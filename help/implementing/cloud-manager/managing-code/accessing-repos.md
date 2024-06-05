---
title: 存取存放庫
description: 了解如何使用 Cloud Manager 中的自助 Git 帳戶管理存取和管理您的 Git 存放庫。
exl-id: 0c0671a3-e400-46f3-ad86-166a6cfdd44b
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 85%

---


# 存取存放庫 {#accessing-repos}

了解如何使用 Cloud Manager 中的自助 Git 帳戶管理存取和管理您的 Git 存放庫。

## 使用自助服務存放庫帳戶管理 {#self-service-repos}

Cloud Manager 可以使用管道卡上顯眼的&#x200B;**存取存放庫資訊**&#x200B;按鈕輕鬆擷取您的存放庫資訊。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和方案。

1. 從&#x200B;**方案概觀**&#x200B;頁面瀏覽至&#x200B;**管道**&#x200B;卡，尋找&#x200B;**存取存放庫資訊**&#x200B;按鈕，以存取和管理您的 Git 存放庫。

   ![環境卡片上的存取存放庫資訊按鈕](/help/implementing/cloud-manager/assets/repos/access-repo1.png)

1. 按一下「**檢視存放庫資訊**」按鈕來開啟對話框以檢視：

   * Cloud Manager Git 存放庫的 URL。
   * Git 使用者名稱。
   * Git 密碼，其值在按一下&#x200B;**產生密碼**&#x200B;按鈕時顯示。

   ![存放庫資訊檢視](/help/implementing/cloud-manager/assets/repos/access-repo-create.png)

使用這些憑證，使用者可以複製存放庫的本機副本，並在該本機存放庫中進行變更，且在準備好後可以將任何計劃碼變更提交回 Cloud Manager 中的遠端計劃碼存放庫。

**管道**&#x200B;卡的&#x200B;**非生產**&#x200B;管道索引標籤上也提供了&#x200B;**存取存放庫資訊**。

![非生產索引標籤上的存取存放庫資訊按鈕](/help/implementing/cloud-manager/assets/repos/access-repo-nonprod.png)

>[!NOTE]
>
>擁有&#x200B;**開發人員**&#x200B;或&#x200B;**部署管理員**&#x200B;角色的使用者可看見該&#x200B;**存取存放庫資訊**&#x200B;選項。

## 撤銷存取密碼 {#revoke-password}

您可以隨時撤銷存取密碼。 若要這麼做，請 [為此請求建立支援票證。](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;support-tab=home#support)

票證將會受到高優先順序的處理，並且應在一天內撤銷。
