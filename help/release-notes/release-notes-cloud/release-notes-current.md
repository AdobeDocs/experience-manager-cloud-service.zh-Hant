---
title: ' [!DNL Adobe Experience Manager] 做為雲端服務的最新發行說明。'
description: ' [!DNL Adobe Experience Manager] 做為雲端服務的最新發行說明。'
translation-type: tm+mt
source-git-commit: 76da904f4fc5a96e6892242c42bae5d05eea2e16
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 4%

---


# [!DNL Adobe Experience Manager] as a Cloud Service 版發行說明 {#release-notes}

以下章節概述[!DNL Experience Manager]做為雲端服務的一般發行說明。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager]作為雲服務2020.12.0的發行日期為2020年12月17日。
下列版本(2021.1.0)將於2021年1月28日發行。

## [!DNL Adobe Experience Manager Sites] 雲端服務  {#sites}

* **[內容片段HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)**:新增使用HTTP API新增／更新和刪除內容片段變數的能力。

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* 與[!DNL Adobe InDesign Server]的整合現在適用於[!DNL Experience Manager]作為[!DNL Cloud Service]。 它提供使用[!DNL Adobe InDesign Server]指令碼處理[!DNL Adobe InDesign]檔案的自動功能，並讓使用者使用[!DNL Assets]範本使用者介面來建立手冊或廣告。 [!DNL Experience Manager as a Cloud Service]僅支援[!DNL Adobe Managed Services]代管的[!DNL InDesign Server]。<!-- TBD: Add link to article. -->

* [!DNL Experience Manager] 已增強，當資產使用連線資產功能用於遠端部署時，可追 [!DNL Experience Manager Sites] 蹤及顯示資產參考。資產的[!UICONTROL 屬性]頁面中新的[!UICONTROL 參考]標籤現在會列出資產的本機和遠端參考。 參考可讓DAM使用者追蹤[!DNL Sites]頁面中的資產使用情況，以及[!DNL Assets]中的複合資產。 請參閱[設定及使用連線資產](/help/assets/use-assets-across-connected-assets-instances.md)。

* [!DNL Dynamic Media] 功能現在可透過影 [!DNL Sites] 像型核心元件存取。作者可以在建立網頁時快速設定元件，使用影像預設集、智慧型裁切和影像修飾元。 請參閱[核心元件2.13.0版](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.13.0)。

* [!DNL Experience Manager] 案頭應用程式可讓使用者從案頭應用程式介面的Windows檔案總管或Mac Finder拖曳檔案，以上傳檔案和檔案夾。請參閱「使用案頭應用程式新增資產」。[](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 發佈的CIF Venia參考網站- 2020.12.01，其中包含最新的CIF核心元件v1.6.0版。如需詳細資訊，請參閱[CIF Venia參考網站](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.12.01)。

* 已發佈CIF核心元件v1.6.0。有關詳細資訊，請參閱[CIF核心元件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.6.0)。

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

AEM中Cloud Manager作為Cloud Service 2021.1.0的發行日期為2021年1月14日。

### 錯誤修正 {#bug-fixes-cloud-manager}

* 資產生產實例有時可能會將&#x200B;**環境**&#x200B;詳細資訊頁面上的品牌入口網站狀態顯示為&#x200B;*待定*，而不允許使用者採取任何動作。

* 從Cloud Manager觸發解除休眠時，有時即使成功啟動解除休眠，仍會顯示失敗訊息。

* 已解決在環境建立或刪除中遇到的罕見故障。

## 程式碼重構工具 {#code-refactoring-tools}

### [!DNL Code Refactoring Tools] {#what-is-new-crt}的新增功能

* 新版AIO-CLI增效模組已發行。 此外掛程式的最新版本包含AEM Dispatcher Converter和Repository Modernizer的錯誤修正，也支援新的公用程式- Index Converter。 請參閱[Unified Experience](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits)以進一步瞭解此外掛程式。

* Index Converter是一個公用程式，可用來將客戶的自訂OAK索引定義轉換為AEM，做為CLoud Service相容的OAK索引定義。 有關詳細資訊，請參閱[索引轉換器](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)。

* 新增至[Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)的新功能，可建立個別的套件`ui.config`以包含所有OSGi組態。

### 錯誤修正 {#crt-bug-fixes}

* 在AEM Dispatcher Converter和Repository Modernizer工具上完成數個錯誤修正。 請參閱[AEM Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)和[Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)。

## 雲端轉換工具 {#code-transition-tools}

### 發行日期 {#release-date-ctt}

內容傳輸工具v1.2.2的發行日期為2021年2月1日。

### [!DNL Content Transfer Tool] {#what-is-new-ctt}的新增功能

* 內容傳輸工具——使用者對應工具新增功能和UI。 這項功能會自動將現有的使用者和群組對應至其Adobe Identity Management System ID，做為內容移轉活動的一部分。 如需詳細資訊，請參閱[使用使用者對應工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html)。
* 內容傳輸工具現在會移轉移移集（包括子系）中參考的所有群組和使用者。
* 在建立遷移集時，允許用戶選擇`/etc`下的某些路徑。
