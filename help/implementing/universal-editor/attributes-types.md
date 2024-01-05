---
title: 屬性與料號型態
description: 瞭解Universal Editor所需的資料屬性和專案型別。
exl-id: 02795a31-244a-42b4-8297-2649125d7777
source-git-commit: 7550491de94f1e2cbb28b07f8abbdaded5aa04ea
workflow-type: tm+mt
source-wordcount: '686'
ht-degree: 81%

---


# 屬性和類型 {#attributes-types}

瞭解Universal Editor所需的資料屬性和專案型別。

{{universal-editor-status}}

## 簡介 {#introduction}

為了讓 Universal Editor 可以編輯應用程式，必須對其進行適當的檢測。這包括包含適當的中繼資料，以便編輯器可以編輯應用程式的內容。本檔案詳細說明這些中繼資料的屬性和專案型別。

>[!NOTE]
>
>內容驗證在伺服器端執行。Universal Editor 僅使用資料屬性。驗證是否符合模型/結構時，必須在API層級處理。

## 資料屬性 {#data-properties}

| 資料屬性 | 說明 |
|---|---|
| `itemid` | 資源的 URN，請參閱 [AEM 中 Universal Editor 快速入門文件的檢測頁面](getting-started.md#instrument-thepage)章節 |
| `itemprop` | 資源的屬性，請參閱 [AEM 中 Universal Editor 快速入門文件的檢測頁面](getting-started.md#instrument-thepage)章節 |
| `itemtype` | 可編輯項目的類型 (例如文字、影像和參考) |
| `data-editor-itemfilter` | 定義可以使用哪些參考 |
| `data-editor-itemlabel` | 為編輯器中顯示的可選項目定義自訂標籤，<br>如果`itemmodel`已經設定了，會透過模型擷取標籤 |
| `data-editor-itemmodel` | 定義模型，該模型用於屬性邊欄中的表單型編輯 |
| `data-editor-behavior` | 定義檢測的行為，例如，獨立的文字或影像也可以模擬元件，使其可移動或可刪除 |

## 項目類型 {#item-types}

| `itemtype` | 說明 | `itemid` | `itemprop` | `data-editor-itemfilter` | `data-editor-itemlabel` | `data-editor-itemmodel` | `data-editor-behvior` |
|---|---|---|---|---|---|---|---|
| `text` | 文字在 HTML 標籤內是可編輯的，但只能是簡單的文字格式，RTF 格式無法編輯，這通常用於標題元件，例如 | 選用 | 必要 | N/A | 選用 | N/A | 選用 |
| `richtext` | 文字是可編輯的，具有完整的 RTF 功能。RTE 會顯示在右側面板中 | 選用 | 必要 | N/A | 選用 | N/A | 選用 |
| `media` | 可編輯的是資產，例如影像或影片 | 選用 | 必要 | 傳遞給資產選擇器的選擇性<br>影像或影片篩選條件清單 | 選用 | N/A | 選用 |
| `container` | 可編輯的行為就像元件的容器，也就是段落系統。 | 視情況而定 <br> (請參閱下文)。 | 視情況而定 <br> (請參閱下文)。 | 選擇性 <br> 允許元件清單 | 選用 | N/A | N/A |
| `component` | 可編輯的是元件。它不會新增額外功能。需要它才能指明 DOM 的可移動/可刪除部分，以及開啟屬性邊欄及其欄位 | 必要 | N/A | N/A | 選用 | 選用 | N/A |
| `reference` | 可編輯是參考資料，例如內容片段、體驗片段或產品 | 視情況而定 <br> (請參閱下文)。 | 視情況而定 <br> (請參閱下文)。 | 傳遞給參考選擇器的選擇性<br>內容片段、產品或體驗片段篩選條件清單 | 選用 | 選用 | N/A |

根據使用案例 `itemprop` 或 `itemid`，可能需要也可能不需要。例如：

* `itemid`如果您透過 GraphQL 查詢內容片段，並且希望清單可在內容中編輯，則需要。
* `itemprop`如果您有元件呈現參考內容片段的內容，並且您想要更新元件中的參考，則需要。

## 行為 {#behaviors}

| `data-editor-behavior` | 說明 |
|---|---|
| `component` | 用於讓獨立的文字、RTF 和媒體模仿元件，因此也可以在頁面上將其移動和刪除 |
| `container` | 用於容許將容器視為自己的元件，因此可以在頁面上將其移動和刪除 |

## 其他資源 {#additional-resources}

若要了解有關 Universal Editor 的詳細資訊，請參閱以下文件。

* [Universal Editor 簡介](introduction.md) - 了解 Universal Editor 如何在任意實作中編輯任何方面的內容，以便提供卓越的體驗、提高內容速度並提供最先進的開發人員體驗。
* [使用 Universal Editor 編寫內容](authoring.md) - 了解內容作者使用 Universal Editor 建立內容有多簡單和直覺。
* [使用通用編輯器發佈內容](publishing.md)  — 瞭解通用編輯器如何發佈內容，以及您的應用程式如何處理已發佈的內容。
* [AEM 中 Universal Editor 快速入門](getting-started.md) - 了解如何存取 Universal Editor，以及如何開始檢測您的第一個 AEM 應用程式以使用它。
* [Universal Editor 架構](architecture.md) - 了解 Universal Editor 的架構，以及資料如何在其服務和階層之間流動。
* [Universal Editor 驗證](authentication.md) - 了解 Universal Editor 如何進行驗證。
