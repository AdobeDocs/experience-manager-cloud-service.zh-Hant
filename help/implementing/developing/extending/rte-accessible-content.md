---
title: 配置RTE以建立可訪問的網頁和站點。
description: 瞭解如何在 [!DNL Adobe Experience Manager]中設定Rich Text Editor以建立可存取的網站。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 96c59974a868779df6979818bea0d942060cf5bc
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 1%

---


# 設定 RTE 以建立可存取的網站 {#configure-rte-accessible-sites}

[!DNL Adobe Experience Manager] 支援標準協助工具功能，例如影像的替代文字，以及建立內容時可存取的額外功能。內容作者將這些功能與使用豐富型文字編輯器(RTE)的元件搭配使用。 這些功能包括新增替代文字、透過標題和段落元素的結構資訊等。

要瞭解RTE的典型配置，請參見[ configure RTE](rich-text-editor.md)和[ configure RTE plug-ins for specific functionality](configure-rich-text-editor-plug-ins.md)。

使用RTE插件配置來配置和自定義與輔助功能相關的功能。 例如，使用`paraformat`新增額外的區塊層級語義元素，包括將支援的標題層級數擴充至預設提供的基本`H1`、`H2`和`H3`。 使用編寫使用者介面中的許多元件，即可進行豐富式文字編輯。 常用的元件有文字、影像、下載等。

RTE功能可在許多元件中使用。 主要元件是`Text`元件。

對於[!DNL Experience Manager]中的`Text`元件，以下螢幕擷取會顯示已啟用多種增效模組（包括`paraformat`）的Rich Text編輯器：

![全屏模式下的RTE Text元件](assets/rte-toolbar-full-screen-mode.png)

## 配置插件功能{#configuring-the-plugin-features}

有關配置RTE的說明，請參見[configure the Rich Text Editor](rich-text-editor.md)頁。 文章內容包括：

* [增效模組及其功能](rich-text-editor.md#aboutplugins)
* [配置位置](rich-text-editor.md#understand-the-configuration-paths-and-locations)
* [啟動外掛程式並設定features屬性](rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)
* [配置RTE的其他功能](rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)

若要啟用外掛程式的幾項或所有功能，請在CRXDE Lite的適當`rtePlugins`子分支中設定外掛程式。

![CRXDE Lite，顯示範例rtePlugin](assets/example-rteplugin-crxde-lite.png)

### 指定RTE選擇欄位{#example-specifying-paragraph-formats-available-in-rte-selection-field}中可用段落格式的示例

新的語義塊格式可供選擇。

1. 根據RTE，確定並導航至[配置位置](rich-text-editor.md#understand-the-configuration-paths-and-locations)。
1. [啟用外掛程](rich-text-editor.md) 式以 [啟用段落選擇欄位](rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)。
1. [在段落選擇欄位中指定您要使用的格式](rich-text-editor.md)。
1. 然後，內容作者可從RTE中的選擇欄位使用段落格式。

在RTE中通過段落格式選項提供結構元素後，[!DNL Experience Manager]為開發可訪問內容提供了良好的基礎。 內容作者無法使用RTE格式化字型大小或顏色或其他相關屬性，因而無法建立內嵌格式。 作者可以選擇適當的結構元素，例如標題，並使用從「樣式」選項中選擇的全域樣式，以確保使用自己樣式表和正確結構化內容的瀏覽者能獲得清晰的標籤和更佳的選項。

## 使用原始碼編輯功能{#use-of-the-source-edit-feature}

在某些情況下，內容作者會發現有必要檢查並調整使用RTE建立的HTML原始碼。 例如，在RTE中建立的一部分內容可能需要更多標注以確保符合WCAG 2.0。這可以通過RTE的[源edit](rich-text-editor.md#aboutplugins)選項來完成。 您可以在`misctools`外掛程式](rich-text-editor.md#aboutplugins)上指定[`sourceedit`功能。

>[!CAUTION]
>
>小心使用`sourceedit`功能。 任何輸入錯誤和不支援的功能都可能導致問題。

<!--
TBD ENGREVIEW: Is this only applicable to Classic UI? 

## Adding Support for further HTML Elements and Attributes {#adding-support-for-additional-html-elements-and-attributes}

To further extend the accessibility features of [!DNL Experience Manager], it is possible to extend the existing components based on the RTE (such as the `Text` and `Table` components) with extra elements and attributes.

The following procedure illustrates how to extend the `Table` component with a `Caption` element that provides information about a data table to assistive technology users:

### Example: Add a caption to a table properties dialog {#example-adding-the-caption-to-the-table-properties-dialog}

In the constructor of the `TablePropertiesDialog`, add an extra text input field that is used for editing the caption. Set the `itemId` to `caption` (the DOM attribute’s name) to automatically handle its content.

In a `Table`, set the attribute to the DOM element or or remove it from the DOM element. The dialog in the `config` object passed the value. Set or remove the DOM attributes using the corresponding `CQ.form.rte.Common` methods (`com` is a shortcut for `CQ.form.rte.Common`). Using `CQ.form.rte.Common` methods avoids common pitfalls with browser implementations.

>[!NOTE]
>
>This procedure is only suitable for the classic UI.

### Step-by-step instructions {#step-by-step-instructions}

1. Start CRXDE Lite. For example: [http://localhost:4502/crx/de/](http://localhost:4502/crx/de/)

1. Copy `/libs/cq/ui/widgets/source/widgets/form/rte/commands/Table.js` to `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`. Create intermediate folders if those do not exist.

1. Copy `/libs/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js` to `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`.

1. Open `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js` file to edit.

1. In the `constructor` method, before the mention of `var dialogRef = this;`, add the following code:

   ```javascript
   editItems.push({
       "itemId": "caption",
       "name": "caption",
       "xtype": "textfield",
       "fieldLabel": CQ.I18n.getMessage("Caption"),
       "value": (this.table && this.table.caption ? this.table.caption.textContent : "")
   });
   ```

1. Open `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js` file.

1. Add the following code at the end of the `transferConfigToTable` method:

   ```javascript
   /**
    * Adds Caption Element
   */
   var captionElement;
   if (dom.firstChild && dom.firstChild.tagName.toLowerCase() == "caption")
   {
      captionElement = dom.firstChild;
   }
   if (config.caption)
   {
       var captionTextNode = document.createTextNode(config.caption)
       if (captionElement)
       {
          dom.replaceNode(captionElement.firstChild,captionTextNode);
       } else
       {
           captionElement = document.createElement("caption");
           captionElement.appendChild(captionTextNode);
           if (dom.childNodes.length>0)
           {
              dom.insertBefore(captionElement, dom.firstChild);
           } else
           {
              dom.appendChild(captionElement);
           }
       }
   } else if (captionElement)
   {
     dom.removeChild(captionElement);
   }
   ```

1. To save your changes, click **[!UICONTROL Save All]**.

## Best practices and limitations {#best-practices-limitations-tips}

* A plain text field is not the only type of input allowed for the value of the caption element. You can use any ExtJS widget, that provides the caption’s value through its `getValue()` method.
* To add editing capabilities for more elements and attributes, ensure that:

  * The `itemId` property for each corresponding field is set to the name of the appropriate DOM attribute (`TablePropertiesDialog`).
  * The attribute is set and/or removed on the DOM element explicitly (`Table`).
-->

>[!MORELIKETHIS]
>
>* [WCAG標準的快速指南](/help/onboarding/accessibility/quick-guide-wcag.md)
>* [如何在Experience Manager中建立可存取的內容](/help/sites-cloud/authoring/fundamentals/accessible-content.md)

