---
title: 記錄
description: 瞭解如何為中央記錄服務設定全域參數、個別服務的特定設定，或如何要求資料記錄。
translation-type: tm+mt
source-git-commit: c7100f53ce38cb8120074ec4eb9677fb7303d007
workflow-type: tm+mt
source-wordcount: '873'
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
| 29.04.2020 21:50:13.398 | `[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]` | `*DEBUG*` | qtp2130572036-1472 | com.example.approval.workflow.impl.CustomApprovalWorkflow | 沒有指定的審批人，預設為「創 [ 作審批人」用戶組 ] |

**日誌輸出示例**

`22.06.2020 18:33:30.120 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *ERROR* [qtp501076283-1809] io.prometheus.client.dropwizard.DropwizardExports Failed to get value from Gauge`
`22.06.2020 18:33:30.229 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [qtp501076283-1805] org.apache.sling.auth.core.impl.SlingAuthenticator getAnonymousResolver: Anonymous access not allowed by configuration - requesting credentials`
`22.06.2020 18:33:30.370 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] org.apache.sling.i18n.impl.JcrResourceBundle Finished loading 0 entries for 'en_US' (basename: <none>) in 4ms`
`22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [FelixLogListener] org.apache.sling.i18n Service [5126, [java.util.ResourceBundle]] ServiceEvent REGISTERED`
`22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *WARN* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] libs.granite.core.components.login.login$jsp j_reason param value 'unknown' cannot be mapped to a valid reason message: ignoring`

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
