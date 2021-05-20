---
title: 如何與無頭應用程式一起運行
description: 在AEM無頭式開發人員歷程中，了解如何以Git取用本機程式碼，並將其移至Cloud Manager Git，以利CI/CD管道使用，即時部署無頭式應用程式。
hide: true
hidefromtoc: true
index: false
exl-id: f79b5ada-8f59-4706-9f90-bc63301b2b7d
source-git-commit: 9e06419f25800199dea92b161bc393e6e9670697
workflow-type: tm+mt
source-wordcount: '1815'
ht-degree: 0%

---

# 如何與無頭應用程式一起運行{#go-live}

>[!CAUTION]
>
>過時 — 此草稿內容已由新的[無頭開發人員歷程檔案取代。](/help/journey-headless/developer/overview.md)

在[AEM無頭開發人員歷程](overview.md)中，了解如何以Git擷取本機程式碼，並將其移至Cloud Manager Git，以利CI/CD管道使用，即時部署無頭應用程式。

## 迄今為止的故事{#story-so-far}

在AEM無頭歷程的上一份檔案中，[如何透過AEM Assets API更新您的內容](update-your-content.md)您已了解如何透過API更新AEM中現有的無頭內容，您現在應：

* 了解AEM Assets HTTP API。

本文以這些基本知識為基礎，讓您了解如何準備自己的AEM無頭專案以上線。

## 目標 {#objective}

本檔案可協助您了解AEM無頭發佈管道，以及在與應用程式上線前需要注意的效能考量事項。

* 了解AEM SDK及所需的開發工具
* 設定本機開發執行階段，以在上線前模擬您的內容
* 了解AEM內容復寫和快取基本知識
* 在啟動前保護並調整應用程式的規模
* 監控效能和除錯問題

## AEM SDK {#the-aem-sdk}

AEM SDK可用來建置和部署自訂程式碼。 這是您在開發和測試無頭應用程式之前所需的主要工具。 它包含下列成品：

* Quickstart jar — 可執行的jar檔案，可用於設定作者和發佈執行個體
* Dispatcher工具 — 適用於Windows和UNIX系統的Dispatcher模組及其相依性
* Java API Jar — 公開所有可用來針對AEM開發的允許Java API的Java Jar/Maven相依性
* Javadoc jar - Java API jar的javadoc

## 其他開發工具{#additional-development-tools}

除了AEM SDK，您還需要其他工具來協助您在本機開發及測試程式碼和內容：

* Java
* Git
* 阿帕奇·馬文
* Node.js程式庫
* 您選擇的IDE

由於AEM是Java應用程式，因此您必須安裝Java和Java SDK，才能支援AEM作為Cloud Service的開發。

您可以使用Git來管理原始碼控制，以及檢查Cloud Manager的變更，然後將其部署至生產執行個體。

AEM使用Apache Maven來建置從AEM Maven專案原型產生的專案。 所有主要IDE都為Maven提供整合支援。

Node.js是JavaScript執行階段環境，用於搭配AEM專案`ui.frontend`子專案的前端資產使用。 Node.js與npm一起分發，實際上是Node.js套件管理器，用於管理JavaScript相依性。

## AEM系統元件一覽{#components-of-an-aem-system-at-a-glance}

接下來，讓我們看一下AEM環境的組成部分。

完整的AEM環境由製作、發佈和Dispatcher組成。 這些相同的元件會在本機開發執行階段中提供，讓您在上線前更輕鬆地預覽程式碼和內容。

* **內部使** 用者可在Author服務中建立、管理和預覽內容。

* **發佈服** 務被視為「即時」環境，且通常是使用者與之互動的環境。內容在Author服務上經過編輯和核准後，會分發至Publish服務。 AEM無頭式應用程式最常見的部署模式是讓生產版本的應用程式連線至AEM發佈服務。

* **Dispatcher** 是一種靜態Web伺服器，可與AEM Dispatcher模組搭配使用。它會快取由發佈例項產生的網頁，以提升效能。

## 本地開發工作流{#the-local-development-workflow}

本機開發專案以Apache Maven為基礎，且使用Git進行原始碼控制。 為了更新專案，開發人員可使用其偏好的整合開發環境，例如Eclipse、Visual Studio Code或IntelliJ等。

若要測試無頭應用程式將擷取的程式碼或內容更新，您必須將更新部署至本機AEM執行階段，其中包括AEM製作和發佈服務的本機例項。

請務必注意本機AEM執行階段中每個元件之間的差異，因為在最重要的位置測試更新非常重要。 例如，在製作上測試內容更新，或在發佈例項上測試新程式碼。

在生產系統中，Dispatcher和http Apache伺服器一律會位於AEM發佈例項之前。 它們為AEM系統提供快取和安全服務，因此也必須針對Dispatcher測試程式碼和內容更新。

## 使用本機開發環境{#previewing-your-code-and-content-locally-with-the-local-development-environment}在本機預覽您的程式碼和內容

若要為啟動準備AEM無標題專案，您必須確定專案的所有組成部分都正常運作。

為此，您需要將所有內容整合在一起：程式碼、內容和設定，並在本機開發環境中測試，以備上線準備。

地方發展環境由三個主要領域組成：

1. AEM專案 — 這將包含AEM開發人員將要使用的所有自訂程式碼、設定和內容
1. 本機AEM執行階段 — 用於從AEM專案部署程式碼的AEM製作與發佈服務的本機版本
1. 本機Dispatcher執行階段 — 包含Dispatcher模組的Apache httpd網站伺服器的本機版本

設定本機開發環境後，您就可以在本機部署靜態節點伺服器，以模擬提供給React應用程式的內容。

若要深入了解如何設定本機開發環境，以及內容預覽所需的所有相依性，請參閱[生產部署檔案](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/production-deployment.html?lang=en#prerequisites)。

## 準備AEM無頭應用程式以投入使用{#prepare-your-aem-headless-application-for-golive}

現在，您可以遵循以下概述的最佳實務，為您的AEM無頭應用程式做好啟動準備。

### 在啟動前保護和擴展無頭應用程式{#secure-and-scale-before-launch}

1. 使用您的GraphQL請求配置[基於令牌的身份驗證](/help/assets/content-fragments/graphql-authentication-content-fragments.md)
1. 配置[快取](/help/implementing/dispatcher/caching.md)。

### 模型結構與GraphQL輸出{#structure-vs-output}

* 請避免建立輸出超過15kb JSON的查詢（gzip壓縮）。 長JSON檔案是需要大量資源，用戶端應用程式才能剖析。
* 避免超過五個巢狀片段階層。 額外的層級使得內容作者很難考慮其變更的影響。
* 使用多對象查詢，而不是在模型內建立具有相關性層次的模型查詢。 這可提供更長期的彈性，以重新建構JSON輸出，而無須進行大量內容變更。

### 最大化CDN快取點擊率{#maximize-cdn}

* 請勿使用直接GraphQL查詢，除非您從表面請求即時內容。
   * 盡可能使用持續查詢。
   * 提供超過600秒的CDN TTL，讓CDN加以快取。
   * AEM可計算模型變更對現有查詢的影響。
* 在低內容和高內容變更率之間分割JSON檔案/GraphQL查詢，以減少CDN的用戶端流量並指派較高的TTL。 如此一來，CDN與來源伺服器重新驗證JSON的程度就能降到最低。
* 若要主動使CDN的內容失效，請使用「軟清除」。 這可讓CDN重新下載內容，而不會造成快取遺失。

### 縮短下載無頭內容的時間{#improve-download-time}

* 請確定HTTP用戶端使用HTTP/2。
* 請確定HTTP用戶端接受gzip的標題要求。
* 將用於托管JSON和參考成品的網域數減到最少。
* 利用`Last-modified-since`刷新資源。
* 在JSON檔案中使用`_reference`輸出，即可開始下載資產，而無須剖析完整的JSON檔案。

## 部署到生產環境{#deploy-to-production}

一旦您確定所有項目皆已通過測試且正常運作後，即可將程式碼更新推送至Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html)中央的Git存放庫[。

更新上傳至Cloud Manager後，即可使用[Cloud Manager的CI/CD管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html)，以Cloud Service形式部署至AEM。

您可以善用Cloud Manager CI/CD管道開始部署程式碼，此管道在[此處](/help/implementing/deploying/overview.md)廣泛涵蓋。

## 效能監視{#performance-monitoring}

為了讓使用者在使用AEM無頭式應用程式時能有最佳體驗，請務必監控關鍵效能量度，如下所述：

* 驗證應用程式的預覽和生產版本
* 驗證AEM狀態頁以了解當前服務可用性狀態
* 訪問效能報告
   * 傳送效能
      * CDN（快速）效能 — 檢查呼叫數、快取率、錯誤率和裝載流量
      * 來源伺服器 — 呼叫數、錯誤率、CPU負載、裝載流量
   * 作者效能
      * 檢查使用者、請求和載入數量
* 訪問特定於應用程式和空間的效能報告
   * 伺服器上線後，檢查一般量度是否為綠色/橙色/紅色，然後找出特定的應用程式問題
   * 開啟上方篩選至應用程式或空間的相同報表(例如Photoshop案頭、付費牆)
   * 使用Splunk日誌API訪問服務和應用程式效能
   * 如有其他問題，請聯絡客戶支援。

## 疑難排解 {#troubleshooting}

### 除錯 {#debugging}

請遵循下列最佳實務作為偵錯的一般方法：

* 使用應用程式的預覽版本驗證功能和效能
* 使用應用程式的生產版本驗證功能和效能
* 使用內容片段編輯器的JSON預覽進行驗證
* Inspect用戶端應用程式中的JSON，以檢查用戶端應用程式是否存在或傳送問題
* Inspect JSON使用GraphQL來檢查是否有與快取內容或AEM相關的問題

### 記錄支援{#logging-a-bug-with-support}的錯誤

若想透過支援有效記錄錯誤，以備您需要進一步協助時使用，請遵循下列步驟：

* 如有必要，請拍攝問題的螢幕截圖
* 記錄重現問題的方法
* 記錄問題用重制的內容
* 透過AEM支援入口網站以適當優先順序記錄問題

## 歷程結束了，還是結束了？{#journey-ends}

恭喜！ 您已完成AEM Headless Developer Journey! 您現在應了解：

* 無頭式內容傳送與無頭式內容傳送之間的差異。
* AEM無頭功能。
* 如何組織及AEM Headless專案。
* 如何在AEM中建立無頭式內容。
* 如何在AEM中擷取和更新無標題內容。
* 如何與AEM Headless專案同時執行。
* 上線後怎麼辦。

## 其他資源 {#additional-resources}

* [部署至AEM as aCloud Service概述](/help/implementing/deploying/overview.md)
* [AEM as a Cloud ServiceSDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
* [設定本機AEM環境](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html)
* [使用Cloud Manager部署程式碼](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html)
* [整合Cloud Manager Git存放庫與外部Git存放庫，並將專案部署至AEM作為Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html)