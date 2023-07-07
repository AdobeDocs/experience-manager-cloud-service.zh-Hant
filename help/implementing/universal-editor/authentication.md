---
title: Universal Editor 驗證
description: 了解 Universal Editor 如何進行驗證。
exl-id: fb86c510-3c41-4511-81b7-1bdf2f5e7dd3
source-git-commit: 0f62245d31074ab7a64d86b97ef3b1a8d7533001
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 89%

---


# Universal Editor 驗證 {#authentication}

了解 Universal Editor 如何進行驗證。

## 選項 {#options}

Universal Editor 使用 Adobe 的 Identity Management System (IMS) 驗證，這是透過 Unified Shell 提供的。

所有應用程式/遠端頁面都負責對所需後端系統進行驗證。Universal Editor 服務需要此驗證才能向後端系統執行 CRUD 動作，因為它是一項獨立服務。

## 標準流程 {#standard-flow}

這是 AEM as a Cloud Service 和「使用 IMS 的 AMS」運用 Universal editor 的解決方案。

若要使用 Universal Editor，使用者必須登入針對 IMS 進行驗證的 Unified Shell。提供的 IMS 權杖會儲存在使用者工作階段儲存體中。

每當使用者執行 CRUD 動作時，都會使用 HTTP 標頭中的 IMS 持有人權杖向 Universal Editor 服務發送呼叫。然後，Universal Editor 服務使用持有人權杖對 AEM 後端系統的要求進行驗證，並以使用者的名義執行動作。

![標準驗證流程](assets/standard-flow.png)

## 其他資源 {#additional-resources}

若要了解有關 Universal Editor 的詳細資訊，請參閱以下文件。

* [通用編輯器簡介](introduction.md)  — 瞭解通用編輯器如何讓您編輯任何實作中任何內容的任何方面，以便提供卓越的體驗、提高內容速度並提供一流的開發人員體驗。
* [使用 Universal Editor 編寫內容](authoring.md) - 了解內容作者使用 Universal Editor 建立內容有多簡單和直觀。
* [使用 Universal Editor 發佈內容](publishing.md) - 了解 Universal Visual Editor 如何發佈內容，和您的應用程式如何處理發佈的內容。
* [AEM 中 Universal Editor 快速入門](getting-started.md) - 了解如何存取 Universal Editor，以及如何開始檢測您的第一個 AEM 應用程式以使用它。
* [Universal Editor 架構](architecture.md) - 了解 Universal Editor 的架構，以及資料如何在其服務和階層之間流動。
* [屬性和類型](attributes-types.md) - 了解 Universal Editor 需要的資料屬性和類型。
