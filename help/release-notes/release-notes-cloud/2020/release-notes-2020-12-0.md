---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.12.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.12.0 版發行說明。'
exl-id: 16875180-1f23-477d-9d4d-e220998c4983
source-git-commit: f0e9fe0bdf35cc001860974be1fa2a7d90f7a3a9
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 16%

---

# [!DNL Adobe Experience Manager]as a Cloud Service 版發行說明 {#release-notes}

以下區段會概述以下專案的一般發行說明： [!DNL Experience Manager] as a Cloud Service。

## 發行日期 {#release-date}

的發行日期 [!DNL Adobe Experience Manager] as a Cloud Service2020.12.0為2020年12月17日。
下列版本(2021.1.0)將於2021年1月28日發行。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* **[內容片段HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)**：新增使用HTTP API新增/更新和刪除內容片段變體的功能。

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* 與整合 [!DNL Adobe InDesign Server] 現在已適用於 [!DNL Experience Manager] as a [!DNL Cloud Service]. 如此一來，流程便能自動化處理 [!DNL Adobe InDesign] 檔案使用 [!DNL Adobe InDesign Server] 指令碼並允許使用者使用 [!DNL Assets] 建立手冊或廣告的範本使用者介面。 僅限 [!DNL InDesign Server] 託管者 [!DNL Adobe Managed Services] 支援 [!DNL Experience Manager as a Cloud Service]. <!-- TBD: Add link to article. -->

* [!DNL Experience Manager] 增強功能，可在遠端使用資產時追蹤及顯示資產參考資料 [!DNL Experience Manager Sites] 使用「連線資產」功能部署。 新 [!UICONTROL 引用] 索引標籤在資產的 [!UICONTROL 屬性] 頁面現在會列出資產的本機與遠端參考。 參考資料可供DAM使用者追蹤中的資產使用情況 [!DNL Sites] 頁面和在中的複合資產 [!DNL Assets]. 另請參閱 [設定及使用「連線資產」](/help/assets/use-assets-across-connected-assets-instances.md).

* [!DNL Dynamic Media] 功能現在可透過 [!DNL Sites] 影像型核心元件。 作者可在建立網頁時快速設定元件，以使用影像預設集、智慧型裁切和影像修飾元。 另請參閱 [核心元件2.13.0版](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.13.0).

* [!DNL Experience Manager] 案頭應用程式可讓使用者從案頭應用程式介面上的Windows檔案總管或Mac Finder拖放檔案，即可上傳檔案和資料夾。 另請參閱 [使用案頭應用程式新增資產](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem).

## Adobe Experience Manager Commerceas a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 已發行CIF Venia Reference Site - 2020.12.01，其中包含最新CIF Core Components v1.6.0版。請參閱 [CIF Venia參考網站](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.12.01) 以取得更多詳細資料。

* 已發行CIF Core Components v1.6.0。請參閱 [CIF Core Components](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.6.0) 以取得更多詳細資料。

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

AEM as a Cloud Service 2020.12.0 中的 Cloud Manager 發行日期是 2020 年 12 月 10 日。

### [!DNL Cloud Manager]的新增功能 {#what-is-new-cm}

* 自助服務管理 [SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) 和 [自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/introduction.md).

* 自助服務管理 [IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).

* **環境**&#x200B;詳細資訊頁面更新完成，現在使用者可管理其環境的自訂網域名稱和 IP 允許清單。

### 錯誤修正 {#bug-fixes-cloud-manager}

* 在計劃碼掃描階段發生的某些故障，但未提供已處理的結果。

* 環境卡未一致顯示&#x200B;**新增**&#x200B;按鈕。

## 程式碼重構工具 {#code-refactoring-tools}

### [!DNL Code Refactoring Tools]的新增功能 {#what-is-new-crt}

* 新版AIO-CLI外掛程式已發行。 此外掛程式的最新版本包含AEM Dispatcher Converter和Repository Modernizer的錯誤修正，並支援新的公用程式Index Converter。 請參閱 [整合式體驗](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) 以進一步瞭解此外掛程式。

* Index Converter公用程式可將客戶的自訂OAK索引定義轉換為與AEMas a Cloud Service相容的OAK索引定義。 請參閱 [索引轉換器](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter) 以取得更多詳細資料。

* 新增功能至 [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) 會建立個別的封裝 `ui.config` 以包含所有OSGi設定。

### 錯誤修正 {#crt-bug-fixes}

* 對AEM Dispatcher Converter和Repository Modernizer工具進行的多項錯誤修正。 請參閱 [AEM Dispatcher轉換工具](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) 和 [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer).

### 發行日期 {#release-date-ctt}

內容轉移工具v1.1.20的發行日期為2021年1月8日。

### [!DNL Content Transfer Tool]的新增功能 {#what-is-new-ctt}

* 使用者現在可以透過將滑鼠游標停留在內容轉移工具(CTT)使用者介面的狀態圖示上來瞭解其存取Token是否已過期。 移轉集詳細資訊UI也會通知他們，他們無法連線到其Cloud Service執行個體。

### 錯誤修正 {#ctt-bug-fixes}

* 移轉集的內容轉移工具(CTT)使用者介面狀態在一段閒置時間後沒有持續存在且已變更。 此問題已修正。
* 如果記錄無法使用，則會停用檢視記錄的選項。 此問題已修正，且已新增傳訊功能，以通知使用者日誌遺失的原因。
* 內容轉移工具使用者介面狀態已顯示 *失敗* 使用者停止內嵌時。 此問題已修正為顯示 *已停止* 而非。
