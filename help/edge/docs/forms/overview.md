---
title: AEM Forms Edge Delivery Services 概觀
description: AEM Forms Edge Delivery Services 旨在為實現最佳效而建置，讓您能夠暢想簡化資料收集和使用者參與的未來。
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: 2766a351938062127babb01d5ed35bd37b705c21
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 100%

---

# AEM Forms Edge Delivery Services

AEM Forms Edge Delivery Services 是一組可組合服務，讓環境可以快速進行開發，以利作者迅速更新、發佈並推出新表單。這些服務提供卓越且高影響力的表單體驗，進而促進使用者的參與度和轉換率。這些表單體驗易於製作和開發。

這些服務可讓您：

* **使用您選擇的工具建立註冊體驗**：透過分離內容來源來提高製作效率。您可以開啟立即使用文件型製作 (Microsoft SharePoint 或 Google Drive) 和 WYSIWYG 製作 (通用編輯器或最適化表單編輯器)。您可以在同一個表單網站上使用多個內容來源，並使用您偏好的製作工具，例如 Microsoft Excel、Google Sheets、通用編輯器或最適化表單編輯器。

* **提供卓越的數位註冊體驗：**&#x200B;提供快速載入和呈現的數位註冊體驗，並透過真實使用監控 (RUM) 持續監視您的表單效能。更快的載入時間和最佳化使用者體驗有助於提高表單完成率和轉換率。

* **使用開發人員易用的工具集：**  AEM Forms Edge Delivery Services 使用純 HTML、現代 CSS 和普通 JavaScript來建立卓越的體驗，避免特定框架出現陡峭學習曲線。只要具備基本 Web 開發技能的開發人員，即可自訂並輕鬆建立表單元件和體驗。無需等待管道開始運作，只需將程式碼簽入 GitHub，您進行的變更就會生效。

## AEM Forms Edge Delivery Services 概觀 {#edge-overview}

AEM Forms Edge Delivery 服務讓您在網站上製作表單時更具靈活性。您可使用 [WYSIWYG 製作](/help/forms/creating-adaptive-form-core-components.md)以及[文件型製作](/help/edge/docs/forms/create-forms.md)來製作內容和表單。AEM Forms Edge Delivery Services 會提供一個表單區塊 (名為[最適化表單區塊](/help/edge/docs/forms/create-forms.md)) 以新增表單至您的 Edge Delivery Services 網站。

例如，您直接在 Microsoft Excel 或 Google 工作表中建立表單，這些表格會轉換為您網站的表單。任何新表單或表單內容 )例如新表單欄位) 都可以立即在您的網站上使用，無需進行重新建立的程序。

下圖說明如何在 Microsoft Excel 或 Google Sheets (文件型編輯) 中編輯表單內容並將其發佈到 Edge Delivery Services。下圖還展示了使用 WYSIWYG 製作 (通用編輯器或最適化表單編輯器) 的 AEM 發佈方法。

![發佈到 Edge Delivery Services 和 AEM](/help/edge/docs/forms/assets/AEM-forms-with-EDS-publishing.png)

AEM Forms Edge Delivery Services 使用 GitHub，因此客戶可以直接從其 GitHub 存放庫管理和部署程式碼。例如，您可以在 [Google Sheets](/help/edge/docs/forms/create-forms.md) 或 [Microsoft Excel](/help/edge/docs/forms/create-forms.md) 中編寫表單，並可使用 GitHub 存放庫中的 CSS 和 JavaScript 開發您的表單元件。

當您準備好表單後，您可以使用 [AEM Sidekick](/help/edge/docs/forms/tutorial.md#preview-and-publish-your-content) (chrome 瀏覽器擴充功能) 來預覽和發佈內容更新。

![安裝 AEM SideKick](/help/edge/assets/aem-sidekick-preview-publish-forms.png)

要選擇[文件型製作](#document-based-authoring-features)或 [WYSIWYG 製作](#wysiwyg-authoring-features)，取決於您的特定要求：

* 若只是為了收集幾個欄位的基本資訊的簡單表單 (例如聯絡我們表單、潛在客戶產生表單或服務請求表單)，以及需要使用試算表進行快速資料連接的情況， [文件型製作](#document-based-authoring-features)很適合這類表單使用。您可以像在 Google Sheets 或 Microsoft Excel 中建立文件一樣來建立這些表單。

* 若是複雜的表單，例如需要多個面板、複雜規則和業務邏輯、資料操作、與外部系統整合或使用 AEM 功能來簡化工作流程的表單，那麼 [WYSIWYG 製作](#wysiwyg-authoring-features) 是一個更好的選擇。


### 文件型製作和 WYSIWYG 製作的主要功能

文件型製作提供了一組基本功能，且 WYSIWYG 製作會解鎖文件型製作以外的其他功能，讓您能夠建立更複雜的互動式表單。文件型製作和 WYSIWYG 製作的主要功能包括：

#### 文件型製作功能

文件型製作可讓您以熟悉的工具來建立表單，例如使用 Microsoft Excel 或 Google Sheets 等。這些表單提供以下功能：

* 提供使用者易用體驗的可存取元件。
* 標準化 HTML 結構以呈現一致性。
* 確保資料準確性的規則和驗證。
* 用來收集附加資訊的檔案附件選項。
* 防止垃圾郵件的 Google reCAPTCHA 整合。
* 具備能力以依據特定需求建立自訂表單元件。
* 直接將表單資料提交到 Microsoft Excel 或 Google Sheets 或電子郵件地址。
* 透過真實使用監控 (RUM) 監視您的表單效能

#### WYSIWYG 製作功能

WYSIWYG 製作提供用來建立表單的 WYSIWYG 介面 (通用編輯器或最適化表單編輯器)，並提供文件型製作的所有功能，以及範圍廣泛的附加功能：

* 用來建立複雜邏輯的進階規則編輯器。
* 提供自訂功能的伺服器端可擴充性。
* 可輕鬆建立表單和視覺效果的 WYSIWYG 編輯體驗。
* 記錄文件功能可建立提交資料的防篡改檔案。
* 與 Adob&#x200B;&#x200B;e Sign 整合以進行電子簽名。
* 與 Adob&#x200B;&#x200B;e Workfront Fusion 整合，以便在提交表單時觸發 Adob&#x200B;&#x200B;e Workfront Fusion 情境。
* 與各種資料來源整合，以預先填入表單和提交資料。
* 用來定義資料結構並與各種資料來源互動的表單資料模型 (FDM)。
* 具備能力從多個提交操作中選擇以處理表單提交，包括將資料提交到 Microsoft SharePoint、Microsoft OneDrive、Adobe Workfront Fusion、Salesforce、Microsoft Dynamics 以及更多資料來源。

上述所有功能也可以透過最適化表單編輯器取得。

基本上，WYSIWYG 製作 (通用編輯器和[最適化表單編輯器](/help/forms/creating-adaptive-form-core-components.md)) 是建立在[件型製作](/help/edge/docs/forms/create-forms.md)的基礎上，可提供更進階的工具包來建立以及管理複雜表單。

>[!NOTE]
>
>
> WYSIWYG 製作功能適用於早期採用者計畫。如果您有興趣，請以您的工作電子郵件地址向 aem-forms-ea@adobe.com 發送簡短電子郵件，以要求存取該功能。

### AEM Forms Edge Delivery Services：表單製作、發佈和提交

下面圖表說明使用文件型製作和 WYSIWYG 製作來建立、發佈和提交表單的流程。

![文件型製作 ](/help/edge/assets/document-based-authoring-workflow.png)

![WYSIWYG 製作](/help/edge/assets/wysiwyg-authoring-workflow.png)

## 開始建立表單

* [開始使用 AEM Forms Edge Delivery Services。](/help/edge/docs/forms/tutorial.md)
* [使用 Google Sheets 或 Microsoft Excel 建立表單](/help/edge/docs/forms/create-forms.md)
* [設定您的 Google 表單或 Microsoft Excel 檔案以開始接受資料](/help/edge/docs/forms/submit-forms.md)
* [發佈您的表單並開始收集資料](/help/edge/docs/forms/publish-forms.md)
* [自訂表單的外觀](/help/edge/docs/forms/style-theme-forms.md)
* [將可重複區段新增到表單](/help/edge/docs/forms/repeatable-forms.md)
* [提交表單後顯示自訂感謝訊息](/help/edge/docs/forms/thank-you-page-form.md)
* [最適化表單區塊元件及其屬性](/help/edge/docs/forms/form-components.md)
* [即時使用者監控](https://www.aem.live/developer/rum#authentication)

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