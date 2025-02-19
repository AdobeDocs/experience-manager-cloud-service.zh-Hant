---
title: Edge Delivery Services for Forms 的通用編輯器 (EDS Forms 區塊)
description: 使用 Edge Delivery Services for Forms 的通用編輯器 (EDS Forms 區塊) 建立最適化表單。
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
exl-id: d711e0d1-a2fc-4aa6-af87-6e77a7bc5d2e
source-git-commit: 35834ba89d20d719a40b930ca672ec242d81d376
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 97%

---

# Edge Delivery Services for Forms 的通用編輯器 (EDS Forms 區塊)

通用編輯器提供簡單、視覺化且直覺易用的所見即所得 (WYSIWYG) 介面，徹底改變 Adobe Edge Delivery Services (EDS) 建立表單的方式。這是專為內容創作者和表單製作者而設計，消除傳統表單建置流程的複雜性，讓非技術使用者也可以存取使用。

使用通用編輯器，您可以使用預先建立的元件 (如文字欄位、核取方塊和選項按鈕) 快速設計回應式、互動式表單。其強大的功能集支援動態規則、無縫資料整合和進階的個人化功能，確保每種表單都符合您的需求。

無論您是管理客戶端的輕量轉譯、確保跨瀏覽器相容性，或者遵守嚴格的無障礙標準，通用編輯器皆是建立和管理表單的精簡型解決方案。

![通用編輯器](/help/edge/docs/forms/universal-editor/assets/universal-editor.png){width=80%, align-center} -->

## EDS Forms 通用編輯器的主要功能


<div>
 <a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/universal-editor/universal-editor-user-interface" target="_blank" style="text-decoration: none; color: inherit;">
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center; cursor: pointer;">
    <img src="/help/edge/docs/forms/universal-editor/assets/generate-forms.svg" alt="WYSIWYG 介面"> 
    <h3>WYSIWYG 介面</h3>
    <p>通用編輯器為表單設計提供 WYSIWYG 介面，具有預先建立的元件資料庫、回應式設計、範本式建立和即時欄位修改。</p>
  </div>
</a>
<a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/universal-editor/rule-editor-universal-editor" target="_blank" style="text-decoration: none; color: inherit;">
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center; cursor: pointer;">
    <img src="/help/edge/docs/forms/universal-editor/assets/rule-editor.svg" alt="規則編輯器">
    <h3>規則編輯器</h3>
    <p>規則編輯器讓使用者能夠透過事件驅動的規則、即時驗證，以及藉由輕量級 JavaScript 和 JSON 進行錯誤處理，來建立動態表單互動。</p>
  </div>
</a>
<a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/universal-editor/submit-action" target="_blank" style="text-decoration: none; color: inherit;">
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center; cursor: pointer;">
    <img src="/help/edge/docs/forms/universal-editor/assets/submit-actions.svg" alt="提交動作">
    <h3>提交動作</h3>
    <p>提交動作功能支援後端整合、條件式提交邏輯、安全端點和預處理器，能簡化提交工作流程。</p>
  </div>
</a>
<div>
<a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/universal-editor/publish-forms" target="_blank" style="text-decoration: none; color: inherit;">
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center; cursor: pointer;">
    <img src="/help/edge/docs/forms/universal-editor/assets/publish-unpublish.svg" alt="發佈/取消發佈">
    <h3>發佈/取消發佈</h3>
    <p>輕鬆控制表單的可見度 - 只需點選幾下即可直接從編輯器發佈或取消發佈表單，您可以即時動態管理可用性和內容更新。</p>
  </div>
</a>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/responsive.svg" alt="回應式模式">
    <h3>回應式模式 </h3>
    <p>設計可跨裝置 (桌上型電腦、平板電腦和行動裝置) 順暢適應的表單。使用回應式模式預覽和測試各種螢幕尺寸的表單。</p>
  </div>
<a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/universal-editor/create-custom-component" target="_blank" style="text-decoration: none; color: inherit;">
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center; cursor: pointer;">
    <img src="/help/edge/docs/forms/universal-editor/assets/custom-components.svg" alt="自訂元件">
    <h3>自訂元件</h3>
    <p>自訂元件功能讓開發人員得以透過建立針對特定組織使用案例而自訂的不重複元素，擴展表單功能。</p>
  </div>
</a>
</div>
<a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/universal-editor/style-theme-forms" target="_blank" style="text-decoration: none; color: inherit;">
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center; cursor: pointer;">
    <img src="/help/edge/docs/forms/universal-editor/assets/personalization.svg" alt="樣式">
    <h3>樣式</h3>
    <p>使用CSS進行樣式設定可讓開發人員自訂表單元素的外觀，並建立與網站美學相一致的美觀設計。</p>
  </div>
</a>
    <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/prefill-services.svg" alt="預填服務">
    <h3>預填服務</h3>
    <p>預填服務會自動使用來自各來源的相關使用者資料填寫表單欄位，減少手動輸入過程並增強使用者體驗。</p>
  </div>
  <a href="https://github.com/adobe/aem-experimentation/blob/main/documentation/experiments.md" target="_blank" style="text-decoration: none; color: inherit;">
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center; cursor: pointer;">
    <img src="/help/edge/docs/forms/universal-editor/assets/experimentation-ab-testing.svg" alt="A/B 測試">
    <h3>A/B 測試</h3>
    <p>A/B 測試 (實驗) 讓組織能夠實驗不同的表單設計、版面和功能，以尋得最佳表現的變體。</p>
  </div>
</a>
</div>
<div>
  <a href="https://www.aem.live/developer/martech-integration" target="_blank" style="text-decoration: none; color: inherit;">
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center; cursor: pointer;">
    <img src="/help/edge/docs/forms/universal-editor/assets/analyticsandtracking.svg" alt="分析與追蹤">
    <h3>分析與追蹤</h3>
    <p>透過內建的分析與追蹤功能，深入了解使用者行為、表單互動和提交率，以達到資料驅動的表單最佳化。</p>
  </div>
</a>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/adobe-workfront.svg" alt="與 Adobe Workfront 整合">
    <h3> 任務管理 </h3>
    <p>與 Adobe Workfront 進行整合，讓團隊能夠管理表單建立與維護任務，確保簡化工作流程。</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/data-binding.svg" alt="資料繫結">
    <h3>資料繫結</h3>
    <p>資料繫結功能讓表單欄位和後端資料來源能直接連線，支援結構化申訴資料儲存的即時更新和進階資料對應。</p>
  </div>
</div>

<div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/editor-customization.svg" alt="編輯器自訂">
    <h3>編輯器自訂</h3>
    <p>開發人員可以透過使用者介面延伸模組來擴展編輯器的功能，進而開發出符合特定組織需求的量身打造解決方案。</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/embedding-forms.svg" alt="嵌入表單">
    <h3>嵌入表單</h3>
    <p>使用通用編輯器的內建嵌入元件，將表單直接嵌入到 Edge Delivery Services Sites 頁面中，形成順暢的使用者體驗。</p>
  </div>
  <a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/universal-editor/submit-action#submit-action-message-ue" target="_blank" style="text-decoration: none; color: inherit;">
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center; cursor: pointer;">
    <img src="/help/edge/docs/forms/universal-editor/assets/thank-you.svg" alt="感謝設定">
    <h3>感謝設定</h3>
    <p>輕鬆自訂在成功提交表單後，欲呈現給使用者看的確認訊息或頁面。</p>
  </div>
</a>
</div>
</div>


<!-- ![Universal Editor](/help/edge/docs/forms/universal-editor/assets/generate-forms.svg)  **WYSIWYG interface for Form creation**: Universal Editor provides a WYSIWYG interface for form design. It provides pre-built component library, responsive design support, and template-based form creation. You can instantly add or remove form fields and modify field properties (like label, data binding, validation). You can also plugin custom form components to Universal Editor.


* **Rule editor**: The rule editor stands out as a powerful mechanism for creating sophisticated form interactions. It supports event-driven rules, instant validation, and error handling through lightweight JavaScript and JSON-based definitions. This allows developers to implement complex form logic, such as conditional field visibility, automatic calculations, and dynamic form behaviour without extensive coding.

* **Submit actions**: Submit Actions enable form submission workflows. These actions provide comprehensive backend integration options, supporting protocols like REST API. The system allows you configure data pre-processors for automatic data transformation, conditional submission logic based on form field values, and secure endpoint connections. Organizations can define complex submission rules that validate data, and manage form responses with granular control.

* **Pre-fill services:** Pre-fill Services enhance user experience by intelligently populating form fields with relevant data. These services connect to various data sources, including user profiles, browser local storage, and external databases. The mechanism supports dynamic data population, enabling automatic completion of form fields based on contextual information. Users benefit from reduced manual data entry, while administrators gain flexibility in configuring pre-fill rules across different form types and scenarios. The pre-fill functionality adapts to different authentication methods, including session-based approaches and token-based systems, ensuring both convenience and security.

* **Data binding capabilities**: Data binding in the Universal Editor enables direct, dynamic connections between form fields and backend data sources. This feature allows real-time synchronization of form data, supporting complex data mapping scenarios. The system supports transforming form inputs into structured database records with minimal configuration. Advanced mapping supports nested data structures, allowing complex form designs to interact seamlessly with intricate data models.

* **Internationalization/localization capabilities**: Internationalization support ensures global accessibility, with multi-language rendering, right-to-left language compatibility, and locale-specific formatting.

* **Analytics and tracking mechanisms**: The built-in analytics and tracking mechanisms provide comprehensive insights into form interactions, submission rates, and user behavior, enabling continuous optimization of form design and performance. 

* **Experimentation (A/B Testing)**: The Universal Editor supports experimentation by allowing organizations to run A/B tests on form designs to identify the best-performing layouts or features.

* **Task Management via Adobe Workfront**: Integration with Adobe Workfront allows teams to manage tasks related to form creation and maintenance, ensuring streamlined collaboration and efficient workflows.

* **Editor Customization via UI Extension**: Developers can extend the functionality of the Universal Editor through UI extensions, enabling tailored solutions that fit specific organizational needs. -->

## 預先建立的表單元件

通用編輯器提供以下立即可用的表單元件：

<table>
  <thead>
    <tr>
      <th></th> 
      <th>表單元件</th>
      <th>說明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="22"><img src="/help/edge/docs/forms/universal-editor/assets/adaptive-forms-components.png" alt="表單元件" style="width: 100%;"></td> 
      <td><b>折疊面板</b></td>
      <td>用於將內容進行組織的可收摺面板結構。</td>
    </tr>
    <tr>
      <td><b>按鈕</b></td>
      <td>替導覽或自訂邏輯等動作新增互動式元素。</td>
    </tr>
    <tr>
      <td><b>驗證碼</b></td>
      <td>要求使用者透過 Google reCaptcha 或 HCaptcha 完成人工驗證任務，以避免垃圾郵件。</td>
    </tr>
    <tr>
      <td><b>核取方塊</b></td>
      <td>讓使用者能夠設定核取方塊。</td>
    </tr>
    <tr>
      <td><b>核取方塊群組</b></td>
      <td>讓使用者能夠從一個群組中選取多個選項。</td>
    </tr>
    <tr>
      <td><b>日期挑選器</b></td>
      <td>讓使用者能夠利用行事曆介面選取日期。</td>
    </tr>
    <tr>
      <td><b>下拉式清單</b></td>
      <td>提供預定義清單中的單選或多選選項。</td>
    </tr>
    <tr>
      <td><b>電子郵件</b></td>
      <td>透過基本格式驗證擷取電子郵件地址。</td>
    </tr>
    <tr>
      <td><b>檔案附件</b></td>
      <td>允許上傳文件、影像或其他類型的檔案。</td>
    </tr>
    <tr>
      <td><b>表單片段</b></td>
      <td>地址欄位或聯絡方式等區段的可重複使用表單元件。</td>
    </tr>
    <tr>
      <td><b>影像</b></td>
      <td>支援在表單中上傳和顯示影像。</td>
    </tr>
    <tr>
      <td><b>模型</b></td>
      <td>呈現快顯視窗對話框，通常用於警報、附加資訊或確認。</td>
    </tr>
    <tr>
      <td><b>數值欄位</b></td>
      <td>擷取數值輸入，允許驗證數字或範圍。</td>
    </tr>
    <tr>
      <td><b>面板</b></td>
      <td>使用可展開/可收摺面板將表單區段進行組織。</td>
    </tr>
    <tr>
      <td><b>選項按鈕</b></td>
      <td>允許從一個群組的選項中進行單項選取。</td>
    </tr>
    <tr>
      <td><b>評等</b></td>
      <td>讓使用者能夠提供星級式評等。</td>
    </tr>
    <tr>
      <td><b>重設按鈕</b></td>
      <td>將表單欄位重設為其預設狀態。</td>
    </tr>
    <tr>
      <td><b>提交按鈕</b></td>
      <td>觸發表單提交並啟動定義好的工作流程。</td>
    </tr>
    <tr>
      <td><b>電話號碼欄位</b></td>
      <td>擷取具有國家/地區格式的電話號碼。</td>
    </tr>
    <tr>
      <td><b>文字</b></td>
      <td>提供專門的區段來顯示法律條款，並透過核取方塊取得使用者同意。</td>
    </tr>
    <tr>
      <td><b>文字欄位</b></td>
      <td>DCapture 擷取單行輸入，例如姓名或電子郵件地址。</td>
    </tr>
    <tr>
      <td><b>精靈</b></td>
      <td>引導使用者逐步完成多部分形式表單的流程。</td>
    </tr>
  </tbody>
</table>

<!-- * Footer: Adds a footer section for consistent design or additional information.
* Form Container: Wraps all form elements and manages overall form properties.
* Header: Adds a header section for form titles, branding, or instructions.-->
<!-- * 
* Prefillable Fields: Automatically populates form fields with data from predefined sources such as user profiles or APIs. 

* Switches/Toggle Buttons: Provides binary on/off choices for user input.


* Title: Adds a text-based heading or label to improve form clarity and organization.


In-addtion to pre-built form components, the Universal editor also provides support for:

* **Embedding Forms in Another Webpage**: The Universal Editor supports embedding forms directly into Edge Deliver Services Sites pages. This can be done using the embed component provided out of the box.

* **Validation Messages**: Validation messages provide real-time feedback to users when they enter incorrect or incomplete data. Features include:
    * Dynamic Error Display: Instantly alerts users to errors, such as invalid email addresses or missing required fields.
    * Customizable Messages: Allows form authors to define user-friendly error texts.
    * Rule-Based Validation: Supports advanced validation logic, such as checking dependencies between fields or implementing conditional rules.

* **Hidden Fields**: Hidden fields store data invisibly within the form, often for backend processing or prefilled values. Use cases include:
    * Passing contextual information (e.g., user ID or session data) to the backend without displaying it to users.
    * Capturing metadata like timestamps or tracking IDs.
    * Hidden fields are not visible to end-users but can be prefilled, updated dynamically, or used in workflows.

* **Custom Components**: Custom components allow developers to extend the functionality of forms by creating specialized or third-party integrations. Features include:
    * Flexibility: Developers can design unique form elements tailored to specific use cases.
    * Third-Party Integration: Embed widgets or tools like payment gateways, analytics trackers, or AI-driven input fields.
    * Seamless Compatibility: Custom components can integrate with the Universal Editor's drag-and-drop interface and existing features like data binding or validation.

* **Thank you Configuration**: Customize the acknowledgment message or page shown after form submission.
-->


## 上線

若要啟用通用編輯器及其進階功能 (如規則編輯器)，請使用您的官方電子郵件 ID 寫信至 aem-forms-ea@adobe.com。Adobe 團隊隨時可協助您轉換表單建置體驗。

## 常見問題集 (FAQ)

**問：誰可以使用通用編輯器？**
通用編輯器旨在供廣泛客群使用，包括：

* 想要建置具有視覺吸引力的表單的內容創作者。
* 需要進階自訂和整合功能的開發人員。
* 尋求可擴充、安全且合規的表單解決方案之組織。

**問：我可否將使用通用編輯器建立的表單整合至現有的系統中？**
當然可以。通用編輯器支援資料與後端系統無縫連結，以利即時更新和進階資料對應。通用編輯器亦與 Adobe Workfront 等工具整合以進行任務管理，並支援供資料提交工作流程使用的安全端點。

**問：可以自訂表單元件嗎？**
可以，通用編輯器可讓開發人員建立符合特定組織需求的自訂元件。此外，您可以透過使用者介面延伸模組和自訂工作流程來擴充編輯器的功能。

**問：通用編輯器如何滿足無障礙要求？**
通用編輯器的設計嚴格遵守無障礙標準，包括 WCAG (網頁內容無障礙指南)。這樣可以確保身心障礙人士可以使用這些表單，提供包容性體驗。

**問：我可以從表單中獲得哪類型的分析？**
通用編輯器包括內建分析和追蹤工具，用於監視使用者互動情形、表單提交率和轉換量度。這些深入分析有助於最佳化您的表單，以達到更好的效能。


## 開始建立表單

* [開始使用 AEM Forms 適用的 Edge Delivery Services](/help/edge/docs/forms/tutorial.md)
* [使用 Google Sheets 或 Microsoft Excel 建立表單](/help/edge/docs/forms/create-forms.md)
* [設定您的 Google 表單或 Microsoft Excel 檔案以開始接受資料](/help/edge/docs/forms/submit-forms.md)
* [發佈您的表單並開始收集資料](/help/edge/docs/forms/publish-forms.md)
* [自訂表單的外觀](/help/edge/docs/forms/style-theme-forms.md)
* [將可重複區段新增到表單](/help/edge/docs/forms/repeatable-forms.md)
* [提交表單後顯示自訂感謝訊息](/help/edge/docs/forms/thank-you-page-form.md)
* [最適化表單區塊元件及其屬性](/help/edge/docs/forms/form-components.md)
* [實際使用監視](https://www.aem.live/developer/rum#authentication)

<!-- 

## Start creating forms

<div>

  <style>
    .card-container {
        width: calc(30% - 10px);;
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
