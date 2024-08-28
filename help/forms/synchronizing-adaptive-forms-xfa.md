---
title: 如何將最適化Forms與XFA表單範本同步？
description: 同步最適化Forms與XFA/XDP檔案。
uuid: 92818132-1ae0-4576-84f2-ece485a34457
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: dac4539b-804d-4420-9170-68000ebb2638
feature: Adaptive Forms
role: User
hide: true
hidefromtoc: true
source-git-commit: 937bd4653e454beea3111cfc7ef7b4bbc1ace193
workflow-type: tm+mt
source-wordcount: '1146'
ht-degree: 0%

---


# 同步最適化Forms與XFA表單範本{#synchronizing-adaptive-forms-with-xfa-form-templates}

## 簡介 {#introduction}

您可以根據XFA表單範本（ `*.XDP`檔案）建立最適化表單。 此重複使用可讓您保留在現有XFA表單中的投資。 有關如何使用XFA表單範本建立最適化表單的資訊，請[根據範本建立最適化表單](creating-adaptive-form.md)。

您可以在最適化表單中重複使用XDP檔案的欄位。 這些欄位稱為繫結欄位。 繫結欄位的屬性（例如指令碼、標籤和顯示格式）會從XDP檔案複製。 您也可以選擇覆寫其中某些屬性的值。

[!DNL AEM Forms]提供一種方法來協助您保持最適化Forms的欄位與稍後對XDP檔案中對應欄位所做的任何變更同步。 本文會說明如何啟用此同步化。

![您可以從XFA表單將欄位拖曳到最適化表單](assets/drag-drop-xfa.gif.gif)

在[!DNL AEM Forms]編寫環境中，您可以從XFA表單（左）將欄位拖曳到調適型表單（右）

## 先決條件 {#prerequisites}

若要使用本文中的資訊，建議您熟悉下列領域：

* [建立最適化表單](creating-adaptive-form.md)

* XFA (XML Forms架構)

若要使用文章範例中提供的資產，請下載範例套件，如下一節[範例套件](synchronizing-adaptive-forms-xfa.md#p-sample-package-p)中所述。

## 範例套件 {#sample-package}

文章以範例示範如何將最適化表單與更新的XFA表單範本同步。 範例中使用的資產可在套件中使用，該套件可從本文的[下載](synchronizing-adaptive-forms-xfa.md#p-downloads-p)區段下載。

上傳封裝後，您可以在[!DNL AEM Forms] UI中檢視這些資產。

使用封裝管理員安裝封裝： `https://<server>:<port>/crx/packmgr/index.jsp`

此套件包含下列資產：

1. `sample-form.xdp`：作為範例使用的XFA表單範本

1. `sample-xfa-af`：以sample-form.xdp檔案為基礎的最適化表單。 不過，此最適化表單不包含任何欄位。 在下一步中，我們將新增內容至此最適化表單。

### 將內容新增至最適化表單 {#add-content-to-adaptive-form-br}

1. 導覽至https://&lt;server>：&lt;port>/aem/forms.html。 如有要求，請輸入您的認證。
1. 開啟sample-af-xfa以在作者模式中編輯。
1. 從側邊欄中的內容瀏覽器，選擇資料模型物件索引標籤。 將NumericField1和TextField1拖曳至最適化表單。
1. 將NumericField1的標題從&#x200B;**數值欄位**&#x200B;變更為&#x200B;**AF數值欄位。**

>[!NOTE]
>
>在上述步驟中，我們覆寫XDP檔案中欄位的屬性。 因此，如果稍後修改XDP檔案中的對應屬性，此屬性將不會同步。

## 偵測XDP檔案中的變更 {#detecting-changes-in-xdp-file}

每當XDP檔案或片段發生任何變更時，[!DNL AEM Forms] UI都會標示所有以XDP檔案或片段為基礎的Adaptive Forms。

更新XDP檔案後，您需要在[!DNL AEM Forms] UI中再次上傳該檔案，才能標籤變更。

例如，讓我們使用下列步驟更新`sample-form.xdp`檔案：

1. 瀏覽至`https://<server>:<port>/projects.html.`如果系統提示，請輸入您的認證。
1. 按一下左側的Forms標籤。
1. 在本機電腦上下載`sample-form.xdp`檔案。 XDP檔案下載為`.zip`檔案，可使用任何檔案解壓縮公用程式解壓縮。

1. 開啟`sample-form.xdp`檔案，並將TextField1欄位的標題從&#x200B;**文字欄位**&#x200B;變更為&#x200B;**我的文字欄位**。

1. 將`sample-form.xdp`檔案上傳回[!DNL AEM Forms] UI。

如果XDP檔案已更新，當您根據XDP檔案編輯最適化Forms時，會在編輯器中看到圖示。 此圖示表示最適化表單與XDP檔案不同步。 在下圖中，請參閱側邊欄中的圖示。

![圖示以顯示最適化表單與XDP檔案不同步](assets/sync-af-xfa.png)

## 將最適化Forms與最新XDP檔案同步 {#synchronizing-adaptive-forms-with-the-latest-xdp-file}

下次開啟與XDP檔案不同步的回應式表單進行製作時，會顯示下列訊息：已更新回應式表單的&#x200B;**結構描述/表單範本。 `Click Here`以使用新版本將其重新作為基礎。**

按一下訊息會將最適化表單中的欄位與XDP檔案中的對應欄位同步。

對於本文中使用的範例，在撰寫模式下開啟`sample-xfa-af`。 訊息會顯示在最適化表單的底部。

![訊息提示您同步處理最適化表單與XDP檔案](assets/sync-af-xfa-1.png)

### 更新屬性 {#updating-the-properties}

從XDP檔案複製到調適型表單的所有屬性都會更新，惟作者在調適型表單（從元件對話方塊）中明確覆寫的內容除外。 伺服器記錄檔中提供已更新的屬性清單。

若要更新最適化表單範例中的屬性，請按一下訊息中的連結（標示為`"Click Here"`）。 TextField1的標題從&#x200B;**文字欄位**&#x200B;變更為&#x200B;**我的文字欄位**。

![update-property](assets/update-property.png)

>[!NOTE]
>
>標籤AF數值欄位未變更，因為您已從元件屬性對話方塊覆寫此屬性，如[將內容新增至最適化Forms](synchronizing-adaptive-forms-xfa.md#p-add-content-to-adaptive-form-br-p)中所述。

### 將XDP檔案的新欄位新增至最適化表單   {#adding-new-fields-from-xdp-file-to-adaptive-form-nbsp}

任何稍後新增至原始XDP檔案的欄位都會顯示在「表單階層」標籤中，而且您可以將這些新欄位拖曳至調適型表單。

您不需要按一下錯誤訊息中的連結，即可更新表單階層標籤中的欄位。

### XDP檔案中的已刪除欄位 {#deleted-fields-in-xdp-file}

如果先前複製到調適型表單的欄位從XDP檔案中刪除，則會在編寫模式下顯示一則錯誤消息，指出該欄位不存在於XDP檔案中。 在這種情況下，請從最適化表單中手動刪除欄位或清除元件對話方塊中的`bindRef`屬性。

以下步驟說明本文使用範例中資產的此使用流程：

1. 更新`sample-form.xdp`檔案並刪除NumericField1。
1. 在[!DNL AEM Forms] UI中上傳`sample-form.xdp`檔案
1. 開啟`sample-xfa-af`最適化表單以進行編寫。 會顯示下列錯誤訊息：已更新最適化表單的架構/表單範本。 `Click Here`以使用新版本重新基準設定。

1. 按一下訊息中的連結（標示為「`Click Here`」）。 系統會顯示錯誤訊息，指出欄位在XDP檔案中不再存在。

![當您刪除XDP檔案中的專案時發現錯誤](assets/no-element-xdp.png)

已刪除的欄位也會標示圖示，以指出欄位中的錯誤。

欄位](assets/error-field.png)中的![錯誤圖示

>[!NOTE]
>
>適用性表單中有不正確繫結（編輯對話方塊中無效的`bindRef`值）的欄位也被視為已刪除欄位。 如果作者未修正這些錯誤並發佈調適型表單，則該欄位會被視為一般未繫結的調適型表單欄位，並包含在輸出XML檔案的未繫結區段中。

## 下載 {#downloads}

本文範例的Content-package

[取得檔案](assets/sample-xfa-af-sync-1.0.zip)
