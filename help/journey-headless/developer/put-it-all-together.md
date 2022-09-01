---
title: 如何將所有內容放在一起 — 您的應用程式和AEM Headless中的內容
description: 在AEM無周邊開發人員歷程的這部分，了解如何帶您的AEM專案（包括內容片段、GraphQL呼叫、REST API呼叫和應用程式），並為其上線做準備。
exl-id: bece84ad-4c8c-410c-847e-9ef3f79970cb
source-git-commit: 421ad8506435e8538be9c83df0b78ad8f222df0c
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 0%

---

# 如何將所有內容放在一起 — 您的應用程式和AEM Headless中的內容 {#put-it-all-together}

在 [AEM Headless Developer Journey](overview.md)，您就能熟悉如何使用AEM開發工具和無頭式SDK，將應用程式整合在一起。

## 迄今為止的故事 {#story-so-far}

在AEM無頭歷程的上一份檔案中， [如何透過AEM Assets API更新您的內容](update-your-content.md) 您已學會如何透過API更新AEM中現有的無頭內容，現在應：

* 了解AEM Assets HTTP API。

## 目標 {#objective}

本文旨在協助您了解如何透過下列方式，將AEM無標題應用程式整合在一起：

* 了解AEM Headless SDK及所需的開發工具
* 設定本機開發執行階段，以在上線前模擬您的內容
* 了解AEM內容復寫基本知識

## AEM SDK {#the-aem-sdk}

AEM SDK可用來建置和部署自訂程式碼。 這是您在開發和測試無頭應用程式之前所需的主要工具。 它包含下列成品：

* Quickstart jar — 可執行的jar檔案，可用於設定作者和發佈執行個體
* Dispatcher工具 — 適用於Windows和UNIX®系統的Dispatcher模組及其相依性
* Java™ API Jar - Java™ Jar/Maven相依性，可公開可用於針對AEM進行開發的所有允許Java™ API
* Javadoc jar - Java™ API jar的javadoc

## AEM Headless SDK {#the-aem-headless-sdk}

與AEM SDK不同，AEM **無頭SDK** 是一組程式庫，供用戶端用來透過HTTP快速輕鬆與AEM Headless API互動。

如需AEM Headless SDK的詳細資訊，請參閱 [說明](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/aem-headless-sdk.html).

## 其他開發工具 {#additional-development-tools}

除了AEM SDK，您還需要其他工具來協助您在本機開發和測試程式碼和內容：

* Java™
* Git
* 阿帕奇·馬文
* Node.js程式庫
* 您選擇的IDE

由於AEM是Java™應用程式，因此您必須安裝Java™和Java™ SDK，才能支援AEM as a Cloud Service的開發。

您可使用Git來管理原始碼控制項，以及簽入Cloud Manager的變更，然後將其部署至生產執行個體。

AEM使用Apache Maven來建置從AEM Maven專案原型產生的專案。 所有主要IDE都為Maven提供整合支援。

Node.js是JavaScript執行階段環境，用於搭配AEM專案的前端資產使用 `ui.frontend` 子專案。 Node.js與npm一起分發，實際上是Node.js套件管理器，用於管理JavaScript相依性。

## AEM系統元件一覽 {#components-of-an-aem-system-at-a-glance}

接下來，我們來看看AEM環境的組成部分。

完整的AEM環境由製作、發佈和Dispatcher組成。 這些相同的元件會在本機開發執行階段中提供，讓您在上線前更輕鬆地預覽程式碼和內容。

* **作者服務** 是內部使用者建立、管理和預覽內容的位置。

* **發佈服務** 會視為「即時」環境，且通常是使用者與之互動的環境。 內容在Author服務上經過編輯和核准後，會分發至Publish服務。 AEM無頭式應用程式最常見的部署模式是讓生產版本的應用程式連線至AEM發佈服務。

* **Dispatcher** 是與AEM Dispatcher模組增強的靜態Web伺服器。 它會快取由發佈例項產生的網頁，以提升效能。

## 本機開發工作流程 {#the-local-development-workflow}

本機開發專案以Apache Maven為基礎，且使用Git進行原始碼控制。 為了更新專案，開發人員可使用其偏好的整合開發環境，例如Eclipse、Visual Studio Code或IntelliJ等。

若要測試無頭應用程式所擷取的程式碼或內容更新，您必須將更新部署至本機AEM執行階段，其中包括AEM製作和發佈服務的本機例項。

請務必注意本機AEM執行階段中每個元件之間的差異，因為在最重要的位置測試更新非常重要。 例如，在製作上測試內容更新，或在發佈例項上測試新程式碼。

在生產系統中，Dispatcher和http Apache伺服器一律會位於AEM發佈例項之前。 它們為AEM系統提供快取和安全性服務，因此也必須針對Dispatcher測試程式碼和內容更新。

## 使用本機開發環境在本機預覽您的程式碼和內容 {#previewing-your-code-and-content-locally-with-the-local-development-environment}

若要為啟動準備AEM無標題專案，您必須確定專案的所有組成部分都正常運作。

要做到這一點，你必須把所有事情放在一起：程式碼、內容和設定，並在本機開發環境中測試，以備上線準備。

地方發展環境由三個主要領域組成：

1. AEM專案 — 此專案包含AEM開發人員將要使用的所有自訂程式碼、設定和內容
1. 本機AEM執行階段 — 用於從AEM專案部署程式碼的AEM製作和發佈服務的本機版本
1. 本機Dispatcher執行階段 — 包含Dispatcher模組的Apache httpd網站伺服器的本機版本

設定本機開發環境後，您就可以在本機部署靜態節點伺服器，以模擬提供給React應用程式的內容。

<!-- THIS TOPIC IS 404. IT DOES NOT APPEAR IN THE TOC OR ANYWHERE ELSE To get a more in-depth look at setting up a local development environment and all dependencies needed for content preview, see [Production Deployment documentation](https://experienceleague.adobe.com/docs/experience-manager-learn/headless-tutorial/graphql/multi-step/production-deployment.html). -->

## 下一步 {#whats-next}

現在您已完成AEM Headless Developer Journey的這一部分，您應：

* 熟悉AEM開發工具
* 了解本機開發工作流程

繼續進行AEM無頭歷程，繼續檢閱此檔案 [如何與無頭應用程式一起運行](/help/journey-headless/developer/go-live.md) 您實際將AEM Headless專案上線的位置！

## 其他資源 {#additional-resources}

* [AEMas a Cloud ServiceSDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
* [設定本機AEM環境](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html)
* [適用於用戶端瀏覽器的AEM Headless SDK(JavaScript)](https://github.com/adobe/aem-headless-client-js)
* [AEM Headless SDK for server-side/Node.js(JavaScript)](https://github.com/adobe/aem-headless-client-nodejs)
* [AEM Headless SDK for Java™](https://github.com/adobe/aem-headless-client-java)

