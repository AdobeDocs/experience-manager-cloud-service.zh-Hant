---
title: 如何將 Headless 應用程式上線
description: 在 AEM Headless 開發人員歷程的這一部分中，了解如何從 Git 取出本機程式碼並移至 Cloud Manager Git 以用於 CI/CD 管道，藉此來部署 Headless 應用程式。
exl-id: 81616e31-764b-44b0-94a6-3ae24ce56bf6
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 100%

---

# 如何將 Headless 應用程式上線 {#go-live}

在 [AEM Headless 開發人員歷程](overview.md)的這一部分中，了解如何從 Git 取出本機程式碼並移至 Cloud Manager Git 以用於 CI/CD 管道，藉此來部署 Headless 應用程式。

## 目前進度 {#story-so-far}

在 AEM Headless 歷程的上一份文件「[如何在 AEM Headless 中將您的應用程式和內容組合在一起](put-it-all-together.md)」中，您已了解如何使用 AEM 開發工具將您專案的所有面向組合在一起。

本文章以這些基本知識為基礎，以便您了解如何準備您自己的 AEM Headless 專案並方案上線。

## 目標 {#objective}

本文件可協助在將您的應用程式上線之前，應該注意的 AEM Headless 發佈管道和效能考量事項。

* 在應用程式推出前加以保護和擴展
* 監控效能和偵錯問題

若要讓 AEM Headless 應用程式準備好推出，請遵循下面概述的最佳做法。

## 在 Headless 應用程式推出前加以保護和擴展 {#secure-and-scale-before-launch}

1. 使用您的 GraphQL 要求設定[權杖型驗證](/help/headless/security/authentication.md)
1. 設定[快取](/help/implementing/dispatcher/caching.md)。

## 模型結構與 GraphQL 輸出 {#structure-vs-output}

* 避免建立輸出超過 15kb JSON (gzip 格式壓縮) 的查詢。長 JSON 檔案是資源密集型檔案，用戶端應用程式需要解析。
* 避免片段階層有超過五個巢狀層。增加層數會使內容作者難以考量變更帶來的影響。
* 使用多物件查詢，而不是在模型中使用相依性階層建立查詢模型。這允許更長期的靈活性來重新建構 JSON 輸出，而無需進行許多內容變更。

## 最大化 CDN 快取命中比例 {#maximize-cdn}

* 不要使用直接 GraphQL 查詢，除非您從表面要求即時內容。
   * 盡可能使用持續性查詢。
   * 提供 600 秒以上的 CDN TTL，以便 CDN 可以快取。
   * AEM 可以計算模型變更對現有查詢的影響。
* 在低內容更改率和高內容變更改率之間分割 JSON 檔案/GraphQL 查詢，以減少流到 CDN 的用戶端流量並指派更高的 TTL。這將 CDN 使用原始伺服器重新驗證 JSON 的需要降至最低。
* 要主動使來自 CDN 的內容無效，請使用軟清除 (Soft Purge)。這允許 CDN 重新下載內容而不會導致快取遺漏。

## 縮短下載 Headless 內容的時間 {#improve-download-time}

* 確保 HTTP 用戶端使用 HTTP/2。
* 確保 HTTP 用戶端接受標頭要求 gzip。
* 盡量減少用於裝載 JSON 和參考成品的網域數量。
* 利用 `Last-modified-since` 重新整理資源。
* 使用 JSON 檔案中的 `_reference` 輸出開始下載資產，而無需解析完整的 JSON 檔案。

## 部署至生產環境 {#deploy-to-production}

確保一切都經過測試且運作正常後，您就可以將程式碼更新推送至 [Cloud Manager 中的集中式 Git 存放庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html)。

將更新上傳到 Cloud Manager 後，可以使用 [Cloud Manager 的 CI/CD 管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html)部署到 AEM as a Cloud Service。

您可以使用 Cloud Manager CI/CD 管道開始部署程式碼，「[透過 Cloud Manager 和封裝管理員部署內容套件](/help/implementing/deploying/overview.md)」對此進行了詳細介紹。

## 效能監控 {#performance-monitoring}

為了讓使用者有最佳的 AEM Headless 應用程式使用體驗，請務必監控關鍵效能量度，如下詳述：

* 驗證應用程式的預覽版本和生產版本
* 確認 AEM 狀態頁面是否有目前的服務可用性狀態
* 存取效能報告
   * 傳遞效能
      * CDN (Fastly) 效能 - 檢查呼叫次數、快取率、錯誤率和負載流量
      * 原始伺服器 - 呼叫次數、錯誤率、CPU 負載、負載流量
   * 作者效能
      * 檢查使用者、要求和負載的數量
* 存取應用程式和空間特定的效能報告
   * 伺服器啟動後，檢查一般量度是否為綠色/橘色/紅色，然後識別特定的應用程式問題
   * 開啟上面篩選到應用程式或空間 (例如 Photoshop 桌面、付費牆) 的相同報告
   * 使用 Splunk log API 存取服務和應用程式效能
   * 如果還有其他問題，請聯絡客戶支援。

## 疑難排解 {#troubleshooting}

### 偵錯 {#debugging}

遵循這些最佳做法做為一般偵錯方法：

* 使用應用程式的預覽版本驗證功能和效能
* 使用應用程式的生產版本驗證功能和效能
* 使用內容片段編輯器的 JSON 預覽進行驗證
* 檢查用戶端應用程式中的 JSON 以檢查是否存在用戶端應用程式或傳遞問題
* 使用 GraphQL 檢查 JSON 以檢查是否存在與快取內容或 AEM 相關的問題

### 向支援團隊記錄錯誤 {#logging-a-bug-with-support}

為了在需要進一步協助時，可以有效率地向支援團隊記錄錯誤，請執行以下操作：

* 如有必要，將問題進行螢幕截圖
* 記錄重現問題的方法
* 記錄問題重現的內容
* 透過 AEM 支援入口網站記錄問題並標註優先順序

## 歷程結束 - 還是結束了？ {#journey-ends}

恭喜！您已經完成 AEM Headless 開發人員歷程！您現在應該已經了解：

*  Headless 和 Headful 內容傳遞之間的差異。
* AEM 的 Headless 功能。
* 如何組織 AEM Headless 專案。
* 如何在 AEM 建立 Headless 內容。
* 如何在 AEM 擷取和更新 Headless 內容。
* 如何使 AEM Headless 專案上線。
* 上線後要做什麼。

您已經推出您的第一個 AEM Headless 專案，或是現在已經掌握完成此作業的所有必要知識。做得好！

### 探索單頁應用程式 {#explore-spa}

不過，AEM Headless 存放區不需要就此停止。您可能還記得，在[歷程的快速入門部分](getting-started.md#integration-levels)中，我們簡短討論到 AEM 如何不僅支援 Headless 傳遞和傳統的全堆疊模型，還可以支援結合兩者優點的混合模型。

如果您的專案需要這種靈活性，請繼續學習此歷程的額外部分 (選用)：[如何使用 AEM 建立單一頁面應用程式 (SPA)](create-spa.md)。

## 其他資源 {#additional-resources}

* [AEM as a Headless CMS 簡介](/help/headless/introduction.md)
* [AEM 開發人員入口網站](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html)
* [AEM 中的 Headless 教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html)
* [部署至 AEM as a Cloud Service 概觀](/help/implementing/deploying/overview.md)
* [使用 Cloud Manager 部署您的程式碼](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html)
* [將 Cloud Manager Git 存放庫與外部 Git 存放庫整合，並將專案部署到 AEM as a Cloud Service。](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html)
