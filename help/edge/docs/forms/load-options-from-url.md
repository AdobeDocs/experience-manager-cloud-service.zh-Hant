---
title: 從URL載入下拉式清單選項
description: 下拉式清單選項會納入不同的試算表中，然後透過提供的URL匯入主要試算表中。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: eadfc3d448bd2fadce08864ab65da273103a6212
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 2%

---


# 從URL載入下拉式清單選項

在Edge Delivery Services表單中，使用者可以選擇從預先定義的選項集中選取值。 表單作者使用 `select` 元素，提供選項清單。
例如， `enquiry` form提供下拉式功能表，供使用者選取國家/地區，並提供一系列預先定義的國家/地區以供選擇。 您可以看到此清單包含以逗號分隔的一長串國家/地區清單。

![下拉式清單選項](/help/forms/assets/drop-down-options.png)

直接將下拉式功能表的選項清單新增至包含表單定義的工作表時，管理這些選項清單可能會很麻煩。 建立單獨的工作表來儲存這些下拉式清單選項可以簡化和簡化程式。 此工作表可作為所有下拉式功能表選項的集中式存放庫，以結構化格式排列。 每個選項都列在其自己的列中，有助於更輕鬆地進行管理和更新。

讓我們透過URL從其他試算表載入選項清單，探索如何改善表單撰寫流程。

閱讀完本文章後，您將學會：

* [在個別的試算表中定義選項](#define-options)
* [新增URL以載入下拉式清單選項](#add-url)

## 在個別的頁面中定義選項 {#define-options}

建立具有兩欄的工作表：`Option` 和 `Value`，以定義選項：

1. 前往Microsoft®SharePoint或Google Drive資料夾中的AEM專案資料夾。
2. 新增名為的工作表 `shared-country` 在Microsoft® SharePoint Site或Google Drive資料夾中新增下列專案：

   * **選項**：代表下拉式選單中選項的顯示值。
   * **值**：代表使用者選取選項時提交的值。

   >[!NOTE]
   >
   > 如果下拉式選項的值與選項相同，試算表僅可包含 **選項** 欄。

   新增工作表， [共用國家/地區](/help/forms/assets/enquiry-options.xlsx) 中顯示的選項 `Destination` 中的下拉式清單 `enquiry` 表單。

   請參閱下圖的 `shared-country` 試算表：

   ![國家/地區的下拉式清單](/help/forms/assets/drop-down-country-options.png)
3. 預覽和發佈 `shared-country` 工作表使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

   請參閱顯示 `shared-country` 工作表： https://main--wefinance--wkndforms.hlx.live/enquiry.json?sheet=country

>[!NOTE]
>
> `?sheet=country` 是附加至URL的查詢引數。 此引數指出根據 `shared-country` 工作表。 它會重新導向至包含與不同國家/地區相關資訊的JSON檔案。

## 新增URL以載入下拉式清單選項{#add-url}

此 `Options` 屬性 `select` 欄位接受URL。 URL會傳回當作選項使用的JSON陣列 `Destination` 下拉式清單。 若要新增URL以載入下拉式清單選項：

1. 前往Microsoft®SharePoint或Google Drive上的AEM專案資料夾，然後開啟試算表。 您也可以為表單建立新的試算表。
1. 複製的URL `shared-country` 將工作表貼到 `Options` 欄為 `Destination` 欄位。

   ![查詢試算表](/help/forms/assets/drop-down-enquiry.png)

1. 預覽和發佈工作表，使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).


   ![國家/地區的下拉式清單](/help/forms/assets/load-dropdown-options-form.png)

您可參閱 [查詢試算表](/help/forms/assets/enquiry-options.xlsx) 新增URL以載入下拉式清單選項。

將URL整合至表單定義以載入下拉式清單選項後， `Destination` 下拉式清單會從URL開始出現。

請參閱下列URL，其中顯示 `enquiry` 顯示儲存在單獨頁面中的選項的表單：

https://main--wefinance--wkndforms.hlx.live/enquiry-form

## 另請參閱

{{see-more-forms-eds}}


