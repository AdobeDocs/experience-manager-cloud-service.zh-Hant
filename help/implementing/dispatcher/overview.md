---
title: 雲端中的 Dispatcher
description: '雲端中的 Dispatcher '
translation-type: tm+mt
source-git-commit: 00912ea1085da2c50ec79ac35bd53d36fd8a9509

---


# 雲端中的 Dispatcher {#Dispatcher-in-the-cloud}

## Apache和Dispatcher組態與測試 {#apache-and-dispatcher-configuration-and-testing}

本節說明如何將AEM架構為雲端服務Apache和Dispatcher組態，以及如何在部署至雲端環境之前在本機驗證並執行它。 此外，也說明在雲端環境中進行除錯。 如需Dispatcher的其他資訊，請參閱 [AEM Dispatcher檔案](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/dispatcher.html)。

>[!NOTE]
>Windows使用者將需要使用Windows 10 Professional或其他支援Docker的散發版本。 這是在本地電腦上運行和調試Dispatcher的先決條件。 以下各節包含使用Mac或Linux版本SDK的命令，但Windows SDK也可以使用類似的方式。

## Dispatcher Tools {#dispatcher-sdk}

Dispatcher Tools是整體AEM的一部分，做為Cloud Service SDK，並提供：

* 一種Vanilla檔案結構，其中包含要包含在調度器的Maven項目中的配置檔案；
* 為客戶在本地驗證調度程式配置提供工具；
* 將調度程式本地化的Docker映像。

## 下載並擷取工具 {#extracting-the-sdk}

Dispatcher Tools可從Software Distribution Portal的zip檔案 [下載](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html) 。 請注意，SDK清單的存取權限僅限於AEM Managed Services或AEM做為雲端服務環境的使用者。 此新Dispatcher Tools版本中提供的任何新設定都可用來部署至在Cloud或更高版本中執行該AEM版本的Cloud環境。

**對於macOS和Linux**，請將shell指令碼下載至您電腦上的檔案夾，讓它可執行並執行。 它將自動解壓儲存在目錄下的Dispatcher Tools檔案(其中 `version` 是Dispatcher Tools的版本)。

```bash
$ chmod +x DispatcherSDKv<version>.sh
$ ./DispatcherSDKv<version>.sh
Verifying archive integrity...  100%   All good.
Uncompressing DispatcherSDKv<version>  100% 
```

**若是Windows**，請下載zip封存並解壓縮。

## 檔案結構 {#file-structure}

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

您可以擁有一個或多個這些檔案。 它們包 `<VirtualHost>` 含符合主機名稱的項目，並允許Apache使用不同規則處理每個網域流量。 檔案在目錄中創 `available_vhosts` 建，並在目錄中啟用符號鏈 `enabled_vhosts` 接。 從檔案 `.vhost` 中，將會包含其他檔案，例如重寫和變數。

* `conf.d/rewrites/rewrite.rules`

此檔案會從您的檔案中包 `.vhost` 含。 它有一組重寫規則 `mod_rewrite`。

>[!NOTE]
>
>目前，必須使用單一重寫檔案，而非網站特定檔案。 該檔案大小必須小於1MB。

* `conf.d/variables/custom.vars`

此檔案會從您的檔案中包 `.vhost` 含。 您可以在此位置放入Apache變數的定義。

* `conf.d/variables/global.vars`

此檔案會從檔案中包 `dispatcher_vhost.conf` 含。 您可以在此檔案中更改調度程式和重寫日誌級別。

* `conf.dispatcher.d/available_farms/<CUSTOMER_CHOICE>.farm`

您可以擁有一個或多個這些檔案，它們包含的群與主機名稱匹配，並允許調度程式模組使用不同的規則處理每個群。 檔案在目錄中創 `available_farms` 建，並在目錄中啟用符號鏈 `enabled_farms` 接。 從檔案 `.farm` 中，會包含其他檔案，例如篩選器、快取規則等。

* `conf.dispatcher.d/cache/rules.any`

此檔案會從您的檔案中包 `.farm` 含。 它指定快取首選項。

* `conf.dispatcher.d/clientheaders/clientheaders.any`

此檔案會從您的檔案中包 `.farm` 含。 它指定應將哪些請求標題轉送至後端。

* `conf.dispatcher.d/filters/filters.any`

此檔案會從您的檔案中包 `.farm` 含。 它有一組規則，可變更應過濾掉的流量，而不會傳送到後端。

* `conf.dispatcher.d/virtualhosts/virtualhosts.any`

此檔案會從您的檔案中包 `.farm` 含。 它包含要由全局匹配匹配的主機名或URI路徑的清單。 這會決定要使用哪些後端來支援請求。

上述檔案會參照下列不可變的設定檔案。 雲端環境中的調度程式不會處理不可變檔案的更改。

**不可變的配置檔案**

這些檔案是基本架構的一部分，並強制執行標準和最佳實務。 這些檔案被視為不可變，因為在本機修改或刪除檔案不會影響您的部署，因為它們不會傳輸至您的Cloud例項。

建議上述檔案參照下列不可變的檔案，後面接著任何其他陳述式或覆寫。 將Dispatcher配置部署到雲環境時，將使用不可變檔案的最新版本，而不管本地開發中使用的版本為何。

* `conf.d/available_vhosts/default.vhost`

包含一個示例虛擬主機。 對於您自己的虛擬主機，請建立此檔案的副本、對其進行自定義、轉 `conf.d/enabled_vhosts` 到並建立指向自定義副本的符號連結。

* `conf.d/dispatcher_vhost.conf`

基本框架的一部分，用於說明如何包括虛擬主機和全局變數。

* `conf.d/rewrites/default_rewrite.rules`

適用於標準專案的預設重寫規則。 如果需要自定義，請修改 `rewrite.rules`。 在您的自訂中，如果預設規則符合您的需求，您仍可以先加入預設規則。

* `conf.dispatcher.d/available_farms/default.farm`

包含一個調度程式群示例。 針對您自己的農場，請建立此檔案的副本、加以自訂、前往並 `conf.d/enabled_farms` 建立自訂副本的符號連結。

* `conf.dispatcher.d/cache/default_invalidate.any`

基本框架的一部分，在啟動時生成。 您必 **須在** 「區段」中，將此檔案加入您定義的每個農場 `cache/allowedClients` 中。

* `conf.dispatcher.d/cache/default_rules.any`

適用於標準專案的預設快取規則。 如果需要自定義，請修改 `conf.dispatcher.d/cache/rules.any`。 在您的自訂中，如果預設規則符合您的需求，您仍可以先加入預設規則。

* `conf.dispatcher.d/clientheaders/default_clientheaders.any`

適用於標準專案的預設請求標題，可轉送至後端。 如果需要自定義，請修改 `clientheaders.any`。 在您的自訂中，如果預設請求標題符合您的需求，您仍可以先加入。

* `conf.dispatcher.d/dispatcher.any`

基本框架的一部分，用於說明如何包括您的調度程式群。

* `conf.dispatcher.d/filters/default_filters.any`

適用於標準專案的預設篩選器。 如果需要自定義，請修改 `filters.any`。 在您的自訂中，如果預設篩選符合您的需求，您仍可以先加入預設篩選。

* `conf.dispatcher.d/renders/default_renders.any`

作為基本框架的一部分，此檔案在啟動時生成。 您必 **須在** 「區段」中，將此檔案加入您定義的每個農場 `renders` 中。

* `conf.dispatcher.d/virtualhosts/default_virtualhosts.any`

適用於標準專案的預設主機回位。 如果需要自定義，請修改 `virtualhosts.any`。 在您的自訂中，您不應包含預設的主機全域化，因為它符合每 **個傳** 入請求。

>[!NOTE]
>AEM（Cloud Service，雲端服務）主要原型將產生相同的分派程式設定檔案結構。

以下各節說明如何在本機驗證配置，以便在部署內部版本時，在Cloud Manager中傳遞相關的品質門。

## Dispatcher配置的本地驗證 {#local-validation-of-dispatcher-configuration}

驗證工具可在SDK中以Mac OS、Linux或Windows二進位格式取得，讓客戶執行與Cloud Manager在建立和部署版本時所執行的驗證相同。 `bin/validator`

它被調用為： `validator full [-d folder] [-w whitelist] zip-file | src folder`

此工具會驗證Apache和Dispatcher組態。 它使用模式掃描所有文 `conf.d/enabled_vhosts/*.vhost` 件，並檢查是否只使用白名單指令。 通過運行驗證器的白名單命令，可以列出Apache配置檔案中允許的指令：

```
$ validator whitelist
Cloud manager validator 2.0.4
 
Whitelisted directives:
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
| `mod_auth_basic` | [https://httpd.apache.org/docs/2.4/mod/mod_auth_basic.html](https://httpd.apache.org/docs/2.4/mod/mod_auth_basic.html) |
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

客戶不能添加任意模組，但是將來可能會考慮將其他模組加入產品中。 如Dispatcher Tools文檔中所述，客戶可以在SDK中執行「驗證器白名單」，以查找指定Dispatcher版本可用的指令清單。

白名單包含客戶配置中允許的Apache指令清單。 如果指令未列入白名單，則工具會記錄錯誤並傳回非零的退出代碼。 如果命令行上沒有提供白名單（這是調用白名單的方式），則該工具會使用預設白名單，Cloud Manager將在部署到雲環境之前用於驗證。

此外，它還會進一步掃描所有具有模式的 `conf.dispatcher.d/enabled_farms/*.farm` 檔案並檢查：

* 沒有使用允許透過的篩選規 `/glob` 則(如需詳細 [資訊，請參閱CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957) )
* 未公開任何管理功能。 例如，存取路徑，例如 `/crx/de or /system/console`。

對maven對象或子目錄運行時， `dispatcher/src` 將報告驗證失敗：

```
$ validator full dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-whitelisted directives:
 conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
 conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

請注意，驗證工具僅報告未列入白名單的Apache指令的禁止使用。 它不會報告Apache配置的語法或語義問題，因為此資訊僅適用於運行環境中的Apache模組。

當未報告任何驗證失敗時，您的設定就可進行部署。

以下是用於調試工具輸出的常見驗證錯誤的故障排除技術：

**在存檔中找`conf.dispatcher.d`不到子資料夾**

您的封存應包含資料 `conf.d` 夾和 `conf.dispatcher.d`。請注意，您不 **應**&#x200B;在封 `etc/httpd` 存中使用首碼。

**找不到`conf.dispatcher.d/enabled_farms`**

啟用的場應位於上述子資料夾中。

**包含的檔案(...)必須命名：...**

您的農場配置中有兩個部分必須 **包含** : `/renders` 和 `/allowedClients` 部分 `/cache` 中。 這些區段必須如下所示：

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

農場配置中有四個部分，允許您在其中包含自己的檔案：, `/clientheaders``filters`, `/rules` section and `/cache``/virtualhosts`所包含的檔案需命名如下：

| 章節 | 包含檔案名 |
|------------------|--------------------------------------|
| `/clientheaders` | `../clientheaders/clientheaders.any` |
| `/filters` | `../filters/filters.any` |
| `/rules` | `../cache/rules.any` |
| `/virtualhosts` | `../virtualhosts/virtualhosts.any` |

或者，您也可以包含 **這些檔案的預設版本** ，其名稱會以字詞 `default_`為前置詞，例如。`../filters/default_filters.any`。

**在任何已知位置之外包含語句(...):...**

除上文各段提及的六個部分外，您不得使用該 `$include` 陳述，例如，以下內容會產生此錯誤：

```
/invalidate {
    $include "../cache/invalidate.any"
}
```

**允許的客戶端／呈現不包括於：...**

當您未在區段中指定包含時，就會 `/renders` 產生 `/allowedClients` 此 `/cache` 錯誤。 請參閱&#x200B;**包含的檔案(...)必須命名：...** 的子菜單。

**篩選不得使用全域模式以允許請求**

允許具有樣式規則的請求是不安全的， `/glob` 該樣式規則與完整的請求行匹配，例如，

```
/0100 {
    /type "allow" /glob "GET *.css *"
}
```

此語句的用意是允許對檔案 `css` 的請求，但也允許對任何 **資源** （後跟查詢字串）的請求 `?a=.css`。 因此，禁止使用此類篩選器（另請參閱CVE-2016-0957）。

**包含的檔案(...)與任何已知檔案不匹配**

Apache虛擬主機配置中有兩種類型的檔案可指定為包括：重寫和變數。
所包含的檔案需命名如下：

| 類型 | 包含檔案名 |
|-----------|---------------------------------|
| 重寫 | `conf.d/rewrites/rewrite.rules` |
| 變數 | `conf.d/variables/custom.vars` |

或者，您也可以包含 **重寫規則** (其名稱為 `conf.d/rewrites/default_rewrite.rules`)的預設版本。
請注意，變數檔案沒有預設版本。

**檢測到不建議使用的配置佈局，啟用相容模式**

此消息表示您的配置具有不建議使用的1版佈局，其中包含完整的Apache配置和帶前置詞的 `ams_` 檔案。 雖然這仍受支援，但是您應切換至新版面。

## 在本機測試您的Apache和Dispatcher配置 {#testing-apache-and-dispatcher-configuration-locally}

您也可以在本機測試Apache和Dispatcher配置。 它要求本機安裝Docker，而您的組態必須如上所述通過驗證。

通過使用&quot;`-d`&quot;參數，驗證器將輸出包含調度程式所需的所有配置檔案的資料夾。

然後，指 `docker_run.sh` 令碼可指向該資料夾，從您的設定開始。

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

## 調試Apache和Dispatcher配置 {#debugging-apache-and-dispatcher-configuration}

以下策略可用於增加調度器模組的日誌輸出，並查看本地和雲環境 `RewriteRule` 中評估結果。

這些模組的日誌級別由變數和定 `DISP_LOG_LEVEL` 義 `REWRITE_LOG_LEVEL`。 可在檔案中設定這些值 `conf.d/variables/global.vars`。 其相關部分如下：

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

在本地運行Dispatcher時，日誌也直接打印到終端輸出。 大部分時間，這些記錄檔應該在DEBUG中，這可以在執行Docker時，將Debug層級傳入為參數來完成。 例如：

`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`

雲端環境的記錄檔將透過Cloud Manager中提供的記錄服務公開。

## 每個環境的不同Dispatcher配置 {#different-dispatcher-configurations-per-environment}

目前，相同的Dispatcher設定會套用至所有AEM做為雲端服務環境。 運行時將具有一個環境變 `ENVIRONMENT_TYPE` 量，其中包含當前運行模式（dev、stage或prod）以及定義。 定義可以是 `ENVIRONMENT_DEV`或 `ENVIRONMENT_STAGE` 或 `ENVIRONMENT_PROD`。 在Apache設定中，變數可直接用於運算式中。 或者，可使用定義來建立邏輯：

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

在本機測試配置時，您可以直接將變數傳遞至指令碼，以模擬 `DISP_RUN_MODE` 不同的 `docker_run.sh` 環境類型：

```
$ DISP_RUN_MODE=stage docker_run.sh out docker.for.mac.localhost:4503 8080
```

未傳入DISP_RUN_MODE值時的預設運行模式為「dev」。
如需可用選項和變數的完整清單，請執行不含引數 `docker_run.sh` 的指令碼。

## 查看Docker容器正在使用的Dispatcher配置 {#viewing-dispatcher-configuration-in-use-by-docker-container}

使用特定於環境的配置時，可能很難確定實際的Dispatcher配置的外觀。 在啟動您的Docker容器後，可 `docker_run.sh` 以按如下方式將其轉儲：

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

## AMS Dispatcher與AEM作為雲端服務的主要差異 {#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

如上述參考頁面所述，AEM中Apache和Dispatcher的Cloud Service組態與AMS組態非常類似。 主要差異是：

* 在AEM中，某些Apache指令不得使用(例如 `Listen` 或 `LogLevel`)
* 在AEM中，Dispatcher設定只能放入部分項目，其命名很重要。 例如，您要在不同主機間重複使用的篩選規則必須放入名為的檔案中 `filters/filters.any`。 如需詳細資訊，請參閱參考頁面。
* 在AEM中，「雲端服務」中有額外的驗證，可禁止使用撰寫的篩選規則來 `/glob` 防止安全性問題。 由於 `deny *` 將使用而不是 `allow *` （不能使用），因此客戶將從在本地運行Dispatcher以及執行試用和錯誤中獲益，查看日誌以確切知道Dispatcher篩選器為了添加這些篩選器而阻塞的路徑。

## 將Dispatcher組態從AMS移轉至AEM做為雲端服務的准則

Dispatcher配置結構在Managed Services和AEM（即雲服務）之間有差異。 以下是如何從AMS Dispatcher設定第2版移轉至AEM做為雲端服務的逐步指南。

## 如何將AMS轉換為AEM做為Cloud服務分派程式設定

下節提供如何轉換AMS配置的逐步說明。 假定您的存檔具有類似於 [Cloud Manager Dispatcher配置中所述的結構](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)

### 解壓縮封存並移除最終首碼

將檔案解壓縮至檔案夾，並確定立即的子檔案夾以 `conf`、 `conf.d``conf.dispatcher.d` 、和開頭 `conf.modules.d`。 如果他們沒有，請在階層中向上移動。

### 移除未儲存的子檔案夾和檔案

移除子檔 `conf` 案夾 `conf.modules.d`和，以及符合的檔案 `conf.d/*.conf`。

### 移除所有非發佈的虛擬主機

刪除名稱中包 `conf.d/enabled_vhosts` 含、 `author`、 `unhealthy``health``lc``flush` 或任何虛擬主機檔案。 所有未連結到 `conf.d/available_vhosts` 的虛擬主機檔案也可以刪除。

### 刪除或注釋不引用埠80的虛擬主機部分

如果您的虛擬主機檔案中仍然有專門引用埠80以外的埠的部分，例如

```
<VirtualHost *:443>
...
</VirtualHost>
```

移除或加上註解。 這些章節中的陳述式將不會被處理，但是，如果您保留這些陳述式，您最後可能仍會編輯這些陳述式，而不會產生任何效果，這會令人困惑。

### 檢查重寫

Enter directory `conf.d/rewrites`.

刪除名為和的任 `base_rewrite.rules` 何文 `xforwarded_forcessl_rewrite.rules` 件，並記住刪除 `Include` 虛擬主機檔案中引用它們的語句。

如果 `conf.d/rewrites` 現在包含單一檔案，則應重新命名為 `rewrite.rules` ，而且不要忘記在虛擬主機 `Include` 檔案中也參照該檔案的陳述式。

但是，如果資料夾包含多個虛擬主機特定檔案，則其內容應被添加到虛擬主 `Include` 機檔案中引用它們的語句中。

### 檢查變數

Enter directory `conf.d/variables`.

刪除任何名為的文 `ams_default.vars` 件，並記得刪除 `Include` 引用它們的虛擬主機檔案中的語句。

如果 `conf.d/variables` 現在包含單一檔案，則應重新命名為 `custom.vars` ，而且不要忘記在虛擬主機 `Include` 檔案中也參照該檔案的陳述式。

但是，如果資料夾包含多個虛擬主機特定檔案，則其內容應被添加到虛擬主 `Include` 機檔案中引用它們的語句中。

### 移除白名單

刪除虛擬主 `conf.d/whitelists` 機檔案中 `Include` 引用該子資料夾中某個檔案的資料夾和刪除語句。

### 取代任何不再可用的變數

在所有虛擬主機檔案中：

重新命 `PUBLISH_DOCROOT` 名為 `DOCROOT`移除參照名為、或 `DISP_ID``PUBLISH_FORCE_SSL``PUBLISH_WHITELIST_ENABLED`

### 運行驗證器以檢查狀態

在目錄中運行dispatcher validator，使用 `httpd` subcommand :

```
$ validator httpd .
```

如果您看到有關遺失包含檔案的錯誤，請檢查您是否正確重新命名這些檔案。

如果您看到未列入白名單的Apache指令，請將其刪除。

### 移除所有非發佈農場

刪除名稱中 `conf.dispatcher.d/enabled_farms` 包含 `author`、 `unhealthy`、 `health``lc``flush` 或的任何群檔案。 中所有未連結 `conf.dispatcher.d/available_farms` 到的群檔案也可以刪除。

### 更名群檔案

必須重新命 `conf.d/enabled_farms` 名中的所有場，以符 `*.farm`合模式，因此，例如，應重新命 `customerX_farm.any` 名名為afarm的檔案 `customerX.farm`。

### 檢查快取

Enter directory `conf.dispatcher.d/cache`.

移除任何前置詞的檔案 `ams_`。

如果 `conf.dispatcher.d/cache` 現在為空，請將檔案從標 `conf.dispatcher.d/cache/rules.any`準調度器配置複製到此資料夾。 標準調度程式組態可在此SDK的資 `src` 料夾中找到。 別忘了也要改寫參照`$include` farm檔案中 `ams_*_cache.any` 規則檔案的語句。

如果現 `conf.dispatcher.d/cache` 在包含一個帶尾碼的檔案 `_cache.any`，則應將其更名為 `rules.any` ，並且不要忘記在場檔案中調整引 `$include` 用該檔案的語句。

但是，如果資料夾包含多個具有該模式的群特定檔案，則應將其內容複製到群 `$include` 檔案中引用它們的語句。

移除任何具有尾碼的檔案 `_invalidate_allowed.any`。

將Cloud Dispatcher `conf.dispatcher.d/cache/default_invalidate_any` 設定中的預設AEM檔案複製至該位置。

在每個群檔案中，刪除該部分中的任 `cache/allowedClients` 何內容，並將其替換為：

```
$include "../cache/default_invalidate.any"
```

### 檢查用戶端標題

Enter directory `conf.dispatcher.d/clientheaders`.

移除任何前置詞的檔案 `ams_`。

如果 `conf.dispatcher.d/clientheaders` 現在包含帶尾碼的單個檔案 `_clientheaders.any`，則應將其更名為 `clientheaders.any` ，並且不要忘記在場檔案中調整引 `$include` 用該檔案的語句。

但是，如果資料夾包含多個具有該模式的群特定檔案，則應將其內容複製到群 `$include` 檔案中引用它們的語句。

將預設AEM `conf.dispatcher/clientheaders/default_clientheaders.any` 的檔案複製為Cloud Service分派程式設定至該位置。

在每個群檔案中，替換任何clientheader包含如下所示的語句：

```
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"
```

和聲明：

```
$include "../clientheaders/default_clientheaders.any"
```

### 檢查篩選

Enter directory `conf.dispatcher.d/filters`.

移除任何前置詞的檔案 `ams_`。

如 `conf.dispatcher.d/filters` 果現在包含單一檔案，則應重新命名為`filters.any` ，並且不要忘記在場檔 `$include` 案中也參照該檔案來調整陳述式。

但是，如果資料夾包含多個具有該模式的群特定檔案，則應將其內容複製到群 `$include` 檔案中引用它們的語句。

將預設AEM `conf.dispatcher/filters/default_filters.any` 的檔案複製為Cloud Service分派程式設定至該位置。

在每個群檔案中，替換任何篩選器包含如下所示的語句：

```
$include "/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"
```

和聲明：

```
$include "../filters/default_filters.any"
```

### 勾選轉譯

Enter directory `conf.dispatcher.d/renders`.

移除該資料夾中的所有檔案。

將預設AEM `conf.dispatcher.d/renders/default_renders.any` 的檔案複製為Cloud Service分派程式設定至該位置。

在每個群檔案中，刪除該部分中的任 `renders` 何內容，並將其替換為：

```
$include "../renders/default_renders.any"
```

### 檢查虛擬主機

將目錄重 `conf.dispatcher.d/vhosts` 命名 `conf.dispatcher.d/virtualhosts` 並輸入。

移除任何前置詞的檔案 `ams_`。

如 `conf.dispatcher.d/virtualhosts` 果現在包含單一檔案，則應重新命名為`virtualhosts.any` ，並且不要忘記在場檔 `$include` 案中也參照該檔案來調整陳述式。

但是，如果資料夾包含多個具有該模式的群特定檔案，則應將其內容複製到群 `$include` 檔案中引用它們的語句。

將預設AEM `conf.dispatcher/virtualhosts/default_virtualhosts.any` 的檔案複製為Cloud Service分派程式設定至該位置。

在每個群檔案中，替換任何篩選器包含如下所示的語句：

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

和聲明：

```
$include "../virtualhosts/default_virtualhosts.any"
```

### 運行驗證器以檢查狀態

在您的目錄中以Cloud Service分派器驗證器的身分，使用子命令執 `dispatcher` 行AEM:

```
$ validator dispatcher .
```

如果您看到有關遺失包含檔案的錯誤，請檢查您是否正確重新命名這些檔案。

如果您看到未定義變數的錯 `PUBLISH_DOCROOT`誤，請將它重新命名 `DOCROOT`。

如需其他錯誤，請參閱驗證工具檔案的疑難排解一節。

### 使用本機部署測試您的組態（需要安裝Docker）

使用AEM中 `docker_run.sh` 的指令碼做為Cloud Service Dispatcher Tools，您可以測試您的設定是否不包含任何其他只會顯示部署錯誤的錯誤：

### 步驟1:使用驗證器生成部署資訊

```
validator full -d out .
```

這將驗證完整配置，並在 `out`

### 步驟2:使用部署資訊在Docker映像中啟動調度程式

當您的AEM發佈伺服器在您的macOS電腦上執行，並在連接埠4503上監聽時，您可以在該伺服器前面執行Dispatcher，如下所示：

```
$ docker_run.sh out docker.for.mac.localhost:4503 8080
```

這將啟動容器，並在本機埠8080上公開Apache。

### 使用您的新調度程式配置

恭喜！ 如果驗證器不再報告任何問題，而docker容器啟動時沒有出現任何故障或警告，則您已準備好將配置移動到git儲存庫 `dispatcher/src` 的子目錄。

**使用AMS Dispatcher配置第1版的客戶應聯繫客戶支援以幫助他們從第1版遷移到第2版，以便遵循上述說明。**
