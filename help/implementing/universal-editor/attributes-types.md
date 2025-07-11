---
title: 屬性和項目類型
description: 瞭解Universal Editor所需的資料屬性和專案型別。
exl-id: 02795a31-244a-42b4-8297-2649125d7777
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 597315a7d569ebd62243322c543627b7a3535a6b
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 45%

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
| `data-aue-type` | [可編輯專案的型別](#item-types) （例如，文字、影像和參考） |
| `data-aue-filter` | 定義：<br> — 已啟用哪些RTE功能<br> — 可以將哪些元件新增到容器<br> — 可以將哪些資產新增到媒體型別 |
| `data-aue-label` | 為編輯器中顯示的可選取專案定義自訂標籤 |
| `data-aue-model` | 定義在屬性面板中用於表單式編輯的模型 |
| `data-aue-behavior` | 已過時。 它曾經定義檢測器的行為，允許獨立文字、RTF和媒體模擬元件，以便它們也能在頁面上移動和刪除，提供`component`的單一潛在值。 此屬性現在會被忽略，當具有`data-aue-resource`的專案是容器的直接子系時，它會自動被視為元件。 |

## 項目類型 {#item-types}

| `data-aue-type` | 說明 | `data-aue-resource` | `data-aue-prop` | `data-aue-filter` | `data-aue-label` | `data-aue-model` |
|---|---|---|---|---|---|---|
| `text` | 文字在 HTML 標籤內是可編輯的，但只能是簡單的文字格式，RTF 格式無法編輯，這通常用於標題元件，例如 | 選用 | 必要 | N/A | 選用 | N/A |
| `richtext` | 文字是可編輯的，具有完整的 RTF 功能。RTE 會顯示在右側面板中 | 選用 | 必要 | N/A | 選用 | N/A |
| `media` | 可編輯的是資產，例如影像或影片 | 選用 | 必要 | 傳遞給資產選擇器的選擇性<br>影像或影片篩選條件清單 | 選用 | N/A |
| `container` | 可編輯的行為就像元件的容器，也就是段落系統。 | 視情況而定 <br> (請參閱下文)。 | 視情況而定 <br> (請參閱下文)。 | 選擇性 <br> 允許元件清單 | 選用 | N/A |
| `component` | 可編輯的是元件。它不會新增額外功能。必須指出DOM的可移動/可刪除部分，以及開啟屬性面板及其欄位時 | 必要 | N/A | N/A | 選用 | 選用 |
| `reference` | 可編輯是參考資料，例如內容片段、體驗片段或產品 | 視情況而定 <br> (請參閱下文)。 | 視情況而定 <br> (請參閱下文)。 | 傳遞給參考選擇器的選擇性<br>內容片段、產品或體驗片段篩選條件清單 | 選用 | 選用 |

`data-aue-resource`永遠是必要的，因為它是表示內容變更寫入位置的主索引鍵。

* 不需要直接在設定`data-aue-type`的標籤上進行。
* 如果未設定，則會使用最接近父項的`data-aue-resource`屬性。

當您想要在內容中進行編輯時需要`data-aue-prop`，但選用容器除外（如果設定容器為內容片段且prop指向多重參考欄位）。

* `data-aue-prop`是`data-aue-resource`之主索引鍵要更新的屬性。
