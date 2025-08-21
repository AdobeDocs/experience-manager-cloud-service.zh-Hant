---
title: Forms Experience Builder
description: 使用表單片段更快地製作強大的表單
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: 750674bbd29ec1b29388579d77c7c15bd89335ab
workflow-type: tm+mt
source-wordcount: '1180'
ht-degree: 2%

---


# Forms Experience Builder簡介

>[!IMPORTANT]
>
> **文件內容可能隨時變更**：此文件目前正在針對產品進行測試，可能會進行更新和修訂。隨著Forms Experience Builder在早期採用者計畫中不斷演化，功能、命令和範例可能會有所變更。

Forms Experience Builder為Adobe Experience Manager (AEM) Forms帶來人工智慧的強大功能。 此創新的解決方案透過自然語言互動和智慧型自動化，改變組織建立、管理和最佳化數位表單的方式。

Forms Experience Builder以現代網路技術為基礎，並以進階AI服務為後盾，可讓技術和非技術使用者透過對話式介面建立精細的專業級表單。 無論您是需要簡單登錄檔單的業務分析師，還是建立複雜的多步驟工作流程的開發人員，Forms Experience Builder都能簡化整個表單建立流程。

## 對話式介面

Forms Experience Builder提供直覺式的聊天式介面，可讓您輕鬆建立表單，就像進行交談一樣：

```
┌─────────────────────────────────────────────────────────┐
│ Forms Experience Builder                               │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  👤 User: Create a customer feedback form              │
│                                                         │
│  🤖 AI: I'll help you create a feedback form. What    │
│       type of feedback do you want to collect?         │
│                                                         │
│  👤 User: Product reviews with ratings and comments    │
│                                                         │
│  🤖 AI: Perfect! I've created a feedback form with:   │
│       * Product rating (1-5 stars)                     │
│       * Comment field                                   │
│       * Customer email (optional)                       │
│       * Submit to email notification                    │
│                                                         │
│  👤 User: Add a field for product category             │
│                                                         │
│  🤖 AI: Added a dropdown field with common categories  │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

## 核心功能

### AI支援表單建立

**自然語言表單產生**

使用簡單的英文說明，從頭開始建立完整的表單。 只需說明您的需求，例如「建立具有評等刻度和評論欄位的客戶意見表單」，Forms Experience Builder就會產生適當的表單結構、欄位型別和驗證規則。

**動態欄位管理**

透過對話式命令新增、修改或移除表單欄位。 AI可瞭解內容，並可根據您的需求聰明地建議欄位型別、驗證規則和使用者介面改進。

**配置最佳化**

透過自然語言更新表單版面配置和設定。 請求變更，例如「讓表單更適合行動使用」或「在邏輯流程中重新組織欄位」，Forms Experience Builder會套用適當的樣式和版面調整。

### 智慧型匯入和轉換

**PDF至表單轉換**

將靜態PDF檔案轉換為互動式動態表單。 上傳任何PDF檔案，Forms Experience Builder即會分析結構，以建立具有適當欄位型別和驗證的對應數位表單。

**表單轉換的URL**

將現有的網路表單或頁面轉換成AEM Forms。 只要提供URL，Forms Experience Builder就會擷取表單元素，然後重新建立為具備增強功能的原生AEM Forms。

**多重格式檔案支援**

處理表單建立的各種檔案型別，包括PDF、影像、熒幕擷取畫面及現有的表單範本。 Forms Experience Builder可以處理這些內容，並將其轉換為功能性AEM Forms。

### 進階表單邏輯與整合

**智慧型規則產生**

透過自然語言建立複雜的表單驗證和業務邏輯規則。 Forms Experience Builder可產生複雜的條件式邏輯、欄位相依性和驗證規則，這些通常需要豐富的編碼知識。

**完整的提交動作組態**

設定表單提交以與您現有的業務系統整合：

- **電子郵件整合**：設定自動化電子郵件通知和確認
- **REST API端點**：連線到自訂應用程式和服務
- **雲端儲存空間**：與Azure Blob儲存空間、SharePoint和OneDrive整合
- **工作流程自動化**：連線至Power Automate和Workfront Fusion
- **行銷平台**：與Marketo直接整合，用於銷售機會管理
- **AEM工作流程**：善用現有的AEM工作流程功能

**效能分析**

分析表單轉換效能和使用者參與模式。 Forms Experience Builder針對表單效益提供深入分析，並提出最佳化建議，以改善完成率和使用者體驗。

## 運作方式

Forms Experience Builder會遵循簡易的對話式方法：

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│  1. Describe    │───▶│  2. AI Creates  │───▶│  3. Refine &    │
│  Your Form      │    │  Initial Form   │    │  Configure      │
│  Requirements   │    │                 │    │                 │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │                       │
         │                       │                       │
         ▼                       ▼                       ▼
┌─────────────────────────────────────────────────────────────────┐
│  "Create a loan application form"  →  Form with relevant        │
│  "Add conditional logic"           →  fields and basic          │
│  "Connect to CRM system"           →  validation rules          │
└─────────────────────────────────────────────────────────────────┘
```

## 使用案例範例

### 貸款申請表

```
┌─────────────────────────────────────────────────────────┐
│ Loan Application - Multi-Step Form                    │
├─────────────────────────────────────────────────────────┤
│ Step 1: Personal Information                           │
│  🏠 Property Type: [Primary] [Investment] [Commercial] │
│  💰 Loan Amount: [$_______] (triggers different paths) │
│  📊 Income Verification: [W2] [Self-Employed] [Other]  │
│                                                         │
│ Step 2: Financial Details (conditional based on above) │
│  ↳ If Self-Employed: Show tax returns, profit/loss     │
│  ↳ If W2: Show employment history, pay stubs           │
│  ↳ Complex debt-to-income calculations                 │
│                                                         │
│ Step 3: Compliance & Review                            │
│  📋 Regulatory disclosures, digital signatures         │
│  🔍 Automated eligibility pre-screening                │
└─────────────────────────────────────────────────────────┘
```

### 保險索賠表

```
┌─────────────────────────────────────────────────────────┐
│ Insurance Claim - Adaptive Form                        │
├─────────────────────────────────────────────────────────┤
│ 🚗 Claim Type: [Auto] [Property] [Health] [Business]   │
│                                                         │
│ ↳ Auto Selected: Shows accident details, police report │
│ ↳ Property: Shows damage assessment, repair estimates  │
│ ↳ Health: Shows medical provider network, pre-auth     │
│                                                         │
│ 📎 Dynamic Document Requirements:                       │
│   * Photos/videos of damage                            │
│   * Police reports (auto only)                         │
│   * Medical records (health only)                      │
│   * Repair estimates (property only)                   │
│                                                         │
│ 🔄 Real-time claim status updates                      │
└─────────────────────────────────────────────────────────┘
```

### 移轉和轉換案例

透過AI支援的轉換，將您現有的表單轉換為強大的數位體驗。


### 📄 PDF至數位

**從靜態檔案到互動式表單**

將包含50多個欄位的PDF forms轉換為具有自動化計算和行動回應式設計的動態數位體驗。

**主要優點：**

- 自動化稅捐計算與欄位相依性
- 數位簽名和電子檔案整合
- 行動裝置回應式版面最佳化
- 處理錯誤減少95%

**最適合：**&#x200B;稅捐表單、政府應用程式、複雜商業檔案

**節省時間：**&#x200B;每個表單2-3小時→15分鐘



### 🏛️舊版XFA現代化

**為過時的表單注入新的活力**

透過即時驗證和協助工具合規性，將複雜的XFA應用程式轉換為現代的多步驟精靈。

**主要優點：**

- 簡化的多步驟精靈介面
- 使用內容說明的即時驗證
- 政府資料庫整合
- 完整WCAG 2.1協助工具合規性

**最適合：**&#x200B;政府許可、企業應用程式、合規表單

**影響：**&#x200B;完成速度加快70%，錯誤減少90%




### 📱數位熒幕擷圖

**將任何紙張表單轉換為數位體驗**

上傳任何紙張表單的影像，並觀看AI擷取欄位、最佳化版面，以及建立可整合的數位表單。

**主要優點：**

- 智慧型欄位型別偵測（99%+準確度）
- 產生最佳化的回應式版面
- 強化驗證功能，超越原始紙張
- 整合就緒架構

**最適合：**&#x200B;紙張應用程式、手寫表格、舊版檔案

**處理時間：** 2小時→5分鐘（每個表單）



### 🌐 HTML增強功能

**為您的現有網路表單額外收費**

新增進階驗證、條件式邏輯和多管道提交至基本的HTML表單，而不中斷現有功能。

**主要優點：**

- 進階驗證邏輯和規則
- 條件欄位行為和工作流程
- 多頻道提交選項
- 內建分析和效能追蹤

**最適合：**&#x200B;連絡人表單、登錄檔單、簡單網路應用程式

**轉換改善：** +40%搭配增強的使用者體驗


## Forms Experience Builder與傳統開發

| 層面 | 傳統表單建立 | Forms Experience Builder |
|--------|---------------------------|----------------------|
| **建立時間** | 2-3天 | 2-3小時 |
| **技術知識** | 必要 | 非必要 |
| **驗證規則** | 手動編碼 | 自然語言 |
| **行動裝置最佳化** | 手動CSS/JS | 自動 |
| **協助工具** | 手動實施 | 內建法規遵循 |
| **更新** | 需要變更程式碼 | 自然語言 |


## 組織的好處

### 普及化表單建立

讓非技術使用者無須程式設計知識即可建立複雜表單。 業務分析師、主題專家和內容創作者可以透過自然語言對話將他們的需求直接轉換為功能形式。

### 縮短實現價值的時間(TTV)

大幅加快表單開發，從數天縮短至數小時。 以前需要大量開發週期的專案，現在可以透過對話式人工智慧在單一工作階段中完成，讓數位計畫更快上市。

### 介面簡單化

使用直覺式的對話介面，消除學習曲線。 使用者可以使用自然語言建立複雜的表單，而不是學習技術表單建立工具，減少培訓時間並增加採用率。

### 縮放現代化工作

有效率地匯入最新的舊版表單產品組合。 將現有的PDF、XFA和HTML表單轉換為回應式數位體驗，同時保留商業邏輯並提升整個表單生態系統的使用者體驗。

## 快速入門

若要開始使用Forms Experience Builder，請瀏覽[Forms Experience Builder檔案](forms-ai-assistant-getting-started.md)。 您可以透過Forms編輯器或通用編輯器存取AEM Forms Experience Builder，具體取決於您偏好的工作流程。

對於希望轉換表單建立流程的組織，Forms Experience Builder提供強大、直覺式的解決方案，結合對話式AI的彈性與企業級表單管理的健全性。

## 入門和搶先使用

Forms Experience Builder目前屬於Early Access (EA)計畫的一部分。 若要參與並取得存取權，請遵循下列步驟：

1. 確保您使用與貴組織相關聯的官方工作電子郵件地址。
2. 傳送電子郵件至[aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)，要求存取Forms Experience Builder。
3. 在您的請求中包含您的組織名稱和任何相關的專案詳細資訊，以協助加快上線流程。

>[!NOTE]
>
> Forms Experience Builder的存取權僅限於「搶先使用」計畫中的已核准參與者。 如果您符合資格，Adobe將稽核您的請求並提供入門的更多說明。

如需搶先存取程式及其功能的詳細資訊，請參閱[AEM Forms搶先存取檔案](/help/forms/early-access-ea-features.md)。

