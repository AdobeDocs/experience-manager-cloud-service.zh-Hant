---
title: 支援的使用者端平台
description: 瞭解哪些瀏覽器支援透過Adobe Experience Manager as a Cloud Service製作內容及存取透過AEM發佈的網站。
topic-tags: platform
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: 22d4e6b5f87221b2739cf1dd9d59b4652a014316
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 1%

---


# 支援的使用者端平台 {#supported-platforms}

瞭解哪些瀏覽器支援透過Adobe Experience Manager as a Cloud Service製作內容及存取透過AEM發佈的網站。

>[!TIP]
>
>本文介紹AEM as a Cloud Service所支援的使用者端平台。 如需有關開發AEM專案的組建環境的詳細資訊，請參閱檔案[組建環境。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)

## 支援等級 {#support-levels}

Adobe會定義AEM使用者端平台的下列支援等級。

| 支援程度 | 說明 |
|---|---|
| 答：支援 | Adobe會針對此設定提供完整支援與維護。 Adobe品質保證程式涵蓋此設定。 |
| R：受限制的支援 | 若要取得支援，必須向Adobe提出正式要求，才能在專案中使用設定。 經Adobe確認後，Adobe會在受限制的支援方案中提供完整支援。 如需詳細資訊，請聯絡Adobe客戶服務。 |
| Z：不支援 | 不支援此設定。 Adobe不會陳述設定是否有效，也不支援此設定。 |

## 製作內容的支援瀏覽器 {#authoring}

AEM使用者介面已針對筆記型電腦、桌上型電腦和平板電腦裝置(例如Apple iPad或Microsoft Surface)的大型熒幕進行最佳化。 電話外型規格不支援任何製作使用案例。

根據[編寫方法，Adobe Experience Manager使用者介面可與下列使用者端平台搭配使用。](/help/edge/authoring-methods.md)

* [通用編輯器](/help/sites-cloud/authoring/universal-editor/authoring.md)
* [頁面編輯器](/help/sites-cloud/authoring/page-editor/introduction.md)
* 使用[Sidekick](/help/edge/docs/sidekick.md)的[檔案式製作](/help/edge/docs/authoring.md)

所有瀏覽器都透過一組預設的外掛程式和附加元件進行測試。

| 瀏覽器 | 通用編輯器支援等級 | 頁面編輯器支援等級 | Sidekick支援等級 |
|---|---|---|---|
| Google Chrome （長青） | 答：支援 | 答：支援 | 答：支援 |
| Microsoft Edge （長青） | 答：支援 | 答：支援 | Z：不支援 |
| Mozilla Firefox （常青） | 答：支援 | 答：支援 | Z：不支援 |
| Mozilla Firefox最新的ESR [1] | 答：支援 | 答：支援 | Z：不支援 |
| macOS上的Safari （常青） | 答：支援 | 答：支援 | Z：不支援 |
| iOS （常青） [2]上的Safari | Z：不支援 | 答：支援 | Z：不支援 |

1. Firefox的延伸支援版本（[在mozilla.org](https://www.mozilla.org/en-US/firefox/enterprise/)上深入瞭解）
1. 僅支援Apple iPad

>[!NOTE]
>
>**支援快速發行週期的瀏覽器：**
>
>Firefox、Chrome和Edge會定期發行更新。 Adobe承諾針對這些瀏覽器的未來版本維持如上列出的支援等級。

## 支援的網站瀏覽器 {#websites}

AEM所轉譯網站的瀏覽器支援取決於AEM頁面範本、區塊、設計和元件輸出的實作。 因此，實作您專案的開發人員最終可控制您網站的相容性。

AEM [專案樣版，](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md#create-github-project) [核心元件，](/help/implementing/developing/components/overview.md#aem-core-components)和[WKND範例網站](/help/implementing/developing/introduction/develop-wknd-tutorial.md)都與所有現代瀏覽器相容。
