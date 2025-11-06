---
title: 如何針對AEM Forms as a Cloud Service環境的安裝和設定問題進行疑難排解？
description: 疑難排解AEM Forms as a Cloud Service環境的安裝和設定。
contentOwner: khsingh
feature: Adaptive Forms
role: User
exl-id: 249ec8f2-4176-428a-bfcf-80b381ec7263
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 1%

---

# 設定 {#installation-and-configuration}

設定Cloud Service環境時，您可能會遇到下列一些問題：

## Forms選項無法使用

**[!UICONTROL Forms]**&#x200B;選項在&#x200B;**[!UICONTROL 導覽]**&#x200B;頁面上無法使用。

![Forms選項無法使用](assets/installation-configuration-forms-option-unavailable-troubleshooting.png)

若要啟用&#x200B;**[!UICONTROL Forms]**&#x200B;選項：

1. 登入[Cloud Manager](https://experience.adobe.com/)
1. 找到您的程式，然後按一下![Forms選項無法使用](assets/Smock_Edit_18_N.svg)圖示。 它會開啟您計畫的編輯計畫頁面。
1. 開啟&#x200B;**[!UICONTROL 解決方案和附加元件]**&#x200B;標籤。
1. 選取&#x200B;**[!UICONTROL Forms]**&#x200B;選項並按一下&#x200B;**[!UICONTROL 儲存]**。

   ![選取Forms選項](assets/installation-configuration-select-forms-option.png)

1. [建立](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html?lang=en#how-to-use)和[執行](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html)生產和非生產管道。

建置和部署管道後，**[!UICONTROL 導覽]**&#x200B;頁面上的&#x200B;**[!UICONTROL Forms]**&#x200B;選項。

<!--  
## Environment creation fails {#environment-creation-fails}

Users are unable to create an [!DNL AEM Forms] as a Cloud Service environment. The environment creation fails after running for some time.

A missing profile can lead to environment creation failure. Check that the profile exists in Admin Console. If the profile does not exist, perform the following steps to create the profile:

1. Log in to [Admin Console](https://adminconsole.adobe.com/). Use Adobe ID of administrator provisioned to use Automated Forms Conversion Service to login. Do not any other ID or Federated ID to login.
1. Click the **[!UICONTROL Automated Forms Conversion Service]** option.
1. Click **[!UICONTROL New Profile]** in the Products tab.
1. Specify Name, Display Name, and Description for the profile. Click **[!UICONTROL Done]**. A profile is created.

If the profile exists and issues still persist, contact Adobe Support. -->

## 建置管道失敗 {#build-pipeline-fails}

使用者無法執行建置管道。 管道執行一段時間後就會失敗。

若要解決此問題，請開啟Cloud Manager，為您的環境選取&#x200B;**[!UICONTROL 更新]**&#x200B;選項，然後執行管道。


## 套件組合未處於作用中狀態 {#bundles-inactive-state}

若要解決此問題，請執行以下步驟：

1. 啟動AEM，並等待它完全啟動，直到所有套件組合都已啟動。
1. 停止AEM (Ctrl + C)。
1. 將Forms `.far`檔案放在安裝資料夾中。
1. 重新啟動AEM伺服器。