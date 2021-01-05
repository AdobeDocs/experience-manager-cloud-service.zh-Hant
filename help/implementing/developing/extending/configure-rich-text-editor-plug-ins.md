---
title: 在 [!DNL Adobe Experience Manager]中設定Rich Text Editor外掛程式。
description: 瞭解如何設定 [!DNL Adobe Experience Manager] Rich Text Editor外掛程式。
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 6db201f00e8f304122ca8c037998b363ff102c1f
workflow-type: tm+mt
source-wordcount: '4301'
ht-degree: 0%

---


# 設定Rich Text Editor外掛程式{#configure-the-rich-text-editor-plug-ins}

RTE功能可透過一系列外掛程式提供，每個外掛程式都包含features屬性。 您可以配置features屬性以啟用或禁用一個或多個RTE功能。 本文說明如何具體配置RTE插件。

有關其他RTE配置的詳細資訊，請參見[configure Rich Text Editor](/help/implementing/developing/extending/rich-text-editor.md)。

>[!NOTE]
>
>使用CRXDE Lite時，建議使用[!UICONTROL Save All]選項定期保存更改。

## 啟動外掛程式並設定features屬性{#activateplugin}

若要啟動外掛程式，請依照下列步驟進行。 只有在您第一次設定外掛程式時，才需要一些步驟，因為對應的節點不存在。

預設情況下，`format`、`link`、`list`、`justify`和`control`插件及其所有功能都在RTE中啟用。

>[!NOTE]
>
>各自的`rtePlugins`節點稱為`<rtePlugins-node>`，以避免在本文中重複。

1. 使用CRXDE Lite，找出專案的文字元件。
1. 如果`<rtePlugins-node>`的父節點不存在，請先建立&lt;a0/>的父節點，然後再配置任何RTE插件：

   * 根據您的元件，父節點包括：

      * `config: .../text/cq:editConfig/cq:inplaceEditing/config`
      * 替代配置節點：`.../text/cq:editConfig/cq:inplaceEditing/inplaceEditingTextConfig`
      * `text: .../text/dialog/items/tab1/items/text`
   * 類型：**jcr:primaryType** `cq:Widget`
   * 兩者皆具有下列屬性：

      * **名稱** `name`
      * **類型** `String`
      * **值** `./text`


1. 根據您為配置的介面，建立節點`<rtePlugins-node>`（如果節點不存在）:

   * **名稱** `rtePlugins`
   * **類型** `nt:unstructured`

1. 在此下，為要激活的每個插件建立一個節點：

   * **類型** `nt:unstructured`
   * **為** 所需插件的插件ID命名

啟動外掛程式後，請依照下列准則來設定`features`屬性。

|  | 啟用所有功能 | 啟用一些特定功能。 | 停用所有功能。 |
|---|---|---|---|
| 名稱 | 功能 | 功能 | 功能 |
| 類型 | 字串 | `String` (多字串；在CRXDE Lite中將 `String` 文字設 `Multi` 為並按一下) | 字串 |
| 值 | `*` （星號） | 設為一或多個功能值。 | - |

## 瞭解findreplace增效模組{#findreplace}

`findreplace`外掛程式不需要任何設定。 它是現成可用的。

使用替換功能時，應與查找字串同時輸入要替換的替換字串。 不過，您仍可以按一下「尋找」，在取代字串之前先搜尋字串。 如果在按一下「查找」後輸入了替換字串，則搜索將重置為文本的開頭。

當點按尋找時，尋找和取代對話方塊會變為透明，當點按取代時，對話方塊會變成不透明。 此行為可讓作者檢閱要取代的文字。 如果用戶按一下「全部替換」(replace all)，則對話框將關閉並顯示已替換的數量。

## 配置貼上模式{#pastemodes}

使用RTE時，作者可以在以下三種模式之一中貼上內容：

* **瀏覽器模式**:使用瀏覽器的預設貼上實作來貼上文字。它不是建議的方法，因為它可能會引入不想要的標籤。

* **純文字檔案模式**:將剪貼簿內容貼為純文字。在[!DNL Experience Manager]元件中插入之前，它會先從複製的內容移除所有樣式和格式元素。

* **MS Word模式**:從MS Word複製時，使用格式化貼上文字（包括表格）。不支援從其他來源（例如網頁或MS Excel）複製和貼上文字，並僅保留部分格式。

### 配置RTE工具欄{#configure-paste-options-available-on-the-rte-toolbar}上的「貼上」選項

您可以在RTE工具列中為作者提供以下三個表徵圖：

* **[!UICONTROL 貼上(Ctrl+V)]**:可預先設定，以對應上述三種「貼上」模式之一。

* **[!UICONTROL 貼上為文字]**:提供純文字檔案模式功能。

* **[!UICONTROL 從Word貼上]**:提供MS Word模式功能。

要配置RTE以顯示所需的表徵圖，請遵循以下步驟。

1. 導覽至您的元件，例如`/apps/<myProject>/components/text`。
1. 導航至節點`rtePlugins/edit`。 如果節點不存在，請參見[激活插件](#activateplugin)。
1. 在`edit`節點上建立`features`屬性，並添加一個或多個功能。 儲存所有變更。

### 設定「貼上」(Ctrl+V)圖示和捷徑{#configure-the-behavior-of-the-paste-ctrl-v-icon-and-shortcut}的行為

您可以使用下列步驟預先設定&#x200B;**[!UICONTROL 貼上(Ctrl+V)]**&#x200B;圖示的行為。 此設定也定義作者用來貼上內容的鍵盤快速鍵Ctrl+V的行為。

此配置允許以下三種類型的使用案例：

* 使用瀏覽器的預設貼上實作來貼上文字。 它不是建議的方法，因為它可能會引入不想要的標籤。 使用下面的`browser`進行配置。

* 將剪貼簿內容貼為純文字。 在[!DNL Experience Manager]元件中插入之前，它會先從複製的內容移除所有樣式和格式元素。 使用下面的`plaintext`進行配置。

* 從MS Word複製時，使用格式化貼上文字（包括表格）。 不支援從其他來源（例如網頁或MS Excel）複製和貼上文字，並僅保留部分格式。 使用下面的`wordhtml`進行配置。

1. 在元件中，導航至`<rtePlugins-node>/edit`節點。 如果節點不存在，請建立節點。 如需詳細資訊，請參閱[啟用外掛程式](#activateplugin)。
1. 在`edit`節點中，使用以下詳細資訊建立屬性：

   * **名稱** `defaultPasteMode`
   * **類型** `String`
   * **值** 是來自、或模式的所需 `browser`貼上 `plaintext`模式之 `wordhtml` 一。

### 配置貼上內容{#pasteformats}時允許的格式

可進一步配置「貼上方式-Microsoft-Word」(`paste-wordhtml`)模式，以便從其他程式（例如[!DNL Microsoft Word]）貼上至[!DNL Experience Manager]時，您可明確允許一些樣式。

例如，如果在[!DNL Experience Manager]中貼上時僅允許使用粗體格式和清單，則可以篩選掉其他格式。 這稱為可設定的貼上篩選，可針對下列兩種方式執行：

* [文字](#pastemodes)
* [連結](#linkstyles)

對於連結，您也可以定義自動接受的通訊協定。

要配置從另一個程式將文本貼上到[!DNL Experience Manager]時允許使用哪些格式：

1. 在元件中，導航到節點`<rtePlugins-node>/edit`。 如果節點不存在，請建立節點。 如需詳細資訊，請參閱[啟用外掛程式](#activateplugin)。
1. 在`edit`節點下建立一個節點以保存HTML貼上規則：

   * **名稱** `htmlPasteRules`
   * **類型** `nt:unstructured`

1. 在`htmlPasteRules`下建立一個節點，以保存允許的基本格式的詳細資訊：

   * **名稱** `allowBasics`
   * **類型** `nt:unstructured`

1. 要控制接受的各種格式，請在`allowBasics`節點上建立以下一個或多個屬性：

   * **名稱** `bold`
   * **名稱** `italic`
   * **名稱** `underline`
   * **名稱** `anchor` （同時適用於連結和命名定位點）
   * **名稱** `image`

   所有屬性均為&#x200B;**Type** `Boolean`，因此，在適當的&#x200B;**Value**&#x200B;中，您可以選擇或移除複選標籤以啟用或停用功能。

   >[!NOTE]
   >
   >如果未明確定義，則使用預設值true並接受格式。

1. 還可以使用其他屬性或節點範圍定義其他格式，這些屬性或節點也應用於`htmlPasteRules`節點：

| 屬性 | 類型 | 說明 |
|--- |--- |--- |
| `allowBlockTags` | `String` | 定義允許的塊標籤清單。 一些可能的塊標籤包括標題(h1、h2、h3)、段落(p)、清單(ol、ul)、表（表）。 |
| `fallbackBlockTag` | `String` | 定義用於任何塊的塊標籤，該塊標籤具有未包含在`allowBlockTags`中的塊標籤。 通常，`p`足夠。 |
| `table` | `nt:unstructured` | 定義貼上表時的行為。 此節點必須具有允許的屬性（鍵入Boolean），以定義是否允許貼上表。 如果allow設為false，您必須指定屬性ignoreMode（鍵入String），以定義貼上表格內容的處理方式。 ignoreMode的有效值為`remove`以移除表格內容，`paragraph`以將表格儲存格轉換為段落。 |
| `list` | `nt:unstructured` | 定義貼上清單時的行為。 必須具有`allow`屬性（鍵入Boolean），才能定義是否允許貼上清單。 如果`allow`設為`false`，請指定屬性`ignoreMode`（鍵入`String`）以定義如何處理貼上的任何清單內容。 ignoreMode的有效值為`remove`，可移除清單內容，而`paragraph`可將清單項目轉換為段落。 |

有效`htmlPasteRules`結構的示例如下：

```xml
"htmlPasteRules": {
    "allowBasics": {
        "italic": true,
        "link": true
    },
    "allowBlockTags": [
        "p", "h1", "h2", "h3"
    ],
    "list": {
        "allow": false,
        "ignoreMode": "paragraph"
    },
    "table": {
        "allow": true,
        "ignoreMode": "paragraph"
    }
}
```

1. 儲存所有變更。

## 配置文本樣式{#textstyles}

作者可以套用「樣式」來變更部分文字的外觀。 這些樣式是以您在CSS樣式表中預先定義的CSS類別為基礎。 使用`class`屬性將樣式化內容括在`span`標籤中，以引用CSS類別。 例如：

`<span class=monospaced>Monospaced Text Here</span>`

當第一次啟用「樣式」外掛程式時，就不提供預設的「樣式」。 快顯清單是空的。 若要為作者提供樣式，請執行下列動作：

* 啟用「樣式」下拉式選取器。
* 指定樣式表的一個或多個位置。
* 指定可從樣式彈出式清單選取的個別樣式。

對於稍後的重新設定，例如若要新增更多樣式，請只依照指示來參考新的樣式表並指定其他樣式。

>[!NOTE]
>
>還可為[表格或表格儲存格](configure-rich-text-editor-plug-ins.md#tablestyles)定義樣式。 這些配置需要單獨的過程。

### 啟用「樣式」下拉式選擇器清單{#styleselectorlist}

若要這麼做，請啟用樣式外掛程式。

1. 在元件中，導航到節點`<rtePlugins-node>/styles`。 如果節點不存在，請建立節點。 如需詳細資訊，請參閱[啟用外掛程式](#activateplugin)。
1. 在`styles`節點上建立`features`屬性：

   * **名稱** `features`
   * **類型** `String`
   * **值** `*` （星號）

1. 儲存所有變更。

>[!NOTE]
>
>啟用「樣式」外掛程式後，「樣式」下拉式清單就會顯示在編輯對話方塊中。 不過，清單是空的，因為未設定任何樣式。

### 指定樣式表位置{#locationofstylesheet}

然後，指定要參照的樣式表的位置：

1. 導覽至文字元件的根節點，例如`/apps/<myProject>/components/text`。
1. 將屬性`externalStyleSheets`添加到`<rtePlugins-node>`的父節點：

   * **名稱** `externalStyleSheets`
   * **Type** `String[]` (multi-string;按一 **** 下多重CRXDE)
   * **值要包** 含的每個樣式表的路徑和檔案名。使用儲存庫路徑。

   >[!NOTE]
   >
   >您可以隨後將參照添加到其他樣式表。

1. 儲存所有變更。

在對話框(Classic UI)中使用RTE時，可以指定針對富格文本編輯而優化的樣式表。 由於技術限制，CSS內容會在編輯器中遺失，因此您可以模擬此內容以改善WYSIWYG體驗。

Rich Text Editor使用ID為`CQrte`的容器DOM元素，提供不同的樣式來檢視和編輯：

```css
#CQ td {
// defines the style for viewing
 }
```

```css
#CQrte td {
 // defines the style for editing
 }
```

### 在快顯清單中指定可用的樣式{#stylesindropdown}

1. 在元件定義中，導航到在[啟用樣式下拉式選擇器](#styleselectorlist)中建立的節點`<rtePlugins-node>/styles`。
1. 在節點`styles`下，建立一個節點（也稱為`styles`）以保存要提供的清單：

   * **名稱** `styles`
   * **類型** `cq:WidgetCollection`

1. 在`styles`節點下建立一個節點以表示單個樣式：

   * **名稱**，您可以指定名稱，但應適合樣式
   * **類型** `nt:unstructured`

1. 將屬性`cssName`添加到此節點以引用CSS類：

   * **名稱** `cssName`
   * **類型** `String`
   * **值** CSS類別的名稱（不含前面的&#39;.&#39;）;例如，`cssClass`而非`.cssClass`)

1. 將屬性`text`添加到同一節點；這定義了選擇框中顯示的文本：

   * **名稱** `text`
   * **類型** `String`
   * **值** 樣式描述；顯示在「樣式」下拉式選擇框中。

1. 儲存變更。

   對每個所需樣式重複上述步驟。

### 配置RTE，以便在日文{#jpwordwrap}中獲得最佳單字分隔

使用[!DNL Experience Manager]來製作日文語言內容的作者可以套用樣式至字元，以避免在不需要分行符的情況下出現分行符。 這可讓作者讓句子在所要的位置中斷。 此功能的樣式是以CSS樣式表中預先定義的CSS類別為基礎。

若要建立作者可套用至日文文字的樣式，請遵循下列步驟：

1. 在樣式節點下建立節點。 請參閱[指定樣式](#stylesindropdown)。
   * 名稱: `jpn-word-wrap`
   * 類型: `nt:unstructure`

1. 將屬性`cssName`新增至節點以參考CSS類別。 此類別名稱是日文繞字功能的保留名稱。
   * 名稱: `cssName`
   * 類型: `String`
   * 值：`jpn-word-wrap`（不含前面的`.`）

1. 將屬性文本添加到同一節點。 該值是作者在選擇樣式時看到的樣式名稱。
   * 名稱：`text`
*類型： 
`String`
   * 值: `Japanese word-wrap`

1. 建立樣式表並指定其路徑。 請參閱[指定樣式表](#locationofstylesheet)的位置。 將下列內容新增至樣式表。 視需要變更背景顏色。

   ```css
   .text span.jpn-word-wrap {
       display:inline-block;
   }
   .is-edited span.jpn-word-wrap {
       background-color: #ffddff;
   }
   ```

   ![樣式表，讓作者可使用日文繞字功能](assets/rte_jpwordwrap_stylesheet.jpg)

## 配置段落格式{#paraformats}

在RTE中編寫的任何文本都放在塊標籤中，預設值為`<p>`。 啟用`paraformat`外掛程式，即可使用下拉式選擇清單，指定可指派給段落的其他區塊標籤。 段落格式通過指定正確的塊標籤來確定段落類型。 作者可以使用「格式」選擇器來選取並指派它們。 範例區塊標籤包括標準段落&lt;p>和標題&lt;h1>、&lt;h2>等。

>[!CAUTION]
>
>此外掛程式不適用於結構複雜的內容，例如清單或表格。

>[!NOTE]
>
>如果無法將塊標籤（例如`<hr>`標籤）分配給段落，則它不是`paraformat`插件的有效使用案例。

首次啟用「段落格式」外掛程式時，不提供預設的「段落格式」。 快顯清單是空的。 要向作者提供段落格式，請執行以下操作：

* 啟用[!UICONTROL Format]彈出式選擇器清單。
* 指定可從彈出式選單中選取為段落格式的區塊標籤。

如需稍後的重新設定，例如若要新增更多格式，請僅依照說明的相關部分進行。

### 啟用「格式」下拉式選擇器{#formatselectorlist}

要啟用`paraformat`插件，請執行以下步驟：

1. 在元件中，導航到節點`<rtePlugins-node>/paraformat`。 如果節點不存在，請建立節點。 如需詳細資訊，請參閱[啟用外掛程式](#activateplugin)。
1. 在`paraformat`節點上建立`features`屬性：

   * **名稱** `features`
   * **類型** `String`
   * **值** `*` （星號）

>[!NOTE]
>
>如果插件未進一步配置，則啟用的預設格式為段落(`<p>`)、標題1(`<h1>`)、標題2(`<h2>`)、標題3(`<h3>`)。

>[!CAUTION]
>
>在配置RTE的段落格式時，不要將段落標籤&lt;p>作為格式選項刪除。 如果`<p>`標籤被移除，則內容作者即使有其他格式設定，也無法選取[!UICONTROL 段落格式]選項。

### 指定可用的段落格式{#paraformatsindropdown}

段落格式可供以下人員選擇：

1. 在元件定義中，導航到在[啟用格式下拉選擇器](#styleselectorlist)中建立的節點`<rtePlugins-node>/paraformat`。
1. 在`paraformat`節點下建立一個節點，以保存格式清單：

   * **名稱** `formats`
   * **類型** `cq:WidgetCollection`

1. 在`formats`節點下建立節點，它保存單個格式的詳細資訊：

   * **名稱**，您可以指定名稱，但它應適合格式（例如myparagraph、myheading1）。
   * **類型** `nt:unstructured`

1. 要使用此節點，請添加屬性以定義使用的塊標籤：

   * **名稱** `tag`
   * **類型** `String`
   * **值** 格式的塊標籤；例如：p、h1、h2等。

      您不需要輸入定界角括弧。

1. 對於同一節點，添加另一個屬性，以便說明性文本顯示在下拉清單中：

   * **名稱** `description`
   * **類型** `String`
   * **值** 此格式的描述性文字；例如，段落、標題1、標題2等。此文本顯示在「格式」(Format)選擇清單中。

1. 儲存變更。

   對每種必要格式重複步驟。

>[!CAUTION]
如果您定義自訂格式，則會移除預設格式（`<p>`、`<h1>`、`<h2>`和`<h3>`）。 重新建立`<p>`格式，因為它是預設格式。

## 配置特殊字元{#spchar}

在標準的[!DNL Experience Manager]安裝中，當`misctools`外掛程式啟用特殊字元(`specialchars`)時，就可立即使用預設選項；例如，著作權和商標符號。

您可以配置RTE，使選擇的字元可用；定義不同的字元或整個序列。

>[!CAUTION]
新增特殊字元會覆寫預設選擇。 如果需要，請在選取範圍中重新定義這些字元。

### 定義單一字元{#definesinglechar}

1. 在元件中，導航到節點`<rtePlugins-node>/misctools`。 如果節點不存在，請建立節點。 如需詳細資訊，請參閱[啟用外掛程式](#activateplugin)。
1. 在`misctools`節點上建立`features`屬性：

   * **名稱** `features`
   * **類型** `String[]`
   * **值** `specialchars`

          （或`String / *`，如果套用此外掛程式的所有功能）

1. 在`misctools`下建立一個節點以保存特殊字元配置：

   * **名稱** `specialCharsConfig`
   * **類型** `nt:unstructured`

1. 在`specialCharsConfig`下建立另一個節點以保存字元清單：

   * **名稱** `chars`
   * **類型** `nt:unstructured`

1. 在`chars`下添加節點以保存單個字元定義：

   * **名** 稱可以指定名稱，但應反映字元；例如，一半。
   * **類型** `nt:unstructured`

1. 要添加到此節點，請添加以下屬性：

   * **名稱** `entity`
   * **類型** `String`
   * **評** 估所需字元的HTML表示；例如，對 `&189;` 於一半的分數。

1. 儲存變更。

在CRXDE中，保存屬性後，將顯示所表示的字元。 請參閱下方的一半範例。 重複上述步驟，讓作者可使用更多特殊字元。

![在CRXDE中，添加一個要在RTE工具欄中提供的單字元在RTE工具欄中](assets/chlimage_1-106.png "添加一個要在RTE工具欄中提供的單字元")

### 定義字元範圍{#definerangechar}

1. 使用[中的步驟1到3定義單個字元](#definesinglechar)。
1. 在`chars`下添加節點以保存字元範圍的定義：

   * **名** 稱可以指定名稱，但應反映字元範圍；比如鉛筆。
   * **類型** `nt:unstructured`

1. 在此節點下（根據您的特殊字元範圍命名）新增下列兩個屬性：

   * **名稱** `rangeStart`

      **類型** `Long`
      **估** 值范 [](https://unicode.org/) 圍中第一個字元的Unicodederepresentation(decimal)

   * **名稱** `rangeEnd`

      **類型** `Long`
      **估** 值范 [](https://unicode.org/) 圍內最後一個字元的Unicodederepresentation(decimal)

1. 儲存變更。

   例如，定義範圍為9998 - 10000，提供下列字元。

   ![在CRXDE中，定義要在RTE中提供的字元範圍](assets/chlimage_1-107.png)

   *圖：在CRXDE中，定義要在RTE中提供的字元範圍*

   ![RTE中可用的特殊字元在彈出窗口中顯示給作者RTE中可用的特殊](assets/rtepencil.png "字元在彈出窗口中顯示給作者")

## 配置表樣式{#tablestyles}

樣式通常套用在文字上，但也可套用在表格或數個表格儲存格上的個別樣式集。 作者可從「儲存格屬性」或「表格屬性」對話方塊的「樣式選取器」方塊中，使用此類樣式。 在「文本」(Text)元件（或衍生）中編輯表時，這些樣式是可用的，在標準「表」(Table)元件中不可用。

>[!NOTE]
您只能為Classic UI定義表格和儲存格的樣式。

>[!NOTE]
在RTE元件中或從RTE元件中複製和貼上表取決於瀏覽器。 並非所有瀏覽器都可立即使用。 根據表格結構和瀏覽器，您可能會得到不同的結果。 例如，當您在Mozilla Firefox的Classic UI和Touch UI中複製並貼上RTE元件中的表格時，表格的版面不會保留。

1. 在元件中導航到節點`<rtePlugins-node>/table`。 如果節點不存在，請建立節點。 如需詳細資訊，請參閱[啟用外掛程式](#activateplugin)。
1. 在`table`節點上建立`features`屬性：

   * **名稱** `features`
   * **類型** `String`
   * **值** `*`

   >[!NOTE]
   如果不想啟用所有表功能，可以將`features`屬性建立為：
   * **類型** `String[]`

   * **視需要**，為下列其中一項或兩項設定值：
      * `table` 允許編輯表屬性；包括樣式。
      * `cellprops` 以允許編輯儲存格屬性，包括樣式。


1. 定義CSS樣式表的位置以參照這些樣式表。 請參閱[指定樣式表的位置](#locationofstylesheet)，因為這與定義文本](#textstyles)的[樣式時相同。 如果定義了其他樣式，則可定義該位置。
1. 在`table`節點下，根據需要建立以下節點：

   * 要定義整個表的樣式（可在&#x200B;**[!UICONTROL 表屬性]**&#x200B;下使用）:

      * **名稱** `tableStyles`
      * **類型** `cq:WidgetCollection`
   * 要定義各個單元格的樣式（可在&#x200B;**[!UICONTROL 單元格屬性]**&#x200B;下使用）,

      * **名稱** `cellStyles`
      * **類型** `cq:WidgetCollection`


1. 建立節點（在`tableStyles`或`cellStyles`節點下，視情況建立）以表示單個樣式，

   * **名** 稱可指定名稱，但應反映樣式。
   * **類型** `nt:unstructured`

1. 在此節點上建立以下屬性：

   * 若要定義參考的CSS樣式，

      * **名稱** `cssName`
      * **類型** `String`
      * **值** CSS類別的名稱(例如，不含 `.`前面的 `cssClass` 名稱 `.cssClass`)
   * 要定義要顯示在彈出式選擇器中的描述性文本，

      * **名稱** `text`
      * **類型** `String`
      * **估** 值要出現在選擇清單中的文本


1. 儲存所有變更。

對每個所需樣式重複上述步驟。

### 為協助工具{#hiddenheader}設定表格中的隱藏標題

有時，您可能會在欄標題中建立不含視覺文字的資料表格，並假設欄與其他欄的視覺關係暗示標題的用途。 在這種情況下，必須在標題儲存格的儲存格內提供隱藏的內文，讓螢幕閱讀程式和其他輔助技術協助有不同需求的讀者瞭解欄目的用途。

為了增強此類場景中的輔助功能，RTE支援隱藏的標題單元格。 此外，它還提供與表格中隱藏標題相關的配置設定。 這些設定可讓您在編輯和預覽模式中，將CSS樣式套用至隱藏的標題。 若要協助作者在編輯模式中識別隱藏的標題，請在程式碼中加入下列參數：

* `hiddenHeaderEditingCSS`:指定編輯RTE時，在隱藏標題單元格上應用的CSS類的名稱。
* `hiddenHeaderEditingStyle`:指定在編輯RTE時應用於隱藏標題單元格的樣式字串。

如果您在程式碼中同時指定CSS和Style字串，CSS類別會優先於樣式字串，而且可能會覆寫Style字串所做的任何設定變更。

若要協助作者在預覽模式中將CSS套用在隱藏的標題上，您可在程式碼中加入下列參數：

* `hiddenHeaderClassName`:指定在預覽模式中套用在隱藏標題儲存格上的CSS類別名稱。
* `hiddenHeaderStyle`:指定在預覽模式下應用於隱藏標題單元格的樣式字串。

如果您在程式碼中同時指定CSS和Style字串，CSS類別會優先於樣式字串，而且可能會覆寫Style字串所做的任何設定變更。

## 為拼寫檢查器{#adddict}添加字典

當spellcheck外掛程式啟動時，RTE會針對每個適當的語言使用字典。 然後根據網站的語言選擇，分別從子樹中抽取語言屬性或從URL中抽取語言；例如。 `/en/`分支會勾選為英文，而`/de/`分支則為德文。

>[!NOTE]
訊息「拼字檢查失敗」。 is seen if a check is treed for a language that is not installed.

標準的Experience Manager安裝包含下列字典：

* 美國英文(en_us)
* 英文(en_gb)

>[!NOTE]
標準字典位於`/libs/cq/spellchecker/dictionaries`，以及適當的讀我檔案。 請勿修改檔案。

若要新增更多字典，請依照下列步驟進行。

1. 導覽至頁面[https://extensions.openoffice.org/](https://extensions.openoffice.org/)。
1. 選擇所需的語言並下載具有拼寫定義的ZIP檔案。 解壓檔案系統上的存檔內容。

   >[!CAUTION]
   僅支援`MySpell`格式的OpenOffice.org v2.0.1或更舊版本字典。 由於字典現在是封存檔案，因此建議您在下載後確認封存。

1. 找到。aff和。dic檔案。 將檔案名稱保留為小寫。 例如，`de_de.aff`和`de_de.dic`。
1. 在`/apps/cq/spellchecker/dictionaries`的儲存庫中載入。aff和。dic檔案。

>[!NOTE]
RTE拼字檢查器是隨選的。 當您開始輸入文字時，它不會自動執行。
若要執行拼字檢查程式，請點選／按一下工具列上的「拼字檢查程式」按鈕。 RTE會檢查單字的拼字，並反白顯示拼字錯誤的單字。
如果您加入拼字檢查程式所建議的任何變更，文字變更和拼字錯誤的字詞狀態將不再反白顯示。 要運行拼字檢查器，請再次點選／按一下「拼字檢查器」按鈕。

## 配置還原和重做操作的歷史記錄大小{#undohistory}

RTE允許作者還原或重做最後幾次編輯。 依預設，50個編輯會儲存在歷史記錄中。 您可以視需要設定此值。

1. 在元件中導航到節點`<rtePlugins-node>/undo`。 如果節點不存在，請建立這些節點。 如需詳細資訊，請參閱[啟用外掛程式](#activateplugin)。
1. 在`undo`節點上建立屬性：

   * **名稱** `maxUndoSteps`
   * **類型** `Long`
   * **估** 計要保存在歷史記錄中的撤消步驟數。預設值為50。 使用`0`可完全停用還原／重做。

1. 儲存變更。

## 配置頁籤大小{#tabsize}

當在任何文本中按下Tab字元時，將插入預定數量的空格；預設情況下，這是三個非斷開空格和一個空格。

要定義標籤大小，請執行以下操作：

1. 在元件中，導航到節點`<rtePlugins-node>/keys`。 如果節點不存在，請建立節點。 如需詳細資訊，請參閱[啟用外掛程式](#activateplugin)。
1. 在`keys`節點上建立屬性：

   * **名稱** `tabSize`
   * **類型** `String`
   * **估** 計用於表格的空格字元數。

1. 儲存變更。

## 設定縮進邊界{#indentmargin}

啟用縮進（預設）時，可以定義縮進大小：

>[!NOTE]
此縮進大小僅應用於文本的段落（塊）;它不會影響實際清單的縮進。

1. 在元件中導航到節點`<rtePlugins-node>/lists`。 如果節點不存在，請建立這些節點。 如需詳細資訊，請參閱[啟用外掛程式](#activateplugin)。
1. 在`lists`節點上建立`identSize`參數：

   * **名稱**:  `identSize`
   * **類型**:  `Long`
   * **值**:縮進邊界所需的像素數。

## 配置可編輯空間{#editablespace}的高度

可定義元件對話框中顯示的可編輯空間的高度。 只有在對話框中使用RTE時，此配置才適用。 配置不會更改對話框窗口的高度。

1. 在`../items/text`節點中，在元件的對話框定義中，建立一個屬性：

   * **名稱** `height`
   * **類型** `Long`
   * **以像** 素為單位來評估編輯畫布的高度。

1. 儲存變更。

## 配置連結{#linkstyles}的樣式和協定

在[!DNL Experience Manager]中新增連結時，您可以定義要使用的CSS樣式和自動接受的通訊協定。 若要設定如何從其他程式在[!DNL Experience Manager]中新增連結，請定義HTML規則。

1. 使用CRXDE Lite，找出專案的文字元件。
1. 建立與`<rtePlugins-node>`級別相同的節點，即在`<rtePlugins-node>`的父節點下建立節點：

   * **名稱** `htmlRules`
   * **類型** `nt:unstructured`

   >[!NOTE]
   `../items/text`節點具有以下屬性：
   * **名稱** `xtype`
   * **類型** `String`
   * **值** `richtext`

   `../items/text`節點的位置可能有所不同，具體取決於對話框的結構。 `/apps/myProject>/components/text/dialog/items/text`和`/apps/<myProject>/components/text/dialog/items/panel/items/text`是兩個範例。

1. 在`htmlRules`下，建立節點。

   * **名稱** `links`
   * **類型** `nt:unstructured`

1. 在`links`節點下，根據需要定義屬性：

   * 內部連結的CSS樣式：

      * **名稱** `cssInternal`
      * **類型** `String`
      * **** 值CSS類的名稱（不帶前面的&#39;.&#39;）;例如，`cssClass`而非`.cssClass`)
   * 外部連結的CSS樣式

      * **名稱** `cssExternal`
      * **類型** `String`
      * **** 值CSS類的名稱（不帶前面的&#39;.&#39;）;例如，`cssClass`而非`.cssClass`)
   * 有效&#x200B;**[!UICONTROL 協定]**&#x200B;的陣列，包括`https://`、`https://`、`file://`、`mailto:`等，

      * **名稱** `protocols`
      * **類型** `String[]`
      * **值**，一個或多個協定
   * **defaultProtocol** ( **String**&#x200B;類型的屬性):當用戶未明確指定協定時使用的協定。

      * **名稱** `defaultProtocol`
      * **類型** `String`
      * **值**，一個或多個預設協定
   * 如何處理連結的目標屬性的定義。 建立節點：

      * **名稱** `targetConfig`
      * **類型** `nt:unstructured`

      在節點`targetConfig`上：定義所需屬性：

      * 指定目標模式：

         * **名稱** `mode`
         * **類型** `String`)
         * **值**:

            * `auto`:意指自動選取目標

               （由`targetExternal`屬性為外部連結指定，或`targetInternal`為內部連結指定）。

            * `manual`:不適用於此上下文
            * `blank`:不適用於此上下文
      * 內部連結的目標：

         * **名稱** `targetInternal`
         * **類型** `String`
         * **評** 估內部連結的目標(僅在模式為時使用 `auto`)
      * 外部連結的目標：

         * **名稱** `targetExternal`
         * **類型** `String`
         * **評** 估外部連結的目標(僅在模式為時 `auto`使用)。








1. 儲存所有變更。
