---
title: 本文概述根據核心元件在最適化表單中規則編輯器的各種使用案例。
description: 本文概述根據核心元件在最適化表單中規則編輯器的各種使用案例。
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
exl-id: 8191e113-f768-4b1e-a191-e3c722f19054
source-git-commit: e10451553692b6ad957421783e176409b36b642b
workflow-type: tm+mt
source-wordcount: '1561'
ht-degree: 0%

---

# 規則編輯器的不同使用案例

本文提供根據核心元件之最適化表單的規則編輯器詳細範例，深入瞭解其針對不同情境的正確實施。 規則編輯器可讓開發人員定義和管理控制表單行為的邏輯。
現在，讓我們討論規則編輯器的不同實作。

## 如果第一個面板有效，請按一下按鈕時將焦點設定為另一個面板

<span class="preview">這是一項預先發佈功能，可透過我們的[預先發佈管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=zh-Hant#new-features)存取。</span>

規則編輯器可讓您驗證面板版面，例如「水準標籤」、「垂直標籤」、「摺疊式面板」或「精靈」，只要按一下按鈕，即可在另一個面板中將焦點設定為表單物件。 您可以使用此功能來改善表單導覽和使用者體驗。

想像使用精靈版面配置的多步驟應用程式表單。 您必須先完成`Personal Information`面板，才能移至`Employment Details`。 當您按一下「`Next`」按鈕時，規則編輯器會驗證`Personal Information`面板。 如果所有必填欄位都填寫正確，表單會自動將焦點移至`Employment Details`面板。 否則，它會顯示錯誤訊息，提示使用者完成缺少的欄位。

您可以在`Next`按鈕上建立規則以驗證第一個面板：

![下一個按鈕的規則](/help/forms/assets/next-rule.png){width=50%}

當您按一下&#x200B;**下一步**&#x200B;按鈕時，**個人資訊**&#x200B;面板就會驗證。 如果輸入的詳細資料正確無誤，焦點會移至&#x200B;**帳戶安全性**&#x200B;面板；否則，錯誤訊息會提示您填寫遺漏的詳細資訊。

>[!VIDEO](https://video.tv.adobe.com/v/3457767)


## 使用按鈕在面板之間導覽

規則編輯器可讓您將導覽按鈕新增至面板版面，例如「水準標籤」、「垂直標籤」、「摺疊式功能表」或「精靈」。 這些按鈕透過簡化表單中不同面板之間的轉換，將焦點移至所選面板，來增強使用者體驗。

想像您正在與應用程式的設定檔設定區段互動，其中導覽是由按鈕而非索引標籤來協助。 從主儀表板進入設定檔設定時，您會遇到一系列專為其設定檔不同層面的面板： **個人資訊**、**帳戶安全性**&#x200B;和&#x200B;**通知偏好設定**。

每個面板都包含更新特定資訊的相關欄位和選項。 導覽按鈕（例如`Next`和`Back`）位於顯眼位置，可讓您在這些面板之間移動。 按一下`Next`將使用者推進至&#x200B;**帳戶安全性**&#x200B;面板，然後按一下`Back`返回&#x200B;**個人資訊**&#x200B;面板。 此導覽方法可確保區段之間的無縫轉換，而不會失去內容，提供順暢且直覺的使用者體驗。 使用導覽按鈕可簡化管理設定檔設定的程式，讓互動更加有組織且方便使用。

您可以使用`Navigate among the panels`規則，為允許在不同面板之間切換的按鈕建立導覽規則。  選取`Shift focus to the next item`屬性，將焦點移至版面配置中的下一個面板。

![下一個面板規則](/help/forms/assets/rule-editor-navigate-in-panel-next.png){width=50%}

按一下`Next`按鈕時，焦點會移至配置中的後續面板。

![使用[下一步]按鈕在面板中導覽](/help/forms/assets/navigate-in-panel.gif)

同樣地，您可以建立`Previous`按鈕的規則，將焦點移至前一個面板。

![上一個面板規則](/help/forms/assets/rule-editor-navigate-in-panel-previous.png){width=50%}

## 在具有函式的可重複面板中簡化複雜的計算

規則編輯器可讓您直接在可重複面板中的欄位上使用現成可用的函式，例如Sum、Min、Max和Join。 您也可以將可重複的面板欄位值傳遞至接受數字陣列、字串陣列、布林陣列等的函式。 這開啟了強大的自動化功能，讓您無需自訂程式碼即可實施複雜的商業邏輯。

想像一個具有可重複面板的表單，其中每個面板執行個體都會收集有關資產宣告值的資訊。

![可重複的表單](/help/forms/assets/ootb-function-support-repeatable-panel-form.png)

您可以使用`Sum`函式自動計算所有面板的總資產值，而不需要手動計算，並降低發生錯誤的可能性。

![支援OOTB函式中的可重複面板欄位](/help/forms/assets/ootb-function-support-repeatable-panel.png)

當您填寫表單並新增執行個體以宣告資產值時，`Calculate Asset Value`按鈕會計算所有已宣告資產值的總和，並在`assetvalue`文字方塊中顯示結果。

![支援OOTB函式中的可重複面板欄位](/help/forms/assets/ootb-function-support-repeatable-panel-form-preview.png)

>[!NOTE]
>
> 如果可重複面板欄位的值傳遞至不接受陣列的函式，則可重複面板的最後一個執行個體的欄位值傳遞至函式。

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

* 選項按鈕&#x200B;**[!UICONTROL 您是Geometrixx現有客戶嗎？]**，提供[!UICONTROL 是]和[!UICONTROL 否]選項。 「是」的值為&#x200B;**0**，「否」的值為&#x200B;**1**。

* 用於指定客戶ID的文字欄位&#x200B;**[!UICONTROL Geometrixx客戶ID]**。

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
