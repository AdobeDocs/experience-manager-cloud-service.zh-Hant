---
title: 上線
description: 瞭解如何在代碼和內容準備好雲後執行遷移
exl-id: 10ec0b04-6836-4e26-9d4c-306cf743224e
source-git-commit: 9a10348251fe7559ae5d3c4a203109f1f6623bce
workflow-type: tm+mt
source-wordcount: '1644'
ht-degree: 0%

---

# 上線 {#go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_prep"
>title="即時準備"
>abstract="為確保在as a Cloud Service上順利成功上線AEM，您應計畫代碼和內容凍結期、測試迭代、內容補充、效能test、安全test等。"

在此過程中，您將學習如何規劃和執行遷移，一旦代碼和內容都準備好移至AEMas a Cloud Service。 此外，您還將瞭解執行遷移時有哪些最佳做法和已知限制。

## 到目前為止的故事 {#story-so-far}

在旅程的前幾個階段：

* 您學會了如何開始移動AEM到as a Cloud Service [入門](/help/journey-migration/getting-started.md) 的子菜單。
* 已通過讀取 [準備階段](/help/journey-migration/readiness.md)
* 熟悉使代碼和內容雲隨時可用的工具和流程 [實施階段](/help/journey-migration/implementation.md)。

## 目標 {#objective}

本文檔將幫助您瞭解如何AEM在您熟悉前面的步驟後，執行到as a Cloud Service的遷移。 您將學習如何執行初始生產遷移，以及遷移到AEMas a Cloud Service時要遵循的最佳做法。

## 初始生產遷移 {#initial-migration}

在執行生產遷移之前，請遵循中概述的配置和遷移證明步驟 [內容遷移策略和時間表](/help/journey-migration/implementation.md##strategy-timeline) 的下界 [實施階段](/help/journey-migration/implementation.md)。

* 根據您在克隆上執行的as a Cloud Service遷移階段所獲AEM的經驗，從生產環境開始遷移：
   * 作者 — 作者
   * 發佈 — 發佈

* 驗證所接收到的內容AEM是否同時存入as a Cloud Service作者和發佈層。
* 指示內容創作團隊避免在源和目標上移動內容，直到接收完成
* 可以添加、編輯或刪除新內容，但避免移動它。 這同時適用於源和目標。
* 錄制 [時間](/help/journey-migration/implementation.md#gathering-data) 用於完全提取和攝取，以便對未來追加遷移時間表進行估計。
* 建立 [遷移規劃器](/help/journey-migration/implementation.md#migration-plan) 和出版。

## 增量頂部 {#top-up}

在從生產環境進行初始遷移後，您必須執行增量頂置，以確保您的內容在雲實例上是最新的。 因此，建議您遵循以下最佳做法：

* 收集有關內容量的資料。 例如：每週，兩週或一個月。
* 確保以這樣的方式規劃追加內容，以避免超過48小時的內容提取和攝取。 建議這樣做，以便內容頂部內容將適合週末時間範圍。
* 計畫所需的頂層數量，並使用這些估計值在「投入使用」日期前後進行計畫。

## 確定遷移的代碼和內容凍結時間表 {#code-content-freeze}

如前所述，您必須安排代碼和內容凍結期。 使用以下問題幫助您計畫凍結期：

* 我必須凍結內容創作活動多久？
* 在多長時間內，我應要求我的交付團隊停止添加新功能？

要回答第一個問題，您應考慮在非生產環境中執行試運行所花費的時間。 要回答第二個問題，您需要添加新功能的團隊和重構代碼的團隊之間進行密切協作。 目標應是確保添加到現有部署的所有代碼也添加、測試和部署到雲服務分支。 一般來說，這意味著代碼凍結量會更低。

此外，您需要在計畫最終內容補充時計畫內容凍結。

## 最佳作法 {#best-practices}

在規劃或執行遷移時，應考慮以下准則：

* 從作者遷移到作者並發佈到發佈
* 請求可用於以下目的的生產克隆：
   * 捕獲儲存庫統計資訊
   * 遷移活動的證明
   * 準備遷移計畫
   * 確定內容凍結要求
   * 在從生產環境遷移時確定生產環境中的任何升級需求

**內容傳輸工具最佳做法**

確保在投入使用時，在生產環境中運行內容遷移，而不是克隆。 一個好方法是 [AZCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) 執行初始遷移，然後頻繁（甚至每天）運行頂級提取以提取較小的塊，並避免源上的任何長期負AEM載。

執行生產遷移時，應避免從克隆運行內容傳輸工具，因為：

* 如果客戶要求在自上而下的遷移期間遷移內容版本，則從克隆執行內容傳輸工具不會遷移這些版本。 即使克隆是從即時作者頻繁重新建立的，每次建立克隆時，內容傳輸工具將使用的檢查點將被重置以計算增量。
* 由於無法將克隆作為一個整體進行刷新，因此必須使用ACL查詢包來打包和安裝從生產到克隆添加或編輯的內容。 此方法的問題在於源實例上任何已刪除的內容將永遠無法訪問克隆，除非從源實例和克隆中手動刪除它。 這會導致在克隆和AEMas a Cloud Service上刪除生產上刪除的內容。

**在執行內容遷移AEM時優化源上的負載**

請記住，在提取AEM階段，源上的負載會更大。 您應該知道：

* 內容傳輸工具是使用JVM堆4 GB的外部Java進程
* 非AzCopy版本下載二進位檔案，將它們儲存在源作者的臨時空間AEM上，佔用磁碟I/O，然後上載到消耗網路頻寬的Azure容器
* [可用區複製](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) 將blob直接從blob儲存區傳輸到Azure容器，該容器可節省磁碟I/O和網路頻寬。 AzCopy版本仍然使用磁碟和網路頻寬從段儲存中提取資料並將其上載到Azure容器
* 在接收階段，內容傳輸工具流程在系統資源上較輕，因為它只流入接收日誌，而且從磁碟I/O或網路頻寬角度看，源實例上的負載不大。

## 已知限制 {#known-limitations}

如果在提取的遷移集中發現以下任何限制，請考慮整個攝取失敗：

* 名稱超過150個字元的JCR節點
* 大於16 MB的JCR節點
* 任何用戶/組 `rep:AuthorizableID` 被攝入as a Cloud Service上已經AEM有
* 如果提取和攝取的任何資產在遷移的下一迭代之前，在源或目標上移動到其他路徑。

## 資產運行狀況 {#asset-health}

與食物攝入量上面的部分 **不** 因以下資產問題而失敗。 但是，強烈建議您在以下情形中採取適當步驟：

* 缺少原始格式副本的任何資產
* 缺少的任何資料夾 `jcr:content` 節點

上述兩個項目均將在 [最佳做法分析器](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) 報告。

## 上線核對表 {#Go-Live-Checklist}

請查看此活動清單，以確保順利成功執行遷移。

* 運行具有功能和UI測試的端到端生產管線，以確保 **始終為當前** 產品AEM體驗。 請參閱以下資源。
   * [版AEM本更新](/help/implementing/deploying/aem-version-updates.md)
   * [自定義功能測試](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)
   * [UI測試](/help/implementing/cloud-manager/ui-testing.md)
* 將內容遷移到生產環境，並確保在準備測試時提供相關子集。
   * 請注意，DevOps的最AEM佳實踐意味著代碼從開發向生產環境移動， [內容從生產環境中移下。](/help/overview/enterprise-devops.md#code-movement)
* 計畫代碼和內容凍結期。
   * 另請參見一節 [遷移的代碼和內容凍結時間表](#code-content-freeze)
* 執行最後內容的上行操作。
* 驗證調度程式配置。
   * 使用本地調度程式驗證程式，該程式便於在本地配置、驗證和模擬調度程式
      * [設定本地調度程式工具。](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=en#prerequisites)
   * 仔細檢查虛擬主機配置。
      * 最簡單（和預設）的解決方案是 `ServerAlias *` 在虛擬主機檔案中 `/dispatcher/src/conf.d/available_vhostsfolder`。
         * 這將允許產品功能test、調度程式快取無效和克隆使用的主機別名發揮作用。
      * 但是，如果 `ServerAlias *` 不可接受，至少以下 `ServerAlias` 除了自定義域外，還必須允許輸入：
         * `localhost`
         * `*.local`
         * `publish*.adobeaemcloud.net`
         * `publish*.adobeaemcloud.com`
* 配置CDN、SSL和DNS。
   * 如果您正在使用自己的CDN，請輸入支援票證以配置適當的路由。
      * 請參閱一節 [客戶CDN指向托AEM管CDN](/help/implementing/dispatcher/cdn.md#point-to-point-cdn) 的子目錄。
      * 您需要根據CDN供應商的文檔配置SSL和DNS。
   * 如果您沒有使用其他CDN，請按照以下文檔管理SSL和DNS:
      * 管理SSL證書
         * [管理SSL證書簡介](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
         * [管理SSL證書](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
      * 管理自定義域名(DNS)
         * [自定義域名簡介](/help/implementing/cloud-manager/custom-domain-names/introduction.md)
         * [添加自定義域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)
         * [管理自定義域名](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)
   * 切記驗證DNS記錄的TTL集。
      * TTL是DNS記錄在請求伺服器更新之前在快取中停留的時間。
      * 如果TTL很高，則對DNS記錄的更新傳播需要更長的時間。
* 運行滿足您的業務需求和目標的效能和安全test。
* 切換，確保在不進行任何新部署或內容更新的情況下執行實際上線。

在執行遷移時需要重新校準任務時，您始終可以引用該清單。

## 下一步是什麼 {#what-is-next}

一旦您瞭解了如何執行遷移到AEMas a Cloud Service，可以檢查 [上線後](/help/journey-migration/post-go-live.md) 頁面以保持實例順利運行。
