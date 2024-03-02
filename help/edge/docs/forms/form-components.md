---
title: 表單元件和屬性
description: 本檔案概述AEM Forms Edge Delivery Service中可用的表單元件及其屬性。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: d0c4f2f880ef7c11b11144502d30430336ac682e
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 5%

---


# 表單元件和屬性的開發人員指南：AEM Forms Edge Delivery Service

AEM Forms Edge Delivery Service可讓您使用各種元件建立好記且互動式的表單。 這些元件適用於不同型別的資料收集，並可輕鬆自訂以符合您的特定需求。

![包含某些元件和屬性的試算表範例](/help/edge/assets/sample-form-in-spreadsheet.png)

最適化表單區塊產生 [統一的HTML結構](/help/edge/docs/forms/style-theme-forms.md) 用於所有欄位型別和容器（面板），確保一致性。 此一致的結構可讓您更容易 [設定表單樣式](/help/edge/docs/forms/style-theme-forms.md).

## 可用元件

以下是可用元件的概觀：

### 輸入欄位

- 所有有效HTML5 [輸入型別](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types) 和 [文字區域](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea). 例如，按鈕、核取方塊、顏色、日期、日期時間 — 本機、電子郵件、檔案、隱藏、影像、月份、數字、密碼、無線電、範圍、重設、提交、電話、文字、時間、url和周。

### 選取範圍控制項

- [核取方塊群組](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox)：用於選取多個選項。
- [選項按鈕群組](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/radio)：用於從群組選取單一選項。
- [下拉式功能表](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select)：顯示選項功能表。 例如，下拉式方塊。

### 容器

- 面板/容器：將相關的表單元素分組在一起，以提升組織效能。 這是以下專案的組合： [欄位集](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset) 和 [圖例](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/legend).




## 元件屬性

每個表單元件都隨附各種屬性，可讓您控制其行為和外觀。 最適化表單元件支援的屬性如下：


| 屬性 | 適用的元件 | 詳細資料 |
|--------------|------------------------------|----------------------------------------------------------------------|
| 類型 | 全部 | 指定元件的型別。 此屬性決定輸入欄位的行為和外觀。 例如，對於文字輸入，型別可以是「text」、「email」用於電子郵件輸入、「password」用於密碼輸入。 最適化表單區塊支援  <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types">所有有效的HTML5輸入型別</a>， <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea">文字區域</a>， <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">選取</a>、和 <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">欄位集</a> 作為型別。 |
| 名稱 | 全部 | 識別表單提交的元件。 將表單資料提交至伺服器時，會使用name屬性，將使用者輸入與特定欄位建立關聯。 |
| 標籤 | 全部 | 為使用者提供內容相關資訊。 標籤是元件旁邊顯示的文字，提供使用者要輸入哪些資訊的指引。 |
| 值 | 文字，密碼，電子郵件，數字，範圍，日期及其變體（日期時間 — 當地，月，周，時間），核取方塊，單選，隱藏，提交，按鈕 | 指定元件的初始值。 對於文字輸入、文字區域和選取元素，這是顯示的預設文字或選項。 對於選項和核取方塊元件，這是選取時提交的值/資料。 value屬性是選用專案，但核取方塊和選項輸入應視為必要專案。 |
| 預留位置 | 文字、電話、電子郵件、密碼、日期（及其變體，例如月、周、時間、日期時間 — 本機）、數字、範圍 | 提供預期輸入的提示。 預留位置屬性提供簡短的提示，說明輸入欄位的預期值。 當使用者開始輸入時，它就會消失。 |
| 說明 | 全部 | 提供有關元件的其他資訊，並作為說明文字。 說明欄位可進一步說明填寫元件的用途或指示。 它可協助使用者瞭解輸入欄位的內容。 |
| 可見 | 全部 | 控制初始可見性。 visible屬性是布林屬性，可決定表單載入時，元件最初是可見還是隱藏。 若設為true，會顯示欄位；否則會隱藏欄位。 |
| 必要 | 文字、電話、電子郵件、密碼、日期及其變體（日期時間 — 當地、月、周、時間）、數字、核取方塊、無線電、檔案、選取（下拉式清單）、文字區域 | 指示在提交之前是否必須填寫欄位。 強制屬性是布林屬性，用於指定使用者在提交表單之前是否必須為欄位提供輸入。 |
| 分鐘 | 日期（及其變數，例如月、周、時間、日期時間 — 本機）、數字、範圍 | 指定允許的最小值。 min屬性會設定使用者可輸入欄位的最小值。 例如，對於數字輸入，它定義了可接受的最低數字。 |
| 最大值 | 日期（及其變數，例如月、周、時間、日期時間 — 本機）、數字、範圍 | 指定允許的最大值。 最大屬性可設定使用者可輸入欄位的最大值。 例如，日期輸入會定義可接受的最高日期。 |
| 接受 | 檔案 | 定義允許的檔案型別。 accept屬性是以逗號分隔的不重複檔案型別說明符清單，可限制使用者可在檔案輸入欄位中選取的檔案型別。 |
| 多個 | 檔案 | 允許多重選取。 multiple attribute是與檔案輸入欄位搭配使用的布林屬性。 若設為true，可讓使用者選取多個檔案。 |
| 選項 | 下拉式清單 | 指定下拉式功能表的選項。 options屬性是下拉式功能表的逗號分隔選項清單，用於定義向使用者顯示的可選選項。 |
| 已核取 | 核取方塊，單選按鈕 | 決定預設是否選取欄位。 checked屬性是搭配核取方塊和選項輸入使用的布林屬性。 若設為true，表示載入表單時，預設會選取欄位。 |
| 欄位集 | 全部 | 將欄位分組，以在表單中建立視覺上不同的區段。 欄位集元素會將表單中的相關欄位分組，並以視覺化方式加以區隔，以改善組織和使用者體驗。 </br> 若要在欄位集中組織一組欄位，只需使用 `fieldset` 屬性並指定其名稱屬性。 在以下範例中，我們會示範如何將選項按鈕封裝在單一欄位集中，以提升組織效能。 ![欄位集範例](/help/edge/assets/fieldset-example.png) |



<!--

## Supported HTML 5 input types in Adaptive Form Block

The Adaptive Form Block supports a range of HTML 5 input types, and it also seamlessly renders forms created with AEM core components.
Here is the table which outlines how core components correspond to their HTML-5 input types in Edge Delivery:
<table>
 <tbody>
  <tr>
   <td><b>Core Components</b> </td>
   <td><b>HTML 5 input type</b> </td>
   <td><b>Details</b></td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/form-container.html">Form Container</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#form">form </td>
   <td> Create a form to capture user inputs.
   </td>
  </tr>
  <tr>
   <td><a herf="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/text-input.html">Text Input</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/text">text</a></td>
   <td> Defines a single-line text input field. </td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/number-input.html">Number Input</a></td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/number">number</a></td>
   <td>Lets user  enter a number input. You can also add built-in validation to reject non-numerical inputs. Lets user  enter a number input. You can also add built-in validation to reject non-numerical inputs. Initially, the input field is displayed as a number input. If a user applies a display pattern, it changes to text to allow the author to apply number formatting, since HTML 5 lacks support for display patterns. However, when the user clicks it, it returns to typing numbers.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/date-picker.html">Date Picker</a></td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/date">date </a></td>
   <td> Create an input field for entering a date. You have the option to input the date either through a text box, which validates the entry, or through a dedicated date picker interface. Initially, the native date input field is displayed. If a user applies a display pattern, it changes to text to allow the user to apply formatting, since HTML 5 lacks support for display patterns. However, when the user clicks it, it returns to typing a date.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment.html">File Attachment</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/file">file</a></td>
   <td> Allows user to choose one or more files from the device storage. It supports enhanced file input validations, such as accepted file types, file size restrictions, and minimum/maximum file selection limits. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/drop-down.html"> Dropdown List</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">select</a></td>
   <td> Allows users to select one or more options from a list of predefined options. The options can be of type String, Number, or Boolean.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox-group.html">Checkbox Group</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox">multiple checkbox</a></td>
   <td> Allow users to select one or more options from a list. Multiple checkboxes are generated with identical names, each corresponding to an item in the enum. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/radio-button.html">Radio Button Group</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/radio">multiple radio</a></td>
   <td> Allows a user to select one option from a group of related options. Multiple radio buttons are generated with identical names, each corresponding to an item in the enum.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/button.html">Button</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/button">button</a></td>
   <td>A UI element that allows users to trigger an action when clicked. </td>
  </tr>
  <tr>
   <td><a href =""https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html">Panel</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset with legend</a></td>
   <td> Group sections within a form, where a nested *legend* element adds a caption for the form.</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html">Wizard</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset</a></td>
   <td>Groups related sections within a form. It also controls the arrangement, supporting display options for positioning them at the top or at the left side. </td>
  </tr>
    <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/text.html">Text</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/p">p</a></td>
   <td>A p tag marks a paragraph. In visual content, paragraphs are chunks of text separated by blank lines or an indented first line</td>
  </tr>
     <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/submit-button.html">Submit button</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/submit">submit</a></td>
   <td> A UI element that enables users to submit a form to the server upon clicking. If a user adds a submit rule to a button, it functions as the submit button. </td>
  </tr>
     <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/reset-button.html">Reset button</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/reset">reset</a></td>
   <td>A UI element that resets a form upon clicking. If a user adds a reset rule to a button, it functions as the reset button. </td>
  </tr>
    <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/email-input.html">Email Input</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/email">email</a></td>
   <td> Allows the user to enter and edit an email address. If the user adds the multiple attributes, a list of email addresses can be added or edited.</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/telephone-input.html">Telephone Input</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/tel">tel</a></td>
   <td>Allows user to enter and edit a telephone number.</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/header.html">Header</td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/header"> header</a></td>
   <td>It includes introductory content, typically a group of introductory or navigational aids. It is supported outside Form container. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/footer.html">Footer</td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/footer">footer</a></td>
   <td> Contains information such as copyright data or links to related documents. It is supported outside Form container.</td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html">Accordion<a></td>
   <td><i>Not yet supported in Adaptive Form Block</i></td>
   <td> Allows user to create expandable and collapsible sections in a form. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html">Horizontal tabs</a></td>
   <td><i>Not yet supported in Adaptive Form Block</i></td>
   <td>Organizes multiple sections of a form into separate tabs which are displayed horizontally.</td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/image.html">Image</a></td>
   <td><i>Not yet supported in Adaptive Form Block</i></td>
   <td> Allows user to include images in a form.</td>
  </tr><tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/title.html">Title</a></td>
   <td><i>Not yet supported in Adaptive Form Block</i></td>
   <td> Refers to the text that appears at the top of the form. </td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/submit-button.html">Switch</td>
   <td><i>Not yet supported in Adaptive Form Block</i></td>
   <td> A two-state toggle that allows user to select between two states such as enabling or disabling a feature, setting, or functionality.</td>
  </tr>
 </tbody>
</table> -->

## 了解更多

- [建立並預覽表單](/help/edge/docs/forms/create-forms.md)
- [啟用表單來傳送資料](/help/edge/docs/forms/submit-forms.md)
- [將表單發佈到網站頁面](/help/edge/docs/forms/publish-eds-forms.md)
- [新增驗證至表單欄位](/help/edge/docs/forms/validate-forms.md)
- [改變主題和樣式風格](/help/edge/docs/forms/style-theme-forms.md)
