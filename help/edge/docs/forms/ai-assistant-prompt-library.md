---
title: 表單體驗建立工具 - 提示資料庫
description: 各種經確認的提示模式和範例之集合，在表單管理使用者介面、自適應表單編輯器和通用編輯器中使用 AI 輔助功能建置表單時可以使用。
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: c8f64082-a23f-4919-ad66-042faad77d31
source-git-commit: fe34b44d02c308e7d18a08dd05f21abc67bd0cb2
workflow-type: ht
source-wordcount: '2193'
ht-degree: 100%

---


# 表單體驗建立工具 - 提示資料庫

為表單體驗建立工具進行最佳化的可重複使用提示模式和範例集合。這個精簡的資料庫專注於兩種核心建立方法：從頭開始建立，以及匯入和轉換，並增強了對 LLM 驅動之智慧欄位和品牌一致性的支援。

>[!NOTE]
>
> 早期採用者方案提供表單體驗建立工具。使用您的工作郵件地址寄送電子郵件至 `aem-forms-ea@adobe.com` 請求存取權限。

>[!IMPORTANT]
>
> **文件內容可能隨時變更**：此提示庫目前正在針對產品進行測試，可能會進行更新和修訂。隨著表單體驗建立工具在早期採用者方案期間持續發展，相關的提示、範例和最佳做法可能會有所變更。

## 使用這個提示資料庫

此資料庫為常見的表單建置情境提供可重複使用的提示模式。如需了解全面的最佳做法，請參閱[表單體驗建立工具快速入門指南](forms-ai-assistant-getting-started.md#best-practices)。

### 關於此資料庫的快速秘訣

- **從範例開始** - 使用所提供的提示作為範本，並根據您的需求進行調整
- **兩種建立方法** - 選擇「從頭開始建立」或「匯入和轉換」方法
- **具體一些** - 在通用範例中加入您自己的詳細資料
- **徹底測試** - 務必在特定環境中驗證結果

### 品牌範本和樣式

**提前準備品牌資產，建立一致的表單：**

- **品牌範本** - 使用您組織的顏色、字體和版面模式，準備標準化的表單範本
- **樣式指引** - 定義表單體驗建立工具可套用的一致性欄位樣式、按鈕設計和間距標準
- **元件資料庫** - 與您的開發團隊合作，準備符合您品牌識別的可重複使用表單元件
- **視覺資產** - 準備用於表單整合的標誌、圖示和背景元素

<!-- **Example Brand Application Prompt:**

    Apply our financial services brand template with:
    - Corporate blue (#003366) and silver (#C0C0C0) color scheme
    - Open Sans font family for all text
    - 16px minimum font size for accessibility
    - Consistent 24px spacing between sections
    - Corporate logo in header with proper sizing
    - Professional button styling with hover effects

>[!NOTE]
>
>**Custom Components**: Check with your development team about using organization-specific components and their compatibility with Forms Experience Builder before implementing custom brand elements.

>[!NOTE]
>
> This prompt library has been updated to reflect the streamlined Forms Experience Builder capabilities. Some advanced integration and testing features shown in examples may require additional configuration.

-->


## 逐步開發範例

這些範例說明如何逐步建立表單，從簡單開始，然後逐漸增加複雜度：

### 範例 1：逐步建立聯絡表單

**第 1 步 - 簡單開始：**

    建立包含姓名、電子郵件和訊息欄位的聯絡表單

**第 2 步 - 新增驗證：**

    將 @name 和 @email 設定為必填欄位並搭配適當的驗證

**第 3 步 - 增強使用者體驗：**

    加入預留位置文字：@name「您的全名」、@email「your.email@company.com」、@message「讓我們知道可以如何提供協助」

**步驟 4 - 新增進階功能：**

    新增下拉式查詢類型，其中包含以下選項：「一般問題」、「支援請求」、「銷售查詢」、「合作夥伴關係」

**步驟 5 - 實施條件式邏輯：**

    /create-rule 僅當 @inquiryType 等於「支援請求」時顯示 @urgencyLevel 下拉式選單 (低、中、高)

### 範例 2：逐步建立註冊表單

**第 1 步 - 基本結構：**

    建立包含個人資訊面板的使用者註冊表單

**第 2 步 - 新增必填欄位：**

    新增 @firstName、@lastName、@email、@phoneNumber 欄位並搭配適當的驗證

**第 3 步 - 新增商業邏輯：**

    建立規則：如果 @age 未滿 18 歲，則顯示父母/監護人資訊區段

**第 4 步 - 使用偏好設定進行增強：**

    新增包含 @newsletterSubscription、@marketingConsent、@termsAccepted 的偏好設定面板

**第 5 步 - 新增檔案上傳區：**

    為 @profilePicture 新增檔案上傳欄位，大小限制為 5MB

## 表單建立與管理

**何時使用：**&#x200B;當您需要建立新表單或修改現有表單時。

**使用方法：**&#x200B;選擇以下兩種方法之一：從頭開始建立或匯入和轉換 (請參閱[快速入門指南](forms-ai-assistant-getting-started.md#two-ways-to-create-forms))。

**範例提示 - 簡單表單建立：**

    建立客戶回饋表單，其中包含：
    - 產品評分 (1 至 5 顆星)
    - 能提供詳細回饋的評論區
    - 客戶電子郵件 (選填)
    - 提交電子郵件通知

**範例提示 - 複雜表單建立：**

    建立全面的員工入職表單，其中包含：
    
    **個人資訊區段：**
    - 全名 (名字、中間名、姓氏)
    - 出生日期及年齡驗證
    - 聯絡資訊 (電子郵件、電話、地址)
    - 緊急聯絡方式
    
    **就業詳情：**
    - 職位和部門選擇
    - 開始日期以及工作日驗證
    - 薪資資訊保密通知
    - 報告結構
    
    **文件上傳：**
    - 履歷/CV 上傳 (PDF、DOC、DOCX)
    - 身分驗證文件
    - 稅務表單和銀行資訊
    - 簽署僱傭協議
    
    **偏好：**
    - 使用成本計算器選擇福利
    - 工作時間偏好
    - 培訓需求
    - 設備需求
    
    **驗證規則：**
    - 電子郵件格式驗證
    - 電話號碼格式驗證
    - 年齡必須年滿 18 歲
    - 必須上傳所有必要文件
    - 必須接受條款和條件
    
    **提交動作：**
    - 向新進員工傳送確認電子郵件
    - 通知人力資源部門
    - 在人力資源系統中建立員工記錄
    - 安排迎新會議

**表單管理提示：**

    匯入此 PDF 申請表單，並將其轉換為具有增強驗證功能的自適應表單
    
    更新現有的聯絡表單，包括社群媒體帳號和偏好的聯絡方式
    
    將註冊表單重新組織為 3 步驟精靈：個人資訊、偏好設定、確認

## 欄位管理和設定

**何時使用：**&#x200B;當您需要新增、修改或設定表單欄位時。

**使用方法：**&#x200B;具體說明欄位類型、驗證規則和對使用者體驗的需求。

**範例提示 - 基本欄位新增：**

    新增「公司名稱」文字輸入欄位，並新增預留位置文字「輸入您的公司名稱」

**範例提示 - 進階欄位設定：**

    新增包含以下內容的綜合地址區段：
    
    **街道地址：**
    - 地址第 1 行 (必填，最多 100 個字元)
    - 地址第 2 行 (選填，最多 100 個字元)
    - 城市 (必填，下拉式選單包含常見城市)
    - 州/省 (必填，下拉式選單)
    - 郵遞區號 (必填，格式驗證)
    - 國家/地區 (必填，預設為「美國」)
    
    **驗證規則：**
    - 郵遞區號必須與所選州相符
    - 地址第 1 行不得空白
    - 城市必須是所選州的有效城市
    
    **使用者體驗：**
    - 自動完成地址欄位
    - 清楚的標籤和說明文字
    - 行動裝置友善的輸入欄位
    - 無障礙功能合規性

**欄位設定提示：**

    將 @email 欄位設為必填項目，搭配即時驗證和自訂錯誤訊息
    
    為 @country 新增下拉式選單，其中包含美國、加拿大、英國、德國、法國和「其他」選項
    
    將 @phoneNumber 欄位設定為 (XXX) XXX-XXXX 格式並搭配驗證
    
    新增 @resume 的檔案上傳欄位並搭配 PDF 和 DOC 限制，大小上限為 5MB

## LLM 增強型智慧欄位

**何時使用：**&#x200B;當您的欄位需要善用 AI 知識庫的預填選項時。

**使用方法：**&#x200B;需要全面資料集的請求欄位 - AI 可以使用其內建知識自動填入選項。

### 地理和位置欄位

**機場和交通：**

    新增包含所有主要國際機場的出發機場下拉式選單
    新增包含 IATA 代碼和全名的到達機場欄位
    建立距離使用者位置最近的機場欄位
    新增歐洲城市火車站選項

**行政區域：**

    新增美國各州及其縮寫的完整清單
    建立包含 ISO 代碼和全名的國家/地區下拉式選單
    新增包含時區的世界主要城市欄位
    包含加拿大各省和地區的下拉式選單
    新增英國郡縣郵政區域

### 商業和行業資料

**公司分類：**

    新增使用 NAICS 代碼進行行業分類的欄位
    建立企業實體類型 (有限責任公司、公司、合夥企業等) 的下拉式選單
    新增公司規模類別欄位 (新創公司、中小型企業、大型企業)
    包含大型組織的部門選項
    新增專業服務類型欄位

**專業分類：**

    新增包含常見行業角色的職位名稱欄位
    依照領域建立專業認證下拉式選單
    包含學位類型的教育程度
    新增包含工作年限範圍的欄位
    建立程式語言和框架的選項

### 標準和監管

**財務與法律：**

    新增包含符號和匯率的貨幣代碼欄位
    以國家/地區建立稅號類型下拉式選單
    新增法律文件類型欄位
    新增具有安全性功能的付款方式選項
    依照國家/地區建立銀行機構選項

**技術標準：**

    新增包含副檔名的檔案格式類型下拉式選單
    包含網路協定選項
    新增資料庫類型和版本的欄位
    建立 API 驗證方法的選項

### 醫療保健和醫學

**醫學分類：**

    新增醫學專科欄位
    建立包含通用名的常用藥物下拉式選單
    新增保險提供者類型欄位
    新增醫療緊急聯絡人關係選項
    建立飲食限制和過敏欄位

### 時間和日曆情報

**日期和時間欄位：**

    新增可處理時區的工作時間欄位
    依照國家/地區建立公共假日下拉式選單
    包含季節性選項和日期範圍
    新增可預約會議室的欄位並顯示可用情況
    建立重複會議模式的選項

### 產品和服務類別

**電子商務分類：**

    新增包含子類別的產品類別欄位
    建立包含預計配送時間的配送方式下拉式選單
    新增退貨政策選項欄位
    新增客戶優先權選項
    建立訂閱結算週期欄位

**智慧欄位提示範例：**

    「新增出發機場欄位，其中包含全球所有主要機場，包括 IATA 代碼和城市名稱」
    
    「使用標準 NAICS 分類和技術子類別建立綜合產業欄位」
    
    「包含根據所選工作領域調整的專業認證下拉式選單」
    
    「新增根據所選國家/地區格式化的國際電話號碼欄位」
    
    「建立大學選項欄位，按國家/地區和排名組織主要院校」

## 規則建立和商業邏輯

**何時使用：**&#x200B;當您需要實施條件式邏輯、驗證規則或業務流程時。

**使用方法：**&#x200B;清晰地描述商業邏輯，指定條件和動作。

**提示範例 - 簡單的條件邏輯：**

    建立一項規則，其中僅當 @maritalStatus 等於「已婚」時才顯示 @spouseInformation 面板

**範例提示 - 複雜的業務規則：**

    實施全面的貸款申請驗證：
    
    **收入驗證：**
    - 如果 @annualIncome 小於 30000：
    - 顯示警告訊息：「收入可能不足以滿足所申請的貸款金額」
    - 需要額外的收入證明
    - 顯示訊息：「可能需要其他文件」
    - 如果 @annualIncome 大於 100000：
    - 顯示進階服務選項
    - 啟用優先處理核取方塊
    
    **年齡驗證：**
    - 若 @age 未滿 18 歲：
    - 顯示父母/監護人資訊區段
    - 強制上傳家長簽名
    - 將提交按鈕文字變更為「提交審閱」
    - 如果 @age 為 65 歲或以上：
    - 顯示老年人折扣選項
    - 新增無障礙功能偏好設定區段

**規則特定提示：**

    建立一個**可見性規則**，僅當 @maritalStatus 等於「已婚」或「同居關係」時才顯示 @spouseInformation 面板
    
    新增**漸進式揭露**，其中根據先前的答案出現其他問題。從基本資訊開始，然後顯示相關的後續訊息
    
    實現**智慧預設**，其中 @country 選項自動設定相關欄位。允許手動覆寫

## 資料整合與提交

**何時使用：**&#x200B;當您需要將表單連接到後端系統、資料庫或外部服務時。

**使用方法：**&#x200B;從基本的提交設定開始，然後逐步增加其他整合。指定整合類型、資料格式要求和錯誤處理偏好。

**提示範例 - 從基本提交開始：**

    為 @applicationForm 設定基本表單提交：
    
    **主要提交內容：**
    - 將表單資料傳送至 REST 端點：`/API/v1/applications`
    - 將資料格式化為 JSON
    - 顯示成功訊息：「申請提交成功」
    - 如果提交失敗，顯示錯誤訊息：「提交失敗，請重試」

**然後漸次新增次要動作：**

    向 @applicationForm 新增電子郵件通知：向 @email 地址傳送確認電子郵件，其中包含申請參考編號
    
    將 CRM 整合新增至 @applicationForm：使用 @firstName、@lastName、@email 建立新的商機記錄，並將狀態設為「新申請」

**提示範例 - 標準多通道提交：**

    設定具有多個資料目標的表單提交：
    
    **主要提交：***
    - 將表單資料傳送至 REST 端點：`/API/v1/applications`
    - 包含驗證標頭和 API 金鑰
    - 將資料格式化為 JSON，並以巢狀物件表示地址和就業情況
    - 顯示感謝訊息，處理成功回應 (201)
    
    **次要操作：**
    - 傳送電子郵件至 @email address 給申請人
    - 將申請資料複製到追蹤系統
    - 觸發工作流程執行核准程序
    - 在 CRM 中建立記錄，商機狀態為「新申請」
    
    **錯誤處理：**
    - 如果主要提交失敗，在本機儲存資料並重試 
    - 顯示使用者友善的錯誤訊息：「提交暫時無法使用」
    - 提供下載表單資料作為備份之用的選項
    - 向管理團隊傳送關於提交失敗的警示電子郵件
    
    **成功流程：**
    - 重新導向至附有申請參考編號的確認頁面
    - 傳送附有後續步驟的確認電子郵件
    - 顯示預估處理時程

**整合特定提示：**

    將此表單連接至**CRM 系統**，建立新的商機。將 @firstName 對應到「姓名」，將 @email 對應到「電子郵件」，將「商機來源」設定為「網頁表單」，將「狀態」設定為「新增」
    
    在提交表單時設定**工作流程觸發程序**。傳遞所有表單資料，並透過管理員通知觸發核准工作流程
    
    設定**資料庫整合**，將表單提交儲存為記錄。替每個提交的上傳檔案建立新資料夾

<!-- ## Import & Convert Existing Forms

**When to use:** When you have existing forms, documents, or designs to transform into modern AEM forms.

**How to use:** Upload your source file and describe the conversion requirements (see [Import Guide](forms-ai-assistant-getting-started.md#2-import-and-convert)).


**Design Import Prompts:**

    Import this **design mockup** and convert it into an adaptive form. Maintain the exact visual design but add proper validation and mobile responsiveness

    Analyze this **image of a paper form** and recreate it digitally. Improve the layout for better mobile experience while keeping all mandatory fields

    Convert this **existing HTML form** to AEM adaptive form format. Preserve all functionality but add AEM-specific features like rules and themes

## Mobile Optimization & Responsiveness

**When to use:** When forms need to work seamlessly across all device types and screen sizes.

**How to use:** Start with basic mobile optimization, then enhance with advanced features. Emphasize mobile-first approach and specify breakpoint behaviors incrementally.

**Example Prompt - Start with Basic Mobile Optimization:**

    Make @contactForm mobile-friendly with:
    
    **Basic Mobile Layout:**
    - Single column layout for all form sections
    - Larger touch targets for buttons and inputs
    - Responsive design that works on phones and tablets

**Then Add Advanced Mobile Features:**

    Enhance @contactForm mobile experience with:
    - Sticky submit button at bottom of screen
    - Touch-friendly date pickers
    - Swipe gestures for multi-step navigation

**Example Prompt - Comprehensive Mobile-First Optimization:**

    Optimize this form for **mobile-first responsive design**:
    
    **Mobile Layout (320px - 768px):**
    - Single column layout for all form sections
    - Larger touch targets (minimum 44px height)
    - Simplified navigation with collapsible sections
    - Sticky submit button at bottom of screen
    - Auto-zoom disabled on input focus
    
    **Tablet Layout (768px - 1024px):**
    - Two-column layout for shorter fields (name, email)
    - Single column for complex fields (address, comments)
    - Side navigation for multi-step forms
    - Optimized for both portrait and landscape
    
    **Desktop Layout (1024px+):**
    - Multi-column layouts where appropriate
    - Horizontal form sections for related fields
    - Sidebar navigation for long forms
    - Hover states and advanced interactions

**Mobile-Specific Prompts:**

    Make this form **touch-friendly** with larger buttons and simplified navigation for mobile users

    Optimize form for **tablet users** with appropriate field sizes and navigation patterns

    Add **swipe gestures** for multi-step form navigation on mobile devices

## Accessibility & Compliance

**When to use:** When forms need to meet accessibility standards (WCAG) or compliance requirements.

**How to use:** Specify the required compliance level and any specific accessibility features needed.

**Example Prompt - Basic Accessibility:**

    Make @contactForm accessible with:
    
    **Basic Accessibility:**
    - Proper ARIA labels for all form fields
    - Keyboard navigation support
    - High contrast color scheme
    - Screen reader compatibility
    - Focus indicators for all interactive elements

**Example Prompt - Advanced Accessibility:**

    Implement comprehensive accessibility for @applicationForm:
    
    **WCAG 2.1 AA Compliance:**
    
    - Semantic HTML structure with proper headings
    - ARIA landmarks and roles for navigation
    - Color contrast ratio of at least 4.5:1
    - Keyboard-only navigation support
    - Screen reader announcements for dynamic content
    
    **Form-Specific Accessibility:**
    
    - Error messages announced to screen readers
    - Field validation with clear error descriptions
    - Progress indicators for multi-step forms
    - Skip navigation links for keyboard users
    - Alternative text for all images and icons
    
    **User Experience:**
    
    - Clear focus indicators on all interactive elements
    - Logical tab order through form fields
    - Descriptive link text and button labels
    - Help text available for complex fields
    - Timeout warnings for session expiration

**Accessibility-Specific Prompts:**

    Add **screen reader support** to this form with proper ARIA labels and announcements

    Implement **keyboard navigation** for all form interactions and navigation elements

    Ensure **color contrast** meets WCAG AA standards for all text and interactive elements  

## Performance Optimization

**When to use:** When forms need to load quickly and perform well under various conditions.

**How to use:** Specify performance requirements and optimization strategies.

**Example Prompt - Basic Performance:**

    
Optimize @contactForm for performance:

**Loading Optimization:**

- Lazy load non-critical form sections
- Minimize initial bundle size
- Optimize images and assets
- Enable caching for static resources
    

**Example Prompt - Advanced Performance:**

    
Implement comprehensive performance optimization for @applicationForm:

**Loading Performance:**

- Progressive loading of form sections
- Optimize images with WebP format
- Minimize JavaScript bundle size
- Enable gzip compression for all assets

**Runtime Performance:**

- Debounce validation calls to reduce API requests
- Optimize conditional logic execution
- Cache frequently used data
- Implement virtual scrolling for long lists

**User Experience:**

- Show loading indicators for async operations
- Provide offline capability for form data
- Auto-save form progress every 30 seconds
- Optimize form submission with retry logic

**Monitoring:**

- Track form load times and user interactions
- Monitor validation performance
- Measure submission success rates
- Alert on performance degradation
    

**Performance-Specific Prompts:**

    
Optimize form **loading speed** by implementing progressive loading and asset optimization
    

    
Add **auto-save functionality** to prevent data loss during form completion
    

    
Implement **offline support** so users can complete forms without internet connection
    

## Testing & Quality Assurance

**When to use:** When forms need comprehensive testing to ensure reliability and user satisfaction.

**How to use:** Specify testing scenarios, validation requirements, and quality metrics.

**Example Prompt - Basic Testing:**

    
Add comprehensive testing for @contactForm:

**Functional Testing:**

- Test all form field validations
- Verify submit functionality works correctly
- Test error handling and user feedback
- Validate conditional logic and rules
    

**Example Prompt - Advanced Testing:**

    
Implement comprehensive testing strategy for @applicationForm:

**Functional Testing:**

- Unit tests for all validation rules
- Integration tests for submit actions
- End-to-end testing for complete user flows
- Cross-browser compatibility testing

**User Experience Testing:**

- Usability testing with target user groups
- Accessibility testing with screen readers
- Mobile device testing on various screen sizes
- Performance testing under load conditions

**Quality Assurance:**

- Automated testing for regression prevention
- Manual testing for edge cases and scenarios
- Security testing for data protection
- Compliance testing for regulatory requirements

**Monitoring:**

- Track form completion rates and abandonment
- Monitor error rates and user feedback
- Measure performance metrics and load times
- Analyze user behavior and interaction patterns
    

**Testing-Specific Prompts:**

    
Add **automated testing** for all form validations and submit functionality
    

    
Implement **user acceptance testing** scenarios for complete form workflows
    

    
Set up **performance monitoring** to track form load times and user interactions
    
-->

## 命令參照

### 基本命令

| 命令 | 最佳使用案例 | 範例 |
|---------|---------------|---------|
| `/create-form` | 開始建立新表單 | `/create-form employee onboarding with personal info and benefits selection` |
| `/add-form` | 將表單新增至頁面中 | `/add-form newsletter signup with email and preferences` |
| `/update-layout` | 變更表單結構 | `/update-layout wizard with 4 steps: info, preferences, review, confirm` |
| `/update-field` | 修改欄位屬性 | `/update-field @email to be mandatory with real-time validation` |
| `/create-rule` | 新增動態行為 | `/create-rule show @spouseInfo if @maritalStatus equals "Married"` |
| `/create-panel` | 整理表單區段 | `/create-panel Employment Details with job title, company, salary fields` |
| `/add-panel` | 轉換設計 | `/add-panel from uploaded form image with field recognition` |
| `/help` | 取得協助 | `/help how to implement multi-step validation?` |

### 欄位參照

使用 `@fieldName` 語法參照提示中的現有欄位：

- `@email` - 參照電子郵件欄位
- `@firstName` - 參照名字欄位
- `@maritalStatus` - 參照婚姻狀況欄位

### 元件類型

**輸入元件：**

- `text`、`email`、`number`、`tel`、`date`、`checkbox`、`radio`、`dropdown`、`file`、`textarea`

**容器元件：**

- `fieldset`、`panel`、`repeatable`、`wizard`

### 元件屬性

**通用屬性 (所有元件)：**

- **類型**：元件類型
- **名稱**：表單提交的欄位識別碼
- **標籤**：顯示欄位的文字
- **描述**：欄位的說明文字
- **可見**：初始可見度的布林值
- **必填**：必填欄位的布林值

**輸入欄位屬性：**

- **值**：預設/初始值
- **預留位置**：輸入欄位的提示文字
- **最小值**：最小的值 (數字/日期適用)
- **最大值**：最大的值 (數字/日期適用)

**檔案上傳屬性：**

- **接受**：文件類型 (.pdf、.doc、.docx、.jpg、.png 等)
- **多個**：用於選擇多個檔案的布林值

**選取控制屬性：**

- **選項**：下拉式選單提供的選擇 (逗號分隔式清單)
- **已勾選**：核取方塊/單選按鈕的預設選擇

**容器屬性：**

- **欄位集**：將相關欄位分組
- **可重複**：可重複區段的布林值

**進階屬性：**

- **可見運算式**：條件式可見度的公式 (=formula)
- **值運算式**：計算值的公式 (=formula)

### 整合命令

**提交動作：**

- 電子郵件通知
- REST API 提交
- 雲端儲存空間 (Azure、SharePoint)
- 工作流程自動化 (Power Automate、Workfront Fusion)
- 行銷平台 (Marketo)
- CRM 整合

### 提示語法指引

- **欄位參照**：為現有欄位使用 `@fieldName`
- **命令**：為特定動作使用 `/command`
- **自然語言**：清楚、具體地描述需求

### 驗證檢查清單

如需了解完整的最佳做法和驗證指引，請參閱[表單體驗建立工具快速入門指南](forms-ai-assistant-getting-started.md#best-practices)。

*此提示程式庫會根據使用者意見回饋和新的表單體驗建立工具功能持續更新。如需了解最新功能和範例，請查看 [AEM Forms 文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html)。*
