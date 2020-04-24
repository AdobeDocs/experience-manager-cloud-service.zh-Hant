---
title: 記錄
description: 瞭解如何為中央記錄服務設定全域參數、個別服務的特定設定，或如何要求資料記錄。
translation-type: tm+mt
source-git-commit: 8a6207596c42c4e1cf85dcccdbd1a1e9501c9073

---


# 記錄{#logging}

AEM即雲端服務是客戶可加入自訂程式碼的平台，可為客戶群建立獨特的體驗。 有鑑於此，登入是在雲端環境中除錯自訂程式碼（尤其是針對本機開發環境）的重要功能。


<!-- ## Global Logging {#global-logging}

[Apache Sling Logging Configuration](https://sling.apache.org/documentation/development/logging.html#user-configuration---osgi-based) is used to configure the root logger. This defines the global settings for logging in AEM as a Cloud Service:

* the logging level
* the location of the central log file
* the number of versions to be kept
* version rotation; either maximum size or a time interval
* the format to be used when writing the log messages
-->

## AEM as a Cloud Service Logging {#aem-as-a-cloud-service-logging}

AEM做為雲端服務，可讓您設定：

* 中央記錄服務的全局參數
* 要求資料記錄；要求資訊的專用記錄設定
* 個別服務的特定設定

在本地開發中，日誌條目將寫入資料夾中的本地 `/crx-quickstart/logs` 檔案。

在雲端環境中，開發人員可以透過Cloud Manager下載記錄檔，或使用命令列工具來追蹤記錄檔。

>[!NOTE]
>
>以雲端服務身分登入AEM是以Sling原則為基礎。 如需詳 [細資訊，請參閱Sling](https://sling.apache.org/site/logging.html) Logging。

## AEM as a Cloud Service Java記錄 {#aem-as-a-cloud-service-java-logging}

### 標準記錄工具和作者 {#standard-loggers-and-writers}

> [!IMPORTANT]
> 如果需要，可自訂這些設定，但標準組態適合大部分安裝。 但是，如果您需要自訂標準記錄設定，請務必只在環境中 `dev` 執行。

標準AEM中包含某些記錄檔和撰寫程式，做為雲端服務安裝。

第一個是特殊情況，因為它同時控制 `request` 和記 `access` 錄：

* The Logger:

   * Apache Sling Customized Request Data Logger

      (org.apache.sling.engine.impl.log.RequestLoggerService)

   * 將請求內容的相關訊息寫入 `request.log`。

* 連結至：

   * Apache Sling Request Logger

      (org.apache.sling.engine.impl.log.RequestLogger)

   * 將消息寫入或 `request.log` 中 `access.log`。

其他配對遵循標準配置：

* The Logger:

   * Apache Sling Logging Logger Configuration

      (org.apache.sling.commons.log.LogManager.factory.config)

   * 將消 `Information` 息寫入 `logs/error.log`。

* Links to the Writer:

   * Apache Sling Logging Writer Configuration

      (org.apache.sling.commons.log.LogManager.factory.writer)

* The Logger:

   * Apache Sling Logging Logger Configuration(org.apache.sling.commons.log.LogManager.factory.config.649d51b7-6425-45c9-81e6-2697a03d6be7)

   * 將消 `Warning` 息寫入 `../logs/error.log` 服務的消息 `org.apache.pdfbox`。

* 不連結到特定的Writer，因此將建立並使用具有預設配置的隱式Writer。

**AEM as a Cloud Service HTTP Request Logging**

AEM WCM和儲存庫的所有存取要求都會在此處註冊。

輸出示例：

**AEM：雲端服務HTTP請求／回應存取記錄**

每個存取請求都會在此與回應一起註冊。

輸出示例：

**Apache Web Server / Dispatcher Logging**

這是用於調試Dispatcher問題的日誌。 如需詳細資訊，請參 [閱除錯您的Apache和Dispatcher設定](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/implementing/)。

<!-- Besides the three types of logs present on an AEM as a Cloud Service instance (`request`, `access` and `error` logs) there is another dispatcher/overview.html#debugging-apache-and-dispatcher-configuration.

leftover text from the last breakaway chunk (re dispatcher) -->

就最早的實務而言，建議您與AEM中目前存在的組態一致，成為Cloud Service Maven原型。 這些設定為特定環境類型設定不同的日誌設定和級別：

* for `local dev` and `dev` environments, set the logger to **DEBUG** level to the `error.log`
* for `stage`, set logger to **WARN** level to the `error.log`
* for `prod`, set logger to **ERROR** level to the `error.log`

請針對每個組態尋找下列範例：

* `dev` 環境：

```
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
    xmlns:jcr="http://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig"
    org.apache.sling.commons.log.level="debug"
    org.apache.sling.commons.log.names="[com.mycompany.myapp]" />
```


* `stage` 環境：

```
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
    xmlns:jcr="http://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig"
    org.apache.sling.commons.log.level="warn"
    org.apache.sling.commons.log.names="[com.mycompany.myapp]" />
```

* `prod` 環境：

```
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
    xmlns:jcr="http://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig"
    org.apache.sling.commons.log.level="error"
    org.apache.sling.commons.log.names="[com.mycompany.myapp]" />
```

### 個人服務的記錄者和撰寫者 {#loggers-and-writers-for-individual-services}

除了全域記錄設定外，AEM as a Cloud Service還可讓您針對個別服務設定特定設定：

* 特定記錄級別
* the logger(the OSGi service suppliding the log messages)

這可讓您將單一服務的記錄訊息傳送至個別檔案。 這在開發或測試時特別有用；例如，當您需要特定服務的日誌級別提高時。

AEM as a Cloud Service使用下列功能將記錄訊息寫入檔案：

1. An **OSGi service** (logger)writes a log message.
1. A **Logging Logger** takes this message and formats it according your specification.
1. 記 **錄寫入器** (Logging Writer)將所有這些消息寫入您定義的物理檔案。

這些元素會依下列參數連結至適當的元素：

* **Logger(Logging Logger)**

   定義生成消息的服務。

<!-- * **Log File (Logging Logger)**

  Define the physical file for storing the log messages.

  This is used to link a Logging Logger with a Logging Writer. The value must be identical to the same parameter in the Logging Writer configuration for the connection to be made.

* **Log File (Logging Writer)**

  Define the physical file that the log messages will be written to.

  This must be identical to the same parameter in the Logging Writer configuration, or the match will not be made. If there is no match then an implicit Writer will be created with default configuration (daily log rotation).
-->

### 設定日誌級別 {#setting-the-log-level}

若要變更雲端環境的記錄層級，Sling Logging OSGI組態應加以修改，然後進行完整重新部署。 由於這並非瞬時，請務必小心在接收大量流量的生產環境中啟用詳細記錄。 在未來，可能會有更快速變更記錄層級的機制。

>[!NOTE]
>
> 若要執行下列的設定變更，您必須在本機開發環境上建立這些變更，然後將它們推送至AEM做為雲端服務例項。 如需如何執行此動作的詳細資訊，請參 [閱「部署至AEM as a Cloud Service](/help/implementing/deploying/overview.md)」。

**啟用DEBUG日誌級別**

>[!WARNING]
>
> 全局激活DEBUG日誌級別將產生大量難以篩選的資訊。 建議您僅針對需要除錯的服務啟用它。 如需詳細資訊，請參 [閱「個別服務的記錄員和撰寫者」](logging.md#loggers-and-writers-for-individual-services)。

預設日誌級別為INFO，即不記錄DEBUG消息。
若要啟用DEBUG記錄檔層級，請設定

``` /libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level ```

屬性進行除錯。 請勿將記錄檔保留在DEBUG記錄檔層級，因為它會產生許多記錄檔。
除錯檔案中的一行通常以DEBUG開頭，然後提供記錄檔層級、安裝程式動作和記錄檔訊息。 例如：

``` DEBUG 3 WebApp Panel: WebApp successfully deployed ```

日誌級別如下：

| 0 | 致命錯誤 | 動作失敗，安裝程式無法繼續。 |
|---|---|---|
| 1 | 錯誤 | 動作失敗。 安裝將繼續，但CRX的某部分安裝不正確，因此無法正常工作。 |
| 2 | 警告 | 行動成功，但遇到問題。 CRX可能正常工作，也可能無法正常工作。 |
| 3 | 資訊 | 動作成功。 |

### 建立您自己的記錄工具和作者 {#creating-your-own-loggers-and-writers}

您可以定義自己的記錄器／寫入器對：

1. 建立Factory Configuration [Apache Sling Logger Configuration的新例項](https://sling.apache.org/documentation/development/logging.html#user-configuration---osgi-based)。

   1. 指定記錄器。

<!-- 1. Create a new instance of the Factory Configuration [Apache Sling Logging Writer Configuration](https://sling.apache.org/documentation/development/logging.html#user-configuration---osgi-based).

    1. Specify the Log File - this must match that specified for the Logger.
    1. Configure the other parameters as required. -->

### 設定記錄 {#configure-logging}

>[!NOTE]
>
>使用Adobe Experience Manager時，有幾種方法可管理此類服務的組態設定。

在某些情況下，您可能希望建立具有不同日誌級別的自定義日誌。 您可以通過以下方式在儲存庫中執行此操作：

1. 如果尚未存在，請為您的項目建立新的配 `sling:Folder`置資料夾() `/apps/<*project-name*>/config`。
1. 在下 `/apps/<*project-name*>/config`面，為新的Apache Sling Logging Logger Configuration建立節點：

   * 名稱： `org.apache.sling.commons.log.LogManager.factory.config-<*identifier*>` (as this is a Logger)

      其中 `<*identifier*>` 由您（必須）輸入以標識實例的自由文本替換（您不能忽略此資訊）。

      例如， `org.apache.sling.commons.log.LogManager.factory.config-MINE`

   * 類型: `sling:OsgiConfig`
   >[!NOTE]
   >
   >雖然不是技術要求，但最好是獨一無 `<*identifier*>` 二。

<!-- 1. Set the following properties on this node:

    * Name: `org.apache.sling.commons.log.file`

      Type: String

      Value: specify the Log File; for example, `logs/myLogFile.log`

    * Name: `org.apache.sling.commons.log.names`

      Type: String[] (String + Multi)

      Value: specify the OSGi services for which the Logger is to log messages; for example, all of the following:

        * `org.apache.sling`
        * `org.apache.felix`
        * `com.day`

    * Name: `org.apache.sling.commons.log.level`

      Type: String

      Value: specify the log level required ( `debug`, `info`, `warn` or `error`); for example `debug`

    * Configure the other parameters as required:

        * Name: `org.apache.sling.commons.log.pattern`

          Type: `String`

          Value: specify the pattern of the log message as required; for example,

          `{0,date,dd.MM.yyyy HH:mm:ss.SSS} *{4}* [{2}] {3} {5}`

   >[!NOTE]
   >
   >`org.apache.sling.commons.log.pattern` supports up to six arguments.

   >
   >
   >{0} The timestamp of type `java.util.Date`
   >{1} the log marker
   >{2} the name of the current thread
   >{3} the name of the logger
   >{4} the log level
   >{5} the log message

   >
   >
   >If the log call includes a `Throwable` the stacktrace is appended to the message.

   >[!CAUTION]
   >
   >org.apache.sling.commons.log.names must have a value.

   >[!NOTE]
   >
   >Log writer paths are relative to the `crx-quickstart` location.
   >
   >
   >Therefore, a log file specified as:
   >
   >
   >`logs/thelog.log`

   >
   >
   >writes to:
   >
   >
   >`` ` ` `<*cq-installation-dir*>/``crx-quickstart/logs/thelog.log`.
   >
   >
   >And a log file specified as:
   >
   >
   >`../logs/thelog.log`

   >
   >
   >writes to a directory:
   >
   >
   >` <*cq-installation-dir*>/logs/`
   >``(i.e. next to ` `<*cq-installation-dir*>/`crx-quickstart/`)
 -->

<!-- open question: see if we need to leave the above warning note in place, but adjust it so that it doesn't mention filenames -->

<!-- 1. This step is only necessary when a new Writer is required (i.e. with a configuration that is different to the default Writer).

   >[!CAUTION]
   >
   >A new Logging Writer Configuration is only required when the existing default is not suitable.

   >
   >
   >If no explicit Writer is configured the system will automatically generate an implicit Writer based on the default.

   Under `/apps/<*project-name*>/config`, create a node for the new `Apache Sling Logging Writer` Configuration:

    * Name: `org.apache.sling.commons.log.LogManager.factory.writer-<*identifier*>` (as this is a Writer)

      As with the Logger, `<*identifier*>` is replaced by free text that you (must) enter to identify the instance (you cannot omit this information). For example, `org.apache.sling.commons.log.LogManager.factory.writer-MINE`

    * Type: `sling:OsgiConfig`

   >[!NOTE]
   >
   >Although not a technical requirement, it is advisable to make `<*identifier*>` unique.

   Set the following properties on this node:

    * Name: `org.apache.sling.commons.log.file`

      Type: `String`

      Value: specify the Log File so that it matches the file specified in the Logger;

      for this example, `../logs/myLogFile.log`.

    * Configure the other parameters as required:

        * Name: `org.apache.sling.commons.log.file.number`

          Type: `Long`

          Value: specify the number of log files you want kept; for example, `5`

        * Name: `org.apache.sling.commons.log.file.size`

          Type: `String`

          Value: specify as required to control file rotation by size/date; for example, `'.'yyyy-MM-dd`

   >[!NOTE]
   >
   >`org.apache.sling.commons.log.file.size` controls the rotation of the log file by setting either:
   >
   >* a maximum file size
   >* a time/date schedule
   >
   >to indicate when a new file will be created (and the existing file renamed according to the name pattern).
   >
   >* A size limit can be specified with a number. If no size indicator is given, then this is taken as the number of bytes, or you can add one of the size indicators - `KB`, `MB`, or `GB` (case is ignored).
   >* A time/date schedule can be specified as a `java.util.SimpleDateFormat` pattern. This defines the time period after which the file will be rotated; also the suffix appended to the rotated file (for identification).
   >
   >The default is '.'yyyy-MM-dd (for daily log rotation).
   >
   >So for example, at midnight of January 20th 2010 (or when the first log message after this occurs to be precise), ../logs/error.log will be renamed to ../logs/error.log.2010-01-20. Logging for the 21st of January will be output to (a new and empty) ../logs/error.log until it is rolled over at the next change of day.
   >
   >      | `'.'yyyy-MM` |Rotation at the beginning of each month |
   >      |---|---|
   >      | `'.'yyyy-ww` |Rotation at the first day of each week (depends on the locale). |
   >      | `'.'yyyy-MM-dd` |Rotation at midnight each day. |
   >      | `'.'yyyy-MM-dd-a` |Rotation at midnight and midday of each day. |
   >      | `'.'yyyy-MM-dd-HH` |Rotation at the top of every hour. |
   >      | `'.'yyyy-MM-dd-HH-mm` |Rotation at the beginning of every minute. |
   >
   >      Note: When specifying a time/date:
   >      1. You should "escape" literal text within a pair of single quotes (' ');
   >      this is to avoid certain characters being interpreted as pattern letters.
   >      1. Only use characters allowed for a valid file name anywhere in the option.

1. Read your new log file with your chosen tool.

   The log file created by this example will be `../crx-quickstart/logs/myLogFile.log`. -->

Felix Console也提供Sling Log Support的相關資訊，網址為 `../system/console/slinglog`;例 `https://localhost:4502/system/console/slinglog`如

## 存取和管理記錄檔 {#manage-logs}

用戶可以使用環境卡訪問選定環境的可用日誌檔案清單。  用戶可以訪問選定環境的可用日誌檔案清單。

這些檔案可透過UI從「概述」頁面 **下載** 。

![](assets/manage-logs1.png)

或者，「環 **境** 」頁：

![](assets/manage-logs2.png)

>[!Note]
>不論其開啟位置為何，都會出現相同的對話方塊，並允許下載個別記錄檔。

![](assets/manage-logs3.png)


### 透過API記錄檔 {#logs-thorugh-api}

除了透過UI下載記錄檔外，記錄檔也可透過API和命令列介面使用。

例如，要下載特定環境的日誌檔案，命令將是

```java
$ aio cloudmanager:download-logs --programId 5 1884 author aemerror
```

以下命令允許跟蹤日誌：

```java
$ aio cloudmanager:tail-log --programId 5 1884 author aemerror
```

為了獲得環境ID（在本例中為1884）和可用的服務或日誌名稱選項，您可以使用：

```java
$ aio cloudmanager:list-environments
Environment Id Name                     Type  Description                          
1884           FoundationInternal_dev   dev   Foundation Internal Dev environment  
1884           FoundationInternal_stage stage Foundation Internal STAGE environment
1884           FoundationInternal_prod  prod  Foundation Internal Prod environment
 
 
$ aio cloudmanager:list-available-log-options 1884
Environment Id Service    Name         
1884           author     aemerror     
1884           author     aemrequest   
1884           author     aemaccess    
1884           publish    aemerror     
1884           publish    aemrequest   
1884           publish    aemaccess    
1884           dispatcher httpderror   
1884           dispatcher aemdispatcher
1884           dispatcher httpdaccess
```

>[!Note]
>雖 **然「記錄下載** 」將可透過UI和API使用，但 **「記錄追蹤** 」僅限API/CLI。

### 其他資源 {#resources}

請參閱下列其他資源，以進一步瞭解Cloud Manager API和Adobe I/O CLI:

* [Cloud Manager API檔案](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html)
* [Adobe I/O CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager)