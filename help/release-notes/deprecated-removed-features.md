---
title: 已過時和移除的功能
description: Adobe Experience Manager中已停用和移除雲端服務功能的發行說明。
translation-type: tm+mt
source-git-commit: b31ae32285080075d2531edd2c4976cf801d1c89

---


# 已過時和移除的功能 {#deprecated-and-removed-features}

Adobe會持續評估產品功能，以更現代的替代方式來革新或取代舊功能，以改善整體客戶價值，並時時考慮回溯相容性。 此外，由於Adobe Experience Manager作為雲端服務提供雲端原生部署模型，因此某些功能和功能已由雲端原生對應者取代。

若要傳達即將移除／取代AEM功能，請套用下列規則：

1. 首先宣佈放棄。 淘汰的功能仍然可用，但未進一步增強。
1. 已宣佈不建議使用的功能最早會在後續的主要版本中移除。 實際的移除目標日期已宣佈。

此程式可讓客戶在實際移除之前，至少有一個發行週期，以調整其實作方式，以適應已過時功能的新版本或後繼版本。

## 不建議使用的功能 {#deprecated-features}

本節列出在Experience manager中標示為已停用的雲端服務的功能。 通常，計畫在未來版本中移除的功能會先設為不建議使用，並提供其他選項。

建議客戶在目前的部署中是否運用了功能／功能，並規劃變更實施以使用提供的替代方案。

| 區域 | 功能 | 取代 |
| ------------ | ------------------ | ----------- |
| 資產 | 資產擷取與處理不再使用工作 `DAM Asset Update` 流程 | 資產擷取現在 [使用資產微服務](/help/assets/asset-microservices-overview.md) 。 |
| 資產 | 直接將資產上傳至AEM —— 請參閱不 [建議使用的資產上傳API](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api) | [直接二進位上傳](/help/assets/add-assets.md) ，在Experience manager中會用作雲端服務。 如需技術詳細資訊，請參 [閱直接上傳API](/help/assets/developer-reference-material-apis.md#overview-binary-upload)。 |
| 資產 | [不支援工作流程中](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps)`DAM Asset Update` 的某些工作流程步驟，包括呼叫命令列工具（例如ImageMagick） | [Asset microservices](/help/assets/asset-microservices-overview.md) 可取代許多工作流程。 若是自訂處理，請使 [用後處理工作流程](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)。 |

## 已移除功能 {#removed-features}

本節列出已從AEM移除的功能和功能，其中Experience Manager是雲端服務。

| 區域 | 功能 | 取代 |
| ------------ | ------------------ | ----------- |
| UI | 雖然部分「傳統型」UI對話方塊仍保留在某些選取功能（例如「連結檢查器」、「版本清除」和某些雲端服務設定），但AEM產品UI中一般已移除對「傳統型」UI的存取。 | 標準UI |
| 動態媒體 | AEM中未提 [供先前與Dynamic Media Classic(Scene7)](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/scene7.html)[](https://helpx.adobe.com/experience-manager/6-5/assets/using/config-dynamic.html) 和Dynamic Media Hybrid模式的整合，即雲端服務。 | 將 [Experience manager隨附的Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) 當做雲端服務使用。 |
| 網站 | Portal Director和Portlet元件 | 這些功能已在AEM 6.4中過時，現在已從AEM移除。 |
| 網站 | Design Importer | 此功能已移除，因為AEM存放庫的不可變區段在執行時期無法存取。 |
| 資產 | [AEM Assets與Marketing Cloud Assets Core service和Creative cloud服務共用](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/configure-assets-cc-integration.html) ，目前不提供。 | 若要與Creative cloud整合，請使 [用Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)。 |
