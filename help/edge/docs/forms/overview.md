---
title: AEM Forms 適用的 Edge Delivery Services 概觀
description: 在Adobe Experience Manager Edge Delivery Services上建立及提供高效能表單，並強調通用編輯器編寫方法。
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: e1ead9342fadbdf82815f082d7194c9cdf6d799d
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 48%

---


# AEM Forms 適用的 Edge Delivery Services


AEM Forms 適用的 Edge Delivery Services 是一套可組合的服務，提供快速開發環境讓作者迅速更新、發佈並推出新表單。這些服務提供卓越且高影響力的表單體驗，進而促進使用者的參與度和轉換率。這些表單體驗易於製作和開發。

這些服務可讓您：

* **使用您選擇的工具建立註冊體驗**：透過分離內容來源來提高製作效率。您可以開啟立即使用文件型製作 (Microsoft SharePoint 或 Google Drive) 和 WYSIWYG 製作 (通用編輯器或最適化 Forms 編輯器)。您可以在同一個表單網站上使用多個內容來源，並使用您偏好的製作工具，例如 Microsoft Excel、Google Sheets、通用編輯器或最適化表單編輯器。

* **提供卓越的數位註冊體驗：**&#x200B;提供能快速載入和呈現的數位註冊體驗，並透過操作遙測持續監視您的表單效能。載入時間更快和使用者體驗最佳化，有助於提高表單完成率和轉換率。

* **使用開發人員易用的工具組：** AEM Forms 適用的 Edge Delivery Services 使用純 HTML、現代 CSS 和普通 JavaScript 來建立卓越的體驗，避免特定框架出現陡峭的學習曲線。只要具備基本 Web 開發技能的開發人員，即可自訂並輕鬆建立表單元件和體驗。無需等待管道開始運作，只需將程式碼簽入 GitHub，您進行的變更就會生效。

## 選擇編寫方法


Adobe Experience Manager (AEM) Edge Delivery Services (EDS)可讓您從邊緣提供極快速、高度擴充的Web體驗。 本指南說明&#x200B;**如何建置和發佈這些體驗的表單** — 具有明確的建議階層：

1. **Universal Editor (UE) — 大多數團隊的最佳選擇**
2. **檔案式製作（檔案/工作表） — 適用於快速、簡單的表單**
3. **Document Authoring (DA) — 使用將表單內嵌至DA編寫的頁面**

到最後，您將能夠選擇正確的撰寫方法、瞭解提交選項，並遵循後續步驟以建立生產就緒的表單。





| 團隊與需求 | 建議的方法 | 原因 |
|--------------------|--------------------|-----|
| 行銷人員/設計人員需要視覺控制、條件邏輯或AEM整合 | **通用編輯器** | 拖放、進階規則、提交至FSS或AEM Publish |
| 內容作者已在Word/Google Docs/工作表中工作；將簡單資料擷取至試算表/電子郵件 | **檔案式製作** | 熟悉的工具，最快速的基本表單路徑 |
| 內建於&#x200B;**檔案製作(DA)**&#x200B;中的網站頁面 | **將UE或檔案型表單內嵌**&#x200B;至DA頁面 | DA不會建置表單本身 |


## 詳細編寫方法

### 通用編輯器

<span class="preview">這是透過我們的<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=zh-hant#new-features">發行前通道</a>提供的發行前功能。</span>

Universal Editor是行銷人員和設計人員適用的視覺化拖放式撰寫工具，結合速度與企業級效能：

* 即時WYSIWYG編輯和裝置預覽。
* 與AEM資產、工作流程和表單資料模型(FDM)直接整合。
* 原始版JS/CSS中自訂元件的無縫交接給開發人員。
* 用來建立複雜邏輯的進階規則編輯器。
* 提供自訂功能的伺服器端可擴充性。
* 可輕鬆建立表單和視覺效果的 WYSIWYG 編輯體驗。
* 記錄文件功能可建立提交資料的防篡改檔案。
* 與 Adob&#x200B;&#x200B;e Sign 整合以進行電子簽名。
* 與 Adob&#x200B;&#x200B;e Workfront Fusion 整合，以便在提交表單時觸發 Adob&#x200B;&#x200B;e Workfront Fusion 情境。
* 與各種資料來源整合，以預先填入表單和提交資料。
* 用來定義資料結構並與各種資料來源互動的表單資料模型 (FDM)。
* 具備能力從多個提交操作中選擇以處理表單提交，包括將資料提交到 Microsoft SharePoint、Microsoft OneDrive、Adobe Workfront Fusion、Salesforce、Microsoft Dynamics 以及更多資料來源。
* 使用Forms提交服務(FSS)或AEM發佈提交動作提交

> **建議**：除非您的團隊是100%以檔案為中心且表單非常基本，否則請使用通用編輯器開始每個新表單專案。


### 檔案式撰寫(使用Microsoft檔案或Google工作表)

檔案式製作最適合使用熟悉的工具(例如Microsoft Word、Google Docs或Google Sheets)來建立簡單、低複雜度的表單。 此方法適用於需要快速且簡單方式建立表單的內容團隊。

* 提供使用者易用體驗的可存取元件。
* 標準化 HTML 結構以呈現一致性。
* 確保資料準確性的規則和驗證。
* 用來收集附加資訊的檔案附件選項。
* 防止垃圾郵件的 Google reCAPTCHA 整合。
* 具備能力以依據特定需求建立自訂表單元件。
* 直接將表單資料提交到 Microsoft Excel 或 Google Sheets 或電子郵件地址。
* 透過操作遙測監視表單效能


### 將Forms內嵌於檔案製作(DA)

檔案製作(DA)是專為建立結構化頁面內容而設計，不支援原生表單建立。 若要將表單新增至DA編寫的頁面，您可以使用&#x200B;**通用編輯器** （建議）或檔案式編寫來建立表單，並將表單內嵌至檔案編寫頁面。

## 發佈Edge Delivery Services Forms {#edge-overview}

下圖說明如何在 Microsoft Excel 或 Google Sheets (文件型編輯) 中編輯表單內容並將其發佈到 Edge Delivery Services。它也會顯示使用AEM Authoring （通用編輯器）的WYSIWYG發佈方法。

![發佈到 Edge Delivery Services 和 AEM](/help/edge/docs/forms/assets/AEM-forms-with-EDS-publishing.png)


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

1. **從通用編輯器開始：**&#x200B;請參閱[通用編輯器快速入門手冊](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)以開始編寫表單。
1. **使用檔案式製作：**&#x200B;若要使用Microsoft Excel或Google工作表建立表單，請遵循[檔案式製作教學課程](/help/edge/docs/forms/tutorial.md)。
1. **在檔案製作中內嵌Forms：**&#x200B;如果您在檔案製作中建置頁面，請使用&#x200B;**通用編輯器** （建議使用）或檔案式製作來建立表單，並將表單內嵌到[DA頁面](https://www.aem.live/developer/da-tutorial)。

您現在已準備好使用AEM Edge Delivery Services建立您的第一個高效能表單。


<!-- 

## Start creating forms

* [Get started with Edge Delivery Services for AEM Forms](/help/edge/docs/forms/tutorial.md)
* [Create a form using Google Sheets or Microsoft Excel](/help/edge/docs/forms/create-forms.md)
* [Set up your Google Sheets or Microsoft Excel files to start accepting data​](/help/edge/docs/forms/submit-forms.md)
* [Publish your form and start collecting data](/help/edge/docs/forms/publish-forms.md)
* [Customize the look of your forms​](/help/edge/docs/forms/style-theme-forms.md)
* [Add repeatable sections to a form​](/help/edge/docs/forms/repeatable-forms.md)
* [Show a custom thank you message after form submission​](/help/edge/docs/forms/thank-you-page-form.md)
* [Adaptive Form Block components and their properties](/help/edge/docs/forms/form-components.md)
* [Real Use Monitoring](https://www.aem.live/developer/rum#authentication)

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