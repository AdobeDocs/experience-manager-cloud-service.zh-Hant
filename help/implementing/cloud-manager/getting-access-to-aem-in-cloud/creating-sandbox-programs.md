---
title: 建立沙箱計畫
description: 了解如何使用 Cloud Manager 建立您自己的沙箱計劃，用於訓練、展示、POC 或其他非生產目的。
exl-id: 10011392-3059-4bb0-88db-0af1d390742e
source-git-commit: bceec9ea6858b1c4c042ecd96f13ae5cac1bbee5
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 95%

---

# 建立沙箱計畫 {#create-sandbox-program}

沙箱計畫通常建立的目的是提供訓練、執行範例、啟用、POC 或文件，而不是承載即時流量。

在[了解計劃和計劃類型](program-types.md)，文件中了解有關計劃類型的更多資訊

## 建立沙箱計畫 {#create}

請依照以下步驟建立沙箱計畫。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 從 Cloud Manager 的登陸頁面，按一下畫面的右上角的&#x200B;**新增計畫**。

   ![Cloud Manager 登陸頁面](assets/cloud-manager-my-programs.png)

1. 從建立程序精靈中，選取&#x200B;**設定沙箱**，並提供程序名稱。

   ![程序類型建立](assets/create-sandbox.png)

1. 或者，您可以將影像檔拖放到&#x200B;**新增程序影像**&#x200B;目標或按一下它從檔案瀏覽器選取影像，藉此新增影像到程序。點選或按一下&#x200B;**繼續**。

   * 該影像僅做為程序概觀視窗的圖磚，有助於識別程序。

1. 在&#x200B;**設定沙箱**&#x200B;對話框中，按一下&#x200B;**解決方案和附加元件**&#x200B;表格中的選項，選擇要在沙箱程序中啟用的解決方案。

   * 使用解決方案名稱旁邊的 > 形符號來顯示解決方案的其他選用的附加元件。

   * 沙箱程序中一律包含 **Sites** 和 **Assets** 解決方案，無法取消選取。

   ![為沙箱選取解決方案和附加元件](assets/sandbox-solutions-add-ons.png)

1. 為沙箱選取解決方案和附加元件後，點選/按一下&#x200B;**建立**。

隨著設定過程的進行，您將在登陸頁面上看到一個帶有狀態指示器的新沙箱程序卡。

![從概覽頁面建立沙箱](assets/sandbox-setup.png)

## 沙箱存取 {#access}

您可以透過查看計劃概覽頁面查看沙箱設定的詳細資訊以及存取環境 (一旦可用)。

1. 在 Cloud Manager 登陸頁面中，單擊新建立程序上的省略符號按鈕。

   ![存取計劃總覽](assets/program-overview-sandbox.png)

1. 專案建立步驟完成後，您可以存取 **存取存放庫資訊** 連結以使用您的Git存放庫。

   ![計劃設定](assets/create-program4.png)

   >[!TIP]
   >
   >要了解有關存取和管理 git 存放庫的更多資訊，請參閱文件[存取 Git](/help/implementing/cloud-manager/managing-code/accessing-repos.md)

1. 建立開發環境後，您可以使用&#x200B;**存取 AEM**&#x200B;連結來登入 AEM。

   ![存取 AEM 連結](assets/create-program-5.png)

1. 部署到開發的非生產管道完成後，安裝精靈將引導您存取 AEM 開發環境或將計劃碼部署到開發環境。

   ![部署沙箱](assets/create-program-setup-deploy.png)

如果您在任何時候需要切換到另一個計劃或返回概覽頁面來建立另一個計劃，請點擊畫面左上角的計劃名稱以顯示&#x200B;**瀏覽**&#x200B;選項。

![瀏覽到](assets/create-program-a1.png)
