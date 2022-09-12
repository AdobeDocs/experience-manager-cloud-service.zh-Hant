---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.12.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.12.0 版發行說明。'
exl-id: 16875180-1f23-477d-9d4d-e220998c4983
source-git-commit: aeee895e4a4b959125d08091619988d0ffa09ace
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 8%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 版發行說明  {#release-notes}

以下章節概述的一般發行說明 [!DNL Experience Manager] as a Cloud Service。

## 發行日期 {#release-date}

的發行日期 [!DNL Adobe Experience Manager] as a Cloud Service的2020.12.0是2020年12月17日。
下列版本(2021.1.0)將於2021年1月28日發行。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* **[內容片段HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)**:新增使用HTTP API新增/更新及刪除內容片段變體的功能。

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* 與整合 [!DNL Adobe InDesign Server] 現在可供 [!DNL Experience Manager] as a [!DNL Cloud Service]. 它提供流程自動化 [!DNL Adobe InDesign] 檔案使用 [!DNL Adobe InDesign Server] 指令碼，讓使用者使用 [!DNL Assets] 範本使用者介面以製作手冊或廣告。 僅 [!DNL InDesign Server] 由 [!DNL Adobe Managed Services] 支援 [!DNL Experience Manager as a Cloud Service]. <!-- TBD: Add link to article. -->

* [!DNL Experience Manager] 已增強為當資產用於遠端時，可追蹤及顯示資產參考 [!DNL Experience Manager Sites] 使用連線資產功能進行部署。 新 [!UICONTROL 參考] 標籤 [!UICONTROL 屬性] 頁面現在會列出資產的本機和遠端參考。 參考資料可讓DAM使用者追蹤 [!DNL Sites] 頁面和複合資產中 [!DNL Assets]. 請參閱 [設定及使用連線資產](/help/assets/use-assets-across-connected-assets-instances.md).

* [!DNL Dynamic Media] 功能現在可透過 [!DNL Sites] 影像型核心元件。 作者可在建立網頁時快速設定元件，以使用影像預設集、智慧型裁切和影像修飾元。 請參閱 [核心元件2.13.0版](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.13.0).

* [!DNL Experience Manager] 案頭應用程式可讓使用者在案頭應用程式介面上，從Windows檔案總管或Mac Finder拖曳檔案，以上傳檔案和資料夾。 請參閱 [使用案頭應用程式新增資產](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem).

## Adobe Experience Manager商務as a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* CIF Venia Reference Site - 2020.12.01已發佈，其中包含最新CIF核心元件1.6.0版。請參閱 [CIF Venia參考站](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.12.01) 以取得更多詳細資訊。

* CIF核心元件1.6.0版已發行。請參閱 [CIF核心元件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.6.0) 以取得更多詳細資訊。

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

AEMas a Cloud Service的Cloud Manager發行日期2020.12.0為2020年12月10日。

### [!DNL Cloud Manager]的新增功能 {#what-is-new-cm}

* 自助管理 [SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) 和 [自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/introduction.md).

* 自助管理 [IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).

* 已更新 **環境** 「詳細資訊」頁面現在可讓使用者管理其環境的自訂網域名稱和IP允許清單。

### 錯誤修正 {#bug-fixes-cloud-manager}

* 在代碼掃描階段發生的某些故障，但未提供已處理的結果。

* 環境卡未一致顯示 **新增** 按鈕。

## 程式碼重構工具 {#code-refactoring-tools}

### [!DNL Code Refactoring Tools]的新增功能 {#what-is-new-crt}

* 新版AIO-CLI增效模組已發行。 此外掛程式的最新版本修正了AEM Dispatcher Converter和Repository Modernizer的錯誤，也支援新的公用程式Index Converter。 請參閱 [統一體驗](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) 以深入了解此外掛程式。

* Index Converter公用程式可將客戶的自訂OAK索引定義轉換為AEMas a Cloud Service相容的OAK索引定義。 請參閱 [索引轉換器](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter) 以取得更多詳細資訊。

* 新增功能至 [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) 建立獨立包 `ui.config` 以包含所有OSGi設定。

### 錯誤修正 {#crt-bug-fixes}

* AEM Dispatcher轉換工具和Repository Modernizer工具上已完成數項錯誤修正。 請參閱 [AEM Dispatcher轉換工具](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) 和 [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer).

### 發行日期 {#release-date-ctt}

內容轉移工具1.1.20版的發行日期為2021年1月8日。

### [!DNL Content Transfer Tool]的新增功能 {#what-is-new-ctt}

* 使用者現在可以透過將游標移至內容轉移工具(CTT)使用者介面中的狀態圖示，了解其存取權杖是否已過期。 移轉集詳細資料UI中也會通知他們無法連線至其Cloud Service執行個體。

### 錯誤修正 {#ctt-bug-fixes}

* 移轉集的「內容轉移工具」(CTT)使用者介面狀態在閒置一段時間後並未持續存在且變更。 此問題已修正。
* 如果日誌不可用，則禁用查看日誌的選項。 此問題已修正，且已新增傳訊功能，以通知使用者記錄遺失的原因。
* 內容轉移工具使用者介面狀態顯示 *失敗* 使用者停止擷取時。 此問題已修正為顯示 *已停止* 。
