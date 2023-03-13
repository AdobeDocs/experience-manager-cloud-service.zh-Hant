---
title: AEM Headless 架構
description: 了解 Adobe Experience Manager 高階架構，因為它與無周邊部署相關。了解 AEM 作者、預覽和發佈服務的角色，以及無周邊應用程式的建議部署模式。
feature: Content Fragments,GraphQL API
exl-id: 5ba6921f-b06e-463d-b956-d1fb434090c9
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: ht
source-wordcount: '554'
ht-degree: 100%

---

# AEM Headless 架構

典型的 AEM 環境由作者服務、發佈服務和預覽服務 (選用) 組成。

* **作者服務**&#x200B;是內部使用者建立、管理和預覽內容的地方。

* **發佈服務**&#x200B;被認為是「即時」環境，通常是一般使用者與其互動。內容在作者服務上經編輯和核准後，將傳遞到發佈服務。AEM 無周邊應用程式最常見的部署模式是讓應用程式的生產版本連接到 AEM Publish 服務。

* **預覽服務**&#x200B;的功能與&#x200B;**發佈服務**&#x200B;相同。但是，它僅供內部使用者使用。因為最適合核准者用來審查即將發生的內容變更，然後再上線給一般使用者。

* **Dispatcher** 是靜態 Web 伺服器，增加了 AEM Dispatcher 模組。它提供快取功能和另一層安全性。**Dispatcher** 位在&#x200B;**發佈**&#x200B;和&#x200B;**預覽**&#x200B;服務之前。

在 AEM as a Cloud Service 方案中，您可以擁有多個環境：開發、預備和生產。每個環境都有自己獨特的&#x200B;**作者**、**發佈**&#x200B;和&#x200B;**預覽**&#x200B;服務。您可以在[此處](/help/implementing/cloud-manager/manage-environments.md)進一步了解如何管理環境。

## 作者發佈模型

AEM 無周邊應用程式最常見的部署模式是讓應用程式的生產版本連接到 AEM Publish 服務。

![作者發佈架構](assets/autho-publish-architecture-diagram.png)

上圖描述了這種常見的部署模式。

1. **內容作者**&#x200B;使用 AEM Author 服務來建立、編輯及管理內容。
1. **內容作者**&#x200B;和其他內部使用者可以直在作者服務預覽內容。可以設定連接到作者服務的應用程式預覽版本。
1. 內容經核准後，即可發佈到 AEM Publish 服務。
1. **Dispatcher** 是&#x200B;**發佈**&#x200B;服務前面的一層，可以快取某些要求並提供加一層安全性。
1. 一般使用者是與應用程式生產版本互動。應用程式生產版本透過 Dispatcher 連接到發佈服務，並使用 GraphQL API 要求和取用內容。

## 作者、預覽、發佈、部署

另一種無周邊部署方法是納入 **AEM Preview** 服務。使用這種方法，內容可以首先發佈到&#x200B;**預覽**&#x200B;服務，無周邊應用程式預覽版本可以連接到它。這種方法的優點是&#x200B;**預覽**&#x200B;服務可以設定成與&#x200B;**發佈**&#x200B;服務有相同的驗證需求和權限，以便輕鬆模擬生產體驗。

![作者、預覽和發佈架構](assets/author-preview-publish-architecture-diagram.png)

1. **內容作者** 使用 AEM Author 服務來建立、編輯及管理內容。
1. 內容首先發佈到 AEM Preview 服務。
1. 可以設定連接到預覽服務的應用程式預覽版本。
1. 內容經審核及核准後，即可發佈到 AEM Publish 服務。
1. 一般使用者是與應用程式生產版本互動。應用程式生產版本透過 Dispatcher 連接到發佈服務，並使用 GraphQL API 要求和取用內容。
