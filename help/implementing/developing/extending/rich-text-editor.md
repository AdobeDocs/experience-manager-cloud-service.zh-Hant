---
title: 配置富格文本編輯器以在 [!DNL Adobe Experience Manager] as a Cloud Service。
description: 配置富格文本編輯器以在 [!DNL Adobe Experience Manager] as a Cloud Service。
contentOwner: AG
exl-id: 1f0ff800-5e95-429a-97f2-221db0668170
source-git-commit: f5f2c7c4dfacc113994c380e8caa37508030ee92
workflow-type: tm+mt
source-wordcount: '1964'
ht-degree: 0%

---

# 配置RTF編輯器 {#configure-the-rich-text-editor}

富格文本編輯器(RTE)為作者提供了編輯文本內容的多種功能。 為WYSIWYG文本編輯體驗提供表徵圖、選擇框、工具欄和菜單。 管理員將RTE配置為啟用、禁用和擴展創作元件中可用的功能。 查看作者 [使用RTE進行創作](/help/sites-cloud/authoring/fundamentals/rich-text-editor.md) 的下界。

下面列出了配置RTE所需的RTE概念和步驟。

| 瞭解RTE概念 | 啟用所需功能 | 配置各個功能 |
|---|---|---|
| [瞭解介面](#understand-rte-ui) | [瞭解並設定配置位置](#understand-the-configuration-paths-and-locations) | [配置插件](#enable-rte-functionalities-by-activating-plug-ins) |
| [編輯模式的類型](#editingmodes) | [激活插件](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#activateplugin) | [設定功能屬性](#aboutplugins) |
| [關於插件](#aboutplugins) | [配置RTE工具欄](#dialogfullscreen) | [配置貼上模式](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#textstyles) |

## 瞭解作者可用的用戶介面 {#understand-rte-ui}

RTE介面提供 [響應設計](/help/sites-cloud/authoring/features/responsive-layout.md) 創作環境。 該介面設計用於觸摸和台式設備。

![富格文本編輯器工具欄](assets/rte-toolbar-full-screen-mode.png)

*圖：啟用了所有可用選項的富格文本編輯器工具欄。*

工具欄提供了WYSIWYG創作體驗的選項。 [!DNL Experience Manager] 管理員可以配置介面工具欄中的可用選項。 預設情況下，在 [!DNL Experience Manager]。 開發人員可以自定義 [!DNL Experience Manager] 的子菜單。

## 各種編輯模式 {#editingmodes}

作者可以在 [!DNL Experience Manager] 使用不同的元件模式。 用於創作和格式化內容的工具欄選項以及在不同編輯模式下啟用RTE的元件的用戶體驗會因RTE配置而異。

| 編輯模式 | 編輯區域 | 建議啟用的功能 |
|--- |--- |--- |
| 內嵌 | 就地編輯，以快速、次要地編輯；不開啟對話框的格式。 | 最小RTE功能。 |
| RTE全屏 | 涵蓋整頁。 | 所有必需的RTE功能。 |
| 對話方塊 | 的子菜單。 | 明智地啟用功能。 |
| 全屏對話框 | 與全屏模式相同；包含對話框的欄位和RTE。 | 所有必需的RTE功能。 |

>[!NOTE]
>
>源編輯功能在串聯編輯模式下不可用。 不能在全屏模式下拖動影像。 所有其它功能在所有模式下都工作。

### 內聯編輯 {#inline-editing}

要編輯頁面內的內容，請緩慢按兩下開啟內容。 給出了一個具有基本選項的緊湊工具欄。

![使用工具欄中的基本選項進行內聯編輯](assets/inline-editing-mode-basic-options.png)

*圖：使用工具欄中的基本選項進行內聯編輯。*

### 全屏編輯 {#full-screen-editing}

[!DNL Experience Manager] 可以在全屏視圖中開啟元件，以隱藏頁面內容並佔據可用螢幕。 考慮對內聯編輯的詳細版本進行全屏編輯，因為它提供的編輯選項最多。 可通過按一下 ![全屏開啟RTE的表徵圖](assets/rte_fullscreen.png)，在使用內嵌編輯模式時從壓縮工具欄中刪除。

在對話框的全屏模式以及詳細的RTE工具欄中，對話框中可用的選項和元件也可用。 它僅適用於包含RTE和其他元件的對話框。

![以全屏模式編輯時的詳細RTE工具欄](assets/rte-toolbar-full-screen-mode.png)

*圖：在全屏模式下編輯時的詳細RTE工具欄。*

### 對話框編輯 {#dialog-editing}

按兩下元件時，將開啟一個對話框以編輯內容。 該對話框在現有頁面頂部開啟。 在某些特定情況下，該對話框會作為彈出窗口開啟。 例如，當文本元件是多列頁面佈局中列的一部分，且對話框可用的區域較小時。

![對話框編輯模式](assets/dialog_editing_modetouchui.png)

*圖：對話框編輯模式。*

## 關於RTE插件和相關功能 {#aboutplugins}

此功能可通過一系列插件提供，每個插件都具有：

* A `features` 就是，

   * 用於激活或停用該插件的基本功能。
   * 使用標準化過程進行配置。

* 在適當情況下，需要專用配置的更多屬性和選項。

RTE的基本特徵將通過 `features` 特定於相應插件的節點上的屬性。

下表列出了當前插件，如下所示：

* 帶有指向API文檔的連結的插件ID。 ID在 [激活插件](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#activateplugin)。
* 允許的值 `features` 屬性。
* 插件提供的功能的說明。

| 插件ID | 特徵 | 說明 |
|--- |--- |--- |
| 編輯 | `cut`。 `copy`。 `paste-default`。 `paste-plaintext`。 `paste-wordhtml` | [剪切、複製和，三種貼上模式](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#textstyles)。 |
| [芬德萊](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.FindReplacePlugin) | `find`, `replace` | 查找和替換。 |
| [格式](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.FormatPlugin) | `bold`。 `italic`。 `underline` | [基本文本格式](configure-rich-text-editor-plug-ins.md#textstyles)。 |
| [影像](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.ImagePlugin) | `image` | 基本影像支援（從內容或Content Finder中拖動）。 根據瀏覽器的不同，支援對作者有不同的行為 |
| [鍵](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.KeyPlugin) | - | 要定義此值，請參閱 [頁籤大小](configure-rich-text-editor-plug-ins.md#tabsize)。 |
| [證明](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.JustifyPlugin) | `justifyleft`。 `justifycenter`。 `justifyright` | 段落對齊。 |
| [連結](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.LinkPlugin) | `modifylink`。 `unlink`。 `anchor` | [超連結和錨點](configure-rich-text-editor-plug-ins.md#linkstyles)。 |
| [清單](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.ListPlugin) | `ordered`。 `unordered`。 `indent`。 `outdent` | 此插件控制 [縮進和清單](configure-rich-text-editor-plug-ins.md#indentmargin);包括嵌套清單。 |
| [錯誤工具](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.MiscToolsPlugin) | `specialchars`。 `sourceedit` | 其他工具允許作者輸入 [特殊字元](configure-rich-text-editor-plug-ins.md#spchar) 或編輯HTML源。 另外，您可以 [特殊字元範圍](configure-rich-text-editor-plug-ins.md#definerangechar) 來修改標籤元素的屬性。 |
| 參數格式 | `paraformat` | 預設段落格式為段落、標題1、標題2和標題3(`<p>`。 `<h1>`。 `<h2>`, `<h3>`)。 你可以 [添加更多段落格式](configure-rich-text-editor-plug-ins.md#paraformats) 或擴展清單。 |
| 拼寫檢查 | `checktext` | [語言感知拼寫檢查器](configure-rich-text-editor-plug-ins.md#adddict)。 |
| 樣式 | `styles` | 支援使用CSS類的樣式。 [添加新文本樣式](configure-rich-text-editor-plug-ins.md#textstyles) 如果要添加（或擴展）您自己的樣式範圍，以便與文本一起使用。 |
| 上標 | `subscript`。 `superscript` | 基本格式的擴展，添加子指令碼和超級指令碼。 |
| 表 | `table`。 `removetable`。 `insertrow`。 `removerow`。 `insertcolumn`。 `removecolumn`。 `cellprops`。 `mergecells`。 `splitcell`。 `selectrow`。 `selectcolumns` | 請參閱 [配置表樣式](configure-rich-text-editor-plug-ins.md#tablestyles) 來修改標籤元素的屬性。 |
| 復原 | `undo`。 `redo` | 歷史記錄大小 [撤消和重做](configure-rich-text-editor-plug-ins.md#undohistory) 操作。 |

>[!NOTE]
>
>對話框模式下不支援全屏插件。 使用 `dialogFullScreen` 設定為配置工具欄以進行全屏模式。

## 瞭解配置路徑和位置 {#understand-the-configuration-paths-and-locations}

的 [RTE編輯模式及介面](#editingmodes) 您為作者提供的配置詳細資訊在您 [激活RTE插件](configure-rich-text-editor-plug-ins.md#activateplugin)。 這些位置是：

* 串聯模式： `cq:editConfig/cq:inplaceEditing`。
* 全屏模式： `cq:editConfig/cq:inplaceEditing`。
* 對話框模式： `cq:dialog`。
* 全屏對話模式： `cq:dialog`。

>[!NOTE]
>
>不將節點命名為 `cq:inplaceEditing` 如 `config`。 開 `cq:inplaceEditing` 節點，定義以下屬性：
>
>* **名稱**: `configPath`
>* **類型**: `String`
>* **值**:包含實際配置的節點的路徑
>
>不要將RTE配置節點命名為 `config`。 否則，RTE配置只對管理員生效，對組中的用戶無效 `content-author`。

配置在「對話框」編輯模式下應用的以下屬性：

* `useFixedInlineToolbar`:可以使RTE工具欄固定而不是浮動。 使用sling:resourceType=設定在RTE節點上定義的此布爾屬性 `cq/gui/components/authoring/dialog/richtext` 至 `True`。 當此屬性設定為 `True`，在 `foundation-contentloaded` 的子菜單。 要阻止此情況，請設定屬性 `customStart` 至 `True` 並觸發 `rte-start` 啟動RTE編輯的事件。 當此屬性為 `true`,RTE不會在按一下時啟動，這是預設行為。

* `customStart`:將RTE節點上定義的此布爾屬性設定為 `True`，通過觸發事件控制何時啟動RTE `rte-start`。

* `rte-start`:在 `contenteditable-div` 開始編輯RTE。 只有當 `customStart` 已設定為 `true`。

在啟用觸摸的對話框中使用RTE時，設定屬性 `useFixedInlineToolbar` 至 `true` 避免問題。

## 通過激活插件啟用RTE功能 {#enable-rte-functionalities-by-activating-plug-ins}

RTE功能可通過一系列插件提供，每個插件都具有features屬性。 可以配置features屬性以啟用或禁用每個插件的各種功能。

有關RTE插件的詳細配置，請參見 [如何激活和配置RTE插件](configure-rich-text-editor-plug-ins.md)。

<!-- TBD ENGREVIEW: To confirm if the sample works in CS or not?
**Sample**: Download [this sample configuration](/help/sites-administering/assets/rte-sample-all-features-enabled-10.zip) that illustrates how to configure RTE. In this package all the features are enabled. -->

的 [核心元件文本元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor) 允許模板編輯器使用用戶介面作為內容策略來配置許多RTE插件，從而消除了對技術配置的需要。 內容策略可以使用RTE UI配置，如本文檔所述。 有關詳細資訊，請參見 [建立頁面模板](/help/sites-cloud/authoring/features/templates.md) 和 [核心元件開發人員文檔](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html)。

>為便於參考，預設文本元件（作為標準安裝的一部分提供）可在以下位置找到：
>
>* `/libs/wcm/foundation/components/text`
>* `/libs/foundation/components/text`
>
>要建立您自己的文本元件，請複製上述元件，而不是編輯這些元件。

## 配置RTE工具欄 {#dialogfullscreen}

[!DNL Experience Manager] 允許您針對不同的編輯模式以不同方式配置富格文本編輯器的介面。 下面提供了預設設定。 您可以根據您的要求改寫這些預設值。 您只定制要提供給作者的工具欄功能。 無需指定所有工具欄配置。

配置工具欄 `dialogFullScreen`，使用以下示例配置。

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

串聯模式和全屏模式使用不同的用戶介面設定。 工具欄屬性指定工具欄的選項。

例如，如果選項本身是特徵(例如， `Bold`)，它指定為 `PluginName#FeatureName` (例如， `links#modifylink`)。

如果該選項是彈出窗口（包含插件的某些功能），則指定為 `#PluginName` (例如， `#format`)。

分隔符(`|`)在選項組之間 `-`。

串聯或全屏模式下的彈出節點包含正在使用的彈出窗口的清單。 位於 `popovers` 節點以插件（例如，format）命名。 它具有一個屬性「items」，其中包含插件的功能清單（例如，format#bold）。

## RTE用戶介面設定和內容策略 {#rtecontentpolicies}

管理員可以使用內容策略來控制RTE選項，例如，不要執行上述配置。 內容策略在用作元件的一部分時定義元件的設計屬性 [可編輯模板](/help/sites-cloud/authoring/features/templates.md)。 例如，如果使用RTE的文本元件與可編輯的模板一起使用，則內容策略可以定義粗體選項可用，以及幾個段落格式選項可用。 內容策略可重用，可跨多個模板應用。

RTE中的可用選項從用戶介面配置到內容策略的下游。

* 用戶介面配置設定定義了哪些選項可用於內容策略。
* 如果刪除了RTE的用戶介面配置或未啟用項目，則內容策略無法配置它。
* 作者只能訪問用戶介面配置和內容策略提供的功能。

例如，您可以看到 [文本核心元件文檔](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor)。

## 自定義工具欄表徵圖和命令之間的映射 {#iconstoolbar}

可以定制RTE工具欄上顯示的珊瑚表徵圖和可用命令之間的映射。 除珊瑚表徵圖外，不能使用任何其他表徵圖。

1. 建立名為 `icons` 在 `uiSettings/cui`。

1. 為下面的單個表徵圖建立節點。
1. 在每個單個表徵圖節點上，指定一個珊瑚表徵圖和一個要映射到該表徵圖的命令。

下面是映射命令的示例代碼段 `Bold` 到名為 `textItalic`。

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

[!DNL Experience Manager] RTE功能具有以下限制：

* RTE功能僅在 [!DNL Experience Manager] 元件對話框。 嚮導或基礎表單不支援RTE。

* [!DNL Experience Manager] 在混合設備上不工作。 <!-- TBD: Check. This is not mentioned in Known Issue /help/release-notes/known-issues.md-->

* 不命名RTE配置節點 `config`。 否則，RTE配置將僅對管理員生效，對組中的用戶無效 `content-author`。

* RTE不支援在內聯幀或iframe中嵌入內容。

## 最佳實踐和提示 {#best-practices-and-tips}

* 對於浮動對話框，只啟用沒有彈出對話框的插件。 沒有彈出窗口的插件尺寸較小，最適合浮動對話框。
* 使用較大的彈出窗口啟用插件，如 `Paste` 插件，僅在全屏對話框模式或全屏模式下。 具有大型彈出窗口的插件需要更多的螢幕空間來提供良好的創作體驗。
* 如果您正在為CoralUI3 RTE使用自定義插件，請使用 `rte.coralui3` 的下界。

>[!MORELIKETHIS]
>
>* [配置RTE插件](configure-rich-text-editor-plug-ins.md)
>* [使用RTF編輯器進行創作](/help/sites-cloud/authoring/fundamentals/rich-text-editor.md)
>* [為可訪問站點配置RTE](rte-accessible-content.md)

