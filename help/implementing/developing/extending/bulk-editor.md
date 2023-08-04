---
title: 設定大量編輯頁面屬性
description: 瞭解如何設定大量編輯，以便一次編輯多個頁面的屬性。
source-git-commit: 9563c24c2794f8209494891da1a4a5a3360781db
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 1%

---


# 設定大量編輯頁面屬性 {#configuring-bulk-editing-of-page-properties}

[大量編輯頁面屬性](/help/sites-cloud/authoring/fundamentals/page-properties.md#from-the-sites-console-multiple-pages) 可讓您一次編輯多個頁面的屬性。

## 考量事項 {#considerations}

預設不會啟用頁面屬性以進行大量編輯。 它們必須明確啟用。 在定義可供大量編輯的頁面屬性時，您必須考量某些含意，例如：

* 某些欄位通常是不重複的。 您必須決定啟用此類欄位進行大量編輯是否有意義，何時將套用一個值。
   * 例如，頁面標題幾乎永遠都是唯一的。
* 某些欄位可能有多個值，在轉譯時需要有意義的表示。
   * 例如，狀態下拉式清單，其標籤為 **準備發佈**. 在大量編輯之前，這可能有數個值，例如 **就緒**， **稽核中**， **進行中**&#x200B;等

由於可能存在多個值，建議僅啟用以下欄位型別以進行大量編輯。

* `/libs/granite/ui/components/foundation/form/textfield`
* `/libs/granite/ui/components/foundation/form/textarea`
* `/libs/granite/ui/components/foundation/form/tagspicker`
* `/libs/granite/ui/components/foundation/form/datepicker`
* `/libs/granite/ui/components/foundation/form/pathbrowser`
* `/libs/granite/ui/components/foundation/form/checkbox`

## 啟用欄位 {#enabling-a-field}

這些步驟使用 `/apps/core/wcm/components/page/v1/page` 從 [WKND範例內容](/help/implementing/developing/introduction/develop-wknd-tutorial.md) 例如，可在開發環境中的欄位上啟用大量編輯。

1. 使用CRXDE開啟您的頁面元件。
1. 導覽至 `cq:dialog` 定義。
1. 在欄位節點上定義下列屬性：

   * **名稱**: `allowBulkEdit`
   * **型別**： `Boolean`
   * **值**: `true`

1. 選取 **全部儲存** 以持續儲存您的更新。

## 限制 {#limitations}

大量編輯頁面屬性為：

* 不適用於即時副本中的頁面。
* 僅適用於具有相同資源型別的頁面。
