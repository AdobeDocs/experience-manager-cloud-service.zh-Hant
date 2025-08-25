---
title: 疑難排解Edge Delivery Services表單提交中的403禁止錯誤
description: 瞭解如何診斷並解決從Edge Delivery Services提交表單到AEM Publish時出現403禁止的錯誤。 本指南會說明常見原因，包括CORS、Dispatcher規則和反向連結篩選問題。
feature: Edge Delivery Services
role: Admin, Developer
exl-id: f397e059-f1b3-4afa-bd38-8f5fc591bb22
source-git-commit: d457bf9af377176222c2b96816fbbc4265e6b167
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 3%

---

# 疑難排解Edge Delivery Services表單提交中的403禁止錯誤 {#troubleshooting-403-forbidden-edge-delivery}

從Edge Delivery Services提交表單至AEM Publish時，您可能會遇到&#x200B;**403禁止存取**&#x200B;錯誤。 此錯誤表示伺服器拒絕處理請求，通常是因為安全性設定。 本文可協助您找出並解決此問題最常見的原因。

## 問題描述

使用者從Edge Delivery Services提交表單至AEM Publish時遇到&#x200B;**403禁止**&#x200B;錯誤。 錯誤顯示為：

- HTTP狀態碼： 403
- 錯誤訊息：「已禁止」或「拒絕存取」
- 表單提交失敗，未送達AEM提交servlet

此問題通常發生在Edge Delivery Services整合中，在Edge網域(`.aem.live`、`.aem.page`、`.hlx.page`、`.hlx.live`)上代管的表單嘗試提交資料至AEM Publish執行個體。

>[!IMPORTANT]
>
>透過重新導向設定，可使用相同存放庫來託管多個網站。 每個網站網域必須個別新增至允許清單，表單提交才能正常運作。
>
>**範例：**
>
>- 存放庫： `https://github.com/adobe/abc`
>- 網站1： `main--abc--adobe.aem.live`
>- 網站2： `main--abc1--adobe.aem.live`
>
>兩個網域都需要個別的允許清單專案，才能讓表單提交從兩個網站正常運作。

## 常見原因與解決方法

Edge Delivery Services表單提交中出現403禁止錯誤可能有多個原因。 請依序按照下列疑難排解步驟進行：

### &#x200B;1. CORS （跨原始資源共用）問題

**症狀：**

- 瀏覽器主控台會顯示CORS相關的錯誤訊息
- 網路索引標籤會顯示連線到伺服器之前遭到封鎖的要求
- 提及「已封鎖跨原始請求」的錯誤訊息

**診斷：**

1. 開啟瀏覽器開發人員工具(F12)
2. 檢查Console索引標籤以取得CORS錯誤訊息
3. 尋找類似以下的訊息： `Access to fetch at 'https://publish-xxx.adobeaemcloud.com' from origin 'https://main--repo--owner.aem.live' has been blocked by CORS policy`

**解決方案：**
在AEM中設定CORS設定，以允許來自您特定Edge Delivery網站網域的請求：

```apache
# Developer Localhost
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(http://localhost(:\d+)?$)#" CORSTrusted=true

# Edge Delivery Sites - Add each site domain individually
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://main--abc--adobe\.aem\.live$)#" CORSTrusted=true
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://main--abc1--adobe\.aem\.live$)#" CORSTrusted=true

# Legacy Franklin domains (if still in use)
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.page$)#" CORSTrusted=true  
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.live$)#" CORSTrusted=true
```

>[!NOTE]
>
>將`main--abc--adobe.aem.live`和`main--abc1--adobe.aem.live`取代為您實際的網站網域。 從相同存放庫託管的每個網站都需要個別的CORS設定專案。

如需詳細的CORS組態，請參閱[CORS組態指南](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors)。

### &#x200B;2. Dispatcher規則

**症狀：**

- 403錯誤發生在瀏覽器控制檯中不含CORS訊息
- 請求到達伺服器但被Dispatcher封鎖
- 到達AEM應用程式層之前發生錯誤

**診斷：**

1. 檢查請求URL是否符合任何Dispatcher篩選規則
2. 檢閱可能封鎖POST請求的`/filter`規則的Dispatcher設定
3. 確認Dispatcher設定中允許表單提交端點

**解決方案：**
更新Dispatcher設定以允許表單提交請求：

1. 確保允許表單提交端點的POST請求
2. 為Edge Delivery網域新增適當的篩選規則
3. 確認未封鎖提交servlet路徑

Dispatcher篩選器設定範例：

```apache
/filter {
  # Allow POST requests to form submission servlet
  /0100 { /type "allow" /method "POST" /url "/content/forms/af/*" }
  /0101 { /type "allow" /method "POST" /url "/adobe/forms/af/submit/*" }
  /0102 { /type "allow" /method "POST" /url "/content/forms/portal/submit/adaptiveform" }
}
```

### 3.反向連結篩選問題

**症狀：**

- 瀏覽器主控台中沒有CORS問題的403錯誤
- 請求到達AEM但被Sling查閱者篩選拒絕
- AEM應用程式層發生錯誤

**診斷：**
檢查AEM錯誤記錄檔中的反向連結篩選拒絕訊息：

1. [透過Cloud Manager存取AEM雲端服務記錄檔](/help/implementing/cloud-manager/manage-logs.md)
2. 尋找`aemerror.log`中包含：
   - 「已拒絕反向連結篩選器」
   - &quot;org.apache.sling.security.impl.ReferrerFilter&quot;
   - 表示反向連結驗證失敗的訊息

**範例記錄專案：**

```
[ERROR] org.apache.sling.security.impl.ReferrerFilter Referrer filter rejected request with referrer 'https://main--abc--adobe.aem.live' for POST /content/forms/af/submit
```

**解決方案：**
設定反向連結篩選條件，以允許您的特定Edge Delivery網站網域：

1. 建立或更新OSGi設定檔： `org.apache.sling.security.impl.ReferrerFilter.cfg.json`

2. 針對您的特定網站網域新增下列設定：

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

3. 透過Cloud Manager部署設定

>[!IMPORTANT]
>
>**對於重複設定：**&#x200B;您必須個別將每個網站網域新增到`allow.hosts`陣列。 僅使用regex模式可能並不足以滿足所有情況。 包含特定網域和規則運算式模式，以便完整涵蓋。

>[!WARNING]
>
>AEM 的查閱者篩選器不是 OSGi 設定工廠，這表示一次只有一個設定在 AEM 服務上作用。儘可能避免新增自訂反向連結篩選設定，因為這會覆寫AEM的原生設定，且可能會破壞產品功能。

## 診斷步驟

請依照下列步驟，識別403錯誤的特定原因：

### 步驟1：檢查瀏覽器主控台

1. 開啟瀏覽器開發人員工具(F12)
2. 導覽至Console標籤
3. 嘗試表單提交
4. 尋找CORS相關的錯誤訊息

**如果出現CORS錯誤：**&#x200B;請遵循上述CORS解決方案。
**如果沒有CORS錯誤：**&#x200B;請繼續執行步驟2。

### 步驟2：檢查網路標籤

1. 開啟瀏覽器開發人員工具(F12)
2. 瀏覽至「網路」標籤
3. 嘗試表單提交
4. 檢查失敗的請求詳細資料
5. 檢視回應標題和狀態

**如果要求無法連線到伺服器：**&#x200B;可能是Dispatcher問題。
**如果要求到達伺服器但失敗：**&#x200B;可能是反向連結篩選問題。

### 步驟3：檢查AEM記錄

1. 存取 Cloud Manager
2. 瀏覽至您環境→環境→記錄檔
3. 下載或檢視`aemerror.log`
4. 搜尋表單提交時間周圍的專案
5. 尋找反向連結篩選或安全性相關訊息

## 預防與最佳實務

### 1.安裝期間正確的設定

- 在初始Edge Delivery Services設定期間設定CORS、Dispatcher和反向連結篩選設定
- **針對每個新網站：**&#x200B;將特定網域新增至所有允許清單（CORS、反向連結篩選器）
- 上線前在開發環境中測試表單提交

### 2.特定環境的設定

- 針對開發、測試和生產環境使用不同的設定
- 納入本機開發測試的本機主機網域
- **記錄您的存放庫需要允許清單存取權的所有網站網域**

### 3.監控與記錄

- 設定反向連結篩選條件拒絕的記錄監視
- 在表單提交程式碼中實作適當的錯誤處理
- 測試期間使用瀏覽器開發人員工具

### 4.檔案與團隊知識

- **使用相同存放庫維護所有網站網域的登入**
- 訓練開發團隊疑難排解步驟
- 維護Edge Delivery Services表單設定的檢查清單
- 當從現有存放庫建立新網站時，**更新允許清單**

## 可重複設定的網站網域管理

使用Helix-5和無防護架構，請遵循下列准則：

### 建立新網站時

1. **識別網站網域** （例如，`main--newsite--adobe.aem.live`）
2. **更新CORS設定**&#x200B;以包含新網域
3. **更新反向連結篩選器**&#x200B;以在`allow.hosts`中包含新網域
4. 從新網站&#x200B;**測試表單提交**
5. **在您的網站登入中記錄新網域**

### 網域命名模式

- 標準模式： `{branch}--{site}--{owner}.aem.live`
- 即使共用相同的存放庫，每個網站也會取得唯一的網域
- 同時可以使用`.aem.live`和`.aem.page`網域

### 設定管理

- 使用`allow.hosts`中的特定網域專案以獲得更好的安全性
- 以規則運算式模式補充，以擴大涵蓋範圍
- 在新增或移除網站時，定期稽核和更新允許清單

## 其他資源

- [使用AEM Headless設定反向連結篩選器](/help/headless/deployment/referrer-filter.md)
- [CORS 設定指南](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors)
- [瞭解跨原始資源共用](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing)
- [Edge Delivery Services Forms檔案](/help/edge/docs/forms/universal-editor/publish-forms.md)

## 相關主題

- [設定提交動作](/help/forms/configuring-submit-actions.md)
- [表單提交服務](/help/forms/forms-submission-service.md)
- [Edge Delivery Services 概觀](/help/edge/overview.md)


**需要其他協助嗎？**&#x200B;如果您在依照這些疑難排解步驟操作後持續遇到問題，請聯絡Adobe客戶支援服務：

- 您的特定錯誤訊息
- AEM Cloud Service環境詳細資料
- **需要表單提交存取權的所有Edge Delivery Services網站網域**
- 從錯誤發生時開始的相關記錄專案

**需要其他協助嗎？**&#x200B;如果您在依照這些疑難排解步驟操作後持續遇到問題，請聯絡Adobe客戶支援服務：

- 您的特定錯誤訊息
- AEM Cloud Service環境詳細資料
- Edge Delivery Services網域資訊
- 從錯誤發生時開始的相關記錄專案
