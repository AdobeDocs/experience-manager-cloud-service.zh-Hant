---
title: 如何為最適化Forms設定現成的Microsoft Dynamics 365和Salesforce表單資料模型？
description: 瞭解如何將Microsoft Dynamics 365和Salesforce與最適化Forms整合。
feature: Adaptive Forms, Form Data Model
role: User, Developer
exl-id: 2a43b2db-2dfb-4c79-88be-ea770b44dac1
source-git-commit: 527c9944929c28a0ef7f3e617ef6185bfed0d536
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 2%

---

# 設定Microsoft® Dynamics 365或Salesforce for AEM Forms {#configure-azure-storage}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/oauth2-client-credentials-flow-for-server-to-server-integration.html) |
| AEM as a Cloud Service  | 本文章 |

[[!DNL Experience Manager Forms] 資料整合](data-integration.md) 提供 [!DNL Microsoft® Dynamics 365] 和 [!DNL Salesforce] 雲端服務，整合最適化表單與立即可用的表單資料模型。 最適化Forms然後可以與 [!DNL Microsoft® Dynamics 365] 和 [!DNL Salesforce] 伺服器以啟用業務工作流程。 例如：

* 將資料寫入 [!DNL Microsoft® Dynamics 365] 和 [!DNL Salesforce] 於最適化表單提交時。
* 將資料寫入 [!DNL Microsoft® Dynamics 365] 和 [!DNL Salesforce] 透過「表單資料模型」中定義的自訂實體，反之亦然。
* 查詢 [!DNL Microsoft® Dynamics 365] 和 [!DNL Salesforce] 資料及預先填入Adaptive Forms的伺服器。
* 從讀取資料 [!DNL Microsoft® Dynamics 365] 和 [!DNL Salesforce] 伺服器。

[!DNL Microsoft® Dynamics 365] 和 [!DNL Salesforce] 雲端服務和表單資料模型可在上立即使用 [!DNL AEM Forms] 在您之後的伺服器 [根據Experience Manager原型設定Forms的開發專案](setup-local-development-environment.md#forms-cloud-service-local-development-environment).

>[!NOTE]
>
>Microsoft® Dynamics 365和 [!DNL Salesforce] 雲端服務和表單資料模型僅在您設定後，才可立即使用 [!DNL Experience Manager Forms] as a [!DNL Cloud Service] 專案依據 [AEM Archetype 30](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-30) 或更新版本。

## 設定 [!DNL Salesforce] 雲端服務 {#configure-salesforce-cloud-service}

設定之前 [!DNL Salesforce] 雲端服務，請確定您執行下列工作：

* [建立已啟用OAuth的連線 [!DNL Salesforce] 應用計畫](https://help.salesforce.com/s/articleView?id=sf.connected_app_create_api_integration.htm&amp;type=5). 當您建立連線時 [!DNL Salesforce] 應用程式，請以下列格式指定回呼URL：

  ```
  https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
  ```

  其中伺服器和連線埠代表 [!DNL AEM Forms] 伺服器。

* 建立連線時 [!DNL Salesforce] 應用程式，指定 `full` 和 `offline_access` 做為OAuth範圍的值。

* 記下連線應用程式的使用者端ID （稱為使用者金鑰）和使用者端密碼（稱為使用者密碼）的值。

執行以下步驟來設定 [!DNL Salesforce] 雲端服務：

1. 開啟 [!DNL AEM Forms] 作者例項，瀏覽至 **[!UICONTROL 工具]** ![錘子](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL 資料來源]**. 可用包裝函式資料夾清單包含一個資料夾，其標題已指定給 `DappTitle`  當 [產生AEM原型專案](setup-local-development-environment.md#forms-cloud-service-local-development-environment).
1. 選取資料夾名稱，選取 **[!UICONTROL Salesforce雲端設定]**，並選取 **[!UICONTROL 屬性]**.
1. 在 **[!UICONTROL 驗證設定]** 標籤：
   1. 指定 [!DNL Salesforce] 中的網域URL **[!UICONTROL 主機]** 欄位。 例如， [網域名稱].my.salesforce.com.
   1. 為連線的應用程式指定使用者端ID （稱為使用者金鑰）和使用者端密碼（稱為使用者密碼）。
   1. 指定 **full offline_access** (`full` 和 `offine_access` 值（以空格分隔） **[!UICONTROL 授權範圍]** 欄位。
   1. 選取 **[!UICONTROL 連線至OAuth]**. 您被重新導向至 [!DNL Microsoft® Dynamics] 登入頁面。
   1. 使用您的帳戶登入 [!DNL Salesforce] 認證並接受，以允許雲端服務設定連線至 [!DNL Salesforce] 服務。 如果連線成功，您將被重新導向至 [!DNL Salesforce] 雲端服務設定頁面，顯示成功訊息。
1. 選取 **[!UICONTROL 儲存並關閉]** 以完成組態設定。

### 開箱即用的存取權 [!DNL Salesforce] 表單資料模型

A [!DNL Salesforce] 表單資料模型可立即在 [!DNL AEM Forms] 在您之後的伺服器 [根據Experience Manager原型設定Forms的開發專案](setup-local-development-environment.md#forms-cloud-service-local-development-environment).

若要存取表單資料模型，請導覽至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL 資料整合]**. 可用資料夾清單包括一個具有指定標題的資料夾 `DappTitle`  當 [產生AEM原型專案](setup-local-development-environment.md#forms-cloud-service-local-development-environment). 選取資料夾名稱，然後選取 **[!UICONTROL Salesforce資料模型]**，然後選取編輯 ![編輯](assets/edit.png) 圖示以檢視表單資料模型。

設定後 [[!DNL Salesforce] 雲端設定服務](#configure-salesforce-cloud-service)，您就可以直接整合最適化表單與最適化表單 [!DNL Salesforce] 資料模型。

## 設定 [!DNL Microsoft® Dynamics 365] 雲端服務 {#configure-dynamics-cloud-service}

設定之前 [!DNL Microsoft® Dynamics 365] cloud service，請確定您執行下列工作：

* [註冊應用程式 [!DNL Microsoft® Dynamics 365] 使用Azure Active Directory](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/walkthrough-register-app-azure-active-directory). 當您建立連線時 [!DNL Microsoft® Dynamics 365] 應用程式，請以下列格式指定回覆URL：

  ```
  https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
  ```

  其中伺服器和連線埠代表 [!DNL AEM Forms] 伺服器。

* 記下所連線應用程式的使用者端ID （也稱為應用程式ID）和使用者端密碼的值。

執行以下步驟來設定 [!DNL Microsoft® Dynamics 365] 雲端服務：

1. 開啟 [!DNL AEM Forms] 作者例項，瀏覽至 **[!UICONTROL 工具]** ![錘子](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL 資料來源]**. 可用包裝函式資料夾清單包含一個資料夾，其標題已指定給 `DappTitle`  當 [產生AEM原型專案](setup-local-development-environment.md#forms-cloud-service-local-development-environment).
1. 選取資料夾名稱，選取 **[!UICONTROL Microsoft® Dynamics 365雲端設定]**，並選取 **[!UICONTROL 屬性]**.
1. 在 **[!UICONTROL 驗證設定]** 標籤：
   1. 輸入值 **[!UICONTROL 服務根目錄]** 欄位。 前往Dynamics執行個體並導覽至 [開發人員資源](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/view-download-developer-resources) 以檢視「服務根」欄位的值。 例如 `https://<tenant-name>.dynamics.com/api/data/v9.1/`
   1. 指定連線應用程式的使用者端ID （稱為應用程式ID）和使用者端密碼。
   1. 取代 `{tenant}` 具有租使用者ID於 **[!UICONTROL OAuth URL]**， **[!UICONTROL 重新整理記號URL]**、和 **[!UICONTROL 存取記號URL]** 欄位。
   1. 在中指定動態執行個體URL **[!UICONTROL 資源]** 要設定的欄位 [!UICONTROL Microsoft® Dynamics] 與表單資料模型搭配使用。 使用服務根URL來衍生Dynamics執行個體URL。 例如，`https://<tenant-name>.dynamics.com`。

   1. 指定 `openid` 在 **[!UICONTROL 授權範圍]** 授權程式的欄位 [!DNL Microsoft® Dynamics 365].
   1. 使用您的帳戶登入 [!DNL Microsoft® Dynamics 365] 認證並接受，以允許雲端服務設定連線至 [!DNL Microsoft® Dynamics 365] 服務。 如果連線成功，您將被重新導向至 [!DNL Microsoft® Dynamics 365] 雲端服務設定頁面，顯示成功訊息。
1. 選取 **[!UICONTROL 儲存並關閉]** 以完成組態設定。

### 開箱即用的存取權 [!DNL Microsoft® Dynamics 365] 表單資料模型

A [!DNL Microsoft® Dynamics 365] 表單資料模型可立即在 [!DNL AEM Forms] 在您之後的伺服器 [根據Experience Manager原型設定Forms的開發專案](setup-local-development-environment.md##forms-cloud-service-local-development-environment).

若要存取表單資料模型，請導覽至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL 資料整合]**. 可用資料夾清單包括一個具有指定標題的資料夾 `DappTitle`  當 [產生AEM原型專案](setup-local-development-environment.md#forms-cloud-service-local-development-environment). 選取資料夾名稱，然後選取 **[!UICONTROL Microsoft® Dynamics 365資料模型]**，然後選取編輯 ![編輯](assets/edit.png) 圖示以檢視表單資料模型。

設定後 [[!DNL Microsoft® Dynamics 365] 雲端設定服務](#configure-dynamics-cloud-service)，您就可以直接整合最適化表單與最適化表單 [!DNL Microsoft® Dynamics 365] 資料模型。

>[!MORELIKETHIS]
>
* [設定AEM Forms的資料來源](/help/forms/configure-data-sources.md)
* [設定AEM Forms的Azure儲存體](/help/forms/configure-azure-storage.md)
[將Forms入口網站新增至AEM Sites頁面](/help/forms/configure-forms-portal.md)
