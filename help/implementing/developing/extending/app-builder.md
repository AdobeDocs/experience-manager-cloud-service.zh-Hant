---
title: 使用「Adobe開發人員應用程式產生器」將 [!DNL Adobe Experience Manager] 延伸為Cloud Service。
description: 使用「Adobe開發人員應用程式產生器」將 [!DNL Adobe Experience Manager] 延伸為Cloud Service。
source-git-commit: 4bd0419ff31195fef1565b50f87b4b55f81361f0
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 0%

---


# 使用「Adobe開發人員應用程式產生器」將[!DNL Adobe Experience Manager]擴充為Cloud Service {#extend-using-app-builder}

## 什麼是AEM as aCloud Service的App Builder {#project-firefly}

全新的Adobe開發人員應用程式產生器為開發人員提供擴充性架構，以輕鬆將AEM擴充為Cloud Service功能。

App Builder提供統一的協力廠商擴充性架構，可整合及建立可擴充Adobe Experience Manager的自訂體驗。 有了這一基於Adobe基礎架構的完整可擴充性框架，開發人員可以跨Adobe解決方案和IT堆棧的其餘部分構建自定義微服務、擴展和整合Adobe Experience Manager。

App Builder可讓客戶在各種使用案例中輕鬆擴充Adobe Experience Manager:

* 中間件的可擴充性 — 將外部系統與Adobe應用程式連接，以建立自訂連接器，或利用一套預先建立的整合。
* 核心服務的擴充性 — 透過自訂功能和業務邏輯擴充預設行為，以擴充核心應用程式功能。
* 使用者體驗的擴充性 — 延伸核心體驗，以支援業務需求，或建立客戶專屬的數位屬性、店面和後台應用程式。

自2020年夏季起，企業客戶和合作夥伴都可透過開發人員預覽功能，取得App Builder（舊稱Project Firefly）。 App Builder的正式發行(GA)預計於2021年12月推出。 我們歡迎開發人員透過我們的[試用計畫](http://adobe.ly/appbuilder-trial)試用App Builder。

## 架構 {#architecture}

「Adobe開發人員應用程式產生器」不提供現成可用的解決方案，而是提供通用、一致且標準化的開發平台，可擴充Adobe雲端解決方案，例如AEM，包括：

* Adobe開發人員主控台 — 適用於自訂微服務和擴充功能開發，讓開發人員在建立外掛程式和整合所需的所有工具和API時，能建立和管理專案。
* 開發人員工具 — 開放原始碼工具、SDK和程式庫，讓開發人員可輕鬆建立自訂擴充功能和整合。 使用React Spectrum(Adobe的UI工具套件)來擁有適用於所有Adobe應用程式的通用UI。
* 服務 — 用於在無伺服器平台上托管基礎架構的I/O運行時，以及用於事件型整合的I/O事件。 我們也提供儲存資料和檔案的現成可用支援。
* Adobe Experience Cloud — 開發人員可提交擴充功能和整合，以發佈在其Experience Cloud組織中。然後，系統管理員就可以檢閱、管理及核准這些擴充功能。 發佈後，您的自訂App Builder擴充功能和工具便可與其他Adobe Experience Cloud應用程式一併取得。

下圖說明以App Builder建置的標準應用程式如何運用下列功能：

![架構](/help/implementing/developing/extending/assets/firefly-architecture.jpg)

如需App Builder架構的詳細資訊，請參閱[架構概述](https://www.adobe.io/project-firefly/docs/guides/)。

## 開始使用App Builder {#additional-resources}

為協助您開始使用App Builder，我們建立了一系列檔案來協助您開始：

* [App Builder快速入門](https://www.adobe.io/project-firefly/docs/getting_started/)

## 繼續學習說明檔案 {#appbuilder-documentation}

App Builder提供開發人員的影片和檔案，包括指南和參考檔案，協助您開始開發自己的自訂應用程式：

* [App Builder檔案](https://www.adobe.io/project-firefly/docs/overview/)
* [App Builder影片](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o)

## 請試用其中一個示例應用程式 {#appbuilder-codesamples}

準備好開發了嗎？ 我們提供許多樣本應用程式，幫助您快速前進：

* [Adobe開發人員網站上的應用程式建立工具程式碼實驗室](https://www.adobe.io/project-firefly/docs/resources/)

## 支援 {#support}

對於開發人員支援類型的請求，我們鼓勵開發人員使用我們的[Experience League論壇](https://experienceleaguecommunities.adobe.com/t5/project-firefly/ct-p/project-firefly)。
