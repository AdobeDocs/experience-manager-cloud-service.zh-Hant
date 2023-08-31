---
title: 使用 Dispatcher 工具進行驗證和偵錯
description: 瞭解本機驗證、偵錯、彈性模式檔案結構，以及如何從舊版模式移轉至彈性模式。
feature: Dispatcher
exl-id: 9e8cff20-f897-4901-8638-b1dbd85f44bf
source-git-commit: fccce4fed057b9cf20825bce043b3ec95c3a5ab8
workflow-type: tm+mt
source-wordcount: '2988'
ht-degree: 1%

---

# 使用 Dispatcher 工具進行驗證和偵錯 {#Dispatcher-in-the-cloud}

## 簡介 {#apache-and-dispatcher-configuration-and-testing}

>[!NOTE]
>如需有關雲端中Dispatcher以及如何下載Dispatcher工具的詳細資訊，請參閱 [雲端中的Dispatcher](/help/implementing/dispatcher/disp-overview.md) 頁面。 如果您的Dispatcher設定是處於舊版模式，請參閱 [舊版模式檔案](/help/implementing/dispatcher/validation-debug-legacy.md).

以下各節將說明彈性模式的檔案結構、本機驗證、偵錯以及從舊版模式移轉至彈性模式。

本文假設您的專案的Dispatcher設定包含檔案 `opt-in/USE_SOURCES_DIRECTLY`. 此檔案會讓SDK和執行階段以比舊版模式更好的方式驗證和部署設定，移除檔案數量和大小的限制。

如果您的Dispatcher設定不包含前述檔案，Adobe建議您從舊版模式移轉至彈性模式，如 [從舊版模式移轉至彈性模式](#migrating) 區段。

## 檔案結構 {#flexible-mode-file-structure}

專案的Dispatcher子資料夾的結構如下：

```bash
./
├── conf.d
│   ├── available_vhosts
│   │   ├── my_site.vhost # Created by customer
│   │   └── default.vhost
│   ├── dispatcher_vhost.conf
│   ├── enabled_vhosts
│   │   ├── README
│   │   └── my_site.vhost -> ../available_vhosts/my_site.vhost  # Created by customer
│   └── rewrites
│   │   ├── default_rewrite.rules
│   │   └── rewrite.rules
│   └── variables
|       ├── custom.vars
│       └── global.vars
│── opt-in
│   └── USE_SOURCES_DIRECTLY
└── conf.dispatcher.d
    ├── available_farms
    │   ├── my_farm.farm # Created by customer
    │   └── default.farm
    ├── cache
    │   ├── default_invalidate.any
    │   ├── default_rules.any
    │   ├── marketing_query_parameters.any
    │   └── rules.any
    ├── clientheaders
    │   ├── clientheaders.any
    │   └── default_clientheaders.any
    ├── dispatcher.any
    ├── enabled_farms
    │   ├── README
    │   └── my_farm.farm -> ../available_farms/my_farm.farm  # Created by customer
    ├── filters
    │   ├── default_filters.any
    │   └── filters.any
    ├── renders
    │   └── default_renders.any
    └── virtualhosts
    │   ├── default_virtualhosts.any
    │   └── virtualhosts.any
    
```

以下是可修改之重要檔案的說明：

**可自訂的檔案**

以下檔案可自訂，並在部署時傳輸到您的雲端執行個體：

* `conf.d/available_vhosts/<CUSTOMER_CHOICE>.vhost`

您可以有一或多個這些檔案。 它們包含 `<VirtualHost>` 和主機名稱相符的專案，並允許Apache使用不同規則處理每個網域流量。 檔案建立於 `available_vhosts` 目錄，並透過中的符號連結啟用 `enabled_vhosts` 目錄。 從 `.vhost` 包括檔案、其他檔案（例如重寫與變數）。

>[!NOTE]
>
>在彈性模式中，您應該使用相對路徑，而非絕對路徑。

請確定至少有一部與ServerAlias相符的虛擬主機永遠可用 `\*.local`， `localhost`、和 `127.0.0.1` Dispatcher失效所需的引數。 伺服器別名 `*.adobeaemcloud.net` 和 `*.adobeaemcloud.com` 在至少一個vhost設定中也需要使用，而在內部Adobe程式中也需要。

如果因為您有多個vhost檔案而想要比對正確的主機，您可以遵循以下範例：

```
<VirtualHost *:80>
    ServerName    "example.com"
    # Put names of which domains are used for your published site/content here
    ServerAlias     "*example.com" "\*.local" "localhost" "127.0.0.1" "*.adobeaemcloud.net" "*.adobeaemcloud.com"
    # Use a document root that matches the one in conf.dispatcher.d/default.farm
    DocumentRoot "${DOCROOT}"
    # URI dereferencing algorithm is applied at Sling's level, do not decode parameters here
    AllowEncodedSlashes NoDecode
    # Add header breadcrumbs for help in troubleshooting which vhost file is chosen
    <IfModule mod_headers.c>
        Header add X-Vhost "publish-example-com"
    </IfModule>
  ...
</VirtualHost>
```

* `conf.d/enabled_vhosts/<CUSTOMER_CHOICE>.vhost`

此資料夾包含指向「conf.dispatcher.d/available_vhosts」下檔案的相對符號連結。

建立這些符號連結所需的命令範例：

Apple®macOS、Linux和WSL

```
ln -s ../available_vhosts/wknd.vhost wknd.vhost
```

Microsoft® Windows

```
mklink wknd.vhost ..\available_vhosts\wknd.vhost
```

>[!NOTE]
>
> 在Windows下使用符號連結時，您應在提升許可權的命令提示字元中執行（在Linux的Windows子系統中），或具有 [建立符號連結](https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/create-symbolic-links) 已指派許可權。

* `conf.d/rewrites/rewrite.rules`

檔案包含在您的 `.vhost` 檔案。 它有一組重寫規則 `mod_rewrite`.

* `conf.d/variables/custom.vars`

檔案包含在您的 `.vhost` 檔案。 您可以在此位置新增Apache變數的定義。

* `conf.d/variables/global.vars`

檔案包含在 `dispatcher_vhost.conf` 檔案。 您可以變更您的Dispatcher並重寫此檔案中的記錄層級。

* `conf.dispatcher.d/available_farms/<CUSTOMER_CHOICE>.farm`

您可以有一或多個這樣的檔案，而且這些檔案包含陣列以符合主機名稱，並允許Dispatcher模組使用不同規則處理每個陣列。 檔案建立於 `available_farms` 目錄，並透過中的符號連結啟用 `enabled_farms` 目錄。 從 `.farm` 檔案、其他檔案（例如篩選器、快取規則等）也會包括在內。

* `conf.dispatcher.d/enabled_farms/<CUSTOMER_CHOICE>.farm`

此資料夾包含指向「conf.dispatcher.d/available_farms」下檔案的相對符號連結。

建立這些符號連結所需的命令範例：

Apple®macOS、Linux和WSL

```
ln -s ../available_farms/wknd.farm wknd.farm
```

Microsoft® Windows

```
mklink wknd.farm ..\available_farms\wknd.farm
```

>[!NOTE]
>
> 在Windows下使用符號連結時，您應在提升許可權的命令提示字元中執行（在Linux的Windows子系統中），或具有 [建立符號連結](https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/create-symbolic-links) 已指派許可權。

* `conf.dispatcher.d/cache/rules.any`

檔案包含在您的 `.farm` 檔案。 它會指定快取偏好設定。

* `conf.dispatcher.d/clientheaders/clientheaders.any`

檔案包含在您的 `.farm` 檔案。 它會指定應該將哪些請求標頭轉送至後端。

* `conf.dispatcher.d/filters/filters.any`

檔案包含在您的 `.farm` 檔案。 它有一組規則可變更應該過濾掉的流量，而不會使其進入後端。

* `conf.dispatcher.d/virtualhosts/virtualhosts.any`

檔案包含在您的 `.farm` 檔案。 它有一個主機名稱或URI路徑的清單，將透過glob比對進行比對。 此比對會決定使用哪個後端來處理請求。

* `opt-in/USE_SOURCES_DIRECTLY`

此檔案可啟用更具彈性的Dispatcher設定，並移除先前對檔案數量和大小的限制。 這樣也會讓SDK和執行階段以改良的方式驗證和部署設定。

上述檔案參照下列不可變的組態檔。 雲端環境中的Dispatcher不會處理不可變檔案的變更。

**不可變組態檔**

這些檔案是基本框架的一部分，可強制實施標準和最佳實務。 這些檔案被視為不可變，因為在本機修改或刪除它們不會對您的部署造成影響，因為它們不會傳輸到您的雲端執行個體。

建議上述檔案參照下列不可變檔案，然後加上任何其他陳述式或覆寫。 將Dispatcher設定部署到雲端環境時，無論本機開發中使用了什麼版本，都會使用最新版本的不可變檔案。

* `conf.d/available_vhosts/default.vhost`

包含範例虛擬主機。 針對您自己的虛擬主機，建立此檔案的復本、自訂，然後前往 `conf.d/enabled_vhosts` 並建立自訂復本的符號連結。
請勿將default.vhost檔案直接複製到 `conf.d/enabled_vhosts`.

請確定虛擬主機一律可用且符合ServerAlias `\*.local`， `localhost`、和 `127.0.0.1` Dispatcher失效所需的引數。 伺服器別名 `*.adobeaemcloud.net` 和 `*.adobeaemcloud.com` 內部Adobe程式所需。

* `conf.d/dispatcher_vhost.conf`

基本框架的一部分，用來說明如何包含虛擬主機和全域變數。

* `conf.d/rewrites/default_rewrite.rules`

重寫適用於標準專案的預設規則。 如果您需要自訂，請修改 `rewrite.rules`. 自訂時，如果預設規則符合您的需求，您仍可先包含這些規則。

* `conf.dispatcher.d/available_farms/default.farm`

包含範例Dispatcher陣列。 針對您自己的陣列，建立此檔案的復本，自訂它，然後前往 `conf.d/enabled_farms` 並建立自訂復本的符號連結。

* `conf.dispatcher.d/cache/default_invalidate.any`

基礎框架的一部分，在啟動時產生。 您是 **必填** 若要將此檔案納入您定義的每個陣列中，請在 `cache/allowedClients` 區段。

* `conf.dispatcher.d/cache/default_rules.any`

適用於標準專案的預設快取規則。 如果您需要自訂，請修改 `conf.dispatcher.d/cache/rules.any`. 自訂時，如果預設規則符合您的需求，您仍可先包含這些規則。

* `conf.dispatcher.d/clientheaders/default_clientheaders.any`

轉送至後端的預設請求標頭，適用於標準專案。 如果您需要自訂，請修改 `clientheaders.any`. 自訂後，您仍可先納入預設的要求標題（若符合您的需求）。

* `conf.dispatcher.d/dispatcher.any`

基本框架的一部分，用於說明如何包含您的Dispatcher陣列。

* `conf.dispatcher.d/filters/default_filters.any`

適用於標準專案的預設篩選器。 如果您需要自訂，請修改 `filters.any`. 在您的自訂中，如果預設篩選器符合您的需求，您仍可先包含這些篩選器。

* `conf.dispatcher.d/renders/default_renders.any`

此檔案屬於基礎架構的一部分，會在啟動時產生。 您是 **必填** 若要將此檔案納入您定義的每個陣列中，請在 `renders` 區段。

* `conf.dispatcher.d/virtualhosts/default_virtualhosts.any`

適用於標準專案的預設主機萬用字元。 如果您需要自訂，請修改 `virtualhosts.any`. 自訂時，請勿包含預設的主機萬用字元，因為它是相符的 **每** 傳入要求。

## 支援的 Apache 模組 {#apache-modules}

另請參閱 [支援的Apache模組](/help/implementing/dispatcher/disp-overview.md#supported-directives).

## 本機驗證 {#local-validation-flexible-mode}

>[!NOTE]
>
>以下各節包含使用Mac或Linux®版SDK的命令，但Windows SDK也可以透過類似方式使用。

使用 `validate.sh` 指令碼，如下所示：

```
$ validate.sh src/dispatcher
opt-in USE_SOURCES_DIRECTLY marker file detected
Phase 1: Dispatcher validator
Cloud manager validator 2.0.32
Phase 1 finished
Phase 2: httpd -t validation in docker image
values.csv not found in deployment folder: /Users/foo/src - using files in 'conf.d' and 'conf.dispatcher.d' subfolders directly
processing configuration subfolder: conf.d
processing configuration subfolder: conf.dispatcher.d
Running script /docker_entrypoint.d/10-check-environment.sh
Running script /docker_entrypoint.d/20-create-docroots.sh
Running script /docker_entrypoint.d/30-wait-for-backend.sh
Waiting until localhost is available
localhost resolves to ::1
Running script /docker_entrypoint.d/40-generate-allowed-clients.sh
Running script /docker_entrypoint.d/50-check-expiration.sh
Running script /docker_entrypoint.d/60-check-loglevel.sh
Running script /docker_entrypoint.d/70-check-forwarded-host-secret.sh
# Dispatcher configuration: (/etc/httpd/conf.dispatcher.d/dispatcher.any)
/farms {

... 

}
Syntax OK
Phase 2 finished
Phase 3: Immutability check
reading immutable file list from /etc/httpd/immutable.files.txt

...

no immutable file has been changed - check is SUCCESSFUL
Phase 3 finished
```

指令碼包含以下三個階段：

1. 它會執行驗證器。 如果設定無效，指令碼會失敗。
2. 它會執行 `httpd -t` 用來測試語法是否正確，以便Apache httpd可以啟動的命令。 如果成功，設定應準備好進行部署。
3. 檢查Dispatcher SDK設定檔案的子集，這些檔案旨在不可變動，如 [檔案結構區段](##flexible-mode-file-structure)，尚未修改且符合目前的SDK版本。

在Cloud Manager部署期間， `httpd -t` 語法檢查也會執行，所有錯誤都會包含在Cloud Manager中 `Build Images step failure` 記錄。

>[!NOTE]
>
請參閱 [自動重新載入及驗證](#automatic-loading) 區段以取得執行的替代方案 `validate.sh` 在每次設定修改後。

### 階段1 {#first-phase}

如果指示詞未加入允許清單，工具會記錄錯誤並傳回非零的退出代碼。 此外，它會進一步掃描所有具有模式的檔案 `conf.dispatcher.d/enabled_farms/*.farm` 並檢查：

* 沒有篩選器規則可使用允許透過 `/glob` (請參閱 [CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957))以取得更多詳細資料。
* 未公開任何管理功能。 例如，存取路徑，例如 `/crx/de or /system/console`.

驗證工具僅報告未列入允許清單的Apache指令的禁用情況。 不會報告您的Apache設定的語法或語意問題，因為此資訊僅供執行環境中的Apache模組使用。

以下提供工具輸出之常見驗證錯誤的疑難排解技巧：

**找不到 `conf.dispatcher.d` 封存中的子資料夾**

您的封存應包含資料 `conf.d` 夾和 `conf.dispatcher.d`。請注意，您不 **應**&#x200B;在封 `etc/httpd` 存中使用首碼。

**在中找不到任何陣列`conf.dispatcher.d/enabled_farms`**

您啟用的陣列應位於提及的子資料夾中。

**包含的檔案(...)必須命名為： ...**

您的陣列設定中有兩個區段， **必須** 包含特定檔案： `/renders` 和 `/allowedClients` 在 `/cache` 區段。 這些區段必須如下所示：

```
/renders {
    $include "../renders/default_renders.any"
}
```

與:

```
/allowedClients {
    $include "../cache/default_invalidate.any"
}
```

**檔案包含在未知的位置： ...**

您的陣列設定中有四個區段可讓您包含自己的檔案： `/clientheaders`， `filters`， `/rules` 在 `/cache` 區段和 `/virtualhosts`. 包含的檔案必須依下列方式命名：

| 區段 | 包含檔案名稱 |
|------------------|--------------------------------------|
| `/clientheaders` | `../clientheaders/clientheaders.any` |
| `/filters` | `../filters/filters.any` |
| `/rules` | `../cache/rules.any` |
| `/virtualhosts` | `../virtualhosts/virtualhosts.any` |

或者，您也可以包含 **預設** 這些檔案的版本，其名稱會以字詞為前置詞 `default_`例如， `../filters/default_filters.any`.

**Include陳述式位於(...)，在任何已知位置以外： ...**

除了上述段落中提到的六個區段外，您不得使用 `$include` 陳述式，例如，下列專案會產生此錯誤：

```
/invalidate {
    $include "../cache/invalidate.any"
}
```

**不允許的使用者端/轉譯器不包括： ...**

若您未指定的「包含」，則會產生此錯誤 `/renders` 和 `/allowedClients` 在 `/cache` 區段。 請參閱
**包含的檔案(...)必須命名為： ...** 區段以取得詳細資訊。

**篩選器不得使用glob模式來允許請求**

允許具有的請求是不安全的 `/glob` 樣式規則，會比對完整的請求行，例如

```
/0100 {
    /type "allow" /glob "GET *.css *"
}
```

此陳述式旨在允許以下專案的請求： `css` 檔案，但也允許要求 **任何** 後接查詢字串的資源 `?a=.css`. 因此，禁止使用這類篩選器（另請參閱CVE-2016-0957）。

**包含的檔案(...)不符合任何已知檔案**

依預設，Apache虛擬主機設定中的兩種檔案型別可以指定為include：重寫與變數。

| 類型 | 包含檔案名稱 |
|-----------|---------------------------------|
| 重寫 | `conf.d/rewrites/rewrite.rules` |
| 變數 | `conf.d/variables/custom.vars` |

在彈性模式中，也可以包含其他檔案，只要它們位於的子目錄（在任何層級）中 `conf.d` 前置詞如下的目錄。

| 包含檔案上層目錄前置詞 |
|-------------------------------------|
| `conf.d/includes` |
| `conf.d/modsec` |
| `conf.d/rewrites` |

例如，您可以將檔案包含在 `conf.d/includes` 目錄，如下所示：

```
Include conf.d/includes/mynewdirectory/myincludefile.conf
```

或者，您也可以包含 **預設** 重寫規則的版本，其名稱為 `conf.d/rewrites/default_rewrite.rules`.
請注意，變數檔案沒有預設版本。

**偵測到已棄用的配置配置，啟用相容性模式**

此訊息指出您的設定具有已棄用的版本1版面，其中包含完整的Apache設定和檔案，其中 `ams_` 字首。 雖然此設定仍支援回溯相容性，但您應切換至新版面。

第一階段也可以是 **單獨執行**，而非來自包裝函式 `validate.sh` 指令碼。

針對您的Maven成品或 `dispatcher/src` 子目錄，它會報告驗證失敗：

```
$ validator full -relaxed dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-allowlisted directives:
  conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
  conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

在Windows上，Dispatcher驗證器會區分大小寫。 因此，如果您不遵循設定所在路徑的大小寫，例如：

```
bin\validator.exe -relaxed full src
Cloud manager validator 2.0.xx
2021/03/15 18:15:40 Dispatcher configuration validation failed:
  conf.dispatcher.d\available_farms\default.farm:15: parent directory outside server root: c:\k\a\aem-dispatcher-sdk-windows-symlinks-testing3\dispatcher\src
```

從Windows檔案總管複製並貼上路徑，然後在命令提示字元上使用 `cd` 命令匯入該路徑。

### 階段2 {#second-phase}

此階段會透過在Docker容器中啟動Apache HTTPD來檢查Apache語法。 Docker必須安裝在本機，但請注意，AEM不需要運行。

>[!NOTE]
>
Windows使用者必須使用支援Docker的Windows 10 Professional或其他發行版本。 此需求是在本機電腦上執行和偵錯Dispatcher的先決條件。
對於Windows和macOS，Adobe建議使用Docker Desktop。

此階段也可以獨立執行，透過 `bin/docker_run.sh src/dispatcher host.docker.internal:4503 8080`.

在Cloud Manager部署期間， `httpd -t` 語法檢查也會執行，所有錯誤都包含在Cloud Manager建置影像步驟失敗記錄檔中。

### 階段3 {#third-phase}

如果在此階段失敗，則表示Adobe已變更一個或多個不可變檔案。 在這種情況下，您必須將對應的不可變檔案替換為 `src` SDK的目錄。 以下記錄範例說明此問題：

```
Phase 3: Immutability check
reading immutable file list from /etc/httpd/immutable.files.txt
(...)
checking existing 'conf.dispatcher.d/clientheaders/default_clientheaders.any' for changes
immutable file 'conf.dispatcher.d/clientheaders/default_clientheaders.any' has been changed:
--- /etc/httpd/conf.dispatcher.d/clientheaders/default_clientheaders.any
+++ /etc/httpd-actual/conf.dispatcher.d/clientheaders/default_clientheaders.any
@@ -40,4 +40,3 @@
"Sling-uploadmode"
"x-requested-with"
"If-Modified-Since"
-"Authorization"
** error: immutable file 'conf.dispatcher.d/clientheaders/default_clientheaders.any' has been changed!
  
```

此階段也可以獨立執行，透過 `bin/docker_immutability_check.sh src/dispatcher`.

您可以透過執行 `bin/update_maven.sh src/dispatcher` 您的Dispatcher資料夾上的指令碼，其中 `src/dispatcher` 是您的Dispatcher設定目錄。 此指令碼也會更新任何 `pom.xml` 檔案，以便maven不變性檢查也能更新。

## 偵錯您的Apache和Dispatcher設定 {#debugging-apache-and-dispatcher-configuration}

您可以使用在本機執行Apache Dispatcher `./bin/docker_run.sh src/dispatcher docker.for.mac.localhost:4503 8080`.

如前所述，必須在本機安裝Docker，AEM不需要運行。 Windows使用者必須使用支援Docker的Windows 10 Professional或其他發行版本。 此需求是在本機電腦上執行和偵錯Dispatcher的先決條件。

以下策略可用於增加Dispatcher模組的記錄輸出並檢視的結果 `RewriteRule` 在本機和雲端環境中進行評估。

這些模組的記錄層級由變數定義 `DISP_LOG_LEVEL` 和 `REWRITE_LOG_LEVEL`. 可在檔案中加以設定 `conf.d/variables/global.vars`. 其相關部分如下：

```
# Log level for the dispatcher
#
# Possible values are: error, warn, info, debug and trace1
# Default value: warn
#
# Define DISP_LOG_LEVEL warn
 
# Log level for mod_rewrite
#
# Possible values are: error, warn, info, debug and trace1 - trace8
# Default value: warn
#
# To debug your RewriteRules, it is recommended to raise your log
# level to trace2.
#
# More information can be found at:
# https://httpd.apache.org/docs/current/mod/mod_rewrite.html#logging
#
# Define REWRITE_LOG_LEVEL warn
```

在本機執行Dispatcher時，記錄會直接列印到終端機輸出。 大多數情況下，您都希望這些記錄位於DEBUG中，這可以通過在執行Docker時傳遞偵錯級別作為引數來完成。 例如：`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh src docker.for.mac.localhost:4503 8080`。

雲端環境的記錄會透過Cloud Manager中提供的記錄服務公開。

>[!NOTE]
>
對於AEMas a Cloud Service上的環境，偵錯是最高詳細程度等級。 不支援追蹤記錄層級，因此您在雲端環境中工作時應該避免進行設定。

### 自動重新載入及驗證 {#automatic-reloading}

>[!NOTE]
>
由於Windows作業系統的限制，此功能僅適用於macOS和Linux®使用者。

不要執行本機驗證(`validate.sh`)並啟動Docker容器(`docker_run.sh`)每次修改設定時，您也可以執行 `docker_run_hot_reload.sh` 指令碼。 指令碼會監視設定的任何變更，並自動重新載入並重新執行驗證。 使用此選項，您便可在除錯時節省大量時間。

您可以使用以下命令執行指令碼： `./bin/docker_run_hot_reload.sh src/dispatcher host.docker.internal:4503 8080`

輸出的第一行看起來與執行的類似 `docker_run.sh`. 例如：

```
~ bin/docker_run_hot_reload.sh src host.docker.internal:8081 8082
opt-in USE_SOURCES_DIRECTLY marker file detected
Running script /docker_entrypoint.d/10-check-environment.sh
Running script /docker_entrypoint.d/15-check-pod-name.sh
Running script /docker_entrypoint.d/20-create-docroots.sh
Running script /docker_entrypoint.d/30-wait-for-backend.sh
Waiting until host.docker.internal is available
host.docker.internal resolves to 192.168.65.2
Running script /docker_entrypoint.d/40-generate-allowed-clients.sh
Running script /docker_entrypoint.d/50-check-expiration.sh
Running script /docker_entrypoint.d/60-check-loglevel.sh
Running script /docker_entrypoint.d/70-check-forwarded-host-secret.sh
Running script /docker_entrypoint.d/80-frontend-domain.sh
Running script /docker_entrypoint.d/zzz-import-sdk-config.sh
WARN Mon Jul  4 09:53:54 UTC 2022: Pseudo symlink conf.d seems to point to a non-existing file!
INFO Mon Jul  4 09:53:55 UTC 2022: Copied customer configuration to /etc/httpd.
INFO Mon Jul  4 09:53:55 UTC 2022: Start testing
Cloud manager validator 2.0.43
2022/07/04 09:53:55 No issues found
INFO Mon Jul  4 09:53:55 UTC 2022: Testing with fresh base configuration files.
INFO Mon Jul  4 09:53:55 UTC 2022: Apache httpd informationServer version: Apache/2.4.54 (Unix)
```

## 每個環境不同的Dispatcher設定 {#different-dispatcher-configurations-per-environment}

目前，相同的Dispatcher設定會套用至AEMas a Cloud Service上的所有環境。 執行階段有環境變數 `ENVIRONMENT_TYPE` 包含目前的執行模式（開發、階段或生產）和「定義」。 「定義」可以是 `ENVIRONMENT_DEV`， `ENVIRONMENT_STAGE`，或 `ENVIRONMENT_PROD`. 在Apache設定中，變數可直接在運算式中使用。 或者，「define」可用來建置邏輯：

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

在Dispatcher設定中，相同的環境變數可供使用。 如果需要更多邏輯，請定義上述範例中顯示的變數，然後在Dispatcher設定區段中使用它們：

```
/virtualhosts {
  { "${VIRTUALHOST}" }
}
```

或者，您可以在httpd/dispatcher設定中使用Cloud Manager環境變數，但不是環境秘密。 如果程式有多個開發環境，而且其中某些開發環境的httpd/Dispatcher設定值不同，此方法就特別重要。 相同的${VIRTUALHOST} 語法將會如上述範例一樣使用，但不會使用上述變數檔案中的Define宣告。 閱讀 [Cloud Manager檔案](/help/implementing/cloud-manager/environment-variables.md) 以取得設定Cloud Manager環境變數的指示。

在本機測試您的設定時，您可以透過傳遞變數來模擬不同的環境型別 `DISP_RUN_MODE` 至 `docker_run.sh` 直接編寫指令碼：

```
$ DISP_RUN_MODE=stage docker_run.sh src docker.for.mac.localhost:4503 8080
```

不傳入DISP_RUN_MODE的值時，預設的執行模式為「dev」。
如需可用選項和變數的完整清單，請執行指令碼 `docker_run.sh` 沒有引數。

## 檢視Docker容器正在使用的Dispatcher設定 {#viewing-dispatcher-configuration-in-use-by-docker-container}

使用特定環境的設定，可能很難判斷實際Dispatcher設定是什麼樣子。 使用啟動您的Docker容器後 `docker_run.sh`，可依下列方式傾印：

* 確定正在使用的Docker容器ID：

```
$ docker ps
CONTAINER ID       IMAGE
d75fbd23b29        adobe/aem-ethos/dispatcher-publish:...
```

* 使用該容器ID執行以下命令列：

```
$ docker exec d75fbd23b29 httpd-test
# Dispatcher configuration: (/etc/httpd/conf.dispatcher.d/dispatcher.any)
/farms {
  /publishfarm {
    /clientheaders {
...
```

## 從舊版模式移轉至彈性模式 {#migrating}

在Cloud Manager 2021.7.0版本中，新的Cloud Manager計畫會使用以下專案產生maven專案結構 [AEM原型28](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hant) 或更高版本，其中包含檔案 **opt-in/USE_SOURCES_DIRECTLY**. 它會移除 [舊版模式](/help/implementing/dispatcher/validation-debug-legacy.md) 檔案的數量和大小，也會導致SDK和執行階段以改良的方式驗證和部署設定。 如果您的Dispatcher設定沒有此檔案，強烈建議您進行移轉。 請使用下列步驟來確保安全轉換：

1. **本機測試。** 使用最新的Dispatcher工具SDK，新增資料夾和檔案 `opt-in/USE_SOURCES_DIRECTLY`. 請依照本文中的「本機驗證」指示進行，以便您可以測試Dispatcher是否在本機運作。
1. **雲端開發測試：**
   * 提交檔案 `opt-in/USE_SOURCES_DIRECTLY` 至非生產管道部署至雲端開發環境的Git分支。
   * 使用Cloud Manager來部署至雲端開發環境。
   * 徹底測試。 在將變更部署到更高層環境之前，請務必驗證Apache和Dispatcher設定的行為是否符合您的預期。 檢查與您的自訂設定相關的所有行為。 如果您認為部署的Dispatcher設定未反映您的自訂設定，請提交客戶支援票證。

   >[!NOTE]
   >
   在彈性模式中，您應該使用相對路徑，而非絕對路徑。
1. **部署至生產環境：**
   * 提交檔案 `opt-in/USE_SOURCES_DIRECTLY` 至生產管道部署至雲端中繼和生產環境的Git分支。
   * 使用Cloud Manager部署至中繼環境。
   * 徹底測試。 在將變更部署到更高層環境之前，請務必驗證Apache和Dispatcher設定的行為是否符合您的預期。 檢查與自訂設定相關的所有行為。 如果您認為部署的Dispatcher設定未反映您的自訂設定，請提交客戶支援票證。
   * 使用Cloud Manager繼續部署到生產環境。
