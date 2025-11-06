---
title: 如何在最適化表單核心元件中建立可重複的面板？
description: 瞭解如何在最適化表單中建立一個或多個可重複的區段。
role: Developer, Developer, Admin, User
feature: Adaptive Forms, Core Components
exl-id: 02521bf3-83c1-40a0-8fe6-23af240727e9
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1258'
ht-degree: 8%

---

# 建立具有可重複區段的表單（核心元件） {#repeat-panel}


| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-forms-repeatable-sections.html?lang=en) |
| AEM as a Cloud Service  | 本文章 |

可重複區段是指可為相同資料的多個例項收集資訊而可重複或多次重複的表單部分。

例如，考慮一個用來收集有關個人工作經驗資訊的表單。您可能有一個可重複區段，用來擷取每項先前工作的詳細資訊。可重複區段通常包含公司名稱、職位、就業日期和工作職責等欄位。使用者可以新增可重複區段的多個實例，以輸入有關他們所做每項工作的資訊。

![重複性](/help/forms/assets/repeatable-adaptive-form-example.gif)

閱讀完本文章後，您將學會：

* 在最適化表單中建立可重複的區段
* 設定最適化表單元件的最小重複次數或最大重複次數
* 使用規則編輯器為可重複區段設定新增或刪除動作

您可以使用[面板](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel)、[摺疊式功能表](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html)、[水準索引標籤](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html)、[垂直索引標籤](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs)或[精靈](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html)元件，讓最適化表單的部分可重複。 您可以將子元件新增到這些元件中，以在表單中建立可重複的區段。


本檔案中的範例是以[面板](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel)元件為基礎。 您可以執行相同的步驟，讓[面板](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel)、[摺疊式功能表](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html)、[水準索引標籤](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html)、[垂直索引標籤](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs)或[精靈](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html)元件可重複。

## 新增或刪除表單中可重複的區段 {#add-or-delete-repeatable-section-in-panel-container}

若要在表單中重複面板或移除可重複面板，表單作者會使用按鈕元件來新增或移除面板的例項。 新增或刪除表單中可重複的區段（面板）：

* [讓面板容器可重複](#make-panel-container-repeatable)
* [新增可重複區段](#add-repeatable-section-using-instance-manager-via-scripts)
* [刪除重複區段](#delete-repeatable-section-using-instance-manager-via-scripts)

### 讓面板容器可重複 {#make-panel-container-repeatable}

![協助工具索引標籤](/help/forms/assets/repeat-panel.png)

若要讓面板可重複，請執行下列步驟：

1. 選取面板容器並選取![cmppr](/help/forms/assets/cmppr.png)。
1. 按一下&#x200B;**重複面板**，然後開啟切換開關以將&#x200B;**面板設為可重複**。
1. 設定&#x200B;**最小重複次數**&#x200B;為最小可重複區段的必要值，您可以將面板非重複的&#x200B;**最小重複次數**&#x200B;設為零，或移除重複的面板。 依預設，最小重複值為零。
1. 設定&#x200B;**最大重複次數**&#x200B;以重複所需的面板次數，預設值為無限。

   >[!NOTE]
   >
   > 
   > * 最小重複次數不能是 — ve值。
   > * 若要建立不可重複的面板，請將最大和最小欄位的值設為1。

### 使用執行個體管理員（透過指令碼）新增可重複區段 {#add-repeatable-section-using-instance-manager-via-scripts}

要重複的面板父項應包含新增按鈕以管理面板的重複例項。 執行以下步驟，將按鈕插入父項，並在按鈕上啟用指令碼：

1. 將&#x200B;**按鈕元件**&#x200B;新增至面板的父系。 在下列範例影片中，使用了標簽名稱為&#x200B;**Add**&#x200B;且欄位名稱為&#x200B;**AddPanel**&#x200B;的按鈕元件。 選取元件並選取![edit-rules](/help/forms/assets/edit-rules.png)。 按鈕元件的規則會在規則編輯器中開啟。
1. 在[規則編輯器]視窗中，按一下[建立]。**&#x200B;**。

   選取[表單物件與函式]列中的&#x200B;**視覺化編輯器**。

   1. 在規則區域的WHEN下，選取狀態&#x200B;**已按一下**。
   1. 在THEN底下，選取&#x200B;**新增執行個體**，並使用![切換側面板](/help/forms/assets/toggle-side-panel.png)拖放面板，或使用&#x200B;**拖放物件或選取這裡。**

   選取[表單物件與函式]列中的&#x200B;**程式碼編輯器**。 按一下&#x200B;**編輯規則**，然後在程式碼區域中：

   * 若要建立新增面板按鈕，請指定`this.panel.instanceManager.addInstance()`

   按一下&#x200B;**完成**。

>[!VIDEO](https://video.tv.adobe.com/v/3421052/adaptive-forms-repeatable-sections-repeat-sections/?quality=12&learn=on)


### 使用執行個體管理員（透過指令碼）刪除重複區段 {#delete-repeatable-section-using-instance-manager-via-scripts}

面板的父項應包含刪除按鈕，用於刪除可重複面板的例項。 執行以下步驟將按鈕插入父項，並在按鈕上啟用指令碼以刪除可重複的面板：

1. 將&#x200B;**按鈕元件**&#x200B;新增至面板的父系。在下面的影片中，使用標簽名稱為&#x200B;**delete**&#x200B;且欄位名稱為&#x200B;**DeletePanel**&#x200B;的按鈕元件。 選取元件並選取![edit-rules](/help/forms/assets/edit-rules.png)。 按鈕元件的規則會在規則編輯器中開啟。
1. 在[規則編輯器]視窗中，按一下[建立]。**&#x200B;**。

   選取[表單物件與函式]列中的&#x200B;**視覺化編輯器**。

   1. 在規則區域中，在WHEN **DeletePanel**&#x200B;下，選取狀態&#x200B;**被點選**。
   1. 在THEN底下，選取&#x200B;**移除執行個體**，並使用![切換側面板](/help/forms/assets/toggle-side-panel.png)拖放面板，或使用&#x200B;**拖放物件或選取這裡。**

   選取[表單物件與函式]列中的&#x200B;**程式碼編輯器**。 按一下&#x200B;**編輯規則**，然後在程式碼區域中：

   * 若要建立刪除面板按鈕，請指定`this.panel.instanceManager.removeInstance(this.panel.instanceIndex)`

   按一下&#x200B;**完成**。

>[!VIDEO](https://video.tv.adobe.com/v/3421620/adaptive-forms-repeatable-sections)

>[!NOTE]
>
>如果欄位屬於可重複面板，則無法在指令碼中使用其名稱直接存取它。 若要存取欄位，請在`instances`中使用`InstanceManager` API指定欄位所屬的可重複執行個體。 在`instances`中使用`InstanceManager` API的語法為：
>
>
>`<panelName>.instanceManager.instances[<instanceNumber>].<fieldname>`
>
>
>例如，您可以建立最適化表單，其可重複面板具有文字方塊。 當您使用三個可重複的文字方塊預填表單時，您需要以下的xml：
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

>[!NOTE]
>
> 從最適化表單中移除面板的所有執行個體時，若要新增已移除面板的執行個體，請使用_panelName語法來擷取面板的執行個體管理員，並使用執行個體管理員的addInstance API來新增已刪除的執行個體。 例如，&#39;_panelName.addInstance()&#39;。 它會新增已移除面板的例項。

## 使用表單範本中的重複子表單(XDP/XSD) {#using-repeating-subforms-from-form-template-xdp-xsd}

可重複子表單類似於最適化Forms中的可重複面板。 在AEM Forms Designer中，執行下列步驟以建立重複的子表單：

1. 在「階層」浮動視窗中，選取要重複的子表單的父子表單。
1. 在「物件」浮動視窗中，按一下「子表單」標籤，然後在「內容」清單中，選取「流程」。
1. 選取要重複的子表單。
1. 在「物件」浮動視窗中，按一下「子表單」標籤，然後在「內容」清單中選取「已定位」或「已流動」。
1. 按一下「繫結」標籤，並為每個資料專案選取「重複子表單」。
1. 若要指定最小重複次數，請選取「最小計數」，並在相關方塊中輸入數字。 如果此選項設為0，且資料合併時沒有為子表單中的物件提供資料，則轉譯表單時不會放置子表單。
1. 若要指定子表單重複次數的最大值，請選取「最大值」，並在相關方塊中輸入數字。 如果您未在「最大值」方塊中指定值，則子表單重複次數將無限制。
1. 若要指定一組子表單重複次數，而不考慮資料數量，請選取「初始計數」，並在相關方塊中輸入數字。 如果選取此選項，但無可用資料或資料專案少於指定的初始計數值，則表格上仍會放置子表格的空白執行個體。
1. 在父子表單中新增兩個按鈕 — 一個用於新增例項，另一個用於刪除可重複子表單的例項。 如需詳細步驟，請參閱[建置動作](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c74572b5612a87ca2b56-8000.2.html#WS107c29ade9134a2c-1f74d86012a87d4fe55-8000.2)。
1. 現在將表單範本連結至最適化表單。 如需詳細步驟，請參閱[根據範本建立最適化表單](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html?lang=en#create-an-adaptive-form-based-on-an-xfa-form-template)。
1. 使用在步驟9中建立的按鈕來新增和移除子表單。

附加的.zip檔案包含一個範例可重複的子表單。

[取得檔案](/help/forms/assets/samplerepeatablesubform.zip)

## 使用XML結構描述(XSD)的重複設定 {#using-repeat-settings-of-an-xml-schema-xsd-br}

您可以從XML結構描述以及任何複雜型別元素的minOccours &amp; maxOccurs屬性建立可重複的面板。 如需XML結構描述的詳細資訊，請參閱[使用XML結構描述作為表單模型建立最適化表單](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/adaptive-form-xml-schema-form-model.html)。

在下列程式碼中，`SampleType`面板使用minOccours &amp; maxOccurs屬性。

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


## 另請參閱 {#see-also}

{{see-also}}

<!--

>[!MORELIKETHIS]
>
>* [Create an Adaptive Form](creating-adaptive-form-core-components.md)
>* [Create style or themes for your forms](using-themes-in-core-components.md)
>* [Add dynamic behavior to forms using the rule editor](rule-editor.md)
>* [Set layout of forms for different screen sizes and device types](/help/sites-cloud/authoring/features/console-layout.md)

-->