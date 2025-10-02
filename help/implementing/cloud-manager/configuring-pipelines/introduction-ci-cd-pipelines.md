---
title: CI/CD管道簡介
description: 瞭解Cloud Manager的CI/CD管道以及如何使用它們來有效部署您的計畫碼。
index: true
exl-id: 40d6778f-65e0-4612-bbe3-ece02905709b
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: ac918008c3f99d74e01be59c9841083abf3604aa
workflow-type: tm+mt
source-wordcount: '1546'
ht-degree: 32%

---


# Cloud Manager CI/CD 管道 {#intro-cicd}

瞭解Cloud Manager的CI/CD （持續整合/持續傳遞）管道，以及如何使用它們來有效部署您的程式碼。

## CI/CD管道簡介 {#introduction}

Cloud Manager 中的 CI/CD 管道是一種從源存放庫構建程式碼並將其部署到環境的機制。事件會觸發管道，例如來自原始程式碼存放庫（例如Git）的提取請求（即程式碼變更）。 或者，可定期觸發以符合發行節奏。

若要設定管道，您必須執行下列操作：

* 定義啟動管道的觸發器。
* 定義控制生產部署的引數。
* 設定效能測試參數。

Cloud Manager 提供兩種類型的管道：

* [生產管道](#prod-pipeline)
* [非生產管道](#non-prod-pipeline)

![管道類型](/help/implementing/cloud-manager/assets/configure-pipeline/ci-cd-config1.png)

## 生產管道 {#prod-pipeline}

生產管道是專門構建的管道，其中包括一系列精心安排的步驟，用於部署來源程式碼以供生產使用。這些步驟包括首先建置、封裝、測試、驗證和部署到所有中繼環境中。因此，只有在建立一組生產和中繼環境後，才能新增生產管道。

>[!TIP]
>
>請參閱[設定生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)。

## 非生產管道 {#non-prod-pipeline}

非生產管道主要用於執行程式碼品質掃描或將原始程式碼部署到開發環境中。

>[!TIP]
>
>請參閱[設定非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)。

## 程式碼來源 {#code-sources}

除了生產和非生產環境外，管道還可能會因它們部署的計畫碼型別而異。

* **[完整棧疊管道](#full-stack-pipeline)** — 同時部署包含一個或多個AEM伺服器應用程式以及HTTPD/Dispatcher設定的後端和前端計畫碼建置。
* **[設定管道](#config-deployment-pipeline)** — 您可以快速部署功能（例如記錄轉送和清除相關的維護工作）的設定。 它也包含各種CDN （內容傳遞網路）設定，例如流量篩選規則，包括網頁應用程式防火牆(WAF)規則。 此外，您可以管理請求和回應轉換、來源選擇器、使用者端重新導向、錯誤頁面、CDN金鑰、清除API金鑰以及基本驗證。 如需詳細資訊，請參閱[使用設定管道](/help/operations/config-pipeline.md)。
* **[前端計畫碼管道](#front-end)** — 部署包含一個或多個使用者端使用者介面應用計畫的前端計畫碼建置。
* **[Web層設定管道](#web-tier-config-pipelines)** — 部署HTTPD/Dispatcher設定。

本檔案稍後將詳細介紹這些管道型別。

### 瞭解Cloud Manager中的CI-CD管道 {#understand-pipelines}

下表總結了Cloud Manager中可用的管道及其用途。

| 管道類型 | 部署或計畫碼品質 | Source程式碼 | 用途 | 附註 |
| --- | --- | --- | --- | ---|
| 生產或非生產 | 部署 | 完整堆疊 | 同時部署後端和前端程式碼構建以及 HTTPD/Dispatcher 配置 | 當前端計畫碼必須與AEM伺服器計畫碼同時部署時使用。 在尚未採用前端管道或Web層配置管道時使用。 |
| 生產或非生產 | 部署 | 前端 | 部署包含一個或多個客戶端 UI 應用程序的前端程式碼建構。 | 支援多個併發的前端管道<br>比完整棧疊部署快得多。 |
| 生產或非生產 | 部署 | Web層設定 | 部署 HTTPD/Dispatcher 配置 | 幾分鐘內部署 |
| 生產或非生產 | 部署 | 設定 | 為與CDN、記錄檔轉送和清除維護工作相關的許多功能[部署](/help/operations/config-pipeline.md)設定 | 幾分鐘內部署 |
| 非生產 | 程式碼品質 | 完整棧疊 | 無需部署即可對完整堆疊程式碼執行程式碼品質掃描 | 支援多管道 |
| 非生產 | 程式碼品質 | 前端 | 無需部署即可對前端程式碼執行程式碼品質掃描 | 支援多管道 |
| 非生產 | 程式碼品質 | Web層設定 | 無需部署即可對Dispatcher設定執行程式碼品質掃描 | 支援多管道 |

下圖說明了 Cloud Manager 的管道配置以及傳統的單一前端存放庫或獨立的前端存放庫設定。

![Cloud Manager 管道配置](/help/implementing/cloud-manager/assets/configure-pipeline/cm-setup.png)

## 完整棧疊管道 {#full-stack-pipeline}

完整棧疊管道同時將後端計畫碼、前端計畫碼和Web層配置部署到AEM執行階段。

* 後端程式碼 - 不可變內容，例如 Java 程式碼、OSGi 配置、repoinit 和可變內容
* 前端程式碼 - 應用程序 UI 資源，例如 JavaScript、CSS、字體
* Web 層設定 - HTTPD/Dispatcher 設定。

完整棧疊管道代表「uber」管道。 它可同時處理所有內容，同時也允許使用者單獨部署其前端計畫碼或Dispatcher設定。 此部署分別透過前端管道和Web層配置管道進行。

完整堆疊管道將前端程式碼 (JavaScript/CSS) 封裝為 [AEM 用戶端程式庫](/help/implementing/developing/introduction/clientlibs.md)。

完整堆疊管道可以部署 Web 層配置，如果 [Web 層配置管道](#web-tier-config-pipelines)未配置。

以下限制適用。

* 使用者必須使用&#x200B;**部署管理員**&#x200B;角色以配置或執行管道。
* 在任何時候，每個環境只能有一個完整堆疊管道。

此外，如果您選擇引入[Web層配置管道](#web-tier-config-pipelines)，請注意完整棧疊管道的行為。

* 如果存在對應的Web層配置管道，則環境的完整棧疊管道會忽略Dispatcher配置。
* 如果環境對應的Web層配置管道不存在，使用者可以將完整棧疊管道配置為包含或忽略Dispatcher配置。

完整堆疊管道可以是程式碼品質管道或部署。

### 設定完整棧疊管道 {#configure-full-stack}

請參閱[新增生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#full-stack-code)。
請參閱[新增非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code)。

## 設定管道 {#config-deployment-pipeline}

使用設定管道，您可以快速部署記錄轉送、清除相關維護任務和各種CDN設定的設定，包括流量篩選規則(例如WAF （Web應用程式防火牆）規則)。 此外，您可以管理請求和回應轉換、來源選擇器、使用者端重新導向、錯誤頁面、客戶管理的CDN金鑰、清除API金鑰以及基本驗證。

請參閱[使用設定管道](/help/operations/config-pipeline.md)以取得支援功能的完整清單，並瞭解如何管理存放庫中的設定，以便正確部署它們。

>[!NOTE]
>
>Edge Delivery設定管道沒有單獨的開發、測試和生產環境。 在AEM as a Cloud Service中，變更會經過開發、階段和生產等層級。 相反地，Edge Delivery設定管道會直接將其設定套用至在Cloud Manager中註冊的所有Edge Delivery Sites網域。 若要深入瞭解，請參閱[新增Edge Delivery管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md)。


### 設定設定管道 {#configure-config-deployment}

請參閱[新增生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#targeted-deployment)。
請參閱[新增非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#targeted-deployment)。

## 前端管道 {#front-end}

前端程式碼是用作靜態文件的任何程式碼。它獨立於 AEM 提供的 UI 程式碼，可能包括網站主題、客戶定義的 SPA、SPA 和其他解決方案。

前端管道透過啟用前端計畫碼的加速部署、與後端開發的非同步，幫助您的團隊簡化您的設計和開發流程。 此專用管道將JavaScript和CSS作為主題部署到AEM分發層，從而產生一個新的主題版本，可以從AEM提供的頁面中引用。

>[!NOTE]
>
>一個使用者&#x200B;**部署管理員**&#x200B;角色可以同時建立和執行多個前端管道。
>
>但是，每個計畫 (所有類型) 最多有 300 個管道。

前端管道可以是程式碼品質管道或部署管道。

### 配置前端管道之前 {#before-start}

在設定前端管道之前，請參閱 [AEM Quick Site 建立歷程](/help/journey-sites/quick-site/overview.md)，以透過易於使用的 AEM Quick Site 建立工具取得端到端指南。此歷程可幫助您簡化前端開發，並讓您無需後端AEM知識即可快速自訂網站。

### 設定前端管道 {#configure-front-end}

請參閱[新增生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)。
請參閱[新增非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)。

### 使用前端管道開發網站 {#developing-with-front-end-pipeline}

有了前端流水線，給前端開發者更多的獨立性，可以加快開發進程。

請參閱[使用前端管道開發Sites](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md)，瞭解此程式的運作方式以及需要注意的一些注意事項，以充分發揮此程式的潛力。

## Web層設定管道 {#web-tier-config-pipelines}

Web層配置管道允許將HTTPD/Dispatcher配置獨佔部署到AEM執行階段，將其與其他程式碼變更分離。 它是一個簡化的管道，為只想部署Dispatcher配置更改的使用者提供了一種在幾分鐘內完成的加速方法。

>[!TIP]
>
>Web層配置管道允許您將Web配置與完整棧疊管道儲存在相同或不同的源位置，具體取決於最適合您的專案結構的內容。

以下限制適用。

* 在AEM版本`2021.12.6151.20211217T120950Z`或更新版本上以使用Web層配置管道。
* [選擇加入Dispatcher工具的彈性模式](/help/implementing/dispatcher/disp-overview.md#validation-debug)以使用Web層設定管道。
* 使用者必須使用&#x200B;**部署管理員**&#x200B;角色以配置或執行管道。
* 在任何時候，每個環境只能有一個 Web 層配置管道。
* 當相應的完整棧疊管道正在執行時，使用者無法配置Web層配置管道。
* Web 層結構必須遵循靈活模式結構，如[雲端中的 Dispatcher](/help/implementing/dispatcher/disp-overview.md#validation-debug) 文件所定義。

此外，如果您選擇引入一個 [Web 層設定管道](#full-stack-pipeline)，請注意完整堆疊管道的運作方式。

* 如果沒有為環境設定Web層設定管道，使用者可以在設定完整棧疊管道時，選擇包含或忽略Dispatcher設定。 在執行和部署期間進行此選擇。
* 為環境設定Web層設定管道後，對應的完整棧疊管道（如果存在）會在執行和部署期間忽略Dispatcher設定。
* Web 層配置管道被刪除後，它對應的完整堆疊管道會重設以在其執行期間部署 Dispatcher 設定。

Web層設定管道可以是型別`Code quality`或`Deployment`。

### 設定Web層管道 {#configure-web-tier}

請參閱[新增生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#targeted-deployment)。
請參閱[新增非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#targeted-deployment)。

## 管道型別的影片概觀 {#video}

如需管道型別的快速概覽，請觀看以下影片（2分鐘、26秒）。

>[!VIDEO](https://video.tv.adobe.com/v/342363)
