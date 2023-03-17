---
title: 通用編輯器驗證
description: 了解通用編輯器如何驗證。
source-git-commit: f454475b65da8f410812bbbe30ca5fc393be410a
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---


# 通用編輯器驗證 {#authentication}

了解通用編輯器如何驗證。

## 選項 {#options}

通用編輯器使用Adobe的Identity Management系統(IMS)驗證，這是透過統一殼層提供。

所有應用程式/遠程頁面都負責對所需的後端系統進行身份驗證。 通用編輯器服務需要此驗證來供後端系統執行CRUD操作，因為它是獨立服務。

實作選項會依您使用通用編輯器的方式而有所不同。

* [標準流量](#standard-flow)  — 適用於AEMas a Cloud Service或使用IMS的AMS。
* [第三方流量](#third-party-flow)  — 適用於AEM內部部署或不含IMS的AMS

## 標準流量 {#standard-flow}

這是AEMas a Cloud Service和AMS使用IMS來使用通用編輯器的解決方案。

若要使用通用編輯器，使用者必須登入針對IMS驗證的統一殼層。 提供的IMS代號儲存在使用者工作階段存放區中。

每當使用者執行CRUD作業時，就會傳送呼叫至通用編輯器服務，並在HTTP標題中帶有IMS承載權杖。 然後，通用編輯器服務會使用承載權杖，根據AEM後端系統驗證請求，以使用者名稱執行操作。

![標準驗證流程](assets/standard-flow.png)

## 其他資源 {#additional-resources}

若要進一步了解通用編輯器，請參閱這些檔案。

* [通用編輯器簡介](introduction.md)  — 了解通用編輯器如何啟用編輯任何實作中任何內容的任何方面，以提供優越的體驗、提高內容速度，並提供最新的開發人員體驗。
* [使用通用編輯器編寫內容](authoring.md)  — 了解內容作者使用通用編輯器建立內容有多簡單且直覺。
* [AEM通用編輯器快速入門](getting-started.md)  — 了解如何存取通用編輯器，以及如何開始檢測您的第一個AEM應用程式以使用它。
* [通用編輯器架構](architecture.md)  — 了解通用編輯器的架構，以及資料在其服務與層之間如何流動。
* [屬性和類型](attributes-types.md)  — 了解通用編輯器需要的資料屬性和類型。
