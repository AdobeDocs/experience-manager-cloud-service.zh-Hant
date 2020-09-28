---
title: AEM版本更新
description: 'AEM版本更新 '
translation-type: tm+mt
source-git-commit: ca37f00926fc110b865e6db2e61ff1198519010b
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 0%

---


# AEM版本更新 {#aem-version-updates}

## 簡介 {#introduction}

AEM作為雲端服務現在使用「持續整合」和「持續傳送」(CI/CD)，以確保您的專案位於最新的AEM版本。 這表示所有升級作業都完全自動化，因此使用者不需要中斷任何服務。

>[!NOTE]
>如果更新到生產環境失敗，Cloud Manager將自動回滾階段環境。 這會自動執行，以確保更新完成後，階段和生產環境都位於相同的AEM版本。

AEM版本更新有兩種類型：

* **推播更新**

   * 可以每天發佈。
   * 主要是維護，包括最新的錯誤修正和安全性更新。

   隨著變更的定期套用，影響會逐漸增加，降低對服務的影響。

>[!NOTE]
>若要進一步瞭解AEM推播更新，請參閱 [Adobe Experience Manager As a Cloud Service Continuous Delivery Model的白皮書](https://fieldreadiness-adobe.highspot.com/items/5ea322e1c714336c23b32599#2)

* **新功能更新**

   * 透過可預測的每月排程發佈。

AEM更新會透過密集且完全自動化的產品驗證管道，包括多個步驟，以確保不中斷生產中任何系統的服務。 Health checks are used to monitor the health of the application. 如果這些檢查在AEM的雲端服務更新期間失敗，則發行將無法繼續，Adobe將調查更新為何造成此非預期行為。

[產品測試和客戶功能測試](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/understand-test-results.html#functional-testing) （防止產品升級和客戶程式碼推送中斷生產）也會在AEM版本更新期間進行驗證。

>[注意]
>如果自訂代碼已推送至測試，然後遭到您拒絕，下一次AEM更新會移除這些變更，以反映上次成功客戶發行的git標籤至生產環境。

## 複合節點儲存 {#composite-node-store}

如上所述，在大多數情況下，更新將導致零停機，包括作者（即節點群集）。 由於Oak中的複合節點儲存功能 *，因此可進行滾動更新* 。

此功能可讓AEM同時參考多個儲存庫。 在滾動部署中，新的綠色AEM版本包含其自己的 `/libs` （以TarMK為基礎的不可變儲存庫），與舊版Blue AEM不同，不過兩者都參照共用的DocumentMK可變儲存庫，其中包含 `/content` 、 `/conf``/etc` 、和其他區域。 由於藍色和綠色都有各自的版本 `/libs`，因此在滾動更新期間，兩者都可以處於活動狀態，在藍色完全被綠色取代之前，都會進行流量。

