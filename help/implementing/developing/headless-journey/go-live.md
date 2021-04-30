---
title: 如何使用您的無頭應用程式上線
description: 在「無頭開發人AEM員歷程」的這部分，瞭解如何即時部署無頭應用程式，方法是將您的本機程式碼以Git格式載入，並將它移至Cloud Manager Git，以利CI/CD管道。
hide: true
hidefromtoc: true
index: false
exl-id: f79b5ada-8f59-4706-9f90-bc63301b2b7d
translation-type: tm+mt
source-git-commit: dc4f1e916620127ebf068fdcc6359041b49891cf
workflow-type: tm+mt
source-wordcount: '1039'
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

* 瞭解內AEM容複製和快取基礎知識
* 設定模擬無頭應用程式上線所需的工具
* 在啟動前保護並調整應用程式的規模
* 監視效能和調試問題

## 內容複製和快取基礎知識{#content-replication-and-caching}

完整AEM的環境由Author、Publish和Dispatcher組成。

* **作者服務** 是內部使用者建立、管理和預覽內容的地方。

* **Publish服** 務被視為「即時」環境，一般是使用者與之互動的環境。內容在「作者」服務上經過編輯和核准後，會分發至「發佈」服務。

* **Dispatcher是** 一種靜態Web伺服器，與Dispatcher模組AEM一起擴展。它會快取由發佈例項產生的網頁，以改善效能。

無頭應用程式最常AEM見的部署模式是讓生產版應用程式連接至AEM Publish服務。

## 要求和配置{#requirements-and-configuration}

1. 使用[作為雲端服務SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)來設定[本機執行階段AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html#install-java)
2. 安裝[WKND示例內容](/help/implementing/developing/introduction/develop-wknd-tutorial.md)和後續的GraphQL端點
3. 部署和配置[靜態節點伺服器](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/production-deployment.html?lang=en#static-server)。

## 在啟動{#secure-and-scale-before-launch}之前，保護並縮放您的無頭應用程式

1. 配置[基於令牌的驗證](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)
2. 安全網頁掛接
3. 設定快取和調整彈性

## 部署至生產{#deploy-to-production}

在本機測試完所有程式碼和內容後，您現在可以開始使用進行生產部署AEM。

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

## 監控 {#monitoring}

### 如何檢查整體效能{#check-overall-performance}

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

### 調試{#debugging}

為了在啟動之前確定您的應用程式是否正常運作，建議您依照下列步驟進行除錯：

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
