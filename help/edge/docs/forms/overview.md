---
title: AEM Forms 適用的 Edge Delivery Services 概觀
description: 適用於AEM Forms的Edge Delivery Services專為最佳效能而打造，可讓您構想簡化資料收集和使用者參與的未來。
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: bca160763fdd1e96f1350ac74eb76ff7c26ac00b
workflow-type: tm+mt
source-wordcount: '1874'
ht-degree: 7%

---


# AEM Edge Delivery Services上的Forms快速入門

<span class="preview">這是一項預先發佈功能，可透過我們的[預先發佈管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=zh-Hant#new-features)存取。</span>

本指南可協助您使用Adobe Experience Manager (AEM) Edge Delivery Services (EDS)來瞭解及實作表單。 無論您是要建立簡單的連絡人表單還是複雜的資料收集工具，本頁都會逐步說明您的選項。

## 瞭解Edge Delivery Services中的Forms

Edge Delivery Services是Adobe的現代化解決方案，可提供卓越效能和靈活性的網路內容（包括表單）。 若您在表單中使用Edge Delivery Services，您可以：

* **提供更快速的體驗：** Forms載入速度驚人，因為服務是由鄰近您使用者的全球邊緣伺服器(CDN)網路所提供。 這麼做可改善使用者滿意度，並提高表單完成率。
* **更輕鬆地更新Forms：** Edge Delivery Services方法通常可讓您更快的開發週期和內容更新，因此您可以快速調整表單。
* **建置回應式現代化Forms：**&#x200B;建立在任何裝置上都能完美運作且外觀流暢的表單。
* **受益於擴充性與可靠性：**&#x200B;您的表單將像基礎邊緣基礎架構一樣強大且可擴充。

本指南將：

* 說明您為Edge Delivery Sites建立（製作）表單的各種方式。
* 顯示如何設定使用者提交表單（提交動作）後會發生什麼情況。
* 協助您根據特定需求和團隊技能選擇最佳方法。
* 提供架構圖表和最佳實務。

## 您應瞭解的重要條款

* **Edge Delivery Services (EDS)：** Adobe透過CDN傳遞AEM內容的效能優先架構。 也稱為Project Franklin。
* **AEM Forms：** Adobe建立、管理及處理表單的解決方案。
* **通用編輯器(UE)：**&#x200B;適用於AEM內容（包括表單）的視覺化WYSIWYG編輯器。
* **檔案式製作：**&#x200B;使用Microsoft Word或Google Docs/工作表建立表單。
* **檔案製作(DA)：** Adobe代管服務，用於為Edge Delivery Services製作內容（包括可以代管表單的頁面）。
* **Forms提交服務(FSS)：**&#x200B;簡化將表單資料傳送到試算表或電子郵件的Adobe服務。
* **AEM發佈執行個體：**&#x200B;可處理複雜表單提交的即時AEM環境。
* **CORS （跨原始資源共用）：**&#x200B;當內嵌來自不同網域的表單時，需要設定的瀏覽器安全性功能。
* **CDN （內容傳遞網路）：**&#x200B;伺服器網路，可依據使用者的地理位置，將網頁內容快速提供給使用者。


**Edge Delivery Services表單互動的概念圖**

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
此圖表顯示使用者與透過CDN快速傳送的表單互動的情形。 然後後端系統會處理這些使用者提交的資料。

## Forms如何在Edge上運作？

有了EDS，您的網站內容（包括表單結構）可以源自各種來源，例如AEM as a Cloud Service、SharePoint、Google Drive或檔案編寫(DA)服務。 然後，此內容會發佈至全域CDN。 當使用者造訪您的網站時，會直接從最近的CDN邊緣伺服器提供內容，以確保最高速度。

<!--*   **Where AEM Forms Fit In**
    Forms in an EDS architecture are designed to be:
    *   **Fast Loading:** Form structures are often simple HTML rendered client-side.
    *   **Decoupled:** The visual part of the form (frontend) is separate from where the data goes after submission (backend).
    *   **Flexible to Create:** You have different tools to build your forms.
    *   **Configurable for Submission:** You can send data to simple services or powerful AEM backends.-->

**簡化的Edge Delivery Services架構搭配Forms**

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
此圖表顯示歷程：表單定義於編寫系統中，發佈至邊緣，提供給使用者，且提交的資料由後端處理。

## 選擇您的表單撰寫方法

您有三種主要方法可為Edge Delivery Services網站建立表單。 您的選擇將取決於您團隊的技能、表單的複雜度以及您的專案需求。

### 哪一種撰寫方法適合您？

使用此決策樹可協助您選擇：

**表單編寫決策樹**
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

此決策樹可協助您根據團隊和表單需求選擇撰寫方法。

### 使用檔案建立Forms (Word/Google Docs)

如果您的團隊熟悉Microsoft Word或Google Docs/工作表[，此方法非常適合快速](/help/edge/docs/forms/create-forms.md)建立表單。

**運作方式：從檔案到網頁表單**

您可以使用特殊表格格式或「表格區塊」，直接在Word檔案或Google工作表定義表格的欄位、標籤和型別。 當您發佈此檔案時，Edge Delivery Services會自動將其轉換為可於網路使用的HTML表單，使用者可在您的網站上與其互動。

**功能與功能**

* 在熟悉的工具中撰寫：Word、Google Docs、Google Sheets。
* 定義欄位：文字輸入、電子郵件、下拉選單、核取方塊、選項按鈕、文字區域。
* 新增標籤、預留位置及說明訊息。
* 設定基本驗證規則：必填欄位、電子郵件格式。
* 整合reCAPTCHA以保護垃圾郵件。
* 允許檔案上傳。
* 立即發佈：檔案中的變更會快速反映在已上線的網站上。
* 使用自訂程式碼擴充：進階使用者可以透過GitHub新增自訂表單元件和樣式。

**考量事項**

* 您的團隊會定期使用Word或Google Docs/工作表作為內容。
* 您需要快速建立從簡單到中等複雜的表單。
* 您想要以最小的設定將表單資料直接傳送至試算表或電子郵件地址。

**提交如何運作(主要是Forms提交服務)**

Forms通常以這種方式[將其資料傳送至AEM Forms提交服務](/help/forms/forms-submission-service.md)。 您將進行此設定（通常在來原始檔本身中）以將資料傳送至Google工作表、OneDrive/SharePoint上的Excel檔案或電子郵件。

**檔案式編寫概念**
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

![基於檔案](/help/forms/assets/eds-doc-based.png)
此圖表顯示檔案中定義的表單如何變成即時Web表單。

### 使用Universal Editor以視覺化方式顯示Forms

[通用編輯器](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)提供現代的拖放介面，可直接在網頁瀏覽器中建立表單。

**運作方式：以拖放方式建立表單**

您使用視覺介面將表單元件（如輸入欄位、按鈕、下拉式清單）拖曳到頁面上。 然後，您可以透過屬性面板設定每個元件的屬性（標籤、驗證等）。 通用編輯器會顯示表單的即時預覽。

**功能與功能**

* 使用預先建立的元件庫建立視覺化表單。
* 設定即時驗證和業務邏輯（例如，根據選擇顯示/隱藏欄位）。
* 檢視不同裝置（桌上型電腦、行動裝置）的即時預覽。
* 整合AEM功能，例如內容片段、AEM工作流程和使用者許可權。
* 使用「體驗產生器」取得AI協助，以使用提示建立或編輯表單。

**考量事項**

* 您需要使用條件式邏輯、多步驟面板或個人化來建置複雜表單。
* 您的團隊（例如行銷人員、業務使用者）偏好視覺工具。
* 您需要與AEM as a Cloud Service緊密整合，以便在表單中進行控管、工作流程或使用AEM資產。

**提交如何運作(Forms提交服務或AEM發佈)**

使用Universal Editor建立的Forms可以：

* 使用簡單的[Forms提交服務](/help/forms/forms-submission-service.md) （用於傳送資料至試算表或電子郵件）。
* 將資料提交至您的AEM發佈執行個體，以進行更進階的處理(例如啟動AEM工作流程、使用表單資料模型或與其他企業系統整合)。

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

此圖表顯示用於建立表單的通用編輯器的主要部分。

### 將Forms用於檔案製作(DA)

[Document Authoring (DA)](https://www.aem.live/developer/da-tutorial)是Adobe託管服務，用於建立和管理將透過Edge Delivery Services傳遞的主要網站內容（頁面、文章）。 這是使用SharePoint或Google Drive來取代Edge Delivery Services來源內容的替代方案。

**瞭解Edge Delivery Services內容的檔案編寫(DA)**

檔案製作使用Adobe的設計系統(Spectrum)和AEM的檔案模型（區塊、區段），提供企業級製作環境。 專為EDS的結構化內容管理而設計。

**DA如何處理Forms （內嵌，而非直接製作）**

DA本身&#x200B;**不是從頭開始建立表單的工具**。 而是使用DA來建立網頁，然後將&#x200B;*內嵌*&#x200B;表單（使用Document-Based Authoring或Universal Editor建立的）至這些DA編寫的頁面。

**將Forms內嵌至DA頁面的步驟**

1. **建立您的表單：**&#x200B;使用以下其中一種方式來建置您的表單：
   * 檔案式撰寫(Word/Google Docs)
   * 通用編輯器

1. **發佈您的表單：**&#x200B;請確定此表單已發佈，並可透過自己的Edge Delivery URL存取（例如`https://your-eds-project.hlx.page/forms/contact-us`）。
1. **在DA中編寫您的頁面：**&#x200B;在Document Authoring中建立或編輯您希望表單出現的頁面。
1. **內嵌表單：**&#x200B;使用您DA頁面中的特定「區塊」或元件，參照並內嵌其URL中的表單。 然後，DA頁面將會擷取並顯示此外部建立的表單。

**使用內嵌表單進行檔案編寫**
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

![檔案製作](/help/forms/assets/eds-da-based.png)

此圖表顯示您先使用UE或檔案建立表單，然後將其嵌入到您在Document Authoring中建立的頁面。


### 比較製作選項

| 條件 | 文件型編寫 | 通用編輯器(WYSIWYG) | 檔案製作(DA)中的Forms |
|----------------------------------|---------------------------------------|-----------------------------------------|-------------------------------------------|
| **主要撰寫工具** | Word/Google Docs/工作表 | 瀏覽器(AEM通用編輯器) | 不適用(Forms為&#x200B;*內嵌*) |
| **團隊技能等級** | 熟悉檔案編輯器 | 熟悉視覺化網頁工具 | 使用DA處理頁面內容 |
| **一般表單複雜度** | 從簡單到中等 | 中等到複雜，企業級 | 取決於內嵌表單 |
| **提交選項1 （簡單）** | Forms提交服務（至工作表/電子郵件） | Forms提交服務（至工作表/電子郵件） | 遵循內嵌表單的設定 |
| **提交選項2 （進階）** | 不適用 | AEM發佈（工作流程、FDM等） | 遵循內嵌表單的設定 |
| **AEM後端整合** | 最小 | 高(透過AEM發佈提交) | 透過內嵌式通用編輯器表單間接取得 |
| **最適合……** | 內容團隊快速建立簡單表單，快速資料擷取。 | 需要視覺控制、複雜表單或深入AEM整合的行銷人員、業務使用者。 | 主要內容在DA中進行管理的網站，需要來自其他來源的表單。 |

**增強型決策樹**
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

| **功能** | **通用編輯器 (WYSIWYG)** | **文件型編寫** | **檔案製作(DA)** |
|-----------------------------------------|-------------------------------|-----------------------------|-----------------------------|
| **使用 Sites 統一結構** | ✅ |                              | ✅ （含內嵌表單） |
| **嵌入表單支援** | ✅ | ✅ | ✅ （從通用編輯器或檔案內嵌） |
| **規則 (動態行為)** | 具有自訂功能的進階規則編輯器 | 受限：顯示/隱藏、運算值、自訂函數 | 取決於內嵌形式 |
| **附件支援** | ✅ | ℹ️ (搶先體驗) | 取決於內嵌形式 |
| **驗證碼支援** | reCAPTCHA Enterprise | reCAPTCHA Enterprise | 取決於內嵌形式 |
| **提交功能** | REST、電子郵件、FDM、工作流程、SharePoint、OneDrive、Azure Blob、Power Automate、Workfront Fusion (EA) | 僅限試算表 | 遵循內嵌表單的設定 |
| **資料結構描述** | FDM、自訂 | 自訂 | 根據內嵌表單 |
| **預填** | 💡 （透過精靈） | ✅ | 取決於內嵌形式 |
| **片段** | ✅ | ✅ | 取決於內嵌形式 |
| **視覺化規則編輯器** | ✅ |                              |                              |
| **本地化** | 💡 （透過網站） | ℹ️ （Excel/工作表手冊） | 取決於內嵌形式 |
| **資料結構描述 (資料樹)** | 💡 （透過UI擴充功能） |                              |                              |
| **範本支援** | 僅初始內容 |                              |                              |
| **入口網站** |                               |                              |                              |
| **主題** | ℹ️ (在專案層級) | ℹ️ (在專案層級) | ℹ️ （根據託管網站） |
| **自訂元件** | ✅ | ✅ | ✅ （如果內嵌元件支援） |
| **OOTB 與自訂函數** | ✅ | ✅ | ✅ （內嵌形式） |
| **片段參考** |                               |                              |                              |
| **簽署整合** |                               |                              |                              |
| **實驗** | ✅ | ✅ | 取決於內嵌內容 |
| **透過 Workfront 管理任務** | ✅ |                              |                              |
| **個人化擴充功能** | 💡 |                              |                              |
| **編輯器自訂** | ✅ （透過UI擴充功能） |                              |                              |
| **提交動作** | ✅ | 僅限試算表 | 根據內嵌表單 |

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

為了以您所學知識為基礎，以下說明如何邁向未來：

[選擇您的提交策略](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)決定您的專案是否需要簡單的Forms提交服務（適用於試算表/電子郵件輸出），還是AEM發佈提交動作所提供的彈性和後端整合。

請參閱[建立Forms的最佳實務](/help/edge/docs/forms/universal-editor/best-pratices-eds-forms.md)文章，瞭解如何設計有效、可存取且方便使用的表單。

## 後續步驟

本指南提供搭配AEM Edge Delivery Services使用表單的概觀。 如需特定設定的詳細逐步指示，請參閱Adobe Experience Manager官方檔案：

* [使用Edge Delivery Services Forms進行檔案式製作](/help/edge/docs/forms/tutorial.md)
* [具有Edge Delivery Services Forms的通用編輯器](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
* [檔案製作(DA)與內嵌內容](https://www.aem.live/developer/da-tutorial)
* [AEM Forms提交服務](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)


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
