---
title: AEM as a Cloud Service 開發方針
description: AEM as a Cloud Service 開發方針
translation-type: tm+mt
source-git-commit: ce797518714a4919bcdb6187aeaaf35dd1cb76b4
workflow-type: tm+mt
source-wordcount: '2283'
ht-degree: 1%

---


# AEM as a Cloud Service 開發方針 {#aem-as-a-cloud-service-development-guidelines}

以Cloud Service身AEM份運行的代碼必須知道它始終在群集中運行。 這表示執行中的例項永遠多於一個。程式碼必須具彈性，尤其是當例項可能在任何時間點停止時。

在更新作為AEMCloud Service的過程中，將會有新舊代碼並行運行的實例。 因此，舊程式碼不得中斷使用新程式碼建立的內容，而新程式碼必須能夠處理舊內容。
<!--

>[!NOTE]
> All of the best practices mentioned here hold true for on-premise deployments of AEM, if not stated otherwise. An instance can always stop due to various reasons. However, with Skyline it is more likely to happen therefore an instance stopping is the rule not an exception.

-->

如果需要識別叢集中的主要檔案，則可使用Apache Sling Discovery API來偵測它。

## 記憶體中的狀態{#state-in-memory}

狀態不能保留在記憶體中，但必須保存在儲存庫中。 否則，如果實例停止，此狀態可能會丟失。

## 檔案系統上的狀態{#state-on-the-filesystem}

實例的檔案系統不應用作AEMCloud Service。 碟片是短暫的，當實例被回收時，碟片將被處理。 對與處理單個請求相關的臨時儲存使用檔案系統是可能的，但不應濫用於大檔案。 這是因為它可能對資源使用配額產生負面影響，並且會遇到磁碟限制。

例如，不支援檔案系統使用，發佈層應確保需要保存的任何資料都會送出至外部服務，以便長期儲存。

## 觀察{#observation}

類似地，由於所有非同步發生的事情，如對觀察事件採取行動，它無法保證在本地執行，因此必須小心使用。 JCR事件和Sling資源事件都是如此。 當發生變更時，該實例可以被取下並被另一個實例替換。 拓撲中當時處於活動狀態的其他實例將能夠對該事件做出響應。 但是，在這種情況下，這將不是本地事件，在事件發佈時，如果領導人選舉持續，甚至可能沒有現任領導人。

## 後台任務和長期運行的作業{#background-tasks-and-long-running-jobs}

作為後台任務執行的代碼必須假定它正在運行的實例可以隨時關閉。 因此，程式碼必須具彈性，而且大部分的匯入都可繼續。 這表示如果重新執行程式碼，它不應從頭開始，而是從離開的位置開始。 雖然這並非此類程式碼的新需求，AEM但Cloud Service而言，執行個體下載的可能性較高。

為了將問題減到最低，應盡可能避免長時間運行的工作，並且應至少恢復這些工作。 若要執行這些工作，請使用Sling Jobs，其中至少提供一次保證，因此，如果中斷，將會盡快重新執行。 但它們或許不應該從頭開始。 對於排程這類作業，最好使用[Sling Jobs](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing)排程器，這又是至少一次執行。

Sling Commons Scheduler不應用於排程，因為執行無法保證。 只是更有可能會排定。

同樣地，所有非同步發生的動作，例如對觀察事件（無論是JCR事件或Sling資源事件），都無法保證執行，因此必須謹慎使用。 目前的部AEM署已如此。

## 傳出HTTP連接{#outgoing-http-connections}

強烈建議任何傳出的HTTP連線都設定合理的連線和讀取逾時。 對於不套用這些逾時的程式碼，AEM以Cloud Service形式執AEM行的例項會強制執行全域逾時。 這些逾時值是連線呼叫的10秒，以及下列常用Java程式庫所使用連線的讀取呼叫的60秒：

Adobe建議使用提供的[Apache HttpComponents客戶端4.x庫](https://hc.apache.org/httpcomponents-client-ga/)進行HTTP連接。

已知可行但可能需要自行提供依賴性的替代方案：

* [java.net.](https://docs.oracle.com/javase/7/docs/api/java/net/URL.html) URL和／或 [java.net.URLConnection](https://docs.oracle.com/javase/7/docs/api/java/net/URLConnection.html) (由提供AEM)
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/) （不建議使用，因為它已過時並由4.x版取代）
* [確定Http](https://square.github.io/okhttp/) (未由提供AEM)

## 無經典UI自定義{#no-classic-ui-customizations}

因AEM為Cloud Service僅支援協力廠商客戶程式碼的Touch UI。 傳統UI無法自訂。

## 避免本機二進位檔{#avoid-native-binaries}

程式碼將無法在執行時期下載二進位檔，也無法加以修改。 例如，它將無法解壓縮`jar`或`tar`檔案。

## 無流二進位檔案AEM以{#no-streaming-binaries}Cloud Service形式傳遞

二進位檔應透過CDN存取，CDN將在核心服務以外提供二進位AEM檔。

例如，請勿使用`asset.getOriginal().getStream()`，因為會觸發將二進位檔下載至AEM服務的短暫磁碟。

## 無反向複製代理{#no-reverse-replication-agents}

作為Cloud Service，不支援從「發佈」到「作者」的AEM反向複製。 如果需要此類策略，您可以使用在發佈實例群（可能包括作者叢集）之間共用的外部永續性商店。

## 轉發複製代理可能需要移植{#forward-replication-agents}

內容會透過pub-sub機制從「作者」複製到「發佈」。 不支援自定義複製代理。

## 監視和調試{#monitoring-and-debugging}

### 記錄檔 {#logs}

對於本地開發，日誌條目將寫入`/crx-quickstart/logs`資料夾中的本地檔案。

在雲端環境中，開發人員可以透過Cloud Manager下載記錄檔，或使用命令列工具來追蹤記錄檔。<!-- See the [Cloud Manager documentation](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Note that custom logs are not supported and so all logs should be output to the error log. -->

**設定日誌級別**

若要變更雲端環境的記錄層級，Sling Logging OSGI組態應加以修改，然後進行完整重新部署。 由於這並非瞬時，請務必小心在接收大量流量的生產環境中啟用詳細記錄。 在未來，可能會有更快速變更記錄層級的機制。

>[!NOTE]
>
>若要執行下列的設定變更，您必須在本機開發環境上建立這些變更，然後將它們推送至AEMCloud Service例項。 有關如何執行此操作的詳細資訊，請參見[ Deploying to AEM as aCloud Service](/help/implementing/deploying/overview.md)。

**啟用DEBUG日誌級別**

預設日誌級別為INFO，即不記錄DEBUG消息。
若要啟用DEBUG記錄檔層級，請設定

``` /libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level ```

屬性進行除錯。 請勿將記錄檔保留在DEBUG記錄檔層級，因為它會產生許多記錄檔。
除錯檔案中的一行通常以DEBUG開頭，然後提供記錄檔層級、安裝程式動作和記錄檔訊息。 例如：

``` DEBUG 3 WebApp Panel: WebApp successfully deployed ```

日誌級別如下：

| 0 | 致命錯誤 | 動作失敗，安裝程式無法繼續。 |
|---|---|---|
| 1 | 錯誤 | 動作失敗。 安裝將繼續，但CRX的某部分安裝不正確，因此無法正常工作。 |
| 2 | 警告 | 行動成功，但遇到問題。 CRX可能正常工作，也可能無法正常工作。 |
| 3 | 資訊 | 動作成功。 |

### 線程轉儲{#thread-dumps}

雲環境上的線程轉儲是持續收集的，但目前無法以自助方式下載。 同時，如果需要執行緒AEM轉儲來調試問題，請與支援部門聯繫，指定確切的時間窗口。

## CRX/DE Lite和Developer Console {#crxde-lite-and-developer-console}

### 本地開發{#local-development}

對於本端開發，開發人員可完整存取CRXDE Lite(`/crx/de`)AEM和Web主控台(`/system/console`)。

請注意，在本機開發（使用SDK）中，`/apps`和`/libs`可直接寫入，這與不可變的雲端環境不同。

### 作AEM為Cloud Service開發工具{#aem-as-a-cloud-service-development-tools}

客戶可在作者層的開發環境中存取CRXDE lite，但不能在舞台或生產環境中存取。 不可變的儲存庫(`/libs`, `/apps`)在運行時無法寫入，因此嘗試寫入將導致錯誤。

Developer Console提供一組工具，AEM可讓您在開發、階段和生產環境中，以Cloud Service開發人員環境的方式進行除錯。 可依下列方式調整「作者」或「發佈」服務URL來判斷URL:

`https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com`

作為捷徑，可使用下列Cloud Manager CLI命令，根據下述環境參數啟動開發人員主控台：

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

如需詳細資訊，請參閱[本頁](/help/release-notes/home.md)。

開發人員可產生狀態資訊，並解析各種資源。

如下圖所示，可用的狀態資訊包括bundles、components、OSGI組態、oak indexes、OSGI服務和Sling工作的狀態。

![開發控制台1](/help/implementing/developing/introduction/assets/devconsole1.png)

如下圖所示，開發人員可解決套件相依性和servlet:

![開發控制台2](/help/implementing/developing/introduction/assets/devconsole2.png)

![開發控制台3](/help/implementing/developing/introduction/assets/devconsole3.png)

此外，Developer Console還提供Explain Query工具的連結，以進行除錯：

![開發控制台4](/help/implementing/developing/introduction/assets/devconsole4.png)

對於「生產」程式，「開發人員主控台」的存取權是由Admin Console中的「雲端管理員——開發人員角色」定義，而對於沙盒程式，「開發人員主控台」則可供任何具有產品設定檔的使用者以Cloud Service的身分AEM存取。 對於所有程式，狀態轉儲都需要「Cloud Manager - Developer Role」，而且用戶還必須在作者和發佈服務的「用戶或管理員產品配置檔案」中定義，才能查看來自這兩個服務的狀態轉儲資料。 如需有關設定使用者權限的詳細資訊，請參閱[Cloud Manager檔案](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html)。


### AEM Staging and Production Service {#aem-staging-and-production-service}

客戶將無法存取測試和生產環境的開發人員工具。

### 效能監控{#performance-monitoring}

Adobe會監控應用程式的效能，並在出現惡化時採取措施加以處理。 目前無法檢視應用程式量度。

## 專用出口IP地址{#dedicated-egress-ip-address}

在請求時，AEM作為Cloud Service，將為HTTP（埠80）和HTTPS（埠443）以Java代碼寫程式的出站通信量提供靜態的專用IP地址。

### 優點{#benefits}

此專屬IP位址可增強與SaaS廠商（如CRM廠商）整合或在外部以Cloud Service方式進行其他整合時的安全性，AEM並提供IP位址允許清單。 通過將專用IP地址添加到允許清單，它確保僅允許來自客戶AEMCloud Service的流量流入外部服務。 這是除了允許來自任何其他IP的流量外。

若未啟用專用的IP位址功能，以Cloud Service形式傳AEM出的流量會透過與其他客戶共用的一組IP流量。

### 設定 {#configuration}

若要啟用專用IP位址，請向客戶支援提交要求，客戶支援將提供IP位址資訊。 請求應指定每個環境，如果新環境在初始請求後需要此功能，則應提出其他請求。 不支援沙盒程式環境。

### 功能使用{#feature-usage}

此功能與導致傳出流量的Java程式碼或程式庫相容，前提是這些程式碼或程式庫使用標準Java系統屬性進行Proxy組態。 實際上，這應該包括最常見的資料庫。

以下是程式碼範例：

```
public JSONObject getJsonObject(String relativePath, String queryString) throws IOException, JSONException {
  String relativeUri = queryString.isEmpty() ? relativePath : (relativePath + '?' + queryString);
  URL finalUrl = endpointUri.resolve(relativeUri).toURL();
  URLConnection connection = finalUrl.openConnection();
  connection.addRequestProperty("Accept", "application/json");
  connection.addRequestProperty("X-API-KEY", apiKey);

  try (InputStream responseStream = connection.getInputStream(); Reader responseReader = new BufferedReader(new InputStreamReader(responseStream, Charsets.UTF_8))) {
    return new JSONObject(new JSONTokener(responseReader));
  }
}
```

同一專用IP適用於客戶Adobe組織中的所有程式，以及每個程式中的所有環境。 它同時適用於作者和發佈服務。

僅支援HTTP和HTTPS埠。 這包括HTTP/1.1，以及加密時的HTTP/2。

### 調試注意事項{#debugging-considerations}

為了驗證流量是否確實在預期的專用IP位址上傳出，請檢查目標服務中的日誌（如果可用）。 否則，呼叫除錯服務(例如[https://ifconfig.me/ip](https://ifconfig.me/ip))可能會很有用，因為除錯服務會傳回呼叫的IP位址。

## 傳送電子郵件{#sending-email}

因AEM為Cloud Service需要加密出站郵件。 以下章節說明如何要求、設定和傳送電子郵件。

### 請求訪問{#requesting-access}

依預設，會停用傳出電子郵件。 若要啟動它，請提交支援票證，其中包含：

1. 郵件伺服器的完全限定域名（例如`smtp.sendgrid.net`）
1. 要使用的埠。 如果郵件伺服器支援，則埠應為465 ，否則埠為587。 請注意，只有當郵件伺服器要求並強制在該埠上使用TLS時，才能使用埠587
1. 要寄出的環境的程式ID和環境ID
1. 作者、發佈或兩者都需要SMTP訪問。

### 傳送電子郵件{#sending-emails}

應使用[Day CQ Mail Service OSGI服務](https://docs.adobe.com/content/help/en/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service)，並且必須將電子郵件發送到支援請求中指明的郵件伺服器，而不是直接發送給收件人。

CSAEM要求透過465連接埠傳送郵件。 如果郵件伺服器不支援埠465，則只要啟用TLS選項，就可以使用埠587。

>[!NOTE]
>
>請注意，Adobe不支援對唯一專用IP地址進行SMTP查找。

### 設定 {#email-configuration}

中的電AEM子郵件應使用[Day CQ Mail Service OSGi服務](https://docs.adobe.com/content/help/en/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service)發送。

如需設定電子郵件設定的詳細資訊，請參AEM閱[ 6.5檔案](https://docs.adobe.com/content/help/en/experience-manager-65/administering/operations/notification.html)。 對於AEMCloud Service，必須對`com.day.cq.mailer.DefaultMailService OSGI`服務進行以下調整：

如果已請求埠465:

* 將`smtp.port`設為`465`
* 將`smtp.ssl`設為`true`

如果請求了埠587（僅當郵件伺服器不支援埠465時允許）:

* 將`smtp.port`設為`587`
* 將`smtp.ssl`設為`false`

`smtp.starttls`屬性將在運行時自AEM動作為Cloud Service設定為適當值。 因此，如果`smtp.tls`設為true，則會忽略`smtp.startls`。 如果`smtp.ssl`設為false，則`smtp.starttls`設為true。 無論在OSGI配置中設定的`smtp.starttls`值如何。
