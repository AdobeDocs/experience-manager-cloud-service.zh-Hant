---
title: AEM Screensas a Cloud Service簡介
description: 本頁介紹AEM Screensas a Cloud Service。
exl-id: b1cc0a63-ecd3-4d89-ac49-f384cc610cdc
source-git-commit: 4b76fbbb1b58324065b39d6928027759b0897246
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# AEM Screensas a Cloud Service簡介 {#introduction-screens-cloud}

借助AEM Screensas a Cloud Service，您可以建立吸引人且動態的數字標牌體驗，以便在公共空間中使用。 它是AEM Screens產品的下一個發展，是可用性和可擴充性方面的一個重大飛躍。

AEM Screensas a Cloud Service是一種數字標牌解決方案，使營銷人員能夠建立和管理動態的數字型驗。 此外，它還涉及不同類型的物理螢幕，作為綜合數字營銷戰略的一部分。 它將Adobe的全方位渠道服務擴展到了通常的網路和移動渠道之外，還包括我們周圍的數字標牌渠道。 AEM Screensas a Cloud Service通過深入理解內容建立、內容整合、觸發事件管理以及任何公共空間中所有消費者和訪問者的媒體回放，實現更相關、上下文相關、高效和可預見的用戶體驗。

## 瞭解螢幕中的元件as a Cloud Service {#understanding-components}

螢幕as a Cloud Service有兩個主要元件，即：

* **[內容提供程式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html?lang=en)**，即在AEM Cloud Service或Adobe托管服務(AMS)上運行的「螢幕」載入項。 螢幕內容提供程式允許內容作者建立和管理頻道。 內容作者可以添加新內容、編輯內容，而無需擔心建立顯示器或播放器註冊的詳細資訊。 內容提供方從開發內容、顯示或播放器註冊的基礎詳細資訊中提供抽象。

* **[服務提供商](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/configure-screens-cloud/navigating-to-screens-services-provider.html?lang=en)**&#x200B;在Adobe I/O運行時運行的數字標牌管理服務。 螢幕服務提供程式允許內容作者、開發人員和管理員在內容添加到頻道後管理內容播放的顯示器和播放器。 此外，「螢幕服務提供程式」會通知Orchestrator內容將在何處以及何時在高級別播放。


## 體系結構概述 {#architectural-overview}

作為AEM Screensas a Cloud Service用戶，您可以添加和管理頻道中的內容，註冊和管理專為螢幕as a Cloud Service而設計的介面中的顯示和播放器，即： **螢幕服務提供程式** 和 **螢幕內容提供程式**。

![影像](/help/screens-cloud/assets/architecture-screenscloud.png)
