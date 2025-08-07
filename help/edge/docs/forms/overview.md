---
title: AEM Forms 適用的 Edge Delivery Services 概觀
description: 在 Adobe Experience Manager Edge Delivery Services 上建立和傳遞高效能表單，並強調通用編輯器的製作方法。
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: ccfb85da187e828b5f7e8b1a8bae3f483209368d
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 100%

---


# AEM Forms 適用的 Edge Delivery Services


AEM Forms 適用的 Edge Delivery Services 是一套可組合的服務，提供快速開發環境讓作者迅速更新、發佈並推出新表單。這些服務提供卓越且高影響力的表單體驗，進而促進使用者的參與度和轉換率。這些表單體驗易於製作和開發。

這些服務可讓您：

- **使用您選擇的工具建立註冊體驗**：透過分離內容來源來提高製作效率。您可以開啟立即使用文件型製作 (Microsoft SharePoint 或 Google Drive) 和 WYSIWYG 製作 (通用編輯器或最適化 Forms 編輯器)。您可以在同一個表單網站上使用多個內容來源，並使用您偏好的製作工具，例如 Microsoft Excel、Google Sheets、通用編輯器或最適化表單編輯器。

- **提供卓越的數位註冊體驗：**&#x200B;提供能快速載入和呈現的數位註冊體驗，並透過操作遙測持續監視您的表單效能。載入時間更快和使用者體驗最佳化，有助於提高表單完成率和轉換率。

- **使用開發人員易用的工具組：** AEM Forms 適用的 Edge Delivery Services 使用純 HTML、現代 CSS 和普通 JavaScript 來建立卓越的體驗，避免特定框架出現陡峭的學習曲線。只要具備基本 Web 開發技能的開發人員，即可自訂並輕鬆建立表單元件和體驗。無需等待管道開始運作，只需將程式碼簽入 GitHub，您進行的變更就會生效。

## 選擇製作方法


透過 Adobe Experience Manager (AEM) Edge Delivery Services (EDS)，您可以從邊緣提供極快速且高度可擴充的網頁體驗。本指南說明&#x200B;**如何建置和發佈符合這些體驗的表單**，並具備明確的建議階層：

- **通用編輯器 (UE) – 大多數團隊的最佳選擇**
- **文件型製作 (文件/試算表)－非常適合快速、簡單的表單**
- **文件製作 (DA) – 可以將表單嵌入至 DA 製作的頁面中**

最後，您將能選擇正確的製作方法、了解提交選項，並按照後續步驟製作立即可用的表單。


| 團隊和要求 | 建議方法 | 原因 |
|--------------------|--------------------|-----|
| 行銷人員/設計師需要視覺化控制、條件邏輯或 AEM 整合 | **通用編輯器** | 拖放功能、進階規則、提交至 FSS 或 AEM Publish |
| 內容作者原本已在使用 Word/Google Docs/試算表；簡單地將資料擷取至試算表/電子郵件 | **文件型製作** | 熟悉的工具，製作基本表單的最快途徑 |
| 以&#x200B;**文件製作 (DA)**&#x200B;建置的網站頁面 | 將 UE 或文件型表單&#x200B;**嵌入**&#x200B;至 DA 頁面 | DA 無法自行建置表單 |


## 製作方法詳細資訊

### 通用編輯器

<!--<span class="preview"> This is a pre-release feature available through our <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features">pre-release channel</a>. </span>-->

[通用編輯器](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)是一款適用於行銷人員和設計師的視覺化拖放式製作工具，兼具速度與企業級效能：

- 即時的所見即所得編輯和裝置預覽。
- 與 AEM 資產、工作流程及表單資料模型 (FDM) 直接整合。
- 將普通 JS/CSS 中的自訂元件順利移交給開發人員。
- 用來建立複雜邏輯的進階規則編輯器。
- 提供自訂功能的伺服器端可擴充性。
- 可輕鬆建立表單和視覺效果的 WYSIWYG 編輯體驗。
- 記錄文件功能可建立提交資料的防篡改檔案。
- 與 Adob&#x200B;&#x200B;e Sign 整合以進行電子簽名。
- 與 Adob&#x200B;&#x200B;e Workfront Fusion 整合，以便在提交表單時觸發 Adob&#x200B;&#x200B;e Workfront Fusion 情境。
- 與各種資料來源整合，以預先填入表單和提交資料。
- 用來定義資料結構並與各種資料來源互動的表單資料模型 (FDM)。
- 具備能力從多個提交操作中選擇以處理表單提交，包括將資料提交到 Microsoft SharePoint、Microsoft OneDrive、Adobe Workfront Fusion、Salesforce、Microsoft Dynamics 以及更多資料來源。
- 使用表單提交服務 (FSS) 或 AEM Publish 提交動作進行提交

**建議**：使用通用編輯器開啟每個新表單專案，除非您的團隊完全以文件為中心且表單設計非常樸素。


### 文件型製作 (使用 Microsoft Docs 或 Google Sheets)

使用如 Microsoft Word、Google Docs 或 Google Sheets 等熟悉的工具來建立簡單、低複雜度的表單者，最適合使用[文件型製作](/help/edge/docs/forms/tutorial.md)。此方法非常適合需要用快速、直接的方式建置表單的內容團隊。

- 提供使用者易用體驗的可存取元件。
- 標準化 HTML 結構以呈現一致性。
- 確保資料準確性的規則和驗證。
- 用來收集附加資訊的檔案附件選項。
- 防止垃圾郵件的 Google reCAPTCHA 整合。
- 具備能力以依據特定需求建立自訂表單元件。
- 直接將表單資料提交到 Microsoft Excel 或 Google Sheets 或電子郵件地址。
- 透過操作遙測監視表單效能


### 在文件製作 (DA) 中嵌入表單

文件製作 (DA) 旨在建立結構化頁面內容，並不支援原生的表單建立功能。若要將表單新增至以 DA 製作的頁面，您可以使用&#x200B;**通用編輯器** (建議) 或文件型製作來建立表單，然後將表單嵌入至文件製作頁面。

## 發佈 Edge Delivery Services 表單 {#edge-overview}

下圖說明如何在 Microsoft Excel 或 Google Sheets (文件型製作) 中編輯表單，並將其發佈至 Edge Delivery Services。此圖也顯示使用所見即所得製作 (通用編輯器)的 AEM 發佈方法。

![發佈至 Edge Delivery Services 和 AEM](/help/edge/docs/forms/assets/AEM-forms-with-EDS-publishing.png)


<!-- 
## Feature Comparison

| Capability | Universal Editor | Document-Based | Document Authoring |
|------------|-----------------|----------------|--------------------|
| Visual drag-and-drop | ✅ | – | – |
| Advanced rules editor | ✅ | Limited | – |
| Attachments | ✅ | EA | – |
| reCAPTCHA Enterprise | ✅ | ✅ | Depends on embed |
| Submit to spreadsheet/email | ✅ (FSS) | ✅ (FSS) | Via embed |
| Submit to AEM workflows/FDM | ✅ | – | Via UE embed |
| Custom components (JS/CSS) | ✅ | ✅ | Via embed |
| Localization via Sites | ✅ | Manual | Via embed |

-->

## 後續步驟

- [Edge Delivery Services for Forms 通用編輯器的特性和功能](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
- [使用通用編輯器建立您的第一份表單](/help/edge/docs/forms/universal-editor/create-forms.md)
- [使用 Google Sheets 或 Microsoft Excel 建立您的第一份表單](/help/edge/docs/forms/tutorial.md)。
- [在文件製作 (DA) 中嵌入表單](https://www.aem.live/developer/da-tutorial)


現在，您已準備好使用 AEM Edge Delivery Services 建立第一個高效能表單。


<!-- 

## Start creating forms

- [Get started with Edge Delivery Services for AEM Forms](/help/edge/docs/forms/tutorial.md)
- [Create a form using Google Sheets or Microsoft Excel](/help/edge/docs/forms/create-forms.md)
- [Set up your Google Sheets or Microsoft Excel files to start accepting data​](/help/edge/docs/forms/submit-forms.md)
- [Publish your form and start collecting data](/help/edge/docs/forms/publish-forms.md)
- [Customize the look of your forms​](/help/edge/docs/forms/style-theme-forms.md)
- [Add repeatable sections to a form​](/help/edge/docs/forms/repeatable-forms.md)
- [Show a custom thank you message after form submission​](/help/edge/docs/forms/thank-you-page-form.md)
- [Adaptive Form Block components and their properties](/help/edge/docs/forms/form-components.md)
- [Real Use Monitoring](https://www.aem.live/developer/rum#authentication)

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
        transition: background-color 0.3s ease; /- Adding transition effect */
    }
    .card-container:hover {
        background-color: #f0f0f0; /- Changing background color on hover */
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