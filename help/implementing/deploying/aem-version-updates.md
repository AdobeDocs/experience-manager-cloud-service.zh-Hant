---
title: AEM 版本更新
description: 瞭解AEMas a Cloud Service如何使用持續整合和交付(CI/CD)來使項目保持最新版本。
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: 7cdc7bb56565cccc04a2dcb74a6c8088ed4e7847
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 23%

---


# AEM 版本更新 {#aem-version-updates}

瞭解AEMas a Cloud Service如何使用持續整合和交付(CI/CD)來使項目保持最新版本。

## CI/CD {#ci-cd}

AEMas a Cloud Service使用連續整合和連續交付(CI/CD)來確保項目處於最新的AEM版本。 這表示生產和預備執行個體會更新到最新的 AEM 版本，而不會對使用者中斷服務。

版本更新僅自動應用於生產和登台實例。 [必AEM須手動將更新應用於所有其他實例。](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment)

## 更新類型 {#update-types}

AEM 版本更新有兩種類型：

* **AEM 維護更新**

   * 可以每天發行。
   * 主要用於維護目的，包括最新的錯誤修正和安全性更新。
   * 因為定期套用變更，可將影響降至最低。

* **新功能更新**

   * 在 [可預測的，每月計畫。](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)

## 更新失敗 {#update-failure}

更新AEM通過密集且完全自動化的產品驗證管道，涉及多個步驟，確保不中斷生產中任何系統的服務。 運行狀況檢查用於監視應用程式的運行狀況。 如果這些檢查在AEMas a Cloud Service更新期間失敗，則發佈將不繼續，Adobe將調查更新導致此意外行為的原因。

[產品test和客戶功能test,](/help/implementing/cloud-manager/overview-test-results.md#functional-testing) 在版本更新期間，還驗證產品升級和客戶代碼推送不會中斷生AEM產系統。

如果生產環境更新失敗，Cloud Manager 會自動復原預備環境。這是自動完成的，以確保在更新完成後，預備環境和生產環境使用相同的 AEM 版本。

>[!NOTE]
>
>如果將自定義代碼推送到暫存而不是生產，則下AEM次更新將刪除這些更改，以反映上次成功將客戶發佈到生產的git標籤。 因此，必須重新部署僅在暫存中可用的自定義代碼。

## 複合節點儲存 {#composite-node-store}

大多數情況下，更新將導致零停機時間，包括創作實例（即節點群集）。 由於以下原因，可以滾動更新 [複合節點在Oak的儲存功能。](https://jackrabbit.apache.org/oak/docs/nodestore/compositens.html)

此功能允AEM許同時引用多個儲存庫。 在滾動中 [藍綠部署，](/help/implementing/deploying/overview.md#how-rolling-deployments-work) 新的綠色版AEM本包含它自己的 `/libs` （基於TarMK的不變儲存庫），與較舊的藍AEM色版本不同，儘管兩者都引用了包含類似區域的基於DocumentMK的共用可變儲存庫 `/content` 。 `/conf` 。 `/etc` 等等。

因為藍和綠都有自己的版本 `/libs`，它們在滾動更新期間都可以處於活動狀態，這兩種狀態都會佔用通信量，直到藍色被綠色完全替換。
