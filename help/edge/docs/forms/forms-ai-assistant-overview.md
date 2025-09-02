---
title: Forms Experience Builder
description: 使用表單片段更快地製作強大的表單
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: 6134772ea9916fc17fb7fc8a30e18799a81d4994
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 3%

---


# Forms Experience Builder簡介

>[!IMPORTANT]
>
> **文件內容可能隨時變更**：此文件目前正在針對產品進行測試，可能會進行更新和修訂。隨著Forms Experience Builder在早期採用者計畫中不斷演化，功能、命令和範例可能會有所變更。

AEM Forms Experience Builder利用Generative AI的強大功能，將數位表單體驗的建立和更新大眾化並加速。 藉由啟用透過自然語言互動驅動的意圖工作流程，讓使用者能夠快速輕鬆地順暢地設計、修改和最佳化表單。

Forms Experience Builder以現代網路技術為基礎，並以進階AI服務為後盾，可讓技術和非技術使用者透過對話式介面建立精細的專業級表單。 這種革命性的方法可將實現價值的時間從數天縮短至數小時，透過介面的簡化消除技術障礙，並可在整個形態的生態系統中調整現代化工作。



## 核心功能

Forms Experience Builder提供建立強大數位表單的兩個主要工作流程：

### &#x200B;1. AI支援表單建立

**自然語言表單產生**

使用簡單的英文說明，從頭開始建立完整的表單。 只需說明您的需求，例如「使用評等刻度和評論欄位建立客戶意見表單」，Forms Experience Builder就會產生適當的表單結構。 您可以使用視覺化編輯器的體驗產生器，新增更多欄位、驗證規則和提交邏輯。

**動態欄位管理**

透過對話式命令新增、修改或移除表單欄位。 AI可瞭解內容，並可根據您的需求聰明地建議欄位型別、驗證規則和使用者介面改進。

**配置最佳化**

透過自然語言更新表單版面配置和設定。 請求變更，例如「將表單版面變更為精靈版面配置」，以及Forms Experience Builder套用適當的樣式和版面配置。

**完整的提交動作組態**

設定表單提交以與您現有的業務系統整合：

- **電子郵件整合**：設定自動化電子郵件通知和確認
- **REST API端點**：連線到自訂應用程式和服務
- **雲端儲存空間**：與Azure Blob儲存空間、SharePoint和OneDrive整合
- **工作流程自動化**：連線至Power Automate和Workfront Fusion
- **行銷平台**：與Marketo直接整合，用於銷售機會管理
- **AEM工作流程**：善用現有的AEM工作流程功能


### 2.智慧型匯入和轉換

**支援的匯入格式**

將現有的表單和檔案轉換為互動式數位體驗。 Forms Experience Builder支援：

- **Acroforms**：具有現有欄位結構的互動式PDF forms
- **XFA PDF**：複雜的XML型表單架構
- **平面PDF**：轉換為互動式表單的靜態檔案
- **影像和熒幕擷取畫面**： JPG、PNG格式（請洽詢團隊以取得大小限制）
- **手繪的Forms**：草圖和紙張形式的像片


**智慧型轉換程式**

上傳的內容會分析至：

- 偵測欄位型別和關係
- 儘可能保留版面
- 透過現代回應式設計增強
- 新增進階驗證和條件式邏輯
- 針對協助工具與行動體驗最佳化

## 運作方式

Forms Experience Builder會遵循簡易的對話式方法：

    ┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
    │ 1. 說明    │───▶│ 2. AI建立│───▶│ 3。 精簡和    │
    │您的表單      │    │初始表單   │    │設定      │
    │需求   │    │                 │    │                 │
    └─────────────────┘    └─────────────────┘    └─────────────────┘
    │                       │                       │
    │                       │                       │
    ▼                       ▼                       ▼
    ┌───────────────────────────────────────────────────────────────────────────┐
    │ 「建立貸款申請表單」→含相關資訊的表單                  │
    │ 「新增電子郵件欄位」           →欄位和基本                          │
    │ 「將歸檔的電子郵件值設定為@firstname@gmail.com」→驗證規則   │
    └───────────────────────────────────────────────────────────────────────────┘

## 範例情境

<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Transform PDF Forms to Digital Forms">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">將PDF forms轉換為數位Forms</p>
                    <p class="is-size-6">將Acroform、XFA PDF或平面PDF檔案轉換為具增強功能的回應式互動式數位表單。</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Modernize Legacy XFA Forms">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">更新舊版XFA Forms</p>
                    <p class="is-size-6">透過改善的使用者工作流程，將複雜的XFA應用程式轉換為現代、可存取的數位體驗。</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Convert Screenshots to Digital Forms">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">將熒幕擷取畫面轉換為數位Forms</p>
                    <p class="is-size-6">將影像、熒幕擷取畫面或手繪表單轉換為功能齊全的數位體驗。</p>
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

## Forms Experience Builder與傳統開發

| 層面 | 傳統表單建立 | Forms Experience Builder |
|--------|---------------------------|----------------------|
| **建立時間** | 2-3天 | 2-3小時 |
| **技術知識** | 必要 | 非必要 |
| **驗證規則** | 手動編碼 | 自然語言 |
| **協助工具** | 手動實施 | 內建法規遵循 |


## 組織的好處

<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Democratized Form Creation">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">普及化表單建立</p>
                    <p class="is-size-6">透過自然語言交談，讓非技術使用者無需程式設計知識即可建立複雜表單。</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Reduced Time to Value (TTV)">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">縮短實現價值的時間(TTV)</p>
                    <p class="is-size-6">大幅加快表單開發，從數天縮短至數小時，讓數位計畫更快上市。</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Interface Simplicity">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">介面簡單化</p>
                    <p class="is-size-6">使用直覺式對話介面消除學習曲線，減少培訓時間並增加採用率。</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Scaling Modernization Efforts">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">縮放現代化工作</p>
                    <p class="is-size-6">有效率地匯入舊版表單產品組合、保留商業邏輯，並提升整個表單生態系統的使用者體驗。</p>
                </div>
            </div>
        </div>
    </div>
</div>

## 上線

Forms Experience Builder目前屬於Early Access (EA)計畫的一部分。 若要參與及取得存取權，您需要下列資訊：

### 必要資訊

- **IMS組織ID**：您的Adobe組織識別碼
- **方案ID**：您在Adobe Experience Cloud中的特定方案識別碼
- **專案詳細資料**：時間表、範圍和預期使用案例
- **正式工作電子郵件**：與您組織的Adobe帳戶相關聯


### 如何取得IMS組織ID和方案ID

如需尋找IMS組織ID和計畫ID的詳細步驟，請參閱：

- [Adobe Experience Cloud組織設定指南](/help/onboarding/cloud-manager-introduction.md)
- [程式和環境管理](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

### 要求存取權

1. 使用上述指南收集您的IMS組織ID和計畫ID
2. 傳送電子郵件至[aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)要求存取權
3. 在您的請求中加入：
   - 組織名稱和IMS組織ID
   - 方案ID
   - 專案時間表和範圍
   - 預期使用案例和業務目標

>[!IMPORTANT]
>
> **有限可用性方案**：存取Forms Experience Builder須待內部利害關係人的核准後，才能進行。 Adobe將根據方案容量以及與搶先存取條件的一致性，審查您的請求。 核准並不保證且取決於目前方案的可用性。

如需搶先存取程式及其功能的詳細資訊，請參閱[AEM Forms搶先存取檔案](/help/forms/early-access-ea-features.md)。


## 快速入門

若要開始使用Forms Experience Builder，請瀏覽[Forms Experience Builder檔案](forms-ai-assistant-getting-started.md)。 您可以透過Forms編輯器或通用編輯器存取AEM Forms Experience Builder，具體取決於您偏好的工作流程。

對於希望轉換表單建立流程的組織，Forms Experience Builder提供強大、直覺式的解決方案，結合對話式AI的彈性與企業級表單管理的健全性。
