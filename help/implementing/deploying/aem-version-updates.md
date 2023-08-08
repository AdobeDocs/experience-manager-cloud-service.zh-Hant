---
title: AEM 版本更新
description: 瞭解AEMas a Cloud Service如何使用持續整合和傳遞(CI/CD)，將您的專案保持在最新版本。
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: ca91e969014415e872ecf8e42fe86ffc9ca41e10
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 9%

---


# AEM 版本更新 {#aem-version-updates}

瞭解AEMas a Cloud Service如何使用持續整合和傳遞(CI/CD)，將您的專案保持在最新版本。

## CI/CD {#ci-cd}

AEMas a Cloud Service使用持續整合和持續傳遞(CI/CD)，以確保您的專案使用最新的AEM版本。 此程式可順暢地更新您的生產、測試和開發執行個體，而不會對使用者造成任何中斷。

在執行個體自動更新之前，新的AEM維護版本會提前3-5天發佈。 在此期間，您可以選擇透過 [觸發開發執行個體的手動更新](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment)在這段時間過後，版本更新會先自動套用至您的開發環境。 如果更新成功，則更新流程會繼續進行您的中繼和生產執行個體。 開發和測試執行個體可作為自動化品質閘道，在生產環境套用更新之前，您可在其中執行自訂編寫的測試。

>[!NOTE]
>
> 注意：開發環境的自動更新將於2023年逐步為所有客戶啟用。 如果您的開發環境未自動更新，則可以使用手動更新，以使其與中繼和生產環境保持同步。


## 更新型別 {#update-types}

AEM 版本更新有兩種類型：

* **AEM 維護更新**

   * 可以每天發行。
   * 主要用於維護目的，包括最新的錯誤修正和安全性更新。
   * 因為定期套用變更，可將影響降至最低。

* **新功能更新**

   * 發行日期 [可預測、每月排程。](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)

## 更新失敗 {#update-failure}

AEM更新會通過密集且完全自動化的產品驗證管道，涉及多個步驟，確保生產中的任何系統不會中斷服務。 健康狀態檢查是用來監視應用程式的健康狀態。 如果這些檢查在AEMas a Cloud Service更新期間失敗，則發行將不會繼續，並且Adobe將會調查更新導致這種意外行為的原因。

當您在環境中部署新版本的自訂程式碼時， [產品和自訂功能測試](/help/implementing/cloud-manager/overview-test-results.md#functional-testing) 在確保生產系統在套用變更後仍保持穩定且運作上扮演關鍵角色。 這些測試也會在AEM版本更新程式中運用。

如果生產環境更新失敗，Cloud Manager 會自動復原中繼環境。這會自動完成，以確保在更新完成後，測試環境和生產環境都會使用相同的AEM版本。
同樣地，如果開發環境的自動更新失敗，則不會更新中繼和生產環境。

>[!NOTE]
>
>如果自訂程式碼推送至測試環境而非生產環境，下次AEM更新會移除這些變更，以反映上次成功客戶發佈至生產環境的Git標籤。 因此，必須再次部署僅可用於中繼的自訂程式碼。

## 最佳做法 {#best-practices}

* 
   * **中繼環境使用**
   * 使用不同的環境（而不是Stage）進行長的QA/UAT週期。
   * 在Stage上完成健全度測試後，移至Production上驗證。

* 
   * **生產管道**
   * 在部署到生產之前暫停。
   * 在中繼部署後取消管道表示程式碼是「一次性」且不是有效的生產候選專案，請參閱 [設定生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md).

* 
   * **非生產管道**
* 設定 [非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code).
* 
   * 加速生產管道故障的傳送速度/頻率。  透過啟用產品功能測試、自訂功能測試和自訂UI測試來識別非生產管道中的問題。

* 
   * **內容複製**
   * 使用 [內容副本](/help/implementing/developing/tools/content-copy.md) 將類似的內容集移動到非生產環境。

* 
   * **自動化功能測試**
* 在您的管道中包含自動化測試，以測試關鍵功能。
* [客戶功能測試](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) 和 [自訂UI測試](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing) 正在封鎖，如果這些訊息失敗，AEM版本將不會推出。

## 回歸 {#regression}

如果您遇到與回歸相關的問題，請透過Admin Console提出支援案例。  如果問題為阻斷因素並影響生產，則應提出P1。  提供重現回歸問題所需的所有詳細資訊。

## 複合節點存放區 {#composite-node-store}

在大多數情況下，更新會產生零停機時間，包括製作執行個體（節點叢集）的停機時間。 滾動更新可能是因為 [Oak中的複合節點存放區功能。](https://jackrabbit.apache.org/oak/docs/nodestore/compositens.html)

此功能可讓AEM同時參照多個存放庫。 在 [滾動式部署，](/help/implementing/deploying/overview.md#how-rolling-deployments-work) 新的AEM版本包含其本身 `/libs` （以TarMK為基礎的不可變存放庫），與舊版AEM不同，不過兩者都參考共用的DocumentMK型可變存放庫，其中包含如區域 `/content` ， `/conf` ， `/etc` 和其他。

因為舊版本和新版本都有各自版本的 `/libs`，則兩者可在滾動更新期間保持作用中狀態，且都可產生流量，直到新完全取代舊流量為止。
