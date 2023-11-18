---
title: AEM as a Cloud Service 開發指導方針
description: 了解在 AEM as a Cloud Service 上進行開發的準則，以及它和內部部署的 AEM 以及 AMS 中的 AEM 的重要區別。
exl-id: 94cfdafb-5795-4e6a-8fd6-f36517b27364
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '2732'
ht-degree: 4%

---

# AEM as a Cloud Service 開發指導方針 {#aem-as-a-cloud-service-development-guidelines}

>[!CONTEXTUALHELP]
>id="development_guidelines"
>title="AEM as a Cloud Service 開發指導方針"
>abstract="了解在 AEM as a Cloud Service 上進行開發的準則，以及它和內部部署的 AEM 以及 AMS 中的 AEM 的重要區別。"
>additional-url="https://video.tv.adobe.com/v/330555/" text="套件結構示範"

本檔案說明在AEMas a Cloud Service上開發的准則，以及它與AEM內部部署和AMS中的AEM不同的重要方式。

## 程式碼必須可感知叢集 {#cluster-aware}

在AEMas a Cloud Service中執行的程式碼必須瞭解，它一律在叢集中執行。 這表示執行中的例項永遠多於一個。程式碼必須具復原性，尤其是因為例項可能隨時停止。

在AEMas a Cloud Service更新期間，有些執行個體同時執行舊程式碼和新程式碼。 因此，舊程式碼不得中斷新程式碼建立的內容，且新程式碼必須能夠處理舊內容。

如果需要識別叢集中的主要節點，可以使用Apache Sling Discovery API來偵測它。

## 記憶體中的狀態 {#state-in-memory}

狀態不得保留在記憶體中，而是要保留在存放庫中。 否則，如果執行個體停止，此狀態可能會遺失。

## 檔案系統上的狀態 {#state-on-the-filesystem}

執行個體的檔案系統不應在AEMas a Cloud Service中使用。 磁碟是暫時性的，當執行個體回收時就會加以處置。 在處理單一請求時，可以限制使用檔案系統作為暫時性儲存空間，但不應將其濫用於大型檔案。 這是因為這可能會對資源使用配額產生負面影響，並遇到磁碟限制。

舉例來說，若不支援使用檔案系統，發佈層級應確保任何必須儲存的資料都會運送至外部服務，以供長期儲存之用。

## 觀察 {#observation}

同樣地，由於所有非同步發生的事（例如在觀察事件上動作），無法保證會在本機執行，因此必須謹慎使用。 JCR事件和Sling資源事件都是如此。 發生變更時，可能會移除執行個體，並由其他執行個體取代。 拓撲中當時處於作用中的其他執行個體能夠對該事件做出反應。 但在此情況下，這不會是本機事件，在發佈事件時進行中的領導人選舉的情況下，甚至可能沒有活動的領導人。

## 背景工作與長時間執行的工作 {#background-tasks-and-long-running-jobs}

作為背景工作執行的程式碼必須假設執行所在的例項隨時都會停機。 因此，程式碼必須有韌性，而且最重要的是可恢復。 這表示如果程式碼重新執行，就不應從頭開始，而應從原本的地方開始。 雖然這並非此類程式碼的新要求，但在AEMas a Cloud Service中，執行個體更有可能停止運作。

為了將問題降至最低，應儘可能避免長時間執行工作，而且這些工作應至少可以恢復。 若要執行這類作業，請使用Sling作業，此作業有至少執行一次的保證，因此如果中斷，將會儘快重新執行。 但是他們或許不應該從頭開始。 若要排程這類工作，最好使用 [Sling工作](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing) 排程器，因為這再次可確保至少執行一次。

Sling Commons排程器不應用於排程，因為無法保證執行。 只是更有可能已排程。

同樣地，由於所有非同步發生的事（例如對觀察事件執行動作，包括JCR事件或Sling資源事件），無法保證執行，因此必須謹慎使用。 目前的AEM部署就是如此。

## 傳出HTTP連線 {#outgoing-http-connections}

強烈建議任何傳出HTTP連線設定合理的連線和讀取逾時；連線逾時建議值為1秒，讀取逾時建議值為5秒。 確切的數字必須根據處理這些要求的後端系統的效能來確定。

對於未套用這些逾時的程式碼，在AEMas a Cloud Service上執行的AEM執行個體將強制執行全域逾時。 這些逾時值是連線呼叫的10秒和連線的讀取呼叫的60秒。

Adobe建議使用提供的 [Apache HttpComponents Client 4.x資料庫](https://hc.apache.org/httpcomponents-client-ga/) 用於建立HTTP連線。

已知可以運作，但可能需要自行提供相依性的替代方法是：

* [java.net.URL](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/net/URL.html) 和/或 [java.net.URLConnection](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/net/URLConnection.html) (AEM提供)
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/) （不建議使用，因為它已過時並由4.x版取代）
* [確定Http](https://square.github.io/okhttp/) (AEM未提供)

除了提供逾時功能外，也應對這類逾時功能進行適當處理，以及非預期的HTTP狀態代碼。

## 處理要求速率限制 {#rate-limit-handling}

當AEM的傳入要求速率超過正常程度時，AEM會以HTTP錯誤碼429回應新要求。 對AEM進行程式化呼叫的應用程式可以考慮防禦式編碼，在幾秒鐘後使用指數回退策略重試。 在2023年8月中旬之前，AEM以HTTP錯誤代碼503回應相同的條件。

## 無傳統UI自訂 {#no-classic-ui-customizations}

AEMas a Cloud Service僅支援第三方客戶程式碼的Touch UI。 傳統UI無法供自訂。

## 沒有原生二進位檔或原生程式庫 {#avoid-native-binaries}

原生二進位檔和程式庫不得部署或安裝在雲端環境中。

此外，程式碼在執行階段不應嘗試下載原生二進位檔或原生Java擴充功能（例如JNI）。

## 沒有透過AEMas a Cloud Service的串流二進位檔 {#no-streaming-binaries}

應透過CDN存取二進位檔案，CDN將在核心AEM服務之外提供二進位檔案。

例如，請勿使用 `asset.getOriginal().getStream()`，會觸發將二進位檔案下載至AEM服務的暫存磁碟。

## 沒有反向復寫代理 {#no-reverse-replication-agents}

AEMas a Cloud Service不支援從發佈到作者的反向復寫。 如果需要這類策略，您可以使用在發佈執行個體的陣列之間共用的外部持續性存放區，並有可能使用作者叢集。

## 可能需要移轉轉轉復寫代理 {#forward-replication-agents}

透過pub-sub機制，將內容從Author復寫到Publish。 不支援自訂復寫代理。

## 沒有多載開發環境 {#overloading-dev-envs}

生產環境的大小較高，可確保穩定操作，而中繼環境的大小類似生產環境，可確保生產條件下的實際測試。

開發環境和快速開發環境應僅限於開發、錯誤分析和功能測試，且不應設計為處理高工作負載或大量內容。

例如，在開發環境中變更大型內容存放庫上的索引定義可能會導致重新索引導致太多處理。 需要大量內容的測試應在中繼環境中執行。

## 監視和偵錯 {#monitoring-and-debugging}

### 記錄檔 {#logs}

對於本機開發，記錄專案會寫入本機檔案中的 `/crx-quickstart/logs` 資料夾。

在雲端環境中，開發人員可以透過Cloud Manager下載記錄，或使用命令列工具來追蹤記錄。 <!-- See the [Cloud Manager documentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Note that custom logs are not supported and so all logs should be output to the error log. -->

**設定記錄層級**

若要變更雲端環境的記錄層級，應修改Sling記錄OSGI設定，然後進行完整重新部署。 由於這並非立即發生，因此在接收大量流量的生產環境中，請謹慎啟用詳細記錄檔。 未來可能會有更快速變更紀錄層級的機制。

>[!NOTE]
>
>若要執行下列設定變更，您可在本機開發環境中建立變更，然後將變更推送至AEMas a Cloud Service執行個體。 如需如何執行此動作的詳細資訊，請參閱 [部署至AEMas a Cloud Service](/help/implementing/deploying/overview.md).

**啟動DEBUG記錄層級**

預設記錄層級為INFO，亦即，不會記錄DEBUG訊息。 若要啟用DEBUG記錄層級，請更新下列屬性以偵錯模式。

`/libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level`

例如，設定 `/apps/<example>/config/org.apache.sling.commons.log.LogManager.factory.config~<example>.cfg.json` ，其值如下。

```json
{
   "org.apache.sling.commons.log.names": [
      "com.example"
   ],
   "org.apache.sling.commons.log.level": "DEBUG",
   "org.apache.sling.commons.log.file": "logs/error.log",
   "org.apache.sling.commons.log.additiv": "false"
}
```

請勿將記錄保留在DEBUG記錄層級超過必要的時間，因為這會產生許多專案。

如需永遠記錄，可使用執行模式型OSGi設定目標定位，針對不同的AEM環境設定分散式記錄層級 `DEBUG` 在開發期間。 例如：

| 環境 | 按執行模式列出的OSGi設定位置 | `org.apache.sling.commons.log.level` 屬性值 |
| - | - | - |
| 開發 | /apps/example/config/org.apache.sling.commons.log.LogManager.factory.config~example.cfg.json | 偵錯 |
| 測試 | /apps/example/config.stage/org.apache.sling.commons.log.LogManager.factory.config~example.cfg.json | 警告 |
| 生產 | /apps/example/config.prod/org.apache.sling.commons.log.LogManager.factory.config~example.cfg.json | 錯誤 |

偵錯檔案中的某一行通常以DEBUG開頭，然後提供記錄層級、安裝程式動作和記錄訊息。 例如：

```text
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

記錄層級如下：

| 0 | 嚴重錯誤 | 動作已失敗，安裝程式無法繼續。 |
|---|---|---|
| 1 | 錯誤 | 動作已失敗。 安裝會繼續，但部分CRX未正確安裝且將無法運作。 |
| 2 | 警告 | 動作成功但發生問題。 CRX可能會或可能不會正常運作。 |
| 3 | 資訊 | 動作已成功。 |

### 執行緒傾印 {#thread-dumps}

雲端環境上的對話串傾印會持續收集，但目前無法自助下載。 同時，如果偵錯問題需要執行緒傾印，請聯絡AEM支援，指定確切的時間範圍。

## CRX/DE Lite和開發人員主控台 {#crxde-lite-and-developer-console}

### 本機開發 {#local-development}

對於本機開發，開發人員擁有CRXDE Lite(`/crx/de`)和AEM Web主控台(`/system/console`)。

請注意，在本機開發中（使用SDK）， `/apps` 和 `/libs` 可以直接寫入，這與雲端環境不同，因為雲端環境中的頂層資料夾是無法變更的。

### AEM as a Cloud Service 開發工具 {#aem-as-a-cloud-service-development-tools}

客戶可以在作者階層的開發環境中存取CRXDE Lite，但不能在預備或生產環境中存取。 不可變的存放庫(`/libs`， `/apps`)無法在執行階段寫入，因此嘗試這麼做將會導致錯誤。

而是可以從開發人員控制檯啟動存放庫瀏覽器，為作者、發佈和預覽層級的所有環境提供存放庫的唯讀檢視。 深入瞭解存放庫瀏覽器 [此處](/help/implementing/developing/tools/repository-browser.md).

針對RDE、開發、測試和生產環境，開發人員控制檯提供了一組用於偵錯AEMas a Cloud Service開發人員環境的工具。 可藉由調整作者或發佈服務URL來決定URL，如下所示：

`https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com`

作為捷徑，以下Cloud Manager CLI命令可用於根據以下所述的環境引數啟動開發人員主控台：

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

另請參閱 [此頁面](/help/release-notes/home.md) 以取得詳細資訊。

開發人員可以產生狀態資訊，並解析各種資源。

如下圖所示，可用的狀態資訊包括套件組合、元件、OSGI設定、Oak索引、OSGI服務和Sling工作的狀態。

![開發主控台1](/help/implementing/developing/introduction/assets/devconsole1.png)

如下圖所示，開發人員可以解析套件相依性和servlet：

![開發主控台2](/help/implementing/developing/introduction/assets/devconsole2.png)

![開發主控台3](/help/implementing/developing/introduction/assets/devconsole3.png)

Developer Console也提供除錯功能，連結至Explain查詢工具：

![開發主控台4](/help/implementing/developing/introduction/assets/devconsole4.png)

對於生產計畫，對開發人員控制檯的存取權由Admin Console中的「Cloud Manager — 開發人員角色」定義，而對於沙箱計畫，任何具有產品設定檔的使用者都可以使用Developer Console來存取AEMas a Cloud Service。 對於所有計畫，狀態傾印需要「Cloud Manager — 開發人員角色」，並且還必須在作者和發佈服務的AEM使用者或AEM管理員產品設定檔中定義存放庫瀏覽器和使用者，才能檢視來自這兩個服務的資料。 如需關於設定使用者許可權的詳細資訊，請參閱 [Cloud Manager檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html).

### 效能監控 {#performance-monitoring}

Adobe會監控應用程式效能，並在發現效能惡化時採取措施解決。 目前無法觀察應用程式量度。

## 傳送電子郵件 {#sending-email}

以下各節說明如何請求、設定和傳送電子郵件。

>[!NOTE]
>
>郵件服務可設定為OAuth2支援。 如需詳細資訊，請參閱 [郵件服務的OAuth2支援](/help/security/oauth2-support-for-mail-service.md).

### 啟用傳出電子郵件 {#enabling-outbound-email}

預設會停用用來傳送電子郵件的連線埠。 若要啟動連線埠，請設定 [進階網路](/help/security/configuring-advanced-networking.md)，請務必針對每個所需的環境設定 `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` 端點的連線埠轉送規則，將預期的連線埠（例如，465或587）對應到Proxy連線埠。

建議使用設定進階網路 `kind` 引數設為 `flexiblePortEgress` 因為Adobe可以最佳化彈性連線埠輸出流量的效能。 如果需要唯一的輸出IP位址，請選擇 `kind` 引數： `dedicatedEgressIp`. 如果您因其他原因已設定VPN，您也可以使用該進階網路變數所提供的唯一IP位址。

您必須透過郵件伺服器傳送電子郵件，而非直接傳送給電子郵件使用者端。 否則，可能會封鎖電子郵件。

### 傳送電子郵件 {#sending-emails}

此 [Day CQ郵件服務OSGI服務](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service) 應使用，且必須將電子郵件傳送至支援請求中指出的郵件伺服器，而非直接傳送給收件者。

### 設定 {#email-configuration}

AEM中的電子郵件應使用 [Day CQ Mail Service OSGi服務](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service).

請參閱 [AEM 6.5檔案](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html) 以取得有關設定電子郵件設定的詳細資訊。 對於AEMas a Cloud Service，請注意下列必要的調整 `com.day.cq.mailer.DefaultMailService OSGI` 服務：

* SMTP伺服器主機名稱應該設定為$[環境：AEM_PROXY_HOST；預設=proxy.tunnel]
* SMTP伺服器連線埠應該設定為設定進階網路時，在API呼叫中使用的portForwards引數中設定的原始Proxy連線埠值。 例如，30465 （而非465）

SMTP伺服器連線埠應該設定為 `portDest` 設定進階網路時，在API呼叫中使用的portForwards引數中設定的值，以及 `portOrig` 值應為介於30000 - 30999所需範圍內的有意義值。 例如，如果SMTP伺服器連線埠是465，則應該使用連線埠30465做為 `portOrig` 值。

在此情況下，並假設需要啟用SSL，請在的 **Day CQ郵件服務OSGI** 服務：

* 設定 `smtp.port` 至 `30465`
* 設定 `smtp.ssl` 至 `true`

或者，如果目的地連線埠是587，則 `portOrig` 應該使用30587的值。 假設有停用SSL，Day CQ Mail Service OSGI服務的設定會：

* 設定 `smtp.port` 至 `30587`
* 設定 `smtp.ssl` 至 `false`

此 `smtp.starttls` 屬性會由AEMas a Cloud Service在執行階段自動設定為適當的值。 因此，如果 `smtp.ssl` 設為true， `smtp.startls` 會忽略。 如果 `smtp.ssl` 設為false `smtp.starttls` 設為true。 這與 `smtp.starttls` 在OSGI設定中設定的值。


您可以選擇使用OAuth2支援來設定郵件服務。 如需詳細資訊，請參閱 [郵件服務的OAuth2支援](/help/security/oauth2-support-for-mail-service.md).

### 舊版電子郵件設定 {#legacy-email-configuration}

在2021.9.0版之前，電子郵件是透過客戶支援要求所設定。 請注意下列必要的調整 `com.day.cq.mailer.DefaultMailService OSGI` 服務：

AEMas a Cloud Service需要透過連線埠465傳送郵件。 如果郵件伺服器不支援連線埠465，只要啟用TLS選項，就可以使用連線埠587。

如果已要求連線埠465：

* 設定 `smtp.port` 至 `465`
* 設定 `smtp.ssl` 至 `true`

如果已要求連線埠587，則：

* 設定 `smtp.port` 至 `587`
* 設定 `smtp.ssl` 至 `false`

此 `smtp.starttls` 屬性會由AEMas a Cloud Service在執行階段自動設定為適當的值。 因此，如果 `smtp.ssl` 設為true， `smtp.startls` 會忽略。 如果 `smtp.ssl` 設為false `smtp.starttls` 設為true。 這與 `smtp.starttls` 在OSGI設定中設定的值。

SMTP伺服器主機應該設定為郵件伺服器的主機。

## 避免大型多值屬性 {#avoid-large-mvps}

AEMas a Cloud Service下的Oak內容存放庫不應與過多的多值屬性(MVP)一起使用。 經驗法則是將MVP維持在1000以下。 然而，實際的效能取決於許多因素。

超過1000個之後，預設會記錄警告。 它們與以下內容類似。

```text
org.apache.jackrabbit.oak.jcr.session.NodeImpl Large multi valued property [/path/to/property] detected (1029 values). 
```

大型的MVP可能會導致錯誤，因為MongoDB檔案超過16 MB，導致類似於以下內容的錯誤。

```text
Caused by: com.mongodb.MongoWriteException: Resulting document after update is larger than 16777216
```

請參閱 [Apache Oak檔案](https://jackrabbit.apache.org/oak/docs/dos_and_donts.html#Large_Multi_Value_Property) 以取得更多詳細資料。

## [!DNL Assets] 開發指導方針與使用案例 {#use-cases-assets}

若要瞭解Assetsas a Cloud Service的開發使用案例、建議和參考資料，請參閱 [Assets開發人員參考資料](/help/assets/developer-reference-material-apis.md#assets-cloud-service-apis).
