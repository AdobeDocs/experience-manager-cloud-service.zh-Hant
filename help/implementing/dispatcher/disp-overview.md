---
title: 雲端中的 Dispatcher
description: '雲端中的 Dispatcher '
feature: Dispatcher
exl-id: 6d78026b-687e-434e-b59d-9d101349a707
source-git-commit: 4be76f19c27aeab84de388106a440434a99a738c
workflow-type: tm+mt
source-wordcount: '917'
ht-degree: 2%

---

# 雲端中的 Dispatcher {#Dispatcher-in-the-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispoverview"
>title="雲端中的 Dispatcher"
>abstract="本頁說明如何下載和擷取Dispatcher工具、支援的Apache模組，並提供舊版和彈性模式的概觀。"

## 簡介 {#apache-and-dispatcher-configuration-and-testing}

本頁說明Dispatcher工具，以及如何下載和擷取工具、支援的Apache模組，並提供舊版和彈性模式的概觀。 此外，也有進一步的驗證和除錯參考，以及將Dispatcher設定從AMS移轉至AEM作為Cloud Service

## Dispatcher工具 {#dispatcher-sdk}

Dispatcher工具是整體AEM的一部分，作為Cloud ServiceSDK，並提供：

* 包含要納入Dispatcher專案之Maven專案的組態檔的Vanilla檔案結構。
* 客戶驗證Dispatcher設定是否僅包含AEM作為Cloud Service支援指令的工具。        此外，工具也會驗證語法是否正確，以便Apache能成功啟動。
* 在本機開啟Dispatcher的Docker影像。

## 下載和解壓縮工具 {#extracting-the-sdk}

[AEM as a Dispatcher SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)的一部分，可從[Software Distribution](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html)入口網站的zip檔案下載Dispatcher工具。 該新Dispatcher工具版本中可用的任何新設定，皆可部署至在雲端或更新版本中執行該AEM版本的雲端環境。

將SDK解壓縮，此SDK會結合macOS、Linux和Windows的Dispatcher工具。

**對於macOS/Linux**，請讓Dispatcher工具工件可執行並執行它。它會自行擷取您儲存Dispatcher工具的目錄下的Dispatcher工具檔案（其中`version`是Dispatcher工具的版本）。

```bash
$ chmod +x aem-sdk-dispatcher-tools-<version>-unix.sh
$ ./aem-sdk-dispatcher-tools-<version>-unix.sh
Verifying archive integrity...  100%   All good.
Uncompressing aem-sdk-dispatcher-tools-<version>-unix.sh 100%
```

**針對Windows**，解壓縮Dispatcher工具郵遞區號封存。

## 使用Dispatcher工具進行驗證和除錯 {#validation-debug}

Dispatcher工具可用來驗證專案的Dispatcher設定並除錯。 進一步了解如何根據專案的Dispatcher設定是以彈性模式還是舊式模式建構，在以下參考的頁面中使用這些工具：

* **彈性模式**  — 建議的模式，以及AEM原型28及更新版本的預設 [](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=en) ,Cloud Manager也會用於在Cloud Manager 2021.7.0版本後建立的新環境。客戶可以通過添加資料夾和檔案`opt-in/USE_SOURCES_DIRECTLY`來激活此模式。 使用此更靈活的模式時，在舊模式中需要單個`rewrite.rules`檔案的重寫資料夾下的檔案結構沒有限制。 此外，您可新增的規則數目並無限制。 如需資料夾結構和本機驗證的詳細資訊，請參閱[使用Dispatcher工具](/help/implementing/dispatcher/validation-debug.md)驗證和除錯。

* **舊版模式**  — 如需Dispatcher設定舊版模式的資料夾結構和本機驗證的詳細資訊，請參 [閱使用Dispatcher工具（舊版）驗證和除錯](/help/implementing/dispatcher/validation-debug-legacy.md)

如需如何從舊版組態模型移轉至更具彈性模型(自AEM原型28起提供)的詳細資訊，請參閱本檔案[](/help/implementing/dispatcher/validation-debug.md#migrating)。

## 支援的Apache模組 {#supported-directives}

下表顯示支援的Apache模組：

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

專案的apache和dispatcher資料夾結構會因專案使用的模式而稍有不同，如上方的[使用Dispatcher工具](#validation-debug)驗證和除錯一節所述。

## 從AMS移轉Dispatcher設定。 {#ams-aem}

如需如何將Dispatcher設定從AMS移轉至AEM as aCloud Service的詳細資訊，請參閱[將Dispatcher設定從AMS移轉至AEM](/help/implementing/dispatcher/ams-aem.md)作為Cloud Service頁面。
