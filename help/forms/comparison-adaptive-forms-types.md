---
title: 最適化Forms核心元件vs Edge Delivery Services Forms vs Foundation元件
description: AEM Forms製作方法的技術比較 — 核心元件、Edge Delivery Services Forms和基礎元件。 架構、呈現、功能和使用案例。
keywords: 調適型表單比較，核心元件， foundation元件， edge delivery services forms， AEM forms比較，表單產生器比較
role: Architect, Developer, Admin
level: Intermediate
feature: Adaptive Forms, Core Components, Edge Delivery Services
exl-id: adaptive-forms-comparison
source-git-commit: 37799555babb15809409ec5cda8a1c46ceff24f2
workflow-type: tm+mt
source-wordcount: '1953'
ht-degree: 8%

---


# 最適化Forms：核心元件vs Edge Delivery Services Forms vs基礎元件

Adobe Experience Manager (AEM) Forms提供三種建置資料擷取體驗的不同方法：以核心元件為基礎的最適化Forms、Edge Delivery Services Forms以及以基礎元件為基礎的最適化Forms。 每種方法都有不同的架構、演算模型和目標使用案例。 本文提供技術比較，以協助解決方案架構師、開發人員和AEM客戶針對其需求選擇適當的方法。

## 概觀

這三種表單型別都可擷取使用者資料並與後端系統整合。 不過，這些變數在其基礎架構中有所不同，其呈現表單的位置、傳送方式以及支援哪些功能。

| 方法 | 狀態 | 主要使用案例 |
|----------|--------|------------------|
| **核心元件** | 建議新表格使用 | 現代、可擴充的表單，需要AEM撰寫與彈性的發佈選項 |
| **Edge Delivery Services Forms** | 建議用於效能關鍵網站 | 高效能表單由邊緣提供，部署迅速 |
| **Foundation 元件** | 維護模式 | 需要舊版功能支援的現有表單 |

## 根據核心元件的最適化Forms

### 定義

最適化Forms核心元件是以Adobe Experience Manager WCM核心元件為基礎所建立的一組30種開放原始碼、符合BEM的元件。 它們代表Adobe建立新最適化Forms的建議方法，可提供現代架構、改良的效能和自動Headless表單產生。

### 架構

核心元件使用標準化的模組化元件架構：

- **元件基礎**：建置在AEM WCM核心元件上
- **樣式方法**： BEM （區塊元素修飾元） CSS慣例
- **內容儲存體**：具有結構化內容節點的JCR存放庫
- **轉譯**： AEM中的伺服器端轉譯，搭配選用的使用者端Headless轉譯
- **Source**：開放原始碼（可在[GitHub](https://github.com/adobe/aem-core-forms-components)上取得）

### 演算模型

核心元件支援多種演算模型：

1. **伺服器端轉譯(SSR)**： Forms會在AEM伺服器上轉譯，並將完整的HTML傳送給瀏覽器
2. **Headless呈現**： Forms透過API公開JSON呈現，以便在React、Angular或其他架構中用於使用者端呈現
3. **混合呈現**：伺服器與使用者端呈現的組合，以獲得最佳效能

### 發佈選項

- AEM發佈執行個體
- Edge Delivery Services （設定時）
- 適用於自訂前端應用程式的Headless API

### 主要功能

| 類別 | 功能 |
|----------|-------------|
| **元件** | 30個標準化元件，包括文字方塊、數值方塊、日期選擇器、下拉式清單、核取方塊群組、選項按鈕、檔案附件、精靈、摺疊式功能表、水平/垂直索引標籤 |
| **表單模型** | JSON結構描述（v4和2020-12）、表單資料模型(FDM)、XDP/XFA範本（受限） |
| **規則引擎** | 具有條件式邏輯、驗證、服務引動和自訂函式的視覺化規則編輯器 |
| **提交動作** | REST端點、電子郵件、AEM工作流程、SharePoint、OneDrive、Azure Blob儲存、Power Automate、Workfront Fusion、表單資料模型 |
| **預填** | 表單資料模型預填服務、自訂預填服務 |
| **驗證碼** | reCAPTCHA， hCaptcha， Turnstile |
| **記錄檔案** | 使用自訂或OOTB範本產生PDF |
| **無障礙功能** | 符合WCAG標準、ARIA標籤、鍵盤導覽、熒幕助讀程式支援 |
| **本地化** | 透過AEM翻譯工作流程提供多語言支援 |
| **版本設定** | 從AEM Sites繼承的內容版本設定 |

### 先決條件

- **AEM Forms as a Cloud Service**：核心元件預設為啟用
- **AEM 6.5 Forms**：需要透過AEM原型啟用
- **使用者許可權**：使用者必須位於`forms-users`群組
- **範本**：需要最適化表單（核心元件）範本
- **主題**：畫布主題(OOTB)或自訂主題

### 限制

- **JSON結構描述限制**：不支援Null型別、聯合型別（任何）、OneOf/AnyOf/AllOf/NOT建構
- **元件間隙**： Adobe Sign區塊、手寫簽名、圖表、影像選擇無法使用（可在Foundation元件中使用）
- **自訂函式**：產生器函式、非同步/等待、不支援類別方法
- **數位簽章**：無法以原生方式使用（不像Foundation元件）

### 使用時機

**建議用於：**

- 新表單開發專案
- 需要現代、可維護架構的組織
- 需要彈性發佈的專案(AEM + Edge Delivery + Headless)
- 透過Headless API自訂前端應用程式(React、Angular)
- 排定效能與協助工具優先順序的專案
- 全通路傳送需求（網頁、行動裝置、資訊站）

**不建議用於：**

- 需要Adobe Sign整合的Forms （使用基礎元件）
- Edge Delivery Services效能關鍵的簡單表單
- 現有的基礎元件型表單（除非移轉，否則保留在Foundation中）

## Edge Delivery Services 表單

### 定義

Edge Delivery Services (EDS) Forms是一組可撰寫的服務，可透過Adobe Experience Manager Edge Delivery Services建立和傳遞表單。 它們透過邊緣型傳送、使用者端轉譯和多種編寫方法，以卓越的效能實現快速表單開發。

### 架構

EDS Forms使用分離式、邊緣優先的架構：

- **內容來源**： Microsoft SharePoint、Google Drive (Document-Based)或通用編輯器(WYSIWYG)
- **程式碼存放庫**： GitHub
- **內容傳遞**： Edge Delivery Services CDN
- **轉譯**：使用vanilla JavaScript的使用者端轉譯
- **表單區塊**：最適化Forms區塊處理表單定義並產生HTML

### 演算模型

EDS Forms僅使用使用者端轉譯：

1. 表單定義儲存為JSON （從試算表轉換或在Universal Editor中編寫）
2. 從邊緣擷取的JSON： `https://<branch>--<repo>--<owner>.aem.live/<form>.json`
3. 最適化Forms區塊JavaScript程式JSON
4. 在瀏覽器中動態產生的HTML結構
5. 套用於樣式的CSS

**HTML結構模式：**

```html
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required="{Required}">
   <label for="{FieldId}" class="field-label">Label</label>
   <input type="{Type}" id="{FieldId}" name="{Name}">
   <div class="field-description" id="{FieldId}-description">Help text</div>
</div>
```

### 編寫方法

EDS Forms支援兩種撰寫方法：

#### 通用編輯器 (WYSIWYG)

- 視覺化拖放介面
- 透過裝置模擬即時預覽
- 條件式邏輯的進階規則編輯器
- 表單資料模型(FDM)整合
- AEM工作流程整合
- 自訂元件支援
- 範本式建立

#### 文件型製作

- Microsoft Excel或Google工作表製作
- 試算表式表單定義
- 即時發佈（變更會立即反映）
- 適合簡單至中度的複雜性表單

### 提交選項

**Forms提交服務(FSS)：**

- 提交至Google工作表
- 提交至Microsoft Excel (OneDrive/SharePoint)
- 電子郵件通知

**AEM發佈提交動作：**

- REST端點
- AEM郵件服務
- 表單資料模型
- AEM 工作流程
- SharePoint/OneDrive
- Azure Blob儲存體
- Microsoft Power Automate
- Adobe Workfront Fusion
- Adobe Marketo Engage

### 主要功能

| 類別 | 功能 |
|----------|-------------|
| **元件** | 所有HTML5輸入型別、核取方塊群組、選項群組、下拉式清單、面板、可重複區段、檔案附件、摺疊式功能表、精靈、強制回應視窗 |
| **驗證** | 欄位層級驗證（必要、最小值/最大值、模式）、自訂驗證訊息 |
| **規則** | 條件式可見度、值運算式、事件導向規則 |
| **整合** | Adobe Sign、Salesforce、Microsoft Dynamics、A/B測試 |
| **安全性** | reCAPTCHA Enterprise、hCaptcha、CORS組態 |
| **分析** | Adobe Experience Platform網頁SDK、表單檢視與提交追蹤 |

### 先決條件

**檔案式製作：**

- GitHub帳戶
- Google Drive或Microsoft SharePoint帳戶
- 本機開發的Node/npm
- 已設定最適化Forms區塊的AEM專案
- 與`forms@adobe.com`共用資料夾（編輯許可權）

通用編輯器的&#x200B;**：**

- AEM Forms as a Cloud Service 執行個體
- Edge Delivery Services 專案已設定完成
- 目標目的地的必要許可權

用於AEM發佈提交的&#x200B;**：**

- 已設定AEM Cloud Service執行個體URL
- OSGi反向連結篩選設定
- Edge Delivery網站網域的CORS設定

### 限制

**檔案式製作：**

- 工作表命名限製為`helix-default`和`shared-aem`
- 最適合低複雜度表單
- 有限的規則功能
- 沒有AEM工作流程(沒有AEM發佈提交)
- 無表單資料模型整合

**通用編輯器：**

- 自訂函式不支援靜態/動態匯入
- 表單片段只能獨立編輯
- 開發中的表單內嵌功能

**一般：**

- `shared-aem`工作表不應包含PII （可公開存取）
- 跨原始提交需要CORS設定
- AEM發佈提交需要OSGi反向連結篩選器

### 使用時機

**建議用於：**

- 需要高Lighthouse分數的效能關鍵網站
- 已使用Edge Delivery Services的網站
- 快速表單開發和部署
- 簡單至中等複雜度的資料擷取
- 團隊偏好試算表式撰寫（檔案式）
- 需要快速上市時間的專案

**不建議用於：**

- Forms需要廣泛的伺服器端處理能力
- 與缺少REST API的舊版系統深入整合
- 離線表單要求
- 需要特定JavaScript架構(React、Angular)且具備完整控制權的組織

## 根據Foundation元件的最適化Forms

### 定義

基礎元件代表典型的AEM Forms編寫方法。 這些是AEM Forms中供應多年的最適化Forms原始元件。 雖然仍受支援，但Adobe建議使用基礎元件，主要是為了維護現有表單，而非建立新表單。

### 架構

基礎元件使用傳統AEM架構：

- **內容模型**：具有JCR內容結構的WCM `cq:Page`元件
- **根結構**： `guideContainer` （根） → `rootPanel` → `items` （表單欄位）
- **轉譯**：使用使用者端JavaScript的伺服器端轉譯
- **SOM運算式**：指令碼物件模型以參考表單物件

### 演算模型

Foundation元件使用伺服器端轉譯：

1. 表單內容儲存在JCR存放庫中
2. AEM伺服器流程表單結構
3. 完成HTML演算並傳送至瀏覽器
4. 使用者端JavaScript處理互動和驗證

### 主要功能

| 類別 | 功能 |
|----------|-------------|
| **元件** | 40多個元件（包含所有同等核心元件）加上：Adobe Sign區塊、圖表、手寫簽名、影像選擇、摘要步驟、檔案附件清單 |
| **表單模型** | 表單資料模型(FDM)、XDP/XFA範本、XML結構(XSD)、JSON結構 |
| **規則引擎** | 視覺化編輯器+程式碼編輯器（適用於表單超級使用者群組） |
| **數位簽章** | Adobe Sign整合，手寫簽名 |
| **提交動作** | 多個OOTB動作，類似核心元件 |

### Foundation專屬元件

下列元件僅&#x200B;**可在Foundation元件中使用**：

- Adobe Sign 區塊
- 圖表
- 檔案附件清單
- 註腳預留位置
- 影像選擇
- 手寫簽名
- 摘要步驟
- Turnstile 驗證碼

### 先決條件

- AEM Forms as a Cloud Service或AEM 6.5 Forms
- 最適化表單範本(Foundation)
- `forms-users`群組中的使用者

### 限制

- **發佈**：僅限AEM (無Edge Delivery Services或Headless API)
- **效能**：標準效能（未針對Lighthouse分數最佳化）
- **架構**：不符合BEM規範的舊版架構
- **開啟Source**：不是開放原始碼
- **未來開發**：維護模式；主要新增到核心元件的新功能

### 使用時機

**建議用於：**

- 維護現有的Foundation表單
- Forms需要Adobe Sign或手寫簽名整合
- 依賴已建立Foundation功能的工作流程
- 具有僅限AEM發佈要求的專案
- 需要Foundation專屬元件的Forms （圖表、影像選擇）

**不建議用於：**

- 新表單開發（使用核心元件）
- 需要Edge Delivery Services發佈的專案
- Headless表單API
- 效能關鍵型實作
- 專案會排定經得起未來考驗的架構優先順序

## 比較表

| 參數 | 核心元件 | Edge Delivery Services 表單 | 基礎元件 |
|-----------|-----------------|-----------------------------|-----------------------|
| **狀態** | 建議新表格使用 | 建議用於高效能網站 | 維護模式 |
| **架構** | 模組化、符合BEM規範 | Edge優先，分離式 | 傳統WCM |
| **演算** | 伺服器端+ Headless | 僅限使用者端 | 伺服器端 |
| **正在發佈** | AEM + Edge Delivery + Headless API | 僅限 Edge Delivery Services | 僅限 AEM |
| **編寫** | AEM Forms 編輯器 | 通用編輯器或試算表 | AEM Forms 編輯器 |
| **效能** | 良好（改善於Foundation） | 極佳（Lighthouse分數較高） | 標準 |
| **元件計數** | 30 | 20+ (所有HTML5輸入型別) | 40+ |
| **開啟Source** | 是(GitHub) | 是 | 否 |
| **表單資料模型** | ✅ | ✅ （僅通用編輯器） | ✅ |
| **JSON結構描述** | ✅ | 有限 | ✅ |
| **XDP/XFA支援** | 有限 | ❌ | ✅ |
| **XML結構描述** | ❌ | ❌ | ✅ |
| **規則引擎** | 進階視覺化編輯器 | 進階（通用編輯器）/有限（檔案型） | 進階視覺化+程式碼編輯器 |
| **數位簽章** | ❌ | ❌ | ✅ |
| **Adobe Sign** | ❌ | 透過整合 | ✅ （原生區塊） |
| **記錄檔案** | ✅ | ✅ | ✅ |
| **驗證碼選項** | reCAPTCHA、hCaptcha | reCAPTCHA Enterprise， hCaptcha | reCAPTCHA， hCaptcha， Turnstile |
| **AEM工作流程** | ✅ | ✅ (透過AEM發佈) | ✅ |
| **Headless API** | ✅ （自動） | ❌ | ❌ |
| **無障礙功能** | 符合WCAG標準 | 符合WCAG標準 | 基本 |
| **部署速度** | Pipeline型 | 即時（提交至即時） | Pipeline型 |
| **樣式** | BEM CSS，主題 | CSS，專案層級主題 | CSS，主題 |
| **版本設定** | ✅ （繼承自網站） | Git型 | ✅ |
| **本地化** | AEM翻譯工作流程 | 手動/AEM Sites工作流程 | AEM翻譯工作流程 |

## 決定矩陣

| 需求 | 建議做法 |
|-------------|---------------------|
| 新表單開發 | 核心元件 |
| 維護現有表單 | 基礎元件（移轉之前） |
| 效能關鍵（Lighthouse高分數） | Edge Delivery Services 表單 |
| Headless/全通道傳送 | 核心元件 |
| Adobe Sign整合 | 基礎元件 |
| 試算表式製作 | Edge Delivery Services （檔案型） |
| 透過邊緣傳遞進行Visual WYSIWYG製作 | Edge Delivery Services （通用編輯器） |
| 複雜的企業整合 | 核心元件或基礎元件 |
| 快速建立原型 | Edge Delivery Services （檔案型） |
| XFA/XDP範本支援 | 基礎元件 |
| 自訂React/Angular前端 | 核心元件(Headless API) |

## 移轉考量事項

### 從基礎元件轉換為核心元件

- **工具**： AEM現代化工具(Forms轉換公用程式)
- **工作量**：中到高取決於表單複雜度
- **考量事項**：
   - 規則需要手動重新建立
   - 基礎專屬元件（Adobe Sign區塊、手寫簽名、圖表）會在移轉期間刪除
   - 翻譯設定未延續
   - 自訂函式需要重寫

### 傳統至Edge Delivery Services

- **方法**：使用通用編輯器或檔案式撰寫重新建置表單
- **工作量**：複雜表單高，簡單表單低
- **優點**：效能大幅提升，現代開發經驗

## 檔案缺口和模稜兩可

下列區域的檔案不完整或不明確：

1. **核心元件XDP/XFA支援**：檔案指出「有限」支援，但未指定確切限制
2. **Edge Delivery Services表單內嵌**：在檔案中標籤為「即將推出」；目前狀態不清楚
3. **基礎元件未來**：沒有明確的淘汰時間表；說明為「維護模式」
4. **Headless API涵蓋範圍**：未記錄伺服器轉譯與Headless表單之間的確切功能比較
5. **效能基準**：未提供方法之間的特定Lighthouse分數比較

## 相關資源

- [建立自適應表單 (核心元件)](/help/forms/creating-adaptive-form-core-components.md)
- [建立最適化表單 (基礎元件)](/help/forms/creating-adaptive-form.md)
- [Edge Delivery Services Forms概觀](/help/edge/docs/forms/overview.md)
- [通用編輯器快速入門](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
- [檔案式撰寫教學課程](/help/edge/docs/forms/tutorial.md)
- [移轉公用程式工具](/help/forms/migration-utility-tool-for-af-core-components.md)
- GitHub上的[AEM Forms核心元件](https://github.com/adobe/aem-core-forms-components)
