---
title: AEM雲端服務開發准則
description: '待完成 '
translation-type: tm+mt
source-git-commit: 13c0a670330532f574c2b38823b8a924c609e8e4

---


# AEM雲端服務開發准則 {#aem-as-a-cloud-service-development-guidelines}

## 後台任務和長期運行的作業 {#background-tasks-and-long-running-jobs}

作為後台任務執行的代碼必須假定它正在運行的實例可以隨時關閉。 因此，程式碼必須具彈性，而且大部分的匯入都可繼續。 這表示如果重新執行程式碼，它不應從頭開始，而是從離開的位置開始。 雖然這並非此類程式碼的新需求，但在AEM中，做為雲端服務，執行個體停止運作的可能性較高。

為了將問題減到最低，應盡可能避免長時間運行的工作，並且應至少恢復這些工作。 若要執行這些工作，請使用Sling Jobs，其中至少提供一次保證，因此，如果中斷，將會盡快重新執行。 但它們或許不應該從頭開始。 對於排程此類作業，最好使用 [Sling Jobs](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing) scheduler，這又是至少一次執行。

Sling Commons Scheduler不應用於排程，因為執行無法保證。 只是更有可能會排定。

同樣地，所有非同步發生的動作，例如對觀察事件（無論是JCR事件或Sling資源事件），都無法保證執行，因此必須謹慎使用。 目前AEM部署已具備這個條件。

## 傳出HTTP連接 {#outgoing-http-connections}

強烈建議任何傳出的HTTP連線都設定合理的連線和讀取逾時。 對於不套用這些逾時的程式碼，在AEM上以雲端服務形式執行的AEM例項將強制執行全域逾時。 這些逾時值是連線呼叫的10秒，以及下列常用Java程式庫所使用連線的讀取呼叫的60秒：

Adobe建議使用提供的 [Apache httpComponents Client 4.x程式庫來建立HTTP連線](https://hc.apache.org/httpcomponents-client-ga/) 。

已知可行但可能需要自行提供依賴性的替代方案：

* [java.net.URL](https://docs.oracle.com/javase/7/docs/api/java/net/URL.html) 和／或java.net.UR [LConnection](https://docs.oracle.com/javase/7/docs/api/java/net/URLConnection.html) （由AEM提供）
* [Apache Commons httpClient 3.x](https://hc.apache.org/httpclient-3.x/) （不建議使用，因為它已過時並由4.x版取代）
* [OK Http](OK Http(Not provided by AEM)（AEM未提供）)

## 監控與除錯 {#monitoring-and-debugging}

### 記錄檔 {#logs}

* 為進行本端開發，記錄項目會寫入本端檔案
   * `./crx-quickstart/logs`
* 在雲端環境中，開發人員可以透過Cloud manager下載記錄檔，或使用命令列工具來追蹤記錄檔。 <!-- See the [Cloud Manager documentation](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Note that custom logs are not supported and so all logs should be output to the error log. -->
* 若要變更雲端環境的記錄層級，Sling Logging OSGI組態應加以修改，然後進行完整重新部署。 由於這並非瞬時，請務必小心在接收大量流量的生產環境中啟用詳細記錄。 在未來，可能會有更快速變更記錄層級的機制。

### 線程轉儲 {#thread-dumps}

雲環境上的線程轉儲是持續收集的，但目前無法以自助方式下載。 同時，如果需要執行緒轉儲來除錯問題，請連絡AEM支援，並指定確切的時間視窗。

### CRX/DE Lite和系統控制台 {#crxde-lite-and-system-console}

## 地方開發 {#local-development}

針對本端開發，開發人員可完整存取CRXDE Lite(`/crx/de`)和AEM Web Console(`/system/console`)。

請注意，在本端開發（使用雲端快速入門）時， `/apps``/libs` 可以直接寫入，這與雲端環境不同，雲端環境中的頂層資料夾是不可變的。

## AEM做為雲端服務開發工具 {#aem-as-a-cloud-service-development-tools}

客戶可在開發環境中存取CRXDE lite，但無法在舞台或生產環境中存取。 不可變的儲存庫(`/libs`, `/apps`)在運行時無法寫入，因此嘗試寫入將導致錯誤。

Developer console中提供一組工具，可讓您將AEM除錯為Cloud Service開發人員環境，以用於開發、階段和生產環境。 可依下列方式調整作者或發佈服務URL來判斷URL:

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

**AEM Staging and Production Service**

客戶將無法存取測試和生產環境的開發人員工具。

### 診斷 {#diagnostics}

系統控制台適用於開發環境。 但是，測試和生產的診斷轉儲不可用。