---
title: 版AEM本更新
description: '版AEM本更新 '
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 0%

---

# 版AEM本更新 {#aem-version-updates}

## 簡介 {#introduction}

AEMas a Cloud Service現在使用連續整合和連續交付(CI/CD)來確保您的項目處於最新的AEM版本。 這意味著生產實例和階段實例將更新為最AEM新版本，而不會中斷用戶服務。

>[!NOTE]
>如果更新到生產環境失敗，Cloud Manager將自動回滾該階段環境。 此操作將自動執行，以確保更新完成後，階段環境和生產環境都處於同一AEM版本。

版AEM本更新有兩種類型：

* **推送AEM更新**

   * 可以每天發佈。

   * 主要是維護，包括最新的錯誤修復和安全更新。

      由於定期應用更改，因此影響是遞增的，因此減少了對服務的影響。

* **新功能更新**

   * 通過可預測的每月計畫發佈。

更新AEM通過密集且完全自動化的產品驗證流水線，涉及多個步驟，確保不中斷生產中任何系統的服務。 運行狀況檢查用於監視應用程式的運行狀況。 如果這些檢查在AEMas a Cloud Service更新期間失敗，則發佈將不繼續，Adobe將調查更新導致此意外行為的原因。

[產品test和客戶功能test](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/understand-test-results.html#functional-testing) 在版本更新期間，還驗證了防止產品升級和客戶代碼推送不中斷生AEM產的功能。

>[!NOTE]
>
>如果將自定義代碼推送到暫存，然後您拒絕，則下AEM次更新將刪除這些更改，以反映上次成功的客戶發佈到生產的git標籤。

## 複合節點儲存 {#composite-node-store}

如上所述，大多數情況下的更新將導致零停機時間，包括作者的停機時間，作者是一個節點群集。 可以滾動更新，因為 *複合節點儲存* 在奧克郡。

此功能允AEM許同時引用多個儲存庫。 在滾動部署中，新的綠色版AEM本包含其自己的 `/libs` （基於TarMK的不變儲存庫），與舊版藍AEM色版本不同，儘管兩者都引用了包含類似 `/content` 。 `/conf` 。 `/etc` 等等。 因為藍和綠都有自己的版本 `/libs`，它們在滾動更新期間都可以處於活動狀態，這兩種狀態都會佔用通信量，直到藍色被綠色完全替換。
