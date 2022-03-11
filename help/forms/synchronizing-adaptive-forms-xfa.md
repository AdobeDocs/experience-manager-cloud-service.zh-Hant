---
title: 將自適應Forms與XFA表單模板同步
seo-title: Synchronizing Adaptive Forms with XFA Form Templates
description: 正在將自適應Forms與XFA/XDP檔案同步。
seo-description: Synchronizing Adaptive Forms with XFA/XDP files.
uuid: 92818132-1ae0-4576-84f2-ece485a34457
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: dac4539b-804d-4420-9170-68000ebb2638
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 0%

---


# 將自適應Forms與XFA表單模板同步{#synchronizing-adaptive-forms-with-xfa-form-templates}

## 簡介 {#introduction}

可以基於XFA表單模板建立自適應表單( `*.XDP` )。 通過此重複使用，您可以保留對現有XFA表單的投資。 有關如何使用XFA表單模板建立自適應表單的資訊， [基於模板建立自適應表單](creating-adaptive-form.md)。

可以在「自適應表單」中重用XDP檔案中的欄位。 這些欄位稱為綁定欄位。 綁定欄位的屬性（如指令碼、標籤和顯示格式）從XDP檔案複製。 也可以選擇覆蓋其中某些屬性的值。

[!DNL AEM Forms] 提供了一種方法，幫助您使Adaptive Forms的欄位與隨後對XDP檔案中相應欄位所做的任何更改保持同步。 本文介紹如何啟用此同步。

![可以將欄位從XFA窗體拖動到自適應窗體](assets/drag-drop-xfa.gif.gif)

在 [!DNL AEM Forms] 創作環境中，可將欄位從XFA表單（左）拖到自適應表單（右）

## 必備條件 {#prerequisites}

要使用本文中的資訊，建議您熟悉以下方面：

* [建立自適應窗體](creating-adaptive-form.md)

* XFA(XMLForms體系結構)

要使用本文中的示例提供的資產，請下載下一節中說明的示例包， [示例包](synchronizing-adaptive-forms-xfa.md#p-sample-package-p)。

## 示例包 {#sample-package}

文章使用一個示例演示如何將自適應表單與更新的XFA表單模板同步。 示例中使用的資產可在包中使用，可從 [下載](synchronizing-adaptive-forms-xfa.md#p-downloads-p) 的下界。

上載包後，您可以在 [!DNL AEM Forms] UI。

使用包管理器安裝包： `https://<server>:<port>/crx/packmgr/index.jsp`

包包含以下資產：

1. `sample-form.xdp`:用作示例的XFA表單模板

1. `sample-xfa-af`:基於sample-form.xdp檔案的自適應表單。 但是，此自適應表單不包括任何欄位。 在下一步中，我們將向此自適應表單添加內容。

### 將內容添加到自適應表單 {#add-content-to-adaptive-form-br}

1. 導航到https://&lt;server>:&lt;port>/aem/forms.html。 如有詢問，請輸入您的憑據。
1. 在作者模式下開啟sample-af-xfa進行編輯。
1. 從提要欄中的「內容」瀏覽器中，選擇「資料模型對象」頁籤。 將NumericField1和TextField1拖到自適應窗體上。
1. 將NumericField1的標題從 **數字欄位** 至 **AF數字欄位。**

>[!NOTE]
>
>在前面的步驟中，我們覆蓋了XDP檔案中欄位的屬性。 因此，如果稍後修改XDP檔案中的相應屬性，則不會同步此屬性。

## 檢測XDP檔案中的更改 {#detecting-changes-in-xdp-file}

只要XDP檔案或片段中有任何更改， [!DNL AEM Forms] UI標籤所有基於XDP檔案或片段的自適應Forms。

更新XDP檔案後，需要在 [!DNL AEM Forms] 要標籤的更改的UI。

例如，讓我們更新 `sample-form.xdp` 檔案：

1. 導航到 `https://<server>:<port>/projects.html.` 如果出現提示，請輸入您的憑據。
1. 按一下左側的Forms頁籤。
1. 下載 `sample-form.xdp` 檔案。 XDP檔案作為 `.zip` 檔案，可使用任何檔案解壓實用程式提取。

1. 開啟 `sample-form.xdp` 檔案，並更改欄位TextField1的標題 **文本欄位** 至 **我的文本欄位**。

1. 上載 `sample-form.xdp` 檔案返回 [!DNL AEM Forms] UI。

如果XDP檔案被更新，則在根據XDP檔案編輯自適應Forms時，在編輯器中會看到一個表徵圖。 此表徵圖表示自適應表單與XDP檔案不同步。 在以下影像中，請參閱提要欄中旁邊的表徵圖。

![用於顯示自適應表單與XDP檔案不同步的表徵圖](assets/sync-af-xfa.png)

## 將自適應Forms與最新的XDP檔案同步 {#synchronizing-adaptive-forms-with-the-latest-xdp-file}

在下次開啟與XDP檔案不同步的自適應表單進行創作時，將顯示以下消息： **已更新自適應表單的架構/表單模板。 `Click Here` 以使其與新版本重新建立基礎。**

按一下消息將Adaptive Form中的欄位與XDP檔案中的相應欄位同步。

對於本文中使用的示例，請開啟 `sample-xfa-af` 在創作模式下。 該消息將顯示在自適應表單的底部。

![提示您將Adaptive Form與XDP檔案同步的消息](assets/sync-af-xfa-1.png)

### 更新屬性 {#updating-the-properties}

從XDP檔案複製到自適應表單的所有屬性都將被更新，但作者在自適應表單（從「元件」對話框）中明確覆蓋的屬性除外。 伺服器日誌中提供已更新的屬性清單。

要更新示例「自適應表單」中的屬性，請按一下連結(標有 `"Click Here"`)。 TextField1的標題更改自 **文本欄位** 至 **我的文本欄位**。

![更新屬性](assets/update-property.png)

>[!NOTE]
>
>未更改標籤AF數字欄位，因為您已從元件屬性對話框中覆蓋此屬性，如中所述 [將內容添加到自適應Forms](synchronizing-adaptive-forms-xfa.md#p-add-content-to-adaptive-form-br-p)。

### 將新欄位從XDP檔案添加到自適應表單   {#adding-new-fields-from-xdp-file-to-adaptive-form-nbsp}

稍後添加到原始XDP檔案的任何欄位都會顯示在「表單層次」頁籤中，您可以將這些新欄位拖到「自適應表單」中。

無需按一下錯誤消息中的連結即可更新「表單層次結構」頁籤中的欄位。

### 已刪除XDP檔案中的欄位 {#deleted-fields-in-xdp-file}

如果先前複製到自適應表單的欄位從XDP檔案中刪除，則在創作模式中顯示一條錯誤消息，指出該欄位在XDP檔案中不存在。 在這種情況下，從「自適應表單」中手動刪除該欄位或清除 `bindRef` 屬性。

以下步驟說明了本文示例中資產的使用流程：

1. 更新 `sample-form.xdp` 檔案並刪除NumericField1。
1. 上載 `sample-form.xdp` 檔案 [!DNL AEM Forms] UI
1. 開啟 `sample-xfa-af` 用於創作的自適應窗體。 將顯示以下錯誤消息：已更新自適應表單的架構/表單模板。 `Click Here` 以使其與新版本重新建立基礎。

1. 按一下連結(標有「 `Click Here`」)。 將顯示一條錯誤消息，指出該欄位在XDP檔案中已不存在。

![刪除XDP檔案中的元素時出現錯誤](assets/no-element-xdp.png)

已刪除的欄位還用表徵圖標籤，以指示該欄位中出現錯誤。

![欄位中的錯誤表徵圖](assets/error-field.png)

>[!NOTE]
>
>自適應表單中綁定不正確（無效）的欄位 `bindRef` )中的值也被視為已刪除的欄位。 如果作者沒有修復這些錯誤並發佈自適應表單，則該欄位將被視為正常的未綁定自適應表單欄位，並包含在輸出XML檔案的未綁定部分中。

## 下載內容 {#downloads}

本文示例的內容包

[取得檔案](assets/sample-xfa-af-sync-1.0.zip)
