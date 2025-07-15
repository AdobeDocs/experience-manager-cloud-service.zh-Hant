---
title: AEM Forms 適用的 Edge Delivery Services 概觀
description: 專為實現尖峰效能而設計之 AEM Forms 適用的 Edge Delivery Services，讓您能夠展望未來簡化資料收集和使用者參與的願景。
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: 67fe933807f8a1bca681a6bcee7164f7c117bcac
workflow-type: tm+mt
source-wordcount: '1874'
ht-degree: 100%

---


# 開始使用 AEM Edge Delivery Services 上的 Forms

<span class="preview">這是一項預先發佈功能，可透過我們的[預先發佈管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=zh-hant#new-features)存取。</span>

本指南能協助您了解並使用 Adobe Experience Manager (AEM) Edge Delivery Services (EDS) 實施表單。無論您是建立簡單的聯絡表單還是複雜的資料收集工具，此頁面都能引導您了解您的選項。

## 了解 Edge Delivery Services 中的 Forms

Edge Delivery Services 是 Adobe 用於交付網頁內容 (包括表單) 的現代解決方案，具有卓越的效能和靈敏度。使用 Edge Delivery Services 處理表單，您可以：

* **提供更快的體驗：** Forms 載入速度非常快，因其是由靠近使用者的全域邊緣伺服器 (CDN) 網路所提供。這能提高使用者滿意度且可以提高表單完成率。
* **更輕鬆地更新表單：** Edge Delivery Services 方法通常可以加快開發週期和內容更新，因此您可以快速調整表單。
* **建置現代化的回應式表單：**&#x200B;建立外觀精美且可在任何裝置上順暢運行的表單。
* **受益於擴充性和可靠性：**&#x200B;您的表單將與底層邊緣基礎結構一樣強大且可擴充。

本指南將：

* 說明為 Edge Delivery Sites 建立 (製作) 表單的不同方法。
* 向您展示如何設定使用者提交表單後發生的情況 (提交動作)。
* 協助您根據您的特定需求和團隊技能選擇最佳方法。
* 提供架構圖和最佳做法。

## 您應該知道的重要術語

* **Edge Delivery Services (EDS)：** Adobe 用於透過 CDN 交付 AEM 內容的效能優先架構。也稱為專案 Franklin。
* **AEM Forms：** Adobe 用於建立、管理和處理表單的解決方案。
* **通用編輯器 (UE)：**&#x200B;用於 AEM 內容 (包括表單) 的視覺化所見即所得編輯器。
* **文件型製作：**&#x200B;使用 Microsoft Word 或 Google Docs/Sheets 建立表單。
* **文件製作 (DA)：**&#x200B;一項 Adobe 託管服務，用於為 Edge Delivery Services 製作內容 (包括可託管表單的頁面)。
* **表單提交服務 (FSS)：**&#x200B;一項表單服務，能簡化將表單資料傳送至試算表或電子郵件的過程。
* **AEM Publish 執行個體：**&#x200B;可以處理複雜表單提交的即時 AEM 環境。
* **CORS (跨來源資源共用)：**&#x200B;一項瀏覽器安全性功能，在嵌入來自不同網域的表單時需要進行設定。
* **CDN (內容傳遞網路)：**&#x200B;根據使用者的地理位置快速分發網路內容給使用者的伺服器網路。


**Edge Delivery Services 表單互動概念圖**

<!--  
```mermaid
graph LR
    User[User on Device] >|Interacts| EdgeForm[Edge-Delivered Form Page]
    EdgeForm >|Loads Instantly| CDN[CDN Edge Server]
    CDN >|Serves Content| User
    EdgeForm >|Submits Data| Backend[Backend Processing - e.g. Forms Submission Service / AEM Publish]
    style User fill:#f9f,stroke:#333,stroke-width:2px
    style EdgeForm fill:#ccf,stroke:#333,stroke-width:2px
    style CDN fill:#9cf,stroke:#333,stroke-width:2px
    style Backend fill:#fca,stroke:#333,stroke-width:2px
``` -->

![表單互動](/help/forms/assets/eds-form-interaction.png)
此圖呈現出使用者透過 CDN 快速與所傳送之表單進行互動。其提交的資料隨後由後端系統處理。

## 表單如何在 Edge 上工作？

藉助 EDS，您的網站內容 (包括表單結構) 可以來自各種來源，例如 AEM as a Cloud Service、SharePoint、Google Drive 或文件製作 (DA) 服務。這些內容隨後會發佈至全域 CDN。當使用者造訪您的網站時，內容將直接從最近的 CDN 邊緣伺服器提供，確保達到最快的速度。

<!--*   **Where AEM Forms Fit In**
    Forms in an EDS architecture are designed to be:
    *   **Fast Loading:** Form structures are often simple HTML rendered client-side.
    *   **Decoupled:** The visual part of the form (frontend) is separate from where the data goes after submission (backend).
    *   **Flexible to Create:** You have different tools to build your forms.
    *   **Configurable for Submission:** You can send data to simple services or powerful AEM backends.-->

**透過 Forms 簡化 Edge Delivery Services 架構**

<!--
```mermaid
    graph TD
        UserStart[<img src='https://img.icons8.com/ios-filled/50/000000/user.png' width='30' /> User on Device] >|Interacts| EdgeForm[Edge-Delivered Form Page]
        EdgeForm >|Loads Instantly| CDN[CDN Edge Server]
        CDN >|Serves Content| UserEnd[<img src='https://img.icons8.com/ios-filled/50/000000/user.png' width='30' /> User on Device]
        EdgeForm >|Submits Data| Backend[Backend Processing - Form Submission Service / AEM Publish]

        style UserStart fill:#f9f,stroke:#333,stroke-width:2px
        style UserEnd fill:#f9f,stroke:#333,stroke-width:2px
        style EdgeForm fill:#ccf,stroke:#333,stroke-width:2px
        style CDN fill:#9cf,stroke:#333,stroke-width:2px
        style Backend fill:#fca,stroke:#333,stroke-width:2px
``` -->

![架構](/help/forms/assets/eds-simplified-architecture.png)
此圖呈現出整個歷程：表單在製作系統中定義、發佈至邊緣、提供給使用者，而所提交的資料由後端處理。

## 選擇表單製作方法

您可以透過三種主要方式為您的 Edge Delivery Services 網站建立表單。您的選擇會取決於您團隊的技能、表單的複雜性，以及您的專案需求。

### 哪種製作方法適合您？

使用此決策樹來幫助您選擇：

**表單製作決策樹**
<!--    
```mermaid
    graph TD
        A{Start: I need to create a form for an Edge Delivery Services site} > B{What are my team's primary content creation tools & skills?}
        B -- "We mainly use Word / Google Docs / Sheets" > C{How complex is the form and where does the data need to go?}
        B -- "We use AEM and prefer visual tools (Marketers or Designers)" > D[Use Universal Editor - WYSIWYG]
        B -- "Our site content is managed in Document Authoring (DA)" > E[Use Document Authoring - Embed Forms]
        C -- "Simple to moderate form, data to a spreadsheet or email" > F[Use Document-Based Authoring]
        C -- "More complex logic or needs AEM backend integration" > D
        E > G[Create form using Document-Based Authoring or Universal Editor, then embed in your DA page]

        style A fill:#f9f,stroke:#333,stroke-width:2px
        style F fill:#ccf,stroke:#333,stroke-width:2px
        style D fill:#ccf,stroke:#333,stroke-width:2px
        style G fill:#ccf,stroke:#333,stroke-width:2px
``` -->

![選取正確的平台](/help/forms/assets/eds-authoring-selection.png)

此決策樹能協助您根據團隊和表單需求選取製作方法。

### 使用文件建立表單 (Word/Google Docs)

如果您的[團隊熟悉 Microsoft Word 或 Google Docs/Sheets，則此方法非常適合快速建立表單](/help/edge/docs/forms/create-forms.md)。

**運作原理：從文件到網頁表單**

您可以使用特殊表格格式或「表單區塊」直接在 Word 文件或 Google Sheet 中定義表單的欄位、標籤和類型。當您發佈此文件時，Edge Delivery Services 會自動將其轉換為適合網頁的 HTML 表單，讓使用者可以在您的網站上與之互動。

**功能與特性**

* 使用熟悉的工具進行製作：Word、Google Docs、Google Sheets。
* 定義欄位：文字輸入、電子郵件、下拉式選單、核取方塊、選項按鈕、文字區域。
* 新增標籤、預留位置和輔助訊息。
* 設定基本驗證規則：必填欄位、電子郵件格式。
* 整合 reCAPTCHA，防止垃圾資訊。
* 允許檔案上傳。
* 立即發佈：文件中的變更會快速地反映在即時網站上。
* 使用自訂程式碼進行擴充：進階使用者可以透過 GitHub 新增自訂表單元件和樣式。

**考量事項**

* 您的團隊定期使用 Word 或 Google Docs/Sheets 處理內容。
* 您需要快速建立簡單到中等複雜程度的表單。
* 您希望以最少的設定將表單資料直接傳送至試算表或電子郵件地址。

**提交的運作方式 (主要為表單提交服務)**

以此方式建立的表單通常會[將其資料傳送至 AEM 表單提交服務](/help/forms/forms-submission-service.md)。您可以對其進行設定 (通常在來源文件本身內)，藉以將資料傳送至 Google Sheet、OneDrive/SharePoint 上的 Excel 檔案或做為電子郵件。

**文件型製作概念**
<!--    
```mermaid
    graph LR
        subgraph Authoring["You define your form in a Google Sheet or Word Document"]
        Sheet[Spreadsheet or Document with field definitions:\nField Name - Type - Label\nemail - email - Email Address\nmessage - textarea - Your Message]
    end

        Sheet >|Edge Delivery Services automatically converts it| JSON[Internal Form Definition as JSON]
    JSON >|A 'Form Block' on your page renders it as| HTMLForm[Live HTML Form on Your Website]

        style Sheet fill:#e6ffe6,stroke:#333
        style JSON fill:#e6e6ff,stroke:#333
        style HTMLForm fill:#ffe6e6,stroke:#333
```-->

![文件型](/help/forms/assets/eds-doc-based.png)
此圖呈現出文件所定義的表單如何成為即時網頁表單。

### 使用通用編輯器將表單視覺化

[通用編輯器](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)提供現代化的拖放介面，可直接在您的網頁瀏覽器中建立表單。

**運作原理：拖放表單建置**

您使用視覺化介面將表單元件 (像是輸入欄位、按鈕、下拉式選單) 拖曳到頁面上。然後您可以透過屬性面板設定每個元件的屬性 (標籤、驗證等)。通用編輯器會向您顯示表單的即時預覽。

**功能與特性**

* 使用預先建立元件資料庫建立視覺化表單。
* 設定即時驗證和商業邏輯 (例如，根據所選取之內容顯示/隱藏欄位)。
* 查看不同裝置 (桌上型電腦、行動裝置) 的即時預覽。
* 與 AEM 功能 (如內容片段、AEM 工作流程和使用者權限) 整合。
* 使用「體驗建立工具」取得 AI 協助，根據提示建立或編輯表單。

**考量事項**

* 您需要使用條件邏輯、多步驟面板或個人化來建置複雜的表單。
* 您的團隊 (例如，行銷人員、商業使用者) 更偏好視覺化工具。
* 您需要與 AEM as a Cloud Service 緊密整合，藉以實現治理、工作流程，或在表單中使用 AEM 資產。

**提交的運作方式 (表單提交服務或 AEM Publish)**

以通用編輯器建置的表單可以：

* 使用簡單的[表單提交服務](/help/forms/forms-submission-service.md) (用於將資料傳送至試算表或電子郵件)。
* 將資料提交至您的 AEM Publish 執行個體，進行更進階的處理 (例如啟動 AEM 工作流程、使用表單資料模型或與其他企業系統整合)。

**通用編輯器概念**

<!--    
```mermaid
    graph TD
    subgraph UE_Interface["Universal Editor Interface in your Browser"]
        Toolbar[Editor Toolbar and Asset Finder]
        Canvas[Your Page with the Form Being Built]
        ComponentPalette[Available Form Components:\nInput / Dropdown / Button\nDrag and drop]
        PropertiesPanel[Configure Selected Component:\nLabel / Validation / Rules]
    end
    ComponentPalette >|Drag & Drop onto| Canvas
    Canvas >|Select a component to edit its| PropertiesPanel
    UE_Interface >|Creates| RenderedForm[Live Form on Your Website]

    style UE_Interface fill:#f0f8ff,stroke:#333
    style RenderedForm fill:#ffe6e6,stroke:#333
```-->

![通用編輯器](/help/forms/assets/eds-ue-based.png)

此圖呈現出用於表單建置之通用編輯器的主要部分。

### 搭配文件製作 (DA) 使用 Forms

[文件製作 (DA)](https://www.aem.live/developer/da-tutorial) 是一項 Adobe 託管服務，用於建立和管理將透過 Edge Delivery Services 交付的主要網站內容 (頁面、文章)。這是使用 SharePoint 或 Google Drive 做為 Edge Delivery Services 來源內容的替代方法。

**了解 Edge Delivery Services 內容的文件製作 (DA)**

文件製作使用 Adobe 的設計系統 (Spectrum) 和 AEM 的文件模型 (Blocks、Sections)，提供企業級創作環境。其是針對 EDS 的結構化內容管理而設計的。

**DA 如何處理表單 (嵌入，而非直接製作)**

DA 本身即&#x200B;**非從頭開始建置表單的工具**。相反地，使用 DA 建立網頁，然後將使用文件型製作或通用編輯器所建立的表單&#x200B;*嵌入*&#x200B;至那些以 DA 製作的頁面中。

**將表單嵌入至 DA 頁面的步驟**

1. **建立表單：**&#x200B;使用以下任一方式建置表單：
   * 文件型製作 (Word/Google Docs)
   * 通用編輯器

1. **發佈表單：**&#x200B;確保此表單已發佈，且可透過其自己的 Edge Delivery URL (例如，`https://your-eds-project.hlx.page/forms/contact-us`) 進行存取。
1. **在 DA 中製作您的頁面：**&#x200B;在文件製作中建立或編輯您希望表單出現的頁面。
1. **嵌入表單：**&#x200B;使用 DA 頁面中的特定「區塊」或元件，自其 URL 參照和嵌入表單。然後 DA 頁面便會取得並顯示這個外部建立的表單。

**使用嵌入式表單製作文件**
<!--
```mermaid
    graph TD
    subgraph FormCreation["1. Create Form using other methods"]
        UE_Form[Universal Editor Form] >|Published to| FormLocation[Form lives at its own Edge Delivery Services URL:\nfor example: /forms/my-contact-form]
        DocBased_Form[Document-Based Form] >|Published to| FormLocation
    end

    subgraph DA_Content["2. Author Page in Document Authoring"]
        DAPage[Your Web Page Authored in DA\nExample: /main-site/landing-page]
        EmbedBlock[On DA Page, add 'Embed Form' Block\nPoints to /forms/my-contact-form]
    end

    DAPage > EmbedBlock
    User[User visits your DA Page] > DAPage
    EmbedBlock >|DA Page fetches and displays| FormLocation[The Form appears on your DA Page]

    style FormCreation fill:#e6ffe6,stroke:#333
    style DA_Content fill:#ffe6cc,stroke:#333
    style FormLocation fill:#ccf,stroke:#333
```-->

![文件製作](/help/forms/assets/eds-da-based.png)

此圖呈現出您首先使用 UE 或 Docs 建立表單，然後將其嵌入至您在文件製作中所建立的頁面內。


### 比較製作選項

| 條件 | 文件型製作 | 通用編輯器 (WYSIWYG) | 文件製作 (DA) 中的表單 |
|----------------------------------|---------------------------------------|-----------------------------------------|-------------------------------------------|
| **主要製作工具** | Word/Google Docs/Sheets | 瀏覽器 (AEM 通用編輯器) | 不適用 (表單&#x200B;*已嵌入*) |
| **團隊技能等級** | 熟悉文件編輯器 | 熟悉視覺化網路工具 | 使用 DA 取得頁面內容 |
| **典型的表單複雜性** | 簡單到中等 | 中等到複雜，企業級 | 取決於嵌入的表單 |
| **提交選項 1 (簡單)** | 表單提交服務 (至 Sheet/電子郵件) | 表單提交服務 (至 Sheet/電子郵件) | 遵循嵌入式表單的設定 |
| **提交選項 2 (進階)** | 不適用 | AEM Publish (工作流程、FDM 等) | 遵循嵌入式表單的設定 |
| **AEM 後端整合** | 最小 | 高 (搭配 AEM Publish 提交) | 間接，透過嵌入的通用編輯器表單 |
| **最適合** | 內容團隊快速建立簡單表單、快速擷取資料。 | 行銷人員、需要視覺化控制、複雜表單或深度 AEM 整合的商業使用者。 | 主要內容在 DA 中進行管理的網站，需要來自其他來源的表單。 |

**增強的決策樹**
<!--
```mermaid
    graph TD
    A{Start Here: I need a form on my Edge Delivery Services Site} > B{What's my team's main authoring tool & skill for form content?};
    B -- "Word/Google Docs" > C{How complex is the form & data destination?};
    C -- "Simple form, data to Sheet/Email" > Sol1[CHOOSE: Document-Based Authoring + Forms Submission Service];
    C -- "Needs more logic OR AEM backend\nlike Workflow or FDM" > Sol2[CONSIDER: Can Universal Editor meet this need better?];

    B -- "AEM User / Visual Editor needed\nMarketer or Designer" > D{Where does the form data need to go?};
    D -- "Simple - to Sheet/Email" > Sol3[CHOOSE: Universal Editor + Forms Submission Service];
    D -- "Advanced - AEM Workflow, FDM,\n3rd Party via AEM" > Sol4[CHOOSE: Universal Editor + AEM Publish Submissions\nRequires additional setup];

    B -- "Our main site content is in Document Authoring (DA)" > Sol5[STRATEGY: Author form using Sol1, Sol2, Sol3 or Sol4 first\nTHEN embed that form into your DA page];

    A > F{Will this form be embedded or fetched from another site or domain?};
    F -- "Yes" > G[IMPORTANT: Configure CORS on the site hosting the form.\nEnsure any form JavaScript blocks are available where the form is displayed];

    style Sol1 fill:#90ee90,stroke:#333
    style Sol2 fill:#fffacd,stroke:#333
    style Sol3 fill:#90ee90,stroke:#333
    style Sol4 fill:#90ee90,stroke:#333
    style Sol5 fill:#add8e6,stroke:#333
    style G fill:#ffb6c1,stroke:#333
```-->

![決策樹](/help/forms/assets/eds-enhanced-decision.png)

## 製作方法的功能比較

下表詳細比較不同 AEM 表單編寫方法的重要功能，協助您選擇最符合需求的方式。&#x200B;

| **功能** | **通用編輯器 (WYSIWYG)** | **文件型編寫** | **文件製作 (DA)** |
|-----------------------------------------|-------------------------------|-----------------------------|-----------------------------|
| **使用 Sites 統一構成** | ✅ |                              | ✅ (搭配嵌入式表單) |
| **嵌入表單支援** | ✅ | ✅ | ✅ (從通用編輯器或 Docs 嵌入) |
| **規則 (動態行為)** | 具有自訂功能的進階規則編輯器 | 受限：顯示/隱藏、運算值、自訂函數 | 取決於嵌入形式 |
| **附件支援** | ✅ | ℹ️ (搶先體驗) | 取決於嵌入形式 |
| **驗證碼支援** | reCAPTCHA Enterprise | reCAPTCHA Enterprise | 取決於嵌入形式 |
| **提交功能** | REST、電子郵件、FDM、工作流程、SharePoint、OneDrive、Azure Blob、Power Automate、Workfront Fusion (EA) | 僅限試算表 | 遵循嵌入式表單的設定 |
| **資料結構描述** | FDM、自訂 | 自訂 | 根據嵌入式表單 |
| **預填** | 💡 (透過精靈) | ✅ | 取決於嵌入形式 |
| **片段** | ✅ | ✅ | 取決於嵌入形式 |
| **視覺化規則編輯器** | ✅ |                              |                              |
| **本地化** | 💡 (透過 Sites) | ℹ️ (Excel/Sheets 手冊) | 取決於嵌入形式 |
| **資料結構描述 (資料樹)** | 💡 (透過使用者介面擴充功能) |                              |                              |
| **範本支援** | 僅限初始內容 |                              |                              |
| **入口網站** |                               |                              |                              |
| **主題** | ℹ️ (在專案層級) | ℹ️ (在專案層級) | ℹ️ (根據託管網站) |
| **自訂元件** | ✅ | ✅ | ✅ (若支援嵌入式元件) |
| **OOTB 與自訂函數** | ✅ | ✅ | ✅ (嵌入形式) |
| **片段參考** |                               |                              |                              |
| **簽署整合** |                               |                              |                              |
| **實驗** | ✅ | ✅ | 取決於嵌入上下文 |
| **透過 Workfront 管理任務** | ✅ |                              |                              |
| **個人化擴充功能** | 💡 |                              |                              |
| **編輯器自訂** | ✅ (透過使用者介面擴充功能) |                              |                              |
| **提交動作** | ✅ | 僅限試算表 | 根據嵌入式表單 |

<!--

## Best Practices for Creating Forms

Building great forms goes beyond just the technology. Here's how to ensure your forms are user-friendly and achieve their goals:

* **Designing User-Friendly and Accessible Forms**

  *   **Use Clear, Visible Labels:** Every form field needs a `<label>`. Don't rely only on placeholder text (text inside the input field), as it disappears when users type and is bad for accessibility.
        *   *Good:* `<label for="email">Email Address:</label> <input type="email" id="email" placeholder="you@example.com">`
        *   *Bad:* `<input type="email" placeholder="Email Address">`
  *   **Keep it Simple:** Use standard HTML input types (`<input type="date">`, `<input type="tel">`) where possible. They often have better mobile support and accessibility than complex custom widgets.
  *   **Logical Order and Grouping:** Arrange fields in a way that makes sense to the user. Group related fields together using `<fieldset>` and `<legend>`.
  *   **Provide Clear Instructions:** For any fields that might be confusing, offer concise help text or tooltips.
  *   **Keyboard Navigation:** Ensure users can navigate through your entire form using only the keyboard (Tab, Shift+Tab, Enter, Spacebar).
  *   **Error Handling:** Make errors obvious and easy to correct. Display error messages next to the relevant field and explain what needs to be fixed.

* **Ensuring Your Forms Load Quickly and Are Visible**

  *   **Place Forms Prominently:** If a form is important, make sure users can see it easily without too much scrolling ("above the fold" if possible). Adobe's research shows many forms get low interaction because they are hidden.
  *   **Optimize Assets:** Keep any custom JavaScript or CSS for your forms as small as possible to ensure fast load times. Edge Delivery Services helps with the base page load, but heavy form scripts can still slow things down.

* **Handling User Data Responsibly**
  *   **Ask Only What You Need:** The less Personal Identifiable Information (PII) you ask for, the better. Every field is a potential reason for a user to abandon the form.
  *   **Be Transparent:** Clearly explain *why* you need certain information and *how it will be used*. Link to your privacy policy. This builds trust.

* **Improving User Experience: Captcha Alternatives**

  * **Rethink Visible Captchas:** Those "type the wavy text" or "click all the traffic lights" tests can be very frustrating for users, especially those with disabilities, and often lead to high drop-off rates.

*   **Consider Alternatives:**
    *   **Honeypot Fields:** Add a hidden field that only bots would fill out. If it has data, the submission is likely spam.
    *   **Time-Based Checks:** Measure how quickly a form is submitted. Submissions that are too fast are often bots.
    *   **Invisible reCAPTCHA (v3):** This Google service analyzes user behavior in the background and only presents a challenge if the user seems suspicious. This is often a much better user experience.

**Form Design Do's and Don'ts**

```mermaid
    graph LR
subgraph GoodFormUX [Do ✅ - For Better Forms]
    direction LR
    ClearLabels[Use Visible <label> Tags for All Fields]
    SimpleInputs[Prefer Standard HTML Input Types]
    KeyboardNav[Ensure Full Keyboard Navigation]
    ClearErrors[Show Clear, Actionable Error Messages]
    MinimalPII[Ask Only for Necessary Information]
    TransparentUse[Explain How Data is Used - Privacy Info]
    InvisibleCaptcha[Use Invisible or Behavioral CAPTCHA]
    ProminentPlacement[Make Form Easy to Find on Page]
end

subgraph BadFormUX [Don't ❌ - Avoid These]
    direction LR
    PlaceholderOnly[Only Use Placeholder Text for Labels]
    ComplexWidgets[Use Overly Complex Custom Widgets]
    PoorErrors[Vague or Missing Error Messages]
    ExcessivePII[Request Excessive Personal Data]
    VisibleHardCaptcha[Use Hard-to-Solve Visible CAPTCHAs]
    HiddenForm[Hide the Form Deep in the Page]
end

style GoodFormUX fill:#e6ffe6,stroke:#333
style BadFormUX fill:#ffe6e6,stroke:#333
```

## Quick Decision Guide: Choosing the Right Form Strategy

Let's bring it all together to help you decide on the best approach for your forms.

*   **Matching Form Features to Your Project Goals**
    *   **For speed and simplicity with basic data capture (to spreadsheets/email):** Document-Based Authoring with the Forms Submission Service is often your fastest route.
    *   **For visually rich forms with potential for AEM backend integration:** Universal Editor is your tool. You can start with the Forms Submission Service for simple needs and scale to full AEM Publish submissions for complex workflows.
    *   **If your site content is managed in Document Authoring (DA):** You'll create forms using one of the above methods and then embed them into your DA pages. The submission logic will be tied to how the original embedded form was configured.-->

若要在已了解的基礎上更進一步，您可以按照以下方法繼續深入：

[選擇您的提交策略](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)決定您的專案是否需要表單提交服務的簡單性 (適合試算表/電子郵件輸出) 或 AEM Publish 提交動作所提供的靈活性和後端整合。

請參閱[建立表單的最佳做法](/help/edge/docs/forms/universal-editor/best-pratices-eds-forms.md)文章，了解如何設計有效、易於存取且使用者友善的表單。

## 後續步驟

本指南的內容概述了如何搭配 AEM Edge Delivery Services 使用表單。有關具體設定的更詳細逐步說明，請參閱 Adobe Experience Manager 官方文件：

* [文件型製作與 Edge Delivery Services 表單](/help/edge/docs/forms/tutorial.md)
* [通用編輯器與 Edge Delivery Services 表單](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
* [文件製作 (DA) 和嵌入內容](https://www.aem.live/developer/da-tutorial)
* [AEM 表單提交服務](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)


<!-- 
# Edge Delivery Services for AEM Forms
 

Edge Delivery Services for AEM Forms is a composable set of services that enables a rapid development environment where authors can update, publish, and launch new forms rapidly. These services deliver exceptional and high impact forms experiences that drive engagement and conversions. These forms experiences are easy to author and develop.

These services enable you to:

* **Create enrolment experiences with tools of your choice:** Increase authoring efficiency by decoupling content sources. Out of the box you can use Document-based Authoring (Microsoft SharePoint or Google Drive), WYSIWYG Authoring (Universal Editor or Adaptive Forms Editor). You can work with multiple content sources on the same forms site and use your preferred authoring tools, such as Microsoft Excel, Google Sheets, Universal Editor, or Adaptive Forms Editor.

* **Deliver exceptional Digital Enrolment experiences:** Deliver Digital Enrolment experiences that load and render quickly and continuously monitor your forms performance through Operational Telemetry. Faster loading times and optimized user experience contribute to higher form completion and conversion rates. 

* **Use developer friendly toolset:** Edge Delivery Services for AEM Forms
 uses plain HTML, modern CSS, and vanilla JavaScript to create exceptional experiences, avoiding the steep learning curve of a specific framework. A developer with basic web development skills can customize and easily build form components and experiences. There is no need to wait for a pipeline to run, just check-in your code into GitHub and your changes are live.

## Edge Delivery Services for AEM Forms Overview {#edge-overview}

Edge Delivery Services for AEM Forms allows for a high degree of flexibility in how you author forms on your website. You can author content and forms with [WYSIWYG Authoring](/help/forms/creating-adaptive-form-core-components.md) as well as [Document-based Authoring](/help/edge/docs/forms/create-forms.md). Edge Delivery Services for AEM Forms
 provide a forms block, known as [Adaptive Forms Block](/help/edge/docs/forms/create-forms.md) to add a form to your Edge Delivery Services site.

For example, you author forms directly in Microsoft Excel or Google Sheets and these spreadsheets are transformed into forms for your website. Any new form or form content, such as a new form field, is instantly available on your website without requiring a rebuild process.

The following diagram illustrates how you can edit forms in Microsoft Excel or Google Sheets (Document-based Authoring) and publish to Edge Delivery Services. It also shows the AEM publishing method using the WYSIWYG Authoring (Universal Editor or Adaptive Forms Editor).

![Publish to Edge Delivery Services and AEM](/help/edge/docs/forms/assets/AEM-forms-with-EDS-publishing.png)

Edge Delivery Services for AEM Forms uses GitHub so customers can manage and deploy code directly from their GitHub repository. For example, you can write forms in either [Google Sheets](/help/edge/docs/forms/create-forms.md) or [Microsoft Excel](/help/edge/docs/forms/create-forms.md) and the components of your forms can be developed by using CSS and JavaScript in a GitHub repository.

When your forms are ready, you can use the [AEM Sidekick](/help/edge/docs/forms/tutorial.md#preview-and-publish-your-content), a chrome browser extension, to preview and publish content updates.

![Install AEM SideKick](/help/edge/assets/aem-sidekick-preview-publish-forms.png)

The choice between the [Document-based Authoring ](#document-based-authoring-features) and [WYSIWYG Authoring](#wysiwyg-authoring-features) depends on your specific requirements:

* For simple forms that just collect basic information with a few fields (think contact us forms, lead generation forms, or service request forms), and where you need quick data connectivity using a spreadsheet, the [Document-based Authoring](#document-based-authoring-features) is a good fit. You can build these forms like you would build a document in Google Sheets or Microsoft Excel. 

* For complex forms, like forms requiring multiple panels, complex rules and business logic, data manipulation, integration with external systems, or streamlined workflows using AEM features, then [WYSIWYG Authoring](#wysiwyg-authoring-features) is a better option. 


### Key Features of Document-based Authoring and WYSIWYG Authoring

Document-based Authoring offers a basic set of features and WYSIWYG Authoring unlocks additional capabilities beyond the Document-based Authoring, empowering you to build more complex and interactive forms. The key features of both Document-based Authoring and WYSIWYG Authoring are:

#### Document-based Authoring features

Document-based Authoring  allows you to create forms using familiar tools like Microsoft Excel or Google Sheets. These forms offer the following functionalities:

* Accessible components for a user-friendly experience.
* Standardized HTML structure for consistent rendering.
* Rules and validations to ensure data accuracy.
* File attachment options for collecting additional information.
* Google reCAPTCHA integration for spam protection.
* Ability to create custom form components for specific needs.
* Submit form data directly to Microsoft Excel or Google Sheets or email addresses.
* Monitor your forms performance through Operational Telemetry

#### WYSIWYG Authoring features

WYSIWYG Authoring provides WYSIWYG interfaces (Universal Editor and Adaptive Forms Editor) for building forms and offers all the capabilities of Document-based Authoring, plus a wide range of additional features:

* Advanced rules editor for creating complex logic.
* Server-side extensibility for custom functionalities.
* WYSIWYG editing experience for easy form creation and visualization.
* Document of record functionality to create tamper-proof archives of submitted data.
* Integration with Adobe Sign for electronic signatures.
* Integration with Adobe Workfront Fusion to triggering Adobe Workfront Fusion scenarios upon form submission.
* Integration with various data sources for pre-populating forms and submitting data.
* Form Data Model (FDM) for defining data structure and interactions with various data sources.
* Ability to choose from multiple submit actions for handling form submissions, including submitting data to Microsoft SharePoint, Microsoft OneDrive, Adobe Workfront Fusion, Salesforce, Microsoft Dynamics, many more data sources.

The all above features are also available via Adaptive Forms Editor. 

In essence, WYSIWYG Authoring (Universal Editor and [Adaptive Forms Editor](/help/forms/creating-adaptive-form-core-components.md)) builds upon the foundation of [Document-based Authoring](/help/edge/docs/forms/create-forms.md), providing a more advanced toolkit for creating and managing complex forms. 

>[!NOTE]
>
>
> The WYSIWYG Authoring capability is available under the early-adopter program. If you are interested, send a quick email from your work address to aem-forms-ea@adobe.com to request access to the capability.

### Edge Delivery Services for AEM Forms

: Authoring, Publishing, and Submission of Forms  

The following diagrams illustrate the process of creating, publishing, and submitting forms using Document-based Authoring and WYSIWYG Authoring.

![Document-based Authoring](/help/edge/assets/document-based-authoring-workflow.png)

![WYSIWYG Authoring](/help/edge/assets/wysiwyg-authoring-workflow.png)

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
            <img src="/help/edge/assets/smock_devices_18_n.svg" alt="Create a form using Edge Delivery Services forms" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Create a form using Google Sheets or Microsoft Excel</b>
        </a>
        <p>Create forms that load and render quickly and automatically reflows on mobile devices.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   
            <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="Submit form" alt="Use Form Fragments in an Edge Delivery Services Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Submit form to spreadsheet</b>
        </a>
        <p>Submit forms directly to your Microsoft Excel or Google Sheets.</p>
    </div>
     <div class="card-container">
        <a href="/help/edge/docs/forms/style-theme-forms.md">
            <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="Apply styles or themes to an Edge Delivery Services form" style="border-radius: 5px;"> </b>
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
            <img src="/help/edge/assets/smock_abc_18_n.svg" alt="Translate an Edge Delivery Services Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Translate a form</b>
        </a>
        <p>Extend the reach of your forms while keeping costs in check.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/repeatable-forms.md">  
            <img src="/help/edge/assets/smock_addto_18_n.svg" alt="Add repeatable sections to an Edge Delivery Services Form" style="border-radius: 5px;"> </b>
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
            <img src="/help//edge/assets/smock_keyclock_18_n.svg" alt="Use reCAPTCHA in an Edge Delivery Services Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Use reCAPTCHA</b>
        </a>
        <p>Use OOTB reCAPTCHA integration for robust spam and bot protection.</p>
    </div>


</div>


</br>


-->
