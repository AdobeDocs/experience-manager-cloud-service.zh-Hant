---
title: 為 Edge Delivery Services 發佈 AEM Forms。
description: 快速且無縫地發佈您的 Edge Delivery Services 表單。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: ba1c608d-36e9-4ca1-b87b-0d1094d978db
source-git-commit: 9ef4c5638c2275052ce69406f54dda3ea188b0ef
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 97%

---

# 將最適化表單發佈到 Edge Delivery Services

<span class="preview">這是透過我們的<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=zh-hant#new-features">發行前通道</a>提供的發行前功能。</span>


當您的表單最終確定並可供使用時，您即可將其發佈，讓您的客戶可存取來進行資料的收集和提交。發佈可確保表單在 Edge Delivery 上可用，從而讓使用者能夠無縫地與其互動。此流程讓客戶可即時填寫並提交表單，確保高效的資料擷取並簡化處理流程。

## 先決條件

* 使用 **Edge Delivery Services 範本**&#x200B;建立的表單。[深入了解](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)如何建立 EDS 型表單。

## 發佈您的表單

您可以發佈任何 **EDS 型最適化表單**&#x200B;至 Edge Delivery，請依照下列步驟進行：

<!--1. Select the **Adaptive Form** that you want to publish and click the **Edit** ![edit icon](/help/forms/assets/edit.svg) icon.
   ![Select EDS-Based Form](/help/forms/assets/select-eds-based-form.png)-->

1. 在編輯器中開啟最適化表單，然後按一下上方邊欄的「**發佈**」圖示。
   ![按一下「發佈」](/help/forms/assets/publish-icon-eds-form.png)。

1. 按一下「**發佈**」，隨即出現螢幕或快顯視窗，顯示發佈資產，包括表單的標題。此範例使用 **Wknd_Form** 範本。
   ![一鍵式發佈](/help/forms/assets/on-click-publish.png)

1. 再次按一下「**發佈**」，隨即出現確認快顯視窗，表示您的表單現已發佈。
   ![發佈成功](/help/forms/assets/publish-success.png)

1. 若要檢查表單的發佈狀態，請再次按一下「**發佈**」。
   ![發佈狀態](/help/forms/assets/publish-status.png)

1. 若要&#x200B;**取消發佈**&#x200B;表單，請在編輯器中開啟表單，按一下右上角的三個點選單，然後按一下「**取消發佈**」。
   ![取消發佈](/help/forms/assets/unpublish--form.png)

## 透過為 AEM 發佈器設定推薦者篩選器在 Edge Delivery 啟用表單提交

若要確保安全的表單提交，您需要在 AEM 發佈器中設定&#x200B;**推薦者篩選器**。此篩選器可確保只有來自 Edge Delivery 的授權請求才能執行寫入作業 (POST、PUT、DELETE、COPY、MOVE)，從而防止未經授權的修改。下列是為 AEM 發佈器設定推薦者篩選器的步驟：

### 在 Edge Delivery 中更新 AEM 執行個體 URL

在表單區塊內的 **constant.js** 檔案中修改 `submitBaseUrl`，以指定 AEM 執行個體 URL：

**對於雲端設定：**

```js
export const submitBaseUrl = 'https://publish-p120-e12.adobeaemcloud.com';
```

**對於本機開發：**

```js
export const submitBaseUrl = 'http://localhost:4503';
```

### 修改 CORS 設定

調整 **CORS 設定**，以允許來自 Edge Delivery 網域的表單提交要求。請參閱「[CORS 設定指南](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors)」以了解詳細資料。

**CORS 設定範例：**

```apache
# Developer Localhost
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(http://localhost(:\d+)?$)#" CORSTrusted=true

# Franklin Stage
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.page$)#" CORSTrusted=true  

# Franklin Live
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.live$)#" CORSTrusted=true
```

對於本機開發，請參閱「[文件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/headless/deployment/referrer-filter)」，以從&#x200B;**開發 UI 主機 URL** 啟用 CORS。

### 設定推薦者篩選器

透過 Cloud Manager 在 AEM Cloud Service 中設定&#x200B;**推薦者篩選器**。 [深入了解](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing)關於如何使用 Cloud Manager 在 AEM Cloud Service 執行個體上設定推薦者篩選器。

**推薦者篩選器的 JSON 設定：**

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

此設定會指定篩選哪些 HTTP 方法、允許哪些推薦者以及從篩選器中排除哪些使用者代理程式。透過實作這些設定，**透過 Edge Delivery 的表單提交**&#x200B;可受到保護並僅限於授權來源。

### 存取您已發佈的最適化表單

您現在可以透過 **Edge Delivery** 使用下列 URL 格式存取最適化表單：

```
https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>
```

例如，**Wknd-Form**  的 URL 為：

```
https://main--universaleditor--wkndforms.aem.live/content/forms/af/wknd-form
```


## 另請參閱

{{universal-editor-see-also}}

