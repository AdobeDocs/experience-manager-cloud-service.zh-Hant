---
title: 如何與無頭應用程式一起生活
description: 在「無頭開發者之旅」的這一部分AEM，瞭解如何即時部署無頭應用程式，方法是將本地代碼以Git格式使用，並將其移至Cloud Manager Git，以用於CI/CD管道。
exl-id: 81616e31-764b-44b0-94a6-3ae24ce56bf6
source-git-commit: 44b24a68e2b9a9abd2a9d609c3a28f6b90e492fa
workflow-type: tm+mt
source-wordcount: '1907'
ht-degree: 0%

---

# 如何與無頭應用程式一起生活 {#go-live}

在 [無AEM頭開發者之旅](overview.md)，瞭解如何通過將本地代碼以Git格式移至Cloud Manager Git以用於CI/CD管道，即時部署無頭應用程式。

## 到目前為止的故事 {#story-so-far}

在前一篇無頭旅AEM程中， [如何通過AEM AssetsAPI更新您的內容](update-your-content.md) 您已經學會了如何通過API更新現有AEM的無頭內容，您現在應：

* 瞭解AEM AssetsHTTP API。

本文基於這些基礎知識，因此您瞭解如何準備AEM自己的無頭項目來投入使用。

## 目標 {#objective}

本文檔可幫助您了AEM解無頭發佈流程，以及您在與應用程式共處之前需要注意的效能注意事項。

* 瞭解所需AEM的SDK和開發工具
* 設定本地開發運行時以在開始運行之前模擬內容
* 瞭解內AEM容複製和快取基礎知識
* 在啟動前保護並擴展應用程式
* 監視效能和調試問題

## SDKAEM {#the-aem-sdk}

SDKAEM用於生成和部署自定義代碼。 它是您在投入使用前開發和test無頭應用程式所需的主要工具。 它包含以下對象：

* 快速啟動jar — 一個可執行的jar檔案，可用於設定作者和發佈實例
* Dispatcher工具 — Dispatcher模組及其對基於Windows和UNIX的系統的依賴項
* Java API Jar - Java Jar/Maven依賴項，它顯示可用於開發的所有允許的Java API AEM
* Javadocjar - Java APIjar的javadoc

## 其他開發工具 {#additional-development-tools}

除了SDKAEM之外，您還需要其他工具來方便本地開發和測試代碼和內容：

* Java
* 蠢貨
* 阿帕奇·馬文
* Node.js庫
* 您選擇的IDE

因AEM為是Java應用程式，需要安裝Java和Java SDK來支援as a Cloud Service的開AEM發。

Git是您用來管理原始碼管理以及簽入對Cloud Manager的更改，然後將其部署到生產實例的。

使AEM用Apache Maven生成從Maven Project原型AEM生成的項目。 所有主要IDE都為Maven提供整合支援。

Node.js是JavaScript運行時環境，用於處理項目的AEM前端資產 `ui.frontend` 子項目。 Node.js與npm一起分發，是事實上的Node.js包管理器，用於管理JavaScript依賴項。

## 系統AEM元件概覽 {#components-of-an-aem-system-at-a-glance}

接下來，我們來看一下環境的組成部AEM分。

完整的AEM環境由Author 、 Publish和Dispatcher組成。 這些相同的元件將在本地開發運行時提供，以便您在開始使用前更輕鬆地預覽代碼和內容。

* **作者服務** 是內部用戶建立、管理和預覽內容的位置。

* **發佈服務** 被認為是「即時」環境，通常是最終用戶與之交互的內容。 在作者服務上編輯和批准內容後，內容將分發到發佈服務。 使用無頭應用程式的最AEM常見部署模式是讓應用程式的生產版本連接到AEM發佈服務。

* **調度員** 是隨調度器模組增強的靜AEM態web伺服器。 它快取由發佈實例生成的網頁以提高效能。

## 本地開發工作流 {#the-local-development-workflow}

本地開發項目是基於Apache Maven開發的，使用Git進行原始碼管理。 為了更新項目，開發人員可以使用其首選的整合開發環境，如Eclipse、Visual Studio代碼或IntelliJ等。

要test將由無頭應用程式接收的代碼或內容更新，您需要將更新部署到本地運行時AEM，其中包括作者的本地實例AEM和發佈服務。

請務必注意本地運行時中每個元件之間的區AEM別，因為在最重要的位置test更新非常重要。 例如，test內容更新作者或test發佈實例上的新代碼。

在生產系統中，調度程式和http Apache伺服器將始終位於發佈實例AEM前面。 它們為系統提供快取和安AEM全服務，因此test代碼和內容更新對調度程式也至關重要。

## 使用本地開發環境本地預覽代碼和內容 {#previewing-your-code-and-content-locally-with-the-local-development-environment}

為了準備啟動AEM您的無頭項目，您需要確保項目的所有組成部分都運行良好。

要做到這一點，你需要把所有東西都放在一起：代碼、內容和配置，並在本地開發環境中test它，以便進行即時準備。

地方發展環境由三個主要領域組成：

1. 項AEM目 — 將包含開發人員將要處理的所AEM有自定義代碼、配置和內容
1. 本地AEM運行時 — 作者的本AEM地版本和發佈服務，將用於從項目部署代AEM碼
1. 本地Dispatcher運行時 — 包括Dispatcher模組的Apache httpd Web伺服器的本地版本

設定本地開發環境後，您可以通過本地部署靜態節點伺服器來模擬內容服務到React應用。

為了更深入地瞭解設定本地開發環境以及內容預覽所需的所有相關性，請參閱 [生產部署文檔](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/production-deployment.html?lang=en#prerequisites)。

## 準AEM備無頭應用程式投入使用 {#prepare-your-aem-headless-application-for-golive}

現在，是時候按照下面介紹的AEM最佳做法，讓您的無頭應用程式準備啟動了。

### 在發佈前保護和擴展您的無頭應用程式 {#secure-and-scale-before-launch}

1. 配置 [基於令牌的身份驗證](/help/headless/security/authentication.md) GraphQL請求
1. 配置 [快取](/help/implementing/dispatcher/caching.md)。

### 模型結構與GraphQL輸出 {#structure-vs-output}

* 避免建立輸出超過15kb的JSON（gzip壓縮）的查詢。 長JSON檔案對客戶端應用程式進行分析的資源密集型。
* 避免五個以上嵌套的片段層次。 附加級別使內容作者很難考慮其更改的影響。
* 使用多對象查詢，而不是在模型內使用依賴關係層次結構建模查詢。 這允許更長期的靈活性來重構JSON輸出，而不必進行大量內容更改。

### 最大化CDN快取命中率 {#maximize-cdn}

* 請勿使用直接GraphQL查詢，除非您正在從曲面請求即時內容。
   * 盡可能使用永續查詢。
   * 提供600秒以上的CDN TTL，以便CDN快取它們。
   * 可AEM以計算模型更改對現有查詢的影響。
* 將JSON檔案/GraphQL查詢在低內容更改率和高內容更改率之間拆分，以減少CDN的客戶端流量並分配更高的TTL。 這將使CDN與源伺服器重新驗證JSON最小化。
* 要主動使CDN中的內容無效，請使用軟清除。 這允許CDN重新下載內容，而不會導致快取丟失。

### 縮短下載無頭內容的時間 {#improve-download-time}

* 確保HTTP客戶端使用HTTP/2。
* 確保HTTP客戶端接受gzip的標頭請求。
* 最小化用於承載JSON和引用對象的域數。
* 利用 `Last-modified-since` 來刷新資源。
* 使用 `_reference` 在JSON檔案中輸出，以開始下載資產，而無需分析完整的JSON檔案。

## 部署到生產 {#deploy-to-production}

一旦您確保所有內容都已測試並正常運行，您就可以將代碼更新推送到 [Cloud Manager中的集中式Git儲存庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html)。

將更新上載到雲管理器後，可以使用將更新部署到AEMas a Cloud Service [Cloud Manager的CI/CD管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html)。

您可以通過利用Cloud Manager CI/CD管道開始部署代碼，該管道已廣泛覆蓋 [這裡](/help/implementing/deploying/overview.md)。

## 效能監控 {#performance-monitoring}

為使用戶在使用無頭應用程式時擁有盡可能AEM最佳的體驗，您必須監控關鍵效能指標，詳見以下：

* 驗證應用的預覽版和生產版本
* 驗證當AEM前服務可用性狀態的狀態頁
* 訪問效能報告
   * 交付效能
      * CDN(Reablish)效能 — 檢查呼叫數、快取速率、錯誤率和負載流量
      * 源伺服器 — 呼叫數、錯誤率、CPU負載、負載流量
   * 作者效能
      * 檢查用戶、請求和載入數
* 訪問特定於應用和空間的效能報告
   * 伺服器啟動後，檢查常規指標是否為綠色/橙色/紅色，然後確定特定應用問題
   * 在篩選到應用程式或空間(例如，Photoshop案頭、付款牆)後開啟相同的報告
   * 使用Splunk日誌API訪問服務和應用程式效能
   * 如有其他問題，請與客戶支援聯繫。

## 疑難排解 {#troubleshooting}

### 調試 {#debugging}

按照以下最佳做法執行調試：

* 使用應用程式的預覽版本驗證功能和效能
* 使用應用程式的生產版本驗證功能和效能
* 使用內容片段編輯器的JSON預覽進行驗證
* Inspect客戶端應用程式中的JSON，用於檢查是否存在客戶端應用程式或傳遞問題
* InspectJSON使用GraphQL檢查是否存在與快取內容或

### 記錄支援的錯誤 {#logging-a-bug-with-support}

為了在需要進一步幫助時通過支援高效地記錄Bug，請執行以下步驟：

* 如有必要，請拍攝問題的截屏
* 記錄複製問題的方法
* 記錄問題所再現的內容
* 通過具有適當優先順序AEM的支援門戶記錄問題

## 旅程結束了，還是結束了？ {#journey-ends}

恭喜！ 您已完成無AEM頭開發者之旅！ 您現在應該瞭解：

* 無頭內容和有頭內容交付之間的區別。
* 無AEM頭部特徵。
* 如何組織和AEM無頭項目。
* 如何在中建立無頭內AEM容。
* 如何檢索和更新中的無頭內AEM容。
* 如何與無頭項目AEM共處。
* 上線後怎麼辦。

您已經啟動了第AEM一個Headless項目，或者現在已掌握了所需的全部知識。 幹得好！

### 瀏覽單頁應用程式 {#explore-spa}

不過，店AEM里的無頭店不必停在這裡。 你可能記得 [入門](getting-started.md#integration-levels) 我們簡要地討AEM論了如何不僅支援無頭遞送和傳統的全棧模型，還支援結合了兩者優點的混合模型。

如果這種靈活性是您項目需要的，請繼續進行可選的附加部分， [如何使用建立單頁應用SPA程式(AEM)。](create-spa.md)

## 其他資源 {#additional-resources}

* [部署到AEMas a Cloud Service](/help/implementing/deploying/overview.md)
* [AEMas a Cloud ServiceSDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
* [設定本地環AEM境](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html)
* [使用雲管理器部署代碼](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html)
* [將Cloud Manager Git儲存庫與外部Git儲存庫整合，並將項目部署到AEMas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html)
