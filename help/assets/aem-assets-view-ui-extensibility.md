---
title: AEM Assets檢視UI擴充性
description: 瞭解AEM Assets檢視的UI擴充功能。 AEM Assets檢視UI可讓您新增自訂UI元件，以符合特定的業務需求。
feature: App Builder
role: User, Developer
exl-id: a11f7043-17cf-4331-b76c-d3db099c2411
source-git-commit: e47a8fc65e58ae2ffff805966d7dae8c6edc7aac
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 3%

---

# AEM Assets檢視UI擴充性{#AEM-Assets-View-UI-Extensibility}

| [搜尋最佳實務](/help/assets/search-best-practices.md) | [中繼資料最佳實務](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [具有 OpenAPI 功能的 Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開發人員文件](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

AEM Assets檢視具有UI擴充功能。 此功能可讓使用者新增自訂UI元件至Assets檢視UI，以符合AEM Assets檢視現成功能無法滿足的特定業務需求。 此擴充功能增強了AEM Assets檢視的彈性，可讓組織根據特定工作流程和需求調整介面。
您可以將擴充功能新增至資產、資料夾和集合層級。 新增的擴充功能會顯示在資產、集合或資料夾詳細資訊頁面的專用面板中。

>[!IMPORTANT]
> [AEM Assets Ultimate](/help/assets/assets-ultimate-overview.md)提供Assets檢視UI擴充功能。

## <a id="1"></a>如何存取Assets檢視

以下列方式存取Assets檢視：
![access-assets-view-ui](/help/assets/assets/access-assets-view.jpg)

## UI擴充功能會在Assets檢視UI上的哪裡顯示？ {#ui-extensibility-panel-assets-view}

在Assets檢視中，導覽至資產、資料夾或集合的「詳細資訊」頁面。 此「詳細資訊」頁面有一個專用面板，可顯示新增的UI擴充功能。
![我的工作區](/help/assets/assets/my-workspace-assets-view3.png)

>[!NOTE]
>
> AEM Assets檢視UI擴充性可供Beta版本使用。 您可以展開「詳細意見回饋」選項並按一下「報告問題」，以提供檔案意見回饋。

## 新增擴充性元件的先決條件

* [存取Assets檢視](#1)。
* 存取[Assets Ultimate](/help/assets/assets-ultimate-overview.md)預設包含的[Adobe應用程式產生器](https://developer.adobe.com/app-builder/docs/overview/)。
* 有權取得組織內系統管理員開發人員的角色。 如需詳細資訊，請參閱[這個](https://developer.adobe.com/uix/docs/guides/get-access/)。
* AdobeIO命令列工具(AIO CLI)必須安裝在您的本機電腦上。 此工具對於建立和部署擴充功能專案至關重要。 如需詳細資訊，請參閱[這個](https://developer.adobe.com/app-builder/docs/getting_started/#local-environment-set-up)。
* 充分瞭解JavaScript、Node.js和React技術。

## 在Assets檢視UI上新增UI擴充性元件{#Adding-UI-Extensibility-Component-on-Assets-View}

1. 如需UI擴充功能和AdobeApp Builder架構的基本資訊，請參閱[快速入門](https://developer.adobe.com/uix/docs/getting-started/)。 瞭解UI擴充功能如何在Adobe Experience Cloud服務中整合自訂邏輯和UI，並瞭解實作UI擴充功能的架構和工作流程。
1. 如需UI擴充性的一般資訊，請參閱[指南](https://developer.adobe.com/uix/docs/guides/)，包括本機環境設定、本機預覽、發佈和管理。
1. 請參閱[建立擴充功能的常見概念](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/commons/)，瞭解為AEM Assets檢視開發UI擴充功能所需的基礎。
1. 新增自訂側面板至Assets檢視介面。 主機應用程式(Assets檢視)會管理這些面板，以處理UI互動，例如切換和深層連結。 擴充功能使用`aem/assets/details/1`擴充功能點來整合指定屬性的自訂面板，例如面板ID、標題及內容URL。 開發人員使用`getPanels()`方法註冊自訂面板，並建立顯示自訂內容的路由。 如需詳細實作，包括API參考和程式碼範例，請參閱[詳細資料檢視](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/details-view/)。
1. 設定您的本機環境，並透過建立您的第一個UI擴充功能，體驗在Assets檢視中開發UI擴充功能的程式。 如需詳細資訊，請參閱[逐步的AEM Assets檢視擴充功能開發](https://developer.adobe.com/uix/docs/services/aem-assets-view/extension-development/)。
1. 使用AIO CLI設定應用程式，以產生基本擴充功能結構和必要的程式碼。 如需詳細資訊，請參閱AEM Assets檢視的[程式碼產生](https://developer.adobe.com/uix/docs/services/aem-assets-view/code-generation/)。
1. 在本機測試您的擴充功能，確保它們在部署前可如預期般運作。 在完全隔離的環境中或以部分隔離的方式執行擴充功能，並將擴充功能連線至生產AEM Assets檢視進行測試。 如需詳細資訊，請參閱[疑難排解 — AEM Assets檢視擴充性](https://developer.adobe.com/uix/docs/services/aem-assets-view/debug/)。
