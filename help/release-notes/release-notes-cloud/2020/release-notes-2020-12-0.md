---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.12.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.12.0 版發行說明。'
exl-id: 16875180-1f23-477d-9d4d-e220998c4983
feature: Release Information
role: Admin
source-git-commit: 64344b9b2cce8d7c7f05d3e5ba94049346308a9d
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 8%

---

# [!DNL Adobe Experience Manager]as a Cloud Service的發行說明 {#release-notes}

以下章節概述[!DNL Experience Manager]as a Cloud Service的一般發行說明。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager]as a Cloud Service2020.12.0版的發行日期為2020年12月17日。
下列版本(2021.1.0)為2021年1月28日。

## [!DNL Adobe Experience Manager Sites]個as a Cloud Service {#sites}

* **[內容片段HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)**：新增使用HTTP API新增/更新及刪除內容片段變體的功能。

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* [!DNL Experience Manager]現在可作為[!DNL Cloud Service]與[!DNL Adobe InDesign Server]整合。 它提供使用[!DNL Adobe InDesign Server]指令碼處理[!DNL Adobe InDesign]檔案的自動化功能，並可讓使用者使用[!DNL Assets]範本使用者介面來建立手冊或廣告。 [!DNL Experience Manager as a Cloud Service]只支援[!DNL Adobe Managed Services]代管的[!DNL InDesign Server]。<!-- TBD: Add link to article. -->

* [!DNL Experience Manager]已獲得改善，現在使用「連線的Assets」功能在遠端[!DNL Experience Manager Sites]部署中使用資產時，可以追蹤及顯示資產參考。 資產[!UICONTROL 屬性]頁面中的新[!UICONTROL 參考]索引標籤現在會列出資產的本機和遠端參考。 參考資料可讓DAM使用者追蹤[!DNL Sites]頁面中的資產使用情況和[!DNL Assets]中的複合資產。 請參閱[設定及使用連線的Assets](/help/assets/use-assets-across-connected-assets-instances.md)。

* [!DNL Dynamic Media]功能現在可透過AEM [!DNL Sites]影像型核心元件存取。 作者可在建立網頁時快速設定元件，以使用影像預設集、智慧型裁切和影像修飾元。 請參閱[核心元件2.13.0版本](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.13.0)。

* [!DNL Experience Manager]案頭應用程式可讓使用者在案頭應用程式介面上，從Windows檔案總管或Mac Finder拖曳檔案，以上傳檔案和資料夾。 請參閱[使用案頭應用程式](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-desktop-app/using/using#upload-and-add-new-assets-to-aem)新增資產。

## Adobe Experience Manager Commerceas a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 已發行CIF Venia參考網站 — 2020.12.01，其中包含最新CIF核心元件1.6.0版。如需詳細資訊，請參閱[CIF Venia參考網站](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.12.01)。

* 已發行CIF Core Components v1.6.0。如需詳細資訊，請參閱[CIF核心元件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.6.0)。

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

Adobe Experience Manager (AEM) as a Cloud Service 2020.12.0中的Cloud Manager發行日期是2020年12月10日。

### [!DNL Cloud Manager] 的新增功能 {#what-is-new-cm}

* 自助管理[SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md)和[自訂網域名稱簡介](/help/implementing/cloud-manager/custom-domain-names/introduction.md)。

* 自助管理 [IP 允許清單](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)。

* 更新的&#x200B;**環境**&#x200B;詳細資訊頁面現在可讓使用者管理其環境的自訂網域名稱和IP允許清單。

### 錯誤修正 {#bug-fixes-cloud-manager}

* 解決在計畫碼掃描階段發生的某些失敗但未提供結果。

* 環境卡未一致顯示&#x200B;**新增**&#x200B;按鈕。

## 程式碼重構工具 {#code-refactoring-tools}

### [!DNL Code Refactoring Tools] 的新增功能 {#what-is-new-crt}

* 新版AIO-CLI外掛程式已發行。 此增效模組的最新版本修正AEM Dispatcher Converter和Repository Modernizer的錯誤，並支援全新公用程式Index Converter。 請參閱[Unified Experience](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/unified-experience#benefits)，您可以在此瞭解更多關於此外掛程式的資訊。

* Index Converter公用程式可將客戶的自訂Oak索引定義轉換成與AEM as a Cloud Service相容的Oak索引定義。 如需詳細資訊，請參閱[索引轉換器](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)。

* 新增功能至[Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)，可建立個別封裝`ui.config`以包含所有OSGi設定。

### 錯誤修正 {#crt-bug-fixes}

* AEM Dispatcher Converter和Repository Modernizer工具已進行數個錯誤修正。 請參閱[AEM Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)和[Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)。

### 發行日期 {#release-date-ctt}

「內容轉移工具v1.1.20」的發行日期為2021年1月8日。

### [!DNL Content Transfer Tool] 的新增功能 {#what-is-new-ctt}

* 使用者現在可以透過將游標移至內容轉移工具(CTT)使用者介面的狀態圖示上，瞭解其存取Token是否已過期。 移轉集詳細資訊UI也會通知他們，他們無法連線到其Cloud Service執行個體。

### 錯誤修正 {#ctt-bug-fixes}

* 移轉集的內容轉移工具(CTT)使用者介面狀態在一段閒置時間後沒有持續存在且已變更。 此問題現已修正。
* 如果日誌無法使用，則會停用檢視日誌的選項。 此問題現在已修正，且訊息現在已新增，以通知使用者缺少記錄的原因。
* 當使用者停止內嵌時，內容轉移工具使用者介面狀態顯示&#x200B;*失敗*。 此問題現在已修正，改為顯示&#x200B;*已停止*。
