---
title: 雲端中的 Dispatcher
description: 雲端中的 Dispatcher
feature: Dispatcher
exl-id: 6d78026b-687e-434e-b59d-9d101349a707
source-git-commit: 98eff568686c72c626d2bf77d82e8c3f224eda42
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 74%

---

# 雲端中的 Dispatcher {#Dispatcher-in-the-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispoverview"
>title="雲端中的 Dispatcher"
>abstract="本頁面說明如何下載和擷取 Dispatcher 工具、受支援的 Apache 模組，並提供對傳統模式和靈活模式的概略介紹。"

## 簡介 {#apache-and-dispatcher-configuration-and-testing}

本頁介紹Dispatcher工具以及如何下載和提取它們以及受支援的Apache模組，並提供了對傳統和靈活模式的高級概述。 此外，還有關於驗證和調試以及將Dispatcher配置從AMS遷移到AEMas a Cloud Service的參考。 <!-- ERROR: NOT FOUND (HTTP ERROR 404) Also, see [this video](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-dispatcher-cloud.html) for additional details about deploying dispatcher files in a cloud service environment. -->

## Dispatcher 工具 {#dispatcher-sdk}

Dispatcher 工具是整體 AEM as a Cloud Service SDK 的一部分，提供：

* 普通文件檔案，其包含要放入 Dispatcher 之 maven 專案中的設定檔案。
* 用於驗證Dispatcher配置是否只包括as a Cloud Service支AEM持的指令的客戶工具。 此外，該工具還驗證了語法是否正確，以便Apache能夠成功啟動。
* 可在本機啟動 Dispatcher 的 Docker 影像。

## 下載並解壓縮工具 {#extracting-the-sdk}

Dispatcher 工具是 [AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) 的一部分，可以在 [Software Distribution](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html) 入口網站下載其壓縮檔。該新的 Dispatcher 工具版本中可用的任何新設定都可用於部署到特定雲端環境，此環境在雲端執行該 AEM 版本或更高版本。

解壓SDK，該SDK捆綁了用於macOS、Linux®和Windows的Dispatcher Tools。

**對於 macOS/Linux**，使 Dispatcher 工具成品可執行並執行它。它會自行提取您儲存到的目錄下的Dispatcher Tools檔案(其中 `version` 是Dispatcher Tools的版本)。

```bash
$ chmod +x aem-sdk-dispatcher-tools-<version>-unix.sh
$ ./aem-sdk-dispatcher-tools-<version>-unix.sh
Verifying archive integrity...  100%   All good.
Uncompressing aem-sdk-dispatcher-tools-<version>-unix.sh 100%
```

**對於 Windows**，擷取 Dispatcher Tooling zip 封存。

## 使用 Dispatcher 工具進行驗證和偵錯 {#validation-debug}

Dispatcher工具用於驗證和調試項目的Dispatcher配置。 瞭解有關如何在下面引用的頁面中使用這些工具的更多資訊，具體取決於項目的Dispatcher配置是以靈活模式還是傳統模式構建的：

* **靈活模式** - 建議使用的模式，也是 [AEM 原型 28](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hant) 及更高版本的預設模式，Cloud Manager 也將其用於 Cloud Manager 2021.7.0 版本之後建立的新環境。客戶可以透過新增資料夾和檔案 `opt-in/USE_SOURCES_DIRECTLY` 來啟動此模式。透過使用這種更靈活的模式，重寫資料夾下的檔案結構沒有限制，而在傳統模式下需要單一 `rewrite.rules` 檔案。此外，可以新增的規則數量也沒有限制。有關資料夾結構和本地驗證的詳細資訊，請參閱 [使用Dispatcher工具驗證和調試](/help/implementing/dispatcher/validation-debug.md)。

* **舊模式**  — 有關Dispatcher配置舊模式的資料夾結構和本地驗證的詳細資訊，請參見 [使用Dispatcher Tools（舊版）驗證和調試](/help/implementing/dispatcher/validation-debug-legacy.md)

如需進一步了解如何從舊設定模型移轉到更靈活的模型 (隨 AEM 原型 28 提供)，請參閱[此文件](/help/implementing/dispatcher/validation-debug.md#migrating)。

## 內容處置 {#content-disposition}

對於發佈層級，用於提供 Blob 的預設值是作為附件。使用標準 [內容處置標題](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Disposition) 調度器。

以下是設定看起來的樣子的範例：

```
<LocationMatch "^\/content\/dam.*\.(pdf).*">
 Header unset Content-Disposition
 Header set Content-Disposition inline
</LocationMatch>
```

## 支援的 Apache 模組 {#supported-directives}

下表顯示了支援的Apache模組：

| 模組名稱 | 參考頁面 |
|---|---|
| `core` | [https://httpd.apache.org/docs/2.4/mod/core.html](https://httpd.apache.org/docs/2.4/mod/core.html) |
| `mod_access_compat` | [https://httpd.apache.org/docs/2.4/mod/mod_access_compat.html](https://httpd.apache.org/docs/2.4/mod/mod_access_compat.html) |
| `mod_alias` | [https://httpd.apache.org/docs/2.4/mod/mod_alias.html](https://httpd.apache.org/docs/2.4/mod/mod_alias.html) |
| `mod_allowmethods` | [https://httpd.apache.org/docs/2.4/mod/mod_allowmethods.html](https://httpd.apache.org/docs/2.4/mod/mod_allowmethods.html) |
| `mod_authn_core` | [https://httpd.apache.org/docs/2.4/mod/mod_authn_core.html](https://httpd.apache.org/docs/2.4/mod/mod_authn_core.html) |
| `mod_authn_file` | [https://httpd.apache.org/docs/2.4/mod/core.html](https://httpd.apache.org/docs/2.4/mod/mod_authn_file.html) |
| `mod_authz_core` | [https://httpd.apache.org/docs/2.4/mod/core.html](https://httpd.apache.org/docs/2.4/mod/mod_authz_core.html) |
| `mod_authz_groupfile` | [https://httpd.apache.org/docs/2.4/mod/mod_authz_groupfile.html](https://httpd.apache.org/docs/2.4/mod/mod_authz_groupfile.html) |
| `mod_deflate` | [https://httpd.apache.org/docs/2.4/mod/mod_deflate.html](https://httpd.apache.org/docs/2.4/mod/mod_deflate.html) |
| `mod_dir` | [https://httpd.apache.org/docs/2.4/mod/mod_dir.html](https://httpd.apache.org/docs/2.4/mod/mod_dir.html) |
| `mod_env` | [https://httpd.apache.org/docs/2.4/mod/mod_env.html](https://httpd.apache.org/docs/2.4/mod/mod_env.html) |
| `mod_filter` | [https://httpd.apache.org/docs/2.4/mod/mod_filter.html](https://httpd.apache.org/docs/2.4/mod/mod_filter.html) |
| `mod_headers` | [https://httpd.apache.org/docs/2.4/mod/mod_headers.html](https://httpd.apache.org/docs/2.4/mod/mod_headers.html) |
| `mod_mime` | [https://httpd.apache.org/docs/2.4/mod/mod_mime.html](https://httpd.apache.org/docs/2.4/mod/mod_mime.html) |
| `mod_proxy` | [https://httpd.apache.org/docs/2.4/mod/mod_proxy.html](https://httpd.apache.org/docs/2.4/mod/mod_proxy.html) |
| `mod_proxy_http` | [https://httpd.apache.org/docs/2.4/mod/mod_proxy_http.html](https://httpd.apache.org/docs/2.4/mod/mod_proxy_http.html) |
| `mod_remoteip` | [https://httpd.apache.org/docs/2.4/mod/mod_remoteip.html](https://httpd.apache.org/docs/2.4/mod/mod_remoteip.html) |
| `mod_reqtimeout` | [https://httpd.apache.org/docs/2.4/mod/mod_reqtimeout.html](https://httpd.apache.org/docs/2.4/mod/mod_reqtimeout.html) |
| `mod_rewrite` | [https://httpd.apache.org/docs/2.4/mod/mod_rewrite.html](https://httpd.apache.org/docs/2.4/mod/mod_rewrite.html) |
| `mod_security` | [https://modsecurity.org/](https://modsecurity.org/) |
| `mod_setenvif` | [https://httpd.apache.org/docs/2.4/mod/mod_setenvif.html](https://httpd.apache.org/docs/2.4/mod/mod_setenvif.html) |
| `mod_ssl (only the SSLProxyEngine directive)` | [https://httpd.apache.org/docs/2.4/mod/mod_ssl.html#sslproxyengine](https://httpd.apache.org/docs/2.4/mod/mod_ssl.html#sslproxyengine) |
| `mod_substitute` | [https://httpd.apache.org/docs/2.4/mod/mod_substitute.html](https://httpd.apache.org/docs/2.4/mod/mod_substitute.html) |
| `mod_userdir` | [https://httpd.apache.org/docs/2.4/mod/mod_userdir.html](https://httpd.apache.org/docs/2.4/mod/mod_userdir.html) |
| `mod_macro` | [https://httpd.apache.org/docs/2.4/mod/mod_macro.html](https://httpd.apache.org/docs/2.4/mod/mod_macro.html) |
| `mod_include (no directives supported)` | [https://httpd.apache.org/docs/2.4/mod/mod_include.html](https://httpd.apache.org/docs/2.4/mod/mod_include.html) |


客戶不能新增任意模組，但將來可能會考慮加入其他模組。客戶可以在 SDK 中執行驗證器的加入允許清單命令，來找到可用於給定 Dispatcher 版本的指示詞清單。

執行驗證器的加入允許清單命令，可以列出允許用於 Apache 設定檔案的指示詞：

```
$ validator allowlist
Cloud manager validator 2.0.4
 
Allowlisted directives:
  <Directory>
  ...
  
```

## 資料夾結構 {#folder-structure}

項目的Apache和Dispatcher資料夾結構因項目使用的模式而略有不同，如中所述 [使用Dispatcher Tools進行驗證和調試](#validation-debug) 的上界。

## 從 AMS 移轉 Dispatcher 設定 {#ams-aem}

如需有關如何將 Dispatcher 設定從 AMS 移轉到 AEM as a Cloud Service 的詳細資訊，請參閱[將 Dispatcher 設定從 AMS 移轉到 AEM as a Cloud Service](/help/implementing/dispatcher/ams-aem.md) 頁面。
