---
title: AEM版本更新
description: 'AEM版本更新 '
feature: Deploying
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---


# AEM版本更新{#aem-version-updates}

## 簡介 {#introduction}

作AEM為Cloud Service，現在使用「持續整合與持續傳送」(CI/CD)來確保您的專案使用最新AEM版本。 這表示Production和Stage實例會更新為最新版本，AEM而不會中斷用戶的服務。

>[!NOTE]
>如果更新到生產環境失敗，Cloud Manager將自動回滾階段環境。 這會自動執行，以確保更新完成後，階段和生產環境都位於同一版AEM本。

版本AEM更新有兩種類型：

* **推AEM送更新**

   * 可以每天發佈。

   * 主要是維護，包括最新的錯誤修正和安全性更新。

      隨著變更的定期套用，影響會逐漸增加，降低對服務的影響。

* **新功能更新**

   * 透過可預測的每月排程發佈。

更新AEM會透過密集且完全自動化的產品驗證管道，包括多個步驟，以確保不中斷生產中任何系統的服務。 Health checks are used to monitor the health of the application. 如果這些檢查在Cloud Service更AEM新期間失敗，則發行將不繼續，Adobe將調查更新為何導致此意外行為。

[產品測試和防止產](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/understand-test-results.html#functional-testing) 品升級和客戶程式碼推動中斷生產的客戶功能測試也會在版本更新期間AEM進行驗證。

>[!NOTE]
>
>如果自訂代碼推送至測試，然後您拒絕，下AEM次更新將移除這些變更，以反映上次成功客戶發行的git標籤至生產環境。

## 複合節點儲存{#composite-node-store}

如上所述，在大多數情況下，更新將導致零停機，包括作者（即節點群集）。 由於Oak中的&#x200B;*複合節點store*&#x200B;功能，因此可進行滾動更新。

此功能允許AEM同時引用多個儲存庫。 在滾動部署中，新的綠色版本包含其自己的`/libs`（基於TarMK的不可變儲存庫），與舊的藍AEM色版本不同，儘管兩者都引用了共用的基於DocumentMK的可變儲存庫，該儲存庫包含`/content`、`/conf`、`/etc`等區域。 由於藍色和綠色都有各自的`/libs`版本，因此在滾動更新期間它們都可以處於活動狀態，在藍色被綠色完全替換之前，它們都會保持通信。

