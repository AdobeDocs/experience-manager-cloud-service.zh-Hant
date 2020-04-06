---
title: AEM 雲端服務開發方針
description: '待完成 '
translation-type: tm+mt
source-git-commit: 3d2705262d9c82a1486e460247b468259d5ed600

---


# AEM 雲端服務開發方針 {#aem-as-a-cloud-service-development-guidelines}

在AEM中以雲端服務形式執行的程式碼必須知道它一律在叢集中執行。 這表示執行中總有多個執行個體。 程式碼必須具彈性，尤其是當例項可能在任何時間點停止時。

在將AEM更新為雲端服務期間，將會有舊程式碼和新程式碼並行執行的例項。 因此，舊程式碼不得中斷使用新程式碼建立的內容，而新程式碼必須能夠處理舊內容。
<!--

>[!NOTE]
> All of the best practices mentioned here hold true for on-premise deployments of AEM, if not stated otherwise. An instance can always stop due to various reasons. However, with Skyline it is more likely to happen therefore an instance stopping is the rule not an exception.

-->

如果需要識別叢集中的主版，可使用Apache Sling Discovery API來偵測主版。

## 記憶體狀態 {#state-in-memory}

狀態不能保留在記憶體中，但必須保存在儲存庫中。 否則，如果實例停止，此狀態可能會丟失。

## 檔案系統上的狀態 {#state-on-the-filesystem}

在AEM中，不應將例項的檔案系統當做雲端服務使用。 碟片是短暫的，當實例被回收時，碟片將被處理。 對與處理單個請求相關的臨時儲存使用檔案系統是可能的，但不應濫用於大檔案。 這是因為它可能對資源使用配額產生負面影響，並且會遇到磁碟限制。

例如，不支援檔案系統使用，發佈層應確保需要保存的任何資料都會送出至外部服務，以便長期儲存。

## 觀察 {#observation}

類似地，由於所有非同步發生的事情，如對觀察事件採取行動，它無法保證在本地執行，因此必須小心使用。 JCR事件和Sling資源事件都是如此。 當發生變更時，該實例可以被取下並被另一個實例替換。 拓撲中當時處於活動狀態的其他實例將能夠對該事件做出響應。 但是，在這種情況下，這將不是本地事件，在事件發佈時，如果領導人選舉持續，甚至可能沒有現任領導人。

## 後台任務和長期運行的作業 {#background-tasks-and-long-running-jobs}

作為後台任務執行的代碼必須假定它正在運行的實例可以隨時關閉。 因此，程式碼必須具彈性，而且大部分的匯入都可繼續。 這表示如果重新執行程式碼，它不應從頭開始，而是從離開的位置開始。 雖然這並非此類程式碼的新需求，但在AEM中，做為雲端服務，執行個體停止運作的可能性較高。

為了將問題減到最低，應盡可能避免長時間運行的工作，並且應至少恢復這些工作。 若要執行這些工作，請使用Sling Jobs，其中至少提供一次保證，因此，如果中斷，將會盡快重新執行。 但它們或許不應該從頭開始。 對於排程此類作業，最好使用 [Sling Jobs](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing) scheduler，這又是至少一次執行。

Sling Commons Scheduler不應用於排程，因為執行無法保證。 只是更有可能會排定。

同樣地，所有非同步發生的動作，例如對觀察事件（無論是JCR事件或Sling資源事件），都無法保證執行，因此必須謹慎使用。 目前AEM部署已具備這個條件。

## 傳出HTTP連接 {#outgoing-http-connections}

強烈建議任何傳出的HTTP連線都設定合理的連線和讀取逾時。 對於不套用這些逾時的程式碼，在AEM上以雲端服務形式執行的AEM例項將強制執行全域逾時。 這些逾時值是連線呼叫的10秒，以及下列常用Java程式庫所使用連線的讀取呼叫的60秒：

Adobe建議使用提供的 [Apache HttpComponents Client 4.x程式庫來建立HTTP連線](https://hc.apache.org/httpcomponents-client-ga/) 。

已知可行但可能需要自行提供依賴性的替代方案：

* [java.net.URL](https://docs.oracle.com/javase/7/docs/api/java/net/URL.html) 和／或java.net.UR [LConnection](https://docs.oracle.com/javase/7/docs/api/java/net/URLConnection.html) （由AEM提供）
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/) （不建議使用，因為它已過時並由4.x版取代）
* [確定Http](https://square.github.io/okhttp/) （AEM未提供）

## 無傳統UI自定義 {#no-classic-ui-customizations}

AEM作為雲端服務僅支援第三方客戶程式碼的Touch UI。 傳統UI無法自訂。

## 避免原生二進位檔 {#avoid-native-binaries}

程式碼將無法在執行時期下載二進位檔，也無法加以修改。 例如，它將無法解壓縮或解 `jar` 壓縮 `tar` 檔案。

## 無透過AEM做為雲端服務的串流二進位檔 {#no-streaming-binaries}

二進位檔案應透過CDN存取，CDN將在核心AEM服務以外提供二進位檔案。

例如，請勿使用，這 `asset.getOriginal().getStream()`會觸發將二進位檔下載到AEM服務的短暫磁碟。

## 無反向複製代理 {#no-reverse-replication-agents}

AEM中不支援從「發佈」到「作者」的反向複製，做為雲端服務。 如果需要此類策略，您可以使用在發佈實例群（可能包括作者叢集）之間共用的外部永續性商店。

## 轉發複製代理可能需要移植 {#forward-replication-agents}

內容會透過pub-sub機制從「作者」複製到「發佈」。 不支援自定義複製代理。

## 監控與除錯 {#monitoring-and-debugging}

### 記錄檔 {#logs}

有關如何使用日誌的詳細資訊，請參閱日 [志文檔](/help/implementing/developing/introduction/logging.md)。

### 線程轉儲 {#thread-dumps}

雲環境上的線程轉儲是持續收集的，但目前無法以自助方式下載。 同時，如果需要執行緒轉儲來除錯問題，請連絡AEM支援，並指定確切的時間視窗。

## CRX/DE Lite和系統控制台 {#crxde-lite-and-system-console}

### 地方開發 {#local-development}

針對本端開發，開發人員可完整存取CRXDE Lite(`/crx/de`)和AEM Web Console(`/system/console`)。

請注意，在本端開發（使用雲端快速入門）時， `/apps``/libs` 可以直接寫入，這與雲端環境不同，雲端環境中的頂層資料夾是不可變的。

### AEM as a Cloud Service Development tools {#aem-as-a-cloud-service-development-tools}

客戶可在開發環境中存取CRXDE lite，但無法在舞台或生產環境中存取。 不可變的儲存庫(`/libs`, `/apps`)在運行時無法寫入，因此嘗試寫入將導致錯誤。

Developer Console中提供一組工具，可讓您將AEM除錯為Cloud Service開發人員環境，以用於開發、階段和生產環境。 可依下列方式調整「作者」或「發佈」服務URL來判斷URL:

`https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com`

作為捷徑，可使用下列Cloud Manager CLI命令，根據下述環境參數啟動開發人員主控台：

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

如需 [詳細資訊](/help/release-notes/home.md) ，請參閱本頁。

開發人員可產生狀態資訊，並解析各種資源。

如下圖所示，可用的狀態資訊包括bundles、components、OSGI組態、oak indexes、OSGI服務和Sling工作的狀態。

![開發控制台1](/help/implementing/developing/introduction/assets/devconsole1.png)

如下圖所示，開發人員可解決套件相依性和servlet:

![開發控制台2](/help/implementing/developing/introduction/assets/devconsole2.png)

![開發控制台3](/help/implementing/developing/introduction/assets/devconsole3.png)

此外，Developer Console還提供Explain Query工具的連結，以進行除錯：

![開發控制台4](/help/implementing/developing/introduction/assets/devconsole4.png)

### AEM Staging and Production Service {#aem-staging-and-production-service}

客戶將無法存取測試和生產環境的開發人員工具。

### 效能監控 {#performance-monitoring}

Adobe會監控應用程式的效能，並在出現惡化時採取措施加以處理。 目前無法檢視應用程式量度。