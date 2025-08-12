---
title: 如何預先填寫最適化表單欄位
description: 使用現有資料預先填寫最適化表單的欄位。 使用者可以使用其社交設定檔登入，以在表單中預先填入基本資訊。
feature: Adaptive Forms, Edge Delivery Services
role: User, Developer
level: Beginner, Intermediate
time: 45-60 minutes
keywords: 預填最適化表單、最適化表單邊緣交付服務、最適化表單自動填入
exl-id: 7b6224e2-a19c-4146-8545-0ce9d1da9b29
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '1787'
ht-degree: 3%

---

# 使用Edge Delivery Services在最適化Forms中設定預填服務

表單預填是當使用者開啟表單時，自動以外部來源的相關資料填入表單欄位的程式。 透過利用使用者設定檔、資料庫、已儲存草稿或其他後端系統的資訊，預先填寫可簡化表單填寫體驗 — 減少手動輸入、將錯誤降至最低並加快完成。 這不僅會提高使用者滿意度，也會增加成功提交表單的可能性。

## 表單預先填寫的優點

| 優點 | 說明 |
|---------|-------------|
| **更快完成** | 減少手動資料輸入，協助使用者快速完成表格 |
| **改善的使用者體驗** | Forms提供更個人化且便利的使用體驗，尤其是對於回頭的使用者而言 |
| **較高的轉換率** | 儘可能減少使用者所需的工作，減少表單放棄率 |
| **減少輸入錯誤** | 來自受信任來源的資料可減少拼寫錯誤和不正確輸入項 |
| **更好的資料品質** | 確保後端系統的資料結構化、正確且一致 |

## 預填的運作方式

下圖說明使用者開啟調適型表單時發生的自動預填程式：

![表單預填程式流程](/help/edge/docs/forms/universal-editor/assets/prefill-process-flow.svg)

預填程式包含四個關鍵步驟：

1. **使用者開啟表單**：使用者透過URL或導覽存取最適化表單
1. **識別資料Source**：預填服務決定已設定的資料來源（表單資料模型或草稿服務）
1. **擷取資料**：系統根據內容、引數或使用者識別擷取相關的使用者資料
1. **對應並顯示**：資料已使用`bindRef`屬性對應至表單欄位，且已填入的表單已顯示給使用者

此自動化程式可確保使用者看到已預先填入其相關資訊的表單，大幅改善使用者體驗和表單完成率。

## 預填的資料結構

最適化Forms支援兩種欄位型別：

- **繫結欄位**：連結至資料來源的欄位具有非空白的`bindRef`屬性
- **未繫結欄位**：具有空白`bindRef`值的獨立欄位

預填資料結構包括：

- **afBoundData**：包含繫結欄位和面板的資料
- **afUnBoundData**：包含未繫結欄位的資料

資料格式必須符合您的表單模式：

- **XFA表單**：符合XFA範本結構描述的XML
- **XML結構描述表單**： XML符合結構描述結構
- **JSON結構描述表單**： JSON符合結構描述
- **表單資料模型(FDM)表單**： JSON符合FDM結構
- **無結構描述表單**：所有欄位都已解除繫結，並使用未繫結的XML

## 先決條件

在設定預填服務之前，請確定您擁有：

### 必要設定

- [為Edge Delivery Services設定的GitHub存放庫](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)
- [最適化Forms區塊已新增至您的專案](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project)
- [已設定的資料來源](/help/forms/configure-data-sources.md)
- [已建立表單資料模型(FDM)](/help/forms/create-form-data-models.md)

### 存取需求

- 存取AEM Forms as a Cloud Service
- 建立和編輯表單的許可權
- 已啟用必要擴充功能的通用編輯器存取

>[!TIP]
>
> 您也可以編輯表單，以在Universal Editor中整合表單資料模型(FDM)，從各種後端來源擷取資料。 如需詳細資訊，請參閱[將表單與通用編輯器中的表單資料模型整合](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md)文章。

## 預填服務選項

Universal Editor提供兩種預填服務選項：

| 服務類型 | 用途 | 資料來源 | 最適合 |
|--------------|---------|-------------|----------|
| **表單入口網站草稿預填** | 繼續部分完成的表單 | Forms Portal中已儲存的草稿 | 繼續未完成的應用程式 |
| **表單資料模型預填** | 從外部系統填入欄位 | 透過FDM的後端資料庫 | 自動填寫使用者設定檔資料 |

### 詳細比較

| 功能 | 草稿預填服務 | FDM預填服務 |
|---------|----------------------|---------------------|
| **驗證** | 草稿存取需要使用者登入 | 可根據資料來源設定 |
| **設定複雜性** | 最低設定 | 需要FDM設定與對應 |
| **資料型別** | 靜態儲存的資料 | 即時動態資料 |
| **使用案例** | 繼續已儲存的應用程式 | 從使用者設定檔或資料庫預先填入 |


## 設定表單的預填服務

+++第1階段：設定表單資料模型

### 步驟1：建立表單資料模型

1. 登入您的AEM Forms as a Cloud Service執行個體
1. 導覽至&#x200B;**Adobe Experience Manager** > **Forms** > **資料整合**
1. 選取&#x200B;**建立** > **表單資料模型**
1. 選擇您的&#x200B;**資料Source設定**，然後選取已設定的&#x200B;**資料Source**

   ![已建立的表單資料模型](/help/edge/docs/forms/universal-editor/assets/create-fdm.png)

   >[!TIP]
   >
   >如需建立表單資料模型的詳細指示，請參閱[建立表單資料模型](/help/forms/create-form-data-models.md)。

### 步驟2：設定FDM服務

1. 移至&#x200B;**Adobe Experience Manager** > **Forms** > **資料整合**
1. 在編輯模式中開啟您的表單資料模型
1. 選取資料模型物件並按一下&#x200B;**編輯屬性**
1. 為選取的資料模型物件設定&#x200B;**讀取**&#x200B;和&#x200B;**寫入**&#x200B;服務

   ![設定讀寫服務](/help/edge/docs/forms/universal-editor/assets/configure-reda-write-service.png)

1. 設定服務引數：

   - 按一下讀取服務引數的編輯圖示
   - 將引數繫結至&#x200B;**使用者設定檔屬性**、**要求屬性**&#x200B;或&#x200B;**常值值**
   - 指定繫結值（例如pet登錄檔單的`petid`）

   ![設定pet id引數](/help/edge/docs/forms/universal-editor/assets/pet-id-arguments.png)

1. 按一下&#x200B;**完成**&#x200B;以儲存引數，並按一下&#x200B;**儲存**&#x200B;以儲存FDM

   >[!NOTE]
   >
   > 深入瞭解如何在[使用表單資料模型(FDM)](/help/forms/work-with-form-data-model.md)中設定FDM服務。

+++

+++第2階段：建立和設定最適化表單

### 步驟3：建立最適化表單

1. 導覽至&#x200B;**Adobe Experience Manager** > **Forms** > **Forms與檔案**
1. 選取&#x200B;**建立** > **最適化Forms**
1. 在&#x200B;**Source**&#x200B;索引標籤中，選取Edge Delivery Services範本：

   ![Edge Delivery Services 範本](/help/edge/assets/create-eds-forms.png)

1. 按一下&#x200B;**建立**&#x200B;以開啟&#x200B;**建立表單**&#x200B;精靈
1. 指定表單詳細資料：

   - **名稱**：為您的表單輸入描述性名稱
   - **標題**：提供使用者易記的標題
   - **GitHub URL**：輸入您的存放庫URL （例如，`https://github.com/wkndforms/edsforms`）

1. 按一下「**建立**」。

   ![建立綱要型表單](/help/edge/docs/forms/universal-editor/assets/create-schema-based-form1.png)

表單會在通用編輯器中開啟以供製作。

### 步驟4：設定表單資料Source

1. 選取您的表單並按一下&#x200B;**屬性**

   ![選取表單屬性](/help/edge/docs/forms/universal-editor/assets/select-form-properties1.png)

2. 開啟&#x200B;**表單模型**&#x200B;標籤
3. 從&#x200B;**從**&#x200B;選取下拉式清單中選擇&#x200B;**表單資料模型(FDM)**
4. 從下拉式清單中選取您建立的表單資料模型（例如PetFDM）

   ![選取表單模型標籤](/help/edge/docs/forms/universal-editor/assets/select-form-model1.png)

5. 按一下&#x200B;**儲存並關閉**
6. 開啟表單以在通用編輯器中編輯

FDM中的表單元素會顯示在&#x200B;**內容瀏覽器**&#x200B;的&#x200B;**資料來源**&#x200B;標籤中。

### 步驟5：新增資料繫結至表單欄位

1. 從&#x200B;**資料來源**&#x200B;索引標籤中選取資料元素
2. 按一下「**新增**」或拖放元素以建置您的表單

   ![通用編輯器的熒幕擷圖顯示結構描述型表單](/help/edge/docs/forms/universal-editor/assets/ue-form.png)

3. 新增資料繫結至表單欄位：

   - 選取表單欄位
   - 在&#x200B;**屬性**&#x200B;面板中，尋找&#x200B;**繫結參考**&#x200B;屬性
   - 選取適當的資料繫結參考

     ![資料繫結](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding1.png)

+++

+++階段3：設定預填服務

### 步驟6：啟用必要的擴充功能

請確定已在通用編輯器中啟用這些擴充功能：

1. **AEM表單屬性延伸**

   - 在通用編輯器中開啟&#x200B;**Extension Manager**
   - 啟用&#x200B;**AEM表單屬性**&#x200B;擴充功能

   ![表單屬性圖示](/help/edge/docs/forms/universal-editor/assets/form-edit-properties.png)

1. **資料Source擴充功能**

   - 如果您沒有看到&#x200B;**資料來源**&#x200B;圖示，請啟用&#x200B;**資料來源**&#x200B;延伸模組

   ![通用編輯器Extension Manager的熒幕擷圖](/help/edge/docs/forms/universal-editor/assets/extension-manager.png)

   >[!TIP]
   >
   > 如需管理擴充功能的詳細指示，請參閱[Extension Manager功能焦點](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)。

### 步驟7：設定預填服務

1. 在通用編輯器中開啟最適化表單
2. 按一下&#x200B;**AEM表單屬性**&#x200B;擴充功能圖示

   ![選取表單屬性圖示](/help/edge/docs/forms/universal-editor/assets/select-fdm-properties-icon.png)

3. 按一下「**預填**」標籤
4. 選取&#x200B;**表單資料模型預填服務**

   ![選取預填服務](/help/edge/docs/forms/universal-editor/assets/select-fdm-prefill.png)

5. 按一下&#x200B;**儲存並關閉**

+++

+++第4階段：測試預填設定

### 步驟8：預覽和測試

1. 移至&#x200B;**Forms** > **Forms和檔案**
2. 選取最適化表單
3. 選擇&#x200B;**預覽為HTML**
4. 將引數附加至URL以測試預先填入：

   https://your-preview-url.com?`<bindreferencefield>`=`<value>`

   **範例：**

   https://your-preview-url.com?petid=12345

   ![預填表單](/help/edge/docs/forms/universal-editor/assets/prefill-form.png)

表單應會根據提供的引數自動填入資料。

+++

## 範例

### 預填資料結構範例

**FDM型表單的JSON範例：**

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

XFA型表單的&#x200B;**XML範例：**

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

### 預填URL範例

下列URL僅供說明用途，無法正常運作。 在測試預填功能時，將主機和引數取代為您自己的環境相關的主機和引數。

**基本預填測試：**

`https://preview.example.com/form.html?userId=12345`

**多重引數測試：**

`https://preview.example.com/form.html?userId=12345&category=premium`


## 疑難排解

+++常見問題與解決方法

| 問題 | 可能的原因 | 解決方案 |
|-------|----------------|----------|
| **表單欄位未預填** | 不正確的`bindRef`值 | 驗證`bindRef`是否完全符合FDM欄位名稱 |
| **資料格式錯誤** | 不相符的資料結構 | 確保預填資料符合表單模型結構描述 |
| 找不到&#x200B;**服務** | FDM組態問題 | 檢查FDM服務是否已正確設定和儲存 |
| **驗證錯誤** | 資料來源連線能力 | 驗證資料來源憑證和連線能力 |
| **正在載入部分資料** | 缺少欄位對應 | 請確定所有必要欄位都有適當的資料繫結 |

+++

+++偵錯步驟

1. **驗證FDM組態：**

   - 檢查服務是否已正確設定
   - 獨立測試FDM服務
   - 驗證資料來源連線能力

2. **檢查表單設定：**

   - 確認表單與正確的FDM相關聯
   - 驗證欄位`bindRef`值
   - 先測試不含預填的表單

3. **測試資料流程：**

   - 使用瀏覽器開發人員工具來檢查網路要求
   - 檢查JavaScript錯誤的控制檯
   - 驗證回應資料格式

4. **常見錯誤訊息：**

   - 「找不到預填服務」：檢查服務設定
   - 「資料繫結失敗」：驗證`bindRef`準確性
   - 「無效的資料格式」：確保資料符合結構描述

+++

## 最佳實務

+++設定最佳實務

- **使用描述性命名**：清楚地命名您的FDM和服務
- **驗證資料結構描述**：確保資料結構符合表單要求
- **逐步測試**：一次設定並測試一個欄位
- **檔案對應**：追蹤欄位對資料的對應

+++

+++效能最佳化

- **將資料量最小化**：僅預填必要的欄位
- **使用快取**：為經常存取的資料設定適當的快取
- **最佳化查詢**：確保資料庫查詢有效率
- **監視效能**：啟用預填以追蹤表單載入時間

+++

+++安全性考量事項

- **驗證輸入引數**：一律驗證URL引數
- **清理資料**：在預填表單之前清理資料
- **實作存取控制**：確保使用者只能存取自己的資料
- **使用HTTPS**：資料傳輸一律使用安全連線

+++

+++使用者體驗准則

- **提供意見回饋**：在資料擷取期間顯示載入中的指標
- **順利處理錯誤**：顯示有用的錯誤訊息
- **允許覆寫**：讓使用者修改預填的資料
- **維持一致性**：跨表單使用一致的預填行為

+++

## 常見問題

+++如何測試預先填充是否正常運作？

預覽您的表單，並使用以下格式將預填引數附加到URL： `?<bindreferencefield>=<value>`。 確定欄位具有符合您資料結構的有效`bindRef`。 使用瀏覽器開發人員工具來檢查網路要求，並確認資料是否正確擷取。

+++

+++預先填寫最適化Forms支援哪些資料格式？

最適化Forms可支援多種格式（視您的表單模型而定）：

- **XFA表單**：符合XFA結構描述的XML
- **JSON結構描述表單**：符合結構描述的JSON資料
- **FDM表單**：對應到資料模型結構的JSON
- **XML結構描述表單**： XML符合結構描述結構

+++

+++我可以預先填入已繫結和未繫結的欄位嗎？

可以，您可以預先填寫這兩種型別的欄位。 繫結欄位使用`afBoundData`區段，且必須符合您的表單模型結構描述。 未繫結欄位使用`afUnBoundData`區段，可包含任何其他資料。

+++

+++如果只有一些欄位在預先填入，怎麼辦？

檢查所有欄位是否有完全符合您FDM的正確`bindRef`值。 確認您的資料來源包含所有必要欄位，且資料結構與您的表單模式結構描述相符。

+++

+++我可以在一個表單中使用多個預填服務嗎？

您可以為每個表單設定一個主要預填服務。 不過，您可以在單一表單資料模型中結合不同的資料來源，以實現類似的功能。

+++

+++如何處理預填服務的驗證？

驗證取決於您的資料來源設定。 對於以FDM為基礎的預先填入，請在資料來源設定中設定驗證。 對於草稿預填，使用者通常需要登入才能存取其儲存的草稿。

+++



## 相關主題

- [在通用編輯器中整合表單與表單資料模型](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md)
- [建立表單資料模型](/help/forms/create-form-data-models.md)
- [使用表單資料模型(FDM)](/help/forms/work-with-form-data-model.md)
- [設定資料來源](/help/forms/configure-data-sources.md)
- [開始使用適用於AEM Forms的Edge Delivery Services](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
