---
title: 如何設定 [!DNL AEM Forms] as a Cloud Service環境？
description: 瞭解如何設定和 [!DNL AEM Forms] as a Cloud Service環境
exl-id: 42f53662-fbcf-4676-9859-bf187ee9e4af
source-git-commit: b6dcb6308d1f4af7a002671f797db766e5cfe9b5
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 17%

---

# 上線至 [!DNL AEM Forms] as a Cloud Service {#overview}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/install-aem-forms/osgi-installation/installing-configuring-aem-forms-osgi.html) |
| AEM as a Cloud Service  | 本文 |


## 決定角色 {#personas-aem-forms-project}

<!-- When you sign up for the service, Adobe creates an Organization identifier for your company in the Adobe Identity Management System (IMS), where your users and their permissions can be managed. So, --> 開始使用前 [!DNL AEM Forms] as a Cloud Service環境，決定角色並為您的專案建構團隊。 典型 [!DNL AEM Forms] 專案團隊有下列角色：

* **使用者體驗(UX)設計工具**：使用者體驗(UX)設計工具定義 [!DNL AEM Forms] 資產。

* **Forms從業者**：Forms從業人員會根據UX設計工具提供的樣式、版面和品牌建立最適化Forms、主題和範本。 從業者也會建立最適化表單並將其與表單資料模型和AEM Workflow整合。 Forms從業人員通常會執行前端相關工作。

* **Forms開發人員**：Forms開發人員開發自訂表單解決方案。  Forms開發人員通常會從事後端開發，例如開發自訂元件、AEM工作流程、預填服務等。

* **AEM管理員**：AEM管理員可協助進行整體設定，例如設定使用者、強化環境、設定資料來源、設定電子郵件和協力廠商軟體。 AEM管理員也可協助進行整合，例如與Adobe Analytics、Adobe Target和Adobe Sign整合。

* **一般使用者**：一般使用者與已發佈的表單互動並提交表單、簽署已提交的表單、透過入口網站追蹤已提交的應用程式，並接收個人化通訊。

<!-- While onboarding to the service, assign the following AEM groups to [!DNL AEM Forms] as a Cloud Service based on their role:

| User type | AEM group |
|---|---|
| Form Practitioner | forms-users (AEM Forms Users), template-authors, workflow-user, workflow-editors, and fdm-author  |
| UX Designer| forms-users, template-authors|
| End-User| <ul> <li>When a user must login to view and submit an Adaptive Form, add such users to forms-users group. </li> <li>When no user authentication is required to access Adaptive Forms, do not assign any group to such users. </li> </ul>| -->

## 服務入門 {#onboarding}

* [上線](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/home.html) 至 [!DNL Adobe Experience Manager] as a Cloud Service。

* （僅適用於沙箱）完成服務後， [建立](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html?lang=en#how-to-use) 和 [執行](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html) 生產和非生產管道。 可啟用並帶來以下的最新功能： [!DNL AEM Forms] 對您的環境as a Cloud Service。

您可以使用Formsas a Cloud Service建立最適化表單（數位註冊）或產生客戶通訊。 完成之後 [入門](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/home.html) 至 [!DNL Adobe Experience Manager] as a Cloud Service，請執行以下其中一項動作以啟用數位註冊或客戶通訊功能。 您也可以啟用這兩項功能：

1. 登入 Cloud Manager 並開啟您的 AEM Forms as a Cloud Service 執行個體。

1. 開啟「編輯方案」選項，前往「解決方案和附加元件」索引標籤，然後選擇&#x200B;**[!UICONTROL Forms - 通訊]**&#x200B;選項。

   ![通訊](assets/communications.png)

   如果您已經啟用&#x200B;**[!UICONTROL Forms - 數位註冊]**&#x200B;選項，則選擇&#x200B;**[!UICONTROL Forms - 通訊附加元件]**&#x200B;選項。

   ![附加元件](assets/add-on.png)

1. 按一下&#x200B;**[!UICONTROL 更新]**。

1. 執行建置管道。建置管道成功後，將為您的環境啟用通訊 API。

>[!NOTE]
>
> 若要啟用和設定文件操控 API，請將以下規則新增至[Dispatcher 設定](setup-local-development-environment.md#forms-specific-rules-to-dispatcher)：
>
> `# Allow Forms Doc Generation requests`
> `/0062 { /type "allow" /method "POST" /url "/adobe/forms/assembler/*" }`

## 設定使用者 {#config-users}

完成服務上線後，請登入 [!DNL AEM Forms] as a Cloud Service環境，開啟Author和Publish執行個體，並將使用者新增至Forms專屬的 [AEM群組](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html#accessing)，根據角色而定。 下表列出Forms專屬的AEM群組（可立即使用）以及對應的使用者型別。 此表格也提供每個使用者型別的AEM執行處理型別：

| 使用者型別（角色） | 使用者群組 | AEM執行個體 |
|---|---|---|
| 表單作業人員/Forms開發人員 | <ul> <li> [!DNL forms-users] </li><li> [!DNL template-author] </li><li> [!DNL workflow-users] </li><li> [!DNL workflow-editors] </li><li> [!DNL fdm-authors] </li></ul> | 作者執行個體 |
| 使用者體驗(UX)設計工具 | <ul> <li> [!DNL forms-users]</li><li> [!DNL template-author] </li></ul> | 作者執行個體 |
| AEM 管理員 | <ul> <li>[!DNL aem-administrators],</li> <li>[!DNL fd-administrators] </li> </ul> | 製作和發佈執行個體 |
| 一般使用者 | <ul> <li>當使用者必須登入才能檢視並提交最適化表單時，請將這類使用者新增至 [!DNL forms-users] 群組。 </li> <li>當不需要使用者驗證即可存取Adaptive Forms時，請勿將任何群組指派給這類使用者。 </li> </ul> | 製作和發佈執行個體 |

如需有關Forms特定AEM群組和相應許可權的詳細資訊，請參閱 [群組與許可權](forms-groups-privileges-tasks.md).

<!-- You can also create  [user groups](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html#accessing) specific  to your organization, assign policies, and [users](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html#accessing) to the groups. The policies help control permissions of the users that are part of the group. For information a -->

## 下一步 {#next-steps}

[設定本機開發環境](setup-local-development-environment.md). 您可以使用本機開發環境來建立最適化表單和相關資產（主題、範本、自訂提交動作、預填服務等），以及 [將PDF forms轉換為最適化Forms](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/introduction.html) 無須登入雲端開發環境。

<!-- ### Business unit and end-users {#business-unit-and-end-users}

| Role| Organization| Description|
|-----|-------|-----|
| UX Designer                  | Customer/System Integrator/Partner | Defines user experience design (style, layout, branding) as per organizational requirements for Adaptive Forms to allow AEM Forms practitioners to design the corresponding themes and templates.                                     |
| Forms Practitioner           | Customer                           | Authors Adaptive Forms, creates Form Data Model integrations, and creates business workflows using the Experience Manager Workflows. Typically undertakes the front-end work.                                                         |
| Business Executive - Digital | Customer                           | Responsible for business unit’s product marketing strategy and revenues, main business stakeholders for digital use cases, solutions, and service offerings for the end-users, signs off on the use case implementation and delivery. |
| Customer Experience Lead     | Customer                           | Business user persona. Authors, personalizes and updates Adaptive Forms fields/rules/styling, identifies, and prioritizes business needs. Validates business use-case with SI/Partner developers/practitioners during UAT.            |
| Forms Back-Office User       | Customer                           | End-user internal to organization filling forms, participating in back-office Forms workflows such as review/approval of applications etc.                                                                                            |
| Forms End-User               | External to customer               | Interacts with and submits the published form as end customer or citizen, signs submitted forms, tracks her applications through web portal, receives personalized interactive communications.                                        |

### Project team {#project-team}

| Role | Org | Description|
|-----|-----|-----|
| Experience Manager Administrator | System Integrator /Partner/Customer | Helps with overall installation, configures SSL certificates, configures data sources, email, and other third-party software, integrations like Adobe Analytics, Adobe Target, Automated Forms Conversion Services with Experience Manager instance. |
| Project Manager                  | System Integrator /Partner/Customer | Converts customer use-case into technical requirements, manages schedule/cost/scope for overall project.                                                                                                                                             |
| Product Owner                    | System Integrator /Partner/Customer | Prioritizes and evaluates scrum team's work for high-quality delivery on time.                                                                                                                                                                       |
| Scrum Master                     | System Integrator /Partner/Customer | Ensures agile values and processes in place to deliver on defined requirements as per prioritization by PO.                                                                                                                                          |
| Infrastructure / security expert | System Integrator /Partner/Customer | Provisions and configures best possible infrastructure, security controls and infra processes to address current and projected RASP requirements.                                                                                                    |
| Technical Architect              | System Integrator /Partner/Customer | Provides best high-level architecture and infrastructure guidance for use-case implementation and address RASP (Reliability, Availability, Scalability, and Performance) and security challenges.                                                    | -->

<!-- ## Onboard to the service {#onboarding}

[Onboard](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/home.html) to the [!DNL Adobe Experience Manager] as a Cloud Service. 

After you onboard the service, configure a [local development environment](setup-local-development-environment.md). 

Administrators are responsible for managing Adobe software and services for their organization. Administrators grant access to developers in their organization to connect and use your [!DNL AEM Forms] as a Cloud Service program. When an administrator is provisioned for an organization, the administrator receives an email with title ‘You now have administrator rights to manage Adobe software and services for your organization’. If you are an administrator, check your mailbox for email with previously mentioned title and proceed to [add users](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#onboarding-users-in-admin-console) via IMS and assign [form-specific groups](forms-groups-privileges-tasks.md) to users based on their role.

## Next step {#next-steps} -->

<!-- ## Prerequisites {#prerequisites}

If you are new to AEM as a cloud service, contact your Adobe representative to create an organization identifier for your company in the Adobe Identity Management System (IMS). Once Adobe has created an organization for your company, your designated administrator is added as the first member of the organization. The administrator can setup an [!DNL AEM Forms] as a Cloud Service instance. 

## Onboard and set up a new environment {#onboard-and-setup-a-new-environment}

Log in to Cloud Manager and create a program. After the program is ready, create environments, add developers or users to environments, and run the pipeline to get the latest version of [!DNL AEM Forms] as a Cloud Service and start developing for your environment. The detailed steps are:

1. Contact your Adobe representative to create an organization identifier for your company in the Adobe Identity Management System (IMS) and provide access to an administrator in your organization.
1. Configure [Automated Forms Conversion Service](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/configure-service.html?lang=en). After a configuration is complete, a profile for Automated Forms Conversion Service is available in [Admin Console](https://adminconsole.adobe.com/).

    If the service is not available, log in to [Admin Console](https://adminconsole.adobe.com/). Use Adobe ID of administrator provisioned to use Automated Forms Conversion Service to login. Do not use any other ID or Federated ID to login.
    1. Click **[!UICONTROL Automated Forms Conversion Service]** option.
    1. Click **[!UICONTROL New Profile]** in the Products tab.
    1. Specify **[!UICONTROL Name]**, **[!UICONTROL Display Name]**, and **[!UICONTROL Description]** for the profile. Click **[!UICONTROL Done]**. A profile is created. 
1. Log in to [Cloud Manager](https://experience.adobe.com/#/@marketinghub/experiencemanager) and [create a program](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html) for your organization.
1. [Create environments](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=en#adding-environments) within your program.
1. Log in to [Admin console](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/what-is-required/add-users-roles.html) and add developers or users to your organization.
1. Run the [build pipeline](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/how-to-use/deploying-code.html). It brings latest [!DNL Experience Manager Forms] as a Cloud Service features to your environment.
1. [Start developing](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) and creating Adaptive Forms on [!DNL Experience Manager Forms] as a Cloud Service environment.
1. Configure the [local development environment](setup-local-development-environment.md) for rapid development

## Configure dispatcher caching {#caching}

You can make dispatcher caching related configuration changes to code on your local development instance and deploy the changes to your [!DNL AEM Forms] as a Cloud Service instance. For details, see [update dispatcher configuration](setup-local-development-environment.md).
 -->
