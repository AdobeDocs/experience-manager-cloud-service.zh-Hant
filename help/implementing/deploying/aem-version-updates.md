---
title: AEM版本更新
description: 'AEM版本更新 '
feature: 部署
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---

# AEM版本更新{#aem-version-updates}

## 簡介 {#introduction}

AEM as aCloud Service現在使用「持續整合」和「持續傳送」(CI/CD)，確保您的專案使用最新的AEM版本。 這表示生產和預備執行個體會更新至最新的AEM版本，而不會中斷使用者的服務。

>[!NOTE]
>如果更新至生產環境失敗，Cloud Manager將自動回滾預備環境。 這會自動完成，以確保更新完成後，預備和生產環境都處於相同的AEM版本。

AEM版本更新有兩種類型：

* **AEM推播更新**

   * 可每天發佈。

   * 主要是維護作業，包括最新的錯誤修正和安全性更新。

      由於定期應用更改，因此影響是增量的，因此減少了對服務的影響。

* **新功能更新**

   * 透過可預測的每月排程發佈。

AEM更新會經過密集且完全自動化的產品驗證管道，包含多個步驟，確保生產中的任何系統不會中斷服務。 運行狀況檢查用於監視應用程式的運行狀況。 如果這些檢查在AEM as a Cloud Service更新期間失敗，則發行將不會繼續，且Adobe會調查更新為何造成此非預期行為。

[產品測試和客戶功](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/understand-test-results.html#functional-testing) 能測試可防止產品升級和客戶代碼推送中斷生產，也會在AEM版本更新期間驗證。

>[!NOTE]
>
>如果自訂程式碼推送至測試環境，然後遭到您拒絕，則下次AEM更新會移除這些變更，以反映上次成功客戶發行到生產環境的git標籤。

## 複合節點儲存{#composite-node-store}

如上所述，大部分情況下的更新會造成零停機時間，包括製作（節點叢集）。 由於Oak中的&#x200B;*複合節點存放區*&#x200B;功能，可能會進行滾動更新。

此功能可讓AEM同時參考多個存放庫。 在滾動部署中，新的綠色AEM版本包含其自己的`/libs`（以TarMK為基礎的不可變儲存庫），這與舊的藍色AEM版本不同，不過兩者都參考共用的DocumentMK型可變儲存庫，其中包含`/content` 、 `/conf` 、 `/etc`等區域。 由於藍色和綠色都有各自的`/libs`版本，因此在滾動更新期間，兩者都可以是作用中狀態，在藍色被綠色完全取代之前都會佔用流量。
