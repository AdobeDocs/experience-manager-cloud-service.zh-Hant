---
title: AEM FormsEdge Delivery Services概觀
description: AEM FormsEdge Delivery Services專為最佳效能而打造，可讓您構想簡化資料收集和使用者參與的未來。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
source-git-commit: d91254b52c257a3758da200a2c74b736ca457884
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 0%

---

# AEM FormsEdge Delivery Services

AEM Forms Edge Delivery Services是一組可撰寫的服務，可啟用快速的開發環境，讓作者可以快速更新、發佈和啟動新表單。 這些服務提供卓越且高影響力的表單體驗，可促進參與和轉換。 這些表單體驗易於編寫和開發。


這些服務可讓您：

* **使用您選擇的工具建立註冊體驗：** 透過分離內容來源來提高撰寫效率。 開箱即用地使用檔案式編寫(Microsoft SharePoint或Google Drive)和AEM編寫(最適化Forms編輯器)。 您可以在相同的表單網站上使用多個內容來源，並使用您偏好的編寫工具，例如Microsoft Excel、Google Sheets或Adaptive Forms Editor。

* **提供卓越的數位註冊體驗：** 提供可快速載入及轉譯的數位註冊體驗。 載入時間更快，使用者體驗最佳化，有助於提高表單完成率和轉換率。

* **使用開發人員友善的工具集：** AEM Forms使用純HTML、現代化CSS和vanilla JavaScript來建立卓越的體驗，避免特定架構的陡峭學習曲線。 具備基本Web開發技能的開發人員可以自訂並輕鬆建置表單元件和體驗。 您不需要等候管道執行，只要將您的程式碼簽入Github中，您的變更即時。

## AEM FormsEdge Delivery Services概觀 {#edge-overview}

下圖說明如何在Microsoft Excel或Google Sheets （檔案式製作）中編輯表單及發佈至Edge Delivery Services。 它也會顯示使用最適化Forms編輯器(AEM製作)的AEM發佈方法。

![Edge Delivery 架構](/help/edge/assets/AEM-forms-with-EDS-publishing.png)

AEM Forms Edge Delivery Services是一組可撰寫的服務，可讓您在網站上撰寫表單時擁有高度彈性。 您可以使用兩種AEM內容管理 [AEM製作](/help/forms/creating-adaptive-form-core-components.md) 以及 [檔案式製作](/help/edge/docs/forms/create-forms.md).

例如，您直接在Microsoft Excel或Google工作表中編寫表單，而這些試算表會轉換為您網站的表單。 任何新表單或表單內容（例如新表單欄位）都可立即在您的網站上使用，而無需重新建置流程。

AEM FormsEdge Delivery Services使用GitHub，因此客戶可以直接從其GitHub存放庫管理和部署程式碼。 例如，您可以用下列方式撰寫表單： [Google Sheets或Microsoft Excel](/help/edge/docs/forms/create-forms.md) 且可在GitHub中使用CSS和JavaScript來開發表單的元件。

準備就緒後，您可以使用 [AEM Sidekick](/help/edge/docs/forms/tutorial.md#preview-and-publish-your-content)，一種chrome瀏覽器擴充功能，可預覽和發佈內容更新。

![安裝AEM Sidekick](/help/edge/assets/install-aem-sidekick.png)

AEM FormsEdge Delivery Services提供forms區塊，稱為 [最適化Forms區塊](/help/edge/docs/forms/create-forms.md) 以新增表單至您的Edge Delivery Services網站。

選擇 [檔案式製作](#document-based-authoring-features) 和 [AEM製作](#aem-authoring-features) 取決於您的特定需求。

對於只收集基本資訊的簡單表單，例如姓名和電子郵件（可以考慮聯絡我們表單、潛在客戶產生表單或服務請求表單），以及您只需要將資料移至試算表的地方， [檔案式製作](/help/edge/docs/forms/create-forms.md) 非常適合。 您可以建置這些表單，就像在Google Sheets或Microsoft Excel中建置檔案一樣。

如果您的表單變得更複雜，例如需要多個面板、複雜規則和商業邏輯、資料操控、與外部系統整合，或使用AEM功能簡化工作流程，則 [AEM製作](/help/forms/creating-adaptive-form-core-components.md) 是更好的選擇。


### 檔案式撰寫和AEM撰寫的主要功能

檔案式撰寫提供一組基本功能，AEM撰寫開啟了檔案式撰寫以外的其他功能，讓您能夠建立更複雜且互動式的表單。 Document-based Authoring和AEM Authoring的主要功能包括：

<!-- 

>[!BEGINTABS]

>[!TAB Document-based Authoring ]

Document-based Authoring  is a versatile option suitable for creating simple forms with essential functionalities. It allows you to integrate various input types like text fields, dropdown menus, and radio buttons, enabling you to collect user data effectively. It offers a basic version of rules to add dynamic behaviour to forms. Key features of Document-based Authoring  are: 

* **[HTML5-based Form Field components](/help/edge/docs/forms/form-components.md)**: AEM Forms Edge Delivery Services allow you to create user-friendly and interactive forms using form components based on HTML5 [input types](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types), <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea">textarea</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">select</a>, and <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset</a>  elements. These components cater to different types of data collection and can be easily customized to fit your specific needs.  

* **Accessibility**: The fields in the form block are accessible. Each label is linked with its respective input element, and IDs are auto-generated for linking. Descriptions associated with fields are linked via the aria-describedby attribute. Keyboard navigation using the standard Tab/Shift + Tab keys is supported.

* **[Styling](/help/edge/docs/forms/style-theme-forms.md)**: Each form field has a fixed HTML structure that can be easily decorated using custom CSS or JavaScript files. Selectors for targeting fields in CSS and JS are provided based on type and name. You can easily create new selectors due to the standradized structure and style your form. 

* **Basic Rules**: Easily create logic that adjusts field visibility, validation, and behavior based on user input or predefined conditions. Rules offer a flexible and intuitive way to add intelligence to your forms, ensuring they adapt seamlessly based on user inputs.

* **Validations**: Before submission, the form is validated, and invalid fields are appropriately marked with error messages displayed to the user. Adaptive Forms Block support all the HTML form validation, supported by modern browsers, and provide additional validation mechanism like validation script, file size, file type, overall file size, and more. 

* **File Uploads**: You can add file attachment capabilities to your forms. Whether you need to gather documents, images, or other files from your users, file upload functionality serves you effortlessly. With custom handling options available, you can tailor the file upload process to suit your specific requirements.

* **reCAPTCHA**: Benefit from seamless integration of Google reCAPTCHA into your forms with our out-of-the-box (OOTB) support. Safeguard your forms against fraudulent activities, spam, and abuse, while maintaining a smooth and uninterrupted user experience. Adaptive Forms Block supports reCaptcha V3 and reCaptcha Enterprise. 

* **Send email notification on form submission**: Eliminate the hassle of manual follow-ups and ensure timely communication with our built-in email automation for form submissions. This integrated solution lets you effortlessly notify relevant parties, including sending form data, whenever someone fills out a form on your website. No need for complex configurations or additional tools – it's ready to use out of the box.

>[!TAB AEM Authoring]

AEM Authoring unlocks additional capabilities beyond the Document-based Authoring , empowering you to build more complex and interactive forms. In additon to the features of Document-based Authoring , AEM authoring offers the following additional features:  

* Advanced Rules: Define logic-based actions within your forms. You can use rules to conditionally show or hide form sections, pre-populate fields based on user input, and perform various validations to ensure data integrity.

* Server-side extensibility: Extend the functionalities of your forms by integrating them with server-side logic. This allows you to perform complex calculations, interact with external systems, and automate specific tasks based on user actions within the form.
* Streamline workflows and data management: Leverage the power of AEM to:
    * Design user-friendly forms using AEM editors.
    * Generate a "Document of Record" for secure and tamper-proof archiving of submitted data.
    * Facilitate e-signing with Adobe Sign for a smooth and secure signing experience.
    * Automate business processes through AEM workflows, triggering actions based on form submissions.
    * Effortlessly integrate with various data sources, enabling seamless data flow and exchange.

>[!ENDTABS]



## Start creating forms

-->

#### 檔案式撰寫功能

檔案式製作可讓您使用熟悉的工具(例如Microsoft Excel或Google Sheets)來建立表單。 這些表單提供下列功能：

* 無障礙元件，提供使用者易用的體驗。
* 標準化HTML結構以一致呈現。
* 規則和驗證以確保資料的準確性。
* 用於收集其他資訊的檔案附件選項。
* Google reCAPTCHA整合可保護垃圾郵件。
* 可針對特定需求建立自訂表單元件。
* 直接將表單資料提交至Microsoft Excel或Google工作表或電子郵件地址。

#### AEM編寫功能

AEM Authoring提供用於建立表單的WYSIWYG介面(最適化Forms編輯器)，並提供檔案式製作的所有功能，以及各種其他功能：

* 用於建立複雜邏輯的進階規則編輯器。
* 自訂功能的伺服器端擴充性。
* 所見即所得編輯體驗，可輕鬆建立表單和視覺化。
* 記錄檔案功能，可針對提交的資料建立防竄改封存。
* 與Adobe Sign整合以提供電子簽章。
* 與Adobe Workfront Fusion整合，在提交表單時觸發Adobe Workfront Fusion案例。
* 與各種資料來源整合，用於預先填入表單和提交資料。
* 表單資料模型，用於定義資料結構以及與各種資料來源的互動。
* 能夠設定多個提交動作以處理表單提交，包括提交資料至Microsoft SharePoint、Microsoft OneDrive、Adobe Workfront Fusion、Salesforce、Microsoft Dynamics以及其他許多資料來源。

本質上，AEM Authoring是以Document-based Authoring為基礎，提供更進階的工具組來建立和管理複雜的表單。

### 編寫工作流程

![檔案式製作 ](/help/edge/assets/document-based-authoring-workflow.png)

![AEM製作](/help/edge/assets/aem-authoring-workflow.png)


## 開始建立表單

* [開始使用AEM FormsEdge Delivery Services](/help/edge/docs/forms/tutorial.md)
* [使用Google工作表或Microsoft Excel建立表單](/help/edge/docs/forms/create-forms.md)
* [設定Google工作表或Microsoft Excel檔案以開始接受資料&#x200B;。](/help/edge/docs/forms/submit-forms.md)
* [發佈您的表單並開始收集資料](/help/edge/docs/forms/publish-forms.md)
* [自訂表單的外觀&#x200B;](/help/edge/docs/forms/style-theme-forms.md)
* [將可重複的區段新增至表單&#x200B;。](/help/edge/docs/forms/repeatable-forms.md)
* [提交表單後顯示自訂感謝訊息&#x200B;。](/help/edge/docs/forms/thank-you-page-form.md)
* [最適化表單區塊元件及其屬性](/help/edge/docs/forms/form-components.md)



<!-- 

## Start creating forms

<div>

  <style>
    .card-container {
        width: calc(33.33% - 10px);;
        margin: 5px;
        border: 1px solid #ccc;
        border-radius: 5px;
        padding: 5px;
        box-sizing: border-box;
        transition: background-color 0.3s ease; /* Adding transition effect */
    }
    .card-container:hover {
        background-color: #f0f0f0; /* Changing background color on hover */
    }
</style>

<div style="display: flex; flex-wrap: wrap; justify-content: space-between; margin: -5px;">
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md">
            <img src="/help/edge/assets/smock_devices_18_n.svg" alt="Create a form using eds forms" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Create a form using Google Sheets or Microsoft Excel</b>
        </a>
        <p>Create forms that load and render quickly and automatically reflows on mobile devices.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   
            <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="Submit form" alt="Use Form Fragments in an EDS Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Submit form to spreadsheet</b>
        </a>
        <p>Submit forms directly to your Microsoft Excel or Google Sheets.</p>
    </div>
     <div class="card-container">
        <a href="/help/edge/docs/forms/style-theme-forms.md">
            <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="Apply styles or themes to an eds form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Customize a theme</b>
        </a>
        <p>Create a consistent brand image by applying the same theme across forms.</p>
    </div>
      <div class="card-container">
        <a href="/help/edge/docs/forms/validate-forms.md">
            <img src="/help/edge/assets/smock_condition_18_n.svg" alt="Add validations to form fields" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Apply field validations</b>
        </a>
        <p>Reduce errors and frustration by checking form inputs for proper formatting.</p>
    </div> 
            <div class="card-container">
        <a href="/help/edge/docs/forms/rules-forms.md">
            <img src="/help/edge/assets/smock_documentfragment_18_n.svg" alt="Use rules to add dynamic behaviour to a form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Use rules to add dynamic behaviour to a form</b>
        </a>
        <p>Reuse preconfigured fragments across multiple forms.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/translate-forms.md">  
            <img src="/help/edge/assets/smock_abc_18_n.svg" alt="Translate an EDS Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Translate a form</b>
        </a>
        <p>Extend the reach of your forms while keeping costs in check.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/repeatable-forms.md">  
            <img src="/help/edge/assets/smock_addto_18_n.svg" alt="Add repeatable sections to an EDS Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Add repeatable sections</b>
        </a>
        <p>Effortlessly create and add repeatable sections to a form.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/custom-components-forms.md"> 
            <img src="/help/edge/assets/smock_userdeveloper_18_n.svg" alt="Create custom forms components using standard JavaScript and CSS"  style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Create custom components</b>
        </a>
        <p>Use standard JavaScript and CSS to create components and themes.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/recaptacha-forms.md">  
            <img src="/help//edge/assets/smock_keyclock_18_n.svg" alt="Use reCAPTCHA in an EDS Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Use reCAPTCHA</b>
        </a>
        <p>Use OOTB reCAPTCHA integration for robust spam and bot protection.</p>
    </div>


</div>


</br>


-->