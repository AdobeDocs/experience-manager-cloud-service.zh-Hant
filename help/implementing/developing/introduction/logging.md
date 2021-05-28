---
title: 登入AEM作為Cloud Service
description: 了解如何為中央記錄服務設定全域參數、個別服務的特定設定，或如何以Cloud Service形式在AEM中要求資料記錄。
exl-id: 262939cc-05a5-41c9-86ef-68718d2cd6a9
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '2330'
ht-degree: 2%

---

# 登入AEM作為Cloud Service{#logging-for-aem-as-a-cloud-service}

AEM as aCloud Service是客戶納入自訂程式碼的平台，可為其客戶群建立獨特體驗。 有鑑於此，記錄是重要功能，可針對本機開發和雲端環境(尤其是AEM as aCloud Service的開發環境)進行除錯和了解程式碼執行情形。

AEM記錄和記錄層級可在設定檔中進行管理，這些設定檔儲存為Git中AEM專案的一部分，並透過Cloud Manager部署為AEM專案的一部分。 以Cloud Service身分登入AEM可劃分為兩個邏輯集：

* AEM記錄，在AEM應用程式層級執行記錄
* Apache HTTPD Web Server/Dispatcher記錄，可在「發佈」層級上執行Web伺服器和Dispatcher的記錄。

## AEM記錄{#aem-loggin}

在AEM應用程式層級記錄，由三個記錄檔處理：

1. AEM Java記錄檔，可轉譯AEM應用程式的Java記錄陳述式。
1. HTTP要求記錄檔，記錄AEM所提供HTTP要求及其回應的相關資訊
1. HTTP存取記錄，記錄由AEM提供的摘要資訊和HTTP要求

>[!NOTE]
>
>從發佈層級的Dispatcher快取或上游CDN提供的HTTP要求不會反映在這些記錄中。

## AEM Java記錄{#aem-java-logging}

AEM as aCloud Service可存取Java記錄陳述式。 AEM應用程式的開發人員應遵循一般Java記錄最佳實務，在下列記錄層級記錄與自訂程式碼執行相關的陳述式：

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
說明應用程式中發生的情況。<br>
當DEBUG記錄處於作用中狀態時，會記錄提供發生活動之清楚畫面的陳述式，以及任何影響處理的關鍵參數。</td>
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
當ERROR日誌記錄處於活動狀態時，僅記錄指示失敗的語句。錯誤日誌語句表示應盡快解決的嚴重問題。</td>
<td>
<ul>
<li> 地方開發</li>
<li>開發</li>
<li>分段</li>
<li>生產</li>
</ul></td>
</tr>
</table>

雖然Java記錄支援其他數種記錄粒度層級，但AEM as aCloud Service建議使用上述三個層級。

AEM記錄層級是透過OSGi設定，依環境類型而設定，而OSGi設定則會提交至Git，並透過Cloud Manager部署至AEM作為Cloud Service。 因此，最好保持日誌陳述式一致且為環境類型所知，以確保通過AEM作為Cloud Service的可用日誌在最佳日誌級別可用，而不需要使用更新的日誌級別配置重新部署應用程式。

**日誌輸出示例**

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
<td>日期時間</td>
<td>29.04.2020 21:50:13.398</td>
</tr>
<tr>
<td>AEM作為Cloud Service節點ID</td>
<td>[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]</td>
</tr>
<tr>
<td>記錄層級</td>
<td>除錯</td>
</tr>
<tr>
<td>線程</td>
<td>qtp2130572036-1472</td>
</tr>
<tr>
<td>Java類</td>
<td>com.example.approval.workflow.impl.CustomApprovalWorkflow</td>
</tr>
<tr>
<td>記錄訊息</td>
<td>沒有指定的批准者，預設為[創作批准者用戶組]</td>
</tr>
</tbody>
</table>

### 配置記錄器{#configuration-loggers}

AEM Java記錄檔定義為OSGi設定，因此可使用執行模式資料夾將特定AEM定位為Cloud Service環境。

透過Sling LogManager工廠的OSGi設定，為自訂Java套件設定Java記錄。 支援兩種配置屬性：

| OSGi配置屬性 | 說明 |
|---|---|
| org.apache.sling.commons.log.names | 要收集日誌陳述式的Java包。 |
| org.apache.sling.commons.log.level | 記錄Java套件的記錄層級，由org.apache.sling.commons.log.names指定 |

更改其他LogManager OSGi配置屬性可能會在AEM as aCloud Service中導致可用性問題。

以下是三個AEM作為Cloud Service環境類型時建議的記錄設定範例（使用`com.example`的預留位置Java套件）。

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

## AEM HTTP要求記錄{#aem-http-request-logging}

AEM as aCloud Service的HTTP要求記錄功能可依時序深入分析向AEM提出的HTTP要求及其HTTP回應。 此記錄有助於了解對AEM提出的HTTP要求，以及處理和回應的順序。

了解此記錄檔的關鍵，是透過其ID對應HTTP要求和回應配對，以方括弧中的數值表示。 請注意，在記錄中，要求及其對應回應之間通常會插入其他HTTP要求和回應。

**記錄範例**

```
29/Apr/2020:19:14:21 +0000 [137] -> POST /conf/global/settings/dam/adminui-extension/metadataprofile/ HTTP/1.1 [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:22 +0000 [139] -> GET /mnt/overlay/dam/gui/content/processingprofilepage/metadataprofiles/editor.html/conf/global/settings/dam/adminui-extension/metadataprofile/main HTTP/1.1 [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:21 +0000 [137] <- 201 text/html 111ms [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:22 +0000 [139] <- 200 text/html;charset=utf-8 637ms [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
```

**記錄格式**

<table>
<tbody>
<tr>
<td>日期時間</td>
<td>2000年4月29日2020:19:14:21 +000</td>
</tr>
<tr>
<td>請求/回應組ID</td>
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
<td>AEM作為Cloud Service節點ID</td>
<td>[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]</td>
</tr>
</tbody>
</table>

### 配置日誌{#configuring-the-log}

AEM HTTP要求記錄檔無法在AEM中設定為Cloud Service。

## AEM HTTP存取記錄{#aem-http-access-logging}

AEM asCloud ServiceHTTP存取記錄會依時序顯示HTTP要求。 每個記錄項目代表存取AEM的HTTP要求。

此記錄有助於快速了解對AEM提出的HTTP要求、查看隨附的HTTP回應狀態代碼是否成功，以及HTTP要求完成所需的時間。 此記錄檔也可協助您依使用者篩選記錄項目，以偵錯特定使用者的活動。

**日誌輸出示例**

```
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css HTTP/1.1" 200 1141 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/customthumb/clientlibs.lc-60e4443805c37afa0c74b674b141f1df-lc.min.css HTTP/1.1" 200 809 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/metadataeditor/clientlibs/metadataeditor.lc-4a2226d8232f8b7ab27d24820b9ddd64-lc.min.js HTTP/1.1" 200 7965 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
```

**記錄格式**

<table>
<tbody>
<tr>
<td>AEM作為Cloud Service節點ID</td>
<td>cm-p1235-e2644-aem-author-59555cb5b8-8kgr2</td>
</tr>
<tr>
<td>客戶端的IP地址</td>
<td>-</td>
</tr>
<tr>
<td>使用者</td>
<td>myuser@adobe.com</td>
</tr>
<tr>
<td>日期時間</td>
<td>2000年4月30日2020:17:37:14 +000</td>
</tr>
<tr>
<td>HTTP方法</td>
<td>GET</td>
</tr>
<tr>
<td>URL</td>
<td>/libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css</td>
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
<td>HTTP要求時間（毫秒）</td>
<td>1141</td>
</tr>
<tr>
<td>反向連結</td>
<td><code>"https://author-p1234-e4444.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/wknd/en/adventures/surf-camp-in-costa-rica/adobestock_266405335.jpeg&_charset_=utf8"</code></td>
</tr>
<tr>
<td>使用者代理</td>
<td>「Mozilla/5.0(Macintosh;英特爾Mac OS X 10_15_4)AppleWebKit/537.36（KHTML，如壁虎）Chrome/81.0.4044.122 Safari/537.36英吋</td>
</tr>
</tbody>
</table>

### 配置HTTP訪問日誌{#configuring-the-http-access-log}

AEM中的HTTP存取記錄無法設定為Cloud Service。

## Apache Web伺服器和Dispatcher記錄{#apache-web-server-and-dispatcher-logging}

AEM as aCloud Service提供發佈上Apache Web伺服器和dispatcher層的三個記錄檔：

* Apache HTTPD Web伺服器訪問日誌
* Apache HTTPD Web伺服器錯誤日誌
* Dispatcher記錄檔

請注意，這些記錄檔僅適用於發佈層級。

這組記錄檔會在AEM應用程式收到這些請求之前，將HTTP請求視為Cloud Service發佈層級，提供這些請求的深入分析。 請務必了解，理想情況下，對Publish層級伺服器的大部分HTTP請求都是由Apache HTTPD Web Server和AEM Dispatcher快取的內容提供，且絕不能觸及AEM應用程式本身。 因此，AEM Java、Request或Access記錄中沒有這些要求的記錄陳述式。

### Apache HTTPD Web伺服器訪問日誌{#apache-httpd-web-server-access-log}

Apache HTTP Web Server存取記錄檔會針對到達發佈層級之Web伺服器/Dispatcher的每個HTTP要求提供陳述式。 請注意，從上游CDN提供的請求不會反映在這些記錄中。

請參閱[官方apache檔案](https://httpd.apache.org/docs/2.4/logs.html#accesslog)中有關錯誤記錄格式的資訊。

**日誌輸出示例**

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
<td>客戶端的IP地址</td>
<td>-</td>
</tr>
<tr>
<td>使用者</td>
<td>-</td>
</tr>
<tr>
<td>日期時間</td>
<td>2000年5月01日2020:00:09:46 +000</td>
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
<td>Referer</td>
<td>-</td>
</tr>
<tr>
<td>使用者代理</td>
<td>「Mozilla/5.0(Macintosh;英特爾Mac OS X 10_15_4)AppleWebKit/537.36（KHTML，如壁虎）Chrome/81.0.4044.122 Safari/537.36英吋</td>
</tr>
</tbody>
</table>

### 配置Apache HTTPD Web伺服器訪問日誌{#configuring-the-apache-httpd-webs-server-access-log}

此記錄檔無法在AEM中設定為Cloud Service。

## Apache HTTPD Web伺服器錯誤日誌{#apache-httpd-web-server-error-log}

Apache HTTP Web Server錯誤記錄會針對發佈層級的Web伺服器/Dispatcher中的每個錯誤提供陳述式。

請參閱[官方apache檔案](https://httpd.apache.org/docs/2.4/logs.html#errorlog)中有關錯誤記錄格式的資訊。

**日誌輸出示例**

```
Fri Jul 17 02:19:48.093820 2020 [mpm_worker:notice] [pid 1:tid 140272153361288] [cm-p1234-e30226-aem-publish-b86c6b466-b9427] AH00292: Apache/2.4.43 (Unix) Communique/4.3.4-20200424 mod_qos/11.63 configured -- resuming normal operations
Fri Jul 17 02:19:48.093874 2020 [core:notice] [pid 1:tid 140272153361288] [cm-p1234-e30226-aem-publish-b86c6b466-b9427] AH00094: Command line: 'httpd -d /etc/httpd -f /etc/httpd/conf/httpd.conf -D FOREGROUND -D ENVIRONMENT_PROD'
Fri Jul 17 02:29:34.517189 2020 [mpm_worker:notice] [pid 1:tid 140293638175624] [cm-p1234-e30226-aem-publish-b496f64bf-5vckp] AH00295: caught SIGTERM, shutting down
```

**記錄格式**

<table>
<tbody>
<tr>
<td>日期時間</td>
<td>星期五2020年7月02:16:42.608913</td>
</tr>
<tr>
<td>事件層級</td>
<td>[mpm_worker:notice]</td>
</tr>
<tr>
<td>程式ID</td>
<td>[pid 1:tid 140715149343624]</td>
</tr>
<tr>
<td>Pod名稱</td>
<td>[cm-p1234-e56789-aem-publish-b86c6b466-qpfvp]</td>
</tr>
<tr>
<td>訊息</td>
<td>AH00094:命令列：'httpd -d /etc/httpd -f /etc/httpd/conf/httpd.conf -D FOREGROUND -D </td>
</tr>
</tbody>
</table>

### 配置Apache HTTPD Web伺服器錯誤日誌{#configuring-the-apache-httpd-web-server-error-log}

mod_rewrite日誌級別由檔案`conf.d/variables/global.var`中的變數REWRITE_LOG_LEVEL定義。

它可以設定為Error、Warn、Info、Debug和Trace1 - Trace8，預設值為Warn。 若要對RewriteRules進行除錯，建議將記錄層級提升為Trace2。

如需詳細資訊，請參閱[mod_rewrite模組檔案](https://httpd.apache.org/docs/current/mod/mod_rewrite.html#logging)。

若要根據環境設定記錄層級，請在global.var檔案中使用適當的條件分支，如下所述：

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

## Dispatcher日誌{#dispatcher-log}

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
<td>日期時間</td>
<td>[2000年7月17日2020:23:48:16 +000]</td>
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
<td>1949ms</td>
</tr>
<tr>
<td>農場</td>
<td>[publishfarm/0]</td>
</tr>
<tr>
<td>快取狀態</td>
<td>[行動失敗]</td>
</tr>
<tr>
<td>主機</td>
<td>"publish-p12904-e25628.adobeemcloud.com"</td>
</tr>
</tbody>
</table>

### 設定Dispatcher錯誤記錄{#configuring-the-dispatcher-error-log}

Dispatcher日誌級別由檔案`conf.d/variables/global.var`中的變數DISP_LOG_LEVEL定義。

它可以設定為Error、Warn、Info、Debug和Trace1，預設值為Warn。

雖然AEM記錄支援數個其他記錄粒度層級，但Dispatcher as aCloud Service建議使用下述層級。

要設定每個環境的日誌級別，請在`global.var`檔案中使用相應的條件分支，如下所述：

```
Define DISP_LOG_LEVEL Debug
  
<IfDefine ENVIRONMENT_STAGE>
  ...
  Define DISP_LOG_LEVEL Warn
  ...
</IfDefine>
<IfDefine ENVIRONMENT_PROD>
  ...
  Define DISP_LOG_LEVEL Error
  ...
</IfDefine>
```

## 如何存取記錄{#how-to-access-logs}

### 雲環境{#cloud-environments}

AEM as a cloud services的Cloud Service記錄檔可透過Cloud Manager介面下載，或使用Adobe I/O命令列介面追蹤命令列的記錄檔，以存取。 如需詳細資訊，請參閱[Cloud Manager記錄檔案](/help/implementing/cloud-manager/manage-logs.md)。

### 本機SDK {#local-sdk}

AEM as aCloud ServiceSDK提供記錄檔以支援本機開發。

AEM記錄檔位於資料夾`crx-quickstart/logs`中，可在此檢視下列記錄檔：

* AEM Java日誌：`error.log`
* AEM HTTP請求記錄：`request.log`
* AEM HTTP存取記錄：`access.log`

Apache層記錄檔（包括Dispatcher）位於Docker容器中，該容器保有Dispatcher。 如需如何啟動Dispatcher的資訊，請參閱[Dispatcher檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html)。

若要擷取記錄檔：

1. 在命令列中，輸入`docker ps`以列出容器
1. 若要登入容器，請輸入「`docker exec -it <container> /bin/sh`」，其中`<container>`是上一個步驟中的Dispatcher容器ID
1. 導覽至`/mnt/var/www/html`下的快取根
1. 記錄在`/etc/httpd/logs`下
1. Inspect記錄檔：可在資料夾XYZ下存取這些檔案，以便檢視下列記錄：
   * Apache HTTPD Web伺服器訪問日誌 — `httpd_access.log`
   * Apache HTTPD Web伺服器錯誤日誌 — `httpd_error.log`
   * Dispatcher記錄檔 — `dispatcher.log`

日誌也直接打印到終端輸出。 大部分情況下，這些記錄檔都應為DEBUG，這可在執行Docker時以參數形式傳入Debug層級來完成。 例如：

`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`

## 調試生產和預備{#debugging-production-and-stage}

在特殊情況下，需要更改日誌級別，以在Stage或Production環境中以更精細的粒度登錄。

雖然如此，但您仍須從「警告」和「錯誤」變更為「除錯」，並執行AEM部署作為Cloud Service，以便在環境中註冊這些設定變更，Git中的設定檔案記錄層級需有所變更。

根據Debug所寫入的流量和記錄陳述式數量，這可能會對環境造成不利的效能影響，因此，建議對Stage和Production偵錯層級進行以下變更：

* 審慎行事，只有在絕對必要時
* 恢復到適當級別並盡快重新部署

## Splunk日誌{#splunk-logs}

擁有Splunk帳戶的客戶可透過客戶支援票證要求，將其AEMCloud Service記錄檔轉送至適當的索引。 記錄資料等同於透過Cloud Manager記錄檔下載取得的功能，但客戶可能會發現，運用Splunk產品中可用的查詢功能相當方便。

與發送到Splunk的日誌關聯的網路頻寬被視為客戶網路I/O使用的一部分。

### 啟用Splunk轉發{#enabling-splunk-forwarding}

在支援請求中，客戶應指出：

* Splunk HEC端點地址
* Splunk索引
* Splunk埠
* Splunk HEC代號。 如需詳細資訊，請參閱[此頁面](https://docs.splunk.com/Documentation/Splunk/8.0.4/Data/HECExamples)。

應為每個相關程式/環境類型組合指定上述屬性。  例如，如果客戶想要開發、測試和生產環境，他們應提供三組資訊，如下所示。

>[!NOTE]
>
>不支援沙箱方案環境的Splunk轉送。

除了預備/生產環境外，您還應確定初始要求包含所有應啟用的開發環境。

如果在初始要求後建立的任何新開發環境都要有Splunk轉送，但未啟用，則應提出其他要求。

另請注意，如果已請求開發環境，請求或甚至沙箱環境中以外的其他開發環境可能會啟用Splunk轉送，且會共用Splunk索引。 客戶可使用`aem_env_id`欄位來區分這些環境。

以下是客戶支援請求的範例：

方案123，生產環境

* Splunk HEC端點地址：`splunk-hec-ext.acme.com`
* Splunk索引：acme_123prod（客戶可選擇想要的任何命名慣例）
* Splunk埠：443
* Splunk HEC令牌：ABC123

方案123，階段環境

* Splunk HEC端點地址：`splunk-hec-ext.acme.com`
* Splunk索引：acme_123stage
* Splunk埠：443
* Splunk HEC令牌：ABC123

方案123, Dev Envs

* Splunk HEC端點地址：`splunk-hec-ext.acme.com`
* Splunk索引：acme_123dev
* Splunk埠：443
* Splunk HEC令牌：ABC123

對於每個環境，它可能足以使用相同的Splunk索引，在這種情況下，可以使用`aem_env_type`欄位來根據dev、stage和prod值進行區分。 如果有多個開發環境，也可以使用`aem_env_id`欄位。 如果關聯的索引限制了對精簡的Splunk用戶集的訪問，則某些組織可能會為生產環境的日誌選擇單獨的索引。

以下是記錄項目的範例：

```
aem_env_id: 1242
aem_env_type: dev
aem_program_id: 12314
aem_tier: author
file_path: /var/log/aem/error.log
host: 172.34.200.12 
level: INFO
msg: [FelixLogListener] com.adobe.granite.repository Service [5091, [org.apache.jackrabbit.oak.api.jmx.SessionMBean]] ServiceEvent REGISTERED
orig_time: 16.07.2020 08:35:32.346
pod_name: aemloggingall-aem-author-77797d55d4-74zvt
splunk_customer: true
```
