---
title: 為 AEM as a Cloud Service 設定 OSGi
description: '具有機密值和環境特定值的OSGi配置 '
translation-type: tm+mt
source-git-commit: 0a2d44a63c3d26460c0836ab6b28989a0aad72da
workflow-type: tm+mt
source-wordcount: '2737'
ht-degree: 1%

---


# 為 AEM as a Cloud Service 設定 OSGi {#configuring-osgi-for-aem-as-a-cloud-service}

[OSGi](https://www.osgi.org/) 是Adobe Experience Manager(AEM)技術堆疊中的基本元素。 它用於控制AEM的組合束及其配置。

OSGi提供標準化的基元，可讓應用程式從可重複使用的小型元件和協作元件建構。 這些元件可組成應用程式並加以部署。 這樣可以輕鬆管理OSGi捆綁包，因為它們可以單獨停止、安裝和啟動。 互依關係會自動處理。 每個OSGi元件都包含在其中一個不同的束中。 如需詳細資訊，請參閱 [OSGi規格](https://www.osgi.org/Specifications/HomePage)。

您可以透過屬於AEM程式碼專案一部分的設定檔案，管理OSGi元件的設定設定。

## OSGi配置檔案 {#osgi-configuration-files}

組態變更在AEM Project的程式碼套件(`ui.apps`)中定義為執行模式特定組態檔案夾下的組態檔(`.cfg.json`):

`/apps/example/config.<runmode>`

OSGi組態檔的格式是以JSON為基礎，使用Apache Sling `.cfg.json` 專案所定義的格式。

OSGi配置通過其持久性標識(PID)定位OSGi元件，該標識預設為OSGi元件的Java類名。 例如，要為由以下項目實施的OSGi服務提供OSGi配置：

`com.example.workflow.impl.ApprovalWorkflow.java`

an OSGi configuration file is defined at:

`/apps/example/config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`

遵循cfg.json OSGi組態格式。

>[!NOTE]
>
>舊版AEM支援的OSGi組態檔案，使用不同的檔案格式，例如。cfg.、.config和XML sling:OsgiConfig資源定義。 這些格式由cfg.json OSGi組態格式取代。

## 執行模式解析度 {#runmode-resolution}

使用執行模式，可將特定OSGi組態定位至特定AEM例項。 若要使用runmode，請在下列格式下 `/apps/example` 建立設定資料夾（其中專案名稱為範例）:

`/apps/example/config.<author|publish>.<dev|stage|prod>/`

如果設定檔案夾名稱中定義的執行模式與AEM使用的執行模式相符，則會使用此類檔案夾中的任何OSGi組態。

例如，如果AEM使用runmodes作者和dev，則會套用 `/apps/example/config.author/` 和 `/apps/example/config.author.dev/` 中的設定節點，而不會套用和 `/apps/example/config.publish/` 中的 `/apps/example/config.author.stage/` 設定節點。

如果同一PID的多個配置適用，則應用具有最多匹配運行模式的配置。

此規則的詳細程度為PID層級。 這表示您無法在相同PID中定義某些屬性，而 `/apps/example/config.author/` 在相同PID中定義更 `/apps/example/config.author.dev/` 多特定屬性。  對於整個PID，具有最多匹配運行模式的配置將有效。

在本機開發時，可傳入runmode啟動參數，以指定將使用哪個runmode OSGI組態。

## OSGi配置值的類型 {#types-of-osgi-configuration-values}

AEM可搭配雲端服務使用三種OSGi組態值。

1. **內嵌值**，這些值是硬式編碼至OSGi組態並儲存在Git中的值。 例如：

   ```json
   {
      "connection.timeout": 1000
   }
   ```

1. **機密值**，這些值是出於安全原因不應儲存在Git中的值。 例如：

   ```json
   {
   "api-key": "$[secret:server-api-key]"
   } 
   ```

1. **環境特定值**，這些值在開發環境之間會有所不同，因此無法依執行模式精確定位(因為AEM中有單一執行模式， `dev` 即雲端服務)。 例如：

   ```json
   {
    "url": "$[env:server-url]"
   }
   ```

   請注意，單個OSGi配置檔案可以結合使用這些配置值類型的任意組合。 例如：

   ```json
   {
   "connection.timeout": 1000,
   "api-key": "$[secret:server-api-key]",
   "url": "$[env:server-url]"
   }
   ```

## 如何選擇適當的OSGi配置值類型 {#how-to-choose-the-appropriate-osgi-configuration-value-type}

OSGi的常見情況是使用內嵌OSGi配置值。 特定環境的配置僅用於開發環境之間值不同的特定使用情形。

![](assets/choose-configuration-value-type_res1.png)

環境特定配置擴展了包含內嵌值的傳統靜態定義OSGi配置，從而提供了通過Cloud Manager API在外部管理OSGi配置值的能力。 必須瞭解何時應使用定義內嵌值並將其儲存在Git中的常見和傳統方法，而不是將值抽象為特定環境的配置。

以下指南說明何時使用非機密和機密環境特定組態：

### 使用內嵌配置值的時機 {#when-to-use-inline-configuration-values}

內嵌組態值被視為標準方法，並應盡可能使用。 內嵌配置提供以下優點：

* 它們會維護，並使用Git的管理和版本記錄
* 值會隱含地系結至程式碼部署
* 它們不需要任何額外的部署考慮或協調

每當定義OSGi配置值時，請從內嵌值開始，只要在使用案例中需要，任何配置都只選擇機密或環境特定的配置。

### 何時使用非機密環境特定配置值 {#when-to-use-non-secret-environment-specific-configuration-values}

當值在開發環境中不同時，`$[env:ENV_VAR_NAME]`僅對非機密配置值使用環境特定配置()。 這包括本機開發執行個體和任何AEM做為雲端服務開發環境。 請避免將AEM的非機密環境特定組態用作雲端服務階段或生產環境。

* 僅針對不同開發環境（包括本地開發實例）的配置值使用非機密的環境特定配置。
* 請改用OSGi組態中的標準內嵌值，以用於「舞台(Stage)」和「生產(Production)」非機密值。  與此相關，不建議使用環境特定的配置，以便在執行時期對舞台和生產環境進行配置更改；這些變更應透過原始碼管理引入。

### 何時使用機密環境特定配置值 {#when-to-use-secret-environment-specific-configuration-values}

AEM作為雲端服務，需要針對任何機密OSGi組態值（例如密碼、私用API金鑰）使用環境特定的組態(`$[secret:SECRET_VAR_NAME]`)，或因安全原因無法儲存在Git中的任何其他值。

使用機密環境特定組態，將所有AEM上機密的值儲存為雲端服務環境，包括「舞台(Stage)」和「生產(Production)」。

<!-- ### Adding a New Configuration to the Repository {#adding-a-new-configuration-to-the-repository}

#### What You Need to Know {#what-you-need-to-know}

To add a new configuration to the repository you need to know the following:

1. The **Persistent Identity** (PID) of the service.

   Reference the **Configurations** field in the Web console. The name is shown in brackets after the bundle name (or in the **Configuration Information** towards the bottom of the page).

   For example, create a node `com.day.cq.wcm.core.impl.VersionManagerImpl.` to configure **AEM WCM Version Manager**.

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. Whether a specific runmode is required. Create the folder:

    * `config` - for all run modes
    * `config.author` - for the author environment
    * `config.publish` - for the publish environment
    * `config.<run-mode>` - as appropriate

1. Whether a **Configuration** or **Factory Configuration** is necessary.
1. The individual parameters to be configured; including any existing parameter definitions that will need to be recreated.

   Reference the individual parameter field in the Web console. The name is shown in brackets for each parameter.

   For example, create a property
   `versionmanager.createVersionOnActivation` to configure **Create Version on Activation**.

   ![chlimage_1-142](assets/chlimage_1-142.png)

1. Does a configuration already exist in `/libs`? To list all configurations in your instance, use the **Query** tool in CRXDE Lite to submit the following SQL query:

   `select * from sling:OsgiConfig`

   If so, this configuration can be copied to ` /apps/<yourProject>/`, then customized in the new location. -->

## 建立OSGi配置

建立新OSGi配置有兩種方法，如下所述。 前一種方法通常用於設定由開發人員具備眾所周知OSGi屬性和值的自訂OSGi元件，後一種方法則用於AEM提供的OSGi元件。

### 編寫OSGi配置

JSON格式的OSGi組態檔可直接手動寫入AEM專案。 這通常是為知名的OSGi元件建立OSGi配置的最快方法，尤其是由定義這些配置的同一開發人員設計和開發的定製OSGi元件。 此方法還可用於複製／貼上和更新不同運行模式資料夾中相同OSGi元件的配置。

1. 在IDE中，開啟項 `ui.apps` 目，找到或建立配置資料夾(`/apps/.../config.<runmode>`)，該資料夾針對新OSGi配置應生效的運行模式
1. 在此配置資料夾中，建立新 `<PID>.cfg.json` 檔案。 PID是OSGi元件的持久標識通常是OSGi元件實施的完整類名。 例如：
   `/apps/.../config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`
請注意，OSGi配置工廠檔案名，請使用 `<PID>-<factory-name>.cfg.json` 命名約定
1. 開啟新 `.cfg.json` 檔案，並依 [JSON OSGi組態格式定義OSGi屬性和值配對的鍵／值組合](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1)。
1. 儲存您對新檔案的變 `.cfg.json` 更
1. 將新的OSGi配置檔案添加並提交到Git

### 使用AEM SDK快速入門產生OSGi設定

AEM SDK Quickstart Jar的AEM Web Console可用來設定OSGi元件，並將OSGi組態匯出為JSON。 這對於設定AEM提供的OSGi元件很有用，其OSGi屬性及其值格式可能無法由開發人員在AEM專案中定義OSGi組態。 請注意，使用AEM Web Console的「設定UI」會將檔案寫入儲存庫，因此請注意，當AEM Project定義的OSGi組態可能與產生的組態不同時，可避免在本機開發期間發生意外行為。 `.cfg.json`

1. 以管理員使用者身分登入AEM SDK Quickstart Jar的AEM Web主控台
1. 導覽至「OSGi >設定」
1. 找到要設定的OSGi元件，並點選其標題以進行編輯
   ![OSGi配置](./assets/configuring-osgi/configuration.png)
1. 視需要透過Web UI編輯OSGi組態屬性值
1. 將永續性身分識別(PID)記錄到安全位置，稍後將用來產生OSGi設定JSON
1. 點選「儲存」
1. 導覽至「OSGi > OSGi安裝程式設定印表機」
1. 貼入步驟5中複製的PID中，確保「序列化格式」已設為「OSGi Configurator JSON」
1. 點選「列印」、
1. JSON格式的OSGi設定將顯示在「序列化設定屬性」區段中
   ![OSGi安裝程式配置打印機](./assets/configuring-osgi/osgi-installer-configurator-printer.png)
1. 在IDE中，開啟項 `ui.apps` 目，找到或建立配置資料夾(`/apps/.../config.<runmode>`)，該資料夾針對新OSGi配置應該生效的運行模式。
1. 在此配置資料夾中，建立新 `<PID>.cfg.json` 檔案。 PID與步驟5的值相同。
1. 將步驟10的序列化設定屬性貼入檔 `.cfg.json` 案。
1. 將變更儲存至新檔 `.cfg.json` 案。
1. 將新的OSGi配置檔案添加並提交到Git。


## OSGi配置屬性格式

### 內嵌值 {#inline-values}

如預期，內嵌值會依照標準JSON語法，格式化為標準名稱——值配對。 例如：

```json
{
   "my_var1": "val",
   "my_var2": [ "abc", "def" ],
   "my_var3": 500
}
```

### 環境特定配置值 {#environment-specific-configuration-values}

OSGi配置應為要根據環境定義的變數指定佔位符：

```
use $[env:ENV_VAR_NAME]
```

客戶只應將此技巧用於與其自訂程式碼相關的OSGI組態屬性；它不應用來覆寫Adobe定義的OSGI設定。

### 機密組態值 {#secret-configuration-values}

OSGi配置應為要根據環境定義的機密指定一個佔位符：

```
use $[secret:SECRET_VAR_NAME]
```

### 變數命名 {#variable-naming}

以下內容適用於特定環境和機密配置值。

變數名稱應遵循下列規則：

* 最小長度：2
* 最大長度：100
* 必須符合regex: `[a-zA-Z_][a-zA-Z_0-9]*`

變數的值不應超過2048個字元。

### 預設值 {#default-values}

以下內容適用於特定環境和機密配置值。

如果未設定每個環境的值，則在執行時期，預留位置器不會被取代並保留在原位，因為未發生內插。 為避免此問題，可使用下列語法將預設值提供為預留位置的一部分：

```
$[env:ENV_VAR_NAME;default=<value>]
```

在提供預設值後，預留位置將會取代為每個環境的值（如果提供）或提供的預設值。

### 地方開發 {#local-development}

以下內容適用於特定環境和機密配置值。

變數可在本機環境中定義，因此本機AEM會在執行時期擷取。 例如，在Linux上：

```bash
export ENV_VAR_NAME=my_value
```

建議您編寫簡單的bash指令碼，以設定在設定中使用的環境變數，並在啟動AEM之前加以執行。 https://direnv.net/等工 [具](https://direnv.net/) ，可協助簡化此方法。 視值類型而定，如果值可以在每個人之間共用，則可能會將其簽入原始碼管理。

機密值會從檔案中讀取。 因此，對於使用密碼的每個佔位符，需要建立包含密碼值的文本檔案。

例如，如 `$[secret:server_password]` 果使用，則需要建立名 **為server_password** 的文本檔案。 所有這些機密檔案都必須儲存在相同的目錄中，而framework屬性 `org.apache.felix.configadmin.plugin.interpolation.secretsdir` 必須以該本機目錄進行設定。

### 作者與發佈設定 {#author-vs-publish-configuration}

如果OSGI屬性要求作者與發佈的值不同：

* 應使 `config.author` 用個 `config.publish` 別和OSGi資料夾，如 [Runmode Resolution區段所述](#runmode-resolution)。
* 應使用獨立變數名稱。 建議使用前置詞，例如 `author_<variablename>` 和 `publish_<variablename>` 變數名稱相同

### 配置示例 {#configuration-examples}

在以下範例中，假設除了舞台和prod環境外，還有3個開發環境。

**範例1**

其目的是讓OSGI屬性的值在舞台和 `my_var1` prod上相同，但在3個開發環境中不同。

<table>
<tr>
<td>
<b>資料夾</b>
</td>
<td>
<b>myfile.cfg.json的內容</b>
</td>
</tr>
<tr>
<td>
config
</td>
<td>
<pre>
{ "my_var1":"val", "my_var2":"abc"、"my_var3":500}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1" :"$[env:my_var1]" "my_var2":"abc"、"my_var3":500}
</pre>
</td>
</tr>
</table>

**範例2**

其目的是讓OSGI屬性的值在舞台、 `my_var1` prod和3開發環境中的每個環境中不同。 因此，需要呼叫Cloud Manager API，以設定每個開發環境 `my_var1` 的值。

<table>
<tr>
<td>
<b>資料夾</b>
</td>
<td>
<b>myfile.cfg.json的內容</b>
</td>
</tr>
<tr>
<td>
config.stage
</td>
<td>
<pre>
{ "my_var1":"val1", "my_var2":"abc"、"my_var3":500}
</pre>
</td>
</tr>
<tr>
<td>
config.prod
</td>
<td>
<pre>
{ "my_var1":"val2", "my_var2":"abc"、"my_var3":500}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1" :"$[env:my_var1]" "my_var2":"abc"、"my_var3":500}
</pre>
</td>
</tr>
</table>

**範例3**

其目的是讓OSGi屬性的值在舞台、生產環境 `my_var1` ，以及其中一個開發環境上都相同，但在其他兩個開發環境上則不同。 在這種情況下，需要調用Cloud Manager API來設定每個開發環境的值， `my_var1` 包括應與舞台和生產環境具有相同值的開發環境的值。 它不會繼承資料夾配置中設定的 **值**。

<table>
<tr>
<td>
<b>資料夾</b>
</td>
<td>
<b>myfile.cfg.json的內容</b>
</td>
</tr>
<tr>
<td>
config
</td>
<td>
<pre>
{ "my_var1":"val1", "my_var2":"abc"、"my_var3":500}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1" :"$[env:my_var1]" "my_var2":"abc"、"my_var3":500}
</pre>
</td>
</tr>
</table>

要達到此目的，另一種方法是在config.dev資料夾中設定取代Token的預設值，使其與 **config** 資料夾中相同。

<table>
<tr>
<td>
<b>資料夾</b>
</td>
<td>
<b>myfile.cfg.json的內容</b>
</td>
</tr>
<tr>
<td>
config
</td>
<td>
<pre>
{ "my_var1":"val1", "my_var2":"abc"、"my_var3":500}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1":"$[env:my_var1;default=val1]" "my_var2":"abc"、"my_var3":500}
</pre>
</td>
</tr>
</table>

## 設定屬性的Cloud Manager API格式 {#cloud-manager-api-format-for-setting-properties}

請參 [閱本頁](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/create-api-integration.md) ，瞭解如何設定API。
>[!NOTE]
>
>請確定已使用的Cloud Manager API已指派角色「部署管理員——雲端服務」。 其他角色無法執行以下所有命令。

### 透過API設定值 {#setting-values-via-api}

呼叫API會將新變數和值部署至雲端環境，類似於一般的客戶程式碼部署管道。 作者和發佈服務將會重新啟動並參考新值，通常需要幾分鐘的時間。

```
PATCH /program/{programId}/environment/{environmentId}/variables
```

```
]
        {
                "name" : "MY_VAR1",
                "value" : "plaintext value",
                "type" : "string"  <---default
        },
        {
                "name" : "MY_VAR2",
                "value" : "<secret value>",
                "type" : "secretString"
        }
]
```

請注意，預設變數不是透過API設定，而是在OSGi屬性本身中。

如需 [詳細資訊](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Environment_Variables/patchEnvironmentVariables) ，請參閱本頁。

### 透過API取得值 {#getting-values-via-api}

```
GET /program/{programId}/environment/{environmentId}/variables
```

如需 [詳細資訊](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Environment_Variables/getEnvironmentVariables) ，請參閱本頁。

### 透過API刪除值 {#deleting-values-via-api}

```
PATCH /program/{programId}/environment/{environmentId}/variables
```

若要刪除變數，請將其加入空白值。

如需 [詳細資訊](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Environment_Variables/patchEnvironmentVariables) ，請參閱本頁。

### 通過命令行獲取值 {#getting-values-via-cli}

```bash
$ aio cloudmanager:list-environment-variables ENVIRONMENT_ID
Name     Type         Value
MY_VAR1  string       plaintext value 
MY_VAR2  secretString ****
```


### 通過命令行設定值 {#setting-values-via-cli}

```bash
$ aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable MY_VAR1 "plaintext value" --secret MY_VAR2 "some secret value"
```

### 通過命令行刪除值 {#deleting-values-via-cli}

```bash
$ aio cloudmanager:set-environment-variables ENVIRONMENT_ID --delete MY_VAR1 MY_VAR2
```

>[!NOTE]
>
>如需 [如何使用](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) Adobe I/O CLI的Cloud Manager外掛程式設定值的詳細資訊，請參閱本頁。

### 變數數 {#number-of-variables}

每個環境最多可聲明200個變數。

## 機密和環境特定配置值的部署注意事項 {#deployment-considerations-for-secret-and-environment-specific-configuration-values}

由於機密和環境特定組態值不在Git中，因此不屬於正式的AEM（雲端服務部署機制），因此客戶應以雲端服務部署程式的形式來管理、管理和整合AEM。

如上所述，呼叫API會將新變數和值部署至雲端環境，類似於一般的客戶程式碼部署管道。 作者和發佈服務將會重新啟動並參考新值，通常需要幾分鐘的時間。 請注意，Cloud Manager在常規代碼部署期間執行的質量門和測試不會在此過程中執行。

通常，客戶會先呼叫API以設定環境變數，然後再將依賴於他們的程式碼部署在Cloud Manager中。 在某些情況下，在已部署程式碼後，您可能會想要修改現有的變數。

請注意，當使用管道時（AEM更新或客戶部署）,API可能無法成功，這取決於當時執行的端對端管道的哪個部分。 錯誤回應會指出請求未成功，但不會指出特定原因。

有時，排程的客戶程式碼部署會依賴現有變數來擁有新值，這與目前的程式碼不適用。 如果這是顧慮，建議您以加法方式進行變數修改。 若要這麼做，請建立新的變數名稱，而不只是變更舊變數的值，讓舊程式碼永遠不會參照新值。 然後，當新客戶版本看起來穩定時，您可以選擇移除舊值。

同樣地，由於變數的值未版本化，因此回滾程式碼可能會導致其參考導致問題的較新值。 上述的加性變數策略在這方面也有幫助。

此添加變數策略也適用於災難恢復情況，如果需要重新部署前幾天的代碼，則其引用的變數名稱和值將保持不變。 這取決於客戶在移除這些舊變數前等待數天的策略，否則舊程式碼將沒有適當的變數可供參考。
