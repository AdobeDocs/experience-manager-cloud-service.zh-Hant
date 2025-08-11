---
title: 適用於Edge Delivery Services的Forms提交服務
description: 使用Adobe的託管Forms提交服務，將表單提交直接儲存在試算表中。 瞭解Google Sheets、OneDrive和SharePoint整合的設定、設定和API使用方式。
keywords: Forms提交服務， Edge Delivery Services forms，試算表整合， Google Sheets forms， OneDrive forms， SharePoint forms，表單資料收集
feature: Edge Delivery Services
role: User, Developer, Admin
level: Beginner, Intermediate
hide: true
hidefromtoc: true
exl-id: 12b4edba-b7a1-4432-a299-2f59b703d583
source-git-commit: a2cdc36d4df7651d70d42118b6641935279673fc
workflow-type: tm+mt
source-wordcount: '1573'
ht-degree: 1%

---

# 適用於Edge Delivery Services的Forms提交服務

Forms提交服務是Adobe的託管解決方案，可自動將表單提交資料直接儲存在您偏好的試算表中：Google Sheets、Microsoft OneDrive或SharePoint。 如此一來，您就不需要複雜的後端基礎架構，同時還能提供即時資料收集與管理。

## 概觀

![Forms提交服務](/help/forms/assets/form-submission-service.png)
*圖：Forms提交服務工作流程 — 從表單提交到試算表儲存*

+++ 誰應該使用此服務？

**最適合：**

- **內容建立者**&#x200B;正在建置簡單的資料收集表單
- **小型企業**&#x200B;需要快速的表單至試算表工作流程
- **行銷團隊**&#x200B;正在收集潛在客戶資訊
- **活動召集人**&#x200B;管理註冊

**考慮下列專案的替代方案：**

- 需要自訂邏輯的複雜工作流程
- 企業與資料庫的整合
- 需要進階驗證或處理的Forms

+++

+++ 常見使用案例

| 使用案例 | 範例 | 試算表優點 |
|----------|---------|-------------------|
| **連絡Forms** | Google工作表→網站查詢 | 輕鬆追蹤及CRM匯入 |
| **活動註冊** | Excel Online→的會議註冊 | 即時出席者追蹤 |
| **銷售機會開發** | SharePoint→電子報註冊 | 行銷活動分析 |
| **意見集合** | Google工作表→的調查回應 | 快速資料視覺效果 |

+++

## 主要優點

Forms提交服務提供幾個簡化資料收集的優點：

+++ 簡化設定

- **不需要後端基礎結構** - Adobe代管提交端點
- **直接整合**&#x200B;與熱門試算表平台
- **自動將表單欄位中的資料對應**&#x200B;至試算表欄

+++


+++ 即時資料管理

- **即時資料擷取** — 提交內容會立即顯示在您的試算表中
- **結構化儲存空間** — 方便分析的結構化資料行
- **即時共同作業** — 多個團隊成員可以存取和分析資料

+++

+++ 內建安全性與存取控制

- **利用現有許可權** — 使用試算表平台的共用控制項
- **Adobe代管安全性** — 具有企業級保護的安全提交端點
- **資料擁有權** — 您的資料會保留在您選擇的試算表平台上

+++

## 先決條件

設定Forms提交服務前，請確定您已：



+++ 技術需求

- 為您的Edge Delivery Services專案設定的&#x200B;**GitHub存放庫**&#x200B;已安裝最新的Adaptive Forms Block
- **存取核准** — 已新增至允許清單的存放庫

+++

+++ 試算表平台設定


選擇其中一個支援的平台：

- **Google工作表** — 具有工作表建立許可權的Google帳戶
- **Microsoft OneDrive** — 具有Excel Online存取權的Microsoft 365帳戶
- **SharePoint** — 使用清單/程式庫許可權存取SharePoint

+++

+++ 許可權與存取

- **編輯目標試算表的許可權**
- **共用功能**&#x200B;以授與`forms@adobe.com`的存取權
- 針對您選擇的平台產生&#x200B;**連結**&#x200B;許可權

+++

>[!TIP]
>
>**不熟悉Edge Delivery Services？**&#x200B;從[快速入門教學課程](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/tutorial)開始，以設定您的專案基礎。

## 設定方法

Forms提交服務提供兩種設定方法。 選擇最適合您工作流程的方法：


+++ 選擇您的設定方法

| 方法 | 最適合 | 所需時間 | 技術等級 |
|--------|----------|---------------|-----------------|
| **[手動設定](#manual-configuration)** | 內容建立者，一次性設定 | 10-15 分鐘 | 初學者 |
| **[API組態](#api-configuration)** | 開發人員，自動化工作流程 | 5-10 分鐘 | 中級 |

+++

+++ 專案設定

在設定任一方法之前，請確定您的AEM專案基礎已準備就緒：

1. **使用最新的Adaptive Forms區塊（**&#x200B;快速入門教學課程[）建立或更新您的AEM專案](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/tutorial)

2. **更新專案根目錄中的`fstab.yaml`**：

   ```yaml
   # Replace with the path to your shared folder
   mountpoints:
     /: https://drive.google.com/drive/folders/your-shared-folder-id
   ```


3. **與**&#x200B;共用您的專案資料夾`forms@adobe.com` （需要編輯許可權）

+++

+++

## 手動設定

![表單提交服務的工作流程](/help/forms/assets/forms-submission-service-workflow.png)
*圖：手動Forms提交服務設定的完整工作流程*

請依照下列逐步指示，設定具有試算表提交的表單：



+++ 步驟1：建立您的表單定義

使用Google Sheets或Microsoft Excel建立您的表單結構。

**表單建立步驟：**

1. **開啟您的試算表平台** (Google工作表或Microsoft Excel)
2. **為您的表單專案建立新的試算表**
3. **為您的工作表命名** （必須是`helix-default`或`shared-aem`）
4. **使用**&#x200B;表單建立指南[定義您的表單結構](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/create-forms)

![表單定義](/help/forms/assets/form-submission-definition.png)
*範例：具有欄位型別、標籤和驗證規則的表單定義*

>[!IMPORTANT]
>
>**工作表命名需求**
>
>您的表單定義表必須命名為：
>
>- `helix-default` （建議用於單一表單）
>- `shared-aem` （適用於多表單專案）
>
>系統無法辨識其他工作表名稱。

**驗證檢查點：**

- 表單結構已完成，包含所有必填欄位
- 工作表已正確命名（`helix-default`或`shared-aem`）
- 欄位型別和驗證規則已正確設定

+++

+++ 步驟2：建立資料收集工作表

設定專用的工作表，以接收表單提交資料。

**資料表設定：**

1. **新增工作表**&#x200B;至您現有的試算表
2. **將工作表命名為`incoming`** （區分大小寫）
3. **設定符合表單欄位的欄標題**
4. **儲存試算表**&#x200B;以確保變更得以保留

![傳入工作表](/help/forms/assets/form-submission-incoming-sheet.png)
*範例：含有與表單欄位相符之欄標題的傳入工作表*

>[!WARNING]
>
>**重要需求**
>
>工作表必須命名為`incoming` （小寫）。 如果沒有此工作表：
>
>- 將拒絕表單提交
>- 不會儲存任何資料
>- 使用者將看到提交錯誤

**驗證檢查點：**

- 您的試算表中有`incoming`張工作表
- 欄標題符合您的表單欄位名稱
- 工作表已正確儲存且可存取

>[!TIP]
>
>**專業秘訣：**&#x200B;複製表單定義中的確切欄位名稱，以確保表單欄位與試算表欄位完全相符。

+++

+++ 步驟3：與Adobe服務共用試算表

授予Adobe Forms提交服務對試算表的存取權。

**共用處理序：**

1. **按一下試算表右上角的「共用」按鈕**
2. **新增Adobe服務帳戶：**
   - 電子郵件： `forms@adobe.com`
   - 許可權層級： **編輯器** （資料寫入所需）
3. **傳送共用邀請**
4. **複製試算表連結**，以供後續步驟使用

   ![共用傳入工作表](/help/forms/assets/form-submission-share-incoming.png)
   *授予Adobe服務存取權的逐步共用程式*

**平台特定指示：**

**Google工作表：**

- 新增`forms@adobe.com`為編輯器
- 確定已啟用「擁有連結的任何人都可以檢視」
- 複製分享連結

**Microsoft Excel (OneDrive/SharePoint)：**

- 新增具有編輯許可權的`forms@adobe.com`
- 將連結共用設定為「擁有連結的任何人都可以編輯」
- 複製共用URL

  ![複製傳入工作表的連結](/help/forms/assets/form-submission-copy-link.png)
  *範例：複製表單組態的可共用連結*

**驗證檢查點：**

- `forms@adobe.com`擁有您試算表的編輯器存取權
- 試算表連結已複製並可供使用
- 共用許可權允許外部存取

+++

+++ 步驟4：將表單連線至試算表

將您的表單定義連結至提交試算表。

**表單試算表連線：**

1. **開啟您的表單定義試算表** （含有`helix-default`或`shared-aem`張表格的試算表）
2. **在您的表單定義中找到提交欄位列**
3. **將複製的試算表連結**&#x200B;貼到[提交]欄位的&#x200B;**動作**&#x200B;欄
4. **儲存變更**&#x200B;至您的表單定義

   ![連結試算表](/help/forms/assets/form-submission-sheet-linking.png)

*範例：將提交動作連線至您的資料收集試算表*

**正在發佈您的表單：**

1. 在瀏覽器中&#x200B;**開啟AEM Sidekick**
2. **預覽您的表單**&#x200B;以測試設定
3. **發佈表單**&#x200B;以使其上線

**最終驗證：**

- 試算表連結已正確新增至提交欄位動作
- 表單定義已儲存並發佈
- 表單預覽正確顯示所有欄位
- 提交按鈕已正確設定

>[!SUCCESS]
>
>**安裝完成！**&#x200B;您的表單現在已連線至Forms提交服務。 提交範例資料並檢查您的`incoming`工作表以進行測試。

**參考資料：**

- [使用適當的組態完成範例試算表](/help/forms/assets/spreadsheet.xlsx)
- 發佈指引的[AEM Sidekick檔案](https://www.aem.live/docs/sidekick)

+++

## API 設定

API方法可讓開發人員以程式設計方式將資料提交至Forms Submission Service，適用於自動化工作流程和自訂整合。


+++ 何時使用API

**最適合：**

- 自動化資料收集系統
- 自訂表單實作
- 與現有應用程式整合
- 大量資料提交工作流程

+++

+++ API必要條件

在使用API之前，請確定您已：

- **試算表設定**&#x200B;已完成（包括`incoming`張工作表）
- **已授與Adobe服務存取權** `forms@adobe.com`
- **表單識別碼** （來自您發佈的表單）
- **存放庫資訊** （組織和網站名稱）

>[!IMPORTANT]
>
>**必要的安裝步驟**
>
>此API需要與手動設定相同的試算表設定：
>
>- `incoming`工作表必須存在
>- `forms@adobe.com`必須擁有編輯器存取權
>- 工作表必須透過AEM Sidekick發佈

+++

+++ API端點與驗證

**基底URL：** `https://forms.adobe.com/adobe/forms/af/submit/{id}`

**必要的標頭：**

- `Content-Type: application/json`
- `x-adobe-routing: tier=live,bucket=main--[repository]--[organization]`

**API檔案：** [完整API參考](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/references/aem-forms-submission-service/)

+++

+++ 使用Postman

Postman提供方便使用者的介面，用於測試API提交。

**安裝指示：**

1. **在Postman中建立新的POST要求**
2. **設定端點：** `https://forms.adobe.com/adobe/forms/af/submit/{id}`
3. **取代預留位置：**
   - `{id}`→您的實際表單識別碼
   - `[repository]`→您的GitHub存放庫名稱
   - `[organization]`→您的GitHub組織/使用者名稱

**要求設定：**

    &grave;&grave;json
發佈https://forms.adobe.com/adobe/forms/af/submit/your-form-id

標頭：
Content-Type： application/json
x-adobe-routing： tier=live，bucket=main—your-repo—your-org

內文(JSON)：
&lbrace;
&quot;data&quot;： &lbrace;
&quot;startDate&quot;： &quot;2025-01-10&quot;，
&quot;endDate&quot;： &quot;2025-01-25&quot;，
&quot;destination&quot;： &quot;Australia&quot;，
「類別」：「第一類」，
&quot;budget&quot;： &quot;2000&quot;，
&quot;amount&quot;： &quot;1000000&quot;，
&quot;name&quot;： &quot;Mary&quot;，
&quot;age&quot;： &quot;35&quot;，
&quot;subscribe&quot;：空值，
&quot;email&quot;： &quot;mary@gmail.com&quot;
&rbrace;
&rbrace;

```

**預期的回應：**

- **狀態碼：** `201 Created`
- **資料會立即顯示在您的**&#x200B;試算表中`incoming`

![郵遞員熒幕](/help/forms/assets/postman-api.png)
*範例：使用Postman介面成功提交API*

+++

+++ 使用命令列(curl)

對於偏好終端機/命令提示的開發人員，請使用curl以程式設計方式提交資料。

**命令列設定：**

在下列命令中取代下列預留位置：

- `{id}`→您的實際表單識別碼
- `[repository]`→您的GitHub存放庫名稱
- `[organization]`→您的GitHub組織/使用者名稱

>[!BEGINTABS]

>[!TAB macOS/Linux]

```bash

curl -X POST "https://forms.adobe.com/adobe/forms/af/submit/your-form-id" \
    --header "Content-Type: application/json" \
  --header "x-adobe-routing: tier=live,bucket=main--your-repo--your-org" \
    --data '&lbrace;
        "data": &lbrace;
            "startDate": "2025-01-10",
            "endDate": "2025-01-25",
            "destination": "Australia",
            "class": "First Class",
            "budget": "2000",
            "amount": "1000000",
            "name": "Joe",
            "age": "35",
            "subscribe": null,
      "email": "joe@example.com"
                &rbrace;
            &rbrace;'

        ```

>[!TAB Windows Command Prompt]
     
```cmd

curl -X POST "https://forms.adobe.com/adobe/forms/af/submit/your-form-id" ^
    --header "Content-Type: application/json" ^
  --header "x-adobe-routing: tier=live,bucket=main--your-repo--your-org" ^
  --data "{\"data\": {\"startDate\": \"2025-01-10\", \"endDate\": \"2025-01-25\", \"destination\": \"Australia\", \"class\": \"First Class\", \"budget\": \"2000\", \"amount\": \"1000000\", \"name\": \"Joe\", \"age\": \"35\", \"subscribe\": null, \"email\": \"joe@example.com\"}}"

```

>[!TAB Windows PowerShell]

```powershell

$body = @&lbrace;
  data = @&lbrace;
    startDate = "2025-01-10"
    endDate = "2025-01-25"
    destination = "Australia"
    class = "First Class"
    budget = "2000"
    amount = "1000000"
    name = "Joe"
    age = "35"
    subscribe = $null
    email = "joe@example.com"
  &rbrace;
&rbrace; | ConvertTo-Json -Depth 3

Invoke-RestMethod -Uri "https://forms.adobe.com/adobe/forms/af/submit/your-form-id" &grave;
  -Method POST &grave;
  -Headers @{"Content-Type"="application/json"; "x-adobe-routing"="tier=live,bucket=main--your-repo--your-org"} &grave;
  -Body $body

    ```

>[!ENDTABS]

+++

+++ API Response & Verification

**Successful Response:**

```http

HTTP/1.1 201 Created
Connection: keep-alive
Content-Length: 0
X-Request-Id: 02a53839-2340-56a5-b238-67c23ec28f9f
X-Message-Id: 42ecb4dd-b63a-4674-8f1a-05a4a5b0372c
Date: Fri, 10 Jan 2025 13:06:10 GMT
Access-Control-Allow-Origin: *

```

**資料驗證：**

成功提交後，請確認資料是否顯示在試算表中：

![已更新工作表](/help/forms/assets/updated-sheet.png)
*範例：資料已透過API成功寫入傳入工作表*

**回應驗證：**

- **HTTP狀態：** `201 Created`表示提交成功
- **X-Request-Id：**&#x200B;用於追蹤提交的唯一識別碼
- **資料會在數秒內顯示在您的**&#x200B;工作表中`incoming`
- **所有表單欄位**&#x200B;皆已正確對應至試算表欄

+++

## 疑難排解



+++ 常見問題與解決方法

**問題： 403禁止錯誤**

```

Causes: Missing or incorrect access permissions
Solutions:
- Verify forms@adobe.com has Editor access to your spreadsheet
- Check that your repository is added to the allowlist
- Confirm the x-adobe-routing header format

```

**問題： 404 Not Found錯誤**

```

Causes: Incorrect Form ID or endpoint URL
Solutions:  
- Verify your Form ID is correct
- Check the API endpoint URL format
- Ensure your form is published and live

```


**問題：資料未出現在試算表中**

```

Causes: Missing 'incoming' sheet or permission issues
Solutions:
- Confirm 'incoming' sheet exists (case-sensitive)
- Verify column headers match form field names exactly
- Check forms@adobe.com has edit permissions
- Ensure spreadsheet is shared properly

```


**問題：無效的JSON格式錯誤**

```

Causes: Malformed request body
Solutions:
- Validate JSON syntax using online JSON validators
- Ensure proper escaping of special characters
- Check quote marks and brackets are balanced

```


+++

+++ 取得協助

**支援管道：**

- **搶先存取問題：**&#x200B;電子郵件[aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)
- **API檔案：** [開發人員參考資料](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/references/aem-forms-submission-service/)
- **社群支援：** [Adobe Experience League社群](https://experienceleaguecommunities.adobe.com/)

+++

## 後續步驟

現在您已設定Forms提交服務，請探索下列相關主題：


+++ 增強您的Forms

- **[建立進階Forms](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/create-forms)** — 新增驗證、條件式邏輯和自訂樣式
- **[表單元件指南](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/forms-components)** — 探索可用的表單欄位型別

+++

+++ 替代提交方法

- **[AEM發佈提交](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)** — 適用於複雜的工作流程和企業整合
- **[自訂提交動作](/help/forms/configure-submit-actions-core-components.md)** — 進階提交處理

+++

+++ 資料管理

- **[表單分析](/help/forms/view-understand-aem-forms-analytics-reports.md)** — 追蹤表單效能和使用狀況
- **[資料整合](/help/forms/configure-data-sources.md)** — 將表單連線至資料庫和CRM系統

+++

## 摘要

Forms提交服務提供功能強大、無程式碼的解決方案，可直接將表單資料收集至試算表中。 主要優點包括：

- **快速設定** — 不需要後端基礎結構
- **即時資料** — 立即提交擷取
- **彈性平台** - Google Sheets、OneDrive或SharePoint
- **API存取** — 程式化提交功能
- **企業安全性** — 具有存取控制項的Adobe管理端點

**準備好開始使用了嗎？**&#x200B;請依照[手動組態](#manual-configuration)指南進行視覺化設定，或跳至[API組態](#api-configuration)進行程式化整合。
