---
title: 如何為最適化Forms設定現成的Microsoft Dynamics 365和Salesforce表單資料模型？
description: 瞭解如何將Microsoft Dynamics 365和Salesforce與最適化Forms整合。
feature: Adaptive Forms, Form Data Model
role: User, Developer
exl-id: 2a43b2db-2dfb-4c79-88be-ea770b44dac1
source-git-commit: 7b31a2ea016567979288c7a8e55ed5bf8dfc181d
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 2%

---

# 設定Microsoft® Dynamics 365或Salesforce for AEM Forms {#configure-azure-storage}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/oauth2-client-credentials-flow-for-server-to-server-integration.html) |
| AEM as a Cloud Service  | 本文章 |

[[!DNL Experience Manager Forms] 資料整合](data-integration.md)提供[!DNL Microsoft® Dynamics 365]和[!DNL Salesforce]雲端服務，整合最適化表單與立即可用的表單資料模型(FDM)。 最適化Forms可以與[!DNL Microsoft® Dynamics 365]和[!DNL Salesforce]伺服器互動，以啟用業務工作流程。 例如：

* 在提交最適化表單時將資料寫入[!DNL Microsoft® Dynamics 365]和[!DNL Salesforce]。
* 透過表單資料模型(FDM)中定義的自訂實體寫入[!DNL Microsoft® Dynamics 365]和[!DNL Salesforce]中的資料，反之亦然。
* 查詢[!DNL Microsoft® Dynamics 365]和[!DNL Salesforce]伺服器以取得資料，並預先填入Adaptive Forms。
* 從[!DNL Microsoft® Dynamics 365]和[!DNL Salesforce]伺服器讀取資料。

在您[根據Experience Manager原型](setup-local-development-environment.md#forms-cloud-service-local-development-environment)為Forms設定開發專案後，[!DNL AEM Forms]伺服器上即可使用[!DNL Microsoft® Dynamics 365]和[!DNL Salesforce]雲端服務與表單資料模型(FDM)。

>[!NOTE]
>
>只有當您根據[AEM Archetype 30](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-30)或更新版本將[!DNL Experience Manager Forms]設定為[!DNL Cloud Service]專案時，Microsoft® Dynamics 365和[!DNL Salesforce]雲端服務以及表單資料模型(FDM)才可立即使用。

## 設定[!DNL Salesforce]雲端服務 {#configure-salesforce-cloud-service}

在設定[!DNL Salesforce]雲端服務之前，請確定您執行下列工作：

* [建立連線的OAuth已啟用 [!DNL Salesforce] 應用程式](https://help.salesforce.com/s/articleView?id=sf.connected_app_create_api_integration.htm&amp;type=5)。 建立連線的[!DNL Salesforce]應用程式時，請以下列格式指定回呼URL：

  ```
  https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
  ```

  其中伺服器和連線埠代表[!DNL AEM Forms]伺服器的主機名稱和連線埠號碼。

* 建立連線的[!DNL Salesforce]應用程式時，請指定`full`和`offline_access`做為OAuth範圍的值。

* 記下連線應用程式的使用者端ID （稱為使用者金鑰）和使用者端密碼（稱為使用者密碼）的值。

執行以下步驟來設定[!DNL Salesforce]雲端服務：

1. 在[!DNL AEM Forms]作者執行個體上，瀏覽至&#x200B;**[!UICONTROL 工具]** ![槌子](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL 資料來源]**。 可用包裝函式資料夾清單包含在[產生AEM原型專案](setup-local-development-environment.md#forms-cloud-service-local-development-environment)時，為`DappTitle`指定標題的資料夾。
1. 選取資料夾名稱，選取&#x200B;**[!UICONTROL Salesforce雲端設定]**，然後選取&#x200B;**[!UICONTROL 屬性]**。
1. 在&#x200B;**[!UICONTROL 驗證設定]**&#x200B;索引標籤中：
   1. 在&#x200B;**[!UICONTROL 主機]**&#x200B;欄位中指定[!DNL Salesforce]網域URL。 例如，[網域名稱].my.salesforce.com。
   1. 為連線的應用程式指定使用者端ID （稱為使用者金鑰）和使用者端密碼（稱為使用者密碼）。
   1. 在&#x200B;**[!UICONTROL 授權範圍]**&#x200B;欄位中指定&#x200B;**full offline_access** （`full`和`offine_access`值，以空格分隔）。
   1. 選取&#x200B;**[!UICONTROL 連線至OAuth]**。 您被重新導向到[!DNL Microsoft® Dynamics]登入頁面。
   1. 使用您的[!DNL Salesforce]認證登入，並接受允許雲端服務設定連線到[!DNL Salesforce]服務。 如果連線成功，系統會將您重新導向至[!DNL Salesforce]雲端服務設定頁面，顯示成功訊息。
1. 選取&#x200B;**[!UICONTROL 儲存並關閉]**&#x200B;以完成組態設定。

### 存取現成可用的[!DNL Salesforce]表單資料模型(FDM)

在您[根據Experience Manager原型](setup-local-development-environment.md#forms-cloud-service-local-development-environment)為Forms設定開發專案後，[!DNL Salesforce]表單資料模型(FDM)可在[!DNL AEM Forms]伺服器上立即使用。

若要存取表單資料模型(FDM)，請導覽至&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL 資料整合]**。 可用資料夾清單包括標題為`DappTitle`的資料夾，而此資料夾是在[產生AEM原型專案](setup-local-development-environment.md#forms-cloud-service-local-development-environment)時指定的。 選取資料夾名稱，選取&#x200B;**[!UICONTROL Salesforce資料模型]**，然後選取[編輯![編輯](assets/edit.png)]圖示以檢視表單資料模型(FDM)。

設定[[!DNL Salesforce] 雲端設定服務](#configure-salesforce-cloud-service)後，您可以將最適化表單與現成可用的[!DNL Salesforce]資料模型整合。

## 設定[!DNL Microsoft® Dynamics 365]雲端服務 {#configure-dynamics-cloud-service}

在設定[!DNL Microsoft® Dynamics 365]雲端服務之前，請確定您執行下列工作：

* [使用Azure Active Directory](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/walkthrough-register-app-azure-active-directory)註冊 [!DNL Microsoft® Dynamics 365] 的應用程式。 當您建立連線的[!DNL Microsoft® Dynamics 365]應用程式時，請以下列格式指定回覆URL：

  ```
  https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
  ```

  其中伺服器和連線埠代表[!DNL AEM Forms]伺服器的主機名稱和連線埠號碼。

* 記下所連線應用程式的使用者端ID （也稱為應用程式ID）和使用者端密碼的值。

執行以下步驟來設定[!DNL Microsoft® Dynamics 365]雲端服務：

1. 在[!DNL AEM Forms]作者執行個體上，瀏覽至&#x200B;**[!UICONTROL 工具]** ![槌子](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL 資料來源]**。 可用包裝函式資料夾清單包含在[產生AEM原型專案](setup-local-development-environment.md#forms-cloud-service-local-development-environment)時，為`DappTitle`指定標題的資料夾。
1. 選取資料夾名稱，選取&#x200B;**[!UICONTROL Microsoft® Dynamics 365雲端設定]**，然後選取&#x200B;**[!UICONTROL 屬性]**。
1. 在&#x200B;**[!UICONTROL 驗證設定]**&#x200B;索引標籤中：
   1. 輸入&#x200B;**[!UICONTROL 服務根]**&#x200B;欄位的值。 移至Dynamics執行個體並導覽至[開發人員資源](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/view-download-developer-resources)，以檢視[服務根目錄]欄位的值。 例如 `https://<tenant-name>.dynamics.com/api/data/v9.1/`
   1. 指定連線應用程式的使用者端ID （稱為應用程式ID）和使用者端密碼。
   1. 將`{tenant}`取代為&#x200B;**[!UICONTROL OAuth URL]**、**[!UICONTROL 重新整理權杖URL]**&#x200B;和&#x200B;**[!UICONTROL 存取權杖URL]**&#x200B;欄位中的租使用者識別碼。
   1. 在&#x200B;**[!UICONTROL 資源]**&#x200B;欄位中指定Dynamics執行個體URL，以使用表單資料模型(FDM)設定[!UICONTROL Microsoft® Dynamics]。 使用服務根URL來衍生Dynamics執行個體URL。 例如，`https://<tenant-name>.dynamics.com`。

   1. 在[!DNL Microsoft® Dynamics 365]上授權程式的&#x200B;**[!UICONTROL 授權範圍]**&#x200B;欄位中指定`openid`。
   1. 使用您的[!DNL Microsoft® Dynamics 365]認證登入，並接受允許雲端服務設定連線到[!DNL Microsoft® Dynamics 365]服務。 如果連線成功，系統會將您重新導向至[!DNL Microsoft® Dynamics 365]雲端服務設定頁面，顯示成功訊息。
1. 選取&#x200B;**[!UICONTROL 儲存並關閉]**&#x200B;以完成組態設定。

### 存取現成可用的[!DNL Microsoft® Dynamics 365]表單資料模型(FDM)

在您[根據Experience Manager原型](setup-local-development-environment.md##forms-cloud-service-local-development-environment)為Forms設定開發專案後，[!DNL Microsoft® Dynamics 365]表單資料模型(FDM)可在[!DNL AEM Forms]伺服器上立即使用。

若要存取表單資料模型(FDM)，請導覽至&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL 資料整合]**。 可用資料夾清單包括標題為`DappTitle`的資料夾，而此資料夾是在[產生AEM原型專案](setup-local-development-environment.md#forms-cloud-service-local-development-environment)時指定的。 選取資料夾名稱，選取&#x200B;**[!UICONTROL Microsoft® Dynamics 365資料模型]**，然後選取「編輯![編輯](assets/edit.png)」圖示以檢視表單資料模型(FDM)。

設定[[!DNL Microsoft® Dynamics 365] 雲端設定服務](#configure-dynamics-cloud-service)後，您可以將最適化表單與現成可用的[!DNL Microsoft® Dynamics 365]資料模型整合。

>[!MORELIKETHIS]
>
>* [設定AEM Forms的資料來源](/help/forms/configure-data-sources.md)
>* [設定AEM Forms的Azure儲存體](/help/forms/configure-azure-storage.md)
>  [將Forms入口網站新增至AEM Sites頁面](/help/forms/configure-forms-portal.md)
