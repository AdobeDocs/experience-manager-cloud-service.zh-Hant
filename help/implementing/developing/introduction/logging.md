---
title: AEM as a Cloud Service的記錄
description: 瞭解如何使用AEM as a Cloud Service的記錄來設定中央記錄服務的全域引數、個別服務的特定設定，或如何請求資料記錄。
exl-id: 262939cc-05a5-41c9-86ef-68718d2cd6a9
feature: Log Files, Developing
role: Admin, Architect, Developer
source-git-commit: 5c32a088cf7e334ba6497a595b5176e5389ce9ed
workflow-type: tm+mt
source-wordcount: '2556'
ht-degree: 10%

---

# AEM as a Cloud Service的記錄 {#logging-for-aem-as-a-cloud-service}

AEM as a Cloud Service是客戶納入自訂程式碼的平台，可為他們的客戶群建立獨特的體驗。 有鑑於此，記錄服務對於在本機開發和雲端環境(尤其是AEM as a Cloud Service的開發環境)上除錯和瞭解程式碼執行至關重要。

AEM as a Cloud Service記錄設定和記錄層級是在組態檔中進行管理，這些組態檔會儲存為Git中AEM專案的一部分，並透過Cloud Manager部署為AEM專案的一部分。 登入AEM as a Cloud Service可分為三個邏輯集：

* AEM記錄，可在AEM應用程式層級執行記錄
* Apache HTTPD網頁伺服器/Dispatcher記錄，可在發佈層級上執行網頁伺服器和Dispatcher的記錄。
* CDN記錄（如其名稱所示）會在CDN上執行記錄。

## AEM記錄 {#aem-logging}

AEM應用程式層級的記錄由三個記錄檔處理：

1. AEM Java記錄，可呈現AEM應用程式的Java記錄陳述式。
1. HTTP請求記錄，會記錄有關AEM所服務的HTTP請求及其回應的資訊
1. HTTP存取記錄，會記錄由AEM提供的摘要資訊和HTTP請求

>[!NOTE]
>
>從發佈層的Dispatcher快取或上游CDN提供的HTTP請求不會反映在這些記錄中。

## AEM Java記錄 {#aem-java-logging}

AEM as a Cloud Service可讓您存取Java記錄陳述式。 AEM應用程式的開發人員應遵循一般Java記錄最佳實務，在下列記錄層級記錄有關自訂程式碼執行的相關陳述：

<table>
<tr>
<td>
<b>AEM環境</b></td>
<td>
<b>記錄層級</b></td>
<td>
<b>說明</b></td>
<td>
<b>記錄陳述式可用性</b></td>
</tr>
<tr>
<td>
開發</td>
<td>
偵錯</td>
<td>
說明應用程式中正在發生的事情。<br>
當DEBUG記錄作用中時，會記錄提供發生之活動以及影響處理的任何關鍵引數之清晰圖表的陳述式。</td>
<td>
<ul>
<li> 本機開發</li>
<li>開發</li>
</ul></td>
</tr>
<tr>
<td>
測試</td>
<td>
警告</td>
<td>
說明有可能變成錯誤的情況。<br>
當WARN記錄作用中時，只會記錄表示接近次最佳化的條件陳述式。</td>
<td>
<ul>
<li> 本機開發</li>
<li>開發</li>
<li>測試</li>
</ul></td>
</tr>
<tr>
<td>
生產</td>
<td>
錯誤</td>
<td>
說明指出失敗及需要解決的條件。<br>
當ERROR記錄作用中時，只會記錄表示失敗的陳述式。 錯誤記錄陳述式指出應儘快解決的嚴重問題。</td>
<td>
<ul>
<li> 本機開發</li>
<li>開發</li>
<li>測試</li>
<li>生產</li>
</ul></td>
</tr>
</table>

雖然Java記錄支援數個其他層級的記錄粒度，但AEM as a Cloud Service建議使用上述三個層級。

AEM記錄層級是透過OSGi設定根據環境型別設定，而這些設定又會提交至Git，並透過Cloud Manager部署至AEM as a Cloud Service。 因此，最好讓記錄陳述一致且對於環境型別而言是眾所周知的，以確保透過AEM as Cloud Service取得的記錄可在最佳記錄層級使用，而不需要以更新的記錄層級設定重新部署應用程式。

>[!NOTE]
>
>為確保有效監控客戶環境，請勿變更預設記錄層級。 此外，請勿修改預設的記錄格式。 記錄輸出必須維持導向預設檔案。如需特定准則，請參閱[下方](#configuration-loggers)一節。

**範例記錄輸出**

```
22.06.2020 18:33:30.120 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *ERROR* [qtp501076283-1809] io.prometheus.client.dropwizard.DropwizardExports Failed to get value from Gauge
22.06.2020 18:33:30.229 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [qtp501076283-1805] org.apache.sling.auth.core.impl.SlingAuthenticator getAnonymousResolver: Anonymous access not allowed by configuration - requesting credentials
22.06.2020 18:33:30.370 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] org.apache.sling.i18n.impl.JcrResourceBundle Finished loading 0 entries for 'en_US' (basename: <none>) in 4ms
22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [FelixLogListener] org.apache.sling.i18n Service [5126, [java.util.ResourceBundle]] ServiceEvent REGISTERED
22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *WARN* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] libs.granite.core.components.login.login$jsp j_reason param value 'unknown' cannot be mapped to a valid reason message: ignoring
```

**記錄格式**

<table>
<tbody>
<tr>
<td>日期和時間</td>
<td>29.04.2020 21:50:13.398</td>
</tr>
<tr>
<td>AEM as a Cloud Service節點ID</td>
<td>[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]</td>
</tr>
<tr>
<td>記錄層級</td>
<td>偵錯</td>
</tr>
<tr>
<td>執行緒</td>
<td>qtp2130572036-1472</td>
</tr>
<tr>
<td>Java類別</td>
<td>com.example.approval.workflow.impl.CustomApprovalWorkflow</td>
</tr>
<tr>
<td>記錄訊息</td>
<td>未指定核准者，預設為[ Creative核准者使用者群組]</td>
</tr>
</tbody>
</table>

### 設定記錄器 {#configuration-loggers}

AEM Java記錄檔會定義為OSGi設定，因此可使用執行模式資料夾鎖定特定AEM as a Cloud Service環境。

透過Sling LogManager Factory的OSGi設定為自訂Java套件設定Java記錄。 有三個支援的組態屬性：

| OSGi設定屬性 | 說明 |
|---|---|
| `org.apache.sling.commons.log.names` | 要收集其記錄陳述式的Java套件。 |
| `org.apache.sling.commons.log.level` | `org.apache.sling.commons.log.names`所指定的Java封裝記錄層級 |

變更其他LogManager OSGi設定屬性可能會導致AEM as a Cloud Service中的可用性問題。

如上一節所述，為確保有效監控客戶環境：
* AEM的預設記錄設定（Apache Sling記錄設定）的記錄層級不能從其預設值「INFO」修改。
* 對於個別產品程式碼套件（使用「Apache Sling記錄記錄器設定」OSGi設定處理站的執行個體），將記錄層級設定為DEBUG是可以接受的，但請謹慎使用，以防止效能降低，並在不再需要時還原為INFO。
* 調整客戶開發程式碼的記錄層級是可接受的。
* 所有記錄(AEM產品程式碼和客戶開發的程式碼)都必須保持預設的記錄格式。
* 記錄輸出必須保持導向到預設檔案&quot;logs/error.log&quot;。

為此，不得對以下OSGi屬性進行變更：
* **Apache Sling 記錄設定** (PID: `org.apache.sling.commons.log.LogManager`)：*所有屬性*
* **Apache Sling 記錄記錄器設定** (工廠 PID: `org.apache.sling.commons.log.LogManager.factory.config`)：
   * `org.apache.sling.commons.log.file`
   * `org.apache.sling.commons.log.pattern`

以下是三種AEM as a Cloud Service環境型別的建議記錄設定範例（使用`com.example`的預留位置Java套件）。

### 開發 {#development}

/apps/my-app/config/org.apache.sling.commons.log.LogManager.factory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "debug"
    "org.apache.sling.commons.log.file": "logs/error.log"
}
```

### 測試 {#stage}

/apps/my-app/config.stage/org.apache.sling.commons.log.LogManager.factory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "warn"
    "org.apache.sling.commons.log.file": "logs/error.log"
}
```

### 生產 {#productiomn}

/apps/my-app/config.prod/org.apache.sling.commons.log.LogManager.factory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "error"
    "org.apache.sling.commons.log.file": "logs/error.log"
}
```

## AEM HTTP要求記錄 {#aem-http-request-logging}

AEM as a Cloud Service的HTTP請求記錄可讓您依時間順序深入分析向AEM提出的HTTP請求及其HTTP回應。 此記錄有助於瞭解向AEM發出的HTTP請求，以及這些請求被處理和回應的順序。

瞭解此記錄的關鍵在於透過其ID （以方括弧中的數值表示）對應HTTP請求和回應配對。 通常請求及其對應的回應會在記錄中於其他HTTP請求和回應之間插入。

**範例記錄檔**

```
29/Apr/2020:19:14:21 +0000 [137] > POST /conf/global/settings/dam/adminui-extension/metadataprofile/ HTTP/1.1 [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:22 +0000 [139] > GET /mnt/overlay/dam/gui/content/processingprofilepage/metadataprofiles/editor.html/conf/global/settings/dam/adminui-extension/metadataprofile/main HTTP/1.1 [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:21 +0000 [137] <- 201 text/html 111ms [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:22 +0000 [139] <- 200 text/html;charset=utf-8 637ms [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
```

**記錄格式**

<table>
<tbody>
<tr>
<td>日期和時間</td>
<td>2020年4月29日:19:14:21 +0000</td>
</tr>
<tr>
<td>請求/回應配對ID</td>
<td><code>[137]</code></td>
</tr>
<tr>
<td>HTTP 方法</td>
<td>POST</td>
</tr>
<tr>
<td>URL</td>
<td>/conf/global/settings/dam/adminui-extension/metadataprofile/</td>
</tr>
<tr>
<td>通訊協定</td>
<td>HTTP/1.1
</td>
</tr>
<tr>
<td>AEM as a Cloud Service節點ID</td>
<td>[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]</td>
</tr>
</tbody>
</table>

### 設定記錄 {#configuring-the-log}

無法在AEM as a Cloud Service中設定AEM HTTP請求記錄檔。

## AEM HTTP存取記錄 {#aem-http-access-logging}

AEM as Cloud Service HTTP存取記錄會依時間順序顯示HTTP請求。 每個記錄專案代表存取AEM的HTTP要求。

此記錄有助於快速瞭解向AEM發出的HTTP要求（如果這些要求透過檢視隨附的HTTP回應狀態代碼成功）以及HTTP要求完成所需的時間。 此記錄檔也可依使用者篩選記錄檔專案，有助於對特定使用者的活動進行除錯。

**範例記錄輸出**

```
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css HTTP/1.1" 200 1141 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/customthumb/clientlibs.lc-60e4443805c37afa0c74b674b141f1df-lc.min.css HTTP/1.1" 200 809 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/metadataeditor/clientlibs/metadataeditor.lc-4a2226d8232f8b7ab27d24820b9ddd64-lc.min.js HTTP/1.1" 200 7965 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
```

| AEM as a Cloud Service節點ID | cm-p1235-e2644-aem-author-59555cb5b8-8kgr2 |
|---|---|
| 使用者端的IP位址 | - |
| 使用者 | myuser@adobe.com |
| 日期和時間 | 2020年4月30日:17:37:14 +0000 |
| HTTP方法 | GET |
| URL | `/libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css` |
| 通訊協定 | HTTP/1.1 |
| HTTP回應狀態 | 200 |
| 回應內文的大小（以位元組為單位） | 1141 |
| 反向連結 | `"https://author-p1234-e4444.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/wknd/en/adventures/surf-camp-in-costa-rica/adobestock_266405335.jpeg&_charset_=utf8"` |
| 使用者代理 | `"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"` |

### 設定HTTP存取記錄檔 {#configuring-the-http-access-log}

無法在AEM as a Cloud Service中設定HTTP存取記錄檔。

## Apache Web Server和Dispatcher記錄 {#apache-web-server-and-dispatcher-logging}

AEM as a Cloud Service為發佈上的Apache Web Server和Dispatcher層提供三個記錄：

* Apache HTTPD Web Server存取記錄
* Apache HTTPD Web Server錯誤記錄
* Dispatcher記錄

這些記錄檔僅適用於發佈階層。

這組記錄提供存取AEM應用程式之前，AEM as a Cloud Service Publish層級的HTTP請求深入分析。 請務必瞭解這點，因為理想情況下，對發佈層級伺服器的大部分HTTP請求都是由Apache HTTPD Web Server和AEM Dispatcher快取的內容所提供，而且絕對不會連線至AEM應用程式本身。 因此，AEM的Java、請求或存取記錄檔中沒有這些請求的記錄陳述式。

### Apache HTTPD Web Server存取記錄檔 {#apache-httpd-web-server-access-log}

Apache HTTP Web Server存取記錄檔會針對到達發佈層級之Web伺服器/Dispatcher的每個HTTP要求提供陳述式。 從上游CDN提供的請求不會反映在這些記錄中。

請參閱[官方apache檔案](https://httpd.apache.org/docs/2.4/logs.html#accesslog)中有關錯誤記錄檔格式的資訊。

**範例記錄輸出**

```
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:41 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/favicons/favicon-32.png HTTP/1.1" 200 715 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:41 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/favicons/favicon-512.png HTTP/1.1" 200 9631 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:42 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/country-flags/US.svg HTTP/1.1" 200 810 "https://publish-p6902-e30226.adobeaemcloud.com/content/wknd/us/en.html" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
```

**記錄格式**

<table>
<tbody>
<tr>
<td>AEM as a Cloud Service節點ID</td>
<td>cm-p1234-e26813-aem-publish-5c787687c-lqlxr</td>
</tr>
<tr>
<td>使用者端的IP位址</td>
<td>-</td>
</tr>
<tr>
<td>使用者</td>
<td>-</td>
</tr>
<tr>
<td>日期和時間</td>
<td>2020年5月1日:00:09:46 +0000</td>
</tr>
<tr>
<td>HTTP 方法</td>
<td>GET</td>
</tr>
<tr>
<td>URL</td>
<td>/content/example.html</td>
</tr>
<tr>
<td>通訊協定</td>
<td>HTTP/1.1</td>
</tr>
<tr>
<td>HTTP回應狀態</td>
<td>200</td>
</tr>
<tr>
<td>大小</td>
<td>310</td>
</tr>
<tr>
<td>推薦者</td>
<td>-</td>
</tr>
<tr>
<td>使用者代理</td>
<td>「Mozilla/5.0 (Macintosh；Intel Mac OS X 10_15_4) AppleWebKit/537.36 （KHTML，如Gecko） Chrome/81.0.4044.122 Safari/537.36」</td>
</tr>
</tbody>
</table>

### 設定Apache HTTPD Web Server存取記錄檔 {#configuring-the-apache-httpd-webs-server-access-log}

此記錄檔無法在AEM as a Cloud Service中設定。

## Apache HTTPD Web Server錯誤記錄 {#apache-httpd-web-server-error-log}

Apache HTTP Web Server錯誤記錄針對發佈層級的Web伺服器/Dispatcher中的每個錯誤提供陳述式。

請參閱[官方apache檔案](https://httpd.apache.org/docs/2.4/logs.html#errorlog)中有關錯誤記錄檔格式的資訊。

**範例記錄輸出**

```
Fri Jul 17 02:19:48.093820 2020 [mpm_worker:notice] [pid 1:tid 140272153361288] [cm-p1234-e30226-aem-publish-b86c6b466-b9427] AH00292: Apache/2.4.43 (Unix) Communique/4.3.4-20200424 mod_qos/11.63 configured -- resuming normal operations
Fri Jul 17 02:19:48.093874 2020 [core:notice] [pid 1:tid 140272153361288] [cm-p1234-e30226-aem-publish-b86c6b466-b9427] AH00094: Command line: 'httpd -d /etc/httpd -f /etc/httpd/conf/httpd.conf -D FOREGROUND -D ENVIRONMENT_PROD'
Fri Jul 17 02:29:34.517189 2020 [mpm_worker:notice] [pid 1:tid 140293638175624] [cm-p1234-e30226-aem-publish-b496f64bf-5vckp] AH00295: caught SIGTERM, shutting down
```

**記錄格式**

<table>
<tbody>
<tr>
<td>日期和時間</td>
<td>2020年7月17日星期五02:16:42.608913</td>
</tr>
<tr>
<td>事件層級</td>
<td>[mpm_worker：notice]</td>
</tr>
<tr>
<td>處理序ID</td>
<td>[pid 1：tid 140715149343624]</td>
</tr>
<tr>
<td>Pod名稱</td>
<td>[cm-p1234-e56789-aem-publish-b86c6b466-qpfvp]</td>
</tr>
<tr>
<td>訊息</td>
<td>AH00094：命令列： 'httpd -d /etc/httpd -f /etc/httpd/conf/httpd.conf -D FOREGROUND -D </td>
</tr>
</tbody>
</table>

### 設定Apache HTTPD Web Server錯誤記錄 {#configuring-the-apache-httpd-web-server-error-log}

mod_rewrite記錄層級是由檔案`conf.d/variables/global.var`中的變數REWRITE_LOG_LEVEL所定義。

可將其設為error、warn、info、debug和trace1 - trace8，預設值為warn。 若要偵錯RewriteRules，建議將記錄層級提升為trace2。 建議您使用[Dispatcher SDK](../../dispatcher/validation-debug.md)來偵錯重新寫入規則。 AEM as a Cloud Service的最大記錄層級為`debug`。 因此，目前不可能有效地在雲端中偵錯重寫規則。

如需詳細資訊，請參閱[mod_rewrite模組檔案](https://httpd.apache.org/docs/current/mod/mod_rewrite.html#logging)。

若要為每個環境設定記錄層級，請在global.var檔案中使用適當的條件分支，如下所述：

```
Define REWRITE_LOG_LEVEL debug

<IfDefine ENVIRONMENT_STAGE>
  ...
  Define REWRITE_LOG_LEVEL warn
  ...
</IfDefine>
<IfDefine ENVIRONMENT_PROD>
  ...
  Define REWRITE_LOG_LEVEL error
  ...
</IfDefine>
```

## Dispatcher記錄檔 {#dispatcher-log}

**範例**

```
[17/Jul/2020:23:48:06 +0000] [I] [cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr] "GET /content/wknd/us/en/adventures.html" - 475ms [publishfarm/0] [action miss] "publish-p12904-e25628.adobeaemcloud.com"
[17/Jul/2020:23:48:07 +0000] [I] [cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr] "GET /content/wknd/us/en/adventures/climbing-new-zealand/_jcr_content/root/responsivegrid/carousel/item_1571266094599.coreimg.jpeg/1473680817282/sport-climbing.jpeg" 302 10ms [publishfarm/0] [action none] "publish-p12904-e25628.adobeaemcloud.com"
[17/Jul/2020:23:48:07 +0000] [I] [cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr] "GET /content/wknd/us/en/adventures/ski-touring-mont-blanc/_jcr_content/root/responsivegrid/carousel/item_1571168419252.coreimg.jpeg/1572047288089/adobestock-238230356.jpeg" 302 11ms [publishfarm/0] [action none] "publish-p12904-e25628.adobeaemcloud.com"
```

**記錄格式**

<table>
<tbody>
<tr>
<td>日期和時間</td>
<td>[2020年7月17日:23:48:16 +0000]</td>
</tr>
<tr>
<td>Pod名稱</td>
<td>[cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr]</td>
</tr>
<tr>
<td>通訊協定</td>
<td>GET</td>
</tr>
<tr>
<td>URL</td>
<td>/content/experience-fragments/wknd/language-masters/en/contributors/sofia-sjoeberg/master/_jcr_content/root/responsivegrid/image.coreimg.100.500.jpeg/1572236359031/ayo-ogunseinde-237739.jpeg</td>
</tr>
<tr>
<td>Dispatcher回應狀態代碼</td>
<td>/content/experience-fragments/wknd/language-masters/en/contributors/sofia-sjoeberg/master/_jcr_content/root/responsivegrid/image.coreimg.100.500.jpeg/1572236359031/ayo-ogunseinde-237739.jpeg</td>
</tr>
<tr>
<td>持續時間</td>
<td>1949毫秒</td>
</tr>
<tr>
<td>陣列</td>
<td>[publishfarm/0]</td>
</tr>
<tr>
<td>快取狀態</td>
<td>[動作未命中]</td>
</tr>
<tr>
<td>主機</td>
<td>"publish-p12904-e25628.adobeaemcloud.com"</td>
</tr>
</tbody>
</table>

### 設定Dispatcher錯誤記錄檔 {#configuring-the-dispatcher-error-log}

Dispatcher記錄層級是由檔案`conf.d/variables/global.var`中的變數DISP_LOG_LEVEL所定義。

它可以設定為error、warn、info、debug和trace1，預設值為warn。

雖然Dispatcher記錄支援數個其他層級的記錄粒度，但AEM as a Cloud Service建議使用下列所述的層級。

若要為每個環境設定記錄層級，請在`global.var`檔案中使用適當的條件分支，如下所述：

```
Define DISP_LOG_LEVEL debug

<IfDefine ENVIRONMENT_STAGE>
  ...
  Define DISP_LOG_LEVEL warn
  ...
</IfDefine>
<IfDefine ENVIRONMENT_PROD>
  ...
  Define DISP_LOG_LEVEL error
  ...
</IfDefine>
```

>[!NOTE]
>
>針對AEM as a Cloud Service環境，除錯是最高詳細程度等級。 不支援追蹤記錄層級，因此您在雲端環境中工作時應該避免進行設定。

## CDN記錄 {#cdn-log}

AEM as a Cloud Service提供對CDN記錄的存取權，這些記錄可用於快取命中比率最佳化等使用案例。 無法自訂CDN記錄格式，且沒有將其設定為不同模式（例如info、warn或error）的概念。

**範例**

```
{
"timestamp": "2023-05-26T09:20:01+0000",
"ttfb": 19,
"cli_ip": "147.160.230.112",
"cli_country": "CH",
"rid": "974e67f6",
"req_ua": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0.3 Safari/605.1.15",
"host": "example.com",
"url": "/content/hello.png",
"method": "GET",
"res_ctype": "image/png",
"cache": "PASS",
"status": 200,
"res_age": 0,
"pop": "PAR",
"rules": "match=Enable-SQL-Injection-and-XSS-waf-rules-globally,waf=SQLI,action=blocked"
}
```

**記錄格式**

CDN記錄與其他記錄不同，因為它會遵循JSON格式。

| **欄位名稱** | **說明** |
|---|---|
| *timestamp* | TLS 終止後要求開始的時間 |
| *ttfb* | *首位元組時間 (Time To First Byte)* 的縮寫。發出要求開始到回應內文開始串流的時間之間的時間間隔。 |
| *cli_ip* | 用戶端 IP 位址。 |
| *cli_country* | 雙字母 [ISO 3166-1](https://zh.wikipedia.org/wiki/tw/ISO_3166-1) 用戶端國家/地區的 alpha-2 國家/地區代碼。 |
| *rid* | 用於唯一識別要求的要求標頭的值。 |
| *req_ua* | 負責發出特定 HTTP 要求的使用者代理程式。 |
| *主機* | 發送要求的目標機構。 |
| *url* | 包括查詢參數的完整路徑。 |
| *方法* | 用戶端傳送的 HTTP 方法，例如「GET」或「POST」。 |
| *res_ctype* | 此內容類型用於指明資源的原始媒體類型。 |
| *cache* | 快取的狀態。可能的值包括 HIT、MISS 或 PASS |
| *狀態* | 作為整數值的 HTTP 狀態代碼。 |
| *res_age* | 回應已經 (在所有的節點) 快取的時間量 (以秒為單位)。 |
| *pop* | CDN 快取伺服器的資料中心。 |
| *rules* | 任何相符的[流量篩選規則](/help/security/traffic-filter-rules-including-waf.md)和WAF旗標的名稱，也表示相符是否造成封鎖。 若沒有相符的規則，則為空白。 |

您可以使用[要求/回應轉換](/help/implementing/dispatcher/cdn-configuring-traffic.md#logproperty)，以您自己的屬性擴充CDN記錄。

## 如何存取記錄檔 {#how-to-access-logs}

### 雲端環境 {#cloud-environments}

雲端服務的AEM as a Cloud Service記錄檔可透過以下方式存取：透過Cloud Manager介面下載，或使用Adobe I/O命令列介面在命令列追蹤記錄檔。 如需詳細資訊，請參閱[Cloud Manager記錄檔案](/help/implementing/cloud-manager/manage-logs.md)。

### 其他發佈區域的記錄 {#logs-for-additional-publish-regions}

如果針對特定環境啟用了其他發佈區域，則可以從Cloud Manager下載每個區域的記錄，如上所述。

其他發佈區域的AEM記錄和Dispatcher記錄將在環境ID之後的前3個字母中指定區域，以下範例中的&#x200B;**nld2**&#x200B;即代表位於荷蘭的其他AEM發佈執行個體：

```
cm-p7613-e12700-nld2-aem-publish-bcbb77549-5qmmt 127.0.0.1 - 07/Nov/2023:23:57:11 +0000 "HEAD /libs/granite/security/currentuser.json HTTP/1.1" 200 - "-" "Java/11.0.19"
```

### 本機 SDK {#local-sdk}

AEM as a Cloud Service SDK提供記錄檔以支援本機開發。

AEM記錄位於資料夾`crx-quickstart/logs`中，您可在此檢視下列記錄：

* AEM Java記錄檔： `error.log`
* AEM HTTP要求記錄： `request.log`
* AEM HTTP存取記錄檔： `access.log`

Apache層記錄檔（包括Dispatcher）位於儲存Dispatcher的Docker容器中。 如需如何啟動Dispatcher的詳細資訊，請參閱[Dispatcher檔案](/help/implementing/dispatcher/disp-overview.md)。

擷取記錄檔：

1. 在命令列中，輸入`docker ps`以列出您的容器
1. 若要登入容器，請輸入&quot;`docker exec -it <container> /bin/sh`&quot;，其中`<container>`是上一步驟的Dispatcher容器ID
1. 瀏覽至`/mnt/var/www/html`下的快取根目錄
1. 記錄檔在`/etc/httpd/logs`之下
1. 檢查記錄：這些記錄可在XYZ資料夾下存取，您可在此檢視以下記錄：
   * Apache HTTPD Web伺服器存取記錄檔 — `httpd_access.log`
   * Apache HTTPD Web伺服器錯誤記錄檔 — `httpd_error.log`
   * Dispatcher記錄 — `dispatcher.log`

記錄也直接列印到終端機輸出。 大多數情況下，這些記錄應為DEBUG，可通過在執行Docker時作為引數傳入Debug級別來完成。 例如：

`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`

## 偵錯生產和中繼 {#debugging-production-and-stage}

在例外情況下，記錄層級需要變更以在中繼或生產環境中的更精細精細記錄。

雖然這是可能的，但需要變更Git中設定檔案的記錄層級（從Warn和Error到Debug），並執行部署至AEM as a Cloud Service以向環境註冊這些設定變更。

根據Debug所寫入的流量和記錄陳述式數量，這可能會導致對環境的效能造成不良影響，因此，建議對「中繼」和「生產」偵錯層級的變更如下：

* 謹慎行事，並且只在絕對必要時進行
* 已恢復至適當層級，並儘快重新部署

## 記錄轉送 {#log-forwarding}

雖然可從Cloud Manager下載記錄檔，但有些組織認為將這些記錄檔轉送至偏好的記錄目的地較為有利。 AEM支援將記錄串流至以下目的地：

* Azure Blob儲存體
* Datadog
* HTTPD
* Elasticsearch （和OpenSearch）
* Splunk

如需有關如何設定此功能的詳細資訊，請參閱[記錄轉送文章](/help/implementing/developing/introduction/log-forwarding.md)。

>[!NOTE]
>
>不支援沙箱計畫環境的記錄檔轉送。
