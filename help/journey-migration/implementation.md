---
title: 實作階段
description: 確定您的程式碼和內容已準備好移轉至雲端
exl-id: d124f9a5-a754-4ed0-a839-f2968c7c8faa
source-git-commit: 13cb8ae059f0a77e517d2e64eae96a08f88ac075
workflow-type: tm+mt
source-wordcount: '2416'
ht-degree: 8%

---

# 實作階段 {#implementation-phase}

在歷程的實作階段中，您將探索各種工具，讓您的程式碼和內容可隨時移至AEMas a Cloud Service。

## 迄今為止的故事 {#story-so-far}

在歷程的前幾個階段，你 [熟悉AEM as a Cloud Service中的變更](/help/journey-migration/getting-started.md)，以及判斷您的部署是否已準備好透過移至雲端 [準備階段](/help/journey-migration/readiness.md).

本文繼續說明如何使用Adobe提供的工具，確保您的程式碼和內容已準備好移至雲端，以利使用。

## 目標 {#objective}

本檔案旨在：

* 向您介紹AEM、Cloud Manager、用於部署程式碼至AEMas a Cloud Service的持續整合和傳送架構
* 使用內容轉移工具讓您快速上手
* 說明您必須使用的程式碼重構工具，以導入最新的AEMas a Cloud Service程式碼

## 使用 Cloud Manager {#using-cloud-manager}

開始之前，您必須熟悉Cloud Manager，因為這是將程式碼部署至AEM as a Cloud Service的唯一方法。

Cloud Manager 可讓組織在雲端中自行管理 AEM。其內容包含持續整合與持續傳送 (CI/CD) 架構，可讓 IT 團隊與實作合作夥伴加快提供自訂或更新的傳送速度，而不會影響效能或安全性。

您可以諮詢下列資源，以熟悉如何使用Cloud Manager:

* [入門歷程](/help/journey-onboarding/overview.md) 了解有關上線的自助資源，以利Experience Manageras a Cloud Service。

* [整合 Git 與 Adobe Cloud Manager](/help/implementing/cloud-manager/managing-code/integrating-with-git.md)，了解如何使用 Single Git 存放庫來部署程式碼。

* [Adobe Experience as a Cloud Service 設定](/help/security/ims-support.md#aem-configuration)，了解如何「在 Admin Console 中管理產品與使用者存取」。

## 使用Adobe提供的工具，讓您的內容和程式碼雲端準備就緒 {#use-tools-to-make-code-and-content-cloud-ready}

轉換為Cloud Service的確切步驟取決於您購買的系統，以及您遵循的軟體開發生命週期實務。

下圖顯示階段中涉及的主要步驟，包括轉換程式碼和內容以搭配AEMas a Cloud Service使用：

![影像](/help/journey-migration/assets/exec-image1.png)

我們將在以下各章中開始詳細說明您需要使用哪些工具來實現此目標。

## 內容移轉 {#content-migration}

若要將內容從您目前的AEM例項移轉至您的Cloud Service例項，您可以使用Adobe的「內容轉移工具」。

使用此工具，即可指定想從您的 AEM 例項轉移至雲端服務例項的內容。

內容移轉是多步驟程式，需要不同團隊之間進行規劃、追蹤及協作。

如需工具運作方式及建議您使用方式的完整詳細資訊，請參閱 [內容轉移工具檔案](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md).

## 程式碼重構 {#code-refactor}

### 設定以供開發 {#set-up-for-development}

現在可以開始重構與Cloud Services相容的現有功能了。

若要這麼做，您需要檢視檔案，其中詳細說明開始重構程式碼所需的基本工具：


* 在規劃期間，最好列出必須重構以便與AEMas a Cloud Service相容的區域。 您可以檢閱 [開發准則](/help/implementing/developing/introduction/development-guidelines.md) 如需如何重構和最佳化程式碼以供Cloud Service的詳細資訊。
* 詳閱 [管理配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/configurations.html?lang=en#what-is-a-configuration) 在AEMas a Cloud Service。
* 了解如何透過下載 [AEMas a Cloud ServiceSDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en)
* 最後，請熟悉 [AEMas a Cloud ServiceJAVA API](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html).

此外，您也可以：

* 請觀看此影片，了解如何在本機安裝Dispatcher SDK:

   >[!VIDEO](https://video.tv.adobe.com/v/30601)

* 請觀看此影片，了解如何設定Dispatcher SDK:

   >[!VIDEO](https://video.tv.adobe.com/v/30602)

### 心態的改變 {#a-change-in-mindset}

在AEM as a Cloud Service中開發及執行程式碼時，需要改變心態。 請注意，程式碼必須具復原性，特別是因為例項可能隨時停止。您必須了解，在雲端服務中執行程式碼時，一律會在叢集中執行。這表示執行中的例項永遠多於一個。

AEM Maven專案必須進行某些變更，才能與雲端相容。 AEMas a Cloud Service需要分離 *內容* 和 *代碼* 部署至AEM的不同套件中：

* `/apps` 和 `/libs` 在AEM中，會視為不可變的區域，因為這些區域在AEM啟動後無法變更（即在執行階段中）。 這包括建立、更新或刪除操作。 在運行時更改不可變區域的任何嘗試都將失敗。

* 存放庫中的其他所有項目(例如 `/content` , `/conf` , `/var` , `/home` , `/etc` , `/oak:index` , `/system` , `/tmp`)都是可變區域，這表示在執行階段可以變更它們。

您可以諮詢 [建議的封裝結構](/help/implementing/developing/introduction/aem-project-content-package-structure.md#recommended-package-structure) 檔案。


### 雲端移轉工具 {#cloud-migration-tools}

Adobe提供數種工具，可協助您加速某些程式碼重構工作。 了解這些工具及其解決的問題將降低遷移複雜性和時間。

* [資產工作流程移轉](/help/journey-migration/moving-to-aem-assets/asset-workflow-migration-tool.md)，此工具可用來自動移轉資產處理工作流程
* [Dispatcher轉換工具](/help/journey-migration/refactoring-tools/dispatcher-transformation-utility-tools.md)，此工具會將您現有的Dispatcher設定轉換為可供AEMas a Cloud Service使用的格式。
* [Repository Modernizer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/moving/refactoring-tools/repo-modernizer.html?lang=en)，此工具會將AEM多模專案作為輸入，並轉換為AEMas a Cloud Service專案
* [索引轉換器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/moving/refactoring-tools/index-converter.html?lang=en)，此工具可將索引轉換為與AEMas a Cloud Service相容的表單
* [現代化工具](/help/journey-migration/refactoring-tools/aem-modernization-tools.md)，此公用程式套裝可用來將舊版AEM功能轉換為AEM as a Cloud Service的現代化及支援功能。

設定本機開發環境後，請參閱以下內容以熟悉AEMas a Cloud ServiceSDK: [檔案](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md).

### 排程程式碼凍結 {#schedule-a-code-freeze}

若要管理您在作用中AEM上持續進行的程式碼開發，以及轉換歷程中的程式碼重構任務，建議您排程程式碼凍結期間，直到您完成重組Maven專案以與AEMas a Cloud Service相容為止。

專案重組完成後，您就可以根據這個新結構繼續開發新的程式碼。 這可減少程式碼部署和測試期間的Cloud Manager管道故障。

>[!NOTE]
>「內容轉移」和「程式碼重構」工作不必依序執行。 這些任務可以各自獨立完成。不過，您需要正確的專案結構，以確保內容能在雲端服務環境中成功轉譯。

## 程式碼部署和測試的最佳作法 {#best-practices}

Cloud Manager管道支援針對預備環境執行的測試。

請依照下列檔案中有關程式碼品質測試的最佳實務：

* [程式碼品質測試](/help/implementing/cloud-manager/code-quality-testing.md)，此檔案說明編寫測試指令碼的程式，並說明建議涵蓋範圍至少50%的概念。
* [了解自訂程式碼品質規則](/help/implementing/cloud-manager/custom-code-quality-rules.md) 此功能旨在說明由Cloud Manager根據AEM Engineering最佳實務建立而執行的自訂程式碼品質規則。

## 準備上線 {#preparing-for-go-live}

為遷移準備源系統涉及系統和AEM管理員級任務。 首先，您可以檢查 [修訂清除](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html) 和 [資料儲存垃圾收集](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/data-store-garbage-collection.html) 任務狀態。 如果您執行的是AEM 6.3版（因為「內容轉移工具」自6.3版起相容），建議您執行離線壓縮，之後是「資料存放區垃圾收集」。

[資料一致性檢查](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/consistency-check.html) 建議所有AEM版本使用，以確保內容存放庫處於良好狀態，以啟動移轉活動。

安裝和配置需要系統管理員級別訪問 [AZCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md)

建議您檢閱任何未使用的資產、頁面、AEM專案、使用者和群組，以節省移轉時間。 請參閱 [內容存放庫健全狀態](#repository-health) 區段。

### 內容存放庫健全狀態 {#repository-health}

存取 [生產原制](#proof-of-migration) 已建立，請繼續檢查存放庫的健全狀態。 如前一節所述，目標是在開始移轉前，先清理並壓縮來源上的存放庫。 此步驟可能會在移轉開始後，節省大量疑難排解問題的時間。

| 動作項目 | 主要優點 |
|---------|----------|
| 使用者、群組和權限 | 您需要了解成員身份的使用者數量、群組和複雜性。 尋找在遷移前清除源中任何未使用的用戶和組的機會。 |
| 未完成資產處理 | 開始移轉前，請嘗試先完成來源系統中資產的處理作業，以避免AEMas a Cloud Service移轉後的潛在疑慮。 |
| 內容健康狀況 | 建議您在開始移轉前，先查詢並清除不良內容。 例如，尋找沒有原始轉譯或停滯於工作流程處理的資產或頁面。 另請參閱 [資產運作狀況](#asset-health). |

## 收集資料 {#gathering-data}

>[!NOTE]
> 此 [內容遷移策略和時間表](#content-strategy-and-timeline) 一節進一步詳細說明如何推斷收集的資料並建立遷移計畫。

收集資料可協助您規劃移轉活動和相關任務。 提取和擷取時間特別有用，因為資料點可以與移轉集的特定大小相關聯。 因此，可以推斷這些資料點以得出一個計畫：

* 所花費的總時間 [摘取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md)
* 所花費的總時間 [擷取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)
* 追加所花費的總時間 [摘取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)
* 追加所花費的總時間 [擷取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process)

更重要的資料點是完成 [使用者對應](/help/journey-migration/content-transfer-tool/user-mapping-tool/overview-user-mapping-tool.md)，如果這與內容移轉結合。 您可以將此資料點納入考量，以獲得更切合實際的估計，因為它將新增至整體提取時間軸，且在追加期間可能不需要執行它。

這些資料點也可協助您 [建立KPI](/help/journey-migration/readiness.md#establish-kpis) 以及其他與移轉相關的任務。

### 遷移計畫 {#migration-plan}

您可以根據收集的資料點（請參閱上文），建立可整合至巨集專案計畫的移轉計畫。 此步驟可讓所有主要利害關係人以視覺化方式，針對移轉活動進行規劃。

下表說明了典型的遷移計畫：

| 遷移迭代 | 開始日期 | 預計結束日期 | 相依性 | 估計持續時間（以天為單位） | 其他詳細資訊/動作項目 |
|---|---|---|---|---|---|
| PRDCLONE-AUTHOR-INITIAL-USRMAP-CSSTAGE-AUTHOR |  |  |  |  |  |
| PRDCLONE-PUBLISH-TOPUP-CSSTAGE-AUTHOR |  |  |  |  |  |

如上表所示，遵循特定的命名格式來識別移轉迭代會很有幫助，例如： **PRDCLONE** 對於來源AEM環境， **作者/發佈** 針對AEMas a Cloud Service環境， **CSSTAGE-AUTHOR** AEMas a Cloud Service例項等。

影響遷移計畫的一些重要詳細資訊：

**需要提取的總數**

* 特定環境中的「製作」和「發佈」擷取會視為兩個平行擷取，因為它們彼此獨立。
* 根據特定時段的儲存庫增長而追加提取的數量。

**需要的擷取總數**

* 請務必將此項目擷取到計畫中，因為擷取的集可擷取到多個Cloud Service環境中。
* 追加擷取次數。
* 將內容從「來源作者」例項移轉至「雲端服務作者」例項，以及從「來源發佈」移轉至「Cloud Service發佈」，是避免將所有「作者」內容擷取至「Cloud Service發佈」的最佳作法。

### 移轉追蹤器 {#migration-tracker}

您可以使用移轉追蹤器記下初始和追加執行的時間。 這些資料點可協助您在最終追加之前制定真實的內容凍結要求。

追蹤器也可協助您：

* 標識需要調整計畫或上線時間表的與計畫員的任何偏差
* 提供可用於所有必要通訊的實際狀態
* 規劃初始或未來的追加遷移

下表說明功能移轉追蹤器：

| 來源（環境/執行個體/ URL） | 目的地（環境/執行個體/ URL） | 移轉集名稱、類型（初始或追加） | 遷移集大小(MB) | 用戶映射（是/否） | 提取期間（開始、結束、所用時間） | 擷取持續時間（開始、結束、所用時間） | 問題/解決方案/詳細資訊 |
|---|---|---|---|---|---|---|---|
|  |  |  |  |  |  |  |  |

## 內容遷移策略和時間表 {#content-strategyand-timeline}

以下章節顯示可用於制定內容遷移策略和時間表的重要步驟和相關任務。

![影像](/help/journey-migration/assets/content-migration2.png)

### Fitment {#fitment}

* 執行修訂清除、資料儲存垃圾收集和資料一致性檢查。 另請參閱 [準備上線](#preparing-for-go-live)
* [收集統計資料](#gathering-data) 關於AEM來源存放庫：
   * 區段存放區大小
   * 索引儲存大小
   * 頁數
   * 資產數量
   * 使用者和群組數
* 了解是否已在AEM來源上啟用下列功能(AEMas a Cloud Service中也需要):
   * 智慧標籤
   * 相似性搜尋
   * 搜索包含Word和PDF文檔中的文本
* 收集Best Practice Analyzer [報告](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md)
* 匯入至 [Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/introduction/overview-cam.md)
   * 查看自我分析建議，以確保AEMas a Cloud Service可以處理儲存需求。
* 繼續執行移轉計畫前，請建立Adobe支援票證以取得任何說明。

### 移轉證明 {#proof-of-migration}

* 請求生產克隆：
   * 位於同一網路區域
   * 將提供生產內容，例如使用者和群組
   * 克隆製作和發佈 — 群集或發佈場中每個節點
* 選擇要移轉的內容子集，以便：
   * 它是所有可用內容類型的組合
   * 包含所有使用者和群組，以防萬一 [使用者對應](/help/journey-migration/content-transfer-tool/user-mapping-tool/overview-user-mapping-tool.md) 必填
* 包括25%的內容或最多1 TB的內容（以較少者為準）。
* 至少執行一個完整和 [追加](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) 移轉，從生產原地複製到AEMas a Cloud Service非生產環境
* 解決任何潛在問題，例如：
   * AEM源上的磁碟空間
   * AEM來源和AEM之間的連線as a Cloud Service
   * 任何 [擷取相關限制](go-live.md#known-limitations).
* 記錄 [擷取和擷取](#gathering-data):
   * 了解每週新增多少內容
   * 從移轉證明推斷測量的時間，以建立 [遷移計畫](#migration-plan).

## 下一步 {#what-is-next}

一旦您完全了解如何評估您的AEM安裝是否已準備好移至雲端，而我們正在學習如何使用所需工具來做好準備，您就可以繼續使用 [上線階段](/help/journey-migration/go-live.md).
