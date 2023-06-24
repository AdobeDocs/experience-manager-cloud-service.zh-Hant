---
title: 延伸 [!DNL Adobe Experience Manager] 使用Adobe Developer App Builderas a Cloud Service。
description: 延伸 [!DNL Adobe Experience Manager] 使用Adobe Developer App Builderas a Cloud Service。
exl-id: 50d82745-5deb-4bfa-961b-714842403601
source-git-commit: 7260649eaab303ba5bab55ccbe02395dc8159949
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---

# 延伸 [!DNL Adobe Experience Manager] as a Cloud Service使用Adobe Developer App Builder {#extend-using-app-builder}

## 什麼是App Builder for AEMas a Cloud Service {#project-appbuilder}

新的Adobe Developer App Builder為開發人員提供擴充性架構，以便輕鬆擴充AEMas a Cloud Service的功能。

App Builder提供統一的第三方擴充功能架構，可整合及建立可擴充Adobe Experience Manager的自訂體驗。 透過這個以Adobe基礎架構為基礎的完整擴充性架構，開發人員可以建立自訂微服務、擴充及整合跨Adobe解決方案和IT棧疊其他部分的Adobe Experience Manager。

App Builder讓客戶能在各種使用案例中輕鬆擴充Adobe Experience Manager：

* 中介軟體擴充性 — 將外部系統與建置自訂聯結器的Adobe應用程式連線，或使用預先建立的整合套件。
* 核心服務擴充性 — 透過自訂功能和商業邏輯擴充預設行為，進而擴充核心應用程式功能。
* 使用者體驗擴充性 — 擴充核心體驗以支援業務需求，或建立客戶專屬的數位財產、店面和後台應用程式。

自2020年夏季起，企業客戶和合作夥伴即可透過Adobe的「開發人員預覽」功能使用App Builder。 App Builder正式發行(GA)日期排定於2021年12月。 Adobe歡迎開發人員透過以下路徑試用應用程式產生器： [試用方案](https://developer.adobe.com/app-builder/trial/).

>[!NOTE]
>
> 若要瞭解想要使用App Builder的AEM 6.5客戶，請參閱 [使用Adobe Developer App Builder延伸Adobe Experience Manager 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/app-builder.html).

## 架構 {#architecture}

Adobe Developer App Builder不是現成可用的解決方案，而是提供通用、一致、標準化的開發平台，用於擴充Adobe雲端解決方案(例如AEM)，包括：

* Adobe Developer Console — 用於自訂微服務和擴充功能開發，可讓開發人員在存取所有所需工具和API時建置和管理專案，以便建立外掛程式和整合。
* 開發人員工具 — 開放原始碼工具、SDK和程式庫，讓開發人員可輕鬆建立自訂擴充功能和整合。 使用React Spectrum (Adobe的UI工具組)，讓所有Adobe應用程式擁有一個通用的使用者介面。
* 服務 — 在Adobe的無伺服器平台上託管基礎結構的I/O執行階段，以及事件式整合的I/O事件。 Adobe也提供儲存資料和檔案的立即可用支援。
* Adobe Experience Cloud — 開發人員可以提交擴充功能和整合內容，以便在其Experience Cloud組織中發佈。接著，系統管理員可以檢閱、管理和核准這些擴充功能。 發佈後，您的自訂App Builder擴充功能和工具可與其他Adobe Experience Cloud應用程式一併找到。

下圖說明在App Builder上建置的標準應用程式如何使用這些功能：

![架構](/help/implementing/developing/extending/assets/appbuilder-architecture.jpg)

如需App Builder架構的詳細資訊，請參閱 [架構概述](https://developer.adobe.com/app-builder/docs/guides/).

## 開始使用App Builder {#additional-resources}

已建立Adobe的快速入門檔案，讓您能夠開始使用App Builder：

* [App Builder入門](https://developer.adobe.com/app-builder/docs/getting_started/)

## 繼續學習使用檔案 {#appbuilder-documentation}

App Builder為開發人員提供影片和檔案，包括指南，以及參考檔案，以協助您開始開發自己的自訂應用程式：

* [App Builder檔案](https://developer.adobe.com/app-builder/docs/overview/)
* [App Builder影片](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o)

## 嘗試其中一個範例應用程式 {#appbuilder-codesamples}

準備好開始開發了嗎？ Adobe有許多範例應用程式可協助您快速上手：

* [Adobe Developer網站上的App Builder程式碼實驗室](https://developer.adobe.com/app-builder/docs/resources/)