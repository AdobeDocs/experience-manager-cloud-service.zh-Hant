---
title: CIF製作快速入門
description: CIF製作快速入門
exl-id: 0bef4d8c-0ad3-4ec8-ab08-8c83203b3b68
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 0%

---

# AEM CIF製作快速入門 {#getting-started}

了解AEM CIF編寫。

## 迄今為止的故事 {#story-so-far}

在此AEM內容與商務歷程的上一份檔案中， [了解AEM內容與商務](/help/commerce-cloud/introduction.md)，您已了解無頭式CMS的基本理論，您現在應該了解AEM內容與商務的基本概念。

本文以這些基本知識為基礎。

## 目標 {#objective}

本檔案可協助您了解如何使用CIF進行內容與商務專屬的編寫。 閱讀後，您應：

* 使用通用編輯器了解CIF製作的概念
* 如何使用產品和類別選擇器存取AEM中的產品目錄資料
* 如何使用產品座艙和AEM Omnisearch存取內容與商務資料

## 通用編輯器的CIF編寫 {#cif-authoring}

CIF擴充了通用編輯器，提供存取即時產品資料而不需離開內容的功能：

開啟側面板，然後從下拉式清單中選取「產品」。
![選擇產品類型](assets/asset-finder-overview.png)

您可以瀏覽產品目錄，或使用全文搜尋欄位來尋找產品。
![產品類型](assets/asset-finder-search.png)

可將產品直接放置在頁面上支援產品投放的元件（例如產品預告、產品轉盤）上，而自動建立產品預告元件。

## 產品和類別選擇器 {#pickers}

如果商務元件或AEM後台對話方塊中需要產品和類別資料，AEM作者可以使用UI元素選擇器，輕鬆搜尋並選取產品目錄資料。

### 產品挑選器

按一下資料夾圖示會開啟選取器強制回應UI（例如產品預告）
![產品選擇器](assets/product-picker-open.png)

瀏覽左側的目錄結構或搜尋，即可找到產品。 全文搜索將遵守選定的類別，並將搜索結果限制為此類別。
![產品選擇器資料夾](assets/product-picker-folders.png)

含有變異的產品會以資料夾圖示標示，按一下該圖示即可顯示所有變異。
![產品選擇器變體](assets/product-picker-variants.png)
![開啟產品選擇器變體](assets/product-picker-variants-open.png)

### 類別選擇器

類似產品選擇器。 按一下資料夾圖示會開啟選取器強制回應UI（例如類別轉盤）
![類別選擇器](assets/category-picker-open.png)

瀏覽左側的目錄結構，然後選取類別。
![類別選擇器](assets/category-picker-folders.png)

## 產品座艙 {#cockpit}

產品座艙是快速訪問產品目錄及其所有豐富內容的中心位置。 您將在下一個模組中學習如何使用內容豐富產品資料。 目前，我們將著重於存取產品資料。

在主功能表中，按一下商務以查看所有附加產品目錄的清單。
![商務功能表項目](assets/commerce-menu-item.png)

這會顯示所有連接產品目錄的清單。
![駕駛艙整合目錄](assets/cockpit-Integrated-catalogs.png)

依預設，產品目錄會顯示所有產品的所有第1層類別。 按一下類別會開啟該類別，其中包含所有相關產品和子類別，包括其產品。
![座艙產品目錄](assets/cockpit-product-catalog.png)

您可以按一下屬性圖示，以開啟產品屬性。 將滑鼠指標暫留在產品圖磚上，即可顯示圖示。
![座艙產品屬性](assets/cockpit-properties.png)

所有產品屬性都為唯讀，因為資料會從連線的後端即時載入。 必須在後端系統（即記錄系統）中更改產品屬性。 索引標籤 **變體** 只有在產品有變體時才會顯示。 按一下索引標籤，會顯示所有具有其屬性的變體。
![駕駛艙產品變型](assets/cockpit-properties-variants.png)

其餘標籤會顯示與產品相關聯的所有AEM內容。 我們將在下一個模組中討論這些頁簽。

## AEM Omnisearch {#omnisearch}

使用Omnisearch是使用全文搜尋來尋找AEM內容的簡單方式。 CIF透過全文搜尋產品目錄及其相關AEM內容，延伸Omnisearch功能。
![商務功能表項目](assets/omnisearch.png)

Omnisearch會在商務後端執行全文搜尋，以尋找所有相關產品。 結果會列在 **查看所有產品**. Omnisearch也會搜尋AEM中與所搜尋產品相關聯的內容。 結果將列在各自的AEM類別下。 在此範例中，一個內容片段與產品相關。

## 下一步 {#what-is-next}

現在您已完成此部分的歷程，您應：

* 使用通用編輯器了解CIF製作的概念
* 如何使用產品和類別選擇器存取AEM中的產品目錄
* 如何使用產品座艙和AEM Omnisearch存取內容與商務資料

根據此知識，接下來檢閱此檔案，繼續您的歷程 [管理產品目錄頁面和範本](catalog-templates.md)，您將在這裡學習如何建立和自訂您的第一個產品目錄體驗。

## 其他資源 {#additional-resources}

雖然建議您檢閱檔案，以繼續前往歷程的下一個階段 [管理產品目錄頁面和範本](catalog-templates.md)，以下是一些額外的選用資源，可深入探討本檔案中提及的一些概念，但您不需要這些資源即可繼續進行歷程。

* [配置儲存和目錄](/help/commerce-cloud/getting-started.md#catalog)
