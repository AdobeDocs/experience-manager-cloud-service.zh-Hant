---
title: 屬性和項目類型
description: 瞭解Universal Editor所需的資料屬性和專案型別。
exl-id: 02795a31-244a-42b4-8297-2649125d7777
source-git-commit: b42390dcecb546853380d64808bcf009680c89a3
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 79%

---


# 屬性和類型 {#attributes-types}

瞭解Universal Editor所需的資料屬性和專案型別。

## 簡介 {#introduction}

為了讓 Universal Editor 可以編輯應用程式，必須對其進行適當的檢測。這包括包含適當的中繼資料，以便編輯器可以編輯應用程式的內容。本檔案詳細說明這些中繼資料的屬性和專案型別。

>[!NOTE]
>
>內容驗證在伺服器端執行。Universal Editor 僅使用資料屬性。驗證是否符合模型/結構時，必須在API層級處理。

## 資料屬性 {#data-properties}

| 資料屬性 | 說明 |
|---|---|
| `data-aue-resource` | 資源的 URN，請參閱 [AEM 中 Universal Editor 快速入門文件的檢測頁面](getting-started.md#instrument-thepage)章節 |
| `data-aue-prop` | 資源的屬性，請參閱 [AEM 中 Universal Editor 快速入門文件的檢測頁面](getting-started.md#instrument-thepage)章節 |
| `data-aue-type` | [可編輯專案的型別](#item-types) （例如，文字、影像和參照） |
| `data-aue-filter` | 定義可以使用哪些參考 |
| `data-aue-label` | 為編輯器中顯示的可選項目定義自訂標籤，<br>如果`data-aue-model`已經設定了，會透過模型擷取標籤 |
| `data-aue-model` | 定義模型，該模型用於屬性邊欄中的表單型編輯 |
| `data-aue-behavior` | 定義 [檢測的行為](#behaviors)例如，獨立文字或影像也可以模擬元件，使其可移動或刪除 |

## 項目類型 {#item-types}

| `data-aue-type` | 說明 | `data-aue-resource` | `data-aue-prop` | `data-aue-filter` | `data-aue-label` | `data-aue-model` | `data-aue-behavior` |
|---|---|---|---|---|---|---|---|
| `text` | 文字在 HTML 標籤內是可編輯的，但只能是簡單的文字格式，RTF 格式無法編輯，這通常用於標題元件，例如 | 選用 | 必要 | N/A | 選用 | N/A | 選用 |
| `richtext` | 文字是可編輯的，具有完整的 RTF 功能。RTE 會顯示在右側面板中 | 選用 | 必要 | N/A | 選用 | N/A | 選用 |
| `media` | 可編輯的是資產，例如影像或影片 | 選用 | 必要 | 傳遞給資產選擇器的選擇性<br>影像或影片篩選條件清單 | 選用 | N/A | 選用 |
| `container` | 可編輯的行為就像元件的容器，也就是段落系統。 | 視情況而定 <br> (請參閱下文)。 | 視情況而定 <br> (請參閱下文)。 | 選擇性 <br> 允許元件清單 | 選用 | N/A | N/A |
| `component` | 可編輯的是元件。它不會新增額外功能。需要它才能指明 DOM 的可移動/可刪除部分，以及開啟屬性邊欄及其欄位 | 必要 | N/A | N/A | 選用 | 選用 | N/A |
| `reference` | 可編輯是參考資料，例如內容片段、體驗片段或產品 | 視情況而定 <br> (請參閱下文)。 | 視情況而定 <br> (請參閱下文)。 | 傳遞給參考選擇器的選擇性<br>內容片段、產品或體驗片段篩選條件清單 | 選用 | 選用 | N/A |

根據使用案例 `data-aue-prop` 或 `data-aue-resource`，可能需要也可能不需要。例如：

* `data-aue-resource`如果您透過 GraphQL 查詢內容片段，並且希望清單可在內容中編輯，則需要。
* `data-aue-prop`如果您有元件呈現參考內容片段的內容，並且您想要更新元件中的參考，則需要。

## 行為 {#behaviors}

| `data-aue-behavior` | 說明 |
|---|---|
| `component` | 用於讓獨立的文字、RTF 和媒體模仿元件，因此也可以在頁面上將其移動和刪除 |
| `container` | 用於容許將容器視為自己的元件，因此可以在頁面上將其移動和刪除 |
