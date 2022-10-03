---
title: 為Adobe Experience Manager as a Cloud Service配置OSGi
description: 具有機密值和環境特定值的OSGi設定
feature: Deploying
exl-id: f31bff80-2565-4cd8-8978-d0fd75446e15
source-git-commit: aeff6c3e81eb71521dbd75fc73d3e177aac60abd
workflow-type: tm+mt
source-wordcount: '3297'
ht-degree: 0%

---

# 為Adobe Experience Manager as a Cloud Service配置OSGi {#configuring-osgi-for-aem-as-a-cloud-service}

>[!NOTE]
>
>AEM已導入使用Cloud Manager使用者介面來設定2021.12.0版標準環境變數的功能。 如需詳細資訊，請參閱本檔案 [此處](/help/implementing/cloud-manager/environment-variables.md).

[OSGi](https://www.osgi.org/) 是Adobe Experience Manager(AEM)技術堆疊中的基本元素。 它用於控制AEM及其配置的複合束。

OSGi提供了標準化基元，允許從小型、可重複使用和協作的元件構建應用程式。 這些元件可組成應用程式並部署。 這樣可輕鬆管理OSGi套件組合，因為它們可以單獨停止、安裝和啟動。 會自動處理互依性。 每個OSGi元件都包含在各種套件組合中。 如需詳細資訊，請參閱 [OSGi規範](https://help.eclipse.org/latest/index.jsp).

您可以透過AEM程式碼專案中的組態檔來管理OSGi元件的組態設定。

## OSGi組態檔 {#osgi-configuration-files}

組態變更會在AEM專案的程式碼套件中定義(`ui.apps`)作為配置檔案()`.cfg.json`)，位於runmode特定的設定資料夾下：

`/apps/example/config.<runmode>`

OSGi組態檔的格式是以JSON為基礎，使用 `.cfg.json` 由Apache Sling專案定義的格式。

OSGi設定會透過其永續身分(PID)來鎖定OSGi元件，預設值為OSGi元件的Java™類別名稱。 例如，若要提供OSGi服務的OSGi設定，請依下列方式實施：

`com.example.workflow.impl.ApprovalWorkflow.java`

OSGi設定檔案的定義位置：

`/apps/example/config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`

遵循 `cfg.json` OSGi配置格式。

>[!NOTE]
>
>舊版AEM支援的OSGi組態檔，使用不同的檔案格式，例如 `.cfg`, `.config` 和作為XML `sling:OsgiConfig` 資源定義。 這些格式會由 `.cfg.json` OSGi配置格式。

## 運行模式解析度 {#runmode-resolution}

>[!TIP]
>
>AEM 6.x支援自訂執行模式，但AEMas a Cloud Service則否。 AEMas a Cloud Service支援 [運行模式的精確集](./overview.md#runmodes). AEMas a Cloud Service環境之間OSGi設定的任何變異，都必須使用 [OSGi設定環境變數](#environment-specific-configuration-values).

使用執行模式，即可將特定OSGi設定鎖定在特定AEM例項。 若要使用執行模式，請在 `/apps/example` （其中範例為您的專案名稱），格式為：

`/apps/example/config.<author|publish>.<dev|stage|prod>/`

如果設定資料夾名稱中定義的執行模式符合AEM使用的執行模式，則會使用此類資料夾中的任何OSGi設定。

例如，如果AEM使用執行模式製作和開發，請在 `/apps/example/config.author/` 和 `/apps/example/config.author.dev/` 時， `/apps/example/config.publish/` 和 `/apps/example/config.author.stage/` 未套用。

如果同一PID的多個配置適用，則應用匹配運行模式數目最多的配置。

此規則的粒度為PID層級。 這表示您無法為 `/apps/example/config.author/` 更具體的 `/apps/example/config.author.dev/` PID相同。 匹配運行模式數目最多的配置對整個PID將有效。

>[!NOTE]
>
>A `config.preview` OSGi配置資料夾 **不能** 以與 `config.publish` 可以聲明資料夾。 預覽層會從發佈層的值繼承其OSGi設定。

本地開發時，運行模式啟動參數， `-r`，可用來指定執行模式OSGI設定。

```shell
$ java -jar aem-sdk-quickstart-xxxx.x.xxx.xxxx-xxxx.jar -r publish,dev
```

### 驗證運行模式

AEMas a Cloud Service執行模式已根據環境類型和服務妥善定義。 檢閱 [完整可用AEMas a Cloud Service執行模式清單](./overview.md#runmodes).

運行模式指定的OSGi配置值可通過以下方法驗證：

1. 開啟AEM as a Cloud Services環境 [開發人員控制台](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html)
1. 選擇要檢查的服務層，使用 __Pod__ 下拉式清單
1. 選取 __狀態__ 標籤
1. 選取 __配置__ 從 __狀態轉儲__ 下拉式清單
1. 選取 __獲取狀態__ 按鈕

產生的檢視會顯示所選層的所有OSGi元件設定及其適用的OSGi設定值。 這些值可與AEM專案原始碼下的OSGi設定值交叉參照 `/apps/example/osgiconfig/config.<runmode(s)>`.


要驗證是否應用了適當的OSGi配置值，請執行以下操作：

1. 在開發人員控制台的配置輸出中
1. 找出 `pid` 表示要驗證的OSGi配置；這是AEM專案原始碼中OSGi設定檔案的名稱。
1. Inspect `properties` 清單 `pid` 並驗證要驗證的運行模式的AEM項目原始碼中的鍵和值與OSGi配置檔案匹配。


## OSGi配置值的類型 {#types-of-osgi-configuration-values}

有三種OSGi設定值可與Adobe Experience Manager as a Cloud Service搭配使用。

1. **內嵌值**，這些值會硬式編碼至OSGi設定中並儲存在Git中。 例如：

   ```json
   {
      "connection.timeout": 1000
   }
   ```

1. **機密值**，這些值基於安全理由不得儲存在Git中。 例如：

   ```json
   {
   "api-key": "$[secret:server-api-key]"
   } 
   ```

1. **環境特定值**，這些值在開發環境之間會有所差異，因此無法以執行模式準確鎖定目標(因為有單一 `dev` 執行模式)。 例如：

   ```json
   {
    "url": "$[env:server-url]"
   }
   ```

   單一OSGi設定檔案可搭配使用這些設定值類型的任何組合。 例如：

   ```json
   {
   "connection.timeout": 1000,
   "api-key": "$[secret:server-api-key]",
   "url": "$[env:server-url]"
   }
   ```

## 如何選擇適當的OSGi配置值類型 {#how-to-choose-the-appropriate-osgi-configuration-value-type}

OSGi的常見案例是使用內嵌OSGi設定值。 環境特定設定僅用於開發環境之間值不同的特定使用案例。

![](assets/choose-configuration-value-type_res1.png)

環境特定配置擴展了包含內嵌值的傳統靜態定義OSGi配置，從而提供了通過Cloud Manager API從外部管理OSGi配置值的功能。 請務必了解何時應使用定義內嵌值並儲存在Git中的常見傳統方法，而非將值抽象為環境特定設定。

下列指南說明何時使用非機密和機密環境專屬設定：

### 何時使用內嵌組態值 {#when-to-use-inline-configuration-values}

內嵌設定值視為標準方法，並應盡可能使用。 內嵌設定具備下列優點：

* 維護這些變數，並以Git管理和版本記錄進行處理
* 值會隱式系結至程式碼部署
* 它們不需要任何額外的部署考量或協調

每當定義OSGi配置值時，請從內嵌值開始，並僅在必要時為使用案例選擇機密或環境特定配置。

### 非機密環境特定設定值的使用時機 {#when-to-use-non-secret-environment-specific-configuration-values}

僅使用環境特定配置(`$[env:ENV_VAR_NAME]`)，以取得非機密設定值（當預覽層級的值不同或開發環境不同時）。 這包括本機開發執行個體和任何Adobe Experience Manager as a Cloud Service開發環境。 除了為預覽層級設定唯一值外，請避免為Adobe Experience Manager as a Cloud Service Stage或生產環境使用非機密的環境專屬設定。

* 只有發佈層級和預覽層級之間不同的設定值，或開發環境（包括本機開發執行個體）之間不同的值，才使用非機密環境專屬設定。
* 除了預覽層級需要與發佈層級不同的案例外，請對「預備」和「生產」非機密值使用OSGi設定中的標準內嵌值。 相關地，不建議使用特定於環境的配置，以便在執行階段對預備和生產環境進行配置更改；這些變更應透過原始碼管理引入。

### 何時使用機密環境特定設定值 {#when-to-use-secret-environment-specific-configuration-values}

Adobe Experience Manager as a Cloud Service需要使用環境特定的設定(`$[secret:SECRET_VAR_NAME]`)取得任何機密OSGi設定值，例如密碼、私密API金鑰，或基於安全理由無法儲存在Git的任何其他值。

使用機密環境專屬設定，以儲存所有Adobe Experience Manager as a Cloud Service環境（包括預備和生產）上機密的值。

## 建立OSGi配置 {#creating-sogi-configurations}

建立OSGi設定的方式有兩種，如下所述。 前一種方法通常用於配置具有由開發人員知道的OSGi屬性和值的自定義OSGi元件，後一種方法用於AEM提供的OSGi元件。

### 編寫OSGi配置 {#writing-osgi-configurations}

JSON格式的OSGi組態檔可直接在AEM專案中手動寫入。 這通常是為知名OSGi元件建立OSGi配置的最快方法，尤其是由定義配置的同一開發人員設計和開發的自定義OSGi元件。 此方法也可用於複製/貼上和更新不同執行模式資料夾中相同OSGi元件的設定。

1. 在IDE中，開啟 `ui.apps` 專案、找到或建立設定資料夾(`/apps/.../config.<runmode>`)，其目標為新OSGi組態需要生效的執行模式
1. 在此設定資料夾中，建立 `<PID>.cfg.json` 檔案。 PID是OSGi元件的永久標識。 這通常是OSGi元件實施的完整類別名稱。 例如：
   `/apps/.../config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`
請注意，OSGi配置工廠檔案名使用 `<factoryPID>-<name>.cfg.json` 命名約定
1. 開啟新 `.cfg.json` ，並在 [JSON OSGi組態格式](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1).
1. 將變更儲存至 `.cfg.json` 檔案
1. 將新的OSGi設定檔案新增並提交至Git

### 使用AEM SDK快速入門產生OSGi設定 {#generating-osgi-configurations-using-the-aem-sdk-quickstart}

AEM SDK Quickstart Jar的AEM Web Console可用來設定OSGi元件，並將OSGi設定匯出為JSON。 這對於設定AEM提供的OSGi元件非常有用，而定義AEM專案中OSGi設定的開發人員可能無法充分了解其OSGi屬性及其值格式。

>[!NOTE]
>
>AEM Web Console的設定UI會寫入 `.cfg.json` 檔案放入存放庫。 因此，請注意這一點，以避免在本機開發期間，當AEM專案定義的OSGi設定可能與產生的設定不同時，可能會發生非預期行為。

1. 以管理員使用者身分登入AEM SDK Quickstart Jar的AEM Web主控台
1. 導覽至「OSGi >設定」
1. 若要設定，請找出OSGi元件，並點選其標題以進行編輯
   ![OSGi配置](./assets/configuring-osgi/configuration.png)
1. 視需要透過Web UI編輯OSGi設定屬性值
1. 將永久身份(PID)記錄到安全位置。 這稍後將用於產生OSGi設定JSON
1. 點選「儲存」
1. 導航至OSGi > OSGi安裝程式配置打印機
1. 貼入步驟5中複製的PID，確認序列化格式已設為「OSGi Configurator JSON」
1. 點選「列印」
1. JSON格式的OSGi設定會顯示在序列化設定屬性區段中
   ![OSGi安裝程式配置打印機](./assets/configuring-osgi/osgi-installer-configurator-printer.png)
1. 在IDE中，開啟 `ui.apps` 專案、找到或建立設定資料夾(`/apps/.../config.<runmode>`)，其目標為新OSGi組態必須生效的執行模式。
1. 在此設定資料夾中，建立 `<PID>.cfg.json` 檔案。 PID與步驟5中的值相同。
1. 將步驟10的序列化設定屬性貼入 `.cfg.json` 檔案。
1. 將變更儲存至 `.cfg.json` 檔案。
1. 將新的OSGi設定檔案新增並提交至Git。


## OSGi配置屬性格式 {#osgi-configuration-property-formats}

### 內嵌值 {#inline-values}

遵循標準JSON語法，內嵌值會格式化為標準名稱值配對。 例如：

```json
{
   "my_var1": "val",
   "my_var2": [ "abc", "def" ],
   "my_var3": 500
}
```

### 環境特定配置值 {#environment-specific-configuration-values}

OSGi設定應為要根據環境定義的變數指派預留位置：

```
use $[env:ENV_VAR_NAME]
```

客戶只應將此技術用於與其自訂程式碼相關的OSGi設定屬性；不得使用它覆寫Adobe定義的OSGi設定。

>[!NOTE]
>
>預留位置不能用於 [重點語句](/help/implementing/deploying/overview.md#repoinit).

### 機密組態值 {#secret-configuration-values}

OSGi設定應為要根據環境定義的機密指派預留位置：

```
use $[secret:SECRET_VAR_NAME]
```

### 變數命名 {#variable-naming}

下列項目適用於環境特定值和機密設定值。

變數名稱必須遵循下列規則：

* 最小長度：2
* 最大長度：100
* 必須符合規則運算式： `[a-zA-Z_][a-zA-Z_0-9]*`

變數的值不得超過2048個字元。

>[!CAUTION]
>
>有些規則與對變數名稱使用某些前置詞有關：
>
>1. 變數名稱首碼為 `INTERNAL_`, `ADOBE_`，或 `CONST_` 由Adobe保留。 任何以這些前置詞開頭的客戶設定變數將被忽略。
>
>1. 客戶不得參考以開頭的變數 `INTERNAL_` 或 `ADOBE_` 或者。
>
>1. 具有首碼的環境變數 `AEM_` 由產品定義為要由客戶使用和設定的公用API。
   >   雖然客戶可以使用並設定以首碼開頭的環境變數 `AEM_` 他們不應以此首碼定義自己的變數。


### 預設值 {#default-values}

下列項目適用於環境特定值和機密設定值。

如果未設定每個環境的值，則在執行階段不會取代預留位置，並保留原有位置，因為未發生內插。 為避免此情況，可使用下列語法將預設值作為預留位置的一部分提供：

```
$[env:ENV_VAR_NAME;default=<value>]
```

提供預設值後，預留位置會取代為提供的每個環境值或提供的預設值。

### 地方開發 {#local-development}

下列項目適用於環境特定值和機密設定值。

變數可在本機環境中定義，以便由本機AEM在執行階段擷取。 例如，在Linux®上：

```bash
export ENV_VAR_NAME=my_value
```

建議編寫簡單的bash指令碼，該指令碼設定配置中使用的環境變數，並在啟動AEM之前執行它。 工具，例如 [https://direnv.net/](https://direnv.net/) 有助於簡化此方法。 視值類型而定，如果值可在每個人之間共用，則可將其簽入原始碼管理。

從檔案讀取機密值。 因此，對於每個使用機密的佔位符，必須建立包含機密值的文本檔案。

例如，若 `$[secret:server_password]` ，則會使用名為的文字檔案 **server_password** 必須建立。 所有這些機密檔案都必須儲存在相同的目錄和框架屬性中 `org.apache.felix.configadmin.plugin.interpolation.secretsdir` 必須使用該本地目錄進行配置。

>[!CAUTION]
>
>文本檔案必須命名 **server_password**  — 沒有副檔名。

此 `org.apache.felix.configadmin.plugin.interpolation.secretsdir` 是Sling架構屬性；因此，此屬性未在felix console(/system/console)中設定，而是在系統引導時使用的sling.properties檔案中設定。 可在擷取的Jar/install資料夾(crx-quickstart/conf)的/conf子目錄中找到此檔案。

範例：將此行添加到「crx-quickstart/conf/sling.properties」檔案的末尾，以將「crx-quickstart/secretsdir」配置為機密資料夾：

```
org.apache.felix.configadmin.plugin.interpolation.secretsdir=${sling.home}/secretsdir
```

### 製作與發佈設定 {#author-vs-publish-configuration}

如果OSGi屬性需要不同的值才能製作與發佈：

* 分隔 `config.author` 和 `config.publish` 必須使用OSGi資料夾，如 [「運行模式解析」部分](#runmode-resolution).
* 建立應使用的獨立變數名稱有兩個選項：
   * 建議使用第一個選項：(例如 `config.author` 和 `config.publish`)來定義不同的值，請使用相同的變數名稱。 例如
      `$[env:ENV_VAR_NAME;default=<value>]`，其中預設值對應至該層級（製作或發佈）的預設值。 透過 [Cloud Manager API](#cloud-manager-api-format-for-setting-properties) 或透過用戶端，使用「服務」參數來區分層級，如下所述 [API參考檔案](https://developer.adobe.com/experience-cloud/cloud-manager/api-reference/). 「service」參數會將變數的值系結至適當的OSGi層。 可以是「作者」、「發佈」或「預覽」。
   * 第二個選項，即使用首碼(例如 `author_<samevariablename>` 和 `publish_<samevariablename>`

### 設定範例 {#configuration-examples}

在下列範例中，假設除了舞台和生產環境外，還有三個開發環境。

**範例 1**

目的是用於OSGi屬性的值 `my_var1` 在stage和prod中保持相同，但在三個開發環境中各自不同。

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
{ "my_var1":"val"、"my_var2":"abc"、"my_var3":500 }
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1" :"$[env:my_var1]" "my_var2":"abc"、"my_var3":500 }
</pre>
</td>
</tr>
</table>

**範例 2**

目的是用於OSGi屬性的值 `my_var1` 對於三個開發環境中的每個環境，prod和會有所不同。 因此，必須呼叫Cloud Manager API，才能設定 `my_var1` 每個開發環境。

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
{ "my_var1":"val1"、"my_var2":"abc"、"my_var3":500 }
</pre>
</td>
</tr>
<tr>
<td>
config.prod
</td>
<td>
<pre>
{ "my_var1":"val2", "my_var2":"abc"、"my_var3":500 }
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1" :"$[env:my_var1]" "my_var2":"abc"、"my_var3":500 }
</pre>
</td>
</tr>
</table>

**範例3**

目的是用於OSGi屬性的值 `my_var1` 在預備、生產和其中一個開發環境中保持相同，但在其他兩個開發環境中則有所不同。 在此情況下，必須呼叫Cloud Manager API，才能設定 `my_var1` 針對每個開發環境，包括應具有與預備和生產相同值的開發環境。 它不會繼承資料夾中設定的值 **設定**.

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
設定
</td>
<td>
<pre>
{ "my_var1":"val1"、"my_var2":"abc"、"my_var3":500 }
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1" :"$[env:my_var1]" "my_var2":"abc"、"my_var3":500 }
</pre>
</td>
</tr>
</table>

另一種實現此目的的方式，是在config.dev資料夾中為取代代號設定預設值，使其與 **設定** 檔案夾。

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
設定
</td>
<td>
<pre>
{ "my_var1":"val1"、"my_var2":"abc"、"my_var3":500 }
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1":"$[env:my_var1;default=val1]" "my_var2":"abc"、"my_var3":500 }
</pre>
</td>
</tr>
</table>

## 用於設定屬性的Cloud Manager API格式 {#cloud-manager-api-format-for-setting-properties}

請參閱 [本頁](https://developer.adobe.com/experience-cloud/cloud-manager/docs/) 關於API的設定方式。
>[!NOTE]
>
>請確定使用的Cloud Manager API已指派「部署管理員 — Cloud Service」角色。 其他角色無法執行以下所有命令。

### 透過API設定值 {#setting-values-via-api}

呼叫API會將新變數和值部署至雲端環境，類似於一般客戶程式碼部署管道。 製作和發佈服務會重新啟動並參考新值，通常需要幾分鐘的時間。

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
>預設變數不是透過API設定，而是透過OSGi屬性本身設定。
>
>請參閱 [本頁](https://developer.adobe.com/experience-cloud/cloud-manager/api-reference/) 以取得更多資訊。

### 透過API取得值 {#getting-values-via-api}

```
GET /program/{programId}/environment/{environmentId}/variables
```

請參閱 [本頁](https://developer.adobe.com/experience-cloud/cloud-manager/api-reference/) 以取得更多資訊。

### 透過API刪除值 {#deleting-values-via-api}

```
PATCH /program/{programId}/environment/{environmentId}/variables
```

若要刪除變數，請將其納入空白值。

請參閱 [本頁](https://developer.adobe.com/experience-cloud/cloud-manager/api-reference/) 以取得更多資訊。

### 透過命令列取得值 {#getting-values-via-cli}

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

### 透過命令列刪除值 {#deleting-values-via-cli}

```bash
$ aio cloudmanager:set-environment-variables ENVIRONMENT_ID --delete MY_VAR1 MY_VAR2
```

>[!NOTE]
>
>請參閱 [本頁](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) 有關如何使用Cloud Manager增效模組配置Adobe I/OCLI的更多資訊。

### 變數數 {#number-of-variables}

每個環境最多可宣告200個變數。

## 機密和環境特定組態值的部署考量事項 {#deployment-considerations-for-secret-and-environment-specific-configuration-values}

由於機密和環境專屬的設定值會存在於Git外部，因此不是正式Adobe Experience Manager as a Cloud Service部署機制的一部分，因此客戶應管理、控管並整合至Adobe Experience Manager as a Cloud Service部署程式。

如上所述，呼叫API會將新變數和值部署至雲端環境，類似於一般的客戶程式碼部署管道。 製作和發佈服務會重新啟動並參考新值，通常需要幾分鐘的時間。 請注意，此程式中不會執行Cloud Manager在一般程式碼部署期間執行的品質閘道和測試。

通常，客戶在Cloud Manager中部署依賴API的程式碼之前，會先呼叫API來設定環境變數。 在某些情況下，部署程式碼後，您可能會想要修改現有變數。

>[!NOTE]
>
>管道使用中(包括AEM更新或客戶部署)時，API可能無法成功，端對端管道的哪個部分屆時會執行。 錯誤回應會指出要求未成功，但不會指出特定原因。

在某些情況下，已排程的客戶程式碼部署會仰賴現有變數來有新值，而這與目前的程式碼不適用。 如果您擔心此問題，建議您以加法方式修改變數。 若要這麼做，請建立新變數名稱，而非只變更舊變數的值，讓舊程式碼永遠不會參照新值。 當新客戶版本看起來穩定時，您可以選擇移除舊值。

同樣地，由於變數的值沒有版本控制，回滾程式碼可能會導致其參考較新值，而造成問題。 前述的加性變數策略在此也有所幫助。

此添加變數策略對於災難恢復情況也很有用，在這些情況下，如果需要重新部署前幾天的代碼，則其引用的變數名稱和值仍將保持不變。 這取決於策略，客戶在移除這些較舊的變數前會等待數天，否則較舊的程式碼將沒有適當的變數可參考。
