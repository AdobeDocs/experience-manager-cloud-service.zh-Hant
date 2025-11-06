---
title: 表單體驗建立工具快速入門
description: 瞭解使用Forms Experience Builder建立第一個AI支援表單的基礎知識。 包含範例和最佳實務的逐步教學課程。
hide: true
index: false
hidefromtoc: true
role: Admin, Developer
exl-id: c4f838bc-a001-48e7-afaa-c2ff9034f5d4
source-git-commit: 1d378e6c8ac714779e77314d3457a14d40cd222f
workflow-type: tm+mt
source-wordcount: '1048'
ht-degree: 5%

---

# 表單體驗建立工具快速入門 {#getting-started-forms-experience-builder}

Forms Experience Builder藉由運用AI將自然語言描述轉換為完整功能的數位表單，徹底變革了表單建立。 本指南將協助您建立第一個表單，並瞭解使Forms Experience Builder具備強大功能的核心概念。

## 什麼是Forms Experience Builder？ {#what-is-forms-experience-builder}

Forms Experience Builder是AI支援的表單建立工具，可讓您使用對話式語言建立複雜的數位表單。 您只需說明所要的內容，而不用傳統的拖放介面或複雜的編碼，AI會為您建立表單。

**主要功能：**

* **自然語言表單建立** — 以純英文描述您的表單需求

* **智慧型匯入和轉換** — 將現有檔案轉換為互動式表單

* **智慧型欄位產生** — 具有預先填入選項的AI支援欄位

* **商業邏輯自動化** — 透過交談建立條件式規則和驗證

* **系統整合** — 將表單連線至您現有的業務工作流程

## 先決條件 {#prerequisites-getting-started}

開始之前，請確定您已：

* **存取Forms Experience Builder** — 可透過搶先使用程式取得
* **AEM Forms as a Cloud Service** — 使用最適化Forms核心元件的生產製作環境
* **基本瞭解** — 熟悉表單概念與業務需求

如需詳細的技術設定需求和環境設定，請參閱[部署和設定Forms Experience Builder](deploy-forms-experience-builder.md)。

## 建立表單的方式 {#two-ways-to-create-forms}

使用Forms精靈選取[核心元件範本](/help/forms/creating-adaptive-form-core-components.md)或[Edge Delivery Services](/help/edge/docs/forms/universal-editor/create-forms.md)範本、主題和其他選項後，Forms Experience Builder提供兩種建立表單的主要方法：

### 1.從頭開始建立 {#create-from-scratch}

使用您需求的自然語言說明來建立表單。

**使用時機：**

* 根據需求建立新表單

* 建立新業務流程的表單

* 當您有明確的規格，但沒有現有檔案時

**範例：**

    建立客戶意見回饋表單，包含：
     — 產品評等（1-5顆星）
     — 詳細意見回饋的評論欄位
     — 客戶電子郵件（選擇性）

>[!VIDEO](https://video.tv.adobe.com/v/3473104)



### 2.匯入及轉換 {#import-and-convert}

將現有檔案轉換為互動式數位表格。

使用此選項之前，請先上傳您的PDF檔案或表單影像。 PDF可以是AcroForm或XFA型PDF表單。 對於[其他型別的PDF forms](https://experienceleague.adobe.com/en/docs/experience-manager-learn/forms/document-services/pdf-forms-and-documents)，請使用Adobe Acrobat中的[準備表單](https://helpx.adobe.com/in/acrobat/using/creating-distributing-pdf-forms.html)選項，將它們轉換為AcroForm

**使用時機：**

* 轉換現有的PDF forms

* 將紙本流程現代化

* 當您有要增強的現有表單設計時

**範例：**

    /create-form將附加的PDF檔案轉換為最適化表單

>[!VIDEO](https://video.tv.adobe.com/v/3474042)


## 您的第一個表單：逐步教學課程 {#first-form-tutorial}

讓我們建立簡單的連絡人表單以瞭解基本的工作流程。

### 步驟1：從簡單的說明開始 {#step-1-simple-description}

從基本表單說明開始：

    建立包含姓名、電子郵件和訊息欄位的聯絡表單

這會建立包含三個基本欄位的表單。

![具有三個基本欄位的表單 — 使用自然語言提示建立](/help/forms/assets/forms-experience-builder-contact-us-form.png)

### 步驟2：新增驗證和需求 {#step-2-add-validation}

使用驗證規則增強表單：

    將 @name 和 @email 設定為必填欄位並搭配適當的驗證

`@`符號參考特定欄位以進行目標修改。

![使用自然語言提示新增表單Experience Builder中的驗證](/help/forms/assets/forms-experience-builder-contact-us-form-add-validation.png)


### 步驟3：改善使用者體驗 {#step-3-improve-ux}

新增有用的預留位置文字和指引：

    加入預留位置文字：@name「您的全名」、@email「your.email@company.com」、@message「讓我們知道可以如何提供協助」

![已使用Forms Experience Builder中的自然語言提示新增驗證](/help/forms/assets/forms-experience-builder-contact-us-form-add-placeholder.png)

### 步驟4：新增進階功能 {#step-4-advanced-features}

包含其他功能：

    新增兩個下拉式清單
    
     — 含選項的inquiryType：「一般問題」、「支援要求」、「銷售查詢」、「合作關係」
    
     — 含選項的緊急等級(低、Medium、高)


![已在Forms Experience Builder中使用自然語言提示新增下拉式清單元件](/help/forms/assets/forms-experience-builder-contact-us-form-add-dropdown.png)


### 步驟5：實作條件式邏輯 {#step-5-conditional-logic}

新增下列規則來建立智慧型內容感知行為：

    隱藏表單載入上的@urgencyLevel下拉式清單
    只有當@inquiryType等於「支援要求」時才顯示@urgencyLevel下拉式清單(低、Medium、高)

以下是兩個獨立的規則：一個會在表單載入時隱藏緊急程度下拉式清單，另一個則僅在查詢型別為「支援要求」時顯示。 您需要使用單獨的提示來建立每個規則 — 一次只能建立一個規則。

## 瞭解AI交談方法 {#ai-conversation-approach}

Forms Experience Builder使用對話式介面，您可以：

### 具有@符號的參考欄位 {#reference-fields}

使用`@fieldName`參考特定欄位：

    設@email必要欄位
    為US格式新增驗證至@phoneNumber
    將@submitButton文字變更為「傳送訊息」

>[!VIDEO](https://video.tv.adobe.com/v/3474043)


### 使用自然語言命令 {#natural-language-commands}

以純英文描述您想要的內容：

     — 新增公司資訊的區段
     — 建立部門選擇的下拉式清單
     — 包含檔案上傳以繼續

### 逐步建置 {#build-incrementally}

從簡單開始，逐步增加複雜性：

1. **基本結構** — 先建立基本欄位
2. **新增驗證** — 實作必要欄位和格式驗證
3. **增強UX** — 新增預留位置、說明文字和樣式
4. **實作邏輯** — 新增條件式規則和商業邏輯
5. **設定提交** — 設定表單處理和通知


## 常見表單模式 {#common-form-patterns}

### 聯絡與意見回饋表單 {#contact-feedback-forms}

**基本連絡人表單：**

    建立連絡人表單，包含：
     — 名稱（必要）
     — 電子郵件（必要、已驗證）
     — 主旨下拉式清單（一般、支援、銷售、合作關係）
     — 訊息（必要、多行）

**客戶意見反應表：**

    建立客戶意見回饋表單，包含：
     — 產品評等（1-5顆星）
     — 詳細意見回饋的評論欄位
     — 客戶電子郵件（選擇性）

### 註冊和入門表單 {#registration-onboarding-forms}

**使用者註冊：**

    建立使用者登錄檔單，包含：
     — 個人資訊（名稱、電子郵件、電話）
     — 帳戶偏好設定（電子報、通知）
     — 接受條款與條件
     — 密碼建立與強度驗證

**員工上線：**

    建立員工入職表單，包含：
     — 個人詳細資料和聯絡資訊
     — 僱用資訊和開始日期
     — 檔案上傳（簡歷、識別碼、稅務表單）
     — 福利選擇和偏好設定

### 調查和評估表單 {#survey-assessment-forms}

**客戶滿意度調查：**

    建立客戶滿意度調查，包含：
     — 整體評等（1-10等級）
     — 類別評等（產品、服務、支援）
     — 開放式意見回饋區段
     — 人口統計資訊（選擇性）

**技能評定：**

    建立技能評估表單，包含：
     — 具有熟練程度等級的技能類別
     — 每個技能的經驗持續時間
     — 認證和訓練資訊
     — 自我評估和目標

## 測試和驗證 {#testing-validation}

### 一律測試您的表單 {#always-test-forms}

部署任何表單之前：

1. **測試所有欄位** — 確保驗證正常運作

2. **驗證條件式邏輯** — 檢查規則是否正確觸發

3. **測試提交** — 確認資料已正確處理

4. **在不同裝置上進行驗證** — 確保行動裝置相容性

5. **與利害關係人一起檢閱** — 取得使用者的意見回饋

### 常見驗證模式 {#validation-patterns}

**電子郵件驗證：**

    新增電子郵件格式驗證至@email欄位

**電話號碼驗證：**

    將美國電話號碼格式驗證新增至@phoneNumber

**年齡驗證：**

    新增年齡驗證：@dateOfBirth
必須是18歲或以上
**檔案上傳驗證：**

    新增檔案型別驗證：僅PDF、DOC、DOCX允許@resume
    新增檔案大小限制：@resume
最多5MB
<!-- 

## Next steps {#next-steps}

Now that you understand the basics, explore these advanced topics:

* **[LLM-enhanced smart fields](forms-experience-builder-llm-smart-fields.md)** - Create fields with pre-populated options using AI knowledge
* **[AI-powered form creation](forms-experience-builder-prompt-examples-library.md)** - Advanced prompt patterns and examples
* **[Intelligent import and conversion](intelligent-import-conversion.md)** - Transform existing documents into forms
* **[Form submission and integration](form-submission-integration.md)** - Connect forms to your business systems

-->


## 相關的文章

* [Forms Experience Builder概述](product-overview.md)

<!-- 
* [LLM-enhanced smart fields](forms-experience-builder-llm-smart-fields.md)
* [AI-powered form creation](forms-experience-builder-prompt-examples-library.md)
* [Intelligent import and conversion](intelligent-import-conversion.md)
* [Form submission and integration](form-submission-integration.md)
* [Frequently asked questions](forms-experience-builder-frequently-asked-questions.md)

-->
