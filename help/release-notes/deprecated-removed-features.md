---
title: 過時和移除的功能
description: 特定於中已棄用和已刪除功能的發行說明 [!DNL Adobe Experience Manager] 作為 [!DNL Cloud Service]。
exl-id: ef082184-4eb7-49c7-8887-03d925e3da6f
source-git-commit: c4809bcbeae5339427b1da588021606d18b482a5
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 31%

---

# 過時和移除的功能 {#deprecated-and-removed-features}

>[!CONTEXTUALHELP]
>id="aem_cloud_deprecated_features"
>title="as a Cloud Service中的已棄用和已刪除功AEM能"
>abstract="AEMas a Cloud Service有雲本機部署模型。 某些功能和功能已由雲本地對應方替換，此頁籤顯示這些功能。"


Adobe 持續評估產品功能，以更新或替代的方式來改善或取代舊功能，以提升客戶享有的整體價值，且隨時謹慎考慮是否回溯相容。另外， [!DNL Adobe Experience Manager] 作為 [!DNL Cloud Service] 提供雲本機部署模型，某些功能和功能被雲本機部署模型取代。

傳達即將拆除/更換的 [!DNL Experience Manager] 權能，適用以下規則：

1. 首先需公告功能已過時。已棄用的功能仍然可用，但不會進一步增強。
1. 已宣佈過時的功能最快會從後續的主要版本中移除。公告預定的實際移除日期。

此程序可讓客戶在功能真正移除之前，至少還有一個發行週期，讓實作適應過時功能的新版本或後續版本。

## 過時的功能 {#deprecated-features}

本節列出在中標籤為不建議使用的功能和功能 [!DNL Experience Manager] 作為 [!DNL Cloud Service]。 通常，將來版本中要刪除的功能會先設定為不建議使用，並提供替代選項。

建議客戶檢查其當前部署中是否使用了該功能/功能，並制定計畫更改其實施以使用提供的替代方案。

| 功能 | 汰除功能 | 替代方案 |
| ------------ | ------------------ | ----------- |
| [!DNL Sites] | 體驗片段屬性 **社交媒體狀態**。 | 該功能將很快刪除。 |
| [!DNL Sites] | 基於模板的簡單內容片段。 | [基於模型的結構化內容片段](/help/assets/content-fragments/content-fragments-models.md) 現在。 |
| [!DNL Assets] | 處理所擷取影像的 `DAM Asset Update` 工作流程。 | 資產擷取現在使用[資產微服務](/help/assets/asset-microservices-overview.md)。 |
| [!DNL Assets] | 將資產直接上載到 [!DNL Experience Manager]。請參閱 [不建議使用的資產上載API](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api)。 | 使用[直接二進位上傳](/help/assets/add-assets.md)。如需技術詳細資訊，請參閱[直接上傳 API](/help/assets/developer-reference-material-apis.md#upload-binary)。 |
| [!DNL Assets] | 不支援 [ 工作流程中的](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps)某些工作流程步驟`DAM Asset Update`，包括呼叫命令列工具，例如 [!DNL ImageMagick]. | [資產微服務](/help/assets/asset-microservices-overview.md)可取代許多工作流程。若要自訂處理程序，請使用[後期處理工作流程](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)。 |
| [!DNL Assets] | FFmpeg 影片轉碼。 | 若要產生 FFmpeg 縮圖，請使用[資產微服務](/help/assets/asset-microservices-overview.md)。若是 FFmpeg 轉碼，請使用 [Dynamic Media](/help/assets/manage-video-assets.md)。 |
| [!DNL Foundation] | 複製代理的「分發」頁籤下的樹複製UI（2021年9月30日後刪除） | [管理發布](/help/operations/replication.md#manage-publication) 或 [發佈內容樹工作流](/help/operations/replication.md#publish-content-tree-workflow) 方法 |
| [!DNL Foundation] | 複製代理管理螢幕的「分發」頁籤和複製API都不能用於複製超過10MB的內容包（2022年9月12日之後實施） | [管理發布](/help/operations/replication.md#manage-publication) 或 [發佈內容樹工作流](/help/operations/replication.md#publish-content-tree-workflow) 方法 |


| [!DNL Foundation]       |複製代理管理螢幕的「分發」頁籤和複製API都不能用於複製超過10MB的內容包。 而是使用 [管理發布](/help/operations/replication.md#manage-publication) 或 [發佈內容樹工作流](/help/operations/replication.md#publish-content-tree-workflow) |

## 刪除的功能 {#removed-features}

本節列出已從中刪除的功能和功能 [!DNL Experience Manager] 與 [!DNL Experience Manager] 作為 [!DNL Cloud Service]。

| 區域 | 功能 | 替代方案 | 目標刪除日期 |
| ------------ | ------------------ | ----------- | ------------------- |
| 使用者介面 | 經典UI將從產品用戶介面中刪除。 幾個標準UI對話框可用於一些選擇的功能，如連結檢查器、版本清除和一些Cloud Service配置。 即將 [產品更新](/help/release-notes/home.md) 可能會進一步刪除經典UI可用性。 | 標準 UI | 已移除 |
| [!DNL Dynamic Media] | 以前與 [Dynamic Media Classic](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/scene7.html#integration) 和 [Dynamic Media混合模式](https://experienceleague.adobe.com/docs/experience-manager-65/assets/dynamic/config-dynamic.html#dynamic) 在中不可用 [!DNL Experience Manager] 作為 [!DNL Cloud Service]。 | 使用 [Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) 提供 [!DNL Experience Manager] 作為 [!DNL Cloud Service]。 | 已移除 |
| [!DNL Sites] | Portal Director 和 Portlet 元件 | 中不建議使用這些功能 [!DNL Experience Manager] 6.4，現已從 [!DNL Experience Manager]。 | 已移除 |
| [!DNL Sites] | Design Importer | 此功能已作為不可變的 [!DNL Experience Manager] 在運行時無法訪問儲存庫。 | 已移除 |
| [!DNL Assets] | [!DNL Assets] 無法與 Marketing Cloud Assets 核心服務和 Creative Cloud 服務共用。 | 與 [!DNL Adobe Creative Cloud]。 [Adobe資產連結](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html)。 | 已移除 |
| [!DNL Foundation] | 支援Apache Sling資料源（OSGi捆綁包org.apache.sling.datasource） | N/A | 已移除 |
| [!DNL Foundation] | 支援JST指令碼模板（OSGi捆綁包org.apache.sling.scripting.jst） | 不適用 | 已移除 |
| [!DNL Foundation] | 支援Apache Felix Http白板 | OSGi Http白板 | 2022年3月 |

## Java API {#java-api}

請參閱 [此頁](/help/release-notes/deprecated-apis.md) 對於任何已棄用或已刪除的Java API，這些API偶爾會被引入。

## OSGI配置 {#osgi-configuration}

請參閱 [這篇文章](/help/implementing/deploying/osgi-configuration-api.md) 對OSGI屬性配置的任何限制，其中某些限制可能會隨時間推移而引入。
