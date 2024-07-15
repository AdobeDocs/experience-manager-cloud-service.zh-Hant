---
title: 建立沙箱計畫
description: 了解如何使用 Cloud Manager 建立您自己的沙箱計畫，用於訓練、展示、POC 或其他非生產目的。
exl-id: 10011392-3059-4bb0-88db-0af1d390742e
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 74%

---

# 建立沙箱計畫 {#create-sandbox-program}

沙箱計畫通常建立的目的是提供訓練、執行範例、啟用、POC 或文件，而不是承載即時流量。

在[了解計畫和計畫類型](program-types.md)，文件中了解有關計畫類型的更多資訊

## 建立沙箱計畫 {#create}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 在&#x200B;**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;主控台上，點選或按一下熒幕右上角附近的&#x200B;**新增程式**。

   ![Cloud Manager 登陸頁面](assets/log-in.png)

1. 從建立計畫精靈中，選取&#x200B;**設定沙箱**，並提供計畫名稱。

   ![計畫類型建立](assets/create-sandbox.png)

1. 或者，您可以將影像檔拖放到&#x200B;**新增計畫影像**&#x200B;目標或按一下它從檔案瀏覽器選取影像，藉此新增影像到計畫。選取「**繼續**」。

   * 該影像僅做為計畫概觀視窗的圖磚，有助於識別計畫。

1. 在&#x200B;**設定您的沙箱**&#x200B;對話方塊中，核取&#x200B;**解決方案和附加元件**&#x200B;表格中的選項，選擇要在沙箱程式中啟用的解決方案。

   * 使用解決方案名稱旁邊的 > 形符號，可以查看解決方案的其他選用的附加元件。

   * 沙箱計畫中一律包含 **Sites** 和 **Assets** 解決方案，無法取消選取。

   ![為沙箱選取解決方案和附加元件](assets/sandbox-solutions-add-ons.png)

1. 為沙箱選取解決方案和附加元件後，按一下「**建立**」。

隨著設定過程的進行，您會在登陸頁面上看到一個帶有狀態指示器的新沙箱計畫卡。

![從概覽頁面建立沙箱](assets/sandbox-setup.png)

## 沙箱存取 {#access}

您可以透過查看計畫概覽頁面查看沙箱設定的詳細資訊以及存取環境 (一旦可用)。

1. 從Cloud Manager登陸頁面，按一下您建立之方案上的省略符號按鈕。

   ![存取計畫概觀](assets/program-overview-sandbox.png)

1. 專案建立步驟完成後，您可以存取&#x200B;**Access 回購資訊**&#x200B;連結，以便能夠使用您的 git repo。

   ![計畫設定](assets/create-program4.png)

   >[!TIP]
   >
   >若要了解有關存取和管理 git 存放庫的詳細資訊，請參閱[存取 Git](/help/implementing/cloud-manager/managing-code/accessing-repos.md)

1. 建立開發環境後，您可以使用&#x200B;**存取 AEM**&#x200B;連結來登入 AEM。

   ![存取 AEM 連結](assets/create-program5.png)

1. 部署到開發的非生產管道完成後，行動號召中的精靈將引導您存取AEM開發環境或將計畫碼部署到開發環境。

   ![部署沙箱](assets/create-program-setup-deploy.png)

>[!TIP]
>
>如需如何導覽Cloud Manager及瞭解&#x200B;**我的程式**&#x200B;主控台的詳細資訊，請參閱檔案[瀏覽Cloud Manager UI](/help/implementing/cloud-manager/navigation.md)。
