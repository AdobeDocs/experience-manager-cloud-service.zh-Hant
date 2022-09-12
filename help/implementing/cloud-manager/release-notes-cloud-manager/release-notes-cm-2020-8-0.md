---
title: AEM as a Cloud Service2020.8.0版中Cloud Manager發行說明
description: AEM as a Cloud Service2020.8.0版中Cloud Manager發行說明
feature: Release Information
exl-id: 70674e16-f9ba-4777-98fe-34161e90a481
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 1%

---

# Adobe Experience Manager as a Cloud Service 2020.8.0版Cloud Manager發行說明 {#release-notes}

本頁概述AEM 2020.8.0as a Cloud Service版中Cloud Manager的發行說明。

## 發行日期 {#release-date}

AEM 2020.8.0中的Cloud Manageras a Cloud Service日期為2020年8月6日。

## 新增功能 {#whats-new-cloud-manager}

* 內容稽核是在Cloud Manager Sites生產管道中啟用的功能。 使用Sites的程式的生產管道設定現在包含第三個索引標籤，名為 **內容稽核**. 生產管道執行期間，只要自訂功能完成測試，管道中就會增加新的內容稽核步驟，以根據多項維度評估網站，包括效能、SEO（搜尋引擎最佳化）、協助工具、最佳作法和PWA（漸進式網頁應用程式）。


   >[!NOTE]
   >「內容稽核」後來已重新命名為「體驗稽核」。

   請參閱 [體驗稽核測試](/help/implementing/cloud-manager/experience-audit-testing.md) 以取得更多詳細資訊。

* Assets程式中新建立的環境現在會自動透過智慧內容服務進行設定。

* 您可以從Cloud Manager的 **概述** 頁面。

* 能在頁面上執行Experience Check(由Google Lighthouse提供技術支援)。 在Cloud Manager管道中，最多可根據體驗KPI檢查及驗證25個頁面，分數會顯示在Cloud Manager UI中。

### 錯誤修正 {#bug-fixes-cm}

* 在程式碼品質掃描中，會執行一些不必要的SonarQube外掛程式。

* 在管道執行頁面上，分支名稱的格式不正確。

* 在某些情況下，完成的管道執行未被成功記錄為已完成，從而防止了管道的新執行。

* 管道執行偶爾會 *卡住* 因內部通訊問題。

* 布建新組織時，系統管理員以外的其他管理角色的某些使用者會錯誤地獲得Cloud Manager的存取權。

* 在某些情況下，更新索引作業同時啟動多次，導致部署失敗。

* 程式卡上的工具提示不一致。

* 在刪除某個環境時，用戶介面錯誤地允許在該環境中嘗試操作。

* Cloud Manager的 **概述** 頁面。

### 已知問題 {#known-issues-cm}

* 包含的頁面無效，使得「內容稽核平均分數」低於應有的分數。

* 「內容稽核」索引標籤使用作者網域（而非發佈網域），錯誤地顯示基本URL。

* 若要啟用「內容稽核」步驟，使用者必須編輯管道，並選擇性地新增頁面。 如果未新增任何頁面，則會稽核首頁。
