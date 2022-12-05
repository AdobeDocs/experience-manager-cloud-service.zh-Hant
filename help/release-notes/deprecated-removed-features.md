---
title: 過時和移除的功能
description: 特定於  [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 中已過時和已移除功能的發行說明。
exl-id: ef082184-4eb7-49c7-8887-03d925e3da6f
source-git-commit: c4809bcbeae5339427b1da588021606d18b482a5
workflow-type: ht
source-wordcount: '666'
ht-degree: 100%

---

# 過時和移除的功能 {#deprecated-and-removed-features}

>[!CONTEXTUALHELP]
>id="aem_cloud_deprecated_features"
>title="AEM as a Cloud Service 中已過時和已移除的功能"
>abstract="AEM as a Cloud Service 具有雲端原生部署模型。某些功能和特性已由對應的雲生原生功能取代，此標籤顯示了這些功能。"


Adobe 持續評估產品功能，以更新或替代的方式來改善或取代舊功能，以提升客戶享有的整體價值，且隨時謹慎考慮是否回溯相容。此外，由於 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 提供雲端原生部署模型，因此某些功能已由對應的雲端原生功能取代。

若要傳達 [!DNL Experience Manager] 功能即將移除/取代的訊息，請套用下列規則：

1. 首先需公告功能已過時。過時的功能仍可使用，但往後不會有所改善。
1. 已宣佈過時的功能最快會從後續的主要版本中移除。公告預定的實際移除日期。

此程序可讓客戶在功能真正移除之前，至少還有一個發行週期，讓實作適應過時功能的新版本或後續版本。

## 過時的功能 {#deprecated-features}

本節提供 [!DNL Experience Manager] as a [!DNL Cloud Service] 中標示為過時的功能。 日後版本通常會先將移除的功能設為過時，並提供其他選項。

建議客戶檢閱是否在目前的部署中使用這些功能，並規劃變更實作，改用所提供的替代方案。

| 功能 | 汰除功能 | 替代方案 |
| ------------ | ------------------ | ----------- |
| [!DNL Sites] | **社交媒體狀態**&#x200B;的體驗片段屬性。 | 該功能不久將移除。 |
| [!DNL Sites] | 基於範本的簡單內容片段。 | 現在[基於模型的結構化內容片段](/help/assets/content-fragments/content-fragments-models.md)。 |
| [!DNL Assets] | 處理所擷取影像的 `DAM Asset Update` 工作流程。 | 資產擷取現在使用[資產微服務](/help/assets/asset-microservices-overview.md)。 |
| [!DNL Assets] | 將資產直接上傳至 [!DNL Experience Manager]。請參閱[過時的資產上傳 API](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api)。 | 使用[直接二進位上傳](/help/assets/add-assets.md)。如需技術詳細資訊，請參閱[直接上傳 API](/help/assets/developer-reference-material-apis.md#upload-binary)。 |
| [!DNL Assets] | 不支援 [ 工作流程中的](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps)某些工作流程步驟`DAM Asset Update`，包括呼叫命令列工具，例如 [!DNL ImageMagick]. | [資產微服務](/help/assets/asset-microservices-overview.md)可取代許多工作流程。若要自訂處理程序，請使用[後期處理工作流程](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)。 |
| [!DNL Assets] | FFmpeg 影片轉碼。 | 若要產生 FFmpeg 縮圖，請使用[資產微服務](/help/assets/asset-microservices-overview.md)。若是 FFmpeg 轉碼，請使用 [Dynamic Media](/help/assets/manage-video-assets.md)。 |
| [!DNL Foundation] | 複寫代理程式的「散發」標籤下的樹狀結構複寫 UI (2021 年 9 月 30 日後移除) | [管理出版物](/help/operations/replication.md#manage-publication)或[發佈內容樹工作流程](/help/operations/replication.md#publish-content-tree-workflow)方法 |
| [!DNL Foundation] | 複寫代理程式管理員畫面的「散發」標籤和複寫 API 都不能用於複寫超過 10MB 的內容套件 (2022 年 9 月 12 日後強制執行) | [管理出版物](/help/operations/replication.md#manage-publication)或[發佈內容樹工作流程](/help/operations/replication.md#publish-content-tree-workflow)方法 |


| [!DNL Foundation]       | 複寫代理程式管理員畫面的「散發」標籤和複寫 API 都不能用於複寫超過 10MB 的內容套件。請改用[管理出版物](/help/operations/replication.md#manage-publication)或[發佈內容樹工作流程](/help/operations/replication.md#publish-content-tree-workflow) |

## 移除的功能 {#removed-features}

本節提供已從具 [!DNL Experience Manager] 之 [!DNL Experience Manager] as a [!DNL Cloud Service] 中移除的功能。

| 區域 | 功能 | 替代方案 | 目標移除日期 |
| ------------ | ------------------ | ----------- | ------------------- |
| 使用者介面 | 傳統 UI 已從產品使用者介面中移除。一些傳統 UI 對話框可用於一些選定的功能，例如連結檢查器、版本清除和一些 Cloud Service 設定。即將推出的[產品更新](/help/release-notes/home.md)可能會進一步移除傳統 UI 可用性。 | 標準 UI | 已移除 |
| [!DNL Dynamic Media] | 先前與 [Dynamic Media Classic](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/scene7.html#integration) 和 [Dynamic Media 混合模式](https://experienceleague.adobe.com/docs/experience-manager-65/assets/dynamic/config-dynamic.html#dynamic)整合無法在 [!DNL Experience Manager] as a [!DNL Cloud Service]中使用。 | 請使用 [Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) (隨 [!DNL Experience Manager] as a [!DNL Cloud Service] 提供)。 | 已移除 |
| [!DNL Sites] | Portal Director 和 Portlet 元件 | 這些功能在 [!DNL Experience Manager] 6.4 中已過時，並已從 [!DNL Experience Manager] 中移除。 | 已移除 |
| [!DNL Sites] | Design Importer | 此功能已移除，因為無法在執行階段存取 [!DNL Experience Manager] 存放庫的不可修改區段。 | 已移除 |
| [!DNL Assets] | [!DNL Assets] 無法與 Marketing Cloud Assets 核心服務和 Creative Cloud 服務共用。 | 若要與 [!DNL Adobe Creative Cloud] 整合，請使用 [Adobe Asset Link](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html)。 | 已移除 |
| [!DNL Foundation] | 支援 Apache Sling 資料來源 (OSGi 套件組合 org.apache.sling.datasource) | N/A | 已移除 |
| [!DNL Foundation] | 支援 JST 指令碼範本 (OSGi 套件組合 org.apache.sling.scripting.jst) | N/A | 已移除 |
| [!DNL Foundation] | 支援 Apache Felix Http Whiteboard | OSGi Http Whiteboard | 2022 年 3 月 |

## Java API {#java-api}

請參閱[本頁](/help/release-notes/deprecated-apis.md)以了解任何已過時或移除的 Java API (偶爾會引入)。

## OSGI 設定 {#osgi-configuration}

請參閱[本文](/help/implementing/deploying/osgi-configuration-api.md)以了解有關 OSGI 屬性設定的任何限制，其中一些可能會隨時間引入。
