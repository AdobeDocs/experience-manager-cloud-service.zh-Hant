---
title: 存取儲存庫
seo-title: Accessing Repositories
description: 本頁說明如何存取和管理Git存放庫。
seo-description: Follow this page to learn how to access and manage your Git repository.
exl-id: 0c0671a3-e400-46f3-ad86-166a6cfdd44b
source-git-commit: 3cdee254eebcf45762feff8fe081b006a803ef1b
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 5%

---

# 存取儲存庫 {#accessing-repos}

您可以使用Cloud Manager UI中的自助服務Git帳戶管理來存取及管理您的Git存放庫。

## 使用自助儲存庫帳戶管理 {#self-service-repos}

使用Cloud Manager UI中可用的&#x200B;**存取存放庫資訊**&#x200B;按鈕，最顯眼的位於管道卡上。

1. 從您的&#x200B;**方案概述**&#x200B;頁面導覽至&#x200B;**管道**&#x200B;卡片。

1. 您將檢視&#x200B;**存取存放庫資訊**&#x200B;選項，以存取及管理您的Git存放庫。

   ![](/help/implementing/cloud-manager/assets/repos/access-repo1.png)

   此外，如果您選取&#x200B;**非生產**&#x200B;管道標籤，您也會在此處檢視&#x200B;**存取存放庫資訊**&#x200B;選項。

   ![](/help/implementing/cloud-manager/assets/repos/access-repo-nonprod.png)

   >[!NOTE]
   >「開發人員」或「部署管理員」角色中的使用者可看到「**存取存放庫資訊**」選項。 按一下此按鈕會開啟一個對話方塊，讓使用者可以找到Cloud Manager Git存放庫的URL及其使用者名稱和密碼。

   ![](/help/implementing/cloud-manager/assets/repos/access-repo-create.png)

   在Cloud Manager中管理Git的重要考量事項包括：

   * **URL**:儲存庫URL
   * **使用者名稱**:使用者名稱
   * **密碼**:按一下「生成密碼」 **按鈕時顯示** 的值。


      >[!NOTE]
      >使用者可以簽出其程式碼的復本，並在本機程式碼存放庫中進行變更。 準備就緒後，使用者可將其程式碼變更提交回Cloud Manager的遠端程式碼存放庫。
