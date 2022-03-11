---
title: 雲端中的 Dispatcher
description: '雲端中的 Dispatcher '
feature: Dispatcher
exl-id: 6d78026b-687e-434e-b59d-9d101349a707
source-git-commit: 4be76f19c27aeab84de388106a440434a99a738c
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 2%

---

# 雲端中的 Dispatcher {#Dispatcher-in-the-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispoverview"
>title="雲端中的 Dispatcher"
>abstract="本頁介紹如何下載和提取調度程式工具以及受支援的apache模組，並提供了對傳統和靈活模式的高級概述。"

## 簡介 {#apache-and-dispatcher-configuration-and-testing}

本頁介紹調度程式工具以及如何下載和提取它們以及受支援的apache模組，並概要介紹了傳統和靈活模式。 此外，還有關於驗證和調試以及將Dispatcher配置從AMS遷移到AEMas a Cloud Service

## Dispatcher工具 {#dispatcher-sdk}

Dispatcher Tools是整個as a Cloud ServiceSDK的一AEM部分，它提供：

* 一種香草檔案結構，包含要包含在Dispatcher的主項目中的配置檔案。
* 用於驗證Dispatcher配置是否只包括as a Cloud Service支援的指AEM令的客戶工具。        此外，工具還驗證語法是否正確，以便apache能夠成功啟動。
* 將Dispatcher本地調出的Docker映像。

## 下載和提取工具 {#extracting-the-sdk}

Dispatcher Tools, [AEMas a Cloud ServiceSDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)，可從zip檔案下載 [軟體分發](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html) 門戶。 該新Dispatcher Tools版本中提供的任何新配置都可用於部署到雲中運行該版本或更高版本AEM的雲環境。

解壓SDK，該SDK捆綁了用於macOS、Linux和Windows的Dispatcher Tools。

**對於macOS/Linux**，使Dispatcher工具項目可執行並運行它。 它將自解壓您儲存到的目錄下的Dispatcher Tools檔案(其中 `version` 是Dispatcher Tools的版本)。

```bash
$ chmod +x aem-sdk-dispatcher-tools-<version>-unix.sh
$ ./aem-sdk-dispatcher-tools-<version>-unix.sh
Verifying archive integrity...  100%   All good.
Uncompressing aem-sdk-dispatcher-tools-<version>-unix.sh 100%
```

**對於Windows**，提取Dispatcher Tooling zip存檔。

## 使用Dispatcher Tools進行驗證和調試 {#validation-debug}

調度程式工具用於驗證和調試項目的Dispatcher配置。 瞭解有關如何在下面引用的頁面中使用這些工具的更多資訊，具體取決於項目的調度程式配置是以靈活模式還是傳統模式構建的：

* **靈活模式**  — 建議的模式，以及 [原AEM型28](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=en) 以及更高版本，Cloud Manager也用於在Cloud Manager 2021.7.0版本後建立的新環境。 客戶可以通過添加資料夾和檔案來激活此模式 `opt-in/USE_SOURCES_DIRECTLY`。 通過使用此更靈活的模式，在舊模式下需要單個的重寫資料夾下，檔案結構沒有任何限制 `rewrite.rules` 的子菜單。 此外，您可以添加的規則數量沒有限制。 有關資料夾結構和本地驗證的詳細資訊，請參閱 [使用Dispatcher工具驗證和調試](/help/implementing/dispatcher/validation-debug.md)。

* **舊模式**  — 有關dispatcher配置舊模式的資料夾結構和本地驗證的詳細資訊，請參見 [使用Dispatcher Tools（舊版）驗證和調試](/help/implementing/dispatcher/validation-debug-legacy.md)

有關如何從舊式配置模型遷移到更靈活的配置模型的詳細資訊，請AEM參見 [本文檔](/help/implementing/dispatcher/validation-debug.md#migrating)。

## 支援的Apache模組 {#supported-directives}

下表顯示了支援的apache模組：

| 模組名稱 | 參考頁 |
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

客戶不能添加任意模組，但將來可能會考慮添加附加模組。 客戶可以通過在SDK中執行驗證程式的allowlist命令來查找指定Dispatcher版本可用的指令清單。

通過運行驗證程式的allowlist命令，可以列出Apache配置檔案中允許的指令：

```
$ validator allowlist
Cloud manager validator 2.0.4
 
Allowlisted directives:
  <Directory>
  ...
  
```

## 資料夾結構 {#folder-structure}

項目的apache和dispatcher資料夾結構將因項目使用的模式而略有不同，如中所述 [使用Dispatcher Tools進行驗證和調試](#validation-debug) 的上界。

## 從AMS遷移Dispatcher配置。 {#ams-aem}

有關如何將Dispatcher配置從AMS遷移到AEMas a Cloud Service的詳細資訊，請參見 [將Dispatcher配置從AMS遷移到AEM](/help/implementing/dispatcher/ams-aem.md) as a Cloud Service頁面。
