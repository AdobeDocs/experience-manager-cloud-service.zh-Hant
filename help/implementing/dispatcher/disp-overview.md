---
title: 雲端中的 Dispatcher
description: '雲端中的 Dispatcher '
feature: Dispatcher
exl-id: 6d78026b-687e-434e-b59d-9d101349a707
source-git-commit: 7b8b9ca2881d07482888ac2a53b8c3bdff02b6dd
workflow-type: tm+mt
source-wordcount: '4247'
ht-degree: 6%

---

# 雲端中的 Dispatcher {#Dispatcher-in-the-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispoverview"
>title="雲端中的 Dispatcher"
>abstract="本節說明如何將AEM建構為Cloud ServiceApache和Dispatcher設定，以及如何在部署至雲端環境之前，先在本機驗證並執行。 此外，也說明在雲端環境中進行除錯的方式。"

## Apache和Dispatcher設定及測試{#apache-and-dispatcher-configuration-and-testing}

本節說明如何將AEM建構為Cloud ServiceApache和Dispatcher設定，以及如何在部署至雲端環境之前，先在本機驗證並執行。 此外，也說明在雲端環境中進行除錯的方式。 如需Dispatcher的其他資訊，請參閱[AEM Dispatcher檔案](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hant)。

>[!NOTE]
>Windows用戶需要使用Windows 10專業版或支援Docker的其他分發版。 這是在本機電腦上執行和偵錯Dispatcher的必要條件。 以下各節包含使用SDK的Mac或Linux版本的命令，但Windows SDK也能以類似方式使用。

## Dispatcher工具{#dispatcher-sdk}

Dispatcher工具是整體AEM的一部分，作為Cloud ServiceSDK，並提供：

* 包含要納入Dispatcher專案之Maven專案的組態檔的Vanilla檔案結構。
* 客戶驗證Dispatcher設定是否僅包含AEM作為Cloud Service支援指令的工具。        此外，工具也會驗證語法是否正確，以便Apache能成功啟動。
* 在本機開啟Dispatcher的Docker影像。

## 下載和解壓縮工具{#extracting-the-sdk}

[AEM as a Dispatcher SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)的一部分，可從[Software Distribution](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html)入口網站的zip檔案下載Dispatcher工具。 該新Dispatcher工具版本中可用的任何新設定，皆可用來部署至在雲端或更新版本中執行該AEM版本的雲端環境。

將SDK解壓縮，此SDK捆綁了macOS/Linux和Windows的Dispatcher工具。

**對於macOS/Linux**，請讓Dispatcher工具工件可執行並執行它。它會自行擷取您儲存Dispatcher工具的目錄下的Dispatcher工具檔案（其中`version`是Dispatcher工具的版本）。

```bash
$ chmod +x aem-sdk-dispatcher-tools-<version>-unix.sh
$ ./aem-sdk-dispatcher-tools-<version>-unix.sh
Verifying archive integrity...  100%   All good.
Uncompressing aem-sdk-dispatcher-tools-<version>-unix.sh 100%
```

**針對Windows**，解壓縮Dispatcher工具郵遞區號封存。

## 檔案結構{#file-structure}

專案的Dispatcher子資料夾結構如下所述，應複製至Maven專案Dispatcher資料夾：

```bash
./
├── conf.d
│   ├── available_vhosts
│   │   └── default.vhost
│   ├── dispatcher_vhost.conf
│   ├── enabled_vhosts
│   │   ├── README
│   │   └── default.vhost -> ../available_vhosts/default.vhost
│   └── rewrites
│   │   ├── default_rewrite.rules
│   │   └── rewrite.rules
│   └── variables
|       ├── custom.vars
│       └── global.vars
└── conf.dispatcher.d
    ├── available_farms
    │   └── default.farm
    ├── cache
    │   ├── default_invalidate.any
    │   ├── default_rules.any
    │   └── rules.any
    ├── clientheaders
    │   ├── clientheaders.any
    │   └── default_clientheaders.any
    ├── dispatcher.any
    ├── enabled_farms
    │   ├── README
    │   └── default.farm -> ../available_farms/default.farm
    ├── filters
    │   ├── default_filters.any
    │   └── filters.any
    ├── renders
    │   └── default_renders.any
    └── virtualhosts
        ├── default_virtualhosts.any
        └── virtualhosts.any
```

以下是可修改的顯著檔案說明：

**可自訂的檔案**

可自訂下列檔案，並會在部署時傳輸至您的雲端執行個體：

* `conf.d/available_vhosts/<CUSTOMER_CHOICE>.vhost`

您可以有一或多個這些檔案。 它們包含與主機名稱相符的`<VirtualHost>`項目，並允許Apache以不同規則處理每個網域流量。 檔案在`available_vhosts`目錄中建立，並在`enabled_vhosts`目錄中使用符號連結啟用。 在`.vhost`檔案中，將包含重寫和變數等其他檔案。

* `conf.d/rewrites/rewrite.rules`

此檔案包含自`.vhost`檔案內。 `mod_rewrite`有一組重寫規則。

>[!NOTE]
>
>目前，必須使用單一重寫檔案，而非網站專用的檔案。 可自訂檔案的內容總和通常必須小於1MB。

* `conf.d/variables/custom.vars`

此檔案包含自`.vhost`檔案內。 您可以在此位置放入Apache變數的定義。

* `conf.d/variables/global.vars`

此檔案包含在`dispatcher_vhost.conf`檔案內。 您可以變更Dispatcher，並重新寫入此檔案中的記錄層級。

* `conf.dispatcher.d/available_farms/<CUSTOMER_CHOICE>.farm`

您可以有一或多個這些檔案，且這些檔案包含伺服器陣列，以符合主機名稱，並允許Dispatcher模組以不同規則處理每個伺服器陣列。 檔案在`available_farms`目錄中建立，並在`enabled_farms`目錄中使用符號連結啟用。 在`.farm`檔案中，將包含其他檔案，如篩選器、快取規則等。

* `conf.dispatcher.d/cache/rules.any`

此檔案包含自`.farm`檔案內。 它指定快取首選項。

* `conf.dispatcher.d/clientheaders/clientheaders.any`

此檔案包含自`.farm`檔案內。 它會指定應將哪些要求標題轉送至後端。

* `conf.dispatcher.d/filters/filters.any`

此檔案包含自`.farm`檔案內。 它有一組規則，可變更應篩選掉的流量，而不是設為傳送至後端。

* `conf.dispatcher.d/virtualhosts/virtualhosts.any`

此檔案包含自`.farm`檔案內。 它包含要由全局匹配匹配的主機名或URI路徑的清單。 這會決定要用來提供要求的後端。

上述檔案會參考下列不可修改的組態檔。 雲端環境中，Dispatcher不會處理不可變檔案的變更。

**不可變的配置檔案**

這些檔案是基本架構的一部分，並強制執行標準和最佳實務。 這些檔案被視為不可修改，因為在本機修改或刪除這些檔案不會影響您的部署，因為這些檔案將不會傳輸至您的雲端例項。

建議上述檔案參考下列不可修改的檔案，後跟任何其他陳述式或覆蓋。 將Dispatcher設定部署至雲端環境時，無論本機開發中使用的版本為何，都會使用不可修改檔案的最新版本。

* `conf.d/available_vhosts/default.vhost`

包含範例虛擬主機。 對於您自己的虛擬主機，建立此檔案的副本，自定義它，轉到`conf.d/enabled_vhosts`並建立指向自定義副本的符號連結。

* `conf.d/dispatcher_vhost.conf`

基本框架的一部分，用於說明如何包括虛擬主機和全局變數。

* `conf.d/rewrites/default_rewrite.rules`

適用於標準專案的預設重寫規則。 如果需要自定義，請修改`rewrite.rules`。 在您的自訂中，如果預設規則符合您的需求，您仍可以先加入。

* `conf.dispatcher.d/available_farms/default.farm`

包含範例Dispatcher伺服器陣列。 針對您自己的伺服器陣列，建立此檔案的副本、自訂該檔案、前往`conf.d/enabled_farms`並建立自訂副本的符號連結。

* `conf.dispatcher.d/cache/default_invalidate.any`

基本框架的一部分，在啟動時生成。 您是&#x200B;**required** ，要在您定義的每個伺服器陣列中，於`cache/allowedClients`區段中包含此檔案。

* `conf.dispatcher.d/cache/default_rules.any`

適用於標準專案的預設快取規則。 如果需要自定義，請修改`conf.dispatcher.d/cache/rules.any`。 在您的自訂中，如果預設規則符合您的需求，您仍可以先加入。

* `conf.dispatcher.d/clientheaders/default_clientheaders.any`

轉送至後端的預設要求標題，適用於標準專案。 如果需要自定義，請修改`clientheaders.any`。 在您的自訂中，如果預設請求標題符合您的需求，您仍可以先加入這些標題。

* `conf.dispatcher.d/dispatcher.any`

基本架構的一部分，用來說明如何包含Dispatcher伺服器陣列。

* `conf.dispatcher.d/filters/default_filters.any`

適用於標準專案的預設篩選器。 如果需要自定義，請修改`filters.any`。 在您的自訂中，如果預設篩選器符合您的需求，您仍可以先加入這些篩選器。

* `conf.dispatcher.d/renders/default_renders.any`

作為基本框架的一部分，此檔案在啟動時生成。 您是&#x200B;**required** ，要在您定義的每個伺服器陣列中，於`renders`區段中包含此檔案。

* `conf.dispatcher.d/virtualhosts/default_virtualhosts.any`

適用於標準專案的預設主機全域。 如果需要自定義，請修改`virtualhosts.any`。 在您的自訂中，您不應包含預設主機全域，因為它符合&#x200B;**every**&#x200B;傳入的要求。

>[!NOTE]
>
>AEM作為Cloud Service的主要原型將產生相同的Dispatcher設定檔案結構。

以下各節說明如何在本機驗證設定，以便在部署內部版本時，讓設定在Cloud Manager中傳遞相關的品質閘道。

## Dispatcher配置{#local-validation-of-dispatcher-configuration}中受支援指令的本地驗證

SDK中`bin/validator`提供驗證工具，作為Mac OS、Linux或Windows二進位檔，讓客戶執行與Cloud Manager在建立和部署版本時將執行的驗證相同。

它叫用為：`validator full [-d folder] [-w allowlist] zip-file | src folder`

此工具會掃描模式為`conf.d/enabled_vhosts/*.vhost`的所有檔案，以驗證AEM as a Cloud service支援的適當指示是否正在使用Dispatcher設定。

在Windows上，Dispatcher驗證器會區分大小寫。 因此，如果您不遵守配置所在路徑的大寫，則可能無法驗證配置，例如：

```
bin\validator.exe full src
Cloud manager validator 2.0.xx
2021/03/15 18:15:40 Dispatcher configuration validation failed:
  conf.dispatcher.d\available_farms\default.farm:15: parent directory outside server root: c:\k\a\aem-dispatcher-sdk-windows-symlinks-testing3\dispatcher\src
  
```

通過從Windows資源管理器複製並貼上路徑，然後在命令提示符下使用`cd`命令將該路徑複製並貼上到該路徑，來避免此錯誤。

運行驗證器的allowlist命令可以列出Apache配置檔案中允許的指令：

```
$ validator allowlist
Cloud manager validator 2.0.4
 
Allowlisted directives:
  <Directory>
  ...
  
```

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

客戶無法添加任意模組，但將來可能會考慮將其他模組包含在產品中。 如上所述，客戶可在SDK中執行驗證器的allowlist命令，以找到指定Dispatcher版本可用的指令清單。

允許清單包含客戶配置中允許的Apache指令清單。 如果未允許列出指令，則工具會記錄錯誤並傳回非零退出代碼。 若命令列上未提供允許清單（即叫用該允許清單的方式），則此工具會使用Cloud Manager在部署至雲端環境前用於驗證的預設允許清單。

此外，它還會進一步掃描模式為`conf.dispatcher.d/enabled_farms/*.farm`的所有檔案，並檢查：

* 沒有透過`/glob`使用的篩選器規則可允許（如需詳細資訊，請參閱[CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957)）
* 未公開管理功能。 例如，對路徑（如`/crx/de or /system/console`）的存取。

對maven工件或`dispatcher/src`子目錄運行時，它將報告驗證失敗：

```
$ validator full dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-allowlisted directives:
  conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
  conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

請注意，驗證工具只會報告未列入允許清單之Apache指示的禁止使用。 它不會報告Apache配置的語法或語義問題，因為此資訊僅可用於運行環境中的Apache模組。

以下提供疑難排解技術，以偵錯工具輸出的常見驗證錯誤：

**在封存中找 `conf.dispatcher.d` 不到子資料夾**

您的封存應包含資料 `conf.d` 夾和 `conf.dispatcher.d`。請注意，您不 **應**&#x200B;在封 `etc/httpd` 存中使用首碼。

**在中找不到任何場`conf.dispatcher.d/enabled_farms`**

已啟用的伺服器陣列應位於提及的子資料夾中。

**包含的檔案(...)必須命名：...**

您的伺服器陣列設定中有兩個區段，**必須**包含
特定檔案：`/cache`區段中的`/renders`和`/allowedClients`。 那些
區段必須如下所示：

```
/renders {
    $include "../renders/default_renders.any"
}
```

和:

```
/allowedClients {
    $include "../cache/default_invalidate.any"
}
```

**包含在未知位置的檔案：...**

您的伺服器陣列設定中有四個區段可讓您包含自己的檔案：`/cache`區段中的`/clientheaders`、`filters`、`/rules`及`/virtualhosts`。 包含的檔案需命名如下：

| 章節 | 包含檔案名 |
|------------------|--------------------------------------|
| `/clientheaders` | `../clientheaders/clientheaders.any` |
| `/filters` | `../filters/filters.any` |
| `/rules` | `../cache/rules.any` |
| `/virtualhosts` | `../virtualhosts/virtualhosts.any` |

或者，您也可以包含 **這些檔案的預設版本** ，其名稱會以字詞 `default_`為前置詞，例如。`../filters/default_filters.any`。

**包含位於(...)的語句，位於任何已知位置之外：...**

除上文各段所述的六節外，不得
要使用`$include`語句，例如，以下語句將生成此錯誤：

```
/invalidate {
    $include "../cache/invalidate.any"
}
```

**允許的用戶端/轉譯不包括於：...**

如果您未在`/cache`區段中指定`/renders`和`/allowedClients`的包含，則會產生此錯誤。 請參閱
包含的**檔案(...)必須命名：...**&#x200B;區段，以取得詳細資訊。

**篩選不得使用全域模式以允許請求**

允許具有`/glob`樣式規則的請求是不安全的，此規則與完整的請求行相符，例如

```
/0100 {
    /type "allow" /glob "GET *.css *"
}
```

此陳述式的用意是允許`css`檔案的要求，但也允許要求&#x200B;**any**&#x200B;資源，後跟查詢字串`?a=.css`。 因此，禁止使用這類篩選器（另請參閱CVE-2016-0957）。

**包含的檔案(...)與任何已知檔案不匹配**

Apache虛擬主機配置中有兩種類型的檔案，可以指定為包括：重寫和變數。
包含的檔案需命名如下：

| 類型 | 包含檔案名 |
|-----------|---------------------------------|
| 重寫 | `conf.d/rewrites/rewrite.rules` |
| 變數 | `conf.d/variables/custom.vars` |

或者，您也可以包含重寫規則的&#x200B;**default**&#x200B;版本，其名稱為`conf.d/rewrites/default_rewrite.rules`。
請注意，變數檔案沒有預設版本。

**檢測到已棄用的配置佈局，啟用相容性模式**

此訊息指出您的設定已棄用第1版配置，包含完整
具有`ams_`前置詞的Apache配置和檔案。 雖然仍支援向後
相容性，您應切換至新版面。

## Dispatcher設定語法的本機驗證，以便apache httpd可以啟動{#local-validation}

建立Dispatcher模組設定僅包含支援的指令後，您應檢查語法是否正確，以便Apache能夠啟動。 若要測試，Docker必須安裝在本機。 請注意，AEM不需要執行。

使用`validate.sh`指令碼，如下所示：

```
$ validate.sh src/dispatcher
Phase 1: Dispatcher validator
2019/06/19 16:02:55 No issues found
Phase 1 finished
Phase 2: httpd -t validation in docker image
Running script /docker_entrypoint.d/10-create-docroots.sh
Running script /docker_entrypoint.d/20-wait-for-backend.sh
Waiting until aemhost is available
aemhost resolves to xx.xx.xx.xx
Running script /docker_entrypoint.d/30-allowed-clients.sh
# Dispatcher configuration: (/etc/httpd/conf.dispatcher.d/dispatcher.any)
/farms {
...
}
Syntax OK
Phase 2 finished
```

指令碼會執行下列動作：

1. 它會從上一節運行驗證器，以確保僅包含受支援的指令。 如果配置無效，指令碼將失敗。
2. 它會執行`httpd -t command`以測試語法是否正確，以便apache httpd可以啟動。 如果成功，配置應已準備就緒，可進行部署。
3. 檢查Dispatcher SDK設定檔案的子集（如[檔案結構區段](#file-structure)所述）是否未修改。 這是AEM SDK版本v2021.1.4738推出的新檢查，其中也包含Dispatcher工具2.0.36版。在此更新前，客戶可能錯誤地假設這些不可變檔案的任何本機SDK修改也會套用至雲端環境。

在Cloud Manager部署期間，也會執行`httpd -t syntax`檢查，且Cloud Manager `Build Images step failure`記錄中會包含任何錯誤。

## 在本機測試您的Apache和Dispatcher設定{#testing-apache-and-dispatcher-configuration-locally}

您也可以在本機測試Apache和Dispatcher設定。 它需要將Docker安裝在本機，而您的設定必須如上所述通過驗證。

使用`-d`參數（會輸出包含所有Dispatcher組態檔的資料夾），執行驗證器工具（請注意，它與先前提到的`validator.sh`不同）。 然後執行`docker_run.sh`指令碼，將該資料夾作為引數傳遞。 提供埠號(此處：8080)，若要公開Dispatcher端點，會啟動Docker容器，使用您的設定執行Dispatcher。

```
$ validator full -d out src/dispatcher
2019/06/19 16:02:55 No issues found
$ docker_run.sh out docker.for.mac.localhost:4503 8080
Running script /docker_entrypoint.d/10-create-docroots.sh
Running script /docker_entrypoint.d/20-wait-for-backend.sh
Waiting until aemhost is available
aemhost resolves to xx.xx.xx.xx
Running script /docker_entrypoint.d/30-allowed-clients.sh
Starting httpd server
...
```

這會啟動容器中的Dispatcher，其後端會指向本機Mac OS電腦上，連接埠4503上執行的AEM例項。

## 為Apache和Dispatcher設定{#debugging-apache-and-dispatcher-configuration}除錯

下列策略可用來增加Dispatcher模組的記錄輸出，並查看本機和雲端環境中`RewriteRule`評估的結果。

這些模組的日誌級別由變數`DISP_LOG_LEVEL`和`REWRITE_LOG_LEVEL`定義。 可在檔案`conf.d/variables/global.vars`中設定。 其相關部分如下：

```
# Log level for the dispatcher
#
# Possible values are: Error, Warn, Info, Debug and Trace1
# Default value: Warn
#
# Define DISP_LOG_LEVEL Warn
 
# Log level for mod_rewrite
#
# Possible values are: Error, Warn, Info, Debug and Trace1 - Trace8
# Default value: Warn
#
# To debug your RewriteRules, it is recommended to raise your log
# level to Trace2.
#
# More information can be found at:
# https://httpd.apache.org/docs/current/mod/mod_rewrite.html#logging
#
# Define REWRITE_LOG_LEVEL Warn
```

在本機執行Dispatcher時，記錄會直接列印至終端輸出。 大部分情況下，您會希望這些記錄處於DEBUG中，這可透過在執行Docker時將Debug層級傳遞為參數來完成。 例如：`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`。

雲端環境的記錄檔會透過Cloud Manager中可用的記錄服務公開。

## 每個環境的不同Dispatcher設定{#different-dispatcher-configurations-per-environment}

目前，相同的Dispatcher設定會套用至所有AEM作為Cloud Service環境。 運行時將具有一個環境變數`ENVIRONMENT_TYPE`，該環境變數包含當前運行模式（開發、測試或生產）以及定義。 定義可以是`ENVIRONMENT_DEV`、`ENVIRONMENT_STAGE`或`ENVIRONMENT_PROD`。 在Apache設定中，變數可直接用於運算式中。 或者，定義可用來建置邏輯：

```
# Simple usage of the environment variable
ServerName ${ENVIRONMENT_TYPE}.company.com
 
# When more logic is required
<IfDefine ENVIRONMENT_STAGE>
  # These statements are for stage
  Define VIRTUALHOST stage.example.com
</IfDefine>
<IfDefine ENVIRONMENT_PROD>
  # These statements are for production
  Define VIRTUALHOST prod.example.com
</IfDefine>
```

在Dispatcher設定中，可使用相同的環境變數。 如果需要更多邏輯，請定義上述範例中所示的變數，然後在Dispatcher設定區段中使用這些變數：

```
/virtualhosts {
  { "${VIRTUALHOST}" }
}
```

在本地測試配置時，可以通過將變數`DISP_RUN_MODE`直接傳遞到`docker_run.sh`指令碼來模擬不同的環境類型：

```
$ DISP_RUN_MODE=stage docker_run.sh out docker.for.mac.localhost:4503 8080
```

未傳入DISP_RUN_MODE值時，預設的執行模式為「dev」。
有關可用選項和變數的完整清單，請運行指令碼`docker_run.sh`，而不帶參數。

## 檢視Docker容器{#viewing-dispatcher-configuration-in-use-by-docker-container}正在使用的Dispatcher設定

若使用環境特定設定，可能很難判斷實際的Dispatcher設定看起來是什麼樣子。 使用`docker_run.sh`啟動Docker容器後，可以按如下方式傾棄該容器：

* 確定使用中的Docker容器ID:

```
$ docker ps
CONTAINER ID       IMAGE
d75fbd23b29        adobe/aem-ethos/dispatcher-publish:...
```

* 使用該容器ID執行以下命令行：

```
$ docker exec d75fbd23b29 httpd-test
# Dispatcher configuration: (/etc/httpd/conf.dispatcher.d/dispatcher.any)
/farms {
  /publishfarm {
    /clientheaders {
...
```

## AMS Dispatcher與AEM as aCloud Service的主要差異{#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

如上方參考頁面所述，AEM as aCloud Service中的Apache和Dispatcher設定與AMS 1相當類似。 主要差異為：

* 在AEM as aCloud Service中，某些Apache指令不得使用（例如`Listen`或`LogLevel`）
* 在AEM as aCloud Service中，只能將Dispatcher設定的某些片段放入包含檔案中，而且其命名很重要。 例如，要在不同主機間重複使用的篩選規則必須放在名為`filters/filters.any`的檔案中。 如需詳細資訊，請參閱參考頁面。
* 在AEM as aCloud Service中，有額外驗證可禁止使用`/glob`撰寫的篩選規則，以防止發生安全性問題。 由於將使用`deny *`而非`allow *`（無法使用），因此客戶將受益於在本機執行Dispatcher，以及執行試用和錯誤，查看記錄檔，以明確知道Dispatcher篩選器封鎖哪些路徑，以便新增這些路徑。

## 將Dispatcher設定從AMS移轉至AEM作為Cloud Service的准則

Managed Services和AEM as aCloud Service之間的Dispatcher設定結構有差異。 以下提供逐步指南，說明如何從AMS Dispatcher設定第2版移轉至AEM as aCloud Service。

## 如何將AMS轉換為AEM as a Cloud service Dispatcher設定

以下章節提供如何轉換AMS設定的逐步指示。 這是假設
封存的結構類似於[Cloud Manager Dispatcher設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)中所述的結構

### 提取封存並移除最終首碼

將存檔解壓到資料夾，並確保直接子資料夾以`conf`、`conf.d`開頭，
`conf.dispatcher.d`和`conf.modules.d`。 如果沒有，請在階層中向上移動。

### 移除未使用的子資料夾和檔案

移除子資料夾`conf`和`conf.modules.d`，以及符合`conf.d/*.conf`的檔案。

### 移除所有非發佈用的虛擬主機

刪除`conf.d/enabled_vhosts`中具有`author`、`unhealthy`、`health`、
`lc`或`flush`。 `conf.d/available_vhosts`中所有非虛擬主機檔案
連結至的也可移除。

### 移除或註解未引用連接埠 80 的虛擬主機區段

如果您的虛擬主機檔案中仍有區段專門引用埠80以外的其他埠，例如：

```
<VirtualHost *:443>
...
</VirtualHost>
```


請移除或加上註解。系統將不會處理這些區段中的陳述式，但如果您保留這些陳述式，您最終可能仍會編輯，但將徒勞無功而倍感困惑。

### 檢查重新寫入

輸入目錄`conf.d/rewrites`。

移除任何名為`base_rewrite.rules`和`xforwarded_forcessl_rewrite.rules`的檔案，並記得
在虛擬主機檔案中移除引用了`Include`陳述式。

如果`conf.d/rewrites`目前包含單一檔案，則應將其重新命名為`rewrite.rules`，否則不應
也別忘了調整在虛擬主機檔案中引用該檔案的`Include`陳述式。

但是，如果資料夾包含多個虛擬主機專用檔案，則其內容應為
複製到`Include`陳述式，在虛擬主機檔案中引用這些語句。

### 檢查變數

輸入目錄`conf.d/variables`。

移除任何名為`ams_default.vars`的檔案，並記得在虛擬檔案中移除`Include`陳述式
主機引用檔案的檔案。

如果`conf.d/variables`目前包含單一檔案，則應將其重新命名為`custom.vars`，否則不應
也別忘了調整在虛擬主機檔案中引用該檔案的`Include`陳述式。

但是，如果資料夾包含多個虛擬主機專用檔案，則其內容應為
複製到`Include`陳述式，在虛擬主機檔案中引用這些語句。

### 移除允許清單

移除資料夾`conf.d/whitelists`，並移除虛擬主機檔案中引用`Include`的陳述式
子資料夾中的檔案。

### 取代任何已無法使用的變數

在所有虛擬主機檔案中：

將`PUBLISH_DOCROOT`更名為`DOCROOT`
移除引用`DISP_ID`、`PUBLISH_FORCE_SSL`或`PUBLISH_WHITELIST_ENABLED`變數的區段

### 執行驗證器以檢查狀態

使用`httpd`子命令，在您的目錄中執行Dispatcher驗證器：

```
$ validator httpd .
```

如果您看見有關遺失 Include 檔案的錯誤，請檢查您是否已正確地重新命名那些檔案。

如果您看到未列入允許清單的Apache指示，請將其移除。

### 移除所有非發佈用的伺服器陣列

移除`conf.dispatcher.d/enabled_farms`中具有`author`、`unhealthy`、`health`、
`lc`或`flush`。 `conf.dispatcher.d/available_farms`中所有非
連結至的也可移除。

### 重新命名伺服器陣列檔案

必須更名`conf.d/enabled_farms`中的所有伺服器陣列以符合模式`*.farm`，例如
名為`customerX_farm.any`的伺服器陣列檔案應重新命名為`customerX.farm`。

### 檢查快取

輸入目錄`conf.dispatcher.d/cache`。

移除任何以「`ams_`」為首碼的檔案。

如果`conf.dispatcher.d/cache`現在為空，請複製檔案`conf.dispatcher.d/cache/rules.any`
從標準Dispatcher設定傳送至此資料夾。 標準Dispatcher
可在此SDK的資料夾`src`中找到設定。 別忘了調整
`$include`引用伺服器陣列檔案中`ams_*_cache.any`規則檔案的語句
還有。

如果`conf.dispatcher.d/cache`現在包含尾碼為`_cache.any`的單一檔案，
應將其重新命名為`rules.any`，同時別忘了調整`$include`陳述式
在伺服器陣列檔案中也參考該檔案。

但是，如果資料夾包含多個具有該模式的伺服器陣列特定檔案，則其內容
應複製到`$include`陳述式，在伺服器陣列檔案中引用這些陳述式。

移除尾碼為`_invalidate_allowed.any`的任何檔案。

從預設值複製檔案`conf.dispatcher.d/cache/default_invalidate_any`
AEM。

在每個伺服器陣列檔案中，移除`cache/allowedClients`區段中的任何內容並加以取代
包含：

```
$include "../cache/default_invalidate.any"
```

### 檢查用戶端標頭

輸入目錄`conf.dispatcher.d/clientheaders`。

移除任何以「`ams_`」為首碼的檔案。

如果`conf.dispatcher.d/clientheaders`現在包含尾碼為`_clientheaders.any`的單一檔案，
應將其重新命名為`clientheaders.any`，同時別忘了調整`$include`陳述式
在伺服器陣列檔案中也參考該檔案。

但是，如果資料夾包含多個具有該模式的伺服器陣列特定檔案，則其內容
應複製到`$include`陳述式，在伺服器陣列檔案中引用這些陳述式。

從預設值複製檔案`conf.dispatcher/clientheaders/default_clientheaders.any`
AEM作為該位置的Cloud ServiceDispatcher設定。

在每個伺服器陣列檔案中，取代任何如下所示的clientheader include陳述式：

```
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"
```

以及以下陳述式：

```
$include "../clientheaders/default_clientheaders.any"
```

### 檢查篩選器

輸入目錄`conf.dispatcher.d/filters`。

移除任何以「`ams_`」為首碼的檔案。

如果`conf.dispatcher.d/filters`現在包含單一檔案，則應將其重新命名為
`filters.any`，別忘記調整引用該的`$include`陳述式
檔案。

但是，如果資料夾包含多個具有該模式的伺服器陣列特定檔案，則其內容
應複製到`$include`陳述式，在伺服器陣列檔案中引用這些陳述式。

從預設值複製檔案`conf.dispatcher/filters/default_filters.any`
AEM作為該位置的Cloud ServiceDispatcher設定。

在每個伺服器陣列檔案中，取代任何如下所示的filter include陳述式：

```
$include "/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"
```

以及以下陳述式：

```
$include "../filters/default_filters.any"
```

### 檢查轉譯

輸入目錄`conf.dispatcher.d/renders`。

移除該資料夾中的所有檔案。

從預設值複製檔案`conf.dispatcher.d/renders/default_renders.any`
AEM作為該位置的Cloud ServiceDispatcher設定。

在每個伺服器陣列檔案中，移除`renders`區段中的任何內容並加以取代
包含：

```
$include "../renders/default_renders.any"
```

### 檢查虛擬主機

將目錄`conf.dispatcher.d/vhosts`更名為`conf.dispatcher.d/virtualhosts`並輸入。

移除任何以「`ams_`」為首碼的檔案。

如果`conf.dispatcher.d/virtualhosts`現在包含單一檔案，則應將其重新命名為
`virtualhosts.any`，別忘記調整引用該的`$include`陳述式
檔案。

但是，如果資料夾包含多個具有該模式的伺服器陣列特定檔案，則其內容
應複製到`$include`陳述式，在伺服器陣列檔案中引用這些陳述式。

從預設值複製檔案`conf.dispatcher/virtualhosts/default_virtualhosts.any`
AEM作為該位置的Cloud ServiceDispatcher設定。

在每個伺服器陣列檔案中，取代任何如下所示的filter include陳述式：

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

以及以下陳述式：

```
$include "../virtualhosts/default_virtualhosts.any"
```

### 執行驗證器以檢查狀態

使用`dispatcher`子命令，在目錄中以Cloud ServiceDispatcher驗證器的形式執行AEM :

```
$ validator dispatcher .
```

如果您看見有關遺失 Include 檔案的錯誤，請檢查您是否已正確地重新命名那些檔案。

如果您看見有關未定義變數「`PUBLISH_DOCROOT`」的錯誤，請將其重新命名為「`DOCROOT`」。

如果看見其他錯誤，請參考驗證器工具文件的疑難排解章節。

### 使用本機部署測試配置（需要安裝Docker）

使用AEM中的指令碼`docker_run.sh`做為Cloud ServiceDispatcher工具，即可進行測試
您的設定不包含任何只會顯示在
部署：

### 步驟1:使用驗證器產生部署資訊

```
validator full -d out .
```

這將驗證完整配置並在`out`中生成部署資訊

### 步驟2:使用該部署資訊在Docker映像中啟動Dispatcher

當AEM發佈伺服器在macOS電腦上執行，並在連接埠4503上接聽時，
您可以依照下列方式，在該伺服器前面執行Dispatcher:

```
$ docker_run.sh out docker.for.mac.localhost:4503 8080
```

如此一來將啟動容器，並在本機連接埠 8080 上公開 Apache。

### 使用您的新Dispatcher設定

恭喜！ 如果驗證器不再回報任何問題，且
docker容器啟動時沒有任何故障或警告，您
準備將配置移至`dispatcher/src`子目錄
的URL。

**使用AMS Dispatcher設定1版的客戶應聯絡客戶支援，協助他們從第1版移轉至第2版，以便遵循上述指示。**
