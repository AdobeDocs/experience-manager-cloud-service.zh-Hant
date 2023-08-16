---
title: 建立沙箱計畫
description: 了解如何使用 Cloud Manager 建立您自己的沙箱計畫，用於訓練、展示、POC 或其他非生產目的。
exl-id: 10011392-3059-4bb0-88db-0af1d390742e
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: ht
source-wordcount: '444'
ht-degree: 100%

---

# 建立沙箱計畫 {#create-sandbox-program}

沙箱計畫通常建立的目的是提供訓練、執行範例、啟用、POC 或文件，而不是承載即時流量。

在[了解計畫和計畫類型](program-types.md)，文件中了解有關計畫類型的更多資訊

## 建立沙箱計畫 {#create}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 在 Cloud Manager 登陸頁面右上角附近，按一下「**新增計畫**」。

   ![Cloud Manager 登陸頁面](assets/cloud-manager-my-programs.png)

1. 從建立計畫精靈中，選取&#x200B;**設定沙箱**，並提供計畫名稱。

   ![計畫類型建立](assets/create-sandbox.png)

1. 或者，您可以將影像檔拖放到&#x200B;**新增計畫影像**&#x200B;目標或按一下它從檔案瀏覽器選取影像，藉此新增影像到計畫。點選或按一下&#x200B;**繼續**。

   * 該影像僅做為計畫概觀視窗的圖磚，有助於識別計畫。

1. 在&#x200B;**設定沙箱**&#x200B;對話框中，按一下&#x200B;**解決方案和附加元件**&#x200B;表格中的選項，選擇要在沙箱計畫中啟用的解決方案。

   * 使用解決方案名稱旁邊的 > 形符號，可以查看解決方案的其他選用的附加元件。

   * 沙箱計畫中一律包含 **Sites** 和 **Assets** 解決方案，無法取消選取。

   ![為沙箱選取解決方案和附加元件](assets/sandbox-solutions-add-ons.png)

1. 為沙箱選取解決方案和附加元件後，按一下「**建立**」。

隨著設定過程的進行，您會在登陸頁面上看到一個帶有狀態指示器的新沙箱計畫卡。

![從概覽頁面建立沙箱](assets/sandbox-setup.png)

## 沙箱存取 {#access}

您可以透過查看計畫概覽頁面查看沙箱設定的詳細資訊以及存取環境 (一旦可用)。

1. 在 Cloud Manager 登陸頁面中，單擊新建立程序上的省略符號按鈕。

   ![存取計畫概觀](assets/program-overview-sandbox.png)

1. 專案建立步驟完成後，您可以存取&#x200B;**Access 回購資訊**&#x200B;連結，以便能夠使用您的 git repo。

   ![計畫設定](assets/create-program4.png)

   >[!TIP]
   >
   >若要了解有關存取和管理 git 存放庫的詳細資訊，請參閱[存取 Git](/help/implementing/cloud-manager/managing-code/accessing-repos.md)

1. 建立開發環境後，您可以使用&#x200B;**存取 AEM**&#x200B;連結來登入 AEM。

   ![存取 AEM 連結](assets/create-program-5.png)

1. 部署到開發的非生產管道完成後，安裝精靈將引導您存取 AEM 開發環境或將程式碼部署到開發環境。

   ![部署沙箱](assets/create-program-setup-deploy.png)

如果必須切換到另一個計畫或返回概覽頁面來建立另一個計畫，請按一下畫面左上角的計畫名稱以顯示「**瀏覽**」選項。

![瀏覽到](assets/create-program-a1.png)
