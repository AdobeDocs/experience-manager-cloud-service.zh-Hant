---
title: AEM as a Cloud Service 開發方針
description: AEM as a Cloud Service 開發方針
exl-id: 94cfdafb-5795-4e6a-8fd6-f36517b27364
source-git-commit: f5ed5561ed19938b4c647666ff7a6a470d307cf7
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# AEM as a Cloud Service 開發方針 {#aem-as-a-cloud-service-development-guidelines}

在AEM as aCloud Service中執行的程式碼必須了解，它一律在叢集中執行。 這表示執行中的例項永遠多於一個。程式碼必須具有彈性，尤其是例項可能隨時停止。

在更新AEM as aCloud Service期間，會有舊程式碼和新程式碼並行執行的例項。 因此，舊程式碼不得中斷由新程式碼建立的內容，而新程式碼必須能夠處理舊內容。
<!--

>[!NOTE]
> All of the best practices mentioned here hold true for on-premise deployments of AEM, if not stated otherwise. An instance can always stop due to various reasons. However, with Skyline it is more likely to happen therefore an instance stopping is the rule not an exception.

-->

如果需要識別叢集中的主要伺服器，則可使用Apache Sling Discovery API來偵測。

## 記憶體{#state-in-memory}中的狀態

狀態不得保留在記憶體中，而應保存在儲存庫中。 否則，如果執行個體停止，則此狀態可能會遺失。

## 檔案系統{#state-on-the-filesystem}上的狀態

在AEM中，不應將執行個體的檔案系統作為Cloud Service。 磁碟是短暫的，當回收實例時，將處理該磁碟。 對與處理單個請求相關的臨時儲存使用檔案系統是可能的，但不應濫用於大型檔案。 這是因為它可能對資源使用配額產生負面影響，並受到磁碟限制。

例如，不支援檔案系統使用情形，發佈層級應確保需要保存的任何資料都傳送至外部服務，以供長期儲存。

## 觀察 {#observation}

類似地，非同步發生的一切都會發生，例如在觀察事件上採取行動，無法保證會在本機執行，因此必須謹慎使用。 JCR事件和Sling資源事件均適用。 當發生變更時，例項可被取下，並由不同例項取代。 拓撲中當時處於活動狀態的其他實例將能夠對該事件做出反應。 但是，在這種情況下，這不會是地方性事件，而且，如果當事件發佈時，領導者選舉正在進行，甚至可能沒有活躍的領導者。

## 後台任務和長時間運行的作業{#background-tasks-and-long-running-jobs}

作為背景任務執行的代碼必須假設它正在運行的實例可以隨時刪除。 因此，程式碼必須具有彈性，且大部分匯入都可恢復。 這表示如果程式碼重新執行，應該不會從頭開始，而是從離開的位置開始。 雖然這並非這類程式碼的新需求，但在AEM as aCloud Service中，執行個體淘汰的可能性較大。

為了將問題降至最低，應盡可能避免長時間運行的作業，並且至少應可恢復這些作業。 若要執行這類工作，請使用Sling工作，Sling工作提供至少一次保證，因此若中斷，系統會盡快重新執行。 但它們或許不應該從頭開始。 對於排程這類作業，最好使用[Sling作業](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing)排程器，這樣至少執行一次。

Sling Commons排程器不應用於排程，因為執行無法保證。 只是更有可能會安排。

同樣地，如果非同步發生所有動作，例如對觀察事件採取行動（無論是JCR事件或Sling資源事件），就無法保證執行，因此必須謹慎使用。 目前的AEM部署已採用此方法。

## 傳出HTTP連線{#outgoing-http-connections}

強烈建議所有傳出的HTTP連線都設定合理的連線和讀取逾時。 對於不套用這些逾時的程式碼，以Cloud Service形式在AEM上執行的AEM例項將強制執行全域逾時。 下列逾時值是連線呼叫的10秒，以及下列熱門Java程式庫所使用連線的讀取呼叫的60秒：

Adobe建議使用提供的[Apache HttpComponents Client 4.x library](https://hc.apache.org/httpcomponents-client-ga/)進行HTTP連線。

已知可行，但可能需要自行提供相依性的替代方案為：

* [java.net.](https://docs.oracle.com/javase/7/docs/api/java/net/URL.html) URLand/或 [java.net.URLConnection](https://docs.oracle.com/javase/7/docs/api/java/net/URLConnection.html) (由AEM提供)
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/) （不建議使用，因為已過時並已由4.x版取代）
* [OK Http](https://square.github.io/okhttp/) (AEM未提供)

## 沒有傳統UI自定義{#no-classic-ui-customizations}

AEM as aCloud Service僅支援第三方客戶程式碼的觸控式UI。 傳統UI無法自訂。

## 避免本機二進位檔{#avoid-native-binaries}

程式碼將無法在執行階段下載二進位檔，也無法加以修改。 例如，它將無法解壓縮`jar`或`tar`檔案。

## 沒有透過AEM as aCloud Service{#no-streaming-binaries}串流二進位檔

二進位檔應透過CDN來存取，CDN將提供核心AEM服務以外的二進位檔。

例如，請勿使用`asset.getOriginal().getStream()`，這會觸發將二進位檔下載至AEM服務的短暫磁碟。

## 無反向複製代理{#no-reverse-replication-agents}

AEM as aCloud Service不支援從「發佈」反向復寫至「作者」。 如果需要此策略，您可以使用在發佈執行個體群組（可能是製作叢集）中共用的外部永續性存放區。

## 轉發複製代理可能需要移植{#forward-replication-agents}

內容會透過發佈子機制從製作複製到發佈。 不支援自定義複製代理。

## 監視和調試{#monitoring-and-debugging}

### 記錄檔 {#logs}

對於本地開發，日誌條目將寫入`/crx-quickstart/logs`資料夾中的本地檔案。

在雲端環境中，開發人員可以透過Cloud Manager下載記錄檔，或使用命令列工具追蹤記錄檔。<!-- See the [Cloud Manager documentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Note that custom logs are not supported and so all logs should be output to the error log. -->

**設定記錄層級**

若要變更雲端環境的記錄層級，應修改Sling Logging OSGI設定，然後完全重新部署。 由於這並非即時進行，請務必小心，不要在接收大量流量的生產環境中啟用詳細記錄。 未來可能會有更快速變更記錄層級的機制。

>[!NOTE]
>
>若要執行下列設定變更，您必須在本機開發環境中建立這些變更，然後以Cloud Service例項的形式推送至AEM。 有關如何執行此操作的詳細資訊，請參閱[部署至AEM as aCloud Service](/help/implementing/deploying/overview.md)。

**啟用偵錯記錄層級**

預設日誌級別為INFO，即未記錄DEBUG消息。
若要啟用DEBUG記錄層級，請設定

``` /libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level ```

要除錯的屬性。 請勿將記錄檔保留在DEBUG記錄層級，因為它會產生許多記錄檔。
除錯檔案中的一行通常以DEBUG開頭，然後提供記錄層級、安裝程式動作和記錄訊息。 例如：

``` DEBUG 3 WebApp Panel: WebApp successfully deployed ```

記錄層級如下：

| 0 | 錯誤 | 操作失敗，安裝程式無法繼續。 |
|---|---|---|
| 1 | 錯誤 | 操作失敗。 安裝繼續，但CRX的一部分未正確安裝，因此無法正常工作。 |
| 2 | 警告 | 操作已成功，但遇到問題。 CRX可能或無法正常運作。 |
| 3 | 資訊 | 操作成功。 |

### 線程轉儲{#thread-dumps}

雲端環境上的執行緒傾印會持續收集，但目前無法以自助方式下載。 同時，如果需要執行緒傾印以偵錯問題，請連絡AEM支援，並指定確切的時間視窗。

## CRX/DE Lite和開發人員控制台{#crxde-lite-and-developer-console}

### 本地開發{#local-development}

針對本機開發，開發人員可完整存取CRXDE Lite(`/crx/de`)和AEM Web主控台(`/system/console`)。

請注意，在本機開發（使用SDK）上，`/apps`和`/libs`可直接寫入，這與雲端環境不同，雲端環境中的這些最上層資料夾不可修改。

### AEM as a Cloud Service開發工具{#aem-as-a-cloud-service-development-tools}

客戶可在製作層級的開發環境中存取CRXDE lite，但無法預備或生產。 不可變的儲存庫(`/libs`, `/apps`)無法在運行時寫入，因此嘗試寫入將導致錯誤。

開發、預備和生產環境的開發人員控制台中提供一組工具，可針對開發、預備和生產環境，將AEM偵錯為Cloud Service開發人員環境。 可依下列方式調整「作者」或「發佈」服務URL來決定URL:

`https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com`

作為快捷方式，可使用下列Cloud Manager CLI命令，根據以下描述的環境參數啟動開發人員控制台：

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

如需詳細資訊，請參閱[此頁面](/help/release-notes/home.md)。

開發人員可產生狀態資訊，並解析各種資源。

如下圖所示，可用的狀態資訊包括套件組合、元件、OSGI設定、oak索引、OSGI服務和Sling作業的狀態。

![開發主控台1](/help/implementing/developing/introduction/assets/devconsole1.png)

如下圖所示，開發人員可以解析套件相依性和servlet:

![開發主控台2](/help/implementing/developing/introduction/assets/devconsole2.png)

![開發控制台3](/help/implementing/developing/introduction/assets/devconsole3.png)

對於除錯來說，開發人員控制台也有一個「說明查詢」工具的連結：

![開發主控台4](/help/implementing/developing/introduction/assets/devconsole4.png)

若為生產計畫，使用者可以透過Admin Console中的「雲端管理員 — 開發人員角色」來定義對開發人員控制台的存取權，若為沙箱計畫，只要使用者具備產品設定檔，便能以Cloud Service存取AEM。 對於所有程式，狀態轉儲都需要「Cloud Manager — 開發人員角色」，且使用者也必須在製作和發佈服務的AEM使用者或AEM管理員產品設定檔中定義，才能檢視兩個服務的狀態轉儲資料。 如需設定使用者權限的詳細資訊，請參閱[Cloud Manager檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html)。

### AEM測試與生產服務{#aem-staging-and-production-service}

客戶將無法存取測試和生產環境的開發人員工具。

### 效能監視{#performance-monitoring}

Adobe會監控應用程式效能，並採取措施，以在出現惡化時加以處理。 目前無法查看應用程式量度。

## 專用輸出IP地址{#dedicated-egress-ip-address}

應要求，AEM as aCloud Service會為以Java程式碼編寫的HTTP（埠80）和HTTPS（埠443）傳出流量布建靜態的專屬IP位址。

### 優點 {#benefits}

此專用IP位址可在與SaaS廠商（例如CRM廠商）整合或AEM以外的其他整合(作為提供IP位址允許清單的Cloud Service)時，增強安全性。 將專用的IP位址新增至允許清單，可確保只有來自客戶AEMCloud Service的流量才可流入外部服務。 這是除了允許來自任何其他IP的流量以外。

若未啟用專用IP位址功能，以Cloud Service形式傳出的流量會透過與其他客戶共用的一組IP流量。

### 設定 {#configuration}

若要啟用專用IP位址，請向客戶支援人員提交請求，由客戶支援人員提供IP位址資訊。 如果新環境在初始要求後需要功能，要求應指定每個環境，並提出其他要求。 不支援沙箱方案環境。

### 功能使用{#feature-usage}

若Java系統屬性用於Proxy設定，則此功能與會產生傳出流量的Java程式碼或程式庫相容。 實際上，這應包含最常見的程式庫。

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

同一專用IP會套用至其Adobe組織中的所有客戶方案，以及每個客戶方案中的所有環境。 它適用於製作和發佈服務。

僅支援HTTP和HTTPS埠。 這包括HTTP/1.1，以及加密時的HTTP/2。

### 調試注意事項{#debugging-considerations}

若要驗證流量是否確實在預期的專用IP位址上傳出，請檢查目的地服務的記錄（若有）。 否則，呼叫[https://ifconfig.me/ip](https://ifconfig.me/ip)等偵錯服務可能會很有用，這會傳回呼叫IP位址。

## 傳送電子郵件{#sending-email}

AEM as aCloud Service需要加密傳出郵件。 以下各節說明如何要求、設定及傳送電子郵件。

>[!NOTE]
>
>可以使用OAuth2支援來設定郵件服務。 如需詳細資訊，請參閱[OAuth2 Support for the Mail Service](/help/security/oauth2-support-for-mail-service.md)。

### 請求訪問{#requesting-access}

依預設，會停用傳出電子郵件。 要激活它，請提交支援票證，具體包括：

1. 郵件伺服器的完全限定域名（例如`smtp.sendgrid.net`）
1. 要使用的埠。 如果郵件伺服器支援，它應為埠465，否則為埠587。 請注意，埠587隻能在郵件伺服器要求並強制該埠上的TLS時使用
1. 想要寄出之環境的方案ID和環境ID
1. 作者、發佈或兩者都需要SMTP存取權。

### 傳送電子郵件{#sending-emails}

應使用[Day CQ Mail Service OSGI服務](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service)，且必須將電子郵件傳送至支援請求中指出的郵件伺服器，而非直接傳送給收件者。

AEM CS要求透過連接埠465發送郵件。 如果郵件伺服器不支援埠465，則只要啟用TLS選項，就可以使用埠587。

>[!NOTE]
>
>請注意，Adobe不支援以唯一的專用IP位址進行SMTP重新命名。

### 設定 {#email-configuration}

AEM中的電子郵件應使用[Day CQ Mail Service OSGi服務](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service)傳送。

如需設定電子郵件設定的詳細資訊，請參閱[AEM 6.5檔案](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html)。 對於AEM as aCloud Service，必須對`com.day.cq.mailer.DefaultMailService OSGI`服務進行下列調整：

如果已請求埠465:

* 將`smtp.port`設為&lt;a1/`465`
* 將`smtp.ssl`設為&lt;a1/`true`

如果已請求埠587（僅當郵件伺服器不支援埠465時允許）:

* 將`smtp.port`設為&lt;a1/`587`
* 將`smtp.ssl`設為&lt;a1/`false`

AEM會在執行階段將`smtp.starttls`屬性自動設定為適當的Cloud Service。 因此，如果`smtp.tls`設為true，則會忽略`smtp.startls`。 如果將`smtp.ssl`設為false，則將`smtp.starttls`設為true。 無論在OSGI設定中設定的`smtp.starttls`值為何。

## [!DNL Assets] 開發指南和使用案例  {#use-cases-assets}

若要了解以Cloud Service形式使用資產的開發使用案例、建議和參考資料，請參閱[資產的開發人員參考](/help/assets/developer-reference-material-apis.md#assets-cloud-service-apis)。
