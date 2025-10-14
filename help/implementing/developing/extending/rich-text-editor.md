---
title: 設定RTF編輯器以在 [!DNL Adobe Experience Manager] as a Cloud Service中編寫內容。
description: 設定RTF編輯器以在 [!DNL Adobe Experience Manager] as a Cloud Service中編寫內容。
contentOwner: AG
exl-id: 1f0ff800-5e95-429a-97f2-221db0668170
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 2c1b444d7b7dad94cc9ebda59783f9c6fde84a91
workflow-type: tm+mt
source-wordcount: '1892'
ht-degree: 0%

---


# 設定RTF編輯器 {#configure-the-rich-text-editor}

RTF編輯器(RTE)為作者提供編輯文字內容的廣泛功能。 提供圖示、選取方塊、工具列和功能表，以提供WYSIWYG文字編輯體驗。 管理員會設定RTE，以啟用、停用及擴充編寫元件中可用的功能。 瞭解作者[如何使用RTE來編寫](/help/sites-cloud/authoring/page-editor/rich-text-editor.md)網頁內容。

以下列出設定RTE所需的概念和步驟。

| 瞭解RTE概念 | 啟用必要功能 | 設定個別功能 |
|---|---|---|
| [瞭解介面](#understand-rte-ui) | [瞭解並設定設定位置](#understand-the-configuration-paths-and-locations) | [設定外掛程式](#enable-rte-functionalities-by-activating-plug-ins) |
| [編輯模式型別](#editingmodes) | [啟動外掛程式](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#activateplugin) | [設定功能屬性](#aboutplugins) |
| [關於外掛程式](#aboutplugins) | [設定RTE工具列](#dialogfullscreen) | [設定貼上模式](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#textstyles) |

>[!NOTE]
>
>本檔案說明的RTE說明「頁面編輯器」中可用的RTE。 如果您使用現代通用編輯器，請參閱檔案[設定通用編輯器的RTE](/help/implementing/universal-editor/configure-rte.md)以取得詳細資料。

## 瞭解作者可用的使用者介面 {#understand-rte-ui}

RTE介面為製作環境提供[回應式設計](/help/sites-cloud/authoring/page-editor/responsive-layout.md)。 此介面專為觸控和桌上型裝置所設計。

![&#x200B; RTF編輯器工具列](assets/rte-toolbar-full-screen-mode.png)

*圖： RTF編輯器工具列已啟用所有可用選項。*

工具列提供WYSIWYG製作體驗的選項。 [!DNL Experience Manager]管理員可以在介面的工具列中設定可用選項。 [!DNL Experience Manager]預設提供完整的編輯選項組。 開發人員可以自訂[!DNL Experience Manager]以新增更多編輯選項。

## 各種編輯模式 {#editingmodes}

作者可以使用不同的元件模式，在[!DNL Experience Manager]中建立和編輯文字內容。 製作和格式化內容的工具列選項，以及不同編輯模式中RTE啟用元件的使用者體驗，會因RTE設定而異。

| 編輯模式 | 編輯區域 | 建議啟用的功能 |
|--- |--- |--- |
| 內嵌 | 就地編輯以進行快速、次要的編輯；格式化而不開啟對話方塊。 | 最小化RTE功能。 |
| RTE全熒幕 | 涵蓋整個頁面。 | 所有必要的RTE功能。 |
| 對話方塊 | 對話方塊位於頁面內容上方，但不會涵蓋整個頁面。 | 謹慎地啟用功能。 |
| 對話方塊全熒幕 | 與全熒幕模式相同；包含對話方塊的欄位以及RTE。 | 所有必要的RTE功能。 |

>[!NOTE]
>
>來源編輯功能在內嵌編輯模式中無法使用。 您無法在全熒幕模式中拖曳影像。 所有其他功能在所有模式中皆可運作。

### 內嵌編輯 {#inline-editing}

若要編輯頁面中的內容，請以慢速按兩下來開啟內容。 將顯示包含基本選項的精簡工具列。

![使用工具列中的基本選項進行內嵌編輯](assets/inline-editing-mode-basic-options.png)

*圖：使用工具列中的基本選項進行內嵌編輯。*

### 全熒幕編輯 {#full-screen-editing}

可以在隱藏頁面內容並佔用可用熒幕的全熒幕檢視中開啟[!DNL Experience Manager]元件。 請考慮以全熒幕編輯內嵌編輯的詳細版本，因為它提供最多的編輯選項。 使用內嵌編輯模式時，可從壓縮工具列按一下![圖示以全熒幕](assets/rte_fullscreen.png)開啟RTE。

在對話方塊全熒幕模式以及詳細的RTE工具列中，對話方塊中可用的選項和元件也可使用。 它僅適用於包含RTE以及其他元件的對話方塊。

![以全熒幕模式編輯時的詳細RTE工具列](assets/rte-toolbar-full-screen-mode.png)

*圖：以全熒幕模式編輯時的詳細RTE工具列。*

### 對話方塊編輯 {#dialog-editing}

當元件按兩下時，會開啟對話方塊以編輯內容。 對話方塊會在現有頁面上方開啟。 在某些特定情況下，對話方塊會以快顯視窗開啟。 例如，當文字元件是多欄頁面配置中的一欄，且可用於對話方塊的區域較少時。

![對話方塊編輯模式](assets/dialog_editing_modetouchui.png)

*圖：對話方塊編輯模式。*

## 關於RTE外掛程式和相關功能 {#aboutplugins}

此功能透過一系列外掛程式提供，每個外掛程式具有：

* `features`屬性，也就是

   * 用來啟用或停用該外掛程式的基本功能。
   * 使用標準化的程式進行設定。

* 適當時，提供更多需要專門設定的屬性和選項。

RTE的基本功能會由適當外掛程式特定節點上的`features`屬性值啟用或停用。

下表列出目前的外掛程式，其中顯示：

* 外掛程式ID及API檔案連結。 [啟用外掛程式](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#activateplugin)時，會將ID用作節點名稱。
* `features`屬性的允許值。
* 外掛程式所提供功能的說明。

| 外掛程式ID | 功能 | 說明 |
|--- |--- |--- |
| 編輯 | `cut`，`copy`，`paste-default`，`paste-plaintext`，`paste-wordhtml` | [剪下、複製和三種貼上模式](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#textstyles)。 |
| findreplace | `find`、`replace` | 尋找和取代。 |
| 格式 | `bold`、`italic`、`underline` | [基本文字格式](configure-rich-text-editor-plug-ins.md#textstyles)。 |
| 影像 | `image` | 基本影像支援（從內容或內容尋找器拖曳）。 根據瀏覽器的不同，支援對作者有不同的行為 |
| 金鑰 | - | 若要定義此值，請參閱[索引標籤大小](configure-rich-text-editor-plug-ins.md#tabsize)。 |
| 左右對齊 | `justifyleft`、`justifycenter`、`justifyright` | 段落對齊方式。 |
| 連結 | `modifylink`、`unlink`、`anchor` | [超連結和錨點](configure-rich-text-editor-plug-ins.md#linkstyles)。 |
| 清單 | `ordered`、`unordered`、`indent`、`outdent` | 此外掛程式同時控制[縮排和清單](configure-rich-text-editor-plug-ins.md#indentmargin)；包括巢狀清單。 |
| misctools | `specialchars`、`sourceedit` | 其他工具可讓作者輸入[特殊字元](configure-rich-text-editor-plug-ins.md#spchar)或編輯HTML來源。 此外，如果您想要定義自己的清單，可以新增[範圍的特殊字元](configure-rich-text-editor-plug-ins.md#definerangechar)。 |
| 引數格式 | `paraformat` | 預設的段落格式為段落、標題1、標題2和標題3 （`<p>`、`<h1>`、`<h2>`和`<h3>`）。 您可以[新增更多段落格式](configure-rich-text-editor-plug-ins.md#paraformats)或擴充清單。 |
| 拼字檢查 | `checktext` | [語言感知拼字檢查程式](configure-rich-text-editor-plug-ins.md#adddict)。 |
| 樣式 | `styles` | 支援使用CSS類別設定樣式。 [如果您想要新增（或擴充）自己的樣式範圍以搭配文字使用，請新增文字樣式](configure-rich-text-editor-plug-ins.md#textstyles)。 |
| 下標 | `subscript`、`superscript` | 基本格式的擴充功能，可新增sub-script和super-script。 |
| 表格 | `table`、`removetable`、`insertrow`、`removerow`、`insertcolumn`、`removecolumn`、`cellprops`、`mergecells`、`splitcell`、`selectrow`、`selectcolumns` | 請參閱[設定表格樣式](configure-rich-text-editor-plug-ins.md#tablestyles)，為整個表格或個別儲存格新增您自己的樣式。 |
| 復原 | `undo`、`redo` | [復原與重做](configure-rich-text-editor-plug-ins.md#undohistory)作業的歷史記錄大小。 |

>[!NOTE]
>
>對話方塊模式不支援全熒幕外掛程式。 使用`dialogFullScreen`設定來設定全熒幕模式的工具列。

## 瞭解設定路徑和位置 {#understand-the-configuration-paths-and-locations}

當您[啟動RTE外掛程式](#editingmodes)時，RTE編輯的[模式和您為作者提供的介面](configure-rich-text-editor-plug-ins.md#activateplugin)將決定組態詳細資料的位置。 位置包括：

* 內嵌模式： `cq:editConfig/cq:inplaceEditing`。
* 全熒幕模式： `cq:editConfig/cq:inplaceEditing`。
* 對話方塊模式： `cq:dialog`。
* 全熒幕對話方塊模式： `cq:dialog`。

>[!NOTE]
>
>請勿將`cq:inplaceEditing`下的節點命名為`config`。 在`cq:inplaceEditing`節點上，定義下列屬性：
>
>* **名稱**：`configPath`
>* **類型**：`String`
>* **值**：包含實際組態的節點路徑
>
>不要將RTE設定節點命名為`config`。 否則，RTE設定只對管理員生效，對群組`content-author`中的使用者則不會生效。

設定以下適用於對話方塊編輯模式的屬性：

* `useFixedInlineToolbar`：您可以使RTE工具列固定而非浮動。 在sling:resourceType= `cq/gui/components/authoring/dialog/richtext`的RTE節點上設定這個定義為`True`的布林值屬性。 當此屬性設定為`True`時，RTF編輯會在`foundation-contentloaded`事件上開始。 若要防止此情況，請將屬性`customStart`設定為`True`並觸發`rte-start`事件以開始RTE編輯。 當這個屬性是`true`時，RTE不會在按一下時開始，而且這是預設行為。

* `customStart`：將這個RTE節點上定義的布林值屬性設定為`True`，以透過觸發事件`rte-start`來控制何時啟動RTE。

* `rte-start`：在RTE的`contenteditable-div`開始編輯RTE時觸發此事件。 只有在`customStart`設定為`true`時才有作用。

當觸控式對話方塊中使用RTE時，請將屬性`useFixedInlineToolbar`設定為`true`以避免問題。

## 透過啟用外掛程式來啟用RTE功能 {#enable-rte-functionalities-by-activating-plug-ins}

RTE功能可透過一系列外掛程式使用，每個外掛程式都具備功能屬性。 您可以設定功能屬性，以啟用或停用每個外掛程式的各種功能。

如需RTE外掛程式的詳細設定，請參閱[如何啟用及設定RTE外掛程式](configure-rich-text-editor-plug-ins.md)。

<!-- TBD ENGREVIEW: To confirm if the sample works in CS or not?
**Sample**: Download [this sample configuration](/help/sites-administering/assets/rte-sample-all-features-enabled-10.zip) that illustrates how to configure RTE. In this package all the features are enabled. -->

[核心元件文字元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html?lang=zh-Hant#the-text-component-and-the-rich-text-editor)可讓範本編輯器使用使用者介面作為內容原則來設定許多RTE外掛程式，而不需要技術設定。 內容原則可搭配使用RTE UI設定，如本檔案所述。 如需詳細資訊，請參閱[建立頁面範本](/help/sites-cloud/authoring/page-editor/templates.md)以及[核心元件開發人員檔案](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html?lang=zh-Hant)。

>為了參考之用，預設Text元件（作為標準安裝的一部分提供）可在以下位置找到：
>
>* `/libs/wcm/foundation/components/text`
>* `/libs/foundation/components/text`
>
>若要建立自己的文字元件，請複製上述元件，而非編輯這些元件。

## 設定RTE工具列 {#dialogfullscreen}

[!DNL Experience Manager]可讓您針對不同的編輯模式，以不同方式設定RTF編輯器的介面。 預設設定如下。 您可以根據需求覆寫這些預設值。 您只需自訂要提供給作者的工具列功能。 您不需要指定所有的工具列設定。

若要設定`dialogFullScreen`的工具列，請使用下列範例設定。

```java
<uiSettings jcr:primaryType="nt:unstructured">
  <cui jcr:primaryType="nt:unstructured">
    <inline
      jcr:primaryType="nt:unstructured"
      toolbar="[format#bold,format#italic,format#underline,#justify,#lists,links#modifylink,links#unlink,#paraformat]">
      <popovers jcr:primaryType="nt:unstructured">
        <justify
          jcr:primaryType="nt:unstructured"
          items="[justify#justifyleft,justify#justifycenter,justify#justifyright,justify#justifyjustify]"
          ref="justify"/>
        <lists
          jcr:primaryType="nt:unstructured"
          items="[lists#unordered,lists#ordered,lists#outdent,lists#indent]"
          ref="lists"/>
        <paraformat
          jcr:primaryType="nt:unstructured"
          items="paraformat:getFormats:paraformat-pulldown"
          ref="paraformat"/>
      </popovers>
    </inline>
    <dialogFullScreen
      jcr:primaryType="nt:unstructured"
      toolbar="[format#bold,format#italic,format#underline,justify#justifyleft,justify#justifycenter,justify#justifyright,justify#justifyjustify,lists#unordered,lists#ordered,lists#outdent,lists#indent,links#modifylink,links#unlink,table#createoredit,#paraformat,image#imageProps]">
      <popovers jcr:primaryType="nt:unstructured">
        <paraformat
          jcr:primaryType="nt:unstructured"
          items="paraformat:getFormats:paraformat-pulldown"
          ref="paraformat"/>
      </popovers>
    </dialogFullScreen>
    <tableEditOptions
      jcr:primaryType="nt:unstructured"
      toolbar="[table#insertcolumn-before,table#insertcolumn-after,table#removecolumn,-,table#insertrow-before,table#insertrow-after,table#removerow,-,table#mergecells-right,table#mergecells-down,table#mergecells,table#splitcell-horizontal,table#splitcell-vertical,-,table#selectrow,table#selectcolumn,-,table#ensureparagraph,-,table#modifytableandcell,table#removetable,-,undo#undo,undo#redo,-,table#exitTableEditing,-]">
    </tableEditOptions>
  </cui>
</uiSettings>
```

內嵌模式和全熒幕模式會使用不同的使用者介面設定。 toolbar屬性指定工具列的選項。

例如，如果選項本身是功能（例如，`Bold`），則會將其指定為`PluginName#FeatureName` （例如，`links#modifylink`）。

如果選項是彈出視窗（包含外掛程式的部分功能），則會將其指定為`#PluginName` （例如`#format`）。

選項群組之間的分隔符號(`|`)可以使用`-`指定。

內嵌或全熒幕模式下的快顯視窗節點包含所使用的快顯視窗清單。 `popovers`節點下的每個子節點都會以外掛程式（例如格式）命名。 其屬性「items」包含外掛程式的功能清單（例如，format#bold）。

## RTE使用者介面設定和內容原則 {#rtecontentpolicies}

管理員可以使用內容原則來控制RTE選項，而不是如上所述進行設定。 當內容原則用作[可編輯的範本](/help/sites-cloud/authoring/page-editor/templates.md)的一部分時，會定義元件的設計屬性。 例如，如果使用RTE的文字元件搭配可編輯的範本使用，則內容原則可定義粗體選項為可用，而一些段落格式選項為可用。 內容原則可重複使用，並可套用至多個範本。

RTE中可用的選項會從使用者介面設定向下流向內容原則。

* 使用者介面組態設定會定義哪些選項可供內容原則使用。
* 如果RTE的使用者介面設定已移除或未啟用專案，則內容原則無法進行設定。
* 作者只能存取使用者介面設定和內容原則所提供的功能。

例如，您可以看到[文字核心元件檔案](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html?lang=zh-Hant#the-text-component-and-the-rich-text-editor)。

## 自訂工具列圖示和命令之間的對應 {#iconstoolbar}

您可以自訂RTE工具列上顯示的Coral圖示與可用命令之間的對應。 除了Coral圖示以外，您無法使用任何其他圖示。

1. 在`icons`下建立名為`uiSettings/cui`的節點。

1. 為下方的個別圖示建立節點。
1. 在每個圖示節點上，指定Coral圖示和對映至圖示的命令。

以下是將命令`Bold`對應到名為`textItalic`的Coral圖示的範例片段。

```java
<text jcr:primaryType="nt:unstructured" sling:resourceType="cq/gui/components/authoring/dialog/richtext" name="./text" useFixedInlineToolbar="{Boolean}true">
    <rtePlugins jcr:primaryType="nt:unstructured">
        <format jcr:primaryType="nt:unstructured" features="bold,italic"/>
    </rtePlugins>
    <uiSettings jcr:primaryType="nt:unstructured">
        <cui jcr:primaryType="nt:unstructured">
            <inline jcr:primaryType="nt:unstructured"
                toolbar="[format#bold,format#italic,format#underline,links#modifylink,links#unlink]">
            </inline>
            <icons jcr:primaryType="nt:unstructured">
                <bold jcr:primaryType="nt:unstructured"
                    command="format#bold"
                    icon="textItalic"/>
            </icons>
        </cui>
    </uiSettings>
</text>
```

## 已知限制 {#known-limitations}

[!DNL Experience Manager] RTE功能有下列限制：

* 只有[!DNL Experience Manager]元件對話方塊才支援RTE功能。 精靈或Foundation-forms不支援RTE。

* [!DNL Experience Manager]無法在混合裝置上運作。<!-- TBD: Check. This is not mentioned in Known Issue /help/release-notes/known-issues.md-->

* 不要命名RTE設定節點`config`。 否則，RTE組態只對管理員生效，對群組`content-author`中的使用者則不會生效。

* RTE不支援內嵌內容至內嵌框架或iframe。

## 最佳作法和秘訣 {#best-practices-and-tips}

* 對於浮動對話方塊，請僅啟用外掛程式，而不使用快顯對話方塊。 沒有快顯視窗的外掛程式尺寸較小，最適合用於浮動對話方塊。
* 只有在全熒幕對話方塊模式或全熒幕模式中，才可使用較大的快顯視窗來啟用外掛程式，例如`Paste`外掛程式。 具有大型快顯視窗的外掛程式需要更多熒幕空間，才能提供良好的撰寫體驗。
* 如果您使用CoralUI3 RTE的自訂外掛程式，請使用`rte.coralui3`資料庫。

>[!MORELIKETHIS]
>
>* [設定RTE外掛程式](configure-rich-text-editor-plug-ins.md)
>* [使用RTF編輯器進行編寫](/help/sites-cloud/authoring/page-editor/rich-text-editor.md)
>* [為可存取的網站設定RTE](rte-accessible-content.md)
