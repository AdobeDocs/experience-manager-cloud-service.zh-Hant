---
title: 入門
description: 瞭解在程式碼和內容準備就緒後，如何執行移轉
exl-id: 10ec0b04-6836-4e26-9d4c-306cf743224e
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '1704'
ht-degree: 4%

---

# 入門 {#go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_prep"
>title="上線準備"
>abstract="為確保 AEM as a Cloud Service 順利而成功地上線，您應該規劃程式碼和內容凍結期、測試反覆項目、內容加值、效能測試、安全性測試等。"

在這段歷程中，您將瞭解在程式碼和內容準備好移至AEMas a Cloud Service後，如何規劃及執行移轉。 此外，您也會瞭解執行移轉時的最佳實務和已知限制。

## 到目前為止 {#story-so-far}

在歷程的前幾個階段中：

* 您已瞭解如何在中開始移至AEMas a Cloud Service [快速入門](/help/journey-migration/getting-started.md) 頁面。
* 閱讀「 」，判斷您的部署是否已準備好移至雲端。 [整備階段](/help/journey-migration/readiness.md)
* 熟悉讓您的程式碼和內容雲端準備好使用的工具和流程 [實作階段](/help/journey-migration/implementation.md).

## 目標 {#objective}

本檔案可協助您瞭解在熟悉歷程的先前步驟後，如何執行移轉至AEMas a Cloud Service。 您將瞭解如何執行初始生產移轉，以及移轉到AEMas a Cloud Service時遵循的最佳實務。

## 初始生產移轉 {#initial-migration}

在執行生產移轉之前，請遵循中概述的移轉步驟說明和證明。 [內容移轉策略和時間表](/help/journey-migration/implementation.md##strategy-timeline) 的區段 [實作階段](/help/journey-migration/implementation.md).

* 根據您在翻制上執行AEMas a Cloud Service階段移轉期間獲得的體驗，從生產環境啟動移轉：
   * Author-Author
   * Publish-Publish

* 驗證內嵌至AEMas a Cloud Service製作和發佈層級的內容。
* 指示內容製作團隊在內嵌完成前，避免同時在來源和目的地移動內容
* 可以新增、編輯或刪除新內容，但請避免移動內容。 這同時適用於來源和目的地。
* 記錄 [花費時間](/help/journey-migration/implementation.md#gathering-data) 完整擷取和內嵌，需要估計未來追加移轉時間表。
* 建立 [移轉規劃工具](/help/journey-migration/implementation.md#migration-plan) 適用於作者與發佈。

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

* 從作者移轉至作者，再從發佈移轉至發佈
* 請求可用於以下作業的生產複製：
   * 擷取儲存區域統計資料
   * 移轉活動證明
   * 準備移轉計畫
   * 識別內容凍結需求
   * 從生產環境執行移轉時，識別生產環境上的任何規模調整需求

**內容轉移工具最佳實務**

確定上線時，您會在生產環境中執行內容移轉，而非翻制。 好的方法是使用 [AZCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) 進行初始移轉，然後經常（甚至每天）執行追加擷取，以擷取較小區塊，並避免來源AEM上的任何長期負載。

執行生產移轉時，您應該避免從翻制執行「內容轉移工具」，因為：

* 如果客戶在追加移轉期間需要移轉內容版本，則從複製執行內容轉移工具不會移轉版本。 即使經常從即時作者重新建立翻制，每次建立翻制時，「內容轉移工具」用來計算延長的查核點都會重設。
* 由於複製無法重新整理為整體，因此必須使用ACL查詢套件來封裝和安裝從生產環境新增或編輯到複製環境的內容。 此方法的問題在於，除非從來源和複製中手動刪除，否則來源執行個體上任何已刪除的內容永遠無法進入複製。 這會產生生產環境刪除的內容不會從原地複製和AEMas a Cloud Service刪除的可能性。

**在執行內容移轉時最佳化AEM來源的負載**

請記住，在提取階段期間，AEM來源的負載會較大。 請留意：

* 內容轉移工具是外部Java程式，使用4 GB的JVM棧積
* 非AzCopy版本會下載二進位檔案，並將其儲存在來源AEM作者的暫存空間中，耗用磁碟I/O，然後上傳至Azure容器，耗用網路頻寬
* [AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) 將blob直接從blob存放區傳輸至Azure容器，以儲存磁碟I/O和網路頻寬。 AzCopy版本仍會使用磁碟和網路頻寬，從區段存放區擷取資料並上傳到Azure容器
* 內容轉移工具程式在擷取階段期間對系統資源較輕，因為它只會串流擷取記錄，而且就磁碟I/O或網路頻寬而言，來源執行個體的負載並不大。

## 已知限制 {#known-limitations}

請考量在下列任一限製作為擷取移轉集的一部分時發現時，整個擷取會失敗：

* 名稱超過150個字元的JCR節點
* 大於16 MB的JCR節點
* 任何使用者/群組具有 `rep:AuthorizableID` 已內嵌在AEMas a Cloud Service上
* 如果任何擷取並擷取的資產在移轉的下一個反複專案之前，會移至來源或目的地的不同路徑。

## 資產健康狀態 {#asset-health}

與擷取上方區段比較 **不會** 失敗，因為有下列資產問題。 不過，強烈建議您在下列情況下採取適當的步驟：

* 缺少原始轉譯的任何資產
* 任何資料夾遺失 `jcr:content` 節點。

以上兩個專案均可識別並回報 [Best Practice Analyzer](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) 報告。

## 上線檢查清單 {#Go-Live-Checklist}

請檢閱此活動清單，以確保您順利且成功地執行移轉。

* 執行具有功能和UI測試的端對端生產管道，以確保 **永遠最新** AEM產品體驗。 請參閱下列資源。
   * [AEM 版本更新](/help/implementing/deploying/aem-version-updates.md)
   * [自訂功能測試](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)
   * [UI 測試](/help/implementing/cloud-manager/ui-testing.md)
* 將內容移轉至生產環境，並確保中繼上有相關的子集可用於測試。
   * AEM適用的DevOps最佳實務表示程式碼會從開發環境移至生產環境，而內容會從生產環境下移。
* 排程程式碼和內容凍結期間。
   * 另請參閱區段 [移轉的程式碼和內容凍結時間表](#code-content-freeze)
* 執行最終追加內容。
* 驗證Dispatcher設定。
   * 使用本機Dispatcher驗證器，方便您在本機設定、驗證和模擬Dispatcher
      * [設定本機Dispatcher工具](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=en#prerequisites)
   * 請仔細檢閱虛擬主機組態。
      * 最簡單（也是預設）的解決方案是包含 `ServerAlias *` 虛擬主機檔案中的 `/dispatcher/src/conf.d/available_vhostsfolder`.
         * 如此一來，產品功能測試、Dispatcher快取失效和複製所使用的主機別名就能正常運作。
      * 但是，如果 `ServerAlias *` 不可接受，至少符合下列條件 `ServerAlias` 除了您的自訂網域外，也必須允許輸入專案：
         * `localhost`
         * `*.local`
         * `publish*.adobeaemcloud.net`
         * `publish*.adobeaemcloud.com`
* 設定CDN、SSL和DNS。
   * 如果您使用自己的CDN，請輸入支援票證以設定適當的路由。
      * 請參閱區段 [客戶CDN指向AEM Managed CDN](/help/implementing/dispatcher/cdn.md#point-to-point-cdn) 詳細資訊，請參閱CDN檔案。
      * 根據您的CDN供應商的檔案設定SSL和DNS。
   * 如果您沒有使用其他CDN，請按照以下檔案管理SSL和DNS：
      * 管理 SSL 憑證
         * [管理 SSL 憑證的簡介](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
         * [管理SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
      * 管理自訂網域名稱(DNS)
         * 為了確保DNS轉換不會帶來非預期的問題，最好是在您上線並進行一輪UAT測試之前，建立測試子網域以將您的生產執行個體連線到上。 因此，如果您的網域是example.com，您可以建立子網域test.example.com並將其套用至生產環境。 在網域的UAT測試期間，您需要尋找適當的連結重新導向、快取和Dispatcher設定等。
         * [自訂網域名稱簡介](/help/implementing/cloud-manager/custom-domain-names/introduction.md)
         * [新增自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)
         * [管理自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)
   * 請記得驗證DNS記錄的TTL集合。
      * TTL是在要求伺服器更新之前DNS記錄保留在快取中的時間。
      * 如果您的TTL非常高，則傳播DNS記錄的更新將需要更長的時間。
* 執行符合業務需求和目標的效能和安全測試。
* 請剪下資料，並確定實際上線是在沒有任何新部署或內容更新的情況下執行的。
* 建立Admin Console使用者通知設定檔。 另請參閱 [通知設定檔](/help/journey-onboarding/notification-profiles.md)

您一律可以參考清單，以備在執行移轉時需重新校準工作時使用。

## 下一步 {#what-is-next}

瞭解如何移轉至AEMas a Cloud Service後，您可以檢查 [上線後](/help/journey-migration/post-go-live.md) 頁面來保持您的執行個體順利執行。
