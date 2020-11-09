---
title: 使用ContextHub設定區段
description: 瞭解如何使用ContextHub來設定區段。
translation-type: tm+mt
source-git-commit: c9c7176f6c3bf70529b761183341a2490d4ecbfc
workflow-type: tm+mt
source-wordcount: '1692'
ht-degree: 1%

---


# 使用ContextHub設定區段{#configuring-segmentation-with-contexthub}

區段是建立促銷活動時的主要考量。 如需細 [分運作方式和關鍵詞](segmentation.md) ，請參閱瞭解細分。

根據您已收集的網站訪客相關資訊以及您要達到的目標，您需要定義目標內容所需的區段和策略。

然後，這些區段會用來為訪客提供特定的目標內容。 [此處定義的](activities.md) 「活動」可包含在任何頁面上，並定義專業內容適用的訪客區段。

AEM可讓您輕鬆個人化使用者的體驗。 此外，還可讓您驗證區段定義的結果。

## 存取區段 {#accessing-segments}

Audiences [主控台](audiences.md) ，用來管理ContextHub的區段，以及Adobe Target帳戶的觀眾。 本檔案涵蓋管理ContextHub的區段。

若要存取您的區段，請在全域導覽中選取「導 **覽>個人化>觀眾」**。

![Managing audiences](../assets/contexthub-segmentation-audiences.png)

## 區段編輯器 {#segment-editor}

<!--The **Segment Editor** allows you to easily modify a segment. To edit a segment, select a segment in the [list of segments](/help/sites-administering/segmentation.md#accessing-segments) and click the **Edit** button.-->
「區 **段編輯器** 」可讓您輕鬆修改區段。 若要編輯區段，請在區段清單中選取區段，然後按一下「編 **輯** 」按鈕。

![區段編輯器](../assets/contexthub-segment-editor.png)

使用元件瀏覽器，您可以新增 **AND** 和 **OR** 容器來定義區段邏輯，然後新增其他元件來比較屬性和值，或參考指令碼和其他區段來定義選擇標準(請參閱建立新區段 [](#creating-a-new-segment))，以定義確切的選擇區段藍本。

當整個陳述式評估為true時，區段即已解決。 若有多個區段適用，則也會使 **用Boost** factor。 如需 [提升系數的詳細資訊](#creating-a-new-segment) ，請參閱建立新區段。

>[!CAUTION]
>
>段編輯器不檢查任何循環參照。 例如，區段A會參照另一個區段B，反過來參照區段A。您必須確保區段不包含任何循環參照。

### 容器 {#containers}

下列容器是現成可用的，可讓您將比較和參考分組，以便進行布林值評估。 它們可從元件瀏覽器拖曳至編輯器。 如需詳細資訊，請 [參閱以下使用AND和OR容器](#using-and-and-or-containers) 一節。

|  |  |
|---|---|
| 容器 AND | 布林AND運算子 |
| 容器 OR | 布林OR運算子 |

### 比較 {#comparisons}

下列區段比較是現成可用的，可用來評估區段屬性。 它們可從元件瀏覽器拖曳至編輯器。

|  |  |
|---|---|
| 屬性值 | 將商店的屬性與定義的值比較 |
| 屬性——屬性 | 將商店的某個屬性與另一個屬性進行比較 |
| 屬性區段參考 | 將商店的屬性與其他參考的區段比較 |
| 屬性——指令碼參考 | 將商店的屬性與指令碼的結果比較 |
| 區段參考指令碼參考 | 將參考的區段與指令碼的結果比較 |

>[!NOTE]
>
>比較值時，如果未設定比較的資料類型（亦即設為自動偵測）,ContextHub的區段引擎將只會像javascript一樣比較值。 它不會將值轉換至其預期類型，而可能導致誤導結果。 例如：
>
>`null < 30 // will return true`
>
>因此， [建立區段時](#creating-a-new-segment)，只要已知比較值 **的類型** ，您就應選取資料類型。 例如：
>
>比較屬性 `profile/age`時，您已知道比較的類型是 **number**，因此即使未設定， `profile/age` 小於30的比較也會傳回 `profile/age` false ****，如您預期。

### 引用 {#references}

以下參考是現成可用的，可直接連結至指令碼或其他區段。 它們可從元件瀏覽器拖曳至編輯器。

|  |  |
|---|---|
| 區段引用 | 評估參考的區段 |
| 指令碼引用 | 評估參考的指令碼。 如需詳細資訊，請 [參閱以下使用指令碼](#using-script-references) 參考章節。 |

## 建立新區段 {#creating-a-new-segment}

要定義新段，請執行以下操作：

1. 存 [取區段後](#accessing-segments), [導覽至您要建立區段的資料夾](#organizing-segments) ，或將其保留在根目錄中。

1. 點選或按一下「建 **立** 」按鈕，然後選 **取「建立ContextHub區段」**。

   ![新增區段](../assets/contexthub-create-segment.png)

1. 在「新 **建ContextHub區段**」中，視需要輸入區段的標題和提升值，然後點選或按一下「建 **立」**。

   ![新區段](../assets/contexthub-new-segment.png)

   每個區段都有提升參數，用作加權系數。 數字越高，表示在多個區段有效的例項中，會優先選擇數字較低的區段。

   * Minimum value: `0`
   * Maximum value: `1000000`

1. 從區段主控台，編輯新建立的區段，以在區段編輯器中開啟。
1. 將比較或參考拖曳至區段編輯器，它將會出現在預設的AND容器中。
1. 連按兩下或點選新參考或區段的設定選項，以編輯特定參數。 在此範例中，我們正在為巴塞爾的人員進行測試。

   ![在巴塞爾為人測試](../assets/contexthub-comparing-property-value.png)

   請盡量設 **定「資料類型** 」，以確保正確評估您的比較。 如需詳 [細資訊](#comparisons) ，請參閱比較。

1. 按一 **下「完成** 」以儲存定義：
1. 視需要新增更多元件。 您可以使用AND和OR比較的容器元件來建立布林運算式(請參 [閱下方的使用AND和Or](#using-and-and-or-containers) Containers)。 使用區段編輯器，您可以刪除不再需要的元件，或將元件拖曳至陳述式中的新位置。

### 使用AND和OR容器 {#using-and-and-or-containers}

使用AND和OR容器元件，您可以在AEM中建構複雜的區段。 在執行此動作時，請注意以下幾個基本要點：

* 定義的頂層永遠是最初建立的AND容器。 這無法變更，但對您的其餘區段定義沒有影響。
* 確保容器巢狀結構合理。 容器可以視為布林運算式的括弧。

以下範例用於選取在我們的Swiss目標群組中被視為的訪客：

```text
 People in Basel

 OR

 People in Zürich
```

首先，將OR容器元件放置在預設的AND容器中。 在OR容器中，您可以新增屬性或參考元件。

![使用OR運算子的區段](../assets/contexthub-or-operator.png)

您可以視需要巢狀內嵌多個AND和OR運算子。

### 使用指令碼引用 {#using-script-references}

使用指令碼參考元件，可將區段屬性的評估委派給外部指令碼。 在正確設定指令碼後，它就可當成區段條件的任何其他元件。

#### 定義要引用的指令碼 {#defining-a-script-to-reference}

1. 將檔案新增至 `contexthub.segment-engine.scripts` clientlib。
1. 實作傳回值的函式。 例如：

   ```javascript
   ContextHub.console.log(ContextHub.Shared.timestamp(), '[loading] contexthub.segment-engine.scripts - script.profile-info.js');
   
   (function() {
       'use strict';
   
       /**
        * Sample script returning profile information. Returns user info if data is available, false otherwise.
        *
        * @returns {Boolean}
        */
       var getProfileInfo = function() {
           /* let the SegmentEngine know when script should be re-run */
           this.dependOn(ContextHub.SegmentEngine.Property('profile/age'));
           this.dependOn(ContextHub.SegmentEngine.Property('profile/givenName'));
   
           /* variables */
           var name = ContextHub.get('profile/givenName');
           var age = ContextHub.get('profile/age');
   
           return name === 'Joe' && age === 123;
       };
   
       /* register function */
       ContextHub.SegmentEngine.ScriptManager.register('getProfileInfo', getProfileInfo);
   
   })();
   ```

1. 向註冊指令碼 `ContextHub.SegmentEngine.ScriptManager.register`。

如果指令檔依賴其他屬性，則指令檔應呼叫 `this.dependOn()`。 例如，如果指令檔依賴 `profile/age`:

```javascript
this.dependOn(ContextHub.SegmentEngine.Property('profile/age'));
```

#### 引用指令碼 {#referencing-a-script}

1. 建立ContextHub區段。
1. 將 **Script Reference** （指令碼參考）元件新增至區段的所需位置。
1. 開啟「指令碼參考」元件 **的編輯對話** 方塊。 如果 [已正確設定](#defining-a-script-to-reference)，則指令碼應可在「指令碼名稱 **** 」下拉式清單中使用。

## 組織區段 {#organizing-segments}

如果您有許多區段，它們將變得難以管理為平面清單。 在這種情況下，建立資料夾以管理區段會很有用。

### 建立新資料夾 {#create-folder}

1. 存取 [區段後](#accessing-segments)，按一下或點選「建立」按鈕，然後選取「資料夾」(Folder ********)。

   ![新增資料夾](../assets/contexthub-create-segment.png)

1. 提供資 **料夾的** 「 **標題** 」和「名稱」。
   * 標 **題** (Title)應為描述性。
   * Name **** （名稱）將成為儲存庫中的節點名稱。
      * 它會根據標題自動產生，並根據 [AEM命名慣例進行調整。](/help/implementing/developing/introduction/naming-conventions.md)
      * 如有需要，可加以調整。

   ![建立資料夾](../assets/contexthub-create-folder.png)

1. 點選或按一下「 **建立**」。

   ![確認資料夾](../assets/contexthub-confirm-folder.png)

1. 資料夾會出現在區段清單中。
   * 對列的排序方式將影響新資料夾在清單中的顯示位置。
   * 您可以點選或按一下欄標題來調整排序。
      ![新資料夾](../assets/contexthub-folder.png)

### 修改現有資料夾 {#modify-folders}

1. 存 [取區段後](#accessing-segments)，按一下或點選您要修改的資料夾以選取它。

   ![選取檔案夾](../assets/contexthub-select-folder.png)

1. 點選或按一下工 **具列中的** 「重新命名」，以重新命名檔案夾。

1. 提供新的資 **料夾標題** ，然後點選或按一 **下儲存**。

   ![更名資料夾](../assets/contexthub-rename-folder.png)

>[!NOTE]
>
>重新命名資料夾時，只能變更標題。 無法更改名稱。

### 刪除資料夾

1. 存 [取區段後](#accessing-segments)，按一下或點選您要修改的資料夾以選取它。

   ![選取檔案夾](../assets/contexthub-select-folder.png)

1. 點選或按一 **下工具列** 中的「刪除」，以刪除資料夾。

1. 對話框顯示選定進行刪除的資料夾清單。

   ![確認刪除](../assets/contexthub-confirm-segment-delete.png)

   * 點選或按一下「 **刪除** 」以確認。
   * 點選或按一 **下「取消** 」以中止。

1. 如果任何選取的檔案夾包含子檔案夾或區段，則必須確認其刪除。

   ![確認刪除子項](../assets/contexthub-confirm-segment-child-delete.png)

   * 點選或按一下「 **強制刪除** 」以確認。
   * 點選或按一 **下「取消** 」以中止。

>[!NOTE]
>
> 無法將區段從一個資料夾移至另一個資料夾。

## 測試區段的應用程式 {#testing-the-application-of-a-segment}

定義區段後，就可在 **[ContextHub的協助下測試潛在](contexthub.md)結果。**

1. 預覽頁面
1. 按一下ContextHub圖示以顯示ContextHub工具列
1. 選擇符合您建立之群體的角色
1. ContextHub將解析所選角色的適用區段

例如，我們在巴塞爾識別使用者的簡單區段定義，是根據使用者的位置而定。 載入符合這些條件的特定角色時，會顯示區段已成功解決：

![解析的區段](../assets/contexthub-segment-resolve.png)

或者，如果未解決：

![無法解決的區段](../assets/contexthub-segment-doesnt-resolve.png)

>[!NOTE]
>
>所有特徵都會立即解決，不過大部分只會在頁面重新載入時變更。

此類測試也可以在內容頁面上，並結合目標內容與相關活動 **與****體驗**。

如果您已設定活動和體驗，則可以使用活動輕鬆測試區段。 如需設定活動的詳細資訊，請參閱製作目標 [內容的相關檔案](targeted-content.md)。

1. 在您已設定目標內容之頁面的編輯模式中，您可以看到內容是透過內容上的箭頭圖示來定位。
1. 切換至預覽模式並使用內容中樞，切換至不符合體驗所設定之區段的個人。
1. 切換至符合為體驗設定之區段的人物角色，並查看體驗會隨之變更。

## 使用您的區段 {#using-your-segment}

區段可用來控制特定目標對象所檢視的實際內容。 如需 [觀眾和群體的詳細資訊](audiences.md) ，請參閱管理觀眾，以及製作 [目標內容](targeted-content.md) ，以瞭解如何使用觀眾和群體來定位內容。
