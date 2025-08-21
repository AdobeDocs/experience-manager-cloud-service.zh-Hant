---
title: Forms Experience Builder快速入門
description: 瞭解如何使用Forms Experience Builder建立和管理具有所有使用者型別漸進式揭露的表單
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: da429952-ccc0-4579-a243-8bddeb73a0fb
source-git-commit: 8be2b09200af58c701721b3e8537ea5e6cc3e4a2
workflow-type: tm+mt
source-wordcount: '1720'
ht-degree: 15%

---

# Forms Experience Builder快速入門

>[!NOTE]
>
> **早期採用者方案**&#x200B;提供Forms Experience Builder功能。 如果您有興趣，請從您的工作地址快速傳送電子郵件給`aem-forms-ea@adobe.com`，以要求存取該功能。

>[!IMPORTANT]
>
> **文件內容可能隨時變更**：此文件目前正在針對產品進行測試，可能會進行更新和修訂。隨著Forms Experience Builder在早期採用者計畫中不斷演化，功能、命令和範例可能會有所變更。

本全方位指南可協助您開始使用對話式AI技術建立和管理表單。 無論您是想要建立第一個表單的初學者，還是想要運用複雜功能的進階使用者，您都能找到詳細資訊和實務範例，以引導您瞭解Forms Experience Builder的功能。

## 必要條件和設定

### 1.要求存取權

如果您沒有Forms Experience Builder的存取權：

1. **要求存取權**：從您的工作電子郵件傳送電子郵件給[aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)
2. **包含資訊**：組織名稱和專案詳細資料
3. **等待核准**： Adobe將稽核並提供上線指示

### 2.確認Forms已啟用

在使用Forms Experience Builder之前，請確定您的環境已啟用[AEM Forms](/help/forms/setup-forms-cloud-service.md)。


### 3.設定環境


* 適用於Edge Delivery Services (EDS)的&#x200B;**：**

   * [設定Edge Delivery Services Forms的環境](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
   * [使用Edge Delivery Forms範本建立新表單](/help/edge/docs/forms/universal-editor/create-forms.md)

* **對於核心元件型表單：**

   * 在您的Adobe Experience Manager執行個體上，前往「Forms > Forms和檔案」
   * [使用核心元件範本建立新頁面](/help/forms/creating-adaptive-form-core-components.md)

## 快速啟動

### 存取Forms Experience Builder

**通用編輯器**

* 在Universal Editor中開啟EDS頁面
* 尋找左側面板中的Forms Experience Builder圖示
* 按一下以開啟對話式介面

**自適應表單編輯器**

* 導覽至： 「AEM > Forms > Forms與檔案」
* 建立或開啟核心元件型表單以進行編輯
* 按一下編輯器工具列中的Forms Experience Builder圖示

### 您的第一個表單

嘗試這個簡單的交談開始：

```
👤 You: "Create a simple contact form"
🤖 AI: "I'll create a contact form with name, email, and message fields for you."

👤 You: "Make the email field required"
🤖 AI: "Updated the email field to be required with validation."
```

### 基本命令

| 符號 | 用途 | 使用方式 |
|--------|---------|------------|
| `/` | 快速動作和捷徑 | 輸入`/create`以建立表單，`/help`以取得協助 |
| `@` | 參考現有表單欄位 | 輸入`@fieldName`以修改特定欄位（例如，`@email`） |
| 純文字 | 自然交談 | 說明您想要的：「新增必要電話號碼欄位」 |

### 成功秘訣

* **必須具體**：「新增含驗證的必要電子郵件欄位」的效果比「新增電子郵件」好
* **參考現有欄位**：修改表單時使用`@fieldName`
* **要求協助**：型別`/help`後面接著您的問題
* **重複**：一次變更一次，以獲得最佳結果

## 核心功能

### 建立Forms的兩種方式

#### 1.從頭開始建立

以自然語言說明您的表單需求，Forms Experience Builder就會產生完整的表單結構：

**範例：**

* 「使用個人資訊、財務詳細資料和檔案上傳建立貸款申請表單」
* 「建立包含評等、評論和產品類別的客戶意見回饋表單」
* 「我需要多步驟登錄檔，才能參加具有付款處理功能的會議」

#### 2.匯入及轉換

將現有的表單與檔案轉換為現代的互動式體驗：

**支援的來源：**

* **PDF forms**：上傳靜態PDF→具有驗證的互動式數位表單
* **熒幕擷圖/影像**：紙張表單像片→功能數位版本
* **HTML Forms**：基本網路表單→具有進階功能的增強型AEM Forms
* **XFA Forms**：舊版Adobe表單→現代回應式表單
* **URL**：具有改良UX→原生AEM Forms的現有網路表單

**如何匯入：**

1. 按一下Forms Experience Builder介面中的附件圖示
2. 上傳檔案(PDF、影像、Figma設計等)
3. 說明您的需求：
   * 「將此PDF表單轉換為數位版本」
   * 「建立符合此熒幕擷圖配置的表單」
   * 「根據我的 Figma 設計建立此表單」

**支援的檔案型別：**

* **影像** (PNG、JPG、GIF)：表單版面配置、UI模型、掃描的表單
* **PDF檔案**：現有的表單、規格、檔案
* **Figma檔案**：設計原型、品牌指南
* **設計檔案**：視覺參考、樣式參考線

### 重要互動

#### 新增表單元素

**基本新增內容：**

```
👤 You: "Add a section for personal information"
🤖 AI: "Added a personal information panel with standard fields"

👤 You: "Include a file upload for resume"
🤖 AI: "Added a secure file upload component for documents"

👤 You: "Add a dropdown for country selection"
🤖 AI: "Added a country dropdown with common options"
```

**詳細規格：**

```
👤 You: "Add a personal information panel with fields for full name, date of birth, phone number, and email address"
🤖 AI: "Created a personal information panel with all requested fields and appropriate validation"

👤 You: "Include a secure file upload component for documents, limited to PDF files under 5MB"
🤖 AI: "Added a file upload field with PDF restriction and 5MB size limit"

👤 You: "Add a country dropdown with options for USA, Canada, UK, and Germany"
🤖 AI: "Added a country dropdown with the specified options"
```

#### 建立動態行為

**簡單邏輯：**

```
👤 You: "Show additional fields when 'Other' is selected"
🤖 AI: "Created a conditional rule that shows additional fields when 'Other' is chosen"

👤 You: "Make the email field required"
🤖 AI: "Updated the email field to be required with validation"

👤 You: "Calculate the total automatically"
🤖 AI: "Added calculation logic to automatically compute totals"
```

**複雜的業務規則：**

```
👤 You: "Show the spouse information fields only when marital status is set to 'Married'"
🤖 AI: "Created a conditional rule that displays spouse fields based on marital status"

👤 You: "Calculate the total cost by multiplying quantity and price, then add 10% tax"
🤖 AI: "Added calculation logic with quantity, price, and tax computation"

👤 You: "Enable the submit button only when all required fields are completed and terms are accepted"
🤖 AI: "Created validation logic that enables submission only when all conditions are met"
```

#### 表單版面和設計

**版面變更：**

```
👤 You: "Make this a multi-step form"
🤖 AI: "Converted the form to a progressive layout with navigation"

👤 You: "Organize fields in two columns"
🤖 AI: "Updated the layout to display fields in a two-column arrangement"

👤 You: "Convert to an accordion layout"
🤖 AI: "Transformed the form to use accordion-style sections"
```

**設計改良：**

```
👤 You: "Create a wizard-style form with 3 steps: personal info, preferences, and review"
🤖 AI: "Created a wizard form with three distinct steps and navigation"

👤 You: "Arrange the address fields in a compact two-column layout"
🤖 AI: "Organized address fields in a compact two-column format"

👤 You: "Update the layout to match the attached wireframe"
🤖 AI: "Modified the layout to match the provided design reference"
```

### 整合設定

Forms Experience Builder可以設定各種提交端點，以將您的表單與外部系統和服務連線：

| 整合型別 | 安裝程式命令 | 使用案例 |
|------------------|---------------|----------|
| **電子郵件** | 「傳送表單至電子郵件」 | 表單提交的通知和確認 |
| **REST API** | &quot;提交至REST端點&quot; | 自訂應用程式和協力廠商系統 |
| **雲端儲存空間** | 「儲存至Azure/SharePoint」 | 檔案儲存和檔案管理 |
| **工作流程** | 連線到Power Automate | 業務流程自動化與核准 |
| **行銷** | 「與Marketo整合」 | 銷售機會管理和行銷自動化 |

**進階整合範例：**

```
👤 You: "Send form submissions to hr@company.com and create a case in our CRM system"
🤖 AI: "Configured email submission and CRM integration"

👤 You: "Submit data to our REST API endpoint and trigger the new customer workflow"
🤖 AI: "Set up REST API submission with workflow triggers"

👤 You: "Email responses to the sales team and add the lead to our marketing automation platform"
🤖 AI: "Configured multi-channel submission with email and marketing automation"
```





## 進階表單作業


### 建立複雜規則

建立能回應使用者互動並確保資料完整性的複雜驗證和業務邏輯：

```
👤 You: "Show the address section only if the user selects 'Ship to different address'"
🤖 AI: "Created a conditional rule that shows/hides the address panel based on checkbox selection"
```

### 多步驟表單建立

```
👤 You: "Create a progressive form with 3 steps: personal info, preferences, confirmation"
🤖 AI: "Created a progressive form with navigation between steps and validation at each stage"
```

### 進階欄位型別

* 具有檔案管理驗證和大小限制的檔案上傳
* 日期選擇器，具有用於排程的限制和業務規則
* 包含根據使用者選擇而變更的動態選項的下拉選單
* 適用於複雜決策樹的具有條件邏輯的選項按鈕


### PDF至表單轉換

```
👤 You: "Convert this PDF into an interactive form"
🤖 AI: "Analyzed the PDF and created a form with appropriate field types and validation"
```

### 表單轉換的URL

```
👤 You: "Create a form from this website"
🤖 AI: "Extracted form elements and created a native AEM Form with enhanced functionality"
```

### 效能分析

```
👤 You: "Analyze this form's conversion performance"
🤖 AI: "Provided insights on form effectiveness and suggested optimizations"
```

### 進階自訂

#### 自訂驗證規則

* 根據使用者輸入建立動態表單行為的欄位相依性
* 根據使用者需求調整表單體驗的複雜條件式邏輯
* 為使用者提供明確指引的自訂錯誤訊息
* 跨欄位驗證，可確保多個輸入之間的資料一致性

#### 版面配置最佳化

* 行動回應能力，可確保表單在所有裝置上順暢運作
* 協助工具合規性，可讓殘障人士使用表格
* 可提升使用者參與度和完成率的視覺化設計改善
* 減少摩擦並提高滿意度的使用者體驗增強功能

#### 整合工作流程

* 透過業務工作流程傳遞表單提交的多步驟核准流程
* 將表單資料轉換為外部系統所需格式的資料轉換
* 將特定規則和計算套用至表單提交的自訂商業邏輯
* 進階的錯誤處理功能，提供從系統問題順利復原的功能

## 命令參考

### 基本命令

| 符號 | 用途 | 使用方式 |
|--------|---------|------------|
| `/` | 快速動作和捷徑 | 輸入`/create`以建立表單，`/help`以取得協助 |
| `@` | 參考現有表單欄位 | 輸入`@fieldName`以修改特定欄位（例如，`@email`） |
| 純文字 | 自然交談 | 說明您想要的：「新增必要電話號碼欄位」 |

### 斜線命令

| 命令 | 上下文 | 使用範例 |
|---------|---------|---------------|
| `/create-form` | 所有環境 | `/create-form customer survey` |
| `/add-form` | 通用編輯器 | `/add-form contact form` |
| `/update-layout` | 表單編輯器 | `/update-layout wizard with 3 steps` |
| `/update-field` | 表單編輯器 | `/update-field @email to be required` |
| `/create-rule` | 表單編輯器 | `/create-rule show @spouse if married` |
| `/create-panel` | 表單編輯器 | `/create-panel Personal Information` |
| `/configure-submit` | 表單編輯器 | `/configure-submit to email support` |
| `/help` | 所有環境 | `/help multi-step forms` |

### 欄位參考

使用 `@fieldName` 來參考現有欄位：

* `@firstName`，`@lastName` *名稱欄位
* `@email`，`@phoneNumber` *連絡人欄位
* `@address`、`@city`、`@zipCode` *位址欄位
* `@dateOfBirth`，`@startDate` *日期欄位

### 元件類型

描述表單元素時，請使用下列詞語：

* `text input` *單行文字欄位
* `text area` *多行文字欄位
* `dropdown` *選取包含選項的清單
* `checkbox` *單一核取方塊
* `checkbox group` *多個核取方塊
* `radio group` *選項按鈕群組
* `date picker` *日期選取欄位
* `file upload` *檔案附件欄位
* `panel` *分組欄位的容器

### 整合命令

| 服務 | 自然語言命令 | 要求 |
|---------|--------------------------|--------------|
| 電子郵件 | 「傳送提交至[電子郵件]」 | 有效的電子郵件地址 |
| REST API | 「提交至REST端點[URL]」 | API端點與認證 |
| Azure 儲存體 | 「將檔案儲存至Azure儲存體」 | 儲存體帳戶設定 |
| SharePoint | 「存放在SharePoint [網站]」 | SharePoint網站存取權 |
| Power Automate | &quot;觸發Power Automate流程&quot; | 流量設定 |
| Marketo | 「將銷售機會新增至Marketo」 | Marketo API認證 |

### 提示

1. **使用自然語言**： AI可瞭解複雜的要求，且可解譯詳細的需求
2. **必須具體**：詳細的說明會產生更好的結果，並產生更精確的表單
3. **重複**：透過對話調整表單，以獲得完美的使用者體驗
4. **善用內容**：參考現有的表單元素，以建置您現有的表單元素
5. **徹底測試**：驗證所有使用者案例，以確保表單如預期般運作

## 產品說明與學習

Forms Experience Builder也可以教導您AEM Forms功能：

### 請提出類似以下問題：

* 「如何建立多步驟表單？」
* 「面板與區段之間有何差異？」
* 「如何設定電子郵件通知？」
* 「建立方便行動裝置使用的表單有哪些最佳實務？」
* 「如何將主題套用到我的表單？」

### 取得以下方面的協助：

* AEM Forms 概念和術語
* 複雜功能的逐步操作指示
* 最佳實務與建議做法
* 常見問題疑難排解

## 最佳做法

### 表單設計

* **保持簡單**：從基本欄位開始，只在必要時增加複雜性，以避免使用者過多
* **使用清楚的標籤**：使用描述性標籤來引導使用者完成表單，讓欄位目的變得明顯
* **提供說明文字**：透過內容說明和範例，引導使用者完成複雜的欄位
* **徹底測試**：驗證所有使用者路徑，以確保表單在所有案例中都正常運作

### 使用者體驗

* **漸進式公開**：根據內容顯示相關欄位，以降低認知負載並改善完成率
* **清除導覽**：協助使用者瞭解他們在表單中的位置以及還有哪些步驟
* **回應式設計**：確保表單可在所有裝置和熒幕大小上運作，以發揮最大的協助工具
* **協助工具**：遵循WCAG准則，讓殘障人士能夠使用表格

### 效能

* **最佳化欄位計數**：僅要求必要的資訊，以減少表單放棄並提高完成率
* **使用適當的驗證**：在提交之前避免錯誤，以提供立即的意見反應和指引
* **測試完成率**：透過分析和使用者意見反應，監視並改善表單效益
* **定期更新**：保持表單符合業務需求和使用者期望，以獲得最佳效能

### 品牌一致性

* **建立品牌範本**：開始建立表單之前，使用您組織的顏色、字型和樣式準備品牌表單範本
* **定義樣式標準**：建立可在提示中參考的一致按鈕樣式、欄位版面配置和間距准則
* **使用品牌資產**：準備圖志、色彩代碼和品牌准則，以便在建立表單時輕鬆參考
* **範本庫**：建立品牌表單範本的集合，用於常見的使用案例（連絡人、註冊、意見回饋）
* **樣式提示**：包含品牌特定指示：「使用公司藍色(#1234AB)作為按鈕和公司字型Helvetica」

### 獲得最佳結果的提示

**開始簡單，建置**

* 從基本請求開始：「建立聯絡表單」
* 逐步增加詳細資料：「對電子郵件欄位新增驗證功能」
* 測試並改進：「將電話欄位設為選用」

**需要時為特定**

* 請不要說：「做一份不錯的表單」
* 請改說：「使用專業的色彩和清晰的印刷樣式」

**使用自然語言**

* 請不要說：「新增文字輸入元件」
* 請改說：「新增名字的欄位」

**參考現有元素**

* 現有欄位請使用 `@fieldName`：「將 @email 設為必填」
* 具體描述欄位名稱：「更新 @phoneNumber 欄位」

**劃分複雜請求**

* 不要提出一個大請求，改為嘗試多個小請求
* 逐步建立表單
* 先測試每一項變更，再進入下一步

## 疑難排解

| 問題 | 快速修正 |
|-------|-----------|
| **介面未載入** | 重新整理瀏覽器，檢查網際網路連線 |
| **命令無法運作** | 請嘗試`/help`或使用自然語言 |
| **@fieldName無法辨識** | 檢查拼字，確定欄位先存在 |
| **檔案上傳失敗** | 在10MB以下使用PDF/JPG/PNG |
| **表單看起來錯誤** | 更具體一些：「讓行動裝置更友好」 |
| **整合失敗** | 驗證API憑證和許可權 |

**仍需要協助嗎？**&#x200B;型別`/help`後接您的特定問題，或連絡您的系統管理員。

如需其他支援，請參閱主要的[Forms Experience Builder提示程式庫](/help/edge/docs/forms/ai-assistant-prompt-library.md)，或連絡您的系統管理員以取得技術協助。
