---
title: AEM 版本更新
description: 瞭解Adobe Experience Manager (AEM) as a Cloud Service如何使用持續整合和交付(CI/CD)，將您的專案保持在最新版本。
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
role: Admin
source-git-commit: 01de7b0c4e0408a3bbc5322e37db5075d43c4c5f
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 2%

---


# AEM 版本更新 {#aem-version-updates}

瞭解Adobe Experience Manager (AEM) as a Cloud Service如何使用持續整合和交付(CI/CD)，將您的專案保持在最新版本。

## CI/CD {#ci-cd}

AEM as a Cloud Service使用持續整合和持續傳遞(CI/CD)，以確保您的專案使用最新的AEM版本。 此程式可順暢地更新您的生產、測試和開發執行個體，而不會對使用者造成任何中斷。

>[!NOTE]
> 由於開發執行個體已自動更新，因此您的程式中的&#x200B;_部分_&#x200B;可能無法使用開發執行個體的手動更新。 此功能正在轉換為自動更新。

在執行個體自動更新之前，新的AEM維護版本會提前3-5天發佈。 在這段期間，您的開發執行個體可能會自動更新，如果可用，您可以選擇性[觸發開發執行個體的更新](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment)。 版本更新會先自動套用至您的開發環境。 如果更新成功，則更新流程會繼續進行您的中繼和生產執行個體。 開發和測試執行個體可作為自動化品質閘道，在生產環境套用更新之前，您可在其中執行自訂編寫的測試。

### NIMU （非侵入式維護更新） {#nimu}

非侵入式維護更新是自動更新，不會涉及客戶管道。
透過NIMU，客戶隨時可以使用管道，即使AEM版本更新已排程或進行中，且維護更新將不再出現在客戶管道執行歷史記錄中，讓您更輕鬆地追蹤程式碼部署歷史記錄。

#### 更新活動

和以前一樣，您仍可以使用AEM UI環境面板，為每個環境檢查目前的Cloud Manager版本。 非侵入式維護更新（包括客戶書面測試）會使用管道中使用的相同品質閘道。
每當非侵入式維護更新套用至您的程式環境時，就會傳送[Cloud Manager UI通知](/help/implementing/cloud-manager/notifications.md)。 您可以將其設定為也傳送至您的電子郵件。

>[!NOTE]
>
> 注意：非侵入式維護更新將於2024年逐步開放所有客戶使用。

## 更新型別 {#update-types}

AEM 版本更新有兩種類型：

* [**AEM維護更新**](/help/release-notes/maintenance/latest.md)

   * 這些更新主要用於維護目的，包括最新的錯誤修正和安全更新。
   * 變更會定期套用，因此影響最小。

* [**AEM功能啟動**](/help/release-notes/release-notes-cloud/release-notes-current.md)

   * 它們會依照可預測的每月排程發行。

>[!NOTE]
>
> 檢查[Experience Manager發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=zh-Hant#aem-as-cloud-service)上每月發行的重要日期，並標示您的行事曆，為關鍵活動做好準備以便發行。

## 更新失敗 {#update-failure}

AEM更新會通過密集且完全自動化的產品驗證管道，涉及多個步驟，確保生產中的任何系統不會中斷服務。 健康狀態檢查是用來監視應用程式的健康狀態。 如果這些檢查在AEM as a Cloud Service更新期間失敗，則發行不會繼續，並且Adobe會調查更新導致這種意外行為的原因。

當您在環境中部署新版本的自訂程式碼時，[產品與自訂功能測試](/help/implementing/cloud-manager/overview-test-results.md#functional-testing)將扮演重要角色。 它們可確保在套用變更後，生產系統仍保持穩定且功能正常。 這些測試也會套用至AEM版本更新程式。

如果對生產環境的更新失敗，Cloud Manager會自動回滾中繼環境。 這會自動完成，以確保在更新完成後，測試環境和生產環境都會採用相同的AEM版本。
同樣地，如果開發環境的自動更新失敗，則不會更新中繼和生產環境。

>[!NOTE]
>
>如果自訂程式碼推送至測試環境而非生產環境，下次AEM更新會移除這些變更，以反映上次成功客戶發佈至生產環境的Git標籤。 因此，必須再次部署僅可用於中繼的自訂程式碼。

## 最佳做法 {#best-practices}

* **中繼環境使用量**
   * 使用不同的環境（而不是Stage）進行長的QA/UAT週期。
   * 在Stage上完成健全度測試後，移至Production上驗證。

* **生產管道**
   * 在部署到生產之前暫停。
   * 在中繼部署後取消管道表示程式碼是「轉寄」且不是有效的生產候選專案，請參閱[設定生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)。

* **非生產管道**
   * 設定[非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code)。
   * 加速生產管道故障的傳送速度/頻率。 透過啟用產品功能測試、自訂功能測試和自訂UI測試來識別非生產管道中的問題。

* **內容副本**
   * 使用[內容副本](/help/implementing/developing/tools/content-copy.md)將類似的內容集移動至非生產環境。

* **自動化功能測試**
   * 在您的管道中包含自動化測試，以便您測試關鍵功能。
   * [客戶功能測試](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)和[自訂UI測試](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing)如果失敗，則會遭到封鎖，AEM版本不會推出。

## 回歸 {#regression}

如果您遇到與回歸相關的問題，請透過Admin Console提交支援案例。 如果問題為阻斷因素及其影響的生產，則應引發P1。 提供重現回歸問題所需的所有詳細資訊。

## 複合節點存放區 {#composite-node-store}

通常，更新會產生零停機時間，包括編寫執行個體（節點叢集）的更新。 因為[Oak](https://jackrabbit.apache.org/oak/docs/nodestore/compositens.html)中的複合節點存放區功能，所以可能會進行滾動更新。

此功能可讓AEM同時參照多個存放庫。 在[滾動式部署](/help/implementing/deploying/overview.md#how-rolling-deployments-work)中，新的AEM版本包含它自己的`/libs` （以TarMK為基礎的不可變存放庫）。 它與舊版AEM不同，不過兩者都參考共用DocumentMK型可變存放庫，其中包含`/content`、`/conf`、`/etc`等區域。

由於舊版本和新版本都有各自的`/libs`版本，因此在滾動更新期間它們都可以處於作用中狀態。 此外，兩者都可以承擔流量，直到新完全取代舊版為止。

## 更多資訊 {#further-information}

如需相關主題的詳細資訊：

* [Cloud Manager CI/CD 管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)
* [Cloud Manager UI通知](/help/implementing/cloud-manager/notifications.md)
* [Adobe Experience Manager as a Cloud Service架構](/help/overview/architecture.md)
