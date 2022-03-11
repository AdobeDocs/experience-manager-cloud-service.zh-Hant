---
title: '安裝和配置疑難解答  '
seo-title: Troubleshooting installation and configuration
description: 安裝和配置疑難解答
seo-description: Troubleshooting installation and configuration
contentOwner: khsingh
exl-id: 249ec8f2-4176-428a-bfcf-80b381ec7263
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# 設定 {#installation-and-configuration}

在配置Cloud Service環境時，您可能會遇到以下一些問題：

## Forms選項不可用

的 **[!UICONTROL Forms]** 選項 **[!UICONTROL 導航]** 的子菜單。

![Forms選項不可用](assets/installation-configuration-forms-option-unavailable-troubleshooting.png)

啟用 **[!UICONTROL Forms]** 選項：

1. 登錄到 [雲管理器](https://experience.adobe.com/)
1. 找到您的程式，然後按一下 ![Forms選項不可用](assets/Smock_Edit_18_N.svg) 表徵圖 它將開啟程式的「編輯程式」頁。
1. 開啟 **[!UICONTROL 解決方案和附加模組]** 頁籤。
1. 選擇 **[!UICONTROL Forms]** 選項，然後按一下 **[!UICONTROL 保存]**。

   ![選擇Forms選項](assets/installation-configuration-select-forms-option.png)
1. [建立](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html?lang=en#how-to-use) 和 [運行](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html) 生產及非生產管道。

在構建和部署管道後， **[!UICONTROL Forms]** 的上界 **[!UICONTROL 導航]** 的子菜單。

<!--  
## Environment creation fails {#environment-creation-fails}

Users are unable to create an [!DNL AEM Forms] as a Cloud Service environment. The environment creation fails after running for some time.

A missing profile can lead to environment creation failure. Check that the profile exists in Admin Console. If the profile does not exist, perform the following steps to create the profile:

1. Log in to [Admin Console](https://adminconsole.adobe.com/). Use Adobe ID of administrator provisioned to use Automated Forms Conversion Service to login. Do not any other ID or Federated ID to login.
1. Click the **[!UICONTROL Automated Forms Conversion Service]** option.
1. Click **[!UICONTROL New Profile]** in the Products tab.
1. Specify Name, Display Name, and Description for the profile. Click **[!UICONTROL Done]**. A profile is created.

If the profile exists and issues still persist, contact Adobe Support. -->

## 生成管道失敗 {#build-pipeline-fails}

用戶無法運行生成管道。 管道在運行一段時間後失敗。

要解決此問題，請開啟雲管理器，選擇 **[!UICONTROL 更新]** 選項，然後運行管線。
