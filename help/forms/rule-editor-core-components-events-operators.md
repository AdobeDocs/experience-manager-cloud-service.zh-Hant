---
title: 根據核心元件的適用性表單的規則編輯器中可用的各種運運算元型別和事件有哪些？
description: 最適化Forms規則編輯器支援各種運運算元型別和事件。
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
exl-id: ac85ff04-25dc-4566-a986-90ae374bf383
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2327'
ht-degree: 2%

---

# 以核心元件為主之最適化表單的規則編輯器中的運算子和事件類型

在AEM Forms as a Cloud中，規則編輯器包含各種運運算元型別和事件，可讓您輕鬆定義和執行複雜的條件和動作。

最適化表單的規則編輯器中可用的運運算元型別，提供完善的結構來建構精確條件。 它們可讓您以邏輯且一致的方式操控資料、執行計算以及結合多個條件。 無論您是要比較值、執行算術運算或操控字串，這些運運算元都能確保您的規則既靈活又強大。

規則編輯器中的事件會作為啟動規則的觸發器。 它們定義當滿足某些條件時會發生的特定動作。 運用不同型別的事件，您可以自動回應廣泛的情境，例如使用者互動、排程時間、資料變更和系統狀態。 有了指定這些觸發器的功能，您可以建立動態且回應式規則，以符合您的特定需求。

透過瞭解並使用可用的運運算元型別和事件，您可以解鎖規則編輯器的完整潛能，這可讓您建立有效率且有效的規則，以滿足您獨特的需求並改善整體系統功能。

## 規則編輯器中可用的運運算元型別和事件 {#available-operator-types-and-events-in-rule-editor}

規則編輯器提供下列邏輯運運算元和事件，您可使用它們建立規則。

* **等於** — 檢查表單物件是否符合指定的值。
* **不等於** — 檢查表單物件是否不符合指定的值。
* **開頭為** — 檢查表單物件是否以指定的字串開頭。
* **結尾為** — 檢查表單物件是否以指定的字串結尾。
* **包含** — 檢查表單物件是否包含指定的子字串。
* **不包含** — 檢查表單物件是否不包含指定的子字串。
* **Is Empty** — 檢查表單物件是否為空白或未提供。
* **不是空的** — 檢查表單物件是否存在且不是空的。
* **已選取** — 當使用者選取特定的核取方塊、下拉式清單或選項按鈕選項時，傳回True。
* **已初始化（事件）** — 在瀏覽器中轉譯表單物件時傳回true。
* **已變更（事件）** — 當使用者修改表單物件的值或選取範圍時，傳回true。
* **已點按（事件）** — 當使用者按一下表單物件（例如按鈕）時，傳回true。 使用者可以[新增多個條件至按鈕點按](/help/forms/rule-editor-core-components-usecases.md#set-focus-to-another-panel-on-button-click-if-the-first-panel-is-valid)。
* **有效** — 檢查表單物件是否符合驗證准則。
* **無效** — 檢查表單物件是否通過驗證准則。


<!--
* **Navigation(event):** Returns true when the user clicks a navigation object. Navigation objects are used to move between panels. 
* **Step Completion(event):** Returns true when a step of a rule completes.
* **Successful Submission(event):** Returns true on successful submission of data to a form data model.
* **Error in Submission(event):**  Returns true on unsuccessful submission of data to a form data model. -->

### 規則編輯器中的可用規則型別 {#available-rule-types-in-rule-editor}

規則編輯器提供了一組預先定義的規則型別，您可以使用這些型別來撰寫規則。 讓我們來詳細瞭解一下每種規則型別。 如需有關在規則編輯器中寫入規則的詳細資訊，請參閱[寫入規則](/help/forms/rule-editor-core-components-user-interface.md#write-rules)。

#### [!UICONTROL When] {#whenruletype}

**[!UICONTROL When]**&#x200B;規則型別遵循&#x200B;**condition-action-alternate action**&#x200B;規則建構，有時只遵循&#x200B;**condition-action**&#x200B;建構。 在此規則型別中，您先指定評估條件，接著指定滿足條件時觸發的動作( `True`)。 使用When規則型別時，您可以使用多個AND和OR運運算元來建立[巢狀運算式](/help/forms/rule-editor-core-components-usecases.md#nested-expressions)。

使用When規則型別，您可以評估表單物件的條件，並對一或多個物件執行動作。

簡單地說，典型的When規則結構如下：

`When on Object A:`

`(Condition 1 AND Condition 2 OR Condition 3) is TRUE;`

`Then, do the following:`

`Action 2 on Object B;`
`AND`
`Action 3 on Object C;`

`Else, do the following:`

`Action 2 on Object C;`

當您有多值元件（如單選按鈕或清單）時，為該元件建立規則時，會自動擷取選項，並讓規則建立者可以使用這些選項。 您不需要再次輸入選項值。

例如，清單有四個選項：紅色、藍色、綠色和黃色。 建立規則時，系統會自動擷取選項（選項按鈕），供規則建立者使用，如下所示：

![多重值顯示選項](assets/multivaluefcdisplaysoptions.png)

撰寫When規則時，您可以觸發「清除值」動作。 清除值動作會清除指定物件的值。 在When陳述式中將的清除值作為選項可讓您建立具有多個欄位的複雜條件。 您可以新增Else陳述式以進一步新增條件

![清除](assets/clearvalueof.png)的值

>[!NOTE]
>
> 當規則型別僅支援單一層級then-else陳述式時。

##### [!UICONTROL When]中允許多個欄位 {#allowed-multiple-fields}

在&#x200B;**When**&#x200B;條件中，您可以選擇新增套用規則的欄位以外的其他欄位。

例如，使用When規則型別，您可以評估不同表單物件的條件並執行動作：

時間：

（物件A條件1）

和/或

（物件B條件2）

接著，執行下列動作：

物件A上的動作1

_

![在When](/help/forms/assets/allowed-multiple-field-when.png)中允許多個欄位

**在When條件功能**&#x200B;中使用允許多個欄位時的考量事項

* 請確定[核心元件設定為3.0.14版或更新版本](https://github.com/adobe/aem-core-forms-components)，以便在規則編輯器中使用此功能。
* 如果規則套用至When條件內的不同欄位，即使這些欄位中只有一個已變更，規則也會觸發。
* 您只能為&#x200B;**AND**&#x200B;規則在&#x200B;**When**&#x200B;條件中新增多個欄位。 **OR**&#x200B;規則無法執行。

>[!NOTE]
>
> 若要新增多個包含按鈕點選的條件，請確定將按鈕點選事件設為第一個條件。 例如，`When button is clicked AND text input equals '5'`有效，但不支援`When text input equals '5' AND button is clicked`。

<!--
* It is not possible to add multiple fields in the When condition while applying rules to a button.

##### To enable Allowed Multiple fields in When condition feature

Allowed Multiple fields in When condition feature is disabled by default. To enable this feature, add a custom property at the template policy:

1. Open the corresponding template associated with an Adaptive Form in the template editor.
1. Select the existing policy as **formcontainer-policy**.
1. Navigate to the **[!UICONTROL Structure]**  view and, from the **[!UICONTROL Allowed Components]** list, open the **[!UICONTROL Adaptive Forms Container]** policy.
1. Go to the **[!UICONTROL Custom Properties]** tab and to add a custom property, click **[!UICONTROL Add]**.
1. Specify the **Group Name** of your choice. For example, in our case, we added the group name as **allowedfeature**.
1. Add the **key** and **value** pair as follows:
   * key: fd:changeEventBehaviour
   * value: deps
1. Click **[!UICONTROL Done]**. -->

如果「條件」功能中允許的多個欄位發生任何問題，請遵循下列疑難排解步驟：

1. 以編輯模式開啟表單。
1. 開啟內容瀏覽器，然後選取最適化表單的&#x200B;**[!UICONTROL 指南容器]**&#x200B;元件。
1. 按一下「指引容器」屬性 ![指引屬性](/help/forms/assets/configure-icon.svg) 圖示。此時會開啟「最適化表單容器」對話框。
1. 按一下完成，然後再次儲存對話方塊。

**[!UICONTROL 隱藏]**&#x200B;隱藏指定的物件。

**[!UICONTROL 顯示]**&#x200B;顯示指定的物件。

**[!UICONTROL 啟用]**&#x200B;啟用指定的物件。

**[!UICONTROL 停用]**&#x200B;停用指定的物件。

**[!UICONTROL 啟動服務]**&#x200B;啟動表單資料模型(FDM)中設定的服務。 選擇「啟動服務」作業時，會出現一個欄位。 點選欄位時，它會顯示您[!DNL Experience Manager]執行個體上所有表單資料模型(FDM)中設定的所有服務。 選擇表單資料模型服務時，會出現更多欄位，您可在其中使用指定服務的輸入引數對應表單物件。 您可以透過指定服務的事件裝載選項對應輸出引數。 您也可以使用規則編輯器，建立處理叫用服務作業成功和失敗回應的規則。

>[!NOTE]
>
> 若要進一步瞭解Invoke服務，[請按一下這裡](/help/forms/invoke-service-enhancements-rule-editor.md)。

請參閱叫用表單資料模型(FDM)服務的規則範例。

除了「表單資料模型」服務之外，您還可以指定直接的WSDL URL來叫用Web服務。 不過，表單資料模型服務有許多優點，且建議叫用服務的方法。

如需有關在表單資料模型(FDM)中設定服務的詳細資訊，請參閱[[!DNL Experience Manager Forms] 資料整合](data-integration.md)。

**[!UICONTROL 設定值]**&#x200B;計算並設定指定物件的值。 您可以將物件值設為字串、其他物件的值、使用數學運算式或函式的計算值、物件屬性的值，或來自已設定表單資料模型服務的輸出值。 當您選擇Web服務選項時，它會顯示您[!DNL Experience Manager]執行個體上所有表單資料模型(FDM)中設定的所有服務。 選擇表單資料模型服務時，會出現更多欄位，您可在其中對應具有指定服務的輸入和輸出引數的表單物件。

如需有關在表單資料模型(FDM)中設定服務的詳細資訊，請參閱[[!DNL Experience Manager Forms] 資料整合](data-integration.md)。

**[!UICONTROL Set Property]**&#x200B;規則型別可讓您根據條件動作來設定指定物件的屬性值。 您可以將屬性設為下列其中一項：

* 可見（布林值）
* label.value （字串）
* label.visible （布林值）
* 說明（字串）
* 已啟用（布林值）
* readOnly （布林值）
* 必要（布林值）
* screenReaderText （字串）
* 有效（布林值）
* errorMessage （字串）
* 預設（數字、字串、日期）
* enumNames （字串[]）
* chartType （字串）

例如，這可讓您定義規則，以便在按一下按鈕時顯示文字方塊。 您可以使用自訂函式、表單物件、物件屬性或服務輸出來定義規則。

![設定屬性](assets/set_property_rule_new.png)

若要根據自訂函式定義規則，請從下拉式清單中選取&#x200B;**[!UICONTROL 函式輸出]**，然後從&#x200B;**[!UICONTROL 函式]**&#x200B;索引標籤中拖放自訂函式。 如果符合條件動作，文字輸入方塊就會顯示。

若要根據表單物件定義規則，請從下拉式清單中選取&#x200B;**[!UICONTROL 表單物件]**，然後從&#x200B;**[!UICONTROL 表單物件]**&#x200B;標籤中拖放表單物件。 如果符合條件動作，文字輸入方塊就會顯示在最適化表單中。

根據物件屬性的「設定屬性」規則可讓您根據最適化表單中包含的其他物件屬性，在最適化表單中顯示文字輸入方塊。

下圖是根據在最適化表單中隱藏或顯示文字方塊來動態啟用核取方塊的範例：

![物件屬性](assets/object_property_set_property_new.png)

**[!UICONTROL 清除值]**&#x200B;清除指定物件的值。

**[!UICONTROL 設定焦點]**&#x200B;將焦點設定在指定的物件上。

**[!UICONTROL 提交表單]**&#x200B;提交表單。

**[!UICONTROL 重設]**&#x200B;重設表單或指定的物件。

**[!UICONTROL 驗證]**&#x200B;驗證表單或指定的物件。

**[!UICONTROL 新增執行個體]**&#x200B;新增指定之可重複面板或表格列的執行個體。

**[!UICONTROL 移除執行個體]**&#x200B;移除指定之可重複面板或表格列的執行個體。

**[!UICONTROL 函式輸出]**&#x200B;根據預先定義的函式或自訂函式定義規則。

**[!UICONTROL 導覽至]**&#x200B;導覽至其他最適化Forms、影像或檔案片段等其他資產，或外部URL。<!-- For more information, see [Add button to the Interactive Communication](create-interactive-communication.md#addbuttontothewebchannel). -->

**[!UICONTROL 分派事件]**&#x200B;根據預先定義的條件或事件觸發特定動作或行為。

#### [!UICONTROL 設定值] {#set-value-of}

**[!UICONTROL 規則型別的]**&#x200B;設定值可讓您依據指定的條件是否符合，來設定表單物件的值。 值可以設定為另一個物件的值、常值字串、衍生自數學運算式或函式的值、另一個物件的屬性值，或表單資料模型服務的輸出。 同樣地，您可以檢查元件、字串、屬性或衍生自函式或數學運算式的值的條件。

**Set Value Of**&#x200B;規則型別不適用於所有表單物件，例如面板和工具列按鈕。 標準的「設定值」規則具有以下結構：

將物件A的值設為：

（字串ABC）或
（物件C的物件屬性X）或
（函式中的值） OR
（數學運算式的值） OR
（資料模型服務的輸出值）；

當（選擇性）：

（條件1和條件2和條件3）為TRUE；

下列範例選取`Question2`的值做為`True`，並將`Result`的值設定為`correct`。

![Set-value-web-service](assets/set-value-web-service.png)

使用表單資料模型服務的設定值規則範例。

#### [!UICONTROL 節目] {#show}

使用&#x200B;**[!UICONTROL 顯示]**&#x200B;規則型別，您可以撰寫規則來根據條件是否滿足來顯示或隱藏表單物件。 Show規則型別也會觸發Hide動作，以防條件未滿足或傳回`False`。

典型的Show規則結構如下：

`Show Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Hide Object A;`

#### [!UICONTROL 隱藏] {#hide}

與「顯示」規則型別類似，您可以使用&#x200B;**[!UICONTROL 隱藏]**&#x200B;規則型別，根據是否符合條件來顯示或隱藏表單物件。 Hide規則型別也會觸發Show動作，以防條件不滿足或傳回`False`。

典型的「隱藏」規則結構如下：

`Hide Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Show Object A;`

#### [!UICONTROL 啟用] {#enable}

**[!UICONTROL 啟用]**&#x200B;規則型別可讓您根據條件是否滿足來啟用或停用表單物件。 Enable規則型別也會觸發Disable動作，以防條件不滿足或傳回`False`。

典型的Enable規則結構如下：

`Enable Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Disable Object A;`

#### [!UICONTROL 停用] {#disable}

與「啟用」規則型別類似，**[!UICONTROL 停用]**&#x200B;規則型別可讓您根據條件是否滿足來啟用或停用表單物件。 Disable規則型別也會觸發Enable動作，以防條件不滿足或傳回`False`。

典型的「停用」規則結構如下：

`Disable Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Enable Object A;`

#### [!UICONTROL 驗證] {#validate}

**[!UICONTROL Validate]**&#x200B;規則型別使用運算式來驗證欄位中的值。 例如，您可以撰寫運算式來檢查指定名稱的文字方塊是否不包含特殊字元或數字。

典型的驗證規則結構如下：

`Validate Object A;`

`Using:`

`(Expression 1 AND Expression 2 AND Expression 3) is TRUE;`

>[!NOTE]
>
>如果指定的值不符合驗證規則，您可以向使用者顯示驗證訊息。 您可以在側邊欄中元件屬性的&#x200B;**[!UICONTROL 指令碼驗證訊息]**&#x200B;欄位中指定訊息。

![指令碼驗證](assets/script-validation.png)

#### [!UICONTROL 在面板之間導覽]

**[!UICONTROL 在面板之間導覽]**&#x200B;規則型別可讓您在表單的不同面板之間切換焦點。 例如，您可以建立運算式，將焦點移至下一個面板。

在面板之間導覽&#x200B;**會將焦點移至下一個面板的規則，其結構如下：**

`Navigate among the panels`

`Shift focus to the next item Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

同樣地，您可以撰寫&#x200B;**在面板之間導覽**&#x200B;將焦點移至上一個面板的規則：

`Navigate among the panels`

`Shift focus to the previous item Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

如需有關如何建立規則以在面板中導覽的詳細資訊，[請按一下這裡](/help/forms/rule-editor-core-components-usecases.md#navigating-between-panels-using-buttons)。

#### [!UICONTROL 非同步函式呼叫]

<span class="preview">這是一項預先發佈功能，可透過我們的[預先發佈管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=zh-Hant#new-features)存取。</span>

**[!UICONTROL 非同步函式呼叫]**&#x200B;規則型別可讓您執行非同步函式。 它可讓您啟動獨立於主要執行緒運作的函式呼叫，讓其他處理程式繼續執行，而不需要等候非同步函式完成。

用來執行非同步函式的典型Async函式呼叫規則的結構如下：

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Async Function call`

`[Callback Function];`

如需如何在視覺規則編輯器中使用非同步函式呼叫的詳細資訊，請參閱規則編輯器[中的](/help/forms/using-async-funct-in-rule-editor.md)使用非同步函式呼叫一文。

<!--
### [!UICONTROL Set Options Of] {#setoptionsof}

The **[!UICONTROL Set Options Of]** rule type enables you to define rules to add check boxes dynamically to the Adaptive Form. You can use a Form Data Model or a custom function to define the rule.

To define a rule based on a custom function, select **[!UICONTROL Function Output]** from the drop-down list, and drag-and-drop a custom function from the **[!UICONTROL Functions]** tab. The number of checkboxes defined in the custom function are added to the Adaptive Form.

![Custom Functions](assets/custom_functions_set_options_new.png)

To create a custom function, see [custom functions in rule editor](#custom-functions).

To define a rule based on a form data model:

1. Select **[!UICONTROL Service Output]** from the drop-down list.
1. Select the data model object.
1. Select a data model object property from the **[!UICONTROL Display Value]** drop-down list. The number of checkboxes in the Adaptive Form is derived from the number of instances defined for that property in the database.
1. Select a data model object property from the **[!UICONTROL Save Value]** drop-down list.

![FDM set options](assets/fdm_set_options_new.png) -->

## 下一步

讓我們現在瞭解根據核心元件[的最適化表單的規則編輯器的各種](/help/forms/rule-editor-core-components-usecases.md)範例。

## 另請參閱

{{see-also-rule-editor}}
