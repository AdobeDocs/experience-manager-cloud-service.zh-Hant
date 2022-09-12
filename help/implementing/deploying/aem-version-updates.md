---
title: AEM版本更新
description: AEM版本更新
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: 575be022704e998e63162f19c37ece877efef627
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---


# AEM版本更新 {#aem-version-updates}

## 簡介 {#introduction}

AEM as a Cloud Service現在使用持續整合和持續傳送(CI/CD)，確保您的專案使用最新的AEM版本。 這表示生產和測試執行個體會更新為最新的AEM版本，使用者的服務不會中斷。

>[!NOTE]
>
>如果生產環境更新失敗，Cloud Manager會自動復原預備環境。 這會自動完成，以確保更新完成後，測試環境和生產環境都使用相同的AEM版本。

AEM版本更新有兩種類型：

* **AEM維護更新**

   * 可每天發佈。
   * 主要用於維護用途，包括最新的錯誤修正和安全性更新。
   * 影響最小，因為會定期套用變更。

* **新功能更新**

   * 會透過可預測的每月排程發佈。

AEM更新會經過密集且完全自動化的產品驗證管道，涉及多個步驟，確保生產中任何系統的服務不會中斷。 運行狀況檢查用於監視應用程式的運行狀況。 如果這些檢查在AEMas a Cloud Service更新期間失敗，則發行將不會繼續，且Adobe會調查更新為何導致此非預期行為。

[產品測試和客戶功能測試，](/help/implementing/cloud-manager/overview-test-results.md#functional-testing) 這可防止產品升級和客戶代碼推送中斷生產系統，也會在AEM版本更新期間驗證。

>[!NOTE]
>
>如果自訂程式碼推送至測試環境，然後遭到您拒絕，則下次AEM更新會移除這些變更，以反映上次成功客戶發行到生產環境的git標籤。

## 複合節點儲存 {#composite-node-store}

多數情況下更新都會導致零停機，包括製作執行個體（節點叢集）。 由於Oak中的複合節點存放區功能，可能會進行滾動更新。

此功能可讓AEM同時參考多個存放庫。 在滾動式部署中，新的綠色AEM版本包含其自己的 `/libs` （以TarMK為基礎的不可變存放庫），與舊的藍色AEM版本不同，不過兩者都參考共用以DocumentMK為基礎的可變存放庫，其中包含區域如 `/content` , `/conf` , `/etc` 還有其他。 因為藍色和綠色都有各自的 `/libs`，則兩者皆可在滾動式更新期間處於作用中狀態，且兩者皆會帶來流量，直到藍色完全取代為綠色為止。
