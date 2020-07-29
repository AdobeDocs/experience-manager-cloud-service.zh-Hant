---
title: 記錄
description: 瞭解如何為中央記錄服務設定全域參數、個別服務的特定設定，或如何要求資料記錄。
translation-type: tm+mt
source-git-commit: 23f7b4b41abf9b909ec55a7f37b6b8e78c689b9b
workflow-type: tm+mt
source-wordcount: '1305'
ht-degree: 2%

---


# 記錄 {#logging}

AEM即雲端服務是客戶可加入自訂程式碼的平台，可為客戶群建立獨特的體驗。 有鑑於此，記錄是本端開發和雲端環境（尤其是雲端服務的Dev環境）上除錯和瞭解程式碼執行的重要功能。

AEM記錄和記錄檔層級會在設定檔中管理，這些設定檔會以Git儲存為AEM專案的一部分，並透過Cloud Manager部署為AEM專案的一部分。 以雲端服務身分登入AEM可分為兩個邏輯集：

* AEM記錄，在AEM應用程式層級執行記錄
* Apache HTTPD Web Server/Dispatcher日誌記錄，它在發佈層執行Web伺服器和Dispatcher的日誌記錄。

## AEM記錄 {#aem-loggin}

在AEM應用程式層級登入，由三個記錄檔處理：

1. AEM Java記錄檔，可為AEM應用程式轉譯Java記錄陳述式。
1. HTTP請求記錄檔，此記錄檔記錄有關HTTP請求及其由AEM提供之回應的資訊
1. HTTP存取記錄檔，記錄AEM所提供的摘要資訊和HTTP要求

請注意，從發佈層的Dispatcher快取或上游CDN所提供的HTTP請求不會反映在這些記錄檔中。

## AEM Java記錄 {#aem-java-logging}

AEM as a Cloud Service&#39;s提供Java記錄陳述式的存取權。 AEM應用程式開發人員應遵循一般Java記錄最佳實務，在下列記錄層級記錄有關執行自訂程式碼的相關陳述式：

<table>
<tr>
<td>
<b>AEM環境</b></td>
<td>
<b>記錄層級</b></td>
<td>
<b>說明</b></td>
<td>
<b>日誌語句可用性</b></td>
</tr>
<tr>
<td>
開發</td>
<td>
除錯</td>
<td>
說明應用程式中的情況。<br>
當DEBUG記錄處於活動狀態時，會記錄提供活動發生情況的清楚說明以及影響處理的任何關鍵參數的語句。</td>
<td>
<ul>
<li> 地方開發</li>
<li>開發</li>
</ul></td>
</tr>
<tr>
<td>
分段</td>
<td>
警告</td>
<td>
說明可能成為錯誤的條件。<br>
當WARN日誌記錄處於活動狀態時，只記錄指示接近子最優性的條件語句。</td>
<td>
<ul>
<li> 地方開發</li>
<li>開發</li>
<li>分段</li>
</ul></td>
</tr>
<tr>
<td>
生產</td>
<td>
錯誤</td>
<td>
說明指出失敗且需要解決的條件。<br>
當ERROR日誌記錄處於活動狀態時，僅記錄指示失敗的語句。 ERROR log語句表示應盡快解決的嚴重問題。</td>
<td>
<ul>
<li> 地方開發</li>
<li>開發</li>
<li>分段</li>
<li>生產</li>
</ul></td>
</tr>
</table>

雖然Java記錄支援其他數種記錄詳細程度層級，但AEM作為雲端服務建議使用上述三個層級。

AEM記錄檔層級是透過OSGi組態依環境類型設定，而OSGi組態會提交至Git，並透過Cloud Manager部署至AEM做為雲端服務。 因此，最好讓記錄檔陳述式與環境類型一致且廣為人知，以確保透過AEM提供的雲端服務可用的記錄檔位於最佳記錄檔層級，而不需透過更新的記錄檔層級設定重新部署應用程式。

### 日誌格式 {#log-format}

| 日期和時間 | AEM a Cloud Service Dode ID | 記錄層級 | 線程 | Java類 | 日誌消息 |
|---|---|---|---|---|---|
| 29.04.2020 21:50:13.398 | `[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]` | `*DEBUG*` | qtp2130572036-1472 | com.example.approval.workflow.impl.CustomApprovalWorkflow | `No specified approver, defaulting to [ Creative Approvers user group ]` |

**日誌輸出示例**

```
22.06.2020 18:33:30.120 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *ERROR* [qtp501076283-1809] io.prometheus.client.dropwizard.DropwizardExports Failed to get value from Gauge
22.06.2020 18:33:30.229 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [qtp501076283-1805] org.apache.sling.auth.core.impl.SlingAuthenticator getAnonymousResolver: Anonymous access not allowed by configuration - requesting credentials
22.06.2020 18:33:30.370 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] org.apache.sling.i18n.impl.JcrResourceBundle Finished loading 0 entries for 'en_US' (basename: <none>) in 4ms
22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [FelixLogListener] org.apache.sling.i18n Service [5126, [java.util.ResourceBundle]] ServiceEvent REGISTERED
22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *WARN* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] libs.granite.core.components.login.login$jsp j_reason param value 'unknown' cannot be mapped to a valid reason message: ignoring
```

### 配置記錄器 {#configuration-loggers}

AEM Java記錄檔已定義為OSGi設定，因此可使用執行模式資料夾將特定AEM定位為雲端服務環境。

透過Sling LogManager工廠的OSGi組態，為自訂Java封裝設定Java記錄。 支援兩種配置屬性：

| OSGi配置屬性 | 說明 |
|---|---|
| org.apache.sling.commons.log.names | 要收集其日誌語句的Java包。 |
| org.apache.sling.commons.log.level | 記錄Java封裝的記錄層級，由org.apache.sling.commons.log.names指定 |

變更其他LogManager OSGi組態屬性可能會導致AEM的雲端服務可用性問題。

以下是三個AEM的建議記錄設定範例(使用預留位置Java套件 `com.example`)，做為雲端服務環境類型。

### 開發 {#development}

/apps/my-app/config/org.apache.sling.commons.log.LogManager.factory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "debug"
}
```

### 分段 {#stage}

/apps/my-app/config.stage/org.apache.sling.commons.log.LogManager.factory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "warn"
}
```

### 生產 {#productiomn}

/apps/my-app/config.prod/org.apache.sling.commons.log.LogManager.factory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "error"
}
```

## AEM HTTP請求記錄 {#aem-http-request-logging}

AEM作為雲端服務的HTTP要求記錄功能，可依時間順序深入瞭解對AEM提出的HTTP要求及其HTTP回應。 此記錄檔有助於瞭解對AEM提出的HTTP要求，以及處理和回覆的順序。

瞭解此記錄檔的關鍵，是將HTTP請求和回應配對對應至其ID，由方括弧中的數值表示。 請注意，請求及其對應的回應通常會在記錄中插入其他HTTP請求和回應。

### 日誌格式 {#http-request-logging-format}

| 日期和時間 | 請求／回應對ID |  | HTTP 方法 | URL | 協定 | AEM做為雲端服務節點ID |
|---|---|---|---|---|---|---|
| 29/Apr/2020:19:14:21 +0000 | `[137]` | -> | 貼文 | /conf/global/settings/dam/adminui-extension/metadataprofile/ | HTTP/1.1 | `[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]` |

**範例記錄檔**

```
29/Apr/2020:19:14:21 +0000 [137] -> POST /conf/global/settings/dam/adminui-extension/metadataprofile/ HTTP/1.1 [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:22 +0000 [139] -> GET /mnt/overlay/dam/gui/content/processingprofilepage/metadataprofiles/editor.html/conf/global/settings/dam/adminui-extension/metadataprofile/main HTTP/1.1 [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:21 +0000 [137] <- 201 text/html 111ms [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:22 +0000 [139] <- 200 text/html;charset=utf-8 637ms [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
```

### 配置日誌 {#configuring-the-log}

AEM中的AEM HTTP請求記錄檔無法設定為雲端服務。

## AEM HTTP存取記錄 {#aem-http-access-logging}

AEM as Cloud Service HTTP存取記錄會依時間順序顯示HTTP請求。 每個記錄項目代表存取AEM的HTTP請求。

此記錄檔有助於快速瞭解AEM的HTTP要求，如果它們成功，請查看隨附的HTTP回應狀態程式碼，以及HTTP要求完成所需的時間。 此記錄檔也有助於依使用者篩選記錄檔項目，以除錯特定使用者的活動。

### 日誌格式 {#access-log-format}

**範例**

```
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css HTTP/1.1" 200 1141 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/customthumb/clientlibs.lc-60e4443805c37afa0c74b674b141f1df-lc.min.css HTTP/1.1" 200 809 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/metadataeditor/clientlibs/metadataeditor.lc-4a2226d8232f8b7ab27d24820b9ddd64-lc.min.js HTTP/1.1" 200 7965 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
```

<table>
<tbody>
<tr>
<td>AEM做為雲端服務節點ID</td>
<td>cm-p1235-e2644-aem-author-5955cb5b8-8kgr2</td>
</tr>
<tr>
<td>客戶機的IP地址</td>
<td>-</td>
</tr>
<tr>
<td>使用者</td>
<td>myuser@adobe.com</td>
</tr>
<tr>
<td>日期時間</td>
<td>30/Apr/2020:17:37:14 +0000</td>
</tr>
<tr>
<td>HTTP方法</td>
<td>取得</td>
</tr>
<tr>
<td>URL</td>
<td>/libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css</td>
</tr>
<tr>
<td>協定</td>
<td>HTTP/1.1</td>
</tr>
<tr>
<td>HTTP回應狀態</td>
<td>200</td>
</tr>
<tr>
<td>HTTP請求時間（以毫秒為單位）</td>
<td>1141</td>
</tr>
<tr>
<td>反向連結</td>
<td><code>"https://author-p1234-e4444.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/wknd/en/adventures/surf-camp-in-costa-rica/adobestock_266405335.jpeg&_charset_=utf8"</code></td>
</tr>
<tr>
<td>使用者代理</td>
<td>「Mozilla/5.0(Macintosh; Intel Mac OS X 10_15_4)AppleWebKit/537.36（KHTML，像Gecko）Chrome/81.0.4044.122 Safari/537.36英吋</td>
</tr>
</tbody>
</table>

### 配置HTTP訪問日誌 {#configuring-the-http-access-log}

AEM中的HTTP存取記錄檔無法設定為雲端服務。

## Apache Web Server和Dispatcher記錄 {#apache-web-server-and-dispatcher-logging}

AEM as a Cloud Service為Publish上的Apache Web Servers和分派程式層提供三個記錄檔：

* Apache HTTPD Web Server訪問日誌
* Apache HTTPD Web Server錯誤日誌
* Dispatcher log

請注意，這些記錄檔僅適用於「發佈」層。

在AEM應用程式收到HTTP請求之前，此組記錄檔會以雲端服務發佈層的形式，提供HTTP請求的見解。 請務必瞭解，最理想的情況是，對「發佈」層伺服器的大部分HTTP請求都是由Apache HTTPD Web Server和AEM Dispatcher快取的內容所提供，而且絕不會觸及AEM應用程式本身。 因此，AEM的Java、Request或Access記錄檔中沒有這些請求的記錄陳述式。

### Apache HTTPD Web Server訪問日誌 {#apache-httpd-web-server-access-log}

Apache HTTP Web Server訪問日誌為到達發佈層的Web伺服器/Dispatcher的每個HTTP請求提供語句。 請注意，從上游CDN所提供的請求不會反映在這些記錄檔中。

請參閱官方Apache檔案中的錯誤記錄 [檔格式資訊](https://httpd.apache.org/docs/2.4/logs.html#accesslog)。

**日誌格式**

<!--blank until prod build finishes-->

**範例**

```
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:41 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/favicons/favicon-32.png HTTP/1.1" 200 715 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:41 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/favicons/favicon-512.png HTTP/1.1" 200 9631 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:42 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/country-flags/US.svg HTTP/1.1" 200 810 "https://publish-p6902-e30226.adobeaemcloud.com/content/wknd/us/en.html" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
```

### 配置Apache HTTPD Web Server訪問日誌 {#configuring-the-apache-httpd-webs-server-access-log}

此記錄檔在AEM中無法設定為雲端服務。

## Apache HTTPD Web Server錯誤日誌 {#apache-httpd-web-server-error-log}

Apache HTTP Web Server錯誤日誌為發佈層的Web伺服器/Dispatcher中的每個錯誤提供語句。

請參閱官方Apache檔案中的錯誤記錄 [檔格式資訊](https://httpd.apache.org/docs/2.4/logs.html#errorlog)。

**日誌格式**

<!--placeholder-->

**範例**

```
Fri Jul 17 02:19:48.093820 2020 [mpm_worker:notice] [pid 1:tid 140272153361288] [cm-p1234-e30226-aem-publish-b86c6b466-b9427] AH00292: Apache/2.4.43 (Unix) Communique/4.3.4-20200424 mod_qos/11.63 configured -- resuming normal operations
Fri Jul 17 02:19:48.093874 2020 [core:notice] [pid 1:tid 140272153361288] [cm-p1234-e30226-aem-publish-b86c6b466-b9427] AH00094: Command line: 'httpd -d /etc/httpd -f /etc/httpd/conf/httpd.conf -D FOREGROUND -D ENVIRONMENT_PROD'
Fri Jul 17 02:29:34.517189 2020 [mpm_worker:notice] [pid 1:tid 140293638175624] [cm-p1234-e30226-aem-publish-b496f64bf-5vckp] AH00295: caught SIGTERM, shutting down
```

### 配置Apache HTTPD Web伺服器錯誤日誌 {#configuring-the-apache-httpd-web-server-error-log}

mod_rewrite日誌級別由檔案中的變數REWRITE_LOG_LEVEL定義 `conf.d/variables/global.var`。

它可以設定為「錯誤」、「警告」、「資訊」、「調試」和「跟蹤1 —— 跟蹤8」，預設值為「警告」。 若要對RewriteRules進行除錯，建議將記錄檔層級提升至Trace2。

如需詳 [細資訊，請參閱mod_rewrite模組檔案](https://httpd.apache.org/docs/current/mod/mod_rewrite.html#logging) 。

若要依環境設定記錄層級，請在global.var檔案中使用適當的條件分支，如下所述：

```
Define REWRITE_LOG_LEVEL Debug
  
<IfDefine ENVIRONMENT_STAGE>
  ...
  Define REWRITE_LOG_LEVEL Warn
  ...
</IfDefine>
<IfDefine ENVIRONMENT_PROD>
  ...
  Define REWRITE_LOG_LEVEL Error
  ...
</IfDefine>
```

## Dispatcher Log {#dispatcher-log}

**日誌格式**

