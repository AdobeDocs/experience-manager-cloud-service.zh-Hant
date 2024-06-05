---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.12.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.12.0 版發行說明。'
exl-id: 16875180-1f23-477d-9d4d-e220998c4983
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 10%

---

# 版本注意事項 [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

以下區段會概述以下的一般發行說明： [!DNL Experience Manager] as a Cloud Service。

## 發行日期 {#release-date}

的發行日期 [!DNL Adobe Experience Manager] as a Cloud Service2020.12.0版本為2020年12月17日。
下列版本(2021.1.0)為2021年1月28日。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* **[內容片段HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)**：新增使用HTTP API新增/更新及刪除內容片段變體的功能。

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* 與整合 [!DNL Adobe InDesign Server] 現在可用於 [!DNL Experience Manager] as a [!DNL Cloud Service]. 如此一來，處理流程便能自動化執行 [!DNL Adobe InDesign] 檔案使用 [!DNL Adobe InDesign Server] 指令碼及允許使用者使用 [!DNL Assets] 範本使用者介面以建立手冊或廣告。 僅限 [!DNL InDesign Server] 託管者 [!DNL Adobe Managed Services] 支援 [!DNL Experience Manager as a Cloud Service]. <!-- TBD: Add link to article. -->

* [!DNL Experience Manager] 增強功能，當遠端使用資產時，可追蹤及顯示資產參考資料 [!DNL Experience Manager Sites] 使用「連線資產」功能部署。 新 [!UICONTROL 引用] 索引標籤作為資產的 [!UICONTROL 屬性] 頁面現在會列出資產的本機與遠端參考。 參考資料可供DAM使用者追蹤中的資產使用情況 [!DNL Sites] 頁面和在中的複合資產 [!DNL Assets]. 另請參閱 [設定及使用「連線資產」](/help/assets/use-assets-across-connected-assets-instances.md).

* [!DNL Dynamic Media] 功能現在可透過AEM存取 [!DNL Sites] 影像型核心元件。 作者可在建立網頁時快速設定元件，以使用影像預設集、智慧型裁切和影像修飾元。 另請參閱 [核心元件2.13.0版](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.13.0).

* 此 [!DNL Experience Manager] 案頭應用程式可讓使用者在案頭應用程式介面上，從Windows檔案總管或Mac Finder拖放檔案，輕鬆上傳檔案和資料夾。 另請參閱 [使用案頭應用程式新增資產](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem).

## Adobe Experience Manager Commerceas a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 已發行CIF Venia參考網站 — 2020.12.01，其中包含最新CIF核心元件1.6.0版。另請參閱 [CIF Venia參考網站](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.12.01) 以取得更多詳細資料。

* 已發行CIF Core Components v1.6.0。另請參閱 [CIF Core Components](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.6.0) 以取得更多詳細資料。

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

Adobe Experience Manager (AEM) as a Cloud Service2020.12.0中的Cloud Manager發行日期是2020年12月10日。

### [!DNL Cloud Manager] 的新增功能 {#what-is-new-cm}

* 自助管理 [SSL 憑證](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)和[自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/introduction.md)。

* 自助管理 [IP 允許清單](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)。

* 更新的 **環境** 詳細資訊頁面現在可讓使用者管理其環境的自訂網域名稱和IP允許清單。

### 錯誤修正 {#bug-fixes-cloud-manager}

* 解決在計畫碼掃描階段發生的某些失敗但未提供結果。

* 環境卡未一致顯示 **新增** 按鈕。

## 程式碼重構工具 {#code-refactoring-tools}

### [!DNL Code Refactoring Tools] 的新增功能 {#what-is-new-crt}

* 新版AIO-CLI外掛程式已發行。 此增效模組的最新版本修正AEM Dispatcher Converter和Repository Modernizer的錯誤，並支援全新公用程式Index Converter。 另請參閱 [Unified Experience](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/unified-experience.html#benefits) 您可在其中進一步瞭解此外掛程式。

* Index Converter公用程式可將客戶的自訂Oak索引定義轉換成與AEMas a Cloud Service相容的Oak索引定義。 另請參閱 [索引轉換器](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter) 以取得更多詳細資料。

* 新增功能至 [存放庫現代化工具](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) 建立另一個封裝 `ui.config` 以包含所有OSGi設定。

### 錯誤修正 {#crt-bug-fixes}

* 對AEM Dispatcher Converter和Repository Modernizer工具進行了一些錯誤修正。 另請參閱 [AEM Dispatcher轉換工具](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) 和 [存放庫現代化工具](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer).

### 發行日期 {#release-date-ctt}

「內容轉移工具v1.1.20」的發行日期為2021年1月8日。

### [!DNL Content Transfer Tool] 的新增功能 {#what-is-new-ctt}

* 使用者現在可以透過將游標移至內容轉移工具(CTT)使用者介面的狀態圖示上，瞭解其存取Token是否已過期。 移轉集詳細資訊UI也會通知他們，他們無法連線到其Cloud Service執行個體。

### 錯誤修正 {#ctt-bug-fixes}

* 移轉集的內容轉移工具(CTT)使用者介面狀態在一段閒置時間後沒有持續存在且已變更。 此問題已修正。
* 如果日誌無法使用，則會停用檢視日誌的選項。 此問題已修正，且已新增傳訊功能，以通知使用者日誌遺失的原因。
* 內容轉移工具使用者介面狀態已顯示 *失敗* 當使用者停止內嵌時。 此問題已修正為顯示 *已停止* 而非。
