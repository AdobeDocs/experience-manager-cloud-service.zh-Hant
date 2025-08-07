---
title: 透過 Edge Delivery Services 設定 AEM Forms 的提交動作
description: 了解如何使用 Edge Delivery Services 設定 AEM Forms 中的提交動作。選擇表單提交服務或 AEM Publish 提交動作，安全有效率地處理表單資料。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 8f490054-f7b6-40e6-baa3-3de59d0ad290
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 12%

---

# 設定AEM Forms的提交動作

使用AEM Forms搭配Edge Delivery Services設定表單提交處理，以將資料路由至試算表、電子郵件或後端系統。

## 快速決策指南

選擇您的提交方法：

| 方法 | 最適合 | 設定複雜性 | 使用案例 |
|--------|----------|------------------|-----------|
| **Forms提交服務** | 簡易資料擷取 | 低 | 聯絡表單、調查、基本資料收集 |
| **AEM發佈提交** | 複雜的工作流程 | 高 | 企業整合、自訂處理、工作流程 |

## 先決條件

在設定提交動作前，請確保您符合以下條件：

- AEM Forms as a Cloud Service執行個體
- 已設定的Edge Delivery Services專案
- 使用檔案製作或通用編輯器建立的表單
- 目標目的地(試算表、電子郵件系統或AEM)的必要許可權

+++ 方法1：Forms提交服務

Forms提交服務是Adobe託管的端點，適用於簡單的資料擷取情況。

### 支援的目的地

- **試算表**：Google工作表、Microsoft Excel (OneDrive/SharePoint)
- **電子郵件**：將表單資料傳送至指定的電子郵件地址

### 設定步驟

1. **設定目的地存取**
   - 針對試算表：授予編輯許可權給目標試算表上的`forms@adobe.com`
   - 針對電子郵件：驗證收件者電子郵件地址是否可供存取

2. **設定表單提交**
   - 在撰寫環境中開啟您的表單
   - 將提交動作設為「Forms提交服務」
   - 指定目標試算表URL或電子郵件地址
   - 儲存並發佈表單

3. **測試提交**
   - 透過表單提交測試資料
   - 驗證資料是否出現在目標目的地中
   - 提交失敗時檢查錯誤記錄

### 重要附註

- 服務帳戶`forms@adobe.com`需要目標試算表的編輯存取權
- 在提交表單時會立即傳送電子郵件通知
- 資料驗證會在服務層級進行

![Forms提交服務流程](/help/forms/assets/eds-fss.png)

+++

+++ 方法2：AEM發佈提交

直接將表單資料提交至您的AEM as a Cloud Service Publish執行個體，以進行複雜處理。

### 何時使用AEM Publish

- 提交後需要自訂AEM工作流程
- 表單資料模型(FDM)與資料庫的整合
- 協力廠商服務整合(Marketo、Power Automate、Workfront Fusion)
- Azure Blob Storage或SharePoint檔案庫
- 複雜的伺服器端驗證或處理邏輯

### 可用的提交動作

- [提交到 REST 端點](/help/forms/configure-submit-action-restpoint.md)
- [透過AEM郵件服務傳送電子郵件](/help/forms/configure-submit-action-send-email.md)
- [使用表單資料模型提交](/help/forms/configure-data-sources.md)
- [呼叫 AEM 工作流程](/help/forms/aem-forms-workflow-step-reference.md)
- [提交到 SharePoint](/help/forms/configure-submit-action-sharepoint.md)
- [提交到 OneDrive](/help/forms/configure-submit-action-onedrive.md)
- [提交至 Azure Blob Storage](/help/forms/configure-submit-action-azure-blob-storage.md)
- [提交至 Microsoft Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)
- [提交至 Adobe Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
- [提交至 Adobe Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md)

![AEM發佈提交流程](/help/forms/assets/eds-aem-publish.png)

### 組態需求

#### &#x200B;1. AEM Dispatcher設定

在您的AEM發佈執行個體上設定Dispatcher：

- **允許提交路徑**：修改`filters.any`以允許`/adobe/forms/af/submit/...`的POST要求
- **沒有重新導向**：確定Dispatcher規則不會重新導向表單提交路徑

#### &#x200B;2. OSGi反向連結篩選器

在AEM OSGi主控台(`/system/console/configMgr`)中：

1. 尋找「Apache Sling反向連結篩選器」
2. 將您的Edge Delivery網域新增至「允許主機」清單
3. 包含`https://your-eds-domain.hlx.page`之類的網域

#### &#x200B;3. CDN重新導向規則

設定您的Edge Delivery CDN以路由提交內容：

- 將請求從`/adobe/forms/af/submit/...`路由到您的AEM發佈執行個體
- 實作因CDN提供者(Fastly、Akamai、Cloudflare)而異

#### 4.表單設定

1. 在通用編輯器中建立表單
2. 設定提交動作以目標AEM Forms動作
3. 指定提交端點路徑
4. 將表單發佈至Edge Delivery網站

+++

+++ 表單內嵌（選擇性）

將在一個位置建立的表單內嵌到不同的網頁或網站中。

### 使用案例

- 在多個登陸頁面中重複使用標準表單
- 在檔案編寫內容中包含專用表單
- 跨多個EDS專案維護單一表單

### CORS 設定

在表單來源上設定跨原始資源共用：

1. **新增CORS標頭**&#x200B;至表單來源回應：
   - `Access-Control-Allow-Origin: https://your-host-domain.com`
   - `Access-Control-Allow-Methods: GET, OPTIONS`
   - `Access-Control-Allow-Headers: Content-Type`

2. **設定範例**：

   裝載表單    之網站的
&#x200B;#設定 標頭：
        — 路徑： /forms/**
       自訂：
       Access-Control-Allow-Origin： https://host-domain.com
       Access-Control-Allow-Methods： GET， OPTIONS
   

### 內嵌步驟

1. **建立和發佈表單**
   - 使用檔案製作或通用編輯器建立表單
   - 設定提交方法(FSS或AEM Publish)
   - 發佈至獨立URL

2. **設定CORS**
   - 在表單來源網站上設定CORS標題
   - 允許主機頁面網域擷取表單

3. **內嵌於主機頁面**
   - 將表單內嵌區塊新增至主機頁面
   - 將區塊指向已發佈的表單URL
   - 發佈主機頁面

![嵌入式表單架構](/help/forms/assets/eds-embedded-form.png)

+++

+++ 常見問題

| 問題 | 解決方案 |
|-------|----------|
| **表單提交失敗** | 檢查主控台錯誤，驗證端點URL，確認許可權 |
| **未出現內嵌表單** | 在表單來源上設定CORS標題，驗證表單URL |
| AEM發生&#x200B;**403/401錯誤** | 更新Sling查閱者篩選器，檢查驗證設定 |
| **資料未到達試算表** | 驗證`forms@adobe.com`是否具有編輯存取權，檢查試算表URL |
| **個CORS錯誤** | 新增適當的`Access-Control-Allow-Origin`標頭至表單來源 |

+++

## 設定範例

+++ 以檔案為基礎的表單，含試算表提交

1. 在Google Docs/Sheets中建立表單結構
2. 設定Forms提交服務端點
3. 授予`forms@adobe.com`目標試算表的編輯存取權
4. 將檔案發佈至Edge Delivery網站
5. 測試表單提交和資料流程

+++

+++ 具有AEM工作流程的通用編輯器表單

1. 在通用編輯器中建立表單
2. 設定提交動作以「叫用AEM工作流程」
3. 在AEM發佈上設定Dispatcher和反向連結篩選器
4. 設定CDN路由規則
5. 發佈表單並測試工作流程執行

+++

## 最佳實務

- **針對簡單的資料擷取案例使用Forms提交服務**
- **當需要複雜的處理或整合時，請選擇AEM發佈**
- 在生產部署之前，在中繼環境中徹底測試&#x200B;**&#x200B;**
- **使用AEM記錄檔和主控台錯誤監視提交**
- **針對失敗的提交實作適當的錯誤處理**
- **在使用者端和伺服器層級驗證資料**
- **使用HTTPS**&#x200B;進行所有表單提交和資料傳輸

## 相關主題

- [使用EDS Forms進行檔案式撰寫](/help/edge/docs/forms/tutorial.md)
- [具有EDS Forms的Universal Editor](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
- [AEM 表單提交服務](/help/forms/forms-submission-service.md)
- [設定資料來源](/help/forms/configure-data-sources.md)
- [AEM Forms工作流程參考](/help/forms/aem-forms-workflow-step-reference.md)
