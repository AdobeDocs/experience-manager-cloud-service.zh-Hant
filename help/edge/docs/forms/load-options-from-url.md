---
title: 從 URL 載入下拉式清單選項
description: 下拉式清單選項是包含在不同的試算表中，然後可透過提供的 URL 匯入到主要試算表中。
feature: Edge Delivery Services
source-git-commit: 2affe155b285986128487043fcc4f2938fc15842
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 59%

---


# 從 URL 載入下拉式清單選項

Forms通常包含下拉式功能表，供使用者從預先定義的選項中選取。 這些選項通常會在表單本身中定義，但管理長清單可能會很麻煩。 本指南會概述如何透過URL從個別的試算表載入下拉式選項，以改善表單撰寫作業。


從個別試算表載入下拉式清單選項的好處包括：

* 簡化管理：在一個集中位置維護下拉式清單選項，以更輕鬆地進行更新和新增。
* 提高效率：無須在表單定義中手動新增長選項清單。




![下拉式清單選項](/help/forms/assets/drop-down-options.png)


閱讀完本文章後，您將學會：

* [在單獨的電子表格中定義選項](#define-options)
* [新增 URL 以載入下拉式清單選項](#add-url)

## 在單獨的工作表中定義選項 {#define-options}

在個別試算表中定義選項

1. 建立試算表：
   1. 在Microsoft®SharePoint或Google Drive中找到AEM專案資料夾。
   1. 新增頁面。 例如，「shared-country」。
1. 定義選項欄：新增兩欄：「選項」和「值」。
   * 「選項」會定義下拉式選單中顯示的文字。
   * 「值」會定義使用者選取選項時提交的值。

   >[!NOTE]
   >
   >如果選項和值都相同，則只需要「Option」欄。

1. 填入試算表：在「選項」欄（如有必要，也在「值」欄）中輸入國家/地區選項。

   如需結構，請參閱以下範例。

   ![國家/地區下拉式選單](/help/forms/assets/drop-down-country-options.png)

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 來預覽和發佈`shared-country`工作表。

   請參閱顯示`shared-country` 工作表的 URL：
https://main--wefinance--wkndforms.hlx.live/enquiry.json?sheet=country

>[!NOTE]
>
> `?sheet=country`是附在 URL 的查詢參數。此參數表示根據`shared-country`工作表篩選後的 JSON。這會重新導向包含與不同國家/地區相關資訊的 JSON 檔案。

## 新增 URL 以載入下拉式清單選項{#add-url}

`Options`欄位的`select`屬性可接受 URL。該 URL 會傳回一個 JSON 陣列，可用作`Destination`下拉式清單的選項。若要新增 URL 以載入下拉式清單選項：

1. 前往 Microsoft® SharePoint 或 Google Drive 的 AEM 專案資料夾，並開啟您的試算表。您也可以為表單建立新的試算表。
1. 複製`shared-country`工作表的 URL，並將其貼上到`Destination`欄位的`Options`欄中。

   ![查詢試算表](/help/forms/assets/drop-down-enquiry.png)

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 來預覽和發佈試算表。


   ![國家/地區下拉式選單](/help/forms/assets/load-dropdown-options-form.png)

您可以參考[查詢試算表](/help/forms/assets/enquiry-options.xlsx)，以新增載入下拉式清單選項的 URL。

將 URL 整合到表單定義並載入下拉式清單選項後，`Destination`下拉式清單的選項一開始會從 URL 顯示。

請參閱下面的 URL，當中會顯示`enquiry`表單 (顯示單獨工作表中儲存的選項)：

https://main--wefinance--wkndforms.hlx.live/enquiry-form

## 另請參閱

{{see-more-forms-eds}}


