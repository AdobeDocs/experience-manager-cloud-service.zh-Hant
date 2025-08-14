---
title: 支援的用戶端平台
description: 了解哪些瀏覽器支援使用 Adobe Experience Manager as a Cloud Service 製作內容，以及存取使用 AEM 發佈的網站。
topic-tags: platform
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
exl-id: 7ddd0a75-621a-4499-91d1-7b3408a68269
source-git-commit: bb149cd43158bfd1ceb43b04cc536c8c8291f968
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 99%

---

# 支援的用戶端平台 {#supported-platforms}

了解哪些瀏覽器支援使用 Adobe Experience Manager as a Cloud Service 製作內容，以及存取使用 AEM 發佈的網站。

>[!TIP]
>
>此文件涵蓋 AEM as a Cloud Service 支援的用戶端平台。有關開發 AEM 專案的建置環境，請參閱[建置環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)的文件，以了解更多詳細資訊。

## 支援層級 {#support-levels}

Adobe 針對 AEM 的用戶端平台定義下列支援層級。

| 支援程度 | 說明 |
|---|---|
| A：支援 | Adobe 為此設定提供完整的支援和維護。Adobe 品質保證流程涵蓋此設定。 |
| R：限制支援 | 需向 Adobe 提出要在專案中使用此設定的正式請求，才會提供支援。經 Adobe 確認後，Adobe 將在限制支援計劃內提供完整支援。如需更多詳細資訊，請聯絡 Adobe 客戶服務。 |
| Z：不支援 | 不支援此設定。Adobe 不會說明此設定是否適用，且不支援此設定。 |

## 支援製作內容的瀏覽器 {#authoring}

AEM 使用者介面已針對筆記型電腦、桌上型電腦及平板電腦裝置中的大螢幕進行最佳化 (例如 Apple iPad 或 Microsoft Surface)。任何製作使用案例皆不支援手機的外型尺寸。

視[製作方法](/help/edge/overview.md#authoring-method)而定，Adobe Experience Manager 使用者介面適用於下列用戶端平台。

* [通用編輯器](/help/sites-cloud/authoring/universal-editor/authoring.md)
* [頁面編輯器](/help/sites-cloud/authoring/page-editor/introduction.md)
* 使用 [Sidekick](https://www.aem.live/docs/sidekick) 的[文件型製作](https://www.aem.live/docs/aem-authoring)

所有瀏覽器均使用預設的外掛程式集和附加元件進行測試。

| 瀏覽器 | 通用編輯器支援層級 | 頁面編輯器支援層級 | Sidekick 支援層級 |
|---|---|---|---|
| Google Chrome (永久) | A：支援 | A：支援 | A：支援 |
| Microsoft Edge (永久) | A：支援 | A：支援 | Z：不支援 |
| Mozilla Firefox (永久) | A：支援 | A：支援 | Z：不支援 |
| Mozilla Firefox 最新 ESR [ 1] | A：支援 | A：支援 | Z：不支援 |
| macOS 上的 Safari (永久) | A：支援 | A：支援 | Z：不支援 |
| iPadOS 上的 Safari (永久) | Z：不支援 | A：支援 | Z：不支援 |

1. Firefox 的擴充支援版本 ([請造訪 mozilla.org 以了解更多資訊](https://www.mozilla.org/en-US/firefox/enterprise/))

>[!NOTE]
>
>**支援發行週期快速的瀏覽器：**
>
>Firefox、Chrome 及 Edge 定期發佈更新。Adobe 致力於對這些瀏覽器即將推出的版本維持上述支援等級。

## 網站支援的瀏覽器 {#websites}

瀏覽器對於 AEM 轉譯的網站是否支援，取決於 AEM 頁面範本、區塊、設計及元件輸出的實作。因此，負責實作專案的開發人員最終可以控制您的網站相容性。

AEM [專案範本、](https://www.aem.live/developer/ue-tutorial#create-github-project)[核心元件、](/help/implementing/developing/components/overview.md#aem-core-components)及[WKND 範本網站](/help/implementing/developing/introduction/develop-wknd-tutorial.md)均與所有現代瀏覽器相容。
