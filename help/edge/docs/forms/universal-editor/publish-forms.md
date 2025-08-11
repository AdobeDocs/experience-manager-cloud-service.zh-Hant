---
title: 使用Edge Delivery Services發佈最適化Forms
description: 瞭解如何使用Edge Delivery Services發佈、設定和存取最適化Forms以供生產使用。
feature: Edge Delivery Services
role: Admin, Architect, Developer
level: Intermediate
keywords: [發佈表單、Edge Delivery Services、表單設定、CORS、反向連結篩選器]
exl-id: ba1c608d-36e9-4ca1-b87b-0d1094d978db
source-git-commit: cfff846e594b39aa38ffbd3ef80cce1a72749245
workflow-type: tm+mt
source-wordcount: 746
ht-degree: 2%

---

# 使用Edge Delivery Services發佈最適化Forms

發佈最適化表單後，使用者可在Edge Delivery Services上存取及提交。 此程式包含三個主要階段：發佈表單、設定安全性設定及存取即時表單。

**您將會完成的內容：**

- 將表單發佈至Edge Delivery Services
- 設定表單提交的安全性設定
- 存取及驗證您發佈的表單
- 設定正確的URL路由和CORS原則

## 先決條件

- 使用Edge Delivery Services範本建立的最適化表單
- 表單已測試並準備好用於生產
- AEM Forms作者許可權
- Cloud Manager存取（用於生產設定）
- 開發人員對表單區塊代碼的存取權（用於提交設定）

## 發佈程式概觀

將表單發佈至Edge Delivery Services會遵循三個階段的方法：

- **階段1：表單發佈** — 將表單發佈至CDN並驗證發佈狀態
- **階段2：安全性設定** — 設定CORS原則與反向連結篩選器，以安全提交內容
- **階段3：存取和驗證** — 測試表單功能並驗證完整的工作流程

每個階段都建立在上一個階段之上，以確保安全且功能性的部署。

### 階段1：發佈表單

+++ 步驟1：啟動發佈

1. **存取您的表單**：在通用編輯器中開啟您的最適化表單
2. **開始發佈**：按一下工具列中的&#x200B;**發佈**&#x200B;圖示

   ![按一下「發佈」](/help/forms/assets/publish-icon-eds-form.png)。

+++


+++ 步驟2：檢閱並確認

1. **檢閱發佈資產**：系統會顯示所有正在發佈的資產，包括您的表單

   ![一鍵式發佈](/help/forms/assets/on-click-publish.png)

2. **確認發佈**：按一下&#x200B;**發佈**&#x200B;以繼續
3. **驗證成功**：尋找確認訊息

   ![發佈成功](/help/forms/assets/publish-success.png)

+++


+++ 步驟3：驗證發佈狀態

**檢查狀態**：再次按一下&#x200B;**發佈**&#x200B;圖示以檢視目前狀態

![發佈狀態](/help/forms/assets/publish-status.png)

**驗證檢查點：**

- 表單在編輯器中顯示「已發佈」狀態
- 發佈程式期間沒有錯誤訊息
- 表單會顯示在已發佈的資產清單中

+++


+++ 管理已發佈的Forms

**若要取消發佈表單：**

1. 在編輯器中開啟您的表單
2. 按一下右上角的三個點選單(⋯)
3. 選取&#x200B;**取消發佈**

![取消發佈表單](/help/forms/assets/unpublish--form.png)

+++


### 階段2：設定安全性設定

+++ 為什麼需要安全性設定

若要啟用安全表單提交，您必須設定符合以下條件的安全設定：

- 允許Edge Delivery Services將資料提交至AEM
- 防止未經授權存取您的AEM執行個體
- 為表單提交啟用CORS （跨原始資源共用）
- 篩選要求以僅允許合法的Edge Delivery網域

>[!IMPORTANT]
>
>**生產環境所需**：這些設定對於表單提交在生產環境中運作是必要的。

+++



+++ 步驟1：設定表單提交URL

**用途**：直接將表單提交至您的AEM執行個體

**檔案位置**： Edge Delivery Services專案中的`blocks/form/constant.js`

**設定範例：**

```javascript
// Production Environment
export const submitBaseUrl = 'https://publish-p120-e12.adobeaemcloud.com';

// Local Development Environment  
export const submitBaseUrl = 'http://localhost:4503';

// Staging Environment
export const submitBaseUrl = 'https://publish-staging-p120-e12.adobeaemcloud.com';
```

**驗證檢查點：**

- 已使用正確的AEM發佈URL更新`constant.js`檔案
- URL符合您的環境（生產、測試或本機）
- URL中沒有結尾斜線

+++



+++ 步驟2：設定CORS設定

**用途**：允許來自Edge Delivery Services網域的表單提交請求

**實作**：將CORS設定新增至您的AEM Dispatcher或Apache設定

```apache
# Local Development Environment
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(http://localhost(:\d+)?$)#" CORSTrusted=true

# Edge Delivery Services - Preview/Stage Environment  
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.page$)#" CORSTrusted=true

# Edge Delivery Services - Production Environment
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.live$)#" CORSTrusted=true
```

**驗證檢查點：**

- 套用至Dispatcher設定的CORS規則
- 包括所有必要的網域(localhost、hlx.page、hlx.live)
- 配置已部署到目標環境

**參考檔案：**

- [CORS設定指南](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors)
- [反向連結篩選檔案](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/headless/deployment/referrer-filter)

+++



+++ 步驟3：設定反向連結篩選器

**用途**：將寫入作業限制在授權的Edge Delivery Services網域

**實作方法**：透過AEM as a Cloud Service中的Cloud Manager進行設定

**設定檔**：新增至您專案的OSGi設定

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

**組態劃分：**

- **`allow.empty`**：拒絕沒有反向連結標題的請求
- **`allow.hosts.regexp`**：允許來自Edge Delivery Services網域的請求
- **`filter.methods`**：將篩選套用到這些HTTP方法
- **`exclude.agents.regexp`**：從篩選中排除的使用者代理

**驗證檢查點：**

- 透過Cloud Manager部署的反向連結篩選設定
- 在AEM發佈執行個體上作用中的設定
- 從Edge Delivery Services網域提交測試表單
- 已封鎖未獲授權的網域，使其無法提交表單

**參考檔案：**

- [透過Cloud Manager設定反向連結篩選器](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing)

+++


### 階段3：存取您發佈的表單



+++ Edge Delivery Services的URL結構

**標準URL格式：**

```
https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>
```

**URL元件：**

- **`<branch>`**： Git分支名稱（通常為`main`）
- **`<repo>`**：存放庫名稱
- **`<owner>`**： GitHub組織或使用者名稱
- **`<form_name>`**：您的表單名稱（小寫，連字）

**環境特定URL：**

```
# Production Environment (.aem.live)
https://main--universaleditor--wkndforms.aem.live/content/forms/af/wknd-form

# Preview Environment (.aem.page) 
https://main--universaleditor--wkndforms.aem.page/content/forms/af/wknd-form
```

+++



+++ 最終驗證步驟

**驗證表單協助工具：**

1. **正在載入測試表單**：請造訪您的表單URL，並確認其已正確載入
2. **測試表單提交**：填寫並提交表單以驗證資料處理
3. **檢查回應式設計**：測試不同裝置和熒幕大小上的表單
4. **驗證安全性**：確定CORS和反向連結篩選器正常運作

**預期結果：**

- 表單載入且無錯誤
- 所有表單欄位皆正確呈現
- 表單提交程式成功
- 資料會顯示在已設定的目的地（試算表、電子郵件等）
- 沒有與CORS或安全性原則相關的主控台錯誤

+++


## 後續步驟


- [設定表單提交動作](/help/edge/docs/forms/universal-editor/submit-action.md)
- [表單的樣式和佈景主題](/help/edge/docs/forms/universal-editor/style-theme-forms.md)
- [建立回應式表單版面配置](/help/edge/docs/forms/universal-editor/responsive-layout.md)
- [新增reCAPTCHA保護](/help/edge/docs/forms/universal-editor/recaptcha-forms.md)



