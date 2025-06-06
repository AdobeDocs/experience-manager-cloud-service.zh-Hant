---
title: 如何設定 [!DNL AEM Forms] 作為雲端服務環境？
description: 瞭解如何設定和設定 [!DNL AEM Forms] as a Cloud Service環境。
role: Admin, Developer, User
feature: Adaptive Forms
exl-id: 42f53662-fbcf-4676-9859-bf187ee9e4af
source-git-commit: 81951a9507ec3420cbadb258209bdc8e2b5e2942
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 7%

---

# 載入[!DNL AEM Forms]as a Cloud Service {#overview}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/install-aem-forms/osgi-installation/installing-configuring-aem-forms-osgi.html?lang=zh-Hant) |
| AEM as a Cloud Service  | 本文章 |


## 決定角色 {#personas-aem-forms-project}

<!-- When you sign up for the service, Adobe creates an Organization identifier for your company in the Adobe Identity Management System (IMS), where your users and their permissions can be managed. So, --> 開始使用Adobe Experience Manager (AEM) Forms as a Cloud Service環境之前，請先決定角色，並為您的專案建立團隊。 一般[!DNL AEM Forms]專案團隊有下列角色：

* **使用者體驗(UX) Designer**：使用者體驗(UX) Designer定義[!DNL AEM Forms]資產的樣式、版面配置和品牌化。

* **Forms從業者**： Forms從業者會根據UX Designer提供的樣式、版面配置和品牌建立最適化Forms、主題和範本。 從業者也會建立最適化表單並將其與表單資料模型(FDM)和AEM工作流程整合。 Forms從業人員通常從事前端相關工作。

* **Forms開發人員**： Forms開發人員開發自訂表單解決方案。 Forms開發人員通常會進行後端開發，例如開發自訂元件、AEM工作流程、預填服務等。

* **AEM管理員**： AEM管理員可協助進行整體設定，例如設定使用者、強化環境、設定資料來源、設定電子郵件以及協力廠商軟體。 AEM管理員也可協助進行整合，例如與Adobe Analytics、Adobe Target和Adobe Sign整合。

* **一般使用者**：使用者與已發佈的表單互動並提交表單、簽署已提交的表單、透過入口網站追蹤已提交的應用程式，以及接收個人化通訊。

<!-- While onboarding to the service, assign the following AEM groups to [!DNL AEM Forms] as a Cloud Service based on their role:

| User type | AEM group |
|---|---|
| Form Practitioner | forms-users (AEM Forms Users), template-authors, workflow-user, workflow-editors, and fdm-author  |
| UX Designer| forms-users, template-authors|
| End-User| <ul> <li>When a user must login to view and submit an Adaptive Form, add such users to forms-users group. </li> <li>When no user authentication is required to access Adaptive Forms, do not assign any group to such users. </li> </ul>| -->

## 服務入門 {#onboarding}

* [將](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/overview.html?lang=zh-Hant)上線到[!DNL Adobe Experience Manager]as a Cloud Service。

* （僅適用於沙箱）服務上線後，[建立](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/pipelines/production-pipelines.html?lang=zh-Hant)和[執行生產和非生產管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/code-deployment.html?lang=zh-Hant)。 它會啟用並將[!DNL AEM Forms]as a Cloud Service的最新功能帶入您的環境。

您可以使用Forms as a Cloud Service建立最適化表單（數位註冊）或產生客戶通訊。 完成[!DNL Adobe Experience Manager]as a Cloud Service的[上線](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/overview.html?lang=zh-Hant)後，請執行下列動作以啟用Forms — 數位註冊或客戶通訊功能。<!--You can also enable both the features-->：

1. 登入 Cloud Manager 並開啟您的 AEM Forms as a Cloud Service 執行個體。
1. 開啟編輯計畫選項，前往解決方案和附加元件索引標籤：

   * 如果您有生產環境，請選取&#x200B;**[!UICONTROL Forms — 通訊]**&#x200B;選項以啟用Forms — 數位註冊和Forms — 通訊附加元件。

     ![通訊](assets/communications.png)

   <!-- If you have already enabled the **[!UICONTROL Forms - Digital Enrollment]** option, then select the **[!UICONTROL Forms - Communications Add-On]** option. ![Addon](assets/add-on.png) -->

   * 如果您有沙箱環境，請選取&#x200B;**[!UICONTROL Forms]**&#x200B;以啟用Forms — 數位註冊和Forms — 通訊附加元件。

     ![表單數位註冊選擇](assets/forms-digital-enrollment1.png)


1. 按一下&#x200B;**[!UICONTROL 更新]**。
1. 執行建置管道。建置管道成功後，為您的環境啟用所選的解決方案。

>[!NOTE]
>
> 若要啟用及設定檔案操作API，請將下列規則新增至[Dispatcher設定](setup-local-development-environment.md#forms-specific-rules-to-dispatcher)：
>
> `# Allow Forms Doc Generation requests`
> `/0062 { /type "allow" /method "POST" /url "/adobe/forms/assembler/*" }`

## 設定使用者 {#config-users}

在您完成服務上線後，請登入您的[!DNL AEM Forms]as a Cloud Service環境、開啟Author和Publish執行個體，並根據使用者的角色，將使用者新增至Forms特定的[AEM群組](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html?lang=zh-Hant#accessing)。 下表列出Forms專屬的AEM群組（可立即使用）以及對應的使用者型別。 此表格也提供每個使用者型別的AEM執行處理型別：

| 使用者型別（角色） | 使用者群組 | AEM執行個體 |
|---|---|---|
| 表單從業者/Forms開發人員 | <ul> <li> [!DNL forms-users] </li><li> [!DNL template-author] </li><li> [!DNL workflow-users] </li><li> [!DNL workflow-editors] </li><li> [!DNL fdm-authors] </li></ul> | 作者執行個體 |
| 使用者體驗(UX) Designer | <ul> <li> [!DNL forms-users]</li><li> [!DNL template-author] </li></ul> | 作者執行個體 |
| AEM 管理員 | <ul> <li>[!DNL aem-administrators]、</li> <li>[!DNL fd-administrators] </li> </ul> | 作者與Publish例項 |
| 一般使用者 | <ul> <li>當使用者必須登入才能檢視並提交最適化表單時，請將這類使用者新增到[!DNL forms-users]群組。 </li> <li>當存取最適化Forms不需要使用者驗證時，不要將任何群組指派給這類使用者。 </li> </ul> | 作者與Publish例項 |

如需有關Forms特定AEM群組與對應許可權的詳細資訊，請參閱[群組與許可權](forms-groups-privileges-tasks.md)。

<!-- You can also create  [user groups](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html?lang=zh-Hant#accessing) specific  to your organization, assign policies, and [users](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html?lang=zh-Hant#accessing) to the groups. The policies help control permissions of the users that are part of the group. For information a -->

## 下一步 {#next-steps}

[設定本機開發環境](setup-local-development-environment.md)。 您可以使用本機開發環境來建立最適化表單和相關資產（主題、範本、自訂提交動作、預填服務等）。 並且[將PDF forms轉換為最適化Forms](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/introduction.html?lang=zh-Hant)，而不登入雲端開發環境。

<!-- ### Business unit and end-users {#business-unit-and-end-users}

| Role| Organization| Description|
|-----|-------|-----|
| UX Designer                  | Customer/System Integrator/Partner | Defines user experience design (style, layout, branding) as per organizational requirements for Adaptive Forms to allow AEM Forms practitioners to design the corresponding themes and templates.                                     |
| Forms Practitioner           | Customer                           | Authors Adaptive Forms, creates Form Data Model integrations, and creates business workflows using the Experience Manager Workflows. Typically undertakes the front-end work.                                                         |
| Business Executive - Digital | Customer                           | Responsible for business unit's product marketing strategy and revenues, main business stakeholders for digital use cases, solutions, and service offerings for the end-users, signs off on the use case implementation and delivery. |
| Customer Experience Lead     | Customer                           | Business user persona. Authors, personalizes and updates Adaptive Forms fields/rules/styling, identifies, and prioritizes business needs. Validates business use-case with SI/Partner developers/practitioners during UAT.            |
| Forms Back-Office User       | Customer                           | End-user internal to organization filling forms, participating in back-office Forms workflows such as review/approval of applications and so on.                                                                                            |
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

[Onboard](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/home.html?lang=zh-Hant) to the [!DNL Adobe Experience Manager] as a Cloud Service. 

After you onboard the service, configure a [local development environment](setup-local-development-environment.md). 

Administrators are responsible for managing Adobe software and services for their organization. Administrators grant access to developers in their organization to connect and use your [!DNL AEM Forms] as a Cloud Service program. When an administrator is provisioned for an organization, the administrator receives an email with title 'You now have administrator rights to manage Adobe software and services for your organization'. If you are an administrator, check your mailbox for email with previously mentioned title and proceed to [add users](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=zh-Hant#onboarding-users-in-admin-console) by way of IMS and assign [form-specific groups](forms-groups-privileges-tasks.md) to users based on their role.

## Next step {#next-steps} -->

<!-- ## Prerequisites {#prerequisites}

If you are new to AEM as a cloud service, contact your Adobe representative to create an organization identifier for your company in the Adobe Identity Management System (IMS). Once Adobe has created an organization for your company, your designated administrator is added as the first member of the organization. The administrator can setup an [!DNL AEM Forms] as a Cloud Service instance. 

## Onboard and set up a new environment {#onboard-and-setup-a-new-environment}

Log in to Cloud Manager and create a program. After the program is ready, create environments, add developers or users to environments, and run the pipeline to get the latest version of [!DNL AEM Forms] as a Cloud Service and start developing for your environment. The detailed steps are:

1. Contact your Adobe representative to create an organization identifier for your company in the Adobe Identity Management System (IMS) and provide access to an administrator in your organization.
1. Configure [Automated Forms Conversion Service](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/configure-service.html?lang=zh-Hant). After a configuration is complete, a profile for Automated Forms Conversion Service is available in [Admin Console](https://adminconsole.adobe.com/).

    If the service is not available, log in to [Admin Console](https://adminconsole.adobe.com/). Use Adobe ID of administrator provisioned to use Automated Forms Conversion Service to login. Do not use any other ID or Federated ID to login.
    1. Click **[!UICONTROL Automated Forms Conversion Service]** option.
    1. Click **[!UICONTROL New Profile]** in the Products tab.
    1. Specify **[!UICONTROL Name]**, **[!UICONTROL Display Name]**, and **[!UICONTROL Description]** for the profile. Click **[!UICONTROL Done]**. A profile is created. 
1. Log in to [Cloud Manager](https://experience.adobe.com/#/@marketinghub/experiencemanager) and [create a program](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html) for your organization.
1. [Create environments](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=zh-Hant#adding-environments) within your program.
1. Log in to [Admin console](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/what-is-required/add-users-roles.html) and add developers or users to your organization.
1. Run the [build pipeline](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-manager/using/how-to-use/deploying-code.html). It brings latest [!DNL Experience Manager Forms] as a Cloud Service features to your environment.
1. [Start developing](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) and creating Adaptive Forms on [!DNL Experience Manager Forms] as a Cloud Service environment.
1. Configure the [local development environment](setup-local-development-environment.md) for rapid development

## Configure dispatcher caching {#caching}

You can make dispatcher caching related configuration changes to code on your local development instance and deploy the changes to your [!DNL AEM Forms] as a Cloud Service instance. For details, see [update dispatcher configuration](setup-local-development-environment.md).
 -->
