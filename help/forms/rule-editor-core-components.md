---
title: 如何使用規則編輯器將規則新增至表單欄位，以新增動態行為並根據核心元件建立複雜邏輯至調適型表單？
description: 最適化Forms規則編輯器可讓您新增動態行為並將複雜邏輯建置到表單中，而不需要編碼或指令碼。
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
exl-id: 1292f729-c6eb-4e1b-b84c-c66c89dc53ae
source-git-commit: 8585ec309b04e04b9a8dcaa43063369d1c9d5d24
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 1%

---


# 根據核心元件之最適化表單的規則編輯器簡介

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service （核心元件） | 本文章 |
| AEM as a Cloud Service （基礎元件） | [按一下這裡](/help/forms/rule-editor.md) |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=zh-Hant) |

在基於核心元件的調適型表單中，規則編輯器功能可讓業務使用者和開發人員編寫調適型表單物件的規則。 這些規則會根據預設條件、使用者輸入及使用者對表單的動作，定義要在表單物件上觸發的動作。 此功能有助於進一步簡化表單填寫體驗，確保準確性和速度。

規則編輯器提供直覺式且簡化的使用者介面來撰寫規則。 它提供迎合所有使用者需求的視覺化編輯器，讓他們不需具備廣泛的技術知識即可建立和管理規則。 這種視覺化方法讓使用者更容易理解並在表單中實作所需的邏輯。

您可使用規則對最適化表單物件執行的部分關鍵動作如下：

* 顯示或隱藏物件
* 啟用或停用物件
* 設定物件的值
* 驗證物件的值
* 執行函式以計算物件的值
* 啟動表單資料模型(FDM)服務並執行作業
* 設定物件的屬性

<!-- Rule editor replaces the scripting capabilities in [!DNL Experience Manager 6.1 Forms] and earlier releases. However, your existing scripts are preserved in the new rule editor. For more information about working with existing scripts in the rule editor, see [Impact of rule editor on existing scripts](rule-editor.md#p-impact-of-rule-editor-on-existing-scripts-p). -->

新增至`forms-power-users`群組的使用者可以建立指令碼並編輯現有指令碼。 [!DNL forms-users]群組中的使用者可以使用指令碼，但不能建立或編輯指令碼。

請參閱Foundation規則編輯器與核心元件規則編輯器之間的[差異](/help/forms/rule-editor-core-components-difference-tables.md)一文，以取得詳細比較。

<!--
## Difference between Rule editor in Core Components and Rule Editor in Foundation Components

{{rule-editor-diff}}

>[!NOTE]
>
> To see how to create and use custom functions in detail, refer to [Custom functions in Adaptive Forms (Core Components)](/help/forms/create-and-use-custom-functions.md) article.

-->

## 瞭解規則 {#understanding-a-rule}

規則是動作和條件的組合。 在規則編輯器中，動作包括隱藏、顯示、啟用、停用或計算表單中物件值等活動。 條件是對表單物件的狀態、值或屬性執行檢查和作業來評估的Boolean運算式。 根據評估條件所傳回的值（ `True`或`False`）執行動作。

規則編輯器提供一組預先定義的規則型別（例如「何時」、「顯示」、「隱藏」、「啟用」、「停用」、「設定值」和「驗證」）來協助您編寫規則。 每種規則型別都可讓您定義規則中的條件和動作。 本檔案將詳細說明每種規則型別。

規則通常會遵循下列其中一種建構：

**Condition-Action**&#x200B;在此建構中，規則會先定義條件，然後定義要觸發的動作。 此建構與程式設計語言中的if-then陳述式類似。

在規則編輯器中，**When**&#x200B;規則型別會強制執行condition-action結構。

**Action-Condition**&#x200B;在此建構中，規則會先定義要觸發的動作，接著定義評估條件。 此建構的另一個變數為action-condition-alternate action，這也會定義在條件傳回False時要觸發的替代動作。

規則編輯器中的「顯示」、「隱藏」、「啟用」、「停用」、「設定值」和「驗證」規則型別會強制執行動作條件規則結構。 依預設，「顯示」的替代動作是「隱藏」，而「啟用」的替代動作是「停用」，反之亦然。 您無法變更預設的替代動作。

>[!NOTE]
>
>可用的規則型別（包括您在規則編輯器中定義的條件和動作）也取決於您建立規則的表單物件型別。 規則編輯器僅顯示有效的規則型別和選項，用於寫入特定表單物件型別的條件和動作陳述式。 例如，您看不到面板物件的「驗證和設定值」型別。

如需規則編輯器中可用規則型別的詳細資訊，請參閱規則編輯器中的[可用規則型別](rule-editor.md#p-available-rule-types-in-rule-editor-p)。

### 選擇規則建構的准則 {#guidelines-for-choosing-a-rule-construct}

雖然您可以使用任何規則建構來實現大部分的使用案例，以下提供一些選擇建構勝過其他建構的准則。 如需規則編輯器中可用規則的詳細資訊，請參閱規則編輯器中的[可用規則型別](rule-editor.md#p-available-rule-types-in-rule-editor-p)。

* 建立規則時，經驗法則的典型做法是思考您所撰寫規則的物件內容。 假設您要根據使用者在欄位A中指定的值隱藏或顯示欄位B。在此案例中，您評估欄位A的條件，並且根據它傳回的值，觸發欄位B的動作。

  因此，如果您在欄位B （您評估條件的物件）上撰寫規則，請使用condition-action建構或When規則型別。 同樣地，使用動作條件建構或在欄位A上顯示或隱藏規則型別。

* 有時候，您必須根據一個條件執行多個動作。 在這種情況下，建議使用條件 — 動作建構。 在此建構中，您可以評估條件一次，並指定多個動作陳述式。

  例如，若要根據條件隱藏欄位B、C和D，以檢查使用者在欄位A中指定的值，請撰寫一個具有條件 — 動作建構的規則或欄位A上的規則型別時並指定動作來控制欄位B、C和D的可見性。否則，您需要在欄位B、C和D上設定三個個別規則，每個規則會檢查條件並顯示或隱藏個別欄位。 在此範例中，在一個物件上撰寫When規則型別比在三個物件上撰寫Show或Hide規則型別更有效率。

* 若要根據多個條件來觸發動作，建議使用動作條件建構。 例如，若要透過評估欄位B、C和D的條件來顯示和隱藏欄位A，請使用欄位A上的顯示或隱藏規則型別。
* 如果規則包含適用於一個條件的一個動作，請使用條件 — 動作或動作條件建構。
* 如果規則檢查條件，並在欄位中提供值或退出欄位時立即執行動作，則建議在評估條件的欄位上編寫具有條件 — 動作建構或When規則型別的規則。
* 當使用者變更套用When規則的物件值時，會評估When規則中的條件。 但是，如果您希望動作在伺服器端變更時觸發（例如預先填入值），建議寫入在欄位初始化時觸發動作的When規則。
* 在撰寫下拉清單、選項按鈕或核取方塊物件的規則時，這些表單物件在表單中的選項或值會預先填入規則編輯器中。

若要瞭解如何使用使用者介面在規則編輯器中撰寫和管理規則，請參閱[規則編輯器使用者介面以核心元件為基礎的最適化Forms &#x200B;](/help/forms/rule-editor-core-components-user-interface.md)文章。

## 另請參閱

{{see-also-rule-editor}}