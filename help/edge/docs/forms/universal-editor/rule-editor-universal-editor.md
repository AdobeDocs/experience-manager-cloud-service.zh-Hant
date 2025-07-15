---
title: 如何使用規則編輯器將規則套用至表單欄位，讓使用 WYSIWYG 製作功能建立的表單能夠擁有動態行為和複雜邏輯？
description: 透過通用編輯器的規則編輯器，您不需要編寫程式碼或指令碼，即可在表單中加入動態行為和建置複雜的邏輯。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 846f56e1-3a98-4a69-b4f7-40ec99ceb348
source-git-commit: e1ead9342fadbdf82815f082d7194c9cdf6d799d
workflow-type: tm+mt
source-wordcount: '2253'
ht-degree: 98%

---


# WYSIWYG 製作中的規則編輯器簡介

<span class="preview">您可以透過搶先體驗方案使用這項功能。若要請求存取權，請使用您的官方地址發送電子郵件至 <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a>，郵件內容須包含您的 GitHub 組織名稱和存放庫名稱。例如，若存放庫 URL 為 https://github.com/adobe/abc,，則組織名稱為 adobe，存放庫名稱為 abc。</span>


您可以使用規則編輯器來建立規則，藉此新增動態表單行為。這些規則會顯示條件式欄位、根據使用者輸入自動進行計算，並改善整體使用者體驗。規則編輯器將表格填寫流程簡化，有助於確保準確性和效率。

規則編輯器透過直覺易用的視覺化介面，提供建立和管理規則的功能。它採用簡單易用的方法，方便所有使用者取用，即使沒有豐富的技術專業知識，使用者仍然可以輕鬆在表單中實作邏輯。

## 了解規則

規則是指導使用者在特定條件下執行哪些動作的指示。

* **條件**：條件是評估某些事情為 true 或 false 的檢查或規則。它會回答下列問題：「這是否符合需求？」

* **動作**：動作是條件為 true 時所發生的事。動作是根據條件評估結果觸發的任務或行為。

規則通常遵循下列其中一種結構：

* **條件-動作**：先檢查條件，再執行動作。在規則編輯器中，規則類型 `When` 會強制執行 `condition-action` 結構。
* **動作-條件**：先執行動作，再檢查條件。`Set Value Of` 和規則編輯器中的 `Validate` 規則類型會強制執行 `action-condition` 結構。
* **動作-條件-替代動作**：執行一個動作，檢查一個條件，然後根據條件來執行主要動作或替代動作。例如，在預設情況下，`Show` 的替代動作是 `Hide`，而 `Enable` 的替代動作則為 `Disable`。

例如，一個條件可能會檢查使用者是否在欄位中已輸入特定值，而動作可能為顯示或隱藏欄位。
* **條件**：檢查收入是否高於 $50,000。
* **動作**：如果條件為 true，則顯示 `Additional Deduction` 欄位；否則便執行替代動作：隱藏 `Additional Deduction` 欄位。

如需詳細的逐步操作指示，請參閱[新增條件式規則](#2-add-a-conditional-rule)。

## 如何啟用規則編輯器延伸模組？

在通用編輯器中，規則編輯器延伸模組預設為未啟用。若要啟用規則編輯器延伸模組，請從您的官方電子郵件 ID 寫信至 [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) 來和我們聯絡。

在您的環境中啟用規則編輯器延伸模組後，![編輯規則](/help/forms/assets/edit-rules-icon.svg)圖示會顯示在編輯器的右上角。

![通用編輯器的規則編輯器](/help/edge/docs/forms/assets/universal-editor-rule-editor.png)

選取要編寫規則的表單元件，然後按一下![編輯規則](/help/forms/assets/edit-rules-icon.svg)圖示。接著顯示規則編輯器使用者介面。

![規則編輯器使用者介面](/help/edge/docs/forms/assets/rule-editor-for-field.png)

在本文中，`form object` 和 `form component` 可互換使用。

您可以立即開始使用[規則編輯器中可用的規則類型](#available-rule-types-in-rule-editor)，為所選取的表單欄位編寫規則或商業邏輯。

## 了解規則編輯器使用者介面

按一下「![編輯規則](/help/forms/assets/edit-rules-icon.svg)」圖示，規則編輯器的編輯器會隨即開啟：

![規則編輯器使用者介面](/help/edge/docs/forms/assets/rule-editor-interface.png)

<table border="1">
  <thead>
    <tr>
      <th>規則編輯器元件</th>
      <th>說明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1. 標題</td>
      <td>顯示表單元件的標題和選取的規則類型。例如，「輸入薪資總額」是選取了「何時」規則類型的文字方塊元件。 </td>
    </tr>
    <tr>
      <td>2. 表單物件和函數</td>
      <td>「<b>表單物件</b>」索引標籤會顯示表單中所包含的所有元件的階層式檢視。「<b>函數</b>」索引標籤會包括一組規則編輯器中的內建函數。</td>
    </tr>
    <tr>
      <td>3. 表單物件和函數切換</td>
      <td>切換按鈕會交替顯示或隱藏表單物件和功能窗格。 </td>
    </tr>
    <tr>
      <td>4. 視覺化規則編輯器</td>
      <td>視覺化規則編輯器是您可以為表單元件建立規則的介面。</td>
    </tr>
    <tr>
      <td>5. 完成和取消按鈕</td>
      <td>「<b>完成</b>」按鈕用於儲存規則。「<b>取消</b>」按鈕會捨棄對規則所做的任何變更並關閉規則編輯器。</td>
    </tr>
  </tbody>
</table>

當您選取元件時，該表單元件的全部現有規則即會列出。您可以在規則編輯器上檢視標題和預覽規則摘要。此外，您可以變更規則的順序、編輯規則、啟用/停用規則或刪除規則。

![顯示表單物件的可用規則](/help/edge/docs/forms/assets/rule-editor15.png)

## 可用規則類型

規則編輯器提供一組預先定義的規則類型，您可以用於編寫規則，如下表所示：

<table border="1">
  <thead>
    <tr>
      <th>規則類型</th>
      <th>說明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>設定值</td>
      <td>根據是否滿足指定條件來設定表單元件的值。</td>
    </tr>
    <tr>
      <td>清除值</td>
      <td>清除指定表單元件的值。</td>
    </tr>
    <tr>
      <td>隱藏/顯示</td>
      <td>根據是否滿足條件來隱藏或顯示表單元件。</td>
    </tr>
    <tr>
      <td>啟用/停用</td>
      <td>根據是否滿足條件來啟用或停用表單元件。</td>
    </tr>
    <tr>
      <td>驗證</td>
      <td>根據條件檢查表單元件，如果未滿足條件即顯示錯誤。 </td>
    </tr>
    <tr>
      <td>條件</td>
      <td>這會指定評估的條件，以及在滿足條件時要觸發的動作。其會遵循<i>條件-動作-替代</i>動作規則結構或<i>條件-動作</i>規則結構。 </td>
    </tr>
    <tr>
      <td>格式</td>
      <td> 當表單元件的值變更時，使用指定的運算式修改其顯示值。</td>
    </tr>
    <tr>
      <td>叫用服務</td>
      <td>叫用使用外部 API、表單資料模型或 RESTful Web 服務所設定的服務。</td>
    </tr>
    <tr>
      <td>設定屬性</td>
      <td>根據條件設定指定表單元件的屬性值。</td>
    </tr>
    <tr>
      <td>設定焦點</td>
      <td>在指定的表單元件上設定焦點。</td>
    </tr>
    <tr>
      <td>儲存表單</td>
      <td>這讓使用者可以使用草稿和提交表單入口網站元件將表單儲存為草稿。 </td>
    </tr>
    <tr>
      <td>提交表單</td>
      <td>提交表單。</td>
    </tr>
    <tr>
      <td>重設表單</td>
      <td>重設表單。</td>
    </tr>
    <tr>
      <td>新增/移除執行個體</td>
      <td>新增或移除指定的可重複面板或表格列執行個體。</td>
    </tr>
    <tr>
      <td>瀏覽至</td>
      <td>瀏覽至其他最適化表單、其他資產 (例如影像或文件片段) 或外部 URL。</td>
    </tr>
    <tr>
      <td>分派事件</td>
      <td>根據預先定義的條件或事件觸發指定動作。</td>
    </tr>
    <tr>
      <td>在面板之間瀏覽</td>
      <td>您可於表單中的不同面板之間切換焦點。</td>
    </tr>
  </tbody>
</table>


立即探索如何[在規則編輯器中編寫規則](#write-rules)。

## 編寫規則

若要了解如何在視覺化規則編輯器中編寫規則，我們以簡單的稅額計算表單為例：

![規則編輯器介面的熒幕擷圖，顯示建立條件式規則，以及表單欄位可見性的When-Then邏輯](/help/edge/docs/forms/assets/rule-editor-1.png)

在上述表單中，使用者輸入薪資總額。根據此輸入，顯示條件式欄位並計算應納稅額。

**表單欄位：**
* 薪資總額 (使用者輸入)
* 其他扣除額 (條件式欄位)
* 應稅所得 (計算欄位)
* 應納稅額 (計算欄位)

**條件式規則：**
* 條件：薪資總額 > 50,000
* 動作：顯示「其他扣除額」欄位

**計算規則：**

* 應稅所得=薪資總額 - 其他扣除額 (如適用)
* 應納稅額 = 應稅所得 * 稅率 (為簡單起見，假設固定稅率為 10%)

若要編寫規則，請執行下列步驟：

### &#x200B;1. 製作表單

若要在通用編輯器中製作表單：

1. 在通用編輯器中開啟表單以進行編輯。
1. 新增下列表單元件：
   * 稅額計算表 (標題)
   * 薪資總額 (數字輸入)
   * 其他扣除額 (數字輸入)
   * 應稅所得 (數字輸入)
   * 應納稅額 (數字輸入)
   * 提交 (提交按鈕)
1. 透過開啟其 `Properties`，隱藏 `Additional Deduction` 表單欄位。

   ![稅捐計算表單的熒幕擷圖，其中包含總薪資、婚姻狀況和受撫養子女的輸入欄位，在套用規則之前先展示表單結構](/help/edge/docs/forms/assets/rule-editor2.png)

### &#x200B;2. 新增表單欄位的條件式規則

製作表單後，請編寫第一條規則，只有在薪資總額超過 $50,000 時才顯示 `Additional Deduction` 欄位。若要新增條件式規則：

1. 在通用編輯器中開啟表單以進行編輯，然後選取內容樹中的「**[!UICONTROL 薪資總額]**」，並選取「![編輯規則](/help/forms/assets/edit-rules-icon.svg)」。或者，您可以直接從「**[!UICONTROL 表單物件]**」窗格選取「**[!UICONTROL 薪資總額]**」欄位。
   ![規則編輯器範例 1](/help/edge/docs/forms/assets/rule-editor3.png)
顯示規則編輯器視覺化介面。
1. 按一下「**[!UICONTROL 建立]**」，即可建立規則。
   ![規則編輯器範例 2](/help/edge/docs/forms/assets/rule-editor4.png)
依預設已選取 `Set Value Of` 規則類型。雖然您無法變更或修改所選物件，但可以使用規則下拉式清單以選取其他規則類型。\
   ![規則編輯器範例 3](/help/edge/docs/forms/assets/rule-editor5.png)
1. 開啟規則類型下拉式清單，並選取 **[!UICONTROL When]** 規則類型。
   ![規則編輯器範例 4](/help/edge/docs/forms/assets/rule-editor6.png)
1. 選取「**[!UICONTROL 選取狀態]**」下拉式清單並選取「**[!UICONTROL 大於]**」。接著顯示「**[!UICONTROL 輸入數字]**」欄位。
   ![規則編輯器範例 5](/help/edge/docs/forms/assets/rule-editor7.png)
1. 在規則的「**[!UICONTROL 輸入數字]**」欄位中輸入 `50000`。
   ![規則編輯器範例 6](/help/edge/docs/forms/assets/rule-editor8.png)
您已將條件定義為 `When Gross Salary is greater than 50000`。接下來，請定義如果條件為 `True` 時要執行的動作。
1. 在 `Then` 陳述式中，從「**[!UICONTROL 選取動作]**」下拉式清單選取「**[!UICONTROL 顯示]**」。
   ![規則編輯器範例 7](/help/edge/docs/forms/assets/rule-editor9.png)
1. 把「表單物件」索引標籤的「**[!UICONTROL 其他扣除額]**」欄位拖放到「**[!UICONTROL 放置物件或選取此處]**」欄位。或者，選取「**[!UICONTROL 放置物件或選取此處]**」欄位，並從列出表單中所有表單物件的快顯選單中選取「**[!UICONTROL 其他扣除額]**」欄位。
   ![規則編輯器範例 8](/help/edge/docs/forms/assets/rule-editor10.png)
1. 按一下「**[!UICONTROL 新增其他區段]**」，針對「**[!UICONTROL 薪資總額]**」欄位新增其他條件，以防您輸入的薪資低於 `50000`。
   ![規則編輯器範例 9](/help/edge/docs/forms/assets/rule-editor11.png)
1. 從 `Else` 陳述式的「**[!UICONTROL 選取動作]**」下拉式清單選取「**[!UICONTROL 隱藏]**」。
   ![規則編輯器範例 10](/help/edge/docs/forms/assets/rule-editor12.png)
1. 把「表單物件」索引標籤的「**[!UICONTROL 其他扣除額]**」欄位拖放到「**[!UICONTROL 放置物件或選取此處]**」欄位。或者，選取「**[!UICONTROL 放置物件或選取此處]**」欄位，並從列出表單中所有表單物件的快顯選單中選取「**[!UICONTROL 其他扣除額]**」欄位。
   ![規則編輯器範例 11](/help/edge/docs/forms/assets/rule-editor13.png)
1. 選取「**[!UICONTROL 完成]**」以儲存此規則。此規則在規則編輯器中顯示如下。
   ![規則編輯器範例 12](/help/edge/docs/forms/assets/rule-editor14.png)

>[!NOTE]
>
> 或者，您可以在「其他扣除額」欄位編寫「Show」規則，而非在「薪資總額」欄位編寫「When」規則，以執行相同行為。

### &#x200B;3. 新增表單欄位的計算規則

接下來，編寫規則來計算 `Taxable Income`，即 `Gross Salary` 和 `Additional Deduction` 之間的差額 (如適用)。若要在「**[!UICONTROL 應稅所得]**」欄位中新增計算規則，請執行下列步驟：

1. 在製作模式中，選取「**[!UICONTROL 應稅所得]**」欄位，並選取![編輯規則](/help/forms/assets/edit-rules-icon.svg)圖示。或者，您可以直接從「**[!UICONTROL 表單物件]**」窗格選取「**[!UICONTROL 應稅所得]**」欄位。
1. 接下來，選取「**[!UICONTROL 建立]**」，即可建立規則。
   ![規則編輯器範例 13](/help/edge/docs/forms/assets/rule-editor16.png)
1. 選取「**[!UICONTROL 選取選項]**」，並選取「**[!UICONTROL 數學運算式]**」。開啟用於編寫數學運算式的欄位。
   ![規則編輯器範例 14](/help/edge/docs/forms/assets/rule-editor17.png)

1. 在數學運算式欄位：

   * 從「表單物件」索引標籤中選取或拖放「**[!UICONTROL 薪資總額]**」欄位到第一個「**[!UICONTROL 放置物件或選取此處]**」欄位。

   * 從「**[!UICONTROL 選取運算子]**」欄位選取「**[!UICONTROL 減]**」。

   * 從「表單物件」索引標籤選取或拖放「**[!UICONTROL 其他扣除額]**」欄位到另一個「**[!UICONTROL 放置物件或選取此處]**」欄位。
     ![規則編輯器範例 15](/help/edge/docs/forms/assets/rule-editor18.png)

1. 選取「**[!UICONTROL 完成]**」以儲存此規則。

   現在為「`Tax Payable `」欄位新增規則，而此欄位是由應稅所得乘以稅率計算得出。為簡單起見，假設固定稅率為 `10%`。

1. 在製作模式中，選取「**[!UICONTROL 應納稅額]**」欄位，並選取![編輯規則](/help/forms/assets/edit-rules-icon.svg)圖示。接下來，選取「**[!UICONTROL 建立]**」，即可建立規則。
   ![規則編輯器範例 16](/help/edge/docs/forms/assets/rule-editor19.png)
1. 選取「**[!UICONTROL 選取選項]**」，並選取「**[!UICONTROL 數學運算式]**」。開啟用於編寫數學運算式的欄位。
   ![規則編輯器範例 17](/help/edge/docs/forms/assets/rule-editor20.png)
1. 在數學運算式欄位：

   * 從「表單物件」索引標籤中選取或拖放「**[!UICONTROL 應稅所得]**」欄位到第一個「**[!UICONTROL 放置物件或選取此處]**」欄位。

   * 從「**[!UICONTROL 選取運算子]**」欄位選取「**[!UICONTROL 乘以]**」。

   * 從「**[!UICONTROL 選取選項]**」欄位選取「**數字**」，並在「**[!UICONTROL 輸入數字]**」欄位中輸入值 `10`。
     ![規則編輯器範例 18](/help/edge/docs/forms/assets/rule-editor21.png)
1. 接下來，選取運算式欄位周圍醒目標示的區域，並選取「**[!UICONTROL 擴充運算式]**」。
   ![規則編輯器範例 19](/help/edge/docs/forms/assets/rule-editor22.png)
1. 在擴展運算式欄位中，從「**[!UICONTROL 選取運算子]**」欄位選取「**[!UICONTROL 除以]**」以及從「**[!UICONTROL 選取選項]**」欄位選取「**[!UICONTROL 數字]**」。然後，在數字欄位指定 `100`。
   ![規則編輯器範例 20](/help/edge/docs/forms/assets/rule-editor23.png)
1. 選取「**[!UICONTROL 完成]**」以儲存此規則。

### &#x200B;4. 預覽表單

現在，當您預覽表單並輸入「**薪資總額**」為 `60,000` 時，會顯示「**其他扣除額**」欄位，並據此計算「**應稅所得**」和「**應納稅額**」。

![預覽表單](/help/edge/docs/forms/assets/rule-editor-form.png)

除了「函數輸出」之下列出的開箱即用函數 (如 Sum、Average) 之外，您還可以[編寫自訂函數](#create-a-custom-function)來執行複雜的商業邏輯。

## 規則編輯器中的自訂函數

Edge Delivery Services 表單支援自訂函數，讓使用者可以定義 JavaScript 函數來執行複雜的業務規則。自訂函數讓使用者更加方便地操作和處理所輸入資料來滿足指定要求，藉此擴展表單的功能。

### 建立自訂函數

若要建立自訂函數，請編輯 `../[blocks]/form/functions.js` 檔案。建立流程通常包括下列步驟：

* **函數宣告**：定義函數名稱及其參數 (其接受的輸入)。
* **邏輯實作**：編寫概述函數執行的特定計算或操作之程式碼。
* **函數匯出**：從相關檔案匯出函數，方便您在規則中存取使用。


此範例示範兩種自訂函數 `getFullName` 和 `days`：

```JavaScript
/**
 * Get Full Name
 * @name getFullName Concats first name and last name
 * @param {string} firstname in Stringformat
 * @param {string} lastname in Stringformat
 * @return {string}
 */
function getFullName(firstname, lastname) {
  return `${firstname} ${lastname}`.trim();
}

/**
 * Calculate the number of days between two dates.
 * @param {*} endDate
 * @param {*} startDate
 * @name days Calculates the numebr of days between two dates
 * @returns {number} returns the number of days between two dates
 */
function days(endDate, startDate) {
  const start = typeof startDate === 'string' ? new Date(startDate) : startDate;
  const end = typeof endDate === 'string' ? new Date(endDate) : endDate;

  // return zero if dates are valid
  if (Number.isNaN(start.getTime()) || Number.isNaN(end.getTime())) {
    return 0;
  }

  const diffInMs = Math.abs(end.getTime() - start.getTime());
  return Math.floor(diffInMs / (1000 * 60 * 60 * 24));
}

// eslint-disable-next-line import/prefer-default-export
export { getFullName, days };
```
![新增自訂函數](/help/edge/docs/forms/assets/create-custom-function.png)

### 在規則編輯器中使用自訂函數

若要在規則編輯器中使用自訂函數：

1. **新增函數**：將您的自訂函數納入 `../[blocks]/form/functions.js` 檔案中。請記得將函數新增至檔案中的 `export` 陳述式。
1. **部署檔案**：將更新的 `functions.js` 檔案部署到您的 GitHub 專案並驗證建置是否成功。
1. **函數使用情況**：在「**[!UICONTROL 選取動作]**」欄位中選取「`Function Output`」選項，即可在表單的規則編輯器中存取函數。

   ![規則編輯器中的自訂函數](/help/edge/docs/forms/assets/custom-function-rule-editor.png)

1. **預覽表單**：預覽您的表單和新實作的函數。

## 其他資訊

>[!NOTE]
>
> 在通用編輯器中，自訂函數指令碼不支援靜態和動態匯入。您需要在 `../[blocks]/form/functions.js` 檔案中新增完整的程式碼。

本文可提供有關通用編輯器中可用的規則編輯器的有限資訊。若要了解規則編輯器和自訂函數的詳細資訊，請參閱下列文章：

{{see-also-rule-editor}}

## 另請參閱

{{universal-editor-see-also}}
