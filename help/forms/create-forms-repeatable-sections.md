---
title: 最適化表單中的重複性（核心元件）
description: 使用面板元件的重複特性以最適化表單重複類似的區段。
role: Architect, Developer, Admin, User
source-git-commit: fcdb96a6bbe8ff8761293eedc0d38efaecb56037
workflow-type: tm+mt
source-wordcount: '1391'
ht-degree: 5%

---


# 建立具有可重複區段的表單（核心元件） {#repeat-panel}


| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-forms-repeatable-sections.html?lang=en) |
| AEM as a Cloud Service  | 本文 |

可重複區段是指表單的一部分，可重複或多次重複以收集相同資料的多個例項的資訊。

例如，考慮用來收集個人工作體驗相關資訊的表單。 您可以有可重複的區段來擷取先前每個工作的詳細資訊。 重複區段通常包含公司名稱、職稱、僱用日期和工作責任等欄位。 使用者可以新增多個可重複區段的執行個體，以輸入有關他們已進行的每個工作的資訊。

![重複性](/help/forms/assets/repeatable-adaptive-form-example.gif)

閱讀本文後，您將瞭解：

* 在最適化表單中建立可重複的區段
* 設定最適化表單元件的最小重複次數或最大重複次數
* 使用規則編輯器為可重複區段設定新增或刪除動作

您可以使用 [面板](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html)， [收合式選單](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html)， [水準標籤](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html)，或 [精靈](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html) 元件，使最適化表單的部分可重複。 您可以將子元件新增至面板、摺疊式功能表、水準標籤或精靈元件，以在表單中建立可重複的區段。


本檔案中的範例是根據 [面板](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html) 元件。 您可以執行相同的步驟，以使 [收合式選單](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html)， [水準索引標籤](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html)、和 [精靈](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html) 元件重複。

## 新增或刪除表單中的可重複區段 {#add-or-delete-repeatable-section-in-panel-container}

若要在表單中重複面板或移除可重複面板，表單作者會使用按鈕元件來新增或移除面板的例項。 若要新增或刪除表單中可重複的區段（面板）：

* [讓面板容器可重複](#make-panel-container-repeatable)
* [新增可重複區段](#add-repeatable-section-using-instance-manager-via-scripts)
* [刪除重複區段](#delete-repeatable-section-using-instance-manager-via-scripts)

### 讓面板容器可重複 {#make-panel-container-repeatable}

![協助工具索引標籤](/help/forms/assets/repeat-panel.png)

若要讓面板可重複，請執行下列步驟：
1. 選取面板容器並點選 ![cmppr](/help/forms/assets/cmppr.png).
1. 按一下 **重複面板** 並開啟切換至 **讓面板可重複**.
1. 設定 **最小重複次數** 根據最小可重複區段的要求，您可以設定 **最小重複次數** 如果面板未重複，則設為零，或移除重複的面板。 依預設，最小重複次數值為零。
1. 設定 **最大重複次數** 若要重複所需的面板次數，預設值為無限。

   >[!NOTE]
   >
   > 
   > * 最小重複次數不能是 — ve值。
   > * 若要建立不可重複的面板，請將最大和最小欄位的值設定為1。

### 使用執行個體管理員新增可重複區段（透過指令碼） {#add-repeatable-section-using-instance-manager-via-scripts}

要重複的面板父項應包含新增按鈕以管理面板的重複執行個體。 執行以下步驟，將按鈕插入父項並在按鈕上啟用指令碼：

1. 新增 **按鈕元件** 至面板的父系。 在以下範例影片中，按鈕元件帶有標簽名稱 **新增** 和欄位名稱 **新增面板**，則會使用。 選取元件並點選 ![edit-rules](/help/forms/assets/edit-rules.png). 按鈕元件的規則會在規則編輯器中開啟。
1. 在「規則編輯器」視窗中，按一下 **建立**.

   選取 **視覺化編輯器** 「表單物件與函式」列中的。

   1. 在規則區域的WHEN下，選取state **已點按**.
   1. 在THEN底下，選取 **新增例項**，並使用拖放面板 ![切換側面板](/help/forms/assets/toggle-side-panel.png) 或使用以下方式選取它： **拖放物件或在這裡選取。**

   選取 **代碼編輯器** 「表單物件與函式」列中的。 按一下 **編輯規則** 在程式碼區域中：

   * 若要建立新增面板按鈕，請指定 `this.panel.instanceManager.addInstance()`

   按一下&#x200B;**「完成」**。

>[!VIDEO](https://video.tv.adobe.com/v/3421052/adaptive-forms-repeatable-sections-repeat-sections/?quality=12&learn=on)


### 使用例項管理器（透過指令碼）刪除可重複的區段 {#delete-repeatable-section-using-instance-manager-via-scripts}

面板的父項應包含刪除按鈕，以刪除可重複面板的例項。 執行以下步驟，將按鈕插入父項，並在按鈕上啟用指令碼以刪除可重複的面板：

1. 新增 **按鈕元件** 至面板的父系，在底下的影片中，帶標簽名稱的按鈕元件 **刪除** 和欄位名稱 **DeletePanel** 已使用。 選取元件並點選 ![edit-rules](/help/forms/assets/edit-rules.png). 按鈕元件的規則會在規則編輯器中開啟。
1. 在「規則編輯器」視窗中，按一下 **建立**.

   選取 **視覺化編輯器** 「表單物件與函式」列中的。

   1. 在規則區域中，在WHEN底下 **DeletePanel**，選取狀態 **已點按**.
   1. 在THEN底下，選取 **移除例項**，並使用拖放面板 ![切換側面板](/help/forms/assets/toggle-side-panel.png) 或使用以下方式選取它： **拖放物件或在這裡選取。**

   選取 **代碼編輯器** 「表單物件與函式」列中的。 按一下 **編輯規則** 在程式碼區域中：

   * 若要建立刪除面板按鈕，請指定 `this.panel.instanceManager.removeInstance(this.panel.instanceIndex)`

   按一下&#x200B;**「完成」**。
>[!VIDEO](https://video.tv.adobe.com/v/3421620/adaptive-forms-repeatable-sections)

>[!NOTE]
>
>如果欄位屬於可重複面板，則無法在指令碼中直接使用其名稱來存取它。 若要存取欄位，請使用 `instances` 中的API `InstanceManager`. 使用的語法 `instances` 中的API `InstanceManager` 為：
>
>
>`<panelName>.instanceManager.instances[<instanceNumber>].<fieldname>`
>
>
>例如，您可以建立最適化表單，其可重複面板具有文字方塊。 當您使用三個可重複的文字方塊預先填入表單時，您需要下列xml：
>
>
>`<panel1><textbox1>AA1</panel1></textbox1>`
>
>
>`<panel1><textbox1>AA2</panel1></textbox1>`
>
>
>`<panel1><textbox1>AA3</panel1></textbox1>`
>
>
>若要讀取AA1資料，請指定：
>
>
>`Panel1.instanceManager.instances[0].textbox.value`
>
>
>若要讀取AA2資料，請指定：
>
>
>`Panel1.instanceManager.instances[1].textbox.value`
>
>
>

<!-- 
>For more information, see: Class: InstanceManager#instances in [AEM Forms Java API reference](https://adobe.com/go/learn_aemforms_documentation_63).      
-->

>[!NOTE]
>
> 從最適化表單中移除面板的所有執行個體時，若要新增已移除面板的執行個體，請使用_panelName語法來擷取面板的執行個體管理員，並使用執行個體管理員的addInstance API來新增已刪除的執行個體。 例如，_panelName.addInstance()。 它會新增已移除面板的例項。

<!--
![panel-repeatability-video](/help/adaptive-forms/assets/panel-repeatability-video.mp4)
-->

<!--

## Using the accordion layout for the parent panel &nbsp; {#using-the-accordion-layout-for-the-parent-panel-nbsp}

A panel has various layouts options. The Layout for accordian design option has out of the box support for repeatable panels. Perform the following steps to repeatable panel with Layout for accordian design option:

1. On the parent of panel to be repeated, tap ![cmppr](assets/cmppr.png). You can see the properties in the sidebar. In the **Layout** drop-down, select **Accordion**.
1. On a panel, which is to be repeated, tap ![cmppr](assets/cmppr.png). You can see the panel properties in the sidebar. Enable the **Make Panel Repeatable** tab, and specify value for the **Maximum** and **Minimum** fields.

   Now, you can use the plus (+) and delete ( ![delete-panel](assets/delete-panel.png)) buttons to add and remove the panels.

-->

## 使用表單範本中的重複子表單(XDP/XSD) {#using-repeating-subforms-from-form-template-xdp-xsd}

可重複子表單類似於最適化Forms中的可重複面板。 在AEM Forms Designer中，執行下列步驟以建立重複的子表單：

1. 在「階層」浮動視窗中，選取要重複的子表單的父子表單。
1. 在「物件」浮動視窗中，按一下「子表單」標籤，然後在「內容」清單中，選取「流程」。
1. 選取要重複的子表單。
1. 在「物件」浮動視窗中，按一下「子表單」標籤，然後在「內容」清單中選取「位置」或「流量」。
1. 按一下「繫結」標籤，並為每個資料專案選取「重複子表單」。
1. 若要指定最小重複次數，請選取「最小計數」，並在相關方塊中輸入數字。 如果此選項設為0，且資料合併時未提供子表單中物件的資料，則轉譯表單時不會放置子表單。
1. 若要指定子表單重複次數上限，請選取「最大值」，並在相關方塊中輸入數字。 如果您未在「最大值」方塊中指定值，則子表單重複次數為無限制。
1. 若要指定一組子表單重複次數，而不考慮資料數量，請選取「初始計數」，並在相關方塊中輸入數字。 如果選取此選項，但無可用資料或資料專案少於指定的「初始計數」值，則表格上仍會放置子表格的空白例項。
1. 在父子表單中新增兩個按鈕 — 一個用於新增例項，另一個用於刪除可重複子表單的例項。 如需詳細步驟，請參閱 [建置動作](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c74572b5612a87ca2b56-8000.2.html#WS107c29ade9134a2c-1f74d86012a87d4fe55-8000.2).
1. 現在，將表單範本連結至最適化表單。 如需詳細步驟，請參閱 [根據範本建立最適化表單](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html?lang=en#create-an-adaptive-form-based-on-an-xfa-form-template).
1. 使用步驟9中建立的按鈕來新增和移除子表單。

附加的.zip檔案包含一個範例可重複的子表單。

[取得檔案](/help/forms/assets/samplerepeatablesubform.zip)

## 使用XML結構描述(XSD)的重複設定 {#using-repeat-settings-of-an-xml-schema-xsd-br}

您可以從XML結構描述以及任何複雜型別元素的minOccours &amp; maxOccurs屬性建立可重複的面板。 如需「XML綱要」的詳細資訊，請參閱 [使用XML結構描述作為表單模型建立調適型表單](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/adaptive-form-xml-schema-form-model.html).

在以下程式碼中， `SampleType`面板使用minOccours &amp; maxOccurs屬性。

```xml
<?xml version="1.0" encoding="utf-8" ?>
    <xs:schema targetNamespace="https://adobe.com/sample.xsd"
                    xmlns="https://adobe.com/sample.xsd"
                    xmlns:xs="https://www.w3.org/2001/XMLSchema"
                >

        <xs:element name="sample" type="SampleType"/>

        <xs:complexType name="SampleType">
            <xs:sequence>
                <xs:element name="leaderName" type="xs:string" default="Enter Name"/>
                <xs:element name="assignmentStartDate" type="xs:date"/>
                <xs:element name="gender" type="GenderEnum"/>
                <xs:element name="noOfProjectsAssigned" type="IntType"/>
                <xs:element name="assignmentDetails" type="AssignmentDetails"
                                            minOccurs="0" maxOccurs="10"/>
            </xs:sequence>
        </xs:complexType>

        <xs:complexType name="AssignmentDetails">
            <xs:attribute name="name" type="xs:string" use="required"/>
            <xs:attribute name="durationOfAssignment" type="xs:unsignedInt" use="required"/>
            <xs:attribute name="numberOfMentees" type="xs:unsignedInt" use="required"/>
             <xs:attribute name="descriptionOfAssignment" type="xs:string" use="required"/>
             <xs:attribute name="financeRelatedProject" type="xs:boolean"/>
       </xs:complexType>
  <xs:simpleType name="IntType">
            <xs:restriction base="xs:int">
            </xs:restriction>
        </xs:simpleType>
  <xs:simpleType name="GenderEnum">
            <xs:restriction base="xs:string">
                <xs:enumeration value="Female"/>
                <xs:enumeration value="Male"/>
            </xs:restriction>
        </xs:simpleType>
    </xs:schema>
```


## 相關文章

* [建立最適化表單](creating-adaptive-form-core-components.md)
* [為您的表單建立樣式或主題](using-themes-in-core-components.md)
* [使用規則編輯器將動態行為新增至表單](rule-editor.md)
* [設定不同熒幕大小和裝置型別的表單版面](/help/sites-cloud/authoring/features/responsive-layout.md)