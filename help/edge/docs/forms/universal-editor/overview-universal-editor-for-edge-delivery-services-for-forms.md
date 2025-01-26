---
title: AEM Forms 適用的 Edge Delivery Services 概觀
description: AEM Forms 適用的 Edge Delivery Services
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
source-git-commit: ae31df22c723c58addd13485259e92abb4d4ad54
workflow-type: tm+mt
source-wordcount: '1144'
ht-degree: 11%

---

# FormsEdge Delivery Services的通用編輯器(EDS Forms區塊)


通用編輯器旨在協助內容建立者和表單作者輕鬆建立、管理和編輯表單。 它提供簡單、視覺化且有效率的編輯體驗，著重於Edge Delivery Services(EDS)。

透過通用編輯器，使用者可以拖放表單元素（如文字欄位、核取方塊和選項按鈕）以在What You See Is What You Get (WYSIWYG)介面中建立表單。 此方法可讓表單建立變得直覺且易於使用，即使對於沒有技術專業知識的人也是如此。

![通用編輯器](/help/edge/docs/forms/universal-editor/assets/universal-editor.png)

Universal Editor可讓內容建立者和表單作者以簡化且有效率的方式建置、管理和編輯表單。 此編輯器特別針對Edge Delivery Services(EDS)。 通用編輯器為建立表單提供使用者易記的視覺化編輯體驗。 您可以輕鬆拖放表單元素（如文字欄位、核取方塊、選項按鈕等），並在WYSIWYG (What You See Is What You Get)樣式介面中加以設定。

Universal Editor的核心優勢在於其強大的功能集，其中包括進階表單建立功能、動態規則編輯以及與各種資料來源的無縫整合。 使用者可使用預先建立的元件、可自訂的範本和廣泛的表單元素資料庫，快速設計回應式表單。

技術功能經過精心設計，以維持輕量型使用者端轉譯、跨瀏覽器相容性，並嚴格遵守協助工具標準。 Universal Editor for EDS Forms Block為尋求靈活、強大的表單建立和管理平台的組織提供全方位的解決方案。

## EDS Forms適用的Universal Editor的主要功能


<div>
  <div class="card" style="display: inline-block; width: calc(33.33% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/universal-editor.png" alt="WYSIWYG介面"> 
    <h3>WYSIWYG介面</h3>
    <p>Universal Editor為表單設計提供WYSIWYG介面。 它提供預先建立的元件資料庫、回應式設計支援，以及範本式表單建立。 您可以立即新增或移除表單欄位，並修改欄位屬性（如標籤、資料繫結、驗證）。 您也可以將自訂表單元件外掛至通用編輯器。</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(33.33% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="https://via.placeholder.com/150" alt="規則編輯器">
    <h3>規則編輯器</h3>
    <p>規則編輯器可讓您透過輕量型的JavaScript和JSON型定義，使用事件導向的規則、即時驗證和錯誤處理來建立複雜的表單互動。</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(33.33% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="https://via.placeholder.com/150" alt="提交動作">
    <h3>提交動作</h3>
    <p>提交動作透過後端整合選項、資料前置處理器、條件提交邏輯和安全端點連線，協助表單提交工作流程。</p>
  </div>
</div>

<div>
  <div class="card" style="display: inline-block; width: calc(33.33% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="https://via.placeholder.com/150" alt="預填服務">
    <h3>預填服務</h3>
    <p>預先填寫服務可聰明地使用來自各種來源的相關資料填入表單欄位，減少手動資料輸入，進而增強使用者體驗。</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(33.33% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="https://via.placeholder.com/150" alt="資料繫結">
    <h3>資料繫結</h3>
    <p>資料繫結可啟用表單欄位與後端資料來源之間的直接、動態連線，支援即時同步和複雜的資料對應。</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(33.33% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="https://via.placeholder.com/150" alt="國際化/本地化">
    <h3>國際化/本地化</h3>
    <p>國際化支援可透過多語言轉譯、從右至左的語言相容性以及地區設定特定格式來確保全球協助工具。</p>
  </div>
</div>

<div>
  <div class="card" style="display: inline-block; width: calc(33.33% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="https://via.placeholder.com/150" alt="Analytics與Tracking">
    <h3>Analytics與Tracking</h3>
    <p>內建的分析和追蹤機制可提供表單互動、提交率和使用者行為的深入分析，進而實現持續最佳化。</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(33.33% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="https://via.placeholder.com/150" alt="實驗（A/B測試）">
    <h3>實驗（A/B測試）</h3>
    <p>實驗可讓組織對表單設計執行A/B測試，以識別表現最佳的版面配置或功能。</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(33.33% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="https://via.placeholder.com/150" alt="任務管理">
    <h3>任務管理</h3>
    <p>與Adobe Workfront整合可讓團隊管理與表單建立和維護相關的工作，確保簡化共同作業。</p>
  </div>
</div>

<div>
  <div class="card" style="display: inline-block; width: calc(33.33% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="https://via.placeholder.com/150" alt="編輯器自訂">
    <h3>編輯器自訂</h3>
    <p>開發人員可透過UI擴充功能擴充通用編輯器的功能，讓量身打造的解決方案符合特定組織需求。</p>
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

Universal Editor提供下列立即可用的表單元件：

<table>
  <thead>
    <tr>
      <th>美極了</th> 
      <th>表單元件 </th>
      <th>說明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="22"><img src="/help/edge/docs/forms/universal-editor/assets/adaptive-forms-components.png" alt="表單元件 " style="width: 100%;"></td> 
      <td><b>折疊面板</b></td>
      <td>用於組織內容的可摺疊面板結構。</td>
    </tr>
    <tr>
      <td><b>按鈕</b></td>
      <td>為導覽或自訂邏輯等動作新增互動元素。</td>
    </tr>
    <tr>
      <td><b>Captcha</b></td>
      <td>透過要求使用者使用Google reCaptcha或HCaptcha完成人工驗證任務來防止垃圾郵件。</td>
    </tr>
    <tr>
      <td><b>核取方塊</b></td>
      <td>允許使用者設定核取方塊。</td>
    </tr>
    <tr>
      <td><b>核取方塊群組</b></td>
      <td>允許使用者從群組選取多個選項。</td>
    </tr>
    <tr>
      <td><b>日期挑選器</b></td>
      <td>允許使用者使用行事曆介面選取日期。</td>
    </tr>
    <tr>
      <td><b>下拉式清單</b></td>
      <td>從預先定義的清單中提供單一或多重選取選項。</td>
    </tr>
    <tr>
      <td><b>電子郵件</b></td>
      <td>透過基本格式驗證擷取電子郵件地址。</td>
    </tr>
    <tr>
      <td><b>檔案附件</b></td>
      <td>可上傳檔案、影像或其他檔案型別。</td>
    </tr>
    <tr>
      <td><b>表單片段</b></td>
      <td>位址列位或聯絡人詳細資料等區段的可重複使用表單元件。</td>
    </tr>
    <tr>
      <td><b>影像</b></td>
      <td>支援在表單內上傳和顯示影像。</td>
    </tr>
    <tr>
      <td><b>模型</b></td>
      <td>顯示快顯對話方塊，通常用於警示、其他資訊或確認。</td>
    </tr>
    <tr>
      <td><b>數值欄位</b></td>
      <td>擷取數值輸入，允許驗證數字或範圍。</td>
    </tr>
    <tr>
      <td><b>面板</b></td>
      <td>使用可展開/可摺疊的面板組織表單區段。</td>
    </tr>
    <tr>
      <td><b>選項按鈕</b></td>
      <td>啟用從選項群組中選取單一選項。</td>
    </tr>
    <tr>
      <td><b>評等</b></td>
      <td>允許使用者提供星級評等。</td>
    </tr>
    <tr>
      <td><b>重設按鈕</b></td>
      <td>將表單欄位重設為預設狀態。</td>
    </tr>
    <tr>
      <td><b>提交按鈕</b></td>
      <td>觸發表單提交並起始定義的工作流程。</td>
    </tr>
    <tr>
      <td><b>電話號碼欄位</b></td>
      <td>根據國家/地區以格式擷取電話號碼。</td>
    </tr>
    <tr>
      <td><b>文字</b></td>
      <td>提供透過核取方塊顯示法律條款及收集使用者協定的專屬區段。</td>
    </tr>
    <tr>
      <td><b>文字欄位</b></td>
      <td>DCaptures單行輸入，例如名稱或電子郵件地址。</td>
    </tr>
    <tr>
      <td><b>精靈</b></td>
      <td>引導使用者逐步完成多部分表單程式。</td>
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

-->

除了預先建立的表單元件外，通用編輯器也提供下列支援：

* **將Forms內嵌在其他網頁中**： Universal Editor支援將表單直接內嵌到Edge Deliver Services Sites頁面。 您可以使用隨附立即可用的內嵌元件完成這項作業。

* **驗證訊息**：當使用者輸入不正確或不完整的資料時，驗證訊息會提供即時回饋。 功能包含：
   * 動態錯誤顯示：立即警示使用者發生錯誤，例如電子郵件地址無效或遺失必要欄位。
   * 可自訂的訊息：可讓表單作者定義好記的錯誤文字。
   * 規則型驗證：支援進階驗證邏輯，例如檢查欄位之間的相依性或實作條件式規則。

* **隱藏欄位**：隱藏欄位會在表單中以不可見的方式儲存資料，通常用於後端處理或預填的值。 使用案例包括：
   * 將內容相關資訊（例如使用者ID或工作階段資料）傳遞至後端，而不向使用者顯示。
   * 擷取如時間戳記或追蹤ID等中繼資料。
   * 一般使用者看不到隱藏欄位，但可以預先填寫、動態更新，或用於工作流程。

* **自訂元件**：自訂元件可讓開發人員透過建立專業化或協力廠商整合來擴充表單功能。 功能包含：
   * 彈性：開發人員可針對特定使用案例設計獨一無二的表單元素。
   * 第三方整合：內嵌Widget或工具，例如支付閘道、分析追蹤器或AI導向的輸入欄位。
   * 緊密相容：自訂元件可與Universal Editor的拖放介面和現有功能（如資料繫結或驗證）整合。

* **感謝您的設定**：自訂表單提交後顯示的認可訊息或頁面。

## 上線

若要為您的環境啟用通用編輯器和規則編輯器，或請求其他功能，例如Forms入口網站、記錄檔案、Adobe Sign整合或從右至左的語言支援，只需透過您的正式地址傳送電子郵件至mailto:aem-forms-ea@adobe.com提出請求即可。



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