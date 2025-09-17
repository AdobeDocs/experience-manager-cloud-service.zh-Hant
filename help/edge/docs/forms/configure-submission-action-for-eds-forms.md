---
title: 透過 Edge Delivery Services 設定 AEM Forms 的提交動作
description: 了解如何使用 Edge Delivery Services 設定 AEM Forms 中的提交動作。選擇表單提交服務或 AEM Publish 提交動作，安全有效率地處理表單資料。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 8f490054-f7b6-40e6-baa3-3de59d0ad290
source-git-commit: 2d16a9bd1f498dd0f824e867fd3b5676fb311bb3
workflow-type: ht
source-wordcount: '810'
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

- AEM Forms as a Cloud Service 執行個體
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

將表單資料直接提交到您的 AEM as a Cloud Service 發佈執行個體進行複雜的處理。

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

#### &#x200B;1. 在 Edge Delivery 中更新 AEM 執行個體 URL

在 `form` 區塊 `constant.js` 檔案中的 `submitBaseUrl` 下方更新 AEM Cloud Service 執行個體 URL。您可以根據您的環境設定 URL：

**若為 Cloud Service 執行個體**

```js
export const submitBaseUrl = '<aem-publish-instance-URL>';
```

**若為本機開發**

```js
export const submitBaseUrl = 'http://localhost:<port-number>';
```

#### &#x200B;2. OSGi 反向連結篩選器

設定反向連結篩選器，允許您的特定 Edge Delivery 網站網域：

1. 建立或更新 OSGi 設定檔案：`org.apache.sling.security.impl.ReferrerFilter.cfg.json`

2. 以您的特定網站網域新增下列設定：

   ```json
   {
     "allow.empty": false,
     "allow.hosts": [
       "main--abc--adobe.aem.live",
       "main--abc1--adobe.aem.live"
     ],
     "allow.hosts.regexp": [
       "https://.*\\.aem\\.live:443",
       "https://.*\\.aem\\.page:443",
       "https://.*\\.hlx\\.page:443",
       "https://.*\\.hlx\\.live:443"
     ],
     "filter.methods": [
       "POST",
       "PUT",
       "DELETE",
       "COPY",
       "MOVE"
     ],
     "exclude.agents.regexp": [
       ""
     ]
   }
   ```

3. 透過 Cloud Manager 部署設定

如需詳細的 OSGi 反向連結篩選器設定相關資訊，請參閱[反向連結篩選器](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/headless/deployment/referrer-filter)指南。

#### &#x200B;3. CORS (跨來源資源共用) 問題

在 AEM 中設定 CORS 設定，允許來自您特定 Edge Delivery 網站網域的請求：

**開發人員 Localhost**

```apache
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(http://localhost(:\d+)?$)#" CORSTrusted=true
```

**Edge Delivery Sites - 個別新增各網站網域**

```apache
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://main--abc--adobe\.aem\.live$)#" CORSTrusted=true
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://main--abc1--adobe\.aem\.live$)#" CORSTrusted=true
```

**舊版 Franklin 網域 (若仍在使用)**

```apache
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.page$)#" CORSTrusted=true  
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.live$)#" CORSTrusted=true
```

>[!NOTE]
>
>將 `main--abc--adobe.aem.live` 和 `main--abc1--adobe.aem.live` 替換為您的實際網站網域。於同一存放庫託管的每個網站皆需要單獨的 CORS 設定項目。

如需詳細的 CORS 設定相關資訊，請參閱 [CORS 設定指南](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors)。


若要為您的本機開發環境啟用 CORS，請參閱[了解跨來源資源共用 (CORS)](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing) 文章。

<!--
#### 4. CDN Redirect Rules

Configure your Edge Delivery CDN to route submissions:

- Route requests from `/adobe/forms/af/submit/...` to your AEM Publish instance
- Implementation varies by CDN provider (Fastly, Akamai, Cloudflare)-->

#### &#x200B;4. 表單設定

1. 在通用編輯器中建立表單
2. 將提交動作設定為指向 AEM Forms 動作
3. 指定提交端點路徑
4. 發佈表單到 Edge Delivery 網站

+++
<!--
+++ Form Embedding

Embed forms created in one location into different web pages or sites.

### Use Cases

- Reuse standard forms across multiple landing pages
- Include specialized forms in Document-Authored content
- Maintain single form across multiple EDS projects

### CORS Configuration

Configure Cross-Origin Resource Sharing on the form source:

1. **Add CORS Headers** to form source responses:
   - `Access-Control-Allow-Origin: https://your-host-domain.com`
   - `Access-Control-Allow-Methods: GET, OPTIONS`  
   - `Access-Control-Allow-Headers: Content-Type`

2. **Example Configuration**:

        # Configuration for site hosting the form
        headers:
          - path: /forms/**
            custom:
              Access-Control-Allow-Origin: https://host-domain.com
              Access-Control-Allow-Methods: GET, OPTIONS

### Embedding Steps

1. **Create and Publish Form**
   - Build form using Document Authoring or Universal Editor
   - Configure submission method (FSS or AEM Publish)
   - Publish to standalone URL

2. **Configure CORS**
   - Set up CORS headers on form source site
   - Allow host page domain to fetch form

3. **Embed in Host Page**
   - Add form embedding block to host page
   - Point block to published form URL
   - Publish host page

![Embedded Form Architecture](/help/forms/assets/eds-embedded-form.png)

+++-->

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
