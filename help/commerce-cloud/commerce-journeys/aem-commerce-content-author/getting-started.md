---
title: CIF創作入門
description: CIF創作入門
exl-id: 0bef4d8c-0ad3-4ec8-ab08-8c83203b3b68
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 0%

---

# CIF創作入AEM門 {#getting-started}

瞭解CIF創AEM作。

## 到目前為止的故事 {#story-so-far}

在此內容和商AEM務之旅的上一文檔中， [瞭解內AEM容和商業](/help/commerce-cloud/introduction.md)，您學習了無頭CMS的基本理論，現在您應該瞭解內容和商AEM業的基本概念。

本文基於這些基本原理。

## 目標 {#objective}

本文檔幫助您瞭解如何將CIF用於特定於內容和商業的創作。 閱讀後，您應：

* 使用通用編輯器瞭解CIF創作的概念
* 如何使用產品和類別選擇AEM器訪問產品目錄資料
* 如何使用產品座艙和Omnisearch訪問內容和商AEM業資料

## 通用編輯器中的CIF創作 {#cif-authoring}

CIF擴展了通用編輯器，它具有訪問即時產品資料而不離開上下文的功能：

開啟側面板，然後從下拉清單中選擇「產品」。
![選擇產品類型](assets/asset-finder-overview.png)

您可以瀏覽產品目錄或使用全文搜索欄位查找產品。
![產品類型](assets/asset-finder-search.png)

產品可以直接放在支援產品投放的元件（例如，產品投放器、產品轉載器）上，該頁面會自動建立產品投放器元件。

## 產品和類別選擇器 {#pickers}

如果商務元件或後台對話中需要產品和類別AEM資料，AEM則作者可以使用UI元素的選取器輕鬆搜索和選擇產品目錄資料。

### 產品挑選器

按一下資料夾表徵圖將開啟選取器模式UI（例如，產品預告）
![產品選取器](assets/product-picker-open.png)

可以通過瀏覽左側的目錄結構或搜索找到產品。 全文搜索將尊重選定的類別，並將搜索結果限制為此類別。
![產品選取器資料夾](assets/product-picker-folders.png)

帶有變體的產品會用資料夾表徵圖進行標籤，該表徵圖可按一下以顯示所有變體。
![產品選擇器變型](assets/product-picker-variants.png)
![產品選擇器變型開啟](assets/product-picker-variants-open.png)

### 類別選取器

工作方式類似於產品選取器。 按一下資料夾表徵圖將開啟選取器模式UI（例如類別旋轉軸）
![類別選取器](assets/category-picker-open.png)

瀏覽左側的目錄結構並選擇類別。
![類別選取器](assets/category-picker-folders.png)

## 產品座艙 {#cockpit}

產品駕駛艙是快速訪問產品目錄及其所有豐富內容的中心位置。 您將在下一個模組中學習如何使用內容豐富產品資料。 現在，我們將重點放在訪問產品資料上。

從主菜單中，按一下commerce查看所有附加產品目錄的清單。
![商務菜單項](assets/commerce-menu-item.png)

這顯示所有連接產品目錄的清單。
![座艙整合目錄](assets/cockpit-Integrated-catalogs.png)

產品目錄預設顯示所有產品的所有第1級類別。 按一下某個類別將開啟該類別，其中包含所有相關產品和子類別，包括其產品。
![座艙產品目錄](assets/cockpit-product-catalog.png)

可以通過按一下屬性表徵圖來開啟產品屬性。 該表徵圖通過懸停在產品圖塊上方顯示。
![座艙產品屬性](assets/cockpit-properties.png)

所有產品屬性都是只讀的，因為資料是從連接的後端即時載入的。 更改產品屬性必須在後端系統（即記錄系統）中完成。 頁籤 **變體** 只有在產品有變體時才顯示。 按一下該頁籤將顯示所有變體及其屬性。
![座艙產品變型](assets/cockpit-properties-variants.png)

其餘的頁籤顯AEM示與產品關聯的所有內容。 我們將在下一個模組中討論這些頁籤。

## 奧姆尼AEM塞克 {#omnisearch}

使用Omnisearch是使用全文搜AEM索查找內容的簡單方法。 CIF擴展了Omnisearch，對產品目錄及其相關內容進行全文AEM搜索。
![商務菜單項](assets/omnisearch.png)

Omnisearch將在商業後端運行全文搜索以查找所有相關產品。 結果列在 **查看所有產品**。 Omnisearch還將搜AEM索與搜索的產品關聯的內容。 結果將列在各個類別AEM下。 在本示例中，一個內容片段與產品相關。

## 下一步是什麼 {#what-is-next}

現在，您已完成此部分行程，您應：

* 使用通用編輯器瞭解CIF創作的概念
* 如何使用產品和類別AEM選擇器訪問產品目錄
* 如何使用產品座艙和Omnisearch訪問內容和商AEM業資料

在此知識基礎上構建並通過下一步查看文檔繼續您的旅程 [管理產品目錄頁和模板](catalog-templates.md)中，您將學習如何構建和定制您的第一個產品目錄體驗。

## 其他資源 {#additional-resources}

雖然建議您通過查看文檔來繼續下一段旅程 [管理產品目錄頁和模板](catalog-templates.md)，下面是一些附加的可選資源，這些資源對本文檔中提到的一些概念進行了更深入的瞭解，但不需要繼續此行程。

* [配置儲存和目錄](/help/commerce-cloud/getting-started.md#catalog)
