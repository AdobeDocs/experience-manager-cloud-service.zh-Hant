---
title: 過時和移除的功能
description: 針對 [!DNL Adobe Experience Manager] 中已過時和已移除功能的發行說明，如a [!DNL Cloud Service]。
translation-type: tm+mt
source-git-commit: e6ad571b7428f6fb7a11907e752ba670a722057c
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 45%

---


# 過時和移除的功能 {#deprecated-and-removed-features}

Adobe 持續評估產品功能，以更新或替代的方式來改善或取代舊功能，以提升客戶享有的整體價值，且隨時謹慎考慮是否回溯相容。此外，由於[!DNL Adobe Experience Manager]是[!DNL Cloud Service]提供雲端原生部署模型，因此某些功能和功能已由雲端原生對應項取代。

要通知[!DNL Experience Manager]功能即將拆除／更換，請遵守以下規則：

1. 首先需公告功能已過時。淘汰的功能仍然可用，但未進一步增強。
1. 已宣佈過時的功能最快會從後續的主要版本中移除。公告預定的實際移除日期。

此程序可讓客戶在功能真正移除之前，至少還有一個發行週期，讓實作適應過時功能的新版本或後續版本。

## 過時的功能 {#deprecated-features}

本節列出在[!DNL Experience Manager]中已標籤為已過時的特性和功能，作為[!DNL Cloud Service]。 通常，未來版本中要移除的功能會先設為不建議使用，並提供替代功能。

建議客戶檢閱其目前部署中是否使用功能／功能，並規劃變更實作以使用提供的替代方案。

| 功能 | 汰除功能 | 替代方案 |
| ------------ | ------------------ | ----------- |
| [!DNL Assets] | 處理所擷取影像的 `DAM Asset Update` 工作流程。 | 資產擷取現在使用[資產微服務](/help/assets/asset-microservices-overview.md)。 |
| [!DNL Assets] | 將資產直接上傳至[!DNL Experience Manager]。請參閱[不建議使用的資產上傳API](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api)。 | 使用[直接二進位上傳](/help/assets/add-assets.md)。如需技術詳細資訊，請參閱[直接上傳 API](/help/assets/developer-reference-material-apis.md#upload-binary)。 |
| [!DNL Assets] | 不支援 `DAM Asset Update` 工作流程中的[某些工作流程步驟](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps)，包括呼叫命令列工具，例如 ImageMagick。 | [資產微服務](/help/assets/asset-microservices-overview.md)可取代許多工作流程。若要自訂處理程序，請使用[後期處理工作流程](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)。 |
| [!DNL Assets] | FFmpeg 影片轉碼。 | 若要產生 FFmpeg 縮圖，請使用[資產微服務](/help/assets/asset-microservices-overview.md)。若是 FFmpeg 轉碼，請使用 [Dynamic Media](/help/assets/manage-video-assets.md)。 |

## 移除的功能 {#removed-features}

本節列出已從[!DNL Experience Manager]移除的功能，其中[!DNL Experience Manager]為[!DNL Cloud Service]。

| 區域 | 功能 | 替代方案 |
| ------------ | ------------------ | ----------- |
| 使用者介面 | 傳統UI會從產品使用者介面中移除。 有幾個「傳統UI」對話框可用於一些選擇功能，如連結檢查器、版本清除和某些Cloud Service配置。 即將推出的[產品更新](/help/release-notes/home.md)可能會進一步移除Classic UI的可用性。 | 標準 UI |
| [!DNL Dynamic Media] | [Dynamic Media經典](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/scene7.html#integration)和[Dynamic Media混合模式](https://experienceleague.adobe.com/docs/experience-manager-65/assets/dynamic/config-dynamic.html#dynamic)先前的整合在[!DNL Experience Manager]中不提供[!DNL Cloud Service]。 | 使用隨[!DNL Experience Manager]提供的[Dynamic Media](/help/assets/dynamic-media/dynamic-media.md)作為[!DNL Cloud Service]。 |
| [!DNL Sites] | Portal Director 和 Portlet 元件 | 這些功能在[!DNL Experience Manager] 6.4中已過時，現在已從[!DNL Experience Manager]中移除。 |
| [!DNL Sites] | Design Importer | 由於[!DNL Experience Manager]儲存庫的不可變部分在運行時無法訪問，因此已刪除此功能。 |
| [!DNL Assets] | [[!DNL Assets]  無法與 Marketing Cloud Assets 核心服務和 Creative Cloud 服務共用](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/configure-assets-cc-integration.html)。 | 若要與[!DNL Adobe Creative Cloud]整合，請使用[Adobe資產連結](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html)。 |
