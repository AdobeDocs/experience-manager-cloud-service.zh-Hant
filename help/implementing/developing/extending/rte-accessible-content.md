---
title: 設定RTE以建立無障礙的網頁和網站。
description: 瞭解如何設定RTF編輯器以在 [!DNL Adobe Experience Manager]中建立無障礙網站。
contentOwner: AG
exl-id: 54050fc9-0348-4033-8e2b-b3897588cb62
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 1%

---

# 設定 RTE 以建立可存取的網站 {#configure-rte-accessible-sites}

[!DNL Adobe Experience Manager]支援標準的協助工具功能，例如影像的替代文字，以及建立內容時可存取的額外功能。 內容作者將這些功能與使用RTF編輯器(RTE)的元件搭配使用。 功能包括新增替代文字、透過標題和段落元素的結構資訊等等。

若要瞭解RTE的典型設定，請參閱[設定RTE](rich-text-editor.md)以及[為特定功能設定RTE外掛程式](configure-rich-text-editor-plug-ins.md)。

使用RTE外掛程式設定來設定和自訂協助工具的相關功能。 例如，使用`paraformat`新增額外的區塊層級語意元素，包括擴充支援的標題層級數目，使其超過預設提供的基本`H1`、`H2`和`H3`。 RTF編輯可使用製作使用者介面的許多元件。 常用的元件有文字、影像、下載等。

RTE功能可用於許多元件中。 主要元件是`Text`元件。

針對`Text`中的[!DNL Experience Manager]元件，下列熒幕擷圖顯示已啟用一系列外掛程式（包括`paraformat`）的RTF編輯器：

全熒幕模式中的![RTE文字元件](assets/rte-toolbar-full-screen-mode.png)

## 設定外掛程式功能 {#configuring-the-plugin-features}

如需設定RTE的說明，請參閱[設定RTF編輯器](rich-text-editor.md)頁面。 文章涵蓋：

* [外掛程式及其功能](rich-text-editor.md#aboutplugins)
* [設定位置](rich-text-editor.md#understand-the-configuration-paths-and-locations)
* [啟動外掛程式並設定功能屬性](rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)
* [設定RTE的其他功能](rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)

若要啟用外掛程式的部分或所有功能，請在CRXDE Lite中適當的`rtePlugins`子分支中設定外掛程式。

![CRXDE Lite顯示範例rtePlugin](assets/example-rteplugin-crxde-lite.png)

### 指定RTE選取欄位中可用段落格式的範例 {#example-specifying-paragraph-formats-available-in-rte-selection-field}

新的語意區塊格式可供選取。

1. 根據您的RTE，決定並導覽至[設定位置](rich-text-editor.md#understand-the-configuration-paths-and-locations)。
1. [啟用外掛程式](rich-text-editor.md)以啟用段落選取欄位[。](rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)
1. [指定您要在段落選取欄位中使用的格式](rich-text-editor.md)。
1. 然後，內容作者可以從RTE的選擇欄位中使用段落格式。

透過RTE中透過段落格式選項提供的結構元素，[!DNL Experience Manager]為開發無障礙內容提供了良好的基礎。 內容作者無法使用RTE來格式化字型大小、顏色或其他相關屬性，因而無法建立內嵌格式。 相反地，作者可以選取適當的結構元素（例如標題），並使用從「樣式」選項中選取的全域樣式，以確保對於使用自己的樣式表瀏覽且結構內容正確的使用者，會有乾淨的標示和更大的選項。

## 使用Source編輯功能 {#use-of-the-source-edit-feature}

在某些情況下，內容作者會發現必須檢查並調整使用RTE建立的HTML原始碼。 例如，在RTE內建立的內容片段可能需要更多標籤，以確保符合WCAG 2.0。您可以使用RTE的[來源編輯](rich-text-editor.md#aboutplugins)選項來完成此操作。 您可以在[`sourceedit`外掛程式`misctools`上指定](rich-text-editor.md#aboutplugins)功能。

>[!CAUTION]
>
>請謹慎使用`sourceedit`功能。 任何輸入錯誤和不支援的功能都可能會造成問題。

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
>* [WCAG標準快速指南](/help/compliance/accessibility/quick-guide-wcag.md)
>* [如何在Experience Manager中建立可存取的內容](/help/sites-cloud/authoring/page-editor/accessible-content.md)
