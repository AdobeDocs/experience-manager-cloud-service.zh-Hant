---
title: 如何使用適用性Forms規則編輯器？
description: 適用性Forms規則編輯器可讓您新增動態行為，並將複雜邏輯建置至表單中，而不需編碼或編寫指令碼。 開始了解選擇規則結構的規則和准則。 進一步了解規則編輯器中可用的運算子類型和事件。
feature: Adaptive Forms
role: User
level: Beginner, Intermediate
exl-id: 6fd38e9e-435e-415f-83f6-3be177738c00
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '6340'
ht-degree: 0%

---

# 新增規則至適用性表單 {#adaptive-forms-rule-editor}

## 概覽 {#overview}

規則編輯器功能可讓表單業務使用者和開發人員在適用性表單物件上撰寫規則。 這些規則會根據預設條件、使用者輸入和表單上的使用者動作，定義要在表單物件上觸發的動作。 它有助於進一步簡化表單填寫體驗，確保準確性和速度。

規則編輯器提供直覺且簡化的使用者介面，可編寫規則。 規則編輯器為所有使用者提供視覺編輯器。<!-- In addition, only for forms power users, rule editor provides a code editor to write rules and scripts. --> 您可以使用規則對適用性表單物件執行的一些關鍵動作為：

* 顯示或隱藏對象
* 啟用或禁用對象
* 為對象設定值
* 驗證物件的值
* 執行函式以計算對象的值
* 調用表單資料模型服務並執行操作
* 設定對象的屬性

<!-- Rule editor replaces the scripting capabilities in [!DNL Experience Manager 6.1 Forms] and earlier releases. However, your existing scripts are preserved in the new rule editor. For more information about working with existing scripts in the rule editor, see [Impact of rule editor on existing scripts](rule-editor.md#p-impact-of-rule-editor-on-existing-scripts-p). -->

新增至Forms-power-users群組的使用者可以建立指令碼並編輯現有的指令碼。 中的使用者 [!DNL forms-users] 群組可以使用指令碼，但無法建立或編輯指令碼。

## 了解規則 {#understanding-a-rule}

規則是動作和條件的組合。 在規則編輯器中，動作包括隱藏、顯示、啟用、停用或計算表單中物件的值等活動。 條件是布林運算式，通過對表單對象的狀態、值或屬性執行檢查和操作來評估。 動作會根據值( `True` 或 `False`)，透過評估條件傳回。

規則編輯器提供一組預先定義的規則類型，例如「時間」、「顯示」、「隱藏」、「啟用」、「停用」、「設定值」和「驗證」，以協助您編寫規則。 每個規則類型都可讓您定義規則中的條件和動作。 本檔案進一步詳細說明每種規則類型。

規則通常遵循下列其中一個結構：

**條件 — 動作** 在此結構中，規則會先定義條件，接著定義要觸發的動作。 此結構可與寫程式語言中的if-then陳述式比較。

在規則編輯器中， **當** 規則類型可強制執行條件 — 動作結構。

**動作條件** 在此結構中，規則會先定義要觸發的動作，接著定義評估的條件。 此結構的另一個變數是action-condition-alternate動作，也定義了條件傳回False時要觸發的替代動作。

規則編輯器中的「顯示」、「隱藏」、「啟用」、「禁用」、「設定值」和「驗證」規則類型強制實施action-condition規則結構。 預設情況下，「顯示」的替代操作為「隱藏」，「啟用」的替代操作為「禁用」，相反。 不能更改預設替代操作。

>[!NOTE]
>
>可用的規則類型，包括您在規則編輯器中定義的條件和動作，也取決於您要建立規則的表單物件類型。 規則編輯器僅顯示有效的規則類型和選項，用於編寫特定表單對象類型的條件和操作語句。 例如，您沒有看到面板物件的「驗證」、「設定值」、「啟用」和「停用」規則類型。

如需規則編輯器中可用規則類型的詳細資訊，請參閱 [規則編輯器中可用的規則類型](rule-editor.md#p-available-rule-types-in-rule-editor-p).

### 選擇規則結構的准則 {#guidelines-for-choosing-a-rule-construct}

雖然您可以使用任何規則結構來達到大部分的使用案例，但以下提供一些准則以供您選擇一個結構而非另一個結構。 如需規則編輯器中可用規則的詳細資訊，請參閱 [規則編輯器中可用的規則類型](rule-editor.md#p-available-rule-types-in-rule-editor-p).

* 建立規則時，一般的經驗法則是在您要撰寫規則的物件內容中加以思考。 請考慮您要根據用戶在欄位A中指定的值來隱藏或顯示欄位B。在此情況下，您正在評估欄位A上的條件，並根據它返回的值，您將觸發欄位B上的操作。

   因此，如果您要在欄位B上撰寫規則（您要評估條件的物件），請使用condition-action結構或When規則類型。 同樣地，請使用action-condition結構，或在欄位A上使用Show或Hide規則類型。

* 有時，您必鬚根據一個條件執行多個動作。 在這種情況下，建議使用條件 — 動作結構。 在此結構中，您可以評估條件一次，並指定多個動作陳述式。

   例如，要根據條件來隱藏欄位B、C和D，以檢查用戶在欄位A中指定的值，請使用條件 — 操作結構或當欄位A上的規則類型編寫一個規則，並指定操作來控制欄位B、C和D的可見性。否則，您需要在欄位B、C和D上使用三個不同的規則，其中每個規則都檢查條件，並顯示或隱藏相應的欄位。 在此示例中，在一個對象上編寫「當」規則類型比在三個對象上顯示或隱藏規則類型更有效。

* 若要根據多個條件觸發動作，建議使用action-condition建構。 例如，要通過評估欄位B、C和D上的條件來顯示和隱藏欄位A，請在欄位A上使用「顯示」或「隱藏」規則類型。
* 如果規則包含一個條件的動作，請使用條件 — 動作或動作條件結構。
* 如果規則檢查條件，並在提供欄位中的值或退出欄位時立即執行動作，建議在評估條件的欄位上使用condition-action結構或When規則類型來編寫規則。
* 當用戶更改應用了When規則的對象的值時，將評估When規則中的條件。 不過，如果您想要在值在伺服器端變更時觸發動作，例如預先填入值，建議您撰寫當欄位初始化時觸發動作的「時間」規則。
* 在編寫下拉清單、單選按鈕或複選框對象的規則時，這些表單對象的選項或值在規則編輯器中預先填充。

## 規則編輯器中可用的運算子類型和事件 {#available-operator-types-and-events-in-rule-editor}

規則編輯器提供下列邏輯運算子和事件，您可使用這些運算子和事件建立規則。

* **等於**
* **不等於**
* **開頭為**
* **結尾為**
* **包含**
* **為空**
* **不為空**
* **已選取：** 當使用者為核取方塊、下拉式清單、選項按鈕選取特定選項時，會傳回true。
* **已初始化（事件）:** 表單物件在瀏覽器中轉譯時傳回true。
* **已變更（事件）:** 當使用者變更表單物件的輸入值或選取的選項時，會傳回true。
* **導覽(event):** 當使用者按一下導覽物件時，會傳回true。 導覽物件可用於在面板之間移動。
* **步驟完成（事件）:** 規則的步驟完成時傳回true。
* **成功提交(event):** 成功將資料提交至表單資料模型時傳回true。
* **提交(event)中出錯：**  將資料提交至表單資料模型失敗時傳回true。

## 規則編輯器中可用的規則類型 {#available-rule-types-in-rule-editor}

規則編輯器提供一組預先定義的規則類型，您可用來編寫規則。 讓我們詳細查看每個規則類型。 如需在規則編輯器中撰寫規則的詳細資訊，請參閱 [寫入規則](rule-editor.md#p-write-rules-p).

### [!UICONTROL 時間] {#whenruletype}

此 **[!UICONTROL 當]** 規則類型遵循 **condition-action-alternate動作** 規則構造，有時只是 **condition-action** 建構。 在此規則類型中，您會先指定評估的條件，然後在滿足條件時觸發動作( `True`)。 使用When規則類型時，您可以使用多個AND和OR運算子來建立 [嵌套表達式](#nestedexpressions).

使用「時間」(When)規則類型，可以評估表單對象上的條件，並對一個或多個對象執行操作。

簡單來說，典型的「當時」規則的結構如下：

`When on Object A:`

`(Condition 1 AND Condition 2 OR Condition 3) is TRUE;`

`Then, do the following:`

對象B上的操作2;對對象C採取AND動作3;

_

如果您有多值元件（如選項按鈕或清單），則在為該元件建立規則時，系統會自動擷取選項，並供規則建立者使用。 您不需要再次輸入選項值。

例如，清單有四個選項：紅、藍、綠、黃。 建立規則時，會自動擷取選項（選項按鈕），並讓規則建立者使用，如下所示：

![多值顯示選項](assets/multivaluefcdisplaysoptions.png)

撰寫「時間」規則時，您可以觸發「清除值」動作。 「清除值」(Clear Value Of)操作會清除指定對象的值。 在When語句中將「清除值」(Clear Value)設定為選項，允許您使用多個欄位建立複雜條件。

![清除值](assets/clearvalueof.png)

**[!UICONTROL 隱藏]** 隱藏指定的對象。

**[!UICONTROL 顯示]** 顯示指定的對象。

**[!UICONTROL 啟用]** 啟用指定的對象。

**[!UICONTROL 停用]** 禁用指定的對象。

**[!UICONTROL 調用服務]** 調用在表單資料模型中配置的服務。 選擇「調用服務」操作時，將顯示一個欄位。 點選欄位時，它會顯示您 [!DNL Experience Manager] 例項。 選擇「表單資料模型」服務時，將顯示更多欄位，您可在其中使用指定服務的輸入和輸出參數映射表單對象。 請參閱叫用表單資料模型服務的範例規則。

除了表單資料模型服務外，還可以指定直接WSDL URL來調用Web服務。 但是，表單資料模型服務有許多優點，並且建議使用叫用服務的方法。

如需在表單資料模型中設定服務的詳細資訊，請參閱 [[!DNL Experience Manager Forms] 資料整合](data-integration.md).

**[!UICONTROL 設定值]** 計算並設定指定對象的值。 您可以將對象值設定為字串、另一個對象的值、使用數學表達式或函式的計算值、對象的屬性值或配置的表單資料模型服務的輸出值。 當您選擇Web服務選項時，它會顯示您 [!DNL Experience Manager] 例項。 選擇「表單資料模型」服務時，將顯示更多欄位，您可在其中使用指定服務的輸入和輸出參數映射表單對象。

如需在表單資料模型中設定服務的詳細資訊，請參閱 [[!DNL Experience Manager Forms] 資料整合](data-integration.md).

此 **[!UICONTROL 設定屬性]** 規則類型可讓您根據條件動作來設定指定物件之屬性的值。

它可讓您定義規則，以動態方式將核取方塊新增至適用性表單。 您可以使用自訂函式、表單物件或物件屬性來定義規則。

![設定屬性](assets/set_property_rule_new.png)

若要根據自訂函式定義規則，請選取 **[!UICONTROL 函式輸出]** 從下拉式清單中，並從 **[!UICONTROL 函式]** 標籤。 如果符合條件動作，則自訂函式中定義的核取方塊數會新增至適用性表單。

若要根據表單物件定義規則，請選取 **[!UICONTROL 表單物件]** 從下拉式清單中，並從 **[!UICONTROL 表單物件]** 標籤。 如果符合條件動作，則表單物件中定義的核取方塊數會新增至適用性表單。

基於對象屬性的設定屬性規則允許您根據包含在適用性表單中的另一個對象屬性在適用性表單中添加複選框的數量。

下圖說明根據適用性表單中的下拉式清單數目動態新增核取方塊的範例：

![物件屬性](assets/object_property_set_property_new.png)

**[!UICONTROL 清除值]** 清除指定對象的值。

**[!UICONTROL 設定焦點]** 將焦點設定在指定的對象上。

**[!UICONTROL 保存表單]** 保存表單。

**[!UICONTROL 提交Forms]** 提交表格。

**[!UICONTROL 重設表單]** 重設表單。

**[!UICONTROL 驗證表單]** 驗證表單。

**[!UICONTROL 新增例項]** 添加指定的可重複面板或表行的實例。

**[!UICONTROL 刪除實例]** 刪除指定的可重複面板或表行的實例。

**[!UICONTROL 導覽至]** 導覽至其他 <!--Interactive Communications,--> 適用性Forms、影像或檔案片段等其他資產，或外部URL。 <!-- For more information, see [Add button to the Interactive Communication](create-interactive-communication.md#addbuttontothewebchannel). -->

### [!UICONTROL 設定下列項目的值: ] {#set-value-of}

此 **[!UICONTROL 設定值]** 規則類型可讓您根據是否滿足指定條件來設定表單物件的值。 該值可以設定為另一個對象的值、常值字串、從數學表達式或函式導出的值、另一個對象的屬性的值或表單資料模型服務的輸出。 同樣地，您也可以檢查元件、字串、屬性，或從函式或數學運算式衍生的值上的條件。

此 **設定值為** 規則類型不適用於所有表單物件，例如面板和工具列按鈕。 規則的標準設定值具有下列結構：

將對象A的值設定為：

（字串ABC）OR（物件C的物件屬性X）OR（函式的值）OR（數學運算式的值）OR（資料模型服務或Web服務的輸出值）;

時機（選用）:

（條件1、條件2、條件3）為TRUE;

下列範例會將值擷取至 `dependentid` 欄位作為輸入，並設定 `Relation` 欄位至 `Relation` 的引數 `getDependent` 表單資料模型服務。

![Set-value-web-service](assets/set-value-web-service.png)

使用表單資料模型服務設定值規則的範例

>[!NOTE]
>
>此外，您也可以使用「設定規則的值」，從表單資料模型服務或網站服務的輸出，填入下拉式清單元件中的所有值。 不過，請確定您選擇的輸出引數為陣列類型。 陣列中傳回的所有值都可在指定的下拉式清單中使用。

### [!UICONTROL 顯示] {#show}

使用 **[!UICONTROL 顯示]** 規則類型，您可以撰寫規則以根據是否滿足條件來顯示或隱藏表單物件。 若不滿足或傳回條件，「顯示」規則類型也會觸發「隱藏」動作 `False`.

典型的「顯示」規則的結構如下：

`Show Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Hide Object A;`

### [!UICONTROL 隱藏] {#hide}

與「顯示」規則類型類似，您可以使用 **[!UICONTROL 隱藏]** 規則類型，根據是否滿足條件來顯示或隱藏表單物件。 隱藏規則類型也會在條件不滿足或傳回時觸發顯示動作 `False`.

典型的隱藏規則結構如下：

`Hide Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Show Object A;`

### [!UICONTROL 啟用] {#enable}

此 **[!UICONTROL 啟用]** 規則類型可讓您根據是否滿足條件來啟用或停用表單物件。 若不滿足或傳回條件，「啟用」規則類型也會觸發「停用」動作 `False`.

一般的「啟用」規則的結構如下：

`Enable Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Disable Object A;`

### [!UICONTROL 停用] {#disable}

與「啟用」規則類型類似， **[!UICONTROL 停用]** 規則類型可讓您根據是否滿足條件來啟用或停用表單物件。 若不滿足或傳回條件，「停用」規則類型也會觸發「啟用」動作 `False`.

典型的「停用」規則的結構如下：

`Disable Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Enable Object A;`

### [!UICONTROL 驗證] {#validate}

此 **[!UICONTROL 驗證]** 規則類型會使用運算式來驗證欄位中的值。 例如，您可以撰寫運算式來檢查用於指定名稱的文字方塊是否不包含特殊字元或數字。

典型的驗證規則結構如下：

`Validate Object A;`

`Using:`

`(Expression 1 AND Expression 2 AND Expression 3) is TRUE;`

>[!NOTE]
>
>如果指定的值不符合驗證規則，您可以向使用者顯示驗證訊息。 您可以在 **[!UICONTROL 指令碼驗證消息]** 欄位（位於側欄的元件屬性中）。

![指令碼驗證](assets/script-validation.png)

### [!UICONTROL 設定選項] {#setoptionsof}

此 **[!UICONTROL 設定選項]** 規則類型可讓您定義規則，以動態方式將核取方塊新增至適用性表單。 您可以使用表單資料模型或自訂函式來定義規則。

若要根據自訂函式定義規則，請選取 **[!UICONTROL 函式輸出]** 從下拉式清單中，並從 **[!UICONTROL 函式]** 標籤。 自訂函式中定義的核取方塊數會新增至適用性表單。

![自訂函式](assets/custom_functions_set_options_new.png)

若要建立自訂函式，請參閱 [規則編輯器中的自訂函式](#custom-functions).

若要根據表單資料模型定義規則：

1. 選擇 **[!UICONTROL 服務輸出]** 從下拉式清單中。
1. 選取資料模型物件。
1. 從 **[!UICONTROL 顯示值]** 下拉式清單。 適用性表單中的核取方塊數目衍生自資料庫中針對該屬性定義的例項數目。
1. 從 **[!UICONTROL 儲存值]** 下拉式清單。

![FDM設定選項](assets/fdm_set_options_new.png)

## 了解規則編輯器使用者介面 {#understanding-the-rule-editor-user-interface}

規則編輯器提供完整且簡單的使用者介面，可編寫及管理規則。 您可以以製作模式從適用性表單內啟動規則編輯器使用者介面。

若要啟動規則編輯器使用者介面：

1. 在製作模式中開啟最適化表單。
1. 點選您要為其編寫規則的表單物件，然後在「元件工具列」中點選 ![編輯規則](assets/edit-rules-icon.svg). 規則編輯器使用者介面隨即顯示。

   ![建立規則](assets/create-rules.png)

   此視圖將列出選定表單對象上的任何現有規則。 如需管理現有規則的詳細資訊，請參閱 [管理規則](rule-editor.md#p-manage-rules-p).

1. 點選 **[!UICONTROL 建立]** 來撰寫新規則。 規則編輯器使用者介面的視覺編輯器在您首次啟動規則編輯器時，會預設開啟。

   ![規則編輯器UI](assets/rule-editor-ui.png)

讓我們詳細查看規則編輯器UI的每個元件。

### A.元件規則顯示 {#a-component-rule-display}

顯示您啟動規則編輯器時所使用的適用性表單物件標題，以及目前選取的規則類型。 在上例中，規則編輯器從標題為Salary的適用性表單物件啟動，而選取的規則類型為When。

### B.表單對象和職能 {#b-form-objects-and-functions-br}

規則編輯器使用者介面左側的窗格包含兩個標籤： **[!UICONTROL Forms物件]** 和 **[!UICONTROL 函式]**.

「表單對象」頁簽顯示「適用性表單」中包含的所有對象的分層視圖。 它顯示對象的標題和類型。 撰寫規則時，您可以將表單物件拖放至規則編輯器。 在將物件或函式拖放至預留位置時建立或編輯規則時，預留位置會自動取用適當的值類型。

已應用一個或多個有效規則的表單對象標籤為綠色圓點。 如果應用於表單對象的任何規則無效，則表單對象將標籤為黃色圓點。

「函式」索引標籤包含一組內建函式，例如「總和」、「最小值」、「最大值」、「平均值」、「數量」和「驗證表單」。 您可以使用這些函式來計算可重複面板和表格列中的值，並在撰寫規則時於動作和條件陳述式中使用這些值。 不過，您可以建立 [自訂函式](#custom-functions) 也是。

![函式頁簽](assets/functions.png)

>[!NOTE]
>
>您可以在「Forms對象和函式」頁簽中對對象和函式名稱和標題執行文本搜索。

在表單對象的左樹中，可以點選表單對象以顯示應用於每個對象的規則。 您不僅可以瀏覽各種表單物件的規則，還可以在表單物件之間複製貼上規則。 如需詳細資訊，請參閱 [複製貼上規則](rule-editor.md#p-copy-paste-rules-p).

### C.表單對象和函式切換 {#c-form-objects-and-functions-toggle-br}

切換按鈕在點選時切換表單對象和函式窗格。

### D.可視化規則編輯器 {#visual-rule-editor}

可視化規則編輯器是規則編輯器用戶介面的可視化編輯器模式中您在其中編寫規則的區域。 它可讓您選取規則類型，並據以定義條件和動作。 在規則中定義條件和動作時，您可以從「表單對象和函式」窗格拖放表單對象和函式。

如需使用可視化規則編輯器的詳細資訊，請參閱 [寫入規則](rule-editor.md#p-write-rules-p).
<!-- 
### E. Visual-code editors switcher {#e-visual-code-editors-switcher}

Users in the forms-power-users group can access code editor. For other users, code editor is not available. If you have the rights, you can switch from visual editor mode to code editor mode of the rule editor, and vice versa, using the switcher right above the rule editor. When you launch rule editor the first time, it opens in the visual editor mode. You can write rules in the visual editor mode or switch to the code editor mode to write a rule script. However, note that if you modify a rule or write a rule in code editor, you cannot switch back to the visual editor for that rule unless you clear the code editor.

[!DNL Experience Manager Forms] tracks the rule editor mode you used last to write a rule. When you launch the rule editor next time, it opens in that mode. However, you can also configure a default mode to open the rule editor in the specified mode. To do so:

1. Go to [!DNL Experience Manager] web console at `https://[host]:[port]/system/console/configMgr`.
1. Click to edit **[!UICONTROL Adaptive Form Configuration Service]**.
1. choose **[!UICONTROL Visual Editor]** or **[!UICONTROL Code Editor]** from the **[!UICONTROL Default Mode for Rule Editor]** drop-down

1. Click **[!UICONTROL Save]**.
-->

### E.完成和取消按鈕 {#done-and-cancel-buttons}

此 **[!UICONTROL 完成]** 按鈕來儲存規則。 您可以儲存不完整的規則。 但是，不完整無效且未執行。 下次從相同表單物件啟動規則編輯器時，會列出表單物件上儲存的規則。 您可以在該檢視中管理現有規則。 如需詳細資訊，請參閱 [管理規則](rule-editor.md#p-manage-rules-p).

此 **[!UICONTROL 取消]** 按鈕會捨棄您對規則所做的任何變更，並關閉規則編輯器。

## 寫入規則 {#write-rules}

您可以使用可視化規則編輯器編寫規則 &lt;!> — 或代碼編輯器>。 第一次啟動規則編輯器時，會以視覺編輯器模式開啟規則編輯器。 您可以切換至程式碼編輯器模式並撰寫規則。 不過，如果您在程式碼編輯器中撰寫或修改規則，則無法切換至該規則的視覺編輯器，除非您清除程式碼編輯器。 下次啟動規則編輯器時，它會以您上次用來建立規則的模式開啟。

先來看看如何使用視覺編輯器撰寫規則。

### 使用視覺編輯器 {#using-visual-editor}

讓我們使用下列範例表單，了解如何在視覺化編輯器中建立規則。

![Create-rule-example](assets/create-rule-example.png)

貸款申請表示例中的「貸款要求」部分要求申請人指定其婚姻狀況、薪金，如果已婚，其配偶的薪金。 此規則會根據用戶輸入計算貸款資格金額，並顯示在「貸款資格」欄位中。 套用下列規則以實作案例：

* 只有在婚姻狀況已婚時，才顯示「配偶的薪金」欄位。
* 貸款資格金額是薪金總額的50%。

要編寫規則，請執行以下步驟：

1. 首先，根據用戶為「婚姻狀態」單選按鈕選擇的選項，編寫規則以控制「配偶薪金」欄位的可見性。

   以編寫模式開啟貸款申請表。 點選 **[!UICONTROL 婚姻狀況]** 元件與分接器 ![編輯規則](assets/edit-rules-icon.svg). 下一步，點選 **[!UICONTROL 建立]** 來啟動規則編輯器。

   ![write-rules-visual-editor-1](assets/write-rules-visual-editor-1.png)

   啟動規則編輯器時，預設會選取「時間」規則。 此外，在When語句中指定了啟動規則編輯器時的表單對象（在本例中是婚姻狀態）。

   雖然您無法更改或修改所選對象，但可以使用規則下拉式清單（如下所示）選擇其他規則類型。 如果您想要在另一個物件上建立規則，請點選「取消」以退出規則編輯器，然後從所需的表單物件重新啟動。

1. 點選 **[!UICONTROL 選擇狀態]** 下拉式清單並選取 **[!UICONTROL 等於]**. 此 **[!UICONTROL 輸入字串]** 欄位。

   ![write-rules-visual-editor-2](assets/write-rules-visual-editor-2.png)

   在「婚姻狀況」單選按鈕中， **[!UICONTROL 已婚]** 和 **[!UICONTROL 單一]** 已指派選項 **0** 和 **1** 值。 您可以驗證「編輯」選項按鈕對話框的「標題」頁簽中的分配值，如下所示。

   ![來自規則編輯器的選項按鈕值](assets/radio-button-values.png)

1. 在 **[!UICONTROL 輸入字串]** 欄位，指定 **0**.

   ![write-rules-visual-editor-4](assets/write-rules-visual-editor-4.png)

   您已將條件定義為 `When Marital Status is equal to Married`. 接下來，定義若此條件為True，則要執行的動作。

1. 在Then陳述式中，選取 **[!UICONTROL 顯示]** 從 **[!UICONTROL 選擇操作]** 下拉式清單。

   ![write-rules-visual-editor-5](assets/write-rules-visual-editor-5.png)

1. 拖放 **[!UICONTROL 配偶薪金]** 欄位(位於 **[!UICONTROL 拖放對象或在此處選擇]** 欄位。 或者，點選 **[!UICONTROL 拖放對象或在此處選擇]** 欄位並選取 **[!UICONTROL 配偶薪金]** 欄位，該欄位將列出窗體中的所有窗體對象。

   ![write-rules-visual-editor-6](assets/write-rules-visual-editor-6.png)

   規則編輯器中的規則顯示如下。

   ![write-rules-visual-editor-7](assets/write-rules-visual-editor-7.png)

1. 點選 **[!UICONTROL 完成]** 來儲存規則。

1. 重複步驟1到5以定義另一個規則，以在婚姻狀態為「單身」時隱藏「配偶薪金」欄位。 規則編輯器中的規則顯示如下。

   ![write-rules-visual-editor-8](assets/write-rules-visual-editor-8.png)

   >[!NOTE]
   >
   >或者，您可以在「配偶薪金」欄位上編寫一個「顯示」規則，而不是在「婚姻狀態」欄位上編寫兩個「當」規則，以實施相同的行為。

   ![write-rules-visual-editor-9](assets/write-rules-visual-editor-9.png)

1. 接下來，編寫一個規則以計算貸款資格金額（該金額是總薪金的50%），並將其顯示在「貸款資格」欄位中。 要實現這一結果，請 **[!UICONTROL 設定值為]** 貸款資格欄位規則。

   在製作模式中，點選 **[!UICONTROL 貸款資格]** 欄位和點選 ![編輯規則](assets/edit-rules-icon.svg). 下一步，點選 **[!UICONTROL 建立]** 來啟動規則編輯器。

1. 選擇 **[!UICONTROL 設定值為]** 規則。

   ![write-rules-visual-editor-10](assets/write-rules-visual-editor-10.png)

1. 點選 **[!UICONTROL 選擇選項]** 選取 **[!UICONTROL 數學表達式]**. 將開啟一個用於編寫數學表達式的欄位。

   ![write-rules-visual-editor-11](assets/write-rules-visual-editor-11.png)

1. 在運算式欄位中：

   * 從「Forms物件」索引標籤中選取或拖放 **[!UICONTROL 薪金]** 欄位 **[!UICONTROL 拖放對象或在此處選擇]** 欄位。

   * 選擇 **[!UICONTROL 加號]** 從 **[!UICONTROL 選擇運算子]** 欄位。

   * 從「Forms物件」索引標籤中選取或拖放 **[!UICONTROL 配偶薪金]** 欄位 **[!UICONTROL 拖放對象或在此處選擇]** 欄位。

   ![write-rules-visual-editor-12](assets/write-rules-visual-editor-12.png)

1. 接下來，在運算式欄位周圍的醒目提示區域點選，然後點選 **[!UICONTROL 擴充運算式]**.

   ![write-rules-visual-editor-13](assets/write-rules-visual-editor-13.png)

   在擴充運算式欄位中，選取 **[!UICONTROL 除以]** 從 **[!UICONTROL 選擇運算子]** 欄位與 **[!UICONTROL 數字]** 從 **[!UICONTROL 選擇選項]** 欄位。 然後，指定 **[!UICONTROL 2]** 在數字欄位中。

   ![write-rules-visual-editor-14](assets/write-rules-visual-editor-14.png)

   >[!NOTE]
   >
   >您可以使用「選取選項」欄位中的元件、函式、數學表達式和屬性值來建立複雜的表達式。

   接下來，建立條件，當傳回True時，運算式會執行。

1. 點選 **[!UICONTROL 新增條件]** 添加When語句。

   ![write-rules-visual-editor-15](assets/write-rules-visual-editor-15.png)

   在When語句中：

   * 從「Forms物件」索引標籤中選取或拖放 **[!UICONTROL 婚姻狀況]** 欄位 **[!UICONTROL 拖放對象或在此處選擇]** 欄位。

   * 選擇 **[!UICONTROL 等於]** 從 **[!UICONTROL 選擇運算子]** 欄位。

   * 選取其他 **[!UICONTROL 拖放對象或在此處選擇]** 欄位和指定 **[!UICONTROL 已婚]** 在 **[!UICONTROL 輸入字串]** 欄位。

   規則編輯器中最後會顯示如下。  ![write-rules-visual-editor-16](assets/write-rules-visual-editor-16.png)

1. 點選 **[!UICONTROL 完成]**. 它會儲存規則。

1. 重複步驟7到14，以定義另一個規則，以計算婚姻狀態為「單一」時的貸款資格。 規則編輯器中的規則顯示如下。

   ![write-rules-visual-editor-17](assets/write-rules-visual-editor-17.png)

>[!NOTE]
>
>或者，您也可以使用「設定值」規則來計算「何時」規則中的貸款資格，該規則是您為顯示 — 隱藏「配偶薪金」欄位而建立的。 「婚姻狀態為單一」時產生的組合規則，在規則編輯器中顯示如下。
>
>同樣，您可以編寫一個組合規則，以控制「配偶薪金」欄位的可見性，並在「婚姻狀態」為「已婚」時計算貸款資格。

![write-rules-visual-editor-18](assets/write-rules-visual-editor-18.png)

<!-- ### Using code editor {#using-code-editor}

Users added to the forms-power-users group can use code editor. The rule editor auto generates the JavaScript code for any rule you create using visual editor. You can switch from visual editor to the code editor to view the generated code. However, if you modify the rule code in the code editor, you cannot switch back to the visual editor. If you prefer writing rules in code editor rather than visual editor, you can write rules afresh in the code editor. The visual-code editors switcher helps you switch between the two modes.

The code editor JavaScript is the expression language of Adaptive Forms. All the expressions are valid JavaScript expressions and use Adaptive Forms scripting model APIs. These expressions return values of certain types. For the complete list of Adaptive Forms classes, events, objects, and public APIs, see [JavaScript Library API reference for Adaptive Forms](https://helpx.adobe.com/experience-manager/6-5/forms/javascript-api/index.html).

For more information about guidelines to write rules in the code editor, see [Adaptive Form Expressions](adaptive-form-expressions.md).

While writing JavaScript code in the rule editor, the following visual cues help you with the structure and syntax:

* Syntax highlights

* Auto Indentation

* Hints and suggestions for Form objects, functions, and their properties

* Auto completion of form component names and common JavaScript functions

![javascriptruleeditor](assets/javascriptruleeditor.png)
-->

#### 規則編輯器中的自訂函式 {#custom-functions}

除了現成可用的功能，例如 *總和* 「函式輸出」下列的函式，您可以編寫您經常需要的自訂函式。 請確定您所撰寫的函式與 `jsdoc` 在上面。

隨附 `jsdoc` 為必要項目：

* 如果您想要自訂設定和說明
* 因為有多種方式可在 `JavaScript,` 和注釋可讓您追蹤功能。

如需詳細資訊，請參閱 [jsdoc.app](https://jsdoc.app/).

支援 `jsdoc` 標籤：

* **私人**
語法：私人函式未包含為自訂函式。`@private`
私人函式未包含為自訂函式。

* **名稱**
語法：或者， `@name funcName <Function Name>`
或者， `,` 您可以使用： `@function funcName <Function Name>` **或** `@func` `funcName <Function Name>`.
   `funcName` 是函式的名稱（不允許使用空格）。
   `<Function Name>` 是函式的顯示名稱。

* **會員**
語法：將命名空間附加到函式。`@memberof namespace`
將命名空間附加到函式。

* **參數**
語法：或者，您也可以使用： `@param {type} name <Parameter Description>`
或者，您也可以使用： `@argument` `{type} name <Parameter Description>` **或** `@arg` `{type}` `name <Parameter Description>`.
顯示函式使用的參數。 函式可以有多個參數標籤，每個參數的標籤會依發生順序排列。
   `{type}` 代表參數類型。 允許的參數類型為：

   1. 字串
   1. 數字
   1. 布林值
   1. 範圍

   範圍是指適用性表單的欄位。 當表單使用延遲載入時，您可以使用 `scope` 來存取其欄位。 在載入欄位時或欄位標示為全域時，您可以存取欄位。

   所有參數類型都分類在上述其中一個項目下。 不支援無。 請確定您選取上述其中一種類型。 類型不區分大小寫。 參數中不允許空格 `name`. `<Parameter Descrption>` `<parameter>  can have multiple words. </parameter>`

* **傳回類型**
語法：或者，您也可以使用 `@return {type}`
或者，您也可以使用 `@returns {type}`.
新增函式的相關資訊，例如其目標。
{type}表示函式的返回類型。 允許的傳回類型包括：

   1. 字串
   1. 數字
   1. 布林值

   所有其他回訪類型則歸入上述其中一個類別。 不支援無。 請確定您選取上述其中一種類型。 傳回類型不區分大小寫。

   * **此**
語法： 
`@this currentComponent`
   使用@this來參照已寫入規則的適用性表單元件。

   下列範例是以欄位值為基礎。 在以下範例中，規則會隱藏表單中的欄位。 此 `this` 部分 `this.value` 是指寫入規則的基礎適用性表單元件。

   ```
      /**
      * @function myTestFunction
      * @this currentComponent
      * @param {scope} scope in which code inside function will be executed.
      */
      myTestFunction = function (scope) {
         if(this.value == "O"){
               scope.age.visible = true;
         } else {
            scope.age.visible = false;
         }
      }
   ```

   >[!NOTE]
   >
   >自訂函式之前的註解會用於摘要。 摘要可延伸至多行，直到遇到標籤為止。 在規則產生器中將大小限制為單一，以取得簡明說明。

**新增自訂函式**

例如，您想要新增自訂函式，以計算平方的面積。 側長是自訂函式的使用者輸入，在表單中使用數值方塊接受。 計算的輸出會顯示在表單中的另一個數值方塊中。 若要新增自訂函式，您必須先建立用戶端程式庫，然後將其新增至CRX存放庫。

若要建立用戶端程式庫並將其新增至CRX存放庫，請執行下列步驟：

1. 建立客戶端對庫執行以下步驟。 如需詳細資訊，請參閱 [使用用戶端程式庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html#developing).
1. 在CRXDE中，新增屬性 `categories`將字串類型值設為 `customfunction` 到 `clientlib` 檔案夾。

   >[!NOTE]
   >
   >`customfunction`是範例類別。 您可以為在 `clientlib`檔案夾。

在CRX存放庫中新增用戶端程式庫後，請在最適化表單中使用。 它可讓您將自訂函式當成表單中的規則。 若要在適用性表單中新增用戶端程式庫，請執行下列步驟：

1. 在編輯模式中開啟表單。
若要在編輯模式中開啟表單，請選取表單並點選 **[!UICONTROL 開啟]**.
1. 在編輯模式中，選取元件，然後點選 ![欄位層級](assets/select_parent_icon.svg) > **[!UICONTROL 適用性表單容器]**，然後點選 ![cppr](assets/configure-icon.svg).
1. 在側欄的「用戶端程式庫名稱」下，新增用戶端程式庫。 ( `customfunction` )。

   ![添加自定義函式客戶端庫](assets/clientlib.png)

1. 選取輸入數值方塊，然後點選 ![編輯規則](assets/edit-rules-icon.svg) 來開啟規則編輯器。
1. 點選 **[!UICONTROL 建立規則]**. 使用下列選項，建立規則以在表單的「輸出」欄位中儲存輸入的平方值。

[![使用自訂函式建立規則](assets/add_custom_rule_new.png)](assets/add-custom-rule.png)

1. 點選 **[!UICONTROL 完成]**. 已新增您的自訂函式。

#### 支援的函式聲明類型 {#function-declaration-supported-types}

**函式語句**

```javascript
function area(len) {
    return len*len;
}
```

此函式包含時， `jsdoc` 意見。

**函式表達式**

```javascript
var area;
//Some codes later
/** */
area = function(len) {
    return len*len;
};
```

**函式表達式和語句**

```javascript
var b={};
/** */
b.area = function(len) {
    return len*len;
}
```

**函式聲明為變數**

```javascript
/** */
var x1,
    area = function(len) {
        return len*len;
    },
    x2 =5, x3 =true;
```

限制：自訂函式只會從變數清單中挑選第一個函式聲明（若相加）。 您可以對每個已宣告的函式使用函式運算式。

**函式聲明作為對象**

```javascript
var c = {
    b : {
        /** */
        area : function(len) {
            return len*len;
        }
    }
};
```

>[!NOTE]
>
>請確定您使用 `jsdoc` 對每個自訂函式。 雖然 `jsdoc`建議您加入空白的留言 `jsdoc`註解以將函式標示為自訂函式。 這會啟用自訂函式的預設處理。

## 管理規則 {#manage-rules}

當您點選物件並點選時，表單物件上的任何現有規則都會列出 ![edit-rules1](assets/edit-rules-icon.svg). 您可以檢視標題並預覽規則摘要。 此外，UI可讓您展開和檢視完整的規則摘要、變更規則的順序、編輯規則和刪除規則。

![清單規則](assets/list-rules.png)

您可以對規則執行下列動作：

* **展開/折疊**:規則清單中的「內容」欄會顯示規則內容。 如果預設檢視中未顯示整個規則內容，請點選 ![expand-rule-content](assets/Smock_ChevronDown.svg) 來擴展。

* **重新排序**:您建立的任何新規則都會堆疊在規則清單的底部。 規則會從上到下執行。 頂端的規則會先執行，接著執行相同類型的其他規則。 例如，如果規則分別位於從上到下的第一個、第二個、第三個和第四個位置的「時間」、「顯示」、「啟用」和「時間」，則頂端的「時間」規則會先執行，而後是第四個位置的「時間」規則。 然後，執行「顯示」和「啟用」規則。
您可以點選 ![排序規則](assets/sort-rules.svg) 或將其拖曳至清單中的所需順序。

* **編輯**:若要編輯規則，請選取規則標題旁的核取方塊。 編輯和刪除規則的選項隨即出現。 點選 **[!UICONTROL 編輯]** 在規則編輯器中開啟所選規則 <!-- in visual  or code editor mode depending on the mode used to create the rule -->.

* **刪除**:若要刪除規則，請選取規則並點選 **[!UICONTROL 刪除]**.

* **啟用/停用**:當您必須暫時暫停規則的使用時，您可以選取一或多個規則並點選 **[!UICONTROL 停用]** 在「動作」工具列中停用。 如果停用規則，則不會在執行階段執行。 若要啟用已停用的規則，您可以選取該規則，然後點選動作工具列中的「啟用」。 規則的狀態欄會顯示規則已啟用或已停用。

![禁用規則](assets/disablerule.png)

## 複製貼上規則 {#copy-paste-rules}

您可以將規則從一個欄位複製並貼到其他類似欄位，以節省時間。

若要複製貼上規則，請執行下列動作：

1. 點選您要從中複製規則的表單物件，然後在元件工具列點選 ![編輯規則](assets/edit-rules-icon.svg). 規則編輯器用戶介面隨即出現，並選定了表單對象，現有規則隨即出現。

   ![複製規則](assets/copyrule.png)

   如需管理現有規則的詳細資訊，請參閱 [管理規則](rule-editor.md#p-manage-rules-p).

1. 選取規則標題旁的核取方塊，便會顯示管理規則的選項。 點選「 **[!UICONTROL 複製]**」。

   ![copyrule2](assets/copyrule2.png)

1. 選取您要貼上規則並點選的其他表單物件 **[!UICONTROL 貼上]**. 此外，您可以編輯規則以進行變更。

   >[!NOTE]
   >
   >只有當該表單物件支援複製規則的事件時，您才可將規則貼到另一個表單物件。 例如，按鈕支援點按事件。 您可以將包含點按事件的規則貼到按鈕，但不貼到核取方塊。

1. 點選 **[!UICONTROL 完成]** 來儲存規則。

## 巢狀運算式 {#nestedexpressions}

規則編輯器可讓您使用多個AND和OR運算子來建立巢狀規則。 您可以在規則中混合使用多個AND和OR運算子。

以下是一個嵌套規則的示例，該規則在滿足所需條件時向用戶顯示有關子女監護資格的消息。

![複雜運算式](assets/complexexpression.png)

您也可以拖放規則內的條件來加以編輯。 點選並暫留在控點上( ![手柄](assets/drag-handle.svg))。 一旦指標變成手形符號（如下所示），將條件拖放至規則內的任意位置。 規則結構會變更。

![拖放](assets/drag-and-drop.png)

## 日期運算式條件 {#dateexpression}

規則編輯器可讓您使用日期比較來建立條件。

以下是範例條件，若已取得房屋上的抵押貸款，則會顯示靜態文字物件，使用者會填寫日期欄位，以表示此條件。

當使用者填入的物業抵押日期為過去時，適用性表單會顯示收入計算的相關附註。 以下規則將用戶填寫的日期與當前日期進行比較，如果用戶填寫的日期早於當前日期，則表單將顯示文本消息（名為「收入」）。

![日期運算式條件](assets/dateexpressioncondition.png)

當填充日期早於當前日期時，表單將顯示文本消息（收入），如下所示：

![滿足日期運算式條件](assets/dateexpressionconditionmet.png)

## 數字比較條件 {#number-comparison-conditions}

規則編輯器可讓您建立比較兩個數字的條件。

如果申請人目前地址所在的月數少於36，以下是顯示靜態文字物件的範例條件。

![數字比較條件](assets/numbercomparisoncondition.png)

當用戶表示居住在當前住址不到36個月時，表單顯示通知，可以請求更多居住證明。

![請求更多證明](assets/additionalproofrequested.png)

<!-- ## Impact of rule editor on existing scripts {#impact-of-rule-editor-on-existing-scripts}

In [!DNL Experience Manager Forms] versions prior to [!DNL Experience Manager 6.1 Forms] feature pack 1, form authors and developers used to write expressions in the Scripts tab of the Edit component dialog to add dynamic behavior to Adaptive Forms. The Scripts tab is now replaced by the rule editor.

Any scripts or expressions that you must have written in the Scripts tab are available in the rule editor. While you cannot view or edit them in visual editor, if you are a part of the forms-power-users group you can edit scripts in code editor. -->

## 規則範例 {#example}

### 調用表單資料模型服務 {#invoke}

考慮Web服務 `GetInterestRates` 以貸款金額、保有期和申請人的信用評分作為輸入，並返回貸款計畫，包括EMI金額和利率。 您可以使用Web服務作為資料源建立表單資料模型。 添加資料模型對象和 `get` 服務至表單模型。 服務會顯示在表單資料模型的「服務」標籤中。 然後，建立包含資料模型物件欄位的最適化表單，以擷取貸款金額、保有權和信用分數的使用者輸入。 新增按鈕以觸發Web服務擷取計畫詳細資訊。 輸出會填入適當欄位。

以下規則顯示如何配置調用服務操作以完成示例方案。

![Example-invoke-services](assets/example-invoke-services.png)

使用適用性表單規則叫用表單資料模型服務

### 使用When規則觸發多個動作 {#triggering-multiple-actions-using-the-when-rule}

在貸款申請表中，您要獲取貸款申請人是否為現有客戶。 根據使用者提供的資訊，應顯示或隱藏客戶ID欄位。 此外，如果使用者是現有客戶，您也想將焦點設定在客戶ID欄位上。 貸款申請表包含下列部分：

* 一個選項按鈕， **[!UICONTROL 您是現有Geometrixx客戶嗎？]**，提供 [!UICONTROL 是] 和 [!UICONTROL 否] 選項。 「是」的值為 **0** 而否則 **1**.

* 文字欄位， **[!UICONTROL Geometrixx客戶ID]**，以指定客戶ID。

在選項按鈕上撰寫「執行時間」規則以實作此行為時，規則會在視覺規則編輯器中顯示如下。

![When-rule-example](assets/when-rule-example.png)

可視化編輯器中的規則

在範例規則中，When區段中的陳述式為條件，當傳回True時，會執行Then區段中指定的動作。

<!-- The rule appears as follows in the code editor.

![when-rule-example-code](assets/when-rule-example-code.png) 

Rule in the code editor -->

### 在規則中使用函式輸出 {#using-a-function-output-in-a-rule}

在採購訂單表單中，您有下表，用戶在其中填寫訂單。 在下表中：

* 第一列是可重複的，因此使用者可以訂購多個產品並指定不同的數量。 其元素名稱為 `Row1`.
* 可重複行的「產品數量」列中的單元格標題為「數量」。 此儲存格的元素名稱為 `productquantity`.
* 表格中的第二行是不可重複的，此行中「產品數量」列中的單元格標題為「總數量」。

![Example-function-table](assets/example-function-table.png)

**答：** 列1 **B.** 數量 **C.** 總數量

現在，您想要在「產品數量」欄中新增所有產品的指定數量，並在「總數量」儲存格中顯示總和。 您可以在「總量」儲存格上撰寫「設定值」規則，來達到此總和，如下所示。

![Example-function-output](assets/example-function-output.png)

可視化編輯器中的規則

<!-- he rule appears as follows in the code editor.

![example-function-output-code](assets/example-function-output-code.png)

Rule in the code editor -->

### 使用運算式驗證欄位值 {#validating-a-field-value-using-expression}

在上例中解釋的採購訂單表單中，您希望限制用戶訂購超過一個數量且定價超過10000的任何產品。 若要執行此驗證，您可以撰寫驗證規則，如下所示。

![Example-validate](assets/example-validate.png)

可視化編輯器中的規則

<!-- The rule appears as follows in the code editor.

![example-validate-code](assets/example-validate-code.png)

Rule in the code editor -->
