---
title: 如何將基於最適化表單的核心元件儲存為草稿？
description: 瞭解如何將最適化表單的核心元件儲存為草稿，並建立Forms入口網站，以及在AEM Sites頁面上使用現成可用的核心元件。
feature: Adaptive Forms, Core Components
exl-id: c0653bef-afeb-40c1-b131-7d87ca5542bc
role: User, Developer, Admin
source-git-commit: 52b87073cad84705b5dc0c6530aff44d1e686609
workflow-type: tm+mt
source-wordcount: '1053'
ht-degree: 2%

---


# 將核心元件型最適化表單儲存為草稿 {#save-af-form}

將最適化表單另存為草稿是提升使用者效率和正確性的重要功能。 此功能可讓使用者儲存進度並在稍後返回完成工作，而不會遺失任何輸入的資訊。 提供`save-as-draft`選項可確保管理時間的彈性、減少資料遺失的風險，並維持提交作業的精確度。 您可以將表單儲存為草稿，以便稍後完成。

## 考量事項

* [為您的環境啟用最適化Forms核心元件。](/help/forms/enable-adaptive-forms-core-components.md)

* 請確定[核心元件設定為3.0.24版或更新版本](https://github.com/adobe/aem-core-forms-components)以使用此功能。
* 確定您有[Azure儲存體帳戶和存取金鑰](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal)，以授權存取Azure儲存體帳戶。

## 將最適化表單另存為草稿

[!DNL Experience Manager Forms] Data Integration (data-integration.md)提供[!DNL Azure]儲存設定，以將表單與[!DNL Azure]儲存服務整合。 表單資料模型(FDM)可用來建立與[!DNL Azure]伺服器互動的Adaptive Forms，以啟用業務工作流程。

若要將表單儲存為草稿，請確定您擁有Azure儲存體帳戶和存取金鑰，以授權存取[!DNL Azure]儲存體帳戶。 若要將表單另存為草稿，請執行下列步驟：

1. [建立 Azure 儲存體設定](#create-azure-storage-configuration)
1. [為Forms入口網站設定統一的儲存聯結器](#configure-usc-forms-portal)
1. [建立將最適化表單儲存為草稿的規則](#rule-to-save-adaptive-form-as-draft)


### 1.建立Azure儲存體設定 {#create-azure-storage-configuration}

一旦您擁有Azure儲存體帳戶和存取金鑰以授權存取[!DNL Azure]儲存體帳戶，請執行下列步驟以建立Azure儲存體設定：

1. 導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Azure儲存體]**。

   ![選擇Azure儲存卡](/help/forms/assets/save-form-as-draft-azure-card.png)

1. 選取設定資料夾以建立設定，並選取&#x200B;**[!UICONTROL 建立]**。

   ![選取Azure儲存設定資料夾](/help/forms/assets/save-form-as-draft-select-config-folder.png)

1. 在&#x200B;**[!UICONTROL 標題]**&#x200B;欄位中指定組態的標題。
1. 在&#x200B;**[!UICONTROL Azure儲存體帳戶]**&#x200B;和&#x200B;**[!UICONTROL Azure存取金鑰]**&#x200B;欄位中指定[!DNL Azure]儲存體帳戶的名稱。

   ![Azure 儲存體設定](/help/forms/assets/save-form-as-draft-azure-storage.png)

1. 按一下「**儲存**」。

>[!NOTE]
>
> 您可以從[Microsoft Azure入口網站](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal)擷取&#x200B;**[!UICONTROL Azure儲存體帳戶]**&#x200B;和&#x200B;**[!UICONTROL Azure存取金鑰]**。


### 2.設定Forms入口網站的統一儲存聯結器 {#configure-usc-forms-portal}

成功建立Azure儲存體設定後，請使用下列步驟設定Forms Portal的統一儲存體聯結器：

1. 導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Forms]** > **[!UICONTROL 整合式儲存聯結器]**。

   ![統一的聯結器存放區](/help/forms/assets/save-form-as-draft-unified-connector.png)

1. 在&#x200B;**[!UICONTROL Forms入口網站]**&#x200B;區段中，從&#x200B;**[!UICONTROL 儲存體]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Azure]**。
1. 在&#x200B;**[!UICONTROL 儲存設定路徑]**&#x200B;欄位中指定Azure儲存體設定](#create-azure-storage-configuration)的[設定路徑。

   ![統一的聯結器儲存設定](/help/forms/assets/save-form-as-draft-unified-connector-storage.png)

1. 選取&#x200B;**[!UICONTROL 儲存]**，然後選取&#x200B;**[!UICONTROL Publish]**&#x200B;以發佈組態。

### 3.建立規則以將最適化表單儲存為草稿 {#rule-to-save-adaptive-form-as-draft}

若要將表單儲存為草稿，請在表單元件（例如按鈕）上建立&#x200B;**儲存表單**&#x200B;規則。 按一下按鈕時會觸發規則，而表單會儲存為草稿。 執行以下步驟，在按鈕元件上建立&#x200B;**儲存表單**&#x200B;規則：

1. 在Author例項中，以編輯模式開啟調適型表單。
1. 從左窗格中，選取![元件圖示](assets/components_icon.png)並將&#x200B;**[!UICONTROL Button]**&#x200B;元件拖曳至表單。
1. 選取&#x200B;**[!UICONTROL 按鈕]**&#x200B;元件，然後選取![設定圖示](assets/configure_icon.png)。
1. 選取&#x200B;**[!UICONTROL 編輯規則]**&#x200B;圖示以開啟規則編輯器。
1. 選取「**[!UICONTROL 建立]**」以設定及建立規則。
1. 在&#x200B;**[!UICONTROL When]**&#x200B;區段中，選取&#x200B;**已點按**，並在&#x200B;**[!UICONTROL Then]**&#x200B;區段中，選取&#x200B;**儲存表單**&#x200B;選項。
1. 選取&#x200B;**[!UICONTROL 完成]**&#x200B;以儲存規則。

![建立按鈕](/help/forms/assets/save-form-as-drfat-create-rule.png)的規則

當您預覽最適化表單並填寫時，按一下&#x200B;**儲存表單**&#x200B;按鈕，表單會儲存為草稿以供稍後使用。

## 在AEM Sites頁面上列出草稿的草稿和提交元件

AEM Forms提供立即可用的&#x200B;**草稿和提交**&#x200B;入口網站元件，以便在AEM Sites頁面上顯示已儲存的表單。 **草稿和提交**&#x200B;元件會顯示儲存為草稿以供稍後完成的表單以及提交的表單。 此元件透過列出與使用者建立的最適化Forms相關的草稿和提交，為任何登入使用者提供個人化體驗。

您可以使用現成的Forms Portal元件，在AEM Sites頁面中列出表單草稿。 執行以下步驟以使用&#x200B;**草稿和提交**&#x200B;入口網站元件：

1. [啟用草稿和提交Forms Portal元件](#enable-component)
2. [在AEM Sites頁面中新增草稿和提交元件](#Add-drafts-submissions-component)
3. [設定草稿和提交元件](#configure-drafts-submissions-component)

### 1.啟用草稿和提交Forms入口網站元件{#enable-component}

若要啟用範本原則中的&#x200B;**[!UICONTROL 草稿與提交]**&#x200B;元件，請執行下列步驟：

1. 以&#x200B;**編輯**&#x200B;模式開啟AEM Sites頁面。
1. 移至&#x200B;**[!UICONTROL 頁面資訊]** > **[!UICONTROL 編輯範本]**
   ![編輯範本原則](/help/forms/assets/save-form-as-draft-edit-template.png)

1. 按一下&#x200B;**[!UICONTROL 原則]**，然後選取&#x200B;**[AEM Archetype專案名稱] - Forms和通訊入口網站**&#x200B;下的&#x200B;**[!UICONTROL 草稿與提交]**&#x200B;核取方塊。

   ![原則選擇](/help/forms/assets/save-form-as-draft-enable-policy.png)

1. 按一下&#x200B;**[!UICONTROL 「完成」]**。

啟用入口網站元件後，您就可以在AEM Sites頁面的製作例項中使用它。

### 2.在AEM Sites頁面中新增草稿與提交元件{#Add-drafts-submissions-component}

您可以透過新增和設定入口網站元件，在使用AEM編寫的網站上建立和自訂Forms入口網站。 在AEM Sites頁面中使用[草稿和提交元件之前，請確定已啟用](#enable-component)。

若要新增元件，請將元件從&#x200B;**草稿和提交**&#x200B;元件窗格拖放至頁面上的配置容器，或選取配置容器上的新增圖示，然後從&#x200B;**[!UICONTROL 插入新元件]**&#x200B;對話方塊新增元件。

![新增草稿與提交元件](/help/forms/assets/save-form-as-draft-add-dns.png)

### 3.設定草稿和提交元件 {#configure-drafts-submissions-component}

**草稿和提交**&#x200B;元件會顯示儲存為草稿以供稍後完成和提交之表單的表單。 若要設定&#x200B;**草稿與提交**，請執行下列步驟：
1. 選取&#x200B;**草稿與提交**&#x200B;元件。
1. 按一下![設定圖示](assets/configure_icon.png)，對話方塊就會顯示。
1. 在&#x200B;**[!UICONTROL 草稿和提交]**&#x200B;對話方塊中，指定下列專案：
   * **標題**&#x200B;若要識別Sites頁面中的元件，根據預設，標題會顯示在元件上方。
   * **型別**：表示表單清單為草稿或已提交的表單。
   * **配置**：以卡片或清單格式顯示清單草稿表單或已提交的表單。

   ![草稿與提交元件屬性](/help/forms/assets/save-form-as-draft-dns-properties.png)

1. 按一下&#x200B;**「完成」**。

當&#x200B;**[!UICONTROL 選取型別]**&#x200B;選取為&#x200B;**草稿Forms**時，儲存為草稿的表單會出現：
![草稿圖示](assets/drafts-component.png)

當&#x200B;**[!UICONTROL 選取型別]**&#x200B;選取為&#x200B;**已提交的Forms**&#x200B;時，已提交的表單會出現：

![提交圖示](assets/submission-listing.png)

您可以按一下個別表單以開啟表單。

<!--

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

## 另請參閱 {#see-also}

{{see-also}}



<!--

>[!MORELIKETHIS]
>
>* [Configure data sources for AEM Forms](/help/forms/configure-data-sources.md)
>* [Configure Azure storage for AEM Forms](/help/forms/configure-azure-storage.md)
>* [Integrate Microsoft Dynamics 365 and Salesforce with Adaptive Forms](/help/forms/configure-msdynamics-salesforce.md)

-->
