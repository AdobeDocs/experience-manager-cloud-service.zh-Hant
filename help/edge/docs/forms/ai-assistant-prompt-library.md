---
title: AEM Forms AI助理 — 提示程式庫
description: 用於透過Forms Management UI、Adaptive Forms Editor和Universal Editor的AI協助建立表單的已驗證提示模式和範例集合。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: d3ade6ee9216b44b55d6808d8acffe83f1e263c9
workflow-type: tm+mt
source-wordcount: '1613'
ht-degree: 0%

---



# AEM Forms AI助理 — 提示程式庫

可重複使用的提示模式集合，以及常見表單建立案例的範例。 您可以將這些視為可適應您特定需求的範本。 每個區段都涵蓋特定使用案例，其中包含使用時機的相關指引以及實證範例。

>[!NOTE]
>
> 適用於AEM Forms的AI Assistant可在率先採用者計畫下取得。 從您的工作地址傳送電子郵件至mailto:aem-forms-ea@adobe.com以請求存取權。

>[!IMPORTANT]
>
> **檔案可能會變更**：此提示程式庫目前正針對產品進行測試，可能會有更新和修訂。 提示、範例和最佳實務可能會隨著AEM Forms的AI Assistant在早期採用者計畫中的持續進化而改變。

## 取得最佳結果的最佳實務

若要充分利用AI Assistant，請記住以下秘訣：

### 開始簡單，逐步建置

從較小的特定命令開始（例如「為『名字』新增文字輸入」），而不是一開始過於複雜的多步驟請求。 此方法有助於確保準確性，並在某些專案未按預期運作時，讓疑難排解變得更容易。

**簡單開始範例：**

```
Add a text input field for "First Name" with placeholder "Enter your first name"
```

**然後逐步建置：**

```
Make @firstName mandatory and add validation message "First name is mandatory"
```

### 使用AEM Forms術語

使用「面板」、「文字輸入欄位」、「核取方塊群組」、「提交動作」、「規則」等詞語，讓助理更易於瞭解。 這可確保AI在AEM Forms內容中正確解讀您的請求。

**偏好的字詞：**

- 「文字輸入欄位」而非「文字方塊」
- 「核取方塊群組」而非「核取方塊」
- &quot;dropdown&quot;而非&quot;select list&quot;
- 「面板」而非「區段」或「容器」
- 「提交動作」而非「表單提交」
- &quot;rule&quot;而非&quot;logic&quot;或&quot;condition&quot;

### 清楚的參考欄位

設定現有欄位時，請使用@fieldName記號(例如「@firstName為必填」)。 這有助於AI準確地識別您參考的欄位，尤其是在具有許多欄位的複雜表單中。

**範例：**

- `Make @email mandatory with real-time validation`
- `Show @spouseInfo panel when @maritalStatus equals "Married"`
- `Set @country default value to "United States"`

### 一律檢閱計畫

在按一下「套用」之前，請務必仔細檢閱助理員在「通用編輯器」中提議的變更計畫。 AI會向您顯示其打算執行的操作 — 請花點時間確認這符合您的預期。

### 手動驗證

助理完成變更後，請一律預覽及測試您的表單，確保表單如預期般運作和顯示。 AI是一個強大的工具，但最終驗證是確保品質的關鍵。

**驗證檢查清單：**

- 在預覽模式下測試表單功能
- 驗證條件邏輯是否正確運作
- 檢查行動裝置回應能力
- 測試表單提交
- 驗證協助工具功能

### 反複和調整

如果第一個提示並未產生完全相同的結果，請嘗試重新措辭或將請求分成較小的步驟。 AI會從情境學習，因此提供更具體的細節通常可以改善結果。

**反複專案範例：**

1. 第一次嘗試：「讓表單適合行動裝置」
2. 細化：「透過單欄版面配置與較大的觸控目標，針對768px以下的行動熒幕最佳化表單版面」

### 提供意見回饋

使用內建的意見回饋機制來協助助理學習和改善。 您的意見回饋有助於讓AI對每個人都更好。


## 增量開發範例

這些範例說明如何逐步建立表單，從簡單開始，逐步增加複雜性：

### 範例1：逐步建立連絡人表單

**步驟1 — 開始簡單：**

```
Create a basic contact form with name, email, and message fields
```

**步驟2 — 新增驗證：**

```
Make @name and @email mandatory fields with appropriate validation
```

**步驟3 — 增強使用者體驗：**

```
Add placeholder text: @name "Your full name", @email "your.email@company.com", @message "Tell us how we can help"
```

**步驟4 — 新增進階功能：**

```
Add a dropdown @inquiryType with options: "General Question", "Support Request", "Sales Inquiry", "Partnership"
```

**步驟5 — 實作條件式邏輯：**

```
Show @urgencyLevel dropdown (Low, Medium, High) only when @inquiryType equals "Support Request"
```

### 範例2：逐步建立登錄檔單

**步驟1 — 基本結構：**

```
Create a user registration form with personal information panel
```

**步驟2 — 新增核心欄位：**

```
Add text input fields: @firstName, @lastName, @email, @phone to the personal information panel
```

**步驟3 — 新增驗證：**

```
Make @firstName, @lastName, and @email mandatory with real-time validation
```

**步驟4 — 新增帳戶資訊：**

```
Create a new panel "Account Information" with @username and @password fields
```

**步驟5 — 增強安全性：**

```
Add password confirmation field @confirmPassword with validation to match @password
```

**步驟6 — 新增偏好設定：**

```
Create "Preferences" panel with @newsletter checkbox and @communicationMethod radio group (Email, SMS, Phone)
```

此漸進式方法可協助您：

- 在問題複合之前及早擷取問題
- 徹底測試每個功能
- 根據使用者意見做出調整
- 維持對開發流程的更好控制

## 開始新的Forms

**何時使用：**&#x200B;在任何表單專案的開頭。 此提示可協助AI瞭解您的需求並建立基礎結構。

**如何使用：**&#x200B;從基本結構和核心需求開始。 指定表單型別、目標對象和主要用途。 在後續提示中新增複雜性。

**範例提示 — 開始簡單：**

```
Create a **customer onboarding form** for new bank account applications with:

**Purpose:** Collect personal information for account setup
**Target Users:** New customers applying for checking/savings accounts
**Basic Structure:** Single panel with essential fields
**Core Fields:** Name, email, phone, account type selection

Start with a simple layout that we can enhance step by step.
```

**然後逐步建置：**

```
Add an address panel to @customerOnboardingForm with street address, city, state, and zip code fields
```

```
Add employment information panel with @employer, @jobTitle, and @annualIncome fields
```

```
Add file upload field @identityDocuments for identity verification (Accept: .pdf,.jpg,.png)
```

**替代簡單啟動提示：**

```
Create a basic **event registration form** with name, email, and event selection fields
```

```
Build a simple **contact form** with name, email, and message fields
```

```
Design a basic **feedback survey** with rating scale and comments field
```

## 表單結構與版面

**何時使用：**&#x200B;當您需要組織複雜的表單或透過更好的版面設計改善使用者體驗時。

**如何使用：**&#x200B;著重於使用者歷程和資訊的邏輯分組。 指定版面偏好設定和導覽模式。

**範例提示 — 多步驟表單結構：**

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

**配置最佳化提示：**

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

**何時使用：**&#x200B;您需要新增、修改或增強具有特定驗證規則和行為的表單欄位時。

**使用方式：**&#x200B;請具體說明欄位型別、驗證要求和使用者體驗期望。 使用@fieldName語法參考現有欄位。

**範例提示 — 欄位增強功能：**

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

**欄位特定提示：**

```
Add a **file upload field** for resume with these specs: Accept only PDF/DOC/DOCX files, allow multiple files, show upload progress, display file names after upload.
```

```
Create a **dropdown field** for country selection with all countries listed. Set default value based on user's location if available.
```

```
Build a **repeatable panel** for work experience where users can add/remove multiple jobs. Each entry needs: company, title, start date, end date, description.
```

## 條件式邏輯和規則

**何時使用：**&#x200B;當您需要根據使用者輸入或商業規則的動態表單行為時。

**使用方式：**&#x200B;清楚定義條件和產生的動作。 使用特定的欄位參考和邏輯運運算元。

**範例提示 — 複雜條件邏輯：**

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

**規則特定提示：**

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

**何時使用：**&#x200B;當您需要將表單連線到後端系統、資料庫或外部服務時。

**如何使用：**&#x200B;從基本提交設定開始，然後逐步新增其他整合。 指定整合型別、資料格式需求和錯誤處理偏好設定。

**範例提示 — 以基本提交開始：**

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

**範例提示 — 進階多頻道提交：**

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

**整合專用提示：**

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

**何時使用：**&#x200B;當您有現有的表單設計(PDF、Figma、影像)需要轉換為功能性的AEM表單時。

**如何使用：**&#x200B;提供來源設計的明確內容，並指定所需的任何修改或增強功能。

**範例提示 — PDF表單轉換：**

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

## 行動最佳化與回應能力

**何時使用：**&#x200B;當表單需要在所有裝置型別和熒幕大小之間順暢運作時。

**如何使用：**&#x200B;從基本行動裝置最佳化開始，然後使用進階功能增強。 強調行動優先方法並以增量方式指定中斷點行為。

**範例提示 — 從基本行動最佳化開始：**

```
Make @contactForm mobile-friendly with:

**Basic Mobile Layout:**
- Single column layout for all form sections
- Larger touch targets for buttons and inputs
- Responsive design that works on phones and tablets
```

**然後新增進階行動功能：**

```
Enhance @contactForm mobile experience with:
- Sticky submit button at bottom of screen
- Touch-friendly date pickers
- Swipe gestures for multi-step navigation
```

**範例提示 — 完整的行動優先最佳化：**

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

**行動專屬簡單提示：**

```
Make @checkoutForm mobile-optimized with large buttons and one-thumb navigation
```

```
Add touch-friendly controls to @surveyForm for tablet users
```

```
Enable offline functionality for @applicationForm with local data saving
```

## 協助工具與法規遵循

**使用時機：**&#x200B;表單必須符合協助工具標準(WCAG 2.1 AA)或法規遵循需求。

**使用方式：**&#x200B;指定必須滿足的協助工具需求和法規遵循標準。

**範例提示 — 協助工具實作：**

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

**規範遵循特定提示：**

```
Ensure this **healthcare form meets HIPAA requirements** with proper data encryption, audit logging, and privacy controls.
```

```
Make this **financial form PCI DSS compliant** with secure payment field handling and data protection measures.
```

```
Create a **government form meeting Section 508 standards** with full accessibility and plain language requirements.
```

## 測試與品質Assurance

**何時使用：**&#x200B;當您需要驗證表單功能、使用者體驗和技術效能時。

**如何使用：**&#x200B;指定必須驗證的測試案例、邊緣案例和品質條件。

**範例提示 — 完整的表單測試：**

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

**測試專用提示：**

```
Create **automated test scripts** for this form's critical user paths: successful submission, validation errors, and conditional logic.
```

```
Design a **user acceptance testing plan** with realistic scenarios and success criteria for business stakeholders.
```

```
Set up **performance monitoring** to track form completion rates, abandonment points, and submission success rates.
```

## 進階功能與整合

**何時使用：**&#x200B;當您需要複雜的表單功能，例如AI協助、進階工作流程或複雜的整合。

**使用方式：**&#x200B;清楚定義進階功能與整合需求。

**範例提示 — AI增強型表單：**

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

## 疑難排解與最佳化

**何時使用：**&#x200B;當表單發生效能問題、使用者體驗問題或技術困難時。

**使用方式：**&#x200B;請清楚描述特定問題和所要的結果。

**範例提示 — 效能最佳化：**

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

### Forms管理UI

**何時使用：**&#x200B;針對高階表單建立和管理工作。

```
In Forms Management UI, create a new **customer survey template** that can be reused across different departments. Include standard branding, common field types, and configurable sections.
```

### 最適化Forms編輯器

**何時使用：**&#x200B;詳細表單設定和複雜規則建立。

```
In the Adaptive Forms Editor, configure **advanced business rules** for this loan application: calculate debt-to-income ratio, determine eligibility, and show appropriate next steps.
```

### 通用編輯器

**何時使用：**&#x200B;針對具有視覺化編輯功能的Edge Delivery Services表單。

```
In Universal Editor, create a **responsive contact form** for the company website. Ensure it matches the site design and integrates with the existing content management workflow.
```

## 命令參考快速指南

| 指令 | 最佳使用案例 | 範例 |
|---------|---------------|---------|
| `/create-form` | 開始新表單 | `/create-form employee onboarding with personal info and benefits selection` |
| `/add-form` | 新增表單至頁面 | `/add-form newsletter signup with email and preferences` |
| `/update-layout` | 變更表單結構 | `/update-layout wizard with 4 steps: info, preferences, review, confirm` |
| `/update-field` | 修改欄位屬性 | `/update-field @email to be mandatory with real-time validation` |
| `/create-rule` | 新增動態行為 | `/create-rule show @spouseInfo if @maritalStatus equals "Married"` |
| `/create-panel` | 組織表單區段 | `/create-panel Employment Details with job title, company, salary fields` |
| `/add-panel` | 轉換設計 | `/add-panel from uploaded form image with field recognition` |
| `/configure-submit` | 設定資料處理 | `/configure-submit to CRM and send confirmation email` |
| `/help` | 取得協助 | `/help how to implement multi-step validation?` |

## 支援的元件屬性參考

### 通用屬性（所有元件）

- **型別**：元件型別（文字、電子郵件、數字、電話、日期、核取方塊、無線電、下拉式清單、檔案等）
- **名稱**：表單提交的欄位識別碼
- **標籤**：顯示欄位的文字
- **描述**：欄位的說明文字
- **可見**：初始可見性的布林值
- **必要欄位**：必要欄位的布林值

### 輸入欄位屬性

- **值**：預設/初始值
- **預留位置**：輸入欄位的提示文字
- **分鐘**：最小值（數字/日期）
- **最大值**：最大值（數字/日期）

### 檔案上傳屬性

- **接受**：檔案型別（.pdf、.doc、.docx、.jpg、.png等）
- **多個**：多個檔案選取範圍的布林值

### 選取控制項屬性

- **選項**：下拉式清單的選擇（逗號分隔清單）
- **已核取**：核取方塊/選項預設選項

### 容器屬性

- **欄位集**：群組相關欄位
- **可重複**：可重複區段的布林值

### 進階屬性

- **可見的運算式**：條件式可見性的公式(=formula)
- **值運算式**：計算值的公式(=formula)

## 最佳實務摘要

### 技術准則

- **僅使用官方AEM Forms元件規格中的支援屬性**
- **請遵循欄位參考(@fieldName)和運算式(=formula)的正確語法**
- 每次變更後&#x200B;**逐步測試**，以及早發現問題
- **從頭開始規劃協助工具**，而不是作為事後考量
- 在每一個設計決定中考慮&#x200B;**行動使用者**
- **記錄複雜規則**，以供未來維護和團隊共同作業

### 策略方法

- **從使用者需求開始** — 著重於使用者需要完成的工作，而不只是技術功能
- **完成設計** — 將表單設計中的摩擦和認知負荷降至最低
- **提前規劃資料流程** — 考慮資料如何處理、儲存及使用
- **為規模建置** — 可處理預期的使用者數量和資料成長的設計表單
- **實作漸進式增強功能** — 確定基本功能可正常運作，然後新增進階功能

### 要避免的常見陷阱

- **過於複雜的初始要求** — 將大型工作分解成較小且可管理的步驟
- **使用不支援的屬性**，不在AEM Forms規格中
- **正在忽略行動體驗**，直到開發程式延遲
- **正在略過使用者測試**&#x200B;真實案例和邊緣案例
- **假設AI瞭解內容**，但不提供明確、特定的指示
- **忘記協助工具**&#x200B;和法規遵循要求
- 在移至下一個步驟之前&#x200B;**未驗證變更**

### 高品質Assurance方法

1. **經常預覽** — 每次重大變更後，在預覽模式下檢查您的工作
2. **測試邊緣案例** — 嘗試不尋常的輸入、長文字、特殊字元
3. **跨裝置驗證** — 在行動裝置、平板電腦和桌上型電腦上測試
4. **檢查協助工具** — 確認鍵盤導覽與熒幕助讀程式的相容性
5. **效能測試** — 確保表單載入快速且回應順暢
6. **使用者驗收測試** — 在部署之前讓真實的使用者測試表單


*此提示程式庫會根據使用者意見與新的AI助理功能持續更新。 如需最新功能和範例，請檢視[AEM Forms檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=zh-Hant)。*
