---
title: CI/CD管道
description: 了解Cloud Manager的CI/CD管道，以及如何使用管道來有效部署程式碼。
index: true
exl-id: 40d6778f-65e0-4612-bbe3-ece02905709b
source-git-commit: 6c246444f48440c64af0951e75f2071c00e477fa
workflow-type: tm+mt
source-wordcount: '1377'
ht-degree: 0%

---

# Cloud Manager CI/CD管道 {#intro-cicd}

了解Cloud Manager的CI/CD管道，以及如何使用管道來有效部署程式碼。

## 簡介 {#introduction}

Cloud Manager中的CI/CD管道是一種從原始碼存放庫建立程式碼，並部署至環境的機制。 管道可由事件觸發，例如來自原始碼存放庫的提取請求（即程式碼變更），或透過定期排程以符合發行順序。

若要設定管道，您必須：

* 定義將啟動管道的觸發器。
* 定義控制生產部署的參數。
* 配置效能測試參數。

Cloud Manager提供兩種管道：

* [生產管道](#prod-pipeline)
* [非生產管道](#non-prod-pipeline)

![管道類型](/help/implementing/cloud-manager/assets/configure-pipeline/ci-cd-config1.png)

## 影片概述 {#video}

如需管道類型的快速概述，請觀看此短片。

>[!VIDEO](https://video.tv.adobe.com/v/342363)

## 生產管道 {#prod-pipeline}

生產管道是專門建置的管道，包含一系列協調步驟，以部署原始碼供生產使用。 這些步驟包括先建立、封裝、測試、驗證，以及部署至所有測試環境。 因此，只有建立一組生產和預備環境後，才能新增生產管道。

>[!TIP]
>
>請參閱檔案 [設定生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) 以取得更多詳細資訊。

## 非生產管道 {#non-prod-pipeline}

非生產管道主要用於執行程式碼品質掃描或將原始碼部署至開發環境。

>[!TIP]
>
>請參閱檔案 [設定非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) 以取得更多詳細資訊。

## 代碼來源 {#code-sources}

除了生產和非生產外，管道還可依其部署的程式碼類型加以區別。

* **[完整堆棧管道](#full-stack-pipeline)**  — 同時部署後端和前端程式碼組建，其中包含一或多個AEM伺服器應用程式以及HTTPD/Dispatcher設定
* **[前端管道](#front-end)**  — 部署包含一或多個用戶端UI應用程式的前端程式碼組建
* **[Web層配置管道](#web-tier-config-pipelines)**  — 部署HTTPD/Dispatcher設定

本檔案稍後會詳細說明這些項目。

### 了解Cloud Manager中的CI-CD管道 {#understand-pipelines}

下表總結了Cloud Manager中可用的所有管道及其使用方式。

| 管線類型 | 部署或程式碼品質 | 原始碼 | 用途 | 附註 |
|--- |--- |--- |---|---|
| 生產或非生產 | 部署 | 完整堆疊 | 同時部署後端和前端程式碼組建，以及HTTPD/Dispatcher設定 | 前端程式碼必須與AEM伺服器程式碼同時部署時。<br>當前端管道或Web層配置管道尚未採用時。 |
| 生產或非生產 | 部署 | 前端 | 部署包含一或多個用戶端UI應用程式的前端程式碼組建 | 支援多個併發前端管道<br>比完整堆疊部署快得多 |
| 生產或非生產 | 部署 | Web層配置 | 部署HTTPD/Dispatcher設定 | 在幾分鐘內完成部署 |
| 非生產 | 程式碼品質 | 完整堆疊 | 在無需部署的完整堆疊程式碼上執行程式碼品質掃描 | 支援多個管道 |
| 非生產 | 程式碼品質 | 前端 | 在前端程式碼上執行程式碼品質掃描，而不需部署 | 支援多個管道 |
| 非生產 | 程式碼品質 | Web層配置 | 在不部署的情況下，對Dispatcher設定執行程式碼品質掃描 | 支援多個管道 |

下圖說明Cloud Manager的管道設定，包括傳統、單一前端存放庫或獨立的前端存放庫設定。

![Cloud Manager管道設定](/help/implementing/cloud-manager/assets/configure-pipeline/cm-setup.png)

## 全堆疊管道 {#full-stack-pipeline}

完整堆疊管道可同時將後端程式碼、前端程式碼和網頁層組態部署至AEM執行階段。

* 後端代碼 — 不可變內容，例如Java代碼、OSGi配置、重新指向以及可變內容
* 前端程式碼 — 應用程式UI資源，例如JavaScript、CSS、字型
* Web層配置 — HTTPD/Dispatcher配置

完整堆疊管道代表「uber」管道，可同時執行所有作業，同時讓使用者可以選擇分別透過前端管道和網頁層設定管道，以專門部署其前端程式碼或Dispatcher設定。

完整堆疊管道封裝前端程式碼(JavaScript/CSS)為 [AEM用戶端程式庫。](/help/implementing/developing/introduction/clientlibs.md)

如果 [網站層組態管道](#web-tier-config-pipelines) 未配置。

適用下列限制。

* 使用者必須以 **部署管理員** 角色來設定或執行管道。
* 在任何時候，每個環境都只能有一個完整堆疊管道。

此外，請注意，如果您選擇引入 [網頁層配置管道。](#web-tier-config-pipelines)

* 如果對應的Web層配置管道存在，則環境的完整堆疊管道將忽略Dispatcher配置。
* 如果環境的對應Web層設定管道不存在，則使用者可以設定完整堆疊管道，包括或忽略Dispatcher設定。

完整堆疊管道可以是程式碼品質管道或部署。

## 前端管道 {#front-end}

前端程式碼是任何以靜態檔案呈現的程式碼。 它與AEM提供的UI程式碼不同，可能包含網站主題、客戶定義的SPA、Firefly SPA和其他解決方案。

前端管道可讓後端開發非同步加速前端程式碼部署，進而協助您的團隊簡化您的設計和開發流程。 此專用管道會將JavaScript和CSS部署至AEM發佈層作為主題，產生新的主題版本，可從AEM傳送的頁面參照。

>[!IMPORTANT]
>
>您必須使用AEM版本 `2021.10.5933.20211012T154732Z ` 或更高版本，並啟用AEM Sites以運用前端管道。

>[!NOTE]
>
>使用 **部署管理員** 角色可以同時建立和運行多個前端管道。
>
>但是，每個方案（所有類型）的管道數上限為300個。 前端程式碼品質或前端部署管道皆可。

前端管道可以是程式碼品質管道或部署。

### 配置前端管道之前 {#before-start}

在配置前端管道之前，請查看 [AEM快速網站建立歷程](/help/journey-sites/quick-site/overview.md) 以取得簡單易用的AEM快速網站建立工具的端對端指南。 此歷程將協助您簡化前端開發，並讓您無需後端AEM知識即可快速自訂網站。

### 配置前端管道 {#configure-front-end}

要了解如何配置前端管道，請參閱以下文檔。

* [新增生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [新增非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)

### 使用前端管道開發網站 {#developing-with-front-end-pipeline}

利用前端管道，前端開發人員可獲得更多獨立性，並加快開發過程。

請參閱該文檔 [使用前端管道開發網站](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) 以了解此程式的運作方式，並注意一些事項，以充分發揮此程式的潛能。

### 配置全堆棧管道 {#configure-full-stack}

若要了解如何設定完整堆疊管道，請參閱下列檔案。

* [新增生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [新增非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)


## Web層配置管道 {#web-tier-config-pipelines}

Web層配置管道可將HTTPD/Dispatcher配置與其他程式碼變更脫鈎，從而將其獨佔部署至AEM執行階段。 這是簡化的管道，可讓只想部署Dispatcher設定變更的使用者，這種加速方式只需幾分鐘即可完成。

>[!TIP]
>
>使用Web層配置管道，您可以選擇將Web配置儲存在與完整堆棧管道相同的源位置或不同位置，具體取決於哪種結構更適合您的項目。

適用下列限制。

* 您必須使用AEM版本 `2021.12.6151.20211217T120950Z` 或更新版本，以利用web層配置管道。
* 您必須 [選擇加入dispatcher工具的彈性模式](/help/implementing/dispatcher/disp-overview.md#validation-debug) 以利用web層配置管道。
* 使用者必須以 **部署管理員** 角色來設定或執行管道。
* 在任何時候，每個環境都只能有一個Web層配置管道。
* 當其對應的完整堆棧管道運行時，用戶無法配置Web層配置管道。
* Web層結構必須遵循檔案中定義的靈活模式結構 [雲端中的Dispatcher。](/help/implementing/dispatcher/disp-overview.md#validation-debug)

此外，請注意 [完整堆棧管道](#full-stack-pipeline) 引入web層管道時會有行為。

* 如果尚未針對環境設定Web層設定管道，則使用者可在設定其對應的完整堆疊管道時進行選取，以在執行和部署期間納入或忽略Dispatcher設定。
* 為環境配置Web層配置管道後，其對應的完整堆棧管道（如果存在）將在執行和部署期間忽略調度程式配置。
* 刪除Web層配置管道後，其對應的完整堆棧管道將會重設，以在其執行期間部署Dispatcher設定。

Web層配置管道可以是代碼質量或部署類型。

### 配置Web層配置管道 {#configure-web-tier-config-pipelines}

要了解如何配置Web層配置管道，請參閱以下文檔。

* [新增生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [新增非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)
