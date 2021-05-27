---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.12.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.12.0 版發行說明。'
exl-id: 16875180-1f23-477d-9d4d-e220998c4983
source-git-commit: aeee895e4a4b959125d08091619988d0ffa09ace
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 6%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 版發行說明 {#release-notes}

以下章節概述[!DNL Experience Manager]作為Cloud Service的一般發行說明。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager]作為Cloud Service2020.12.0的發行日期為2020年12月17日。
下列版本(2021.1.0)將於2021年1月28日發行。

## [!DNL Adobe Experience Manager Sites] 作為Cloud Service {#sites}

* **[內容片段HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)**:新增使用HTTP API新增/更新及刪除內容片段變體的功能。

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* 與[!DNL Adobe InDesign Server]的整合現在可作為[!DNL Cloud Service]用於[!DNL Experience Manager]。 它提供使用[!DNL Adobe InDesign Server]指令碼處理[!DNL Adobe InDesign]檔案的自動化，並允許用戶使用[!DNL Assets]模板用戶介面來製作手冊或廣告。 [!DNL Experience Manager as a Cloud Service]僅支援由[!DNL Adobe Managed Services]托管的[!DNL InDesign Server]。 <!-- TBD: Add link to article. -->

* [!DNL Experience Manager] 已獲得增強，現在使用「連線資產」功能在遠端部署中使用資產時，可 [!DNL Experience Manager Sites] 以追蹤及顯示資產參考。資產的[!UICONTROL 屬性]頁面中新的[!UICONTROL 參考]標籤現在會列出資產的本機和遠端參考。 參考資料可讓DAM使用者追蹤[!DNL Sites]頁面中的資產使用情況和[!DNL Assets]中的複合資產。 請參閱[設定及使用連線資產](/help/assets/use-assets-across-connected-assets-instances.md)。

* [!DNL Dynamic Media] 現在可透過影像 [!DNL Sites] 型核心元件存取功能。作者可在建立網頁時快速設定元件，以使用影像預設集、智慧型裁切和影像修飾元。 請參閱[核心元件2.13.0版](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.13.0)。

* [!DNL Experience Manager] 案頭應用程式可讓使用者在案頭應用程式介面上，從Windows檔案總管或Mac Finder拖曳檔案，以上傳檔案和資料夾。請參閱[使用案頭應用程式新增資產](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem)。

## Adobe Experience Manager Commerce as aCloud Service{#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* CIF Venia Reference Site - 2020.12.01版已發行，其中包含最新CIF核心元件1.6.0版。如需詳細資訊，請參閱[CIF Venia Reference Site](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.12.01)。

* CIF核心元件v1.6.0已發行。如需詳細資訊，請參閱[CIF核心元件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.6.0) 。

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

AEM as aCloud Service中的Cloud Manager 2020.12.0的發行日期為2020年12月10日。

### [!DNL Cloud Manager] {#what-is-new-cm}中的新增功能

* 自助管理[SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)和[自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/introduction.md)。

* [IP允許清單的自助管理](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)。

* 更新&#x200B;**環境**&#x200B;詳細資訊頁面現在可讓使用者管理其環境的自訂網域名稱和IP允許清單。

### 錯誤修正 {#bug-fixes-cloud-manager}

* 在代碼掃描階段發生的某些故障，但未提供已處理的結果。

* 環境卡未一致地顯示&#x200B;**Add**&#x200B;按鈕。

## 程式碼重構工具 {#code-refactoring-tools}

### [!DNL Code Refactoring Tools] {#what-is-new-crt}中的新增功能

* 新版AIO-CLI增效模組已發行。 此外掛程式的最新版本修正了AEM Dispatcher Converter和Repository Modernizer的錯誤，也支援新的公用程式Index Converter。 請參閱[Unified Experience](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits)以深入了解此外掛程式。

* Index Converter公用程式可將客戶的自訂OAK索引定義轉換為AEM，作為相容Cloud Service的OAK索引定義。 有關詳細資訊，請參閱[Index Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)。

* 新增至[Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)的新功能，可建立獨立的套件`ui.config`以包含所有OSGi設定。

### 錯誤修正 {#crt-bug-fixes}

* AEM Dispatcher轉換工具和Repository Modernizer工具上已完成數項錯誤修正。 請參閱[AEM Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)和[Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)。

### 發行日期 {#release-date-ctt}

內容轉移工具1.1.20版的發行日期為2021年1月8日。

### [!DNL Content Transfer Tool] {#what-is-new-ctt}中的新增功能

* 使用者現在可以透過將游標移至內容轉移工具(CTT)使用者介面中的狀態圖示，了解其存取權杖是否已過期。 移轉集詳細資料UI中也會通知他們無法連線至其Cloud Service執行個體。

### 錯誤修正 {#ctt-bug-fixes}

* 移轉集的「內容轉移工具」(CTT)使用者介面狀態在閒置一段時間後並未持續存在且變更。 此問題已修正。
* 如果日誌不可用，則禁用查看日誌的選項。 此問題已修正，且已新增傳訊功能，以通知使用者記錄遺失的原因。
* 當使用者停止擷取時，「內容轉移工具」使用者介面狀態顯示&#x200B;*FAILED*。 此問題已修正，改為顯示&#x200B;*STOPPED*。
