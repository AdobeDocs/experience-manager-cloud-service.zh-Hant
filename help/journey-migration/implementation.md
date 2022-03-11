---
title: 實施階段
description: 確保您的代碼和內容已準備好遷移到雲
exl-id: d124f9a5-a754-4ed0-a839-f2968c7c8faa
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '2422'
ht-degree: 9%

---

# 實施階段 {#implementation-phase}

在此過程的實施階段，您將探索各種工具，通過這些工具，您可以隨時將代碼和內容移至AEMas a Cloud Service。

## 到目前為止的故事 {#story-so-far}

在前一段旅程中， [熟悉as a Cloud Service的變AEM化](/help/journey-migration/getting-started.md)，以及確定您的部署是否已準備好隨 [就緒階段](/help/journey-migration/readiness.md)。

本文繼續就如何使用Adobe提供的工具來確保您的代碼和內容已準備好移至雲提供建議。

## 目標 {#objective}

本文旨在：

* 向您介紹Cloud Manager、AEM用於將代碼部署到as a Cloud Service的持續整合和交AEM付框架
* 使用內容傳輸工具使您快速
* 描述您必須使用的代碼重構工具，以便將代碼現代化以實現AEMas a Cloud Service

## 使用 Cloud Manager {#using-cloud-manager}

在開始之前，您必須熟悉雲管理器，因為它是將代碼部署到AEMas a Cloud Service的唯一機制。

Cloud Manager 可讓組織在雲端中自行管理 AEM。其內容包含持續整合與持續傳送 (CI/CD) 架構，可讓 IT 團隊與實作合作夥伴加快提供自訂或更新的傳送速度，而不會影響效能或安全性。

您可以通過咨詢以下資源來熟悉使用雲管理器：

* [加入 Experience Manager as a Cloud Service](/help/onboarding/home.md)，了解有關加入 Experience Manager as a Cloud Service 的自助資源。

* [整合 Git 與 Adobe Cloud Manager](/help/implementing/cloud-manager/managing-code/integrating-with-git.md)，了解如何使用 Single Git 存放庫來部署程式碼。

* [Adobe Experience as a Cloud Service 設定](/help/security/ims-support.md#aem-configuration)，了解如何「在 Admin Console 中管理產品與使用者存取」。

## 使用Adobe提供的工具使您的內容和代碼雲就緒 {#use-tools-to-make-code-and-content-cloud-ready}

您向Cloud Service過渡的確切步驟取決於您購買的系統和遵循的軟體開發生命週期做法。

下圖顯示了該階段涉及的主要步驟，這些步驟涉及轉換代碼和內容以用於AEMas a Cloud Service:

![影像](/help/journey-migration/assets/exec-image1.png)

我們將開始在以下章節中詳細介紹您需要使用的工具，以實現此目標。

## 內容移轉 {#content-migration}

要將內容從當前實AEM例遷移到Cloud Service實例，可以使用Adobe的內容傳輸工具。

使用此工具，即可指定想從您的 AEM 例項轉移至雲端服務例項的內容。

內容遷移是一個多步過程，需要不同團隊之間進行規劃、跟蹤和協作。

有關該工具的工作原理以及我們建議您使用它的完整詳細資訊，請參閱 [內容傳輸工具文檔](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md)。

## 程式碼重構 {#code-refactor}

### 設定用於開發 {#set-up-for-development}

現在是時候開始重構與Cloud Services相容的現有功能了。

為此，您需要查看詳細說明啟動重構代碼所需的基本工具的文檔：


* 在規劃期間，最好列出必須重新考慮的區域，以便與AEMas a Cloud Service相容。 您可以查看 [發展指南](/help/implementing/developing/introduction/development-guidelines.md) 的子菜單。
* 瞭解如何 [管理配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/configurations.html?lang=en#what-is-a-configuration) 在AEMas a Cloud Service。
* 瞭解如何通過下載 [AEMas a Cloud ServiceSDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en)
* 最後，熟悉 [AEMas a Cloud ServiceJAVA API](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html)。

此外，您還可以：

* 觀看此視頻以瞭解如何在本地安裝Dispatcher SDK:

   >[!VIDEO](https://video.tv.adobe.com/v/30601)

* 觀看此視頻以瞭解如何配置Dispatcher SDK:

   >[!VIDEO](https://video.tv.adobe.com/v/30602)

### 心態的轉變 {#a-change-in-mindset}

在as a Cloud Service中開發和運AEM行代碼需要改變思維。 請注意，程式碼必須具復原性，特別是因為例項可能隨時停止。您必須了解，在雲端服務中執行程式碼時，一律會在叢集中執行。這表示執行中的例項永遠多於一個。

Maven項目需要某些AEM更改才能與雲相容。 AEMas a Cloud Service要求 *內容* 和 *代碼* 到不同的包中AEM:

* `/apps` 和 `/libs` 被視為不可變AEM的區域，因為它們在啟AEM動後無法更改（即在運行時）。 這包括建立、更新或刪除操作。 在運行時更改不可變區域的任何嘗試都將失敗。

* 儲存庫中的其他所有內容(例如， `/content` 。 `/conf` 。 `/var` 。 `/home` 。 `/etc` 。 `/oak:index` 。 `/system` 。 `/tmp`)是所有可變區域，這意味著可以在運行時更改這些區域。

通過咨詢 [推薦的包結構](/help/implementing/developing/introduction/aem-project-content-package-structure.md#recommended-package-structure) 文檔。


### 雲遷移工具 {#cloud-migration-tools}

Adobe提供了多種工具來幫助加速某些代碼重構任務。 瞭解這些工具及其解決的問題將減少遷移的複雜性和時間。

* [資產工作流遷移](/help/journey-migration/moving-to-aem-assets/asset-workflow-migration-tool.md)，用於自動遷移資產處理工作流的工具
* [調度器轉換器](/help/journey-migration/refactoring-tools/dispatcher-transformation-utility-tools.md)，將現有Dispatcher配置轉換為可供as a Cloud Service使用的格AEM式的工具。
* [儲存庫現代化器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/moving/refactoring-tools/repo-modernizer.html?lang=en)，一個將多模AEM式項目作為輸入並轉換為as a Cloud Service項AEM目的工具
* [索引轉換器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/moving/refactoring-tools/index-converter.html?lang=en)，將索引轉換為與AEMas a Cloud Service
* [現代化工具](/help/journey-migration/refactoring-tools/aem-modernization-tools.md)，一套實用程式，可用於將舊功能AEM轉換為現代和支援的AEMas a Cloud Service功能。

一旦您設定了本地開發環境，請咨詢AEMas a Cloud ServiceSDK [文檔](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)。

### 計畫代碼凍結 {#schedule-a-code-freeze}

要在您的活動代碼開發上管理您的持續代碼開發AEM，並將代碼重構任務作為過渡過程的一部分，我們建議您安排一個代碼凍結期，直到您完成對Maven項目的重組以與as a Cloud Service兼AEM容。

項目重組完成後，可以基於此新結構恢復新代碼開發。 這可減少代碼部署和測試期間Cloud Manager管道故障。

>[!NOTE]
>「內容傳輸」和「代碼重構」任務不必按順序完成。 這些任務可以各自獨立完成。不過，您需要正確的專案結構，以確保內容能在雲端服務環境中成功轉譯。

## 程式碼部署和測試的最佳作法 {#best-practices}

Cloud Manager管道支援針對階段環境運行的test的執行。

請遵循以下文檔中有關代碼質量測試的最佳做法：

* [代碼質量測試](/help/implementing/cloud-manager/code-quality-testing.md)，一個描述編寫test指令碼的過程並說明至少50%建議覆蓋範圍的概念的文檔。
* [瞭解自定義代碼質量規則](/help/implementing/cloud-manager/custom-code-quality-rules.md) 它旨在描述由Cloud Manager根據工程部門的最佳實踐建立的自定義代碼質量規AEM則。

## 準備投入使用 {#preparing-for-go-live}

為遷移準備源系統涉及系統級和管AEM理員級任務。 您可以通過檢查 [修訂](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html) 和 [資料儲存垃圾收集](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/data-store-garbage-collection.html) 任務狀態。 如果您運行的AEM是6.3版（因為內容傳輸工具從6.3版開始相容），建議執行離線壓縮，然後執行資料儲存垃圾收集。

[資料一致性檢查](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/consistency-check.html) 建議跨所有版AEM本進行遷移，以確保內容儲存庫處於啟動遷移活動的良好狀態。

安裝和配置需要系統管理員級別訪問權限 [AZCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md)

還建議您查看任何未使用的資產、頁AEM面、項目、用戶和組，以節省遷移時間。 查看 [內容儲存庫運行狀況](#repository-health) 的子菜單。

### 內容儲存庫運行狀況 {#repository-health}

訪問 [生產克隆](#proof-of-migration) 已建立，以檢查儲存庫的運行狀況。 如上節所述，目標是在開始遷移之前清理並壓縮源上的儲存庫。 此步驟可能會節省大量時間，否則，在遷移開始後，將花費大量時間進行故障排除。

| 措施項 | 關鍵要點 |
|---------|----------|
| 用戶、組和權限 | 您需要瞭解用戶數量、組數量和成員資格的複雜性。 在遷移前查找清除源中任何未使用的用戶和組的機會。 |
| 未完成資產處理 | 嘗試在開始遷移之前完成源系統中資產的處理，以避免as a Cloud Service遷移後AEM的潛在問題。 |
| 內容運行狀況 | 建議在開始遷移之前查詢錯誤內容並將其清除。 例如，查找沒有原始格式副本或在工作流處理中停滯的資產或頁面。 另請參閱 [資產運行狀況](#asset-health)。 |

## 收集資料 {#gathering-data}

>[!NOTE]
> 的 [內容遷移策略和時間表](#content-strategy-and-timeline) 部分進一步詳細說明如何推斷收集的資料並建立遷移計畫。

收集資料可以幫助您規劃遷移活動和相關任務。 提取和攝取時間特別有用，因為資料點可以與遷移集的特定大小相關聯。 因此，可以推斷這些資料點，以便制定計畫：

* 所用時間總額 [提取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md)
* 所用時間總額 [攝食](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)
* 補充所用的總時間 [提取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)
* 補充所用的總時間 [攝食](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process)

另一個重要的資料點是完成 [用戶映射](/help/journey-migration/content-transfer-tool/user-mapping-tool/overview-user-mapping-tool.md)，如果這與內容遷移相結合。 您可以考慮此資料點，以便進行更為現實的估計，因為它將添加到整個提取時間線中，並且可能不需要在頂部操作期間運行它。

這些資料點也可幫助您 [建立KPI](/help/journey-migration/readiness.md#establish-kpis) 和其他遷移相關任務。

### 遷移計畫 {#migration-plan}

根據您收集的資料點（請參閱上面），您可以建立可整合到宏項目計畫中的遷移計畫。 此步驟將使所有關鍵利益相關方能夠直觀顯示和規劃遷移活動。

下表說明了典型的遷移計畫：

| 遷移迭代 | 開始日期 | 估計結束日期 | 相依關係 | 估計持續時間（天） | 附加詳細資訊/措施項 |
|---|---|---|---|---|---|
| PRDCLONE-AUTHOR-INITIAL-USRMAP-CSSTAGE-AUTHOR |  |  |  |  |  |
| PRDCLONE-PUBLISH-TOPUP-CSSTAGE-AUTHOR |  |  |  |  |  |

如上表所示，遵循特定命名格式來標識遷移小版本非常有幫助，例如： **PRDCLONE** 對於源環AEM境， **作者/發佈** 為了AEMas a Cloud Service, **CSSTAGE作者** 例AEM如as a Cloud Service。

影響遷移計畫的一些重要詳細資訊：

**所需提取的總數**

* 在特定環境中，作者提取和發佈提取被視為兩個並行提取，因為它們彼此獨立。
* 根據特定時間段中的儲存庫增長進行的Top Up提取數。

**所需接收總數**

* 將此項目捕獲到計畫中非常重要，因為提取的集可以被捕獲到多個Cloud Service環境中。
* 追加接收數。
* 將內容從源作者遷移到雲服務作者實例以及從源發佈遷移到Cloud Service發佈是避免將所有作者內容插入Cloud Service發佈的最佳做法。

### 遷移跟蹤器 {#migration-tracker}

您可以使用遷移跟蹤器記下初始運行和上行運行的時間。 這些資料點將幫助您在最終的備份之前制定真實的內容凍結要求。

該跟蹤器還將幫助您：

* 確定需要在計畫或即時時間表中進行調整的與計畫員的任何偏差
* 提供可用於所有必要通信的真實狀態
* 規劃初始或將來的補充遷移

下表說明了功能性遷移跟蹤器：

| 源（環境/實例/URL） | 目標（環境/實例/URL） | 遷移集名稱、類型（初始或自上而下） | 遷移集大小(MB) | 用戶映射（是/否） | 提取持續時間（開始、結束、所用時間） | 攝取持續時間（開始、結束、所用時間） | 問題/解決方案/詳細資訊 |
|---|---|---|---|---|---|---|---|
|  |  |  |  |  |  |  |  |

## 內容遷移策略和時間表 {#content-strategyand-timeline}

以下部分顯示了可用於制定內容遷移策略和時間表的重要步驟和相關任務。

![影像](/help/journey-migration/assets/content-migration2.png)

### 裝修 {#fitment}

* 執行修訂版清理、資料儲存垃圾收集和資料一致性檢查。 另請參閱 [準備投入使用](#preparing-for-go-live)
* [收集統計資訊](#gathering-data) 關於源AEM儲存庫：
   * 段儲存大小
   * 索引儲存大小
   * 頁數
   * 資產數
   * 用戶和組數
* 瞭解是否在源上啟AEM用了以下功AEM能：
   * 智慧標籤
   * 相似性搜索
   * 搜索包含Word和PDF文檔中的文本
* 收集最佳實踐分析器 [報告](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md)
* 導入到 [雲加速管理器](/help/journey-migration/cloud-acceleration-manager/introduction/overview-cam.md)
   * 查看自我分析建議，確保AEMas a Cloud Service能夠處理儲存需求。
* 在繼續遷移計畫之前，請建立Adobe支援票證以便進行任何澄清。

### 遷移證明 {#proof-of-migration}

* 請求生產克隆：
   * 位於同一網路區域
   * 將提供生產內容，如用戶和組
   * 克隆作者和發佈 — 在群集或發佈場中，每個節點一個
* 選擇要遷移的內容的子集，以便：
   * 它是所有可用內容類型的混合
   * 包含所有用戶和組（以防萬一） [用戶映射](/help/journey-migration/content-transfer-tool/user-mapping-tool/overview-user-mapping-tool.md) 必填
* 包括25%的內容或最多1 TB的內容（以較小者為準）。
* 至少執行一個完整和 [上](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) 遷移，從生產克隆到AEMas a Cloud Service非生產環境
* 解決任何潛在問題，例如：
   * 源上的磁碟空AEM間
   * 源與AEMas a Cloud Service之間的連AEM接
   * 任意 [與攝取相關的限制](go-live.md#known-limitations)。
* 記錄所花費的時間 [提取與攝食](#gathering-data):
   * 瞭解每週添加的內容數
   * 根據遷移證明推斷所測量的時間以建立 [遷移計畫](#migration-plan)。

## 下一步是什麼 {#what-is-next}

一旦您完全瞭解了如何評估AEM您的安裝是否已準備好移至雲，我們將學習如何使用使安裝準備就緒所需的工具，現在就是時候繼續 [上線階段](/help/journey-migration/go-live.md)。
