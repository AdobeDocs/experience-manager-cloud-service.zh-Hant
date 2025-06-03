---
title: AEM Forms的AI助理(Forms Experience Builder)
description: 使用表單片段更快地製作強大的表單
feature: Edge Delivery Services
hide: true
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: 2db966405b5326d735083a66b2625d6d973ad7db
workflow-type: tm+mt
source-wordcount: '2354'
ht-degree: 1%

---


# AEM Forms的AI助理(Forms Experience Builder)

>[!NOTE]
>
>
> 適用於AEM Forms的AI助理(Forms Experience Builder)功能可在&#x200B;**早期採用者方案**&#x200B;下使用。 如果您有興趣，請從您的工作地址快速傳送電子郵件至mailto:aem-forms-ea@adobe.com，以請求存取功能。

>[!IMPORTANT]
>
> **檔案可能會有所變更**：此檔案目前正針對產品進行測試，可能會有更新和修訂。 隨著適用於AEM Forms的AI Assistant在早期採用者計畫期間不斷演化，功能、命令和範例可能會發生變化。

AEM Forms的AI Assistant (Forms Experience Builder)透過自然語言提示簡化常見的表單建置工作，進而增強您的撰寫體驗。 它適用於Forms Management UI、Adaptive Forms Editor和Universal Editor，可支援建立和設定動作，讓您更聰明、更快速地建置。 本指南將幫助您開始使用並充分利用其功能。

## 快速入門

在深入探究之前，讓我們先來談談存取AI助理及與之互動的基礎知識。

### 存取AI助理

您可以從AEM Forms中的三個不同位置存取AI助理：

1. **Forms管理UI**
   - 導覽至： 「Adobe Experience Manager > Forms > Forms與檔案」
   - 尋找介面左側的AI助理圖示
   - 按一下圖示以開啟AI助理面板

   ![AI助理圖示*](/help/edge/docs/forms/assets/forms-manager.gif)

2. **最適化Forms編輯器**
   - 導覽至： 「Adobe Experience Manager > Forms > Forms與檔案」
   - 選取並開啟表單以進行編輯
   - 在編輯器介面中按一下「AI助理」圖示

   ![AI助理圖示*](/help/edge/docs/forms/assets/adaptive-forms-editor.gif)

3. **通用編輯器**

   - 導覽至： 「Adobe Experience Manager > Forms > Forms與檔案」
   - 尋找介面左側的AI助理圖示
   - 在編輯器介面中按一下「AI助理」圖示

AI Assistant會根據您目前的位置和任務調整其功能，為每個內容提供相關協助。

### 如何互動：

- 只要以自然語言輸入您的要求即可。
- 使用`/`檢視可用命令或快速動作的清單。
- 當您想要助理員設定或更新特定欄位時，請使用`@fieldName` （例如`@firstName`、`@emailAddress`）參考特定表單欄位。
- 您可以上傳影像、PDF、Figma檔案或其他設計資產，以協助AI助理更清楚瞭解您的需求。


### 快速入門

觀看我們的入門影片，快速上手並執行：

>[!VIDEO](https://video.tv.adobe.com/v/3463164/)


本影片涵蓋在所有環境中啟動助理、基本互動及其功能概述。

## AI助理指令參考

| 指令 | 說明 | 用途 | 使用內容 | 範例 | 主要功能 |
|---------|-------------|---------|---------------|----------|--------------|
| /create-form | 在Forms管理UI或Forms編輯器中開始新表單 | 從頭開始建立全新表單 | Forms管理UI、最適化Forms編輯器 | /create-form以附加的PDF為基礎的客戶意見調查 | 提供表單結構的選項並建立表單。 **支援設計參考的附件** |
| /add-form | 在通用編輯器中新增表單 | 在通用編輯器中新增表單區塊或元件 | 適用於Edge Delivery Services的通用編輯器 | /add-form連絡人表單，包含名稱及電子郵件 | 插入表單區塊，適用於區塊式編輯。 **支援佈局指南的附件** |
| /update-layout | 將表單版面變更為摺疊式功能表、定位點式、精靈或單頁回應式設計 | 修改整體結構版面配置與導覽模式 | 所有編輯環境 | /update-layout精靈，包含3個步驟 | 摺疊面板、標籤、精靈、單頁回應式選項 |
| /update-field | 修改現有表單欄位的屬性和設定 | 變更欄位屬性，例如，標籤、驗證、格式、行為 | 所有編輯環境 | /update-field@email數必須搭配驗證 | 標籤、驗證規則、欄位型別、預設值、可見度。 **支援欄位設計範例的附件** |
| /create-rule | 為表單建立動態行為和條件式邏輯 | 實作商業邏輯、計算、條件式互動 | 所有編輯環境 | /create-rule在@maritalStatus等於「已婚」時顯示@spouseName | 條件式可視性、計算、驗證、值設定 |
| /create-panel | 建立新面板（群組相關欄位的容器） | 新增結構性容器以邏輯地組織表單欄位 | 所有編輯環境 | /create-panel個人資訊，包括名稱、電子郵件、電話 | 欄位分組、標題、版面配置選項、可摺疊區段。 **支援面板配置參考的附件** |
| /add-panel | 在通用編輯器中將影像轉換為表單面板 | 使用AI來分析上傳的影像並轉換為結構化表單面板 | 通用編輯器 | /add-panel從已上傳的表單影像 | 影像辨識、視覺到功能轉換、版面保留。 **需要附件**&#x200B;才能進行影像分析 |
| /configure-submit | 設定表單提交動作和資料處理 | 定義使用者提交完成的表單時會發生什麼情況 | 所有編輯環境 | /configure-submit傳送電子郵件給`support@company.com` | 電子郵件、REST API、工作流程、試算表、資料庫、Power Automate |
| /help | 存取AI助理中的協助和檔案 | 提供有關AEM Forms的關聯式說明、指引和答案 | 所有編輯環境 | /help如何建立多步驟表單？ | 功能說明、指南、最佳作法、疑難排解 |

### 命令類別

| 類別 | 命令 | 主要使用案例 |
|----------|----------|-------------------|
| 表單建立 | /create-form， /add-form | 開始新表單，新增表單區塊 |
| 結構與版面 | /update-layout， /create-panel， /add-panel | 組織表單結構、視覺化設計 |
| 欄位管理 | /update-field | 設定個別表單元素 |
| 邏輯與規則 | /create-rule | 新增動態行為和驗證 |
| 提交 | /configure-submit | 設定資料處理和工作流程 |
| 支援 | /help | 取得協助和檔案 |

### 語法准則

| 元素 | 格式 | 範例 | 備註 |
|---------|--------|---------|-------|
| 命令 | /command-name | /create-form | 一律以正斜線開頭 |
| 欄位參考 | @fieldName | @email， @firstName | 對現有欄位使用@符號 |
| 自然語言 | Command +說明 | /create-rule show field if condition | 結合命令與描述性文字 |
| 多個動作 | 分隔命令 | /create-panel然後/update-layout | 一次套用一個命令 |


### 環境特定功能

| 環境 | 可用命令 | 特殊功能 |
|-------------|-------------------|------------------|
| Forms管理UI | /create-form， /help | 表單層級的建立與管理 |
| 最適化Forms編輯器和通用編輯器 | 所有命令 | 完整功能集，詳細設定 |



### 欄位參考語法（內容元素）

使用`@fieldName`參考現有欄位：

- `@firstName` — 名字欄位
- `@email` — 電子郵件欄位
- `@phoneNumber` — 電話號碼欄位
- `@dateOfBirth` — 出生日期欄位

### 元件型別

此清單涵蓋常見的元件型別。 AI可能會識別變數或更專業的型別，但使用這些精確辭彙會產生最佳結果：

- `text input` — 單行文字欄位
- `text area` — 多行文字欄位
- `dropdown` — 選取清單
- `checkbox` — 單一核取方塊
- `checkbox group` — 多個核取方塊
- `radio group` — 選項按鈕群組
- `date picker` — 日期選擇
- `file upload` — 檔案附件
- `panel` — 分組欄位的容器


## 核心功能與擴充提示範例

AI Assistant可瞭解廣泛的命令。 以下範例將說明其功能。 請記得為元件使用精確術語，例如「面板」、「文字輸入」、「核取方塊」等。

| 功能類別 | 說明 | 提示範例 |
| ------------------------- | --------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **表單建立** | 從頭開始新表單，或根據說明開始新表單。 | `Create a new form titled 'Employee Onboarding'.` <br> `Generate a customer feedback form with fields for name, email, rating (1-5 stars), and comments.` <br> `Start a simple contact form with name, email, and message fields.` <br> `Design a multi-page registration form for an event.` <br> `Create a form based on the attached PDF template.` |
| **匯入設計** | 將現有設計(影像、Figma、PDF)轉換為AEM表單。 | `Import the form design from this uploaded PDF file.` <br> `Convert the uploaded Figma design into an adaptive form, focusing on the 'User Profile' frame.` <br> `Use this JPEG image of our old paper form to create a new digital version.` <br> `Create a form based on the layout of the attached PNG.` <br> `Recreate the form shown in the attached screenshot with modern styling.` |
| **新增元件與面板** | 新增各種表單欄位和結構容器（面板）。 | `Add a text input field for 'First Name'.` <br> `Add a 'Personal Details' panel with fields for full name, date of birth, and phone number.` <br> `Insert a checkbox group for 'Interests' with options: Technology, Sports, Music.` <br> `Add a file upload component for 'Resume'.` <br> `Create a repeatable panel named 'WorkExperience' with fields for company, title, and dates.` <br> `Add a panel matching the layout shown in the attached design mockup.` |
| **配置調整** | 修改表單版面的結構和外觀。 | `Change the 'Personal Details' panel to a two-column layout.` <br> `Set the overall form layout to a wizard (multi-step) navigation.` <br> `Make the header section span the full width of the form.` <br> `Adjust the spacing between fields in the 'Address' panel to be compact.` <br> `Align all field labels to the left.` <br> `Update the form layout to match the attached wireframe.` |
| **規則建立與邏輯** | 實作動態行為、計算和條件式可見度。 | `Make the 'Spouse Name' field visible only if 'Marital Status' is selected as 'Married'.` <br> `Calculate the 'Total Amount' by multiplying @quantity and @price.` <br> `Enable the submit button only when the @termsAndConditions checkbox is checked.` <br> `Set the value of @countryCode to '+1' if @country is 'United States'.` <br> `If @age is less than 18, show a message 'Must be 18 or older'.` |
| **欄位屬性更新** | 修改特定表單欄位（如標籤、預留位置等）的屬性。 | `Change the label of @email to 'Primary Email Address'.` <br> `Set the @comment field to be a multi-line text area.` <br> `Make the @phoneNumber field mandatory.` <br> `Add placeholder text 'Enter your ZIP code' to the @zipCode field.` <br> `Change the @country field to a dropdown and populate it with: USA, Canada, UK, Germany.` <br> `Update the help description for @password to 'Must include an uppercase letter, a number, and be at least 8 characters long.'` <br> `Set the maximum length of the @username field to 15 characters.` <br> `Configure the @dateOfBirth field to use a date picker.` <br> `Style the @email field to match the design shown in the attached image.` |
| **提交動作** | 定義使用者提交表單時會發生什麼情況。 | `Configure the form to submit data to the REST endpoint /api/v2/application-submit.` <br> `Set up an email submission to hr@example.com and sales@example.com on successful submission.` <br> `Trigger an AEM workflow named 'NewLeadProcessing' when this form is submitted.` <br> `On submit, redirect the user to a thank you page at /content/thankyou.html.` |
| **佈景主題** | 套用現有的AEM Forms主題來設定表單樣式。 | `Apply the 'Modern Business' theme to this form.` <br> `Switch to the 'Accessible Dark' theme.` <br> `Revert to the default canvas theme.` <br> `Apply styling that matches the brand guidelines shown in the attached style guide.` |
| **導覽與結構** | 新增導覽元素或重新組織表單部分。 | `Add a 'Next' button to the current panel and a 'Previous' button to the next panel.` <br> `Create a Table of Contents based on the form's panels.` <br> `Move the 'Address' panel to be before the 'Contact Information' panel.` |
| **驗證** | 設定欄位的特定驗證規則。 | `Set a regex pattern for the @employeeID field to be 'EMP\d{5}'.` <br> `Ensure the @age field only accepts numeric values between 18 and 99.` <br> `Validate the @email field to ensure it is a valid email format.` |
| **檢閱計畫** （通用編輯器） | 在執行前預覽助理的建議變更。 | `Add a contact form with fields for name, email, subject, and message.` (助理會顯示要建立的元件和屬性計畫，然後您按一下[套用]。<br> `Create a form based on the attached design file.` （助理會在實作前分析附件並顯示詳細計畫）。 |

## 取得最佳結果的最佳實務

若要充分利用AI Assistant，請記住以下秘訣：

- **開始簡單，逐步建置：**&#x200B;開始使用較小的特定命令（例如「為&#39;名字&#39;新增文字輸入」），而不是一開始過於複雜的多步驟請求。
- **使用AEM Forms術語：**&#x200B;使用「面板」、「文字輸入欄位」、「核取方塊群組」、「提交動作」、「規則」等詞語，讓助理更易於瞭解。
- **明確的參考欄位：**&#x200B;設定現有欄位時，請使用`@fieldName`標籤法（例如`Make @firstName mandatory`）。
- **檢閱計畫**&#x200B;在按一下[套用]之前，請一律仔細檢閱助理員在[通用編輯器]中提議的變更計畫。
- **手動驗證：**&#x200B;助理進行變更後，請一律預覽並測試您的表單，以確保其運作與外觀符合預期。 AI是一個強大的工具，但最終驗證是關鍵。
- **重複及調整：**&#x200B;如果第一個提示未產生正確的結果，請嘗試重新措辭或將請求分成較小的步驟。
- **提供意見回饋：**&#x200B;使用內建意見回饋機制來協助助理學習及改善（請參閱「意見回饋與支援」一節）。

## AI助理的產品說明

適用於AEM Forms的AI助理不僅適用於建置；也可協助您學習、瞭解及使用AEM Forms的各種功能。

### 支援的說明主題

您可以詢問助理員的問題，例如：

- 「如何從頭開始建立新的最適化表單？」
- 「什麼是Adaptive Forms中的面板，如何使用它？」
- 「說明如何將主題套用至表單。」
- 「表單和面板支援哪些版面配置型別？」
- 「如何設定不同的提交動作，例如傳送電子郵件？」
- 「您能指導我使用Figma設計來建立表單嗎？」
- 「建立多步驟表單的最佳方式為何？」

### 如何尋求協助：

1. 在Forms Management UI或最適化Forms編輯器中開啟AI助理。
2. 以自然語言輸入您的問題（例如「如何新增可重複的面板？」）。
3. 助理員會回應如下：
   - 逐步指示。
   - AEM Forms概念的說明。
   - 相關Adobe Experience League檔案的連結（如適用）。

### 取得更佳說明的秘訣：

- **明確：**&#x200B;一次詢問一個明確的問題。
- **使用關鍵字：**&#x200B;包含與AEM Forms功能或UI元素相關的關鍵字（例如，「最適化表單編輯器」、「規則編輯器」、「主題」）。
- **若有需要，請改寫：**&#x200B;若助理不瞭解或提供想要的資訊，請嘗試簡化您的問題或使用不同的詞語。


## 疑難排解常見問題

- **助理未回應：**
   - 確保您在支援的環境中主動工作(Forms管理UI、Adaptive Forms編輯器或Universal Editor)。
   - 檢查您的網際網路連線。
   - 請嘗試關閉AI助理面板再重新開啟。

- **不正確或未預期的回應：**
   - 請將您的請求重新表述得更具體或更簡單。
   - 將複雜的請求劃分為較小的個別命令。
   - 確保您使用標準的AEM Forms術語。

- **設計匯入問題(PDF/Figma/Image)：**
   - 確認設計檔案清晰、結構良好且清晰易讀。
   - 確認檔案格式受到支援(PDF、Figma連結、PNG、JPG等常見影像型別)。
   - 對於Figma，請確定您定位的框架已清楚定義且可存取。

- **欄位`@fieldName`無法辨識：**
   - 仔細檢查表單中欄位的確切名稱。 欄位名稱會區分大小寫，且必須完全相符。
   - 如果您嘗試修改欄位，請確定欄位已存在。


## 意見與支援

您的輸入對AI助理的不斷改進是無價之寶。

- **提供意見回饋：**&#x200B;使用AI助理介面中的內建&#x200B;**「提供意見回饋」命令或按鈕**，共用您的體驗、報告問題或建議增強功能。 （例如，您可以輸入`/feedback`或尋找意見回饋圖示）。
- **官方支援：**&#x200B;若有嚴重問題或需要進一步的協助，請透過官方Adobe支援管道或貴組織的指定支援聯絡人來聯絡。



## 使用附件

AI Assistant支援檔案附件，以增強您的表單建立和設定體驗。 您可以附加各種檔案型別，以提供要轉換的視覺內容、設計參照或現有表單。

### 支援的附件型別

| 檔案類型 | 使用案例 | 支援附件的命令 | 範例 |
|-----------|-----------|-----------------------------------|----------|
| **影像** (PNG、JPG、JPEG、GIF) | 表單版面參考、UI模型、紙張表單掃描 | /create-form， /add-form， /create-panel， /add-panel， /update-field | 上傳所需版面的熒幕擷圖 |
| **PDF檔案** | 要轉換的現有表單，設計規格 | /create-form， /add-form， /create-panel， /add-panel | 轉換PDF應用程式表單 |
| **Figma檔案** | 設計系統參考、UI原型 | /create-form， /add-form， /create-panel | 匯入圖形設計框架 |
| **設計檔案** (Sketch、Adobe XD匯出) | 視覺化設計參考 | /create-form， /add-form， /create-panel | 參考設計系統元件 |

### 如何使用附件

1. **附加在之前或使用您的命令：**

   - 按一下AI助理介面中的附件圖示
   - 從裝置選取檔案
   - 輸入參考附加檔案的指令

2. **在命令中參考附件：**

   ```
   /create-form based on the attached PDF application form
   /add-panel using the layout shown in the uploaded image
   /create-panel following the design in the attached Figma file
   /update-field @email to match the style in the attached screenshot
   ```

3. **多個附件：**

   - 您可以附加多個檔案以供比較或參考
   - 指定要使用的附件：「使用第一個附加的影像」或「根據PDF檔案」

### 附件最佳實務

- **清晰、高品質的影像：**&#x200B;確保上傳的影像清晰易讀，以便進行AI分析
- **相關檔案名稱：**&#x200B;使用描述性檔案名稱來協助AI瞭解內容
- **單一焦點：**&#x200B;每個附件都應專注於一個特定方面（版面配置、欄位設計等）
- **支援的格式：**&#x200B;請遵循常用格式(PNG、JPG、PDF)以獲得最佳相容性
- **檔案大小：**&#x200B;將附件保持在10MB以下，以獲得最佳處理速度

### 範例附件工作流程

**轉換紙張表單：**

1. 清晰的掃描或拍攝紙張表單
2. 上傳影像檔案
3. 使用命令： `/create-form based on the attached form image, converting all fields to digital equivalents`

**符合設計系統：**

1. 匯出或熒幕擷圖相關的設計元件
2. 附加設計參考
3. 使用命令： `/create-panel following the visual style and layout shown in the attached design`

**欄位樣式參考：**

1. 附加所需欄位外觀的熒幕擷圖
2. 使用命令： `/update-field @email to match the styling and layout shown in the attached image`

## 相關內容

[AEM Forms AI助理 — 提示程式庫](/help/edge/docs/forms/ai-assistant-prompt-library.md)

## 使用附件

AI Assistant支援檔案附件，以增強您的表單建立和設定體驗。 您可以附加各種檔案型別，以提供要轉換的視覺內容、設計參照或現有表單。

### 支援的附件型別

| 檔案類型 | 使用案例 | 支援附件的命令 | 範例 |
|-----------|-----------|-----------------------------------|----------|
| **影像** (PNG、JPG、JPEG、GIF) | 表單版面參考、UI模型、紙張表單掃描 | /create-form， /add-form， /create-panel， /add-panel， /update-field | 上傳所需版面的熒幕擷圖 |
| **PDF檔案** | 要轉換的現有表單，設計規格 | /create-form， /add-form， /create-panel， /add-panel | 轉換PDF應用程式表單 |
| **Figma檔案** | 設計系統參考、UI原型 | /create-form， /add-form， /create-panel | 匯入圖形設計框架 |
| **設計檔案** (Sketch、Adobe XD匯出) | 視覺化設計參考 | /create-form， /add-form， /create-panel | 參考設計系統元件 |

### 如何使用附件

1. **附加在之前或使用您的命令：**

   - 按一下AI助理介面中的附件圖示
   - 從裝置選取檔案
   - 輸入參考附加檔案的指令

2. **在命令中參考附件：**

   ```
   /create-form based on the attached PDF application form
   /add-panel using the layout shown in the uploaded image
   /create-panel following the design in the attached Figma file
   /update-field @email to match the style in the attached screenshot
   ```

3. **多個附件：**

   - 您可以附加多個檔案以供比較或參考
   - 指定要使用的附件：「使用第一個附加的影像」或「根據PDF檔案」

### 附件最佳實務

- **清晰、高品質的影像：**&#x200B;確保上傳的影像清晰易讀，以便進行AI分析
- **相關檔案名稱：**&#x200B;使用描述性檔案名稱來協助AI瞭解內容
- **單一焦點：**&#x200B;每個附件都應專注於一個特定方面（版面配置、欄位設計等）
- **支援的格式：**&#x200B;請遵循常用格式(PNG、JPG、PDF)以獲得最佳相容性
- **檔案大小：**&#x200B;將附件保持在10MB以下，以獲得最佳處理速度

### 範例附件工作流程

**轉換紙張表單：**

1. 清晰的掃描或拍攝紙張表單
2. 上傳影像檔案
3. 使用命令： `/create-form based on the attached form image, converting all fields to digital equivalents`

**符合設計系統：**

1. 匯出或熒幕擷圖相關的設計元件
2. 附加設計參考
3. 使用命令： `/create-panel following the visual style and layout shown in the attached design`

**欄位樣式參考：**

1. 附加所需欄位外觀的熒幕擷圖
2. 使用命令： `/update-field @email to match the styling and layout shown in the attached image`
