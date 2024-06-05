---
title: 延伸 [!DNL Adobe Experience Manager] 使用Adobe Developer App Builder時as a Cloud Service。
description: 延伸 [!DNL Adobe Experience Manager] 使用Adobe Developer App Builder時as a Cloud Service。
exl-id: 50d82745-5deb-4bfa-961b-714842403601
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# 延伸 [!DNL Adobe Experience Manager] 使用Adobe Developer App Builderas a Cloud Service {#extend-using-app-builder}

## 什麼是AEM適用的App Builderas a Cloud Service {#project-appbuilder}

全新的Adobe Developer App Builder為開發人員提供擴充性架構，以便輕鬆擴充AEMas a Cloud Service的功能。

App Builder提供統一的協力廠商擴充架構，可整合及建立擴充Adobe Experience Manager的自訂體驗。 有了這個以Adobe基礎架構為基礎的完整擴充性架構，開發人員便能建立自訂微服務，並跨Adobe解決方案及其他IT棧疊進行擴充和整合Adobe Experience Manager。

App Builder讓客戶能在各種使用案例中輕鬆擴充Adobe Experience Manager：

* 中介軟體擴充性 — 連線外部系統與Adobe應用程式，以建置自訂聯結器，或使用預先建立的整合套件。
* 核心服務擴充性 — 透過自訂功能和商業邏輯擴充預設行為，進而擴充核心應用程式功能。
* 使用者體驗擴充性 — 擴充核心體驗以支援業務需求，或建置客戶專屬的數位財產、店面和後台應用程式。

自2020年夏季起，App Builder已透過Adobe的「開發人員預覽」功能開放企業客戶和合作夥伴使用。 App Builder正式發行(GA)日期排定於2021年12月。 Adobe歡迎開發人員透過試用應用程式生成器 [試用方案](https://developer.adobe.com/app-builder/trial/).

>[!NOTE]
>
> 如需使用App Builder的AEM 6.5客戶，請參閱 [使用Adobe Developer App Builder延伸Adobe Experience Manager 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/app-builder.html).

## 架構 {#architecture}

Adobe Developer App Builder並非開箱即用的解決方案，而是提供通用、一致、標準化的開發平台，以擴充Adobe雲端解決方案(例如AEM)，包括：

* Adobe Developer Console — 對於自訂微服務和擴充功能開發，可讓開發人員在存取所有所需工具和API時建置和管理專案，以便建立外掛程式和整合。
* 開發人員工具 — 開放原始碼工具、SDK和程式庫，讓開發人員可輕鬆建立自訂擴充功能和整合。 使用React Spectrum (Adobe的UI工具組)，讓所有Adobe應用程式擁有一個通用使用者介面。
* 服務 — I/O Runtime，用於在Adobe的無伺服器平台上託管基礎結構，以及I/O事件，用於事件式整合。 Adobe也提供開箱即用的資料與檔案儲存支援。
* Adobe Experience Cloud — 開發人員可以提交擴充功能和整合專案，以便在其Experience Cloud組織中發佈。系統管理員可以檢閱、管理和核准這些擴充功能。 發佈後，您的自訂App Builder擴充功能和工具可與其他Adobe Experience Cloud應用程式一併找到。

下圖說明在App Builder上建置的標準應用程式如何使用這些功能：

![架構](/help/implementing/developing/extending/assets/appbuilder-architecture.jpg)

如需App Builder架構的詳細資訊，請參閱 [架構概述](https://developer.adobe.com/app-builder/docs/guides/).

## 開始使用App Builder {#additional-resources}

已建立Adobe的快速入門檔案，以便您開始使用App Builder：

* [App Builder入門](https://developer.adobe.com/app-builder/docs/getting_started/)

## 繼續學習說明檔案 {#appbuilder-documentation}

App Builder為開發人員提供影片和檔案，包括指南，以及參考檔案，協助您開始開發自己的自訂應用程式：

* [App Builder檔案](https://developer.adobe.com/app-builder/docs/overview/)
* [App Builder影片](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o)

## 試用其中一個範例應用程式 {#appbuilder-codesamples}

準備好開始開發了嗎？ Adobe有許多範例應用程式，可幫助您快速上手：

* [Adobe Developer網站上的App Builder程式碼實驗室](https://developer.adobe.com/app-builder/docs/resources/)