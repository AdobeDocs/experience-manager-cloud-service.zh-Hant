---
title: 使用Adobe Developer App Builder延伸 [!DNL Adobe Experience Manager] as a Cloud Service。
description: 使用Adobe Developer App Builder延伸 [!DNL Adobe Experience Manager] as a Cloud Service。
exl-id: 50d82745-5deb-4bfa-961b-714842403601
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 00a05b3bdc1a689947c1507847da99b54c94dcac
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# 使用Adobe Developer App Builder延伸[!DNL Adobe Experience Manager] as a Cloud Service {#extend-using-app-builder}

## 什麼是AEM as a Cloud Service適用的App Builder {#project-appbuilder}

新的Adobe Developer App Builder為開發人員提供了一個擴充性架構，以便輕鬆擴充AEM as a Cloud Service中的功能。

App Builder提供統一的協力廠商擴充性架構，可整合及建立擴充Adobe Experience Manager的自訂體驗。 有了這個以Adobe基礎架構為基礎的完整擴充性架構，開發人員可以建立自訂微服務，並在Adobe解決方案和IT棧疊的其餘部分間擴充及整合Adobe Experience Manager。

App Builder為客戶提供了一種方法，可輕鬆地在各種使用案例中擴充Adobe Experience Manager：

* 中介軟體擴充性 — 將外部系統與Adobe應用程式連線以建置自訂聯結器，或使用預先建立的整合套件。
* 核心服務擴充性 — 透過自訂功能和商業邏輯擴充預設行為，進而擴充核心應用程式功能。
* 使用者體驗擴充性 — 擴充核心體驗以支援業務需求，或建置客戶專屬的數位財產、店面和後台應用程式。

>[!NOTE]
>
> 若是想要使用App Builder的AEM 6.5客戶，請參閱[使用Adobe Developer App Builder延伸Adobe Experience Manager 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/app-builder.html?lang=zh-Hant)。

## 架構 {#architecture}

Adobe Developer App Builder並非提供立即可用的解決方案，而是提供通用、一致、標準化的開發平台，以擴充Adobe Cloud解決方案(例如AEM)，包括：

* Adobe Developer Console — 對於自訂微服務和擴充功能開發，可讓開發人員在存取所有所需工具和API時建置和管理專案，以便建立外掛程式和整合。
* 開發人員工具 — 開放原始碼工具、SDK和程式庫，讓開發人員可輕鬆建立自訂擴充功能和整合。 使用React Spectrum (Adobe的UI工具組)，讓所有Adobe應用程式擁有一個共同的使用者介面。
* 服務 — 在Adobe的無伺服器平台上託管基礎建設的I/O執行階段，以及用於事件式整合的I/O事件。 Adobe也提供開箱即用的資料與檔案儲存支援。
* Adobe Experience Cloud — 開發人員可提交擴充功能和整合專案，以便在其Experience Cloud組織中發佈。系統管理員可以檢閱、管理和核准這些擴充功能。 發佈後，您的自訂App Builder擴充功能和工具可與其他Adobe Experience Cloud應用程式一併找到。

下圖說明在App Builder上建置的標準應用程式如何使用這些功能：

![架構](/help/implementing/developing/extending/assets/appbuilder-architecture.jpg)

如需App Builder架構的詳細資訊，請參閱[架構概覽。](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/architecture_overview/architecture-overview)

## 開始使用App Builder {#additional-resources}

Adobe已建立快速入門檔案，方便您開始使用App Builder：

* [App Builder快速入門](https://developer.adobe.com/app-builder/docs/getting_started/)

## 繼續學習說明檔案 {#appbuilder-documentation}

App Builder為開發人員提供影片和檔案，包括指南，以及參考檔案，協助您開始開發自己的自訂應用程式：

* [App Builder檔案](https://developer.adobe.com/app-builder/docs/overview/)
* [App Builder影片](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o)

## 試用其中一個範例應用程式 {#appbuilder-codesamples}

準備好開始開發了嗎？ Adobe有許多範例應用程式可協助您快速上手：

* [Adobe Developer網站上的App Builder Code Labs](https://developer.adobe.com/app-builder/docs/resources/)