---
title: 屬性和類型
description: 了解通用編輯器需要的資料屬性和類型。
source-git-commit: 0e66c379e10d275610d85a699da272dc0c32a9a8
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 7%

---


# 屬性和類型 {#attributes-types}

了解通用編輯器需要的資料屬性和類型。

## 簡介 {#introduction}

為了讓通用編輯器可編輯應用程式，必須正確檢測應用程式。 這包括納入適當的中繼資料，讓編輯器可以編輯應用程式的內容。 本檔案詳細說明這些中繼資料的屬性和類型。

>[!NOTE]
>
>會在伺服器端執行內容驗證。 通用編輯器只能與資料屬性搭配使用。 需在API層級處理符合模型/結構的驗證。

## 資料屬性 {#data-properties}

| 資料屬性 | 說明 |
|---|---|
| `itemid` | URN至資源，請參閱區段 [檢測AEM中通用編輯器快速入門檔案的頁面](getting-started.md#instrument-thepage) |
| `itemprop` | 資源的屬性，請參閱區段 [檢測AEM中通用編輯器快速入門檔案的頁面](getting-started.md#instrument-thepage) |
| `itemtype` | 可編輯項目的類型（例如文字、影像、參考等） |
| `data-editor-itemfilter` | 定義可使用的參照 |
| `data-editor-itemlabel` | 為編輯器中顯示的可選項定義自定義標籤 <br>在 `itemmodel` 已設定，則會透過模型擷取標籤 |
| `data-editor-itemmodel` | 定義將用於屬性邊欄中表單式編輯的模型 |
| `data-editor-behavior` | 定義檢測器的行為，例如，獨立文本或影像也可以模擬元件，使其可移動或可刪除 |

## 項目類型 {#item-types}

| `itemtype` | 說明 | `itemid` | `itemprop` | `data-editor-itemfilter` | `data-editor-itemlabel` | `data-editor-itemmodel` | `data-editor-behvior` |
|---|---|---|---|---|---|---|---|
| `text` | 文字可在HTML標籤內編輯，但只能以簡單的文字格式，沒有可用的RTF格式，這通常用於標題元件，例如 | 選用 | 必要 | N/A | 選用 | N/A | 選用 |
| `richtext` | 使用完整RTF功能可編輯文字。 RTE會顯示在右側面板中 | 選用 | 必要 | N/A | 選用 | N/A | 選用 |
| `media` | 可編輯的資產，例如影像或視訊 | 選用 | 必要 | 可選<br>傳遞至資產選擇器的影像或視訊篩選條件清單 | 選用 | N/A | 選用 |
| `container` | 可編輯的行為與元件的容器一樣，即段落系統。 | 視情況而定 <br>下面 | 視情況而定 <br>下面 | 可選<br>允許的元件清單 | 選用 | N/A | N/A |
| `component` | 可編輯的是元件。 不會新增其他功能，需要用來指示DOM的可移動/可刪除部分，以及開啟屬性邊欄及其欄位 | 必要 | N/A | N/A | 選用 | 選用 | N/A |
| `reference` | 可編輯是參考，例如內容片段、體驗片段或產品 | 視情況而定 <br>下面 | 視情況而定 <br>下面 | 可選<br>內容片段、產品或體驗片段篩選條件清單，此條件會傳遞至參考選取器 | 選用 | 選用 | N/A |

視使用案例而定 `itemprop` 或 `itemid` 可能是必要或不必要。 例如：

* `itemid` 如果您透過GraphQL查詢內容片段，而且想要讓清單在內容中可編輯，則此為必要項目。
* `itemprop` 如果元件已轉譯所參考內容片段的內容，且您想要更新元件內的參考，則此為必要項目。

## 行為 {#behaviors}

| `data-editor-behavior` | 說明 |
|---|---|
| `component` | 可用來讓獨立文字、RTF和媒體模擬元件，以便在頁面上移動和刪除元件 |

## 其他資源 {#additional-resources}

若要進一步了解通用編輯器，請參閱這些檔案。

* [通用編輯器簡介](introduction.md)  — 了解通用編輯器如何啟用編輯任何實作中任何內容的任何方面，以提供優越的體驗、提高內容速度，並提供最新的開發人員體驗。
* [使用通用編輯器編寫內容](authoring.md)  — 了解內容作者使用通用編輯器建立內容有多簡單且直覺。
* [使用通用編輯器發佈內容](publishing.md)  — 了解通用視覺編輯器如何發佈內容，以及您的應用程式如何處理已發佈的內容。
* [AEM通用編輯器快速入門](getting-started.md)  — 了解如何存取通用編輯器，以及如何開始檢測您的第一個AEM應用程式以使用它。
* [通用編輯器架構](architecture.md)  — 了解通用編輯器的架構，以及資料在其服務與層之間如何流動。
* [通用編輯器驗證](authentication.md)  — 了解通用編輯器如何驗證。
