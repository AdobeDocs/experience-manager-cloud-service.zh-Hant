---
title: CI-CD管道
description: 請詳閱本頁，了解Cloud Manager CI-CD管道
index: true
source-git-commit: 45cb3ea26a86de07f98e576a23542e250c99291f
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 0%

---


# Cloud Manager CI-CD管道 {#intro-cicd}

## 簡介 {#introduction}

Cloud Manager中的CI/CD管道可透過某種事件觸發，例如來自原始碼存放庫的提取請求，即程式碼變更，或是符合發行順序的某種定期排程。

>[!NOTE]
>若要設定管道，您必須：
>* 定義將啟動管道的觸發器
>* 定義控制生產部署的參數
>* 配置效能測試參數


在Cloud Manager中，有兩種管道：

* [生產管道](#prod-pipeline)
* [非生產管道](#non-prod-pipeline)

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/ci-cd-config1.png)


## 生產管道 {#prod-pipeline}

生產管道是專門建置的管道，包含一系列協調步驟，可將原始碼一直帶入生產環境。 這些步驟包括首先構建、打包、測試、驗證和部署到所有階段環境中。 不消說，只有建立生產和預備環境集後，才能新增生產管道。

請參閱 [設定生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) 以取得更多詳細資訊。


## 非生產管道 {#non-prod-pipeline}

非生產管道旨在執行程式碼品質掃描，或將原始碼部署至開發環境。

請參閱 [設定非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) 以取得更多詳細資訊。

## 了解Cloud Manager中的CI-CD管道 {#understand-pipelines}

下表匯總了Cloud Manager中的所有管道及其使用情況。

| 管線類型 | 部署或程式碼品質 | 原始碼 | 使用時機 | 我應何時使用或為何使用？ |
|--- |--- |--- |---|---|
| 生產或非生產 | 部署 | 前端 | 部署時間快。<br>可以為每個環境配置多個前端管道並行運行。<br>前端管道組建會將組建推出至儲存空間。 提供html頁面時，可參考CDN會以此儲存作為來源提供的前端程式碼靜態檔案。 | 僅部署包含一個或多個客戶端UI應用程式的前端代碼。 前端程式碼是任何以靜態檔案呈現的程式碼。 它與AEM提供的UI程式碼不同。 其中包括Sites主題、客戶定義的SPA、Firefly SPA和任何其他解決方案。<br>必須使用AEM 2021.10.5933.20211012T154732Z版 |
| 生產或非生產 | 部署 | 完整堆棧 | 當前端管道尚未採用時。<br>若是前端程式碼必須與AEM伺服器程式碼部署的時間完全相同， | 部署AEM伺服器代碼（不可變內容、Java代碼、OSGi配置、HTTPD/dispatcher配置、重新指向、可變內容、字型） — 同時包含一個或多個AEM伺服器應用程式。 |
| 非生產 | 程式碼品質 | 前端 | 讓Cloud Manager進行評估。 無需進行部署，即可成功建置並提升程式碼品質。<br>可以配置和運行多個管道。 | 在前端程式碼上執行程式碼品質掃描。 |
| 非生產 | 程式碼品質 | 完整堆棧 | 讓Cloud Manager進行評估。 無需進行部署，即可成功建置並提升程式碼品質。<br>可以配置和運行多個管道。 | 對完整堆疊程式碼執行程式碼品質掃描。 |


下圖說明Cloud Manager管道設定，包含傳統、單一前端存放庫或獨立的前端存放庫設定：

![](/help/implementing/cloud-manager/assets/configure-pipeline/cm-setup.png)

## Cloud Manager前端管道 {#front-end}

前端管道可協助您的團隊簡化您的設計和開發流程，方法是啟用用於部署前端代碼的加速前端管道。 這個有區別的管道會將JavaScript和CSS部署至AEM發佈層，作為主題，產生新的主題版本，可從AEM執行階段傳送的頁面參照。 前端程式碼是任何以靜態檔案呈現的程式碼。 它與AEM提供的UI程式碼不同。 其中包括Sites主題、客戶定義的SPA、Firefly SPA和任何其他解決方案。

>[!IMPORTANT]
>您必須使用AEM版本 `2021.10.5933.20211012T154732Z ` 以利用前端管道。

>[!NOTE]
>以部署管理員角色登錄的用戶可以同時建立和運行多個前端管道。 但是，每個方案（所有類型）的管道數上限為300個。

這些可以是前端代碼質量或前端部署管道類型。

### 配置前端管道之前 {#before-start}

開始配置前端管道之前，請參見 [AEM快速網站建立歷程](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites-journey/quick-site/overview.html) 透過簡單易用的AEM快速網站建立工具，提供端對端工作流程。 本檔案網站可協助您簡化AEM網站的前端開發，並在不具備AEM後端知識的情況下快速自訂網站。

### 配置前端管道 {#configure-front-end}

要了解如何配置前端管道，請參閱：

* [新增生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [新增非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)

## 完整堆棧管道 {#full-stack-pipeline}

完整堆疊管道可讓使用者選擇同時部署後端、前端和HTTPD/Dispatcher設定。  它會將程式碼和內容部署至AEM執行階段，包括封裝為AEM用戶端程式庫的前端程式碼(JavaScript/CSS)。 如果未配置Web層管道，則可部署Web層配置。 這代表「uber」管道，同時讓使用者可以選擇分別透過前端管道和網頁層組態管道，以專門部署其前端程式碼或調度程式設定。

將適用下列限制：

1. 用戶必須以部署管理器身份登錄才能配置或運行管道。

1. 在任何時候，每個環境都只能有一個完整堆疊管道。

1. 如果環境的對應Web層配置管道不存在，則用戶可以為環境配置完全堆棧管道以忽略或不忽略調度程式配置。

1. 如果環境的對應Web層配置管道存在，則環境的完整堆疊管道將忽略調度程式配置。

這些類型可以是「完整堆疊 — 程式碼品質」或「完整堆疊 — 部署」管道。

### 配置完整堆棧管道 {#configure-full-stack}

若要了解如何設定完整堆疊管道，請參閱：

* [新增生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [新增非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)