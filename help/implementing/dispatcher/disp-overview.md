---
title: 雲端中的 Dispatcher
description: 雲端中的 Dispatcher
feature: Dispatcher
exl-id: 6d78026b-687e-434e-b59d-9d101349a707
source-git-commit: 6ea869b3067d168c661ea925e112857c4bbd70e9
workflow-type: ht
source-wordcount: '1010'
ht-degree: 100%

---

# 雲端中的 Dispatcher {#Dispatcher-in-the-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispoverview"
>title="雲端中的 Dispatcher"
>abstract="本頁面說明如何下載和擷取 Dispatcher 工具、受支援的 apache 模組，並提供對傳統模式和靈活模式的概略介紹。"

## 簡介 {#apache-and-dispatcher-configuration-and-testing}

本頁面介紹 Dispatcher 工具，並說明如何下載和擷取此工具、受支援的 apache 模組，並提供對傳統模式和靈活模式的概略介紹。此外，還有關於驗證和偵錯以及將 Dispatcher 設定從 AMS 移轉到 AEM as a Cloud Service 的進一步參考。此外，請參閱[此影片](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-dispatcher-cloud.html)，進一步了解如何在雲端服務環境中部署 Dispatcher 檔案。

## Dispatcher 工具 {#dispatcher-sdk}

Dispatcher 工具是整體 AEM as a Cloud Service SDK 的一部分，提供：

* 普通文件檔案，其包含要放入 Dispatcher 之 maven 專案中的設定檔案。
* 供客戶驗證 Dispatcher 設定是否僅包含 AEM as a Cloud Service 受支援指示詞的工具。此外，該工具也會驗證語法是否正確，以便 apache 可以成功啟動。
* 可在本機啟動 Dispatcher 的 Docker 影像。

## 下載並解壓縮工具 {#extracting-the-sdk}

Dispatcher 工具是 [AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) 的一部分，可以在 [Software Distribution](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html) 入口網站下載其壓縮檔。該新的 Dispatcher 工具版本中可用的任何新設定都可用於部署到特定雲端環境，此環境在雲端執行該 AEM 版本或更高版本。

解壓縮 SDK，其包含適用於 macOS、Linux 和 Windows 的 Dispatcher 工具。

**對於 macOS/Linux**，使 Dispatcher 工具成品可執行並執行它。它將於所在目錄下自行擷取 Dispatcher 工具檔案 (其中 `version`是 Dispatcher 工具的版本)。

```bash
$ chmod +x aem-sdk-dispatcher-tools-<version>-unix.sh
$ ./aem-sdk-dispatcher-tools-<version>-unix.sh
Verifying archive integrity...  100%   All good.
Uncompressing aem-sdk-dispatcher-tools-<version>-unix.sh 100%
```

**對於 Windows**，擷取 Dispatcher Tooling zip 封存。

## 使用 Dispatcher 工具進行驗證和偵錯 {#validation-debug}

Dispatcher 工具用於驗證和偵錯專案的 Dispatcher 設定。根據專案的 Dispatcher 設定是以靈活模式還是傳統模式建構的，在下面參考的頁面中進一步了解如何使用這些工具：

* **靈活模式** - 建議使用的模式，也是 [AEM 原型 28](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hant) 及更高版本的預設模式，Cloud Manager 也將其用於 Cloud Manager 2021.7.0 版本之後建立的新環境。客戶可以透過新增資料夾和檔案 `opt-in/USE_SOURCES_DIRECTLY` 來啟動此模式。透過使用這種更靈活的模式，重寫資料夾下的檔案結構沒有限制，而在傳統模式下需要單一 `rewrite.rules` 檔案。此外，可以新增的規則數量也沒有限制。如需資料夾結構和本機驗證的詳細資訊，請參閱[使用 Dispatcher 工具進行驗證和偵錯](/help/implementing/dispatcher/validation-debug.md)。

* **傳統模式** - 如需詳細了解 Dispatcher 設定傳統模式的資料夾結構和本機驗證，請參閱[使用 Dispatcher 工具進行驗證和偵錯 (傳統)](/help/implementing/dispatcher/validation-debug-legacy.md)

如需進一步了解如何從舊設定模型移轉到更靈活的模型 (隨 AEM 原型 28 提供)，請參閱[此文件](/help/implementing/dispatcher/validation-debug.md#migrating)。

## 內容處置 {#content-disposition}

對於發佈層級，用於提供 Blob 的預設值是作為附件。這可以使用 Dispatcher 中的標準[內容處置標頭](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Disposition)覆寫。

以下是設定看起來的樣子的範例：

```
<LocationMatch "^\/content\/dam.*\.(pdf).*">
 Header unset Content-Disposition
 Header set Content-Disposition inline
</LocationMatch>
```

## 支援的 Apache 模組 {#supported-directives}

下表顯示了支援的 apache 模組：

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

專案的 apache 和 Dispatcher 資料夾結構將根據專案使用的模式略有不同，如上文[使用 Dispatcher 工具進行驗證和偵錯](#validation-debug)章節所述。

## 從 AMS 移轉 Dispatcher 設定 {#ams-aem}

如需有關如何將 Dispatcher 設定從 AMS 移轉到 AEM as a Cloud Service 的詳細資訊，請參閱[將 Dispatcher 設定從 AMS 移轉到 AEM as a Cloud Service](/help/implementing/dispatcher/ams-aem.md) 頁面。
