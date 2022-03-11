---
title: 擴展 [!DNL Adobe Experience Manager] as a Cloud Service使用Adobe開發人員應用程式生成器。
description: 擴展 [!DNL Adobe Experience Manager] as a Cloud Service使用Adobe開發人員應用程式生成器。
exl-id: 50d82745-5deb-4bfa-961b-714842403601
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---

# 擴展 [!DNL Adobe Experience Manager] as a Cloud Service使用Adobe開發人員應用程式生成器 {#extend-using-app-builder}

## 什麼是App Builder for AEMas a Cloud Service {#project-firefly}

新的Adobe開發人員應用程式構建器為開發人員提供了擴展框架，以便輕鬆擴展AEMas a Cloud Service功能。

App Builder提供了統一的第三方擴展框架，用於整合和建立擴展Adobe Experience Manager的自定義體驗。 借助這一基於Adobe基礎架構的完整擴展框架，開發人員可以構建定製的微服務，跨Adobe解決方案和IT堆棧的其他部分擴展和整合Adobe Experience Manager。

App Builder為客戶提供了一種在各種使用情形中輕鬆擴展Adobe Experience Manager的方法：

* 中間件可擴充性 — 將外部系統與Adobe應用程式連接，構建定制連接器或利用一套預構建的整合。
* 核心服務可擴充性 — 通過使用自定義功能和業務邏輯擴展預設行為來擴展核心應用程式功能。
* 用戶體驗可擴充性 — 擴展核心體驗以支援業務需求或構建特定於客戶的數字屬性、店面和後台應用。

自2020年夏季以來，App Builder（以前稱為Project Firefly）已通過我們的Developer Preview提供給企業客戶和合作夥伴。 App Builder的正式上市定於2021年12月開始。 我們歡迎開發人員通過我們的 [試用計畫](http://adobe.ly/appbuilder-trial)。

>[!NOTE]
>
> 對於AEM希望利用App Builder的6.5客戶，請轉至 [使用Adobe開發人員應用程式生成器擴展Adobe Experience Manager6.5](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/app-builder.html)。

## 架構 {#architecture}

Adobe開發商App Builder不是現成解決方案，而是為擴展Adobe雲解決方案提供了一個通用、一致、標準化的開發平台，AEM包括：

* Adobe開發人員控制台 — 用於定制微服務和擴展開發，讓開發人員在訪問建立插件和整合所需的所有工具和API時構建和管理項目。
* 開發人員工具 — 開源工具、SDK和庫，使開發人員能夠輕鬆構建自定義擴展和整合。 使用React Spectrum(Adobe的UI工具包)為所有Adobe應用提供一個通用UI。
* 服務 — 用於在無伺服器平台上托管基礎架構的I/O運行時，以及用於基於事件的整合的I/O事件。 我們還為儲存和檔案提供現成支援。
* Adobe Experience Cloud — 開發人員可以提交擴展和整合，以在其Experience Cloud組織中發佈。然後，系統管理員可以審閱、管理和批准這些擴展。 發佈後，您的自定義App Builder擴展和工具可以與其他Adobe Experience Cloud應用一起找到。

下圖說明了在App Builder上構建的標準應用程式如何利用這些功能：

![架構](/help/implementing/developing/extending/assets/firefly-architecture.jpg)

有關App Builder體系結構的詳細資訊，請查看 [體系結構概述](https://www.adobe.io/app-builder/docs/guides/)。

## 開始使用App Builder {#additional-resources}

為幫助您開始使用App Builder，我們建立了一系列文檔來幫助您開始：

* [應用程式生成器入門](https://www.adobe.io/app-builder/docs/getting_started/)

## 繼續學習文檔 {#appbuilder-documentation}

App Builder為開發人員提供視頻和文檔，包括指南和參考文檔，幫助您開始開發自己的自定義應用程式：

* [App Builder文檔](https://www.adobe.io/app-builder/docs/overview/)
* [App Builder視頻](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o)

## 試用一個示例應用程式 {#appbuilder-codesamples}

準備開始發展了嗎？ 我們提供了大量示例應用程式，幫助您快速前進：

* [Adobe開發人員網站上的App Builder代碼實驗](https://www.adobe.io/app-builder/docs/resources/)

## 支援 {#support}

對於開發人員支援類型的請求，我們鼓勵開發人員使用 [Experience League論壇](https://experienceleaguecommunities.adobe.com/t5/project-firefly/ct-p/project-firefly)。
