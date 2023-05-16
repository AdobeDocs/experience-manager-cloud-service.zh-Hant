---
title: AEM 版本更新
description: 了解AEM as a Cloud Service如何使用持續整合和傳送(CI/CD)，讓您的專案保持在最新版本。
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: 59bc2b5af22ef23775195f098517cec40d98d66b
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 23%

---


# AEM 版本更新 {#aem-version-updates}

了解AEM as a Cloud Service如何使用持續整合和傳送(CI/CD)，讓您的專案保持在最新版本。

## CI/CD {#ci-cd}

AEM as a Cloud Service採用持續整合和持續傳送(CI/CD)，確保您的專案使用最新的AEM版本。 這表示生產和預備執行個體會更新到最新的 AEM 版本，而不會對使用者中斷服務。

版本更新只會自動套用至生產和測試執行個體。 [AEM更新必須手動套用至所有其他例項。](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment)

## 更新類型 {#update-types}

AEM 版本更新有兩種類型：

* **AEM 維護更新**

   * 可以每天發行。
   * 主要用於維護目的，包括最新的錯誤修正和安全性更新。
   * 因為定期套用變更，可將影響降至最低。

* **新功能更新**

   * 在 [可預測，每月排程。](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)

## 更新失敗 {#update-failure}

AEM更新會經過密集且完全自動化的產品驗證管道，涉及多個步驟，確保生產中任何系統的服務不會中斷。 運行狀況檢查用於監視應用程式的運行狀況。 如果這些檢查在AEMas a Cloud Service更新期間失敗，則發行將不會繼續，且Adobe會調查更新為何導致此非預期行為。

[產品測試和客戶功能測試，](/help/implementing/cloud-manager/overview-test-results.md#functional-testing) 這可防止產品升級和客戶代碼推送中斷生產系統，也會在AEM版本更新期間驗證。

如果生產環境更新失敗，Cloud Manager 會自動復原預備環境。這是自動完成的，以確保在更新完成後，預備環境和生產環境使用相同的 AEM 版本。

>[!NOTE]
>
>如果自訂程式碼推送至測試環境，而非生產環境，則下次AEM更新會移除這些變更，以反映上次成功客戶發行到生產環境的Git標籤。 因此，只有測試環境上可用的自訂程式碼必須再次部署。

## 複合節點儲存 {#composite-node-store}

多數情況下更新都會導致零停機，包括製作執行個體（節點叢集）。 可能會滾動更新，因為 [複合節點存放區功能。](https://jackrabbit.apache.org/oak/docs/nodestore/compositens.html)

此功能可讓AEM同時參考多個存放庫。 滾動 [藍綠色部署，](/help/implementing/deploying/overview.md#index-management-using-blue-green-deployments) 新的綠色AEM版本包含其專屬的 `/libs` （以TarMK為基礎的不可變存放庫），與舊的藍色AEM版本不同，不過兩者都參考共用以DocumentMK為基礎的可變存放庫，其中包含區域如 `/content` , `/conf` , `/etc` 還有其他。

因為藍色和綠色都有各自的 `/libs`，則兩者皆可在滾動式更新期間處於作用中狀態，且兩者皆會帶來流量，直到藍色完全取代為綠色為止。
