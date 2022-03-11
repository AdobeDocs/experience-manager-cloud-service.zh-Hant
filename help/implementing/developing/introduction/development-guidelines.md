---
title: AEM as a Cloud Service 開發指導方針
description: AEM as a Cloud Service 開發指導方針
exl-id: 94cfdafb-5795-4e6a-8fd6-f36517b27364
source-git-commit: 68c9ae2c79fa3d328d31d8653db3ebc9bb9e575a
workflow-type: tm+mt
source-wordcount: '2288'
ht-degree: 2%

---

# AEM as a Cloud Service 開發指導方針 {#aem-as-a-cloud-service-development-guidelines}

>[!CONTEXTUALHELP]
>id="development_guidelines"
>title="AEM as a Cloud Service 開發指導方針"
>abstract="在此頁籤中，您可以查看as a Cloud Service中編碼的建議最佳AEM做法。 編碼可以與AMS或On-Prem部署有很大不同。"
>additional-url="https://video.tv.adobe.com/v/330555/" text="軟體包結構演示"

在as a Cloud ServiceAEM中運行的代碼必須知道它始終在群集中運行。 這表示執行中的例項永遠多於一個。代碼必須具有彈性，特別是當實例可能在任何時間點停止時。

在更新AEMas a Cloud Service時，將有舊代碼和新代碼並行運行的實例。 因此，舊代碼不能與新代碼建立的內容斷開，新代碼必須能夠處理舊內容。
<!--

>[!NOTE]
> All of the best practices mentioned here hold true for on-premise deployments of AEM, if not stated otherwise. An instance can always stop due to various reasons. However, with Skyline it is more likely to happen therefore an instance stopping is the rule not an exception.

-->

如果需要標識群集中的主伺服器，則可以使用Apache Sling Discovery API來檢測它。

## 記憶體中的狀態 {#state-in-memory}

狀態不能保留在記憶體中，但必須保留在儲存庫中。 否則，如果實例停止，則此狀態可能會丟失。

## 檔案系統上的狀態 {#state-on-the-filesystem}

實例的檔案系統不應用於AEMas a Cloud Service。 磁碟是短暫的，當實例被回收時，磁碟將被放置。 對與處理單個請求相關的臨時儲存使用檔案系統是可能的，但不應濫用於大型檔案。 這是因為它可能對資源使用配額產生負面影響，並會遇到磁碟限制。

例如，在不支援檔案系統使用的情況下，發佈層應確保需要保留的任何資料都被發送到外部服務以用於長期儲存。

## 觀察 {#observation}

類似的，由於非同步發生的一切，如對觀察事件採取行動，無法保證它在本地執行，因此必須謹慎使用。 對於JCR事件和Sling資源事件，都是如此。 在發生更改時，實例可以被取下，並被另一實例替換。 拓撲中當時處於活動狀態的其他實例將能夠對該事件做出反應。 但是，在這種情況下，這將不是一個地方性事件，而且，如果在事件發佈後進行領導人選舉，甚至可能沒有活躍的領導人。

## 後台任務和長時間運行的作業 {#background-tasks-and-long-running-jobs}

作為後台任務執行的代碼必須假定它正在運行的實例可以隨時關閉。 因此，代碼必須具有彈性，最重要的是可恢復。 這意味著，如果代碼重新執行，則不應從頭開始，而應從離開的位置開始。 雖然這不是此類代碼的新要求，但AEMas a Cloud Service而言，更有可能發生實例刪除。

為了將問題減到最小，應盡可能避免長時間運行的作業，並且應至少恢復這些作業。 要執行此類作業，請使用Sling Jobs，它至少有一次保證，因此如果中斷，將盡快重新執行。 但他們可能不應該從頭再來。 對於調度此類作業，最好使用 [斯林喬布斯](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing) 調度程式，因為這樣可確保至少一次執行。

由於無法保證執行，因此不應將Sling Commons調度程式用於調度。 只是更有可能會安排。

同樣，由於非同步發生的一切，如對觀察事件採取行動（即JCR事件或Sling資源事件），無法保證執行，因此必須謹慎使用。 對於當前的部AEM署，情況已經如此。

## 傳出HTTP連接 {#outgoing-http-connections}

強烈建議任何傳出HTTP連接設定合理的連接和讀取超時。 對於不應用這些超時的代碼，在AEMas a Cloud Service上運行的實AEM例將強制執行全局超時。 以下超時值是連接調用10秒，下列常用Java庫使用的連接讀取調用60秒：

Adobe建議使用 [Apache HttpComponents客戶端4.x庫](https://hc.apache.org/httpcomponents-client-ga/) 用於建立HTTP連接。

已知有效但可能需要自己提供依賴的替代方案有：

* [java.net.URL](https://docs.oracle.com/javase/7/docs/api/java/net/URL.html) 和/或 [java.net.URLConnection](https://docs.oracle.com/javase/7/docs/api/java/net/URLConnection.html) (提供者AEM)
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/) （不建議使用，因為它已過時，並被4.x版取代）
* [確定Http](https://square.github.io/okhttp/) (未由提供AEM)

## 無經典UI自定義 {#no-classic-ui-customizations}

AEMas a Cloud Service僅支援第三方客戶代碼的Touch UI。 經典UI不可用於自定義。

## 避免本機二進位檔案 {#avoid-native-binaries}

代碼將無法在運行時下載二進位檔案，也無法修改它們。 例如，它無法解包 `jar` 或 `tar` 的子菜單。

## 無流二進位文AEM件通過as a Cloud Service {#no-streaming-binaries}

應通過CDN訪問二進位檔案，CDN將在核心服務之外提供二進位AEM檔案。

例如，不使用 `asset.getOriginal().getStream()`，觸發將二進位檔案下載到AEM服務的臨時磁碟上。

## 無反向複製代理 {#no-reverse-replication-agents}

as a Cloud Service不支援從「發佈」到「作者」的反向復AEM制。 如果需要這樣的策略，您可以使用一個外部持久性儲存，該儲存在發佈實例的場之間共用，並且可能是作者群集。

## 可能需要移植轉發複製代理 {#forward-replication-agents}

內容通過pub-sub機制從「作者」複製到「發佈」。 不支援自定義複製代理。

## 監視和調試 {#monitoring-and-debugging}

### 記錄檔 {#logs}

對於本地開發，日誌條目將寫入 `/crx-quickstart/logs` 的子菜單。

在雲環境中，開發人員可以通過Cloud Manager下載日誌，或使用命令行工具跟蹤日誌。 <!-- See the [Cloud Manager documentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Note that custom logs are not supported and so all logs should be output to the error log. -->

**設定日誌級別**

要更改雲環境的日誌級別，應修改Sling Logging OSGI配置，然後完全重新部署。 由於這不是即時的，因此請小心在接收大量通信的生產環境中啟用詳細日誌。 將來，可能會有更快改變日誌級別的機制。

>[!NOTE]
>
>要執行下面列出的配置更改，您需要在本地開發環境中建立這些更改，然後將它們推送到AEMas a Cloud Service實例。 有關如何執行此操作的詳細資訊，請參見 [部署到AEMas a Cloud Service](/help/implementing/deploying/overview.md)。

**激活DEBUG日誌級別**

預設日誌級別為INFO，即DEBUG消息未記錄。 要激活DEBUG日誌級別，請將以下屬性更新為調試模式。

`/libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level`

例如，設定 `/apps/<example>/config/org.apache.sling.commons.log.LogManager.factory.config~<example>.cfg.json` 值。

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

不要將日誌保留在DEBUG日誌級別的時間超過必要時間，因為這樣會生成大量條目。

如果希望始終登錄，則可以使用基於AEM運行模式的OSGi配置目標為不同環境設定離散日誌級別 `DEBUG` 在開發過程中。 例如：

|環境 |按運行模式的OSGi配置位置 | `org.apache.sling.commons.log.level` 屬性值 | | - | - | - | |開發 | /apps/example/config/org.apache.sling.commons.log.LogManager.factory.config~example.cfg.json |調試 | |舞台 | /apps/example/config.stage/org.apache.sling.commons.log.LogManager.factory.config~example.cfg.json |警告 | |生產 | /apps/example/config.prod/org.apache.sling.commons.log.LogManager.factory.config~example.cfg.json |錯誤 |

調試檔案中的一行通常以DEBUG開頭，然後提供日誌級別、安裝程式操作和日誌消息。 例如：

```text
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

日誌級別如下：

| 0 | 錯誤 | 操作失敗，安裝程式無法繼續。 |
|---|---|---|
| 1 | 錯誤 | 操作失敗。 安裝將繼續，但CRX的一部分安裝不正確，無法正常工作。 |
| 2 | 警告 | 操作已成功，但遇到問題。 CRX可能正確工作，也可能不正確。 |
| 3 | 資訊 | 操作已成功。 |

### 線程轉儲 {#thread-dumps}

雲環境中的線程轉儲會持續收集，但此時無法以自助方式下載。 同時，如果調試問題AEM需要線程轉儲，請與支援部門聯繫，並指定確切的時間窗口。

## CRX/DE Lite和開發人員控制台 {#crxde-lite-and-developer-console}

### 地方發展 {#local-development}

對於本地開發，開發人員可以完全訪問CRXDE Lite(`/crx/de`)和AEMWeb控制台(`/system/console`)。

請注意，在本地開發（使用SDK）中， `/apps` 和 `/libs` 可以直接寫入，這與雲環境不同，雲環境中頂級資料夾是不可變的。

### AEMas a Cloud Service開發工具 {#aem-as-a-cloud-service-development-tools}

客戶可以在作者層的開發環境中訪問CRXDE lite ，但不能進行階段或生產。 不可變的儲存庫(`/libs`。 `/apps`)無法在運行時寫入，因此嘗試寫入將導致錯誤。

在開發人員控制台中，AEM提供一組用於調試as a Cloud Service開發人員環境的工具，用於開發、階段和生產環境。 可以通過調整「作者」或「發佈」服務URL來確定URL，如下所示：

`https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com`

作為快捷方式，可以使用以下Cloud Manager CLI命令根據下面描述的環境參數啟動開發人員控制台：

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

請參閱 [此頁](/help/release-notes/home.md) 的子菜單。

開發人員可以生成狀態資訊，並解決各種資源。

如下所示，可用狀態資訊包括捆綁包、元件、OSGI配置、橡樹索引、OSGI服務和Sling作業的狀態。

![開發控制台1](/help/implementing/developing/introduction/assets/devconsole1.png)

如下所示，開發人員可以解決包依賴項和Servlet:

![開發控制台2](/help/implementing/developing/introduction/assets/devconsole2.png)

![開發控制台3](/help/implementing/developing/introduction/assets/devconsole3.png)

對於調試，Developer控制台還具有指向「解釋查詢」工具的連結：

![開發控制台4](/help/implementing/developing/introduction/assets/devconsole4.png)

對於生產程式，對開發人員控制台的訪問由Admin Console中的「雲管理器 — 開發人員角色」定義，而對於沙盒程式，任何用戶都可以使用開發人員控制台，其產品配置檔案允許他們訪問AEMas a Cloud Service。 對於所有程式，狀態轉儲需要「Cloud Manager - Developer Role」，而且用戶還必須在作者和發佈服務的「用戶」或「管理員產品配置檔案」中定義，才能查看來自兩個服務的狀態轉儲資料。 有關設定用戶權限的詳細資訊，請參見 [Cloud Manager文檔](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html)。

### 試AEM運行和生產服務 {#aem-staging-and-production-service}

客戶將無法訪問用於過渡和生產環境的開發人員工具。

### 效能監控 {#performance-monitoring}

Adobe監控應用程式效能，並採取措施在出現惡化時予以解決。 此時，無法觀察應用程式度量。

## 發送電子郵件 {#sending-email}

以下各節介紹如何請求、配置和發送電子郵件。

>[!NOTE]
>
>郵件服務可以配置OAuth2支援。 有關詳細資訊，請參見 [郵件服務的OAuth2支援](/help/security/oauth2-support-for-mail-service.md)。

### 啟用出站電子郵件 {#enabling-outbound-email}

預設情況下，用於發送電子郵件的埠被禁用。 要激活埠，請配置 [先進網路](/help/security/configuring-advanced-networking.md)，確保為每個需要的環境設定 `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` 端點的埠轉發規則，將目標埠（例如465或587）映射到代理埠。

建議使用 `kind` 參數設定為 `flexiblePortEgress` 因為Adobe可以優化靈活的埠出口流量的效能。 如果需要唯一的出口IP地址，請選擇 `kind` 參數 `dedicatedEgressIp`。 如果出於其他原因已配置了VPN，則還可以使用該高級網路變體提供的唯一IP地址。

您必須通過郵件伺服器發送電子郵件，而不是直接通過電子郵件客戶端發送。 否則，電子郵件可能會被阻止。

### 發送電子郵件 {#sending-emails}

的 [第CQ天郵件服務OSGI服務](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service) 郵件必須發送到支援請求中指明的郵件伺服器，而不是直接發送給收件人。

### 設定 {#email-configuration}

中的電AEM子郵件應使用 [第CQ天郵件服務OSGi服務](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service)。

查看 [AEM 6.5文檔](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html) 有關配置電子郵件設定的詳細資訊。 對AEM於as a Cloud Service，請注意 `com.day.cq.mailer.DefaultMailService OSGI` 服務：

* SMTP伺服器主機名應設定為$[env:AEM_PROXY_HOST;default=proxy.tunnel]
* 配置高級網路時，SMTP伺服器埠應設定為API調用中使用的portForws參數中設定的原始代理埠的值。 例如，30465（而不是465）

如果已請求埠465，還建議：

* 集 `smtp.port` 至 `465`
* 集 `smtp.ssl` 至 `true`

如果已請求埠587:

* 集 `smtp.port` 至 `587`
* 集 `smtp.ssl` 至 `false`

的 `smtp.starttls` 在運行時，as a Cloud Service將AEM自動將屬性設定為適當的值。 因此，如果 `smtp.ssl` 設定為true, `smtp.startls` 忽略。 如果 `smtp.ssl` 設定為false, `smtp.starttls` 設定為true。 這不管 `smtp.starttls` 在OSGI配置中設定的值。


可以選擇為郵件服務配置OAuth2支援。 有關詳細資訊，請參見 [郵件服務的OAuth2支援](/help/security/oauth2-support-for-mail-service.md)。

### 舊式電子郵件配置 {#legacy-email-configuration}

在2021.9.0版之前，電子郵件是通過客戶支援請求配置的。 請注意以下對 `com.day.cq.mailer.DefaultMailService OSGI` 服務：

AEMas a Cloud Service需要通過埠465發送郵件。 如果郵件伺服器不支援埠465，則只要啟用了TLS選項，就可以使用埠587。

如果已請求埠465:

* 集 `smtp.port` 至 `465`
* 集 `smtp.ssl` 至 `true`

如果已請求埠587:

* 集 `smtp.port` 至 `587`
* 集 `smtp.ssl` 至 `false`

的 `smtp.starttls` 在運行時，as a Cloud Service將AEM自動將屬性設定為適當的值。 因此，如果 `smtp.ssl` 設定為true, `smtp.startls` 忽略。 如果 `smtp.ssl` 設定為false, `smtp.starttls` 設定為true。 這不管 `smtp.starttls` 在OSGI配置中設定的值。

SMTP伺服器主機應設定為郵件伺服器主機。


## [!DNL Assets] 開發指南和使用案例 {#use-cases-assets}

要瞭解資產as a Cloud Service的開發使用案例、建議和參考資料，請參閱 [資產的開發人員參考](/help/assets/developer-reference-material-apis.md#assets-cloud-service-apis)。
