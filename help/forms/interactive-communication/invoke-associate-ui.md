---
title: 在發佈執行個體上叫用關聯UI
description: 瞭解如何在發佈執行個體上整合及叫用AEM Forms關聯UI，讓面對客戶的專業人員即時產生個人化的互動式通訊。
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
hide: true
hidefromtoc: true
source-git-commit: 2f3badafddfdfe1dd21eb74be7189102aa0474bc
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 2%

---


# 產生與關聯UI的個人化通訊

<span>互動式通訊功能可在率先採用者程式下使用。 從您的工作地址傳送電子郵件給`aem-forms-ea@adobe.com`以要求存取權。</span>

「關聯」UI可直接在「發佈」例項上叫用，讓面對客戶的專業人員（例如現場助理和服務代理）在客戶互動期間即時產生個人化通訊。

下表描述各種真實情況，其中關聯UI可用於傳送個人化訊息給客戶：

| 產業 | 使用案例 |
|----------|----------|
| **金融服務** | 在客戶會議期間產生即時貸款確認函、帳戶對帳單和風險設定檔摘要 |
| **保險** | 在服務櫃檯製作立即的保險證明卡和索賠處理摘要 |
| **醫療保健** | 使用已計算的Copay金額與排程建立患者治療計畫彙總 |
| **政府** | 現場產生警方驗證報告、公民服務收據和案件更新摘要 |

## 先決條件

將「關聯UI」與應用程式整合之前，請確定您已：

- 已建立和發佈互動式通訊
- 已啟用快顯視窗支援的瀏覽器
- 關聯[使用者必須屬於Forms-associates群組](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/administrator-help/setup-organize-users/creating-configuring-roles#assign-a-role-to-users-and-groups)
- 已設定驗證 — [SAML 2.0](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/saml-2-0)

>[!NOTE]
>
> 對於Associate UI，[SAML 2.0驗證](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/saml-2-0)文章中所述的標準設定之外，還需要其他SAML設定。 如需詳細資訊，請參閱[關聯UI的其他SAML設定](#additional-saml-configurations-for-associate-ui)區段。

### 關聯UI的其他SAML設定

為關聯UI設定SAML 2.0驗證時，您必須在OSGi設定檔案中套用以下特定設定。

#### SAML驗證處理常式

在`com.adobe.granite.auth.saml.SamlAuthenticationHandler~saml.cfg.json`中建立檔案`ui.config/src/main/content/jcr_root/apps/<project-name>/osgiconfig/config.publish`：

```json
  {
    "path": ["/libs/fd/associate"],
    "serviceProviderEntityId": "https://publish-p{program-id}-e{env-id}.adobeaemcloud.com",
    "assertionConsumerServiceURL": "https://publish-p{program-id}-e{env-id}.adobeaemcloud.com/libs/fd/associate/saml_login",
    "idpUrl": "https://login.microsoftonline.com/{azure-tenant-id}/saml2",
    "idpCertAlias": "{your-certificate-alias}",
    "idpIdentifier": "https://sts.windows.net/{azure-tenant-id}/",
    "userIDAttribute": "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name",
    "createUser": true,
    "userIntermediatePath": "saml",
    "synchronizeAttributes": [
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname=profile/givenName",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname=profile/familyName",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress=profile/email"
      ],
      "addGroupMemberships": true,
      "defaultGroups": ["forms-associates"],
      "defaultRedirectUrl": "/libs/fd/associate/ui.html",
      "idpHttpRedirect": false,
      "service.ranking": 5002
  }
```

| 屬性 | 說明 |
|----------|-------------|
| `path` | 關聯UI必須設定為`/libs/fd/associate` |
| `defaultGroups` | 設定為`forms-associates`以自動將使用者指派給所需的群組 |
| `defaultRedirectUrl` | 將已驗證的使用者重新導向至關聯UI |
| `idpHttpRedirect` | SP起始的流程必須是`false` |
| `idpCertAlias` | 必須完全符合信任存放區中的憑證別名（區分大小寫） |

#### Sling驗證器

更新`org.apache.sling.engine.impl.auth.SlingAuthenticator~saml.cfg.json`中的檔案`ui.config/src/main/content/jcr_root/apps/<project-name>/osgiconfig/config.publish`：

```json
{
  "sling.auth.requirements": ["+/libs/fd/associate/ui.html"],
  "sling.auth.anonymous": false
}
```

#### Dispatcher篩選器

如果尚未出現，請將下列規則新增至您的`dispatcher/src/conf.dispatcher.d/filters/filters.any`檔案：

```json
  # Allow Interactive Communications APIs and Associate UI
  /XXXX { /type "allow" /method '(GET|OPTIONS)' /url "/adobe/communications" }
  /XXXX { /type "allow" /method '(GET|POST|OPTIONS)' /url "/adobe/communications/*" }
  /XXXX { /type "allow" /method "GET" /url "/content/dam/fd:fonts/*" }
  /XXXX { /type "allow" /method '(GET|OPTIONS)' /url "/libs/fd/associate/*" }
```

>[!NOTE]
>
> 將`XXXX`取代為您現有`filters.any`檔案中使用的適當數字序列。

## 在發佈執行個體上叫用關聯UI

若要從您的應用程式叫用關聯UI，請設定發佈執行個體URL、準備資料裝載，並使用整合函式在新的瀏覽器視窗中啟動關聯UI。

### 步驟1：設定發佈執行個體URL

關聯UI可透過您AEM Forms Cloud Service發佈執行個體上的特定端點進行存取：

```javascript
const AEM_URL = 'https://publish-p{program-id}-e{env-id}.adobeaemcloud.com/libs/fd/associate/ui.html';
```

將`{program-id}`和`{env-id}`取代為您的實際環境值。

### 步驟2：準備資料裝載

以下列格式建構您的資料裝載：

```javascript
const data = {
  id: "your-ic-id",              // Required: Interactive Communication ID
  prefill: {                      // Optional: Data to prefill the IC
    serviceName: "YourService",
    serviceParams: { key: "value" }
  },
  options: {}                     // Optional: Additional configuration options
};
```

**承載元件：**

| 元件 | 必要 | 說明 |
|-----------|----------|-------------|
| `id` | 是 | 要載入的互動式通訊(IC)識別碼 |
| `prefill` | 選用 | 包含用於資料預填的服務設定。 |
| `prefill.serviceName` | 選用 | 為預先填寫資料而呼叫的表單資料模型服務的名稱 |
| `prefill.serviceParams` | 選用 | 傳遞至預填服務的機碼值組 |
| `options` | 選用 | PDF轉譯支援的其他屬性 — 地區設定、includeAttachments、embedFonts、makeAccessible |

### 步驟3：實作整合函式

建立JavaScript函式以啟動關聯UI並處理訊息通訊：

```javascript
function launchAssociateUI(icId, prefillService, prefillParams, options) {
  if (!icId) {
    console.error('IC ID required');
    return;
  }
   
  const data = {
    id: icId,
    prefill: {
      serviceName: prefillService || '',
      serviceParams: prefillParams || {}
    },
    options: options || {}
  };
   
  const AEM_URL = 'https://your-aem.adobeaemcloud.com/libs/fd/associate/ui.html';
  const win = window.open(AEM_URL, '_blank');
   
  if (!win) {
    alert('Please enable pop-ups for this site');
    return;
  }
   
  const readyHandler = (event) => {
    if (event.data && event.data.type === 'READY' && event.data.source === 'APP') {
      win.postMessage({ type: 'INIT', source: 'PORTAL', data: data }, '*');
      window.removeEventListener('message', readyHandler);
    }
  };
   
  window.addEventListener('message', readyHandler);
   
  // Fallback timeout in case READY message is missed
  setTimeout(() => {
    if (win && !win.closed) {
      win.postMessage({ type: 'INIT', source: 'PORTAL', data: data }, '*');
      window.removeEventListener('message', readyHandler);
    }
  }, 1000);
}
```

### 步驟4：叫用函式

使用適當的引數呼叫函式：

```javascript
// Basic invocation with IC ID only
launchAssociateUI('12345', '', {}, {});

// With prefill service
launchAssociateUI('12345', 'FdmTestData', 
  { customerId: '101'}, {});

// With all parameters
launchAssociateUI('12345', 'FdmTestData', 
  { policyNumber: 'POL-123' }, 
  { locale: 'en', acrobatVersion: 'Acrobat_11' });
```

## 使用範例HTML頁面測試整合

若要觀察關聯UI如何出現在前端並測試您的整合，以下是一個簡單的HTML範例。 此範例頁面可讓您輸入IC ID、設定預填服務引數、設定PDF選項，以及在您的發佈執行個體上啟動關聯UI。

```html
<!DOCTYPE html>
<html>
<head>
  <title>Associate UI Integration</title>
  <style>
    body { 
      font-family: sans-serif; 
      max-width: 600px; 
      margin: 50px auto; 
      padding: 20px; 
    }
    .form-group { 
      margin: 20px 0; 
    }
    label { 
      display: block; 
      margin-bottom: 5px; 
      font-weight: bold; 
    }
    input, textarea { 
      width: 100%; 
      padding: 8px; 
      border: 1px solid #ccc; 
      border-radius: 4px; 
      box-sizing: border-box;
    }
    textarea { 
      height: 80px; 
      font-family: monospace; 
    }
    button { 
      padding: 10px 20px; 
      margin: 5px; 
      cursor: pointer; 
      border-radius: 4px;
    }
    .btn-primary { 
      background: #007bff; 
      color: white; 
      border: none; 
    }
    .btn-primary:hover {
      background: #0056b3;
    }
    .error { 
      color: red; 
      font-size: 12px; 
      display: none; 
    }
  </style>
</head>
<body>
  <h1>Launch Associate UI</h1>
  
  <form id="form">
    <div class="form-group">
      <label>IC ID *</label>
      <input type="text" id="icId" placeholder="Enter Interactive Communication ID" required>
    </div>
    
    <div class="form-group">
      <label>Prefill Service</label>
      <input type="text" id="serviceName" placeholder="e.g., CustomerDataService">
    </div>
    
    <div class="form-group">
      <label>Service Parameters (JSON)</label>
      <textarea id="serviceParams" placeholder='{"customerId": "12345"}'>{}</textarea>
      <span id="paramsError" class="error">Invalid JSON format</span>
    </div>
    
    <div class="form-group">
      <label>Options (JSON)</label>
      <textarea id="options" placeholder='{"mode": "edit", "locale": "en_US"}'>{}</textarea>
      <span id="optionsError" class="error">Invalid JSON format</span>
    </div>
    
    <button type="button" onclick="reset()">Reset</button>
    <button type="button" class="btn-primary" onclick="launch()">Launch Associate UI</button>
  </form>

  <script>
    // Replace with your AEM Publish instance URL
    const AEM_URL = 'https://publish-p{program-id}-e{env-id}.adobeaemcloud.com/libs/fd/associate/ui.html';
    
    function validateJSON(str, errorId) {
      const err = document.getElementById(errorId);
      try {
        const obj = JSON.parse(str || '{}');
        err.style.display = 'none';
        return obj;
      } catch (e) {
        err.style.display = 'block';
        return null;
      }
    }
    
    function launch() {
      const icId = document.getElementById('icId').value.trim();
      if (!icId) { 
        alert('IC ID is required'); 
        return; 
      }
      
      const params = validateJSON(document.getElementById('serviceParams').value, 'paramsError');
      const opts = validateJSON(document.getElementById('options').value, 'optionsError');
      
      if (!params || !opts) { 
        alert('Please fix JSON errors before launching'); 
        return; 
      }
      
      const data = {
        id: icId,
        prefill: {
          serviceName: document.getElementById('serviceName').value.trim(),
          serviceParams: params
        },
        options: opts
      };
      
      const win = window.open(AEM_URL, '_blank');
      if (!win) { 
        alert('Pop-up blocked. Please enable pop-ups for this site.'); 
        return; 
      }
      
      const handler = (e) => {
        if (e.data && e.data.type === 'READY' && e.data.source === 'APP') {
          win.postMessage({ type: 'INIT', source: 'PORTAL', data }, '*');
          window.removeEventListener('message', handler);
        }
      };
      
      window.addEventListener('message', handler);
      
      // Fallback timeout in case READY message is missed
      setTimeout(() => {
        if (win && !win.closed) {
          win.postMessage({ type: 'INIT', source: 'PORTAL', data }, '*');
          window.removeEventListener('message', handler);
        }
      }, 1000);
    }
    
    function reset() {
      document.getElementById('form').reset();
      document.getElementById('serviceParams').value = '{}';
      document.getElementById('options').value = '{}';
      document.getElementById('paramsError').style.display = 'none';
      document.getElementById('optionsError').style.display = 'none';
    }
  </script>
</body>
</html>
```

### 範例的運作方式

1. **IC ID欄位**：輸入互動式通訊識別碼（必要）
2. **預填服務**：指定預填資料的表單資料模型服務名稱
3. **服務引數**：輸入JSON物件以及要傳遞至預填服務的引數
4. **選項**：輸入PDF的組態選項，例如locale、includeAttachments、embedFonts、makeAccessible
5. **啟動按鈕**：在新視窗中開啟關聯UI，並傳送初始化資料

## 資料裝載範例

### 最小裝載（僅限IC）

當不需要預填資料時，請使用此選項：

```json
{
  "id": "12345",
  "prefill": { 
    "serviceName": "", 
    "serviceParams": {} 
  },
  "options": {}
}
```

### 使用預填資料

使用此選項以動態方式將客戶資料填入IC：

```json
{
  "id": "12345",
  "prefill": {
    "serviceName": "IC_FDM",
    "serviceParams": {
      "customerId": "101",
      "accountNumber": "ACC-98765"
    }
  },
  "options": {}
}
```

### 使用選項設定

使用此專案來指定其他演算選項：

```json
{
  "id": "12345",
  "prefill": {
    "serviceName": "IC_FDM",
    "serviceParams": {
      "customerId": "101",
      "accountNumber": "ACC-98765"
    }
  },
  "options": { 
      locale: "en_US",
      includeAttachments: "true",
      webOptimized: "false",
      embedFonts: "false",
      makeAccessible: "false"
  }
}
```

## 疑難排解

### 快顯視窗已封鎖

**問題**：「關聯UI」視窗未開啟。

**解決方案**：
- 在瀏覽器設定中為您的網域啟用快顯視窗
- 確定從使用者動作（例如按鈕點按）呼叫`window.open()`
- 使用不同的瀏覽器進行測試以識別封鎖行為

### 資料未載入

**問題**：互動式通訊已開啟，但資料未填入。

**解決方案**：
- 驗證IC ID是否正確，以及IC是否已發佈
- 檢查瀏覽器主控台是否有 JavaScript 錯誤
- 確定`postMessage`結構完全符合規格
- 驗證表單資料模型服務已正確設定

### 驗證錯誤

**問題**：當關聯使用者介面開啟時，使用者會收到驗證錯誤。

**解決方案**：
- 在發佈執行個體上設定SAML 2.0驗證
- 驗證使用者是否為&#x200B;**forms-associates**&#x200B;群組的成員
- 檢查工作階段逾時設定

### CORS錯誤

**問題**：主控台中有跨原始資源共用錯誤。

**解決方案**：
- 針對開發：在`'*'`中使用`postMessage`作為目標來源
- 用於生產：指定應用程式的確切來源URL
- 確認發佈執行個體CORS設定允許您的應用程式網域

<!--## Best Practices

When implementing the Associate UI integration, follow these best practices:

1. **Validation**: Always validate the IC ID and JSON payload before sending
2. **Error Handling**: Implement proper error handling for `window.open()` failures
3. **User Experience**: Display a loading indicator while the Associate UI initializes
4. **Memory Management**: Remove event listeners after initialization to prevent memory leaks
5. **Testing**: Test the integration with popup blockers enabled to ensure graceful handling
6. **User Permissions**: Verify users have appropriate access to the forms-associates group-->

## 另請參閱

- [在互動式通訊編輯器中建立UI關聯](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md)
- [雲端上的互動式通訊](/help/forms/early-access-ea-features.md#interactive-communications-on-cloud)
- [搶先使用的功能](/help/forms/early-access-ea-features.md)