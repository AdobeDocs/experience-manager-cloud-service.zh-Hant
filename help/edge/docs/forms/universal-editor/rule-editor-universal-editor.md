---
title: 通用編輯器中的動態表單規則編輯器
description: 在通用編輯器中使用規則編輯器建立動態的智慧型表單。無需編寫程式碼即可新增條件式邏輯、計算和互動式行為。
feature: Edge Delivery Services
role: Admin, Architect, Developer
level: Intermediate
exl-id: 846f56e1-3a98-4a69-b4f7-40ec99ceb348
source-git-commit: 03e46bb43e684a6b7057045cf298f40f9f1fe622
workflow-type: tm+mt
source-wordcount: '2781'
ht-degree: 4%

---


# 通用編輯器中的動態表單規則編輯器

規則編輯器可讓作者將靜態表單轉換為回應式智慧型體驗，而不需撰寫程式碼。 您可以有條件地顯示欄位、執行計算、驗證資料、引導使用者完成流程，以及整合隨人員型別而適應的商業邏輯。

## 您將瞭解的內容

在本指南結束時，您將能夠：

- 了解規則如何運作以及何時使用不同類型的規則
- 在通用編輯器中啟用及存取規則編輯器
- 建立條件式邏輯以動態顯示或隱藏欄位
- 實施自動計算和資料驗證
- 為複雜的業務規則建置自訂函數
- 將最佳實務應用於效能、可維護性和UX

## 為何使用規則編輯器？

- **條件式邏輯**：只有在需要減少雜訊和認知負載時，才顯示相關欄位。
- **動態計算**：根據使用者型別自動計算值（總計、費率、稅捐）。
- **資料驗證**：透過即時檢查及清除訊息，提前避免錯誤。
- **引導式體驗**：引導使用者完成邏輯步驟（精靈、分支）。
- **無程式碼編寫**：透過視覺化介面設定強大的行為。

常見案例包括稅捐電腦、貸款和保費估算、適用流程、多步驟應用程式以及有條件問題的調查。

## 規則如何運作

規則會定義當滿足條件時會發生什麼情況。 從概念上講，規則有兩個部分：

- **條件**：評估為true或false的陳述式。
   - 範例：「收入> 50,000」、「涵蓋範圍= &#39;是&#39;」、「欄位空白」
- **動作**：當條件為True時會發生什麼事（或者當條件為False時會發生什麼事）。
   - 範例：顯示/隱藏欄位、設定/清除值、驗證輸入、啟用/停用按鈕

+++ 規則邏輯模式

- **條件→動作(When/Then)**

  ```text
  WHEN Gross Salary > 50000
  THEN Show "Additional Deduction"
  ```

  最適合條件式可見度與漸進式公開。

- **動作←條件（設定為If/Only If）**

  ```text
  SET Taxable Income = Gross Salary - Deductions
  IF Deductions are applicable
  ```

  最適合用於計算和資料轉換。

- **If → Then → Else （替代動作）**

  ```text
  IF Income > 50000
  THEN Show "High Income" fields
  ELSE Show "Standard Income" fields
  ```

  最適合分支邏輯和互斥流程。

+++

+++ 真實世界的範例

- **條件**：「總薪資超過 50,000 美元」
- **主要動作**：顯示「額外扣除」
- **替代動作**：隱藏[額外扣除]
- **結果**：使用者只會看到套用至他們的欄位

+++

## 先決條件


+++ 存取需求

**基本許可權和設定**：

- **AEM as a Cloud Service**：具有表單編輯許可權的編寫存取權
- **通用編輯器**：已在您的環境中安裝及設定
- **規則編輯器延伸模組**：已透過[Extension Manager](/help/implementing/developing/extending/extension-manager.md)啟用
- **表單編輯許可權**：可在通用編輯器中建立和修改表單元件

**驗證步驟**：

1. 確認您可以從AEM Sites主控台存取通用編輯器
2. 確認您可以建立及編輯表單元件
3. 選取表單元件時，請檢查是否顯示規則編輯器圖示![edit-rules](/help/forms/assets/edit-rules-icon.svg)

+++

+++ 技術需求

**必要的知識和技能**：

- **通用編輯器熟練程度**：使用文字輸入、下拉式清單及基本欄位屬性來建立表單的體驗
- **商業邏輯瞭解**：可針對您的特定使用案例定義條件式需求和驗證規則
- **表單元件熟悉度**：欄位型別（文字、數字、下拉式清單）、屬性（必要、可見、唯讀）和表單結構的知識

**進階使用方式為選用**：

- **JavaScript基礎知識**：只有建立自訂函式（資料型別、函式、基本語法）時才需要
- **JSON瞭解**：有助於複雜的資料操作和API整合

**評估問題**：

- 您可以在通用編輯器中建立包含文字輸入和提交按鈕的基本表單嗎？
- 您是否瞭解在您的業務內容中，何時欄位是必填欄位還是選用欄位？
- 您是否能找出在您的使用案例中哪些表單元素需要條件式可見度？

+++

+++ 啟用規則編輯器擴充功能

**重要**：在通用編輯器環境中，預設不會啟用規則編輯器延伸模組。

**啟動步驟**：

1. 導覽至您AEM環境中的[Extension Manager](/help/implementing/developing/extending/extension-manager.md)
2. 在可用的擴充功能清單中找到「規則編輯器」擴充功能
3. 按一下&#x200B;**啟用**&#x200B;並確認啟用
4. 等待系統重新整理（可能需要1-2分鐘）

**驗證**：

- 啟用後，當您選取表單元件時，規則編輯器圖示會出現： ![edit-rules](/help/forms/assets/edit-rules-icon.svg)

![通用編輯器規則編輯器](/help/edge/docs/forms/assets/universal-editor-rule-editor.png)
圖：選取表單元件時，會出現規則編輯器圖示

若要開啟規則編輯器：

1. 在通用編輯器中選取表單元件。
2. 按一下「規則編輯器」圖示。
3. 「規則編輯器」會在側面板中開啟。

![規則編輯器使用者介面](/help/edge/docs/forms/assets/rule-editor-for-field.png)
圖：用於編輯元件規則的規則編輯器介面

>[!NOTE]
>
> 在本文中，「表單元件」和「表單元件」是指相同的元素（例如輸入、按鈕、面板）。

## 規則編輯器介面概觀

![規則編輯器使用者介面](/help/edge/docs/forms/assets/rule-editor-interface.png)
圖：具有編號元件的完整規則編輯器介面

- **元件標題和規則型別**：確認選取的元件和作用中的規則型別。
- **表單物件與函式面板**：
   - 表單物件：在規則中參考的欄位和容器的階層檢視
   - 函式：內建數學、字串、日期和驗證協助程式
- **面板切換**：顯示/隱藏物件和函式面板，以增加工作區
- **視覺化規則產生器**：拖放、下拉式驅動規則撰寫器
- **控制項**：完成（儲存）、取消（捨棄）。 儲存之前請務必測試規則。

+++

+++ 管理現有規則

當元件已有規則時，您可以：

- **檢視**：檢視規則摘要和邏輯
- **編輯**：修改條件和動作
- **重新排序**：變更執行順序（由上到下）
- **啟用/停用**：切換測試規則
- **刪除**：安全地移除規則

>[!TIP]
>
> 在一般規則之前放置特定規則。 由上到下執行。

+++

## 可用規則類型

選擇最符合您意圖的規則型別。

+++ 條件式邏輯

- **When**：複雜條件行為的主要規則(條件→動作± Else)
- **隱藏/顯示**：根據條件控制可見性（漸進式公開）
- **啟用/停用**：控制欄位是否為互動式欄位（例如，停用送出，直到必要欄位有效）

+++

+++ 資料操控

- **設定值**：自動填入值（例如，日期、總計、副本）
- **清除**&#x200B;的值：條件變更時移除資料
- **格式**：轉換顯示格式（貨幣、電話、日期），而不變更儲存的值

+++

+++ 驗證

- **驗證**：自訂驗證邏輯，包括跨欄位檢查與商業規則

+++

+++ 計算

- **數學運算式**：即時計算值（總計、稅捐、比率）

+++

+++ 使用者介面

- **設定焦點**：將焦點移至特定欄位（謹慎使用）
- **設定屬性**：動態修改元件屬性（預留位置、選項等）

+++

+++ 表單控制項

- **提交表單**：以程式設計方式提交表單（只有在通過驗證之後）
- **重設表單**：清除並重設為初始狀態（使用前確認）
- **儲存表單**：儲存為草稿以供稍後使用（長表單、多工作階段）

+++

+++ 進階

- **啟動服務**：呼叫外部API/服務（控制碼載入和錯誤）
- **新增/移除執行個體**：管理可重複的區段（例如相依專案、地址）
- **導覽至**：路由至其他表單/頁面（導覽前先保留資料）
- **在面板之間導覽**：控制精靈步驟導覽並略過
- **分派事件**：觸發整合或分析的自訂事件

+++

## 逐步教學課程：建置智慧型稅務電腦

+++ 教學課程概覽

此範例示範條件式可視性和自動計算。

![規則編輯器介面的熒幕擷圖，顯示建立條件式規則，以及表單欄位可見性的When-Then邏輯](/help/edge/docs/forms/assets/rule-editor-1.png)
圖：含智慧型條件欄位的稅捐計算表單

您將建置符合以下條件的表單：

1. 顯示相關欄位，以調整使用者輸入
2. 即時計算值
3. 驗證資料以提高準確性

+++

+++ 表單結構

| 欄位名稱 | 類型 | 用途 | 行為 |
|-------------------------|---------------|--------------------------------|-----------------------------------------|
| 薪資毛額 | 數字輸入 | 使用者的年收入 | 觸發條件式邏輯 |
| 額外扣除 | 數字輸入 | 額外扣除額（如果適用） | 只有在薪資> $50,000時才可見 |
| 應課稅收入 | 數字輸入 | 計算值 | 唯讀，變更時更新 |
| 應付稅金 | 數字輸入 | 計算值 | 唯讀，以固定速率計算 |

+++

+++ 商業邏輯

- **規則1：條件式顯示**

  ```text
  WHEN Gross Salary > 50,000
  THEN Show "Additional Deduction"
  ELSE Hide "Additional Deduction"
  ```

- **規則2：應稅收入計算**

  ```text
  SET Taxable Income = Gross Salary - Additional Deduction
  (Only when Additional Deduction applies)
  ```

- **規則3：應付稅金計算**

  ```text
  SET Tax Payable = Taxable Income × 10%
  (Simplified flat rate)
  ```

+++

+++ 步驟1：建立基礎表單

**目標**：建置具有所有欄位和初始設定的基礎表單。

1. **開啟通用編輯器**：
   - 導覽至AEM Sites主控台，選取您的頁面，按一下&#x200B;**編輯**
   - 確定您已正確設定[通用編輯器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction.html)

2. **依此順序新增表單元件**：
   - 標題(H2)：「稅捐計算表單」
   - 數字輸入：「薪資毛額」（必要：是，預留位置：「輸入年薪」）
   - 數字輸入：「額外扣除」（必要：否，預留位置：「輸入額外扣除」）
   - 數字輸入：「應課稅收入」（唯讀：是）
   - 編號輸入：「應付稅金」（唯讀：是）
   - 提交按鈕：「計算稅捐」

3. **設定初始欄位屬性**：
   - 隱藏「額外扣除」（設定可見：屬性面板中為「否」）
   - 將「應課稅收入」與「應付稅金」設為唯讀：是

![稅捐計算表單的熒幕擷圖，其中包含總薪資、婚姻狀況和受撫養子女的輸入欄位，在套用規則之前先展示表單結構](/help/edge/docs/forms/assets/rule-editor2.png)
圖：配置基本元件的初始表單結構

**查核點**：您應該要有一個表單，其中包含所有必要欄位，其中「額外扣款」是隱藏的，且計算欄位是唯讀的。

+++

+++ 步驟2：新增條件式可見性規則

**目標**：僅在薪資總額超過$50,000時顯示「額外扣減」欄位。

1. **選取[薪資總額]欄位**&#x200B;並按一下[規則編輯器]圖示![edit-rules](/help/forms/assets/edit-rules-icon.svg)
2. **建立新規則**：
   - 按一下「**建立**」
   - 將規則型別從&quot;Set Value Of&quot;變更為&#x200B;**&quot;When&quot;**
3. **設定條件**：
   - 從下拉式清單中選取&#x200B;**&quot;大於&quot;**
   - 在數字欄位中輸入`50000`
4. **設定Then動作**：
   - 從「選取動作」下拉式清單中選擇&#x200B;**「顯示」**
   - 從表單物件拖曳或選取&#x200B;**「額外扣除」**&#x200B;欄位
5. **新增Else動作**：
   - 按一下&#x200B;**「新增其他區段」**
   - 從「選取動作」下拉式清單中選擇&#x200B;**「隱藏」**
   - 選取&#x200B;**「額外扣款」**&#x200B;欄位
6. **儲存規則**：按一下&#x200B;**完成**

>[!NOTE]
>
> 替代方法：您可以直接在「額外扣款」欄位上建立「顯示/隱藏」規則，而不是在「薪資總額」上建立「時間」規則，以取得相同的結果。

+++

+++ 步驟3：新增計算規則

**目標**：根據使用者輸入自動計算「應課稅收入」和「應付稅金」。

**設定應稅收入計算**：

1. **選取[應課稅收入]欄位**&#x200B;並開啟規則編輯器
2. **建立數學運算式**：
   - 按一下&#x200B;**建立**→選取&#x200B;**「數學運算式」**
   - 建置運算式： **薪資總額−額外扣款**
   - 將「薪資毛額」拖曳至第一個欄位
   - 選取&#x200B;**&quot;減號&quot;**&#x200B;運運算元
   - 將「額外扣除」拖曳至第二個欄位
3. **儲存**：按一下&#x200B;**完成**

**設定應付稅金計算**：

1. **選取[應付稅項]欄位**&#x200B;並開啟規則編輯器
2. **建立數學運算式**：
   - 按一下&#x200B;**建立**→選取&#x200B;**「數學運算式」**
   - 建置運算式： **應納稅所得× 10 ÷ 100**
   - 將「應稅收入」拖曳至第一個欄位
   - 選取&#x200B;**「乘以」**&#x200B;運運算元
   - 輸入`10`作為數字
   - 按一下&#x200B;**「延伸運算式」**
   - 選取&#x200B;**除以**&#x200B;運運算元
   - 輸入`100`作為數字
3. **儲存**：按一下&#x200B;**完成**

+++

+++ 步驟4：測試表單

**測試完整流程，以驗證您的實作**：

1. **預覽表單**：按一下通用編輯器中的預覽模式
2. **測試條件式邏輯**：
   - 輸入薪資總額= `30000` →「額外扣款」應保持隱藏
   - 輸入薪資總額= `60000` →應出現「額外扣款」
3. **測試計算**：
   - 如果薪水總額= `60000`，請輸入額外扣款= `5000`
   - 驗證應課稅收入= `55000` (60000 - 5000)
   - 驗證應付稅金= `5500` (55000 × 10%)

![預覽表單](/help/edge/docs/forms/assets/rule-editor-form.png)
圖：已完成的稅捐電腦，包含條件欄位和自動計算

**成功標準**：表單應動態顯示/隱藏欄位，並依據使用者型別即時計算值。


+++

## 進階：自訂函式

若是除了內建功能以外的複雜商業邏輯，您可以建立自訂JavaScript功能，以便順暢地與規則編輯器整合。

+++ 自訂函式的使用時機

**自訂函式的理想案例**：

- **複雜計算**：數學運算式規則中不易表示多步驟計算
- **特定企業驗證**：貴組織或產業專屬的自訂驗證邏輯
- **資料轉換**：格式轉換、字串處理或資料剖析
- **外部整合**：呼叫內部API或協力廠商服務（具有限制）

**自訂函式的優點**：

- **可重複使用**：寫入一次，使用多個表單和規則
- **可維護性**：易於更新和偵錯的集中式邏輯
- **效能**：最佳化的JavaScript執行與複雜規則鏈比較
- **彈性**：處理標準規則未處理的邊緣案例和複雜案例

+++

+++ 建立及實作自訂函式

**檔案位置**：所有自訂函式都必須在Edge Delivery Services專案的`/blocks/form/functions.js`中定義。

**開發工作流程**：

1. **函式設計**
   - 使用描述性、動作導向的函式名稱
   - 定義清除引數型別和傳回值
   - 妥善處理邊緣案例和無效的輸入

2. **實作**
   - 撰寫簡潔、評論良好的JavaScript
   - 包含輸入驗證和錯誤處理
   - 整合前需獨立測試功能

3. **文件**
   - 新增完整的JSDoc註解
   - 包含使用範例和引數說明
   - 記錄任何限制或相依性

4. **部署**
   - 使用具名匯出功能的匯出函式
   - 部署至您的專案存放庫
   - 測試前請先驗證建置完成

**實作範例**：

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

![正在新增自訂函式](/help/edge/docs/forms/assets/create-custom-function.png)
圖：將自訂函式新增至functions.js檔案

+++

+++ 在規則編輯器中使用自訂函式

**整合步驟**：

1. **新增函式至專案**
   - 在您的專案中建立或編輯`/blocks/form/functions.js`
   - 在匯出陳述式中包含您的函式

2. **部署並建置**
   - 認可對存放庫的變更
   - 確保建置流程成功完成
   - 允許CDN快取更新的時間

3. 在規則編輯器中&#x200B;**存取權**
   - 開啟任何表單元件的規則編輯器
   - 在&#x200B;**選取動作**&#x200B;下拉式清單中選取&#x200B;**「函式輸出」**
   - 從可用函式清單中選擇自訂函式
   - 使用表單欄位或靜態值設定函式引數

4. **徹底測試**
   - 預覽表單以驗證函式行為
   - 使用包括邊緣案例的各種輸入組合進行測試
   - 驗證對表單載入和互動的效能影響

規則編輯器中的![自訂函式](/help/edge/docs/forms/assets/custom-function-rule-editor.png)
圖：在規則編輯器介面中選取和設定自訂函式


**函式使用方式的最佳實務**：

- **錯誤處理**：一律包含函式失敗的遞補行為
- **效能**：設定檔功能與真實資料量
- **安全性**：驗證所有輸入以防止安全漏洞
- **測試**：建立涵蓋一般和邊緣案例的測試案例

+++


### 自訂函式的靜態匯入

Universal Editor的規則編輯器支援靜態匯入，可讓您在多個檔案和表單中組織可重複使用的邏輯。 您可以匯入其他模組的函式，而不必將所有自訂函式放在單一檔案(/blocks/form/functions.js)中。
例如：從外部檔案匯入函式
考量下列檔案夾結構：

```
      form
      ┣ commonLib
      ┃ ┗ functions.js
      ┣ rules
      ┃ ┗ _form.json
      ┣ form.js
      ┗ functions.js
```

您可以從`commonLib/functions.js`將函式匯入您的主要`functions.js`檔案，如下所示：

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

### 組織不同Forms的自訂函式

您可以在不同的檔案或資料夾中建立不同的功能集，並視需要匯出：

- 如果您希望特定函式僅能用於特定表單，則可以在表單設定中提供函式檔案的路徑。

- 如果路徑的文字方塊留空，則規則編輯器預設為從`/blocks/form/functions.js`載入函式

UE![中的](/help/forms/assets/custom-function-in-ue.png){width=50%}自訂函式

在上面的熒幕擷圖中，自訂函式的路徑已新增到自訂函式路徑文字方塊中。 此表單的自訂函式是從指定的檔案(`cc_function.js`)載入。

這可讓多個表單中共用功能或每個表單都保持隔離狀態，進而提供彈性。

## 規則開發的最佳實務


+++ 效能最佳化

- 將規則複雜度降至最低；將大型邏輯分割為小型、重點明確的規則
- 依頻率排序規則（最常見的為前）
- 讓每個元件的規則集保持在可管理狀態
- 偏好可重複使用的自訂函式，而非複製邏輯

+++

+++ 使用者體驗

- 提供清晰的驗證和內嵌意見反應
- 避免不一致的視覺變化；周詳地使用顯示/隱藏
- 跨裝置和版面進行測試

+++

+++ 開發衛生

- 使用邊緣案例和已知值進行測試
- 跨瀏覽器驗證
- 複雜規則背後的檔案意圖，而不只是力學
- 維護大型表單的規則詳細目錄
- 對元件和規則使用一致的命名
- 在非生產環境中執行版本自訂函式和測試

+++

## 常見問題疑難排解


+++ 未觸發規則

- 驗證元件名稱和參照
- 檢查執行順序（由上到下）
- 使用已知值驗證條件
- 檢查瀏覽器主控台是否有封鎖錯誤

+++

+++ 錯誤行為

- 檢閱運運算元與群組（與/或）
- 個別測試運算式片段
- 確認資料型別（數字與字串）

+++

+++ 效能問題

- 簡化深度巢狀條件
- 設定檔自訂函式
- 將規則內的外部呼叫最小化
- 使用特定的選取器和參照

+++

+++ 自訂函式問題

- 確認檔案路徑： `/blocks/form/functions.js`
- 確定已命名的匯出正確
- 確認組建包含您的變更
- 部署後清除瀏覽器快取
- 驗證引數型別和錯誤處理

+++

+++ 通用編輯器整合

- 確認已啟用規則編輯器擴充功能
- 選取支援的元件
- 使用支援的瀏覽器(Chrome、Firefox、Safari)
- 確認您擁有必要的許可權

## 重要限制

>[!IMPORTANT]
>
> 自訂函式限制：
>
> - 不支援靜態/動態匯入
> - 所有邏輯都必須位於`/blocks/form/functions.js`
> - 函式必須是同步的（無非同步/等待或Promise）
> - 瀏覽器API存取權有限

>[!WARNING]
>
> 生產考量事項：
>
> - 在中繼環境中徹底測試
> - 監視部署後的效能
> - 制定規則問題的復原計畫
> - 考慮低速網路和低規格裝置

## 摘要

Universal Editor中的規則編輯器將靜態表單轉換為智慧型、回應式體驗，可即時因應使用者的輸入內容。 運用條件式邏輯、自動化計算及自訂商業規則，您無需撰寫應用程式程式碼即可建立複雜的表單工作流程。

**您已學到的關鍵功能**：

- **條件式邏輯**：根據使用者輸入顯示和隱藏欄位，以建立集中、相關的體驗
- **動態計算**：當使用者與表單互動時，自動計算值（稅捐、總計、稅率）
- **資料驗證**：透過清晰、可操作的意見反應訊息實作即時驗證
- **自訂函式**：使用JavaScript擴充功能以進行複雜的商業邏輯和整合
- **效能最佳化**：套用可維護、有效率規則開發的最佳實務

**已傳遞值**：

- **增強的使用者體驗**：透過漸進式公開和智慧型表單流程，減少認知負擔
- **減少錯誤**：透過即時驗證和引導式輸入，防止無效的提交
- **提高效率**：自動計算及資料輸入，將使用者工作量降至最低
- **可維護的解決方案**：建立可在整個組織內擴充的可重複使用、完整記錄的規則

**業務影響**：

Forms成為資料收集、潛在客戶資格和使用者參與的強大工具。 規則編輯器可讓非技術作者實作複雜的商業邏輯，降低開發成本，同時提高表單完成率和資料品質。

+++

## 後續步驟

**建議的學習路徑**：

1. **從基本概念開始**：建立簡單的顯示/隱藏規則以瞭解核心概念
2. **使用教學課程實作**：使用稅捐計算器範例作為您自己表單的基礎
3. **逐步展開**：隨著您信賴度的增加，新增數學運算式和驗證規則
4. **實作自訂函式**：針對特殊的業務需求開發JavaScript函式
5. **最佳化及擴充**：套用效能最佳實務並維護規則檔案

**其他資源**：

- [通用編輯器檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction.html)，用於更廣泛的內容
- [Extension Manager指南](/help/implementing/developing/extending/extension-manager.md)啟用其他功能
- [Edge Delivery Services表單](/help/edge/docs/forms/overview.md)，以取得完整的表單開發指引

