---
title: 在Forms的規則編輯器中整合API
description: 瞭解規則編輯器中Invoke Service的最新增強功能，包括如何在不使用表單資料模型的情況下，根據核心元件來整合最適化Forms的API。
feature: Adaptive Forms, Core Components, Edge Delivery Services
role: User, Developer
level: Beginner, Intermediate
keywords: 在規則編輯器中整合API，叫用服務增強功能
exl-id: fc51f86d-e672-4513-b473-6700757a0c3d
source-git-commit: 80dde7ddaa08d752391b4004d7c93e5baac9716e
workflow-type: tm+mt
source-wordcount: '1021'
ht-degree: 0%

---

# 在規則編輯器中整合API

<span>規則編輯器中的Integrating API在早期採用者程式之下。 您可以從您的正式電子郵件ID寫信到`aem-forms-ea@adobe.com`，以加入早期採用者程式並請求存取權能。</span>

最適化Forms中的視覺化規則編輯器支援直接API整合，而不需要建立表單資料模型。 您可以輸入API URL （JSON格式）或透過cURL命令匯入設定，以連線至API端點。 整合後，**Invoke Service**&#x200B;動作可用於呼叫API。

表單欄位可以直接對應到API設定中定義的輸入引數。 同樣地，對於對應的API回應，可以使用&#x200B;**事件裝載**&#x200B;選項將輸出引數對應至表單欄位。

此外，視覺規則編輯器可讓您在叫用服務時定義&#x200B;**success**&#x200B;和&#x200B;**failure處理常式**。 成功處理常式會指定要在成功的API呼叫後執行的動作，而失敗處理常式會定義發生錯誤時表單的回應方式。

>[!NOTE]
>
> 規則編輯器中的API整合也適用於在Universal Editor[中編寫的](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)Edge Delivery Services Forms。

## 比較： API整合方法

| 層面 | API與表單資料模型(FDM)整合 | 直接API整合（透過&#x200B;*建立API整合*） |
|--------------------------------|---------------------------------------------------------------------|-----------------------------------------------------------|
| **用途** | 跨多個表單的集中式、可重複使用的API整合 | 快速、表單特定的API整合 |
| **安裝位置** | 在表單資料模型編輯器(AEM主控台)中建立和編輯 | 直接在自適應表單規則編輯器中建立和編輯 |
| **複雜度** | 更高的設定工作量（需要對應和設定） | 簡單輕量 |
| **最適合** | 具有多種表單的企業或大型使用案例 | 小型表單、原型或一次性API呼叫 |

## API整合設定

底下熒幕擷圖顯示API整合設定視窗：

![API整合設定](/help/forms/assets/api-integration-configuration.png)

### 主要組態選項

**API整合設定**

* **從cURL匯入**：貼上現成的cURL命令來設定API整合，而非手動輸入詳細資料，例如API URL、HTTP方法、標頭和引數。
* **顯示名稱**： API服務的自訂名稱。
* **API URL**： API服務的端點。
* **選取HTTP方法**：用來呼叫API的HTTP要求方法。
* **內容型別**：定義要求與回應格式。
* **需要加密**： （選擇性）確保在傳輸期間加密機密資料。
* **在使用者端執行**：啟用時，會從使用者端（瀏覽器）而不是伺服器執行API呼叫。

**驗證型別**

* **選項**：無、基本、API金鑰、OAuth 2.0。

**輸入引數**

* **為輸入上傳JSON**：上傳範例JSON檔案以自動填入輸入對應。
   * **名稱**： API需要的輸入引數名稱。
   * **型別**：輸入的資料型別（字串、數字、布林值等）。
   * **In**：引數（查詢、標頭或內文）的位置。
   * **預設值**：若使用者未提供，則為預填值。
   * **新增**：新增其他輸入引數的選項。

**輸出引數**

* **為輸出上傳JSON**：上傳範例API回應以自動產生對應。
   * **名稱**： API回應中的輸出引數名稱。
   * **型別**：輸出引數的預期資料型別（字串、數字等）。
   * **In**：定義對應值的預期位置。
   * **新增/刪除**：新增對應或移除現有對應。

## 使用案例：在簽證申請表單中填入國家/地區欄位

>[!VIDEO](https://video.tv.adobe.com/v/3471606/rule-editor-api-integration/?quality=12&learn=on)

**案例**：政府機構提供包含下列欄位的線上簽證申請表：

1. 全名（文字）
2. 出生日期（日期）
3. 公民身分國家（下拉式清單）
4. 護照號碼（文字）
5. 護照簽發國家/地區（下拉式清單）
6. 目的地國家/地區（下拉式清單）
7. 預定抵達日期（日期）

表單不會維護靜態的國家清單，而是使用&#x200B;**getcountryname API**&#x200B;動態擷取國家/地區資訊(大陸、資本、ISO Alpha代碼等)：

`https://secure.geonames.org/countryInfoJSON?username=aemforms`

這可確保在填寫表單時，申請人一律能看到最新且正確的國家清單。

### 在規則編輯器中使用API整合的實作

您可以按一下規則編輯器中的「**建立API整合**」按鈕，整合API而不建立表單資料模型。

![建立API整合](/help/forms/assets/create-api-integration.png)

名稱為&#x200B;**getcountryname**&#x200B;的API服務是在規則編輯器中的&#x200B;**API整合組態**&#x200B;下設定：

![API REST端點設定](/help/forms/assets/api-restendpoint.png)

* **API端點URL** → `https://secure.geonames.org/countryInfoJSON?username=aemforms`
* GET→的&#x200B;**HTTP方法**
* **內容型別** → JSON
* **輸入** → `username`已傳遞為查詢引數(`aemforms`)。
* **輸出** →回應欄位（例如`continent`、`capital`、`countrynames`、`isoAlpha3`和`languages`）已對應至表單欄位。

在&#x200B;**簽證申請表單**&#x200B;中，三個下拉式欄位（**公民國家/地區**、**護照簽發國家/地區**&#x200B;和&#x200B;**目的地國家/地區**）繫結至&#x200B;**叫用服務**&#x200B;動作。

表單載入時，**叫用服務**&#x200B;會從API擷取國家/地區清單。 接著會對映回應，以自動填入下拉式選項。

例如，當使用者開啟&#x200B;**公民權國家**&#x200B;時，API回應會動態顯示國家/地區清單。

![invoke-service-api-integration](/help/forms/assets/invoke-service-api-integration.png)

![API整合輸出](/help/forms/assets/api-integration-output.png)

同樣地，**Passport Issuance**&#x200B;和&#x200B;**目的地國家/地區**&#x200B;使用相同的API呼叫，確保所有三個欄位中的資料一致且為最新狀態。

## 實作API失敗的重試機制

當API請求失敗時，在報告錯誤給使用者之前重試請求通常會有幫助。 您可以在&#x200B;**function.js**&#x200B;檔案中寫入自訂程式碼，以實作輪詢和重試機制。

以下範例示範如何處理最多兩次重試和兩次重試之間的指數輪迴的API失敗：

```javascript
/**
 * Handles request retries with up to 2 retry attempts
 * @param {function} requestFn - The request function to execute
 * @return {Promise} A promise that resolves with the response or rejects after all retries
 */
function retryHandler(requestFn) {
    const MAX_RETRIES = 2;
    
    /**
     * Attempts the request with retry metadata
     * @param {number} retryCount - Current retry attempt count
     * @return {Promise} The request promise
     */
    function attemptRequest(retryCount = 0) {
        // Include retry metadata if this is a retry
        const requestOptions = retryCount > 0 ? {
            headers: {
                'X-Retry': 'true',
                'X-Retry-Count': retryCount.toString(),
                'X-Retry-Time': new Date().toISOString()
            },
            body: {
                retry: true,
                retryCount: retryCount,
                timestamp: Date.now()
            }
        } : undefined;

        return requestFn(requestOptions)
            .then(function(response) {
                if (response && response.status >= 400) {
                    console.warn('Request failed with status ' + response.status);
                    throw new Error('Request failed with status ' + response.status);
                }
                return response;
            })
            .catch(function(error) {
                console.warn('Request attempt ' + (retryCount + 1) + ' failed:', error.message);
                
                // Retry if max attempts not reached
                if (retryCount < MAX_RETRIES) {
                    console.log('Retrying request, attempt ' + (retryCount + 2) + ' of ' + (MAX_RETRIES + 1));
                    
                    // Exponential backoff delay: 1s, 2s, 4s...
                    const delay = Math.pow(2, retryCount) * 1000;
                    
                    return new Promise(function(resolve) {
                        setTimeout(resolve, delay);
                    }).then(function() {
                        return attemptRequest(retryCount + 1);
                    });
                } else {
                    // All retries exhausted
                    console.error('All retry attempts failed. Final error:', error.message);
                    throw new Error('Request failed after ' + (MAX_RETRIES + 1) + ' attempts: ' + error.message);
                }
            });
    }
    
    // Start the first attempt
    return attemptRequest(0);
}
```

在上述程式碼中，**retryHandler**&#x200B;函式會管理API要求，並在失敗時自動重試。 它會採用請求函式(requestFn)，並嘗試請求最多兩次，為每次重試新增中繼資料。

>[!NOTE]
>
> 如需有關如何新增自訂函式的詳細步驟，請參閱[以核心元件為基礎的最適化Forms的自訂函式簡介](/help/forms/create-and-use-custom-functions.md)一文。

## 常見問題

* **我需要建立表單資料模型以整合最適化Forms中的API嗎？**\
  不行。使用視覺化規則編輯器，您可以使用&#x200B;**建立API整合**&#x200B;選項直接整合API，而不需要建立表單資料模型。 此方法最適合輕量型或特定表單的使用案例。

* **我可以保護從規則編輯器發出的API呼叫嗎？**\
  可以。API整合設定提供驗證選項，例如&#x200B;**Basic、API Key和OAuth 2.0**。 您也可以啟用&#x200B;**需要加密**，以確保機密資料的安全傳輸。
