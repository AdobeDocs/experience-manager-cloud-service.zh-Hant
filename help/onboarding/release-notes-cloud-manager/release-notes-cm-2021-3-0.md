---
title: Cloud Manager的發行說明，作AEM為Cloud Service版本2021.3.0
description: Cloud Manager的發行說明，作AEM為Cloud Service版本2021.3.0
feature: 發行資訊
exl-id: 42cc9cab-6e66-4976-a3b1-ecb9dbaaabf4
translation-type: tm+mt
source-git-commit: 69694f2067c53667803d38bbf7bc752f3b3afac6
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 2%

---

# Adobe Experience ManagerCloud Manager的發行說明，Cloud Service2021.3.0 {#release-notes}

本頁概述了Cloud Manager的發行說明，AEM作為Cloud Service2021.3.0。

## 發行日期 {#release-date}

Cloud Manager作為2021.3.0Cloud ServiceAEM的發行日期為2021年3月11日。

## Cloud Manager {#cloud-manager}

### 新功能 {#what-is-new}

* 具有[IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md#pre-existing-cdn)、[SSL證書](/help/implementing/cloud-manager/managing-ssl-certifications/check-status-ssl-certificate.md#pre-existing-cdn)和[自訂域名](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn)的現有自訂域名配置的環境的客戶將看到有關其先前現有配置的消息，並能夠通過UI自助服務。

* 具備必要權限的使用者現在可以編輯程式，讓他們以自助方式進行下列作業：
   * 將Sites解決方案新增至包含資產的現有計畫，反之亦然。
   * 將網站或資產從既有的計畫中移除，同時包含網站和資產。
   * 將第二個未使用的解決方案權益新增至現有的方案，或新增為新的方案。

* **現AEM在，「Pipeline執** 行」和「活動」畫面都會顯示推播更新標籤。

* 如果環境已休眠，但也有可用的更AEM新，則&#x200B;**已休眠**&#x200B;狀態將優先於&#x200B;**可用更新**。

* 現在，在導覽至Unified Shell的「使用者設定檔」圖示（右上角）後，使用者可以選取「檢視雲端管理員角色」選項，以查看其Cloud Manager角色。

* **申請批准**&#x200B;標籤已重新標籤至&#x200B;**生產批准**，以更清楚明瞭。

* **版本**&#x200B;標籤已重新標籤至「生產管線」執行畫面中的&#x200B;**Git Tag**。

* 當重要量度不符合定義的臨界值時，定義行為的標籤已重新標籤，以反映其真實行為：**取消立即**&#x200B;和&#x200B;**批准立即**。

* 類別和方法取代清單已根據Cloud ServiceSDK的`2021.3.4997.20210303T022849Z-210225`版AEM本更新。

* Cloud Manager生產管道現在將包含[自訂UI測試](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing)功能。

### 錯誤修正 {#bug-fixes}

* 在推播升級期間，在某些情況下會略過套AEM件版本。

* 在將包嵌入其他包時，未正確發現某些質量問題。

* 在模糊的情況下，開啟「添加程式」對話框時生成的預設程式名稱可能是現有程式名稱的副本。

* 有時，如果用戶在啟動管線後立即導航離開管線執行頁面，則會顯示一條錯誤消息，指出操作失敗，儘管實際上執行開始。

* 當客戶建置導致無效包時，不必要地重新啟動建置步驟。

* 有時，即使未部署IP允許清單，用戶也會看到該配置旁邊的綠色「活動」狀態。

* 所有現有的生產管道都會透過體驗稽核步驟自動啟用。
