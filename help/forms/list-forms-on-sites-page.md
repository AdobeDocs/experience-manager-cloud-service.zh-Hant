---
title: 如何使用Forms Portal元件在Adobe Experience Manager Sites頁面上列出表單？
description: 瞭解如何在AEM Sites頁面上列出表單。
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: 37e3ddd9-b20d-4156-b52e-64e36c455184
source-git-commit: 16b1e7ffa4e3812e9207bb283c63029939f7d14e
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 1%

---

# 列出網站頁面上的表單

想像一下，某個使用者造訪銀行的網站，搜尋開戶表單。 銀行使用Forms Portal元件，透過輸入特定關鍵字或依類別（例如「新帳戶」或「個人銀行」）篩選，幫助使用者快速找到表單，並可讓使用者輕鬆找到所需表單，而無需捲動冗長的清單。

Forms入口網站的&#x200B;**搜尋與清單製作程式**&#x200B;元件可讓您在Sites頁面上顯示和列出表單。 使用者可以根據特定條件設定並顯示完整的表單清單，以滿足組織需求。 匿名使用者可以造訪Sites頁面以檢視和瀏覽可用的表單。 使用位於畫面右上角的&#x200B;**排序依據**&#x200B;下拉式選項，可依遞增或遞減順序排序列出的表單。

![搜尋和製表器圖示](assets/search-and-lister-component.png)

## 先決條件

探索Forms Portal元件的各種功能之前，請確定您的環境已啟用核心元件。 安裝最新的Far，為AEM Cloud Service環境啟用最適化Forms核心元件。

<!--
## Enable Forms Portal components for your existing environment

To enable out-of-the-box Forms Portal components on existing AEM Forms as a Cloud Service, perform the following steps:

1. **Clone Cloud Manager Git repository on your local development instance:**  Your Cloud Manager Git repository contains a default AEM project. It is based on [AEM Archetype](https://github.com/adobe/aem-project-archetype/). Clone your Cloud Manager Git Repository using Self-Service Git Account Management from Cloud Manager UI to bring the project on your local development environment. For details on accessing the repository, see [Accessing Repositories](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/accessing-repos.html?lang=zh-Hant).  

1. **Create [!DNL Experience Manager Forms] as a [Cloud Service] project:** Create [!DNL Experience Manager Forms] as a [Cloud Service] project based on [AEM Archetype 50](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-50) or later. The archetype help developers easily start developing for [!DNL AEM Forms] as a Cloud Service. It also includes some sample themes and templates to help you started quickly.

    To create [!DNL Experience Manager Forms] as a Cloud Service project, open the command prompt and run the below command. To include [!DNL Forms] specific configurations, themes, and templates, set `includeForms=y`.  

    ```shell
    mvn -B archetype:generate -DarchetypeGroupId=com.adobe.aem -DarchetypeArtifactId=aem-project-archetype -DarchetypeVersion=30 -DaemVersion="cloud" -DappTitle="My Site" -DappId="mysite" -DgroupId="com.mysite" -DincludeForms="y"
    ```

    Also, change `appTitle`, `appId`, and `groupId`, in the above command to reflect your environment.

    After the project is ready, update the `<core.forms.components.version>x.y.z</core.forms.components.version>` property in the top-level `pom.xml` of the Archetype project to reflect the latest version of [core-forms-components](https://github.com/adobe/aem-core-forms-components) in your `AEM Archetype` project. 
 
1. **Deploy the project to your local development environment:** You can use the following command to deploy to your local development environment

    `mvn -PautoInstallPackage clean install`

    For the complete list of commands, see [Building and Installing](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=zh-Hant#building-and-installing)

1. [Deploy the archetype to your [!DNL AEM Forms] as a Cloud Service environment](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=zh-Hant#embeddeds). -->

將最新核心元件部署至您的環境後，您便可在編寫環境中存取Forms Portal元件。

## 列出網站頁面上的表單

若要將&#x200B;**Search &amp; Lister**&#x200B;入口網站元件新增至您的網站頁面，請執行下列步驟：

1. 以&#x200B;**編輯**&#x200B;模式開啟AEM Sites頁面。
1. 移至&#x200B;**[!UICONTROL 頁面資訊]** > **[!UICONTROL 編輯範本]**
   ![編輯範本原則](/help/forms/assets/save-form-as-draft-edit-template.png)

1. 按一下&#x200B;**[!UICONTROL 原則]**，然後選取&#x200B;**[!UICONTROL AEM Archetype專案名稱]** - Forms和通訊入口網站&#x200B;**[下的]搜尋與清單程式**&#x200B;核取方塊。

   ![原則選擇](/help/forms/assets/search-lister-enable-policy.png)

1. 按一下&#x200B;**[!UICONTROL 「完成」]**。
1. 現在，請在撰寫模式中重新開啟AEM Sites頁面。
1. 在頁面編輯器中找出區段，讓您新增Forms Portal元件。

1. 按一下&#x200B;**新增**&#x200B;圖示。 圖示是加號(+)，表示可新增元件的選項。

   按一下&#x200B;**新增**&#x200B;圖示會顯示&#x200B;**插入新元件**&#x200B;對話方塊，其中顯示要插入的各種元件。

   >[!NOTE]
   >
   > 或者，您也可以拖放元件。

1. 瀏覽對話方塊中的可用元件，並從清單中選取所需元件。 例如，從清單中選取&#x200B;**Search and Lister**&#x200B;元件，以新增&#x200B;**Search &amp; Lister** Forms Portal元件。

   ![搜尋和清單元件](/help/forms/assets/add-search-lister.png)

現在，請設定&#x200B;**Search and Lister**&#x200B;元件的屬性。

## 瞭解「搜尋並製表器」元件的屬性

您可以使用[設定]對話方塊輕鬆自訂&#x200B;**搜尋和清單程式**&#x200B;元件屬性，以提供順暢的使用者體驗。 若要設定，請選取元件，然後選取![設定圖示](assets/configure_icon.png)。 **[!UICONTROL 搜尋與清單製作者]**&#x200B;對話方塊開啟。

### 顯示標籤

![顯示標籤](/help/forms/assets/search-and-lister-display-tab.png)

1. 在&#x200B;**[!UICONTROL Title]**&#x200B;中，指定Search &amp; Lister元件的標題。 指示性標題可讓使用者在表單清單中執行快速搜尋。
1. 從&#x200B;**[!UICONTROL 配置]**&#x200B;清單中，選取配置以卡片或清單格式表示表單。
1. 選取&#x200B;**[!UICONTROL 隱藏搜尋]**&#x200B;和&#x200B;**[!UICONTROL 隱藏排序]**&#x200B;以隱藏搜尋並按功能排序。
1. 在&#x200B;**[!UICONTROL 工具提示]**&#x200B;中，提供將游標停留在元件上時顯示的工具提示。

### 資產索引標籤

![資產標籤](/help/forms/assets/search-and-lister-asset-tab.png)

1. 在&#x200B;**[!UICONTROL 資產資料夾]**&#x200B;索引標籤中，指定提取表單並列在頁面上的位置。
1. 使用&#x200B;**[!UICONTROL 新增其他位置]**，您可以設定多個資料夾位置。

### 結果標籤

![顯示標籤](/help/forms/assets/search-and-lister-result-tab.png)

在&#x200B;**[!UICONTROL 結果]**&#x200B;索引標籤中，設定每頁要顯示的表單數目上限。 預設為每頁八個表單。

## 使用Search &amp; Lister元件在Sites頁面上檢視表單

若要檢視表單清單，請使用&#x200B;**Search &amp; Lister** Forms Portal元件。 預覽AEM Sites頁面，以檢視熒幕上顯示之&#x200B;**Assets**&#x200B;資料夾中的表單清單。 您也可以使用搜尋列來搜尋特定表單。

![搜尋和製表器圖示](assets/search-and-lister-component.png)

<!--
## Configure Azure Storage for Adaptive Forms {#configure-azure-storage-adaptive-forms}

[[!DNL Experience Manager Forms] Data Integration](data-integration.md) provides [!DNL Azure] storage configuration to integrate forms with [!DNL Azure] storage services. The Form Data Model (FDM) can be used to create Adaptive Forms that interact with [!DNL Azure] server to enable business workflows.

### Create Azure Storage Configuration {#create-azure-storage-configuration}

Before executing these steps, ensure that you have an Azure storage account and an access key to authorize access to the [!DNL Azure] storage account.

1. Navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Cloud Services]** &gt; **[!UICONTROL Azure Storage]**.
1. Select a folder to create the configuration and select **[!UICONTROL Create]**.
1. Specify a title for the configuration in the **[!UICONTROL Title]** field.
1. Specify the name of the [!DNL Azure] storage account in the **[!UICONTROL Azure Storage Account]** field.

### Configure Unified Storage Connector for Forms Portal {#configure-usc-forms-portal}

Perform the following steps to configure Unified Storage Connector for AEM Workflows:

1. Navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Forms]** &gt; **[!UICONTROL Unified Storage Connector]**.
1. In the **[!UICONTROL Forms Portal]** section, select **[!UICONTROL Azure]** from the **[!UICONTROL Storage]** drop-down list.
1. Specify the [configuration path for the Azure storage configuration](#create-azure-storage-configuration) in the **[!UICONTROL Storage Configuration Path]** field.
1. Select **[!UICONTROL Publish]** and then select **[!UICONTROL Save]** to save the configuration.

## Enable Forms Portal Components {#enable-forms-portal-components}

To use any core component (including the out-of-the-box portal components) in an Adobe Experience Manager (AEM) site, you must create a proxy component and enable it for your site. For creating a proxy component and enabling portal components, see [Using Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/using.html?lang=zh-Hant#create-proxy-components). 

Once a portal component is enabled, you can use it in the author instance of your sites page.

## Add and Configure Forms Portal Components {#configure-forms-portal-components}

You can create and customize Forms Portal on websites authored using AEM by adding and configuring the portal components. Ensure that the [components are enabled](#enable-forms-portal-components) before using them in the Forms Portal.

To add a component, either drag and drop the component from the Components pane to the layout container on the page, or select the add icon on the layout container and add the component from the [!UICONTROL Insert New Component] dialog.

### Configure Drafts & Submissions Component {#configure-drafts-submissions-component}

The Drafts & Submissions component displays forms that are saved as draft for completing later and submitted forms. To configure, select the component and then select the ![Configure icon](assets/configure_icon.png). In the [!UICONTROL Drafts and Submissions] dialog, specify the title to indicate the form listing as draft or submitted forms. Also select whether the component should list draft forms or submitted forms in card or list format.

![Drafts icon](assets/drafts-component.png)

![Submissions icon](assets/submission-listing.png)

### Configure Search & Lister Component {#configure-search-lister-component}

The Search & Lister component is used to list adaptive forms on a page and to implement search on the listed forms. 

![Search and Lister icon](assets/search-and-lister-component.png)

To configure, select the component and then select the ![Configure icon](assets/configure_icon.png). The [!UICONTROL Search and Lister] dialog opens.

1. In the [!UICONTROL Display] tab, configure the following:
    * In **[!UICONTROL Title]**, specify the title for the Search & Lister component. An indicative title enables the users perform quick search across the list of forms.
    * From the **[!UICONTROL Layout]** list, select the layout to represent the forms in card or list format.
    * Select **[!UICONTROL Hide Search]** and **[!UICONTROL Hide Sorting]** to hide the search and sort by features.
    * In **[!UICONTROL Tooltip]**, provide the tooltip that appears when you hover over the component. 
1. In the [!UICONTROL Asset Folder] tab, specify the location from where the forms are pulled and listed on the page. You can configure multiple folder locations.
1. In the [!UICONTROL Results] tab, configure the maximum number of forms to display per page. The default is eight forms per page.

### Configure Link Component {#configure-link-component}

The link component enables you to provide links to an adaptive form on the page. To configure, select the component and then select the ![Configure icon](assets/configure_icon.png). The [!UICONTROL Edit Link Component] dialog opens.

1. In the [!UICONTROL Display] tab, provide the link caption and tooltip to ease identification of the forms represented by the link.
1. In the [!UICONTROL Asset Info] tab, specify the repository path where the asset is stored. 
1. In the [!UICONTROL Query Params] tab, specify the additional parameters in the key-value pair format. When the link is clicked, these additional parameters and passed along with the form.

## Configure Asynchronous Form Submission Using Adobe Sign {#configure-asynchronous-form-submission-using-adobe-sign}

You can configure to submit an adaptive form only when all the recipients have completed the signing ceremony. Follow the steps below to configure the setting using Adobe Sign.

1. In the author instance, open an Adaptive Form in the edit mode.
1. From the left pane, select the Properties icon and expand the **[!UICONTROL ELECTRONIC SIGNTATURE]** option.
1. Select **[!UICONTROL Enable Adobe Sign]**. Various configuration options display. 
1. In the [!UICONTROL Submit the form] section, select the **[!UICONTROL after every recipient completes signing ceremony]** option to configure the Submit Form action, where the form is first sent to all the recipients for signing. Once all the recipients have signed the form, only then the form is submitted. 

## Save Adaptive Forms As Drafts {#save-adaptive-forms-as-drafts}

You can save forms as Drafts for completing them later. There are two ways in which a form is saved as a draft:

* Create a "Save Form" rule on a form component, for example, a button. On clicking the button, the rule triggers and the form are saved a draft.
* Enable Auto-Save feature, which saves the form as per the specified event or after a configured interval of time.

### Create Rules to Save an Adaptive Form as Draft {#rule-to-save-adaptive-form-as-draft}

To create a "Save Form" rule on a form component, for example, a button, follow the steps below:

1. In the author instance, open an Adaptive Form in edit mode.
1. From the left pane, select ![Components icon](assets/components_icon.png) and drag the [!UICONTROL Button] component to the form.
1. Select the [!UICONTROL Button] component and then select the ![Configure icon](assets/configure_icon.png). 
1. Select the [!UICONTROL Edit Rules] icon to open the Rule Editor. 
1. Select **[!UICONTROL Create]** to configure and create the rule.
1. In the [!UICONTROL When] section, select "is clicked" and in the [!UICONTROL Then] section, select the "Save Form" options.
1. Select **[!UICONTROL Done]** to save the rule.

### Enable Auto-save {#enable-auto-save}

You can configure the auto-save feature for an adaptive form as follows:

1. In the author instance, open an Adaptive Form in edit mode.
1. From the left pane, select the ![Properties icon](assets/configure_icon.png) and expand the [!UICONTROL AUTO-SAVE] option.
1. Select the **[!UICONTROL Enable]** check box to enable auto-save of the form. You can configure the following:
* By default, the [!UICONTROL Adaptive Form Event] is set to "true", which implies that the form is auto-saved after every event.
* In [!UICONTROL Trigger], configure to trigger auto-save based on the occurrence of an event or after a specific interval of time.
-->


## 後續步驟

在下一篇文章中，讓我們瞭解[如何將表單儲存為草稿，並使用Forms Portal元件草稿和提交在Sites頁面上將其列出](/help/forms/save-core-component-based-form-as-draft.md)。

## 相關的文章

{{forms-portal-see-also}}

## 另請參閱 {#see-also}

{{see-also}}
