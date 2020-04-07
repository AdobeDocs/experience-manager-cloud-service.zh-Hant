---
title: 記錄
description: 瞭解如何為中央記錄服務設定全域參數、個別服務的特定設定，或如何要求資料記錄。
translation-type: tm+mt
source-git-commit: 73813dd87e3eebfe26673640125ea64916e14789

---


# 記錄{#logging}

AEM做為雲端服務，可讓您設定：

* 中央記錄服務的全局參數
* 要求資料記錄；要求資訊的專用記錄設定
* 個別服務的特定設定；例如，日誌消息的單個日誌檔案和格式

在本地開發中，日誌條目將寫入資料夾中的本地 `/crx-quickstart/logs` 檔案。

在雲端環境中，開發人員可以透過Cloud Manager下載記錄檔，或使用命令列工具來追蹤記錄檔。

>[!NOTE]
>
>以雲端服務身分登入AEM是以Sling原則為基礎。 如需詳 [細資訊，請參閱Sling](https://sling.apache.org/site/logging.html) Logging。

## 全域記錄 {#global-logging}

[Apache Sling Logging Configuration](https://sling.apache.org/documentation/development/logging.html#user-configuration---osgi-based) is used to configure the root logger. 這會定義將AEM登入為雲端服務的全域設定：

* 記錄級別
* 中央日誌檔案的位置
* 要保存的版本數
* 版本輪換；最大大小或時間間隔
* 寫入日誌消息時使用的格式

## 個人服務的記錄者和撰寫者 {#loggers-and-writers-for-individual-services}

除了全域記錄設定外，AEM as a Cloud Service還可讓您針對個別服務設定特定設定：

* 特定記錄級別
* 單個日誌檔案的位置
* 要保存的版本數
* 版本輪換；最大大小或時間間隔
* 寫入日誌消息時使用的格式
* the logger(the OSGi service suppliding the log messages)

這可讓您將單一服務的記錄訊息傳送至個別檔案。 這在開發或測試時特別有用；例如，當您需要特定服務的日誌級別提高時。

AEM as a Cloud Service使用下列功能將記錄訊息寫入檔案：

1. An **OSGi service** (logger)writes a log message.
1. A **Logging Logger** takes this message and formats it according your specification.
1. 記 **錄寫入器** (Logging Writer)將所有這些消息寫入您定義的物理檔案。

這些元素會依下列參數連結至適當的元素：

* **Logger(Logging Logger)**

   定義生成消息的服務。

* **記錄檔（記錄檔）**

   定義用於儲存日誌消息的物理檔案。

   This is used to link a Logging Logger with a Logging Writer. 該值必須與要建立的連接的記錄寫入器配置中的相同參數相同。

* **日誌檔案（記錄寫入器）**

   定義日誌消息將寫入的物理檔案。

   此參數必須與記錄寫入器配置中的相同參數相同，否則不會進行匹配。 如果沒有匹配項，則將使用預設配置（每日日誌旋轉）建立隱式寫入器。

### 標準記錄工具和作者 {#standard-loggers-and-writers}

標準AEM中包含某些記錄檔和撰寫程式，做為雲端服務安裝。

第一個是特殊情況，因為它同時控制 `request.log` 和文 `access.log` 件：

* The Logger:

   * Apache Sling Customized Request Data Logger

      (org.apache.sling.engine.impl.log.RequestLoggerService)

   * 將請求內容的相關訊息寫入 `request.log`。

* 連結至：

   * Apache Sling Request Logger

      (org.apache.sling.engine.impl.log.RequestLogger)

   * 將消息寫入或 `request.log` 中 `access.log`。

如果需要，可自訂這些設定，但標準組態適合大部分安裝。

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

* 不連結到特定寫入器，因此將建立並使用具有預設配置的隱式寫入器（每日日誌旋轉）。

## 設定日誌級別 {#setting-the-log-level}

若要變更雲端環境的記錄層級，Sling Logging OSGI組態應加以修改，然後進行完整重新部署。 由於這並非瞬時，請務必小心在接收大量流量的生產環境中啟用詳細記錄。 在未來，可能會有更快速變更記錄層級的機制。

> [!NOTE]
> 
> 若要執行下列的設定變更，您必須在本機開發環境上建立這些變更，然後將它們推送至AEM做為雲端服務例項。 如需如何執行此動作的詳細資訊，請參 [閱「部署至AEM as a Cloud Service](/help/implementing/deploying/overview.md)」。

### 啟用DEBUG日誌級別 {#activating-the-debug-log-level}

> [!WARNING]
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

   1. 指定「記錄檔」。
   1. 指定記錄器。
   1. 視需要設定其他參數。

1. 建立Factory Configuration [Apache Sling Logging Writer Configuration的新例項](https://sling.apache.org/documentation/development/logging.html#user-configuration---osgi-based)。

   1. 指定Log File - this must match that specified for the Logger.
   1. 視需要設定其他參數。

### 建立自訂記錄檔 {#create-a-custom-log-file}

>[!NOTE]
>
>使用Adobe Experience Manager時，有幾種方法可管理此類服務的組態設定。

在某些情況下，您可能希望建立具有不同日誌級別的自定義日誌檔案。 您可以通過以下方式在儲存庫中執行此操作：

1. 如果尚未存在，請為您的項目建立新的配 `sling:Folder`置資料夾() `/apps/<*project-name*>/config`。
1. 在下 `/apps/<*project-name*>/config`面，為新的Apache Sling Logging Logger Configuration建立節點：

   * 名稱： `org.apache.sling.commons.log.LogManager.factory.config-<*identifier*>` (as this is a Logger)

      其中 `<*identifier*>` 由您（必須）輸入以標識實例的自由文本替換（您不能忽略此資訊）。

      例如， `org.apache.sling.commons.log.LogManager.factory.config-MINE`

   * 類型: `sling:OsgiConfig`
   >[!NOTE]
   >
   >雖然不是技術要求，但最好是獨一無 `<*identifier*>` 二。

1. 在此節點上設定以下屬性：

   * 名稱: `org.apache.sling.commons.log.file`

      類型：字串

      值：指定日誌檔案；例如， `logs/myLogFile.log`

   * 名稱: `org.apache.sling.commons.log.names`

      類型：字串[] （字串+多重）

      值：指定Logger要記錄訊息的OSGi services;例如，以下所有項目：

      * `org.apache.sling`
      * `org.apache.felix`
      * `com.day`
   * 名稱: `org.apache.sling.commons.log.level`

      類型：字串

      值：指定所需的日誌級 `debug`別( `info`、 `warn` 或 `error`);例如 `debug`

   * 視需要設定其他參數：

      * 名稱: `org.apache.sling.commons.log.pattern`

         類型: `String`

         值：根據需要指定日誌消息的模式；例如，

         `{0,date,dd.MM.yyyy HH:mm:ss.SSS} *{4}* [{2}] {3} {5}`
   >[!NOTE]
   >
   >`org.apache.sling.commons.log.pattern` 最多支援6個引數。

   >{0}類型的時間戳記 `java.util.Date`
   >
   >{1}記錄標籤{2}目前執行緒的名稱{3}記錄器{4}記錄層級{5}記錄訊息的名稱

   >如果日誌調用包含 `Throwable` 堆棧跟蹤，則附加到消息。

   >[!CAUTION]
   org.apache.sling.commons.log.names必須有值。

   >[!NOTE]
   日誌寫入器路徑與位置相 `crx-quickstart` 對。
   因此，日誌檔案指定為：
   `logs/thelog.log`

   >寫入：
   `` ` ` `<*cq-installation-dir*>/``crx-quickstart/logs/thelog.log`。
   以及指定為：
   `../logs/thelog.log`

   >寫入目錄：
   ` <*cq-installation-dir*>/logs/`
&quot;(即&lt; ` `cq-installation-dir *>/*`crx-quickstart/`)

1. 只有在需要新寫入器時（即配置與預設寫入器不同），才需要此步驟。

   >[!CAUTION]
   只有當現有預設值不適合時，才需要新的記錄寫入器配置。

   >如果未配置顯式寫入器，系統將根據預設自動生成隱式寫入器。

   在下 `/apps/<*project-name*>/config`面，為新配置建立 `Apache Sling Logging Writer` 節點：

   * 名稱： `org.apache.sling.commons.log.LogManager.factory.writer-<*identifier*>` （因為這是作家）

      與Logger一樣， `<*identifier*>` 由您（必須）enter用來識別實例的自由文本（您不能忽略此資訊）替換。 例如， `org.apache.sling.commons.log.LogManager.factory.writer-MINE`

   * 類型: `sling:OsgiConfig`
   >[!NOTE]
   雖然不是技術要求，但最好是獨一無 `<*identifier*>` 二。

   在此節點上設定以下屬性：

   * 名稱: `org.apache.sling.commons.log.file`

      類型: `String`

      值：指定Log File，使其與Logger；中指定的檔案匹配

      例如， `../logs/myLogFile.log`。

   * 視需要設定其他參數：

      * 名稱: `org.apache.sling.commons.log.file.number`

         類型: `Long`

         值：指定要保留的日誌檔案數；例如， `5`

      * 名稱: `org.apache.sling.commons.log.file.size`

         類型: `String`

         值：指定依大小／日期控制檔案旋轉；例如， `'.'yyyy-MM-dd`
   >[!NOTE]
   `org.apache.sling.commons.log.file.size` 通過設定以下任一設定控制日誌檔案的旋轉：
   * 最大檔案大小
   * 時間／日期計畫
   以指示何時將建立新檔案（並根據名稱模式更名現有檔案）。
   * 可以用數字指定大小限制。 如果沒有提供大小指示器，則此指示器被視為位元組數，或者您可以添加一個大小指示器- `KB`、 `MB`或 `GB` （忽略大小寫）。
   * 時間／日期排程可指定為模 `java.util.SimpleDateFormat` 式。 這定義了檔案旋轉的時段；也附加到旋轉檔案的字尾（用於識別）。
   預設值為&#39;.&#39;。yyyy-MM-dd（用於每日日誌旋轉）。
   例如，在2010年1月20日的午夜（或當發生此事後的第一個記錄訊息時，請務必精確）,../logs/error.log將重新命名為../logs/error.log.2010-01-20。 1月21日的記錄將輸出為（新的和空的）../logs/error.log，直到在下一天的變更時滾動。
       | `&#39;.&#39;yyyy-MM`|每月初的輪值|
    |—|—|
    | &#39;&#39;。&#39;yyyy-ww`|每週第一天的旋轉（視地區而定）。 |
       | `&#39;.&#39;yyyy-MM-dd`每天午夜時輪流。 |
       | `&#39;.&#39;yyyy-MM-dd-a`在每天的午夜和中午旋轉。 |
       | `&#39;.&#39;yyyy-MM-dd-HH`每小時最上方的旋轉。 |
       | `&#39;.&#39;yyyy-MM-dd-HH-mm`每分鐘開始時輪流。 |
     
    Note:指定時間／日期時：
      1. 您應「逸出」一對單引號(&#39; &#39;)中的常值文字；
  這     是為了避免某些字元被解譯為圖樣字母。
       1. 在選項中的任何位置，僅允許使用有效檔案名的字元。
   

1. 使用您選擇的工具讀取您的新記錄檔。

   由此示例建立的日誌檔案將為 `../crx-quickstart/logs/myLogFile.log`。

Felix Console也提供Sling Log Support的相關資訊，網址為 `../system/console/slinglog`;例 `https://localhost:4502/system/console/slinglog`如