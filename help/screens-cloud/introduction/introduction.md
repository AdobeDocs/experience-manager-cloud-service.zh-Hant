---
title: AEM Screens作為Cloud Service
description: 本頁提供AEM Screens as aCloud Service的簡介。
source-git-commit: 3a636a512da40f9a577d25399d33f96d8f6ad8a0
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---


# AEM Screens as aCloud Service簡介 {#introduction-screens-cloud}

以AEM Screens為Cloud Service，您可以建立吸引人且動態的數位看板體驗，以便在公共空間使用。 這是AEM Screens產品的下一個發展，代表著可用性和可擴充性的重大飛躍。

AEM Screens as aCloud Service是數位看板解決方案，可讓行銷人員大規模建立及管理動態數位體驗。 此外，作為全面數位行銷策略的一部分，它涉及不同類型的實體螢幕。 它將Adobe的全頻道服務擴展到了通常的網路和移動頻道之外，還包括我們身邊的數位看板頻道。 AEM Screens as aCloud Service可讓您深入了解內容建立、內容組合、觸發事件管理，以及任何公共空間中所有消費者和訪客的媒體播放，從而提供更相關、情境式、生產性和預期性的使用者體驗。

## 了解Screens中的元件作為Cloud Service {#understanding-components}

作為Cloud Service的Screens有兩個主要元件，即：

* **[內容提供者](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html?lang=en)**，此元件為在AEMCloud Service或Adobe Managed Services(AMS)上執行的Screens附加元件。Screens內容提供者可讓內容作者建立和管理頻道。 內容作者可以新增內容、編輯內容，不必擔心建立顯示器或播放器註冊的詳細資訊。 內容提供者提供從開發內容、顯示或播放器註冊的基礎詳細資訊的抽象概念。

* **[服務提供者](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/configure-screens-cloud/navigating-to-screens-services-provider.html?lang=en)**，這是在Adobe I/O執行階段上執行的數位看板管理服務。Screens服務提供者可讓內容作者、開發人員和管理員在內容新增至頻道後，管理內容播放的顯示器和播放器。 此外， Screens Services Provider會通知Orchestrator內容將在何處和何時以高級別播放。


## 架構概述 {#architectural-overview}

身為AEM Screens的Cloud Service使用者，您可以從專為Screens設計的介面（即&#x200B;**Screens服務提供者**&#x200B;和&#x200B;**Screens內容提供者**），新增及管理頻道中的內容、註冊及管理顯示器與播放器。

![影像](/help/screens-cloud/assets/architecture-screenscloud.png)

