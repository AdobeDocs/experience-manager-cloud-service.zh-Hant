---
title: 最適化Forms根據核心元件的版面配置功能為何？
description: Adaptive Forms在各種裝置上的版面配置與外觀是由版面配置設定所控制。 瞭解各種版面以及如何套用它們。
feature: Adaptive Forms, Core Components
keywords: 根據核心元件的調適型表單版面配置、表單的不同版面配置、動態表單版面配置AEM、AEM Cloud Service表單版面配置、AEM核心元件中的表單版面配置型別、調適型表單版面配置
role: User, Developer, Admin
exl-id: dcc01d84-0d39-4fa8-ac47-71a9aba91b1e
source-git-commit: ab84a96d0e206395063442457a61f274ad9bed23
workflow-type: tm+mt
source-wordcount: '2106'
ht-degree: 16%

---

# 根據核心元件的最適化Forms版面配置功能


| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/layout-capabilities-adaptive-forms.html) |
| AEM as a Cloud Service (基礎元件) | [按一下這裡](/help/forms/layout-capabilities-adaptive-forms.md) |
| AEM as a Cloud Service (核心元件) | 本文章 |

最適化Forms提供第一流的元件，讓您有效率地佈局和設計表單。 版面配置可控制元件在表單中的顯示方式。 最適化Forms支援各種版面：面板、精靈、摺疊式功能表、上/水準索引標籤上的索引標籤，以及左/垂直索引標籤上的索引標籤。

<!-- ![Types of Layout](/help/forms/assets/generic-layout-hero-image.png){align="center"}-->

## 必要條件

在探索版面的各種功能之前，請確定您的環境已啟用核心元件。 安裝最新的Far，為AEM Cloud Service環境啟用最適化Forms核心元件。

## 最適化Forms版面配置型別

根據核心元件的調適型表單支援下列版面型別：

* **面板配置**
* **精靈配置**
* **垂直配置**
* **水準配置**
* **收合式選單版面配置**

>[!BEGINTABS]

>[!TAB 面板版面]

面板版面對於組織相關欄位而言非常實用，可以更輕鬆地導覽和尋找相應內容。面板版面配置會將表單元件排列在最適化表單的不同區段或面板中。

![面板版面](/help/forms/assets/panel-layout.png)

面板版面

您可以使用[面板元件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel)在表單中新增面板版面。如需有關如何設定面板元件各種屬性的詳細說明，請參閱「[面板元件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel)」一文。

>[!TAB 精靈版面]

精靈配置將複雜表單分成不同的步驟，有助於簡化表單。 每個步驟代表流程的不同部分，使用者會依序瀏覽各個步驟，通常使用&#x200B;**下一個**&#x200B;和&#x200B;**上一個**&#x200B;按鈕。 您可以使用精靈版面來建立包含多個區段或步驟的表單。

![精靈版面](/help/forms/assets/wizard-layout-compare.gif)

精靈版面

您可以使用[精靈元件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard)在表單中新增精靈版面。如需有關如何設定精靈元件各種屬性的詳細說明，請參閱「[精靈元件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard)」一文。

>[!TAB 垂直索引標籤配置]

垂直標籤版面配置也稱為左側版面配置上的標籤。 垂直標籤版面配置會沿著表單左側組織面板或區段。 這是面板/區段垂直棧疊的表單的常見配置，可方便閱讀和導覽。

![垂直配置](/help/forms/assets/vertical-tab.gif)

垂直索引標籤配置

您可以使用[垂直分頁元件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs)，在表單中新增垂直分頁配置。 如需有關如何設定垂直標籤元件各種屬性的詳細指示，請參閱[垂直標籤元件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs)文章。


>[!TAB 水準標籤配置]

水準索引標籤版面配置也稱為頂端版面配置上的索引標籤。 水準標籤版面配置會將面板或區段並排排列成一列。 此版面配置以線性方式跨表單或面板寬度顯示表單區段。


![水準配置](/help/forms/assets/horizontal-layout.gif)

水準索引標籤配置

您可以使用[水準標籤元件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs)，在表單中新增水準標籤配置。 如需如何設定水準標籤元件各種屬性的詳細指示，請參閱[水準標籤元件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs)文章。


>[!TAB 摺疊式版面]

摺疊式版面以自適應表單中的可摺疊區段或面板來顯示內容。當某個區段展開時，會顯示其中的內容，而其他區段則保持摺疊狀態。這種版面非常適合以精簡的表單顯示大量資訊。

![摺疊式版面](/help/forms/assets/accordion-layout-compare.gif)

摺疊式版面

您可以使用[摺疊式元件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion)在表單中新增摺疊式版面。如需有關如何設定摺疊式元件各種屬性的詳細說明，請參閱「[摺疊式元件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion)」一文。

>[!ENDTABS]

若要瞭解如何插入版面並在其中新增表單元件，請參閱標題為[如何插入版面並在其中新增表單元件？](#how-to-insert-a-layout-and-add-form-components-to-it)

### 如何選擇正確的最適化表單版面配置？

請務必選擇正確的最適化表單版面配置，以最佳化使用者體驗和表單功能。 此表格可協助您瞭解可用的不同版面配置選項，並引導您根據特定需求和使用案例選取最適合的版面：

| 功能 | 面板版面 | 精靈版面 | 索引標籤在頂端/垂直索引標籤版面配置中 | 索引標籤在左側/水準索引標籤配置 | 摺疊式版面 |
|--------------------------|-----------------------------------------------------|----------------------------------------------------|-----------------------------------------------------|--------------------------------------------------------|--------|
| **用途** | 將相關的內容分組到不同的區段 | 引導使用者完成多步驟流程或表單 | 允許在同一頁面的區段/檢視之間切換 | 類似於頂端標籤，但垂直排列在左側 | 將內容組織為可摺疊的區段 |
| **結構** | 不同的區段 | 連續的步驟/頁面 | 頂端的水準索引標籤 | 左側垂直索引標籤 | 可摺疊的面板/區段 |
| **導覽** | 按一下面板標頭進行導覽 | - 往前：「下一步」按鈕<br>- 往回：「返回」按鈕<br>- 選擇性跳過步驟 | 按一下標籤以切換區段 | 按一下標籤以切換區段 | 按一下標頭可展開/摺疊區段 |
| **使用者體驗** | 以可管理的方式組織大量內容 | 逐步引導，減輕負荷 | 清晰、可存取的檢視間切換 | 有效率地使用垂直空間，永遠顯示標籤 | 使用展開/摺疊區段呈現精簡視圖 |
| **使用案例** | 具有分類區段的複雜表單 | 設定流程、複雜的表單 | 組織設定或內容類別 | 儀表板、複雜的資料檢視 | 常見問題集、設定選單、詳細的內容區段 |


## 如何插入版面並在其中新增表單元件？

下圖顯示將版面配置插入表單及新增表單元件的步驟：

![新增版面配置與表單元件的工作流程](/help/forms/assets/workflow-to-add-component-to-a-layout.png)

請考慮&#x200B;**最適化Forms配置型別**&#x200B;區段中顯示的[IT要求表單](#adaptive-forms-layout-types)。 此表單會收集員工因網路或筆記型電腦相關技術問題而得到的資訊。 它包含三個面板：

* **員工詳細資料**：面板會收集員工的相關資訊，並包含三個標示為「名稱」、「電子郵件ID」和「部門」的文字方塊。

* **問題詳細資料**：面板會擷取有關問題的詳細資料。 它包含問題類別的核取方塊，包含三個選項：「網路」、「電腦」或「其他」。 它也有兩個標示為「請指定和註解」的文字方塊。

* **附件**：面板可讓使用者上傳與問題相關的支援檔案。

讓我們來探索插入配置圖及新增元件的逐步程式。 在此範例中，水準分頁配置會插入至表單。

### 1.將版面配置元件插入表單

1. 登入您的[!DNL Experience Manager Forms]執行個體。
1. 在左上角，選取&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**。
1. 在編輯模式中開啟現有的自適應表單（如果已經建立）。

   ![開啟最適化表單](/help/forms/assets/insert-layout.png)

   或者，您也可以[建立新的最適化表單](/help/forms/creating-adaptive-form-core-components.md)。

1. 在表單產生器中找出可讓您新增版面的區段。

   ![表單產生器](/help/forms/assets/form-editor.png)
1. 按一下&#x200B;**新增**&#x200B;圖示。 圖示是加號(+)，表示可新增元件的選項。

   ![插入版面配置](/help/forms/assets/insert-layout-add-icon.png)

   按一下&#x200B;**新增**&#x200B;圖示會顯示&#x200B;**插入新元件**&#x200B;對話方塊，其中顯示要插入的各種元件。

   >[!NOTE]
   >
   > 或者，您也可以[拖放配置元件](#extra-bytes)。

1. 瀏覽對話方塊中的可用元件，並從清單中選取所需的版面。 在本例中，我們選取「水平定位點」元件來插入水平定位點版面配置。

   ![選取水準索引標籤](/help/forms/assets/select-horizontal-tab.png)

   將水準標籤元件新增至表單時，預設情況下它最初由兩個空白面板組成，名為Item1和Item2。 您必須手動將表單元件新增至這些面板。

   ![水準索引標籤](/help/forms/assets/insert-tabs-on-top.png)

1. 開啟水準標籤元件的屬性，並指定元件的名稱。
例如，在此案例中，我們將水平定位點元件的名稱新增為IT請求表單。

   ![新增水準索引標籤的名稱](/help/forms/assets/change-name-of-horizontal-tabs.png)

1. 按一下&#x200B;**完成**。

   ![水準索引標籤](/help/forms/assets/tabs-on-top-rename-component.png)

在表單中新增版面配置元件後，請根據需求修改面板數量。

### 2.將面板新增至版面

將面板新增至水準索引標籤元件：

1. 開啟水準標籤元件屬性，然後按一下&#x200B;**專案**&#x200B;標籤。

   水準索引標籤的![專案索引標籤](/help/forms/assets/tabs-on-top-items-tab.png)

1. 按一下「**新增**」圖示以新增面板。

   ![新增面板](/help/forms/assets/tabs-on-top-add-panel.png)

   當您按一下&#x200B;**新增**&#x200B;圖示時，**插入新元件**&#x200B;對話方塊就會顯示。

1. 選取面板元件。

   ![新增面板](/help/forms/assets/tabs-on-top-new-panel.png)

   當您選取面板元件時，新面板會新增至水準版面配置中。

   ![新增面板](/help/forms/assets/tabs-on-top-add-new-panel.png)

   提供新面板的名稱；否則，您無法儲存水準索引標籤元件的屬性。

1. 指定面板的名稱，如下圖所示：

   ![面板名稱](/help/forms/assets/tabs-on-tops-panel-name.png)

1. 按一下&#x200B;**完成**。

   按一下&#x200B;**完成**&#x200B;後，這三個面板會並排顯示。 面板名稱會顯示為每個面板的標題，而您可以將表單元件新增至每個面板。

   ![面板名稱](/help/forms/assets/tabs-on-top-initial-view.png)

   您可以設定面板元件的屬性。 例如，IT申請表單不包含面板標題，以下是設定面板元件屬性的步驟。

1. 開啟第一個面板的屬性。

   ![面板1屬性](/help/forms/assets/tabs-on-tops-panel1-properties.png)

1. 從&#x200B;**基本**&#x200B;索引標籤中選取&#x200B;**隱藏標題**&#x200B;核取方塊。

   ![隱藏標題](/help/forms/assets/tabs-on-top-hide-panel.png)

1. 按一下&#x200B;**完成**。

同樣地，您也可以隱藏其他兩個面板的標題。 完成後，您可以繼續將表單元件新增至每個面板。

### 3.將表單元件新增至面板

<!-- You can employ one of the following method to add form components to the panel:
* [Add components to a layout's panel using the Add icon](#add-components-to-a-layouts-panel-using-the-add-icon)
* [Drag and drop components into a layout's panel](#drag-and-drop-components-into-a-layouts-panel) -->

1. 在面板中找出可新增元件的區段。
1. 按一下&#x200B;**新增**圖示。 圖示是加號(+)，表示可新增元件的選項。
   ![插入版面配置](/help/forms/assets/tabs-on-top-add-component.png)

   按一下&#x200B;**新增**&#x200B;圖示會顯示&#x200B;**插入新元件**&#x200B;對話方塊，其中顯示要插入的各種元件。

   ![插入新元件對話方塊](/help/forms/assets/insert-new-component.png)

1. 瀏覽出現的對話方塊中的可用元件，並選取所需元件。 在本例中，請選取「文字方塊」元件。
1. 開啟新增元件的屬性並指定其名稱。 讓編輯新增的「文字方塊」元件的屬性，並指定其名稱。
   ![插入版面配置](/help/forms/assets/tabs-on-top-textbox-component.png)
1. 同樣地，新增兩個更多Text Box元件，且name已將元件新增為Email ID和Department。\
   ![第一個面板](/help/forms/assets/tabs-on-tops-first-panel.png)

   現在第一個面板中的元件已新增，您可以繼續將元件新增至第二個面板。

1. 若要切換面板，請按一下工具列中的&#x200B;**選取面板**。

   ![切換面板](/help/forms/assets/tabs-on-top-select-panel.png)

   當您按一下&#x200B;**選取面板**&#x200B;時，水準標籤元件中新增的面板清單就會顯示。

   ![切換面板](/help/forms/assets/tabs-on-tops-panel2.png)

1. 從面板清單中選取&#x200B;**2面板**，檢視就會從第一個面板變更為第二個面板。

   ![第二個面板](/help/forms/assets/tabs-on-top-panel2-component.png)

1. 重複步驟2至步驟4所述的步驟，在面板2中新增所需的元件，如下圖所示：

   ![第二個面板元件](/help/forms/assets/panel-2-components.png)

1. 依照步驟6和步驟7中概述的步驟，切換至&#x200B;**3面板**。

1. 重複步驟2至步驟4所述的步驟，在面板3中新增所需的元件：

   ![第三面板元件](/help/forms/assets/panel-3-component.png)

1. 按一下編寫環境右上角的&#x200B;**[!UICONTROL 預覽]**。
   ![水準配置](/help/forms/assets/horizontal-layout.gif)

您也可以[拖放元件](#extra-bytes)，將表單元件新增至每個面板。


<!-- #### Drag and drop components into a layout's panel 

1. Locate the section within the panel that allows you to add components. 
2. Navigate to the left panel within your authoring environment and click **Components**.

    ![Component Panel](/help/forms/assets/add-new-component.png){width="200" align="center"}

    When you click the **Components** option, the list of the available components appears.   

    ![Component Panel](/help/forms/assets/add-new-component2.png){width="200" align="center"}

3. Browse the available components and select the Text Box component.

4. Drag the component by clicking and holding the selected component, then drag it over to the panel area to place it.

5. Drop the component into the panel by releasing the mouse. 

6. Open the properties of the added Text Box component and specify its name as Name.
    ![Insert layout](/help/forms/assets/tabs-on-top-textbox-component.png){width="200" align="center"}
7. Similarly, add two more Text Box components and name added the components as Email ID and Department.   
    ![First Panel](/help/forms/assets/tabs-on-tops-first-panel.png){width="200" align="center"}

    Now that the components in the first panel have been added, you can proceed with adding the components to the second panel. 

8. To switch the panel, click **Select Panel** from the toolbar. 

    ![Switch Panel](/help/forms/assets/tabs-on-top-select-panel.png){width="200" align="center"}

    When you click the **Select Panel**, the list of the added panels in the Horizontal Tabs component appears.

    ![Switch Panel](/help/forms/assets/tabs-on-tops-panel2.png){width="200" align="center"}

9. Select **2 Panel** from the panel list and the view changes from the first panel to the second panel.

    ![Second Panel](/help/forms/assets/tabs-on-top-panel2-component.png){width="200" align="center"}

10. Repeat the steps outlined from Step 2 to Step 6 for adding the desired components in panel 2 as shown in the below figure:   

     ![Second Panel components](/help/forms/assets/panel-2-components.png){width="200" align="center"}

11. Switch to the **3 Panel** by following the steps outlined in Step 8 and Step 9.

12. Repeat the steps outlined from Step 2 to Step 6 for adding the desired component in panel 3:

    ![Third Panel components](/help/forms/assets/panel-3-component.png){width="200" align="center"} 

    -->



您也可以使用![刪除圖示](/help/forms/assets/Smock_Delete_18_N.svg)圖示從面板刪除表單元件。

![刪除元件](/help/forms/assets/delete-component.png)

您也可以視需要為元件新增必要的驗證。

## 如何以新版面配置取代現有版面？

您可以使用新的版面配置來取代表單的版面，其中涉及修改元件在表單中的排列和顯示方式。

執行以下步驟來取代現有的表單版面：

1. 按一下配置元件工具列上的「取代」圖示，就會顯示&#x200B;**[!UICONTROL 取代元件]**&#x200B;對話方塊。

   ![取代配置](/help/forms/assets/replace-layout.png)

1. 從&#x200B;**[!UICONTROL 取代元件]**&#x200B;對話方塊中選取所需的版面。

   ![取代元件對話方塊](/help/forms/assets/replace-component.png)

   選取配置圖後，配置圖中的元件排列會隨之變更。 例如，從&#x200B;**[!UICONTROL 取代元件]**&#x200B;對話方塊中選取垂直索引標籤元件；面板的排列會變更為左側的索引標籤：

   ![垂直配置](/help/forms/assets/vertical-tab.gif)

## 額外的位元組

若要將元件拖放至表單產生器，請執行下列步驟：

1. 找出可新增元件的區段。
1. 導覽至您編寫環境中的左側面板，然後按一下&#x200B;**元件**。

   ![元件面板](/help/forms/assets/add-new-component.png)

   當您按一下&#x200B;**元件**&#x200B;選項時，可用的元件清單就會顯示。

   ![元件面板](/help/forms/assets/add-new-component2.png)

1. 瀏覽可用的元件並選取所需的元件。

1. 按一下並按住選取的元件以拖曳元件，然後將其拖曳至面板區域以放置它。

1. 放開滑鼠，將元件拖放到面板中。

## 後續步驟

在您熟悉基於核心元件的調適型表單的各種版面配置功能後，便可繼續進行後續步驟：

* [根據核心元件建立第一個最適化表單](/help/forms/creating-adaptive-form-core-components.md)
* [建立及使用最適化表單主題](/help/forms/using-themes-in-core-components.md)



## 另請參閱

{{see-also}}
