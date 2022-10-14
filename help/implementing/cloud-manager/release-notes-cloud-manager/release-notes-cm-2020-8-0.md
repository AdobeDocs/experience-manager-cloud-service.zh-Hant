---
title: AEM as a Cloud Service 版本 2020.8.0 中 Cloud Manager 的發行說明
description: AEM as a Cloud Service 版本 2020.8.0 中 Cloud Manager 的發行說明
feature: Release Information
exl-id: 70674e16-f9ba-4777-98fe-34161e90a481
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 2020.8.0 中 Cloud Manager 的發行說明 {#release-notes}

本頁面總覽 AEM as a Cloud Service 2020.8.0 中 Cloud Manager 的發行說明

## 發行日期 {#release-date}

AEM as a Cloud Service 2020.8.0 中的 Cloud Manager 發行日期是 2020 年 8 月 06 日。

## 新增功能 {#whats-new-cloud-manager}

* 內容稽核是 Cloud Manager Sites Production Pipelines 上啟用的一項功能。具有 Sites 的程序的生產管道配置現在包括名為的第三個索引標籤&#x200B;**內容稽核**。每當執行生產管道時，在自訂功能測試之後將在管道中包含一個新的內容稽核步驟，該步驟將根據多個維度評估網站，包括性能、SEO (搜索引擎優化)、可存取性、最佳做法和 PWA (漸進式網路應用程序)。


   >[!NOTE]
   >此後，內容稽核已重命名為體驗稽核。

   如需更多詳細資訊，請參考[體驗稽核結果](/help/implementing/cloud-manager/experience-audit-testing.md)。

* Assets 程序中新建立的環境現在將自動配置智慧內容服務。

* 休眠的環境可以從 Cloud Manager 的&#x200B;**概論**&#x200B;頁。

* 能夠在頁面上執行經驗檢查，由 Google Lighthouse 提供支援。作為 Cloud Manager 管道的一部分，最多可以根據體驗 KPI 檢查和驗證 25 個頁面，並且分數會顯示在 Cloud Manager UI 中。

### 錯誤修正 {#bug-fixes-cm}

* 作為計劃碼品質掃描的一部分，正在執行一些不必要和不受歡迎的 SonarQube 插件。

* 在管道執行頁面上，分支名稱的格式不正確。

* 在某些情況下，已完成的管道執行未成功記錄為已完成，從而阻止了管道的新執行。

* 管道執行偶爾會得到&#x200B;*卡住*&#x200B;由於內部溝通問題。

* 在配置新組織時，某些具有系統管理員以外的管理角色的使用者被錯誤地授予對 Cloud Manager 的存取權限。

* 在某些情況下，更新索引作業會並行啟動多次，從而導致部署失敗。

* 程序卡上的工具提示並非始終正確。

* 在刪除環境時，使用者界面錯誤地允許在環境中嘗試操作。

* Cloud Manager 的顏色不匹配&#x200B;**總覽**&#x200B;頁。

### 已知問題 {#known-issues-cm}

* 包含無效頁面，使內容稽核平均分數低於應有的水平。

* 內容稽核索引標籤使用作者域而不是發布域錯誤地顯示了 BASE URL。

* 為了激活內容稽核步驟，使用者必須編輯管道並 (可選) 新增頁面。如果沒有新增任何頁面，則將稽核主頁。
