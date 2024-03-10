---
title: AEM FormsEdge Delivery Services概觀
description: AEM FormsEdge Delivery Services專為最佳效能而打造，可讓您構想簡化資料收集和使用者參與的未來。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
source-git-commit: 2aa70e78764616f41fe64e324c017873cfba1d5b
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 18%

---

# AEM FormsEdge Delivery Services

透過Adobe的AEM FormsEdge Delivery Services，簡化表單建立流程並提高完成率。 這些功能強大、可撰寫的服務可讓您建立具有卓越效能和視覺吸引力的企業級表單。 AEM會同時優先考慮使用者體驗和業務目標，確保超快的載入時間和更高的表單轉換率。

您可以使用該服務來：

* **建立卓越的註冊體驗**：建立可快速載入和轉譯的註冊體驗，即使在網際網路連線速度緩慢時亦然。 更快的載入時間和最佳化使用者體驗有助於提高表單完成率和轉換率。

* **使用您選擇的工具建立註冊體驗**：透過分離內容來源來提高編寫效率。 現成可用兩者 **document-based authoring** (Microsoft SharePoint或Google Drive)和 **AEM製作** (最適化Forms編輯器)。 因此，您可以在相同表單上使用多個內容來源，並使用您偏好的編寫工具，例如Microsoft Excel、Google Sheets或Adaptive Forms Editor。

* **使用開發人員友善的工具集：** AEM Forms使用純HTML、新式CSS和vanilla JavaScript，建立卓越的體驗，免除平常的額外負荷。 任何具備HTML、CSS和JS基礎知識的開發人員都應該能夠建立自己的元件，而且不需要學習任何特定語言或架構。 無需任何管道或等待，將您的程式碼簽入Github中且您的變更已上線。 此外，無需任何管道或等待，您可以將程式碼簽入Github中，且您的變更已上線。


## AEM FormsEdge Delivery Services概觀 {#edge-overview}

下圖說明如何在Microsoft Excel或Google Sheets中編輯內容（以檔案為基礎的編輯）以及發佈至Edge Delivery Services。 此外也顯示使用最適化Forms編輯器的AEM發佈方法。

![Edge Delivery 架構](/help/edge/assets/AEM-forms-with-EDS-publishing.png)

Edge Delivery Services 是一組可組合的服務，可讓您以高度靈活的方式在網站上製作內容。如前所述，您可以使用兩者 [AEM內容管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/getting-started/concepts.html) 替換為 [AEM製作](/help/implementing/universal-editor/introduction.md) 以及 [document-based authoring](https://www.aem.live/docs/authoring)

例如，您可以直接從Microsoft Excel或Google Sheets使用內容。 這表示來自這些來源的內容可以成為您網站上的表單。 新內容將立即加入，無需重建過程。

Edge Delivery Services 使用 GitHub，因此客戶可以直接從其 GitHub 存放庫管理和部署程式碼。例如，您可以在Google工作表或Microsoft Excel中撰寫表單，而您可以使用GitHub中的CSS和JavaScript來開發表單元件。 準備好後，您可以使用 Sidekick 瀏覽器擴充功能來預覽和發佈內容更新。

AEM FormsEdge Delivery Services提供forms區塊，稱為 [最適化Forms區塊](/help/edge/docs/forms/create-forms.md) 以新增表單至您的Edge Delivery Services網站。

### AEM FormsEdge Delivery Services的主要功能

檔案式製作是一組基本功能和AEM製作，除了檔案式製作之外，還能開啟其他功能，讓您能夠建立更複雜且互動式的表單。 下表重點說明兩者的主要功能：

<!-- 

>[!BEGINTABS]

>[!TAB Document-based authoring]

Document-based authoring is a versatile option suitable for creating simple forms with essential functionalities. It allows you to integrate various input types like text fields, dropdown menus, and radio buttons, enabling you to collect user data effectively. It offers a basic version of rules to add dynamic behaviour to forms. Key features of Document-based authoring are: 

* **[HTML5-based Form Field components](/help/edge/docs/forms/form-components.md)**: AEM Forms Edge Delivery Services allow you to create user-friendly and interactive forms using form components based on HTML5 [input types](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types), <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea">textarea</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">select</a>, and <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset</a>  elements. These components cater to different types of data collection and can be easily customized to fit your specific needs.  

* **Accessibility**: The fields in the form block are accessible. Each label is linked with its respective input element, and IDs are auto-generated for linking. Descriptions associated with fields are linked via the aria-describedby attribute. Keyboard navigation using the standard Tab/Shift + Tab keys is supported.

* **[Styling](/help/edge/docs/forms/style-theme-forms.md)**: Each form field has a fixed HTML structure that can be easily decorated using custom CSS or JavaScript files. Selectors for targeting fields in CSS and JS are provided based on type and name. You can easily create new selectors due to the standradized structure and style your form. 

* **Basic Rules**: Easily create logic that adjusts field visibility, validation, and behavior based on user input or predefined conditions. Rules offer a flexible and intuitive way to add intelligence to your forms, ensuring they adapt seamlessly based on user inputs.

* **Validations**: Before submission, the form is validated, and invalid fields are appropriately marked with error messages displayed to the user. Adaptive Forms Block support all the HTML form validation, supported by modern browsers, and provide additional validation mechanism like validation script, file size, file type, overall file size, and more. 

* **File Uploads**: You can add file attachment capabilities to your forms. Whether you need to gather documents, images, or other files from your users, file upload functionality serves you effortlessly. With custom handling options available, you can tailor the file upload process to suit your specific requirements.

* **reCAPTCHA**: Benefit from seamless integration of Google reCAPTCHA into your forms with our out-of-the-box (OOTB) support. Safeguard your forms against fraudulent activities, spam, and abuse, while maintaining a smooth and uninterrupted user experience. Adaptive Forms Block supports reCaptcha V3 and reCaptcha Enterprise. 

* **Send email notification on form submission**: Eliminate the hassle of manual follow-ups and ensure timely communication with our built-in email automation for form submissions. This integrated solution lets you effortlessly notify relevant parties, including sending form data, whenever someone fills out a form on your website. No need for complex configurations or additional tools – it's ready to use out of the box.

>[!TAB AEM Authoring]

AEM Authoring unlocks additional capabilities beyond the document-based authoring, empowering you to build more complex and interactive forms. In additon to the features of Document-based authoring, AEM authoring offers the following additional features:  

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

|                                           | 檔案式撰寫 | AEM製作(最適化Forms編輯器) |
| ----------------------------------------- | ------------------------ | ------------------------------------ |
| **表單功能** |                          |                                      |
| 可存取的元件 | ✓ | ✓ |
| 標準化HTML結構 | ✓ | ✓ |
| 規則和驗證 | ✓ | ✓ |
| 檔案附件（檔案上傳） | ✓ | ✓ |
| Google reCAPTCHA | ✓ | ✓ |
| 自訂元件 | ✓ | ✓ |
| 提交至電子郵件 | ✓ | ✓ |
| **進階功能** |                          |                                      |
| 使用視覺化規則編輯器的進階規則 |                          | ✓ |
| 伺服器端擴充性 |                          | ✓ |
| 多重提交動作 |                          | ✓ |
| **表單設計與管理** |                          |                                      |
| 所見即所得編輯的最適化Forms編輯器 |                          | ✓ |
| **整合** |                          |                                      |
| 記錄文件 |                          | ✓ |
| 與Adobe Sign整合 |                          | ✓ |
| 與Adobe Analytics整合 |                          | ✓ |
| 與Marketo整合 |                          | ✓ |
| 與多個資料來源整合 |                          | ✓ |
| 多重提交動作 |                          | ✓ |


## 開始建立表單

* [快速入門 — 開發人員教學課程](/help/edge/docs/forms/tutorial.md)
* [使用Google工作表或Microsoft Excel建立表單](/help/edge/docs/forms/create-forms.md)
* [直接將表單提交至您的Microsoft Excel或Google工作表](/help/edge/docs/forms/submit-forms.md)
* [變更表單外觀](/help/edge/docs/forms/style-theme-forms.md)


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