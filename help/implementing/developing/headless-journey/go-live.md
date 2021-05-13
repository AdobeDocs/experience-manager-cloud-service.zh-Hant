---
title: 如何使用您的無頭應用程式上線
description: 在「無頭開發人AEM員歷程」的這部分，瞭解如何即時部署無頭應用程式，方法是將您的本機程式碼以Git格式載入，並將它移至Cloud Manager Git，以利CI/CD管道。
hide: true
hidefromtoc: true
index: false
exl-id: f79b5ada-8f59-4706-9f90-bc63301b2b7d
source-git-commit: 309fae113f98111e8dc548226a7fba1b72f16248
workflow-type: tm+mt
source-wordcount: '1836'
ht-degree: 0%

---

# 如何與您的無頭應用程式一起上線{#go-live}

>[!CAUTION]
>
>正在進行中的工作——本檔案的建立工作正在進行中，不應將其理解為完整或明確，也不應將其用於生產目的。

在[AEM Headless Developer Journey中，](overview.md)瞭解如何即時部署無頭應用程式，方法是將您的本機程式碼以Git格式移至Cloud Manager Git，以取得CI/CD管道。

## 到目前為止的故事{#story-so-far}

在上一份無頭歷程的AEM檔案中，[如何將所有內容整合在一起——您的應用程式與您的無頭內容AEM](put-it-all-together.md)您學習了如何準備自己的無頭AEM專案上線，您現在應：

* 瞭解上線的需求。

本文以這些基礎為基礎，讓您瞭解如何實際實作AEM無頭專案。

## 目標 {#objective}

本檔案可協助您瞭解無頭AEM出版管道，以及您在應用程式上線前需要注意的效能考量。

* 瞭解AEMSDK及所需的開發工具
* 設定本機開發執行階段，以模擬內容上線前的內容
* 瞭解內AEM容複製和快取基礎知識
* 在啟動前保護並調整應用程式的規模
* 監視效能和調試問題

## AEMSDK {#the-aem-sdk}

它包含下列對象：

* Quickstart jar —— 可執行的jar檔案，可用於設定作者和發佈實例
* Dispatcher tools - Dispatcher模組及其對基於Windows和UNIX的系統的依賴性
* Java API Jar - Java Jar/Maven Dependency，它公開所有允許的可用於開發的Java API AEM
* Javadocjar - Java APIjar的javadoc

## 開發工具{#development-tools}

除了SDK之AEM外，您還需要其他工具，以協助在本端開發和測試您的程式碼和內容：

* Java
* SDKAEM
* Git
* 阿帕奇·馬文
* Node.js程式庫
* 您選擇的IDE

由AEM於是Java應用程式，您必須安裝Java和Java SDK，才能支援將AEM其開發為Cloud Service。

SDKAEM可用來建立和部署自訂程式碼。 它是您在上線前測試無頭應用程式所需的主要工具。

Git是您用來管理來源控制以及簽入Cloud Manager的變更，然後將其部署至生產實例的工具。

使AEM用Apache Maven來建立從Maven Project原型產生AEM的專案。 所有主要IDE都提供Maven的整合支援。

Node.js是JavaScript執行時期環境，用於處理專案的ui.frontendAEM子專案的前端資產。 Node.js與npm一起分發，實際上是Node.js包管理器，用於管理JavaScript依賴性。

## 系統AEM元件總覽{#components-of-an-aem-system-at-a-glance}

完整AEM的環境由Author、Publish和Dispatcher組成。 這些相同的元件將會在本機開發執行時期中提供，讓您更輕鬆地在上線前預覽程式碼和內容。

* **作者服務** 是內部使用者建立、管理和預覽內容的地方。

* **Publish服** 務被視為「即時」環境，一般是使用者與之互動的環境。內容在「作者」服務上經過編輯和核准後，會分發至「發佈」服務。 無頭應用程式最常AEM見的部署模式是讓生產版應用程式連接至AEM Publish服務。

* **Dispatcher是** 一種靜態Web伺服器，與Dispatcher模組AEM一起擴展。它會快取由發佈例項產生的網頁，以改善效能。

## 本機開發工作流程{#the-local-development-workflow}

本端開發專案是以Apache Maven為基礎，並使用Git進行來源控制。 為了更新專案，開發人員可使用他們偏好的整合開發環境，例如Eclipse、Visual Studio程式碼或IntelliJ等。

若要測試無頭應用程式所擷取的程式碼或內容更新，您必須將更新部署至本機執行階段，其中包AEM含作者的本機例AEM項和發佈服務。

請務必注意本端執行階段中各元件之AEM差異，因為在最重要的地方測試更新非常重要。 例如，測試作者的內容更新或在發佈例項上測試新程式碼。

在生產系統中，調度程式和http Apache伺服器將始終位於發佈實例AEM前面。 它們為系統提供快取和安全AEM服務，因此必須針對分派程式測試程式碼和內容更新。

一旦您確定所有項目都經過測試並正常運作後，就可將程式碼更新推送至Cloud Manager的集中式Git儲存庫。

將更新上傳到Cloud Manager後，即可使用Cloud Manager的CI/CD管道將AEM其部署為Cloud Service。

## 使用本機開發環境在本機預覽程式碼和內容{#previewing-your-code-and-content-locally-with-the-local-development-environment}

為了讓您的無頭專AEM案準備啟動，您需要確保專案的所有組成部分都正常運作。

要做到這一點，您需要將一切整合在一起：程式碼、內容和設定，並在本機開發環境中進行測試，以便上線準備。

地方發展環境由三個主要領域組成：

1. 專AEM案——這將包含開發人員將要處理的所有自訂程AEM式碼、設定和內容
1. 本機執AEM行階段——作AEM者和發佈服務的本機版本，將用來從專案部署程AEM式碼
1. The Local Dispatcher Runtime - Apache httpd webserver的本地版本，其中包含Dispatcher模組

在設定本機開發環境後，您就可以在本機部署靜態Node伺服器，來模擬內容對React應用程式的服務。

若要深入瞭解如何設定本機開發環境，以及內容預覽所需的所有相依性，請參閱「使用AEM Publish Service進行生產部署」（英文）[](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/production-deployment.html?lang=en#prerequisites)。

## 部署至生產{#deploy-to-production}

在本機測試完所有程式碼和內容後，您就可開始使用進行生產部署AEM。

您可以利用Cloud Manager CI/CD管道開始部署代碼，該管道在[此處](/help/implementing/deploying/overview.md)廣泛介紹。

## 準備您AEM的無頭應用程式上線{#prepare-your-aem-headless-application-for-golive}

現在，您應該依照下列最AEM佳實務，讓無頭應用程式準備好啟動。

### 在啟動{#secure-and-scale-before-launch}之前，保護並縮放您的無頭應用程式

1. 配置[基於令牌的驗證](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)
1. 安全網頁掛接
1. 設定快取和調整彈性

### 模型結構與GraphQL輸出{#structure-vs-output}

* 請避免建立輸出超過15kb JSON（gzip壓縮）的查詢。 長JSON檔案需要大量資源，客戶端應用程式才能進行剖析。
* 避免超過5個巢狀層次的片段層級。 其他層級讓內容作者很難考慮其變更的影響。
* 使用多物件查詢，而非模型內具有相依性階層的查詢。 這可讓您更具長期彈性，來重新架構JSON輸出，而不需進行許多內容變更。

### 最大化CDN快取點擊率{#maximize-cdn}

* 請勿使用直接GraphQL查詢，除非您要從表面請求即時內容。
   * 請改用持續查詢。
   * 提供超過600秒的CDN TTL，讓CDN可快取它們。
   * 可AEM以計算模型更改對現有查詢的影響。
* 將JSON檔案/GraphQL查詢分割為低和高內容變更率，以減少CDN的用戶端流量並指派較高的TTL。 如此可將CDN與原始伺服器重新驗證JSON的程式碼減到最少。
* 若要主動使CDN的內容無效，請使用「軟清除」。 這可讓CDN重新下載內容，而不會造成快取遺失。

### 縮短下載無頭內容的時間{#improve-download-time}

* 請確定HTTP用戶端使用HTTP/2。
* 請確定HTTP用戶端接受gzip的標頭要求。
* 將用來裝載JSON和參考對象的網域數減到最少。
* 利用`Last-modified-since`刷新資源。
* 使用JSON檔案中的`_reference`輸出，即可開始下載資產，毋需剖析完整的JSON檔案。

## 效能監控{#performance-monitoring}

為了讓使用者在使用無頭應用程式時擁有最佳AEM的體驗，您務必要監控關鍵效能量度，如下所述：

* 驗證應用程式的預覽和生產版本
* 驗證當AEM前服務可用性狀態頁
* 存取效能報告
   * 傳送效能
      * 快速檢查呼叫數、快取速率、錯誤率、裝載流量
      * 原始伺服器——呼叫數、錯誤率、CPU負載、裝載流量
   * 作者效能
      * 檢查使用者、請求和載入的數目
* 存取應用程式和空間專用的效能報表
   * 伺服器啟動後，檢查一般量度是否為綠色／橘色／紅色，然後找出特定應用程式問題
   * 開啟上方篩選至應用程式／空間的相同報表(例如Photoshop案頭、付費牆等)
   * 使用Splunk記錄檔API存取服務和應用程式效能
   * 如有其他問題，請聯絡客戶支援。

## 疑難排解 {#troubleshooting}

### 除錯 {#debugging}

請遵循下列最佳實務做法，做為除錯的一般方法：

* 使用應用程式的預覽版本驗證功能與效能
* 使用應用程式的生產版本驗證功能與效能
* 使用內容片段編輯器的JSON預覽進行驗證
* InspectJSON在用戶端應用程式中，以檢查用戶端應用程式是否存在傳送問題
* InspectJSON使用GraphQL來檢查是否有與快取內容或

### 記錄支援{#logging-a-bug-with-support}的錯誤

為了在您需要進一步協助時，透過支援有效記錄錯誤，請遵循下列步驟：

* 視需要擷取問題的螢幕擷取畫面
* 記錄重制期刊的方式
* 記錄期刊以
* 以適當的優先順序AEM透過支援入口網站記錄問題

## 下一個{#what-is-next}

現在，您已完成這部分的無AEM頭開發人員旅程，您應：

* 瞭解內AEM容複製和快取基礎知識。
* 瞭解如何設定模擬無頭應用程式上線所需的工具。
* 瞭解如何在啟動之前保護和擴充您的應用程式。
* 瞭解如何監控效能和除錯問題。

您應繼續無AEM頭之旅，接下來檢閱檔案[Post Launch](post-launch.md)，以瞭解如何維持無頭之體驗。

## 其他資源 {#additional-resources}

* [設定本地環AEM境](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html)
* [作AEM為Cloud ServiceSDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
* [部署為Cloud ServiceAEM概述](/help/implementing/deploying/overview.md)
* [使用Cloud Manager部署您的程式碼](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html)
* [將Cloud Manager Git儲存庫與外部Git儲存庫整合，並將項目部署AEM為Cloud Service](https://git.corp.adobe.com/AdobeDocs/experience-manager-cloud-service.en/blob/master/help/implementing/developing/headless-journey/access-your-content.md)