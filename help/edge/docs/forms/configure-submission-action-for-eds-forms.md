---
title: 透過 Edge Delivery Services 設定 AEM Forms 的提交動作
description: 了解如何使用 Edge Delivery Services 設定 AEM Forms 中的提交動作。選擇表單提交服務或 AEM Publish 提交動作，安全有效率地處理表單資料。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 8f490054-f7b6-40e6-baa3-3de59d0ad290
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: ht
source-wordcount: '855'
ht-degree: 100%

---

# 設定 AEM Forms 的提交動作

使用搭配 Edge Delivery Services 的 AEM Forms 設定表單提交處理，將資料路由至試算表、電子郵件或後端系統。

## 快速決策指南

選擇您的提交方法：

| 方法 | 最適合 | 設定複雜度 | 使用案例 |
|--------|----------|------------------|-----------|
| **表單提交服務** | 簡單的資料擷取 | 低 | 聯絡表單、問卷調查、基本資料彙集 |
| **AEM Publish 提交功能** | 複雜工作流程 | 高 | 企業整合、自訂處理、工作流程 |

## 先決條件

在設定提交動作前，請確保您符合以下條件：

- AEM Forms as a Cloud Service 實例
- Edge Delivery Services 專案已設定完成
- 使用文件製作或通用編輯器建立的表單
- 存取目標位置 (試算表、電子郵件系統或 AEM) 的必要權限

+++ 方法 1：表單提交服務

表單提交服務是 Adobe 託管的端點，非常適合簡單的資料擷取情境。

### 支援的目標

- **試算表**：Google Sheets、Microsoft Excel (OneDrive/SharePoint)
- **電子郵件**：將表單資料傳送到指定的電子郵件地址

### 設定步驟

1. **設定目標存取權**
   - 對於試算表：授予 `forms@adobe.com` 在目標試算表上進行編輯的權限
   - 對於電子郵件：驗證收件者電子郵件是否可存取

2. **設定表單提交**
   - 在製作環境中開啟表單
   - 設定提交動作為「表單提交服務」
   - 指定目標試算表 URL 或電子郵件地址
   - 儲存並發佈表單

3. **測試提交**
   - 透過表單提交測試資料
   - 驗證出現在目標目的地的資料
   - 如果提交失敗，請檢查錯誤記錄

### 重要注意事項

- 服務帳戶 `forms@adobe.com` 需要目標試算表的編輯存取權
- 提交表單後立即發送電子郵件通知
- 資料驗證在服務層級進行

![表單提交服務流程圖](/help/forms/assets/eds-fss.png)

+++

+++ 方法 2：AEM Publish 提交功能

將表單資料直接提交到您的 AEM as a Cloud Service 發布實例進行複雜的處理。

### 何時使用 AEM Publish

- 提交後需使用自訂 AEM 工作流程
- 表單資料模型 (FDM) 與資料庫整合
- 第三方服務整合 (Marketo、Power Automate、Workfront Fusion)
- Azure Blob 儲存體或 SharePoint 文件資料庫
- 複雜的伺服器端驗證或處理邏輯

### 可用的提交動作

- [提交到 REST 端點](/help/forms/configure-submit-action-restpoint.md)
- [透過 AEM 郵件服務傳送電子郵件](/help/forms/configure-submit-action-send-email.md)
- [使用表單資料模型提交](/help/forms/configure-data-sources.md)
- [呼叫 AEM 工作流程](/help/forms/aem-forms-workflow-step-reference.md)
- [提交到 SharePoint](/help/forms/configure-submit-action-sharepoint.md)
- [提交到 OneDrive](/help/forms/configure-submit-action-onedrive.md)
- [提交至 Azure Blob Storage](/help/forms/configure-submit-action-azure-blob-storage.md)
- [提交至 Microsoft Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)
- [提交至 Adobe Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
- [提交至 Adobe Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md)

![AEM Publish 提交流程圖](/help/forms/assets/eds-aem-publish.png)

### 設定要求

#### &#x200B;1. AEM Dispatcher 設定

在 AEM 發布實例上設定 Dispatcher：

- **允許提交路徑**：修改 `filters.any` 以允許向 `/adobe/forms/af/submit/...` 發出 POST 要求
- **無重新導向**：確保 Dispatcher 規則不會將表單提交路徑重新導向

#### &#x200B;2. OSGi 反向連結篩選器

在 AEM OSGi 控制台 (`/system/console/configMgr`) 中：

1. 尋找「Apache Sling 反向連結篩選器」
2. 將您的 Edge Delivery 網域新增至「允許主機」清單
3. 加入網域，如 `https://your-eds-domain.hlx.page`

#### &#x200B;3. 內容傳遞網路重新導向規則

設定 Edge Delivery 內容傳遞網路來路由提交：

- 將來自 `/adobe/forms/af/submit/...` 的請求路由到您的 AEM 發布實例
- 內容傳遞網路提供者 (Fastly、Akamai、Cloudflare) 各有不同的實施方式

#### &#x200B;4. 表單設定

1. 在通用編輯器中建立表單
2. 將提交動作設定為指向 AEM Forms 動作
3. 指定提交端點路徑
4. 發佈表單到 Edge Delivery 網站

+++

+++ 表單嵌入 (選用)

將在某個位置建立的表單嵌入到不同的網頁或網站中。

### 使用案例

- 在多個登陸頁面重複使用標準表單
- 在文件製作型內容中加入專用表單
- 在多個 EDS 專案中維持單一表單

### CORS 設定

在表單來源上設定跨來源資源共用：

1. **新增 CORS 標頭** 至表單來源回應：
   - `Access-Control-Allow-Origin: https://your-host-domain.com`
   - `Access-Control-Allow-Methods: GET, OPTIONS`
   - `Access-Control-Allow-Headers: Content-Type`

2. **設定範例**：

       # Configuration for site hosting the form
       headers:
       - path: /forms/**
       custom:
       Access-Control-Allow-Origin: https://host-domain.com
       Access-Control-Allow-Methods: GET, OPTIONS
   
### 嵌入步驟

1. **建立與發佈表單**
   - 使用文件製作功能或通用編輯器建置表單
   - 設定提交方法 (FSS 或 AEM Publish)
   - 發佈到獨立 URL

2. **設定 CORS**
   - 在表單來源網站上設定 CORS 標頭
   - 允許主機頁面網域擷取表單

3. **嵌入到主機頁面**
   - 將表單嵌入區塊新增至主機頁面
   - 將區塊指向已發佈的表單 URL
   - 發佈主機頁面

![嵌入式表單架構](/help/forms/assets/eds-embedded-form.png)

+++

+++ 常見問題

| 問題 | 解決方案 |
|-------|----------|
| **表單提交失敗** | 查看控制台錯誤，驗證端點 URL，確認權限 |
| **嵌入的表單未顯示** | 在表單來源上設定 CORS 標頭，驗證表單 URL |
| **AEM 發生 403/401 錯誤** | 更新 Sling 反向連結篩選器，檢查驗證設定 |
| **資料未傳送到試算表** | 驗證 `forms@adobe.com` 具有編輯權限，檢查試算表 URL |
| **CORS 錯誤** | 把適當的 `Access-Control-Allow-Origin` 標頭加入表單來源 |

+++

## 設定範例

+++ 文件型表單搭配試算表提交

1. 在 Google Docs/Sheets 中建立表單結構
2. 設定表單提交服務端點
3. 將目標試算表的編輯存取權授予 `forms@adobe.com`
4. 發佈文件到 Edge Delivery 網站
5. 測試表單提交和資料流程

+++

+++ 通用編輯器表單搭配 AEM 工作流程

1. 使用通用編輯器建置表單
2. 將提交動作設定為「呼叫 AEM 工作流程」
3. 在 AEM Publish 上設定 Dispatcher 和反向連結篩選器
4. 設定內容傳遞網路路由規則
5. 發佈表單並測試工作流程執行

+++

## 最佳做法

- 簡單的資料擷取情境應&#x200B;**使用表單提交服務**
- 需要複雜的處理或整合時&#x200B;**選擇 AEM Publish**
- 在生產部署前，於中繼環境進行&#x200B;**全面測試**
- 使用 AEM 記錄和控制台錯誤&#x200B;**監視提交**
- 對失敗的提交動作&#x200B;**實施適當的錯誤處理**
- 在用戶端和伺服器層級都&#x200B;**驗證資料**
- **使用 HTTPS**&#x200B;進行所有表單提交和資料傳輸

## 相關主題

- [使用 EDS Forms 進行文件型製作](/help/edge/docs/forms/tutorial.md)
- [通用編輯器與 EDS Forms](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
- [AEM Forms 提交服務](/help/forms/forms-submission-service.md)
- [設定資料來源](/help/forms/configure-data-sources.md)
- [AEM Forms Workflow 參考](/help/forms/aem-forms-workflow-step-reference.md)
