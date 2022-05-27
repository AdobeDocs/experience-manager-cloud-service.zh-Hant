---
title: 如何將所有內容放在一起 — 您的應用和您的內容以無AEM頭
description: 在「無頭開發AEM者之旅」的這一部分，瞭解如何利用您的項目（包括內容碎片、GraphQL調用、REST API調用和應用程式），並為其投入使用做好準備。
exl-id: bece84ad-4c8c-410c-847e-9ef3f79970cb
source-git-commit: 270eb35023e34eed2cd17674372794c6c2cc7757
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 0%

---

# 如何將所有內容放在一起 — 您的應用和您的內容以無AEM頭 {#put-it-all-together}

在 [無AEM頭開發者之旅](overview.md)，您將熟悉如何使用開發工具AEM和無頭SDK將應用程式組合在一起。

## 到目前為止的故事 {#story-so-far}

在前一篇無頭旅AEM程中， [如何通過AEM AssetsAPI更新您的內容](update-your-content.md) 您已經學會了如何通過API更新現有AEM的無頭內容，您現在應：

* 瞭解AEM AssetsHTTP API。

## 目標 {#objective}

本文旨在幫助您瞭解如何通過以下方式將無AEM頭應用程式放在一起：

* 瞭解無AEM頭SDK和所需的開發工具
* 設定本地開發運行時以在開始運行之前模擬內容
* 瞭解內AEM容複製基礎知識

## SDKAEM {#the-aem-sdk}

SDKAEM用於生成和部署自定義代碼。 它是您在投入使用前開發和test無頭應用程式所需的主要工具。 它包含以下對象：

* 快速啟動jar — 一個可執行的jar檔案，可用於設定作者和發佈實例
* Dispatcher工具 — Dispatcher模組及其對基於Windows和UNIX®的系統的依賴項
* Java™ API Jar - Java™ Jar/Maven依賴項，它公開了所有允許的可用於開發的Java™ API AEM
* Javadocjar - Java™ APIjar的javadoc

## 無AEM頭SDK {#the-aem-headless-sdk}

與AEMSDK不同AEM, **無頭SDK** 是一組庫，客戶端可以使用這些庫通過HTTP快AEM速方便地與Headless API交互。

有關無頭SDK的AEM詳細資訊，請參見 [此處](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/how-to/aem-headless-sdk.html?lang=en)。

## 其他開發工具 {#additional-development-tools}

除了AEMSDK之外，您還需要其他工具來方便本地開發和測試代碼和內容：

* Java™
* 蠢貨
* 阿帕奇·馬文
* Node.js庫
* 您選擇的IDE

因AEM為是Java™應用程式，您需要安裝Java™和Java™ SDK以支援as a Cloud Service的開AEM發。

Git是您用來管理原始碼管理和檢入對Cloud Manager的更改，然後將其部署到生產實例的內容。

使AEM用Apache Maven生成從Maven Project原型AEM生成的項目。 所有主要IDE都為Maven提供整合支援。

Node.js是JavaScript運行時環境，用於處理項目的AEM前端資產 `ui.frontend` 子項目。 Node.js與npm一起分發，是事實上的Node.js包管理器，用於管理JavaScript依賴項。

## 系統AEM元件概覽 {#components-of-an-aem-system-at-a-glance}

接下來，我們來看一下環境的組成部AEM分。

完整的AEM環境由Author 、 Publish和Dispatcher組成。 這些相同的元件在本地開發運行時可用，以便您更輕鬆地預覽代碼和內容，然後才能投入使用。

* **作者服務** 是內部用戶建立、管理和預覽內容的位置。

* **發佈服務** 被認為是「即時」環境，通常是最終用戶與之交互的內容。 在作者服務上編輯和批准內容後，內容將分發到發佈服務。 使用無頭應用程式的最AEM常見部署模式是讓應用程式的生產版本連接到AEM發佈服務。

* **調度員** 是一個通過Dispatcher模組增強的靜AEM態Web伺服器。 它快取由發佈實例生成的網頁以提高效能。

## 本地開發工作流 {#the-local-development-workflow}

本地開發項目是基於Apache Maven開發的，使用Git進行原始碼管理。 為了更新項目，開發人員可以使用其首選的整合開發環境，如Eclipse、Visual Studio代碼或IntelliJ等。

要test將由無頭應用程式接收的代碼或內容更新，必須將更新部署到本地運行時AEM，其中包括作者的本地實例AEM和發佈服務。

請務必注意本地運行時中每個元件之間的區AEM別，因為在最重要的位置test更新非常重要。 例如，test內容更新作者或test發佈實例上的新代碼。

在生產系統中， Dispatcher和http Apache伺服器將始終位於發佈實例AEM前面。 它們為系統提供快取和安AEM全服務，因此對Dispatchertest代碼和內容更新也至關重要。

## 使用本地開發環境本地預覽代碼和內容 {#previewing-your-code-and-content-locally-with-the-local-development-environment}

為了準備啟動AEM您的無頭項目，您需要確保項目的所有組成部分都運行良好。

要做到這一點，你必須把所有東西都放在一起：代碼、內容、配置，並在本地開發環境中test它，以便進行即時準備。

地方發展環境由三個主要領域組成：

1. 項AEM目 — 將包含開發人員將要處理的所AEM有自定義代碼、配置和內容
1. 本地AEM運行時 — 作者的本AEM地版本和發佈服務，將用於從項目部署代AEM碼
1. 本地Dispatcher運行時 — 包括Dispatcher模組的Apache httpd Web伺服器的本地版本

設定本地開發環境後，您可以通過本地部署靜態節點伺服器來模擬內容服務到React應用。

為了更深入地瞭解設定本地開發環境以及內容預覽所需的所有相關性，請參閱 [生產部署文檔](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/production-deployment.html?lang=en#prerequisites)。

## 下一步 {#whats-next}

現在，您已完成了「無頭開發AEM者之旅」的這一部分，您應：

* 熟悉開發工AEM具
* 瞭解本地開發工作流

您應繼續無AEM頭之旅，下次查看文檔 [如何與無頭應用程式一起生活](/help/journey-headless/developer/go-live.md) 讓你的&quot;無頭AEM計畫&quot;實現！

## 其他資源 {#additional-resources}

* [AEMas a Cloud ServiceSDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
* [設定本地環AEM境](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html)
* [用AEM於客戶端瀏覽器(JavaScript)的無頭SDK](https://github.com/adobe/aem-headless-client-js)
* [用AEM於server-side/Node.js的無頭SDK(JavaScript)](https://github.com/adobe/aem-headless-client-nodejs)
* [用AEM於Java™的無頭SDK](https://github.com/adobe/aem-headless-client-java)

