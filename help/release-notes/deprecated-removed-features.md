---
title: 過時和移除的功能
description: 特定於 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]中已棄用和已移除功能的發行說明。
exl-id: ef082184-4eb7-49c7-8887-03d925e3da6f
source-git-commit: 8742c4058a5b89a0d6aca0d6e58ed993b01d084d
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 38%

---

# 過時和移除的功能 {#deprecated-and-removed-features}

>[!CONTEXTUALHELP]
>id="aem_cloud_deprecated_features"
>title="AEM as aCloud Service中已棄用和已移除的功能"
>abstract="AEM as aCloud Service採用雲端原生部署模型。 雲端原生對應功能已更換某些功能，此索引標籤會顯示這些功能。"


Adobe 持續評估產品功能，以更新或替代的方式來改善或取代舊功能，以提升客戶享有的整體價值，且隨時謹慎考慮是否回溯相容。此外，由於[!DNL Adobe Experience Manager]作為[!DNL Cloud Service]提供雲端原生部署模型，因此某些功能已由雲端原生對應項目取代。

為傳達[!DNL Experience Manager]功能即將移除/取代的訊息，請套用下列規則：

1. 首先需公告功能已過時。已棄用的功能仍可用，但未進一步增強。
1. 已宣佈過時的功能最快會從後續的主要版本中移除。公告預定的實際移除日期。

此程序可讓客戶在功能真正移除之前，至少還有一個發行週期，讓實作適應過時功能的新版本或後續版本。

## 過時的功能 {#deprecated-features}

本節列出在[!DNL Experience Manager]中標籤為[!DNL Cloud Service]的功能。 日後版本通常會將移除的功能設為先過時，並提供替代選項。

建議客戶檢閱是否在目前部署中使用功能，並規劃變更實作的計畫，以使用所提供的替代方案。

| 功能 | 汰除功能 | 替代方案 |
| ------------ | ------------------ | ----------- |
| [!DNL Assets] | 處理所擷取影像的 `DAM Asset Update` 工作流程。 | 資產擷取現在使用[資產微服務](/help/assets/asset-microservices-overview.md)。 |
| [!DNL Assets] | 直接將資產上傳至[!DNL Experience Manager]。請參閱[已棄用的資產上傳API](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api)。 | 使用[直接二進位上傳](/help/assets/add-assets.md)。如需技術詳細資訊，請參閱[直接上傳 API](/help/assets/developer-reference-material-apis.md#upload-binary)。 |
| [!DNL Assets] | 不支援 [ 工作流程中的](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps)某些工作流程步驟`DAM Asset Update`，包括呼叫命令列工具，例如 [!DNL ImageMagick]. | [資產微服務](/help/assets/asset-microservices-overview.md)可取代許多工作流程。若要自訂處理程序，請使用[後期處理工作流程](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)。 |
| [!DNL Assets] | FFmpeg 影片轉碼。 | 若要產生 FFmpeg 縮圖，請使用[資產微服務](/help/assets/asset-microservices-overview.md)。若是 FFmpeg 轉碼，請使用 [Dynamic Media](/help/assets/manage-video-assets.md)。 |
| [!DNL Foundation] | 復寫代理的「分發」標籤下的樹狀復寫UI（在2021年9月30日後刪除） | [管理](/help/operations/replication.md#manage-publication) 發佈或 [發佈內容樹工](/help/operations/replication.md#publish-content-tree-workflow) 作流程方法 |

## 移除的功能 {#removed-features}

本節列出已從[!DNL Experience Manager]中移除且[!DNL Experience Manager]為[!DNL Cloud Service]的功能。

| 區域 | 功能 | 替代方案 |
| ------------ | ------------------ | ----------- |
| 使用者介面 | 傳統UI會從產品使用者介面中移除。 少數傳統UI對話方塊可用於一些特定功能，例如連結檢查程式、版本清除和某些Cloud Service設定。 即將推出的[產品更新](/help/release-notes/home.md)可能會進一步移除傳統UI可用性。 | 標準 UI |
| [!DNL Dynamic Media] | 先前與[Dynamic Media Classic](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/scene7.html#integration)和[Dynamic Media混合模式](https://experienceleague.adobe.com/docs/experience-manager-65/assets/dynamic/config-dynamic.html#dynamic)的整合，在[!DNL Experience Manager]中無法以[!DNL Cloud Service]的形式提供。 | 使用隨[!DNL Experience Manager]提供的[Dynamic Media](/help/assets/dynamic-media/dynamic-media.md)作為[!DNL Cloud Service]。 |
| [!DNL Sites] | Portal Director 和 Portlet 元件 | 這些功能在[!DNL Experience Manager] 6.4中已過時，並已從[!DNL Experience Manager]中移除。 |
| [!DNL Sites] | Design Importer | 此功能已被刪除，因為在運行時無法訪問[!DNL Experience Manager]儲存庫的不可修改部分。 |
| [!DNL Assets] | [!DNL Assets] 無法與 Marketing Cloud Assets 核心服務和 Creative Cloud 服務共用。 | 若要與[!DNL Adobe Creative Cloud]整合，請使用[Adobe資產連結](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html)。 |
| [!DNL Foundation] | 支援Apache Sling資料來源（OSGi套件組合org.apache.sling.datasource）。 | N/A |
