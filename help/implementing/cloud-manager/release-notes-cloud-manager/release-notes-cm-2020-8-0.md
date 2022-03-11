---
title: Cloud Manager在as a Cloud Service版AEM2020.8.0中的發行說明
description: Cloud Manager在as a Cloud Service版AEM2020.8.0中的發行說明
feature: Release Information
exl-id: 70674e16-f9ba-4777-98fe-34161e90a481
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 1%

---

# Adobe Experience Manager as a Cloud ServiceCloud Manager發行說明2020.8.0 {#release-notes}

本頁概述了as a Cloud Service2020.8.0中Cloud Manager的發行說明AEM。

## 發行日期 {#release-date}

Cloud Manager在as a Cloud Service中的發AEM布日期為2020年8月06日。

## 新增功能 {#whats-new-cloud-manager}

* 內容審核是在Cloud Manager站點生產管道上啟用的功能。 現在，具有站點的程式的生產管道配置包含名為 **內容審核**。 每當生產管道運行時，在自定義功能測試後，管道中將包括新的內容審核步驟，該步驟將根據包括效能、 SEO（搜索引擎優化）、可訪問性、最佳實踐和PWA(Progressive Web App)在內的多個維度評估站點。


   >[!NOTE]
   >此後，「內容審核」已更名為「體驗審核」。

   請參閱 [體驗審計測試](/help/implementing/cloud-manager/experience-audit-testing.md) 的子菜單。

* Assets程式中新建立的環境現在將自動配置為Smart Content Services。

* 休眠的環境可以從雲管理器的 **概述** 的子菜單。

* 能夠在頁面上執行體驗檢查，由Google燈塔提供支援。 作為Cloud Manager管道的一部分，最多可以根據體驗KPI檢查和驗證25頁，並且分數顯示在Cloud Manager UI中。

### 錯誤修正 {#bug-fixes-cm}

* 正在執行一些不必要的和不需要的SonarQube插件，作為代碼質量掃描的一部分。

* 在管道執行頁上，分支名稱的格式不正確。

* 在某些情況下，未完成的管道執行未成功記錄為已完成，從而防止了管道的新執行。

* 管道執行偶爾會 *卡住* 內部通信問題。

* 在設定新組織時，系統管理員以外的一些具有管理角色的用戶被錯誤地授予了對Cloud Manager的訪問權限。

* 在某些情況下，更新索引作業被並行多次啟動，導致部署失敗。

* 程式卡上的工具提示不一致。

* 用戶介面錯誤地允許在刪除環境時嘗試操作。

* 雲管理器的 **概述** 的子菜單。

### 已知問題 {#known-issues-cm}

* 包含的無效頁面使內容審核平均分數低於應該的分數。

* 「內容審核」頁籤使用作者域而不是發佈域錯誤地顯示基本URL。

* 要激活「內容審核」步驟，用戶必須編輯管道，並（可選）添加頁面。 如果未添加任何頁面，將審核首頁。
