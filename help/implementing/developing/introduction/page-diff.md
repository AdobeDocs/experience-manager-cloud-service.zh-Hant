---
title: 開發與頁面差異
description: 了解頁面差異功能的運作方式，以及如何影響開發人員
exl-id: 03c08616-2203-4b90-bed6-4836266e2507
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 1%

---

# 開發與頁面差異 {#developing-and-page-diff}

## 功能概述 {#feature-overview}

內容建立是一個迭代過程。 以效率製作需要能夠查看從一個迭代到另一個迭代的更改。 檢視一個頁面版本，而另一個頁面版本則效率低下且容易出錯。 作者想要能夠並排比較目前的頁面與上一個版本，並反白顯示差異。

頁面差異可讓使用者比較目前的頁面與啟動、舊版等。 如需此使用者功能的詳細資訊，請參閱 [頁面差異](/help/sites-cloud/authoring/features/page-diff.md).

## 操作詳細資訊 {#operation-details}

比較頁面版本時，使用者想要比較的舊版本會由AEM在背景重新建立，以利比較。 這必須能夠呈現內容 [並排比較](/help/sites-cloud/authoring/features/page-diff.md).

此休閒作業由AEM內部完成，且對使用者而言是透明的，不需要干預。 但是，如果管理員檢視儲存庫（例如在CRX DE Lite中），會在內容結構中看到這些重新建立的版本。

比較內容時，會在下列位置重新建立要比較的頁面前整個樹狀結構：

`/tmp/versionhistory/`

清除任務會自動運行以清除此臨時內容。

## 限制 {#limitations}

差異會透過DOM比較在用戶端發生，使得差異處理程式更簡單，但開發人員需要考慮許多限制。

* 此功能使用的CSS類別名稱與AEM Product不同。 如果頁面上包含其他具有相同名稱的自訂CSS類或第三方CSS類，則差異的顯示可能會受到影響。

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* 由於差異是用戶端並會在頁面載入時執行，因此在用戶端差異服務執行後對DOM所做的任何調整都不會計入。 這可能會影響

   * 使用AJAX來包含內容的元件
   * 單頁應用程式
   * 在使用者互動時操控DOM的Javascript型元件。
