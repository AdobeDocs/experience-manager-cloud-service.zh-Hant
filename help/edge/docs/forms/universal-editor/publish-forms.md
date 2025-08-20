---
title: 使用 Edge Delivery Services 發佈自適應表單
description: 了解如何使用 Edge Delivery Services 發佈、設定和存取自適應表單以供生產使用。
feature: Edge Delivery Services
role: Admin, Architect, Developer
level: Intermediate
keywords: 發佈表單，Edge Delivery Services，表單設定，CORS，反向連結篩選器
exl-id: ba1c608d-36e9-4ca1-b87b-0d1094d978db
source-git-commit: 05c0d8fd16cc8bd805a0e8644d3145685fe6fa12
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 89%

---

# 使用 Edge Delivery Services 發佈自適應表單

發佈自適應表單，讓最終使用者可以在 Edge Delivery Services 上存取和提交。此過程涉及三個主要階段：發佈表單、進行安全性設定和存取上線表單。

**您會學到什麼：**

- 將表單發佈到 Edge Delivery Services
- 設定表單提交的安全性設定
- 存取並確認您發佈的表單
- 設定適當的 URL 路由和 CORS 策略

## 先決條件

- 使用 Edge Delivery Services 範本建立的自適應表單
- 表單已經過測試並準備好投入生產使用
- AEM Forms 作者權限
- Cloud Manager 存取權 (用於生產設定)
- 開發人員存取表單區塊程式碼 (用於提交設定)

## 發佈程式概觀

將表單發佈至Edge Delivery Services會遵循三個階段的方法：

- **階段1：表單發佈** — 將表單發佈至CDN並驗證發佈狀態
- **階段2：安全性設定** — 設定CORS原則與反向連結篩選器，以安全提交內容
- **階段3：存取和驗證** — 測試表單功能並驗證完整的工作流程

每個階段都建立在上一個階段之上，以確保安全且功能性的部署。

### 第一階段：發佈表單

+++ 步驟 1：開始發佈

1. **存取您的表單**：在通用編輯器中開啟您的自適應表單
2. **開始發佈**：按一下工具列中的「**發佈**」圖示

   ![按一下「發佈」](/help/forms/assets/publish-icon-eds-form.png)

+++


+++ 步驟 2：審閱並確認

1. **審閱發佈資產**：系統顯示所有正要發佈的資產，包括您的表單

   ![一鍵式發佈](/help/forms/assets/on-click-publish.png)

2. **確認發佈**：按一下「**發佈**」以繼續
3. **確認成功**：尋找確認訊息

   ![發佈成功](/help/forms/assets/publish-success.png)

+++


+++ 步驟 3：檢查出版狀態

**檢查狀態**：再次按一下「**發佈**」圖示即可檢視目前狀態

![發佈狀態](/help/forms/assets/publish-status.png)

**驗證查核點：**

- 表單在編輯器中顯示「已發佈」狀態
- 發佈過程中沒有錯誤訊息
- 表單出現在已發佈資產清單中

+++


+++ 管理已發佈的表單

**若要取消發佈表單：**

1. 在編輯器中開啟您的表單
2. 按一下右上角的三點選單 (…)
3. 選取「**取消發佈**」。

![取消發佈表單](/help/forms/assets/unpublish--form.png)

+++


### 第二階段：進行安全性設定

+++ 為什麼需要安全性設定

若要安全地提交表單，您必須設定以下安全性設定：

- 允許 Edge Delivery Services 向 AEM 提交資料
- 防止未經授權存取您的 AEM 實例
- 啟用 CORS (跨來源資源共用) 以利提交表單
- 篩選請求至僅允許合法的 Edge Delivery 網域

>[!IMPORTANT]
>
>**生產環境所需**：要在生產環境中提交表單，這些是必要設定。

+++



+++ 步驟 1：設定表單提交 URL

**用途**：將表單提交直接傳送到您的 AEM 實例

**檔案位置**：`blocks/form/constant.js` 在您的 Edge Delivery Services 專案中

**設定範例：**

```javascript
// Production Environment
export const submitBaseUrl = 'https://publish-p120-e12.adobeaemcloud.com';

// Local Development Environment  
export const submitBaseUrl = 'http://localhost:4503';

// Staging Environment
export const submitBaseUrl = 'https://publish-staging-p120-e12.adobeaemcloud.com';
```

**驗證查核點：**

- 使用正確的 AEM Publish URL 更新 `constant.js` 檔案
- URL 符合您的環境 (生產、中繼或本機)
- URL 中沒有結尾斜線

+++



+++ 步驟 2：進行 CORS 設定

**用途**：允許來自 Edge Delivery Services 網域的表單提交請求

**實施**：將 CORS 設定新增至您的 AEM dispatcher 或 Apache 設定

```apache
# Local Development Environment
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(http://localhost(:\d+)?$)#" CORSTrusted=true

# Edge Delivery Services - Preview/Stage Environment  
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.page$)#" CORSTrusted=true

# Edge Delivery Services - Production Environment
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.live$)#" CORSTrusted=true
```

**驗證查核點：**

- CORS 規則已套用至 dispatcher 設定
- 包含所有必要的網域 (localhost、hlx.page、hlx.live)
- 設定部署到目標環境

**參考文件：**

- [CORS 設定指南](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors)
- [反向連結篩選器文件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/headless/deployment/referrer-filter)

+++



+++ 步驟 3：設定反向連結篩選器

**用途**：限制對授權的 Edge Delivery Services 網域進行寫入操作

**實施方法**：透過 AEM as a Cloud Service 中的 Cloud Manager 進行設定

**設定檔案**：新增至專案的 OSGi 設定

```json
{
  "allow.empty": false,
  "allow.hosts": [],
  "allow.hosts.regexp": [
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

**設定劃分：**

- **`allow.empty`**：拒絕沒有反向連結標頭的請求
- **`allow.hosts.regexp`**：允許來自 Edge Delivery Services 網域的請求
- **`filter.methods`**：對這些 HTTP 方法套用篩選
- **`exclude.agents.regexp`**：篩選範圍不包括使用者代理人

**驗證查核點：**

- 透過 Cloud Manager 部署反向連結篩選器設定
- AEM 發布實例上的設定為使用中狀態
- 從 Edge Delivery Services 網域測試表單提交工作
- 未經授權的網域被禁止提交表單

**參考文件：**

- [透過 Cloud Manager 設定反向連結篩選器](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing)

+++


### 第三階段：存取您發佈的表單



+++ Edge Delivery Services 的 URL 結構

**標準 URL 格式：**

```
https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>
```

**URL 元件：**

- **`<branch>`**：Git 分支名稱 (通常為 `main`)
- **`<repo>`**：存放庫名稱
- **`<owner>`**：GitHub 組織或使用者名稱
- **`<form_name>`**：您的表單名稱 (小寫，帶連字號)

**特定環境的 URL：**

```
# Production Environment (.aem.live)
https://main--universaleditor--wkndforms.aem.live/content/forms/af/wknd-form

# Preview Environment (.aem.page) 
https://main--universaleditor--wkndforms.aem.page/content/forms/af/wknd-form
```

+++



+++ 最終驗證步驟

**確認表單無障礙：**

1. **測試表單載入**：造訪您的表單 URL 並確認其正確載入
2. **測試表單提交**：填寫並提交表單以確認資料處理
3. **檢查回應式設計**：使用不同的裝置和螢幕尺寸測試表單
4. **驗證安全性**：確保 CORS 和反向連結篩選器正常運作

**預期結果：**

- 表單載入無錯誤
- 所有表單欄位均正確呈現
- 成功處理表單提交
- 資料出現在所設定的目標 (試算表、電子郵件等)
- 沒有與 CORS 或安全性原則相關的控制台錯誤

+++


## 後續步驟


- [設定表單提交動作](/help/edge/docs/forms/universal-editor/submit-action.md)
- [設定表單的樣式和主題](/help/edge/docs/forms/universal-editor/style-theme-forms.md)
- [建立回應式表單版面](/help/edge/docs/forms/universal-editor/responsive-layout.md)
- [新增 reCAPTCHA 保護](/help/edge/docs/forms/universal-editor/recaptcha-forms.md)



