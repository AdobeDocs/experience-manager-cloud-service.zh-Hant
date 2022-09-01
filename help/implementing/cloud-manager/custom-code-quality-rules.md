---
title: 自訂程式碼品質規則
description: 本頁說明Cloud Manager在[程式碼品質測試]中執行的自訂程式碼品質規則。 這些建議以AEM工程的最佳實務為基礎。
exl-id: f40e5774-c76b-4c84-9d14-8e40ee6b775b
source-git-commit: 421ad8506435e8538be9c83df0b78ad8f222df0c
workflow-type: tm+mt
source-wordcount: '3493'
ht-degree: 4%

---

# 自訂程式碼品質規則 {#custom-code-quality-rules}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_customcodequalityrules"
>title="自訂程式碼品質規則"
>abstract="本頁說明Cloud Manager在程式碼品質測試中所執行的自訂程式碼品質規則。 這些建議以AEM工程的最佳實務為基礎。"

本頁說明Cloud Manager在 [程式碼品質測試。](/help/implementing/cloud-manager/code-quality-testing.md) 這些建議以AEM工程的最佳實務為基礎。

>[!NOTE]
>
>此處提供的程式碼範例僅供說明之用。 看聲納快報 [概念檔案](https://docs.sonarqube.org/7.4/user-guide/concepts/) 了解聲納庫比的概念和質量規則。

## SonarQube規則 {#sonarqube-rules}

以下章節詳細說明Cloud Manager執行的SonarQube規則。

### 不使用潛在危險的功能 {#do-not-use-potentially-dangerous-functions}

* **金鑰**:CQRules:CWE-676
* **類型**:漏洞
* **嚴重性**:主要
* **自**:2018.4.0版

方法 `Thread.stop()` 和 `Thread.interrupt()` 可能會產生難以重現的問題，在某些情況下，還會產生安全漏洞。 它們的使用應受到嚴密監控和驗證。總的來說，傳遞資訊是實現類似目標的更安全的方式。

#### 不相容代碼 {#non-compliant-code}

```java
public class DontDoThis implements Runnable {
  private Thread thread;
 
  public void start() {
    thread = new Thread(this);
    thread.start();
  }
 
  public void stop() {
    thread.stop();  // UNSAFE!
  }
 
  public void run() {
    while (true) {
        somethingWhichTakesAWhileToDo();
    }
  }
}
```

#### 相容代碼 {#compliant-code}

```java
public class DoThis implements Runnable {
  private Thread thread;
  private boolean keepGoing = true;
 
  public void start() {
    thread = new Thread(this);
    thread.start();
  }
 
  public void stop() {
    keepGoing = false;
  }
 
  public void run() {
    while (this.keepGoing) {
        somethingWhichTakesAWhileToDo();
    }
  }
}
```

### 請勿使用可能受外部控制的格式字串 {#do-not-use-format-strings-which-may-be-externally-controlled}

* **金鑰**:CQRules:CWE-134
* **類型**:漏洞
* **嚴重性**:主要
* **自**:2018.4.0版

使用來自外部源的格式字串（如請求參數或用戶生成的內容）可以生成，使應用程式暴露於拒絕服務攻擊。 在某些情況下，格式字串可能受外部控制，但僅允許來自受信任的源。

#### 不相容代碼 {#non-compliant-code-1}

```java
protected void doPost(SlingHttpServletRequest request, SlingHttpServletResponse response) {
  String messageFormat = request.getParameter("messageFormat");
  request.getResource().getValueMap().put("some property", String.format(messageFormat, "some text"));
  response.sendStatus(HttpServletResponse.SC_OK);
}
```

### HTTP要求應一律有通訊端和連線逾時 {#http-requests-should-always-have-socket-and-connect-timeouts}

* **金鑰**:CQRules:ConnectionTimeoutMechanism
* **類型**:錯誤
* **嚴重性**:關鍵
* **自**:2018.6.0版

從AEM應用程式內執行HTTP要求時，請務必確保已設定正確逾時，以避免不必要的執行緒耗用。 很可惜，兩個Java預設HTTP用戶端的預設行為(`java.net.HttpUrlConnection`)，且常用的Apache HTTP元件用戶端永不逾時，因此必須明確設定逾時。 此外，作為最佳實務，這些逾時不應超過60秒。

#### 不相容代碼 {#non-compliant-code-2}

```java
@Reference
private HttpClientBuilderFactory httpClientBuilderFactory;
 
public void dontDoThis() {
  HttpClientBuilder builder = httpClientBuilderFactory.newBuilder();
  HttpClient httpClient = builder.build();

  // do something with the client
}

public void dontDoThisEither() {
  URL url = new URL("http://www.google.com");
  URLConnection urlConnection = url.openConnection();
 
  BufferedReader in = new BufferedReader(new InputStreamReader(
    urlConnection.getInputStream()));
 
  String inputLine;
  while ((inputLine = in.readLine()) != null) {
    logger.info(inputLine);
  }
 
  in.close();
}
```

#### 相容代碼 {#compliant-code-1}

```java
@Reference
private HttpClientBuilderFactory httpClientBuilderFactory;
 
public void doThis() {
  HttpClientBuilder builder = httpClientBuilderFactory.newBuilder();
  RequestConfig requestConfig = RequestConfig.custom()
    .setConnectTimeout(5000)
    .setSocketTimeout(5000)
    .build();
  builder.setDefaultRequestConfig(requestConfig);
 
  HttpClient httpClient = builder.build();
   
  // do something with the client
}

public void orDoThis() {
  URL url = new URL("http://www.google.com");
  URLConnection urlConnection = url.openConnection();
  urlConnection.setConnectTimeout(5000);
  urlConnection.setReadTimeout(5000);
 
  BufferedReader in = new BufferedReader(new InputStreamReader(
    urlConnection.getInputStream()));
 
  String inputLine;
  while ((inputLine = in.readLine()) != null) {
    logger.info(inputLine);
  }
 
  in.close();
}
```

### 應始終關閉ResourceResolver對象 {#resourceresolver-objects-should-always-be-closed}

* **金鑰**:CQRules:CQBP-72
* **類型**:代碼氣味
* **嚴重性**:主要
* **自**:2018.4.0版

`ResourceResolver` 從 `ResourceResolverFactory` 使用系統資源。 雖然已制定措施，以在 `ResourceResolver` 不再使用，則明確關閉任何已開啟的 `ResourceResolver` 對象，通過調用 `close()` 方法。

一個相對常見的誤解是 `ResourceResolver` 使用現有JCR會話建立的對象不應顯式關閉，否則將關閉基礎的JCR會話。 情況並非如此。 無論 `ResourceResolver` 已開啟，則應在不再使用時關閉。 自 `ResourceResolver` 實作 `Closeable` 介面，也可使用 `try-with-resources` 語法，而非明確叫用 `close()`.

#### 不相容代碼 {#non-compliant-code-4}

```java
public void dontDoThis(Session session) throws Exception {
  ResourceResolver resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object)session));
  // do some stuff with the resolver
}
```

#### 相容代碼 {#compliant-code-2}

```java
public void doThis(Session session) throws Exception {
  ResourceResolver resolver = null;
  try {
    resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object)session));
    // do something with the resolver
  } finally {
    if (resolver != null) {
      resolver.close();
    }
  }
}

public void orDoThis(Session session) throws Exception {
  try (ResourceResolver resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object) session))){
    // do something with the resolver
  }
}
```

### 請勿使用Sling Servlet路徑來註冊Servlet {#do-not-use-sling-servlet-paths-to-register-servlets}

* **金鑰**:CQRules:CQBP-75
* **類型**:代碼氣味
* **嚴重性**:主要
* **自**:2018.4.0版

如 [Sling檔案](http://sling.apache.org/documentation/the-sling-engine/servlets.html)不建議依路徑系結servlet。 路徑綁定的servlet無法使用標準JCR訪問控制，因此需要額外的安全嚴格性。 建議您不要使用路徑限制的servlet，而是在存放庫中建立節點，並依資源類型註冊servlet。

#### 不相容代碼 {#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### 捕獲的例外應記錄或擲回，而非兩者 {#caught-exceptions-should-be-logged-or-thrown-but-not-both}

* **金鑰**:CQRules:CQBP-44—CatchAndOtherLogOrThow
* **類型**:代碼氣味
* **嚴重性**:次要
* **自**:2018.4.0版

一般而言，例外只應記錄一次。 多次記錄例外可能會造成混淆，因為不清楚例外發生的次數。 導致此情況的最常見模式是記錄並擲回已捕捉的例外。

#### 不相容代碼 {#non-compliant-code-6}

```java
public void dontDoThis() throws Exception {
  try {
    someOperation();
  } catch (Exception e) {
    logger.error("something went wrong", e);
    throw e;
  }
}
```

#### 相容代碼 {#compliant-code-3}

```java
public void doThis() {
  try {
    someOperation();
  } catch (Exception e) {
    logger.error("something went wrong", e);
  }
}

public void orDoThis() throws MyCustomException {
  try {
    someOperation();
  } catch (Exception e) {
    throw new MyCustomException(e);
  }
}
```

### 避免Log陳述式後緊接著Throw陳述式 {#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

* **金鑰**:CQRules:CQBP-44—ConsellyLogAndThrow
* **類型**:代碼氣味
* **嚴重性**:次要
* **自**:2018.4.0版

另一種常見的避免模式是記錄訊息，然後立即擲回例外狀況。 這通常表示異常消息將在日誌檔案中重複。

#### 不相容代碼 {#non-compliant-code-7}

```java
public void dontDoThis() throws Exception {
  logger.error("something went wrong");
  throw new RuntimeException("something went wrong");
}
```

#### 相容代碼 {#compliant-code-4}

```java
public void doThis() throws Exception {
  throw new RuntimeException("something went wrong");
}
```

### 處理GET或HEAD請求時，請避免登入資訊 {#avoid-logging-at-info-when-handling-get-or-head-requests}

* **金鑰**:CQRules:CQBP-44—LogInfoInGetOrHeadRequests
* **類型**:代碼氣味
* **嚴重性**:次要

一般而言，INFO記錄層級應用來標定重要動作，且依預設，AEM會設定為在INFO層級或更高層級登入。 GET和HEAD方法只應是只讀操作，因此不構成重要行動。 響應GET或HEAD請求而以INFO級別記錄可能會產生顯著的日誌噪音，因此在日誌檔案中更難識別有用資訊。 處理GET或HEAD要求時的記錄應位於發生錯誤時的「警告」或「錯誤」層級，或位於「除錯」或「TRACE」層級（如果更深入的疑難排解資訊有幫助的話）。

>[!NOTE]
>
>這不適用於 `access.log`-type記錄。

#### 不相容代碼 {#non-compliant-code-8}

```java
public void doGet() throws Exception {
  logger.info("handling a request from the user");
}
```

#### 相容代碼 {#compliant-code-5}

```java
public void doGet() throws Exception {
  logger.debug("handling a request from the user.");
}
```

### 請勿將Exception.getMessage()用作記錄陳述式的第一個參數 {#do-not-use-exception-getmessage-as-the-first-parameter-of-a-logging-statement}

* **金鑰**:CQRules:CQBP-44—ExceptionGetMessageIsFirstLogParam
* **類型**:代碼氣味
* **嚴重性**:次要
* **自**:2018.4.0版

記錄訊息應提供關於應用程式中發生例外狀況的內容資訊，此為最佳作法。 雖然上下文也可以通過使用堆棧跟蹤來確定，但通常日誌消息將更容易讀取和理解。 因此，在記錄例外時，使用例外的訊息作為記錄訊息是不正確的作法。 例外消息將包含出錯的內容，而日誌消息應用於告知日誌讀取器發生異常時應用程式正在執行什麼操作。 系統仍會記錄例外訊息。 透過指定您自己的訊息，記錄檔將更容易理解。

#### 不相容代碼 {#non-compliant-code-9}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error(e.getMessage(), e);
  }
}
```

#### 相容代碼 {#compliant-code-6}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 登錄捕獲塊應處於「警告」或「錯誤」級別 {#logging-in-catch-blocks-should-be-at-the-warn-or-error-level}

* **金鑰**:CQRules:CQBP-44—WrongLogLevelInCatchBlock
* **類型**:代碼氣味
* **嚴重性**:次要
* **自**:2018.4.0版

如名稱所示，在特殊情況下，一律應使用Java例外。 因此，當捕獲到異常時，務必確保日誌消息記錄在適當的級別，即「警告」或「錯誤」。 這可確保這些訊息在記錄檔中正確顯示。

#### 不相容代碼 {#non-compliant-code-10}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.debug(e.getMessage(), e);
  }
}
```

#### 相容代碼 {#compliant-code-7}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 不將堆棧跟蹤打印到控制台 {#do-not-print-stack-traces-to-the-console}

* **金鑰**:CQRules:CQBP-44 - ExceptionPrintStackTrace
* **類型**:代碼氣味
* **嚴重性**:次要
* **自**:2018.4.0版

如前所述，了解日誌消息時，上下文至關重要。 使用 `Exception.printStackTrace()` 僅導致堆棧跟蹤輸出到標準錯誤流，從而丟失所有上下文。 此外，在諸如AEM的多線程應用程式中，如果使用此方法並行打印多個例外，則其堆棧跡線可能重疊，這會產生明顯的混淆。 只有記錄架構才應記錄例外。

#### 不相容代碼 {#non-compliant-code-11}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    e.printStackTrace();
  }
}
```

#### 相容代碼 {#compliant-code-8}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 不輸出到標準輸出或標準錯誤 {#do-not-output-to-standard-output-or-standard-error}

* **金鑰**:CQRules:CQBP-44—LogLevelConsolePrinters
* **類型**:代碼氣味
* **嚴重性**:次要
* **自**:2018.4.0版

登入AEM的作業一律應透過記錄架構(SLF4J)完成。 直接輸出到標準輸出或標準錯誤流會丟失由日誌記錄框架提供的結構和上下文資訊，在某些情況下，可能會導致效能問題。

#### 不相容代碼 {#non-compliant-code-12}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    System.err.println("Unable to do something");
  }
}
```

#### 相容代碼 {#compliant-code-9}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 避免硬式編碼/apps和/libs路徑 {#avoid-hardcoded-apps-and-libs-paths}

* **金鑰**:CQRules:CQBP-71
* **類型**:代碼氣味
* **嚴重性**:次要
* **自**:2018.4.0版

一般而言，開頭為的路徑 `/libs` 和 `/apps` 不應以硬式編碼撰寫，因為他們參考的路徑最常儲存為相對於Sling搜尋路徑的路徑，而此路徑設為 `/libs,/apps` 依預設。 使用絕對路徑可能會引入細微缺陷，這些缺陷只會在項目生命週期的稍後出現。

#### 不相容代碼 {#non-compliant-code-13}

```java
public boolean dontDoThis(Resource resource) {
  return resource.isResourceType("/libs/foundation/components/text");
}
```

#### 相容代碼 {#compliant-code-10}

```java
public void doThis(Resource resource) {
  return resource.isResourceType("foundation/components/text");
}
```

### 不應使用Sling排程器 {#sonarqube-sling-scheduler}

* **金鑰**:CQRules:AMSCORE-554
* **類型**:代碼氣味/Cloud Service相容性
* **嚴重性**:次要
* **自**:2020.5.0版

Sling排程器不得用於需要保證執行的工作。 Sling排程作業可確保執行，且更適合叢集和非叢集環境。

請參閱 [Apache Sling事件和作業處理](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html) 以進一步了解在叢集環境中如何處理Sling作業。

### AEM已棄用的API不應使用 {#sonarqube-aem-deprecated}

* **金鑰**:AMSCORE-553
* **類型**:代碼氣味/Cloud Service相容性
* **嚴重性**:次要
* **自**:2020.5.0版

AEM API表面不斷修訂，以識別不建議使用且因此視為已過時的API。

在許多情況下，這些API會使用標準Java來取代 `@Deprecated` 注釋，因此，由 `squid:CallToDeprecatedMethod`.

不過，在AEM的內容中，API有時會遭到取代，但在其他內容中，API可能不會遭到取代。 此規則可識別此第二類。


## OakPAL內容規則 {#oakpal-rules}

以下章節詳細說明由Cloud Manager執行的OakPAL檢查。

>[!NOTE]
>
>OakPAL為架構，可使用獨立Oak存放庫來驗證內容套件。 由AEM合作夥伴及2019年AEM Rockstar北美獎得主所開發。

### 客戶不應實作或擴充@ProviderType附註的產品API {#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}

* **金鑰**:CQBP-84
* **類型**:錯誤
* **嚴重性**:關鍵
* **自**:2018.7.0版

AEM API包含Java介面和類別，這些介面和類別僅能由自訂程式碼使用，但不能實作。例如，介面 `com.day.cq.wcm.api.Page` 僅由 AEM實作。

將新方法添加到這些介面時，這些附加方法不會影響使用這些介面的現有代碼，因此，在這些介面中添加新方法會被視為向後相容。但是，如果自訂程 式碼實作 其中一個介面，該自訂程式碼會給客戶帶來向後相容性風險。

僅打算由AEM實現的介面和類會用注釋 `org.osgi.annotation.versioning.ProviderType` 或在某些情況下類似的舊式註解 `aQute.bnd.annotation.ProviderType`. 此規則可識別實作此類介面或由自訂程式碼擴充類別的情況。

#### 不相容代碼 {#non-compliant-code-3}

```java
import com.day.cq.wcm.api.Page;

public class DontDoThis implements Page {
// implementation here
}
```

### 自訂Lucene Oak索引必須有Tika設定 {#oakpal-indextikanode}

* **金鑰**:IndexTikaNode
* **類型**:錯誤
* **嚴重性**:封鎖程式
* **自**:2021.8.0

多個現成可用的AEM Oak索引包含tika設定，而這些索引的自訂必須包含tika設定。 此規則會檢查 `damAssetLucene`, `lucene`，和 `graphqlConfig` 索引並引發問題(若 `tika`  節點遺失，或 `tika` 節點缺少名為的子節點 `config.xml`.

請參閱 [索引檔案](/help/operations/indexing.md#preparing-the-new-index-definition) 有關自定義索引定義的詳細資訊。

#### 不相容代碼 {#non-compliant-code-indextikanode}

```text
+ oak:index
    + damAssetLucene-1-custom
      - async: [async]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - reindex: false
      - tags: [visualSimilaritySearch]
      - type: lucene
```

#### 相容代碼 {#compliant-code-indextikanode}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - reindex: false
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### 自訂Lucene Oak索引不得同步 {#oakpal-indexasync}

* **金鑰**:IndexAsyncProperty
* **類型**:錯誤
* **嚴重性**:封鎖程式
* **自**:2021.8.0

類型的Oak索引 `lucene` 必須一律以非同步方式編列索引。 如果不這樣做，可能導致系統不穩定。 有關lucene索引結構的詳細資訊，請參閱 [Oak檔案。](https://jackrabbit.apache.org/oak/docs/query/lucene.html#index-definition)

#### 不相容代碼 {#non-compliant-code-indexasync}

```text
+ oak:index
    + damAssetLucene-1-custom
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - reindex: false
      - type: lucene
      - reindex: false
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

#### 相容代碼 {#compliant-code-indexasync}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - reindex: false
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### 自訂DAM資產Lucene Oak索引已正確建構  {#oakpal-damAssetLucene-sanity-check}

* **金鑰**:IndexDamAssetLucene
* **類型**:錯誤
* **嚴重性**:封鎖程式
* **自**:2021.6.0

為了讓資產搜尋在AEM Assets中正常運作，請自訂 `damAssetLucene` Oak索引必須遵循本索引專屬的准則集。 此規則檢查索引定義必須具有名為的多值屬性 `tags` 其中包含值 `visualSimilaritySearch`.

#### 不相容代碼 {#non-compliant-code-damAssetLucene}

```text
+ oak:index
    + damAssetLucene-1-custom
      - async: [async, nrt]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - reindex: false
      - type: lucene
      + tika
        + config.xml
```

#### 相容代碼 {#compliant-code-damAssetLucene}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async, nrt]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - reindex: false
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### 客戶包不應在/libs下建立或修改節點 {#oakpal-customer-package}

* **金鑰**:UnpandedPath
* **類型**:錯誤
* **嚴重性**:關鍵
* **自**:2019.6.0版

長期以來，最佳做法是 `/libs` 客戶應將AEM內容存放庫中的內容樹視為唯讀。 修改下的節點和屬性 `/libs` 會造成重大和微幅更新的重大風險。 修改 `/libs` 只能通過官方渠道進行Adobe。

### 套件不應包含重複的OSGi設定 {#oakpal-package-osgi}

* **金鑰**:DuplicateOsgiConfigurations
* **類型**:錯誤
* **嚴重性**:主要
* **自**:2019.6.0版

複雜專案中發生的常見問題是多次設定相同的OSGi元件。 這會造成哪個設定適用的模糊情況。 此規則「執行模式感知」，因為它只會識別在同一執行模式或執行模式組合中多次設定相同元件的問題。

>[!NOTE]
>
>此規則會產生多個套件中定義相同配置（在相同路徑）的問題，包括內建套件的整體清單中複製相同套件的情況。
>
>例如，如果組建產生名為 `com.myco:com.myco.ui.apps` 和 `com.myco:com.myco.all` where `com.myco:com.myco.all` 內嵌 `com.myco:com.myco.ui.apps`，則 `com.myco:com.myco.ui.apps` 會報告為重複項目。
>
>這通常是不遵循 [內容套件結構指南。](/help/implementing/developing/introduction/aem-project-content-package-structure.md). 在此特定範例中，套件 `com.myco:com.myco.ui.apps` 缺少 `<cloudManagerTarget>none</cloudManagerTarget>` 屬性。

#### 不相容代碼 {#non-compliant-code-osgi}

```text
+ apps
  + projectA
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
  + projectB
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

#### 相容代碼 {#compliant-code-osgi}

```text
+ apps
  + shared-config
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

### 配置和安裝資料夾應僅包含OSGi節點 {#oakpal-config-install}

* **金鑰**:ConfigAndInstallShouldOnlyContainOsgiNodes
* **類型**:錯誤
* **嚴重性**:主要
* **自**:2019.6.0版

基於安全原因，包含 `/config/` 和 `/install/` 只有AEM中的管理使用者才能閱讀，且應僅用於OSGi設定和OSGi套件組合。 將其他類型的內容置於包含這些區段的路徑之下，會導致應用程式行為，這會無意中在管理使用者和非管理使用者之間有所差異。

常見的問題是使用名為 `config` 在元件對話方塊內，或指定用於內嵌編輯的rtf編輯器設定時。 要解決此問題，應將違規節點重新命名為符合規範的名稱。 對於RTF編輯器設定，請使用 `configPath` 屬性 `cq:inplaceEditing` 節點，指定新位置。

#### 不相容代碼 {#non-compliant-code-config-install}

```text
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    + config [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

#### 相容代碼 {#compliant-code-config-install}

```text
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    ./configPath = inplaceEditingConfig (String)
    + inplaceEditingConfig [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

### 套件不應重疊 {#oakpal-no-overlap}

* **金鑰**:封裝重疊
* **類型**:錯誤
* **嚴重性**:主要
* **自**:2019.6.0版

類似於 [套件不應包含重複的OSGi設定規則，](#oakpal-package-osgi) 這是複雜專案中常見的問題，其中同一個節點路徑是由多個不同的內容套件所寫入。 雖然可使用內容套件相依性來確保結果一致，但最好避免完全重疊。

### 預設編寫模式不應為傳統UI {#oakpal-default-authoring}

* **金鑰**:ClassicUIAuthoringMode
* **類型**:代碼氣味/Cloud Service相容性
* **嚴重性**:次要
* **自**:2020.5.0版

OSGi設定 `com.day.cq.wcm.core.impl.AuthoringUIModeServiceImpl` 定義AEM中的預設製作模式。 因為 [傳統UI自AEM 6.4起即已過時，](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/deprecated-removed-features.html) 現在當將預設製作模式設為傳統UI時，會發生問題。

### 具有對話方塊的元件應具有觸控式UI對話方塊 {#oakpal-components-dialogs}

* **金鑰**:ComponentWithOnlyClassicUIDialog
* **類型**:代碼氣味/Cloud Service相容性
* **嚴重性**:次要
* **自**:2020.5.0版

具有傳統UI對話方塊的AEM元件應一律具有對應的觸控式UI對話方塊，以提供最佳的製作體驗，並與不支援傳統UI的Cloud Service部署模型相容。 此規則會驗證下列情況：

* 具有傳統UI對話方塊的元件(即 `dialog` 子節點)必須具有對應的觸控式UI對話方塊(即 `cq:dialog` 子節點)。
* 具有傳統UI設計對話方塊的元件(即 `design_dialog` 節點)必須具有對應的觸控式UI設計對話方塊(即 `cq:design_dialog` 子節點)。
* 元件具有傳統UI對話方塊和傳統UI設計對話方塊，必須同時具有對應的觸控式UI對話方塊和對應的觸控式UI設計對話方塊。

AEM現代化工具檔案提供如何將元件從傳統UI轉換為觸控式UI的檔案和工具。 請參閱 [AEM現代化工具檔案](https://opensource.adobe.com/aem-modernize-tools/) 以取得更多詳細資訊。

### 套件不應混用可變和不可變內容 {#oakpal-packages-immutable}

* **金鑰**:ImmutableMutableMixedPackage
* **類型**:代碼氣味/Cloud Service相容性
* **嚴重性**:次要
* **自**:2020.5.0版

為了與Cloud Service部署模型相容，單個內容包必須包含儲存庫不可變區域(即 `/apps` 和 `/libs`)或可變區域(即 `/apps` 或 `/libs`)，但不能兩者兼而有之。 例如，包含兩者的套件 `/apps/myco/components/text and /etc/clientlibs/myco` 與Cloud Service不相容，且會造成問題回報。

>[!NOTE]
>
>規則 [客戶包不應在/libs下建立或修改節點](#oakpal-customer-package) 一律適用。

請參閱 [AEM專案結構](/help/implementing/developing/introduction/aem-project-content-package-structure.md) 以取得更多詳細資訊。

### 不應使用反向複製代理 {#oakpal-reverse-replication}

* **金鑰**:反向複製
* **類型**:代碼氣味/Cloud Service相容性
* **嚴重性**:次要
* **自**:2020.5.0版

如AEM as a Cloud Service的一部分所述，Cloud Service部署中不支援反向復寫 [發行說明。](/help/release-notes/aem-cloud-changes.md#replication-agents)

使用反向復寫的Adobe應聯絡其他解決方案的客戶。

### 已啟用代理的客戶端庫中所包含的資源應位於名為「資源」的資料夾中 {#oakpal-resources-proxy}

* **金鑰**:ClientlibProxyResource
* **類型**:錯誤
* **嚴重性**:次要
* **自**:2021.2.0版

AEM用戶端程式庫可包含靜態資源，例如影像和字型。 如文檔所述 [使用前置處理器，](/help/implementing/developing/introduction/clientlibs.md#using-preprocessors) 使用代理客戶端庫時，這些靜態資源必須包含在名為的子資料夾中 `resources` 以便在發佈例項上有效參考。

#### 不相容代碼 {#non-compliant-proxy-enabled}

```text
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + images
        + myimage.jpg
```

#### 相容代碼 {#compliant-proxy-enabled}

```tet
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + resources
        + myimage.jpg
```

### Cloud Service不相容的工作流程的使用 {#oakpal-usage-cloud-service}

* **金鑰**:CloudServiceIncomplatedWorkflowProcess
* **類型**:錯誤
* **嚴重性**:主要
* **自**:2021.2.0版

隨著移轉至資產微服務以在AEM as a Cloud Service進行資產處理，內部部署和AEM AMS版本中使用的數個工作流程程式，已變得不受支援或不必要。

移轉工具，位於 [AEM Assetsas a Cloud ServiceGitHub存放庫](https://github.com/adobe/aem-cloud-migration) 可在移轉至AEM as a Cloud Service時用來更新工作流程模型。

### 不建議使用靜態範本，而改用可編輯的範本 {#oakpal-static-template}

* **金鑰**:StaticTemplateUsage
* **類型**:代碼氣味
* **嚴重性**:次要
* **自**:2021.2.0版

雖然靜態範本的使用在AEM專案中向來很常見，但強烈建議使用可編輯的範本，因為這些範本可提供最大的彈性，並支援靜態範本中未出現的其他功能。 可在文檔中找到更多資訊 [頁面範本。](/help/implementing/developing/components/templates.md)

從靜態範本移轉至可編輯的範本，可透過 [AEM現代化工具。](https://opensource.adobe.com/aem-modernize-tools/)

### 不建議使用舊版基礎元件 {#oakpal-usage-legacy}

* **金鑰**:LegacyFoundationComponentUsage
* **類型**:代碼氣味
* **嚴重性**:次要
* **自**:2021.2.0版

舊版Foundation元件(即 `/libs/foundation`)已 [已棄用於數個AEM版本](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/deprecated-removed-features.html) 以支援核心元件。 不建議您以「基礎元件」作為自訂元件的基礎（不論是透過覆蓋或繼承），且應轉換為對應的核心元件。

此轉換可由 [AEM現代化工具。](https://opensource.adobe.com/aem-modernize-tools/)

### 僅應使用支援的運行模式名稱和順序 {#oakpal-supported-runmodes}

* **金鑰**:支援的運行模式
* **類型**:代碼氣味
* **嚴重性**:次要
* **自**:2021.2.0版

AEMas a Cloud Service會針對執行模式名稱強制執行嚴格的命名原則，並針對這些執行模式執行嚴格的排序。 可在文檔中找到支援的運行模式清單 [部署至AEMas a Cloud Service](/help/implementing/deploying/overview.md#runmodes) 而任何偏離這一點的行為都會被認定為問題。

### 自訂搜尋索引定義節點必須是/oak:index的直接子項 {#oakpal-custom-search}

* **金鑰**:OakIndexLocation
* **類型**:代碼氣味
* **嚴重性**:次要
* **自**:2021.2.0版

AEM as a Cloud Service要求自訂搜尋索引定義（即類型的節點） `oak:QueryIndexDefinition`)是直接的子節點 `/oak:index`. 其他位置中的索引必須移動以與AEMas a Cloud Service相容。 有關搜索索引的更多資訊，請參見文檔 [內容搜尋和索引。](/help/operations/indexing.md)

### 自定義搜索索引定義節點必須具有2的compat版本 {#oakpal-custom-search-compatVersion}

* **金鑰**:IndexCompatVersion
* **類型**:代碼氣味
* **嚴重性**:次要
* **自**:2021.2.0版

AEM as a Cloud Service要求自訂搜尋索引定義（即類型的節點） `oak:QueryIndexDefinition`)必須有 `compatVersion` 屬性設定為 `2`. AEM as a Cloud Service不支援任何其他值。 有關搜索索引的更多資訊，請參見 [內容搜尋和索引。](/help/operations/indexing.md)

### 自定義搜索索引定義節點的子節點必須為Nt:Unstructured類型 {#oakpal-descendent-nodes}

* **金鑰**:IndexDescendationNodeType
* **類型**:代碼氣味
* **嚴重性**:次要
* **自**:2021.2.0版

當自訂搜尋索引定義節點具有無序的子節點時，可能會發生難以疑難排解的問題。 為避免此情況，建議 `oak:QueryIndexDefinition` 節點類型 `nt:unstructured`.

### 自定義搜索索引定義節點必須包含一個名為indexRules的子節點，該子節點具有子節點 {#oakpal-custom-search-index}

* **金鑰**:IndexRulesNode
* **類型**:代碼氣味
* **嚴重性**:次要
* **自**:2021.2.0版

正確定義的自定義搜索索引定義節點必須包含名為的子節點 `indexRules` 而這又必須至少有一個孩子。 如需詳細資訊，請參閱 [Oak檔案。](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

### 自定義搜索索引定義節點必須遵循命名慣例 {#oakpal-custom-search-definitions}

* **金鑰**:IndexName
* **類型**:代碼氣味
* **嚴重性**:次要
* **自**:2021.2.0版

AEM as a Cloud Service要求自訂搜尋索引定義（即，類型的節點） `oak:QueryIndexDefinition`)必須依照檔案中所述的特定模式命名 [內容搜尋和索引。](/help/operations/indexing.md)

### 自定義搜索索引定義節點必須使用索引類型lucene  {#oakpal-index-type-lucene}

* **金鑰**:IndexType
* **類型**:錯誤
* **嚴重性**:封鎖程式
* **自**:2021.2.0版（2021.8.0中更改了類型和嚴重性）

AEM as a Cloud Service要求自訂搜尋索引定義（即類型的節點） `oak:QueryIndexDefinition`)有 `type` 值設為的屬性 `lucene`. 使用舊版索引類型建立索引之前，必須先更新，才能移轉至AEMas a Cloud Service。 查看文檔 [內容搜尋與索引](/help/operations/indexing.md#how-to-use) 以取得更多資訊。

### 自定義搜索索引定義節點不得包含名為Seed的屬性 {#oakpal-property-name-seed}

* **金鑰**:IndexSeedProperty
* **類型**:代碼氣味
* **嚴重性**:次要
* **自**:2021.2.0版

AEMas a Cloud Service禁止自訂搜尋索引定義（即，類型的節點） `oak:QueryIndexDefinition`)，從包含名為 `seed`. 使用此屬性建立索引必須先更新，才能移轉至AEMas a Cloud Service。 請參閱檔案 [內容搜尋與索引](/help/operations/indexing.md#how-to-use) 以取得更多資訊。

### 自定義搜索索引定義節點不能包含名為重新索引的屬性 {#oakpal-reindex-property}

* **金鑰**:IndexReindexProperty
* **類型**:代碼氣味
* **嚴重性**:次要
* **自**:2021.2.0版

AEMas a Cloud Service禁止自訂搜尋索引定義（即，類型的節點） `oak:QueryIndexDefinition`)，從包含名為 `reindex`. 使用此屬性建立索引必須先更新，才能移轉至AEMas a Cloud Service。 請參閱檔案 [內容搜尋與索引](/help/operations/indexing.md#how-to-use) 以取得更多資訊。
