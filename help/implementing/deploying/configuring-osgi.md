---
title: 將Adobe Experience Manager的OSGi配置為Cloud Service
description: '具有機密值和環境特定值的OSGi配置 '
feature: 部署
translation-type: tm+mt
source-git-commit: a91743ba97f9b18c7f67208e7f1dcd873a3bbd65
workflow-type: tm+mt
source-wordcount: '2737'
ht-degree: 0%

---


# 將Adobe Experience Manager的OSGi配置為Cloud Service{#configuring-osgi-for-aem-as-a-cloud-service}

[](https://www.osgi.org/) OSG是Adobe Experience Manager(M)技術層面的一個基AEM本要素。它用於控制複合束及其AEM結構。

OSGi提供標準化的基元，可讓應用程式從小型、可重複使用且協作的元件建構。 這些元件可組成應用程式並加以部署。 這樣可以輕鬆管理OSGi捆綁包，因為它們可以單獨停止、安裝和啟動。 互依關係會自動處理。 每個OSGi元件都包含在其中一個不同的束中。 有關詳細資訊，請參見[OSGi規範](https://www.osgi.org/Specifications/HomePage)。

您可以透過屬於程式碼專案一部分的設定檔案，管理OSGi元件的設AEM定設定。

## OSGi配置檔案{#osgi-configuration-files}

配置更改在項AEM目的代碼包(`ui.apps`)中定義為運行模式特定配置資料夾下的配置檔案(`.cfg.json`):

`/apps/example/config.<runmode>`

OSGi組態檔的格式是以JSON為基礎，使用Apache Sling專案所定義的`.cfg.json`格式。

OSGi配置通過其永久標識(PID)來定位OSGi元件，該標識預設為OSGi元件的Java™類名。 例如，要為由以下項目實施的OSGi服務提供OSGi配置：

`com.example.workflow.impl.ApprovalWorkflow.java`

an OSGi configuration file is defined at:

`/apps/example/config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`

遵循cfg.json OSGi組態格式。

>[!NOTE]
>
>舊版支援AEM的OSGi組態檔使用不同的檔案格式，例如。cfg.、.config和XML sling:OsgiConfig資源定義。 這些格式由cfg.json OSGi組態格式取代。

## 運行模式解析度{#runmode-resolution}

使用執行模式可將特定OSGiAEM組態定位至特定例項。 若要使用runmode，請在`/apps/example`（其中，您的專案名稱為範例）下建立組態資料夾，格式為：

`/apps/example/config.<author|publish>.<dev|stage|prod>/`

如果配置資料夾名稱中定義的運行模式與所使用的運行模式匹配，則會使用此類資料夾中的任何OSGi配AEM置。

例如，AEM如果使用runmodes author和dev，則會套用`/apps/example/config.author/`和`/apps/example/config.author.dev/`中的設定節點，而不套用`/apps/example/config.publish/`和`/apps/example/config.author.stage/`中的設定節點。

如果同一PID的多個配置適用，則應用具有最多匹配運行模式的配置。

此規則的詳細程度為PID層級。 這表示您不能為`/apps/example/config.author/`中的相同PID定義某些屬性，而為相同PID在`/apps/example/config.author.dev/`中定義更多特定屬性。 對於整個PID，具有最多匹配運行模式的配置將是有效的。

在本機開發時，可傳入runmode啟動參數，以指定使用哪個runmode OSGI組態。

## OSGi配置值類型{#types-of-osgi-configuration-values}

OSGi組態值有三種，可搭配Adobe Experience ManagerCloud Service使用。

1. **內嵌值**，這些值是硬式編碼至OSGi組態並儲存在Git中的值。例如：

   ```json
   {
      "connection.timeout": 1000
   }
   ```

1. **機密值**，這些值是出於安全原因不得儲存在Git中的值。例如：

   ```json
   {
   "api-key": "$[secret:server-api-key]"
   } 
   ```

1. **特定於環境的值**，這些值在開發環境之間會有所不同，因此無法按運行模式準確定位(因為在Adobe Experience Manager作為Cloud Service，有單 `dev` 一運行模式)。例如：

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

## 如何選擇適當的OSGi配置值類型{#how-to-choose-the-appropriate-osgi-configuration-value-type}

OSGi的常見情況是使用內嵌OSGi配置值。 特定環境的配置僅用於開發環境之間值不同的特定使用情形。

![](assets/choose-configuration-value-type_res1.png)

環境特定配置擴展了包含內嵌值的傳統靜態定義OSGi配置，從而提供了通過Cloud Manager API在外部管理OSGi配置值的能力。 必須瞭解何時應使用定義內嵌值並將其儲存在Git中的常見和傳統方法，而不是將值抽象為特定環境的配置。

以下指南說明何時使用非機密和機密環境特定組態：

### 何時使用內嵌配置值{#when-to-use-inline-configuration-values}

內嵌組態值被視為標準方法，並應盡可能使用。 內嵌配置提供以下優點：

* 它們會維護，並使用Git的管理和版本記錄
* 值會隱含地系結至程式碼部署
* 它們不需要任何額外的部署考慮或協調

每當定義OSGi配置值時，請從內嵌值開始，並僅在使用案例需要時選擇機密或環境特定的配置。

### 何時使用非機密環境特定配置值{#when-to-use-non-secret-environment-specific-configuration-values}

當值在開發環境中不同時，僅對非機密配置值使用環境特定配置(`$[env:ENV_VAR_NAME]`)。 這包括本地開發實例和作為Cloud Service開發環境的任何Adobe Experience Manager。 避免將Adobe Experience Manager的非機密環境特定配置用作Cloud Service階段或生產環境。

* 僅針對不同開發環境（包括本地開發實例）的配置值使用非機密的環境特定配置。
* 請改用OSGi組態中的標準內嵌值，以用於「舞台(Stage)」和「生產(Production)」非機密值。 因此，不建議使用環境特定配置來促進在運行時對舞台和生產環境進行配置更改；這些變更應透過原始碼管理引入。

### 何時使用特定於環境的機密配置值{#when-to-use-secret-environment-specific-configuration-values}

Adobe Experience Manager作為Cloud Service，要求對於任何機密OSGi配置值(如密碼、私有API金鑰或出於安全原因無法儲存在Git中的任何其他值，都使用環境特定配置(`$[secret:SECRET_VAR_NAME]`)。

使用特定於環境的機密配置，將機密的價值儲存在所有Adobe Experience Manager的Cloud Service環境，包括舞台和生產環境。

## 建立OSGi配置{#creating-sogi-configurations}

建立OSGi配置有兩種方法，如下所述。 前者通常用於配置具有由開發人員所知OSGi屬性和值的自訂OSGi元件，後者用於提供AEM的OSGi元件。

### 編寫OSGi配置{#writing-osgi-configurations}

JSON格式的OSGi組態檔可直接手動寫入專AEM案。 這通常是為知名OSGi元件建立OSGi配置的最快方式，尤其是由定義這些配置的同一開發人員設計和開發的定製OSGi元件。 此方法也可用於複製／貼上和更新不同運行模式資料夾中相同OSGi元件的配置。

1. 在IDE中，開啟`ui.apps`項目，找到或建立配置資料夾(`/apps/.../config.<runmode>`)，該資料夾針對新OSGi配置需要生效的運行模式
1. 在此配置資料夾中，建立新的`<PID>.cfg.json`檔案。 PID是OSGi元件的持久標識通常是OSGi元件實施的完整類名。 例如：
   `/apps/.../config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`
請注意，OSGi配置工廠檔案名使用 `<PID>-<factory-name>.cfg.json` 命名約定
1. 開啟新的`.cfg.json`檔案，並定義OSGi屬性和值配對的索引鍵／值組合，並遵循[JSON OSGi組態格式](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1)。
1. 將更改保存到新的`.cfg.json`檔案
1. 將新的OSGi配置檔案添加並提交到Git

### 使用AEMSDK Quickstart {#generating-osgi-configurations-using-the-aem-sdk-quickstart}生成OSGi配置

SDK Quickstart AEM Jar的Web AEM Console可用來設定OSGi元件，並將OSGi組態匯出為JSON。 這對於配置提供AEM的OSGi元件非常有用，其OSGi屬性及其值格式可能無法由項目中定義OSGi配置的開發人員充分理AEM解。

>[!NOTE]
>
>Web AEM Console的Configuration UI將`.cfg.json`檔案寫入儲存庫。 因此，請注意這一點，以避免在本端開發期間，當AEMProject-defined OSGi組態可能與產生的組態不同時，可能會發生意外行為。

1. 以管理員AEM用戶身份登錄AEM到SDK Quickstart Jar的Web控制台
1. 導覽至「OSGi >設定」
1. 若要設定，請找出OSGi元件並點選其標題以進行編輯
   ![OSGi配置](./assets/configuring-osgi/configuration.png)
1. 視需要透過Web UI編輯OSGi組態屬性值
1. 將永久性身分(PID)記錄到安全位置。 稍後會用來產生OSGi設定JSON
1. 點選「儲存」
1. 導覽至「OSGi > OSGi Installer Configuration Printer」
1. 在步驟5中複製的PID中貼上，確保「序列化格式」已設為「OSGi Configurator JSON」
1. 點選列印
1. JSON格式的OSGi設定將顯示在「序列化設定屬性」區段中
   ![OSGi安裝程式配置打印機](./assets/configuring-osgi/osgi-installer-configurator-printer.png)
1. 在IDE中，開啟`ui.apps`項目，找到或建立配置資料夾(`/apps/.../config.<runmode>`)，該資料夾針對新OSGi配置需要生效的運行模式。
1. 在此配置資料夾中，建立新的`<PID>.cfg.json`檔案。 PID與步驟5的值相同。
1. 將步驟10中的序列化配置屬性貼上到`.cfg.json`檔案中。
1. 將更改保存到新的`.cfg.json`檔案。
1. 將新的OSGi配置檔案添加並提交到Git。


## OSGi配置屬性格式{#osgi-configuration-property-formats}

### 內嵌值{#inline-values}

內嵌值會依照標準JSON語法，格式化為標準名稱——值配對。 例如：

```json
{
   "my_var1": "val",
   "my_var2": [ "abc", "def" ],
   "my_var3": 500
}
```

### 環境特定配置值{#environment-specific-configuration-values}

OSGi配置應為要根據環境定義的變數指定佔位符：

```
use $[env:ENV_VAR_NAME]
```

客戶只應將此技巧用於與其自訂程式碼相關的OSGI組態屬性；它不得用於覆蓋Adobe定義的OSGI配置。

>[!NOTE]
>
>佔位符不能用於[repoinit語句](/help/implementing/deploying/overview.md#repoinit)。

### 密碼配置值{#secret-configuration-values}

OSGi配置應為要根據環境定義的機密指定一個佔位符：

```
use $[secret:SECRET_VAR_NAME]
```

### 變數命名{#variable-naming}

以下內容適用於特定環境和機密配置值。

變數名稱必須遵循下列規則：

* 最小長度：2
* 最大長度：100
* 必須符合regex:`[a-zA-Z_][a-zA-Z_0-9]*`

變數的值不得超過2048個字元。

### 預設值 {#default-values}

以下內容適用於特定環境和機密配置值。

如果未設定每個環境的值，則在執行時期不會取代預留位置，並保留原位，因為未發生插值。 為避免此問題，可使用下列語法將預設值提供為預留位置的一部分：

```
$[env:ENV_VAR_NAME;default=<value>]
```

在提供預設值後，預留位置會以依環境而定的值取代，或以提供的預設值取代。

### 本地開發{#local-development}

以下內容適用於特定環境和機密配置值。

變數可在本機環境中定義，如此便可由本機在執行時AEM期擷取。 例如，在Linux®上：

```bash
export ENV_VAR_NAME=my_value
```

建議編寫簡單的bash指令碼，該指令碼設定配置中使用的環境變數並在啟動之前執行該指令碼AEM。 [https://direnv.net/](https://direnv.net/)等工具有助於簡化此方法。 視值類型而定，如果值可以在每個人之間共用，則可能會將其簽入原始碼管理。

機密值會從檔案中讀取。 因此，對於使用密碼的每個佔位符，必須建立包含密碼值的文本檔案。

例如，如果使用`$[secret:server_password]`，則必須建立名為&#x200B;**server_password**&#x200B;的文本檔案。 所有這些機密檔案都必須儲存在相同的目錄中，且架構屬性`org.apache.felix.configadmin.plugin.interpolation.secretsdir`必須以該本機目錄設定。

### 作者與發佈組態{#author-vs-publish-configuration}

如果OSGI屬性要求作者與發佈的值不同：

* 必須使用單獨的`config.author`和`config.publish` OSGi資料夾，如[ Runmode Resolution部分](#runmode-resolution)中所述。
* 應使用獨立變數名稱。 建議使用變數名稱相同的前置詞，例如`author_<variablename>`和`publish_<variablename>`

### 配置示例{#configuration-examples}

在以下範例中，假設除了舞台和prod環境外，還有3個開發環境。

**範例1**

其目的是讓OSGI屬性`my_var1`的值在舞台和prod上相同，但在三個開發環境中各有不同。

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
{ 
 "my_var1":"val",
 "my_var2":「abc」、
 "my_var3":500
}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ 
 "my_var1" :"$[env:my_var1]"
 "my_var2":「abc」、
 "my_var3":500
}
</pre>
</td>
</tr>
</table>

**範例2**

其目的是讓OSGI屬性`my_var1`的值與舞台、prod和三個開發環境中的每個環境不同。 因此，必須呼叫Cloud Manager API，才能為每個開發環境設定`my_var1`的值。

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
{ 
 "my_var1":"val1"、
 "my_var2":「abc」、
 "my_var3":500
}
</pre>
</td>
</tr>
<tr>
<td>
config.prod
</td>
<td>
<pre>
{ 
 "my_var1":"val2",
 "my_var2":「abc」、
 "my_var3":500
}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ 
 "my_var1" :"$[env:my_var1]"
 "my_var2":「abc」、
 "my_var3":500
}
</pre>
</td>
</tr>
</table>

**範例3**

其目的是讓OSGi屬性`my_var1`的值在舞台、生產環境和開發環境中都相同，但在其他兩個開發環境中則不同。 在這種情況下，必須調用Cloud Manager API，為每個開發環境設定`my_var1`值，包括應與舞台和生產環境具有相同值的開發環境。 它將不繼承資料夾&#x200B;**config**&#x200B;中設定的值。

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
{ 
 "my_var1":"val1"、
 "my_var2":「abc」、
 "my_var3":500
}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ 
 "my_var1" :"$[env:my_var1]"
 "my_var2":「abc」、
 "my_var3":500
}
</pre>
</td>
</tr>
</table>

要達到此目的，另一種方法是在config.dev檔案夾中設定取代Token的預設值，使其與&#x200B;**config**&#x200B;檔案夾中的值相同。

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
{ 
 "my_var1":"val1"、
 "my_var2":「abc」、
 "my_var3":500
}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ 
 "my_var1":"$[env:my_var1;default=val1]"
 "my_var2":「abc」、
 "my_var3":500
}
</pre>
</td>
</tr>
</table>

## 用於設定屬性{#cloud-manager-api-format-for-setting-properties}的Cloud Manager API格式

請參閱[本頁](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/create-api-integration.md)，瞭解如何配置API。
>[!NOTE]
>
>請確定已使用的Cloud Manager API已指派角色「部署管理員-Cloud Service」。 其他角色無法執行以下所有命令。

### 透過API設定值{#setting-values-via-api}

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

>[!NOTE]
>預設變數不是透過API設定，而是在OSGi屬性本身中。
>
>如需詳細資訊，請參閱[本頁](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Environment_Variables/patchEnvironmentVariables)。

### 透過API取得值{#getting-values-via-api}

```
GET /program/{programId}/environment/{environmentId}/variables
```

如需詳細資訊，請參閱[本頁](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Environment_Variables/getEnvironmentVariables)。

### 透過API {#deleting-values-via-api}刪除值

```
PATCH /program/{programId}/environment/{environmentId}/variables
```

若要刪除變數，請將其加入空白值。

如需詳細資訊，請參閱[本頁](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Environment_Variables/patchEnvironmentVariables)。

### 通過命令行獲取值{#getting-values-via-cli}

```bash
$ aio cloudmanager:list-environment-variables ENVIRONMENT_ID
Name     Type         Value
MY_VAR1  string       plaintext value 
MY_VAR2  secretString ****
```


### 通過命令行{#setting-values-via-cli}設定值

```bash
$ aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable MY_VAR1 "plaintext value" --secret MY_VAR2 "some secret value"
```

### 通過命令行{#deleting-values-via-cli}刪除值

```bash
$ aio cloudmanager:set-environment-variables ENVIRONMENT_ID --delete MY_VAR1 MY_VAR2
```

>[!NOTE]
>
>如需如何使用Cloud Manager外掛程式配置Adobe I/OCLI值的詳細資訊，請參閱[本頁](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid)。

### 變數數{#number-of-variables}

每個環境最多可聲明200個變數。

## 機密和環境特定配置值的部署注意事項{#deployment-considerations-for-secret-and-environment-specific-configuration-values}

由於機密和特定環境的組態值不在Git之外，因此不屬於正式的Adobe Experience ManagerCloud Service部署機制，因此客戶應該管理、管理並整合Adobe Experience Manager，作為Cloud Service部署程式。

如上所述，呼叫API會將新變數和值部署至雲端環境，類似於一般的客戶程式碼部署管道。 作者和發佈服務將會重新啟動並參考新值，通常需要幾分鐘的時間。 請注意，Cloud Manager在常規代碼部署期間執行的質量門和測試不會在此過程中執行。

通常，客戶會先呼叫API以設定環境變數，然後再將依賴於他們的程式碼部署在Cloud Manager中。 在某些情況下，在已部署程式碼後，您可能會想要修改現有的變數。

>[!NOTE]
>
>API在使用管道（更新或客戶部署）時，AEM可能無法成功，這取決於當時正在執行端到端管道的哪個部分。 錯誤回應會指出請求未成功，但不會指出特定原因。

有時，排程的客戶程式碼部署會依賴現有變數來擁有新值，這與目前的程式碼不適用。 若有此顧慮，建議您以加法方式進行變數修改。 若要這麼做，請建立新的變數名稱，而不只是變更舊變數的值，讓舊程式碼永遠不會參照新值。 然後，當新客戶版本看起來穩定時，您可以選擇移除舊值。

同樣地，由於變數的值未版本化，因此回滾程式碼可能會導致其參考導致問題的較新值。 上述的加性變數策略在此也有幫助。

此添加變數策略也適用於災難恢復情況，如果需要重新部署前幾天的代碼，則其引用的變數名稱和值將保持不變。 這取決於客戶在移除這些舊變數前等待數天的策略，否則舊程式碼將沒有適當的變數可供參考。
