---
title: 版AEM本更新
description: '版AEM本更新 '
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: 575be022704e998e63162f19c37ece877efef627
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---


# 版AEM本更新 {#aem-version-updates}

## 簡介 {#introduction}

AEMas a Cloud Service現在使用連續整合和連續交付(CI/CD)來確保項目處於最新的AEM版本。 這意味著生產實例和交叉實例將更新為最AEM新版本，而不會中斷用戶服務。

>[!NOTE]
>
>如果更新到生產環境失敗，Cloud Manager將自動回退登台環境。 此操作將自動執行，以確保在更新完成後，轉移環境和生產環境都處於同一AEM版本。

有兩種版本更AEM新類型：

* **維AEM護更新**

   * 可以每天發佈。
   * 主要用於維護目的，包括最新的錯誤修復和安全更新。
   * 由於定期應用更改，因此影響最小。

* **新功能更新**

   * 通過可預測的每月計畫發佈。

更新AEM通過密集且完全自動化的產品驗證管道，涉及多個步驟，確保不中斷生產中任何系統的服務。 運行狀況檢查用於監視應用程式的運行狀況。 如果這些檢查在AEMas a Cloud Service更新期間失敗，則發佈將不繼續，Adobe將調查更新導致此意外行為的原因。

[產品test和客戶功能test,](/help/implementing/cloud-manager/overview-test-results.md#functional-testing) 在版本更新期間，還驗證產品升級和客戶代碼推送不會中斷生AEM產系統。

>[!NOTE]
>
>如果將自定義代碼推送到暫存，然後您拒絕，則下AEM次更新將刪除這些更改，以反映上次成功的客戶發佈到生產的git標籤。

## 複合節點儲存 {#composite-node-store}

大多數情況下，更新將導致零停機時間，包括創作實例（即節點群集）。 由於Oak中的複合節點儲存功能，可以滾動更新。

此功能允AEM許同時引用多個儲存庫。 在滾動部署中，新綠AEM色版本包含其自己 `/libs` （基於TarMK的不變儲存庫），與較舊的藍AEM色版本不同，儘管兩者都引用了包含類似區域的基於DocumentMK的共用可變儲存庫 `/content` 。 `/conf` 。 `/etc` 等等。 因為藍和綠都有自己的版本 `/libs`，它們在滾動更新期間都可以處於活動狀態，這兩種狀態都會佔用通信量，直到藍色被綠色完全替換。
