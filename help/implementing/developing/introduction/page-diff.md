---
title: 開發與頁面比較
description: 瞭解「頁面比較」功能的運作方式，以及它對開發人員的影響
translation-type: tm+mt
source-git-commit: fee73b5f5ba69422494efe554ac5aa62c046ad86
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---


# 開發與頁面比較 {#developing-and-page-diff}

## 功能概觀 {#feature-overview}

內容建立是一個反覆的過程。 製作具效率的內容需要能夠查看從一個迭代到另一個迭代的變化。 檢視一個頁面版本，然後檢視另一個頁面版本則無效率且容易出錯。 作者想要能夠並排比較目前頁面與先前版本的差異。

頁面差異可讓使用者比較目前頁面與啟動、舊版等。 有關此用戶功能的詳細資訊，請參 [閱頁面差異](/help/sites-cloud/authoring/features/page-diff.md)。

## 操作詳細資訊 {#operation-details}

比較頁面版本時，使用者想要比較的舊版會由AEM在背景重新建立，以利比較。 這需要能夠演算內容以 [進行並排比較](/help/sites-cloud/authoring/features/page-diff.md)。

此娛樂作業由AEM在內部完成，而且對使用者透明，不需要干預。 但是，在CRX DE Lite中查看儲存庫的管理員在內容結構中可以看到這些重新建立的版本。

比較內容時，會在下列位置重新建立整個要比較頁面的樹狀結構：

`/tmp/versionhistory/`

自動執行清除任務以清除此臨時內容。

## 權限 {#permissions}

比較是透過DOM比較在用戶端進行，讓比較程式變得簡單，但開發人員需要考慮許多限制。

* 此功能使用的CSS類別名稱與AEM產品間隔不開。 如果頁面上包含其他具有相同名稱的自訂CSS類別或第三方CSS類別，則會影響比較的顯示。

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* 由於比較是客戶端，並在頁面載入時執行，因此在客戶端比較服務運行後對DOM的任何調整都不會計算在內。 這可能會影響

   * 使用AJAX來包含內容的元件
   * 單頁應用程式
   * 在使用者互動時控制DOM的Javascript型元件。
