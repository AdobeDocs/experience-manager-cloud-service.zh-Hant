---
title: AEM Forms 適用的 AI 助理 (表單體驗建立工具)
description: 使用表單片段更快地製作強大的表單
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: 750674bbd29ec1b29388579d77c7c15bd89335ab
workflow-type: tm+mt
source-wordcount: '1145'
ht-degree: 97%

---


# 開始使用AEM Forms的AI Assistant (Forms Experience Builder)

>[!NOTE]
>
>
> **早期採用者計劃**&#x200B;提供 AEM Forms 適用的 AI Assistant (Forms Experience Builder) 功能。如果您有興趣，請從您的工作地址快速傳送電子郵件至mailto:aem-forms-ea@adobe.com，以要求存取此功能。

>[!IMPORTANT]
>
> **文件內容可能隨時變更**：此文件目前正在針對產品進行測試，可能會進行更新和修訂。隨著 AEM Forms 適用的 AI 助理在早期採用者計劃期間不斷發展，相關的功能、命令和範例可能有所變更。

AEM Forms 適用的 AI 助理改變建立表單的方式；只需用自然語言描述您需要的內容，然後觀看表單從無到有。在表單管理 UI、自適應表單編輯器和通用編輯器中皆可使用，此功能了解您的意圖並建立您想要的表單內容。

## 快速入門：直接說出來

AI 助理的運作方式就像與一位知識淵博的同事進行對話。您無需學習複雜的選單和設定，可直接描述您想要建立的內容。

### 快速啟動

觀看我們的介紹影片即可快速啟動並開始運作：

>[!VIDEO](https://video.tv.adobe.com/v/3463164/)

### 存取 AI 助理

您可以從 AEM Forms 中三個不同位置存取 AI 助理：

1. **表單管理 UI**
   - 導覽至：「Adobe Experience Manager > 表單 > 表單與文件」。
   - 在介面左側找到 AI 助理圖示
   - 點選圖示開啟 AI 助理面板

   ![AI 助理圖示*](/help/edge/docs/forms/assets/forms-manager.gif){width="50%"}

2. **自適應表單編輯器**
   - 導覽至：「Adobe Experience Manager > 表單 > 表單與文件」。
   - 選擇並開啟表單進行編輯
   - 點選編輯器介面中的 AI 助理圖示

   ![AI 助理圖示*](/help/edge/docs/forms/assets/adaptive-forms-editor.gif){width="75%"}

3. **通用編輯器**

   - 導覽至：「Adobe Experience Manager > 表單 > 表單與文件」。
   - 在介面左側找到 AI 助理圖示
   - 點選編輯器介面中的 AI 助理圖示

### 如何開始：簡單的對話

開始使用 AI 助理最好的方式是使用自然語言。方法如下：

**直接描述您的需求：**

- 「為我的網站建立聯絡表單」
- 「我需要一份包含評分量表的客戶意見回饋表單」
- 「為即將舉行的活動建立一份註冊表單」
- 「製作一份產品滿意度的簡易問卷調查」

**在過程中逐步增加詳細資料：**

- 「建立包含姓名、電子郵件、電話和訊息欄位的聯絡表單」
- 「我需要一份會議用的多步驟註冊表單」
- 「建立一份包含五星級評價和評論區段的客戶意見回饋表單」

**參考您現有的欄位：**

- 「將電子郵件欄位設為必填」(適用於 @email)
- 「對電話號碼欄位新增驗證功能」(適用於 @phoneNumber)
- 「唯有選擇已婚時才顯示配偶資訊」(適用於 @spouseInfo 和 @maritalStatus)

### 其他功能

除了自然語言之外，AI 助理亦提供其他互動方式：

- **上傳檔案**：附加圖像、PDF 或 Figma 設計，向 AI 說明您設想的內容
- **使用快速命令**：輸入 `/` 來查看常用動作的快速鍵
- **參考特定欄位**：使用 `@fieldName` 修改現有的表單欄位 (例如 `@firstName`、`@emailAddress`)

## 您可以建立什麼表單：適用範例

以下是使用簡單的自然語言便可以完成任務的真實範例：

### 開始建立新表單

**簡單方法：**

```
"Create a contact form"
```

**更詳細的方法：**

```
"Create a professional contact form for a law firm with fields for name, email, phone, case type, and message. Make it mobile-friendly."
```

**提供設計參考：**

```
"Create a contact form based on the attached design mockup. Include all the fields shown in the layout."
```

### 新增表單元素

**基本新增內容：**

```
"Add a section for personal information"
"Include a file upload for resume"
"Add a dropdown for country selection"
```

**詳細規格：**

```
"Add a personal information panel with fields for full name, date of birth, phone number, and email address"
"Include a secure file upload component for documents, limited to PDF files under 5MB"
"Add a country dropdown with options for USA, Canada, UK, and Germany"
```

### 建立動態行為

**簡單邏輯：**

```
"Show additional fields when 'Other' is selected"
"Make the email field required"
"Calculate the total automatically"
```

**複雜的業務規則：**

```
"Show the spouse information fields only when marital status is set to 'Married'"
"Calculate the total cost by multiplying quantity and price, then add 10% tax"
"Enable the submit button only when all required fields are completed and terms are accepted"
```

### 表單版面和設計

**版面變更：**

```
"Make this a multi-step form"
"Organize fields in two columns"
"Convert to an accordion layout"
```

**設計改良：**

```
"Create a wizard-style form with 3 steps: personal info, preferences, and review"
"Arrange the address fields in a compact two-column layout"
"Update the layout to match the attached wireframe"
```

### 提交和整合

**基本提交：**

```
"Send form data to our email"
"Save responses to a spreadsheet"
"Redirect to a thank you page"
```

**進階整合：**

```
"Send form submissions to hr@company.com and create a case in our CRM system"
"Submit data to our REST API endpoint and trigger the new customer workflow"
"Email responses to the sales team and add the lead to our marketing automation platform"
```

## 使用附件

上傳檔案以協助 AI 準確了解您想要的內容：

### 支援的檔案類型

| 檔案類型 | 最適合 | 使用範例 |
|-----------|----------|-------------|
| **影像** (PNG、JPG、GIF) | 表單版面、UI 模型、紙本表單掃描 | 「建立符合此版面的表單」 |
| **PDF 檔案** | 要轉換的現有表單、規格 | 「將此 PDF 表單轉換為數位格式」 |
| **Figma 檔案** | 設計雛型、品牌準則 | 「根據我的 Figma 設計建立此表單」 |
| **設計檔案** | 視覺參考、樣式指南 | 「符合此設計的樣式」 |

### 如何使用附件

1. 在 AI 助理介面中&#x200B;**點選附件圖示**
2. 從您的裝置&#x200B;**選取您的檔案**
3. 參考附加的檔案，**描述您想要的內容**：
   - 「根據此附加 PDF 建立表單」
   - 「根據此影像中的版面建立聯絡表單」
   - 「將此紙本表單轉換為數位版本」

### 使用附件的最佳實務

- **使用清晰、高品質的影像**&#x200B;提高 AI 分析品質
- **每個附件專門處理一個概念** (版本、樣式等)
- 搭配附件&#x200B;**描述您想要的內容**
- **保持檔案大小不超過 10 MB**&#x200B;以利處理最佳化

## 獲得最佳結果的提示

### 簡單開始，逐步累積

- 從基本請求開始：「建立聯絡表單」
- 逐步增加詳細資料：「對電子郵件欄位新增驗證功能」
- 測試並改進：「將電話欄位設為選用」

### 必要時請具體說明

- 請不要說：「做一份不錯的表單」
- 請改說：「使用專業的色彩和清晰的印刷樣式」

### 使用自然語言

- 請不要說：「新增文字輸入元件」
- 請改說：「新增名字的欄位」

### 參考現有元素

- 現有欄位請使用 `@fieldName`：「將 @email 設為必填」
- 具體描述欄位名稱：「更新 @phoneNumber 欄位」

### 分解複雜請求

- 不要提出一個大請求，改為嘗試多個小請求
- 逐步建立表單
- 先測試每一項變更，再進入下一步

## 產品說明與學習

AI 助理還可以為您解說 AEM Forms 的功能：

### 請提出類似以下問題：

- 「如何建立多步驟表單？」
- 「面板與區段之間有何差異？」
- 「如何設定電子郵件通知？」
- 「建立方便行動裝置使用的表單有哪些最佳實務？」
- 「如何將主題套用到我的表單？」

### 取得以下方面的協助：

- AEM Forms 概念和術語
- 複雜功能的逐步操作指示
- 最佳實務與建議做法
- 常見問題疑難排解

## 進階功能參考

對於想要探索進階功能的使用者：

### 快速命令

輸入 `/` 可查看可用快速鍵：

| 命令 | 用途 | 範例 |
|---------|---------|---------|
| `/create-form` | 開始建立新表單 | `/create-form customer survey` |
| `/add-form` | 在通用編輯器中新增表單 | `/add-form contact form` |
| `/update-layout` | 變更表單結構 | `/update-layout wizard with 3 steps` |
| `/update-field` | 修改欄位屬性 | `/update-field @email to be required` |
| `/create-rule` | 新增動態行為 | `/create-rule show @spouse if married` |
| `/create-panel` | 新增欄位容器 | `/create-panel Personal Information` |
| `/configure-submit` | 設定表單提交 | `/configure-submit to email support` |
| `/help` | 取得協助 | `/help multi-step forms` |

### 欄位參考語法

使用 `@fieldName` 來參考現有欄位：

- `@firstName` - 名字欄位
- `@email` - 電子郵件欄位
- `@phoneNumber` - 電話號碼欄位
- `@dateOfBirth` - 出生日期欄位

### 元件類型

使用這些詞語以獲得最佳結果：

- `text input` - 單行文字欄位
- `text area` - 多行文字欄位
- `dropdown` - 選取清單
- `checkbox` - 單一核取方塊
- `checkbox group` - 多個核取方塊
- `radio group` - 單選按鈕群組
- `date picker` - 選取日期
- `file upload` - 檔案附件
- `panel` - 用於欄位分組的容器

## 疑難排解

### 常見問題和解決方案

**AI 助理沒有回應：**

- 檢查網際網路連線
- 確認您所在的環境受支援
- 關閉並重新開啟 AI 助理面板

**結果不符預期：**

- 嘗試重新措辭，更加具體說明您的請求
- 將複雜的請求分解成小步驟
- 使用標準 AEM Forms 術語

**欄位參考無法運作：**

- 檢查欄位名稱的拼法是否與顯示完全一致
- 現有欄位使用 `@fieldName` 語法
- 確認欄位存在再參考

**設計匯入問題：**

- 檢查檔案是否清楚且結構良好
- 使用支援的格式 (PDF、PNG、JPG、Figma)
- 確認檔案大小不超過 10 MB

## 意見回饋和支援

協助我們改善 AI 助理：

- **提供意見回饋**：使用 AI 助理介面的意見回饋按鈕
- **報告問題**：透過官方管道聯絡 Adobe 支援人員
- **分享經驗**：您的意見有助於改善助理的功能，讓每個人都受益。

## 相關資源

[AEM Forms AI 助理 - 提示程式庫](/help/edge/docs/forms/ai-assistant-prompt-library.md)
