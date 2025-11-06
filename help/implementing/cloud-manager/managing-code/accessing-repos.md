---
title: 存放庫存取資訊
description: 了解如何使用 Cloud Manager 中的自助 Git 帳戶管理存取和管理您的 Adobe 託管 Git 存放庫。
exl-id: 0c0671a3-e400-46f3-ad86-166a6cfdd44b
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 96%

---


# 存放庫存取資訊 {#accessing-repos}

了解如何使用 Cloud Manager 中的自助 Git 帳戶管理存取和管理您的 Adobe 託管 Git 存放庫。

## 從總覽頁面存取儲存區域資訊 {#overview-page}

Cloud Manager 可以使用&#x200B;**管道**&#x200B;卡上的&#x200B;**存取存放庫資訊**，輕鬆擷取 Adobe 託管存放庫的存放庫存取資訊。

透過&#x200B;**存放庫資訊**&#x200B;對話框，您可以查看 Adobe 託管存放庫的以下存取資訊：

* Git 使用者名稱。
* Git 密碼。
* Cloud Manager Git 存放庫的 URL。
* 預先建立的 Git 指令，可快速新增遠端連線至 Git 存放庫並推送程式碼。

![存放庫資訊視窗](assets/repository-info.png)

Cloud Manager 不會提供[私人存放庫](private-repositories.md)的存取資訊。

擁有&#x200B;**開發人員**&#x200B;或&#x200B;**部署管理員**&#x200B;角色的使用者可看見該&#x200B;**存取存放庫資訊**&#x200B;功能。

**若要從概觀頁面存取存放庫資訊：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和方案。

1. 在&#x200B;**計畫概觀**&#x200B;頁面 (位於&#x200B;**管道**&#x200B;卡片下面)，按一下「**存取存放庫資訊**」。

   ![管道卡上的存取存放庫資訊](assets/pipelines-card.png)

1. 若要存取密碼，必須產生新密碼。在&#x200B;**存放庫資訊**&#x200B;對話框中，選取「**產生密碼**」。

1. 在確認對話框中，選取「**產生密碼**」。

   ![確認產生密碼](assets/confirm-generated-password.png)

1. 在「**密碼**」欄位右側，按一下![複製圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg)，可將密碼複製到剪貼簿。

   * 產生密碼後，先前的密碼便會失效。
   * Cloud Manager 不會儲存密碼。您有責任以安全方式儲存密碼。
   * 由於 Cloud Manager 不會儲存密碼，因此如果遺失密碼，您就必須重新產生新密碼。

   ![複製存放庫資訊對話框中的密碼](/help/implementing/cloud-manager/managing-code/assets/repository-copy-password.png)

若使用這些憑證，您可以複製存放庫的本機副本，並在該本機存放庫中進行變更，且在準備好後可以將任何程式碼變更提交回 Cloud Manager 中的遠端程式碼存放庫。

## 從存放庫頁面存取存放庫資訊 {#repositories-window}

 **存取存放庫資訊**&#x200B;功能也可從&#x200B;[**存放庫**&#x200B;頁面](managing-repositories.md)取得。此按鈕顯示有關存取受 Adobe 管理的存放庫的相同資訊。

## 撤銷存取密碼 {#revoke-password}

您可以隨時撤銷存取密碼。

若要如此做，請[為此請求建立支援服務單](https://experienceleague.adobe.com/zh-hant?support-solution=Experience+Manager&support-tab=home#support)。此服務單會以高優先性處理，且通常會在一天內撤銷。
