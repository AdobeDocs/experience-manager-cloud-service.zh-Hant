---
title: AEM FormsEdge Delivery Services概觀
description: AEM FormsEdge Delivery Services專為最佳效能而打造，可讓您構想簡化資料收集和使用者參與的未來。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
source-git-commit: bae9a5178c025b3bafa8ac2da75a1203206c16e1
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 0%

---

# AEM FormsEdge Delivery Services

AEM Forms Edge Delivery Services是一組可撰寫的服務，可啟用快速的開發環境，讓作者可以快速更新、發佈和啟動新表單。 這些服務提供卓越且高影響力的表單體驗，可促進參與和轉換。 這些表單體驗易於編寫和開發。

這些服務可讓您：

* **使用您選擇的工具建立註冊體驗：** 透過分離內容來源來提高撰寫效率。 開箱即用地使用檔案式製作(Microsoft SharePoint或Google Drive)和AEM製作(最適化Forms編輯器)。 您可以在相同的表單網站上使用多個內容來源，並使用您偏好的編寫工具，例如Microsoft Excel、Google Sheets或Adaptive Forms Editor。

* **提供卓越的數位註冊體驗：** 提供可快速載入及轉譯的數位註冊體驗。 載入時間更快，使用者體驗最佳化，有助於提高表單完成率和轉換率。

* **使用開發人員友善的工具集：** AEM FormsEdge Delivery Services使用純HTML、現代化CSS和vanilla JavaScript來建立卓越的體驗，避免特定架構的陡峭學習曲線。 具備基本Web開發技能的開發人員可以自訂並輕鬆建置表單元件和體驗。 您不需要等候管道執行，只要將您的程式碼簽入GitHub中，變更即時。

## AEM FormsEdge Delivery Services概觀 {#edge-overview}

AEM Forms Edge Delivery Services可讓您在網站上撰寫表單的方式上擁有高度彈性。 您可以編寫內容和表單，使用 [AEM製作](/help/forms/creating-adaptive-form-core-components.md) 以及 [檔案式製作](/help/edge/docs/forms/create-forms.md). AEM FormsEdge Delivery Services會提供表單區塊，稱為 [最適化Forms區塊](/help/edge/docs/forms/create-forms.md) 以新增表單至您的Edge Delivery Services網站。

例如，您直接在Microsoft Excel或Google工作表中編寫表單，而這些試算表會轉換為您網站的表單。 任何新表單或表單內容（例如新表單欄位）都可立即在您的網站上使用，而無需重新建置流程。

下圖說明如何在Microsoft Excel或Google Sheets （檔案式製作）中編輯表單及發佈至Edge Delivery Services。 它也會顯示使用最適化Forms編輯器(AEM製作)的AEM發佈方法。

![Edge Delivery 架構](/help/edge/assets/AEM-forms-with-EDS-publishing.png)

AEM FormsEdge Delivery Services使用GitHub，因此客戶可以直接從其GitHub存放庫管理和部署程式碼。 例如，您可以用下列方式撰寫表單： [Google工作表](/help/edge/docs/forms/create-forms.md) 或 [Microsoft Excel](/help/edge/docs/forms/create-forms.md) 且可在GitHub存放庫中使用CSS和JavaScript來開發表單的元件。

當您的表單準備就緒時，您可以使用 [AEM Sidekick](/help/edge/docs/forms/tutorial.md#preview-and-publish-your-content)，一種chrome瀏覽器擴充功能，可預覽和發佈內容更新。

![安裝AEM Sidekick](/help/edge/assets/aem-sidekick-preview-publish-forms.png)

選擇 [檔案式製作](#document-based-authoring-features) 和 [AEM製作](#aem-authoring-features) 取決於您的特定需求：

* 對於只收集一些欄位基本資訊的簡單表單（想像一下聯絡我們表單、潛在客戶產生表單或服務請求表單），以及您需要使用試算表快速連線資料的處方， [檔案式製作](#document-based-authoring-features) 非常適合。 您可以建置這些表單，就像在Google Sheets或Microsoft Excel中建置檔案一樣。

* 針對複雜表單，例如需要多個面板、複雜規則和商業邏輯、資料操控、與外部系統整合，或使用AEM功能簡化工作流程的表單，則 [AEM製作](#aem-authoring-features) 是更好的選擇。


### 檔案式撰寫和AEM撰寫的主要功能

檔案式撰寫提供一組基本功能，AEM撰寫開啟了檔案式撰寫以外的其他功能，讓您能夠建立更複雜且互動式的表單。 Document-based Authoring和AEM Authoring的主要功能包括：

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
* 能夠選擇多個提交動作以處理表單提交，包括提交資料至Microsoft SharePoint、Microsoft OneDrive、Adobe Workfront Fusion、Salesforce、Microsoft Dynamics以及其他許多資料來源。

本質上， [AEM製作](/help/forms/creating-adaptive-form-core-components.md) 建立在 [檔案式製作](/help/edge/docs/forms/create-forms.md)，提供更進階的工具組，用於建立和管理複雜的表單。

>[!NOTE]
>
>
> AEM編寫功能可在率先採用者程式中取得。 如果您有興趣，請從您的工作地址快速傳送電子郵件至aem-forms-ea@adobe.com，以請求存取功能。

### AEM FormsEdge Delivery Services：製作。 Forms的發佈與提交

下列圖表說明使用檔案式製作和AEM製作來建立、發佈和提交表單的程式。

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