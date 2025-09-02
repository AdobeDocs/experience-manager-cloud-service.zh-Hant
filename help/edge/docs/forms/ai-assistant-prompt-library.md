---
title: Forms Experience Builder — 提示資料庫
description: 各種經驗證的提示模式和範例之集合，在表單管理 UI、自適應表單編輯器和通用編輯器中使用 AI 輔助功能建立表單時可以使用。
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: c8f64082-a23f-4919-ad66-042faad77d31
source-git-commit: fe34b44d02c308e7d18a08dd05f21abc67bd0cb2
workflow-type: tm+mt
source-wordcount: '2193'
ht-degree: 13%

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

- **品牌範本** — 使用您組織的色彩、字型和版面配置圖樣，準備標準化的表單範本
- **樣式指南** — 定義Forms Experience Builder可套用的一致欄位樣式、按鈕設計和間距標準
- **元件庫** — 與您的開發團隊合作，準備符合您品牌識別的可重複使用表單元件
- **視覺Assets** — 準備表單整合的圖志、圖示和背景元素

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

    建立包含姓名、電子郵件和訊息欄位的基本連絡人表單

**第 2 步 - 新增驗證：**

    使@name及@email必要欄位具有適當的驗證

**第 3 步 - 增強使用者體驗：**

    新增預留位置文字： @name 「您的全名」、「your.email@company.com」@email，@message「告訴我們如何協助」

**步驟 4 - 新增進階功能：**

    新增包含下列選項的下拉式清單inquiryType：「一般問題」、「支援要求」、「銷售查詢」、「合作關係」

**步驟 5 - 實作條件邏輯：**

    /建@urgencyLevel規則僅在@inquiryType等於「支援請求」
時顯示下拉式清單(低、Medium、高)

### 範例 2：逐步建立註冊表單

**第 1 步 - 基本結構：**

    使用個人資訊面板建立使用者登錄檔單

**步驟2 — 新增必要欄位：**

    新增具有適當驗證的@firstName、@lastName、@email、@phoneNumber的欄位

**步驟3 — 新增商業邏輯：**

    建立規則：如果@age低於18，則顯示家長/監護人資訊區段

**步驟4 — 使用偏好設定增強：**

    新增包含@newsletterSubscription、@marketingConsent、@termsAccepted
的偏好設定面板
**步驟5 — 新增檔案上傳：**

    包含大小限製為5MB的檔案@profilePicture傳欄位

## 表單建立與管理

**使用時機：**&#x200B;需要建立新表單或修改現有表單時。

**使用方式：**&#x200B;從頭開始建立或匯入並轉換（請參閱[快速入門手冊](forms-ai-assistant-getting-started.md#two-ways-to-create-forms)），選擇下列兩種方式之一：

**範例提示 — 建立簡易表單：**

    建立客戶意見表單，包含：
     — 產品評等（1-5顆星）
     — 詳細意見的評論欄位
     — 客戶電子郵件（選擇性）
     — 提交至電子郵件通知

**範例提示 — 建立複雜表單：**

    建立完整的員工入職表單，包含：
    
    **個人資訊區段：**
     — 全名（名字、中間名、姓氏）
     — 具有年齡驗證的出生日期
     — 聯絡資訊（電子郵件、電話、地址）
     — 緊急聯絡詳細資料
    
    **僱用詳細資料：**
     — 職位和部門選擇
     — 具有營業日驗證的開始日期
     — 具有機密性通知的薪資資訊
     — 報告結構
    
    **檔案上傳：**
     — 恢復/簡歷上傳(PDF、DOC、DOCX) ID驗證檔案
    - ID驗證檔案
     — 納稅表單和銀行資訊
     — 已簽署的僱傭協定
    
    **首選項：**
     — 使用成本計算器的福利選擇
     — 工作計畫首選項
     — 培訓要求
     — 裝置需求
    
    **驗證規則：**
     — 電子郵件格式驗證
     — 電話號碼格式驗證
     — 年齡必須為18歲或以上
     — 必須上載所有必需的檔案
     — 條款和條件被接受
    
    **提交操作：**
     — 向新員工傳送確認電子郵件
     — 通知HR部門
     — 在HR系統中建立員工記錄
     — 安排指導會議

**表單管理提示：**

    匯入此PDF應用程式表單，並將其轉換為具有增強式驗證的最適化表單
    
    更新現有的連絡人表單以包含社群媒體控制代碼和慣用的連絡方式
    
    將登錄檔單重新組織成三步驟精靈：個人資訊、偏好設定、確認

## 欄位管理與設定

**何時使用：**&#x200B;您需要新增、修改或設定表單欄位時。

**使用方式：**&#x200B;請具體說明欄位型別、驗證規則和使用者體驗需求。

**範例提示 — 基本欄位新增：**

    為「公司名稱」新增文字輸入欄位，預留位置為「輸入您的公司名稱」

**範例提示 — 進階欄位設定：**

    新增完整的位址區段，包含：
    
    **街道地址：**
     — 地址行1 （必要，最多100個字元）
     — 地址行2 （選用，最多100個字元）
     — 城市（必要，包含常用城市的下拉式清單）
     — 州/省（必要，下拉式清單）
     — 郵遞區號（必要，格式驗證）
     — 國家（必要，預設為「美國」）
    
    **驗證規則：**
     — 郵遞區號必須符合州選擇
     — 地址行1 empty
     — 城市必須是選定州
    
    **使用者體驗：**
     — 自動完成地址欄位
     — 清除標籤和幫助文本
     — 移動友好的輸入欄位
     — 輔助功能合規性

**欄位設定提示：**

    讓@email欄位成為具有即時驗證和自訂錯誤訊息的必要欄位
    
    為具有USA、Canada、UK、Germany、France和「其他」選項的@country位新增下拉式清單
    
    使用格式(XXX) XXX-XXXX和驗證設定@phoneNumber欄位
    
    為具有PDF和DOC限制的@resume位新增檔案上傳欄位，最多5MB

## LLM增強型智慧型欄位

**何時使用：**&#x200B;當您需要具有預先填入選項的欄位時，這些選項會利用AI知識庫。

**如何使用：**&#x200B;需要完整資料集的要求欄位 — AI可以使用其內建知識自動填入選項。

### 地理和位置欄位

**機場和交通工具：**

    新增適用於所有主要國際機場的出發機場的下拉式清單
    新增包含IATA代碼和全名的抵達機場欄位
    建立離使用者地點最近的機場欄位
    新增歐洲城市的火車站選項

**管理區域：**

    新增包含縮寫的美國州完整清單
    建立包含ISO代碼和全名的國家/地區下拉式清單
    新增包含時區之主要世界城市的欄位
    包含加拿大省和地區的下拉式清單
    新增英國縣和郵遞區欄位

### 商業和產業資料

**公司分類：**

    新增具有NAICS代碼的產業分類欄位
    建立商業實體型別（LLC、Corporation、Partnership等）的下拉式清單
    新增公司規模類別（啟動、SME、企業）的欄位
    包含大型組織的部門選擇
    新增專業服務型別的欄位

**專業分類：**

    為具有一般產業角色的工作標題新增欄位
    依欄位建立專業認證的下拉式清單
    包含學位型別的教育等級
    為多年的經驗範圍新增欄位
    為程式語言和架構建立選擇

### 標準與法規

**財務與法律：**

    新增包含符號與匯率的貨幣代碼欄位
    依國家/地區建立稅捐識別碼型別的下拉式清單
    加入合法檔案型別的欄位
    新增具有安全性功能的付款方式選項
    依國家/地區建立銀行機構的選擇

**技術標準：**

    新增副檔名為的檔案格式型別下拉式清單
    包含網路通訊協定選項
    新增資料庫型別和版本的欄位
    建立API驗證方法的選取專案

### 醫療保健與醫療

**醫療分類：**

    新增醫療專科的欄位
    建立一般名稱的一般藥物下拉式清單
    納入保險提供者型別的欄位
    新增醫療緊急聯絡人關係的選項
    建立飲食限制和過敏的欄位

### 時間與行事曆智慧

**日期和時間欄位：**

    新增具有時區處理功能的營業時間欄位
    依國家建立公共假日的下拉式清單
    包含日期範圍的季節性選項
    新增可供會議室預約的欄位
    建立週期性會議模式的選取專案

### 產品和服務類別

**電子商務分類：**

    新增具有子類別的產品類別欄位
    建立具有預估交貨的送貨方法下拉式清單
    加入退貨政策選項的欄位
    新增客戶優先順序層級的選項
    建立訂閱計費週期的欄位

**智慧型欄位提示範例：**

    「新增出發機場欄位，其中包含全球所有主要機場，包括IATA代碼和城市名稱」
    
    「使用技術子類別的標準NAICS分類建立完整的產業欄位」
    
    「包含根據所選工作欄位改寫的專業認證下拉式清單」
    
    「新增根據所選國家/地區格式的國際電話號碼欄位」
    
    「建立包含按國家/地區及排名組織的主要機構的大學選擇欄位」

## 規則建立與商業邏輯

**何時使用：**&#x200B;當您需要實作條件式邏輯、驗證規則或商務程式時。

**使用方式：**&#x200B;請清楚描述商業邏輯，指定條件和動作。

**範例提示 — 簡單條件邏輯：**

    建立一個規則，只在@maritalStatus等於「已婚」時顯示@spouseInformation面板

**範例提示 — 複雜商業規則：**

    實作完整的貸款應用程式驗證：
    
    **收入驗證：**
     — 如果@annualIncome小於30000：
     — 顯示警告訊息：「收入可能不足以支付請求的貸款金額」
     — 需要其他收入檔案
     — 顯示訊息：「可能需要其他檔案」
     — 如果@annualIncome大於100000：
     — 顯示付費服務選項
     — 啟用優先順序處理核取方塊
    
    **基於年齡的驗證：**
     — 如果@age低於18：
     — 顯示父母/監護人資訊區段
     — 製作強制簽名上傳
     — 將提交按鈕文本更改為「提交以供稽核」
     — 如果@age的年齡為65歲或以上：
     — 顯示高級折扣選項
     — 新增輔助功能首選項部分

**針對規則的提示：**

    建立一個&#x200B;**可見性規則**，只在@maritalStatus等於「已婚」或「國內合作關係」時顯示@spouseInformation面板
    
    新增&#x200B;**漸進式披露**，其中會根據先前的回答顯示其他問題。 從基本資訊開始，然後顯示相關的後續資訊
    
    實作&#x200B;**智慧型預設值**，@country選取專案會自動設定相關欄位。 允許手動覆寫

## 資料整合與提交

**何時使用：**&#x200B;當您需要將表單連接到後端系統、資料庫或外部服務時。

**使用方法：**&#x200B;從基本的提交設定開始，然後逐步增加其他整合。指定整合類型、資料格式要求和錯誤處理偏好。

**提示範例 - 從基本提交開始：**

    設定@applicationForm的基本表單提交：
    
    **主要提交：**
     — 將表單資料傳送至REST端點： &#39;/api/v1/applications&#39;
     — 將資料格式化為JSON
     — 顯示成功訊息：「已成功提交應用程式」
     — 如果提交失敗，則顯示錯誤訊息：「提交失敗，請再試一次」

**然後逐步新增次要動作：**

    新增電子郵件通知至@applicationForm：傳送確認電子郵件至@email有應用程式參考編號的地址
    
    新增CRM整合至@applicationForm：建立具有@firstName、@lastName、@email的新潛在客戶記錄，並將「狀態」設為「新應用程式」

**範例提示 — 標準多頻道提交：**

    設定含有多個資料目的地的表單提交：
    
    **主要提交：**
     — 將表單資料傳送至REST端點： &#39;/api/v1/applications&#39;
     — 包含API金鑰的驗證標頭
     — 將資料格式化為含有巢狀物件的JSON，以用於位址和僱用
     — 顯示感謝訊息來處理成功回應(201)
    
    **次要動作：**
     — 將通知電子郵件傳送至@email位址的申請人
     — 將應用程式資料複製到追蹤系統
     — 觸發核准程式的工作流程
     — 在含有潛在客戶狀態的CRM中建立記錄「新應用程式」
    
    **錯誤處理：**
     — 如果主提交失敗，請將資料儲存在本地並重試
     — 顯示使用者友好的錯誤消息：「提交暫時不可用」
     — 提供將表單資料下載為備份的選項
     — 向管理員團隊傳送有關提交失敗的警報電子郵件
    
    **成功流程：**
     — 重定向到具有應用程式參考編號的確認頁面
     — 傳送包含後續步驟的確認電子郵件
     — 顯示估計的處理時間線

**針對整合的提示：**

    將此表單連線到&#x200B;**CRM系統**&#x200B;以建立新的潛在客戶。 將@firstName對應到FirstName、@email對應到Email、將LeadSource設定為&quot;Web Form&quot;，並將Status設定為&quot;New&quot;
    
    在提交表單時設定&#x200B;**工作流程觸發器**。 傳遞所有表單資料並透過管理員通知
    
    設定&#x200B;**資料庫整合**&#x200B;觸發核准工作流程，以將表單提交儲存為記錄。 針對上載檔案的每次提交建立新資料夾

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

*此提示程式庫會根據使用者意見與新的Forms Experience Builder功能持續更新。 如需了解最新功能和範例，請查看 [AEM Forms 文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=zh-Hant)。*
