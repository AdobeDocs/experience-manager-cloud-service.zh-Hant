---
title: 開發和頁面差異
description: 瞭解頁面差異功能的運作方式及其對開發人員的影響
exl-id: 03c08616-2203-4b90-bed6-4836266e2507
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 1%

---

# 開發和頁面差異 {#developing-and-page-diff}

## 功能概述 {#feature-overview}

內容建立是一個反複的過程。 以高效率撰寫需要能夠檢視反複專案之間的變更。 檢視一個頁面版本然後檢視另一個頁面版本會效率低下，並容易發生錯誤。 作者想要能夠並排比較目前頁面與先前版本，並醒目提示差異。

頁面差異可讓使用者將目前頁面與啟動項、舊版等專案進行比較。 如需此使用者功能的詳細資訊，請參閱[頁面差異](/help/sites-cloud/authoring/sites-console/page-diff.md)。

## 作業詳細資料 {#operation-details}

比較頁面的版本時，使用者想要比較的先前版本會由AEM在背景重新建立，以利差異的進行。 若要呈現內容[以並排比較](/help/sites-cloud/authoring/sites-console/page-diff.md)，則必須使用這個舊版。

此重新建立操作由AEM內部完成，對使用者而言是透明的，不需要任何干涉。 但是，管理員檢視存放庫(例如，在CRXDE Lite中)，會在內容結構中看到這些重新建立的版本。

比較內容時，系統會在下列位置重新建立整個樹狀結構，一直到要比較的頁面為止：

`/tmp/versionhistory/`

清除工作會自動執行，以清除此暫存內容。

## 限制 {#limitations}

差異是透過DOM比較在使用者端發生，讓差異處理程式變得簡單。 不過，開發人員必須考量到幾項限制。

* 此功能使用的CSS類別未與AEM產品建立名稱空間。 如果頁面上包含其他相同名稱的自訂CSS類別或協力廠商CSS類別，差異的顯示可能會受到影響。

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* 由於diff是使用者端並在頁面載入時執行，因此使用者端diff服務執行後對DOM所做的任何調整都不會計入。 此程式可能會影響下列專案：

   * 使用AJAX來包含內容的元件
   * 單頁應用程式
   * 在使用者互動時操控DOM的JavaScript型元件。
