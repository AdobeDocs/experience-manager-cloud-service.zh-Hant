---
title: 如何配置MicrosoftDynamics 365和Salesforce的現成的表單資料模型以適應表單？
description: 瞭解如何將MicrosoftDynamics 365和Salesforce與自適應表單整合。
exl-id: 2a43b2db-2dfb-4c79-88be-ea770b44dac1
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 0%

---

# 設定[!DNL Microsoft Dynamics 365]和[!DNL Salesforce]雲端服務 {#configure-azure-storage}

[[!DNL Experience Manager Forms] 資料整合](data-integration.md) 提供 [!DNL Microsoft Dynamics 365] 和 [!DNL Salesforce] 雲服務將自適應表單與現成的表單資料模型整合。 自適應Forms可以與 [!DNL Microsoft Dynamics 365] 和 [!DNL Salesforce] 伺服器以啟用業務工作流。 例如：

* 將資料寫入 [!DNL Microsoft Dynamics 365] 和 [!DNL Salesforce] 在自適應表單提交上。
* 將資料寫入 [!DNL Microsoft Dynamics 365] 和 [!DNL Salesforce] 定義的自定義圖元，反之亦然。
* 查詢 [!DNL Microsoft Dynamics 365] 和 [!DNL Salesforce] 用於資料和預填充AdaptiveForms。
* 從中讀取資料 [!DNL Microsoft Dynamics 365] 和 [!DNL Salesforce] 伺服器。

[!DNL Microsoft Dynamics 365] 和 [!DNL Salesforce] 雲服務和表單資料模型可在 [!DNL AEM Forms] 伺服器 [基於Experience Manager原型的Forms開發項目](setup-local-development-environment.md##forms-cloud-service-local-development-environment)。

>[!NOTE]
>
>Microsoft動力365和 [!DNL Salesforce] 只有在您設定了 [!DNL Experience Manager Forms] 作為 [!DNL Cloud Service] 基於 [原型AEM30](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-30) 或稍後。

## 配置 [!DNL Salesforce] 雲服務 {#configure-salesforce-cloud-service}

在配置 [!DNL Salesforce] 雲服務，確保執行以下任務：

* [建立已連接的啟用OAuth的 [!DNL Salesforce] 應用](https://help.salesforce.com/s/articleView?id=sf.connected_app_create_api_integration.htm&amp;type=5)。 建立已連接的 [!DNL Salesforce] ，請按以下格式指定回調URL:

   ```
   https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
   ```

   其中，伺服器和埠指的是 [!DNL AEM Forms] 伺服器。

* 建立已連接的 [!DNL Salesforce] 應用程式，指定 `full` 和 `offline_access` 作為OAuth作用域的值。

* 請記下所連接應用程式的客戶端ID（稱為Consumer Key）和客戶端密鑰（稱為Consumer Secret）的值。

執行以下步驟來配置 [!DNL Salesforce] 雲服務：

1. 開 [!DNL AEM Forms] 作者實例，導航 **[!UICONTROL 工具]** ![錘](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL 資料源]**。 可用包裝資料夾清單包括具有為指定標題的資料夾 `DappTitle`  同時 [生成原AEM型項目](setup-local-development-environment.md##forms-cloud-service-local-development-environment)。
1. 點擊資料夾名稱，選擇 **[!UICONTROL Salesforce雲配置]**，然後點擊 **[!UICONTROL 屬性]**。
1. 在 **[!UICONTROL 驗證設定]** 頁籤：
   1. 指定 [!DNL Salesforce] 中的域URL **[!UICONTROL 主機]** 的子菜單。 比如說， [域名].my.salesforce.com。
   1. 為連接的應用程式指定客戶端ID（稱為Consumer Key）和客戶端機密（稱為Consumer Secret）。
   1. 指定 **完全離線訪問** (`full` 和 `offine_access` 值（用空格分隔） **[!UICONTROL 授權範圍]** 的子菜單。
   1. 點擊 **[!UICONTROL 連接到OAuth]**。 您被重定向到 [!DNL Microsoft Dynamics] 登錄頁。
   1. 使用 [!DNL Salesforce] 憑據，並接受允許雲服務配置連接到 [!DNL Salesforce] 服務。 如果連接成功，您將重定向到 [!DNL Salesforce] 「雲服務配置」頁，其中顯示成功消息。
1. 點擊 **[!UICONTROL 保存並關閉]** 完成配置設定。

### 出機 [!DNL Salesforce] 窗體資料模型

A [!DNL Salesforce] 窗體資料模型在 [!DNL AEM Forms] 伺服器 [基於Experience Manager原型的Forms開發項目](setup-local-development-environment.md##forms-cloud-service-local-development-environment)。

要訪問表單資料模型，請導航至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL 資料整合]**。 可用資料夾清單包括為指定標題的資料夾 `DappTitle`  同時 [生成原AEM型項目](setup-local-development-environment.md##forms-cloud-service-local-development-environment)。 點擊資料夾名稱，選擇 **[!UICONTROL Salesforce資料模型]**，然後按一下編輯 ![編輯](assets/edit.png) 表徵圖。

配置 [[!DNL Salesforce] 雲配置服務](#configure-salesforce-cloud-service)，可將自適應表單與出廠設定整合 [!DNL Salesforce] 資料模型。

## 配置 [!DNL Microsoft Dynamics 365] 雲服務 {#configure-dynamics-cloud-service}

在配置 [!DNL Microsoft Dynamics 365] 雲服務，確保您執行以下任務：

* [註冊申請 [!DNL Microsoft Dynamics 365] 使用Azure Active Directory](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/walkthrough-register-app-azure-active-directory)。 建立已連接的 [!DNL Microsoft Dynamics 365] ，請按以下格式指定答復URL:

   ```
   https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
   ```

   其中，伺服器和埠指的是 [!DNL AEM Forms] 伺服器。

* 記下所連接應用程式的客戶端ID（也稱為應用程式ID）和客戶端機密的值。

執行以下步驟來配置 [!DNL Microsoft Dynamics 365] 雲服務：

1. 開 [!DNL AEM Forms] 作者實例，導航 **[!UICONTROL 工具]** ![錘](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL 資料源]**。 可用包裝資料夾清單包括具有為指定標題的資料夾 `DappTitle`  同時 [生成原AEM型項目](setup-local-development-environment.md##forms-cloud-service-local-development-environment)。
1. 點擊資料夾名稱，選擇 **[!UICONTROL MicrosoftDynamics 365雲配置]**，然後點擊 **[!UICONTROL 屬性]**。
1. 在 **[!UICONTROL 驗證設定]** 頁籤：
   1. 輸入 **[!UICONTROL 服務根]** 的子菜單。 轉至Dynamics實例並導航至 [開發人員資源](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/view-download-developer-resources) 查看「服務根」欄位的值。 例如， `https://<tenant-name>.dynamics.com/api/data/v9.1/`
   1. 為連接的應用程式指定客戶端ID（稱為應用程式ID）和客戶端密鑰。
   1. 替換 `{tenant}` 租戶ID **[!UICONTROL OAuth URL]**。 **[!UICONTROL 刷新標籤URL]**, **[!UICONTROL 訪問令牌URL]** 的子菜單。
   1. 在中指定動態實例URL **[!UICONTROL 資源]** 欄位 [!UICONTROL Microsoft動力] 的下界。 使用服務根URL可導出Dynamics實例URL。 比如說， `https://<tenant-name>.dynamics.com`。

   1. 指定 `openid` 的 **[!UICONTROL 授權範圍]** 在上的授權進程欄位 [!DNL Microsoft Dynamics 365]。
   1. 使用 [!DNL Microsoft Dynamics 365] 憑據，並接受允許雲服務配置連接到 [!DNL Microsoft Dynamics 365] 服務。 如果連接成功，您將重定向到 [!DNL Microsoft Dynamics 365] 「雲服務配置」頁，其中顯示成功消息。
1. 點擊 **[!UICONTROL 保存並關閉]** 完成配置設定。

### 出機 [!DNL Microsoft Dynamics 365] 窗體資料模型

A [!DNL Microsoft Dynamics 365] 窗體資料模型在 [!DNL AEM Forms] 伺服器 [基於Experience Manager原型的Forms開發項目](setup-local-development-environment.md##forms-cloud-service-local-development-environment)。

要訪問表單資料模型，請導航至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL 資料整合]**。 可用資料夾清單包括為指定標題的資料夾 `DappTitle`  同時 [生成原AEM型項目](setup-local-development-environment.md##forms-cloud-service-local-development-environment)。 點擊資料夾名稱，選擇 **[!UICONTROL MicrosoftDynamics 365資料模型]**，然後按一下編輯 ![編輯](assets/edit.png) 表徵圖。

配置 [[!DNL Microsoft Dynamics 365] 雲配置服務](#configure-dynamics-cloud-service)，可將自適應表單與出廠設定整合 [!DNL Microsoft Dynamics 365] 資料模型。
