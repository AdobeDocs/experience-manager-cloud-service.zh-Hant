---
title: 如何根據核心元件建立最適化表單範本？
description: 根據核心元件建立最適化表單範本，以使用範本編輯器定義基本結構和初始內容。
feature: Adaptive Forms, Core Components
Keywords: create adaptive form template, create adaptive form template based on core components, Use template to create adpative form.
exl-id: c1c050d3-953e-4e56-a96b-d84f2ec05e5e
role: User, Developer
source-git-commit: e9c595d0afae5c29adf2842bfb2ee28a046b804c
workflow-type: tm+mt
source-wordcount: '1951'
ht-degree: 1%

---

# 建立以核心元件為基礎的最適化表單範本 {#adaptive-form-templates}

當您編寫表單時，可在編輯器中新增欄位和元件以定義表單結構、內容和動作。 您在表單容器的`guideRootPanel`中新增欄位和元件。 使用範本編輯器，您可以建立包含基本結構和初始內容的範本，以供作者建立表單。

例如，您希望所有表單作者在登錄檔單中都擁有某些文字方塊、導覽按鈕和提交按鈕。 您可以使用作者可用來建立與其他登錄檔單一致的表單的元件，來建立範本。 當作者使用範本建立最適化表單時，新表單會繼承您在範本中指定的結構和元件。 範本編輯器可讓您：

* 在結構圖層中新增表單的頁首與頁尾元件。
* 提供表單的初始內容。
* 指定主題，提交動作。

<!--
You can download and install [!DNL AEM Forms] reference content package from [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) portal to import reference themes and templates to your environment.
-->

## 先決條件

**為您的環境啟用最適化Forms核心元件**：當您建立程式時，最適化Forms核心元件已為您的環境啟用。請安裝最新版本以為您的AEM Cloud Service環境啟用最適化Forms核心元件。

>[!NOTE]
>
> 根據Archetype 45部署Forms as a Cloud Service環境時，**最適化Forms （核心元件）**&#x200B;範本和核心元件型主題會新增到您的環境中。

## 使用範本 {#working-with-templates}

您可以導覽至&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL 範本]**，從「工具」功能表存取範本編輯器。 範本會整理在啟用可編輯範本的資料夾中。

>[!NOTE]
>
> 您可以在核心元件特定的資料夾中找到核心元件型的可編輯範本。

Experience Manager提供可組織範本的全域資料夾。 但預設不會啟用。 您可以要求管理員啟用全域資料夾或建立範本資料夾。 如需有關如何建立資料夾的詳細資訊，請參閱[範本資料夾](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/features/templates.html#editing-templates-template-authors)。

## 建立範本 {#create-template}

建立資料夾後，請開啟資料夾並執行以下步驟來建立範本：

1. 在您建立的資料夾中選取&#x200B;**[!UICONTROL 建立]**。
1. 在&#x200B;**[!UICONTROL 挑選範本型別]**&#x200B;區段中，選取&#x200B;**[!UICONTROL 最適化表單（核心元件）範本]**&#x200B;並選取&#x200B;**[!UICONTROL 下一步]**。

1. 在&#x200B;**[!UICONTROL 範本詳細資料]**&#x200B;區段中，提供&#x200B;**範本標題**&#x200B;並選取&#x200B;**[!UICONTROL 建立]**。
您也可以提供說明。

1. 選取&#x200B;**[!UICONTROL 完成]**&#x200B;以返回主控台，或選取&#x200B;**[!UICONTROL 開啟]**&#x200B;以在編輯器中開啟範本。

## 範本編輯器UI {#template-editor-ui}

開啟範本進行編輯時，您可以看到下列AEM Editor元件：

* **頁面工具列**
包含下列選項：

   * **切換側面板**：可讓您顯示或隱藏側欄。
   * **頁面資訊**：可讓您指定發佈/取消發佈時間、縮圖、使用者端資料庫、頁面原則及頁面設計使用者端資料庫等資訊。
     <!-- * **Emulator**: Lets you simulate and customize the look for different devices.-->
   * **模式選取器：**&#x200B;可讓您變更模式。 您可以選擇&#x200B;**[!UICONTROL 結構]**&#x200B;模式、**[!UICONTROL 初始內容]**、**[!UICONTROL 配置控制項]**&#x200B;模式。 「結構」模式可讓您新增及自訂頁首與頁尾。 初始內容模式可讓您自訂表單內容。
   * **預覽：**&#x200B;讓您預覽範本在發佈時的外觀。 您可以使用「圖層選取器」和「預覽」來切換編輯和預覽模式。
* **側欄：**&#x200B;提供內容、屬性、Assets和元件瀏覽器。
* **元件工具列：**&#x200B;選取元件時，您會看到可自訂元件的工具列。
* **頁面**：您新增內容以建立範本的區域。

<!-- See [Introduction to authoring Adaptive Forms](introduction-forms-authoring.md) to understand the Touch UI editor. -->

## 編輯範本 {#editing-a-template}

選取和編輯範本適當外觀的不同模式包括：

* [結構](#structure)
* [初始內容](#initial-content)
* [版面配置](#layout)

圖層選取器位於熒幕右上角的「預覽」選項旁。

### 結構 {#structure}

當您在範本編輯器中選取結構層時，它有助於預先定義內容，而在建立與範本關聯的調適型Forms時無法變更內容。

<!-- you can see the layout containers above and below the Adaptive Form Container. Authors can use these layout containers for header and footer. -->


結構圖層中的![配置容器](/help/forms/assets/header-layer-selector-core-component.png)

<!--

**A. Layout container for Header component**
Drag-drop the Adaptive Form Header component in the layout container above the Adaptive Form Container. After you add the component, you can specify its properties that let you add a logo and provide its title.
**B. Adaptive Form Container component**
Drag-drop the Adaptive Form components in the Adaptive Form Container. You can specify the design and arrangement of fields and components in the template editor. After you add the components, you can specify its properties.
**C. Layout container for Footer component**
Similarly, when you drag-drop the footer component in the layout container below the Adaptive Form Container, you can provide the copyright information and company details. 
You can add, edit, or customize the header and footer. Drag-drop the Adaptive Form Header and Footer component to customize the template. Drag-drop the Adaptive Form components in the Adaptive Form Container. You can specify the design and arrangement of fields and components in the template editor. 


Header and footer are added in the Initial Content layer.
-->

#### 鎖定/解除鎖定結構層中的元件 {#locking-unlocking-components-in-the-structure-layer}

當您在選取結構圖層的情況下編輯範本時，可以解鎖範本的頁首和頁尾。 如果範本中的元件已解除鎖定，表單作者可以在使用該範本的最適化表單中編輯元件。 鎖定元件會使表單作者無法在最適化表單中編輯它。 元件工具列中有鎖定選項。

例如，在範本中新增標題元件。 選取元件時，您會在元件工具列中看到鎖定選項。 通常頁首包含公司名稱和標誌，您不希望表單作者變更範本中的標誌和頁首。 在使用範本建立並鎖定頁首元件的調適型表單中，表單作者無法變更標誌和公司名稱。

>[!NOTE]
>
>不建議分別鎖定或解除鎖定頁首元件中的影像或標誌。 您可以解除鎖定標頭元件。

### 初始內容 {#initial-content}

選取「初始內容」選項時，範本的「最適化表單」容器會像要編輯的最適化表單一樣開啟。 它可讓您建立預先定義的內容，此內容可在建立與範本關聯的最適化Forms時變更。 如同製作最適化表單，您可以指定初始設定，例如選取主題和提交動作。

表單作者可將其用作建立表單的基礎。 內容流程結構是在範本的「初始內容」層中所指定。 若要切換到編輯表單範本的初始內容，在頁面工具列的[預覽]之前，選取![畫佈下拉式清單](assets/canvas-drop-down.png) **>** **[!UICONTROL 初始內容]**。

![頁首與頁尾已新增至初始內容層](assets/header-and-footer.png)

在初始內容層中，您建立作者用作基礎的最適化表單範本。 製作範本與製作表單類似，您會使用側邊欄中的可用選項。 側欄提供內容、屬性、資產和元件瀏覽器。

<!-- See [Sidebar](introduction-forms-authoring.md#sidebar). -->

>[!NOTE]
>
>當您選取「儲存內容」或「儲存PDF」作為「提交動作」時，您會獲得一個選項來指定「儲存」路徑。 如果您在範本中指定路徑，則以此範本建立的所有表單都會有相同的路徑。 您可以指定正確的儲存路徑，或確保表單作者更新路徑，以防止每個表單中的資料都儲存在相同位置。

### 版面配置 {#layout}

編輯範本時，您可以定義版面，這會使用標準回應式版面。 佈局有助於根據裝置寬度管理元件的寬度，以促進回應式最適化表單設計。

結構圖層中的![配置容器](/help/forms/assets/layout-template-core-component.png)

如需詳細資訊，請參閱文章[瞭解回應式配置](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/responsive-layout-feature-video-understand.html?lang=en)。

## 啟用範本 {#enabling-the-template}

當您建立範本時，它會新增為草稿。 啟用範本以將其用於建立最適化Forms。 若要啟用範本：

1. 導覽至&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 工具]** > **[!UICONTROL 範本]**，並開啟您建立範本的資料夾。
您建立的範本會標示為「草稿」。
1. 選取範本並在工具列中選取&#x200B;**[!UICONTROL 啟用]**。
建立最適化表單時，系統要求您選擇範本時，您會看到範本列出。

## 匯入或匯出範本 {#importing-or-exporting-a-template}

表單可與其範本搭配使用。 下載使用自訂範本建立的最適化表單時，未下載範本。 當您在不同的[!DNL AEM Forms]執行個體上匯入表單時，會匯入表單而不包含其範本。 如果表單已匯入，但其範本無法使用，則不會轉譯表單。 您可以封裝來自`/conf`中`https://<server>:<port>/crx/packmgr`節點的自訂範本，並將其連線您要上傳表單的[!DNL AEM Forms]執行個體。 您也可以[使用AEM Archetype建立範本，並將其部署至您的雲端服務執行個體](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/pages-templates.html#prerequisites)。

>[!NOTE]
>
> * 您也可以直接從最適化表單編輯器或最適化表單範本編輯器設定[!UICONTROL 記錄檔案]範本。 如需詳細資訊，請參閱[產生最適化Forms的記錄檔案](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#document-of-record-support-in-adaptive-form-editor-dor-support-in-adaptiveform)。

## 將表單資料模型結構描述關聯至範本 {#associating-form-data-model-schema-in-template}

作者可以在範本編輯器中將[!UICONTROL 表單資料模型結構描述]關聯到調適型表單範本。 它可讓作者從範本編輯器選取結構。 當您將結構描述與範本建立關聯，且表單作者根據範本建立表單時，系統會為表單預先選取結構描述。 它有助於表單作者規範架構的使用，也可為表單作者節省時間。 若要在範本編輯器中選取表單資料模型結構描述：

1. 選取位於左側的&#x200B;**[!UICONTROL 內容瀏覽器]**。
1. 移至表單容器&#x200B;**[!UICONTROL 設定]**。
1. 選取&#x200B;**[!UICONTROL 資料模型]**。
1. 選擇您的表單資料模型(FDM)至&#x200B;**[!UICONTROL 選擇表單資料模型]**&#x200B;並儲存組態。

![Form-Data-Model-Association-in-Forms](/help/forms/assets/select-form-data-model-img-core-component.png)

<!--

## Creating an Adaptive Form template with tabs and panels {#creating-an-adaptive-form-template-with-tabs-and-panels-nbs}

For example, you want to create a template with the following tabs:

* General Information
* Professional Information

You have added a logo, provided a title, and added a footer in the structure layer. Lock the header and footer to stop form authors from editing them when they use the template to create forms.

Change the layer from **Structure** to **Initial Content**, and start adding content to the form. To create a tabbed structure, add a child Panel in the guideRootPanel of the Adaptive Form container. To add a panel:

* You can add a panel by tapping the **[!UICONTROL +]** button when you select the **[!UICONTROL Drag components here]** option.

* You can drag-drop the panel component from the components browser in the sidebar.
* You can add child panel of the `guideRootPanel` from the component toolbar.

To create the General Information and Professional Information tabs, add two panels in the child panel of the `guideRootPanel`. Select the panels and select ![cmppr](assets/configure-icon.svg) to open the properties in the sidebar. Change the element names as `general-info` and `professional-info`, and titles as General Information and Professional Information respectively. In the sidebar, select content to open the content browser. In the Form Objects tab, select `guideRootPanel`. In the editor, the guideRootPanel is selected. Select ![cmppr](assets/configure-icon.svg) in the component toolbar to open its properties. In the Panel Layout field, select **[!UICONTROL Tabs on Top]** and select **[!UICONTROL Done]**. The tabbed template structure is applied.

### Adding content in tabs {#adding-content-in-tabs}

After you add panels and structure them as tabs, you can add fields inside the tabs. When you select a tab in the editor, you can see the **[!UICONTROL Drag components here]** option. You can drag-drop components such as text-boxes, list items, and buttons. You can drag-drop components from the components browser in the sidebar.

Each component has properties that enhance data capturing and manipulation. For example, you can enable the **[!UICONTROL Required field]** property of a component. Your authors can specify a message that your customers see when they skip filling a required field. Specify the message in **[!UICONTROL Required Field Message]** property.

In the example template, Name, Phone number, and Date of birth fields are added in the General Information tab. In the Professional Information tab, Currently employed, employment type, Educational qualification fields are added.

After you have added fields, you can add buttons such as Submit and Reset.
-->

### 使用範本原則新增自訂屬性至最適化表單元件

自訂屬性可讓您使用表單範本，將自訂屬性（索引鍵/值組）與最適化表單核心元件建立關聯。 自訂屬性會反映在元件Headless轉譯的&#x200B;**[!UICONTROL 屬性]**&#x200B;區段中。 它可讓您建立根據自訂屬性值調整的動態表單行為。 例如，開發人員可以為行動、桌上型電腦或Web平台設計各種無頭Forms元件的轉譯，大幅提升各種裝置的使用者體驗。

將自訂屬性新增至最適化表單核心元件欄位的步驟如下：

1. [在範本編輯器的原則中新增自訂群組名稱](#add-a-custom-group-name)
1. [在調適型表單元件的編輯對話方塊中選取自訂群組名稱](#select-a-custom-group-name)

#### 在範本編輯器的原則中新增自訂群組名稱 {#add-a-custom-group-name}

1. 移至&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL 範本]**。
1. 根據核心元件選取範本，並以編輯模式開啟。
1. 按一下需要定義自訂屬性之最適化表單核心元件欄位的&#x200B;**[!UICONTROL 原則]** ![原則](/help/forms/assets/Smock_FeedManagement_18_N.svg)圖示。 **[!UICONTROL 最適化表單欄位]**&#x200B;對話方塊就會顯示。
1. 選取&#x200B;**[!UICONTROL 自訂屬性]**&#x200B;標籤。
1. 在&#x200B;**[!UICONTROL 原則]**&#x200B;區段下指定&#x200B;**[!UICONTROL 原則標題]**。
1. 指定&#x200B;**[!UICONTROL 群組名稱]**，並新增與特定群組相關聯的機碼值組。 表單作者可在元件的「編輯」對話方塊中看到群組名稱。 如果您選取群組名稱，則每個關聯的索引鍵/值配對都適用於元件。
1. 按一下&#x200B;**[「完成」]**。

![正在範本編輯器中新增自訂屬性群組名稱](/help/forms/assets/custom-properties-core-component.png)

當您使用範本原則新增至少一個自訂屬性群組時，**[!UICONTROL 進階]**&#x200B;索引標籤會顯示在對應核心元件的「編輯」對話方塊中。

#### 在核心元件的編輯對話方塊中選取自訂群組名稱 {#select-a-custom-group-name}

1. 以編輯模式開啟最適化表單。
1. 選取已在範本編輯器中定義自訂屬性的元件，並選取![settings_icon](assets/configure-icon.svg)以開啟元件的編輯對話方塊。
1. 選取&#x200B;**[!UICONTROL 進階]**&#x200B;標籤。
1. 從&#x200B;**[!UICONTROL 自訂屬性選取]**&#x200B;下拉式清單中選取自訂屬性群組名稱。 下拉式清單會自動填入所有已定義的自訂群組名稱。
1. 選取&#x200B;**[!UICONTROL 完成]**&#x200B;以儲存屬性。

![選取自訂屬性群組名稱](/help/forms/assets/select-custom-properties-group-name.png)

>[!NOTE]
>
> * **[!UICONTROL 其他自訂屬性]**&#x200B;核取方塊可讓您在範本原則中提供的內容之外，動態新增元件特定的自訂屬性。 當索引鍵名稱值相符時，特定元件的自訂屬性會優先於範本原則所設定的自訂屬性。

## 使用範本建立最適化表單 {#creating-an-adaptive-form-using-the-template}

建立並啟用範本後，當您建立最適化表單時，可在表單管理員中使用範本。 若要使用範本並建立調適型表單，請參閱[根據核心元件建立調適型表單](/help/forms/creating-adaptive-form-core-components.md)。
<!--
## Change display option of out of the box templates  {#change-display-option-of-out-of-the-box-templates}

You can create custom templates for Adaptive Forms to define basic structure and initial content. [!DNL AEM Forms] also provides a set of out of the box template for Adaptive Forms. You can choose to show or hide the templates.

Perform the following steps to show and hide templates:

1. Log in to [!DNL AEM Forms] author instance and navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.

   >[!NOTE]
   >
   >The URL of AEM web console is https://'[server]:[port]'/system/console/configMgr

1. Locate and open the **FormsManager Configuration** settings:

    * To show or hide out of the box Adaptive Forms template, check or uncheck the **Include Out of the box AF and AD Templates** option.
    * To show or hide out of the box Adaptive Form templates that were added in AEM 6.0 Forms or AEM 6.1 Forms releases but are now deprecated, check or uncheck the **Include AEM 6.0 AF Templates** option. If this option is checked, and you want it to take effect, it requires the **Include Out of the box AF and AD Templates** configuration to be enabled.

1. Click **Save**. The display options for the out of the box templates are changed. 

## Save an Adaptive Form as a template {#saving-adaptive-form-as-template}

You can also save an Adaptive Form as a template for future use. To save a Adaptive Form as a template:

1. Select an Adaptive Form to save it as a template.
1. Click **[!UICONTROL Save as Template]**. A dialog box appears.
1. Specify **[!UICONTROL Title]** (mandatory field), **[!UICONTROL Location]** (mandatory field) and **[!UICONTROL Description]** (optional field) for the template. 
1. Click **[!UICONTROL Create]**.

   ![Save as Form as Template](/help/forms/assets/saveformastemplate.png)



>[!NOTE]
>
>To use the same container policy as of the source Adaptive Form, it is recommended to save the template in the same folder as of the source Adaptive Form. In case, the template is saved in any other folder, than the created template uses a default container policy.
-->

## 最佳做法 {#best-practices}

* 使用根據核心元件的元件建立範本，例如最適化表單文字、最適化表單容器等。 若要取得最適化Forms核心元件的資訊，[請按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)。
* 限制範本的數量，以符合網站上提供的根本不同的表單型別
* 為範本中使用的自訂元件提供必要的彈性和設定功能。

<!--
## See next

* [Create style or themes for your forms](using-themes-in-core-components.md)
* [Create an Adaptive Form (core components)](/help/forms/creating-adaptive-form-core-components.md)

-->

## 另請參閱 {#see-also}

{{see-also}}
* [為您的表單建立樣式或主題](using-themes-in-core-components.md)
* [建立最適化表單（核心元件）](/help/forms/creating-adaptive-form-core-components.md)

