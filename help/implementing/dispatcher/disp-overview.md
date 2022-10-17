---
title: 雲端中的 Dispatcher
description: 雲端中的 Dispatcher
feature: Dispatcher
exl-id: 6d78026b-687e-434e-b59d-9d101349a707
source-git-commit: 69cb9b9015ed3a7acdcc42c7e25fb45b479a7f4e
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 7%

---

# 雲端中的 Dispatcher {#Dispatcher-in-the-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispoverview"
>title="雲端中的 Dispatcher"
>abstract="本頁說明如何下載和擷取Dispatcher工具、支援的Apache模組，並提供舊版和彈性模式的概觀。"

## 簡介 {#apache-and-dispatcher-configuration-and-testing}

本頁說明Dispatcher工具，以及如何下載和擷取工具、支援的Apache模組，並提供舊版和彈性模式的概觀。 此外，也有進一步的驗證和除錯參考，以及將Dispatcher設定從AMS移轉至AEMas a Cloud Service。 另請參閱 [此影片](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-dispatcher-cloud.html) 如需有關在雲端服務環境中部署dispatcher檔案的其他詳細資訊。

## Dispatcher工具 {#dispatcher-sdk}

Dispatcher工具是整體AEMas a Cloud ServiceSDK的一部分，並提供：

* 包含要納入Dispatcher專案之Maven專案的組態檔的Vanilla檔案結構。
* 客戶驗證Dispatcher設定是否僅包含AEMas a Cloud Service支援指示的工具。        此外，工具也會驗證語法是否正確，以便Apache能成功啟動。
* 在本機開啟Dispatcher的Docker影像。

## 下載和解壓縮工具 {#extracting-the-sdk}

Dispatcher工具， [AEMas a Cloud ServiceSDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)，可從zip檔案下載： [Software Distribution](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html) 入口網站。 該新Dispatcher工具版本中可用的任何新設定，皆可部署至在雲端或更新版本中執行該AEM版本的雲端環境。

將SDK解壓縮，此SDK捆綁了macOS、Linux和Windows的Dispatcher工具。

**針對macOS/Linux**，讓Dispatcher工具工件可執行並執行。 它會從您儲存的目錄下(其中 `version` 是Dispatcher工具的版本)。

```bash
$ chmod +x aem-sdk-dispatcher-tools-<version>-unix.sh
$ ./aem-sdk-dispatcher-tools-<version>-unix.sh
Verifying archive integrity...  100%   All good.
Uncompressing aem-sdk-dispatcher-tools-<version>-unix.sh 100%
```

**Windows版**，解壓縮Dispatcher工具zip封存。

## 使用Dispatcher工具進行驗證和除錯 {#validation-debug}

Dispatcher工具可用來驗證專案的Dispatcher設定並除錯。 進一步了解如何根據專案的Dispatcher設定是以彈性模式還是舊式模式建構，在以下參考的頁面中使用這些工具：

* **彈性模式**  — 建議的模式，以及 [AEM原型28](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hant) 以及更高版本，Cloud Manager也用於Cloud Manager 2021.7.0版之後建立的新環境。 客戶可以新增資料夾和檔案來啟動此模式 `opt-in/USE_SOURCES_DIRECTLY`. 使用此更靈活的模式時，重寫資料夾下的檔案結構沒有限制，在舊版模式中，只需單一 `rewrite.rules` 檔案。 此外，您可新增的規則數目並無限制。 如需資料夾結構和本機驗證的詳細資訊，請參閱 [使用Dispatcher工具進行驗證和除錯](/help/implementing/dispatcher/validation-debug.md).

* **舊式模式**  — 如需dispatcher設定舊版模式的資料夾結構和本機驗證的詳細資訊，請參閱 [使用Dispatcher工具（舊版）進行驗證和除錯](/help/implementing/dispatcher/validation-debug-legacy.md)

如需如何從舊版設定模型移轉至更具彈性模型(隨附於AEM原型28)的詳細資訊，請參閱 [本檔案](/help/implementing/dispatcher/validation-debug.md#migrating).

## 內容處置 {#content-disposition}

對於發佈層級，提供Blob的預設值為附件。 這可以使用標準來覆寫 [內容處置標題](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Disposition) 在dispatcher中。

以下是設定看起來的範例：

```
<LocationMatch "^\/content\/dam.*\.(pdf).*">
 Header unset Content-Disposition
 Header set Content-Disposition inline
</LocationMatch>
```

## 支援的Apache模組 {#supported-directives}

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


客戶無法添加任意模組，但將來可能會考慮添加其他模組。 客戶可在SDK中執行驗證器的allowlist命令，以找到指定Dispatcher版本可用的指令清單。

運行驗證器的allowlist命令可以列出Apache配置檔案中允許的指令：

```
$ validator allowlist
Cloud manager validator 2.0.4
 
Allowlisted directives:
  <Directory>
  ...
  
```

## 資料夾結構 {#folder-structure}

專案的apache和dispatcher資料夾結構會因專案使用的模式而稍有不同，如 [使用Dispatcher工具進行驗證和除錯](#validation-debug) 一節。

## 從AMS移轉Dispatcher設定。 {#ams-aem}

如需如何將Dispatcher設定從AMS移轉至AEM as a Cloud Service的詳細資訊，請參閱 [將Dispatcher設定從AMS移轉至AEM](/help/implementing/dispatcher/ams-aem.md) as a Cloud Service頁面。
