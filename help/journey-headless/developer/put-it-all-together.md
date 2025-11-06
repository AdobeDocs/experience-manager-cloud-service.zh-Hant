---
title: 如何在 AEM Headless 中將您的應用程式和內容組合在一起
description: 在 AEM Headless 開發人員歷程的這一部分中，了解如何使用您的 AEM 專案 (包含內容片段)、GraphQL 呼叫、REST API 呼叫和您的應用程式，並為上線做好準備。
exl-id: bece84ad-4c8c-410c-847e-9ef3f79970cb
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 100%

---

# 如何在 AEM Headless 中將您的應用程式和內容組合在一起 {#put-it-all-together}

在 [AEM Headless 開發人員歷程](overview.md)的這一部分中，了解如何使用 AEM 開發工具和 Headless SDK 將您的應用程式組合在一起。

## 到目前為止 {#story-so-far}

在 AEM Headless 歷程的上一個文件「[如何透過 AEM Assets API 更新您的內容](update-your-content.md)」中，您已了解如何通過 API 更新 AEM 中現有的 Headless 內容，您現在應該：

* 了解 AEM Assets HTTP API。

## 目標 {#objective}

本文旨在透過以下方式幫助您了解如何將 AEM Headless 應用程式組合在一起：

* 了解 AEM Headless SDK 和所需的開發工具
* 設定本機開發執行階段以在上線前模擬您的內容
* 了解 AEM 內容複製基本知識

## AEM SDK {#the-aem-sdk}

AEM SDK 用於建置和部署自訂程式碼。它是您在上線前開發和測試 Headless 應用程式所需的主要工具。它都包含下列成品：

* Quickstart jar - 這是可執行的 jar 檔案，可用於設定編寫和發佈執行個體
* Dispatcher 工具 - Dispatcher 模組及其對基於 Windows 和 Unix® 系統的相依性
* Java™ API Jar - Java™ Jar/Maven 相依性公開了所有允許的 Java™ API，其可用於針對 AEM 進行開發
* Javadoc jar - Java™ API jar 的 javadoc

## AEM Headless SDK {#the-aem-headless-sdk}

與 AEM SDK 不同，AEM **Headless SDK** 是一組程式庫，用戶端可以使用這些程式庫透過 HTTP 快速輕鬆地與 AEM Headless API 互動。

如需詳細資訊，請參閱 [AEM Headless SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/aem-headless-sdk.html?lang=zh-Hant)。

## 其他開發工具 {#additional-development-tools}

除了 AEM SDK 之外，您還需要其他工具來協助您在本機開發和測試程式碼和內容：

* Java™
* Git
* Apache Maven
* Node.js 程式庫
* 您選擇的 IDE

由於 AEM 是 Java™ 應用程式，因此您需要安裝 Java™ 和 Java™ SDK 以支援開發 AEM as a Cloud Service。

Git 是您用來管理原始檔控制系統和簽入對 Cloud Manager 的變更，然後將它們部署到生產執行個體的工具。

AEM 使用 Apache Maven 建置從 AEM Maven 專案原型產生的專案。所有主要的 IDE 都提供對 Maven 的整合支援。

Node.js 是 JavaScript 執行階段環境，用於處理 AEM 專案 `ui.frontend`子專案的前端資產。Node.js 與 npm 一起傳遞，是事實上的 Node.js 封裝管理員，用於管理 JavaScript 相依性。

## AEM 系統元件一覽 {#components-of-an-aem-system-at-a-glance}

接下來，讓我們看看 AEM 環境的組成部分。

完整的 AEM 環境由編寫、發佈和 Dispatcher 組成。這些相同的元件在本機開發執行階段中可用，以方便您在上線前預覽您的程式碼和內容。

* **編寫服務**&#x200B;是內部使用者建立、管理和預覽內容的地方。

* **發佈服務**&#x200B;被認為是「即時」環境，通常是一般使用者與其互動。內容在編寫服務上經編輯和核准後，將傳遞到發佈服務。AEM Headless 應用程式最常見的部署模式是讓應用程式的生產版本連接到 AEM Publish 服務。

* **Dispatcher** 是靜態 Web 伺服器，增加了 AEM Dispatcher 模組。它快取發佈執行個體產生的網頁以提升效能。

## 本機開發工作流程 {#the-local-development-workflow}

本機開發專案以 Apache Maven 為基礎建置，並使用 Git 進行原始檔控制。若要更新專案，開發人員可以使用偏好的整合式開發環境，例如 Eclipse、Visual Studio Code 或 IntelliJ 等。

若要測試 Headless 應用程式取用的程式碼或內容更新，您必須將更新部署到本機 AEM 執行階段，其中包括 AEM 編寫和發佈服務的本機執行個體。

請務必注意本機 AEM 執行階段每個元件之間的區別，因為在與您的更新最有關係的地方測試它，這一點非常重要。例如，在編寫執行個體測試內容更新或在發佈執行個體測試新程式碼。

在生產系統中，Dispatcher 和 http Apache 伺服器一律位於 AEM 發佈執行個體的前面。它們為 AEM 系統提供快取和安全性服務，因此針對 Dispatcher 測試程式碼和內容更新是最重要的。

## 使用本機開發環境在本機預覽程式碼和內容 {#previewing-your-code-and-content-locally-with-the-local-development-environment}

若要讓 AEM Headless 專案準備好開始，您需要確保專案的所有組成部分都正常運作。

為此，您必須將所有項目放在一起：程式碼、內容和設定，並在本機開發環境中測試以準備好上線。

本機開發環境由三個主要區域組成：

1. AEM 專案 - 此專案包含 AEM 開發人員將要處理的所有自訂程式碼、設定和內容
1. 本機 AEM 執行階段 - AEM 編寫和發佈服務本機版本，用於從 AEM 專案部署程式碼
1. 本機 Dispatcher 執行階段 - 包含 Dispatcher 模型的 Apache htttpd 網頁伺服器本機版本

設定好本機開發環境後，您可以透過在本機部署靜態節點伺服器來模擬提供給 React 應用程式的內容。

<!-- THIS TOPIC IS 404. IT DOES NOT APPEAR IN THE TOC OR ANYWHERE ELSE To get a more in-depth look at setting up a local development environment and all dependencies needed for content preview, see [Production Deployment documentation](https://experienceleague.adobe.com/docs/experience-manager-learn/headless-tutorial/graphql/multi-step/production-deployment.html). -->

## 下一步 {#whats-next}

您已完成此部分的 AEM Headless 開發人員歷程，您應該：

* 熟悉 AEM 開發工具
* 了解本機開發工作流程

接下來查看文件[如何將 Headless 應用程式上線](/help/journey-headless/developer/go-live.md)繼續您的 AEM Headless 歷程，在其中您可實際將 AEM Headless 專案上線！

## 其他資源 {#additional-resources}

* [AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
* [設定本機 AEM 環境](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html?lang=zh-Hant)
* [適用於用戶端瀏覽器的 AEM Headless SDK (JavaScript)](https://github.com/adobe/aem-headless-client-js)
* [適用於伺服器端/Node.js 的 AEM Headless SDK (JavaScript)](https://github.com/adobe/aem-headless-client-nodejs)
* [適用於 Java™ 的 AEM Headless SDK](https://github.com/adobe/aem-headless-client-java)
* [AEM as a Headless CMS 簡介](/help/headless/introduction.md)
* [AEM 開發人員入口網站](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=zh-Hant)
* [AEM 中的 Headless 教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=zh-Hant)
