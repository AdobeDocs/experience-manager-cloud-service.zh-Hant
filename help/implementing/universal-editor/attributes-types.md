---
title: 屬性和類型
description: 了解 Universal Editor 需要的資料屬性和類型。
source-git-commit: 0e66c379e10d275610d85a699da272dc0c32a9a8
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 100%

---


# 屬性和類型 {#attributes-types}

了解 Universal Editor 需要的資料屬性和類型。

## 簡介 {#introduction}

為了讓 Universal Editor 可以編輯應用程式，必須對其進行適當的檢測。這包括包含適當的中繼資料，以便編輯器可以編輯應用程式的內容。本文件詳細說明了這些中繼資料的屬性和類型。

>[!NOTE]
>
>內容驗證在伺服器端執行。Universal Editor 僅使用資料屬性。需要在 API 層級驗證它們是否適合模型/結構。

## 資料屬性 {#data-properties}

| 資料屬性 | 說明 |
|---|---|
| `itemid` | 資源的 URN，請參閱 [AEM 中 Universal Editor 快速入門文件的檢測頁面](getting-started.md#instrument-thepage)章節 |
| `itemprop` | 資源的屬性，請參閱 [AEM 中 Universal Editor 快速入門文件的檢測頁面](getting-started.md#instrument-thepage)章節 |
| `itemtype` | 可編輯項目的類型 (例如文字、影像、參考等) |
| `data-editor-itemfilter` | 定義可以使用哪些參考 |
| `data-editor-itemlabel` | 為編輯器中顯示的可選項目定義自訂標籤 <br>如果`itemmodel`已經設定了，將透過模型擷取標籤 |
| `data-editor-itemmodel` | 定義模型，該模型將用於屬性邊欄中的表單型編輯 |
| `data-editor-behavior` | 定義檢測行為，例如獨立的文字或影像也可以像元件一樣可移動或刪除 |

## 項目類型 {#item-types}

| `itemtype` | 說明 | `itemid` | `itemprop` | `data-editor-itemfilter` | `data-editor-itemlabel` | `data-editor-itemmodel` | `data-editor-behvior` |
|---|---|---|---|---|---|---|---|
| `text` | 文字在 HTML 標籤內是可編輯的，但只能是簡單的文字格式，RTF 格式無法編輯，這通常用於標題元件，例如 | 選用 | 必要 | N/A | 選用 | N/A | 選用 |
| `richtext` | 文字是可編輯的，具有完整的 RTF 功能。RTE 將顯示在右側面板中 | 選用 | 必要 | N/A | 選用 | N/A | 選用 |
| `media` | 可編輯的是資產，例如影像或影片 | 選用 | 必要 | 傳遞給資產選擇器的選擇性<br>影像或影片篩選條件清單 | 選用 | N/A | 選用 |
| `container` | 可編輯的行為就像元件的容器，也就是段落系統。 | 視情況而定 <br> (請參閱下文)。 | 視情況而定 <br> (請參閱下文)。 | 選擇性 <br> 允許元件清單 | 選用 | N/A | N/A |
| `component` | 可編輯的是元件。不新增額外的功能，將需要指示 DOM 的可移動/可刪除部分以及打開屬性邊欄及其欄位 | 必要 | N/A | N/A | 選用 | 選用 | N/A |
| `reference` | 可編輯的是參考，例如內容片段、體驗片段或產品 | 視情況而定 <br> (請參閱下文)。 | 視情況而定 <br> (請參閱下文)。 | 傳遞給參考選擇器的選擇性<br>內容片段、產品或體驗片段篩選條件清單 | 選用 | 選用 | N/A |

根據使用案例 `itemprop` 或 `itemid`，可能需要也可能不需要。例如：

* `itemid`如果您透過 GraphQL 查詢內容片段，並且希望清單可在內容中編輯，則需要。
* `itemprop`如果您有元件呈現參考內容片段的內容，並且您想要更新元件中的參考，則需要。

## 行為 {#behaviors}

| `data-editor-behavior` | 說明 |
|---|---|
| `component` | 可用於讓獨立的文字、RTF 和媒體模仿元件，讓它們也可以在頁面上移動和刪除 |

## 其他資源 {#additional-resources}

若要了解有關 Universal Editor 的詳細資訊，請參閱以下文件。

* [Universal Editor 簡介](introduction.md) - 了解 Universal Editor 如何在任意實施中編輯任何方面的內容，以提供卓越的體驗、提高內容速度並提供最先進的開發人員體驗。
* [使用 Universal Editor 編寫內容](authoring.md) - 了解內容作者使用 Universal Editor 建立內容有多簡單和直觀。
* [使用 Universal Editor 發佈內容](publishing.md) - 了解 Universal Visual Editor 如何發佈內容，和您的應用程式如何處理發佈的內容。
* [AEM 中 Universal Editor 快速入門](getting-started.md) - 了解如何存取 Universal Editor，以及如何開始檢測您的第一個 AEM 應用程式以使用它。
* [Universal Editor 架構](architecture.md) - 了解 Universal Editor 的架構，以及資料如何在其服務和階層之間流動。
* [Universal Editor 驗證](authentication.md) - 了解 Universal Editor 如何進行驗證。
