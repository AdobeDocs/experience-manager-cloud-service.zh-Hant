---
title: 如何與無頭應用程式一起運行
description: 在AEM無頭式開發人員歷程中，了解如何以Git取用本機程式碼，並將其移至Cloud Manager Git，以利CI/CD管道使用，即時部署無頭式應用程式。
exl-id: 81616e31-764b-44b0-94a6-3ae24ce56bf6
source-git-commit: 270eb35023e34eed2cd17674372794c6c2cc7757
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 0%

---

# 如何與無頭應用程式一起運行 {#go-live}

在 [AEM Headless Developer Journey](overview.md)，了解如何在Git中取用本機程式碼，並移至Cloud Manager Git，以利CI/CD管道使用，即時部署無頭應用程式。

## 迄今為止的故事 {#story-so-far}

在AEM無頭歷程的上一份檔案中， [如何將所有內容放在一起 — 您的應用程式和AEM Headless中的內容](put-it-all-together.md) 您已學會如何使用AEM開發工具，將專案的所有層面整合在一起。

本文以這些基本知識為基礎，讓您了解如何準備自己的AEM無頭專案以上線。

## 目標 {#objective}

本檔案可協助您了解AEM無頭發佈管道，以及在與應用程式上線前必須注意的效能考量事項。

* 在啟動前保護並調整應用程式的規模
* 監控效能和除錯問題

<!-- Alexandru: this is a bit redundant, to review again later

## Prepare your AEM Headless Application for Go-Live {#prepare-your-aem-headless-application-for-golive}

-->
若要讓您的AEM無頭應用程式準備好投入啟動，請遵循下列最佳實務。

## 在啟動前保護和擴展您的無頭應用程式 {#secure-and-scale-before-launch}

1. 設定 [基於令牌的驗證](/help/headless/security/authentication.md) GraphQL請求
1. 設定 [快取](/help/implementing/dispatcher/caching.md).

## 模型結構與GraphQL輸出 {#structure-vs-output}

* 請避免建立輸出超過15kb JSON的查詢（gzip壓縮）。 長JSON檔案是需要大量資源，用戶端應用程式才能剖析。
* 避免超過五個巢狀片段階層。 額外的層級使得內容作者很難考慮其變更的影響。
* 使用多對象查詢，而不是在模型內建立具有相關性層次的模型查詢。 這可提供更長期的彈性，以重新建構JSON輸出，而無須進行大量內容變更。

## 最大化CDN快取點擊率 {#maximize-cdn}

* 請勿使用直接GraphQL查詢，除非您從表面要求即時內容。
   * 盡可能使用持續查詢。
   * 提供超過600秒的CDN TTL，讓CDN加以快取。
   * AEM可計算模型變更對現有查詢的影響。
* 在低內容和高內容變更率之間分割JSON檔案/GraphQL查詢，以減少CDN的用戶端流量並指派較高的TTL。 如此一來，CDN與來源伺服器重新驗證JSON的程度就能降到最低。
* 若要主動使CDN的內容失效，請使用「軟清除」。 這可讓CDN重新下載內容，而不會造成快取遺失。

## 縮短下載無頭內容的時間 {#improve-download-time}

* 請確定HTTP用戶端使用HTTP/2。
* 請確定HTTP用戶端接受gzip的標題要求。
* 將用於托管JSON和參考成品的網域數減到最少。
* 運用 `Last-modified-since` 重新整理資源。
* 使用 `_reference` JSON檔案中的輸出，即可開始下載資產，而不需剖析完整的JSON檔案。

## 部署至生產環境 {#deploy-to-production}

一旦您確定所有項目皆已測試且正常運作，即可將程式碼更新推送至 [Cloud Manager中的集中式Git存放庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html).

更新上傳至Cloud Manager後，即可使用部署至AEM as a Cloud Service [Cloud Manager的CI/CD管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html).

您可以善用Cloud Manager CI/CD管道（已廣泛涵蓋），開始部署程式碼 [此處](/help/implementing/deploying/overview.md).

## 效能監控 {#performance-monitoring}

為使用者在使用AEM無頭式應用程式時能有最佳的使用體驗，請務必監控關鍵效能量度，如下所述：

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

### 偵錯 {#debugging}

請遵循下列最佳實務作為偵錯的一般方法：

* 使用應用程式的預覽版本驗證功能和效能
* 使用應用程式的生產版本驗證功能和效能
* 使用內容片段編輯器的JSON預覽進行驗證
* Inspect用戶端應用程式中的JSON，以檢查用戶端應用程式是否存在或傳送問題
* Inspect JSON使用GraphQL來檢查是否有與快取內容或AEM相關的問題

### 記錄有支援的錯誤 {#logging-a-bug-with-support}

若想透過支援有效記錄錯誤，以備您需要進一步協助時使用，請遵循下列步驟：

* 如有必要，請拍攝問題的螢幕截圖
* 記錄重現問題的方法
* 記錄問題用重制的內容
* 透過AEM支援入口網站以適當優先順序記錄問題

## 歷程結束了，還是結束了？ {#journey-ends}

恭喜！ 您已完成AEM Headless Developer Journey! 您現在應了解：

* 無頭式內容傳送與無頭式內容傳送之間的差異。
* AEM無頭功能。
* 如何組織及AEM Headless專案。
* 如何在AEM中建立無頭式內容。
* 如何在AEM中擷取和更新無標題內容。
* 如何與AEM Headless專案同時執行。
* 上線後該做什麼。

您已啟動第一個AEM Headless專案，或現在擁有所需的所有知識。 幹得好！

### 探索單頁應用程式 {#explore-spa}

不過，AEM的無頭店不需要停在這裡。 您可能會記得 [快速入門歷程部分](getting-started.md#integration-levels) 我們簡要地討論了AEM如何不僅支援無頭式傳送和傳統的完整堆疊模型，還支援結合兩者優點的混合模型。

如果您專案需要這種彈性，請繼續前往歷程的其他選用部分， [如何使用AEM建立單頁應用程式(SPA)。](create-spa.md)

## 其他資源 {#additional-resources}

* [部署至AEM as a Cloud Service概述](/help/implementing/deploying/overview.md)
* [使用Cloud Manager部署程式碼](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html)
* [整合Cloud Manager Git存放庫與外部Git存放庫，並將專案部署至AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html)
