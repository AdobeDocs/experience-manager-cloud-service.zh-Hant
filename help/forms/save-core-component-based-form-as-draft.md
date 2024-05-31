---
title: 如何將基於最適化表單的核心元件儲存為草稿？
description: 瞭解如何將最適化表單的核心元件儲存為草稿，並建立Forms入口網站，以及在AEM Sites頁面上使用現成可用的核心元件。
feature: Adaptive Forms, Core Components
source-git-commit: 494e90bd5822495f0619e8ebf55f373a26a3ffe6
workflow-type: tm+mt
source-wordcount: '1072'
ht-degree: 1%

---


<span class="preview"> 本文包含搶鮮版功能的內容。 搶鮮版功能只能透過我們的 [發行前通道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features).

# 將核心元件型最適化表單儲存為草稿 {#save-af-form}

將最適化表單另存為草稿是提升使用者效率和正確性的重要功能。 此功能可讓使用者儲存進度並在稍後返回完成工作，而不會遺失任何輸入的資訊。 提供  `save-as-draft` 選項可確保管理時間的彈性、減少資料遺失的風險，並維持提交作業的精確度。 您可以將表單儲存為草稿，以便稍後完成。

## 考量事項

* [為您的環境啟用最適化Forms核心元件。](/help/forms/enable-adaptive-forms-core-components.md)

* 確保 [核心元件設定為3.0.24版或更新版本](https://github.com/adobe/aem-core-forms-components) 以使用此功能。
* 確定您有 [Azure儲存體帳戶和存取金鑰](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal) 以授權存取Azure儲存體帳戶。

## 將最適化表單儲存為草稿

[!DNL Experience Manager Forms] 資料整合(data-integration.md)提供 [!DNL Azure] 整合表單與的儲存體設定 [!DNL Azure] 儲存服務。 表單資料模型(FDM)可用來建立與互動的最適化Forms [!DNL Azure] 伺服器以啟用業務工作流程。

若要將表單儲存為草稿，請確保您擁有Azure儲存體帳戶和存取金鑰，以授權存取 [!DNL Azure] 儲存體帳戶。 若要將表單另存為草稿，請執行下列步驟：

1. [建立 Azure 儲存體設定](#create-azure-storage-configuration)
1. [為Forms入口網站設定統一的儲存聯結器](#configure-usc-forms-portal)
1. [建立將最適化表單儲存為草稿的規則](#rule-to-save-adaptive-form-as-draft)


### 1.建立Azure儲存體設定 {#create-azure-storage-configuration}

一旦您擁有Azure儲存體帳戶和存取金鑰，可授權存取 [!DNL Azure] 儲存體帳戶時，請執行以下步驟來建立Azure儲存體設定：

1. 瀏覽至 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Azure儲存體]**.

   ![Azure儲存卡選擇](/help/forms/assets/save-form-as-draft-azure-card.png)

1. 選取設定資料夾以建立設定，然後選取 **[!UICONTROL 建立]**.

   ![選取Azure儲存設定資料夾](/help/forms/assets/save-form-as-draft-select-config-folder.png)

1. 在中指定設定的標題 **[!UICONTROL 標題]** 欄位。
1. 指定 [!DNL Azure] 中的儲存體帳戶 **[!UICONTROL Azure儲存體帳戶]** 和 **[!UICONTROL Azure存取金鑰]** 欄位。

   ![Azure 儲存體設定](/help/forms/assets/save-form-as-draft-azure-storage.png)

1. 按一下「**儲存**」。

>[!NOTE]
>
> 您可以擷取 **[!UICONTROL Azure儲存體帳戶]** 和 **[!UICONTROL Azure存取金鑰]** 從 [Microsoft Azure入口網站](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal).


### 2.設定Forms入口網站的統一儲存聯結器 {#configure-usc-forms-portal}

成功建立Azure儲存體設定後，請使用下列步驟設定Forms Portal的統一儲存體聯結器：

1. 瀏覽至 **[!UICONTROL 工具]** > **[!UICONTROL Forms]** > **[!UICONTROL 統一的儲存聯結器]**.

   ![統一的聯結器儲存](/help/forms/assets/save-form-as-draft-unified-connector.png)

1. 在 **[!UICONTROL Forms入口網站]** 區段，選取 **[!UICONTROL Azure]** 從 **[!UICONTROL 儲存]** 下拉式清單。
1. 指定 [Azure儲存體設定的設定路徑](#create-azure-storage-configuration) 在 **[!UICONTROL 儲存設定路徑]** 欄位。

   ![統一的聯結器儲存設定](/help/forms/assets/save-form-as-draft-unified-connector-storage.png)

1. 選取 **[!UICONTROL 儲存]** 然後選取 **[!UICONTROL 發佈]** 以發佈設定。

### 3.建立規則以將最適化表單儲存為草稿 {#rule-to-save-adaptive-form-as-draft}

若要將表單儲存為草稿，請建立 **儲存表單** 規則，例如按鈕。 按一下按鈕時會觸發規則，而表單會儲存為草稿。 執行以下步驟以建立 **儲存表單** 按鈕元件的規則：

1. 在Author例項中，以編輯模式開啟調適型表單。
1. 從左窗格中選取 ![元件圖示](assets/components_icon.png) 並拖曳 **[!UICONTROL 按鈕]** 元件至表單。
1. 選取 **[!UICONTROL 按鈕]** 元件，然後選取 ![「設定」圖示](assets/configure_icon.png).
1. 選取 **[!UICONTROL 編輯規則]** 圖示以開啟規則編輯器。
1. 選取 **[!UICONTROL 建立]** 以設定及建立規則。
1. 在 **[!UICONTROL 時間]** 區段，選取 **已點按** 和 **[!UICONTROL 則]** 區段，選取 **儲存表單** 選項。
1. 選取 **[!UICONTROL 完成]** 以儲存規則。

![建立按鈕的規則](/help/forms/assets/save-form-as-drfat-create-rule.png)

預覽最適化表單時，請填寫並按一下 **儲存表單** 按鈕時，表單會儲存為草稿以供稍後使用。

## 在AEM Sites頁面上列出草稿的草稿和提交元件

AEM Forms提供 **草稿和提交** 開箱即用的入口網站元件，可在AEM Sites頁面上顯示已儲存的表單。 此 **草稿和提交** 元件會顯示儲存為草稿以供稍後完成的表單以及已提交的表單。 此元件透過列出與使用者建立的最適化Forms相關的草稿和提交，為任何登入使用者提供個人化體驗。

您可以使用現成的Forms Portal元件，在AEM Sites頁面中列出表單草稿。 執行以下步驟以使用 **草稿和提交** 入口網站元件：

1. [啟用草稿和提交Forms Portal元件](#enable-component)
2. [在AEM Sites頁面中新增草稿和提交元件](#Add-drafts-submissions-component)
3. [設定草稿和提交元件](#configure-drafts-submissions-component)

### 1.啟用草稿和提交Forms入口網站元件{#enable-component}

若要啟用 **[!UICONTROL 草稿和提交]** 元件時，請執行下列步驟：

1. 在中開啟AEM Sites頁面 **編輯** 模式。
1. 前往 **[!UICONTROL 頁面資訊]** > **[!UICONTROL 編輯範本]**
   ![編輯範本原則](/help/forms/assets/save-form-as-draft-edit-template.png)

1. 按一下 **[!UICONTROL 原則]** 並選取 **[!UICONTROL 草稿和提交]**  核取方塊( **[AEM原型專案名稱] - Forms與通訊入口網站**.

   ![原則選擇](/help/forms/assets/save-form-as-draft-enable-policy.png)

1. 按一下&#x200B;**[!UICONTROL 「完成」]**。

啟用入口網站元件後，您就可以在AEM Sites頁面的製作例項中使用它。

### 2.在AEM Sites頁面中新增草稿與提交元件{#Add-drafts-submissions-component}

您可以透過新增和設定入口網站元件，在使用AEM編寫的網站上建立和自訂Forms入口網站。 確保 [已啟用草稿和提交元件](#enable-component) 在AEM Sites頁面中使用它們之前。

若要新增元件，請從以下位置拖放元件： **草稿和提交** 元件窗格至頁面上的佈局容器，或選取佈局容器上的新增圖示，然後從以下位置新增元件： **[!UICONTROL 插入新元件]** 對話方塊。

![新增草稿和提交元件](/help/forms/assets/save-form-as-draft-add-dns.png)

### 3.設定草稿和提交元件 {#configure-drafts-submissions-component}

此 **草稿和提交** 元件會顯示儲存為草稿以供稍後完成及提交的表單。 進行設定 **草稿和提交**，請執行下列步驟：
1. 選取 **草稿和提交** 元件。
1. 按一下 ![「設定」圖示](assets/configure_icon.png) ，對話方塊就會顯示。
1. 在 **[!UICONTROL 草稿與提交]** 對話方塊，請指定下列專案：
   * **標題** 若要在Sites頁面中識別元件，預設情況下，標題會顯示在元件上方。
   * **型別**：將表單指定為草稿或已提交表單。
   * **版面**：以卡片或清單格式顯示清單草稿表單或已提交表單。

   ![草稿與提交元件屬性](/help/forms/assets/save-form-as-draft-dns-properties.png)

1. 按一下&#x200B;**「完成」**。

時間 **[!UICONTROL 選擇型別]** 已選取為 **草稿Forms**，儲存為草稿的表單會出現：
![草稿圖示](assets/drafts-component.png)

時間 **[!UICONTROL 選擇型別]** 已選取為 **已提交Forms**，則會顯示提交的表單：

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