---
title: 如何為最適化Forms設定立即可用的Microsoft Dynamics 365表單資料模型？
description: 瞭解如何整合Microsoft Dynamics 365與最適化Forms。
feature: Adaptive Forms, Form Data Model
role: User, Developer
exl-id: 29ee324c-cd4c-403b-bb3d-b1eda8e8ad88
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 2%

---


# 設定Microsoft® Dynamics 365 for AEM Forms

Adobe Experience Manager Forms資料整合提供雲端服務設定，將表單與Microsoft Dynamics伺服器整合。 它可讓您根據Microsoft Dynamics服務中定義的實體、屬性和服務來建立表單資料模型(FDM)。 表單資料模型(FDM)可用來建立與Microsoft Dynamics伺服器互動的Adaptive Forms，以啟用業務工作流程。 例如：

* 查詢Microsoft Dynamics伺服器以取得資料，並預先填入Adaptive Forms。
* 提交最適化表單時將資料寫入Microsoft Dynamics。
* 透過表單資料模型(FDM)中定義的自訂實體在Microsoft Dynamics中寫入資料。

AEM as a Cloud Service提供多種立即可用的提交動作，用於處理表單提交。 您可以在[最適化表單提交動作](/help/forms/configure-submit-actions-core-components.md)文章中進一步瞭解這些選項。

<!-- 
[[!DNL Experience Manager Forms] Data Integration](data-integration.md) provides [!DNL Microsoft&reg; Dynamics 365] Cloud Services to integrate Adaptive Forms with out of the box Form Data Model (FDM). The Adaptive Forms can then interact with [!DNL Microsoft&reg; Dynamics 365] servers to enable business workflows. For example:

* Write data into [!DNL Microsoft&reg; Dynamics 365] on Adaptive Form submission.
* Write data in [!DNL Microsoft&reg; Dynamics 365] through custom entities defined in Form Data Model (FDM) and conversely.
* Query [!DNL Microsoft&reg; Dynamics 365]server for data and prepopulate Adaptive Forms.
* Read data from [!DNL Microsoft&reg; Dynamics 365] server.

[!DNL Microsoft&reg; Dynamics 365] cloud services and Form Data Model (FDM) are available out of the box on the [!DNL AEM Forms] Server after you [set up a development project for Forms based on Experience Manager archetype](setup-local-development-environment.md#forms-cloud-service-local-development-environment).

>[!NOTE]
>
>Microsoft&reg; Dynamics 365 cloud services and Form Data Model (FDM) are available out of the box only if you set up an [!DNL Experience Manager Forms] as a [!DNL Cloud Service] project based on [AEM Archetype 30](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-30) or later.-->

## 先決條件

將[!DNL Microsoft® Dynamics 365]與AEM Forms as a Cloud Service整合之前，請確定您已執行下列步驟：


1. **在Microsoft Dynamics 365**&#x200B;中設定帳戶

   依照影片中說明的步驟設定Microsoft Dynamics 365帳戶。 在此影片中，會建立試用帳戶以供示範之用。

   >[!VIDEO](https://video.tv.adobe.com/v/3444389/)

1. **在Power Platform系統管理中心中建立帳戶**

   在&#x200B;**Power Platform系統管理中心**&#x200B;中建立帳戶以：

   * 新增Dataverse
   * 啟用Microsoft Dynamics 365應用

   依照影片中的步驟，在Power Platform管理中心建立帳戶。 在此影片中，已建立試用帳戶以供示範之用。

   >[!VIDEO](https://video.tv.adobe.com/v/3444388)

1. **在Azure Active Directory中註冊[!DNL Microsoft® Dynamics 365]的應用程式**

   請依照影片中的步驟，在Azure Active Directory中註冊[!DNL Microsoft® Dynamics 365]的應用程式。

   >[!VIDEO](https://video.tv.adobe.com/v/3444369/dynamics365integration-microsoftdynamics-apiaccess-azuread-appregistration)

   >[!NOTE]
   >
   >* 若要建立連線的[!DNL Microsoft® Dynamics 365]應用程式，請選取&#x200B;**Web**&#x200B;作為平台，並以下列格式指定&#x200B;**重新導向URI**： `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/fdm.html`。
   >* 請務必儲存使用者端ID （也稱為應用程式ID）和使用者端密碼以供日後參考。

## 將Forms連線至Microsoft® Dynamics 365

設定好上述必要條件後，您就可以繼續整合Adaptive Forms與Microsoft® Dynamics 365。 若要在提交表單時傳送資料至Microsoft® Dynamics 365，請遵循下列步驟：

[1.設定Microsoft Dynamics的雲端服務設定](#1-configure-cloud-service-configuration-for-microsoft-dynamics)

[2.建立表單資料模型(FDM)](#2-create-form-data-model-fdm)

### 1.設定Microsoft Dynamics的雲端服務設定

>[!VIDEO](https://video.tv.adobe.com/v/3444370/cloudconfiguration-dataintegration-adobeexperiencemanager-aemforms-microsoftdynamics)

執行以下步驟來設定[!DNL Microsoft® Dynamics 365]雲端服務設定：

1. 瀏覽至&#x200B;**[!UICONTROL 作者執行個體上的]**&#x200B;工具![ ](assets/hammer.png)hammer **[!UICONTROL >]**&#x200B;雲端服務&#x200B;**[!UICONTROL >]**&#x200B;資料來源[!DNL AEM Forms]。

   ![選取雲端資料Source](/help/forms/assets/dynamics-data-source.png)
1. 選取設定容器。 設定會儲存在選取的設定容器中。
1. 按一下「**[!UICONTROL 建立]**」。

   ![建立雲端設定](/help/forms/assets/dynamics-select-configuration.png)

   **建立資料Source設定**&#x200B;設定精靈出現。

   ![建立資料Source設定精靈](/help/forms/assets/dynamics-create-data-configuration.png)

1. 指定&#x200B;**[!UICONTROL Title]**、**[!UICONTROL Name]**&#x200B;並選取&#x200B;**[!UICONTROL 服務型別]**&#x200B;作為&#x200B;**OData服務**。
1. 按一下「**[!UICONTROL 下一步]**」。**驗證**&#x200B;標籤出現。

   ![驗證標籤](/help/forms/assets/dynamics-authentication-tab.png)

1. 指定&#x200B;**[!UICONTROL 服務根]**&#x200B;欄位的值。

   移至&#x200B;**Power Platform系統管理中心**&#x200B;中的Dynamics執行個體，並導覽至[開發人員資源](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/view-download-developer-resources)，以檢視&#x200B;**服務根目錄**&#x200B;的值。 **Web API端點**&#x200B;代表您要與最適化Forms整合之Dynamics執行個體的&#x200B;**服務根**&#x200B;值。 **服務根** URL的格式如下： `https://<tenant-name>.dynamics.com/api/data/v9.1/`

   ![服務根目錄欄位](/help/forms/assets/dynamics-service-root.png)

1. 選取&#x200B;**[!UICONTROL 驗證型別]**&#x200B;做為&#x200B;**OAuth2.0**。
1. 為連線的應用程式指定&#x200B;**使用者端識別碼** （稱為應用程式識別碼）和&#x200B;**使用者端密碼**。
您可以從Azure Active Directory應用程式擷取**使用者端識別碼**&#x200B;和&#x200B;**使用者端密碼**。

   ![使用者端識別碼與使用者端密碼](/help/forms/assets/dynamics-azure-app-resgistration.png)

1. 在&#x200B;**[!UICONTROL OAuth URL]**、**[!UICONTROL 重新整理權杖URL]**&#x200B;和&#x200B;**[!UICONTROL 存取權杖URL]**欄位中指定下列專案。
您可以從Azure Active Directory應用程式的**[!UICONTROL 端點]**&#x200B;區段中，擷取&#x200B;**[!UICONTROL OAuth URL]**、**[!UICONTROL 重新整理權杖URL]**&#x200B;和&#x200B;**存取權杖URL**。

   ![Azure應用程式端點](/help/forms/assets/dynamics-azure-app-endpoints.png)

1. 在`openid`上授權程式的&#x200B;**[!UICONTROL 授權範圍]**&#x200B;欄位中指定[!DNL Microsoft® Dynamics 365]。
1. 在&#x200B;**[!UICONTROL 資源]**&#x200B;欄位中指定Dynamics執行個體URL，以使用表單資料模型(FDM)設定[!DNL Microsoft® Dynamics 365]。
您可以從**Power Platform系統管理中心**&#x200B;複製&#x200B;**環境URL**，或使用&#x200B;**服務根** URL衍生Dynamics執行個體URL。 資源URL的格式如下： `https://<tenant-name>.dynamics.com`。

   ![電源應用程式資源欄位](/help/forms/assets/dynamics-resource-field.png)

1. 使用您的[!DNL Microsoft® Dynamics 365]認證登入，並接受允許雲端服務設定連線到[!DNL Microsoft® Dynamics 365]服務。 如果連線成功，系統會將您重新導向至[!DNL Microsoft® Dynamics 365]雲端服務設定頁面，顯示成功訊息。
1. 選取&#x200B;**[!UICONTROL 建立]**&#x200B;以儲存組態。

### 2.建立表單資料模型(FDM)

>[!VIDEO](https://video.tv.adobe.com/v/3444367/aemforms-adobeexperiencemanager-formdatamodel--dataintegration-digitalforms)

您可以使用建立的[!DNL Microsoft® Dynamics 365]雲端設定來建立表單資料模型(FDM)。 執行以下步驟來建立表單資料模型：

1. 導覽至&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL 資料整合]**。
   ![建立表單資料模型](/help/forms/assets/dynamics-create-fdm.png)

1. 按一下&#x200B;**[!UICONTROL 建立]**&#x200B;並選取&#x200B;**[!UICONTROL 表單資料模型]**。
   ![選取表單資料模型](/help/forms/assets/dynamics-select-fdm.png)

   **建立表單資料模型**&#x200B;精靈出現。
1. 按一下「**[!UICONTROL 下一步]**」。
1. 從&#x200B;**選取資料來源**索引標籤中選取建立的雲端設定。
   ![選取雲端設定](/help/forms/assets/dynamics-select-cloud-config.png)

1. 按一下「編輯![編輯](assets/edit.png)」圖示以檢視及設定表單資料模型(FDM)。

接著，您可以[設定表單資料模型(FDM)](/help/forms/work-with-form-data-model.md#configure-services)，並將其用於各種最適化表單使用案例，例如：

* 透過查詢[!DNL Microsoft Dynamics]實體和服務中的資訊預填調適型表單
* 使用最適化表單規則叫用表單資料模型(FDM)中定義的[!DNL Microsoft Dynamics]伺服器作業
* 將提交的表單資料寫入[!DNL Microsoft Dynamics]個實體
* 您可以設定最適化表單的表單資料模型提交動作，以將資料傳送至[!DNL Microsoft Dynamics]。

然後，您可以在[最適化表單](/help/forms/using-form-data-model.md)中使用表單資料模型(FDM)**選項的**&#x200B;提交，將資料從您的表單傳輸到設定的[!DNL Microsoft® Dynamics 365]。


>[!MORELIKETHIS]
>
>* [設定AEM Forms的資料來源](/help/forms/configure-data-sources.md)
>* [設定AEM Forms的Azure儲存體](/help/forms/configure-azure-storage.md)
>  [將Forms入口網站新增至AEM Sites頁面](/help/forms/configure-forms-portal.md)
