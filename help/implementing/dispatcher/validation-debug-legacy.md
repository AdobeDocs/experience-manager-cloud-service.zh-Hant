---
title: 使用Dispatcher工具（舊版）進行驗證和除錯
description: 使用Dispatcher工具（舊版）進行驗證和除錯
feature: Dispatcher
hidefromtoc: true
exl-id: dc04d035-f002-42ef-9c2e-77602910c2ec
source-git-commit: 687323031ecfd179a1875033411b8398a3d1d74b
workflow-type: tm+mt
source-wordcount: '2345'
ht-degree: 0%

---

# 使用Dispatcher工具（舊版）進行驗證和除錯  {#Dispatcher-tools-legacy}

## 簡介 {#apache-and-dispatcher-configuration-and-testing}

>[!NOTE]
>如需雲端中Dispatcher的詳細資訊，以及如何下載Dispatcher工具，請參閱 [雲端中的Dispatcher](/help/implementing/dispatcher/disp-overview.md) 頁面。

以下各節將說明舊模式檔案結構、本機驗證、除錯，以及如何從舊模式移轉至 [柔性模式](/help/implementing/dispatcher/validation-debug.md).

本文假設您專案的Dispatcher設定不包含檔案opt-in/USE_SOURCES_DIRECTLY。 因此，它在檔案的數量和大小上都有所限制，例如：

* 必須使用的單一重寫檔案，而非網站專屬的檔案。
* 可自定義檔案的內容總和必須小於1MB。

自Cloud Manager 2021.7.0版本起，新的Cloud Manager程式會以AEM原型28及更新版本產生Maven專案結構，其中包括上述檔案。

是 **推薦** 從舊版模式移轉至彈性模式（如移轉區段所述） [從舊版模式移轉至彈性模式](#migrating-flexible). 使用彈性模式也會導致SDK和執行階段以改良的方式驗證和部署設定。

## 檔案結構 {#legacy-mode-file-structure}

專案的Dispatcher子資料夾（在舊版模式中）的結構如下：

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
    │   ├── marketing_query_parameters.any
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

您可以有一或多個這些檔案。 包含 `<VirtualHost>` 符合主機名稱且允許Apache以不同規則處理每個網域流量的項目。 檔案是在 `available_vhosts` 目錄，並在 `enabled_vhosts` 目錄。 從 `.vhost` 檔案、其他檔案（例如重寫和變數）將會包含在內。

* `conf.d/rewrites/rewrite.rules`

此檔案包含於 `.vhost` 檔案。 有一套重寫規則 `mod_rewrite`.

>[!NOTE]
>
>目前，必須使用單一重寫檔案，而非網站專用的檔案。 可自訂檔案的內容總和通常必須小於1MB。

* `conf.d/variables/custom.vars`

此檔案包含於 `.vhost` 檔案。 您可以在此位置為Apache變數新增定義。

* `conf.d/variables/global.vars`

此檔案包含於 `dispatcher_vhost.conf` 檔案。 您可以變更Dispatcher，並重新寫入此檔案中的記錄層級。

* `conf.dispatcher.d/available_farms/<CUSTOMER_CHOICE>.farm`

您可以有一或多個這些檔案，且這些檔案包含伺服器陣列，以符合主機名稱，並允許Dispatcher模組以不同規則處理每個伺服器陣列。 檔案是在 `available_farms` 目錄，並在 `enabled_farms` 目錄。 從 `.farm` 將包括檔案、其他檔案（如篩選器、快取規則等）。

* `conf.dispatcher.d/cache/rules.any`

此檔案包含於 `.farm` 檔案。 它指定快取首選項。

* `conf.dispatcher.d/clientheaders/clientheaders.any`

此檔案包含於 `.farm` 檔案。 它會指定應將哪些要求標題轉送至後端。

* `conf.dispatcher.d/filters/filters.any`

此檔案包含於 `.farm` 檔案。 它有一組規則，可變更應篩選掉的流量，而不是設為傳送至後端。

* `conf.dispatcher.d/virtualhosts/virtualhosts.any`

此檔案包含於 `.farm` 檔案。 它包含要由全局匹配匹配的主機名或URI路徑的清單。 這會決定要用來提供要求的後端。

上述檔案會參考下列不可修改的組態檔。 雲端環境中，Dispatcher不會處理不可變檔案的變更。

**不可變的配置檔案**

這些檔案是基本架構的一部分，並強制執行標準和最佳實務。 這些檔案被視為不可修改，因為在本機修改或刪除這些檔案不會影響您的部署，因為這些檔案將不會傳輸至您的雲端例項。

建議上述檔案參考下列不可修改的檔案，後跟任何其他陳述式或覆蓋。 將Dispatcher設定部署至雲端環境時，無論本機開發中使用的版本為何，都會使用不可修改檔案的最新版本。

* `conf.d/available_vhosts/default.vhost`

包含範例虛擬主機。 針對您自己的虛擬主機，建立此檔案的副本、自訂，請前往 `conf.d/enabled_vhosts` 並建立到自定義副本的符號連結。

* `conf.d/dispatcher_vhost.conf`

基本框架的一部分，用於說明如何包括虛擬主機和全局變數。

* `conf.d/rewrites/default_rewrite.rules`

適用於標準專案的預設重寫規則。 如果需要自定義，請修改 `rewrite.rules`. 在您的自訂中，如果預設規則符合您的需求，您仍可以先加入。

* `conf.dispatcher.d/available_farms/default.farm`

包含範例Dispatcher伺服器陣列。 針對您自己的伺服器陣列，建立此檔案的復本，加以自訂，請前往 `conf.d/enabled_farms` 並建立到自定義副本的符號連結。

* `conf.dispatcher.d/cache/default_invalidate.any`

基本框架的一部分，在啟動時生成。 您 **必填** 要在您定義的每個場中包含此檔案，請在 `cache/allowedClients` 區段。

* `conf.dispatcher.d/cache/default_rules.any`

適用於標準專案的預設快取規則。 如果需要自定義，請修改 `conf.dispatcher.d/cache/rules.any`. 在您的自訂中，如果預設規則符合您的需求，您仍可以先加入。

* `conf.dispatcher.d/clientheaders/default_clientheaders.any`

轉送至後端的預設要求標題，適用於標準專案。 如果需要自定義，請修改 `clientheaders.any`. 在您的自訂中，如果預設請求標題符合您的需求，您仍可以先加入這些標題。

* `conf.dispatcher.d/dispatcher.any`

基本架構的一部分，用來說明如何包含Dispatcher伺服器陣列。

* `conf.dispatcher.d/filters/default_filters.any`

適用於標準專案的預設篩選器。 如果需要自定義，請修改 `filters.any`. 在您的自訂中，如果預設篩選器符合您的需求，您仍可以先加入這些篩選器。

* `conf.dispatcher.d/renders/default_renders.any`

作為基本框架的一部分，此檔案在啟動時生成。 您 **必填** 要在您定義的每個場中包含此檔案，請在 `renders` 區段。

* `conf.dispatcher.d/virtualhosts/default_virtualhosts.any`

適用於標準專案的預設主機全域。 如果需要自定義，請修改 `virtualhosts.any`. 在您的自訂中，不應包含預設的全域主機，因為它符合 **ever** 傳入的請求。

## 支援的Apache模組 {#apache-modules}

請參閱 [支援的Apache模組](/help/implementing/dispatcher/disp-overview.md#supported-directives).

## 本機驗證 {#local-validation-legacy-mode}

>[!NOTE]
>以下各節包含使用Mac或Linux版SDK的命令，但Windows SDK也可以以類似方式使用。

使用 `validate.sh` 指令碼，如下所示：

```
$ validate.sh src/dispatcher
Phase 1: Dispatcher validator
Cloud manager validator 2.0.32
Phase 1 finished
Phase 2: httpd -t validation in docker image
values.csv found in deployment folder: /tmp/dispatcher_validation_1625150390 - using files listed there
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

指令碼會執行下列動作：

1. 它會執行驗證器。 如果配置無效，指令碼將失敗。
2. 會執行 `httpd -t` 命令來測試語法是否正確，以便apache httpd可以啟動。 如果成功，配置應已準備就緒，可進行部署。
3. 檢查Dispatcher SDK設定檔案的子集，如 [檔案結構部分](##legacy-mode-file-structure)，尚未修改。 這是AEM SDK版本v2021.1.4738推出的新檢查，其中也包含Dispatcher工具2.0.36版。在此更新前，客戶可能錯誤地假設這些不可變檔案的任何本機SDK修改也會套用至雲端環境。

在Cloud Manager部署期間， `httpd -t` 語法檢查也會一併執行，且Cloud Manager中會包含任何錯誤 `Build Images step failure` 記錄檔。

### 階段1 {#first-phase}

如果未允許列出指令，則工具會記錄錯誤並傳回非零退出代碼。 此外，它還會進一步掃描所有具有模式的檔案 `conf.dispatcher.d/enabled_farms/*.farm` 並檢查：

* 沒有使用允許的篩選規則 `/glob` (請參閱 [CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957) 以取得更多詳細資訊。
* 未公開管理功能。 例如，存取路徑，例如 `/crx/de or /system/console`.

請注意，驗證工具只會報告未列入允許清單之Apache指示的禁止使用。 它不會報告Apache配置的語法或語義問題，因為此資訊僅可用於運行環境中的Apache模組。

以下提供疑難排解技術，以偵錯工具輸出的常見驗證錯誤：

**找不到 `conf.dispatcher.d` 封存中的子資料夾**

您的封存應包含資料 `conf.d` 夾和 `conf.dispatcher.d`。請注意，您不 **應**&#x200B;在封 `etc/httpd` 存中使用首碼。

**在中找不到任何場`conf.dispatcher.d/enabled_farms`**

已啟用的伺服器陣列應位於提及的子資料夾中。

**包含的檔案(...)必須命名：...**

您的伺服器陣列設定中有兩個區段 **必須** 包含特定檔案： `/renders` 和 `/allowedClients` 在 `/cache` 區段。 這些區段必須如下所示：

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

您的伺服器陣列設定中有四個區段可讓您包含自己的檔案： `/clientheaders`, `filters`, `/rules` in `/cache` 區段與 `/virtualhosts`. 包含的檔案需命名如下：

| 章節 | 包含檔案名 |
|------------------|--------------------------------------|
| `/clientheaders` | `../clientheaders/clientheaders.any` |
| `/filters` | `../filters/filters.any` |
| `/rules` | `../cache/rules.any` |
| `/virtualhosts` | `../virtualhosts/virtualhosts.any` |

或者，您也可以包含 **預設** 這些檔案的版本，其名字前面加上 `default_`，例如 `../filters/default_filters.any`.

**包含位於(...)的語句，位於任何已知位置之外：...**

除上文各段所述的六節外，您不得使用 `$include` 語句，例如，以下語句將生成此錯誤：

```
/invalidate {
    $include "../cache/invalidate.any"
}
```

**允許的用戶端/轉譯不包括於：...**

當您未指定的包含時，會產生此錯誤 `/renders` 和 `/allowedClients` 在 `/cache` 區段。 請參閱
**包含的檔案(...)必須命名：...** 一節以取得詳細資訊。

**篩選不得使用全域模式以允許請求**

允許的要求具有 `/glob` 樣式規則，此規則會與完整的請求行相符，例如

```
/0100 {
    /type "allow" /glob "GET *.css *"
}
```

此陳述式的用意是允許 `css` 檔案，但也允許請求 **any** 資源，後接查詢字串 `?a=.css`. 因此，禁止使用這類篩選器（另請參閱CVE-2016-0957）。

**包含的檔案(...)與任何已知檔案不匹配**

Apache虛擬主機配置中有兩種類型的檔案，可以指定為包括：重寫和變數。
包含的檔案需命名如下：

| 類型 | 包含檔案名 |
|-----------|---------------------------------|
| 重寫 | `conf.d/rewrites/rewrite.rules` |
| 變數 | `conf.d/variables/custom.vars` |

>[!TIP]
>
>若要以更少限制的方式包含更多檔案，您可能會想要切換至彈性的Dispatcher設定模式。 請查看該文檔 [使用Dispatcher工具進行驗證和除錯](/help/implementing/dispatcher/validation-debug.md) 以取得彈性模式的詳細資訊。

或者，您也可以包含 **預設** 重寫規則的版本，其名稱為 `conf.d/rewrites/default_rewrite.rules`.
請注意，變數檔案沒有預設版本。

**檢測到已棄用的配置佈局，啟用相容性模式**

此訊息指出您的設定已棄用第1版配置，包含完整的Apache設定和具有 `ams_` 前置詞。 雖然回溯相容性仍支援此功能，但您應切換至新版面。

請注意，第一階段也可以 **單獨運行**，而非來自包裝函式 `validate.sh` 指令碼。

當對你的瑪文藏物或 `dispatcher/src` 子目錄，它會報告驗證失敗：

```
$ validator full dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-allowlisted directives:
  conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
  conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

在Windows上，Dispatcher驗證器會區分大小寫。 因此，如果您不遵守配置所在路徑的大寫，則可能無法驗證配置，例如：

```
bin\validator.exe full src
Cloud manager validator 2.0.xx
2021/03/15 18:15:40 Dispatcher configuration validation failed:
  conf.dispatcher.d\available_farms\default.farm:15: parent directory outside server root: c:\k\a\aem-dispatcher-sdk-windows-symlinks-testing3\dispatcher\src
  
```

從Windows資源管理器複製並貼上路徑，然後使用 `cd` 命令進入該路徑。

### 階段2 {#second-phase}

此階段會在影像中啟動Docker以檢查Apache語法。 Docker必須安裝在本機，但請注意，AEM不需要執行。

>[!NOTE]
>Windows用戶需要使用Windows 10專業版或支援Docker的其他分發版。 這是在本機電腦上執行和偵錯Dispatcher的必要條件。

此階段也可獨立執行 `validator full -d out src/dispatcher`，它會生成下一個命令所需的外部目錄 `bin/docker_run.sh out host.docker.internal:4503 8080`.

在Cloud Manager部署期間， `httpd -t` 語法檢查也會執行，且任何錯誤都會包含在Cloud Manager「建置影像」步驟失敗記錄中。

### 階段3 {#third-phase}

如果此階段出現故障，則表示Adobe已更改一個或多個不可變檔案，並且必須用中傳遞的新版本替換相應的不可變檔案 `src` SDK的目錄。 以下記錄範例說明此問題：

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

此階段也可獨立執行 `validator full -d out src/dispatcher`，它會生成下一個命令所需的外部目錄 `bin/docker_immutability_check.sh out`.

## 對Apache和Dispatcher設定進行除錯 {#debugging-apache-and-dispatcher-configuration}

請注意，您可以透過 `./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`.

如前所述，Docker必須安裝在本機，且AEM不需要執行。 Windows用戶需要使用Windows 10專業版或支援Docker的其他分發版。 這是在本機電腦上執行和偵錯Dispatcher的必要條件。

下列策略可用來增加Dispatcher模組的記錄輸出，並查看 `RewriteRule` 在本機和雲端環境中進行評估。

這些模組的記錄層級由變數定義 `DISP_LOG_LEVEL` 和 `REWRITE_LOG_LEVEL`. 可在檔案中設定 `conf.d/variables/global.vars`. 其相關部分如下：

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

在本機執行Dispatcher時，記錄會直接列印至終端輸出。 大部分情況下，您會希望這些記錄處於DEBUG中，這可透過在執行Docker時將Debug層級傳遞為參數來完成。 例如： `DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`.

雲端環境的記錄檔會透過Cloud Manager中可用的記錄服務公開。

## 每個環境的不同Dispatcher設定 {#different-dispatcher-configurations-per-environment}

目前，相同的Dispatcher設定會套用至所有AEMas a Cloud Service環境。 執行階段會有環境變數 `ENVIRONMENT_TYPE` 包含當前運行模式（dev、stage或prod）以及定義。 定義可以是 `ENVIRONMENT_DEV`, `ENVIRONMENT_STAGE` 或 `ENVIRONMENT_PROD`. 在Apache設定中，變數可直接用於運算式中。 或者，定義可用來建置邏輯：

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

在本機測試設定時，您可以傳遞變數來模擬不同的環境類型 `DISP_RUN_MODE` 到 `docker_run.sh` 直接指令碼：

```
$ DISP_RUN_MODE=stage docker_run.sh out docker.for.mac.localhost:4503 8080
```

未傳入DISP_RUN_MODE值時，預設的執行模式為「dev」。
如需完整的可用選項和變數清單，請執行指令碼 `docker_run.sh` 沒有引數。

## 檢視Docker容器正在使用的Dispatcher設定 {#viewing-dispatcher-configuration-in-use-by-docker-container}

若使用環境特定設定，可能很難判斷實際的Dispatcher設定看起來是什麼樣子。 啟動Docker容器後， `docker_run.sh` 可傾棄如下：

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

## 從舊版模式移轉至彈性模式 {#migrating-flexible}

在Cloud Manager 2021.7.0版本中，新的Cloud Manager程式會以AEM原型28或更新版本產生maven專案結構，其中包含檔案 **選擇加入/USE_SOURCES_DIRECTLY**. 如此一來，舊版模式先前對檔案數量和大小的限制便已移除，也導致SDK和執行階段以改良的方式驗證和部署設定。 如果您的Dispatcher設定沒有此檔案，強烈建議您進行移轉。 使用 [柔性模式](/help/implementing/dispatcher/validation-debug.md#migrating) 頁面。
