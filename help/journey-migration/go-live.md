---
title: 入門
description: 瞭解在程式碼和內容準備就緒後，如何執行移轉
exl-id: 10ec0b04-6836-4e26-9d4c-306cf743224e
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1239'
ht-degree: 3%

---

# 入門 {#go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_prep"
>title="上線準備"
>abstract="為確保 AEM as a Cloud Service 順利而成功地上線，您應該規劃程式碼和內容凍結期、測試反覆項目、內容加值、效能測試、安全性測試等。"

在這段歷程中，您將瞭解在程式碼和內容準備好移至AEM as a Cloud Service後，如何規劃及執行移轉。 此外，您也會瞭解執行移轉時的最佳實務和已知限制。

## 目前進度 {#story-so-far}

在歷程的前幾個階段中：

* 您已在[快速入門](/help/journey-migration/getting-started.md)頁面中瞭解如何開始移至AEM as a Cloud Service。
* 已透過讀取[整備階段](/help/journey-migration/readiness.md)來判斷您的部署是否已準備好移至雲端
* 熟悉[實作階段](/help/journey-migration/implementation.md)的工具和程式，讓您的程式碼和內容雲端準備就緒。

## 目標 {#objective}

本檔案可協助您瞭解在熟悉歷程的先前步驟後，如何執行移轉至AEM as a Cloud Service。 您將瞭解如何執行初始生產移轉，以及移轉到AEM as a Cloud Service時要遵循的最佳實務。

## 初始生產移轉 {#initial-migration}

在您可以執行生產移轉之前，請遵循[實作階段](/help/journey-migration/implementation.md)的[內容移轉策略與時間表](/help/journey-migration/implementation.md##strategy-timeline)區段中概述的移轉步驟準備與證明。

* 根據您在翻制上執行AEM as a Cloud Service階段移轉期間獲得的體驗，從生產環境啟動移轉：
   * Author-Author
   * Publish-Publish

* 驗證內嵌至AEM as a Cloud Service作者和發佈層級的內容。
* 指示內容製作團隊在內嵌完成前，避免同時在來源和目的地移動內容
* 可以新增、編輯或刪除新內容，但請避免移動內容。 這同時適用於來源和目的地。
* 記錄完整擷取與擷取所花費的[時間](/help/journey-migration/implementation.md#gathering-data)，以估計未來的追加移轉時間表。
* 為作者與發佈同時建立[移轉規劃工具](/help/journey-migration/implementation.md#migration-plan)。

## 遞增增值 {#top-up}

從生產環境初始移轉後，您必須執行累加追加，以確保您在雲端例項上最新的內容。 因此，建議您遵循下列最佳實務：

* 收集有關內容量的資料。 例如：每一週、兩週或一個月。
* 請務必避免超過48小時的內容擷取和擷取工作，以計畫追加費用。 建議使用此功能，讓內容追加可符合週末的時間範圍。
* 規劃所需的追加數量，並使用這些估計在上線日期進行規劃。

## 識別移轉的程式碼和內容凍結時間表 {#code-content-freeze}

如前所述，您必須排程程式碼和內容凍結期間。 使用下列問題來協助您計畫凍結期間：

* 我需要多久才能凍結內容製作活動？
* 我該要求我的傳送團隊停止新增功能多久時間？

若要回答第一個問題，您應該考量在非生產環境中執行試用執行所花的時間。 若要回答第二個問題，您需要在新增功能的團隊和重構程式碼的團隊之間密切合作。 目標是要確保新增到現有部署的所有程式碼也會新增、測試和部署至雲端服務分支。 一般而言，這表示程式碼凍結的量會比較低。

此外，您還需要在排程最終追加內容時規劃內容凍結。

## 最佳做法 {#best-practices}

規劃或執行移轉時，您應考量下列准則：

* 從作者移轉至作者，以及從Publish移轉至Publish
* 請求可用於以下作業的生產複製：
   * 擷取儲存區域統計資料
   * 移轉活動證明
   * 準備移轉計畫
   * 識別內容凍結需求
   * 從生產環境執行移轉時，識別生產環境上的任何規模調整需求

**內容轉移工具最佳實務**

確定上線時，您會在生產環境中執行內容移轉，而非翻制。 一個好的方法是使用[AZCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md)進行初始移轉，然後頻繁執行追加擷取（甚至每天）以擷取較小的區塊，並避免來源AEM上的任何長期負載。

執行生產移轉時，您應該避免從翻制執行「內容轉移工具」，因為：

* 如果客戶在追加移轉期間需要移轉內容版本，則從複製執行內容轉移工具不會移轉版本。 即使經常從即時作者重新建立翻制，每次建立翻制時，「內容轉移工具」用來計算延長的查核點都會重設。
* 由於複製無法重新整理為整體，因此必須使用ACL查詢套件來封裝和安裝從生產環境新增或編輯到複製環境的內容。 此方法的問題在於，除非從來源和複製中手動刪除，否則來源執行個體上任何已刪除的內容永遠無法進入複製。 這會產生在生產環境中刪除的內容不會從原地複製和AEM as a Cloud Service上刪除的可能性。

**在執行內容移轉時最佳化AEM來源的負載**

請記住，在提取階段期間，AEM來源的負載會較大。 請注意下列事項：

* 內容轉移工具是外部Java程式，使用4 GB的JVM棧積
* 非AzCopy版本會下載二進位檔案，並將其儲存在來源AEM作者的暫存空間中，耗用磁碟I/O，然後上傳至Azure容器，耗用網路頻寬
* [AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md)會將blob直接從blob存放區傳輸到Azure容器，以儲存磁碟I/O和網路頻寬。 AzCopy版本仍會使用磁碟和網路頻寬，從區段存放區擷取資料並上傳到Azure容器
* 內容轉移工具程式在擷取階段期間對系統資源較輕，因為它只會串流擷取記錄，而且就磁碟I/O或網路頻寬而言，來源執行個體的負載並不大。

## 已知限制 {#known-limitations}

請考量在下列任一限製作為擷取移轉集的一部分時發現時，整個擷取會失敗：

* 名稱超過150個字元的JCR節點
* 大於16 MB的JCR節點
* 任何已擷取`rep:AuthorizableID`的使用者/群組已出現在AEM as a Cloud Service上
* 如果任何擷取並擷取的資產在移轉的下一個反複專案之前，會移至來源或目的地的不同路徑。

## 資產健康狀態 {#asset-health}

與上方區段相比，內嵌&#x200B;**不會**&#x200B;由於下列資產問題而失敗。 不過，強烈建議您在下列情況下採取適當的步驟：

* 缺少原始轉譯的任何資產
* 任何資料夾都遺失`jcr:content`節點。

以上兩個專案皆已在[Best Practice Analyzer](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md)報告中識別及報告。

## 上線檢查清單 {#Go-Live-Checklist}

如需詳細資訊，請參閱[上線檢查清單](/help/journey-onboarding/go-live-checklist.md)檔案。

## 下一步 {#what-is-next}

瞭解如何移轉至AEM as a Cloud Service後，您可以檢查[Post — 上線](/help/journey-migration/post-go-live.md)頁面，讓您的執行個體保持順暢運作。
