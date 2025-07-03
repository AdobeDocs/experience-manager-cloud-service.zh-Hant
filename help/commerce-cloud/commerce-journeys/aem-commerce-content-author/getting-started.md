---
title: CIF 編寫快速入門
description: CIF製作快速入門。
exl-id: 0bef4d8c-0ad3-4ec8-ab08-8c83203b3b68
feature: Commerce Integration Framework
role: Admin
index: false
source-git-commit: 173b70aa6f9ad848d0f80923407bf07540987071
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 2%

---

# AEM CIF製作快速入門 {#getting-started}

進一步瞭解Adobe Experience Manager (AEM) CIF Authoring。

## 目前進度 {#story-so-far}

在此AEM內容和Commerce歷程的上一個檔案[瞭解AEM內容和Commerce](/help/commerce-cloud/introduction.md)中，您已瞭解Headless CMS的基本理論和概念，以及AEM內容和Commerce。

本文基於這些基礎之上。

## 目標 {#objective}

本檔案可協助您瞭解如何使用CIF進行內容及Commerce特定撰寫。 閱讀文件後，您應該會：

* 瞭解使用AEM中的頁面編輯器進行CIF撰寫的概念
* 如何使用產品和類別選擇器存取AEM中的產品目錄資料
* 如何使用產品駕駛艙和AEM Omnisearch存取內容和商務資料

## 在AEM頁面編輯器中編寫CIF {#cif-authoring}

CIF擴充AEM中的頁面編輯器，提供存取即時產品資料的功能，而不需離開內容：

開啟側面板，然後從下拉式清單中選取「產品」。
![選取產品型別](assets/asset-finder-overview.png)

您可以瀏覽產品目錄或使用全文檢索搜尋欄位來尋找產品。
![產品型別](assets/asset-finder-search.png)

產品可放置在支援產品放置的元件上（例如產品Teaser、產品輪播），而頁面會自動建立產品Teaser元件。

## 產品和類別選擇器 {#pickers}

如果Commerce元件或AEM後台對話方塊中需要產品和類別資料，AEM作者可以使用屬於UI元素的選擇器，輕鬆搜尋和選取產品目錄資料。

### 產品挑選器

按一下資料夾圖示會開啟選擇器強制回應UI （例如產品Teaser）
![產品挑選器](assets/product-picker-open.png)

瀏覽左側的目錄結構或搜尋，即可找到產品。 全文檢索搜尋會遵循選取的類別，並將搜尋結果限制在此類別。
![產品挑選器資料夾](assets/product-picker-folders.png)

具有變異的產品會以資料夾圖示標籤，而且可以按一下該圖示顯示所有變異。
![產品挑選器變體](assets/product-picker-variants.png)
![產品挑選器變體已開啟](assets/product-picker-variants-open.png)

### 類別選取器

像產品選擇器一樣運作。 按一下資料夾圖示會開啟選擇器強制回應視窗UI （例如類別輪播）
![類別選擇器](assets/category-picker-open.png)

瀏覽左側的目錄結構並選取類別。
![類別選擇器](assets/category-picker-folders.png)

## 產品駕駛艙 {#cockpit}

產品駕駛艙是快速存取產品目錄及其所有豐富內容的中心位置。 您會在接下來的其中一個單元中學習如何使用內容豐富產品資料。 現在，讓我們專注於存取產品資料。

從主功能表中按一下商務，以檢視所有附加產品目錄的清單。
![商務功能表專案](assets/commerce-menu-item.png)

這會顯示所有已連線產品目錄的清單。
![駕駛艙整合式目錄](assets/cockpit-Integrated-catalogs.png)

產品目錄依預設會顯示所有產品的所有第一級類別。 按一下類別會開啟該類別，其中包含所有相關產品和子類別，包括其產品。
![駕駛艙產品目錄](assets/cockpit-product-catalog.png)

您可以按一下屬性圖示來開啟產品屬性。 將滑鼠游標停留在產品圖磚上會顯示圖示。
![駕駛艙產品屬性](assets/cockpit-properties.png)

所有產品屬性都是唯讀的，因為資料會從連線的後端即時載入。 變更產品屬性必須在後端系統（記錄系統）中完成。 標籤&#x200B;**Variants**只有在產品有變化時才出現。 按一下標籤會顯示所有變數及其屬性。
![駕駛艙產品變體](assets/cockpit-properties-variants.png)

其餘索引標籤會顯示與產品相關聯的所有AEM內容。 這些標籤將在下一個模組中討論。

## AEM Omnisearch {#omnisearch}

使用Omnisearch是一種透過全文檢索搜尋AEM內容的簡單方法。 CIF延伸了Omnisearch，全文搜尋產品目錄及其相關聯的AEM內容。
![商務功能表專案](assets/omnisearch.png)

Omnisearch會在商務後端執行全文檢索搜尋，以尋找所有相關產品。 結果列在&#x200B;**檢視所有產品**&#x200B;下。 Omnisearch也會搜尋AEM中與搜尋到的產品相關聯的內容。 結果會列在個別AEM類別下。 在此範例中，一個內容片段與產品相關。

## 後續步驟 {#what-is-next}

現在您已完成歷程的這一部分，您應該：

* 瞭解使用頁面編輯器編寫CIF的概念
* 如何使用產品和類別選擇器存取AEM中的產品目錄
* 如何使用產品駕駛艙和AEM Omnisearch存取內容和商務資料

在此知識的基礎上繼續您的歷程，接下來檢閱檔案[管理產品目錄頁面和範本](catalog-templates.md)，瞭解如何建立和自訂您的第一個產品目錄體驗。

## 其他資源 {#additional-resources}

雖然我們建議您繼續下一段歷程 — [管理產品目錄頁面和範本](catalog-templates.md) — 以下是一些可選資源，這些資源對這裡提到的一些概念進行了更深入的探究。 不過，這些選用資源並非繼續此歷程的必要條件。

* [設定存放區和目錄](/help/commerce-cloud/getting-started.md#catalog)
