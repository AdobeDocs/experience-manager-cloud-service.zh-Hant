---
title: 使用規則為表單新增動態行為
description: AEM Forms 適用的 Edge Delivery Services 專為實現尖峰效能而設計，讓您能夠展望未來簡化資料收集和使用者參與的願景。使用規則為您的表單新增動態行為。
feature: Edge Delivery Services
exl-id: 58042016-e655-446f-a2bf-83f1811525e3
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2218'
ht-degree: 100%

---

# 使用規則為您的表單新增動態行為

使用試算表建立表單的強大功能之一，是能夠使用內建的試算表函數來建立規則，讓您有條件地顯示或隱藏表單欄位、根據使用者輸入自動執行計算，以及建立更機動性的使用者體驗。

本文將引導您了解如何使用各種最適化表單區塊屬性，主要是 [`Visible`](#visible-property)、[`Visibility Expression`](#visible-expression-property) 和 [`Value Expression`](#value-expression-property) 屬性以及[試算表函數](#spreadsheet-functions-for-rules)，為您的表單建立有效的規則。我們也將探討一些範例來說明如何在實務中實施這些規則。

## 了解規則的結構

規則就像指令，告訴我們在不同情況下該怎麼做。規則通常具備以下結構：

- 條件：這些會指定規則適用的情況。可以將這些視為需要回答 (是或否) 的問題。

- 操作：這些是定義當符合 (true) 或不符合 (false) 條件時會發生什麼情況。


例如，當選取核取方塊時，要顯示電子郵件信箱：

- 條件：「您想要訂閱雜誌和活動資訊嗎？」選取核取方塊。(是或否？)。此條件設定在表單的`Visible`屬性中。
- 操作 (true)：顯示電子郵件信箱。(選取「是」發生的情況)。 `Visibility Expression`使用為`visible`屬性定義的條件來動態性地顯示欄位。
- 操作 (false)：隱藏電子郵件信箱被。(選取「否」時發生的情況)。 `Visibility Expression` 使用為`Value`定義的條件來動態性地隱藏欄位。

有關詳細的逐步說明，請參閱[根據條件顯示/隱藏電子郵件欄位](#example-1-conditional-email-field)


## 了解值、可見度、可見度運算式和值運算式屬性

### 可見度屬性

想像一下您的表單欄位有一個電燈開關。`Visible`屬性就像那個開關，可以控制欄位在首次載入時是否在表單上可見到。

- true (冋同電燈開關呈「開啟」狀態 )：表單上會顯示此欄位。
- false (如同電燈開關呈「關閉」狀態)：表單上會隱藏此欄位。

您可以使用試算表公式 (包括 = 標記) 來使用類似試算表的邏輯編寫公式，以此決定欄位的可見度。您可以在此公式中使用表單其他欄位的值。例如，如果使用者在註冊類型欄位中選取「個人」，您可以使用檢查該值的公式隱藏電子郵件欄位。

### 可見度運算式屬性 (顯示/隱藏欄位)

`Visible Expression`屬性可讓您使用新增至`Visible`屬性的規則，以此決定是否根據使用者互動來顯示或隱藏欄位。

使用 `=FORMULATEXT("Address of the corresponding Visible property)` 將`Visible`屬性中提到的公式作為字串帶入`Visible Expression`屬性欄位。這對於在已發佈表單中動態顯示/隱藏欄位是必要的。

![Forumaltext](/help/edge/assets/aem-forms-formulatext.png)

### 值屬性 (設定初始資料)

想像一下房間燈光的調光開關預設值。`Value`屬性類似這個值，可決定使用者在欄位中看到的資料初始狀態。這會設定或擷取表單欄位中目前顯示的資料。

首次載入表單時，`Value`屬性會決定使用者在進行任何變更之前在欄位中看到的內容。與控制可見度的`Visible`和`Visible Expression`屬性不同，值屬性可以直接影響資料本身。使用者可以透過輸入、選取選項 (下拉式選單) 或與欄位互動來修改此值。

您可以使用 Excel 公式 (包括 = 標記) 來使用類似試算表的邏輯編寫公式，以此決定欄位中顯示的值。您可以在此公式中使用表單中其他欄位的值。例如，您可以根據在另一個欄位中輸入的訂單金額自動計算折扣。


### 值運算式屬性 (計算要在欄位中顯示的值)

此屬性可讓您根據公式控制欄位中顯示的值，類似於可見度運算式。想像一下在欄位內建一個計算機。

使用 `=FORMULATEXT("Address of the corresponding Value property)` 將`Value`屬性中提到的公式作為字串帶入`Value Expression`屬性欄位。這對於在已發佈的表單中動態計算和顯示計算值是必要的。

![Forumaltext](/help/edge/assets/aem-forms-formulatext-value.png)

為了使這些概念具體化，我們來看看以下類比：

- 可見度：想像表單是一間房子。「可見度」屬性就像每個房間 (欄位) 的電燈開關。您可以決定當有人進入房子 (開啟表單) 時，房間一開始是亮的 (可見) 還是暗的 (隱藏)。
- 可見度運算式：這就像一個動作感應電燈開關。房間 (欄位) 一開始可能是暗的 (隱藏)，但如果有人走過 (變更另一個欄位中的值)，公式 (動作感應器) 可以將其開啟 (顯示欄位)。
- 值：這就像電燈的預設調光開關 (欄位的初始資料)。使用者接著可以調整亮度 (修改值)。
- 值運算式：這就像是房子 (表單) 中產品價格標籤內建的精美計算器。價格標籤 (欄位) 會根據公式顯示最終價格 (例如，在基本價格加上稅金)，該公式會使用如基本價格的其他資訊 (來自另一個欄位的值)。

透過將這些屬性與[試算表函數](#spreadsheet-functions-for-rules)結合，您可以在表單中實現各種動態行為。

## 適用於規則的試算表函數

最適化 Forms 支援各種可用於建立規則的試算表函數。以下是開箱即用 (OOTB) 的函數：

### 邏輯函數

- [NOT()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#__RefHeading__1018452_715980110)：反轉邏輯狀態 (TRUE 變成 FALSE，反之亦然)。
- [AND()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#AND)：僅當所有指定的條件都為 TRUE 時才傳回 TRUE。
- [OR()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#OR)：當至少其中一個指定的條件為 TRUE，會傳回 TRUE。

### 條件函數

- [IF()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#__RefHeading__1018446_715980110)：運算一個條件，如果為 TRUE，則傳回一個特定值；如果為 FALSE，則傳回另一個值。

### 數學函數

- [SUM()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#SUM)：從指定儲存格範圍內新增值。
- [ROUND()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#ROUND)：將數字四捨五入到指定的小數位數。
- [MIN()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#MIN)：傳回指定儲存格範圍內的最小值。

## 建立規則

讓我們深入研究一些實際範例來說明如何使用規則來增強您的表單：

## 範例 1：有條件的電子郵件欄位

此範例顯示核取方塊如何做為條件。選取時 (條件為 true)，將出現電子郵件信箱 (為 true 時的操作)。未選取時 (條件為 false)，電子郵件信箱將保持隱藏狀態 (為 false 時的操作)。

建立一個內含核取方塊和電子郵件信箱的表單，如下圖所示：

![有條件的電子郵件表單](/help/edge/assets/aem-forms-conditional-email-form.png)


以下是如何使用規則在選取核取方塊時顯示電子郵件欄位：

1. 將核取方塊欄位的`Value`屬性設定為 `TRUE`。
1. 將核取方塊欄位的`Checked`屬性設定為 `FALSE`。這可確保預設不會選取該核取方塊。
1. 將電子郵件欄位的`Visible`屬性設定為 `=[address of Checked property of the checkbox field] = true()`。例如 `=Q11=TRUE()`。無論是否選取核取方塊，公式都會進行運算。如果選取核取方塊，則公式的運算結果為 TRUE。如果未選取核取方塊，則公式的運算結果為 FALSE。



   當您將函數設定為指向`Checked`屬性時，`TRUE()` 函數會傳回邏輯值；如果`checked = false`，則傳回 false。如果 `checked=true`，則傳回 `true`。這可確保電子郵件欄位依預設為隱藏狀態。


1. 將核取方塊欄位的`Visible Expression`屬性設定為 `=FORMULATEXT ((address of Visible property of the checkbox field))`。例如 `=FORMULATEXT((G12))`。FORMULATEXT() 函數會將公式作為輸入，並將公式本身作為文字字串傳回。這有助於使用表單中的公式。

   ![有條件的電子郵件欄位](/help/edge/assets/aem-forms-visible-expression-formula-text.png)

1. 預覽和發佈您的表單。現在，選取核取方塊時會顯示電子郵件欄位，取消選取時會隱藏該欄位，以此提供動態的使用者體驗。

   ![有條件的電子郵件](/help/edge/assets/aem-forms-coditional-email.gif)


## 範例 2：自動計算

此範例顯示表單如何在表單中選取旅行日期時自動計算預估的旅行成本。

建立一個表單，其中包含日期欄位、房間預算、預估的旅行成本欄位 (如下所示) 和電子郵件信箱，如下圖所示：

![有條件的電子郵件表單](/help/edge/assets/aem-forms-automatic-calculations-form.png)

：以下是如何使用執行自動計算來顯示預估的旅行成本

1. 將`amount`欄位的`Value`屬性設定為 `=F6*DAYS(F3,F2)`。此公式會根據 `Start Date`和 `End Date`來計算天數，將天數乘以房間預算，並將結果顯示在`Estimated Trip Cost`欄位。

1. 將`Estimated Trip Cost`欄位的`Value Expression`屬性設定為 `=FORMULATEXT ((address of value property of the amount field))`。例如 `=FORMULATEXT(F7)`。FORMULATEXT() 函數會將公式作為輸入，並將公式本身作為文字字串傳回。這有助於使用表單中的公式。

1. 預覽和發佈您的表單。現在，指定`Start Date`、`End Date` 和房間預算。系統會自動計算 `Estimated Trip Cost`。

## 試算表函數範例


以下是常用試算表函數的一些範例：

**邏輯函數：**

- **NOT()：**&#x200B;反轉邏輯狀態 (TRUE 變成 FALSE，反之亦然)。

  範例：如果電子郵件欄位留空，則隱藏「確認電子郵件」欄位。

   1. 將「確認電子郵件」欄位的`Visible`屬性設定為 `=NOT(if('address of email field'=""))`。

      ![AEM Forms 隱藏確認電子郵件欄位](/help/edge/assets/aem-forms-not-function-hide-email-field.png)


   1. 將「確認電子郵件」欄位的可見度運算式設定為 `=FORMULATEXT ((address of visible property of the Confirm Email field))`

      ![AEM Forms 可見度運算式公式](/help/edge/assets/aem-forms-visible-expression-formula-text.png)


- AND()：僅當所有指定的條件都為 TRUE 時才傳回 TRUE。

   - 範例：僅當所有必填欄位均已填寫時才啟用「提交」按鈕。

   1. 將「提交」按鈕的`Visible`屬性設定為：



      ```JavaScript
      =AND(NOT(address of `value` property of the `name` field = ""), NOT(address of `value` property of the `email` field = ""), NOT(address of `value` property of the `phone` field))
      ```

      例如，

      ```JavaScript
      =AND(NOT(F9=""), NOT(F12=""), NOT(F10=""))
      ```

   1. 將「確認電子郵件」欄位的可見度運算式設定為 

      ```JavaScript
      =FORMULATEXT ((address of visible property of the Confirm Email field))
      ```

      例如，

      ```JavaScript
      =FORMULATEXT(G14)
      ```

      只有當所有欄位 (姓名、電子郵件、電話) 均已填寫 (NOT(()) 對每個欄位傳回 TRUE) 時，此公式才會顯示「提交」按鈕 (TRUE)，否則會隱藏該按鈕 (AND(multiple FALSES) = FALSE)。

- OR()：當至少其中一個指定的條件為 TRUE，就會傳回 TRUE。

   - 例如：如果使用者輸入任何適用的折扣優惠券代碼，則套用折扣。

   1. 將「最終金額」欄位的`Visible`屬性設定為：


  ```JavaScript
     =IF(OR(F14="BlackFridaySale", F14="NewYearDiscount"), (F6*DAYS(F3,F2)* 0.7) , (F6*DAYS(F3,F2)))
  ```

   1. 將「確認電子郵件」欄位的可見度運算式設定為

      ```JavaScript
      =FORMULATEXT ((address of value property of the final amount field))
      ```

      例如，

      ```JavaScript
      =FORMULATEXT(F7)
      ```

      如果使用者輸入優惠券代碼 (couponCode = &quot;NewYearDiscount&quot;) 或 (couponCode = &quot;BlackFridaySale&quot;)，此公式將計算 30% 的折扣，否則將折扣設為 0。

**文字函數：**

- IF()：運算一個條件，如果為 TRUE，則傳回一個特定值；如果為 FALSE，則傳回另一個值。

   - 範例：根據所選產品類別顯示自訂訊息。

   1. 將`message`欄位的`Value`屬性設定為 `Only upto 7 kg check-in lagguage is allowed!`：

   1. 將`message`欄位的`Visible`屬性設定為：


      ```JavaScript
      =if(address of value property of chosen product category ="Economy", TRUE(), FALSE())
      ```

      例如，

      ```JavaScript
      =if(F5="Economy", TRUE(), FALSE())
      ```

   1. 將`message`欄位的值運算式設定為

      ```JavaScript
      =FORMULATEXT ((address of value property of the final amount field))
      ```

      例如，

      ```JavaScript
      =FORMULATEXT(G15)
      ```

      此公式顯示訊息「僅允許托運最多 7 公斤的行李！」如果所選艙位是「經濟艙」，否則訊息欄位將留空。

**數學函數：**

- SUM()：新增指定儲存格範圍內的值。

  範例：計算購物車中商品的總金額。

  「總金額」欄位的值運算式中：
SUM(price * quantity)

  此公式假設每件商品有單獨的「價格」和「數量」欄位。將其相乘並使用 SUM() 將購物車中所有商品的總金額相加。

- ROUND()：將數字四捨五入到指定的小數位數。

  範例：將計算出的折扣金額四捨五入到小數點後兩位。

  在「折扣金額」欄位的值運算式中 (假設在其他地方計算折扣)：
ROUND(discount, 2)

  此公式將折扣值四捨五入至小數點後兩位。

- MIN()：傳回指定儲存格範圍內的最小值。

  範例：根據所選國家/地區尋找註冊表單所要求的最低年齡。

  在「最低年齡」欄位的值運算式中：
MIN(ageLimits[&quot;US&quot;],ageLimits[&quot;UK&quot;],ageLimits[&quot;France&quot;])

  此公式假設您有一個名為「ageLimits&quot;」的表求格，其中儲存不同國家/地區的最低&#x200B;&#x200B;年齡要求。公式會使用 MIN() 來找出其中的最小值。


此外，最適化表單區塊可讓您透過建立 [自訂函數](#creating-custom-functions)來完全掌控表單。自訂函數可讓您定義自己的規則和邏輯，讓您可以完全控制表單的行為。


## 建立和部署自訂函數

開箱即用 (OOTB) 最適化表單區塊提供了許多[常用試算表函數](#spreadsheet-functions-for-rules)的實施。但是，為了對表單進行更精細的控制，您可以在最適化表單區塊中使用 Microsoft® Excel 或 Google 工作表提供的任何 OOTB 函數。最適化表單區塊不包含 Microsoft® Excel 或 Google 工作表所提供全部 OOTB 函數的實施。如果您需要任何此類函數，您可以開發具有類似語法的自訂函數來實施 Microsoft® Excel 或 Google 工作表提供的功能。例如，您可以實施 [Microsoft® Excel&#39;s Year() 函數](https://support.microsoft.com/zh-hant/office/calculate-age-113d599f-5fea-448f-a4c3-268927911b37#)，從出生日期計算年齡。


### 建立自訂函數

自訂函數位於 `[Adaptive form block]/functions.js` 檔案中。建立程序一般包括以下步驟：

- 函數宣告：定義函數名稱及其參數 (其接受的輸入)。
- 邏輯實施：編寫程式碼，概述函數執行的特定計算或操控。
- 函數匯出：從相關檔案匯出函數，使函數在您的規則中可供存取。

### 範例：年份函數

此範例示範了兩個模仿 Microsoft® Excel&#39;s YEAR() 函數來計算年齡的自訂函數：


```JavaScript
/**
 - Get the current date and time
 - @name now
 - @returns {Date} The current date and time as a Date object
 */
function now() {
  const today = new Date();
  return today;
}

/**
 - Get the year from a Date object
 - @name year
 - @param {Date} date The date object
 - @throws {TypeError} If the input is not a Date object
 - @returns {number} The year as a number
 */
function year(date) {
  let inputDate = new Date(date)

  if (!(inputDate instanceof Date)) {
    throw new TypeError("Input must be a Date object");
  }

  const year = inputDate.getFullYear();

  return year;
}

// Make the function accessible for use in rules
export { now, year };
```

### 在表單中使用自訂函數

若要在表單中使用自訂函數：

1. **新增函數**：將您的自訂函數包含在 `[Adaptive form block]/functions.js` 檔案中。請記住將其新增至檔案中的匯出陳述式。
1. **部署檔案**：將更新的 `functions.js` 檔案部署到您的 GitHub 專案並驗證建置是否成功。
1. **函數使用**：使用`Value`、`Value Expression`、`Visible` 或 `Visible Expression` 屬性存取表單試算表中的函數，類似於任何其他支援 OOTB 的試算表函數。
1. **預覽表單**：使用 AEM Sidekick 透過新實施的函數來預覽表單。

