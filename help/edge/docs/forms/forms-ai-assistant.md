---
title: AEM Forms的AI助理(Forms Experience Builder)
description: 使用表單片段更快地製作強大的表單
feature: Edge Delivery Services
hide: true
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: a8d64082-a23f-4919-ad66-042faad77d29
source-git-commit: ab071b9159f3d4db275313080d7c14a46096c4de
workflow-type: tm+mt
source-wordcount: '1141'
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

適用於AEM Forms的AI Assistant可改變您建立表單的方式，只需以自然語言描述您需要的內容，看著表單生動呈現。 此工具適用於Forms Management UI、Adaptive Forms Editor和Universal Editor，可瞭解您的意圖並準確建置您要尋找的內容。

## 快速入門：直接與其交談

AI助理的運作方式就像與知識淵博的同事進行交談。 您不必學習複雜的選單和設定，只需說明您想要建立的專案。

### 快速入門

觀看我們的入門影片，快速上手並執行：

>[!VIDEO](https://video.tv.adobe.com/v/3463164/)

### 存取AI助理

您可以從AEM Forms中的三個不同位置存取AI助理：

1. **Forms管理UI**
   - 導覽至： 「Adobe Experience Manager > Forms > Forms與檔案」
   - 尋找介面左側的AI助理圖示
   - 按一下圖示以開啟AI助理面板

   ![AI助理圖示*](/help/edge/docs/forms/assets/forms-manager.gif){width="50%"}

2. **最適化Forms編輯器**
   - 導覽至： 「Adobe Experience Manager > Forms > Forms與檔案」
   - 選取並開啟表單以進行編輯
   - 在編輯器介面中按一下「AI助理」圖示

   ![AI助理圖示*](/help/edge/docs/forms/assets/adaptive-forms-editor.gif){width="75%"}

3. **通用編輯器**

   - 導覽至： 「Adobe Experience Manager > Forms > Forms與檔案」
   - 尋找介面左側的AI助理圖示
   - 在編輯器介面中按一下「AI助理」圖示

### 如何開始：簡單交談

從AI Assistant開始的最佳方式是透過自然語言。 方法如下：

**請描述您需要的內容：**

- 「為我的網站建立連絡人表單」
- 「我需要具有評等量表的客戶意見回饋表單」
- 「建立我即將舉辦活動的報名表」
- 「進行簡單的產品滿意度調查」

**隨時新增詳細資料：**

- 「建立連絡人表單，包含姓名、電子郵件、電話和訊息欄位」
- 「我需要會議的多步驟登錄檔」
- 「建立包含5星級評級和評論區域的客戶意見回饋表單」

**參考您現有的欄位：**

- 「將電子郵件欄位設為必填」(@email)
- 「將驗證新增至電話號碼欄位」(@phoneNumber)
- 「僅在已婚時顯示配偶資訊」(適用於@spouseInfo和@maritalStatus)

### 您也可以進行的工作

除了自然語言之外，AI Assistant還提供其他互動方式：

- **上傳檔案**：附加影像、PDF或Figma設計，以使用您預期的AI顯示
- **使用快速命令**：輸入`/`以檢視常用動作的可用捷徑
- **參考特定欄位**：使用`@fieldName`修改現有的表單欄位（例如，`@firstName`、`@emailAddress`）

## 您可以建立的專案：可行的範例

以下是您使用簡單自然語言所能達到的真正範例：

### 開始新表單

**簡單方法：**

```
"Create a contact form"
```

**更詳細的方法：**

```
"Create a professional contact form for a law firm with fields for name, email, phone, case type, and message. Make it mobile-friendly."
```

**含設計參考：**

```
"Create a contact form based on the attached design mockup. Include all the fields shown in the layout."
```

### 新增表單元素

**基本新增：**

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

**複雜的商業規則：**

```
"Show the spouse information fields only when marital status is set to 'Married'"
"Calculate the total cost by multiplying quantity and price, then add 10% tax"
"Enable the submit button only when all required fields are completed and terms are accepted"
```

### 表單版面配置與設計

**配置變更：**

```
"Make this a multi-step form"
"Organize fields in two columns"
"Convert to an accordion layout"
```

**設計改進：**

```
"Create a wizard-style form with 3 steps: personal info, preferences, and review"
"Arrange the address fields in a compact two-column layout"
"Update the layout to match the attached wireframe"
```

### 提交與整合

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

上傳檔案以協助AI瞭解您到底在尋找什麼：

### 支援的檔案類型

| 檔案類型 | 最適合 | 使用範例 |
|-----------|----------|-------------|
| **影像** (PNG、JPG、GIF) | 表單版面配置、UI模型、紙張表單掃描 | 「建立符合此配置的表單」 |
| **PDF檔案** | 要轉換的現有表單，規格 | &quot;將此PDF表單轉換為數位&quot; |
| **Figma檔案** | 設計原型，品牌方針 | 「從我的Figma設計建立此表單」 |
| **設計檔案** | 視覺參考，樣式參考線 | 「符合此設計中的樣式」 |

### 如何使用附件

1. **在AI助理介面中按一下附件圖示**
2. 從您的裝置&#x200B;**選取您的檔案**
3. **描述您想要的內容**&#x200B;參考附加的檔案：
   - 「根據此附加的PDF建立表單」
   - 「建立符合此影像配置的連絡人表單」
   - 「將此紙本表單轉換為數位版本」

### 使用附件的最佳實務

- **使用清晰、高品質的影像**，以進行更佳的AI分析
- **每個附件著重一個概念** （配置、樣式等）
- **描述您想要的內容**&#x200B;以及附件
- **將檔案保持在10MB以下**&#x200B;以進行最佳處理

## 取得最佳結果的秘訣

### 開始簡單，建立

- 從基本請求開始：「建立聯絡人表單」
- 逐步新增詳細資料：「新增驗證至電子郵件欄位」
- 測試並調整：「將電話欄位設為選用」

### 需要時提供具體資訊

- 而非：「做得很好看」
- 試用：「使用專業色彩和簡潔的印刷樣式」

### 使用自然語言

- 而非：「新增文字輸入元件」
- 嘗試：「新增名字欄位」

### 參考現有元素

- 將`@fieldName`用於現有欄位：「使@email為必要欄位」
- 指定欄位名稱：「更新@phoneNumber欄位」

### 劃分複雜請求

- 請嘗試多個較小的請求，而不是一個大型請求
- 逐步建置您的表單
- 在移至下一個變更之前先測試每個變更

## 產品說明與學習

AI助理也可以教導您AEM Forms功能：

### 提出下列問題：

- 「如何建立多步驟表單？」
- 「面板和區段之間有何差異？」
- 「如何設定電子郵件通知？」
- 「適合行動裝置的表單有哪些最佳實務？」
- 「如何將主題套用至我的表單？」

### 取得以下相關協助：

- AEM Forms概念和術語
- 複雜功能的逐步指示
- 最佳實務和建議
- 疑難排解常見問題

## 進階功能參考

若使用者想探索進階功能：

### 快速命令

輸入`/`檢視可用的捷徑：

| 指令 | 用途 | 範例 |
|---------|---------|---------|
| `/create-form` | 開始新表單 | `/create-form customer survey` |
| `/add-form` | 在通用編輯器中新增表單 | `/add-form contact form` |
| `/update-layout` | 變更表單結構 | `/update-layout wizard with 3 steps` |
| `/update-field` | 修改欄位屬性 | `/update-field @email to be required` |
| `/create-rule` | 新增動態行為 | `/create-rule show @spouse if married` |
| `/create-panel` | 新增欄位容器 | `/create-panel Personal Information` |
| `/configure-submit` | 設定表單提交 | `/configure-submit to email support` |
| `/help` | 取得協助 | `/help multi-step forms` |

### 欄位參考語法

使用`@fieldName`參考現有欄位：

- `@firstName` — 名字欄位
- `@email` — 電子郵件欄位
- `@phoneNumber` — 電話號碼欄位
- `@dateOfBirth` — 出生日期欄位

### 元件型別

請使用下列辭彙以獲得最佳結果：

- `text input` — 單行文字欄位
- `text area` — 多行文字欄位
- `dropdown` — 選取清單
- `checkbox` — 單一核取方塊
- `checkbox group` — 多個核取方塊
- `radio group` — 選項按鈕群組
- `date picker` — 日期選擇
- `file upload` — 檔案附件
- `panel` — 分組欄位的容器

## 疑難排解

### 常見問題與解決方法

**AI助理沒有回應：**

- 檢查您的網際網路連線
- 確定您是在支援的環境中
- 關閉並重新開啟AI助理面板

**未預期的結果：**

- 請更明確地嘗試改寫您的請求
- 將複雜的請求分成較小的步驟
- 使用標準AEM Forms術語

**欄位參考無法運作：**

- 檢查欄位名稱的拼寫與顯示完全相同
- 使用現有欄位的`@fieldName`語法
- 在參照欄位之前，請先確認欄位是否存在

**設計匯入問題：**

- 確認檔案清晰且結構合理
- 使用支援的格式(PDF、PNG、JPG、Figma)
- 確認檔案大小低於10MB

## 意見與支援

協助我們改進AI助理：

- **提供意見反應**：使用AI助理介面中的意見反應按鈕
- **報告問題**：透過正式通道聯絡Adobe支援
- **共用體驗**：您的輸入有助於讓助理更適合所有人

## 相關資源

[AEM Forms AI助理 — 提示程式庫](/help/edge/docs/forms/ai-assistant-prompt-library.md)
