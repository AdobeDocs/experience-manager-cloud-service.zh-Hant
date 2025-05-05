---
title: 使用Dispatcher工具進行驗證和偵錯（舊版）
description: 使用Dispatcher工具進行驗證和偵錯（舊版）
feature: Dispatcher
hidefromtoc: true
exl-id: dc04d035-f002-42ef-9c2e-77602910c2ec
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '2337'
ht-degree: 1%

---

# 使用Dispatcher工具進行驗證和偵錯（舊版）  {#Dispatcher-tools-legacy}

## 簡介 {#apache-and-dispatcher-configuration-and-testing}

>[!NOTE]
>如需雲端中Dispatcher以及如何下載Dispatcher工具的詳細資訊，請參閱雲端中[Dispatcher](/help/implementing/dispatcher/disp-overview.md)頁面。

以下章節說明舊版模式的檔案結構、本機驗證、偵錯以及如何從舊版模式移轉至[彈性模式](/help/implementing/dispatcher/validation-debug.md)。

本文假設您專案的Dispatcher設定不包含檔案選擇加入/USE_SOURCES_DIRECTLY。 因此，檔案的數目和大小受到限制，例如：

* 必須使用單一重寫檔案，而非網站專屬的檔案。
* 可自訂檔案的內容總和必須小於1 MB。

截至Cloud Manager 2021.7.0版，新的Cloud Manager計畫會產生AEM原型28及更高版本的maven專案結構，其中包括前述的檔案。

**強烈建議**&#x200B;您從舊版模式移轉至彈性模式，如移轉區段[從舊版模式移轉至彈性模式](#migrating-flexible)中所述。 使用彈性模式也會讓SDK和執行階段以改良的方式驗證和部署設定。

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

以下是可修改之重要檔案的說明：

**可自訂的檔案**

以下檔案可自訂，並在部署時傳輸到您的雲端執行個體：

* `conf.d/available_vhosts/<CUSTOMER_CHOICE>.vhost`

您可以有一或多個這些檔案。 它們包含符合主機名稱的`<VirtualHost>`專案，並允許Apache使用不同規則處理每個網域流量。 在`available_vhosts`目錄中建立檔案，並在`enabled_vhosts`目錄中啟用符號連結。 從`.vhost`個檔案中，包含其他檔案，例如重寫與變數。

* `conf.d/rewrites/rewrite.rules`

此檔案包含在您的`.vhost`檔案中。 它有一組`mod_rewrite`的重寫規則。

>[!NOTE]
>
>目前，必須使用單一重寫檔案，而非網站專屬的檔案。 一般而言，可自訂檔案的內容總和必須小於1 MB。

* `conf.d/variables/custom.vars`

此檔案包含在您的`.vhost`檔案中。 您可以在此位置新增Apache變數的定義。

* `conf.d/variables/global.vars`

此檔案包含在`dispatcher_vhost.conf`檔案內。 您可以變更您的Dispatcher並重新寫入此檔案中的記錄層級。

* `conf.dispatcher.d/available_farms/<CUSTOMER_CHOICE>.farm`

您可以有一或多個這類檔案，而且這些檔案包含陣列以符合主機名稱，並允許Dispatcher模組使用不同規則處理每個陣列。 在`available_farms`目錄中建立檔案，並在`enabled_farms`目錄中啟用符號連結。 從`.farm`個檔案中，包含其他檔案，例如篩選器、快取規則等。

* `conf.dispatcher.d/cache/rules.any`

此檔案包含在您的`.farm`檔案中。 它會指定快取偏好設定。

* `conf.dispatcher.d/clientheaders/clientheaders.any`

此檔案包含在您的`.farm`檔案中。 它會指定應該將哪些請求標頭轉送至後端。

* `conf.dispatcher.d/filters/filters.any`

此檔案包含在您的`.farm`檔案中。 它有一組規則可變更應該過濾掉的流量，而不會使其進入後端。

* `conf.dispatcher.d/virtualhosts/virtualhosts.any`

此檔案包含在您的`.farm`檔案中。 它有一個主機名稱或URI路徑的清單，將透過glob比對進行比對。 此比對會決定使用哪個後端來處理請求。

上述檔案參照下列不可變的組態檔。 雲端環境中的Dispatcher不會處理不可變檔案的變更。

**不可變組態檔**

這些檔案是基本框架的一部分，可強制實施標準和最佳實務。 這些檔案被視為不可變，因為在本機修改或刪除它們不會對您的部署造成影響，因為它們不會傳輸到您的雲端執行個體。

建議上述檔案參照下列不可變檔案，然後加上任何其他陳述式或覆寫。 將Dispatcher設定部署到雲端環境時，無論本機開發中使用了哪個版本，都會使用最新版本的不可變檔案。

* `conf.d/available_vhosts/default.vhost`

包含範例虛擬主機。 針對您自己的虛擬主機，建立此檔案的復本、自訂該檔案、移至`conf.d/enabled_vhosts`並建立指向您自訂復本的符號連結。

* `conf.d/dispatcher_vhost.conf`

基本框架的一部分，用來說明如何包含虛擬主機和全域變數。

* `conf.d/rewrites/default_rewrite.rules`

適用於標準專案的預設重寫規則。 如果您需要自訂，請編輯`rewrite.rules`。 自訂時，如果預設規則符合您的需求，您仍可先包含這些規則。

* `conf.dispatcher.d/available_farms/default.farm`

包含範例Dispatcher陣列。 針對您自己的伺服器陣列，建立此檔案的復本、自訂該檔案、移至`conf.d/enabled_farms`並建立符號連結至您的自訂復本。

* `conf.dispatcher.d/cache/default_invalidate.any`

基礎框架的一部分，在啟動時產生。 您&#x200B;**需要**，才能在`cache/allowedClients`區段中將此檔案納入您定義的每個伺服器陣列。

* `conf.dispatcher.d/cache/default_rules.any`

適用於標準專案的預設快取規則。 如果您需要自訂，請修改`conf.dispatcher.d/cache/rules.any`。 自訂時，如果預設規則符合您的需求，您仍可先包含這些規則。

* `conf.dispatcher.d/clientheaders/default_clientheaders.any`

轉送至後端的預設請求標頭，適用於標準專案。 如果您需要自訂，請修改`clientheaders.any`。 自訂後，您仍可先納入預設的要求標題（若符合您的需求）。

* `conf.dispatcher.d/dispatcher.any`

基本框架的一部分，用於說明如何包含您的Dispatcher陣列。

* `conf.dispatcher.d/filters/default_filters.any`

適用於標準專案的預設篩選器。 如果您需要自訂，請修改`filters.any`。 在您的自訂中，如果預設篩選器符合您的需求，您仍可先包含這些篩選器。

* `conf.dispatcher.d/renders/default_renders.any`

此檔案屬於基礎架構的一部分，會在啟動時產生。 您&#x200B;**需要**，才能在`renders`區段中將此檔案納入您定義的每個伺服器陣列。

* `conf.dispatcher.d/virtualhosts/default_virtualhosts.any`

適用於標準專案的預設主機萬用字元。 如果您需要自訂，請修改`virtualhosts.any`。 在您的自訂中，您不應該包含預設主機萬用字元，因為它符合&#x200B;**every**&#x200B;傳入的要求。

## 支援的 Apache 模組 {#apache-modules}

請參閱[支援的Apache模組](/help/implementing/dispatcher/disp-overview.md#supported-directives)。

## 本機驗證 {#local-validation-legacy-mode}

>[!NOTE]
>以下各節包含使用Mac或Linux®版SDK的命令，但Windows SDK也可以透過類似方式使用。

使用`validate.sh`指令碼，如下所示：

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

1. 它會執行驗證器。 如果設定無效，指令碼會失敗。
2. 它會執行`httpd -t`命令來測試語法是否正確，以便Apache httpd可以啟動。 如果成功，設定應準備好進行部署。
3. 檢查Dispatcher SDK組態檔的子集（預期會如[檔案結構區段](##legacy-mode-file-structure)中所述，不可變動）是否尚未編輯。 此檢查是全新功能，已於AEM SDK v2021.1.4738推出，其中也包含Dispatcher Tools 2.0.36版。在此更新之前，客戶可能錯誤地認為這些不可變檔案的任何本機SDK修改也將套用至雲端環境。

在Cloud Manager部署期間，也會執行`httpd -t`語法檢查，且任何錯誤都會包含在Cloud Manager `Build Images step failure`記錄檔中。

### 階段1 {#first-phase}

如果指示詞未加入允許清單，工具會記錄錯誤並傳回非零的退出代碼。 此外，它會進一步掃描所有具有模式`conf.dispatcher.d/enabled_farms/*.farm`的檔案，並檢查：

* 不存在允許透過`/glob`使用的篩選器規則（如需詳細資訊，請參閱[CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957)）。
* 未公開任何管理功能。 例如，存取路徑，例如`/crx/de or /system/console`。

驗證工具僅報告未列入允許清單的Apache指令的禁用情況。 不會報告您的Apache設定的語法或語意問題，因為此資訊僅供執行環境中的Apache模組使用。

以下提供工具輸出之常見驗證錯誤的疑難排解技巧：

**在封存中找不到`conf.dispatcher.d`子資料夾**

您的封存應包含資料 `conf.d` 夾和 `conf.dispatcher.d`。請注意，您不 **應**&#x200B;在封 `etc/httpd` 存中使用首碼。

**在`conf.dispatcher.d/enabled_farms`**&#x200B;中找不到任何陣列

您啟用的陣列應位於提及的子資料夾中。

**包含的檔案(...)必須命名為： ...**

您的伺服器陣列設定中有兩個區段，**必須**&#x200B;包含一個
特定檔案： `/cache`區段中的`/renders`和`/allowedClients`。 這些
區段必須如下所示：

```
/renders {
    $include "../renders/default_renders.any"
}
```

以及：

```
/allowedClients {
    $include "../cache/default_invalidate.any"
}
```

**檔案包含在未知的位置： ...**

您的伺服器陣列設定中有四個區段，允許您包含自己的檔案： `/cache`區段中的`/clientheaders`、`filters`、`/rules`以及`/virtualhosts`。 包含的檔案必須依下列方式命名：

| 區段 | 包含檔案名稱 |
|------------------|--------------------------------------|
| `/clientheaders` | `../clientheaders/clientheaders.any` |
| `/filters` | `../filters/filters.any` |
| `/rules` | `../cache/rules.any` |
| `/virtualhosts` | `../virtualhosts/virtualhosts.any` |

或者，您也可以包含這些檔案的&#x200B;**預設**&#x200B;版本，其名稱會以單字`default_`為前置詞，例如`../filters/default_filters.any`。

**Include陳述式位於(...)，在任何已知位置之外： ...**

除了上述段落中提及的六個區段以外，您不可以
例如，若要使用`$include`陳述式，下列專案會產生此錯誤：

```
/invalidate {
    $include "../cache/invalidate.any"
}
```

**不允許的使用者端/轉譯器不包括： ...**

當您未在`/cache`區段中為`/renders`和`/allowedClients`指定「包含」時，會產生此錯誤。 請參閱
**包含的檔案(...)必須命名為： ...**&#x200B;區段以取得詳細資訊。

**篩選器不能使用glob模式來允許請求**

允許具有`/glob`樣式規則的請求是不安全的，該規則與完整的請求行相符，例如

```
/0100 {
    /type "allow" /glob "GET *.css *"
}
```

此陳述式可允許要求`css`個檔案，但同時也允許要求&#x200B;**任何**&#x200B;資源，後面接著查詢字串`?a=.css`。 因此，禁止使用這類篩選器（另請參閱CVE-2016-0957）。

**包含的檔案(...)不符合任何已知檔案**

Apache虛擬主機設定中有兩種型別的檔案可指定為包含：重寫與變數。
包含的檔案必須依下列方式命名：

| 類型 | 包含檔案名稱 |
|-----------|---------------------------------|
| 重寫 | `conf.d/rewrites/rewrite.rules` |
| 變數 | `conf.d/variables/custom.vars` |

>[!TIP]
>
>為了能夠以更少限制的方式包含更多檔案，您可能會想要切換為彈性的Dispatcher設定模式。 如需有關彈性模式的詳細資訊，請參閱[使用Dispatcher工具進行驗證和偵錯](/help/implementing/dispatcher/validation-debug.md)。

或者，您也可以包含名稱為`conf.d/rewrites/default_rewrite.rules`的&#x200B;**預設**&#x200B;版本重寫規則。
請注意，變數檔案沒有預設版本。

**偵測到已棄用的組態配置，正在啟用相容性模式**

此訊息指出您的設定有已棄用的版本1版面，其中包含完整的
具有`ams_`首碼的Apache設定和檔案。 雖然此設定仍支援回溯
相容性，您應該切換至新版面。

第一個階段也可以是&#x200B;**單獨執行**，而不是從包裝函式`validate.sh`指令碼執行。

當針對您的Maven成品或`dispatcher/src`子目錄執行時，它會報告驗證失敗：

```
$ validator full dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-allowlisted directives:
  conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
  conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

在Windows上，Dispatcher驗證器會區分大小寫。 因此，如果您不遵循設定所在路徑的大小寫，例如：

```
bin\validator.exe full src
Cloud manager validator 2.0.xx
2021/03/15 18:15:40 Dispatcher configuration validation failed:
  conf.dispatcher.d\available_farms\default.farm:15: parent directory outside server root: c:\k\a\aem-dispatcher-sdk-windows-symlinks-testing3\dispatcher\src
  
```

從Windows檔案總管複製並貼上路徑，然後在命令提示字元上使用`cd`命令將路徑複製到該路徑，以避免此錯誤。

### 階段2 {#second-phase}

此階段會透過在影像中啟動Docker來檢查Apache語法。 Docker必須安裝在本機，但請注意，AEM不需要運行。

>[!NOTE]
>Windows使用者必須使用支援Docker的Windows 10 Professional或其他發行版本。 若要在本機電腦上執行並偵錯Dispatcher，必須具備此先決條件。

此階段也可以透過`validator full -d out src/dispatcher`獨立執行，這會產生下一個命令`bin/docker_run.sh out host.docker.internal:4503 8080`所需的「out」目錄。

在Cloud Manager部署期間，會執行`httpd -t`語法檢查，所有錯誤都包含在Cloud Manager組建影像步驟失敗記錄檔中。

### 階段3 {#third-phase}

如果在此階段失敗，則表示Adobe已變更一個或多個不可變檔案。 在這種情況下，您必須以SDK `src`目錄中傳送的新版本，取代對應的不可變檔案。 以下記錄範例說明此問題：

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

此階段也可以透過`validator full -d out src/dispatcher`獨立執行，這會產生下一個命令`bin/docker_immutability_check.sh out`所需的「out」目錄。

## 偵錯您的Apache和Dispatcher設定 {#debugging-apache-and-dispatcher-configuration}

您可以使用`./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`在本機執行Apache Dispatcher。

如前所述，必須在本機安裝Docker，AEM不需要運行。 Windows使用者必須使用支援Docker的Windows 10 Professional或其他發行版本。 若要在本機電腦上執行並偵錯Dispatcher，必須具備此先決條件。

下列策略可用來增加Dispatcher模組的記錄輸出，並在本機與雲端環境中檢視`RewriteRule`評估的結果。

這些模組的記錄層級是由變數`DISP_LOG_LEVEL`和`REWRITE_LOG_LEVEL`所定義。 它們可以在檔案`conf.d/variables/global.vars`中設定。 其相關部分如下：

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

在本機執行Dispatcher時，記錄會直接列印到終端機輸出。 大多數情況下，您都希望這些記錄位於DEBUG中，這可以通過在執行Docker時傳遞偵錯級別作為引數來完成。 例如：`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`。

雲端環境的記錄會透過Cloud Manager提供的記錄服務公開。

## 每個環境有不同的Dispatcher設定 {#different-dispatcher-configurations-per-environment}

目前，相同的Dispatcher設定已套用至AEM as a Cloud Service上的所有環境。 執行階段有包含目前執行模式（dev、stag或prod）的環境變數`ENVIRONMENT_TYPE`和定義。 定義可以是`ENVIRONMENT_DEV`、`ENVIRONMENT_STAGE`或`ENVIRONMENT_PROD`。 在Apache設定中，變數可直接在運算式中使用。 或者，也可使用定義來建置邏輯：

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

在Dispatcher設定中，可使用相同的環境變數。 如需更多邏輯，請定義上述範例中的變數，然後在Dispatcher設定區段中使用它們：

```
/virtualhosts {
  { "${VIRTUALHOST}" }
}
```

在本機測試您的設定時，您可以直接將變數`DISP_RUN_MODE`傳遞到`docker_run.sh`指令碼來模擬不同的環境型別：

```
$ DISP_RUN_MODE=stage docker_run.sh out docker.for.mac.localhost:4503 8080
```

不傳入DISP_RUN_MODE的值時，預設的執行模式為「dev」。
如需可用選項和變數的完整清單，請執行指令碼`docker_run.sh`，但不使用引數。

## 檢視Docker容器正在使用的Dispatcher配置 {#viewing-dispatcher-configuration-in-use-by-docker-container}

透過特定環境的設定，可能很難判斷實際的Dispatcher設定是什麼樣子。 使用`docker_run.sh`啟動您的Docker容器後，可以如下傾印：

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

## 從舊版模式移轉至彈性模式 {#migrating-flexible}

在Cloud Manager 2021.7.0版本中，新的Cloud Manager程式會產生AEM原型為28或更高版本的Maven專案結構，其中包括檔案&#x200B;**opt-in/USE_SOURCES_DIRECTLY**。 舊版模式先前對檔案數量和大小的限制已移除，也會導致SDK和執行階段以改良的方式驗證和部署設定。 如果您的Dispatcher設定沒有此檔案，強烈建議您進行移轉。 使用[彈性模式](/help/implementing/dispatcher/validation-debug.md#migrating)頁面中說明的方法。
