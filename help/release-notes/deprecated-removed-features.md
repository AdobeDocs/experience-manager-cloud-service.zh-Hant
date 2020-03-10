---
title: 過時和移除的功能
description: 此發行說明著重於 Adobe Experience Manager 雲端服務中已過時和移除的功能。
translation-type: ht
source-git-commit: b31ae32285080075d2531edd2c4976cf801d1c89

---


# 過時和移除的功能 {#deprecated-and-removed-features}

Adobe 持續評估產品功能，以更新或替代的方式來改善或取代舊功能，以提升客戶享有的整體價值，且隨時謹慎考慮是否回溯相容。此外，由於 Adobe Experience Manager 雲端服務提供雲端原生部署模型，因此某些功能已由對應的雲端原生功能取代。

若要傳達 AEM 功能即將移除/取代的訊息，請套用下列規則：

1. 首先需公告功能已過時。過時的功能仍可使用，但往後不會有所改善。
1. 已宣佈過時的功能最快會從後續的主要版本中移除。公告預定的實際移除日期。

此程序可讓客戶在功能真正移除之前，至少還有一個發行週期，讓實作適應過時功能的新版本或後續版本。

## 過時的功能 {#deprecated-features}

本節提供 Experience Manager 雲端服務中標示為過時的功能。日後版本通常會將預計移除的功能設為過時，並提供其他選項。

建議客戶檢視是否在目前的部署中使用這些功能，並規劃變更實作，改為使用所提供的替代方案。

| 區域 | 功能 | 替代方案 |
| ------------ | ------------------ | ----------- |
| 資產 | 資產擷取與處理功能不再使用 `DAM Asset Update` 工作流程 | 資產擷取現在使用[資產微服務](/help/assets/asset-microservices-overview.md)。 |
| 資產 | 將資產直接上傳至 AEM - 請參閱[過時資產上傳 API](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api) | Experience Manager 雲端服務會使用[直接二進位上傳](/help/assets/add-assets.md)。如需技術詳細資訊，請參閱[直接上傳 API](/help/assets/developer-reference-material-apis.md#overview-binary-upload)。 |
| 資產 | 不支援 `DAM Asset Update` 工作流程中的[某些工作流程步驟](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps)，包括呼叫命令列工具，例如 ImageMagick | [資產微服務](/help/assets/asset-microservices-overview.md)可取代許多工作流程。若要自訂處理程序，請使用[後期處理工作流程](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)。 |

## 移除的功能 {#removed-features}

本節提供已從具 Experience Manager 雲端服務之 AEM 中移除的功能。

| 區域 | 功能 | 替代方案 |
| ------------ | ------------------ | ----------- |
| UI | 雖然少數特定功能 (例如「連結檢查程式」、「版本清除」和部分雲端服務設定) 會保留部分傳統 UI 對話方塊，但使用者已無法在 AEM 產品 UI 中存取傳統 UI。 | 標準 UI |
| Dynamic Media | AEM 雲端服務中無法使用先前整合的 [Dynamic Media Classic (Scene7)](https://helpx.adobe.com/tw/experience-manager/6-5/sites/administering/using/scene7.html) 和 [Dynamic Media 混合模式](https://helpx.adobe.com/tw/experience-manager/6-5/assets/using/config-dynamic.html)。 | 請使用 Experience Manager 雲端服務隨附的 [Dynamic Media](/help/assets/dynamic-media/dynamic-media.md)。 |
| 網站 | Portal Director 和 Portlet 元件 | 這些功能在 AEM 6.4 中已過時，已從 AEM 中移除。 |
| 網站 | Design Importer | 此功能已移除，因為無法在執行階段存取 AEM 儲存庫的不可修改區段。 |
| Assets | [AEM Assets 無法與 Marketing Cloud Assets 核心服務和 Creative Cloud 服務共用](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/configure-assets-cc-integration.html)。 | 若要與 Creative Cloud 整合，請使用 [Adobe Asset Link](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html)。 |
