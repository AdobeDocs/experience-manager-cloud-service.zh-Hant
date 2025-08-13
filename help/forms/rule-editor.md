---
title: 如何使用規則編輯器將規則新增至表單欄位，以新增動態行為並將複雜邏輯建置至最適化表單？
description: 最適化Forms規則編輯器可讓您新增動態行為並將複雜邏輯建置到表單中，而不需要編碼或指令碼。
feature: Adaptive Forms, Foundation Components
role: User, Developer
level: Beginner, Intermediate
exl-id: 6fd38e9e-435e-415f-83f6-3be177738c00
source-git-commit: 2830f06817b65a2ae059c1381a9d5588b661d74e
workflow-type: tm+mt
source-wordcount: '6649'
ht-degree: 4%

---

# 將規則新增至最適化表單 {#adaptive-forms-rule-editor}

>[!NOTE]
>
> Adobe建議針對[建立新的Adaptive Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)或[將Adaptive Forms新增至AEM Sites頁面](/help/forms/creating-adaptive-form-core-components.md)，使用現代且可擴充的資料擷取[核心元件](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)。 這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。本文說明使用基礎元件製作最適化Forms的舊方法。

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service （基礎元件） | 本文章 |
| AEM as a Cloud Service （核心元件） | [按一下這裡](/help/forms/rule-editor-core-components.md) |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html) |

## 概觀 {#overview}

規則編輯器功能可讓表單業務使用者和開發人員在調適型表單物件上編寫規則。 這些規則會根據預設條件、使用者輸入及使用者對表單的動作，定義要在表單物件上觸發的動作。 它有助於進一步簡化表單填寫體驗，確保準確性和速度。

規則編輯器提供直覺式且簡化的使用者介面來撰寫規則。 規則編輯器為所有使用者提供一個視覺化編輯器。<!-- In addition, only for forms power users, rule editor provides a code editor to write rules and scripts. -->您可以使用規則對最適化表單物件執行的部分關鍵動作如下：

* 顯示或隱藏物件
* 啟用或停用物件
* 設定物件的值
* 驗證物件的值
* 執行函式以計算物件的值
* 啟動表單資料模型服務並執行作業
* 設定物件的屬性

<!-- Rule editor replaces the scripting capabilities in [!DNL Experience Manager 6.1 Forms] and earlier releases. However, your existing scripts are preserved in the new rule editor. For more information about working with existing scripts in the rule editor, see [Impact of rule editor on existing scripts](rule-editor.md#p-impact-of-rule-editor-on-existing-scripts-p). -->

新增至表單超級使用者群組的使用者可以建立指令碼並編輯現有指令碼。 [!DNL forms-users]群組中的使用者可以使用指令碼，但不能建立或編輯指令碼。

## 核心元件中的規則編輯器和基礎元件中的規則編輯器之間的差異

{{rule-editor-diff}}

## 了解規則 {#understanding-a-rule}

規則是動作和條件的組合。 在規則編輯器中，動作包括隱藏、顯示、啟用、停用或計算表單中物件值等活動。 條件是對表單物件的狀態、值或屬性執行檢查和作業來評估的Boolean運算式。 根據評估條件所傳回的值（ `True`或`False`）執行動作。

規則編輯器提供一組預先定義的規則型別（例如「何時」、「顯示」、「隱藏」、「啟用」、「停用」、「設定值」和「驗證」）來協助您編寫規則。 每種規則型別都可讓您定義規則中的條件和動作。 本檔案將詳細說明每種規則型別。

規則通常遵循下列其中一種結構：

**Condition-Action**&#x200B;在此建構中，規則會先定義條件，然後定義要觸發的動作。 此建構與程式設計語言中的if-then陳述式類似。

在規則編輯器中，**When**&#x200B;規則型別會強制執行condition-action結構。

**Action-Condition**&#x200B;在此建構中，規則會先定義要觸發的動作，接著定義評估條件。 此建構的另一個變數為action-condition-alternate action，這也會定義在條件傳回False時要觸發的替代動作。

規則編輯器中的「顯示」、「隱藏」、「啟用」、「停用」、「設定值」和「驗證」規則型別會強制實施動作條件規則結構。 依預設，「顯示」的替代動作是「隱藏」，而「啟用」的替代動作是「停用」，反之亦然。 您無法變更預設的替代動作。

>[!NOTE]
>
>可用的規則型別（包括您在規則編輯器中定義的條件和動作）也取決於您建立規則的表單物件型別。 規則編輯器僅顯示有效的規則型別和選項，用於寫入特定表單物件型別的條件和動作陳述式。 例如，您看不到面板物件的驗證、設定值、啟用和停用規則型別。

如需規則編輯器中可用規則型別的詳細資訊，請參閱規則編輯器中的[可用規則型別](rule-editor.md#p-available-rule-types-in-rule-editor-p)。

### 選擇規則建構的准則 {#guidelines-for-choosing-a-rule-construct}

雖然您可以使用任何規則建構來實現大部分的使用案例，以下提供一些選擇建構勝過其他建構的准則。 如需規則編輯器中可用規則的詳細資訊，請參閱規則編輯器中的[可用規則型別](rule-editor.md#p-available-rule-types-in-rule-editor-p)。

* 建立規則時，經驗法則的典型做法是思考您所撰寫規則的物件內容。 假設您要根據使用者在欄位A中指定的值隱藏或顯示欄位B。在此案例中，您評估欄位A的條件，並且根據它傳回的值，觸發欄位B的動作。

  因此，如果您在欄位B （您評估條件的物件）上撰寫規則，請使用condition-action建構或When規則型別。 同樣地，使用動作條件建構或在欄位A上顯示或隱藏規則型別。

* 有時候，您必須根據一個條件執行多個動作。 在這種情況下，建議使用條件 — 動作建構。 在此建構中，您可以評估條件一次，並指定多個動作陳述式。

  例如，若要根據條件隱藏欄位B、C和D，以檢查使用者在欄位A中指定的值，請撰寫一個具有條件 — 動作建構的規則或欄位A上的規則型別時並指定動作來控制欄位B、C和D的可見性。否則，您需要在欄位B、C和D上設定三個個別規則，每個規則會檢查條件並顯示或隱藏個別欄位。 在此範例中，在一個物件上撰寫When規則型別比在三個物件上撰寫Show或Hide規則型別更有效率。

* 若要根據多個條件來觸發動作，建議使用動作條件建構。 例如，若要藉由評估欄位B、C和D的條件來顯示和隱藏欄位A，請在欄位A上使用顯示或隱藏規則型別。
* 如果規則包含適用於一個條件的一個動作，請使用條件 — 動作或動作條件建構。
* 如果規則檢查條件，並在欄位中提供值或退出欄位時立即執行動作，則建議在評估條件的欄位上編寫具有條件 — 動作建構或When規則型別的規則。
* 當使用者變更套用When規則的物件值時，會評估When規則中的條件。 但是，如果您希望動作在伺服器端變更時觸發（例如預先填入值），建議寫入在欄位初始化時觸發動作的When規則。
* 在撰寫下拉清單、選項按鈕或核取方塊物件的規則時，這些表單物件在表單中的選項或值會預先填入規則編輯器中。

## 規則編輯器中可用的運運算元型別和事件 {#available-operator-types-and-events-in-rule-editor}

規則編輯器提供下列邏輯運運算元和事件，您可使用它們建立規則。

* **等於**
* **不等於**
* **開頭為**
* **結尾為**
* **包含**
* **是空的**
* **不是空的**
* **已選取：**&#x200B;當使用者選取核取方塊、下拉式清單單選按鈕的特定選項時，傳回True。
* **已初始化（事件）：**&#x200B;當表單物件在瀏覽器中呈現時傳回True。
* **已變更（事件）：**&#x200B;當使用者變更表單物件的輸入值或選取的選項時，傳回true。
* **Navigation(event)：**&#x200B;當使用者按一下導覽物件時，傳回true。 導覽物件用於在面板之間移動。
* **步驟完成（事件）：**&#x200B;當規則的步驟完成時傳回true。
* **成功提交（事件）：**&#x200B;成功將資料提交至表單資料模型時傳回True。
* **提交時發生錯誤（事件）：**&#x200B;資料提交至表單資料模型失敗時傳回True。

## 規則編輯器中的可用規則型別 {#available-rule-types-in-rule-editor}

規則編輯器提供了一組預先定義的規則型別，您可以使用這些型別來撰寫規則。 讓我們來詳細瞭解一下每種規則型別。 如需有關在規則編輯器中寫入規則的詳細資訊，請參閱[寫入規則](rule-editor.md#p-write-rules-p)。

### [!UICONTROL 時間] {#whenruletype}

**[!UICONTROL When]**&#x200B;規則型別遵循&#x200B;**condition-action-alternate action**&#x200B;規則建構，有時只遵循&#x200B;**condition-action**&#x200B;建構。 在此規則型別中，您先指定評估條件，接著指定滿足條件時觸發的動作( `True`)。 使用When規則型別時，您可以使用多個AND和OR運運算元來建立[巢狀運算式](#nestedexpressions)。

使用When規則型別，您可以評估表單物件的條件，並對一或多個物件執行動作。

簡單地說，典型的When規則結構如下：

`When on Object A:`

`(Condition 1 AND Condition 2 OR Condition 3) is TRUE;`

`Then, do the following:`

物件B上的動作2；
和
物件C上的動作3；

_

當您有多值元件（如單選按鈕或清單）時，為該元件建立規則時，會自動擷取選項，並讓規則建立者可以使用這些選項。 您不需要再次輸入選項值。

例如，清單有四個選項：紅色、藍色、綠色和黃色。 建立規則時，會自動擷取選項（選項按鈕），以供規則建立者使用，如下所示：

![多重值顯示選項](assets/multivaluefcdisplaysoptions1.png)

撰寫When規則時，您可以觸發「清除值」動作。 清除值動作會清除指定物件的值。 在When陳述式中將的清除值作為選項可讓您建立具有多個欄位的複雜條件。

![清除](assets/clearvalueof1.png)的值

**[!UICONTROL 隱藏]**&#x200B;隱藏指定的物件。

**[!UICONTROL 顯示]**&#x200B;顯示指定的物件。

**[!UICONTROL 啟用]**&#x200B;啟用指定的物件。

**[!UICONTROL 停用]**&#x200B;停用指定的物件。

**[!UICONTROL 啟動服務]**&#x200B;啟動表單資料模型(FDM)中設定的服務。 選擇「啟動服務」作業時，會出現一個欄位。 點選欄位時，它會顯示您[!DNL Experience Manager]執行個體上所有表單資料模型(FDM)中設定的所有服務。 選擇表單資料模型(FDM)服務時，會出現更多欄位，您可在其中對應具有指定服務的輸入和輸出引數的表單物件。 請參閱呼叫表單資料模型服務的規則範例。

除了表單資料模型服務之外，您還可以指定直接的WSDL URL來叫用Web服務。 不過，表單資料模型服務有許多優點，且建議叫用服務的方法。

如需有關在表單資料模型(FDM)中設定服務的詳細資訊，請參閱[[!DNL Experience Manager Forms] 資料整合](data-integration.md)。

**[!UICONTROL 設定值]**&#x200B;計算並設定指定物件的值。 您可以將物件值設為字串、其他物件的值、使用數學運算式或函式的計算值、物件屬性的值，或來自已設定表單資料模型服務的輸出值。 當您選擇Web服務選項時，它會顯示您[!DNL Experience Manager]執行個體上所有表單資料模型(FDM)中設定的所有服務。 選擇表單資料模型服務時，會出現更多欄位，您可在其中對應具有指定服務的輸入和輸出引數的表單物件。

如需有關在表單資料模型(FDM)中設定服務的詳細資訊，請參閱[[!DNL Experience Manager Forms] 資料整合](data-integration.md)。

**[!UICONTROL Set Property]**&#x200B;規則型別可讓您根據條件動作來設定指定物件的屬性值。 您可以將屬性設定為下列其中一項：
* 可見（布林值）
* dorExclusion （布林值）
* chartType （字串）
* 標題（字串）
* 已啟用（布林值）
* 強制（布林值）
* validationsDisabled （布林值）
* validateExpMessage （字串）
* 值（數字、字串、日期）
* 專案（清單）
* 有效（布林值）
* errorMessage （字串）

例如，它可讓您定義規則，以動態地將核取方塊新增至最適化表單。 您可以使用自訂函式、表單物件或物件屬性來定義規則。

![設定屬性](assets/set_property_rule_new1.png)

若要根據自訂函式定義規則，請從下拉式清單中選取&#x200B;**[!UICONTROL 函式輸出]**，然後從&#x200B;**[!UICONTROL 函式]**&#x200B;索引標籤中拖放自訂函式。 如果符合條件動作，則自訂函式中定義的核取方塊數會新增至最適化表單。

若要根據表單物件定義規則，請從下拉式清單中選取&#x200B;**[!UICONTROL 表單物件]**，然後從&#x200B;**[!UICONTROL 表單物件]**&#x200B;標籤中拖放表單物件。 如果符合條件動作，則表單物件中定義的核取方塊數會新增至調適型表單。

根據物件屬性的「設定屬性」規則可讓您根據最適化表單中包含的其他物件屬性，新增最適化表單中的核取方塊數目。

下圖是根據最適化表單中的下拉式清單數量，以動態方式新增核取方塊的範例：

![物件屬性](assets/object_property_set_property_new1.png)

**[!UICONTROL 清除值]**&#x200B;清除指定物件的值。

**[!UICONTROL 設定焦點]**&#x200B;將焦點設定在指定的物件上。

**[!UICONTROL 儲存表單]**&#x200B;儲存表單。

**[!UICONTROL 提交Forms]**&#x200B;提交表單。

**[!UICONTROL 重設表單]**&#x200B;重設表單。

**[!UICONTROL 驗證表單]**&#x200B;驗證表單。

**[!UICONTROL 新增執行個體]**&#x200B;新增指定之可重複面板或表格列的執行個體。

**[!UICONTROL 移除執行個體]**&#x200B;移除指定之可重複面板或表格列的執行個體。

**[!UICONTROL 導覽至]**&#x200B;導覽至其他<!--Interactive Communications,-->最適化Forms、其他資產（例如影像或檔案片段）或外部URL。<!-- For more information, see [Add button to the Interactive Communication](create-interactive-communication.md#addbuttontothewebchannel). -->

### [!UICONTROL 設定值] {#set-value-of}

**[!UICONTROL 規則型別的]**&#x200B;設定值可讓您依據指定的條件是否符合，來設定表單物件的值。 值可以設定為另一個物件的值、常值字串、衍生自數學運算式或函式的值、另一個物件的屬性值，或表單資料模型服務的輸出。 同樣地，您可以檢查元件、字串、屬性或衍生自函式或數學運算式的值的條件。

**Set Value Of**&#x200B;規則型別不適用於所有表單物件，例如面板和工具列按鈕。 標準的「設定值」規則具有以下結構：

將物件A的值設為：

（字串ABC）或
（物件C的物件屬性X）或
（函式中的值） OR
（數學運算式的值） OR
（資料模型服務或Web服務的輸出值）；

當（選擇性）：

（條件1和條件2和條件3）為TRUE；

下列範例以`dependentid`欄位中的值作為輸入，並將`Relation`欄位的值設定為`Relation`表單資料模型服務的`getDependent`引數的輸出。

![Set-value-web-service](assets/set-value-web-service1.png)

使用表單資料模型服務的設定值規則範例

>[!NOTE]
>
>此外，您可以使用規則的「設定值」，從表單資料模型服務或Web服務的輸出，填入下拉式清單元件中的所有值。 不過，請確定您選擇的輸出引數屬於陣列型別。 陣列中傳回的所有值都可在指定的下拉式清單中使用。

### [!UICONTROL 節目] {#show}

使用&#x200B;**[!UICONTROL 顯示]**&#x200B;規則型別，您可以撰寫規則來根據條件是否滿足來顯示或隱藏表單物件。 Show規則型別也會觸發Hide動作，以防條件未滿足或傳回`False`。

典型的Show規則結構如下：

`Show Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Hide Object A;`

### [!UICONTROL 隱藏] {#hide}

與「顯示」規則型別類似，您可以使用&#x200B;**[!UICONTROL 隱藏]**&#x200B;規則型別，根據是否符合條件來顯示或隱藏表單物件。 Hide規則型別也會觸發Show動作，以防條件不滿足或傳回`False`。

典型的「隱藏」規則結構如下：

`Hide Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Show Object A;`

### [!UICONTROL 啟用] {#enable}

**[!UICONTROL 啟用]**&#x200B;規則型別可讓您根據條件是否滿足來啟用或停用表單物件。 Enable規則型別也會觸發Disable動作，以防條件不滿足或傳回`False`。

典型的Enable規則結構如下：

`Enable Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Disable Object A;`

### [!UICONTROL 停用] {#disable}

與「啟用」規則型別類似，**[!UICONTROL 停用]**&#x200B;規則型別可讓您根據條件是否滿足來啟用或停用表單物件。 Disable規則型別也會觸發Enable動作，以防條件不滿足或傳回`False`。

典型的「停用」規則結構如下：

`Disable Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Enable Object A;`

### [!UICONTROL 驗證] {#validate}

**[!UICONTROL Validate]**&#x200B;規則型別使用運算式來驗證欄位中的值。 例如，您可以撰寫運算式來檢查指定名稱的文字方塊是否不包含特殊字元或數字。

典型的驗證規則結構如下：

`Validate Object A;`

`Using:`

`(Expression 1 AND Expression 2 AND Expression 3) is TRUE;`

>[!NOTE]
>
>如果指定的值不符合驗證規則，您可以向使用者顯示驗證訊息。 您可以在側邊欄中元件屬性的&#x200B;**[!UICONTROL 指令碼驗證訊息]**&#x200B;欄位中指定訊息。

![指令碼驗證](assets/script-validation.png)

### [!UICONTROL 設定]的選項 {#setoptionsof}

**[!UICONTROL Set Options Of]**&#x200B;規則型別可讓您定義規則，以動態地將核取方塊新增至最適化表單。 您可以使用表單資料模型(FDM)或自訂函式來定義規則。

若要根據自訂函式定義規則，請從下拉式清單中選取&#x200B;**[!UICONTROL 函式輸出]**，然後從&#x200B;**[!UICONTROL 函式]**&#x200B;索引標籤中拖放自訂函式。 自訂函式中定義的核取方塊數會新增至最適化表單。

![自訂函式](assets/custom_functions_set_options_new.png)

若要建立自訂函式，請參閱規則編輯器中的[自訂函式](#custom-functions)。

若要根據表單資料模型(FDM)定義規則：

1. 從下拉式清單中選取&#x200B;**[!UICONTROL 服務輸出]**。
1. 選取資料模型物件。
1. 從&#x200B;**[!UICONTROL 顯示值]**&#x200B;下拉式清單中選取資料模型物件屬性。 最適化表單中的核取方塊數目是從資料庫中為該屬性定義的例項數目衍生而來。
1. 從&#x200B;**[!UICONTROL 儲存值]**&#x200B;下拉式清單中選取資料模型物件屬性。

![FDM集選項](assets/fdm_set_options_new.png)

## 瞭解規則編輯器使用者介面 {#understanding-the-rule-editor-user-interface}

規則編輯器提供完整但簡單的使用者介面，用於撰寫和管理規則。 您可以在撰寫模式下，從最適化表單中啟動規則編輯器使用者介面。

若要啟動規則編輯器使用者介面：

1. 以撰寫模式開啟最適化表單。
1. 選取您要編寫規則的表單物件，然後在元件工具列中選取![edit-rules](assets/edit-rules-icon.svg)。 規則編輯器使用者介面隨即顯示。

   ![create-rules](assets/create-rules1.png)

   此檢視中會列出所選表單物件上的任何現有規則。 如需有關管理現有規則的資訊，請參閱[管理規則](rule-editor.md#p-manage-rules-p)。

1. 選取&#x200B;**[!UICONTROL 建立]**&#x200B;以撰寫新規則。 第一次啟動規則編輯器時，規則編輯器使用者介面的視覺化編輯器預設會開啟。

   ![規則編輯器UI](assets/rule-editor-ui1.png)

讓我們來詳細瞭解規則編輯器UI的每個元件。

### A.元件規則顯示 {#a-component-rule-display}

顯示啟動規則編輯器所使用之最適化表單物件的標題，以及目前選取的規則型別。 在上述範例中，規則編輯器是從名為Salary的最適化表單物件啟動，且選取的規則型別是When。

### B.表單物件與函式 {#b-form-objects-and-functions-br}

規則編輯器使用者介面左側的窗格包含兩個標籤 — **[!UICONTROL Forms物件]**&#x200B;和&#x200B;**[!UICONTROL 函式]**。

「表單物件」標籤會顯示最適化表單中包含之所有物件的階層檢視。 它會顯示物件的標題和型別。 撰寫規則時，您可以將表單物件拖放至規則編輯器上。 將物件或函式拖放至預留位置時，在建立或編輯規則時，預留位置會自動採用適當的值型別。

已套用一或多個有效規則的表單物件會以綠色圓點標示。 如果套用至表單物件的任何規則無效，則表單物件會標示為黃點。

函式索引標籤包含一組內建函式，例如Sum Of、Min Of、Max Of、Average Of、Number Of和Validate表單。 您可以使用這些函式計算可重複面板和表格列中的值，並在撰寫規則時在動作和條件陳述式中使用它們。 不過，您也可以建立[自訂函式](#custom-functions)。

![函式索引標籤](assets/functions1.png)

>[!NOTE]
>
>您可以在Forms「物件」和「函式」標籤中搜尋物件和函式的名稱及標題。

在表單物件的左側樹狀結構中，您可以選取表單物件，以顯示套用到每個物件的規則。 您不僅可以瀏覽各種表單物件的規則，也可以在表單物件之間複製 — 貼上規則。 如需詳細資訊，請參閱[複製貼上規則](rule-editor.md#p-copy-paste-rules-p)。

### C.表單物件與功能切換 {#c-form-objects-and-functions-toggle-br}

點選「切換」按鈕時，會切換表單物件和函數窗格。

### D.視覺規則編輯器 {#visual-rule-editor}

視覺化規則編輯器是規則編輯器使用者介面的視覺化編輯器模式中您編寫規則的區域。 它可讓您選取規則型別，並據此定義條件和動作。 在規則中定義條件和動作時，您可以從「表單物件與函式」窗格中拖放表單物件與函式。

如需使用視覺化規則編輯器的詳細資訊，請參閱[撰寫規則](rule-editor.md#p-write-rules-p)。
<!-- 
### E. Visual-code editors switcher {#e-visual-code-editors-switcher}

Users in the forms-power-users group can access code editor. For other users, code editor is not available. If you have the rights, you can switch from visual editor mode to code editor mode of the rule editor, and conversely, using the switcher right above the rule editor. When you launch rule editor the first time, it opens in the visual editor mode. You can write rules in the visual editor mode or switch to the code editor mode to write a rule script. However, note that if you modify a rule or write a rule in code editor, you cannot switch back to the visual editor for that rule unless you clear the code editor.

[!DNL Experience Manager Forms] tracks the rule editor mode you used last to write a rule. When you launch the rule editor next time, it opens in that mode. However, you can also configure a default mode to open the rule editor in the specified mode. To do so:

1. Go to [!DNL Experience Manager] web console at `https://[host]:[port]/system/console/configMgr`.
1. Click to edit **[!UICONTROL Adaptive Form Configuration Service]**.
1. choose **[!UICONTROL Visual Editor]** or **[!UICONTROL Code Editor]** from the **[!UICONTROL Default Mode for Rule Editor]** drop-down

1. Click **[!UICONTROL Save]**.
-->

### E.完成和取消按鈕 {#done-and-cancel-buttons}

「**[!UICONTROL 完成]**」按鈕用於儲存規則。您可以儲存不完整的規則。 但是，不完整內容無效，因此不會執行。 當您下次從相同表單物件啟動規則編輯器時，會列出表單物件上已儲存的規則。 您可以在該檢視中管理現有規則。 如需詳細資訊，請參閱[管理規則](rule-editor.md#p-manage-rules-p)。

「**[!UICONTROL 取消]**」按鈕會放棄您對規則所做的任何變更並關閉規則編輯器。

## 寫入規則 {#write-rules}

您可以使用視覺化規則編輯器來撰寫規則。

讓我們先來看看如何使用視覺化編輯器來撰寫規則。

### 使用視覺化編輯器 {#using-visual-editor}

讓我們瞭解如何使用下列範例表單在視覺化編輯器中建立規則。

![Create-rule-example](assets/create-rule-example.png)

範例貸款申請表單中的「貸款需求」區段要求申請人指定其婚姻狀況、薪資，如果已婚，則指定其配偶的薪資。 規則會根據使用者輸入來計算貸款資格金額，並顯示在「貸款資格」欄位中。 套用下列規則以實施情境：

* 配偶的「薪資」欄位僅在「婚姻狀況」為「已婚」時顯示。
* 貸款資格金額為薪資總額的50%。

若要編寫規則，請執行下列步驟：

1. 首先，根據使用者為「婚姻狀況」選項按鈕選取的選項，撰寫規則以控制「配偶薪資」欄位的可見度。

   以編寫模式開啟貸款申請表單。 選取&#x200B;**[!UICONTROL 婚姻狀況]**&#x200B;元件並選取![編輯 — 規則](assets/edit-rules-icon.svg)。 接著，選取&#x200B;**[!UICONTROL 建立]**&#x200B;以啟動規則編輯器。

   ![write-rules-visual-editor-1](assets/write-rules-visual-editor-1.png)

   啟動規則編輯器時，預設會選取When規則。 此外，您啟動規則編輯器的表單物件（在此例中為「婚姻狀況」）會在When陳述式中指定。

   雖然您無法變更或修改選取的物件，但可以使用規則下拉式清單（如下所示）來選取其他規則型別。 如果您想在其他物件上建立規則，請選取「取消」結束規則編輯器，然後從想要的表單物件再次啟動它。

1. 選取&#x200B;**[!UICONTROL 選取狀態]**&#x200B;下拉式清單，並選取&#x200B;**[!UICONTROL 等於]**。 **[!UICONTROL 輸入字串]**&#x200B;欄位就會顯示。

   ![write-rules-visual-editor-2](assets/write-rules-visual-editor-2.png)

   在「婚姻狀況」選項按鈕中，**[!UICONTROL 已婚]**&#x200B;與&#x200B;**[!UICONTROL 單身]**&#x200B;選項分別被指派為&#x200B;**0**&#x200B;與&#x200B;**1**&#x200B;值。 您可以在「編輯」選項按鈕對話方塊的「標題」標籤中驗證指派的值，如下所示。

   來自規則編輯器的![選項按鈕值](assets/radio-button-values.png)

1. 在規則的&#x200B;**[!UICONTROL 輸入字串]**&#x200B;欄位中，指定&#x200B;**0**。

   ![write-rules-visual-editor-4](assets/write-rules-visual-editor-4.png)

   您已將條件定義為`When Marital Status is equal to Married`。 接著，定義若此條件為True時要執行的動作。

1. 在Then陳述式中，從&#x200B;**[!UICONTROL 選取動作]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL 顯示]**。

   ![write-rules-visual-editor-5](assets/write-rules-visual-editor-5.png)

1. 從&#x200B;**[!UICONTROL 拖放物件上的[表單物件]索引標籤中拖放]**&#x200B;配偶薪資&#x200B;**[!UICONTROL 欄位，或選取這裡]**&#x200B;欄位。 或者，選取&#x200B;**[!UICONTROL 拖放物件或選取這裡]**&#x200B;欄位，然後從躍現式選單中選取&#x200B;**[!UICONTROL 配偶薪資]**&#x200B;欄位，這會列出表單中的所有表單物件。

   ![write-rules-visual-editor-6](assets/write-rules-visual-editor-6.png)

   規則在規則編輯器中會顯示如下。

   ![write-rules-visual-editor-7](assets/write-rules-visual-editor-7.png)

1. 選取「**[!UICONTROL 完成]**」以儲存此規則。

1. 重複步驟1到5，定義另一個規則，以在「婚姻狀況」為「單身」時隱藏「配偶薪資」欄位。 規則在規則編輯器中會顯示如下。

   ![write-rules-visual-editor-8](assets/write-rules-visual-editor-8.png)

   >[!NOTE]
   >
   >或者，您可以在「配偶薪資」欄位上撰寫一個「顯示」規則，而不是在「婚姻狀況」欄位上撰寫兩個「當規則」，以實施相同的行為。

   ![write-rules-visual-editor-9](assets/write-rules-visual-editor-9.png)

1. 接著，撰寫規則以計算貸款資格金額（為薪資總額的50%），並在「貸款資格」欄位中顯示。 若要取得此結果，請在貸款適用性欄位上建立&#x200B;**[!UICONTROL 設定值（共]**&#x200B;個）。

   在撰寫模式中，選取&#x200B;**[!UICONTROL 貸款資格]**&#x200B;欄位，然後選取![編輯規則](assets/edit-rules-icon.svg)。 接著，選取&#x200B;**[!UICONTROL 建立]**&#x200B;以啟動規則編輯器。

1. 從規則下拉式清單中選取&#x200B;**[!UICONTROL 設定值]**。

   ![write-rules-visual-editor-10](assets/write-rules-visual-editor-10.png)

1. 選取「**[!UICONTROL 選取選項]**」，並選取「**[!UICONTROL 數學運算式]**」。開啟用於編寫數學運算式的欄位。

   ![write-rules-visual-editor-11](assets/write-rules-visual-editor-11.png)

1. 在運算式欄位中：

   * 從Forms物件標籤中選取或拖放第一個&#x200B;**[!UICONTROL 放置物件中的]** Salary **[!UICONTROL 欄位，或選取這裡]**&#x200B;欄位。

   * 從&#x200B;**[!UICONTROL 選取運運算元]**&#x200B;欄位中選取&#x200B;**[!UICONTROL 加號]**。

   * 從「Forms物件」標籤中選取或拖放其他&#x200B;**[!UICONTROL 拖放物件的]**&#x200B;配偶薪資&#x200B;**[!UICONTROL 欄位，或選取這裡]**&#x200B;欄位。

   ![write-rules-visual-editor-12](assets/write-rules-visual-editor-12.png)

1. 接下來，選取運算式欄位周圍醒目標示的區域，並選取「**[!UICONTROL 擴充運算式]**」。

   ![write-rules-visual-editor-13](assets/write-rules-visual-editor-13.png)

   在擴展運算式欄位中，從「**[!UICONTROL 選取運算子]**」欄位選取「**[!UICONTROL 除以]**」以及從「**[!UICONTROL 選取選項]**」欄位選取「**[!UICONTROL 數字]**」。然後在數字欄位中指定&#x200B;**[!UICONTROL 2]**。

   ![write-rules-visual-editor-14](assets/write-rules-visual-editor-14.png)

   >[!NOTE]
   >
   >您可以在「選取選項」欄位中使用元件、函式、數學運算式和屬性值來建立複雜運算式。

   接著，建立條件，當傳回True時，執行運算式。

1. 選取&#x200B;**[!UICONTROL 新增條件]**&#x200B;以新增When陳述式。

   ![write-rules-visual-editor-15](assets/write-rules-visual-editor-15.png)

   在When陳述式中：

   * 從Forms物件索引標籤中選取或拖放第一個&#x200B;**[!UICONTROL 放置物件的]**&#x200B;婚姻狀況&#x200B;**[!UICONTROL 欄位，或選取這裡]**&#x200B;欄位。

   * 從&#x200B;**[!UICONTROL 選取運運算元]**&#x200B;欄位中選取&#x200B;**[!UICONTROL 等於]**。

   * 選取其他&#x200B;**[!UICONTROL 拖放物件中的字串，或選取這裡]**&#x200B;欄位，並在&#x200B;**[!UICONTROL 輸入字串]**&#x200B;欄位中指定&#x200B;**[!UICONTROL 已婚]**。

   規則最後會顯示在規則編輯器中，如下所示。  ![write-rules-visual-editor-16](assets/write-rules-visual-editor-16.png)

1. 選取&#x200B;**[!UICONTROL 完成]**。 這會儲存規則。

1. 重複步驟7到14，定義另一個規則，以計算婚姻狀況為「單身」時的貸款資格。 規則在規則編輯器中會顯示如下。

   ![write-rules-visual-editor-17](assets/write-rules-visual-editor-17.png)

>[!NOTE]
>
>或者，您可以使用「設定值」規則，在您建立用來顯示 — 隱藏「配偶薪資」欄位的「時機」規則中，計算貸款資格。 當「婚姻狀況」為「單一」時，產生的合併規則會顯示在規則編輯器中，如下所示。
>
>同樣地，您可以撰寫合併規則來控制「配偶薪資」欄位的可見度，並在「婚姻狀況」為「已婚」時計算貸款資格。

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

除了列在函式輸出下的現成函式（如&#x200B;*總和*）之外，您也可以撰寫您經常需要的自訂函式。 確定您撰寫的函式上方有`jsdoc`。

必須隨附`jsdoc`：

* 如果您想要自訂設定和說明
* 因為有多種方式可以在`JavaScript,`中宣告函式，而註解可讓您追蹤函式。

規則編輯器支援指令碼和自訂函式的JavaScript ES5語法。
如需詳細資訊，請參閱[jsdoc.app](https://jsdoc.app/)。

支援的`jsdoc`標籤：

* **私人**
語法： `@private`
私人函式不會納入為自訂函式。

* **名稱**
語法： `@name funcName <Function Name>`
或者`,`，您可以使用： `@function funcName <Function Name>` **或** `@func` `funcName <Function Name>`。
  `funcName`是函式的名稱（不允許空格）。
  `<Function Name>`是函式的顯示名稱。

* **成員**
語法： `@memberof namespace`
將名稱空間附加至函式。

* **引數**
語法： `@param {type} name <Parameter Description>`
或者，您可以使用： `@argument` `{type} name <Parameter Description>` **或** `@arg` `{type}` `name <Parameter Description>`。
顯示函式使用的引數。 一個函式可以有多個引數標籤，每個引數會依發生順序各一個標籤。
  `{type}`代表引數型別。 允許的引數型別為：

   1. 字串
   1. 數字
   1. 布林值
   1. 範圍

  範圍是指最適化表單的欄位。 表單使用延遲載入時，您可以使用`scope`存取其欄位。 您可以在載入欄位時存取欄位，或者如果欄位標示為全域。

  所有引數型別都會歸類到上述其中一種型別下。 不支援任何專案。 請確定您選取以上任一型別。 型別不區分大小寫。 引數`name`中不允許空格。`<Parameter Descrption>` `<parameter>  can have multiple words. </parameter>`

* **傳回型別**
語法： `@return {type}`
或者，您可以使用`@returns {type}`。
新增函式的相關資訊，例如其目標。
  {type}代表函式的傳回型別。 允許的傳回型別為：

   1. 字串
   1. 數字
   1. 布林值

  所有其他回訪型別則會歸類到上述任一型別下。 不支援任何專案。 請確定您選取以上任一型別。 傳回型別不區分大小寫。

   * **此**
語法： `@this currentComponent`

  使用@this可參照寫入規則的最適化表單元件。

  以下範例是根據欄位值。 在以下範例中，規則會隱藏表單中的欄位。 `this`的`this.value`部分參考寫入規則的基礎調適型表單元件。

  ```
     /**
     * @function myTestFunction
     * @this currentComponent
     * @param {scope} scope in which code inside function is run.
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
  >使用自訂函式之前的註解作為摘要。 摘要可以延伸至多行，直到遇到標籤為止。 將大小限製為單一，以在規則產生器中提供簡要說明。

**正在新增自訂函式**

例如，您想要新增計算正方形區域的自訂函式。 側邊長度是自訂函式的使用者輸入，可使用表單中的數字方塊來接受。 計算的輸出會顯示在表單的另一個數值方塊中。 若要新增自訂函式，必須先建立使用者端資料庫，然後將其新增至CRX存放庫。

若要建立使用者端程式庫並將其新增至CRX存放庫，請執行以下步驟：

1. 建立使用者端資源庫。 如需詳細資訊，請參閱[使用使用者端資料庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html#developing)。
1. 在CRXDE中，將字串型別值為`categories`的屬性`customfunction`新增至`clientlib`資料夾。

   >[!NOTE]
   >
   >`customfunction`是範例類別。 您可以在`clientlib`資料夾中為建立的類別選擇任何名稱。

在CRX存放庫中新增使用者端程式庫後，請於最適化表單中使用。 它可讓您使用自訂函式作為表單中的規則。 若要在最適化表單中新增使用者端程式庫，請執行下列步驟：

1. 在編輯模式中開啟您的表單。
若要以編輯模式開啟表單，請選取表單並選取**[!UICONTROL 開啟]**。
1. 在編輯模式中，選取元件，然後選取![欄位層級](assets/select_parent_icon.svg) > **[!UICONTROL 最適化表單容器]**，然後選取![cmppr](assets/configure-icon.svg)。
1. 在側邊欄中的「使用者端資料庫名稱」下方，新增您的使用者端資料庫。 （範例中為`customfunction`。）

   ![正在新增自訂函式使用者端程式庫](assets/clientlib.png)

1. 選取輸入數值方塊，然後選取![edit-rules](assets/edit-rules-icon.svg)以開啟規則編輯器。
1. 選取&#x200B;**[!UICONTROL 建立規則]**。 使用下列選項，建立規則以將輸入的平方值儲存在表單的「輸出」欄位中。

   [![使用自訂函式建立規則](assets/add_custom_rule_new.png)](assets/add-custom-rule.png)

1. 選取&#x200B;**[!UICONTROL 完成]**。 您的自訂函式已新增。

   >[!NOTE]
   >
   > 若要使用自訂函式從規則編輯器叫用表單資料模型(FDM)，[請參閱此處](/help/forms/using-form-data-model.md#invoke-services-in-adaptive-forms-using-rules-invoke-services)。

#### 函式宣告支援的型別 {#function-declaration-supported-types}

**函式陳述式**

```javascript
function area(len) {
    return len*len;
}
```

此函式包含，但不包含`jsdoc`個註解。

**函式運算式**

```javascript
var area;
//Some codes later
/** */
area = function(len) {
    return len*len;
};
```

**函式運算式和陳述式**

```javascript
var b={};
/** */
b.area = function(len) {
    return len*len;
}
```

**函式宣告為變數**

```javascript
/** */
var x1,
    area = function(len) {
        return len*len;
    },
    x2 =5, x3 =true;
```

限制：自訂函式只會從變數清單中挑選第一個函式宣告（如果同時挑選）。 您可以對每個宣告的函式使用函式運算式。

**函式宣告為物件**

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
>請確定您對每個自訂函式都使用`jsdoc`。 雖然建議使用`jsdoc`個註解，但請加入空白的`jsdoc`註解，以將您的函式標示為自訂函式。 它會啟用自訂函式的預設處理。

### 支援驗證運算式中的自訂函數 {#supporting-custom-functions-in-validation-expressions-br}

有時候，如果有&#x200B;**複雜的驗證規則**，則確切的驗證指令碼會駐留在自訂函數中，且作者會從欄位驗證運算式中呼叫這些自訂函數。若要在執行伺服器端驗證時公開和提供此自訂函數程式庫，表單作者可以在「最適化表單容器」屬性的「**[!UICONTROL 基礎]**」標籤下方，設定 AEM 用戶端程式庫的名稱，如以下所示。

![支援驗證運算式中的自訂函數](assets/clientlib-cat.png)

支援驗證運算式中的自訂函數

作者可以根據最適化表單來設定自訂 JavaScript 程式庫。程式庫中只會保留可重複使用的函數，這些函數與 jquery 和 underscore.js 第三方程式庫有相依性。

## 提交動作的錯誤處理 {#error-handling-on-submit-action}

為了 AEM 安全性和強化準則，請設定自訂錯誤頁面，例如 400.jsp、404.jsp 和 500.jsp。提交表單時，如果出現 400、404 或 500 錯誤，就會呼叫這些處理常式。在發佈節點上觸發這些錯誤代碼時，也會呼叫處理常式。您也可以為其他 HTTP 錯誤代碼建立 JSP 頁面。

當您將包含XML或JSON資料投訴的表單資料模型(FDM)或結構描述型調適型表單預填至資料不包含`<afData>`、`<afBoundData>`和`</afUnboundData>`標籤的結構描述時，調適型表單未限制欄位的資料會遺失。 結構描述可以是XML結構描述、JSON結構描述或表單資料模型(FDM)。 未繫結欄位是最適化表單欄位，但沒有 `bindref` 屬性。

## 管理規則 {#manage-rules}

當您選取物件並選取![edit-rules1](assets/edit-rules-icon.svg)時，表單物件上的任何現有規則都會列出。 您可以檢視標題並預覽規則摘要。 此外，UI可讓您展開並檢視完整的規則摘要、變更規則順序、編輯規則及刪除規則。

![清單規則](assets/list-rules.png)

您可以對規則執行下列動作：

* **展開/摺疊**：規則清單中的「內容」欄會顯示規則內容。 如果在預設檢視中看不到整個規則內容，請選取![expand-rule-content](assets/Smock_ChevronDown.svg)以展開它。

* **重新排序**：您建立的任何新規則都會棧疊在規則清單底部。 規則會從上到下執行。 頂端的規則會先執行，接著執行相同型別的其他規則。 例如，如果您分別從頂端開始，在第一、第二、第三和第四個位置有When、Show、Enable和When規則，則頂端的規則會先執行，接著在第四個位置有When規則。 接著會執行「顯示」和「啟用」規則。
您可以對規則點選![排序規則](assets/sort-rules.svg)或將其拖放到清單中所需的順序來變更規則的順序。

* **編輯**：若要編輯規則，請選取規則標題旁的核取方塊。 隨即顯示編輯和刪除規則的選項。 選取&#x200B;**[!UICONTROL 編輯]**&#x200B;以在規則編輯器<!-- in visual  or code editor mode depending on the mode used to create the rule -->中開啟選取的規則。

* **刪除**：若要刪除規則，請選取該規則並選取&#x200B;**[!UICONTROL 刪除]**。

* **啟用/停用**：當您必須暫時暫停使用規則時，您可以選取一或多個規則，並在[動作]工具列中選取[停用] **[!UICONTROL 停用]**&#x200B;以停用這些規則。 如果規則已停用，則不會在執行階段執行。 若要啟用已停用的規則，您可以選取該規則，然後選取動作工具列中的「啟用」 。 規則的狀態列顯示規則是啟用還是停用。

![停用規則](assets/disablerule.png)

## 複製貼上規則 {#copy-paste-rules}

您可以將規則從一個欄位複製並貼上到其他類似欄位，以節省時間。

若要複製貼上規則，請執行下列動作：

1. 選取您要從中複製規則的表單物件，然後在元件工具列中選取![編輯規則](assets/edit-rules-icon.svg)。 規則編輯器使用者介面會出現，並選取表單物件，而現有規則會出現。

   ![複製規則](assets/copyrule.png)

   如需有關管理現有規則的資訊，請參閱[管理規則](rule-editor.md#p-manage-rules-p)。

1. 選取規則標題旁的核取方塊，管理規則的選項就會出現。 選取&#x200B;**[!UICONTROL 複製]**。

   ![copyrule2](assets/copyrule2.png)

1. 選取您要貼上規則的其他表單物件，並選取&#x200B;**[!UICONTROL 貼上]**。 此外，您可以編輯規則以對其進行變更。

   >[!NOTE]
   >
   >只有當表單物件支援所複製規則的事件，您才能將規則貼到另一個表單物件。 例如，按鈕支援點選事件。 您可以將具有點選事件的規則貼到按鈕上，但無法貼到核取方塊上。

1. 選取「**[!UICONTROL 完成]**」以儲存此規則。

## 巢狀運算式 {#nestedexpressions}

規則編輯器可讓您使用多個AND和OR運運算元來建立巢狀規則。 您可以在規則中混合使用多個AND和OR運運算元。

以下是巢狀規則的範例，該規則會在符合所需條件時，向使用者顯示有關子女監護權的資格的訊息。

![複雜運算式](assets/complexexpression.png)

您也可以拖放規則中的條件以進行編輯。 選取並將滑鼠游標停留在條件前的控制代碼（ ![控制代碼](assets/drag-handle.svg)）上。 指標變成如下所示的手形符號後，請將條件拖放至規則內的任何位置。 規則結構會變更。

![拖放](assets/drag-and-drop.png)

## 日期運算式條件 {#dateexpression}

規則編輯器可讓您使用日期比較來建立條件。

以下是一個範例條件，會在房屋抵押貸款已辦理時顯示靜態文字物件，使用者填寫日期欄位即表示該條件。

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

## 規則範例 {#example}

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

視覺化編輯器中的規則

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

視覺化編輯器中的規則

<!-- he rule appears as follows in the code editor.

![example-function-output-code](assets/example-function-output-code.png)

Rule in the code editor -->

### 使用運算式驗證欄位值 {#validating-a-field-value-using-expression}

在上一個範例中說明的採購單表單中，您想要限制使用者訂購超過一10000數量的產品。 若要執行此驗證，您可以編寫驗證規則，如下所示。

![Example-validate](assets/example-validate.png)

視覺化編輯器中的規則

<!-- The rule appears as follows in the code editor.

![example-validate-code](assets/example-validate-code.png)

Rule in the code editor -->