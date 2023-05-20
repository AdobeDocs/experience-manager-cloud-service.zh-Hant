---
title: 配置RTE以建立可訪問的網頁和站點。
description: 瞭解如何配置富格文本編輯器以在 [!DNL Adobe Experience Manager]。
contentOwner: AG
exl-id: 54050fc9-0348-4033-8e2b-b3897588cb62
source-git-commit: e9c1ec6807f86ab00f89ef292a89a0c8efdf802b
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 1%

---

# 設定 RTE 以建立可存取的網站 {#configure-rte-accessible-sites}

[!DNL Adobe Experience Manager] 支援標準輔助功能，如影像的替代文本，以及建立內容時可訪問的額外功能。 內容作者將這些功能與使用RTE的元件一起使用。 這些功能包括添加Alt-Text、通過標題和段落元素的結構資訊等。

要瞭解RTE的典型配置，請參見 [配置RTE](rich-text-editor.md) 和 [為特定功能配置RTE插件](configure-rich-text-editor-plug-ins.md)。

使用RTE插件配置配置和自定義與輔助功能相關的功能。 例如，使用 `paraformat` 添加額外的塊級語義元素，包括擴展支援的標題級數超出基本 `H1`。 `H2` 和 `H3` 預設提供。 富格文本編輯可以使用創作用戶介面中的許多元件。 常用的元件有文本、影像、下載等。

RTE功能可在許多元件中使用。 主要元件是 `Text` 元件。

對於 `Text` 元件 [!DNL Experience Manager]，以下螢幕快照顯示啟用了一系列插件的富格文本編輯器，包括 `paraformat`:

![RTE全屏模式下的文本元件](assets/rte-toolbar-full-screen-mode.png)

## 配置插件功能 {#configuring-the-plugin-features}

有關配置RTE的說明，請參見 [配置RTF編輯器](rich-text-editor.md) 的子菜單。 文章包括：

* [插件及其功能](rich-text-editor.md#aboutplugins)
* [配置位置](rich-text-editor.md#understand-the-configuration-paths-and-locations)
* [激活插件並配置features屬性](rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)
* [配置RTE的其他功能](rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)

要激活插件的幾項或所有功能，請在適當的 `rtePlugins` CRXDE Lite支行。

![CRXDE Lite顯示示例rtePlugin](assets/example-rteplugin-crxde-lite.png)

### 指定RTE選擇欄位中可用的段落格式的示例 {#example-specifying-paragraph-formats-available-in-rte-selection-field}

新的語義塊格式可供選擇。

1. 根據RTE，確定並導航到 [配置位置](rich-text-editor.md#understand-the-configuration-paths-and-locations)。
1. [啟用段落選擇欄位](rich-text-editor.md) 按 [激活插件](rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)。
1. [指定段落選擇欄位中要使用的格式](rich-text-editor.md)。
1. 然後，從RTE的選擇欄位中，內容作者可以使用段落格式。

在RTE中通過段落格式選項提供結構元素的情況下， [!DNL Experience Manager] 為可訪問內容的開發提供了良好的基礎。 內容作者不能使用RTE格式化字型大小、顏色或其他相關屬性，從而阻止建立內嵌格式。 相反，作者可以選擇適當的結構元素，如標題，並使用從「樣式」選項中選擇的全局樣式，以確保使用自己的樣式表和正確結構化內容瀏覽的用戶具有乾淨的標籤和更好的選項。

## 源編輯功能的使用 {#use-of-the-source-edit-feature}

在某些情況下，內容作者將發現有必要檢查和調整使用RTE建立的HTML原始碼。 例如，在RTE中建立的某一內容可能需要更多標籤，以確保符合WCAG 2.0。這可以通過 [源編輯](rich-text-editor.md#aboutplugins) 選項。 可以指定 [`sourceedit` 功能 `misctools` 插件](rich-text-editor.md#aboutplugins)。

>[!CAUTION]
>
>使用 `sourceedit` 特寫。 任何鍵入錯誤和不受支援的功能都可能導致問題。

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
>* [WCAG標準的快速指南](/help/compliance/accessibility/quick-guide-wcag.md)
>* [如何在Experience Manager中建立可訪問內容](/help/sites-cloud/authoring/fundamentals/accessible-content.md)

