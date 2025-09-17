---
title: Edge Delivery Services Forms的規則編輯器
description: 在通用編輯器中使用規則編輯器建立動態的智慧型表單。無需編寫程式碼即可新增條件式邏輯、計算和互動式行為。
feature: Edge Delivery Services
role: Admin, Architect, Developer
level: Intermediate
exl-id: 846f56e1-3a98-4a69-b4f7-40ec99ceb348
source-git-commit: 0d088d4e3b4e27fac0a05ff93a7fd01535bba6af
workflow-type: tm+mt
source-wordcount: '2824'
ht-degree: 97%

---


# Edge Delivery Services Forms的規則編輯器

規則編輯器可讓作者將靜態表單轉換為回應式智慧型體驗，而不需撰寫程式碼。 您可以依據各種條件來顯示欄位、執行計算、驗證資料、引導使用者完成流程，以及整合會根據人們輸入之內容而調整的商業邏輯。

## 將了解的內容

閱讀完本指南後，您將能夠：

- 了解規則如何運作以及何時使用不同類型的規則
- 在通用編輯器中啟用及存取規則編輯器
- 建立讓欄位動態顯示或隱藏的條件式邏輯
- 實施自動計算和資料驗證
- 為複雜的業務規則建置自訂函數
- 套用效能、可維護性和使用者體驗方面的最佳做法

## 為什麼要使用規則編輯器？

- **條件式邏輯**：僅在需要時顯示相關欄位，減少干擾和認知負荷。
- **動態計算**：在使用者輸入的同時自動計算值 (總計、比率、稅額)。
- **資料驗證**：透過即時檢查和清楚的訊息提早預防錯誤。
- **引導式體驗**：引導使用者完成邏輯化步驟 (精靈、分支)。
- **無程式碼製作**：透過視覺化介面設定功能強大的行為。

常見情境包括稅額計算機、貸款和保費估算器、適用性流程、多步驟申請，以及具有條件式問題的問卷調查。

## 規則如何運作

規則會定義當滿足某個條件時應該發生什麼事。從概念上來說，規則有兩個部分：

- **條件**：一個評估「真」或「假」的陳述式。
   - 範例：「收入 > 50,000」、「承保 = &#39;Yes&#39;」、「欄位為空」
- **動作**：當條件為真時 (以及可選地，當條件為假時) 會發生的情況。
   - 範例：顯示/隱藏欄位、設定/清除值、驗證輸入、啟用/停用按鈕

+++ 規則邏輯模式

- **條件 → 動作 (When/Then)**

  ```text
  WHEN Gross Salary > 50000
  THEN Show "Additional Deduction"
  ```

  最適合條件式可見度和漸進式揭露使用。

- **動作 ← 條件 (Set If/Only if)**

  ```text
  SET Taxable Income = Gross Salary - Deductions
  IF Deductions are applicable
  ```

  最適合計算和資料轉換。

- **If → Then → Else (替代動作)**

  ```text
  IF Income > 50000
  THEN Show "High Income" fields
  ELSE Show "Standard Income" fields
  ```

  最適合分支邏輯和互斥流程。

+++

+++ 真實世界範例

- **條件**：「總薪資超過 50,000 美元」
- **主要動作**：顯示「其他扣除額」
- **替代動作**：隱藏「其他扣除額」
- **結果**：使用者只會看到適用於他們的欄位

+++

## 先決條件


+++ 存取需求

**基本權限和設定**：

- **AEM as a Cloud Service**：具有表單編輯權限的製作存取權
- **通用編輯器**：在您的環境中安裝及設定
- **規則編輯器擴充功能**：透過 [Extension Manager](/help/implementing/developing/extending/extension-manager.md) 啟用
- **表單編輯權限**：能夠在通用編輯器中建立及修改表單元件

**驗證步驟**：

1. 確認您可以從 AEM Sites 控制台存取通用編輯器
2. 驗證您可以建立及編輯表單元件
3. 確認選取表單元件時是否出現規則編輯器圖示![編輯規則](/help/forms/assets/edit-rules-icon.svg)

+++

+++ 技術需求

**必要的知識和技能**：

- **通用編輯器熟練程度**：擁有建立包含文字輸入、下拉式選單和基本欄位屬性之表單的經驗
- **理解商業邏輯**：有能力針對您特定的使用案例定義條件式需求和驗證規則
- **表單元件熟悉度**：了解欄位類型 (文字、數字、下拉式選單)、屬性 (必填、可見、唯讀) 和表單結構

**進階使用可選**：

- **JavaScript 基礎知識**：唯有建立自訂函數 (資料類型、函數、基本語法) 時需要使用
- **理解 JSON**：可協助處理複雜的資料操作和 API 整合

**評估問題**：

- 您可以在通用編輯器中建立包含文字輸入和提交按鈕的基本表單嗎？
- 您是否了解在您的業務環境中，欄位在什麼情況下為必填或選填？
- 您能否在您的使用案例中指出哪些表單元件需要設定條件式可見度？

+++

+++ 啟用規則編輯器擴充功能

**重要**：在通用編輯器環境中並未預設啟用規則編輯器擴充功能。

**啟動步驟**：

1. 導覽至您 AEM 環境中的 [Extension Manager](/help/implementing/developing/extending/extension-manager.md)
2. 在可用擴充功能清單中找到「規則編輯器」擴充功能
3. 按一下「**啟用**」並確認啟用狀態
4. 等待系統重新整理 (可能需要 1 至 2 分鐘)

**驗證**：

- 啟用後，當您選取表單元件時會出現規則編輯器圖示：![編輯規則](/help/forms/assets/edit-rules-icon.svg)

![通用編輯器規則編輯器](/help/edge/docs/forms/assets/universal-editor-rule-editor.png)
圖：選取表單元件時出現規則編輯器圖示

若要開啟規則編輯器：

1. 在通用編輯器中選取一個表單元件。
2. 按一下「規則編輯器」圖示。
3. 規則編輯器會在側面板中開啟。

![規則編輯器使用者介面](/help/edge/docs/forms/assets/rule-editor-for-field.png)
圖：用於編輯元件規則的規則編輯器介面

>[!NOTE]
>
> 在本文中，「表單元件」和「表單物件」是指相同的元素 (例如輸入、按鈕、面板)。

## 規則編輯器介面概觀

![規則編輯器使用者介面](/help/edge/docs/forms/assets/rule-editor-interface.png)
圖：完整的規則編輯器介面，並以數字標註各個元件

1. **元件標題和規則類型**：確認所選元件和使用中的規則類型。
2. **表單物件和函數面板**：

   - 表單物件：欄位和容器的階層視圖，以便在規則中進行參照
   - 函數：內建的數學、字串、日期和驗證輔助函數

3. **面板切換**：顯示/隱藏物件和函數面板，以便增加工作區範圍
4. **視覺化規則產生器**：拖放式、下拉式選單驅動的規則編寫器
5. **控制項**：「完成」(儲存)、「取消」(放棄)。儲存之前務必測試規則。

+++

+++ 管理現有規則

當元件已有規則時，您可以：

- **檢視**：查看規則摘要與邏輯
- **編輯**：修改條件與動作
- **重新排列**：變更執行順序 (從上到下)
- **啟用/停用**：切換測試規則
- **刪除**：安全地移除規則

>[!TIP]
>
> 先設定具體規則，再設定通用規則。從上到下依序執行。

+++

## 可用規則類型

選擇最符合您意圖的規則類型。

+++ 條件式邏輯

- **When (當條件成立時)**：複雜條件式行為的主要規則 (條件 → 動作 ± 否則)
- **隱藏/顯示**：根據條件控制可見度 (漸進式揭露)
- **啟用/停用**：控制是否為互動式欄位 (例如停用提交功能直到必填欄位填入有效內容)

+++

+++ 資料操作

- **設定值**：自動填入值 (例如日期、總計、副本數)
- **清除值**：當條件改變時移除資料
- **格式**：轉換顯示格式 (貨幣、電話、日期) 但不改變已儲存的值

+++

+++ 驗證

- **驗證**：自訂驗證邏輯，包括跨欄位檢查和業務規則

+++

+++ 計算

- **數學運算式**：即時計算值 (總計、稅額、比率)

+++

+++ 使用者介面

- **設定焦點**：將焦點移至特定欄位 (謹慎使用)
- **設定屬性**：動態修改元件屬性 (預留位置、選項等)

+++

+++ 表單控制

- **提交表單**：以程式化方式提交表單 (僅在驗證通過後)
- **重設表單**：清除並重設為初始狀態 (使用前先確認)
- **儲存表單**：儲存為草稿供後續使用 (長表單、多工作階段)

+++

+++ 進階

- **叫用服務**：呼叫外部 API/服務 (處理載入和錯誤)
- **新增/移除執行個體**：管理可重複的區段 (例如受扶養人、地址)
- **導覽至**：路由至其他表單/頁面 (導覽前請保存資料)
- **在面板間導覽**：控制精靈步驟導覽及跳過
- **分派事件**：觸發整合或分析的自訂事件

+++

## 逐步操作教學課程：建置智慧稅額計算機

+++ 教學課程概觀

此範例會示範條件式可見度和自動計算。

![規則編輯器介面的螢幕擷圖，顯示其使用 When-Then 邏輯建立條件式規則，以設定表單欄位可見度](/help/edge/docs/forms/assets/rule-editor-1.png)
圖：具有智慧型條件式欄位的稅務計算表單

您會建置一個具備以下功能的表單：

1. 顯示相關欄位，適應使用者輸入
2. 即時計算值
3. 驗證資料以提高準確性

+++

+++ 表單結構

| 欄位名稱 | 類型 | 用途 | 行為 |
|-------------------------|---------------|--------------------------------|-----------------------------------------|
| 總薪資 | 數字輸入 | 使用者的年收入 | 觸發條件式邏輯 |
| 其他扣除額 | 數字輸入 | 其他扣除額 (如適用) | 僅當薪資高於 50,000 美元時可見 |
| 應稅所得 | 數字輸入 | 計算後的值 | 唯讀，變更時更新 |
| 應繳稅額 | 數字輸入 | 計算後的值 | 唯讀，以固定費率計算 |

+++

+++ 商業邏輯

- **規則 1：條件式顯示**

  ```text
  WHEN Gross Salary > 50,000
  THEN Show "Additional Deduction"
  ELSE Hide "Additional Deduction"
  ```

- **規則 2：應稅所得計算**

  ```text
  SET Taxable Income = Gross Salary - Additional Deduction
  (Only when Additional Deduction applies)
  ```

- **規則 3：應繳稅額計算**

  ```text
  SET Tax Payable = Taxable Income × 10%
  (Simplified flat rate)
  ```

+++

+++ 步驟1：建立表單

**目標**：建置包含所有欄位和初始設定的基礎表單。

1. **開啟通用編輯器**：
   - 導覽至 AEM Sites 控制台，選取您的頁面，然後按一下「**編輯**」
   - 確保您已正確設定[通用編輯器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction.html?lang=zh-Hant)

2. **依下列順序新增表單元件**：
   - 標題 (H2)：「稅額計算表」
   - 數字輸入：「總薪資」(必填：是，預留位置：「輸入年薪」)
   - 數字輸入：「其他扣除額」(必填：否，預留位置：「輸入其他扣除額」)
   - 數字輸入：「應稅所得」(唯讀：是)
   - 數字輸入：「應繳稅額」(唯讀：是)
   - 提交按鈕：「計算稅額」

3. **設定初始欄位屬性**：
   - 隱藏「其他扣除額」(在屬性面板中設定「可見：否」)
   - 將「應稅所得」和「應繳稅額」設定為「唯讀：是」

![稅額計算表單的螢幕擷圖，顯示總薪資、婚姻狀況及受扶養子女的輸入欄位，呈現套用規則前的表單結構](/help/edge/docs/forms/assets/rule-editor2.png)
圖：已設定基本元件的初始表單結構

**查核點**：您應具備一個包含所有必填欄位的表單，其中隱藏「其他扣除額」，且計算後的欄位是唯讀狀態。

+++

+++ 步驟 2：新增條件式可見度規則

**目標**：僅當總薪資超過 50,000 美元時才顯示「其他扣除額」欄位。

1. **選取「總薪資」欄位**，按一下「規則編輯器」圖示![編輯規則](/help/forms/assets/edit-rules-icon.svg)
2. **建立新規則**：
   - 按一下「**建立**」
   - 將規則類型從「設定值」變更為&#x200B;**「When」**
3. **設定條件**：
   - 從下拉式選單中選取&#x200B;**「大於」**
   - 在數字欄位中輸入 `50000`
4. **設定 Then 動作**：
   - 從「選取動作」下拉式選單中選擇「**顯示**」
   - 從表單物件中拖曳或選取「**其他扣除額**」欄位
5. **新增 Else 動作**：
   - 按一下「**新增 Else 區段**」
   - 從「選取動作」下拉式選單中選擇「**隱藏**」
   - 選取「**其他扣除額**」欄位
6. **儲存規則**：按一下「**完成**」

>[!NOTE]
>
> 替代方法：您可以直接在「其他扣除額」欄位上建立顯示/隱藏規則而獲得相同的結果，不用在「總薪資」上使用 When 規則。

+++

+++ 步驟 3：新增計算規則

**目標**：根據使用者輸入自動計算「應稅所得」和「應繳稅額」。

**設定應稅所得計算**：

1. **選取「應稅所得」欄位**，然後開啟規則編輯器
2. **建立數學運算式**：
   - 按一下「**建立**」→ 選取&#x200B;**「數學運算式」**
   - 建置運算式：**總薪資 − 其他扣除額**
   - 將「總薪資」拖到第一個欄位
   - 選取&#x200B;**「減」**&#x200B;運算子
   - 將「其他扣除額」拖到第二個欄位
3. **儲存**：按一下「**完成**」

**設定應繳稅額計算**：

1. **選取「應繳稅額」欄位**，然後開啟規則編輯器
2. **建立數學運算式**：
   - 按一下「**建立**」→ 選取&#x200B;**「數學運算式」**
   - 建置運算式：**應繳稅額 × 10 ÷ 100**
   - 將「應稅所得」拖到第一個欄位
   - 選取&#x200B;**「乘以」**&#x200B;運算子
   - 輸入數字「`10`」
   - 按一下&#x200B;**「擴充運算式」**
   - 選取&#x200B;**「除以」**&#x200B;運算子
   - 輸入數字「`100`」
3. **儲存**：按一下「**完成**」

+++

+++ 步驟 4：測試表單

**測試完整流程來驗證您的實施**：

1. **預覽表單**：在通用編輯器中按一下預覽模式
2. **測試條件式邏輯**：
   - 輸入總薪資 = `30000` →「其他扣除額」應保持隱藏
   - 輸入總薪資 = `60000` →「其他扣除額」應出現
3. **測試計算**：
   - 假設總薪資 = `60000`，輸入其他扣除額 = `5000`
   - 驗證應稅所得 = `55000` (60000 - 5000)
   - 驗證應繳稅額 = `5500` (55000 × 10%)

![預覽表單](/help/edge/docs/forms/assets/rule-editor-form.png)
圖：已完成的稅額計算機，包含條件式欄位和自動計算

**成功標準**：表單應動態顯示/隱藏欄位，並在使用者輸入時即時計算值。


+++

## 進階：自訂函數

對於超出內建功能的複雜商業邏輯，您可以建立與規則編輯器緊密整合的自訂 JavaScript 函數。

+++ 使用自訂函數的時機

**使用自訂函數的理想情境**：

- **複雜計算**：數學運算式規則中不易表達的多步驟運算
- **業務特定的驗證**：您的組織或產業特定的自訂驗證邏輯
- **資料轉換**：格式轉換、字串操作或資料解析
- **外部整合**：呼叫內部 API 或第三方服務 (有限制)

**自訂函數的好處**：

- **可重複使用**：寫入一次，可供多個表單和規則使用
- **便於維護**：容易更新及偵錯的集中式邏輯
- **效能**：JavaScript 執行最佳化，優於複雜的規則鏈
- **靈活性**：能夠處理標準規則無法解決的邊緣案例和複雜情境

+++

+++ 建立和實施自訂函數

**檔案位置**：所有自訂函數的定義必須儲存您的 Edge Delivery Services 專案的 `/blocks/form/functions.js` 中。

**開發工作流程**：

1. **函數設計**
   - 使用描述性、動作導向的函數名稱
   - 定義明確的參數類型和傳回值
   - 妥善處理邊緣案例和無效輸入

2. **實施**
   - 編寫乾淨、註解完好的 JavaScript
   - 包含輸入驗證和錯誤處理
   - 在整合之前先獨立測試函數

3. **文件**
   - 新增全方位的 JSDoc 註解
   - 包含使用範例和參數說明
   - 將所有限制或相依性記錄下來

4. **部署**
   - 使用已命名的匯出將函數匯出
   - 部署至您的專案存放庫
   - 在測試之前先驗證建置完成情況

**實施範例**：

```javascript
/**
 * Concatenates first and last name with proper formatting
 * @name getFullName
 * @description Combines first and last name, handles edge cases like missing values
 * @param {string} firstName - The person's first name
 * @param {string} lastName - The person's last name  
 * @returns {string} Formatted full name or empty string if both inputs are invalid
 */
function getFullName(firstName, lastName) {
  // Handle null, undefined, or empty string inputs
  const first = (firstName || '').toString().trim();
  const last = (lastName || '').toString().trim();
  
  return `${first} ${last}`.trim();
}

/**
 * Calculates the number of days between two dates
 * @name days
 * @description Computes absolute difference in days, handles various date input formats
 * @param {Date|string} endDate - End date (Date object or ISO string)
 * @param {Date|string} startDate - Start date (Date object or ISO string)
 * @returns {number} Number of days between dates, 0 if inputs are invalid
 */
function days(endDate, startDate) {
  // Convert string inputs to Date objects
  const start = typeof startDate === 'string' ? new Date(startDate) : startDate;
  const end = typeof endDate === 'string' ? new Date(endDate) : endDate;

  // Validate date objects
  if (Number.isNaN(start.getTime()) || Number.isNaN(end.getTime())) {
    return 0;
  }

  // Calculate absolute difference in milliseconds, then convert to days
  const diffInMs = Math.abs(end.getTime() - start.getTime());
  return Math.floor(diffInMs / (1000 * 60 * 60 * 24));
}

// Export functions for use in Rule Editor
export { getFullName, days };
```

![新增自訂函數](/help/edge/docs/forms/assets/create-custom-function.png)
圖：在 functions.js 檔案中新增自訂函數

+++

+++ 使用規則編輯器中的自訂函數

**整合步驟**：

1. **在專案中新增函數**
   - 在您的專案中建立或編輯 `/blocks/form/functions.js`
   - 在匯出陳述式中加入您的函數

2. **部署和建置**
   - 將變更提交至存放庫
   - 確保建置過程成功完成
   - 預留內容傳遞網路快取更新的時間

3. **在規則編輯器中存取**
   - 針對任何表單元件開啟規則編輯器
   - 在「**選取動作**」下拉式選單中選取&#x200B;**「函數輸出」**
   - 從可用函數清單中選擇您的自訂函數
   - 使用表單欄位或靜態值設定函數參數

4. **進行全面測試**
   - 預覽表單以驗證函數行為
   - 使用各種輸入組合 (包括邊緣案例) 進行測試
   - 驗證效能對於表單載入和互動的影響

![規則編輯器中的自訂函數](/help/edge/docs/forms/assets/custom-function-rule-editor.png)
圖：在規則編輯器介面中選取及設定自訂函數

>
>
> Edge Delivery Services Forms也提供規則編輯器的增強功能，包括自訂事件型規則、動態變數支援，以及API整合。 若要進一步瞭解這些增強功能及使用方法，請參閱[規則編輯器增強功能和使用案例](/help/forms/rule-editor-enhancements-use-cases.md)文章。

**函數使用的最佳做法**：

- **錯誤處理**：務必要包含函數失敗時的遞補行為
- **效能**：使用實際資料量分析函數效能
- **安全性**：驗證所有輸入，防止安全性漏洞
- **測試**：建立涵蓋正常與邊緣案例的測試案例

+++


### 自訂函數的靜態匯入

通用編輯器的規則編輯器支援靜態匯入，讓您能夠跨多個檔案及表單，組織可重複使用的邏輯。您可以自其他模組匯入函數，而不必將所有自訂函數都保存在單一檔案 (/blocks/form/functions.js) 中。
例如：從外部檔案匯入函數
考慮以下資料夾結構：

```
      form
      ┣ commonLib
      ┃ ┗ functions.js
      ┣ rules
      ┃ ┗ _form.json
      ┣ form.js
      ┗ functions.js
```

您可以將函數從 `commonLib/functions.js` 匯入主要的 `functions.js` 檔案中，如下所示：

```
`import {days} from './commonLib/functions';
/**
 * Get Full Name
 * @name getFullName Concats first name and last name
 * @param {string} firstname in String format
 * @param {string} lastname in String format
 * @return {string}
 */
function getFullName(firstname, lastname) {
  return `${firstname} ${lastname}`.trim();
}

// Export multiple functions for use in Rule Editor
export { getFullName, days};
```

### 跨不同表單組織自訂函數

您可以在個別的檔案或資料夾中建立不同的函數集，並根據需要將其匯出：

- 如果您希望某些函數僅能在特定的表單中使用，可於表單設定中提供函數檔案的路徑。

- 若路徑的文字方塊留空，規則編輯器預設會從 `/blocks/form/functions.js` 匯入函數

![UE 中的自訂函數](/help/forms/assets/custom-function-in-ue.png){width=50%}

於上方的螢幕擷圖中，自訂函數路徑文字方塊內有加入自訂函數的路徑。該表單的自訂函數會從指定檔案 (`cc_function.js`) 載入。

此功能可以在多個表單間共用函數，或於各表單間保持函數隔離，因而帶來靈活性。

## 制訂規則的最佳做法


+++ 效能最佳化

- 盡量降低規則複雜度；將大邏輯分解成小而集中的規則
- 依照頻率對規則進行排序 (最常用的優先)
- 保持每個元件的規則集皆易於管理
- 偏好可重複使用的自訂函數，而非重複的邏輯

+++

+++ 使用者體驗

- 提供清晰的驗證和內聯回饋
- 避免不協調的視覺變化；謹慎使用顯示/隱藏
- 針對各種裝置和版面進行測試

+++

+++ 開發衛生

- 使用邊緣案例和已知規則進行測試
- 針對各種瀏覽器進行驗證
- 記錄複雜規則背後的意圖，而不只是機制
- 維護大型表單的規則清單
- 元件和規則使用一致的命名方式
- 控制自訂函數的版本，並在非生產環境中進行測試

+++

## 常見問題疑難排解


+++ 規則未觸發

- 驗證元件名稱和參照
- 檢查執行順序 (從上到下)
- 使用已知值驗證條件
- 檢查瀏覽器控制台是否有封鎖錯誤

+++

+++ 不正確的行為

- 審閱運算子和分組 (AND/OR)
- 單獨測試運算式片段
- 確認資料類型 (數字與字串)

+++

+++ 效能問題

- 簡化深度巢狀條件
- 設定檔自訂函數
- 盡量減少規則內的外部呼叫
- 使用特定的選擇器和參照

+++

+++ 自訂函數問題

- 確認檔案路徑：`/blocks/form/functions.js`
- 確保已命名的匯出正確無誤
- 確認建置版本包含您的變更
- 部署後清除瀏覽器快取
- 驗證參數類型和錯誤處理

+++

+++ 通用編輯器整合

- 確認規則編輯器擴充功能已啟用
- 選取一個支援的元件
- 使用支援的瀏覽器 (Chrome、Firefox、Safari)
- 驗證您是否具有必要的權限

## 重要限制

>[!IMPORTANT]
>
> 自訂函數限制：
>
> - 不支援靜態/動態匯入
> - 所有邏輯都必須存放在 `/blocks/form/functions.js`
> - 函數必須同步 (不能使用 async/await 或 Promises)
> - 瀏覽器 API 存取受限

>[!WARNING]
>
> 生產考量：
>
> - 於中繼階段進行全面測試
> - 監視部署後的效能
> - 制定規則問題的復原計劃
> - 考慮慢速網路和低規格裝置

## 摘要

通用編輯器中的規則編輯器會將靜態表單轉換為智慧、回應式的體驗，可以即時適應使用者輸入。運用條件式邏輯、自動計算和自訂業務規則，您可以建立複雜的表單工作流程，而不需要編寫應用程式程式碼。

**您已了解的重要功能**：

- **條件式邏輯**：根據使用者輸入顯示和隱藏欄位，以建立重點式、相關的體驗
- **動態計算**：在使用者與表單互動時，自動計算數值 (稅額、總計、比率)
- **資料驗證**：透過清晰、可操作的回饋訊息，實施即時驗證
- **自訂函數**：使用 JavaScript 來擴充功能，以利實現複雜的商業邏輯和整合
- **效能最佳化**：套用最佳做法，實現可維護、有效率的規則開發過程

**所傳遞的價值**：

- **增強使用者體驗**：透過漸進式揭露和智慧表單流程，減輕認知負荷
- **減少錯誤**：透過即時驗證和引導式輸入，防止無效提交
- **提高效率**：自動化計算與資料輸入，盡量減少使用者工作量
- **可維護的解決方案**：建立可重複使用、記錄詳盡，且可擴大適用於整個組織的規則

**業務影響**：

表單成為資料彙集、商機鑑定以及促進使用者參與的強大工具。規則編輯器讓非技術作者能夠實施複雜的商業邏輯，降低開發成本，同時提高表單完成率和資料品質。

+++

## 後續步驟

**建議的學習路徑**：

1. **從基礎開始**：建立簡單的顯示/隱藏規則，以理解核心概念
2. **透過教學課程練習**：使用稅額計算機範例，做為您自己表單的基礎
3. **逐步擴充**：隨著信心的增長，加入數學運算式和驗證規則
4. **實施自訂函數**：針對專門的業務需求開發 JavaScript 函數
5. **最佳化和擴展**：套用效能最佳做法，並維護規則文件

**其他資源**：

- [通用編輯器文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction.html?lang=zh-Hant)提供更多相關內容
- [Extension Manager 指南](/help/implementing/developing/extending/extension-manager.md)，協助啟用更多功能
- [Edge Delivery Services 表單](/help/edge/docs/forms/overview.md)，提供全方位的表單製作指引

