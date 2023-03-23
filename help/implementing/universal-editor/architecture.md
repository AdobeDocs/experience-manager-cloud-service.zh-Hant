---
title: 通用編輯器架構
description: 了解通用編輯器的架構，以及資料在其服務與層之間如何流動。
source-git-commit: 0e66c379e10d275610d85a699da272dc0c32a9a8
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 1%

---


# 通用編輯器架構 {#architecture}

了解通用編輯器的架構，以及資料在其服務與層之間如何流動。

## 架構建置區塊 {#building-blocks}

通用編輯器由四個基本建置區塊組成，可互動讓內容作者編輯任何實作中任何內容的任何方面，以提供優越的體驗、提高內容速度，並提供最新的開發人員體驗。

1. [編輯](#editors)
1. [遠端應用程式](#remote-app)
1. [API層](#api-layer)
1. [持久層](#persistence-layer)

本檔案概述這些基礎要素的每一個，以及它們如何交換資料。

![通用編輯器的架構](assets/architecture.png)

>[!TIP]
>
>如果您想查看通用編輯器及其架構的實際運作，請參閱本檔案 [AEM通用編輯器快速入門](getting-started.md) 了解如何存取通用編輯器，以及如何開始檢測您的第一個AEM應用程式以使用它。

### 編輯 {#editors}

* **通用編輯器**  — 通用編輯器使用工具化DOM來允許就地編輯內容。 請查看該文檔 [屬性和類型](attributes-types.md) 以取得必要中繼資料的詳細資訊。 請參閱檔案 [AEM通用編輯器快速入門](getting-started.md) 例如AEM中的檢測範例。
* **屬性邊欄**  — 無法在內容中編輯元件的某些屬性，例如輪播的旋轉時間，或應一律開啟或關閉折疊式功能表索引標籤。 為了允許編輯這種元件資訊，在編輯器的側邊欄中提供基於表單的編輯器。

### 遠端應用程式 {#remote-app}

若要讓應用程式內文可在通用編輯器中編輯，必須檢測DOM。 遠端應用程式必須在DOM中轉譯特定屬性。 請查看該文檔 [屬性和類型](attributes-types.md) 以取得必要中繼資料的詳細資訊。 請參閱檔案 [AEM通用編輯器快速入門](getting-started.md) 例如AEM中的檢測範例。

通用編輯器致力於將SDK降至最低，因此儀器是遠端應用程式實作的責任。

### API層 {#api-layer}

* **內容資料**  — 對於通用編輯器，內容資料的來源系統及其使用方式並不重要。 只有使用內容內可編輯的資料來定義和提供所需屬性才重要。
* **持續資料**  — 對於每個可編輯的資料，都有URN標識符。 此URN用於將持久性路由到正確的系統和資源。

### 持久層 {#persistence-layer}

* **內容片段模型**  — 若要支援用於編輯內容片段屬性的邊欄，需要內容片段編輯器和表單式編輯器、每個元件的模型和內容片段。
* **內容**  — 內容可儲存在任何位置，例如AEM、Magento等。

![持久層](assets/persistence-layer.png)

## 通用編輯器服務和後端系統調度 {#service}

通用編輯器將所有內容更改分派到稱為通用編輯器服務的集中服務。 此服務於Adobe I/O Runtime上執行，會根據提供的URN載入擴充功能註冊表中可用的外掛程式。 外掛程式負責與後端通訊並傳回統一回應。

![通用編輯器服務](assets/universal-editor-service.png)

## 演算管道 {#rendering-pipelines}

### 伺服器端轉譯 {#server-side}

![伺服器端轉譯](assets/server-side.png)

### 靜態網站產生 {#static-generation}

![靜態網站產生](assets/static-generation.png)

### 用戶端轉譯 {#client-side}

![用戶端呈現](assets/client-side.png)

## 其他資源 {#additional-resources}

若要進一步了解通用編輯器，請參閱這些檔案。

* [通用編輯器簡介](introduction.md)  — 了解通用編輯器如何啟用編輯任何實作中任何內容的任何方面，以提供優越的體驗、提高內容速度，並提供最新的開發人員體驗。
* [使用通用編輯器編寫內容](authoring.md)  — 了解內容作者使用通用編輯器建立內容有多簡單且直覺。
* [使用通用編輯器發佈內容](publishing.md)  — 了解通用視覺編輯器如何發佈內容，以及您的應用程式如何處理已發佈的內容。
* [AEM通用編輯器快速入門](getting-started.md)  — 了解如何存取通用編輯器，以及如何開始檢測您的第一個AEM應用程式以使用它。
* [屬性和類型](attributes-types.md)  — 了解通用編輯器需要的資料屬性和類型。
* [通用編輯器驗證](authentication.md)  — 了解通用編輯器如何驗證。
