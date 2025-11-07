---
title: 實施階段
description: 確定您的程式碼和內容已準備好移轉至雲端
exl-id: d124f9a5-a754-4ed0-a839-f2968c7c8faa
feature: Migration
role: Admin
source-git-commit: 2e257634313d3097db770211fe635b348ffb36cf
workflow-type: tm+mt
source-wordcount: '2288'
ht-degree: 9%

---

# 實施階段 {#implementation-phase}

在歷程的實作階段，您將探索可用來讓程式碼和內容準備好移至AEM as a Cloud Service的工具。

## 目前進度 {#story-so-far}

在歷程的上一部分中，您已通過[熟悉AEM as a Cloud Service](/help/journey-migration/getting-started.md)中的變更，並判斷您的部署是否已準備好移至雲端，並具有[整備階段](/help/journey-migration/readiness.md)。

本文繼續就如何使用Adobe提供的工具，以確保您的程式碼和內容已準備好移至雲端提供建議。

## 目標 {#objective}

本檔案旨在：

* 向您介紹Cloud Manager，AEM用來將程式碼部署到AEM as a Cloud Service的持續整合和傳送架構
* 透過內容轉移工具，讓您快速上手
* 說明您必須使用的程式碼重構工具，以便匯入最新的AEM as a Cloud Service程式碼

## 使用Cloud Manager {#using-cloud-manager}

開始之前，您必須先熟悉Cloud Manager，因為這是將程式碼部署至AEM as a Cloud Service的唯一機制。

Cloud Manager 可讓組織在雲端中自行管理 AEM。其內容包含持續整合與持續傳送 (CI/CD) 架構，可讓 IT 團隊與實作合作夥伴加快提供自訂或更新的傳送速度，而不會影響效能或安全性。

您可以參閱下列資源，以熟悉Cloud Manager的使用：

* [入門歷程](/help/journey-onboarding/overview.md)，瞭解有關Experience Manager as a Cloud Service入門的自助資源。

* [整合 Git 與 Adobe Cloud Manager](/help/implementing/cloud-manager/managing-code/integrating-with-git.md)，了解如何使用 Single Git 存放庫來部署程式碼。

* [Adobe Experience as a Cloud Service 設定](/help/security/ims-support.md#aem-configuration)，了解如何「在 Admin Console 中管理產品與使用者存取」。

## 使用Adobe提供的工具，讓您的內容和程式碼雲端就緒 {#use-tools-to-make-code-and-content-cloud-ready}

轉換至Cloud Service的確切步驟取決於您購買的系統，以及所遵循的軟體開發生命週期作法。

下圖顯示階段中涉及轉換程式碼和內容以用於AEM as a Cloud Service的主要步驟：

![轉換步驟](/help/journey-migration/assets/exec-image1.png)

我們將在以下章節開始詳細說明您必須使用的工具，讓您能夠達成此目標。

## 內容移轉 {#content-migration}

若要將內容從您目前的AEM例項移轉至Cloud Service例項，您可以使用Adobe的「內容轉移工具」。

使用此工具，即可指定想從您的 AEM 例項轉移至雲端服務例項的內容。

內容移轉是多步驟的流程，需要規劃、追蹤以及不同團隊之間的共同作業。

如需此工具如何運作以及Adobe建議您如何使用的完整詳細資訊，請參閱[內容轉移工具檔案](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md)。

## 程式碼重構 {#code-refactor}

### 為開發設定 {#set-up-for-development}

是時候開始重構現有功能以與雲端服務相容了。

首先，檢視詳細說明基本工具的檔案，然後開始重構您的程式碼：


* 在規劃期間，建議您先列出必須重構以便與AEM as a Cloud Service相容的區域。 您可以檢閱[開發指導方針](/help/implementing/developing/introduction/development-guidelines.md)，以取得有關如何重構和最佳化Cloud Service程式碼的詳細資訊。
* 閱讀如何在AEM as a Cloud Service中[管理設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/configurations.html?lang=zh-Hant#what-is-a-configuration)。
* 瞭解如何下載[AEM as a Cloud Service SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=zh-Hant)來設定本機開發環境
* 最後，請熟悉[AEM as a Cloud Service Java API](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html)。

您也可以：

* 觀看此影片以瞭解如何在本機安裝Dispatcher SDK：

  >[!VIDEO](https://video.tv.adobe.com/v/30601)

* 觀看此影片以瞭解如何設定Dispatcher SDK：

  >[!VIDEO](https://video.tv.adobe.com/v/30602)

### 心態的改變 {#a-change-in-mindset}

在AEM as a Cloud Service中開發及執行程式碼時必須改變心態。 請注意，程式碼必須具復原性，特別是因為例項可能隨時停止。您必須了解，在雲端服務中執行程式碼時，一律會在叢集中執行。這表示執行中的例項永遠多於一個。

AEM Maven專案若要與雲端相容，必須進行某些變更。 AEM as a Cloud Service需要將&#x200B;*內容*&#x200B;和&#x200B;*程式碼*&#x200B;分離為不同的套件，才能部署至AEM：

* `/apps`和`/libs`在AEM中被視為不可變區域，因為在AEM啟動後（也就是說，在執行階段）就無法變更它們。 這包括建立、更新或刪除作業。 在運行時更改不可變區域的任何嘗試都將失敗。

* 存放庫中的所有其他專案（例如，`/content` 、 `/conf` 、 `/var` 、 `/home` 、 `/etc` 、 `/oak:index` 、 `/system` 、 `/tmp`）都是可變區域，這表示可在執行階段變更這些區域。

您可以參閱[建議的封裝結構](/help/implementing/developing/introduction/aem-project-content-package-structure.md#recommended-package-structure)檔案以深入瞭解。


### 雲端移轉工具 {#cloud-migration-tools}

Adobe提供數種工具，可協助您加速部分程式碼重構任務。 瞭解這些工具及其解決的問題將降低移轉的複雜性和時間。

* [資產工作流程移轉](/help/journey-migration/moving-to-aem-assets/asset-workflow-migration-tool.md)，此工具可用來自動移轉資產處理工作流程
* [Dispatcher Converter](/help/journey-migration/refactoring-tools/dispatcher-transformation-utility-tools.md)，此工具會將您現有的Dispatcher設定轉換成可供AEM as a Cloud Service使用的格式。
* [Repository Modernizer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/moving/refactoring-tools/repo-modernizer.html?lang=zh-Hant)，此工具會將AEM多模式專案當作輸入，並將其轉換為AEM as a Cloud Service專案
* [索引轉換器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/moving/refactoring-tools/index-converter.html?lang=zh-Hant)，此工具會將索引轉換為與AEM as a Cloud Service相容的表單
* [現代化工具](/help/journey-migration/refactoring-tools/aem-modernization-tools.md)，這是一套公用程式，可用來將舊版AEM功能轉換為AEM as a Cloud Service的現代化且受支援的功能。

設定本機開發環境後，請參閱[檔案](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)以熟悉AEM as a Cloud Service SDK。

### 排程程式碼凍結 {#schedule-a-code-freeze}

若要管理您正在作用中AEM上開發的程式碼，以及轉換過程中的程式碼重構任務，Adobe建議您排程程式碼凍結期間，直到您的Maven專案重建完畢、可以與AEM as a Cloud Service相容為止。

專案一旦重建完畢，您就可以根據這個新結構繼續新的程式碼開發。 這可減少Cloud Manager管道在程式碼部署和測試期間的故障情形。

>[!NOTE]
>「內容轉移」和「程式碼重新調整」工作不必依序完成。 這些任務可以各自獨立完成。不過，您需要正確的專案結構，以確保內容能在雲端服務環境中成功轉譯。

## 程式碼部署和測試的最佳作法 {#best-practices}

Cloud Manager管道支援執行針對預備環境執行的測試。

遵循以下檔案中有關程式碼品質測試的最佳實務：

* [程式碼品質測試](/help/implementing/cloud-manager/code-quality-testing.md)，說明編寫測試指令碼的程式，並說明建議涵蓋範圍至少50%的概念。
* [瞭解自訂程式碼品質規則](/help/implementing/cloud-manager/custom-code-quality-rules.md)，此規則旨在說明Cloud Manager根據AEM Engineering最佳作法建立並執行的自訂程式碼品質規則。

## 準備上線 {#preparing-for-go-live}

準備來源系統以進行移轉涉及系統和AEM管理員層級的工作。 您可以檢查[修訂清理](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html?lang=zh-Hant)和[資料存放區記憶體回收](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/data-store-garbage-collection.html?lang=zh-Hant)工作狀態，以驗證內容存放庫是否處於維護良好的狀態。 如果您執行AEM 6.3版（因為「內容轉移工具」與6.3版以後相容），建議執行離線壓縮，然後進行「資料存放區記憶體回收」。

建議在所有AEM版本中進行[資料一致性檢查](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/consistency-check.html?lang=zh-Hant)，以確保內容存放庫處於良好的狀態，可以啟動移轉活動。

需要系統管理員層級存取權才能安裝和設定[AZCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md)

建議您檢閱任何未使用的Assets、頁面、AEM專案、使用者和群組，以節省移轉時間。 請參閱[內容存放庫健全狀況](#repository-health)區段。

### 內容存放庫健全狀況 {#repository-health}

建立[生產複製](#proof-of-migration)的存取權後，請繼續檢查存放庫的健康狀態。 如上一節所述，目標是在開始移轉之前，清理並壓縮來源上的存放庫。 此步驟可能會節省大量時間，否則會在移轉開始時用於疑難排解問題。

| 動作專案 | 關鍵重點 |
|---------|----------|
| 使用者、群組和許可權 | 您需要瞭解成員資格的使用者數量、群組和複雜性。 在移轉之前，尋找機會清理來源中未使用的使用者和群組。 |
| 未完成的資產處理 | 嘗試在開始移轉前完成來源系統中的資產處理，以避免移轉後AEM as a Cloud Service中潛在的問題。 |
| 內容健康狀態 | 建議您在開始移轉之前，先查詢並清除不良內容。 例如，尋找沒有原始轉譯或卡在工作流程處理的資產或頁面。 另請參閱[資產健康狀態](#asset-health)。 |

## 正在收集資料 {#gathering-data}

>[!NOTE]
> [內容移轉策略與時間表](#content-strategy-and-timeline)部分進一步詳細說明如何推斷收集的資料並建立移轉計畫。

收集資料可協助您規劃移轉活動和相關工作。 擷取和內嵌時間尤其實用，因為資料點可與移轉集的特定大小相關聯。 因此，這些資料點可外推以得出計畫：

* [擷取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md)所花費的總時間
* [擷取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)所花費的總時間
* 加值[擷取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)所花費的總時間
* 加值[擷取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process)所花費的總時間


<!-- Alexandru: hiding this for now

One more important datapoint is the amount of time it takes to complete the [user mapping](/help/journey-migration/content-transfer-tool/user-mapping-tool/overview-user-mapping-tool.md), if this is coupled with the content migration. You can take this data point into consideration for more realistic estimates, because it is added to the overall extraction timeline and it may not be required to run it during top-ups.

-->

這些資料點也可協助您[建立KPI](/help/journey-migration/readiness.md#establish-kpis)和其他移轉相關工作。

### 移轉計畫 {#migration-plan}

根據您收集的資料點（請參閱上文），您可以建立可整合至巨集專案計畫的移轉計畫。 此步驟可讓所有主要利害關係人針對移轉活動進行視覺化呈現和規劃。

下表說明典型的移轉計畫：

| 移轉反複專案 | 開始日期 | 估計結束日期 | 相依性 | 估計期間（以天為單位） | 其他明細/行動專案 |
|---|---|---|---|---|---|
| PRDCLONE-AUTHOR-INITIAL-USRMAP-CSSTAGE-AUTHOR |   |   |   |   |   |
| PRDCLONE-PUBLISH-TOP-UP-CSSTAGE-AUTHOR |   |   |   |   |   |

如上表所示，遵循特定命名格式以識別移轉反複專案很有幫助，例如：來源AEM環境為&#x200B;**PRDCLONE**、AEM as a Cloud Service環境為&#x200B;**AUTHOR/PUBLISH**、AEM as a Cloud Service執行個體為&#x200B;**CSSTAGE-AUTHOR**&#x200B;等等。

影響移轉計畫的一些重要細節：

**所需的擷取總數**

* 在特定環境中製作和發佈擷取會視為兩個平行擷取，因為它們彼此獨立。
* 根據特定時段中存放庫增長的追加擷取次數。

**所需的內嵌總數**

* 請務必將此專案擷取至計畫中，因為擷取的集合可內嵌至多個Cloud Service環境中。
* 追加擷取次數。
* 將內容從Source Author移轉至Cloud Service Author例項，以及從Source Publish移轉至Cloud Service Publish是避免將所有Author內容內嵌至Cloud Service Publish的最佳作法。

### 移轉追蹤器 {#migration-tracker}

您可以使用移轉追蹤器來記錄初始和追加執行的時間。 這些資料點將幫助您在最後的追加之前制定現實的內容凍結要求。

此追蹤器也可協助您：

* 識別供需規劃員需要調整計畫或上線時間表的任何偏差
* 提供可用於所有必要通訊的真實狀態
* 規劃初始或未來的追加移轉

下表說明功能性的移轉追蹤器：

| Source （環境/執行個體/URL） | 目的地（環境/執行個體/URL） | 移轉集名稱、型別（初始或追加） | 移轉集大小(MB) | 使用者對應（是/否） | 擷取持續時間（開始、結束、花費時間） | 擷取持續時間（開始、結束、花費時間） | 問題/解決方案/詳細資訊 |
|---|---|---|---|---|---|---|---|
|   |   |   |   |   |   |   |   |

## 內容移轉策略和時間表 {#content-strategyand-timeline}

下節顯示可用於制定內容移轉策略和時間表的重要步驟和相關工作。

![制定移轉策略的步驟](/help/journey-migration/assets/content-migration2.png)

### 裝置 {#fitment}

* 執行修訂清理、資料存放區記憶體回收和資料一致性檢查。 另請參閱[準備上線](#preparing-for-go-live)
* [收集有關AEM來源存放庫的統計資料](#gathering-data)：
   * 區段存放區大小
   * 索引存放區大小
   * 頁數
   * 資產數量
   * 使用者和群組數目
* 瞭解是否在AEM來源上啟用下列功能(AEM as a Cloud Service也需要)：
   * 智慧標籤
   * 相似性搜尋
   * 搜尋包含Word和PDF檔案中的文字
* 收集最佳做法分析工具[報告](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md)
* 匯入[Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/introduction/overview-cam.md)
   * 請檢閱自我分析建議，以確保AEM as a Cloud Service可處理儲存需求。
* 在繼續移轉計畫之前，請先建立Adobe支援票證以供澄清。

### 移轉證明 {#proof-of-migration}

* 請求符合以下條件的生產複製：
   * 位於相同的網路區域
   * 將提供使用者和群組之類的生產內容
   * 復製作者和發佈 — 若是叢集或發佈伺服器陣列，則各一個節點
* 選擇已移轉內容的子集，以便：
   * 而是所有可用內容型別的組合
   * 包含所有使用者和群組
* 包含25%的內容或最多1 TB的內容（以較小者為準）。
* 從生產複製移轉至AEM as a Cloud Service非生產環境，至少執行一次完整和[追加](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process)移轉
* 解決任何潛在問題，例如：
   * AEM來源上的磁碟空間
   * AEM來源與AEM as a Cloud Service之間的連線
   * 任何[內嵌相關限制](go-live.md#known-limitations)。
* 記錄[擷取與擷取](#gathering-data)所花的時間：
   * 瞭解每週新增多少內容
   * 推斷從移轉證明所測量的時間，以建立[移轉計畫](#migration-plan)。

## 後續步驟 {#what-is-next}

在您完全瞭解如何評估您的AEM安裝是否已準備好移至雲端後，當我們瞭解如何使用所需的工具讓安裝準備就緒時，您就可以移至[上線階段](/help/journey-migration/go-live.md)。
