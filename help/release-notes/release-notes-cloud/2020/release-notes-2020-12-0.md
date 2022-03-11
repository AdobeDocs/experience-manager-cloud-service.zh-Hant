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

以下部分概述了有關 [!DNL Experience Manager] as a Cloud Service。

## 發行日期 {#release-date}

發放日期 [!DNL Adobe Experience Manager] as a Cloud Service2020.12.0是2020年12月17日。
以下版本(2021.1.0)將於2021年1月28日發佈。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* **[內容片段HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)**:添加使用HTTP API添加/更新和刪除內容片段變體的功能。

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* 與 [!DNL Adobe InDesign Server] 現在可供使用 [!DNL Experience Manager] 作為 [!DNL Cloud Service]。 它為流程提供自動化 [!DNL Adobe InDesign] 檔案使用 [!DNL Adobe InDesign Server] 指令碼編寫和允許用戶使用 [!DNL Assets] 模板用戶介面以建立手冊或廣告。 僅 [!DNL InDesign Server] 托管 [!DNL Adobe Managed Services] 支援 [!DNL Experience Manager as a Cloud Service]。 <!-- TBD: Add link to article. -->

* [!DNL Experience Manager] 在遠程中使用資產時，將增強以跟蹤和顯示資產引用 [!DNL Experience Manager Sites] 部署。 新 [!UICONTROL 引用] 頁籤 [!UICONTROL 屬性] 頁面現在列出資產的本地和遠程引用。 這些引用使DAM用戶能夠跟蹤 [!DNL Sites] 頁面和複合資產 [!DNL Assets]。 請參閱 [配置和使用連接的資產](/help/assets/use-assets-across-connected-assets-instances.md)。

* [!DNL Dynamic Media] 現在可通過 [!DNL Sites] 基於影像的核心元件。 作者可以在建立網頁時快速配置元件以使用「影像預設」、「智慧裁剪」和「影像修飾符」。 請參閱 [核心元件2.13.0版](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.13.0)。

* [!DNL Experience Manager] 案頭應用允許用戶通過從案頭應用介面上的Windows資源管理器或Mac查找器拖動檔案來上載檔案和資料夾。 請參閱 [使用案頭應用程式添加資產](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem)。

## Adobe Experience Manager商業as a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 已發佈CIF Venia參考站點 — 2020.12.01，包括最新的CIF核心元件版本v1.6.0。請參閱 [CIF Venia參考站點](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.12.01) 的子菜單。

* 已發佈CIF核心元件v1.6.0。請參閱 [CIF核心元件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.6.0) 的子菜單。

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

as a Cloud Service中的Cloud Manager的發AEM布日期為2020年12月10日。

### [!DNL Cloud Manager]的新增功能 {#what-is-new-cm}

* 自助管理 [SSL證書](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) 和 [自定義域名](/help/implementing/cloud-manager/custom-domain-names/introduction.md)。

* 自助管理 [IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)。

* 已更新 **環境** 「詳細資訊」頁允許用戶管理其環境中的自定義域名和IP允許清單。

### 錯誤修正 {#bug-fixes-cloud-manager}

* 在代碼掃描階段出現一些故障，但未提供解決結果。

* 環境卡顯示不一致 **添加** 按鈕

## 程式碼重構工具 {#code-refactoring-tools}

### [!DNL Code Refactoring Tools]的新增功能 {#what-is-new-crt}

* 已發佈新版本的AIO-CLI插件。 此插件的最新版本包括Dispatcher Converter和Repository Modernizer的AEM錯誤修復程式，並且還支援新的實用程式 — 索引轉換器。 請參閱 [統一體驗](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) 瞭解有關此插件的詳細資訊。

* 索引轉換器是一種實用程式，可用於將客戶的自定義OAK索引定義轉換為AEMas a Cloud Service相容的OAK索引定義。 請參閱 [索引轉換器](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter) 的子菜單。

* 添加到的新功能 [儲存庫現代化器](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) 建立單獨的包 `ui.config` 包含所有OSGi配置。

### 錯誤修正 {#crt-bug-fixes}

* 在Dispatcher Converter和Repository Modernizer工具上執AEM行了幾個錯誤修復。 請參閱 [調度AEM器轉換器](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) 和 [儲存庫現代化器](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)。

### 發行日期 {#release-date-ctt}

內容傳輸工具v1.1.20的發佈日期為2021年1月8日。

### [!DNL Content Transfer Tool]的新增功能 {#what-is-new-ctt}

* 用戶現在可以通過懸停在內容傳輸工具(CTT)用戶介面中的狀態表徵圖上來瞭解其訪問令牌是否已過期。 在「遷移集詳細資訊」UI中，還會通知他們無法連接到其Cloud Service實例。

### 錯誤修正 {#ctt-bug-fixes}

* 遷移集的內容傳輸工具(CTT)用戶介面狀態在一段不活動時間後未持續並更改。 這個已經修復了。
* 如果日誌不可用，則禁用了查看日誌的選項。 此問題已修復，並且已添加消息來通知用戶日誌丟失的原因。
* 顯示內容傳輸工具用戶介面狀態 *失敗* 當用戶停止攝取時。 此項已固定為顯示 *已停止* 的雙曲餘切值。
