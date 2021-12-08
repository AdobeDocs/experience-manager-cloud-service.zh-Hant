---
title: 過時和移除的功能
description: 特定於中已過時和已移除功能的發行說明 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service].
exl-id: ef082184-4eb7-49c7-8887-03d925e3da6f
source-git-commit: 9410b061278d916c95233ecba7f7f946fccc51ed
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 34%

---

# 過時和移除的功能 {#deprecated-and-removed-features}

>[!CONTEXTUALHELP]
>id="aem_cloud_deprecated_features"
>title="AEMas a Cloud Service中已棄用和已移除的功能"
>abstract="AEMas a Cloud Service採用雲端原生部署模型。 雲端原生對應功能已更換某些功能，此索引標籤會顯示這些功能。"


Adobe 持續評估產品功能，以更新或替代的方式來改善或取代舊功能，以提升客戶享有的整體價值，且隨時謹慎考慮是否回溯相容。另外，如 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 提供雲端原生部署模型，某些功能已由雲端原生對應項目取代。

通知即將移除/更換的 [!DNL Experience Manager] 功能，則套用下列規則：

1. 首先需公告功能已過時。已棄用的功能仍可用，但未進一步增強。
1. 已宣佈過時的功能最快會從後續的主要版本中移除。公告預定的實際移除日期。

此程序可讓客戶在功能真正移除之前，至少還有一個發行週期，讓實作適應過時功能的新版本或後續版本。

## 過時的功能 {#deprecated-features}

本節列出已標籤為過時的功能， [!DNL Experience Manager] as a [!DNL Cloud Service]. 日後版本通常會將移除的功能設為先過時，並提供替代選項。

建議客戶檢閱是否在目前部署中使用功能，並規劃變更實作的計畫，以使用所提供的替代方案。

| 功能 | 汰除功能 | 替代方案 |
| ------------ | ------------------ | ----------- |
| [!DNL Sites] | 的體驗片段屬性 **社交媒體狀態**. | 功能即將移除。 |
| [!DNL Sites] | 以範本為基礎的簡單內容片段。 | [基於模型的結構化內容片段](/help/assets/content-fragments/content-fragments-models.md) 現在。 |
| [!DNL Assets] | 處理所擷取影像的 `DAM Asset Update` 工作流程。 | 資產擷取現在使用[資產微服務](/help/assets/asset-microservices-overview.md)。 |
| [!DNL Assets] | 直接將資產上傳至 [!DNL Experience Manager].請參閱 [汰除的資產上傳API](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api). | 使用[直接二進位上傳](/help/assets/add-assets.md)。如需技術詳細資訊，請參閱[直接上傳 API](/help/assets/developer-reference-material-apis.md#upload-binary)。 |
| [!DNL Assets] | 不支援 [ 工作流程中的](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps)某些工作流程步驟`DAM Asset Update`，包括呼叫命令列工具，例如 [!DNL ImageMagick]. | [資產微服務](/help/assets/asset-microservices-overview.md)可取代許多工作流程。若要自訂處理程序，請使用[後期處理工作流程](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)。 |
| [!DNL Assets] | FFmpeg 影片轉碼。 | 若要產生 FFmpeg 縮圖，請使用[資產微服務](/help/assets/asset-microservices-overview.md)。若是 FFmpeg 轉碼，請使用 [Dynamic Media](/help/assets/manage-video-assets.md)。 |
| [!DNL Foundation] | 復寫代理的「分發」標籤下的樹狀復寫UI（在2021年9月30日後刪除） | [管理出版物](/help/operations/replication.md#manage-publication) 或 [發佈內容樹工作流程](/help/operations/replication.md#publish-content-tree-workflow) 方法 |

## 移除的功能 {#removed-features}

本節列出已從 [!DNL Experience Manager] with [!DNL Experience Manager] as a [!DNL Cloud Service].

| 區域 | 功能 | 替代方案 |
| ------------ | ------------------ | ----------- |
| 使用者介面 | 傳統UI會從產品使用者介面中移除。 少數傳統UI對話方塊可用於一些特定功能，例如連結檢查程式、版本清除和某些Cloud Service設定。 即將推出 [產品更新](/help/release-notes/home.md) 可能會進一步移除傳統UI可用性。 | 標準 UI |
| [!DNL Dynamic Media] | 先前的整合，搭配 [Dynamic Media Classic](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/scene7.html#integration) 和 [Dynamic Media混合模式](https://experienceleague.adobe.com/docs/experience-manager-65/assets/dynamic/config-dynamic.html#dynamic) 中不提供 [!DNL Experience Manager] as a [!DNL Cloud Service]. | 使用 [Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) 隨附 [!DNL Experience Manager] as a [!DNL Cloud Service]. |
| [!DNL Sites] | Portal Director 和 Portlet 元件 | 這些功能已於 [!DNL Experience Manager] 6.4，現已從 [!DNL Experience Manager]. |
| [!DNL Sites] | Design Importer | 此功能已移除，作為 [!DNL Experience Manager] 在運行時無法訪問儲存庫。 |
| [!DNL Assets] | [!DNL Assets] 無法與 Marketing Cloud Assets 核心服務和 Creative Cloud 服務共用。 | 與整合 [!DNL Adobe Creative Cloud]，使用 [Adobe資產連結](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html). |
| [!DNL Foundation] | 支援Apache Sling資料來源（OSGi套件組合org.apache.sling.datasource）。 | N/A |

## Java API {#java-api}

請參閱 [本頁](/help/release-notes/deprecated-apis.md) 適用於任何已過時或已移除的Java API，這些API偶爾會導入。

## OSGI設定 {#osgi-configuration}

請參閱 [這篇文章](/help/implementing/deploying/osgi-configuration-api.md) OSGI屬性設定的任何限制，部分可能會隨著時間引入。
