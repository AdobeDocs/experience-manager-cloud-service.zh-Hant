---
title: 如何使用規則編輯器將規則套用至表單欄位，以針對使用WYSIWYG撰寫功能建立的表單啟用動態行為和複雜邏輯？
description: 通用編輯器中的規則編輯器可讓您新增動態行為並將複雜的邏輯建置到表單中，而不需要編碼或指令碼。
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
source-git-commit: c27b8e413c060de601a72a669d86c4add2a4167d
workflow-type: tm+mt
source-wordcount: '2111'
ht-degree: 5%

---


# 通用編輯器中的規則編輯器簡介

您可以使用規則編輯器來新增動態表單行為，這可讓您建立規則。 這些規則可啟用條件欄位可視性、根據使用者輸入自動計算並改善整體使用者體驗。 透過簡化表單填寫程式，規則編輯器可確保正確性和效率。

規則編輯器提供用於建立和管理規則的直覺式視覺介面。 其簡單易用的方法可讓所有使用者存取，包括沒有豐富技術專業知識的使用者，讓他們輕鬆地在表單中實作邏輯。

## 瞭解規則

規則是引導使用者在特定條件下執行哪些動作的指示。

* **條件**：條件是一種檢查或規則，可評估某條件是否成立。 這可回答以下問題：「是否符合要求？」

* **動作**：當條件為true時，就會發生動作。 它是根據條件評估觸發的任務或行為。

規則通常會遵循下列其中一種建構：

* **Condition-Action**：請先檢查條件，然後執行動作。 在規則編輯器中，`When`規則型別會強制執行`condition-action`建構。
* **Action-Condition**：先執行動作，然後檢查條件。 規則編輯器中的`Set Value Of`和`Validate`規則型別強制執行`action-condition`建構。
* **Action-Condition-Alternate Action**：執行動作、檢查條件，然後根據條件執行主要動作或替代動作。 例如，依預設，`Show`的替代動作是`Hide`，而`Enable`則是`Disable`。

例如，條件可能會檢查使用者是否已在欄位中輸入特定值，動作可能是顯示或隱藏欄位。
* **條件**：檢查收入是否大於$50,000。
* **動作**：如果條件為true，則顯示`Additional Deduction`欄位；否則，請執行替代動作：隱藏`Additional Deduction`欄位。

如需詳細的逐步指示，請參閱[新增條件式規則](#2-add-a-conditional-rule)。

## 如何啟用規則編輯器擴充功能？

在Universal Editor中，預設不會啟用規則編輯器。 若要為您的環境啟用規則編輯器擴充功能，請傳送一封電子郵件，由您的正式地址傳送至[aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)，附上您的要求。

為您的環境啟用規則編輯器擴充功能後，![edit-rules](/help/forms/assets/edit-rules-icon.svg)圖示會出現在編輯器的右上角。

![通用編輯器規則編輯器](/help/edge/docs/forms/assets/universal-editor-rule-editor.png)

選取您要寫入規則的表單物件，然後按一下![edit-rules](/help/forms/assets/edit-rules-icon.svg)圖示。 「規則編輯器」使用者介面隨即顯示。

![規則編輯器使用者介面](/help/edge/docs/forms/assets/rule-editor-for-field.png)

現在，您可以使用規則編輯器](#available-rule-types-in-rule-editor)中的[可用規則型別，開始為選取的表單欄位寫入規則或商業邏輯。

## 瞭解規則編輯器使用者介面

按一下![edit-rules](/help/forms/assets/edit-rules-icon.svg)圖示時，規則編輯器的視覺化編輯器會開啟：

![規則編輯器使用者介面](/help/edge/docs/forms/assets/rule-editor-interface.png)

<table border="1">
  <thead>
    <tr>
      <th>規則編輯器的元件</th>
      <th>說明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1.元件規則顯示</td>
      <td>顯示您用來啟動規則編輯器的表單物件標題，以及目前選取的規則型別。</td>
    </tr>
    <tr>
      <td>2.表單物件與函式</td>
      <td><b>Forms物件</b>索引標籤會顯示表單中包含之所有物件的階層檢視。 <b>函式</b>索引標籤包含一組內建函式。</td>
    </tr>
    <tr>
      <td>3.表單物件與功能切換</td>
      <td>點選切換按鈕時，會切換表單物件和函式窗格。</td>
    </tr>
    <tr>
      <td>4.視覺規則編輯器</td>
      <td>視覺化規則編輯器是規則編輯器使用者介面的視覺化編輯器模式中您編寫規則的區域。</td>
    </tr>
    <tr>
      <td>5.完成和取消按鈕</td>
      <td><b>Done</b>按鈕是用來儲存規則。 「<b>取消</b>」按鈕會放棄您對規則所做的任何變更，並關閉規則編輯器。</td>
    </tr>
  </tbody>
</table>

當您選取物件時，會列出表單物件上的任何現有規則。 您可以在視覺化規則編輯器中檢視標題和預覽規則摘要。 此外，您可以變更規則的順序、編輯規則、啟用/停用規則或刪除規則。

![顯示表單物件的可用規則](/help/edge/docs/forms/assets/rule-editor15.png)

## 可用的規則型別

規則編輯器提供了一組預先定義的規則型別，您可以使用這些型別來寫入規則，如下表所示：

<table border="1">
  <thead>
    <tr>
      <th>規則型別</th>
      <th>說明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>設定值</td>
      <td>根據是否符合指定的條件，設定表單物件的值。</td>
    </tr>
    <tr>
      <td>清除值</td>
      <td>清除指定物件的值。</td>
    </tr>
    <tr>
      <td>隱藏/顯示</td>
      <td>根據是否滿足條件隱藏或顯示表單物件。</td>
    </tr>
    <tr>
      <td>啟用/停用</td>
      <td>根據是否滿足條件來啟用或停用表單物件。</td>
    </tr>
    <tr>
      <td>驗證</td>
      <td>驗證表單或指定的物件。</td>
    </tr>
    <tr>
      <td>時間</td>
      <td>遵循<i>condition-action-alternate</i>動作規則結構或<i>condition-action</i>規則結構。 這會指定評估條件，之後會在滿足條件時觸發動作。</td>
    </tr>
    <tr>
      <td>格式</td>
      <td>根據函式或規則運算式來格式化表單物件。</td>
    </tr>
    <tr>
      <td>啟動服務</td>
      <td>叫用表單資料模型(FDM)中設定的服務。</td>
    </tr>
    <tr>
      <td>設定屬性</td>
      <td>根據條件設定指定物件的屬性值。</td>
    </tr>
    <tr>
      <td>設定焦點</td>
      <td>將焦點設定在指定的物件上。</td>
    </tr>
    <tr>
      <td>儲存表單</td>
      <td>儲存表單。</td>
    </tr>
    <tr>
      <td>提交/重設表單</td>
      <td>提交或重設表單。</td>
    </tr>
    <tr>
      <td>新增/移除執行個體</td>
      <td>新增或移除指定之可重複面板或表格列的例項。</td>
    </tr>
    <tr>
      <td>瀏覽至</td>
      <td>導覽至其他最適化Forms、影像或檔案片段等其他資產，或外部URL。</td>
    </tr>
    <tr>
      <td>分派事件</td>
      <td>根據預先定義的條件或事件觸發特定動作。</td>
    </tr>
    <tr>
      <td>在面板之間導覽</td>
      <td>可讓您在表單的不同面板之間切換焦點。</td>
    </tr>
  </tbody>
</table>


現在，讓我們探索如何在規則編輯器中[撰寫規則](#write-rules)。

## 寫入規則

若要瞭解如何在「視覺規則編輯器」中編寫規則，讓我們來看看稅捐計算表單的簡單範例：

![規則編輯器範例](/help/edge/docs/forms/assets/rule-editor-1.png)

使用者可透過上述表單輸入薪資毛額。 根據此輸入，會顯示條件欄位，並計算應付稅金。

**表單欄位：**
* 薪資毛額（使用者輸入）
* 額外扣除（條件欄位）
* 應課稅收入（計算欄位）
* 應付稅金（計算欄位）

**條件規則：**
* 條件：薪資毛額> 50,000
* 動作：顯示額外扣除欄位

**計算規則：**

* 應課稅收入=薪資總額 — 額外扣減（若適用）
* 應付稅金=應稅所得*稅率（為簡單起見，假設固定稅率為10%）

若要撰寫規則，請執行下列步驟：

### 1.撰寫表單

若要在Universal Editor中編寫表單：

1. 在Universal Editor中開啟表單以進行編輯。
1. 新增下清單單元件：
   * 稅捐計算表單（標題）
   * 薪資毛額（文字輸入）
   * 額外扣除（文字輸入）
   * 應課稅收入（文字輸入）
   * 應付稅金（文字輸入）
   * 提交（提交按鈕）
1. 透過開啟其`Properties`來隱藏`Additional Deduction`表單欄位。

   ![規則編輯器範例](/help/edge/docs/forms/assets/rule-editor2.png)

### 2.為表單欄位新增條件規則

撰寫表單後，撰寫第一個規則，只有在薪資總額超過$50,000時，才會顯示`Additional Deduction`欄位。 若要新增條件規則：

1. 在Universal Editor中開啟表單以進行編輯。
1. 在內容樹狀結構中選取&#x200B;**[!UICONTROL Gross Salary]**&#x200B;元件，並選取![edit-rules](/help/forms/assets/edit-rules-icon.svg)。
   ![規則編輯器範例1](/help/edge/docs/forms/assets/rule-editor3.png)
視覺化規則編輯器介面隨即顯示。
1. 按一下&#x200B;**[!UICONTROL 建立]**以啟動規則編輯器。
   ![規則編輯器範例2](/help/edge/docs/forms/assets/rule-editor4.png)
依預設，會選取`Set Value Of`規則型別。 雖然您無法變更或修改選取的物件，但可以使用規則下拉式清單來選取其他規則型別。\
   ![規則編輯器範例3](/help/edge/docs/forms/assets/rule-editor5.png)
1. 開啟規則型別下拉式清單，並選取&#x200B;**[!UICONTROL 當]**規則型別。
   ![規則編輯器範例4](/help/edge/docs/forms/assets/rule-editor6.png)
1. 選取&#x200B;**[!UICONTROL 選取狀態]**&#x200B;下拉式清單，並選取&#x200B;**[!UICONTROL 大於]**。 **[!UICONTROL 輸入數字]**欄位就會顯示。
   ![規則編輯器範例5](/help/edge/docs/forms/assets/rule-editor7.png)
1. 在規則的&#x200B;**[!UICONTROL 輸入數字]**&#x200B;欄位中輸入`50000`。
   ![規則編輯器範例6](/help/edge/docs/forms/assets/rule-editor8.png)
您已將條件定義為`When Gross Salary is greater than 50000`。 接著，定義此條件為`True`時要執行的動作。
1. 在`Then`陳述式中，從&#x200B;**[!UICONTROL 選取動作]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL 顯示]**。
   ![規則編輯器範例7](/help/edge/docs/forms/assets/rule-editor9.png)
1. 從&#x200B;**[!UICONTROL 拖放物件上的[表單物件]索引標籤中拖放**[!UICONTROL &#x200B;額外扣款&#x200B;]**欄位，或選取這裡]**&#x200B;欄位。 或者，選取&#x200B;**[!UICONTROL 拖放物件或選取這裡]**&#x200B;欄位，然後從躍現式選單中選取&#x200B;**[!UICONTROL 額外扣繳]**欄位，這會列出表單中的所有表單物件。
   ![規則編輯器範例8](/help/edge/docs/forms/assets/rule-editor10.png)
1. 按一下&#x200B;**[!UICONTROL 新增其他區段]**，為&#x200B;**[!UICONTROL 總薪資]**&#x200B;欄位新增其他條件，以防您輸入的薪資低於`50000`。
   ![規則編輯器範例9](/help/edge/docs/forms/assets/rule-editor11.png)
1. 從`Else`陳述式中的&#x200B;**[!UICONTROL 選取動作]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL 隱藏]**。
   ![規則編輯器範例10](/help/edge/docs/forms/assets/rule-editor12.png)
1. 從&#x200B;**[!UICONTROL 拖放物件上的[表單物件]索引標籤中拖放**[!UICONTROL &#x200B;額外扣款&#x200B;]**欄位，或選取這裡]**&#x200B;欄位。 或者，選取&#x200B;**[!UICONTROL 拖放物件或選取這裡]**&#x200B;欄位，然後從躍現式選單中選取&#x200B;**[!UICONTROL 額外扣繳]**欄位，這會列出表單中的所有表單物件。
   ![規則編輯器範例11](/help/edge/docs/forms/assets/rule-editor13.png)
1. 選取&#x200B;**[!UICONTROL 完成]**以儲存規則。
規則在規則編輯器中會顯示如下。
   ![規則編輯器範例12](/help/edge/docs/forms/assets/rule-editor14.png)

>[!NOTE]
>
> 或者，您可以在「額外扣款」欄位上撰寫「顯示」規則，而不是「薪資總額」欄位上的「何時」規則，以實施相同的行為。

### 3.新增表單欄位的計算規則

接下來，撰寫規則以計算`Taxable Income`，這是`Gross Salary`與`Additional Deduction`之間的差異（如果適用）。 若要在&#x200B;**[!UICONTROL 應稅收入]**&#x200B;欄位中新增計算規則，請執行下列步驟：

1. 在撰寫模式中，選取&#x200B;**[!UICONTROL 應稅收入]**&#x200B;欄位，並選取![編輯規則](/help/forms/assets/edit-rules-icon.svg)圖示。 接著，選取&#x200B;**[!UICONTROL 建立]**以啟動規則編輯器。
   ![規則編輯器範例13](/help/edge/docs/forms/assets/rule-editor16.png)
1. 選取&#x200B;**[!UICONTROL 選取選項]**&#x200B;並選取&#x200B;**[!UICONTROL 數學運算式]**。 用於寫入數學運算式的欄位隨即開啟。
   ![規則編輯器範例14](/help/edge/docs/forms/assets/rule-editor17.png)

1. 在數學運算式欄位中：

   * 從Forms物件索引標籤中選取或拖放第一個&#x200B;**[!UICONTROL 拖放物件中的**[!UICONTROL  Gross Salary ]**欄位，或選取這裡]**&#x200B;欄位。

   * 從&#x200B;**[!UICONTROL 選取運運算元]**&#x200B;欄位中選取&#x200B;**[!UICONTROL 減號]**。

   * 從Forms物件索引標籤中選取或拖放其他&#x200B;**[!UICONTROL 拖放物件中的**[!UICONTROL &#x200B;額外扣款&#x200B;]**欄位，或選取這裡]**欄位。
     ![規則編輯器範例15](/help/edge/docs/forms/assets/rule-editor18.png)

1. 選取&#x200B;**[!UICONTROL 完成]**&#x200B;以儲存規則。

   現在，為`Tax Payable `欄位新增規則，這是透過將應課稅收入乘以稅率所決定。 為簡單起見，假設固定稅率為`10%`。

1. 在撰寫模式中，選取&#x200B;**[!UICONTROL 應付稅金]**&#x200B;欄位，並選取![編輯規則](/help/forms/assets/edit-rules-icon.svg)圖示。 接著，選取&#x200B;**[!UICONTROL 建立]**以啟動規則編輯器。
   ![規則編輯器範例16](/help/edge/docs/forms/assets/rule-editor19.png)
1. 選取&#x200B;**[!UICONTROL 選取選項]**&#x200B;並選取&#x200B;**[!UICONTROL 數學運算式]**。 用於寫入數學運算式的欄位隨即開啟。
   ![規則編輯器範例17](/help/edge/docs/forms/assets/rule-editor20.png)
1. 在數學運算式欄位中：

   * 在Forms物件標籤中，選取或拖放第一個&#x200B;**[!UICONTROL 拖放物件的**[!UICONTROL &#x200B;應課稅收入&#x200B;]**欄位，或選取這裡]**&#x200B;欄位。

   * 從&#x200B;**[!UICONTROL 選取運運算元]**&#x200B;欄位中選取&#x200B;**[!UICONTROL 乘以]**。

   * 從&#x200B;**[!UICONTROL 選取選項]**&#x200B;欄位中選取&#x200B;**數字**，並在&#x200B;**[!UICONTROL 輸入數字]**&#x200B;欄位中輸入值為`10`。
     ![規則編輯器範例18](/help/edge/docs/forms/assets/rule-editor21.png)
1. 接著，在運算式欄位周圍反白的區域中選取，並選取&#x200B;**[!UICONTROL 延伸運算式]**。
   ![規則編輯器範例19](/help/edge/docs/forms/assets/rule-editor22.png)
1. 在延伸運算式欄位中，從&#x200B;**[!UICONTROL 選取運運算元]**&#x200B;欄位中選取&#x200B;**[!UICONTROL 除以]**，並從&#x200B;**[!UICONTROL 選取選項]**&#x200B;欄位中選取&#x200B;**[!UICONTROL 數字]**。 然後在數字欄位中指定`100`。
   ![規則編輯器範例20](/help/edge/docs/forms/assets/rule-editor23.png)
1. 選取&#x200B;**[!UICONTROL 完成]**&#x200B;以儲存規則。

### 4.預覽表單

現在，當您預覽表單並輸入&#x200B;**薪資總額**&#x200B;作為`60,000`時，會顯示&#x200B;**額外扣減**&#x200B;欄位，並據此計算&#x200B;**應課稅收入**&#x200B;及&#x200B;**應付稅金**。

![預覽表單](/help/edge/docs/forms/assets/rule-editor-form.png)

除了現成可用的函式（例如Sum、Average）之外（列在函式輸出下），您可以[撰寫自訂函式](#create-a-custom-function)以實作複雜的商業邏輯。

## 規則編輯器中的自訂函式

Edge Delivery Services Forms支援自訂函式，可讓使用者定義JavaScript函式以實作複雜的商業規則。 自訂函式可協助處理輸入的資料，以符合指定的需求，進而擴充表單的功能。

### 建立自訂函數

若要建立自訂函式，請編輯`../[blocks]/form/functions.js`檔案。 建立程序一般包括以下步驟：

* **函式宣告**：定義函式名稱及其引數（它接受的輸入）。
* **邏輯實作**：撰寫程式碼，概述函式所執行的特定計算或操作。
* **函式匯出**：從相關檔案匯出函式，讓函式可在您的規則中存取。


此範例示範兩個自訂函式： `getFullName`和`days`：

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
![正在新增自訂函式](/help/edge/docs/forms/assets/create-custom-function.png)

### 在規則編輯器中使用自訂函式

若要在規則編輯器中使用自訂函式：

1. **新增函式**：將您的自訂函式包含在`../[blocks]/form/functions.js`檔案中。 請記得將它新增至檔案中的`export`陳述式。
1. **部署檔案**：將更新的 `functions.js` 檔案部署到您的 GitHub 專案並驗證建置是否成功。
1. **函式使用方式**：選取&#x200B;**[!UICONTROL 選取動作]**&#x200B;欄位中的`Function Output`選項，存取表單規則編輯器中的函式。

   規則編輯器中的![自訂函式](/help/edge/docs/forms/assets/custom-function-rule-editor.png)

1. **預覽表單**：使用新實作的函式預覽您的表單。

## 相關文章

{{see-also-rule-editor}}

## 另請參閱

* [開始使用 AEM Forms 適用的 Edge Delivery Services](/help/edge/docs/forms/tutorial.md)
* [使用 Google Sheets 或 Microsoft Excel 建立表單](/help/edge/docs/forms/create-forms.md)
* [設定您的 Google 表單或 Microsoft Excel 檔案以開始接受資料](/help/edge/docs/forms/submit-forms.md)
* [發佈您的表單並開始收集資料](/help/edge/docs/forms/publish-forms.md)
* [自訂表單的外觀](/help/edge/docs/forms/style-theme-forms.md)
* [將可重複區段新增到表單](/help/edge/docs/forms/repeatable-forms.md)
* [提交表單後顯示自訂感謝訊息](/help/edge/docs/forms/thank-you-page-form.md)
* [最適化表單區塊元件及其屬性](/help/edge/docs/forms/form-components.md)
* [實際使用監視](https://www.aem.live/developer/rum#authentication)
