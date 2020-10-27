---
title: AEM中Cloud Manager的Cloud Manager版本注意事項2020.8.0版
description: AEM中Cloud Manager的Cloud Manager版本注意事項2020.8.0版
translation-type: tm+mt
source-git-commit: ca690144a8254d5ffba354f0f96d9ef1c5202533
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 1%

---


# Release Notes for Cloud Manager in Adobe Experience Manager as a Cloud Service 2020.8.0 {#release-notes}

本頁概述AEM中Cloud Manager的發行說明，即Cloud Service 2020.8.0。

## 發行日期 {#release-date}

AEM中Cloud Manager作為Cloud Service 2020.8.0的發行日期為2020年8月06日。

## 新功能 {#whats-new-cloud-manager}

* 「內容審核」是在Cloud Manager Sites生產管道上啟用的功能。 具有「網站」的程式的「生產管道」設定現在包含名為「內容審核」的第 **三個標籤**。 每當生產管道執行時，在自訂功能測試後，管道中就會包含新的「內容稽核」步驟，以根據多項維度評估網站，包括效能、搜尋引擎最佳化(SEO)、協助工具、最佳實務和PWA（漸進式網頁應用程式）。


   >[!NOTE]
   >「內容審核」已重新命名為「體驗審核」。

   如需詳細 [資訊，請參閱Experience Audit Testing](/help/implementing/cloud-manager/experience-audit-testing.md) 。

* 「資產」程式中新建立的環境現在會自動設定Smart Content Services。

* 高眠環境可以從Cloud Manager的「概述」頁面中解除高 **眠** 。

* 能夠在Google Lighthouse支援的頁面上執行Experience Checks。 作為Cloud Manager管道的一部分，最多可以根據體驗KPI檢查和驗證25頁，並在Cloud Manager UI中顯示分數。

### 錯誤修正 {#bug-fixes-cm}

* 在程式碼品質掃描中，會執行一些不必要和不需要的SonarQube外掛程式。

* 在管線執行頁面上，分支名稱格式不正確。

* 在某些情況下，未完成的管線執行未成功記錄為已完成，從而防止了管線的新執行。

* 管道執行偶爾會因 *內部* 通訊問題而卡住。

* 在布建新組織時，系統管理員以外的其他管理角色的部分使用者會錯誤地獲得Cloud Manager的存取權。

* 在特定條件下，更新索引作業並行啟動多次，導致部署失敗。

* 程式卡上的工具提示不一致正確。

* 在刪除環境中嘗試操作時，用戶介面錯誤地允許該操作。

* Cloud Manager的「概述」頁面上有顏色不 **符** 。

### 已知問題 {#known-issues-cm}

* 包含無效頁面，使「內容審核平均分數」低於應有的分數。

* 「內容稽核」標籤會使用作者網域而非發佈網域，錯誤地顯示基本URL。

* 若要啟動「內容稽核」步驟，使用者必須編輯管線，並可選擇新增頁面。 如果未新增任何頁面，則會檢查首頁。