---
title: AEM Screens as a Cloud Service 簡介
description: 了解 AEM Screens as a Cloud Service。
exl-id: b1cc0a63-ecd3-4d89-ac49-f384cc610cdc
feature: Screens Deployments
role: Admin, Developer, User
source-git-commit: 53086e2ec6d9d962a8f1cb1cc40f0601da74ac63
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 98%

---


# AEM Screens as a Cloud Service 簡介 {#introduction-screens-cloud}

有了 Adobe Experience Manager Screens as a Cloud Service，您可以建立吸引人的動態數位招牌體驗，用於公共空間。它是 AEM Screens 產品的下一個進化階段，代表可用性和可擴展性的重大進展。

AEM Screens as a Cloud Service 是數位招牌解決方案，可讓行銷人員大規模建立和管理動態數位體驗。同時，這也涉及不同類型的實體螢幕，作為全面數位行銷策略的一部分。它擴展了 Adobe 的全管道產品/服務，超越一般網頁和行動管道，還包括我們周圍的數位招牌管道。透過深度了解如何建立內容、組合內容、管理觸發的事件以及為任何公共公間的所有取用者和訪客播放媒體，AEM Screens as a Cloud Service 可實現相關性更高、更符合情境、更富成效及符合期望的使用者體驗。

## 了解 Screens as a Cloud Service 元件 {#understanding-components}

Screens as a Cloud Service 有兩個主要元件，即：

* **[內容提供者](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html?lang=zh-Hant)**，這是在 AEM Cloud Service 或 Adobe Managed Services (AMS) 上執行的 Screens 附加元件。Screens 內容提供者可讓內容作者建立和管理管道。內容作者可以新增新內容、編輯內容，而無需擔心建立顯示器或播放器註冊的細節。內容提供者提取開發內容、顯示器或播放器註冊的基本細節。

* **[服務提供者](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/navigating-to-screens-services-provider.html?lang=zh-Hant)**，這是在 Adobe I/O Runtime 上運作的數位招牌管理服務。Screens 服務提供者可讓內容作者、開發人員和管理員在內容新增到管道後，管理顯示器和播放器以播放內容。同時，Screens 服務提供者會通知協調器內容將在何處以及何時在高層級播放。


## 架構概觀 {#architectural-overview}

身為 AEM Screens as a Cloud Service 使用者，您可以新增和管理頻道中的內容。您可以透過專為 Screens as a Cloud Service 設計的介面來註冊和管理顯示器和播放器；即為 **Screens 服務提供者**&#x200B;和 **Screens 內容提供者**&#x200B;專門設計的介面。

![架構概觀](/help/screens-cloud/assets/architecture-screenscloud.png)
