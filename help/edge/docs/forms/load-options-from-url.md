---
title: 從一個 URL 或另一份工作表載入 Edge Delivery Services for AEM Forms as a Cloud Service 的下拉式清單選項
description: 下拉式清單選項包含在不同的試算表中，然後透過所提供的 URL 匯入到主要試算表。
feature: Edge Delivery Services
exl-id: 5b0bc1b6-6e33-41f3-b7c1-4d997787b6cd
role: Admin, Architect, Developer
source-git-commit: cb914f76b0b785a89b20ef5eaacbc36e8217944b
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 87%

---


# 來自一個 URL 或另一份工作表的 Edge Delivery Services for AEM Forms as a Cloud Service 選項

表單通常包含下拉式選單，供使用者選取預先定義的選項。這些選項通常在表單本身內定義，但清單很長管理起來會很麻煩。本指南概述如何透過 URL 從單獨的試算表載入下拉式清單選項來提升表單製作效率。


從單獨的試算表載入下拉式清單選項的好處是：

* 簡化管理：在集中位置維護下拉式清單選項，可輕鬆更新和新增。
* 提升效率：無需在表單定義中手動新增很長的選項清單。

![下拉式清單選項](/help/forms/assets/drop-down-options.png)


閱讀完本文章後，您將學會：

* [在單獨的試算表中定義選項](#define-options)
* [新增 URL 以載入下拉式清單選項](#add-url)

## 在單獨的工作表中定義選項 {#define-options}

在單獨的試算表中定義選項

1. 建立試算表：
   1. 在 Microsoft® SharePoint 或 Google Drive 中找到 AEM 專案資料夾。
   1. 新增試算表。例如，「共用的國家/地區」。
1. 定義「選項」欄：
新增兩個欄：「選項」和「值」。
   * 「選項」是定義下拉式選單中顯示的文字。
   * 「值」是定義使用者選取該選項時提交的值。

   >[!NOTE]
   >
   >如果選項和值相同，則只需要「選項」欄即可。

1. 填入試算表：
在「選項」欄 (若需要，還有「值」欄) 中輸入您的國家/地區選項。

   請參考下方範例，以了解相關結構。

   ![國家/地區下拉式選單](/help/forms/assets/drop-down-country-options.png)

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 來預覽和發佈`shared-country`工作表。

   例如，如果專案的存放庫命名為「wefinance」，則位於帳戶擁有者「wkndform」下方，而您使用的是「主要」分支，即顯示`shared-country`工作表的URL：
   `https://main--wefinance--wkndform.aem.live/enquiry.json?sheet=country`
   <!--(https://main--wefinance--wkndform.aem.live/enquiry.json?sheet=country)  -->

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

您可以參考[查詢試算表](/help/edge/assets/enquiry.xlsx)，以新增載入下拉式清單選項的 URL。

將 URL 整合到表單定義並載入下拉式清單選項後，`Destination`下拉式清單的選項一開始會從 URL 顯示。

例如，如果專案的存放庫命名為「wefinance」，它位於帳戶擁有者「wkndform」下方，而您使用的是「main」分支，以下URL會顯示`enquiry`表單，其中顯示儲存在個別工作表中的選項：

`https://main--wefinance--wkndform.aem.live/enquiry-form`
<!--(https://main--wefinance--wkndform.aem.live/enquiry-form) 
-->

## 另請參閱

{{see-more-forms-eds}}


