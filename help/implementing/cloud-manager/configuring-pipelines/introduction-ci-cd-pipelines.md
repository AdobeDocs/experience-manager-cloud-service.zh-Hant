---
title: CI/CD管道
description: 瞭解Cloud Manager的CI/CD管道，以及如何使用這些管道來高效地部署代碼。
index: true
exl-id: 40d6778f-65e0-4612-bbe3-ece02905709b
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1364'
ht-degree: 0%

---

# Cloud Manager CI/CD管道 {#intro-cicd}

瞭解Cloud Manager的CI/CD管道，以及如何使用這些管道來高效地部署代碼。

## 簡介 {#introduction}

Cloud Manager中的CI/CD管道是一種機制，用於從源儲存庫生成代碼並將其部署到環境。 管道可以由事件(如來自原始碼儲存庫的拉取請求（即代碼更改）)或常規計畫觸發以匹配發行代碼。

要配置管道，必須：

* 定義將啟動管線的觸發器。
* 定義控制生產部署的參數。
* 配置效能test參數。

Cloud Manager提供兩種類型的管道：

* [生產管線](#prod-pipeline)
* [非生產管道](#non-prod-pipeline)

![管線類型](/help/implementing/cloud-manager/assets/configure-pipeline/ci-cd-config1.png)

## 生產管線 {#prod-pipeline}

生產管線是專門構建的管線，包括一系列精心安排的步驟，以部署原始碼以供生產使用。 這些步驟包括第一次構建、打包、測試、驗證和部署到所有過渡環境。 因此，只有建立一組生產和分段環境後，才能添加生產管道。

>[!TIP]
>
>請參閱文檔 [配置生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) 的子菜單。

## 非生產管道 {#non-prod-pipeline}

非生產流水線主要用於運行代碼質量掃描或將原始碼部署到開發環境。

>[!TIP]
>
>請參閱文檔 [配置非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) 的子菜單。

## 代碼源 {#code-sources}

除了生產和非生產，管道還可以根據它們部署的代碼類型進行區分。

* **[完整堆棧管線](#full-stack-pipeline)**  — 同時部署包含一個或多個伺服器應用程式以及HTTPD/AEMDispatcher配置的後端和前端代碼生成
* **[前端管線](#front-end)**  — 部署包含一個或多個客戶端UI應用程式的前端代碼生成
* **[Web層配置管道](#web-tier-config-pipelines)**  — 部署HTTPD/Dispatcher配置

本文檔稍後將詳細介紹這些內容。

### 瞭解Cloud Manager中的CI-CD管道 {#understand-pipelines}

下表匯總了Cloud Manager中可用的所有管道及其使用實例。

| 管線類型 | 部署或代碼質量 | 原始碼 | 目的 | 附註 |
|--- |--- |--- |---|---|
| 生產或非生產 | 部署 | 完整堆棧 | 同時部署後端和前端代碼生成以及HTTPD/Dispatcher配置 | 當前端代碼必須與伺服器代碼同時部AEM署時。<br>當前端管道或Web層配置管道尚未採用時。 |
| 生產或非生產 | 部署 | 前端 | 部署包含一個或多個客戶端UI應用程式的前端代碼生成 | 支援多條併發前端管道<br>比完整堆棧部署快得多 |
| 生產或非生產 | 部署 | Web層配置 | 部署HTTPD/Dispatcher配置 | 在幾分鐘內部署 |
| 非生產 | 代碼質量 | 完整堆棧 | 在沒有部署的全堆棧代碼上運行代碼質量掃描 | 支援多條管線 |
| 非生產 | 代碼質量 | 前端 | 在前端代碼上運行代碼質量掃描，而不進行部署 | 支援多條管線 |
| 非生產 | 代碼質量 | Web層配置 | 在沒有部署的調度程式配置上運行代碼質量掃描 | 支援多條管線 |

下圖說明了Cloud Manager的管道配置，包括傳統的、單個前端儲存庫或獨立的前端儲存庫設定。

![Cloud Manager管道配置](/help/implementing/cloud-manager/assets/configure-pipeline/cm-setup.png)

## 全堆棧管道 {#full-stack-pipeline}

全棧管道將後端代碼、前端代碼和Web層配置同時部署到AEM所有運行時。

* 後端代碼 — 不可變的內容，如Java代碼、OSGi配置、重新點擊以及可變內容
* 前端代碼 — 應用程式UI資源，如JavaScript、CSS、字型
* Web層配置 — HTTPD/Dispatcher配置

整個堆棧管道代表一個&quot;uber&quot;管道，同時執行所有操作，同時為用戶提供通過前端管道和web層配置管道分別專門部署其前端代碼或Dispatcher配置的選項。

全棧管道包前端代碼(JavaScript/CSS) [客戶AEM端庫。](/help/implementing/developing/introduction/clientlibs.md)

如果Web層配置 [web層配置管道](#web-tier-config-pipelines) 未配置。

適用以下限制。

* 用戶必須使用 **部署管理器** 角色以配置或運行管道。
* 在任何時候，每個環境只能有一個完整堆棧管道。

此外，如果您選擇引入 [web層配置管道。](#web-tier-config-pipelines)

* 如果存在相應的Web層配置管道，則環境的完整堆棧管道將忽略Dispatcher配置。
* 如果環境的相應Web層配置管道不存在，則用戶可以配置包含或忽略Dispatcher配置的全堆棧管道。

全堆棧管道可以是代碼質量管道或部署。

## 前端管線 {#front-end}

前端代碼是用作靜態檔案的任何代碼。 它獨立於由提供的UI代AEM碼，可能包括站點主題、客戶定SPA義、FireflySPA和其他解決方案。

前端管道通過支援加快前端代碼非同步後端開發的部署，幫助您的團隊簡化設計和開發流程。 此專用管道將JavaScript和CSS作為主AEM題部署到分發層，從而生成新的主題版本，該版本可以從傳遞的頁面中引AEM用。

>[!IMPORTANT]
>
>您必須處於版AEM本 `2021.10.5933.20211012T154732Z ` 或者更高，因為AEM Sites能夠利用前端管道。

>[!NOTE]
>
>具有 **部署管理器** 角色可以同時建立和運行多個前端管道。
>
>但是，每個程式（跨所有類型）的管線最多限制為300條。 這些可以是前端代碼質量或前端部署管道。

前端管道可以是代碼質量管道或部署。

### 在配置前端管線之前 {#before-start}

在配置前端管道之前，請查看 [快速AEM建立站點](/help/journey-sites/quick-site/overview.md) 通過易於使用的快速站點建立工AEM具提供端到端指南。 此過程將幫助您簡化前端開發，並讓您無需任何後端知識即可快速定制您的站AEM點。

### 配置前端管道 {#configure-front-end}

要瞭解如何配置前端管道，請參閱以下文檔。

* [添加生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [添加非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)

### 利用前端管道開發站點 {#developing-with-front-end-pipeline}

通過前端管道，使前端開發者更加獨立，加快開發進程。

請參閱文檔 [利用前端管道開發站點](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) 瞭解此流程的工作方式以及需要注意的一些注意事項，以便充分利用此流程的潛力。

### 配置全堆棧管道 {#configure-full-stack}

要瞭解如何配置全堆棧管道，請參閱以下文檔。

* [添加生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [添加非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)


## Web層配置管道 {#web-tier-config-pipelines}

Web層配置管道通過將HTTPD/Dispatcher配置與其他代碼更改脫AEM離，使其可以獨佔部署到運行時。 它是一個簡化的管道，為希望只部署調度程式配置更改的用戶提供了一種快速方法，只需幾分鐘即可完成。

>[!TIP]
>
>使用Web層配置管道，您可以選擇將Web配置儲存在與整個堆棧管道相同的源位置或不同的位置，具體取決於哪種結構更適合您的項目。

適用以下限制。

* 您必須處於版AEM本 `2021.12.6151.20211217T120950Z` 或更新版本，以利用web層配置管道。
* 你必須 [選擇調度工具的靈活模式](/help/implementing/dispatcher/disp-overview.md#validation-debug) 以利用web層配置管道。
* 用戶必須使用 **部署管理器** 角色以配置或運行管道。
* 在任何時候，每個環境只能有一個Web層配置管道。
* 當Web層配置管線的相應全堆棧管線正在運行時，用戶無法配置該管線。
* Web層結構必須遵循文檔中定義的靈活模式結構 [雲中的調度程式。](/help/implementing/dispatcher/disp-overview.md#validation-debug)

另外，要瞭解 [完整堆棧管道](#full-stack-pipeline) 在引入Web層管道時將採取行為。

* 如果尚未為環境配置Web層配置管道，則用戶可以在配置其相應的全棧管道時進行選擇，以便在執行和部署期間包括或忽略Dispatcher配置。
* 為環境配置Web層配置管道後，其相應的全堆棧管道（如果存在）將在執行和部署期間忽略調度程式配置。
* 刪除Web層配置管線後，其相應的完整堆棧管線將被重置，以在Dispatcher配置執行期間部署。

Web層配置管道可以是代碼質量或部署類型。

### 配置Web層配置管道 {#configure-web-tier-config-pipelines}

要瞭解如何配置Web層配置管道，請參閱以下文檔。

* [添加生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [添加非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)
