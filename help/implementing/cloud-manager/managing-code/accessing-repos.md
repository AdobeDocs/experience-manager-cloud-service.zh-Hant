---
title: 存放庫存取資訊
description: 瞭解如何使用Cloud Manager中的自助Git帳戶管理存取和管理您的Adobe管理的Git存放庫。
exl-id: 0c0671a3-e400-46f3-ad86-166a6cfdd44b
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 0b39fc4dcaf86d436547d3941b1f12bca8c5bc9b
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 11%

---


# 存放庫存取資訊 {#accessing-repos}

瞭解如何使用Cloud Manager中的自助Git帳戶管理存取和管理您的Adobe管理的Git存放庫。

## 從總覽頁面存取存放庫資訊 {#overview-page}

Cloud Manager可讓您使用，輕鬆擷取Adobe管理的存放庫的存放庫存取資訊 **存取存放庫資訊** 按鈕在管道卡上顯眼可用。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和方案。

1. 瀏覽至 **管道** 卡片來自您的 **計畫總覽** 頁面。

   ![環境卡片上的存取存放庫資訊按鈕](assets/pipelines-card.png)

1. 點選或按一下 **存取存放庫資訊** 按鈕以開啟 **存放庫資訊** 對話方塊和檢視：

   * Git 使用者名稱。
   * Git密碼。
   * Cloud Manager Git 存放庫的 URL。
   * 預先建立的Git命令，可快速將遠端新增至您的Git存放庫和推送程式碼。

   ![存放庫資訊視窗](assets/repository-info.png)

1. 若要存取密碼，必須產生新密碼。 若要這麼做，請點選或按一下 **產生密碼** 按鈕。

1. 確認在中產生密碼 **您確定……** 對話方塊（點選或按一下） **產生密碼**.

   ![確認密碼產生](assets/confirm-password-generation.png)

1. 系統會產生密碼，並會在中顯示該密碼以複製 **密碼** 欄位。

   * 產生密碼會使先前的密碼無效。
   * Cloud Manager不會儲存密碼。 您有責任安全地儲存此密碼。
   * 由於Cloud Manager不會儲存密碼，因此如果您遺失密碼，則必須重新產生新密碼。

   ![產生的密碼範例](assets/generated-password.png)

使用這些憑證，您可以複製存放庫的本機副本、在該本機存放庫中進行變更，並在準備好後將任何程式碼變更提交回Cloud Manager中的遠端程式碼存放庫。

>[!NOTE]
>
>* 擁有&#x200B;**開發人員**&#x200B;或&#x200B;**部署管理員**&#x200B;角色的使用者可看見該&#x200B;**存取存放庫資訊**&#x200B;選項。
>* 此 **存取存放庫資訊** 按鈕只會顯示Adobe管理的存放庫的存放庫存取資訊。 存取以下資訊： [私人存放庫](private-repositories.md) 在Cloud Manager中無法使用。

## 從儲存區域視窗存取儲存區域資訊 {#repositories-window}

一個 **存取存放庫資訊** 按鈕也可在的工具列中找到 [**存放庫** 視窗。](managing-repositories.md) 它會顯示有關存取Adobe管理的存放庫的相同資訊。

## 撤銷存取密碼 {#revoke-password}

您可以隨時撤銷存取密碼。 若要這麼做，請 [為此請求建立支援票證。](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;support-tab=home#support)

票證將會受到高優先順序的處理，並且應在一天內撤銷。
