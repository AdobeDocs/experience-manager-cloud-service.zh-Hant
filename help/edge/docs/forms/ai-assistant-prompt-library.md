---
title: AEM Forms AI 助理 - 提示程式庫
description: 各種經驗證的提示模式和範例之集合，在表單管理 UI、自適應表單編輯器和通用編輯器中使用 AI 輔助功能建立表單時可以使用。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: 333d42e0-625f-432e-a61b-5d49bf08765a
source-git-commit: abcd5be06b0bf24ebe8737827fb4abdbf148b1b0
workflow-type: ht
source-wordcount: '1613'
ht-degree: 100%

---

# AEM Forms AI 助理 - 提示程式庫

適用於常見的表單建立情境且可重複使用的提示模式和範例的集合。您可以將其視為可根據特定需求進行調整的範本。每個區段說明一個特定使用案例，並提供何時使用的指引以及經驗證的範例。

>[!NOTE]
>
> 早期採用者計劃提供 AEM Forms 適用的 AI 助理。使用您的工作郵件地址發送電子郵件至 mailto:aem-forms-ea@adobe.com 請求存取權限。

>[!IMPORTANT]
>
> **文件內容可能隨時變更**：此提示庫目前正在針對產品進行測試，可能會進行更新和修訂。隨著 AEM Forms 適用的 AI 助理在早期採用者計劃期間不斷發展，相關的提示、範例和最佳實務可能有所變更。

## 獲得最佳結果的最佳實務

為了充分利用 AI 助理，請記住以下提示：

### 簡單開始，逐步建立

從具體的小命令開始 (例如「新增『名字』的文字輸入」)，而不要一開始便使用過於複雜的多步驟請求。這種方法有助於確保準確性，而且運作若不如預期，也可以更輕鬆地進行疑難排解。

**簡單開始的範例：**

```
Add a text input field for "First Name" with placeholder "Enter your first name"
```

**然後逐步建立：**

```
Make @firstName mandatory and add validation message "First name is mandatory"
```

### 使用 AEM Forms 術語

使用「面板」、「文字輸入欄位」、「核取方塊群組」、「提交動作」、「規則」等詞語，讓 AI 助理更加清楚了解。這樣才能確保 AI 在 AEM Forms 的環境中正確地理解您的請求。

**首選詞語：**

- 「文字輸入欄位」而不是「文字方塊」
- 「核取方塊群組」而不是「多個核取方塊」
- 「下拉式選單」而不是「選取清單」
- 「面板」而不是「區段」或「容器」
- 「提交動作」而不是「表單提交」
- 「規則」而不是「邏輯」或「條件」

### 欄位參考明確

在設定現有欄位時，使用 @fieldName 註記 (例如，「將 @firstName 設為必要欄位」)。這樣做有助於 AI 準確識別您所參考的欄位，尤其是在包含許多欄位的複雜表單中。

**範例：**

- `Make @email mandatory with real-time validation`
- `Show @spouseInfo panel when @maritalStatus equals "Married"`
- `Set @country default value to "United States"`

### 務必審查計劃

在點選「套用」之前，請務必仔細審查計劃，了解通用編輯器中由助理建議的變更。AI 會說明其計劃內容，請您花點時間確認其符合您的期望。

### 手動驗證

在助理進行變更後，請務必預覽並測試您的表單，確保其行為和外觀符合預期。AI 是功能強大的工具，但最終驗證是確保品質的關鍵。

**驗證檢查清單：**

- 在預覽模式中測試表單功能
- 驗證條件邏輯是否正常運作
- 檢查行動裝置反應能力
- 測試表單提交
- 驗證無障礙功能

### 反覆修正和改進

如果第一個提示沒有產生準確的結果，請嘗試重新措辭，或將請求拆分成多個小步驟。AI 會從上下文的脈絡中學習，因此提供更具體的細節通常可以改善結果。

**反覆修正的範例：**

1. 第一次嘗試：「設計方便行動裝置使用的表單」
2. 改進：「針對 768px 的行動裝置螢幕將表單版面最佳化，採用單一直欄的版面並加大觸控目標」

### 提供意見回饋

使用內建的意見回饋機制，協助助理學習和改進。您的意見回饋有助於提升 AI 能力並讓所有人受益。


## 逐步開發範例

這些範例說明如何逐步建立表單，從簡單開始，然後逐漸增加複雜度：

### 範例 1：逐步建立聯絡表單

**第 1 步 - 簡單開始：**

```
Create a basic contact form with name, email, and message fields
```

**第 2 步 - 新增驗證：**

```
Make @name and @email mandatory fields with appropriate validation
```

**第 3 步 - 增強使用者體驗：**

```
Add placeholder text: @name "Your full name", @email "your.email@company.com", @message "Tell us how we can help"
```

**步驟 4 - 新增進階功能：**

```
Add a dropdown @inquiryType with options: "General Question", "Support Request", "Sales Inquiry", "Partnership"
```

**步驟 5 - 實作條件邏輯：**

```
Show @urgencyLevel dropdown (Low, Medium, High) only when @inquiryType equals "Support Request"
```

### 範例 2：逐步建立註冊表單

**第 1 步 - 基本結構：**

```
Create a user registration form with personal information panel
```

**第 2 步 - 新增核心欄位：**

```
Add text input fields: @firstName, @lastName, @email, @phone to the personal information panel
```

**第 3 步 - 新增驗證：**

```
Make @firstName, @lastName, and @email mandatory with real-time validation
```

**步驟 4 - 新增帳戶資訊：**

```
Create a new panel "Account Information" with @username and @password fields
```

**第 5 步 - 增強安全性：**

```
Add password confirmation field @confirmPassword with validation to match @password
```

**第 6 步 - 新增偏好設定：**

```
Create "Preferences" panel with @newsletter checkbox and @communicationMethod radio group (Email, SMS, Phone)
```

這種逐步建立的方法可以幫助您：

- 儘早發現問題以免持續惡化
- 全面測試每個功能
- 根據使用者意見回饋進行調整
- 更好地控制開發過程

## 開始建立新表單

**何時使用：**&#x200B;在任何表單專案開始時。這個提示可以幫助 AI 了解您的要求並建立基礎結構。

**使用方法：**&#x200B;從基本結構和核心要求開始。指定表單類型、目標對象和主要用途。在後續的提示中增加複雜度。

**提示範例 - 從簡單開始：**

```
Create a **customer onboarding form** for new bank account applications with:

**Purpose:** Collect personal information for account setup
**Target Users:** New customers applying for checking/savings accounts
**Basic Structure:** Single panel with essential fields
**Core Fields:** Name, email, phone, account type selection

Start with a simple layout that we can enhance step by step.
```

**然後逐步建立：**

```
Add an address panel to @customerOnboardingForm with street address, city, state, and zip code fields
```

```
Add employment information panel with @employer, @jobTitle, and @annualIncome fields
```

```
Add file upload field @identityDocuments for identity verification (Accept: .pdf,.jpg,.png)
```

**其他簡單開始的提示：**

```
Create a basic **event registration form** with name, email, and event selection fields
```

```
Build a simple **contact form** with name, email, and message fields
```

```
Design a basic **feedback survey** with rating scale and comments field
```

## 表單結構和版面

**何時使用：**&#x200B;當您需要整理複雜的表單，或透過改善版面設計來提升使用者體驗時。

**使用方法：**&#x200B;專心處理使用者歷程以及依邏輯將資訊分組。指定版面偏好和導覽模式。

**提示範例 - 多步驟表單結構：**

```
Convert this single-page form into a **3-step wizard** with:

**Step 1: Personal Information**
- Name, email, phone, address fields
- Progress indicator showing "Step 1 of 3"
- "Next" button (validate mandatory fields before proceeding)

**Step 2: Preferences & Requirements** 
- Service selection (checkbox group)
- Budget range (dropdown)
- Timeline preferences (radio group)
- Special requirements (text input field)

**Step 3: Review & Submit**
- Summary of all entered information
- Edit links to go back to specific steps
- Terms and conditions checkbox
- Submit button with confirmation

Include "Previous" and "Next" buttons, allow users to jump between completed steps, save progress automatically.
```

**版面最佳化提示：**

```
Reorganize this form using a **wizard layout** for desktop and single column for mobile. 
```

```
Convert this long form into an **accordion layout** where users can expand/collapse sections.
```

```
Create a **vertical tabbed interface** for this form with tabs for: Basic Info, Contact Details, Preferences, and Review.
```

## 欄位管理與驗證

**何時使用：**&#x200B;當您需要為表單欄位新增、修改或加強特定的驗證規則和行為時。

**使用方法：**&#x200B;具體說明欄位類型、驗證要求和對使用者體驗的期望。使用 @fieldName 語法參考現有欄位。

**提示範例 - 增強欄位功能：**

```
Enhance the form fields with these specific requirements:

**Email Field (@email):**
- Make mandatory with real-time validation
- Show green checkmark when valid format entered
- Display helpful error message: "Please enter a valid email address"
- Add placeholder: "your.email@company.com"

**Phone Number (@phone):**
- Type: tel for mobile optimization
- Make mandatory for business customers, optional for personal
- Add placeholder: "Enter your phone number"

**Date of Birth (@dateOfBirth):**
- Type: date with date picker
- Validate age is 18+ for account opening
- Show error if under 18: "Must be 18 or older to open account"

**File Upload (@documents):**
- Accept: .pdf,.doc,.docx
- Multiple: true for multiple document upload
- Show upload progress and file names after upload
```

**針對欄位的提示：**

```
Add a **file upload field** for resume with these specs: Accept only PDF/DOC/DOCX files, allow multiple files, show upload progress, display file names after upload.
```

```
Create a **dropdown field** for country selection with all countries listed. Set default value based on user's location if available.
```

```
Build a **repeatable panel** for work experience where users can add/remove multiple jobs. Each entry needs: company, title, start date, end date, description.
```

## 條件邏輯和規則

**何時使用：**&#x200B;當您需要根據使用者輸入或業務規則而動態決定表單行為時。

**使用方法：**&#x200B;明確定義條件及所產生的動作。使用特定的欄位參考和邏輯運算子。

**提示範例 - 複雜的條件邏輯：**

```
Implement these conditional rules for the application form:

**Business vs Personal Account Logic:**
- If @accountType equals "Business", show:
  - Business name field (mandatory)
  - Tax ID field (mandatory)
  - Business address section
  - Number of employees dropdown
- If @accountType equals "Personal", hide all business fields

**Income-Based Requirements:**
- If @annualIncome is less than 25000:
  - Show additional verification section
  - Make co-signer information mandatory
  - Display message: "Additional documentation may be required"
- If @annualIncome is greater than 100000:
  - Show premium services options
  - Enable priority processing checkbox

**Age-Based Validation:**
- If @age is under 18:
  - Show parent/guardian information section
  - Make parent signature upload mandatory
  - Change submit button text to "Submit for Review"
- If @age is 65 or older:
  - Show senior discount options
  - Add accessibility preferences section
```

**針對規則的提示：**

```
Create a **visibility rule** that shows @spouseInformation panel only when @maritalStatus equals "Married" or "Domestic Partnership".
```

```
Add **progressive disclosure** where additional questions appear based on previous answers. Start with basic info, then show relevant follow-ups.
```

```
Implement **smart defaults** where @country selection auto-sets related fields. Allow manual override.
```

## 資料整合與提交

**何時使用：**&#x200B;當您需要將表單連接到後端系統、資料庫或外部服務時。

**使用方法：**&#x200B;從基本的提交設定開始，然後逐步增加其他整合。指定整合類型、資料格式要求和錯誤處理偏好。

**提示範例 - 從基本提交開始：**

```
Configure basic form submission for @applicationForm:

**Primary Submission:**
- Send form data to REST endpoint: `/api/v1/applications`
- Format data as JSON
- Show success message: "Application submitted successfully"
- Show error message if submission fails: "Submission failed, please try again"
```

**然後逐步新增次要動作：**

```
Add email notification to @applicationForm: Send confirmation email to @email address with application reference number
```

```
Add CRM integration to @applicationForm: Create new lead record with @firstName, @lastName, @email, and set Status to "New Application"
```

**提示範例 - 進階多管道提交：**

```
Configure form submission with multiple data destinations:

**Primary Submission:**
- Send form data to REST endpoint: `/api/v1/applications`
- Include authentication header with API key
- Format data as JSON with nested objects for address and employment
- Handle success response (201) by showing thank you message

**Secondary Actions:**
- Send notification email to applicant at @email address
- Copy application data to tracking system
- Trigger workflow for approval process
- Create record in CRM with lead status "New Application"

**Error Handling:**
- If primary submission fails, save data locally and retry
- Show user-friendly error message: "Submission temporarily unavailable"
- Provide option to download form data as backup
- Send alert email to admin team about failed submission

**Success Flow:**
- Redirect to confirmation page with application reference number
- Send confirmation email with next steps
- Display estimated processing timeline
```

**針對整合的提示：**

```
Connect this form to **CRM system** to create new leads. Map @firstName to FirstName, @email to Email, set LeadSource to "Web Form", and Status to "New".
```

```
Set up **workflow trigger** when form is submitted. Pass all form data and trigger approval workflow with manager notification.
```

```
Configure **database integration** to save form submissions as records. Create new folder for each submission with uploaded documents.
```

## 設計匯入和轉換

**何時使用：**&#x200B;當您現有的表單設計 (PDF、Figma、影像) 需要轉換成功能性 AEM 表單時。

**使用方法：**&#x200B;提供有關來源設計的清楚背景資訊，並指定所需的任何修改或增強。

**提示範例 - PDF 表單轉換：**

```
Convert this uploaded **PDF application form** into a functional AEM adaptive form:

**Source Analysis:**
- Analyze the PDF layout and identify all form fields
- Preserve the visual hierarchy and grouping
- Maintain the professional appearance and branding

**Field Mapping:**
- Convert PDF text fields to adaptive form text inputs
- Transform checkboxes to checkbox components
- Convert dropdown lists to AEM dropdown components
- Map signature areas to digital signature fields

**Enhancements:**
- Add real-time validation that wasn't possible in PDF
- Implement conditional logic for dependent fields
- Make the form responsive for mobile devices
- Add progress saving capability
- Include accessibility improvements (ARIA labels, keyboard navigation)

**Styling:**
- Match the original color scheme and fonts
- Maintain professional business appearance
- Ensure consistent spacing and alignment
- Add subtle animations for better user experience

Preserve all original field labels and help text, but improve the user experience with modern form interactions.
```

**設計匯入提示：**

```
Import this **design mockup** and convert it into an adaptive form. Maintain the exact visual design but add proper validation and mobile responsiveness.
```

```
Analyze this **image of a paper form** and recreate it digitally. Improve the layout for better mobile experience while keeping all mandatory fields.
```

```
Convert this **existing HTML form** to AEM adaptive form format. Preserve all functionality but add AEM-specific features like rules and themes.
```

## 行動裝置最佳化和回應能力

**何時使用：**&#x200B;當表單需要在所有裝置類型和螢幕尺寸上皆可順暢運作時。

**使用方法：**&#x200B;從基本的行動裝置最佳化開始，然後透過進階功能增強。強調行動裝置優先的方法並逐步指定斷點行為。

**提示範例 - 從基本的行動裝置最佳化開始：**

```
Make @contactForm mobile-friendly with:

**Basic Mobile Layout:**
- Single column layout for all form sections
- Larger touch targets for buttons and inputs
- Responsive design that works on phones and tablets
```

**然後新增進階行動裝置功能：**

```
Enhance @contactForm mobile experience with:
- Sticky submit button at bottom of screen
- Touch-friendly date pickers
- Swipe gestures for multi-step navigation
```

**提示範例 - 全面的行動裝置優先最佳化：**

```
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

**Touch Optimization:**
- Larger checkbox and radio button targets
- Swipe gestures for multi-step navigation
- Pull-to-refresh for saved drafts
- Touch-friendly date/time pickers

**Performance:**
- Lazy load non-critical form sections
- Optimize images and icons for mobile
- Minimize JavaScript for faster loading
- Progressive enhancement approach
```

**針對行動裝置的簡單提示：**

```
Make @checkoutForm mobile-optimized with large buttons and one-thumb navigation
```

```
Add touch-friendly controls to @surveyForm for tablet users
```

```
Enable offline functionality for @applicationForm with local data saving
```

## 無障礙與合規性

**何時使用：**&#x200B;表單必須符合無障礙標準 (WCAG 2.1 AA) 或合規性要求。

**使用方法：**&#x200B;指定必須符合的無障礙要求和合規標準。

**提示範例 - 無障礙實作：**

```
Make this form **WCAG 2.1 AA compliant** with these accessibility features:

**Keyboard Navigation:**
- Logical tab order through all form elements
- Skip links to main content and form sections
- Keyboard shortcuts for common actions
- Focus indicators clearly visible on all interactive elements

**Screen Reader Support:**
- Proper ARIA labels for all form fields
- Descriptive error messages announced to screen readers
- Form section headings with proper hierarchy (h1, h2, h3)
- Progress announcements for multi-step forms

**Visual Accessibility:**
- Color contrast ratio minimum 4.5:1 for text
- Don't rely solely on color to convey information
- Text size minimum 16px for body text
- Scalable up to 200% without horizontal scrolling

**Motor Accessibility:**
- Large click targets (minimum 44x44px)
- Generous spacing between interactive elements
- No time limits or provide extension options
- Alternative input methods support

**Cognitive Accessibility:**
- Clear, simple language in all instructions
- Consistent navigation and layout patterns
- Error prevention and clear error recovery
- Help text and examples for complex fields

**Testing Requirements:**
- Test with screen readers (NVDA, JAWS, VoiceOver)
- Verify keyboard-only navigation
- Check color contrast with automated tools
- Validate HTML for semantic correctness
```

**針對合規性的提示：**

```
Ensure this **healthcare form meets HIPAA requirements** with proper data encryption, audit logging, and privacy controls.
```

```
Make this **financial form PCI DSS compliant** with secure payment field handling and data protection measures.
```

```
Create a **government form meeting Section 508 standards** with full accessibility and plain language requirements.
```

## 測試與品質保證

**何時使用：**&#x200B;當您需要驗證表單功能、使用者體驗和技術效能時。

**使用方法：**&#x200B;指定必須驗證的測試場景、邊緣案例和品質標準。

**提示範例 - 綜合表單測試：**

```
Create a **comprehensive testing plan** for this application form:

**Functional Testing:**
- Test all field validations with valid and invalid data
- Verify conditional logic shows/hides fields correctly
- Test file upload with various file types and sizes
- Validate calculation fields update correctly
- Test form submission with complete and incomplete data

**User Experience Testing:**
- Test form completion time (target: under 10 minutes)
- Verify error messages are helpful and actionable
- Test progress saving and restoration
- Validate mobile touch interactions
- Check form accessibility with assistive technologies

**Edge Case Testing:**
- Test with extremely long text inputs
- Verify behavior with special characters and emojis
- Test with slow internet connections
- Validate offline functionality if applicable
- Test browser back/forward button behavior

**Performance Testing:**
- Measure form load time (target: under 3 seconds)
- Test with large file uploads
- Verify memory usage with long form sessions
- Test concurrent user submissions
- Validate database performance under load

**Security Testing:**
- Test input sanitization and XSS prevention
- Verify CSRF protection is working
- Test file upload security restrictions
- Validate data encryption in transit and at rest
- Check authentication and authorization controls

**Cross-Browser Testing:**
- Test on Chrome, Firefox, Safari, Edge
- Verify mobile browsers (iOS Safari, Chrome Mobile)
- Test on different operating systems
- Validate older browser fallbacks
- Check print functionality across browsers
```

**針對測試的提示：**

```
Create **automated test scripts** for this form's critical user paths: successful submission, validation errors, and conditional logic.
```

```
Design a **user acceptance testing plan** with realistic scenarios and success criteria for business stakeholders.
```

```
Set up **performance monitoring** to track form completion rates, abandonment points, and submission success rates.
```

## 進階功能和整合

**何時使用：**&#x200B;當您需要精密的表單功能 (例如 AI 輔助、進階工作流程或複雜整合) 時。

**使用方法：**&#x200B;明確定義進階功能和整合要求。

**提示範例 - AI 增強表單：**

```
Add **AI-powered features** to enhance this application form:

**Smart Auto-Complete:**
- Use AI to suggest company names as user types
- Auto-populate address fields from partial input
- Suggest job titles based on industry selection
- Provide intelligent form completion suggestions

**Dynamic Question Generation:**
- Generate follow-up questions based on previous answers
- Adapt form complexity to user's experience level
- Show relevant optional fields based on user profile
- Personalize form sections for different user types

**Intelligent Validation:**
- Use AI to detect potentially incorrect information
- Suggest corrections for common data entry errors
- Validate business information against public databases
- Flag suspicious or inconsistent responses

**Content Optimization:**
- A/B test different form layouts automatically
- Optimize field order based on completion patterns
- Adjust form length based on user engagement
- Personalize help text based on user behavior

**Predictive Analytics:**
- Predict likelihood of form completion
- Identify users who might need assistance
- Suggest optimal times for form completion reminders
- Analyze drop-off points and suggest improvements

**Natural Language Processing:**
- Allow voice input for text fields
- Convert speech to text for accessibility
- Analyze open-text responses for sentiment
- Extract structured data from unstructured input
```

**進階整合提示：**

```
Integrate with **CRM system** to pre-populate known customer data, update records in real-time, and trigger automated follow-up sequences.
```

```
Connect to **payment gateway** for secure transaction processing with PCI compliance, fraud detection, and multiple payment methods.
```

```
Implement **blockchain verification** for document authenticity, immutable audit trails, and decentralized identity verification.
```

## 疑難排解和最佳化

**何時使用：**&#x200B;當表單出現效能問題、使用者體驗問題或技術困難時。

**使用方法：**&#x200B;清楚描述具體問題和想要的結果。

**提示範例 - 效能最佳化：**

```
Optimize this form for **better performance and user experience**:

**Current Issues:**
- Form takes 8+ seconds to load on mobile
- Users are abandoning at the address section (60% drop-off)
- File uploads frequently fail or timeout
- Validation errors are confusing users

**Performance Improvements:**
- Implement lazy loading for non-critical form sections
- Optimize images and reduce bundle size
- Add progressive loading indicators
- Cache frequently used data (country lists, etc.)
- Minimize JavaScript execution time

**User Experience Fixes:**
- Simplify the address section with auto-complete
- Add inline validation with helpful error messages
- Implement smart defaults based on user location
- Add progress saving every 30 seconds
- Provide clear instructions for each section

**Technical Optimizations:**
- Implement chunked file uploads with resume capability
- Add client-side validation before server submission
- Optimize database queries for faster responses
- Implement proper error handling and retry logic
- Add comprehensive logging for debugging

**Monitoring & Analytics:**
- Set up form analytics to track user behavior
- Monitor completion rates by section
- Track error rates and types
- Measure performance metrics continuously
- A/B test improvements with real users
```

**疑難排解提示：**

```
**Debug this form submission error:** Users report getting "500 Internal Server Error" when submitting. Check validation logic, server endpoints, and data formatting.
```

```
**Fix mobile layout issues:** Form fields are overlapping on iPhone screens and submit button is not visible. Ensure proper responsive design.
```

```
**Resolve validation conflicts:** Some users can't submit even with valid data. Review validation rules for conflicts and edge cases.
```

## 特定環境的最佳實務

### 表單管理 UI

**何時使用：**&#x200B;用於高階表單建立和管理任務。

```
In Forms Management UI, create a new **customer survey template** that can be reused across different departments. Include standard branding, common field types, and configurable sections.
```

### 自適應表單編輯器

**何時使用：**&#x200B;要進行詳細的表單設定和建立複雜規則時使用。

```
In the Adaptive Forms Editor, configure **advanced business rules** for this loan application: calculate debt-to-income ratio, determine eligibility, and show appropriate next steps.
```

### 通用編輯器

**何時使用：**&#x200B;適用於具有視覺化編輯功能的 Edge Delivery Services 表單。

```
In Universal Editor, create a **responsive contact form** for the company website. Ensure it matches the site design and integrates with the existing content management workflow.
```

## 命令參考快速指南

| 命令 | 最佳使用案例 | 範例 |
|---------|---------------|---------|
| `/create-form` | 開始建立新表單 | `/create-form employee onboarding with personal info and benefits selection` |
| `/add-form` | 將表單新增至頁面中 | `/add-form newsletter signup with email and preferences` |
| `/update-layout` | 變更表單結構 | `/update-layout wizard with 4 steps: info, preferences, review, confirm` |
| `/update-field` | 修改欄位屬性 | `/update-field @email to be mandatory with real-time validation` |
| `/create-rule` | 新增動態行為 | `/create-rule show @spouseInfo if @maritalStatus equals "Married"` |
| `/create-panel` | 整理表單區段 | `/create-panel Employment Details with job title, company, salary fields` |
| `/add-panel` | 轉換設計 | `/add-panel from uploaded form image with field recognition` |
| `/configure-submit` | 設定資料處理方式 | `/configure-submit to CRM and send confirmation email` |
| `/help` | 取得協助 | `/help how to implement multi-step validation?` |

## 受支援的元件屬性參考

### 通用屬性 (所有元件)

- **類型**：元件類型 (文字、電子郵件、數字、電話、日期、核取方塊、單選按鈕、下拉式選單、檔案等)
- **名稱**：表單提交的欄位識別碼
- **標籤**：顯示欄位的文字
- **描述**：欄位的說明文字
- **可見**：初始可見度的布林值
- **必填**：必填欄位的布林值

### 輸入欄位屬性

- **值**：預設/初始值
- **預留位置**：輸入欄位的提示文字
- **最小值**：最小的值 (數字/日期適用)
- **最大值**：最大的值 (數字/日期適用)

### 檔案上傳屬性

- **接受**：文件類型 (.pdf、.doc、.docx、.jpg、.png 等)
- **多個**：用於選擇多個檔案的布林值

### 選取控制屬性

- **選項**：下拉式選單提供的選擇 (逗號分隔式清單)
- **已勾選**：核取方塊/單選按鈕的預設選擇

### 容器屬性

- **欄位集**：將相關欄位分組
- **可重複**：可重複區段的布林值

### 進階屬性

- **可見運算式**：條件式可見度的公式 (=formula)
- **值運算式**：計算值的公式 (=formula)

## 最佳實務摘要

### 技術準則

- **僅使用受支援的屬性**，依照官方 AEM Forms 元件規格所示
- 欄位參考 (@fieldName) 和運算式 (=formula) **須使用正確語法**
- 在每一項變更後&#x200B;**進行漸進式測試**，以便及早發現問題
- 從一開始就&#x200B;**規劃無障礙設計**，而不是事後才想到
- 每一個設計決策均&#x200B;**考慮行動裝置使用者**
- **將複雜的規則記錄在案**，方便未來維護和團隊協作

### 策略方法

- **從使用者需求入手** - 專注於使用者需要完成的任務，而不只是技術功能
- **以完成表單填寫為設計目標** - 在表單設計中盡量減少摩擦和認知負荷
- 提前&#x200B;**規劃資料流** - 考慮處理、儲存和使用資料的方式
- **建立具擴充性的表單** - 設計可以處理預期的使用者數量和資料增長的表單
- **實作漸進式增強** - 確保基本功能運作正常，然後新增進階功能

### 需要避免的常見陷阱

- **初始請求過於複雜** - 將大型任務分解為更小、更易於管理的多個步驟
- **使用不支援的屬性**，即不在 AEM Forms 規格中的屬性
- **忽略行動裝置體驗**，直到開發過程後期才處理
- **略過使用者測試**，包括使用真實情境和邊緣案例的測試
- **假設 AI 可以理解背景脈絡**，卻未提供明確、具體的指示
- **忘記無障礙設計**&#x200B;和合規性要求
- **未驗證相關變更**&#x200B;便進入下一步驟

### 品質保證方法

1. **經常預覽** - 每次進行重大變更後，都以預覽模式檢查您的工作
2. **測試邊緣案例** - 嘗試不尋常的輸入、長篇文字、特殊字元
3. **跨裝置驗證** - 在行動裝置、平板電腦和桌上型電腦上進行測試
4. **檢查無障礙設計** - 檢查鍵盤導覽功能和螢幕閱讀器相容性
5. **效能測試** - 確保表單快速載入並順暢回應
6. **使用者接受度測試** - 部署之前先讓真實使用者測試表單


*此提示程式庫會根據使用者意見回饋和新的 AI 助理功能持續更新。如需了解最新功能和範例，請查看 [AEM Forms 文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html)。*
