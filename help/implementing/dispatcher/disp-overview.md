---
title: 雲端中的 Dispatcher
description: '雲端中的 Dispatcher '
translation-type: tm+mt
source-git-commit: 49b2f4abf64e404fcda7ea8d35e3ab9dc5fec90f
workflow-type: tm+mt
source-wordcount: '4119'
ht-degree: 8%

---


# 雲端中的 Dispatcher {#Dispatcher-in-the-cloud}

## Apache和Dispatcher配置和測試{#apache-and-dispatcher-configuration-and-testing}

本節說明如何將AEM架構為雲端服務Apache和Dispatcher組態，以及如何在部署至雲端環境之前在本機驗證並執行它。 此外，也說明在雲端環境中進行除錯。 有關Dispatcher的其他資訊，請參閱[AEM Dispatcher檔案](https://docs.adobe.com/content/help/zh-Hant/experience-manager-dispatcher/using/dispatcher.html)。

>[!NOTE]
>Windows使用者將需要使用Windows 10 Professional或其他支援Docker的散發版本。 這是在本地電腦上運行和調試Dispatcher的先決條件。 以下各節包含使用Mac或Linux版本SDK的命令，但Windows SDK也可以使用類似的方式。

## Dispatcher Tools {#dispatcher-sdk}

Dispatcher Tools是整體AEM的一部分，做為Cloud Service SDK，並提供：

* 一種Vanilla檔案結構，其包含要包含在調度程式的Maven項目中的配置檔案。
* 為客戶提供工具，以驗證分派器組態是否僅包含AEM作為雲端服務支援的指令。        此外，工具也會驗證語法是否正確，以便Apache能成功啟動。
* 將調度程式本地化的Docker映像。

## 下載並解壓工具{#extracting-the-sdk}

Dispatcher Tools是[AEM的一部分，是雲端服務SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)，可從[軟體散發](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html)入口網站的zip檔案下載。 該新Dispatcher Tools版本中提供的任何新設定都可用來部署至在Cloud或更高版本中執行該AEM版本的Cloud環境。

解壓縮SDK，此SDK搭售適用於macOS/Linux和Windows的Dispatcher Tools。

**對於macOS/Linux**，請使調度器工具對象可執行並運行它。它將自動將Dispatcher Tools檔案解壓到儲存到的目錄下（其中`version`是Dispatcher Tools的版本）。

```bash
$ chmod +x aem-sdk-dispatcher-tools-<version>-unix.sh
$ ./aem-sdk-dispatcher-tools-<version>-unix.sh
Verifying archive integrity...  100%   All good.
Uncompressing aem-sdk-dispatcher-tools-<version>-unix.sh 100%
```

**對於Windows**，請解壓縮Dispatcher Tooling郵遞區號封存。

## 檔案結構{#file-structure}

項目的調度程式子資料夾的結構如下所述，應將其複製到maven項目調度程式資料夾：

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

以下是可修改之顯著檔案的說明：

**可自訂的檔案**

可自訂下列檔案，並將在部署時傳送至您的Cloud實例：

* `conf.d/available_vhosts/<CUSTOMER_CHOICE>.vhost`

您可以擁有一個或多個這些檔案。 它們包含與主機名稱相符的`<VirtualHost>`條目，並允許Apache使用不同規則處理每個域通信。 檔案在`available_vhosts`目錄中建立，並在`enabled_vhosts`目錄中啟用符號連結。 在`.vhost`檔案中，將會包含其他檔案，例如重寫和變數。

* `conf.d/rewrites/rewrite.rules`

此檔案包含在`.vhost`檔案中。 它有一組`mod_rewrite`的重寫規則。

>[!NOTE]
>
>目前，必須使用單一重寫檔案，而非網站特定檔案。 該檔案大小必須小於1MB。

* `conf.d/variables/custom.vars`

此檔案包含在`.vhost`檔案中。 您可在此位置放入Apache變數的定義。

* `conf.d/variables/global.vars`

此檔案包含在`dispatcher_vhost.conf`檔案內。 您可以在此檔案中更改調度程式和重寫日誌級別。

* `conf.dispatcher.d/available_farms/<CUSTOMER_CHOICE>.farm`

您可以擁有一個或多個這些檔案，它們包含的群與主機名稱匹配，並允許調度程式模組使用不同的規則處理每個群。 檔案在`available_farms`目錄中建立，並在`enabled_farms`目錄中啟用符號連結。 在`.farm`檔案中，會包含其他檔案，例如篩選器、快取規則等。

* `conf.dispatcher.d/cache/rules.any`

此檔案包含在`.farm`檔案中。 它指定快取首選項。

* `conf.dispatcher.d/clientheaders/clientheaders.any`

此檔案包含在`.farm`檔案中。 它指定應將哪些請求標題轉送至後端。

* `conf.dispatcher.d/filters/filters.any`

此檔案包含在`.farm`檔案中。 它有一組規則，可變更應過濾掉的流量，而不會傳送到後端。

* `conf.dispatcher.d/virtualhosts/virtualhosts.any`

此檔案包含在`.farm`檔案中。 它包含要由全局匹配匹配的主機名或URI路徑的清單。 這會決定要使用哪些後端來支援請求。

上述檔案會參照下列不可變的設定檔案。 雲端環境中的調度程式不會處理不可變檔案的更改。

**不可變的配置檔案**

這些檔案是基本架構的一部分，並強制執行標準和最佳實務。 這些檔案被視為不可變，因為在本機修改或刪除檔案不會影響您的部署，因為它們不會傳輸至您的Cloud例項。

建議上述檔案參照下列不可變的檔案，後面接著任何其他陳述式或覆寫。 將Dispatcher配置部署到雲環境時，將使用不可變檔案的最新版本，而不管本地開發中使用的版本為何。

* `conf.d/available_vhosts/default.vhost`

包含一個示例虛擬主機。 對於您自己的虛擬主機，請建立此檔案的副本、對其進行自定義，轉到`conf.d/enabled_vhosts`並建立指向自定義副本的符號連結。

* `conf.d/dispatcher_vhost.conf`

基本框架的一部分，用於說明如何包括虛擬主機和全局變數。

* `conf.d/rewrites/default_rewrite.rules`

適用於標準專案的預設重寫規則。 如果需要自定義，請修改`rewrite.rules`。 在您的自訂中，如果預設規則符合您的需求，您仍可以先加入預設規則。

* `conf.dispatcher.d/available_farms/default.farm`

包含一個調度程式群示例。 對於您自己的農場，請建立此檔案的副本，對其進行自定義，轉至`conf.d/enabled_farms`並建立指向自定義副本的符號連結。

* `conf.dispatcher.d/cache/default_invalidate.any`

基本框架的一部分，在啟動時生成。 您是&#x200B;**required**&#x200B;的成員，可以在您定義的每個群中，在`cache/allowedClients`區段中包含此檔案。

* `conf.dispatcher.d/cache/default_rules.any`

適用於標準專案的預設快取規則。 如果需要自定義，請修改`conf.dispatcher.d/cache/rules.any`。 在您的自訂中，如果預設規則符合您的需求，您仍可以先加入預設規則。

* `conf.dispatcher.d/clientheaders/default_clientheaders.any`

適用於標準專案的預設請求標題，可轉送至後端。 如果需要自定義，請修改`clientheaders.any`。 在您的自訂中，如果預設請求標題符合您的需求，您仍可以先加入。

* `conf.dispatcher.d/dispatcher.any`

基本框架的一部分，用於說明如何包括您的調度程式群。

* `conf.dispatcher.d/filters/default_filters.any`

適用於標準專案的預設篩選器。 如果需要自定義，請修改`filters.any`。 在您的自訂中，如果預設篩選符合您的需求，您仍可以先加入預設篩選。

* `conf.dispatcher.d/renders/default_renders.any`

作為基本框架的一部分，此檔案在啟動時生成。 您是&#x200B;**required**&#x200B;的成員，可以在您定義的每個群中，在`renders`區段中包含此檔案。

* `conf.dispatcher.d/virtualhosts/default_virtualhosts.any`

適用於標準專案的預設主機回位。 如果需要自定義，請修改`virtualhosts.any`。 在您的自訂中，您不應包含預設的主機全域化，因為它符合&#x200B;**every**&#x200B;傳入的要求。

>[!NOTE]
>
>AEM（Cloud Service，雲端服務）主要原型將產生相同的分派程式設定檔案結構。

以下各節說明如何在本機驗證配置，以便在部署內部版本時，在Cloud Manager中傳遞相關的品質門。

## 在Dispatcher配置{#local-validation-of-dispatcher-configuration}中本地驗證支援的指令

驗證工具在SDK的`bin/validator`中以Mac OS、Linux或Windows二進位檔形式提供，讓客戶執行與Cloud Manager在建立和部署版本時所執行的相同驗證。

它被調用為：`validator full [-d folder] [-w allowlist] zip-file | src folder`

此工具會以模式`conf.d/enabled_vhosts/*.vhost`掃描所有檔案，以驗證分派程式設定是否使用AEM支援的適當指令做為雲端服務。 通過運行驗證器的allowlist命令，可以列出Apache配置檔案中允許的指令：

```
$ validator allowlist
Cloud manager validator 2.0.4
 
Allowlisted directives:
  <Directory>
  ...
  
```

下表顯示了支援的apache模組：

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
| `mod_remoteip` | [https://httpd.apache.org/docs/2.4/mod/mod_remoteip.html](https://httpd.apache.org/docs/2.4/mod/mod_remoteip.html) |
| `mod_reqtimeout` | [https://httpd.apache.org/docs/2.4/mod/mod_reqtimeout.html](https://httpd.apache.org/docs/2.4/mod/mod_reqtimeout.html) |
| `mod_rewrite` | [https://httpd.apache.org/docs/2.4/mod/mod_rewrite.html](https://httpd.apache.org/docs/2.4/mod/mod_rewrite.html) |
| `mod_security` | [https://modsecurity.org/](https://modsecurity.org/) |
| `mod_setenvif` | [https://httpd.apache.org/docs/2.4/mod/mod_setenvif.html](https://httpd.apache.org/docs/2.4/mod/mod_setenvif.html) |
| `mod_substitute` | [https://httpd.apache.org/docs/2.4/mod/mod_substitute.html](https://httpd.apache.org/docs/2.4/mod/mod_substitute.html) |
| `mod_userdir` | [https://httpd.apache.org/docs/2.4/mod/mod_userdir.html](https://httpd.apache.org/docs/2.4/mod/mod_userdir.html) |

客戶不能添加任意模組，但是將來可能會考慮將其他模組加入產品中。 如上所述，客戶可以在SDK中執行validator&#39;s allowlist命令，以找到指定Dispatcher版本可用的指令清單。

allowlist包含客戶配置中允許的Apache指令清單。 如果不允許列出指令，工具將記錄錯誤並返回非零的退出代碼。 如果命令行上未提供任何allowlist（即應調用該allowlist的方式），則該工具會使用Cloud Manager在部署至Cloud環境之前用於驗證的預設allowlist。

此外，它還會進一步掃描模式為`conf.dispatcher.d/enabled_farms/*.farm`的所有檔案並檢查：

* 沒有透過`/glob`允許使用的篩選規則（如需詳細資訊，請參閱[CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957)）
* 未公開任何管理功能。 例如，存取路徑，例如`/crx/de or /system/console`。

對maven對象或`dispatcher/src`子目錄運行時，將報告驗證失敗：

```
$ validator full dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-allowlisted directives:
  conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
  conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

請注意，驗證工具僅報告未允許列出的禁止使用Apache指令。 它不會報告Apache配置的語法或語義問題，因為此資訊僅適用於運行環境中的Apache模組。

以下是用於調試工具輸出的常見驗證錯誤的故障排除技術：

**在存檔中找 `conf.dispatcher.d` 不到子資料夾**

您的封存應包含資料 `conf.d` 夾和 `conf.dispatcher.d`。請注意，您不 **應**&#x200B;在封 `etc/httpd` 存中使用首碼。

**找不到`conf.dispatcher.d/enabled_farms`**

啟用的場應位於上述子資料夾中。

**包含的檔案(...)必須命名：...**

您的農場配置中有兩個部分&#x200B;**must**包含a
特定檔案：`/cache`區段中的`/renders`和`/allowedClients`。 那些
章節必須如下所示：

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

**檔案包含於未知位置：...**

農場配置中有四個部分，允許您在其中包含自己的檔案：`/clientheaders`、`filters`、`/rules`在`/cache`區段和`/virtualhosts`區段中。 所包含的檔案需命名如下：

| 章節 | 包含檔案名 |
|------------------|--------------------------------------|
| `/clientheaders` | `../clientheaders/clientheaders.any` |
| `/filters` | `../filters/filters.any` |
| `/rules` | `../cache/rules.any` |
| `/virtualhosts` | `../virtualhosts/virtualhosts.any` |

或者，您也可以包含 **這些檔案的預設版本** ，其名稱會以字詞 `default_`為前置詞，例如。`../filters/default_filters.any`。

**在任何已知位置之外包含語句(...):...**

除上文各段所述之六節外，您不得
要使用`$include`語句，例如，以下語句將生成此錯誤：

```
/invalidate {
    $include "../cache/invalidate.any"
}
```

**允許的客戶端／呈現不包括於：...**

當您未在`/cache`區段中指定`/renders`和`/allowedClients`的包含時，就會產生此錯誤。 請參閱
包含的**檔案(...)必須命名：...**&#x200B;章節，以取得詳細資訊。

**篩選不得使用全域模式以允許請求**

允許具有`/glob`樣式規則的請求是不安全的，該規則與完整的請求行匹配，例如：

```
/0100 {
    /type "allow" /glob "GET *.css *"
}
```

此語句的用意是允許對`css`檔案的請求，但也允許對&#x200B;**任何**&#x200B;資源的請求，後面跟著查詢字串`?a=.css`。 因此，禁止使用此類篩選器（另請參閱CVE-2016-0957）。

**包含的檔案(...)與任何已知檔案不匹配**

Apache虛擬主機配置中有兩種類型的檔案可指定為包括：重寫和變數。
所包含的檔案需命名如下：

| 類型 | 包含檔案名 |
|-----------|---------------------------------|
| 重寫 | `conf.d/rewrites/rewrite.rules` |
| 變數 | `conf.d/variables/custom.vars` |

或者，您也可以包含重寫規則的&#x200B;**default**&#x200B;版本，其名稱為`conf.d/rewrites/default_rewrite.rules`。
請注意，變數檔案沒有預設版本。

**檢測到不建議使用的配置佈局，啟用相容模式**

此訊息指出您的設定已停用第1版配置，包含完整版
具有`ams_`前置詞的Apache配置和檔案。 雖然這仍支援向後
相容性，您應切換至新版面。

## 本地驗證調度程式配置語法，以便apache httpd可以啟動{#local-validation}

在確定分發程式模組配置僅包含受支援指令後，您應檢查語法是否正確，以便Apache能夠啟動。 為了測試此功能，Docker必須安裝在本地。 請注意，AEM不需要執行。

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

指令碼執行下列操作：

1. 它從上一節運行驗證器，以確保僅包含受支援的指令。 如果配置無效，則指令碼將失敗。
2. 它會執行`httpd -t command`以測試語法是否正確，以便Apache httpd可以啟動。 如果成功，配置應準備好進行部署。
3. 檢查未修改發送器SDK配置檔案的子集（如[檔案結構部分](#file-structure)所述）。 這是AEM SDK v2021.1.4738版新增的檢查，其中也包含Dispatcher Tools 2.0.36版。在此更新之前，客戶可能錯誤地認為這些不可變檔案的任何本機SDK修改也會套用至雲端環境。

在Cloud Manager部署期間，`httpd -t syntax`檢查也會執行，Cloud Manager `Build Images step failure`記錄檔中會包含任何錯誤。

## 在本地測試Apache和Dispatcher配置{#testing-apache-and-dispatcher-configuration-locally}

您也可以在本機測試Apache和Dispatcher配置。 它要求在本機安裝Docker，而您的配置必須如上所述通過驗證。

使用`-d`參數（該參數輸出包含所有調度程式配置檔案的資料夾），執行驗證器工具（請注意，它與前面提到的`validator.sh`不同）。 然後執行`docker_run.sh`指令碼，將該資料夾傳遞為引數。 通過提供埠號(此處：8080)，以公開發送程式端點，將啟動Docker容器，使用您的配置運行發送程式。

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

這會在容器中啟動Dispatcher，其後端會指向在您本機Mac OS機器上執行的AEM例項，埠為4503。

## 調試Apache和Dispatcher配置{#debugging-apache-and-dispatcher-configuration}

以下策略可用於增加調度器模組的日誌輸出，並查看本地和雲環境中`RewriteRule`評估的結果。

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

在本地運行調度程式時，日誌將直接打印到終端輸出。 大部分時候，您都希望這些記錄檔在DEBUG中，這可在執行Docker時將Debug層級傳入為參數。 例如：`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`。

雲端環境的記錄檔會透過Cloud Manager中提供的記錄服務公開。

## 每個環境{#different-dispatcher-configurations-per-environment}的不同Dispatcher配置

目前，相同的Dispatcher設定會套用至所有AEM做為雲端服務環境。 運行時將具有環境變數`ENVIRONMENT_TYPE`，其中包含當前運行模式（dev、stage或prod）以及定義。 定義可以是`ENVIRONMENT_DEV`、`ENVIRONMENT_STAGE`或`ENVIRONMENT_PROD`。 在Apache設定中，變數可直接用於運算式中。 或者，可使用定義來建立邏輯：

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

在Dispatcher配置中，可以使用相同的環境變數。 如果需要更多邏輯，請定義上述示例中所示的變數，然後在Dispatcher配置部分中使用這些變數：

```
/virtualhosts {
  { "${VIRTUALHOST}" }
}
```

在本機測試配置時，可以通過直接將變數`DISP_RUN_MODE`傳遞到`docker_run.sh`指令碼來模擬不同的環境類型：

```
$ DISP_RUN_MODE=stage docker_run.sh out docker.for.mac.localhost:4503 8080
```

未傳入DISP_RUN_MODE值時的預設運行模式為「dev」。
有關可用選項和變數的完整清單，請運行不帶參數的指令碼`docker_run.sh`。

## 查看Docker容器{#viewing-dispatcher-configuration-in-use-by-docker-container}正在使用的Dispatcher配置

使用特定於環境的配置時，可能很難確定實際的Dispatcher配置的外觀。 使用`docker_run.sh`啟動Docker容器後，可以按如下方式轉儲該容器：

* 確定正在使用的Docker容器ID:

```
$ docker ps
CONTAINER ID       IMAGE
d75fbd23b29        adobe/aem-ethos/dispatcher-publish:...
```

* 使用該容器ID執行下列命令列：

```
$ docker exec d75fbd23b29 httpd-test
# Dispatcher configuration: (/etc/httpd/conf.dispatcher.d/dispatcher.any)
/farms {
  /publishfarm {
    /clientheaders {
...
```

## AMS Dispatcher與AEM作為雲端服務的主要差異{#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

如上述參考頁面所述，AEM中Apache和Dispatcher的Cloud Service組態與AMS組態非常類似。 主要差異是：

* 在AEM中，某些Apache指令可能不會使用（例如`Listen`或`LogLevel`）
* 在AEM中，Dispatcher設定只能放入部分項目，其命名很重要。 例如，您要在不同主機間重複使用的篩選規則必須放入名為`filters/filters.any`的檔案中。 如需詳細資訊，請參閱參考頁面。
* 在AEM中，「雲端服務」中有額外的驗證，可禁止使用`/glob`撰寫的篩選規則，以防止發生安全性問題。 由於`deny *`將被使用，而不是`allow *`（不能使用），因此客戶將從在本地運行Dispatcher以及執行試用和錯誤中獲益，查看日誌以確切知道Dispatcher篩選器為了添加這些篩選器而阻塞的路徑。

## 將Dispatcher組態從AMS移轉至AEM做為雲端服務的准則

Dispatcher配置結構在Managed Services和AEM（即雲服務）之間有差異。 以下是如何從AMS Dispatcher設定第2版移轉至AEM做為雲端服務的逐步指南。

## 如何將AMS轉換為AEM做為Cloud服務分派程式設定

下節提供如何轉換AMS配置的逐步說明。 它假設
具有與[Cloud Manager Dispatcher configuration](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)中所述結構類似的歸檔檔案

### 提取封存並移除最終首碼

將存檔解壓到資料夾，並確保立即的子資料夾以`conf`、`conf.d`開頭，
`conf.dispatcher.d`和`conf.modules.d`。 如果他們沒有，請在階層中向上移動。

### 移除未使用的子資料夾和檔案

移除子檔案夾`conf`和`conf.modules.d`，以及符合`conf.d/*.conf`的檔案。

### 移除所有非發佈用的虛擬主機

刪除`conf.d/enabled_vhosts`中具有`author`、`unhealthy`、`health`、
`lc`或`flush`。 `conf.d/available_vhosts`中所有非
連結至的項目也可移除。

### 移除或註解未引用連接埠 80 的虛擬主機區段

如果您的虛擬主機檔案中，仍有區段單獨引用連接埠 80 以外的連接埠，例如：

```
<VirtualHost *:443>
...
</VirtualHost>
```


請移除或加上註解。系統將不會處理這些區段中的陳述式，但如果您保留這些陳述式，您最終可能仍會編輯，但將徒勞無功而倍感困惑。

### 檢查重新寫入

輸入`conf.d/rewrites`目錄。

刪除任何名為`base_rewrite.rules`和`xforwarded_forcessl_rewrite.rules`的檔案，並記住
在引用`Include`語句的虛擬主機檔案中刪除語句。

如果`conf.d/rewrites`現在包含單一檔案，則應將它重新命名為`rewrite.rules`，而不要
忘記在虛擬主機檔案中調整引用該檔案的`Include`語句。

如果資料夾包含多個虛擬主機特定的檔案，則其內容應為
複製到虛擬主機檔案中引用`Include`語句的語句。

### 檢查變數

輸入`conf.d/variables`目錄。

刪除名為`ams_default.vars`的任何檔案，並記得刪除虛擬檔案中的`Include`語句
代表其的主機檔案。

如果`conf.d/variables`現在包含單一檔案，則應將它重新命名為`custom.vars`，而不要
忘記在虛擬主機檔案中調整引用該檔案的`Include`語句。

如果資料夾包含多個虛擬主機特定的檔案，則其內容應為
複製到虛擬主機檔案中引用`Include`語句的語句。

### 刪除允許清單

刪除虛擬主機檔案中引用的`conf.d/whitelists`資料夾和`Include`語句
子資料夾中的檔案。

### 取代任何已無法使用的變數

在所有虛擬主機檔案中：

將`PUBLISH_DOCROOT`重新命名為`DOCROOT`
移除引用名為`DISP_ID`、`PUBLISH_FORCE_SSL`或`PUBLISH_WHITELIST_ENABLED`之變數的區段

### 執行驗證器以檢查狀態

使用`httpd`子命令在目錄中運行dispatcher validator:

```
$ validator httpd .
```

如果您看見有關遺失 Include 檔案的錯誤，請檢查您是否已正確地重新命名那些檔案。

如果您看到未列出的Apache指令，請將其刪除。

### 移除所有非發佈用的伺服器陣列

刪除`conf.dispatcher.d/enabled_farms`中具有`author`、`unhealthy`、`health`、
`lc`或`flush`。 `conf.dispatcher.d/available_farms`中所有非
連結至的項目也可移除。

### 重新命名伺服器陣列檔案

`conf.d/enabled_farms`中的所有場都必須重新命名，以符合模式`*.farm`，例如a
名為`customerX_farm.any`的農場檔案應更名為`customerX.farm`。

### 檢查快取

輸入`conf.dispatcher.d/cache`目錄。

移除任何以「`ams_`」為首碼的檔案。

如果`conf.dispatcher.d/cache`現在為空，則複製檔案`conf.dispatcher.d/cache/rules.any`
從標準調度程式配置到此資料夾。 標準調度程式
此SDK的`src`資料夾中可找到設定。 別忘了要調整
`$include`語句引用群檔案中的`ams_*_cache.any`規則檔案
還有。

如果`conf.dispatcher.d/cache`現在包含尾碼為`_cache.any`的單一檔案，
它應重新命名為`rules.any`，且不要忘記改變`$include`陳述式
也參照農場檔案中的該檔案。

但是，如果資料夾包含多個具有該模式的群特定檔案，則其內容
應複製到群檔案中參照它們的`$include`語句。

刪除尾碼為`_invalidate_allowed.any`的任何檔案。

從預設位置複製檔案`conf.dispatcher.d/cache/default_invalidate_any`
Cloud Dispatcher設定中的AEM。

在每個群檔案中，刪除`cache/allowedClients`部分中的所有內容並將其替換
with:

```
$include "../cache/default_invalidate.any"
```

### 檢查用戶端標頭

輸入`conf.dispatcher.d/clientheaders`目錄。

移除任何以「`ams_`」為首碼的檔案。

如果`conf.dispatcher.d/clientheaders`現在包含尾碼為`_clientheaders.any`的單個檔案，
它應重新命名為`clientheaders.any`，且不要忘記改變`$include`陳述式
也參照農場檔案中的該檔案。

但是，如果資料夾包含多個具有該模式的群特定檔案，則其內容
應複製到群檔案中參照它們的`$include`語句。

從預設位置複製檔案`conf.dispatcher/clientheaders/default_clientheaders.any`
AEM做為該位置的Cloud Service分派程式設定。

在每個伺服器陣列檔案中，取代任何如下所示的「clientheader include」陳述式：

```
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"
```

以及以下陳述式：

```
$include "../clientheaders/default_clientheaders.any"
```

### 檢查篩選器

輸入`conf.dispatcher.d/filters`目錄。

移除任何以「`ams_`」為首碼的檔案。

如果`conf.dispatcher.d/filters`現在包含單一檔案，則應將其重新命名為
`filters.any`，且別忘了改變`$include`陳述式，並參照該陳述式
檔案。

但是，如果資料夾包含多個具有該模式的群特定檔案，則其內容
應複製到群檔案中參照它們的`$include`語句。

從預設位置複製檔案`conf.dispatcher/filters/default_filters.any`
AEM做為該位置的Cloud Service分派程式設定。

在每個伺服器陣列檔案中，取代任何如下所示的 filter include 陳述式：

```
$include "/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"
```

以及以下陳述式：

```
$include "../filters/default_filters.any"
```

### 檢查轉譯

輸入`conf.dispatcher.d/renders`目錄。

移除該資料夾中的所有檔案。

從預設位置複製檔案`conf.dispatcher.d/renders/default_renders.any`
AEM做為該位置的Cloud Service分派程式設定。

在每個群檔案中，刪除`renders`部分中的所有內容並將其替換
with:

```
$include "../renders/default_renders.any"
```

### 檢查虛擬主機

將目錄`conf.dispatcher.d/vhosts`更名為`conf.dispatcher.d/virtualhosts`並輸入。

移除任何以「`ams_`」為首碼的檔案。

如果`conf.dispatcher.d/virtualhosts`現在包含單一檔案，則應將其重新命名為
`virtualhosts.any`，且別忘了改變`$include`陳述式，並參照該陳述式
檔案。

但是，如果資料夾包含多個具有該模式的群特定檔案，則其內容
應複製到群檔案中參照它們的`$include`語句。

從預設位置複製檔案`conf.dispatcher/virtualhosts/default_virtualhosts.any`
AEM做為該位置的Cloud Service分派程式設定。

在每個伺服器陣列檔案中，取代任何如下所示的 filter include 陳述式：

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

以及以下陳述式：

```
$include "../virtualhosts/default_virtualhosts.any"
```

### 執行驗證器以檢查狀態

使用`dispatcher`子命令，在您的目錄中以Cloud Service Dispatcher Validator身分執行AEM:

```
$ validator dispatcher .
```

如果您看見有關遺失 Include 檔案的錯誤，請檢查您是否已正確地重新命名那些檔案。

如果您看見有關未定義變數「`PUBLISH_DOCROOT`」的錯誤，請將其重新命名為「`DOCROOT`」。

如果看見其他錯誤，請參考驗證器工具文件的疑難排解章節。

### 使用本機部署測試您的組態（需要安裝Docker）

使用AEM中的指令碼`docker_run.sh`做為Cloud Service Dispatcher Tools，您可以測試
您的設定不包含任何其他只會顯示在
部署：

### 步驟1:使用驗證器生成部署資訊

```
validator full -d out .
```

這將驗證完整配置並在`out`中生成部署資訊

### 步驟2:使用部署資訊在Docker映像中啟動調度程式

在您的 macOS 電腦上執行 AEM 發佈伺服器，並在連接埠 4503 上接聽後，即可在該伺服器前端執行 Dispatcher，如下所示：

```
$ docker_run.sh out docker.for.mac.localhost:4503 8080
```

如此一來將啟動容器，並在本機連接埠 8080 上公開 Apache。

### 使用您的新調度程式配置

恭喜！ 如果驗證器不再報告任何問題，則
docker容器啟動時沒有任何故障或警告，您
準備將配置移動到`dispatcher/src`子目錄
Git儲存庫。

**使用AMS Dispatcher配置第1版的客戶應聯繫客戶支援以幫助他們從第1版遷移到第2版，以便遵循上述說明。**
