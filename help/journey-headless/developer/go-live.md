---
title: 如何與無頭應用程式一起生活
description: 在「無頭開發者之旅」的這一部分AEM，瞭解如何即時部署無頭應用程式，方法是將本地代碼以Git格式使用，並將其移至Cloud Manager Git，以用於CI/CD管道。
exl-id: 81616e31-764b-44b0-94a6-3ae24ce56bf6
source-git-commit: 270eb35023e34eed2cd17674372794c6c2cc7757
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 0%

---

# 如何與無頭應用程式一起生活 {#go-live}

在 [無AEM頭開發者之旅](overview.md)，瞭解如何通過將本地代碼以Git格式移至Cloud Manager Git以用於CI/CD管道，即時部署無頭應用程式。

## 到目前為止的故事 {#story-so-far}

在前一篇無頭旅AEM程中， [如何將所有內容放在一起 — 您的應用和您的內容以無AEM頭](put-it-all-together.md) 您學會了如何使用AEM開發工具將項目的所有方面放在一起。

本文基於這些基礎知識，因此您瞭解如何準備AEM自己的無頭項目來投入使用。

## 目標 {#objective}

本文檔可幫助您了AEM解無頭發佈管道，以及在與應用程式共處之前必須注意的效能注意事項。

* 在啟動前保護並擴展應用程式
* 監視效能和調試問題

<!-- Alexandru: this is a bit redundant, to review again later

## Prepare your AEM Headless Application for Go-Live {#prepare-your-aem-headless-application-for-golive}

-->
要使您的無AEM頭應用程式準備好啟動，請遵循下面概述的最佳做法。

## 在發佈前保護和擴展您的無頭應用程式 {#secure-and-scale-before-launch}

1. 配置 [基於令牌的身份驗證](/help/headless/security/authentication.md) GraphQL請求
1. 配置 [快取](/help/implementing/dispatcher/caching.md)。

## 模型結構與GraphQL輸出 {#structure-vs-output}

* 避免建立輸出超過15kb的JSON（gzip壓縮）的查詢。 長JSON檔案對客戶端應用程式進行分析的資源密集型。
* 避免五個以上嵌套的片段層次。 附加級別使內容作者很難考慮其更改的影響。
* 使用多對象查詢，而不是在模型內使用依賴關係層次結構建模查詢。 這允許更長期的靈活性來重構JSON輸出，而不必進行大量內容更改。

## 最大化CDN快取命中率 {#maximize-cdn}

* 請勿使用直接GraphQL查詢，除非您正在從曲面請求即時內容。
   * 盡可能使用永續查詢。
   * 提供600秒以上的CDN TTL，以便CDN快取它們。
   * 可AEM以計算模型更改對現有查詢的影響。
* 將JSON檔案/GraphQL查詢在低內容更改率和高內容更改率之間拆分，以減少CDN的客戶端流量並分配更高的TTL。 這將使CDN與源伺服器重新驗證JSON最小化。
* 要主動使CDN中的內容無效，請使用軟清除。 這允許CDN重新下載內容，而不會導致快取丟失。

## 縮短下載無頭內容的時間 {#improve-download-time}

* 確保HTTP客戶端使用HTTP/2。
* 確保HTTP客戶端接受gzip的標頭請求。
* 最小化用於承載JSON和引用對象的域數。
* 利用 `Last-modified-since` 來刷新資源。
* 使用 `_reference` 在JSON檔案中輸出，以開始下載資產，而無需分析完整的JSON檔案。

## 部署到生產 {#deploy-to-production}

一旦您確保所有內容都經過測試並且工作正常，您就準備好將代碼更新推送到 [Cloud Manager中的集中式Git儲存庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html)。

將更新上載到雲管理器後，可以使用將更新部署到AEMas a Cloud Service [Cloud Manager的CI/CD管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html)。

您可以通過利用Cloud Manager CI/CD管道開始部署代碼，該管道已廣泛覆蓋 [這裡](/help/implementing/deploying/overview.md)。

## 效能監控 {#performance-monitoring}

要使用戶在使用無頭應用程式時擁有盡可能AEM最佳的體驗，您必須監控關鍵效能指標，詳見下文：

* 驗證應用的預覽版和生產版本
* 驗證當AEM前服務可用性狀態的狀態頁
* 訪問效能報告
   * 交付效能
      * CDN(Reablish)效能 — 檢查呼叫數、快取速率、錯誤率和負載流量
      * 源伺服器 — 呼叫數、錯誤率、CPU負載、負載流量
   * 作者效能
      * 檢查用戶、請求和載入數
* 訪問特定於應用程式和空間的效能報告
   * 伺服器啟動後，檢查常規指標是否為綠色/橙色/紅色，然後確定特定應用問題
   * 在篩選到應用程式或空間(例如，Photoshop案頭、付款牆)後開啟相同的報告
   * 使用Splunk日誌API訪問服務和應用程式效能
   * 如有其他問題，請與客戶支援聯繫。

## 疑難排解 {#troubleshooting}

### 偵錯 {#debugging}

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

不過，店AEM里的無頭店不必停在這裡。 你可能記得 [入門](getting-started.md#integration-levels) 我們簡要地AEM討論了如何不僅支援無頭遞送和傳統的全棧模型，還支援結合兩者優點的混合模型。

如果這種靈活性是您項目需要的，請繼續進行可選的附加部分， [如何使用建立單頁應用SPA程式(AEM)。](create-spa.md)

## 其他資源 {#additional-resources}

* [部署到AEMas a Cloud Service](/help/implementing/deploying/overview.md)
* [使用雲管理器部署代碼](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html)
* [將Cloud Manager Git儲存庫與外部Git儲存庫整合，並將項目部署到AEMas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html)
