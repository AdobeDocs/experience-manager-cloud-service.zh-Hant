---
title: 記錄AEMas a Cloud Service
description: 瞭解如何將日誌記錄AEM用於as a Cloud Service，以便為中央日誌記錄服務配置全局參數、單個服務的特定設定或如何請求資料記錄。
exl-id: 262939cc-05a5-41c9-86ef-68718d2cd6a9
source-git-commit: 197bff164df83788b4b8b16ba4c7a82021f86002
workflow-type: tm+mt
source-wordcount: '2334'
ht-degree: 2%

---

# 記錄AEMas a Cloud Service {#logging-for-aem-as-a-cloud-service}

AEMas a Cloud Service是客戶包括定制代碼以為客戶群創造獨特體驗的平台。 考慮到這一點，日誌服務是調試和瞭解本地開發和雲環境(尤其是AEMas a Cloud Service的開發環境)上代碼執行的關鍵功能。

在配置AEM檔案中管理as a Cloud Service的日誌記錄設定和日誌級別，這些配置檔案以AEMGit形式儲存為項目的一部分，並通過Cloud Manager部署為AEM項目的一部分。 登錄AEMas a Cloud Service可以分為兩個邏輯集：

* AEM日誌記錄，在應用程式級別執AEM行日誌記錄
* Apache HTTPD Web Server/Dispatcher日誌記錄，它在發佈層上執行Web伺服器和Dispatcher日誌記錄。

## 記AEM錄 {#aem-logging}

在應用程AEM序級別登錄由以下三個日誌處理：

1. Java日AEM志，用於為應用程式呈現Java日誌AEM語句。
1. HTTP請求日誌，它記錄有關HTTP請求及其響應的資訊AEM。
1. HTTP訪問日誌，記錄摘要資訊和HTTP請求AEM。

>[!NOTE]
>
>從發佈層的Dispatcher快取或上游CDN提供的HTTP請求不會反映在這些日誌中。

## Java日AEM志 {#aem-java-logging}

AEMas a Cloud Service提供對Java日誌語句的訪問。 應用程式的開發AEM人員應遵循常規Java日誌記錄最佳做法，在以下日誌級別記錄有關自定義代碼執行的相關語句：

<table>
<tr>
<td>
<b>環AEM境</b></td>
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
調試</td>
<td>
描述應用程式中發生的情況。<br>
當DEBUG日誌記錄處於活動狀態時，將記錄提供活動發生情況以及影響處理的任何關鍵參數的清晰說明的語句。</td>
<td>
<ul>
<li> 地方發展</li>
<li>開發</li>
</ul></td>
</tr>
<tr>
<td>
分段</td>
<td>
警告</td>
<td>
描述可能成為錯誤的條件。<br>
當WARN日誌記錄處於活動狀態時，只記錄指示接近次優性的條件語句。</td>
<td>
<ul>
<li> 地方發展</li>
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
描述表示故障並需要解決的條件。<br>
當ERROR日誌記錄處於活動狀態時，只記錄指示失敗的語句。 ERROR日誌語句表示應盡快解決的嚴重問題。</td>
<td>
<ul>
<li> 地方發展</li>
<li>開發</li>
<li>分段</li>
<li>生產</li>
</ul></td>
</tr>
</table>

雖然Java日誌記錄支援其他幾個級別的日誌粒度，AEM但as a Cloud Service建議使用上述三個級別。

通AEM過OSGi配置按環境類型設定日誌級別，OSGi配置又提交到Git，並通過雲管理器部署到AEMas a Cloud Service。 因此，最好保持日誌語句一致並為環境類型眾所周知，以確保通過「Cloud Service」提供的日誌在最佳日誌級別可用，而不需要使用更新的日誌級別配置重新部署應用程式。

**日誌輸出示例**

```
22.06.2020 18:33:30.120 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *ERROR* [qtp501076283-1809] io.prometheus.client.dropwizard.DropwizardExports Failed to get value from Gauge
22.06.2020 18:33:30.229 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [qtp501076283-1805] org.apache.sling.auth.core.impl.SlingAuthenticator getAnonymousResolver: Anonymous access not allowed by configuration - requesting credentials
22.06.2020 18:33:30.370 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] org.apache.sling.i18n.impl.JcrResourceBundle Finished loading 0 entries for 'en_US' (basename: <none>) in 4ms
22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [FelixLogListener] org.apache.sling.i18n Service [5126, [java.util.ResourceBundle]] ServiceEvent REGISTERED
22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *WARN* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] libs.granite.core.components.login.login$jsp j_reason param value 'unknown' cannot be mapped to a valid reason message: ignoring
```

**日誌格式**

<table>
<tbody>
<tr>
<td>日期時間</td>
<td>29.04.2020 21:50:13.398</td>
</tr>
<tr>
<td>AEMas a Cloud Service節點ID</td>
<td>[cm-p1234-e5678-aem-author-5955cb5b8-q7l9s]</td>
</tr>
<tr>
<td>日誌級別</td>
<td>調試</td>
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
<td>日誌消息</td>
<td>沒有指定的批准者，預設為[ Creative Approvers用戶組]</td>
</tr>
</tbody>
</table>

### 配置記錄程式 {#configuration-loggers}

AEMJava日誌定義為OSGi配置，因此使用運行模式文AEM件夾針對特定as a Cloud Service環境。

通過Sling LogManager工廠的OSGi配置為自定義Java包配置Java日誌記錄。 支援兩個配置屬性：

| OSGi配置屬性 | 說明 |
|---|---|
| org.apache.sling.commons.log.names | 要為其收集日誌語句的Java包。 |
| org.apache.sling.commons.log.level | 要記錄Java包的日誌級別，由org.apache.sling.commons.log.names指定 |

更改其他LogManager OSGi配置屬性可能會導致as a Cloud Service中的可用性AEM問題。

以下是建議的日誌配置示例(使用的佔位符Java包 `com.example`)的AEMas a Cloud Service。

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

## AEMHTTP請求日誌 {#aem-http-request-logging}

AEMas a Cloud Service的HTTP請求記錄可以按時間順序查看對HTTP請AEM求及其HTTP響應。 此日誌有助於瞭解對HTTP請求的AEM處理和響應順序。

瞭解此日誌的關鍵是用ID映射HTTP請求和響應對，用括弧中的數字值表示。 請注意，請求及其相應響應通常在日誌中插入其他HTTP請求和響應。

**示例日誌**

```
29/Apr/2020:19:14:21 +0000 [137] -> POST /conf/global/settings/dam/adminui-extension/metadataprofile/ HTTP/1.1 [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:22 +0000 [139] -> GET /mnt/overlay/dam/gui/content/processingprofilepage/metadataprofiles/editor.html/conf/global/settings/dam/adminui-extension/metadataprofile/main HTTP/1.1 [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:21 +0000 [137] <- 201 text/html 111ms [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:22 +0000 [139] <- 200 text/html;charset=utf-8 637ms [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
```

**日誌格式**

<table>
<tbody>
<tr>
<td>日期時間</td>
<td>2020年4月29日:19:14:21 +000</td>
</tr>
<tr>
<td>請求/響應對ID</td>
<td><code>[137]</code></td>
</tr>
<tr>
<td>HTTP 方法</td>
<td>POST</td>
</tr>
<tr>
<td>URL</td>
<td>/conf/global/settings/dam/adminui擴展/metadataprofile/</td>
</tr>
<tr>
<td>協定</td>
<td>HTTP/1.1
</td>
</tr>
<tr>
<td>AEMas a Cloud Service節點ID</td>
<td>[cm-p1234-e5678-aem-author-5955cb5b8-q7l9s]</td>
</tr>
</tbody>
</table>

### 配置日誌 {#configuring-the-log}

HTTP請AEM求日誌在as a Cloud Service中不可AEM配置。

## AEMHTTP訪問日誌 {#aem-http-access-logging}

因AEM為Cloud ServiceHTTP訪問記錄按時間順序顯示HTTP請求。 每個日誌條目都表示訪問的HTTP請AEM求。

此日誌有助於快速瞭解正在向哪些HTTP請求發出AEM，如果通過查看隨附的HTTP響應狀態代碼成功，以及HTTP請求完成所花的時間。 此日誌還有助於通過按用戶篩選日誌條目來調試特定用戶的活動。

**日誌輸出示例**

```
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css HTTP/1.1" 200 1141 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/customthumb/clientlibs.lc-60e4443805c37afa0c74b674b141f1df-lc.min.css HTTP/1.1" 200 809 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/metadataeditor/clientlibs/metadataeditor.lc-4a2226d8232f8b7ab27d24820b9ddd64-lc.min.js HTTP/1.1" 200 7965 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
```

| AEMas a Cloud Service節點ID | cm-p1235-e2644-aem-author-5955cb5b8-8kgr2 |
|---|---|
| 客戶端的IP地址 | - |
| 使用者 | myuser@adobe.com |
| 日期時間 | 2020年4月30日:17:37:14 +0000 |
| HTTP方法 | GET |
| URL | `/libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css` |
| 協定 | HTTP/1.1 |
| HTTP響應狀態 | 200 |
| 響應正文的大小（以位元組為單位） | 1141 |
| 反向連結 | `"https://author-p1234-e4444.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/wknd/en/adventures/surf-camp-in-costa-rica/adobestock_266405335.jpeg&_charset_=utf8"` |
| 用戶代理 | `"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"` |

### 配置HTTP訪問日誌 {#configuring-the-http-access-log}

HTTP訪問日誌在as a Cloud Service中不可AEM配置。

## Apache Web Server和Dispatcher日誌記錄 {#apache-web-server-and-dispatcher-logging}

AEMas a Cloud Service在「發佈」中為Apache Web Server和調度程式層提供三個日誌：

* Apache HTTPD Web伺服器訪問日誌
* Apache HTTPD Web伺服器錯誤日誌
* 調度程式日誌

請注意，這些日誌僅可用於發佈層。

這組日誌在as a Cloud Service發佈層的HTTP請求到達應AEM用程式之前提供了對這些請求的AEM洞見。 理解這一點非常重要，因為理想情況下，發佈層伺服器的大多數HTTP請求都由Apache HTTPD Web Server和AEMDispatcher快取的內容提供，並且永遠不能訪問應AEM用程式本身。 因此，在Java、Request或Access日誌中AEM沒有這些請求的log語句。

### Apache HTTPD Web伺服器訪問日誌 {#apache-httpd-web-server-access-log}

Apache HTTP Web Server訪問日誌為到達發佈層的Web伺服器/Dispatcher的每個HTTP請求提供語句。 請注意，從上游CDN服務的請求不會反映在這些日誌中。

請參閱中有關錯誤日誌格式的資訊 [官方apace文檔](https://httpd.apache.org/docs/2.4/logs.html#accesslog)。

**日誌輸出示例**

```
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:41 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/favicons/favicon-32.png HTTP/1.1" 200 715 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:41 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/favicons/favicon-512.png HTTP/1.1" 200 9631 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:42 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/country-flags/US.svg HTTP/1.1" 200 810 "https://publish-p6902-e30226.adobeaemcloud.com/content/wknd/us/en.html" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
```

**日誌格式**

<table>
<tbody>
<tr>
<td>作AEM為雲服務節點ID</td>
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
<td>協定</td>
<td>HTTP/1.1</td>
</tr>
<tr>
<td>HTTP響應狀態</td>
<td>200</td>
</tr>
<tr>
<td>大小</td>
<td>310</td>
</tr>
<tr>
<td>參考</td>
<td>-</td>
</tr>
<tr>
<td>用戶代理</td>
<td>「Mozilla/5.0(Macintosh;英特爾MacOS X 10_15_4)AppleWebKit/537.36（KHTML，如Gecko）Chrome/81.0.4044.122 Safari/537.36"</td>
</tr>
</tbody>
</table>

### 配置Apache HTTPD Web伺服器訪問日誌 {#configuring-the-apache-httpd-webs-server-access-log}

此日誌在AEMas a Cloud Service中不可配置。

## Apache HTTPD Web伺服器錯誤日誌 {#apache-httpd-web-server-error-log}

Apache HTTP Web Server錯誤日誌為發佈層的Web伺服器/調度程式中的每個錯誤提供語句。

請參閱中有關錯誤日誌格式的資訊 [官方apace文檔](https://httpd.apache.org/docs/2.4/logs.html#errorlog)。

**日誌輸出示例**

```
Fri Jul 17 02:19:48.093820 2020 [mpm_worker:notice] [pid 1:tid 140272153361288] [cm-p1234-e30226-aem-publish-b86c6b466-b9427] AH00292: Apache/2.4.43 (Unix) Communique/4.3.4-20200424 mod_qos/11.63 configured -- resuming normal operations
Fri Jul 17 02:19:48.093874 2020 [core:notice] [pid 1:tid 140272153361288] [cm-p1234-e30226-aem-publish-b86c6b466-b9427] AH00094: Command line: 'httpd -d /etc/httpd -f /etc/httpd/conf/httpd.conf -D FOREGROUND -D ENVIRONMENT_PROD'
Fri Jul 17 02:29:34.517189 2020 [mpm_worker:notice] [pid 1:tid 140293638175624] [cm-p1234-e30226-aem-publish-b496f64bf-5vckp] AH00295: caught SIGTERM, shutting down
```

**日誌格式**

<table>
<tbody>
<tr>
<td>日期時間</td>
<td>週五7月17日02:16:42.608913 2020</td>
</tr>
<tr>
<td>事件級別</td>
<td>[mpm_worker：注意]</td>
</tr>
<tr>
<td>進程ID</td>
<td>[pid 1:tid 140715149343624]</td>
</tr>
<tr>
<td>Pod名稱</td>
<td>[cm-p1234-e56789-aem-publish-b86c6b466-qpfvp]</td>
</tr>
<tr>
<td>訊息</td>
<td>AH00094:命令行：'httpd -d /etc/httpd -f /etc/httpd/conf/httpd.conf -D前景 — D </td>
</tr>
</tbody>
</table>

### 配置Apache HTTPD Web伺服器錯誤日誌 {#configuring-the-apache-httpd-web-server-error-log}

mod_rewrite日誌級別由檔案中的變數REWRITE_LOG_LEVEL定義 `conf.d/variables/global.var`。

它可以設定為Error、Warn、Info、Debug和Trace1 - Trace8，預設值為Warn。 要調試RewriteRules，建議將日誌級別提升到Trace2。

查看 [mod_rewrite模組文檔](https://httpd.apache.org/docs/current/mod/mod_rewrite.html#logging) 的子菜單。

要設定每個環境的日誌級別，請在global.var檔案中使用相應的條件分支，如下所述：

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

## 調度程式日誌 {#dispatcher-log}

**範例**

```
[17/Jul/2020:23:48:06 +0000] [I] [cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr] "GET /content/wknd/us/en/adventures.html" - 475ms [publishfarm/0] [action miss] "publish-p12904-e25628.adobeaemcloud.com"
[17/Jul/2020:23:48:07 +0000] [I] [cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr] "GET /content/wknd/us/en/adventures/climbing-new-zealand/_jcr_content/root/responsivegrid/carousel/item_1571266094599.coreimg.jpeg/1473680817282/sport-climbing.jpeg" 302 10ms [publishfarm/0] [action none] "publish-p12904-e25628.adobeaemcloud.com"
[17/Jul/2020:23:48:07 +0000] [I] [cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr] "GET /content/wknd/us/en/adventures/ski-touring-mont-blanc/_jcr_content/root/responsivegrid/carousel/item_1571168419252.coreimg.jpeg/1572047288089/adobestock-238230356.jpeg" 302 11ms [publishfarm/0] [action none] "publish-p12904-e25628.adobeaemcloud.com"
```

**日誌格式**

<table>
<tbody>
<tr>
<td>日期時間</td>
<td>[2020年7月17日:23:48:16 +000]</td>
</tr>
<tr>
<td>Pod名稱</td>
<td>[cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr]</td>
</tr>
<tr>
<td>協定</td>
<td>GET</td>
</tr>
<tr>
<td>URL</td>
<td>/content/experience-fragments/wknd/language-masters/en/contributors/sofia-sjoeberg/master/_jcr_content/root/responsivegrid/image.coreimg.100.500.jpeg/1572236359031/ayo-ogunseinde-237739.jpeg</td>
</tr>
<tr>
<td>調度程式響應狀態代碼</td>
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
<td>[未完成操作]</td>
</tr>
<tr>
<td>主機</td>
<td>"publish-p12904-e25628.adobeamcloud.com"</td>
</tr>
</tbody>
</table>

### 配置Dispatcher錯誤日誌 {#configuring-the-dispatcher-error-log}

調度程式日誌級別由檔案中的變數DISP_LOG_LEVEL定義 `conf.d/variables/global.var`。

它可以設定為「錯誤」、「警告」、「資訊」、「調試」和「跟蹤1」，預設值為「警告」。

雖然Dispatcher日誌記錄支援其他幾個級別的日誌記錄粒度，AEM但as a Cloud Service建議使用下述級別。

要設定每個環境的日誌級別，請使用 `global.var` 檔案，如下所述：

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

## 如何訪問日誌 {#how-to-access-logs}

### 雲環境 {#cloud-environments}

可AEM通過Cloud Manager介面下載或使用Adobe I/O命令行介面跟蹤命令行上的日誌來訪問雲服務的as a Cloud Service日誌。 有關詳細資訊，請參見 [Cloud Manager日誌記錄文檔](/help/implementing/cloud-manager/manage-logs.md)。

### 本地SDK {#local-sdk}

AEMas a Cloud ServiceSDK提供日誌檔案以支援本地開發。

日誌AEM位於資料夾中 `crx-quickstart/logs`，其中可以查看以下日誌：

* AEMJava日誌： `error.log`
* AEMHTTP請求日誌： `request.log`
* AEMHTTP訪問日誌： `access.log`

Apache層日誌（包括調度程式）位於Docker容器中，該容器容納Dispatcher。 查看 [調度程式文檔](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html) 的子菜單。

要檢索日誌，請執行以下操作：

1. 在命令行上，鍵入 `docker ps` 列出容器
1. 要登錄到容器，請鍵入「`docker exec -it <container> /bin/sh`」 `<container>` 是上一步中的調度程式容器id
1. 導航到以下的快取根 `/mnt/var/www/html`
1. 日誌在 `/etc/httpd/logs`
1. Inspect:可以在資料夾XYZ下訪問這些日誌，在該資料夾中可以查看以下日誌：
   * Apache HTTPD Web伺服器訪問日誌 —  `httpd_access.log`
   * Apache HTTPD Web伺服器錯誤日誌 —  `httpd_error.log`
   * 調度程式日誌 —  `dispatcher.log`

日誌也直接打印到終端輸出。 大多數情況下，這些日誌應是DEBUG ，這可以通過在運行Docker時以參數形式傳遞Debug級別來完成。 例如：

`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`

## 調試生產和階段 {#debugging-production-and-stage}

在特殊情況下，需要更改日誌級別以在階段或生產環境中以更精細的粒度進行日誌。

雖然這是可能的，但需要將Git中配置檔案中的日誌級別從「警告」和「錯誤」更改為「調試」，並執行部署到AEMas a Cloud Service以向環境註冊這些配置更改。

根據流量和Debug編寫的日誌語句的數量，這可能會對環境造成不利的效能影響，因此，建議對階段和生產調試級別進行以下更改：

* 謹慎行事，只有在絕對必要時
* 恢復到適當的級別並盡快重新部署

## Splunk日誌 {#splunk-logs}

擁有Splunk帳戶的客戶可通過客戶支援票證請求將其AEM Cloud Service日誌轉發到相應的索引。 日誌資料等效於通過Cloud Manager日誌下載提供的內容，但客戶可能會發現利用Splunk產品中提供的查詢功能非常方便。

與發送到Splunk的日誌關聯的網路頻寬被認為是客戶網路I/O使用的一部分。

### 啟用Splunk轉發 {#enabling-splunk-forwarding}

在支援請求中，客戶應指出：

* Splunk HEC終結點地址。 此終結點必須具有有效的SSL證書
* Splunk指數
* 斯普隆克港
* Splunk HEC令牌。 請參閱 [此頁](https://docs.splunk.com/Documentation/Splunk/8.0.4/Data/HECExamples) 的子菜單。

應為每個相關程式/環境類型組合指定上述屬性。  例如，如果客戶想要開發、試運行和生產環境，他們應提供三組資訊，如下所示。

>[!NOTE]
>
>不支援沙盒程式環境的Splunk轉發。

您應確保初始請求包括除階段/prod環境外應啟用的所有開發環境。 Splunk必須具有SSL證書，並且是面向公共的。

如果在初始請求後建立的任何新開發環境都打算進行Splunk轉發，但未啟用它，則應發出其他請求。

另請注意，如果請求了開發環境，則請求環境中甚至沙盒環境以外的其他開發環境可能會啟用Splunk轉發並共用Splunk索引。 客戶可以 `aem_env_id` 欄位來區分這些環境。

在下面，您將找到客戶支援請求示例：

方案123，生產環境

* Splunk HEC終結點地址： `splunk-hec-ext.acme.com`
* Splunk索引：acme_123prod（客戶可以選擇它希望的任何命名約定）
* Splunk埠：443
* Splunk HEC令牌：ABC123

方案123，階段環境

* Splunk HEC終結點地址： `splunk-hec-ext.acme.com`
* Splunk索引：acme_123賽段
* Splunk埠：443
* Splunk HEC令牌：ABC123

方案123，開發人員

* Splunk HEC終結點地址： `splunk-hec-ext.acme.com`
* Splunk索引：acme_123dev
* Splunk埠：443
* Splunk HEC令牌：ABC123

對於每個環境，使用同一Splunk索引可能足夠，在這種情況下 `aem_env_type` 欄位可用於根據dev、stage和prod的值進行區分。 如果存在多個開發環境， `aem_env_id` 欄位。 如果關聯的索引限制對精簡的Splunk用戶集的訪問，則某些組織可能會為生產環境的日誌選擇單獨的索引。

下面是一個示例日誌條目：

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
