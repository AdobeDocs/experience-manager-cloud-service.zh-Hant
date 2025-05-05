---
title: 為Adobe Experience Manager as a Cloud Service設定OSGi
description: 具有機密值和環境特定值的OSGi設定
feature: Deploying
exl-id: f31bff80-2565-4cd8-8978-d0fd75446e15
role: Admin
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '3321'
ht-degree: 1%

---


# 為Adobe Experience Manager as a Cloud Service設定OSGi {#configuring-osgi-for-aem-as-a-cloud-service}

[OSGi](https://www.osgi.org/)是Adobe Experience Manager (AEM)技術棧疊中的基本元素。 它可用來控制AEM的複合套件組合及其組態。

OSGi提供標準化的原語，允許使用小型、可重複使用的合作元件來建構應用程式。 這些元件可組成應用程式並進行部署。 這可讓您輕鬆管理OSGi套件組合，因為它們可以個別停止、安裝和啟動。 系統會自動處理相依性。 每個OSGi元件都包含在各種套件組合中。 如需詳細資訊，請參閱[OSGi規格](https://help.eclipse.org/latest/index.jsp)。

您可以透過AEM程式碼專案一部分的組態檔案來管理OSGi元件的組態設定。

>[!TIP]
>
>您可以使用Cloud Manager來設定環境變數。 如需詳細資訊，請參閱檔案[這裡](/help/implementing/cloud-manager/environment-variables.md)。

## OSGi組態檔 {#osgi-configuration-files}

組態變更在AEM Project的程式碼封裝(`ui.config`)中定義為runmode特定組態資料夾下的組態檔(`.cfg.json`)：

`/apps/example/config.<runmode>`

OSGi設定檔案的格式是以JSON為基礎，使用Apache Sling專案定義的`.cfg.json`格式。

OSGi設定會透過元件的持續身分識別(PID) (預設為OSGi元件的Java™類別名稱)來鎖定OSGi元件。 例如，若要為以下實施的OSGi服務提供OSGi設定：

`com.example.workflow.impl.ApprovalWorkflow.java`

OSGi設定檔案定義於：

`/apps/example/config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`

遵循`cfg.json` OSGi設定格式。

>[!NOTE]
>
>舊版AEM支援的OSGi組態檔使用不同的檔案格式，例如`.cfg`、`.config`，並做為XML `sling:OsgiConfig`資源定義。 這些格式已由`.cfg.json` OSGi組態格式取代。

>[!NOTE]
>
>OSGi設定不會像雲端中的典型AEM例項那樣儲存在外部位置中的/apps底下。 簽入Cloud Manager [Developer Console](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console#configurations)以檢視OSGi設定。

## 執行模式解析度 {#runmode-resolution}

>[!TIP]
>
>AEM 6.x支援自訂執行模式，但AEM as a Cloud Service不支援。 AEM as a Cloud Service支援[一組確切的執行模式](./overview.md#runmodes)。 必須使用[OSGi設定環境變數](#environment-specific-configuration-values)處理AEM as a Cloud Service環境之間的OSGi設定任何差異。

特定OSGi設定可以透過使用執行模式以特定AEM執行個體為目標。 若要使用runmode，請在`/apps/example`下建立設定資料夾（範例為專案名稱），格式為：

`/apps/example/config.<author|publish>.<dev|stage|prod>/`

如果設定資料夾名稱中定義的執行模式符合AEM使用的執行模式，則會使用此類資料夾中的任何OSGi設定。

例如，如果AEM使用runmodes author和dev，則套用`/apps/example/config.author/`和`/apps/example/config.author.dev/`中的設定節點，但未套用`/apps/example/config.publish/`和`/apps/example/config.author.stage/`中的設定節點。

如果同一PID適用多個設定，則會套用符合執行模式數量最多的設定。

此規則的詳細程度位於PID層級。 這表示您無法在`/apps/example/config.author/`中為同一個PID定義某些屬性，也無法在`/apps/example/config.author.dev/`中為同一個PID定義更具體的屬性。 符合執行模式數量最多的設定對整個PID有效。

>[!NOTE]
>
>`config.preview` OSGi設定資料夾&#x200B;**無法**&#x200B;以宣告`config.publish`資料夾的方式宣告。 預覽層級會繼承發佈層級值的OSGi設定。

在本機開發時，執行模式啟動參數 `-r` 用於指定執行模式 OSGI 設定。

```shell
$ java -jar aem-sdk-quickstart-xxxx.x.xxx.xxxx-xxxx.jar -r publish,dev
```

### 驗證執行模式

AEM as a Cloud Service執行模式會根據環境型別和服務妥善定義。 檢閱可用AEM as a Cloud Service執行模式的[完整清單](./overview.md#runmodes)。

可由以下驗證執行模式指定的OSGi設定值：

1. 正在開啟AEM as a Cloud Service環境的[Developer Console](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=zh-Hant)
1. 使用&#x200B;__Pod__&#x200B;下拉式清單選取要檢查的服務層
1. 正在選取&#x200B;__狀態__&#x200B;標籤
1. 從&#x200B;__狀態傾印__&#x200B;下拉式清單中選取&#x200B;__組態__
1. 選取&#x200B;__取得狀態__&#x200B;按鈕

產生的檢視會顯示所選階層的所有OSGi元件設定及其適用的OSGi設定值。 這些值可以與AEM專案原始程式碼中`/apps/example/osgiconfig/config.<runmode(s)>`下的OSGi設定值互動參照。


若要確認已套用適當的OSGi設定值：

1. 在Developer Console的設定輸出中
1. 找出代表要驗證OSGi設定的`pid`；這是AEM專案原始碼中的OSGi設定檔名稱。
1. Inspect `pid`的`properties`清單，並驗證金鑰和值是否符合正在驗證之執行模式的AEM專案原始碼中的OSGi設定檔。


## OSGi設定值的型別 {#types-of-osgi-configuration-values}

有三種不同的OSGi設定值可與Adobe Experience Manager as a Cloud Service搭配使用。

1. **內嵌值**，這些值已硬式編碼至OSGi設定中並儲存在Git中。 例如：

   ```json
   {
      "connection.timeout": 1000
   }
   ```

1. **密碼值**，基於安全考量，這些值不可以儲存在Git中。 例如：

   ```json
   {
   "api-key": "$[secret:server-api-key]"
   } 
   ```

1. **環境特定值**，這些值在開發環境之間會有所不同，因此無法由執行模式精準定位(因為Adobe Experience Manager as a Cloud Service中有單一`dev`執行模式)。 例如：

   ```json
   {
    "url": "$[env:server-url]"
   }
   ```

   單一OSGi設定檔案可結合使用這些設定值型別的任何組合。 例如：

   ```json
   {
   "connection.timeout": 1000,
   "api-key": "$[secret:server-api-key]",
   "url": "$[env:server-url]"
   }
   ```

## 如何選擇適當的OSGi設定值型別 {#how-to-choose-the-appropriate-osgi-configuration-value-type}

OSGi的常見情況是使用內嵌OSGi設定值。 特定環境的設定僅用於開發環境之間值不同的特定使用案例。

![有關如何使用適當組態值型別的決策樹狀結構](assets/choose-configuration-value-type_res1.png)

環境特定設定擴充了包含內嵌值的傳統、靜態定義的OSGi設定，提供透過Cloud Manager API從外部管理OSGi設定值的功能。 瞭解何時應該使用定義內嵌值並將其儲存在Git中的常見和傳統方法，而不是將值抽象為特定於環境的設定時，這一點很重要。

以下指南說明何時使用非機密和機密環境特定設定：

### 何時使用內嵌設定值 {#when-to-use-inline-configuration-values}

內嵌組態值會視為標準方法，並應儘可能使用。 內嵌組態具備以下優點：

* 這些區段會進行維護，並在Git中進行控管和版本記錄
* 值會隱含繫結至程式碼部署
* 它們不需要任何其他部署考量或協調

每當定義OSGi設定值時，請從內嵌值開始，並根據使用案例的需要僅選取密碼或環境特定的設定。

### 何時使用非機密環境特定設定值 {#when-to-use-non-secret-environment-specific-configuration-values}

只有在預覽層的值不同或開發環境的值不同時，才使用非機密組態值的環境特定組態(`$[env:ENV_VAR_NAME]`)。 這包括本機開發執行個體和任何Adobe Experience Manager as a Cloud Service開發環境。 除了為預覽層級設定唯一值外，請避免對Adobe Experience Manager as a Cloud Service中繼或生產環境使用非機密環境專屬設定。

* 僅針對發佈和預覽層之間不同的設定值，或開發環境（包括本機開發執行個體）之間不同的值，使用非機密環境專屬設定。
* 除了預覽層級必須不同於發佈層級的情境外，請在OSGi設定中，將標準內嵌值用於中繼和生產非機密值。 因此，不建議使用環境特定的設定，以便於在執行階段對中繼和生產環境進行設定變更；這些變更應透過原始程式碼管理引入。

### 何時使用機密環境特定的設定值 {#when-to-use-secret-environment-specific-configuration-values}

Adobe Experience Manager as a Cloud Service要求針對任何機密的OSGi設定值（例如密碼、私人API金鑰或任何其他基於安全原因而無法儲存在Git中的值），使用特定於環境的設定(`$[secret:SECRET_VAR_NAME]`)。

使用秘密環境特定的設定，以儲存所有Adobe Experience Manager as a Cloud Service環境（包括中繼和生產環境）的秘密值。

## 建立OSGi設定 {#creating-osgi-configurations}

建立OSGi設定的方式有兩種，如下所述。 前者通常用於設定自訂OSGi元件，這些元件具有開發人員熟知的OSGi屬性和值，而後者則用於AEM提供的OSGi元件。

### 寫入OSGi設定 {#writing-osgi-configurations}

JSON格式的OSGi設定檔案可直接在AEM專案中手動撰寫。 這通常是建立已知OSGi元件（尤其是自訂OSGi元件）的OSGi設定的最快方法，這些元件是由定義設定的相同開發人員設計和開發的。 此方法也可用於跨各種執行模式資料夾，複製/貼上及更新相同OSGi元件的設定。

1. 在您的IDE中，開啟`ui.apps`專案，尋找或建立設定資料夾(`/apps/.../config.<runmode>`)，以鎖定新OSGi設定需要生效的執行模式
1. 在此設定資料夾中，建立`<PID>.cfg.json`檔案。 PID是OSGi元件的永續性身分識別。 這通常是OSGi元件實作的完整類別名稱。 例如：
   `/apps/.../config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`
OSGi組態處理站檔案名稱使用`<factoryPID>-<name>.cfg.json`命名慣例
1. 開啟新的`.cfg.json`檔案，並依照[JSON OSGi組態格式](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1)定義OSGi屬性和值組的索引鍵/值組合。
1. 將變更儲存至新的`.cfg.json`檔案
1. 新增新的OSGi設定檔案並將其提交到Git

### 使用AEM SDK快速入門產生OSGi設定 {#generating-osgi-configurations-using-the-aem-sdk-quickstart}

AEM SDK Quickstart Jar的AEM Web Console可用於設定OSGi元件，以及將OSGi設定匯出為JSON。 這對於設定AEM提供的OSGi元件而言，若開發人員在AEM專案中定義OSGi設定，可能無法深入瞭解這些元件的OSGi屬性及其值格式。

>[!NOTE]
>
>AEM Web Console的設定UI不會將`.cfg.json`檔案寫入存放庫。 因此，請注意此工作流程，以避免在本機開發期間，當AEM專案定義的OSGi設定可能與產生的設定不同時，出現潛在的非預期行為。

1. 以管理員使用者身分在`https://<host>:<port>/system/console`登入AEM SDK Quickstart Jar的AEM Web主控台
1. 瀏覽至&#x200B;**OSGi** > **設定**
1. 若要設定，請找到OSGi元件並選取其標題以進行編輯
   ![OSGi設定](./assets/configuring-osgi/configuration.png)
1. 視需要透過Web UI編輯OSGi設定屬性值
1. 將持續身分識別(PID)記錄到安全的地方。 這稍後用於產生OSGi設定JSON
1. 選取儲存
1. 導覽至「OSGi > OSGi安裝程式設定印表機」
1. 在步驟5中複製的PID中貼上，確認序列化格式已設為「OSGi設定器JSON」
1. 選取列印
1. JSON格式的OSGi設定將顯示在序列化設定屬性區段中
   ![OSGi安裝程式設定印表機](./assets/configuring-osgi/osgi-installer-configurator-printer.png)
1. 在您的IDE中，開啟`ui.apps`專案，尋找或建立設定資料夾(`/apps/.../config.<runmode>`)，以鎖定新OSGi設定需要生效的執行模式。
1. 在此設定資料夾中，建立`<PID>.cfg.json`檔案。 PID與步驟5中的值相同。
1. 將步驟10中的序列化組態屬性貼到`.cfg.json`檔案中。
1. 將變更儲存至新的`.cfg.json`檔案。
1. 新增新的OSGi設定檔案並將其提交到Git。


## OSGi設定屬性格式 {#osgi-configuration-property-formats}

### 內嵌值 {#inline-values}

內嵌值的格式為遵循標準JSON語法的標準名稱 — 值組。 例如：

```json
{
   "my_var1": "val",
   "my_var2": [ "abc", "def" ],
   "my_var3": 500
}
```

### 環境特定的設定值 {#environment-specific-configuration-values}

OSGi設定應為要根據環境定義的變數指派預留位置：

```
use $[env:ENV_VAR_NAME]
```

客戶應該僅將此技巧用於與其自訂程式碼相關的OSGi設定屬性；不得使用此技巧來覆寫Adobe定義的OSGi設定。

>[!NOTE]
>
>預留位置不能在[repoinit陳述式](/help/implementing/deploying/overview.md#repoinit)中使用。

### 密碼設定值 {#secret-configuration-values}

OSGi設定應為要根據環境定義的密碼指派預留位置：

```
use $[secret:SECRET_VAR_NAME]
```

### 變數命名 {#variable-naming}

以下適用於特定環境和密碼設定值。

變數名稱必須符合下列規則：

* 最小長度：2
* 最大長度：100
* 必須符合規則運算式： `[a-zA-Z_][a-zA-Z_0-9]*`

變數的值不得超過2048個字元。

>[!CAUTION]
>
>有些規則與變數名稱使用某些首碼有關：
>
>1. 前置詞為`INTERNAL_`、`ADOBE_`或`CONST_`的變數名稱已由Adobe保留。 任何以這些首碼開頭的客戶設定變數都會被忽略。
>
>1. 客戶不得參考帶有`INTERNAL_`或`ADOBE_`首碼的變數。
>
>1. 產品會將前置詞為`AEM_`的環境變數定義為Public API，以供客戶使用和設定。
>   雖然客戶可以使用和設定以首碼`AEM_`開頭的環境變數，但他們不應該以此首碼定義自己的變數。

### 預設值 {#default-values}

以下適用於特定環境和密碼設定值。

如果未設定每個環境的值，則在執行階段不會取代預留位置，而且由於未發生內插，因此會保留預留位置。 為避免此問題，可以使用以下語法在預留位置中提供預設值：

```
$[env:ENV_VAR_NAME;default=<value>]
```

在提供預設值時，預留位置會取代為根據環境提供的值或提供的預設值。

### 本機開發 {#local-development}

以下適用於特定環境和密碼設定值。

變數可在本機環境中定義，以便由本機AEM在執行階段擷取。 例如，在Linux®上：

```bash
export ENV_VAR_NAME=my_value
```

建議撰寫簡單的bash指令碼，此指令碼會設定設定中使用的環境變數，並在啟動AEM之前執行。 [https://direnv.net/](https://direnv.net/)等工具有助於簡化此方法。 根據值的型別，如果可在所有人之間共用，這些值可能會被簽入原始程式碼管理。

密碼的值會從檔案中讀取。 因此，必須為使用密碼的每個預留位置建立包含密碼值的文字檔案。

例如，如果使用`$[secret:server_password]`，則必須建立名為&#x200B;**server_password**&#x200B;的文字檔。 所有這些機密檔案必須儲存在相同的目錄中，而且架構屬性`org.apache.felix.configadmin.plugin.interpolation.secretsdir`必須設定為該本機目錄。

>[!CAUTION]
>
>文字檔不允許副檔名。
>
>因此，在上述範例中，文字檔必須命名為&#x200B;**server_password** — 沒有副檔名。

`org.apache.felix.configadmin.plugin.interpolation.secretsdir`是Sling架構屬性；因此此屬性不是在felix主控台(/system/console)中設定，而是在系統啟動時使用的sling.properties檔案中設定。 此檔案可在解壓縮的Jar/install資料夾(crx-quickstart/conf)的/conf子目錄中找到。

範例：將此行新增到「crx-quickstart/conf/sling.properties」檔案的結尾以將「crx-quickstart/secretsdir」設定為機密資料夾：

```
org.apache.felix.configadmin.plugin.interpolation.secretsdir=${sling.home}/secretsdir
```

### 作者與Publish設定 {#author-vs-publish-configuration}

如果OSGi屬性對author和publish需要不同的值：

* 必須使用個別的`config.author`和`config.publish` OSGi資料夾，如[執行模式解析區段](#runmode-resolution)所述。
* 建立獨立變數名稱有兩個選項，應該使用：
   * 建議使用的第一個選項：在宣告要定義不同值的所有OSGi資料夾（例如`config.author`和`config.publish`）中，使用相同的變數名稱。 例如

     `$[env:ENV_VAR_NAME;default=<value>]`，其中預設值對應至該階層（作者或發佈）的預設值。 透過[Cloud Manager API](#cloud-manager-api-format-for-setting-properties)或透過使用者端設定環境變數時，請依照[Cloud Manager API參考檔案](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/)所述，使用「服務」引數來區分層級。 「service」引數會將變數的值繫結至適當的OSGi層。 它可以是「作者」、「發佈」或「預覽」。
   * 第二個選項是使用前置詞（例如`author_<samevariablename>`和`publish_<samevariablename>`）宣告不同的變數

### 設定範例 {#configuration-examples}

在以下範例中，假設除了舞台和生產環境外，還有三個開發環境。

**範例 1**

目的是讓OSGi屬性`my_var1`的值在階段和生產環境中相同，但三個開發環境的每一個不同。

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
&lbrace; 
 "my_var1"： "val"，
 "my_var2"： "abc"，
 "my_var3"：500
&rbrace;
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
&lbrace; 
 "my_var1" ： "$[env：my_var1]"
 "my_var2"： "abc"，
 "my_var3"：500
&rbrace;
</pre>
</td>
</tr>
</table>

**範例 2**

目的是讓OSGi屬性`my_var1`的值在階段、生產以及三個開發環境的每一個中有所不同。 因此，必須呼叫Cloud Manager API來為每個開發環境設定`my_var1`的值。

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
&lbrace; 
 "my_var1"： "val1"，
 "my_var2"： "abc"，
 "my_var3"：500
&rbrace;
</pre>
</td>
</tr>
<tr>
<td>
config.prod
</td>
<td>
<pre>
&lbrace; 
 "my_var1"： "val2"，
 "my_var2"： "abc"，
 "my_var3"：500
&rbrace;
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
&lbrace; 
 "my_var1" ： "$[env：my_var1]"
 "my_var2"： "abc"，
 "my_var3"：500
&rbrace;
</pre>
</td>
</tr>
</table>

**範例 3**

目的是為了讓OSGi屬性`my_var1`的值在暫存、生產及其中一個開發環境中相同，但在其他兩個開發環境中不同。 在此情況下，必須呼叫Cloud Manager API來為每個開發環境設定`my_var1`的值，包括應具有與中繼和生產環境相同值的開發環境。 它不會繼承資料夾&#x200B;**config**&#x200B;中設定的值。

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
&lbrace; 
 "my_var1"： "val1"，
 "my_var2"： "abc"，
 "my_var3"：500
&rbrace;
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
&lbrace; 
 "my_var1" ： "$[env：my_var1]"
 "my_var2"： "abc"，
 "my_var3"：500
&rbrace;
</pre>
</td>
</tr>
</table>

完成此任務的另一種方法是為config.dev資料夾中的取代權杖設定預設值，使其與&#x200B;**config**&#x200B;資料夾中的值相同。

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
&lbrace; 
 "my_var1"： "val1"，
 "my_var2"： "abc"，
 "my_var3"：500
&rbrace;
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
&lbrace; 
 "my_var1"： "$[env：my_var1；default=val1]"
 "my_var2"： "abc"，
 "my_var3"：500
&rbrace;
</pre>
</td>
</tr>
</table>

## 用於設定屬性的Cloud Manager API格式 {#cloud-manager-api-format-for-setting-properties}

如需Cloud Manager API的相關資訊以及設定方式，請參閱[在Adobe Developer網站](https://developer.adobe.com/experience-cloud/cloud-manager/docs/)上AdobeCloud Manager 。

>[!NOTE]
>
>確保使用的Cloud Manager API已指派「部署管理員 — Cloud Service」角色。 其他角色無法執行以下所有命令。

>[!TIP]
>
>您也可以使用Cloud Manager來設定環境變數。 如需詳細資訊，請參閱[Cloud Manager環境變數](/help/implementing/cloud-manager/environment-variables.md)。

### 透過API設定值 {#setting-values-via-api}

呼叫API會將新變數和值部署至雲端環境，類似於典型的客戶程式碼部署管道。 作者和發佈服務會重新啟動，並參考新值，通常需要幾分鐘的時間。

```
PATCH /program/{programId}/environment/{environmentId}/variables
```

```json
[
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
>預設變數不是透過API設定，而是在OSGi屬性本身中設定。
>
>如需詳細資訊，請參閱[Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/)。

### 透過API取得值 {#getting-values-via-api}

```
GET /program/{programId}/environment/{environmentId}/variables
```

如需詳細資訊，請參閱[Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/)。

### 透過API刪除值 {#deleting-values-via-api}

```
PATCH /program/{programId}/environment/{environmentId}/variables
```

若要刪除變數，請將其納入空白值。

如需詳細資訊，請參閱[Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/)。

### 透過命令列取得值 {#getting-values-via-cli}

```bash
$ aio cloudmanager:list-environment-variables ENVIRONMENT_ID
Name     Type         Value
MY_VAR1  string       plaintext value 
MY_VAR2  secretString ****
```


### 透過命令列設定值 {#setting-values-via-cli}

```bash
$ aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable MY_VAR1 "plaintext value" --secret MY_VAR2 "some secret value"
```

### 透過命令列刪除值 {#deleting-values-via-cli}

```bash
$ aio cloudmanager:set-environment-variables ENVIRONMENT_ID --delete MY_VAR1 MY_VAR2
```

>[!NOTE]
>
>請參閱GitHub[&#128279;](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid)上的aio-cli-plugin-cloudmanager，以取得有關如何使用Cloud Manager外掛程式為Adobe I/OCLI設定值的詳細資訊。

### 變數數量 {#number-of-variables}

每個環境最多可以宣告200個變數。

## 秘密和環境特定設定值的部署考量事項 {#deployment-considerations-for-secret-and-environment-specific-configuration-values}

由於機密和特定環境的設定值位於Git之外，因此不屬於正式的Adobe Experience Manager as a Cloud Service部署機制，因此客戶應管理、控管並整合至Adobe Experience Manager as a Cloud Service部署程式。

如上所述，呼叫API會將新變數和值部署到雲端環境，類似於典型的客戶程式碼部署管道。 作者和發佈服務會重新啟動，並參考新值，通常需要幾分鐘的時間。 在此過程中，Cloud Manager在定期程式碼部署期間執行的品質閘道和測試不會執行。

通常，客戶在部署在Cloud Manager中依賴環境變數的程式碼之前，會呼叫API來設定環境變數。 在某些情況下，您可能想要在部署程式碼後修改現有變數。

>[!NOTE]
>
>當管道正在使用中(AEM更新或客戶部署)時，API可能不會成功，具體取決於當時端對端管道執行的部分。 錯誤回應會指出要求不成功，但不會指出特定原因。

在某些情況下，已排程的客戶程式碼部署會依賴現有變數來擁有新值，而這對目前的程式碼而言是不合適的。 如果這令人擔憂，建議以累加方式進行變數修改。 若要這麼做，請建立新的變數名稱，而非只變更舊變數的值，讓舊程式碼絕不會參考新值。 然後，當新的客戶版本看起來穩定時，您可以選擇移除舊的值。

同樣地，由於變數的值未建立版本，程式碼復原可能會導致它參考較新的值，進而導致問題。 前述的加法變數策略在此也有幫助。

此附加變數策略也適合用於需要重新部署數天前程式碼的災害復原情況，其參照的變數名稱和值將維持不變。 這有賴於客戶在移除這些舊版變數前會等待數天的策略，否則舊版程式碼將沒有適當的變數可參照。
