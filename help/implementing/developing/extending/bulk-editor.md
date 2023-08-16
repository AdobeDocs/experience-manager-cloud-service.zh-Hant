---
title: 設定頁面屬性的大量編輯
description: 了解如何設定大量編輯，以便您可以同時編輯多個頁面的屬性。
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 93%

---


# 設定頁面屬性的大量編輯 {#configuring-bulk-editing-of-page-properties}

[大量編輯頁面屬性](/help/sites-cloud/authoring/fundamentals/page-properties.md#from-the-sites-console-multiple-pages) 可讓您一次編輯多個頁面的屬性。

## 考量事項 {#considerations}

預設情況下，頁面屬性未啟用大量編輯。這項功能必須明確啟用。定義可進行大量編輯的頁面屬性時，您需要考慮特定意涵，例如：

* 某些欄位通常是唯一的。套用一個值時，您必須決定啟用這類欄位的大量編輯是否有意義。
   * 例如，頁面標題幾乎永遠是唯一的。
* 某些欄位可能具有多個值，在轉譯時需要有意義的表示。
   * 例如，標示為「**準備好發佈**」的狀態下拉選單。在大量編輯之前，這可能會有幾個值，例如&#x200B;**就緒**、**檢閱中**、**進行中**&#x200B;等。

由於可能存在多個值，建議僅啟用下列欄位類型供大量編輯。

* `/libs/granite/ui/components/foundation/form/textfield`
* `/libs/granite/ui/components/foundation/form/textarea`
* `/libs/granite/ui/components/foundation/form/tagspicker`
* `/libs/granite/ui/components/foundation/form/datepicker`
* `/libs/granite/ui/components/foundation/form/pathbrowser`
* `/libs/granite/ui/components/foundation/form/checkbox`

## 啟用欄位 {#enabling-a-field}

這些步驟會使用 `/apps/core/wcm/components/page/v1/page` (來自 [WKND 範本內容](/help/implementing/developing/introduction/develop-wknd-tutorial.md)) 作為在開發環境中啟用欄位大量編輯的範例。

1. 使用 CRXDE 開啟您的頁面元件。
1. 導覽至 `cq:dialog` 定義內的所需欄位。
1. 在欄位節點上定義以下屬性：

   * **名稱**：`allowBulkEdit`
   * **類型**：`Boolean`
   * **值**：`true`

1. 選取「**儲存全部**」即可保留您的更新。

## 限制 {#limitations}

頁面屬性的大量編輯有以下特性：

* 不適用於 Live Copy 內的頁面。
* 僅適用於具有相同資源類型的頁面。
