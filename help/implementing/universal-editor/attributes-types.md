---
title: 屬性和項目類型
description: 了解通用編輯器需要的資料屬性和項目類型。
exl-id: 02795a31-244a-42b4-8297-2649125d7777
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 100%

---


# 屬性和類型 {#attributes-types}

了解通用編輯器需要的資料屬性和項目類型。

## 簡介 {#introduction}

為了讓 Universal Editor 可以編輯應用程式，必須對其進行適當的檢測。這包括包含適當的中繼資料，以便編輯器可以編輯應用程式的內容。本文件將詳細說明這些後設資料的屬性和項目類型。

>[!NOTE]
>
>內容驗證在伺服器端執行。Universal Editor 僅使用資料屬性。必須在 API 層級驗證其是否符合模型/結構。

## 資料屬性 {#data-properties}

| 資料屬性 | 說明 |
|---|---|
| `data-aue-resource` | 資源的 URN，請參閱 [AEM 中 Universal Editor 快速入門文件的檢測頁面](getting-started.md#instrument-thepage)章節 |
| `data-aue-prop` | 資源的屬性，請參閱 [AEM 中 Universal Editor 快速入門文件的檢測頁面](getting-started.md#instrument-thepage)章節 |
| `data-aue-type` | [可編輯項目的類型](#item-types) (例如文字、影像和參照) |
| `data-aue-filter` | 定義：<br>- 啟用哪些 RTE 功能<br>- 可將哪些元件新增到容器<br>- 可將哪些資產新增到媒體類型 |
| `data-aue-label` | 為編輯器中顯示的可選項目定義自訂標籤 |
| `data-aue-model` | 定義在屬性面板中用於表單型編輯的模型 |
| `data-aue-behavior` | 已淘汰。之前曾定義檢測的行為，讓獨立的文字、RTF 和媒體能夠模仿元件，以便同樣可以在頁面上移動和刪除，從而提供 `component` 的單一潛在價值。現在會忽略這個屬性，若具有 `data-aue-resource` 的項目為容器的直接子系，則會自動將其視為元件。 |

## 項目類型 {#item-types}

| `data-aue-type` | 說明 | `data-aue-resource` | `data-aue-prop` | `data-aue-filter` | `data-aue-label` | `data-aue-model` |
|---|---|---|---|---|---|---|
| `text` | 文字在 HTML 標籤內是可編輯的，但只能是簡單的文字格式，RTF 格式無法編輯，這通常用於標題元件，例如 | 選用 | 必要 | N/A | 選用 | N/A |
| `richtext` | 可以使用 RTF 文字功能來編輯文字。RTE 會顯示在右側面板中 | 選用 | 必要 | N/A | 選用 | N/A |
| `media` | 可編輯項目是一項資產，例如影像或影片 | 選用 | 必要 | 傳遞給資產選擇器的選擇性<br>影像或影片篩選條件清單 | 選用 | N/A |
| `container` | 可編輯的行為就像元件的容器，也就是段落系統。 | 視情況而定 <br> (請參閱下文)。 | 視情況而定 <br> (請參閱下文)。 | 選擇性 <br> 允許元件清單 | 選用 | N/A |
| `component` | 可編輯的是元件。它不會新增額外功能。必須使用元件才能指明 DOM 的可移動/可刪除部分，以及開啟屬性面板及其欄位。 | 必要 | N/A | N/A | 選用 | 選用 |
| `reference` | 可編輯項目是一項參照，例如內容片段、體驗片段或產品 | 視情況而定 <br> (請參閱下文)。 | 視情況而定 <br> (請參閱下文)。 | 傳遞給參考選擇器的選擇性<br>內容片段、產品或體驗片段篩選條件清單 | 選用 | 選用 |

`data-aue-resource` 永遠是必要屬性，因為這是指明內容變更寫入位置的主索引鍵。

* 不需要在設定 `data-aue-type` 的標記上直接設定。
* 若未設定，則會使用最接近之上層標籤的 `data-aue-resource` 屬性。

每當您想要在內容中進行編輯時，`data-aue-prop` 皆屬必要，但是可選用此屬性的容器除外 (若設定屬性，容器便是內容片段，且 prop 指向多重參照欄位)。

* `data-aue-prop` 是 `data-aue-resource` 主索引鍵所要更新的屬性。
