---
title: 在 Cloud Manager 中新增 Adobe 存放庫
description: 了解如何在 Cloud Manager 中新增 Adobe 託管的存放庫。
exl-id: 6c32c4ae-f48d-4440-bfc2-cdc1a3d59599
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 100%

---

# 在 Cloud Manager 中新增 Adobe 存放庫 {#adobe-repositories}

了解如何在 Cloud Manager 中新增 Adobe 託管的存放庫。

「**存放庫**」頁面讓您輕鬆地將其他 Adobe 託管的存放庫新增至選定的方案。

**若要在 Cloud Manager 中新增 Adobe 存放庫：**

1. 透過 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager，然後選取要新增 Adobe 託管存放庫的相關組織和方案。

1. 在&#x200B;**方案概觀**&#x200B;頁面 (位於側邊選單內)，按一下 ![資料夾圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg)「**存放庫**」標籤。

1. 在&#x200B;**存放庫**&#x200B;頁面 (位於右上角附近)，按一下「**新增存放庫**」。

   ![新增存放庫按鈕](assets/add-repository.png)

1. 在「**新增存放庫**」對話框中，確保選取 **Adobe 存放庫**&#x200B;作為存放庫類型。

1. 在各別的文字欄位中，輸入以下內容：

   * **存放庫名稱** - 新存放庫使用表達清楚的名稱。
   * **存放庫 URL 預覽**  - 您無需輸入 URL 路徑或編輯現有路徑，因為存放庫已有所需的基礎架構且由 Adobe 完全整合和管理。
   * **說明 (選項)** - 存放庫的詳細說明。

   ![新增存放庫對話框](assets/add-adobe-repository.png)

1. 按一下「**儲存**」。
您的新存放庫將顯示在「**存放庫**」頁面的表格中。

您現在可以將 [CI/CD 管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)與存放庫建立關聯，或在&#x200B;[**存放庫**&#x200B;頁面](managing-repositories.md)中管理存放庫。

>[!TIP]
>
>您也可以新增自己管理的 GitHub 存放庫，以此作為[私人存放庫](private-repositories.md)。
