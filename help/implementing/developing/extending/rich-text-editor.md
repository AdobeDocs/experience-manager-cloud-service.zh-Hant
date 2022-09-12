---
title: 設定RTF編輯器以在中製作內容 [!DNL Adobe Experience Manager] as a Cloud Service。
description: 設定RTF編輯器以在中製作內容 [!DNL Adobe Experience Manager] as a Cloud Service。
contentOwner: AG
exl-id: 1f0ff800-5e95-429a-97f2-221db0668170
source-git-commit: f5f2c7c4dfacc113994c380e8caa37508030ee92
workflow-type: tm+mt
source-wordcount: '1964'
ht-degree: 0%

---

# 設定RTF編輯器 {#configure-the-rich-text-editor}

RTF編輯器(RTE)為作者提供多種編輯文字內容的功能。 WYSIWYG文字編輯體驗提供圖示、選取方塊、工具列和功能表。 管理員設定RTE以啟用、停用和擴充製作元件中可用的功能。 了解作者的方式 [使用RTE進行編寫](/help/sites-cloud/authoring/fundamentals/rich-text-editor.md) 網頁內容。

以下列出設定RTE的必要概念和步驟。

| 了解RTE概念 | 啟用必要功能 | 設定個別功能 |
|---|---|---|
| [了解介面](#understand-rte-ui) | [了解並設定設定位置](#understand-the-configuration-paths-and-locations) | [設定外掛程式](#enable-rte-functionalities-by-activating-plug-ins) |
| [編輯模式類型](#editingmodes) | [啟用外掛程式](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#activateplugin) | [設定功能屬性](#aboutplugins) |
| [關於外掛程式](#aboutplugins) | [配置RTE工具欄](#dialogfullscreen) | [設定貼上模式](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#textstyles) |

## 了解可供作者使用的使用者介面 {#understand-rte-ui}

RTE介面提供 [回應式設計](/help/sites-cloud/authoring/features/responsive-layout.md) ，以製作環境。 此介面專為在觸控式和桌上型電腦上使用而設計。

![RTF編輯器工具列](assets/rte-toolbar-full-screen-mode.png)

*圖：RTF編輯器工具列，並啟用所有可用選項。*

工具列提供WYSIWYG製作體驗的選項。 [!DNL Experience Manager] 管理員可以配置介面工具欄中的可用選項。 預設提供一組完整的編輯選項，位於 [!DNL Experience Manager]. 開發人員可自訂 [!DNL Experience Manager] 添加更多編輯選項。

## 各種編輯模式 {#editingmodes}

作者可在 [!DNL Experience Manager] 使用不同的元件模式。 用於編寫和格式化內容的工具列選項以及不同編輯模式下啟用RTE的元件的用戶體驗，會因RTE配置而異。

| 編輯模式 | 編輯區域 | 要啟用的建議功能 |
|--- |--- |--- |
| 內嵌 | 就地編輯，以快速、微幅編輯；格式，不開啟對話框。 | 最小RTE功能。 |
| RTE全螢幕 | 涵蓋整個頁面。 | 所有必要的RTE功能。 |
| 對話方塊 | 對話方塊，但不涵蓋整個頁面。 | 審慎啟用功能。 |
| 全螢幕對話方塊 | 與全螢幕模式相同；包含與RTE一起的對話框欄位。 | 所有必要的RTE功能。 |

>[!NOTE]
>
>在內聯編輯模式下，源編輯功能不可用。 您無法以全螢幕模式拖曳影像。 所有其他功能都可在所有模式中運作。

### 內嵌編輯 {#inline-editing}

若要編輯頁面內的內容，請以慢速連按兩下來開啟內容。 提供包含基本選項的緊湊型工具列。

![使用工具列中的基本選項進行內嵌編輯](assets/inline-editing-mode-basic-options.png)

*圖：內嵌編輯與工具列中的基本選項。*

### 全螢幕編輯 {#full-screen-editing}

[!DNL Experience Manager] 元件可以以全螢幕檢視開啟，隱藏頁面內容並佔據可用螢幕。 請考慮以全螢幕編輯詳細的內嵌編輯版本，因為它提供最多的編輯選項。 可按一下 ![以全螢幕開啟RTE的圖示](assets/rte_fullscreen.png)，即可在使用內嵌編輯模式時從緊密工具列取得。

在對話框全螢幕模式中，以及詳細的RTE工具欄，還可以使用對話框中可用的選項和元件。 此變數僅適用於包含RTE與其他元件的對話方塊。

![以全螢幕模式編輯時的詳細RTE工具列](assets/rte-toolbar-full-screen-mode.png)

*圖：以全螢幕模式編輯時的詳細RTE工具列。*

### 對話方塊編輯 {#dialog-editing}

按兩下元件時，將開啟用於編輯內容的對話框。 對話框將在現有頁面的頂部開啟。 在某些特定情況下，對話方塊會以快顯視窗的形式開啟。 例如，當文本元件是多列頁面佈局中列的一部分時，對話框的可用區域較小。

![對話方塊編輯模式](assets/dialog_editing_modetouchui.png)

*圖：對話框編輯模式。*

## 關於RTE外掛程式和相關功能 {#aboutplugins}

此功能可透過一系列外掛程式提供，每個外掛程式都具備：

* A `features` 屬性，

   * 用於啟用或停用該外掛程式的基本功能。
   * 使用標準化程式進行配置。

* 需要專門配置的更多屬性和選項（如果適用）。

RTE的基本功能會由 `features` 屬性。

下表列出目前的外掛程式，顯示：

* 具有API檔案連結的外掛程式ID。 當 [啟用外掛程式](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#activateplugin).
* 允許的值 `features` 屬性。
* 外掛程式所提供功能的說明。

| 外掛程式ID | 功能 | 說明 |
|--- |--- |--- |
| 編輯 | `cut`, `copy`, `paste-default`, `paste-plaintext`, `paste-wordhtml` | [剪下、複製和三種貼上模式](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#textstyles). |
| [芬德雷普萊斯](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.FindReplacePlugin) | `find`, `replace` | 查找和替換。 |
| [格式](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.FormatPlugin) | `bold`, `italic`, `underline` | [基本文字格式](configure-rich-text-editor-plug-ins.md#textstyles). |
| [影像](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.ImagePlugin) | `image` | 基本影像支援（從內容或內容尋找器拖曳）。 根據瀏覽器，支援對作者有不同的行為 |
| [鍵](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.KeyPlugin) | - | 若要定義此值，請參閱 [標籤大小](configure-rich-text-editor-plug-ins.md#tabsize). |
| [證明](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.JustifyPlugin) | `justifyleft`, `justifycenter`, `justifyright` | 段落對齊。 |
| [連結](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.LinkPlugin) | `modifylink`, `unlink`, `anchor` | [超連結和錨點](configure-rich-text-editor-plug-ins.md#linkstyles). |
| [清單](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.ListPlugin) | `ordered`, `unordered`, `indent`, `outdent` | 此外掛程式可同時控制 [縮排和清單](configure-rich-text-editor-plug-ins.md#indentmargin);包括巢狀清單。 |
| [miscools](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.MiscToolsPlugin) | `specialchars`, `sourceedit` | 其他工具可讓作者輸入 [特殊字元](configure-rich-text-editor-plug-ins.md#spchar) 或編輯HTML來源。 此外，您可以新增 [特殊字元範圍](configure-rich-text-editor-plug-ins.md#definerangechar) 如果您想定義自己的清單。 |
| Paraformat | `paraformat` | 預設段落格式為段落、標題1、標題2和標題3(`<p>`, `<h1>`, `<h2>`，和 `<h3>`)。 您可以 [添加更多段落格式](configure-rich-text-editor-plug-ins.md#paraformats) 或擴充清單。 |
| 拼字檢查 | `checktext` | [語言感知拼寫檢查程式](configure-rich-text-editor-plug-ins.md#adddict). |
| 樣式 | `styles` | 支援使用CSS類別的樣式。 [新增文字樣式](configure-rich-text-editor-plug-ins.md#textstyles) 如果您想要新增（或擴充）您自己的樣式範圍以搭配文字使用。 |
| 上標 | `subscript`, `superscript` | 基本格式的擴充功能，新增子指令碼和超指令碼。 |
| 表格 | `table`, `removetable`, `insertrow`, `removerow`, `insertcolumn`, `removecolumn`, `cellprops`, `mergecells`, `splitcell`, `selectrow`, `selectcolumns` | 請參閱 [配置表格樣式](configure-rich-text-editor-plug-ins.md#tablestyles) 為整個表格或個別儲存格新增您自己的樣式。 |
| 復原 | `undo`, `redo` | 歷史記錄大小 [還原和重做](configure-rich-text-editor-plug-ins.md#undohistory) 操作。 |

>[!NOTE]
>
>對話方塊模式中不支援全螢幕外掛程式。 使用 `dialogFullScreen` 設定，以設定全螢幕模式的工具列。

## 了解設定路徑和位置 {#understand-the-configuration-paths-and-locations}

此 [RTE編輯模式與介面](#editingmodes) 提供給作者的設定，會在您 [啟用RTE外掛程式](configure-rich-text-editor-plug-ins.md#activateplugin). 位置包括：

* 內嵌模式： `cq:editConfig/cq:inplaceEditing`.
* 全螢幕模式： `cq:editConfig/cq:inplaceEditing`.
* 對話框模式： `cq:dialog`.
* 全螢幕對話框模式： `cq:dialog`.

>[!NOTE]
>
>請勿將節點命名為 `cq:inplaceEditing` as `config`. 開啟 `cq:inplaceEditing` 節點，定義下列屬性：
>
>* **名稱**: `configPath`
>* **類型**: `String`
>* **值**:包含實際配置的節點的路徑
>
>請勿將RTE設定節點命名為 `config`. 否則，RTE設定只對管理員有效，對群組中的使用者無效 `content-author`.

配置在「對話框」編輯模式下應用的以下屬性：

* `useFixedInlineToolbar`:您可以讓RTE工具列固定，而非浮動。 使用sling:resourceType=在RTE節點上定義的此布林屬性 `cq/gui/components/authoring/dialog/richtext` to `True`. 此屬性設為時 `True`，則在 `foundation-contentloaded` 事件。 若要防止此情況，請設定屬性 `customStart` to `True` 並觸發 `rte-start` 開始RTE編輯的事件。 此屬性為 `true`,RTE不會在點按時開始，而這是預設行為。

* `customStart`:將RTE節點上定義的此布林屬性設定為 `True`，透過觸發事件來控制何時啟動RTE `rte-start`.

* `rte-start`:在 `contenteditable-div` ，開始編輯RTE時。 只有在 `customStart` 設為 `true`.

在觸控式對話方塊中使用RTE時，請設定屬性 `useFixedInlineToolbar` to `true` 以避免問題。

## 啟用外掛程式以啟用RTE功能 {#enable-rte-functionalities-by-activating-plug-ins}

可透過一系列外掛程式使用RTE功能，每個外掛程式都具有features屬性。 您可以配置features屬性，以啟用或停用每個外掛程式的各種功能。

如需RTE外掛程式的詳細設定，請參閱 [如何啟用和配置RTE外掛程式](configure-rich-text-editor-plug-ins.md).

<!-- TBD ENGREVIEW: To confirm if the sample works in CS or not?
**Sample**: Download [this sample configuration](/help/sites-administering/assets/rte-sample-all-features-enabled-10.zip) that illustrates how to configure RTE. In this package all the features are enabled. -->

此 [核心元件文字元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor) 可讓範本編輯器使用使用者介面作為內容原則來設定許多RTE外掛程式，而不需要進行技術設定。 內容原則可搭配RTE UI設定使用，如本檔案所述。 如需詳細資訊，請參閱 [建立頁面範本](/help/sites-cloud/authoring/features/templates.md) 和 [核心元件開發人員檔案](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html).

>如需參考，可在以下網址找到預設的文字元件（在標準安裝中提供）:
>
>* `/libs/wcm/foundation/components/text`
>* `/libs/foundation/components/text`
>
>若要建立您自己的文字元件，請複製上述元件，而非編輯這些元件。

## 配置RTE工具欄 {#dialogfullscreen}

[!DNL Experience Manager] 可讓您針對不同的編輯模式，以不同方式設定RTF編輯器的介面。 預設設定如下。 您可以根據需求改寫這些預設值。 您只可自訂要提供給作者的工具列功能。 您不需要指定所有工具列組態。

若要為 `dialogFullScreen`，請使用下列範例設定。

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

內嵌模式和全螢幕模式使用不同的使用者介面設定。 工具欄屬性指定工具欄的選項。

例如，如果選項本身是特徵(例如， `Bold`)，則會指定為 `PluginName#FeatureName` (例如， `links#modifylink`)。

如果選項是快顯視窗（包含外掛程式的某些功能），則會指定為 `#PluginName` (例如， `#format`)。

分隔符號(`|`)，可在一組選項之間指定 `-`.

內嵌或全螢幕模式下的快顯節點包含所使用快顯視窗的清單。 位於 `popovers` 節點以外掛程式命名（例如格式）。 其屬性為「項目」，包含外掛程式的功能清單（例如format#bold）。

## RTE使用者介面設定和內容原則 {#rtecontentpolicies}

管理員可以使用內容原則來控制RTE選項，例如，不必如上所述執行設定。 內容原則會定義元件在 [可編輯的範本](/help/sites-cloud/authoring/features/templates.md). 例如，如果使用RTE的文本元件與可編輯的模板一起使用，則內容策略可以定義粗體選項可用，並可以定義幾個段落格式選項。 內容原則可重複使用，可套用至多個範本。

RTE中的可用選項從用戶介面配置流向內容策略。

* 用戶介面配置設定定義了哪些選項可用於內容策略。
* 如果RTE的用戶介面配置已刪除或未啟用項目，則內容策略無法配置它。
* 作者只能存取使用者介面設定和內容原則所提供的功能。

例如，您可以看到 [文字核心元件檔案](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor).

## 自定義工具欄表徵圖和命令之間的映射 {#iconstoolbar}

您可以自訂RTE工具列上顯示的珊瑚圖示和可用命令之間的對應。 除了Coral圖示，您無法使用其他任何圖示。

1. 建立名為的節點 `icons` 在 `uiSettings/cui`.

1. 為其下的各個表徵圖建立節點。
1. 在每個個別圖示節點上，指定一個Coral圖示和一個命令來對應該圖示。

以下是映射命令的示例代碼段 `Bold` 珊瑚表徵圖已命名 `textItalic`.

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

* RTE功能僅支援 [!DNL Experience Manager] 元件對話方塊。 嚮導或Foundation-forms不支援RTE。

* [!DNL Experience Manager] 在混合裝置上無法運作。 <!-- TBD: Check. This is not mentioned in Known Issue /help/release-notes/known-issues.md-->

* 不要為RTE配置節點命名 `config`. 否則，RTE設定只對管理員有效，對群組中的使用者無效 `content-author`.

* RTE不支援內嵌內容至內嵌框架或iframe。

## 最佳實務與秘訣 {#best-practices-and-tips}

* 對於浮動對話方塊，請僅啟用不含快顯對話方塊的外掛程式。 不含快顯視窗的外掛程式大小較小，最適合浮動式對話。
* 使用較大的快顯視窗啟用外掛程式，例如 `Paste` 外掛程式，僅限以全螢幕對話方塊模式或全螢幕模式。 具有大型快顯視窗的外掛程式需要更多螢幕空間，才能提供良好的製作體驗。
* 如果您使用CoralUI3 RTE的自訂外掛程式，請使用 `rte.coralui3` 程式庫。

>[!MORELIKETHIS]
>
>* [設定RTE外掛程式](configure-rich-text-editor-plug-ins.md)
>* [使用RTF編輯器進行編寫](/help/sites-cloud/authoring/fundamentals/rich-text-editor.md)
>* [為可存取的網站配置RTE](rte-accessible-content.md)

