---
title: 使用規則將動態行為新增至表單
description: AEM FormsEdge Delivery Services專為最佳效能而打造，可讓您構想簡化資料收集和使用者參與的未來。 使用規則將動態行為新增至表單。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 58042016-e655-446f-a2bf-83f1811525e3
source-git-commit: 61c8d08a21ad81a74e1093838b38f22af94751c3
workflow-type: tm+mt
source-wordcount: '2216'
ht-degree: 0%

---

# 使用規則將動態行為新增至表單

使用試算表建立表單的強大功能之一，是使用內建試算表函式來建立規則，可讓您有條件地顯示或隱藏表單欄位、根據使用者輸入自動計算並建立更動態的使用者體驗。

本文主要說明如何使用各種最適化表單區塊屬性 [`Visible`](#visible-property)， [`Visibility Expression`](#visible-expression-property) 和 [`Value Expression`](#value-expression-property) 屬性以及 [試算表函式](#spreadsheet-functions-for-rules) 為您的表單建立有效規則。 我們也會探索一些範例，以說明如何在實踐中實作這些規則。

## 瞭解規則的結構

規則就像指示我們在不同情況下應該做什麼的指示。 規則通常具有下列建構：

* 條件：指定套用規則的情況。 將其視為需要回答的問題（是或否）。

* 動作：這些會定義當符合條件(true)或未符合(false)時所發生的情況。


例如，若要顯示電子郵件方塊，在選取核取方塊時：

* 條件： 「您想要訂閱《雜誌與活動》嗎？」 核取方塊已選取。 （是或否？）。 此條件設定於 `Visible` 表單的屬性。
* 動作(True)：顯示電子郵件方塊。 （如果有的話，會發生什麼情況）。 此 `Visibility Expression`  使用為定義的條件 `visible` 屬性以動態顯示欄位。
* 動作(False)：電子郵件方塊為隱藏。 （如果沒有，會發生什麼事）。 此 `Visibility Expression`  使用為定義的條件 `Value` 以動態隱藏欄位。

如需詳細的逐步指示，請參閱 [根據條件顯示/隱藏電子郵件欄位](#example-1-conditional-email-field)


## 瞭解「值」、「可見」、「可見度」運算式和「值」運算式屬性

### 可見屬性

想像一下您的表單欄位有燈光開關。 此 `Visible` 屬性就像該開關，控制欄位在首次載入時是否最初顯示在表單上。

* True （就像燈號開關是「開啟」）：此欄位會顯示在表單上。
* False （就像燈號開關「關閉」一樣）：此欄位在表單上為隱藏狀態。

您可以使用試算表公式（包括=標籤）來撰寫公式，使用類似試算表的邏輯來判斷欄位的可見度。 您可以使用此公式中表單其他欄位的值。 例如，如果使用者在註冊型別欄位中選擇「個人」，您可以使用檢查該值的公式來隱藏電子郵件欄位。

### 可見運算式屬性（顯示/隱藏欄位）

此 `Visible Expression` 屬性可讓您使用新增至的規則 `Visible` 根據使用者互動來決定要顯示或隱藏欄位的屬性。

使用 `=FORMULATEXT("Address of the corresponding Visible property)` 以匯入 `Visible` 作為字串的屬性至 `Visible Expression` 屬性欄位。 若要以動態方式顯示/隱藏已發佈表單中的欄位，必須要有此欄位。

![Forumaltext](/help/edge/assets/aem-forms-formulatext.png)

### 值屬性（設定初始資料）

想像一下，在較暗的交換器上，設定一個房間燈光的預設值。 此 `Value` 屬性類似，可判斷使用者在欄位中看到的資料初始狀態。  它會設定或擷取表單欄位中顯示的目前資料。

首次載入表單時， `Value` 屬性會指定使用者在變更前可在欄位中看到的內容。 取消讚 `Visible` 和 `Visible Expression` 屬性會控制可見性，而Value屬性會直接影響資料本身。 使用者可以透過輸入、選取選項（下拉式選單）或與欄位互動來修改此值。

您可以使用Excel公式（包括=標籤）來撰寫公式，使用類似試算表的邏輯來決定欄位中顯示的值。 您可以使用此公式中表單其他欄位的值。 例如，您可以根據在另一個欄位中輸入的訂單金額，自動計算折扣。


### 值運算式屬性（計算要顯示在欄位中的值）

此屬性可讓您根據公式控制欄位中顯示的值，類似於「可見運算式」。 想像一下此欄位內建的計算器。

使用 `=FORMULATEXT("Address of the corresponding Value property)` 以匯入 `Value` 作為字串的屬性至 `Value Expression` 屬性欄位。 若要在發佈的表單中動態計算並顯示計算值，則需要此專案。

![Forumaltext](/help/edge/assets/aem-forms-formulatext-value.png)

以下是將這些概念固化的類比：

* 可見：想像一個像房子一樣的表單。 「可見」屬性就像每個房間（欄位）的燈光開關。 當有人進入房間時（開啟表單），您可以決定房間最初是亮的（可見）還是暗的（隱藏）。
* 可見運算式：這就像動作感應器燈光開關。 空間（欄位）一開始可能很暗（隱藏），但如果有人走過（變更其他欄位中的值），公式（動作感應器）可以將其開啟（顯示欄位）。
* 值：這就像是為光源預先設定的調光開關（欄位中的初始資料）。 接著，使用者可以調整亮度（修改值）。
* 值運算式：這就像是（表單）中內建在產品價格標籤上的華麗電腦。 價格標籤（欄位）會根據公式（例如，將稅捐新增至基本價格）顯示最終價格，該公式會使用其他資訊，例如基本價格（來自其他欄位的值）。

將這些屬性與 [試算表函式](#spreadsheet-functions-for-rules)，您可以在表單中達成廣泛的動態行為。

## 規則的試算表函式

最適化Forms Block支援多種可用來建立規則的試算表函式。 以下是現成可用的功能(OOTB)：

### 邏輯函式

* [NOT()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#__RefHeading__1018452_715980110)：反轉邏輯狀態（TRUE會變成FALSE，反之亦然）。
* [AND()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#AND)：只有在指定的所有條件皆為TRUE時，才會傳回TRUE。
* [OR()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#OR)：如果至少有一個指定的條件為TRUE，則傳回TRUE。

### 條件函式

* [IF()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#__RefHeading__1018446_715980110)：評估條件並在為TRUE時傳回特定值，若為FALSE時傳回另一個值。

### 數學函式

* [SUM()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#SUM)：新增指定儲存格範圍內的值。
* [ROUND()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#ROUND)：將數字四捨五入至指定的小數位數。
* [MIN()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#MIN)：從指定的儲存格範圍傳回最小值。

## 建立規則

讓我們深入探討幾個實用的範例，說明如何使用規則來增強您的表單：

## 範例1：條件電子郵件欄位

此範例顯示核取方塊作為條件的運作方式。 選取時（條件為true），會出現電子郵件方塊（動作true）。 若未選取（條件為false），則電子郵件方塊會維持隱藏狀態（動作false）。

建立包含核取方塊和電子郵件方塊的表單，如下圖所示：

![條件電子郵件表單](/help/edge/assets/aem-forms-conditional-email-form.png)


以下說明如何透過規則在選取核取方塊時顯示電子郵件欄位：

1. 設定 `Value` 「 」核取方塊欄位的屬性 `TRUE`.
1. 設定 `Checked` 「 」核取方塊欄位的屬性 `FALSE`. 如此可確保在預設情況下不會選取核取方塊。
1. 設定 `Visible` 要傳送的電子郵件欄位的屬性 `=[address of Checked property of the checkbox field] = true()`. 例如 `=Q11=TRUE()`. 公式會評估核取方塊是否選取。 如果選取核取方塊，公式的計算結果為TRUE。 如果未選取核取方塊，公式的計算結果為FALSE。



   此 `TRUE()` 函式中，當您將邏輯值設定為指向時傳回邏輯值 `Checked` 屬性，如果 `checked = false` 它會傳回false。 如果 `checked=true`，它會傳回 `true`. 這可確保預設隱藏電子郵件欄位。


1. 設定 `Visible Expression` 「 」核取方塊欄位的屬性 `=FORMULATEXT ((address of Visible property of the checkbox field))`. 例如 `=FORMULATEXT((G12))`。FORMULATEXT()函式以公式作為輸入，並將公式本身傳回為文字字串。 這有助於在表單中使用公式。

   ![條件電子郵件欄位](/help/edge/assets/aem-forms-visible-expression-formula-text.png)

1. 預覽並發佈您的表單。 現在，勾選核取方塊會顯示電子郵件欄位，但取消勾選時會隱藏欄位，提供動態的使用者體驗。

   ![條件電子郵件](/help/edge/assets/aem-forms-coditional-email.gif)


## 範例2：自動計算

此範例說明在表單中選取運送航程日期時，表單如何自動計算「預估運送航程成本」。

建立包含日期欄位、房間預算、預估運送成本欄位（如下所示）的表單，以及電子郵件方塊（如下所示）：

![條件電子郵件表單](/help/edge/assets/aem-forms-automatic-calculations-form.png)

以下說明如何使用執行自動計算來顯示「預估運送航程成本」：

1. 設定 `Value` 的屬性 `amount` 欄位至 `=F6*DAYS(F3,F2)`. 此公式計算天數 `Start Date`  和 `End Date`，與會議室預算相乘的天數，且顯示結果為 `Estimated Trip Cost` 欄位。

1. 設定 `Value Expression` 的屬性 `Estimated Trip Cost` 欄位至 `=FORMULATEXT ((address of value property of the amount field))`. 例如 `=FORMULATEXT(F7)`。FORMULATEXT()函式以公式作為輸入，並將公式本身傳回為文字字串。 這有助於在表單中使用公式。

1. 預覽並發佈您的表單。 現在，在指定 `Start Date`， `End Date`和會議室預算。 此 `Estimated Trip Cost` 是自動計算的。

## 試算表函式範例


以下是常用試算表函式的一些範例：

**邏輯函式：**

* **NOT()：** 反轉邏輯狀態（TRUE會變成FALSE，反之亦然）。

  範例：如果電子郵件欄位留白，則隱藏「確認電子郵件」欄位。

   1. 設定 `Visible` 「確認電子郵件」欄位的屬性 `=NOT(if('address of email field'=""))`.

      ![AEM Forms隱藏確認電子郵件欄位](/help/edge/assets/aem-forms-not-function-hide-email-field.png)


   1. 將「確認電子郵件」欄位的可見運算式設定為 `=FORMULATEXT ((address of visible property of the Confirm Email field))`

      ![AEM Forms可見運算式公式](/help/edge/assets/aem-forms-visible-expression-formula-text.png)


* AND()：只有在指定的所有條件皆為TRUE時，才會傳回TRUE。

   * 範例：僅在填寫所有必填欄位時啟用「提交」按鈕。

   1. 設定 `Visible` 「提交」按鈕的屬性至：



      ```JavaScript
      =AND(NOT(address of `value` property of the `name` field = ""), NOT(address of `value` property of the `email` field = ""), NOT(address of `value` property of the `phone` field))
      ```

      例如，

      ```JavaScript
      =AND(NOT(F9=""), NOT(F12=""), NOT(F10=""))
      ```

   1. 將「確認電子郵件」欄位的可見運算式設定為

      ```JavaScript
      =FORMULATEXT ((address of visible property of the Confirm Email field))
      ```

      例如，

      ```JavaScript
      =FORMULATEXT(G14)
      ```

      只有在填寫了所有欄位（名稱、電子郵件、電話）時，此公式才會顯示「提交」按鈕(TRUE) (NOT())會傳回每個欄位的TRUE)，否則會隱藏按鈕(AND(multiple FALSES) = FALSE)。

* OR()：如果指定的條件中至少有一個是TRUE，則傳回TRUE。

   * 範例：若使用者輸入任何適用的折扣券代碼，則套用折扣。

   1. 設定 `Visible` 「最終金額」欄位的屬性設為：


  ```JavaScript
     =IF(OR(F14="BlackFridaySale", F14="NewYearDiscount"), (F6*DAYS(F3,F2)* 0.7) , (F6*DAYS(F3,F2)))
  ```

   1. 將「確認電子郵件」欄位的值運算式設定為

      ```JavaScript
      =FORMULATEXT ((address of value property of the final amount field))
      ```

      例如，

      ```JavaScript
      =FORMULATEXT(F7)
      ```

      如果使用者輸入優惠券代碼（優惠券代碼= &quot;NewYearDiscount&quot;）或（優惠券代碼= &quot;BlackFridaySale&quot;），則此公式會計算30%的折扣，否則會將折扣設為0。

**文字函式：**

* IF()：評估條件，如果為TRUE則傳回特定值，如果為FALSE則傳回另一個值。

   * 範例：根據所選產品類別顯示自訂訊息。

   1. 設定 `Value` 的屬性 `message` 欄位至 `Only upto 7 kg check-in lagguage is allowed!`：

   1. 設定 `Visible` 的屬性 `message` 欄位至：


      ```JavaScript
      =if(address of value property of chosen product category ="Economy", TRUE(), FALSE())
      ```

      例如，

      ```JavaScript
      =if(F5="Economy", TRUE(), FALSE())
      ```

   1. 設定下列專案的值運算式： `message` 欄位至

      ```JavaScript
      =FORMULATEXT ((address of value property of the final amount field))
      ```

      例如，

      ```JavaScript
      =FORMULATEXT(G15)
      ```

      此公式會顯示訊息：「最多只允許7公斤的簽到行李！」 如果選擇的類別是「經濟」，否則會將訊息欄位留空。

**數學函式：**

* SUM()：將指定儲存格範圍的值相加。

  範例：計算購物車中專案的總成本。

  在「總成本」欄位的值運算式中：SUM(price * quantity)

  此公式假設您對每個專案的「價格」與「數量」有不同的欄位。 這會將兩者相乘，然後使用SUM()來加總購物車中所有專案的總成本。

* ROUND()：將數字四捨五入到指定的小數位數。

  範例：將計算的折扣金額四捨五入為兩位小數。

  在「折扣金額」欄位的值運算式中（假設在其他地方計算折扣）： ROUND(discount， 2)

  此公式會將折扣值四捨五入為兩位小數。

* MIN()：從指定的儲存格範圍傳回最小值。

  範例：根據選取的國家/地區尋找登錄檔單的最低年齡要求。

  在「最小年齡」欄位的值運算式中：MIN(ageLimits[&quot;US&quot;]，年齡限制[&quot;UK&quot;]，年齡限制[&quot;法國&quot;])

  此公式假設您有一個名為「ageLimits」的表格，其中儲存不同國家/地區的最低年齡需求。 它會使用MIN()來尋找其中最小的值。


此外，Adaptive Forms Block可讓您透過建立 [自訂函式](#creating-custom-functions). 自訂函式可讓您定義自己的規則和邏輯，讓您完全控制表單的行為。


## 建立和部署自訂函式

現成可用(OOTB) Adaptive Forms區塊可提供許多實作 [通用試算表函式](#spreadsheet-functions-for-rules). 不過，為了更精細地控制表單，您可以在調適型Forms區塊中使用Microsoft®Excel或Google Sheets中提供的任何OOTB函式。 最適化Forms區塊不包含Microsoft®Excel或Google Sheets中所有可用OOTB函式的實作。 如果您需要任何這類函式，可以開發具有類似語法的自訂函式，以實現Microsoft®Excel或Google Sheets所提供的功能。 例如，您可以實作 [Microsoft® Excel的Year()函式](https://support.microsoft.com/en-us/office/calculate-age-113d599f-5fea-448f-a4c3-268927911b37#) 以從出生日期計算年齡。


### 建立自訂函式

自訂函式位於 `[Adaptive form block]/functions.js` 檔案。 建立程式通常涉及以下步驟：

* 函式宣告：定義函式名稱及其引數（它接受的輸入）。
* 邏輯實作：撰寫程式碼，概述函式所執行的特定計算或操作。
* 函式匯出：從相關檔案匯出函式，讓函式可在規則中存取。

### 範例： Year函式

此範例示範兩個自訂函式，它們會模擬Microsoft®Excel的YEAR()函式來計算年齡：


```JavaScript
/**
 * Get the current date and time
 * @name now
 * @returns {Date} The current date and time as a Date object
 */
function now() {
  const today = new Date();
  return today;
}

/**
 * Get the year from a Date object
 * @name year
 * @param {Date} date The date object
 * @throws {TypeError} If the input is not a Date object
 * @returns {number} The year as a number
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

### 在您的表單中使用自訂函式

若要在表單中使用自訂函式：

1. **新增函式**：將您的自訂函式加入至 `[Adaptive form block]/functions.js` 檔案。 請記得將它新增至檔案中的匯出陳述式。
1. **部署檔案**：部署更新的 `functions.js` 檔案至您的GitHub專案，並驗證建置成功。
1. **函式用途**：使用存取表單試算表中的函式 `Value`， `Value Expression`， `Visible`，或 `Visible Expression` 屬性，類似於其他支援OOTB的試算表函式。
1. **預覽表單**：使用AEM Sidekick以預覽具有新實作函式的表單。

