---
title: 如何針對最適化表單設定Microsoft Dynamics 365和Salesforce現成可用的表單資料模型？
description: 了解如何將Microsoft Dynamics 365和Salesforce與最適化表單整合。
exl-id: 2a43b2db-2dfb-4c79-88be-ea770b44dac1
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 0%

---

# 設定 [!DNL Microsoft Dynamics 365] 和 [!DNL Salesforce] 雲端服務 {#configure-azure-storage}

[[!DNL Experience Manager Forms] 資料整合](data-integration.md) proves [!DNL Microsoft Dynamics 365] 和 [!DNL Salesforce] 雲端服務，將最適化表單與現成可用的表單資料模型整合。 隨後適用性Forms便可與 [!DNL Microsoft Dynamics 365] 和 [!DNL Salesforce] 伺服器，以啟用業務工作流程。 例如：

* 將資料寫入 [!DNL Microsoft Dynamics 365] 和 [!DNL Salesforce] 在適用性表單提交時。
* 將資料寫入 [!DNL Microsoft Dynamics 365] 和 [!DNL Salesforce] 透過「表單資料模型」中定義的自訂實體，反之亦然。
* 查詢 [!DNL Microsoft Dynamics 365] 和 [!DNL Salesforce] 伺服器以取得資料並預先填入適用性Forms。
* 從讀取資料 [!DNL Microsoft Dynamics 365] 和 [!DNL Salesforce] 伺服器。

[!DNL Microsoft Dynamics 365] 和 [!DNL Salesforce] 雲端服務和表單資料模型可立即在 [!DNL AEM Forms] 伺服器 [基於Experience Manager原型設定Forms開發專案](setup-local-development-environment.md##forms-cloud-service-local-development-environment).

>[!NOTE]
>
>Microsoft Dynamics 365和 [!DNL Salesforce] 只有當您設定 [!DNL Experience Manager Forms] as a [!DNL Cloud Service] 基於 [AEM原型30](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-30) 或更新版本。

## 設定 [!DNL Salesforce] 雲端服務 {#configure-salesforce-cloud-service}

在設定 [!DNL Salesforce] 雲端服務，請確定您執行下列工作：

* [建立已連線的OAuth啟用 [!DNL Salesforce] 應用程式](https://help.salesforce.com/s/articleView?id=sf.connected_app_create_api_integration.htm&amp;type=5). 建立已連接的 [!DNL Salesforce] 應用程式中，以下列格式指定回呼URL:

   ```
   https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
   ```

   其中，伺服器和埠是指 [!DNL AEM Forms] 伺服器。

* 建立已連接 [!DNL Salesforce] 應用程式，指定 `full` 和 `offline_access` 作為OAuth範圍的值。

* 記下連線應用程式的用戶端ID（稱為使用者金鑰）和用戶端密碼（稱為使用者密碼）的值。

執行下列步驟以設定 [!DNL Salesforce] 雲端服務：

1. 開啟 [!DNL AEM Forms] 製作例項，導覽至 **[!UICONTROL 工具]** ![錘](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL 資料來源]**. 可用包裝資料夾的清單包括一個資料夾，其標題為 `DappTitle`  whel [產生AEM原型專案](setup-local-development-environment.md##forms-cloud-service-local-development-environment).
1. 點選資料夾名稱，選取 **[!UICONTROL Salesforce雲配置]**，然後點選 **[!UICONTROL 屬性]**.
1. 在 **[!UICONTROL 驗證設定]** 標籤：
   1. 指定 [!DNL Salesforce] 中的網域URL **[!UICONTROL 主機]** 欄位。 例如， [域名].my.salesforce.com。
   1. 指定所連線應用程式的用戶端ID（即使用者金鑰）和用戶端密碼（即使用者密碼）。
   1. 指定 **full offline_access** (`full` 和 `offine_access` 值（以空格分隔） **[!UICONTROL 授權範圍]** 欄位。
   1. 點選 **[!UICONTROL 連線至OAuth]**. 系統會將您重新導向至 [!DNL Microsoft Dynamics] 登入頁面。
   1. 使用 [!DNL Salesforce] 憑證並接受，以允許雲端服務設定連線至 [!DNL Salesforce] 服務。 如果連線成功，系統會將您重新導向至 [!DNL Salesforce] 雲端服務設定頁面，其中顯示成功訊息。
1. 點選 **[!UICONTROL 儲存並關閉]** 完成配置設定。

### 立即存取 [!DNL Salesforce] 表單資料模型

A [!DNL Salesforce] 「表單資料模型」可立即在 [!DNL AEM Forms] 伺服器 [基於Experience Manager原型設定Forms開發專案](setup-local-development-environment.md##forms-cloud-service-local-development-environment).

若要存取「表單資料模型」，請導覽至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL 資料整合]**. 可用資料夾清單包含一個資料夾，其標題為 `DappTitle`  whel [產生AEM原型專案](setup-local-development-environment.md##forms-cloud-service-local-development-environment). 點選資料夾名稱，選取 **[!UICONTROL Salesforce資料模型]**，然後點選「編輯」 ![編輯](assets/edit.png) 圖示來檢視表單資料模型。

設定 [[!DNL Salesforce] 雲端設定服務](#configure-salesforce-cloud-service)，您可以將最適化表單與現成可用的 [!DNL Salesforce] 資料模型。

## 設定 [!DNL Microsoft Dynamics 365] 雲端服務 {#configure-dynamics-cloud-service}

在設定 [!DNL Microsoft Dynamics 365] 雲端服務，請確定您執行下列工作：

* [註冊申請 [!DNL Microsoft Dynamics 365] 與Azure Active Directory](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/walkthrough-register-app-azure-active-directory). 建立已連接的 [!DNL Microsoft Dynamics 365] ，請以下列格式指定「回覆URL」：

   ```
   https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
   ```

   其中，伺服器和埠是指 [!DNL AEM Forms] 伺服器。

* 記下用戶端ID（也稱為應用程式ID）和所連線應用程式的用戶端密碼。

執行下列步驟以設定 [!DNL Microsoft Dynamics 365] 雲端服務：

1. 開啟 [!DNL AEM Forms] 製作例項，導覽至 **[!UICONTROL 工具]** ![錘](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL 資料來源]**. 可用包裝資料夾的清單包括一個資料夾，其標題為 `DappTitle`  whel [產生AEM原型專案](setup-local-development-environment.md##forms-cloud-service-local-development-environment).
1. 點選資料夾名稱，選取 **[!UICONTROL Microsoft Dynamics 365雲端設定]**，然後點選 **[!UICONTROL 屬性]**.
1. 在 **[!UICONTROL 驗證設定]** 標籤：
   1. 輸入 **[!UICONTROL 服務根]** 欄位。 前往Dynamics例項，並導覽至 [開發人員資源](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/view-download-developer-resources) 查看「服務根」欄位的值。 例如， `https://<tenant-name>.dynamics.com/api/data/v9.1/`
   1. 指定所連接應用程式的用戶端ID（即「應用程式ID」）和用戶端密碼。
   1. 取代 `{tenant}` 在 **[!UICONTROL OAuth URL]**, **[!UICONTROL 重新整理Token URL]**，和 **[!UICONTROL 存取權杖URL]** 欄位。
   1. 在 **[!UICONTROL 資源]** 配置欄位 [!UICONTROL Microsoft Dynamics] 表單資料模型。 使用服務根URL來衍生Dynamics實例URL。 例如， `https://<tenant-name>.dynamics.com`.

   1. 指定 `openid` 在 **[!UICONTROL 授權範圍]** 授權處理的欄位 [!DNL Microsoft Dynamics 365].
   1. 使用 [!DNL Microsoft Dynamics 365] 憑證並接受，以允許雲端服務設定連線至 [!DNL Microsoft Dynamics 365] 服務。 如果連線成功，系統會將您重新導向至 [!DNL Microsoft Dynamics 365] 雲端服務設定頁面，其中顯示成功訊息。
1. 點選 **[!UICONTROL 儲存並關閉]** 完成配置設定。

### 立即存取 [!DNL Microsoft Dynamics 365] 表單資料模型

A [!DNL Microsoft Dynamics 365] 「表單資料模型」可立即在 [!DNL AEM Forms] 伺服器 [基於Experience Manager原型設定Forms開發專案](setup-local-development-environment.md##forms-cloud-service-local-development-environment).

若要存取「表單資料模型」，請導覽至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL 資料整合]**. 可用資料夾清單包含一個資料夾，其標題為 `DappTitle`  whel [產生AEM原型專案](setup-local-development-environment.md##forms-cloud-service-local-development-environment). 點選資料夾名稱，選取 **[!UICONTROL Microsoft Dynamics 365資料模型]**，然後點選「編輯」 ![編輯](assets/edit.png) 圖示來檢視表單資料模型。

設定 [[!DNL Microsoft Dynamics 365] 雲端設定服務](#configure-dynamics-cloud-service)，您可以將最適化表單與現成可用的 [!DNL Microsoft Dynamics 365] 資料模型。
