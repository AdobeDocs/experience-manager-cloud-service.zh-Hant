---
title: Forms Experience Builder — 提示資料庫
description: 各種經驗證的提示模式和範例之集合，在表單管理 UI、自適應表單編輯器和通用編輯器中使用 AI 輔助功能建立表單時可以使用。
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: c8f64082-a23f-4919-ad66-042faad77d31
source-git-commit: 9996bc602ae6169dd1aade622d5dbc5b1addeb54
workflow-type: tm+mt
source-wordcount: '1338'
ht-degree: 28%

---


# Forms Experience Builder — 提示資料庫

針對Forms Experience Builder最佳化的可重複使用提示模式和範例的集合。 這個簡化的程式庫著重於兩種核心建立方法：從頭開始建立和匯入與轉換，並增強LLM支援的智慧欄位和品牌一致性支援。

>[!NOTE]
>
> 率先採用者程式下提供Forms Experience Builder 。 從您的工作地址傳送電子郵件給`aem-forms-ea@adobe.com`以要求存取權。

>[!IMPORTANT]
>
> **文件內容可能隨時變更**：此提示庫目前正在針對產品進行測試，可能會進行更新和修訂。提示、範例和最佳實務可能會隨著Forms Experience Builder在早期採用者計畫中的持續進化而改變。

## 使用此提示程式庫

此程式庫為常見的表單建立案例提供可重複使用的提示模式。 如需完整的最佳作法，請參閱[Forms Experience Builder快速入門手冊](forms-ai-assistant-getting-started.md#best-practices)。

### 此資料庫的快速提示

- **從範例開始** — 使用提供的提示作為範本並調整您的需求
- **兩種建立方法** — 選擇「從頭開始建立」或「匯入並轉換」方法
- **要明確** — 將您自己的詳細資料加入一般範例
- **徹底測試** — 一律在您的特定環境中驗證結果

### 品牌範本和樣式

**預先準備品牌資產以建立一致的表單：**

- **品牌範本** — 使用您組織的色彩、字型和版面配置圖樣，建立標準化的表單範本
- **樣式指南** — 定義一致的欄位樣式、按鈕設計和間距標準
- **元件庫** — 建置符合您品牌識別的可重複使用表單元件
- **視覺Assets** — 準備表單整合的圖志、圖示和背景元素

**範例品牌範本提示：**

```
Create a brand template for financial services forms with:
- Corporate blue (#003366) and silver (#C0C0C0) color scheme
- Open Sans font family for all text
- 16px minimum font size for accessibility
- Consistent 24px spacing between sections
- Corporate logo in header with proper sizing
- Professional button styling with hover effects
```

>[!NOTE]
>
>**自訂元件**：在實作自訂品牌元素之前，請洽詢您的開發團隊，瞭解如何使用組織特定的元件及其與Forms Experience Builder的相容性。

>[!NOTE]
>
> 此提示程式庫已更新，以反映簡化的Forms Experience Builder功能。 範例中顯示的某些進階整合和測試功能可能需要額外的設定。



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

**步驟2 — 新增必要欄位：**

```
Add fields for @firstName, @lastName, @email, @phoneNumber with appropriate validation
```

**步驟3 — 新增商業邏輯：**

```
Create a rule: if @age is under 18, show parent/guardian information section
```

**步驟4 — 使用偏好設定增強：**

```
Add a preferences panel with @newsletterSubscription, @marketingConsent, @termsAccepted
```

**步驟5 — 新增檔案上傳：**

```
Include a file upload field for @profilePicture with size limit of 5MB
```

## 表單建立與管理

**使用時機：**&#x200B;需要建立新表單或修改現有表單時。

**使用方式：**&#x200B;從頭開始建立或匯入並轉換（請參閱[快速入門手冊](forms-ai-assistant-getting-started.md#two-ways-to-create-forms)），選擇下列兩種方式之一：

**範例提示 — 建立簡易表單：**

```
Create a customer feedback form with:
- Product rating (1-5 stars)
- Comment field for detailed feedback
- Customer email (optional)
- Submit to email notification
```

**範例提示 — 建立複雜表單：**

```
Create a comprehensive employee onboarding form with:

**Personal Information Section:**
- Full name (first, middle, last)
- Date of birth with age validation
- Contact information (email, phone, address)
- Emergency contact details

**Employment Details:**
- Position and department selection
- Start date with business day validation
- Salary information with confidentiality notice
- Reporting structure

**Document Upload:**
- Resume/CV upload (PDF, DOC, DOCX)
- ID verification documents
- Tax forms and banking information
- Signed employment agreement

**Preferences:**
- Benefits selection with cost calculator
- Work schedule preferences
- Training requirements
- Equipment needs

**Validation Rules:**
- Email format validation
- Phone number format validation
- Age must be 18 or older
- All required documents must be uploaded
- Terms and conditions must be accepted

**Submit Actions:**
- Send confirmation email to new employee
- Notify HR department
- Create employee record in HR system
- Schedule orientation meeting
```

**表單管理提示：**

```
Import this PDF application form and convert it to an adaptive form with enhanced validation
```

```
Update the existing contact form to include social media handles and preferred contact method
```

```
Reorganize the registration form into a 3-step wizard: personal info, preferences, confirmation
```

## 欄位管理與設定

**何時使用：**&#x200B;您需要新增、修改或設定表單欄位時。

**使用方式：**&#x200B;請具體說明欄位型別、驗證規則和使用者體驗需求。

**範例提示 — 基本欄位新增：**

```
Add a text input field for "Company Name" with placeholder "Enter your company name"
```

**範例提示 — 進階欄位設定：**

```
Add a comprehensive address section with:

**Street Address:**
- Address line 1 (required, max 100 characters)
- Address line 2 (optional, max 100 characters)
- City (required, dropdown with common cities)
- State/Province (required, dropdown)
- Postal code (required, format validation)
- Country (required, default to "United States")

**Validation Rules:**
- Postal code must match state selection
- Address line 1 cannot be empty
- City must be a valid city for selected state

**User Experience:**
- Auto-complete for address fields
- Clear labels and help text
- Mobile-friendly input fields
- Accessibility compliance
```

**欄位設定提示：**

```
Make @email field required with real-time validation and custom error message
```

```
Add a dropdown for @country with options for USA, Canada, UK, Germany, France, and "Other"
```

```
Configure @phoneNumber field with format (XXX) XXX-XXXX and validation
```

```
Add a file upload field for @resume with PDF and DOC restrictions, max 5MB
```

## LLM增強型智慧型欄位

**何時使用：**&#x200B;當您需要具有預先填入選項的欄位時，這些選項會利用AI知識庫。

**如何使用：**&#x200B;需要完整資料集的要求欄位 — AI可以使用其內建知識自動填入選項。

### 地理和位置欄位

**機場和交通工具：**

```
Add a dropdown for departure airports with all major international airports
Add arrival airport field with IATA codes and full names
Create a field for nearest airport to user location
Add a selection of train stations for European cities
```

**管理區域：**

```
Add a complete list of US states with abbreviations
Create a country dropdown with ISO codes and full names
Add a field for major world cities with time zones
Include a dropdown of Canadian provinces and territories
Add a field for UK counties and postal areas
```

### 商業和產業資料

**公司分類：**

```
Add a field for industry classification with NAICS codes
Create a dropdown of business entity types (LLC, Corporation, Partnership, etc.)
Add a field for company size categories (startup, SME, enterprise)
Include department selection for large organizations
Add a field for professional service types
```

**專業分類：**

```
Add a field for job titles with common industry roles
Create a dropdown of professional certifications by field
Include education levels with degree types
Add a field for years of experience ranges
Create a selection for programming languages and frameworks
```

### 標準與法規

**財務與法律：**

```
Add a field for currency codes with symbols and exchange rates
Create a dropdown of tax ID types by country
Include a field for legal document types
Add payment method options with security features
Create a selection for banking institutions by country
```

**技術標準：**

```
Add a dropdown of file format types with extensions
Include network protocol options
Add a field for database types and versions
Create a selection for API authentication methods
```

### 醫療保健與醫療

**醫療分類：**

```
Add a field for medical specialties
Create a dropdown of common medications with generic names
Include a field for insurance provider types
Add a selection for medical emergency contact relationships
Create a field for dietary restrictions and allergies
```

### 時間與行事曆智慧

**日期和時間欄位：**

```
Add a field for business hours with time zone handling
Create a dropdown of public holidays by country
Include seasonal options with date ranges
Add a field for conference room booking with availability
Create a selection for recurring meeting patterns
```

### 產品和服務類別

**電子商務分類：**

```
Add a field for product categories with subcategories
Create a dropdown of shipping methods with delivery estimates
Include a field for return policy options
Add a selection for customer priority levels
Create a field for subscription billing cycles
```

**智慧型欄位提示範例：**

```
"Add a departure airport field with all major airports worldwide including IATA codes and city names"
```

```
"Create a comprehensive industry field using standard NAICS classification with technology subcategories"
```

```
"Include a professional certification dropdown that adapts based on the selected job field"
```

```
"Add an international phone number field that formats based on the selected country"
```

```
"Create a university selection field with major institutions organized by country and ranking"
```

## 規則建立與商業邏輯

**何時使用：**&#x200B;當您需要實作條件式邏輯、驗證規則或商務程式時。

**使用方式：**&#x200B;請清楚描述商業邏輯，指定條件和動作。

**範例提示 — 簡單條件邏輯：**

```
Create a rule that shows @spouseInformation panel only when @maritalStatus equals "Married"
```

**範例提示 — 複雜商業規則：**

```
Implement comprehensive loan application validation:

**Income Validation:**
- If @annualIncome is less than 30000:
  - Show warning message: "Income may be insufficient for requested loan amount"
  - Require additional income documentation
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
Create a **visibility rule** that shows @spouseInformation panel only when @maritalStatus equals "Married" or "Domestic Partnership"
```

```
Add **progressive disclosure** where additional questions appear based on previous answers. Start with basic info, then show relevant follow-ups
```

```
Implement **smart defaults** where @country selection auto-sets related fields. Allow manual override
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

**範例提示 — 標準多頻道提交：**

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
Connect this form to **CRM system** to create new leads. Map @firstName to FirstName, @email to Email, set LeadSource to "Web Form", and Status to "New"
```

```
Set up **workflow trigger** when form is submitted. Pass all form data and trigger approval workflow with manager notification
```

```
Configure **database integration** to save form submissions as records. Create new folder for each submission with uploaded documents
```

## 匯入和轉換現有的Forms

**何時使用：**&#x200B;當您有現有的表單、檔案或設計要轉換成現代AEM表單時。

**如何使用：**&#x200B;上傳您的來源檔案並描述轉換需求（請參閱[匯入指南](forms-ai-assistant-getting-started.md#2-import-and-convert)）。

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

Preserve all original field labels and help text, but improve the user experience with modern form interactions
```

**設計匯入提示：**

```
Import this **design mockup** and convert it into an adaptive form. Maintain the exact visual design but add proper validation and mobile responsiveness
```

```
Analyze this **image of a paper form** and recreate it digitally. Improve the layout for better mobile experience while keeping all mandatory fields
```

```
Convert this **existing HTML form** to AEM adaptive form format. Preserve all functionality but add AEM-specific features like rules and themes
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
```

**行動裝置特定提示：**

```
Make this form **touch-friendly** with larger buttons and simplified navigation for mobile users
```

```
Optimize form for **tablet users** with appropriate field sizes and navigation patterns
```

```
Add **swipe gestures** for multi-step form navigation on mobile devices
```

## 無障礙與合規性

**何時使用：**&#x200B;當表單需要符合協助工具標準(WCAG)或法規遵循要求時。

**使用方式：**&#x200B;指定必要的規範遵循層級，以及需要的任何特定協助工具功能。

**範例提示 — 基本協助工具：**

```
Make @contactForm accessible with:

**Basic Accessibility:**
- Proper ARIA labels for all form fields
- Keyboard navigation support
- High contrast color scheme
- Screen reader compatibility
- Focus indicators for all interactive elements
```

**範例提示 — 進階協助工具：**

```
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
```

**特定協助工具提示：**

```
Add **screen reader support** to this form with proper ARIA labels and announcements
```

```
Implement **keyboard navigation** for all form interactions and navigation elements
```

```
Ensure **color contrast** meets WCAG AA standards for all text and interactive elements
```

## 效能最佳化

**何時使用：**&#x200B;當表單需要快速載入並在各種條件下執行良好時。

**使用方式：**&#x200B;指定效能需求和最佳化策略。

**範例提示 — 基本效能：**

```
Optimize @contactForm for performance:

**Loading Optimization:**
- Lazy load non-critical form sections
- Minimize initial bundle size
- Optimize images and assets
- Enable caching for static resources
```

**範例提示 — 進階效能：**

```
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
```

**效能特定提示：**

```
Optimize form **loading speed** by implementing progressive loading and asset optimization
```

```
Add **auto-save functionality** to prevent data loss during form completion
```

```
Implement **offline support** so users can complete forms without internet connection
```

## 測試與品質保證

**何時使用：**&#x200B;當表單需要全面測試以確保可靠性和使用者滿意度時。

**使用方式：**&#x200B;指定測試案例、驗證需求和品質度量。

**範例提示 — 基本測試：**

```
Add comprehensive testing for @contactForm:

**Functional Testing:**
- Test all form field validations
- Verify submit functionality works correctly
- Test error handling and user feedback
- Validate conditional logic and rules
```

**範例提示 — 進階測試：**

```
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
```

**針對測試的提示：**

```
Add **automated testing** for all form validations and submit functionality
```

```
Implement **user acceptance testing** scenarios for complete form workflows
```

```
Set up **performance monitoring** to track form load times and user interactions
```

## 疑難排解

Forms Experience Builder常見問題的快速解決方案：

| 問題 | 快速修正 |
|-------|-----------|
| 表單未提交 | 檢查提交動作設定和驗證規則 |
| 驗證錯誤未顯示 | 驗證欄位驗證設定和錯誤訊息位置 |
| 行動佈局問題 | 檢閱回應式設計設定和欄位大小 |
| 未出現欄位 | 檢查條件邏輯和可見性規則 |
| 匯入失敗 | 驗證檔案格式相容性和大小限制 |
| 整合錯誤 | 驗證API端點和驗證認證 |
| 效能問題 | 最佳化欄位計數並移除不必要的驗證 |
| 協助工具問題 | 檢閱欄位標籤、ARIA屬性和索引標籤順序 |

**偵錯模式提示：**

```
Enable debug mode to identify issues with form submission and field validation
```

**錯誤分析提示：**

```
Analyze form errors: check validation rules, API responses, and user input patterns
```

## 進階分析與深入分析

**使用時機：**&#x200B;您需要瞭解表單效能和使用者行為時。

**使用方式：**&#x200B;指定所需的分析需求和深入分析。

**範例提示 — 基本分析：**

```
Add analytics to @contactForm:

**Basic Metrics:**
- Form completion rates
- Field abandonment rates
- Submit success/failure rates
- User session duration
```

**範例提示 — 進階分析：**

```
Implement comprehensive analytics for @applicationForm:

**User Behavior Analytics:**
- Track field completion rates and abandonment
- Monitor user session duration and patterns
- Analyze form navigation and user flow
- Identify bottlenecks and friction points

**Performance Analytics:**
- Measure form load times and performance
- Track API response times and failures
- Monitor validation rule effectiveness
- Analyze submission success rates

**Business Intelligence:**
- Generate reports on form effectiveness
- Track conversion rates and ROI
- Monitor user satisfaction and feedback
- Identify opportunities for optimization

**Predictive Analytics:**
- Predict form completion likelihood
- Identify users likely to abandon
- Recommend form improvements
- Optimize user experience based on data
```

**Analytics專用提示：**

```
Add **conversion tracking** to measure form completion rates and user behavior
```

```
Implement **A/B testing** to compare different form designs and optimize performance
```

```
Create **analytics dashboard** to monitor form performance and user insights
```

## 安全性與資料保護

**何時使用：**&#x200B;表單處理敏感資料並需要安全性措施時。

**使用方式：**&#x200B;指定安全性需求和資料保護措施。

**範例提示 — 基本安全性：**

```
Add security measures to @contactForm:

**Basic Security:**
- HTTPS encryption for all data transmission
- Input validation and sanitization
- CSRF protection for form submissions
- Secure session management
```

**範例提示 — 進階安全性：**

```
Implement comprehensive security for @applicationForm:

**Data Protection:**
- End-to-end encryption for sensitive data
- PII data masking and anonymization
- Secure file upload with virus scanning
- Data retention and deletion policies

**Access Control:**
- Role-based access control for form data
- Multi-factor authentication for admin access
- Audit logging for all data access
- Secure API authentication and authorization

**Compliance:**
- GDPR compliance for data handling
- HIPAA compliance for health information
- PCI DSS compliance for payment data
- SOC 2 compliance for data security

**Monitoring:**
- Real-time security monitoring and alerts
- Intrusion detection and prevention
- Data breach notification systems
- Regular security audits and assessments
```

**安全性特定提示：**

```
Implement **data encryption** for sensitive form submissions and user information
```

```
Add **access control** to restrict form data access based on user roles and permissions
```

```
Set up **security monitoring** to detect and prevent unauthorized access to form data
```

## 命令參考

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
| `/configure-submit` | 設定資料處理方式 | `/configure-submit to CRM and send confirmation email` |
| `/help` | 取得協助 | `/help how to implement multi-step validation?` |

### 欄位參考

使用`@fieldName`語法來參考提示中的現有欄位：

- `@email` — 參考電子郵件欄位
- `@firstName` — 參考名字欄位
- `@maritalStatus` — 參考婚姻狀況欄位

### 元件類型

**輸入元件：**

- `text`、`email`、`number`、`tel`、`date`、`checkbox`、`radio`、`dropdown`、`file`、`textarea`

**容器元件：**

- `fieldset`，`panel`，`repeatable`，`wizard`

### 元件屬性

**通用屬性（所有元件）：**

- **型別**：元件型別
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

**選取控制項內容：**

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
- REST API提交
- 雲端儲存空間(Azure、SharePoint)
- 工作流程自動化(Power Automate、Workfront Fusion)
- 行銷平台(Marketo)
- CRM整合

### 提示語法准則

- **欄位參考**：將`@fieldName`用於現有欄位
- **命令**：針對特定動作使用`/command`
- **自然語言**：清楚且明確地描述需求

### 驗證檢查清單

如需完整的最佳實務和驗證准則，請參閱[Forms Experience Builder快速入門手冊](forms-ai-assistant-getting-started.md#best-practices)。

*此提示程式庫會根據使用者意見與新的Forms Experience Builder功能持續更新。 如需了解最新功能和範例，請查看 [AEM Forms 文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html)。*
