---
title: 本文概述根據核心元件在最適化表單中規則編輯器的各種使用案例。
description: 本文概述根據核心元件在最適化表單中規則編輯器的各種使用案例。
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
source-git-commit: c600af3f2e866483cda2426e188dbc104b07688e
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 0%

---


# 規則編輯器的不同使用案例

本文提供根據核心元件之最適化表單的規則編輯器詳細範例，深入瞭解其針對不同情境的正確實施。 規則編輯器可讓開發人員定義和管理控制表單行為的邏輯。
現在，讓我們討論規則編輯器的不同實作。


## 使用內建函式簡化可重複面板中的複雜計算

規則編輯器可讓您直接在可重複面板中的欄位上使用現成可用的函式，例如Sum、Min、Max和Join。 這開啟了強大的自動化功能，讓您無需自訂程式碼即可實施複雜的商業邏輯。
想像一個具有可重複面板的表單，其中每個面板執行個體都會收集有關資產宣告值的資訊。

![可重複的表單](/help/forms/assets/ootb-function-support-repeatable-panel-form.png)

您可以使用`Sum`函式自動計算所有面板的總資產值，而不需要手動計算，並降低發生錯誤的可能性。

![支援OOTB函式中的可重複面板欄位](/help/forms/assets/ootb-function-support-repeatable-panel.png)

當您填寫表單並新增執行個體以宣告資產值時，`Calculate Asset Value`按鈕會計算所有已宣告資產值的總和，並在`assetvalue`文字方塊中顯示結果。

![支援OOTB函式中的可重複面板欄位](/help/forms/assets/ootb-function-support-repeatable-panel-form-preview.png)

這只是個範例！ 探索可用的[功能](#b-form-objects-and-functions-br)以簡化工作流程，並提高表單中的資料準確度。

## 巢狀運算式 {#nestedexpressions}

規則編輯器可讓您使用多個AND和OR運運算元來建立巢狀規則。 您可以在規則中混合使用多個AND和OR運運算元。

以下是巢狀規則的範例，會在符合所需條件時，向使用者顯示有關子女監護權的資格的訊息。

![複雜運算式](assets/complexexpression.png)

您也可以拖放規則中的條件以進行編輯。 選取並將滑鼠游標停留在條件前的控制代碼（ ![控制代碼](assets/drag-handle.svg)）上。 指標變成如下所示的手形符號後，請將條件拖放至規則內的任何位置。 規則結構會變更。

![拖放](assets/drag-and-drop.png)

## 日期運算式條件 {#dateexpression}

規則編輯器可讓您使用日期比較來建立條件。

下列範例條件會在房屋已抵押時顯示靜態文字物件，使用者填寫日期欄位即表示該條件。

當使用者填寫的屬性按揭日期為過去時，最適化表單會顯示收入計算的相關備註。 下列規則會比較使用者填寫的日期與目前日期，如果使用者填寫的日期早於目前日期，則表單會顯示文字訊息（名為「收入」）。

![日期運算式條件](assets/dateexpressioncondition.png)

當填寫日期早於目前日期時，表單會顯示文字訊息（收入）如下：

![符合日期運算式條件](assets/dateexpressionconditionmet.png)

## 數字比較條件 {#number-comparison-conditions}

規則編輯器可讓您建立比較兩個數字的條件。

如果應徵者在目前地址停留的月數少於36，則會顯示靜態文字物件的範例條件如下。

![數字比較條件](assets/numbercomparisoncondition.png)

當使用者表示在目前的居住地址生活少於36個月時，表單會顯示通知，要求更多居住證明。

![已要求更多校訂](assets/additionalproofrequested.png)

<!-- ## Impact of rule editor on existing scripts {#impact-of-rule-editor-on-existing-scripts}

In [!DNL Experience Manager Forms] versions prior to [!DNL Experience Manager 6.1 Forms] feature pack 1, form authors and developers used to write expressions in the Scripts tab of the Edit component dialog to add dynamic behavior to Adaptive Forms. The Scripts tab is now replaced by the rule editor.

Any scripts or expressions that you must have written in the Scripts tab are available in the rule editor. While you cannot view or edit them in visual editor, if you are a part of the forms-power-users group you can edit scripts in code editor. -->

### 啟動表單資料模型服務 {#invoke}

假設有一項Web服務`GetInterestRates`，它會將貸款金額、保有權及申請者的信用評分當作輸入，並傳回包含EMI金額和利率的貸款計畫。 您可以使用Web服務作為資料來源來建立表單資料模型(FDM)。 您新增資料模型物件和`get`服務至表單模型。 服務會出現在表單資料模型(FDM)的「服務」標籤中。 接著，建立包含資料模型物件欄位的最適化表單，以擷取貸款金額、使用期限和信用評分的使用者輸入。 新增觸發Web服務擷取計畫詳細資料的按鈕。 輸出會填入適當的欄位中。

下列規則顯示如何設定叫用服務動作來完成範例案例。

![Example-invoke-services](assets/example-invoke-services.png)

>[!NOTE]
>
>如果輸入為陣列型別，則支援陣列的欄位會顯示在「輸出」下拉式區段下。

### 使用When規則觸發多個動作 {#triggering-multiple-actions-using-the-when-rule}

在貸款申請表單中，您想要擷取貸款申請人是否為現有客戶。 根據使用者提供的資訊，客戶ID欄位應顯示或隱藏。 此外，如果使用者是現有客戶，您想要將焦點設定在客戶ID欄位。 貸款申請表單包含下列元件：

* 單選按鈕&#x200B;**[!UICONTROL 您是現有的Geometrixx客戶嗎？]**，提供[!UICONTROL 是]和[!UICONTROL 否]選項。 「是」的值為&#x200B;**0**，「否」的值為&#x200B;**1**。

* 文字欄位&#x200B;**[!UICONTROL 客戶ID]** Geometrixx，用以指定客戶ID。

當您在選項按鈕上編寫實施此行為的When規則時，該規則在視覺規則編輯器中會顯示如下。

![When-rule-example](assets/when-rule-example.png)

在範例規則中，When區段中的陳述式是條件，當傳回True時，會執行Then區段中指定的動作。

<!-- The rule appears as follows in the code editor.

![when-rule-example-code](assets/when-rule-example-code.png) 

Rule in the code editor -->

### 在規則中使用函式輸出 {#using-a-function-output-in-a-rule}

在採購單表單中，您有下表，使用者可在其中填寫訂單。 在此表格中：

* 第一列是可重複的，因此使用者可以訂購多個產品並指定不同的數量。 它的元素名稱為`Row1`。
* 重複資料列之「產品數量」欄中的儲存格標題為「數量」。 此儲存格的元素名稱為`productquantity`。
* 表格中的第二列是不可重複的，且此列中「產品數量」欄中的儲存格標題為「總數量」。

![Example-function-table](assets/example-function-table.png)

**A.**&#x200B;列1 **B.**&#x200B;數量&#x200B;**C.**&#x200B;總數量

現在，您要在所有產品的「產品數量」欄中新增指定數量，並在「總數量」儲存格中顯示總和。 您可以在「總數量」儲存格上撰寫「設定值」規則，以達到此總和，如下所示。

![Example-function-output](assets/example-function-output.png)

### 使用運算式驗證欄位值 {#validating-a-field-value-using-expression}

在上一個範例中說明的採購單表單中，您想要限制使用者訂購超過一10000數量的產品。 若要執行此驗證，您可以編寫驗證規則，如下所示。

![Example-validate](assets/example-validate.png)

## 另請參閱

{{see-also-rule-editor}}