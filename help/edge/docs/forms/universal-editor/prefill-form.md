---
title: 如何預填自適應表單欄位
description: 使用現有資料預先填入自適應表單的欄位。使用者可以使用其社群設定檔登入，來預先填寫表單中的基本資訊。
feature: Adaptive Forms, Edge Delivery Services
role: User, Developer
level: Beginner, Intermediate
time: 45-60 minutes
keywords: 預填自適應表單, 自適應表單 edge delivery services, 自適應表單自動填入
exl-id: 7b6224e2-a19c-4146-8545-0ce9d1da9b29
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: ht
source-wordcount: '1787'
ht-degree: 100%

---

# 使用 Edge Delivery Services 在自適應表單中設定預填服務

表單預填是指使用者開啟表單時，自動使用來自外部來源的相關資料填入表單欄位的過程。善用來自使用者設定檔、資料庫、已儲存的草稿或其他後端系統的資訊，透過預填簡化表單填寫體驗，減少手動輸入、盡量減少錯誤並加速完成填寫。這不僅提升使用者滿意度，也增加表單提交成功的可能性。

## 預填表單的優點

| 優點 | 說明 |
|---------|-------------|
| **更快完成** | 減少手動輸入資料，幫助使用者快速填寫表單 |
| **改善使用者體驗**。 | 表單變得更加個人化也方便使用，對於回訪使用者來說尤其如此 |
| **更高的轉換率** | 盡量減少使用者需花費的精力，藉此減少放棄表單的情況 |
| **減少輸入錯誤** | 來自可靠來源的資料減少拼字錯誤和錯誤輸入 |
| **更好的資料品質** | 確保為後端系統提供結構化、準確且一致的資料 |

## 預填的運作原理

下圖說明使用者開啟自適應表單時發生的自動預填過程：

![表單預填流程](/help/edge/docs/forms/universal-editor/assets/prefill-process-flow.svg)

預填過程涵蓋四個關鍵步驟：

1. **使用者開啟表單**：使用者透過 URL 或導覽存取自適應表單
1. **確認資料來源**：預填服務會決定所設定的資料來源 (表單資料模型或草稿服務)
1. **檢索資料**：系統根據內容關聯性、參數或使用者身分取得相關使用者資料
1. **對應和顯示**：使用 `bindRef` 屬性將資料對應到表單欄位，並向使用者顯示已填入資料的表單

此自動化流程可確保使用者看到預先填入相關資訊的表單，從而顯著提高使用者體驗和表單完成率。

## 預填的資料結構

自適應表單支援兩種類型的欄位：

- **繫結欄位**：透過非空白 `bindRef` 屬性連接到資料來源的欄位
- **未繫結欄位**：具空白 `bindRef` 值的獨立欄位

預填資料結構包括：

- **afBoundData**：包含繫結欄位和面板的資料
- **afUnBoundData**：包含未繫結欄位的資料

資料格式必須符合您的表單模型：

- **XFA 表單**：符合 XFA 範本結構描述的 XML
- **XML 結構描述表單**：與結構描述結構相符的 XML
- **JSON 結構描述表單**：符合結構描述的 JSON
- **表單資料模型 (FDM) 表單**：與 FDM 結構相符的 JSON
- **無結構描述表單**：所有欄位均未繫結，並使用未繫結的 XML

## 先決條件

在設定預填服務之前，請確保您符合以下條件：

### 必要設定

- [為 Edge Delivery Services 設定 GitHub 存放庫](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)
- [自適應表單區塊已新增至您的專案](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project)
- [資料來源已設定](/help/forms/configure-data-sources.md)
- [已建立表單資料模型 (FDM)](/help/forms/create-form-data-models.md)

### 存取要求

- AEM Forms as a Cloud Service 存取權
- 建立和編輯表單的權限
- 通用編輯器存取權並啟用必要的擴充功能

>[!TIP]
>
> 您也可以在通用編輯器中編輯表單來整合表單資料模型 (FDM)，以便從各種後端來源取得資料。詳細資訊請參閱[在通用編輯器中整合表單與表單資料模型](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md)的文章。

## 預填服務選項

通用編輯器提供兩種預填服務選項：

| 服務類型 | 用途 | 資料來源 | 最適合 |
|--------------|---------|-------------|----------|
| **表單入口網站草稿預填** | 繼續已填寫部分的表單 | 表單入口網站中已儲存的草稿 | 持續未完成的應用程式 |
| **表單資料模型預填** | 從外部系統填入欄位 | 透過 FDM 存取的後端資料庫 | 自動填入使用者設定檔 |

### 詳細比較

| 功能 | 草稿預填服務 | FDM 預填服務 |
|---------|----------------------|---------------------|
| **驗證** | 需要使用者登入才能存取草稿 | 可根據資料來源進行設定 |
| **設定複雜度** | 最低設定 | 需要 FDM 設定和對應 |
| **資料類型** | 靜態的儲存資料 | 即時動態資料 |
| **使用案例** | 繼續已儲存的應用程式 | 從使用者設定檔或資料庫預填 |


## 設定表單的預填服務

+++第 1 階段：設定表單資料模型

### 步驟 1：建立表單資料模型

1. 登入您的 AEM Forms as a Cloud Service 實例
1. 導覽至「**Adobe Experience Manager**」>「**表單**」>「**資料整合**」
1. 選取「**建立**」>「**表單資料模型**」
1. 選擇您的「**資料來源設定**」並選取已設定的「**資料來源**」

   ![已建立表單資料模型](/help/edge/docs/forms/universal-editor/assets/create-fdm.png)

   >[!TIP]
   >
   >有關建立表單資料模型的詳細說明，請參閱 [建立表單資料模型](/help/forms/create-form-data-models.md)。

### 步驟 2：設定 FDM 服務

1. 前往「**Adobe Experience Manager**」>「**表單**」>「**資料整合**」
1. 以編輯模式開啟表單資料模型
1. 選取一個資料模型物件並按一下「**編輯屬性**」
1. 針對所選取資料模型物件設定&#x200B;**閱讀**&#x200B;和&#x200B;**寫入**&#x200B;服務

   ![設定讀寫服務](/help/edge/docs/forms/universal-editor/assets/configure-reda-write-service.png)

1. 設定服務引數：

   - 按一下讀取服務引數的編輯圖示
   - 將引數繫結到「**使用者設定檔屬性**」、「**請求屬性**」或者「**常值**」
   - 指定繫結值 (例如，用於寵物登記表的) `petid`

   ![設定寵物 ID 引數](/help/edge/docs/forms/universal-editor/assets/pet-id-arguments.png)

1. 按一下「**完成**」以儲存引數，並按一下「**儲存**」以儲存 FDM

   >[!NOTE]
   >
   > 參閱[使用表單資料模型 (FDM)](/help/forms/work-with-form-data-model.md)，了解更多關於設定 FDM 服務的詳細資訊。

+++

+++第 2 階段：建立和設定自適應表單

### 步驟 3：建立自適應表單

1. 導覽至「**Adobe Experience Manager**」>「**表單**」>「**表單與文件**」
1. 選取「**建立**」>「**自適應表單**」
1. 在「**來源**」索引標籤中，選取一個 Edge Delivery Services 範本：

   ![Edge Delivery Services 範本](/help/edge/assets/create-eds-forms.png)

1. 按一下「**建立**」來開啟&#x200B;**建立表單**&#x200B;精靈
1. 指定表單詳細資料：

   - **名稱**：輸入表單的說明性名稱
   - **標題**：提供簡單易懂的標題
   - **GitHub URL**：輸入您的存放庫 URL (例如 `https://github.com/wkndforms/edsforms`)

1. 按一下「**建立**」

   ![建立結構描述型表單](/help/edge/docs/forms/universal-editor/assets/create-schema-based-form1.png)

表單會在通用編輯器中開啟以供製作。

### 步驟 4：設定表單資料來源

1. 選取您的表單然後按一下「**屬性**」

   ![選取表單屬性](/help/edge/docs/forms/universal-editor/assets/select-form-properties1.png)

2. 開啟「**表單模型**」標籤
3. 從「**選取來源**」下拉式選單，選擇「**表單資料模型 (FDM)**」
4. 從下拉式選單中選取您建立的表單資料模型 (例如 PetFDM)

   ![選取表單模型標籤](/help/edge/docs/forms/universal-editor/assets/select-form-model1.png)

5. 按一下「**儲存並關閉**」
6. 在通用編輯器中開啟表單進行編輯

FDM 中的表單元素出現在&#x200B;**內容瀏覽器**&#x200B;的「**資料來源**」標籤中。

### 步驟 5：把資料繫結新增到表單欄位

1. 從「**資料來源**」標籤中選取資料元素 
2. 按一下「**新增**」或拖放元素來建置表單

   ![通用編輯器的螢幕擷圖，顯示結構描述型表單](/help/edge/docs/forms/universal-editor/assets/ue-form.png)

3. 新增資料繫結至表單欄位：

   - 選取表單欄位
   - 在「**屬性**」面板中，找到「**繫結參考**」屬性
   - 選取適當的資料繫結參考

     ![資料繫結](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding1.png)

+++

+++第 3 階段：設定預填服務

### 步驟 6：啟用必要的擴充功能

確保在通用編輯器中啟用這些擴充功能：

1. **AEM 表單屬性擴充功能**

   - 在通用編輯器中開啟 **Extension Manager**
   - 啟用 **AEM 表單屬性**&#x200B;擴充功能

   ![表單屬性圖示](/help/edge/docs/forms/universal-editor/assets/form-edit-properties.png)

1. **資料來源擴充功能**

   - 如果您沒有看到「**資料來源**」圖示，請啟用 **資料來源**&#x200B;擴充功能

   ![通用編輯器 Extension Manager 的螢幕擷圖](/help/edge/docs/forms/universal-editor/assets/extension-manager.png)

   >[!TIP]
   >
   > 有關管理擴充功能的詳細說明，請參閱 [Extension Manager 功能重點介紹](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)。

### 步驟 7：設定預填服務

1. 在通用編輯器中開啟您的自適應表單
2. 按一下「**AEM 表單屬性**」擴充功能圖示

   ![選取表單屬性圖示](/help/edge/docs/forms/universal-editor/assets/select-fdm-properties-icon.png)

3. 按一下「**預填**」標籤。
4. 選取&#x200B;**表單資料模型預填服務**

   ![選取預填服務](/help/edge/docs/forms/universal-editor/assets/select-fdm-prefill.png)

5. 按一下「**儲存並關閉**」

+++

+++第 4 階段：測試您的預填設定

### 步驟 8：預覽和測試

1. 前往「**表單**」>「**表單和文件**」
2. 選取您的自適應表單
3. 選擇「**以 HTML 格式預覽**」
4. 將參數附加到 URL 來測試預填：

   https://your-preview-url.com?`<bindreferencefield>`=`<value>`

   **範例：**

   https://your-preview-url.com?petid=12345

   ![預填表單](/help/edge/docs/forms/universal-editor/assets/prefill-form.png)

表單應根據所提供的參數自動填入資料。

+++

## 範例

### 預填資料結構範例

**FDM 型表單的 JSON 範例：**

```
  {
    "afBoundData": {
      "user": {
        "firstName": "John",
        "lastName": "Doe",
        "email": "john.doe@example.com",
        "phone": "+1-555-0123"
      }
    },
    "afUnBoundData": {
      "additionalInfo": "User preferences loaded"
    }
  }
```

**XFA 型表單的 XML 範例：**

```
  <?xml version="1.0" encoding="UTF-8"?>
  <afData>
    <afBoundData>
      <user>
        <firstName>John</firstName>
        <lastName>Doe</lastName>
        <email>john.doe@example.com</email>
      </user>
    </afBoundData>
  </afData>
```

### 預填 URL 範例

以下 URL 僅為舉例示意，無法按原樣運作。測試預填功能時，請更換成與您自己的環境相關的主機和參數。

**基本預填測試：**

`https://preview.example.com/form.html?userId=12345`

**多參數測試：**

`https://preview.example.com/form.html?userId=12345&category=premium`


## 疑難排解

+++常見問題和解決方案

| 問題 | 可能的原因 | 解決方案 |
|-------|----------------|----------|
| **表單欄位未預填** | 錯誤 `bindRef` 值 | 確認 `bindRef` 是否與 FDM 欄位名稱完全相符 |
| **資料格式錯誤** | 資料結構不相符 | 確保預填資料與表單模型結構描述相符 |
| **找不到服務** | FDM 設定問題 | 檢查 FDM 服務是否已正確設定並儲存 |
| **驗證錯誤** | 資料來源連接 | 驗證資料來源認證和連接 |
| **部分資料載入** | 缺少欄位對應 | 確保所有必填欄位都有正確的資料繫結 |

+++

+++偵錯步驟

1. **驗證 FDM 設定：**

   - 檢查服務設定是否正確
   - 獨立測試 FDM 服務
   - 驗證資料來源連接

2. **檢查表單設定：**

   - 確認表單與正確的 FDM 關聯
   - 確認欄位 `bindRef` 的值
   - 在不先預填的情況下測試表單

3. **測試資料流程：**

   - 使用瀏覽器開發者工具來檢查網路請求
   - 檢查控制台是否存在 JavaScript 錯誤
   - 驗證回應式資料格式

4. **常見錯誤訊息：**

   - 「未找到預填服務」：檢查服務設定
   - 「資料繫結失敗」：驗證 `bindRef` 準確性
   - 「無效資料格式」：確保資料與結構描述相符

+++

## 最佳做法

+++設定最佳做法

- **使用說明性命名**：清楚地命名您的 FDM 和服務
- **驗證資料結構描述**：確保資料結構符合表單要求
- **漸進式測試**：一次設定並測試一個欄位
- **文件對應**：持續追蹤欄位到資料的對應

+++

+++效能最佳化

- **盡量減少資料量**：僅預填必要欄位
- **使用快取**：為頻繁存取的資料設定適當的快取
- **最佳化查詢**：確保資料庫查詢有效率
- **監視效能**：在啟用預填的情況下追蹤表單載入時間

+++

+++安全性考量

- **驗證輸入參數**：持續驗證 URL 參數
- **清理資料**：在預填表單之前清理資料
- **實施存取控制**：確保使用者只能存取自己的資料
- **使用 HTTPS**：始終使用安全連線進行資料傳輸

+++

+++使用者體驗準則

- **提供回饋**：在資料擷取期間顯示載入指示器
- **妥善地處理錯誤**：顯示實用的錯誤訊息
- **允許覆蓋**：允許使用者修改預先填入的資料
- **保持一致性**：在各個表單中使用一致的預填行為

+++

## 常見問題

+++如何測試預填是否正確運作？

預覽您的表單並使用以下格式將預填參數附加到 URL：`?<bindreferencefield>=<value>`。確保該欄位具有與您的資料結構相符的有效 `bindRef`。使用瀏覽器開發工具檢查網路請求並確認是否正確地擷取資料。

+++

+++預填自適應表單支援哪些資料格式？

自適應表單支援多種格式，取決於您的表單模型：

- **XFA 表單**：與 XFA 結構描述相符的 XML
- **JSON 結構描述表單**：符合結構描述的 JSON 資料
- **FDM 表單**：對應到資料模型結構的 JSON
- **XML 結構描述表單**：與結構描述結構相符的 XML

+++

+++我可以預填繫結和未繫結欄位嗎？

是的，您可以預填這兩種類型的欄位。繫結欄位使用 `afBoundData` 區段並且必須符合您的表單模型結構描述。未繫結欄位使用 `afUnBoundData` 區段並且可以包含任何其他資料。

+++

+++如果只有預填部分欄位，我要怎麼做？

檢查所有欄位是否都有正確的 `bindRef` 值，與您的 FDM 完全相符。確認您的資料來源包含所有必填欄位，以及資料結構與您的表單模型結構描述相符。

+++

+++我可以在一個表單中使用多個預填服務嗎？

您可以為每個表單設定一個主要預填服務。但是，您可以將不同的資料來源結合在單一表單資料模型中，來實現類似的功能。

+++

+++如何處理預填服務的驗證？

驗證取決於您的資料來源設定。對於以 FDM 為基礎的預填，請在資料來源設定中設定驗證。對於草稿預填，使用者通常需要登入才能存取他們已儲存的草稿。

+++



## 相關主題

- [在通用編輯器中整合表單與表單資料模型](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md)
- [建立表單資料模型](/help/forms/create-form-data-models.md)
- [處理表單資料模型 (FDM)](/help/forms/work-with-form-data-model.md)
- [設定資料來源](/help/forms/configure-data-sources.md)
- [開始使用 AEM Forms 適用的 Edge Delivery Services](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
