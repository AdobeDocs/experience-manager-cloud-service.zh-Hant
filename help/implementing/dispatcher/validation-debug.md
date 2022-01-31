---
title: 使用Dispatcher工具驗證和調試
description: 使用Dispatcher工具驗證和調試
feature: Dispatcher
exl-id: 9e8cff20-f897-4901-8638-b1dbd85f44bf
source-git-commit: ddc49ef1eed491a4464d17b6a47f924c42381e7f
workflow-type: tm+mt
source-wordcount: '2518'
ht-degree: 1%

---

# 使用Dispatcher工具驗證和調試 {#Dispatcher-in-the-cloud}

## 簡介 {#apache-and-dispatcher-configuration-and-testing}

>[!NOTE]
>有關雲中的Dispatcher以及如何下載Dispatcher Tools的詳細資訊，請參見 [雲中的調度程式](/help/implementing/dispatcher/disp-overview.md) 的子菜單。 如果您的調度程式配置處於舊模式，請參閱 [舊模式文檔](/help/implementing/dispatcher/validation-debug-legacy.md)。

以下各節介紹了靈活模式檔案結構、本地驗證、調試以及從舊模式遷移到靈活模式。

本文假定項目的調度程式配置包括該檔案 `opt-in/USE_SOURCES_DIRECTLY`，這將使SDK和運行時以與舊模式相比的改進方式驗證和部署配置，從而消除對檔案數量和大小的限制。

因此，如果調度程式配置不包括上述檔案，則 **建議** 從舊模式遷移到靈活模式(如 [從舊模式遷移到靈活模式](#migrating) 的子菜單。

## 檔案結構 {#flexible-mode-file-structure}

項目的Dispatcher子資料夾的結構如下：

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
│── opt-in
│   └── USE_SOURCES_DIRECTLY
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
    │   ├── default_virtualhosts.any
    │   └── virtualhosts.any
    
```

以下是可修改的顯著檔案的說明：

**可自定義的檔案**

以下檔案可自定義，並將在部署時傳輸到雲實例：

* `conf.d/available_vhosts/<CUSTOMER_CHOICE>.vhost`

您可以擁有一個或多個這些檔案。 它們包含 `<VirtualHost>` 與主機名匹配且允許Apache使用不同規則處理每個域通信的條目。 檔案是在 `available_vhosts` 目錄中的符號連結啟用 `enabled_vhosts` 的子菜單。 從 `.vhost` 將包括檔案、其他檔案（如重寫和變數）。

* `conf.d/rewrites/rewrite.rules`

此檔案包含於 `.vhost` 的子菜單。 它有一組重寫規則 `mod_rewrite`。

* `conf.d/variables/custom.vars`

此檔案包含於 `.vhost` 的子菜單。 可在此位置中為Apache變數添加定義。

* `conf.d/variables/global.vars`

此檔案包含於 `dispatcher_vhost.conf` 的子菜單。 您可以更改此檔案中的Dispatcher和重寫日誌級別。

* `conf.dispatcher.d/available_farms/<CUSTOMER_CHOICE>.farm`

您可以擁有一個或多個這些檔案，這些檔案包含與主機名匹配的場，並允許Dispatcher模組使用不同的規則處理每個場。 檔案是在 `available_farms` 目錄中的符號連結啟用 `enabled_farms` 的子菜單。 從 `.farm` 將包括檔案、過濾器、快取規則等其他檔案。

* `conf.dispatcher.d/cache/rules.any`

此檔案包含於 `.farm` 的子菜單。 它指定快取首選項。

* `conf.dispatcher.d/clientheaders/clientheaders.any`

此檔案包含於 `.farm` 的子菜單。 它指定應將哪些請求標頭轉發到後端。

* `conf.dispatcher.d/filters/filters.any`

此檔案包含於 `.farm` 的子菜單。 它有一組規則，這些規則更改了應過濾出的流量，而不是將流量發送到後端。

* `conf.dispatcher.d/virtualhosts/virtualhosts.any`

此檔案包含於 `.farm` 的子菜單。 它包含要由全局匹配匹配的主機名或URI路徑的清單。 這決定了用於服務請求的後端。

* `opt-in/USE_SOURCES_DIRECTLY`

此檔案支援更靈活的調度程式配置，並刪除了以前對檔案數量和大小的限制。 它還使SDK和運行時以改進的方式驗證和部署配置。

上述檔案引用下面列出的不可改變的配置檔案。 雲環境中的調度程式將不處理對不可變檔案所做的更改。

**不可變的配置檔案**

這些檔案是基本框架的一部分，並強制實施標準和最佳做法。 這些檔案被視為不可變的，因為在本地修改或刪除它們不會對您的部署產生影響，因為它們不會被傳輸到您的雲實例。

建議上述檔案引用下面列出的不可變檔案，然後是任何附加語句或替代。 將Dispatcher配置部署到雲環境時，將使用不可變檔案的最新版本，而不管本地開發中使用的是哪個版本。

* `conf.d/available_vhosts/default.vhost`

包含示例虛擬主機。 對於您自己的虛擬主機，建立此檔案的副本，對其進行自定義，轉到 `conf.d/enabled_vhosts` 並建立到自定義副本的符號連結。

確保始終有與ServerAlias匹配的虛擬主機可用 `\*.local` 以及內部Adobe過程所需的localhost。

* `conf.d/dispatcher_vhost.conf`

基本框架的一部分，用於說明如何包括虛擬主機和全局變數。

* `conf.d/rewrites/default_rewrite.rules`

適用於標準項目的預設重寫規則。 如果需要自定義，請修改 `rewrite.rules`。 在自定義中，如果預設規則適合您的需要，您仍可以先包括這些規則。

* `conf.dispatcher.d/available_farms/default.farm`

包含Dispatcher場示例。 對於您自己的伺服器場，建立此檔案的副本，自定義它，轉到 `conf.d/enabled_farms` 並建立到自定義副本的符號連結。

* `conf.dispatcher.d/cache/default_invalidate.any`

基框架的一部分，在啟動時生成。 你是 **要求** 在您定義的每個場中包括此檔案， `cache/allowedClients` 的子菜單。

* `conf.dispatcher.d/cache/default_rules.any`

適用於標準項目的預設快取規則。 如果需要自定義，請修改 `conf.dispatcher.d/cache/rules.any`。 在自定義中，如果預設規則適合您的需要，您仍可以先包括這些規則。

* `conf.dispatcher.d/clientheaders/default_clientheaders.any`

要轉發到後端（適用於標準項目）的預設請求標頭。 如果需要自定義，請修改 `clientheaders.any`。 在自定義中，如果預設請求標頭適合您的需要，您仍可以先包括它們。

* `conf.dispatcher.d/dispatcher.any`

基本框架的一部分，用於說明如何包括Dispatcher場。

* `conf.dispatcher.d/filters/default_filters.any`

適用於標準項目的預設篩選器。 如果需要自定義，請修改 `filters.any`。 在自定義中，如果預設篩選器適合您的需要，您仍可以先包括這些篩選器。

* `conf.dispatcher.d/renders/default_renders.any`

作為基本框架的一部分，此檔案在啟動時生成。 你是 **要求** 在您定義的每個場中包括此檔案， `renders` 的子菜單。

* `conf.dispatcher.d/virtualhosts/default_virtualhosts.any`

適用於標準項目的預設主機全局。 如果需要自定義，請修改 `virtualhosts.any`。 在自定義中，不應包括預設的主機globbing，因為它與 **每** 傳入請求。

## 支援的Apache模組 {#apache-modules}

請參閱 [支援的Apache模組](/help/implementing/dispatcher/disp-overview.md#supported-directives)。

## 本地驗證 {#local-validation-flexible-mode}

>[!NOTE]
>
>以下各節包括使用SDK的Mac或Linux版本的命令，但Windows SDK也可以以類似方式使用。

使用 `validate.sh` 指令碼如下所示：

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

該指令碼包含以下三個階段：

1. 它運行驗證程式。 如果配置無效，則指令碼將失敗。
2. 執行 `httpd -t` 命令以test語法是否正確，以便apache httpd可以啟動。 如果成功，配置應準備好進行部署。
3. 檢查Dispatcher SDK配置檔案的子集（如中所述）是否不可變 [「檔案結構」部分](##flexible-mode-file-structure)，尚未修改。

在部署雲管理器期間， `httpd -t` 語法檢查也將執行，並且Cloud Manager中將包含任何錯誤 `Build Images step failure` 日誌。

### 階段1 {#first-phase}

如果不允許列出指令，則工具將記錄錯誤並返回非零退出代碼。 另外，它還用模式掃描所有檔案 `conf.dispatcher.d/enabled_farms/*.farm` 並檢查：

* 不存在使用允許通過的篩選器規則 `/glob` （請參見） [CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957) 的子菜單。
* 未公開任何管理功能。 例如，對路徑(如 `/crx/de or /system/console`。

請注意，驗證工具僅報告未允許列出的禁止使用Apache指令。 它不報告Apache配置的語法或語義問題，因為此資訊僅對運行環境中的Apache模組可用。

以下是用於調試工具輸出的常見驗證錯誤的故障排除技術：

**找不到 `conf.dispatcher.d` 存檔中的子資料夾**

您的封存應包含資料 `conf.d` 夾和 `conf.dispatcher.d`。請注意，您不 **應**&#x200B;在封 `etc/httpd` 存中使用首碼。

**在中找不到任何場`conf.dispatcher.d/enabled_farms`**

已啟用的場應位於上述子資料夾中。

**必須命名包含的檔案(...):...**

您的伺服器場配置中有兩個部分 **必須** 包括特定檔案： `/renders` 和 `/allowedClients` 的 `/cache` 的子菜單。 這些部分必須如下所示：

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

場配置中有四個部分，允許您包括自己的檔案： `/clientheaders`。 `filters`。 `/rules` 在 `/cache` 節和 `/virtualhosts`。 包含的檔案需要命名如下：

| 章節 | 包括檔案名 |
|------------------|--------------------------------------|
| `/clientheaders` | `../clientheaders/clientheaders.any` |
| `/filters` | `../filters/filters.any` |
| `/rules` | `../cache/rules.any` |
| `/virtualhosts` | `../virtualhosts/virtualhosts.any` |

或者，您也可以包含 **這些檔案的預設版本** ，其名稱會以字詞 `default_`為前置詞，例如。`../filters/default_filters.any`。

**包含位於(...)的語句，位於任何已知位置之外：...**

除上述六節外，您不得使用 `$include` 語句，例如，以下語句將生成此錯誤：

```
/invalidate {
    $include "../cache/invalidate.any"
}
```

**允許的客戶端/呈現不包括於：...**

如果未指定包含，則會生成此錯誤 `/renders` 和 `/allowedClients` 的 `/cache` 的子菜單。 查看
**必須命名包含的檔案(...):...** 的子菜單。

**篩選器不能使用glob模式允許請求**

不安全允許使用 `/glob` 樣式規則，與完整請求行匹配，例如

```
/0100 {
    /type "allow" /glob "GET *.css *"
}
```

此語句用於允許 `css` 檔案，但也允許請求 **任何** 資源後跟查詢字串 `?a=.css`。 因此，禁止使用此類過濾器（另見CVE-2016-0957）。

**包含的檔案(...)與任何已知檔案不匹配**

Apache虛擬主機配置中有兩種類型的檔案可指定為包括：重寫和變數。
包含的檔案需要命名如下：

| 類型 | 包括檔案名 |
|-----------|---------------------------------|
| 重寫 | `conf.d/rewrites/rewrite.rules` |
| 變數 | `conf.d/variables/custom.vars` |

或者，您可以 **預設** 重寫規則的版本，其名稱為 `conf.d/rewrites/default_rewrite.rules`。
請注意，變數檔案沒有預設版本。

**檢測到不建議使用的配置佈局，啟用相容模式**

此消息表示您的配置具有不建議使用的版本1佈局，包含完整的Apache配置和檔案， `ams_` 前置詞。 雖然仍然支援向後相容，但應切換到新佈局。

請注意，第一階段也 **單獨運行**，而不是包裝 `validate.sh` 的下界。

當你用手工製品或 `dispatcher/src` 子目錄，它將報告驗證失敗：

```
$ validator full -relaxed dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-allowlisted directives:
  conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
  conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

在Windows上，調度程式驗證程式區分大小寫。 因此，如果您不尊重配置所在路徑的大寫，則無法驗證配置，例如：

```
bin\validator.exe -relaxed full src
Cloud manager validator 2.0.xx
2021/03/15 18:15:40 Dispatcher configuration validation failed:
  conf.dispatcher.d\available_farms\default.farm:15: parent directory outside server root: c:\k\a\aem-dispatcher-sdk-windows-symlinks-testing3\dispatcher\src
```

通過從Windows資源管理器中複製並貼上路徑，然後使用 `cd` 命令進入該路徑。

### 階段2 {#second-phase}

此階段通過在映像中啟動Docker來檢查apache語法。 Docker必須在本地安裝，但請注意，不需要AEM運行。

>[!NOTE]
>
>Windows用戶需要使用Windows 10專業版或支援Docker的其他發行版。 這是在本地電腦上運行和調試Dispatcher的先決條件。

此階段也可獨立運行 `bin/docker_run.sh src/dispatcher host.docker.internal:4503 8080`。

在部署雲管理器期間， `httpd -t` 還將執行語法檢查，並且任何錯誤都將包含在Cloud Manager生成映像步驟失敗日誌中。

### 階段3 {#third-phase}

如果此階段出現故障，則表明Adobe已更改一個或多個不可變檔案，並且您必須用在 `src` SDK的目錄。 下面的日誌示例說明了此問題：

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

此階段也可獨立運行 `bin/docker_immutability_check.sh src/dispatcher`。

## 調試Apache和Dispatcher配置 {#debugging-apache-and-dispatcher-configuration}

請注意，您可以使用 `./bin/docker_run.sh src/dispatcher docker.for.mac.localhost:4503 8080`。

如前所述，Docker必須本地安裝，並且不必AEM運行。 Windows用戶需要使用Windows 10專業版或支援Docker的其他發行版。 這是在本地電腦上運行和調試Dispatcher的先決條件。

以下策略可用於增加Dispatcher模組的日誌輸出，並查看 `RewriteRule` 在本地和雲環境中進行評估。

這些模組的日誌級別由變數定義 `DISP_LOG_LEVEL` 和 `REWRITE_LOG_LEVEL`。 可以在檔案中設定 `conf.d/variables/global.vars`。 其相關部分如下：

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

在本地運行Dispatcher時，日誌會直接打印到終端輸出。 大多數時候，您希望這些日誌處於DEBUG中，這可以通過在運行Docker時將調試級別作為參數傳遞來完成。 例如： `DISP_LOG_LEVEL=Debug ./bin/docker_run.sh src docker.for.mac.localhost:4503 8080`。

雲環境的日誌通過Cloud Manager中提供的日誌服務公開。

## 每個環境的不同Dispatcher配置 {#different-dispatcher-configurations-per-environment}

當前，同一Dispatcher配置應用於所有AEMas a Cloud Service環境。 運行時將具有環境變數 `ENVIRONMENT_TYPE` 包含當前運行模式（dev、stage或prod）以及定義。 定義可以是 `ENVIRONMENT_DEV`。 `ENVIRONMENT_STAGE` 或 `ENVIRONMENT_PROD`。 在Apache配置中，變數可以直接在表達式中使用。 或者，定義可用於生成邏輯：

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

在Dispatcher配置中，可以使用相同的環境變數。 如果需要更多邏輯，請定義上例所示的變數，然後在Dispatcher配置部分中使用這些變數：

```
/virtualhosts {
  { "${VIRTUALHOST}" }
}
```

或者，您可以在httpd/dispatcher配置中使用Cloud Manager環境變數。 如果程式具有多個開發環境，並且其中某些開發環境對httpd/dispatcher配置具有不同的值，則此方法尤其重要。 將使用與上例相同的${VIRTUALHOST}語法，但不會使用上述變數檔案中的Define聲明。 閱讀 [Cloud Manager文檔](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/environment-variables.html?lang=en) 有關配置Cloud Manager環境變數的說明。

在本地測試配置時，可以通過傳遞變數來模擬不同的環境類型 `DISP_RUN_MODE` 到 `docker_run.sh` 指令碼直接：

```
$ DISP_RUN_MODE=stage docker_run.sh src docker.for.mac.localhost:4503 8080
```

當未傳遞DISP_RUN_MODE的值時，預設運行模式為&quot;dev&quot;。
有關可用選項和變數的完整清單，請運行指令碼 `docker_run.sh` 沒有參數。

## 查看Docker容器正在使用的Dispatcher配置 {#viewing-dispatcher-configuration-in-use-by-docker-container}

對於特定於環境的配置，可能很難確定實際的Dispatcher配置的樣式。 在啟動您的Docker容器後 `docker_run.sh` 可以按如下方式傾棄：

* 確定正在使用的Docker容器ID:

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

## 從舊模式遷移到靈活模式 {#migrating}

隨著Cloud Manager 2021.7.0版的推出，新的Cloud Manager程式將生成許多項目結構 [原AEM型28](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=en) 或更高版本，包括檔案 **opt-in/USE_SOURCES_DIRECTLY**。 這將刪除 [舊模式](/help/implementing/dispatcher/validation-debug-legacy.md) 在檔案數量和大小上，還會導致SDK和運行時以改進的方式驗證和部署配置。 如果您的調度程式配置沒有此檔案，強烈建議您遷移。 使用以下步驟確保安全過渡：

1. **本地測試。** 使用最新的調度程式工具SDK添加資料夾和檔案 `opt-in/USE_SOURCES_DIRECTLY`。 按照本文中的「本地驗證」說明test調度程式在本地工作。
2. **雲開發測試：**
   * 提交檔案 `opt-in/USE_SOURCES_DIRECTLY` 到由非生產管道部署到雲開發環境的git分支。
   * 使用Cloud Manager部署到雲開發環境。
   * Test。 在將更改部署到更高的環境之前，必須驗證您的apache和分派程式配置是否像您預期的那樣工作。 檢查與自定義配置相關的所有行為！ 如果您認為部署的調度程式配置不反映您的自定義配置，請提交客戶支援票證。
3. **部署到生產：**
   * 提交檔案 `opt-in/USE_SOURCES_DIRECTLY` 到生產管道部署到雲階段和生產環境的git分支。
   * 使用雲管理器部署到暫存。
   * Test。 在將更改部署到更高的環境之前，必須驗證您的apache和分派程式配置是否像您預期的那樣工作。 檢查與自定義配置相關的所有行為！ 如果您認為部署的調度程式配置不反映您的自定義配置，請提交客戶支援票證。
   * 使用雲管理器繼續將部署到生產環境中。
