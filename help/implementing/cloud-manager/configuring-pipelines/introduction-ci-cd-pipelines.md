---
title: CI/CD 管道
description: 了解 Cloud Manager 的 CI/CD 管道以及如何使用它們來有效地部署您的計劃碼。
index: true
exl-id: 40d6778f-65e0-4612-bbe3-ece02905709b
source-git-commit: 6c246444f48440c64af0951e75f2071c00e477fa
workflow-type: tm+mt
source-wordcount: '1377'
ht-degree: 100%

---

# Cloud Manager CI/CD 管道 {#intro-cicd}

了解 Cloud Manager 的 CI/CD 管道以及如何使用它們來有效地部署您的計劃碼。

## 簡介 {#introduction}

Cloud Manager 中的 CI/CD 管道是一種從源存放庫構建計劃碼並將其部署到環境的機制。管道可以由事件觸發，例如來自源計劃碼存放庫的拉取請求 (即計劃碼更改)，也可以定期觸發以匹配發布節奏。

若要配置管道，您必須：

* 定義將啟動管道的觸發器。
* 定義控制生產部署的參數。
* 設定效能測試參數。

Cloud Manager 提供兩種類型的管道：

* [生產管道](#prod-pipeline)
* [非生產管道](#non-prod-pipeline)

![管道類型](/help/implementing/cloud-manager/assets/configure-pipeline/ci-cd-config1.png)

## 影片總覽 {#video}

如需快速了解管道類型，請觀看此短影片。

>[!VIDEO](https://video.tv.adobe.com/v/342363)

## 生產管道 {#prod-pipeline}

生產管道是專門構建的管道，其中包括一系列精心安排的步驟，用於部署來源計劃碼以供生產使用。這些步驟包括首先構建、打包、測試、驗證和部署到所有暫存環境中。因此，只有在建立了一組生產和中繼環境後，才能新增生產管道。

>[!TIP]
>
>如需了解詳細資訊，請參閱文件：[設定非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)。

## 非生產管道 {#non-prod-pipeline}

非生產管道主要用於執行計劃碼品質掃描或將原始計劃碼部署到開發環境中。

>[!TIP]
>
>如需了解詳細資訊，請參閱文件：[設定非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)。

## 計劃碼來源 {#code-sources}

除了生產和非生產之外，管道還可以透過它們部署的計劃碼類型來區分。

* **[完整堆疊計劃碼管道](#full-stack-pipeline)** - 同時部署包含一個或多個 AEM 伺服器應用程序以及 HTTPD/Dispatcher 配置的後端和前端計劃碼構建
* **[前端計劃碼管道](#front-end)** - 部署包含一個或多個用戶端 UI 應用計劃的前端計劃碼建置。
* **[Web 層設定管道](#web-tier-config-pipelines)** - 部署 HTTPD/Dispatcher 設定。

這些將在本文件後面詳細描述。

### 了解 Cloud Manager 中的 CI-CD 管道 {#understand-pipelines}

下表總結了 Cloud Manager 中可用的所有管道及其用途。

| 管道類型 | 部署或計劃碼品質 | 原始碼 | 用途 | 附註 |
|--- |--- |--- |---|---|
| 生產或非生產 | 部署 | 完整堆疊 | 同時部署後端和前端計劃碼構建以及 HTTPD/Dispatcher 配置 | 當前端計劃碼必須與 AEM 伺服器計劃碼同時部署時。<br>當尚未採用前端管道或 Web 層配置管道時。 |
| 生產或非生產 | 部署 | 前端 | 部署包含一個或多個客戶端 UI 應用程序的前端計劃碼建構。 | 支援多個並發的前端管道<br>比完整堆疊部署快得多 |
| 生產或非生產 | 部署 | Web 層設定 | 部署 HTTPD/Dispatcher 配置 | 幾分鐘內部署 |
| 非生產 | 計劃碼品質 | 完整堆疊 | 無需部署即可對完整堆疊計劃碼執行計劃碼品質掃描 | 支援多管道 |
| 非生產 | 計劃碼品質 | 前端 | 無需部署即可對前端計劃碼執行計劃碼品質掃描 | 支援多管道 |
| 非生產 | 計劃碼品質 | Web 層設定 | 在沒有部署的情況下對 Dispatcher 配置執行計劃碼品質掃描 | 支援多管道 |

下圖說明了 Cloud Manager 的管道配置以及傳統的單一前端存放庫或獨立的前端存放庫設定。

![Cloud Manager 管道配置](/help/implementing/cloud-manager/assets/configure-pipeline/cm-setup.png)

## 完整堆疊管道 {#full-stack-pipeline}

完整堆疊管道同時將後端計劃碼、前端計劃碼和 Web 層配置部署到 AEM 執行時。

* 後端計劃碼 - 不可變內容，例如 Java 計劃碼、OSGi 配置、repoinit 以及可變內容
* 前端計劃碼 - 應用程序 UI 資源，例如 JavaScript、CSS、字體
* Web 層設定管道 - 部署 HTTPD/Dispatcher 設定。

完整堆疊管道代表“超級”管道，一次完成所有工作，同時為使用者提供分別透過前端管道和 Web 層配置管道專門部署其前端計劃碼或 Dispatcher 配置的選項。

完整堆疊管道將前端計劃碼（JavaScript/CSS）封裝為[AEM 客戶端庫。](/help/implementing/developing/introduction/clientlibs.md)

完整堆疊管道可以部署 Web 層配置，如果[Web 層配置管道](#web-tier-config-pipelines)未配置。

以下限制適用。

* 使用者必須使用&#x200B;**部署管理器**&#x200B;角色以配置或執行管道。
* 在任何時候，每個環境只能有一個完整堆疊管道。

此外，如果您選擇引入一個[Web 層配置管道。](#web-tier-config-pipelines)

* 如果存在相應的 Web 層配置管道，則環境的完整堆疊管道將忽略 Dispatcher 配置。
* 如果環境對應的 Web 層配置管道不存在，使用者可以配置完整堆疊管道包括或忽略 Dispatcher 配置。

完整堆疊管道可以是計劃碼品質管道或部署。

## 前端管道 {#front-end}

前端計劃碼是用作靜態文件的任何計劃碼。它獨立於 AEM 提供的 UI 計劃碼，可能包括網站主題、客戶定義的 SPA、Firefly SPA 和其他解決方案。

前端管道透過啟用與後端開發異步的前端計劃碼的加速部署，幫助您的團隊簡化您的設計和開發流程。此專用管道將 JavaScript 和 CSS 作為主題部署到 AEM 分發層，從而產生一個新的主題版本，可以從 AEM 提供的頁面中引用。

>[!IMPORTANT]
>
>您必須使用 AEM 版本 `2021.10.5933.20211012T154732Z ` 或更高版本，並啟用 AEM Sites 以利用前端管道。

>[!NOTE]
>
>一個使用者&#x200B;**部署管理器**&#x200B;角色可以同時建立和執行多個前端管道。
>
>但是，每個程序（所有類型）最多有 300 個管道。這些可以是前端計劃碼品質或前端部署管道。

前端管道可以是計劃碼品質管道或部署。

### 配置前端管道之前 {#before-start}

在設定前端管道之前，請參閱 [AEM Quick Site 建立歷程](/help/journey-sites/quick-site/overview.md)，以透過易於使用的 AEM Quick Site 建立工具取得端到端指南。此歷程可幫助您簡化 AEM 網站的前端開發，讓您無需 AEM 後端知識即可快速自訂網站。

### 配置前端管道 {#configure-front-end}

要了解如何配置前端管道，請參閱以下文件。

* [新增生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [新增非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)

### 使用前端管道開發 Sites {#developing-with-front-end-pipeline}

有了前端流水線，給前端開發者更多的獨立性，可以加快開發進程。

請參考文件[使用前端管道開發 Sites](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) 了解此過程的工作原理以及需要注意的一些注意事項，以充分發揮此過程的潛力。

### 正在設定完整堆疊管道 {#configure-full-stack}

要了解如何配置完整堆疊管道，請參閱以下文件。

* [新增生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [新增非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)


## 網頁層級設定管道 {#web-tier-config-pipelines}

Web 層配置管道透過將 HTTPD/Dispatcher 配置與其他計劃碼更改分離，從而能夠將 HTTPD/Dispatcher 配置以獨占方式部署到 AEM 執行時。它是一個簡化的管道，為希望僅部署調度程序配置更改的使用者提供了一種在幾分鐘內完成的加速方法。

>[!TIP]
>
>使用 Web 層配置管道，您可以選擇將 Web 配置存儲在與完整堆棧管道相同的源位置或不同位置，具體取決於哪種結構更適合您的項目。

以下限制適用。

* 您必須使用 AEM 版本`2021.12.6151.20211217T120950Z`或更新以利用 Web 層配置管道。
* 你必須[選擇使用調度工具的靈活模式](/help/implementing/dispatcher/disp-overview.md#validation-debug)利用 Web 層配置管道。
* 使用者必須使用&#x200B;**部署管理器**&#x200B;角色以配置或執行管道。
* 在任何時候，每個環境只能有一個完整堆疊設定管道。
* 當相應的完整堆疊管道正在執行時，使用者無法配置 Web 層配置管道。
* Web 層結構必須遵循文件中定義的靈活模式結構[雲端中的調度員。](/help/implementing/dispatcher/disp-overview.md#validation-debug)

此外，如果您選擇引入一個[Web 層配置管道。](#full-stack-pipeline)

* 如果尚未為環境配置 Web 層配置管道，則使用者可以在配置其對應的完整堆疊管道時進行選擇，以在執行和部署期間包括或忽略 Dispatcher 配置。
* 為環境配置了 Web 層設定管道後，對應的全堆疊管道 (如果存在) 將在執行和部署期間忽略調度程序配置。
* 一旦 Web 層配置管道被刪除，它對應的完整堆疊管道將被重置以在其執行期間部署 Dispatcher 配置。

Web 層配置管道可以是計劃碼品質或部署類型。

### 正在設定網頁層級設定管道 {#configure-web-tier-config-pipelines}

要了解如何配置網頁層級設定檔完整堆疊管道，請參閱以下文件。

* [新增生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [新增非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)
