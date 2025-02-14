---
title: 發佈適用於Edge Delivery Services的AEM Forms。
description: 快速且順暢地發佈您的Edge Delivery Services表單。
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
exl-id: ba1c608d-36e9-4ca1-b87b-0d1094d978db
source-git-commit: d48048ab130805d2be40ac3f7ee60e4269337cb5
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# 將最適化表單發佈至Edge Delivery Services

當您的表單完成並可供使用時，您可以發佈該表單，以供客戶存取以進行資料收集和提交。 發佈可確保表單可在Edge Delivery上使用，讓使用者能夠順暢地與其互動。 此程式可讓客戶即時填寫並提交表單，確保有效率的資料擷取並簡化處理。

## 先決條件

* 使用&#x200B;**Edge Delivery Services (EDS)範本**&#x200B;建立的表單。 [深入瞭解](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)如何建立EDS表單。

## 發佈您的表單

您可以依照下列步驟將任何&#x200B;**EDS式最適化表單**&#x200B;發佈到Edge Delivery：

<!--1. Select the **Adaptive Form** that you want to publish and click the **Edit** ![edit icon](/help/forms/assets/edit.svg) icon.
   ![Select EDS-Based Form](/help/forms/assets/select-eds-based-form.png)-->

1. 在編輯器中開啟最適化表單，然後按一下上方邊欄上的&#x200B;**發佈**圖示。
   ![按一下發佈](/help/forms/assets/publish-icon-eds-form.png)

1. 當您按一下&#x200B;**發佈**&#x200B;時，畫面或快顯視窗會顯示發佈資產，包括表單標題。 在此範例中，使用&#x200B;**Wknd_Form**範本。
   ![按一下發佈](/help/forms/assets/on-click-publish.png)

1. 再按一下&#x200B;**發佈**，就會出現確認快顯視窗，表示您的表單已發佈。
   ![發佈成功](/help/forms/assets/publish-success.png)

1. 若要檢查表單的發佈狀態，請再按一下&#x200B;**發佈**。
   ![發佈狀態](/help/forms/assets/publish-status.png)

1. 若要&#x200B;**取消發佈**&#x200B;表單，請在編輯器中開啟您的表單，按一下右上角的三個點功能表，然後按一下&#x200B;**取消發佈**。
   ![取消發佈](/help/forms/assets/unpublish--form.png)

## 為Edge Delivery Publisher設定反向連結篩選條件，以在AEM上啟用表單提交

為確保表單提交安全，您需要在AEM Publisher中設定&#x200B;**反向連結篩選器**。 此篩選器可確保只有Edge Delivery的授權請求才能執行寫入操作(POST、PUT、DELETE、COPY、MOVE)，以防止未經授權的修改。 以下是為AEM Publisher設定反向連結篩選器的指定步驟：

### 更新Edge Delivery中的AEM執行個體URL

修改表單區塊內&#x200B;**constant.js**&#x200B;檔案中的`submitBaseUrl`，以指定AEM執行個體URL：

雲端設定的&#x200B;**：**

```js
export const submitBaseUrl = 'https://publish-p120-e12.adobeaemcloud.com';
```
本機開發的&#x200B;**：**

```js
export const submitBaseUrl = 'http://localhost:4503';
```

### 修改CORS設定

調整&#x200B;**CORS設定**&#x200B;以允許來自Edge Delivery網域的表單提交請求。 如需詳細資訊，請參閱[CORS設定指南](https://experienceleague.adobe.com/en/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors)。

**範例CORS組態：**

```apache
# Developer Localhost
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(http://localhost(:\d+)?$)#" CORSTrusted=true

# Franklin Stage
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.page$)#" CORSTrusted=true  

# Franklin Live
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.live$)#" CORSTrusted=true
```
如需本機開發，請參閱[檔案](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/headless/deployment/referrer-filter)，以啟用您&#x200B;**開發UI主機URL**&#x200B;的CORS。

### 設定反向連結篩選

透過Cloud Manager在AEM雲端服務中設定&#x200B;**反向連結篩選器**。 [進一步瞭解](https://experienceleague.adobe.com/en/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing)如何使用Cloud Manager在AEM Cloud Service執行個體上設定反向連結篩選器。

反向連結篩選的&#x200B;**JSON設定：**

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

此設定會指定篩選哪些HTTP方法、允許哪些反向連結，以及從篩選中排除哪些使用者代理。 實作這些設定後，透過Edge Delivery **提交的**&#x200B;表單將會受到保護，且僅限授權來源使用。

### 存取您發佈的最適化表單

您的最適化表單現在可以透過&#x200B;**Edge Delivery**&#x200B;使用下列URL格式存取：

```
https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>
```

例如，**Wknd-Form**&#x200B;的URL是：

```
https://main--universaleditor--wkndforms.aem.live/content/forms/af/wknd-form
```


## 另請參閱

{{see-more-forms-eds}}
