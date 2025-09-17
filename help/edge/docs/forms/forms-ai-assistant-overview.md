---
title: 表單體驗建立工具
description: 表單體驗建立工具簡介
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: ce61bc434614e5d7b92de3f1290e7e15325d27b7
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 100%

---


# 表單體驗建立工具簡介

>[!IMPORTANT]
>
> **文件內容可能隨時變更**：此文件目前正在針對產品進行測試，可能會進行更新和修訂。隨著表單體驗建立工具在早期採用者方案期間持續發展，相關的功能、命令和範例可能會有所變更。

AEM Forms 體驗建立工具善用生成式 AI 的強大功能，讓數位表單體驗的建立及更新大眾化並加速。藉由自然語言互動驅動的意圖型工作流程，讓使用者能夠快速、簡單地順暢設計、修改和最佳化表單。

表單體驗建立工具建置於現代網頁技術之上，並由先進的 AI 服務提供支援，讓技術使用者和非技術使用者都能透過對話式介面建立複雜的專業級表單。這種革命性的方法，將價值實現所需的時間從幾天縮短到幾小時，透過介面簡化而消除技術障礙，並在整個表單生態系統中擴展現代化努力。

## 核心功能

表單體驗建立工具提供兩種用於建立強大數位表單的主要工作流程：

### &#x200B;1. AI 驅動的表單建立

**以自然語言產生表單**

使用簡單的英語描述，從頭開始建立完整的表單。只需描述您的需求，例如「建立包含評分量表和評論欄位的客戶回饋表單」，表單體驗建立工具就會產生適當的表單結構。您可以使用視覺編輯器的體驗建立工具新增更多欄位、驗證規則和提交邏輯。

**動態欄位管理**

透過對話式命令新增、修改或移除表單欄位。AI 會理解內容，並且可以根據您的需求智慧地建議欄位類型、驗證規則和使用者介面改善。

**版面最佳化**

透過自然語言更新表單版面和設定。請求變更，例如「將表單版面變更為精靈版面」，表單體驗建立工具便會套用適當的樣式和版面調整。

**全面的提交動作設定**

設定表單提交，與您現有的業務系統整合：

- **電子郵件整合**：設定自動化電子郵件通知和確認
- **REST API 端點**：連接至自訂應用程式和服務
- **雲端儲存空間**：與 Azure Blob Storage、SharePoint 及 OneDrive 整合
- **工作流程自動化**：連接至 Power Automate 和 Workfront Fusion
- **行銷平台**：與 Marketo 直接整合，用於商機管理
- **AEM 工作流程**：善用現有的 AEM 工作流程功能

### &#x200B;2. 智慧匯入和轉換

**支援的匯入格式**

將現有的表單和文件轉變為互動式數位體驗。表單體驗建立工具支援：

- **Acroforms**：具有現有欄位結構的互動式 PDF 表單
- **XFA PDF**：XML 型的複雜表單架構
- **平面 PDF**：靜態文件轉換為互動式表單
- **影像與螢幕擷圖**：JPG、PNG 格式 (請與團隊確認尺寸限制)
- **手繪表單**：草圖與紙本表單照片

**智慧轉換過程**

將上傳的內容進行分析，用於：

- 偵測欄位類型和關係
- 盡可能保留版面
- 透過現代回應式設計進行增強
- 新增進階驗證和條件式邏輯
- 針對可存取性和行動體驗進行最佳化

## 運作方式

表單體驗建立工具會遵循簡單的對話方式：

    ┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
    │  1. 描述    │───▶│  2. AI 建立  │───▶│  3. 調整與    │
    │  您的表單      │    │  初始表單   │    │  設定      │
    │  需求   │    │                 │    │                 │
    └─────────────────┘    └─────────────────┘    └─────────────────┘
    │                       │                       │
    │                       │                       │
    ▼                       ▼                       ▼
    ┌───────────────────────────────────────────────────────────────────────────┐
    │  「建立貸款申請表單」  →  表單相關                  │
    │  「新增電子郵件欄位」           →  欄位與基本                          │
    │  「設定將電子郵件值傳送至 @firstname@gmail.com」 →  驗證規則   │
    └───────────────────────────────────────────────────────────────────────────┘

## 範例情境

<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Transform PDF Forms to Digital Forms">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">將 PDF 表單轉換為數位表單</p>
                    <p class="is-size-6">將 Acroforms、XFA PDF 或平面 PDF 文件轉換為具有增強功能的回應式互動式數位表單。</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Modernize Legacy XFA Forms">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">將舊版 XFA 表單現代化</p>
                    <p class="is-size-6">藉由改善的使用者工作流程，將複雜的 XFA 應用程式轉變為現代、可存取的數位體驗。</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Convert Screenshots to Digital Forms">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">將螢幕擷圖轉換為數位表單</p>
                    <p class="is-size-6">將影像、螢幕擷圖或手繪表單轉變為功能齊全的數位體驗。</p>
                </div>
            </div>
        </div>
    </div>
</div>

<!-- #### Import and Enhance Web Forms

Import existing HTML forms and enhance them with advanced features while preserving existing functionality.

**Key benefits:**

- Advanced validation and business logic
- Conditional field behaviors
- Multi-channel submission options
- Enhanced user experience design -->

## 表單體驗建立工具與傳統開發的比較

| 層面 | 傳統表單建立 | 表單體驗建立工具 |
|--------|---------------------------|----------------------|
| **建立所需時間** | 2 至 3 天 | 2 至 3 小時 |
| **技術知識** | 必要 | 非必要 |
| **驗證規則** | 手動編碼 | 自然語言 |
| **無障礙功能** | 手動實施 | 內建合規性 |


## 組織益處

<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Democratized Form Creation">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">大眾化的表單建立</p>
                    <p class="is-size-6">透過自然語言對話，讓非技術使用者不需要具備程式設計知識即可建立複雜的表單。</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Reduced Time to Value (TTV)">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">縮短實現價值時間 (TTV)</p>
                    <p class="is-size-6">將表單開發時間從數日大幅縮短至數小時，加快數位計劃的上市速度。</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Interface Simplicity">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">介面簡潔</p>
                    <p class="is-size-6">透過直覺的對話式介面消除學習曲線，減少培訓時間並提高採用率。</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Scaling Modernization Efforts">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">擴大現代化努力</p>
                    <p class="is-size-6">有效地將舊版表單組合進行現代化改造，保留商業邏輯並增強整個表單生態系統的使用者體驗。</p>
                </div>
            </div>
        </div>
    </div>
</div>

## 上線

表單體驗建立工具目前是以搶先體驗 (EA) 方案一部分的方式提供。若要參與並取得存取權限，您需要以下資訊：

### 必要資訊

- **IMS 組織 ID**：您的 Adobe 組織識別碼
- **方案 ID**：您在 Adobe Experience Cloud 內的特定方案識別碼
- **專案詳細資料**：時間軸、範圍和預期使用案例
- **官方工作電子郵件**：與您組織的 Adobe 帳戶關聯

### 如何取得 IMS 組織 ID 和方案 ID

關於尋找 IMS 組織 ID 和方案 ID 的詳細步驟，請參閱：

- [Adobe Experience Cloud 組織設定指南](/help/onboarding/cloud-manager-introduction.md)
- [方案和環境管理](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

### 要求存取權

1. 使用上述指南收集您的 IMS 組織 ID 和方案 ID
2. 寄送電子郵件至 [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) 請求存取權限
3. 請求中需包含以下資訊：
   - 組織名稱和 IMS 組織 ID
   - 方案 ID
   - 專案時間軸和範圍
   - 預期使用案例和業務目標

>[!IMPORTANT]
>
> **限量開放方案**：表單體驗建立工具的存取權限需經內部利害關係人核准。Adobe 將根據方案產能以及與搶先體驗條件的相符程度審閱您的請求。不保證一定能獲得核准，且會取決於目前方案的可用性。

關於搶先體驗方案及其功能的進一步資訊，請參閱 [AEM Forms 搶先體驗文件](/help/forms/early-access-ea-features.md)。

## 快速入門

若要開始使用表單體驗建立工具，請造訪[表單體驗建立工具文件](forms-ai-assistant-getting-started.md)。您可以透過 AEM Forms 編輯器或通用編輯器存取表單體驗建立工具，取決於您偏好何種工作流程。

對於希望轉變其表單建立流程的組織，表單體驗建立工具能提供強大、直覺的解決方案，將對話式 AI 的靈活性與企業級表單管理的穩健性相結合。
