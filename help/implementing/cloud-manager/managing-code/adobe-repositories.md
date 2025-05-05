---
title: 在Cloud Manager中新增Adobe存放庫
description: 瞭解如何在Cloud Manager中新增Adobe管理的存放庫。
exl-id: 6c32c4ae-f48d-4440-bfc2-cdc1a3d59599
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f2364de6237ca9f0285815b581bcf3881488188d
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 7%

---

# 在Cloud Manager中新增Adobe存放庫 {#adobe-repositories}

瞭解如何在Cloud Manager中新增Adobe管理的存放庫。

**存放庫**&#x200B;頁面可讓您輕鬆將其他Adobe管理的存放庫新增至選取的方案。

**若要在Cloud Manager中新增Adobe存放庫：**

1. 在[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)登入Cloud Manager，並選取適當的組織以及您要新增Adobe管理存放庫的程式。

1. 從&#x200B;**方案總覽**&#x200B;頁面，按一下側邊功能表中的![資料夾圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) **存放庫**&#x200B;索引標籤。

1. 在&#x200B;**存放庫**&#x200B;頁面右上角附近，按一下&#x200B;**新增存放庫**。

   ![新增存放庫按鈕](assets/add-repository.png)

1. 在&#x200B;**新增存放庫**&#x200B;對話方塊中，確定已選取&#x200B;**Adobe存放庫**&#x200B;作為存放庫型別。

1. 在個別文字欄位中輸入下列內容：

   * **存放庫名稱** — 您新存放庫的表達式名稱。
   * **存放庫URL預覽** — 您不需要輸入URL路徑或編輯現有路徑，因為存放庫基礎結構已經就位，並已完全整合併由Adobe管理。
   * **描述（選擇性）** — 存放庫的詳細描述。

   ![新增存放庫對話方塊](assets/add-adobe-repository.png)

1. 按一下&#x200B;**儲存**。
您的新存放庫會顯示在&#x200B;**存放庫**&#x200B;頁面的表格中。

您現在可以將[CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)與其建立關聯，或在&#x200B;[**存放庫**&#x200B;頁面](managing-repositories.md)中管理它。

>[!TIP]
>
>您也可以新增自己管理的 GitHub 存放庫，以此作為[私人存放庫](private-repositories.md)。
