---
title: 自訂程式碼品質規則
description: 本頁描述了作為[代碼質量測試的一部分，由Cloud Manager執行的自定義代碼質量規則。 它們基於工程部門的最佳AEM實踐。
exl-id: f40e5774-c76b-4c84-9d14-8e40ee6b775b
source-git-commit: 4567581eb02c928f1493defdab667cc713fc222a
workflow-type: tm+mt
source-wordcount: '3464'
ht-degree: 3%

---

# 自訂程式碼品質規則 {#custom-code-quality-rules}

>[!CONTEXTUALHELP]
>
>id="aemcloud_nonbpa_customcodequalityrules"
>title="Custom Code Quality Rules"
>abstract="This page describes the custom code quality rules executed by Cloud Manager as part of code quality testing. They are based on best practices from AEM Engineering."

本頁介紹Cloud Manager作為元件執行的自定義代碼質量規則 [代碼質量測試。](/help/implementing/cloud-manager/code-quality-testing.md) 它們基於工程部門的最佳AEM實踐。

>[!NOTE]
此處提供的代碼示例僅供說明之用。 看聲納隊 [概念文檔](https://docs.sonarqube.org/7.4/user-guide/concepts/) 瞭解聲納庫比的概念和質量規則。

## 《聲納量子規則》 {#sonarqube-rules}

以下部分詳細介紹了雲管理器執行的SonarQube規則。

### 不要使用潛在的危險函式 {#do-not-use-potentially-dangerous-functions}

* **鍵**:CQRules:CWE-676
* **類型**:漏洞
* **嚴重性**:主
* **自**:2018.4.0版

方法 `Thread.stop()` 和 `Thread.interrupt()` 會產生難以複製的問題，在某些情況下，還會產生安全漏洞。 它們的使用應受到嚴密監控和驗證。總的來說，傳遞資訊是實現類似目標的更安全的方式。

#### 不符合代碼 {#non-compliant-code}

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

#### 符合代碼 {#compliant-code}

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

### 不要使用可能受外部控制的格式字串 {#do-not-use-format-strings-which-may-be-externally-controlled}

* **鍵**:CQRules:CWE-134
* **類型**:漏洞
* **嚴重性**:主
* **自**:2018.4.0版

使用來自外部源（如請求參數或用戶生成的內容）的格式字串可以使應用程式暴露於拒絕服務攻擊。 在某些情況下，格式字串可能受外部控制，但僅允許來自受信任源。

#### 不符合代碼 {#non-compliant-code-1}

```java
protected void doPost(SlingHttpServletRequest request, SlingHttpServletResponse response) {
  String messageFormat = request.getParameter("messageFormat");
  request.getResource().getValueMap().put("some property", String.format(messageFormat, "some text"));
  response.sendStatus(HttpServletResponse.SC_OK);
}
```

### HTTP請求應始終具有套接字和連接超時 {#http-requests-should-always-have-socket-and-connect-timeouts}

* **鍵**:CQRules:ConnectionTimeoutMechanism
* **類型**:蟲
* **嚴重性**:關鍵
* **自**:2018.6.0版

當從應用程式內部執行HTTP請AEM求時，確保配置適當的超時以避免不必要的線程消耗至關重要。 很遺憾，兩個Java的預設HTTP客戶端的預設行為(`java.net.HttpUrlConnection`)，並且常用的Apache HTTP元件客戶端永不超時，因此必須顯式設定超時。 此外，作為最佳做法，這些超時應不超過60秒。

#### 不符合代碼 {#non-compliant-code-2}

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

#### 符合代碼 {#compliant-code-1}

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

* **鍵**:CQRules:CQBP-72
* **類型**:代碼氣味
* **嚴重性**:主
* **自**:2018.4.0版

`ResourceResolver` 從 `ResourceResolverFactory` 使用系統資源。 儘管已制定措施，以在 `ResourceResolver` 不再使用，更高效地顯式關閉任何已開啟的 `ResourceResolver` 通過調用 `close()` 的雙曲餘切值。

一個比較常見的誤解是 `ResourceResolver` 不應顯式關閉使用現有JCR會話建立的對象，否則將關閉基礎JCR會話。 事實並非如此。 不管 `ResourceResolver` 開啟，在不再使用時應關閉。 自 `ResourceResolver` 實現 `Closeable` 介面，也可以使用 `try-with-resources` 語法而不是顯式調用 `close()`。

#### 不符合代碼 {#non-compliant-code-4}

```java
public void dontDoThis(Session session) throws Exception {
  ResourceResolver resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object)session));
  // do some stuff with the resolver
}
```

#### 符合代碼 {#compliant-code-2}

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

### 不使用Sling Servlet路徑註冊Servlet {#do-not-use-sling-servlet-paths-to-register-servlets}

* **鍵**:CQRules:CQBP-75
* **類型**:代碼氣味
* **嚴重性**:主
* **自**:2018.4.0版

如 [Sling文檔](http://sling.apache.org/documentation/the-sling-engine/servlets.html)不鼓勵按路徑綁定servlet。 路徑綁定的Servlet不能使用標準JCR訪問控制，因此需要額外的安全嚴格性。 建議不要使用路徑綁定的Servlet，而是在儲存庫中建立節點並按資源類型註冊Servlet。

#### 不符合代碼 {#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### 捕獲到的異常應記錄或拋出，而不是同時記錄或拋出 {#caught-exceptions-should-be-logged-or-thrown-but-not-both}

* **鍵**:CQRules:CQBP-44 - CatchAndOitherLogOrThrow
* **類型**:代碼氣味
* **嚴重性**:小
* **自**:2018.4.0版

通常，應只記錄一次異常。 多次記錄異常可能會造成混亂，因為不清楚發生異常的次數。 導致這種情況的最常見模式是記錄並引發捕獲到的異常。

#### 不符合代碼 {#non-compliant-code-6}

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

#### 符合代碼 {#compliant-code-3}

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

### 避免日誌語句後跟Throw語句 {#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

* **鍵**:CQRules:CQBP-44 —ConcentiusLogAndThrow
* **類型**:代碼氣味
* **嚴重性**:小
* **自**:2018.4.0版

另一個需要避免的常見模式是記錄消息，然後立即引發異常。 這通常表示異常消息將在日誌檔案中重複。

#### 不符合代碼 {#non-compliant-code-7}

```java
public void dontDoThis() throws Exception {
  logger.error("something went wrong");
  throw new RuntimeException("something went wrong");
}
```

#### 符合代碼 {#compliant-code-4}

```java
public void doThis() throws Exception {
  throw new RuntimeException("something went wrong");
}
```

### 在處理GET或HEAD請求時避免在INFO處記錄 {#avoid-logging-at-info-when-handling-get-or-head-requests}

* **鍵**:CQRules:CQBP-44 - LogInfoInGetOrHeadRequests
* **類型**:代碼氣味
* **嚴重性**:小

通常，應使用INFO日誌級別來標定重要操作，並且預設AEM配置為在INFO級別或更高級別登錄。 GET和HEAD方法只應是只讀操作，因此不構成重要行動。 響應GET或HEAD請求而以INFO級別登錄可能會產生嚴重的日誌噪音，從而使識別日誌檔案中的有用資訊變得更加困難。 處理GET或HEAD請求時的日誌記錄應位於出錯時的「警告」或「錯誤」級別，或位於「調試」或「TRACE」級別（如果更深入的故障排除資訊有幫助）。

>[!NOTE]
這不適用於 `access.log`-type每個請求的日誌記錄。

#### 不符合代碼 {#non-compliant-code-8}

```java
public void doGet() throws Exception {
  logger.info("handling a request from the user");
}
```

#### 符合代碼 {#compliant-code-5}

```java
public void doGet() throws Exception {
  logger.debug("handling a request from the user.");
}
```

### 不將Exception.getMessage()用作Logging語句的第一個參數 {#do-not-use-exception-getmessage-as-the-first-parameter-of-a-logging-statement}

* **鍵**:CQRules:CQBP-44 - ExceptionGetMessageIsFirstLogParam
* **類型**:代碼氣味
* **嚴重性**:小
* **自**:2018.4.0版

最佳做法是，日誌消息應提供有關應用程式中發生異常的位置的上下文資訊。 雖然上下文也可以通過使用堆棧跟蹤來確定，但通常日誌消息將更容易讀取和理解。 因此，在記錄異常時，將異常的消息用作日誌消息是一種錯誤的做法。 異常消息將包含出錯的內容，而日誌消息應用於告訴日誌讀取器在發生異常時應用程式正在執行什麼操作。 仍將記錄異常消息。 通過指定您自己的消息，日誌將更容易理解。

#### 不符合代碼 {#non-compliant-code-9}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error(e.getMessage(), e);
  }
}
```

#### 符合代碼 {#compliant-code-6}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 登錄捕獲塊應處於WARN或ERROR級別 {#logging-in-catch-blocks-should-be-at-the-warn-or-error-level}

* **鍵**:CQRules:CQBP-44 - WrongLogLevelInCatchBlock
* **類型**:代碼氣味
* **嚴重性**:小
* **自**:2018.4.0版

如名稱所示，Java例外應始終用於特殊情況。 因此，當捕獲到異常時，必須確保日誌消息記錄在適當級別，即WARN或ERROR。 這可確保這些消息在日誌中正確顯示。

#### 不符合代碼 {#non-compliant-code-10}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.debug(e.getMessage(), e);
  }
}
```

#### 符合代碼 {#compliant-code-7}

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

* **鍵**:CQRules:CQBP-44 - ExceptionPrintStackTrace
* **類型**:代碼氣味
* **嚴重性**:小
* **自**:2018.4.0版

如前所述，上下文在理解日誌消息時至關重要。 使用 `Exception.printStackTrace()` 僅使堆棧跟蹤輸出到標準錯誤流，從而丟失所有上下文。 此外，在多線程應用中，AEM如果使用該方法並行打印多個異常，則其堆棧軌跡可能重疊，從而產生明顯的混淆。 應僅通過日誌記錄框架記錄異常。

#### 不符合代碼 {#non-compliant-code-11}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    e.printStackTrace();
  }
}
```

#### 符合代碼 {#compliant-code-8}

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

* **鍵**:CQRules:CQBP-44 - LogLevelConsolePrinters
* **類型**:代碼氣味
* **嚴重性**:小
* **自**:2018.4.0版

登錄AEM應始終通過日誌框架(SLF4J)完成。 直接輸出到標準輸出或標準錯誤流會丟失由日誌記錄框架提供的結構和上下文資訊，並且在某些情況下可能導致效能問題。

#### 不符合代碼 {#non-compliant-code-12}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    System.err.println("Unable to do something");
  }
}
```

#### 符合代碼 {#compliant-code-9}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 避免硬編碼/apps和/libs路徑 {#avoid-hardcoded-apps-and-libs-paths}

* **鍵**:CQRules:CQBP-71
* **類型**:代碼氣味
* **嚴重性**:小
* **自**:2018.4.0版

通常，以 `/libs` 和 `/apps` 不應硬編碼，因為它們引用的路徑通常儲存為相對於Sling搜索路徑的路徑，該路徑設定為 `/libs,/apps` 預設值。 使用絕對路徑可能會引入一些細微的缺陷，這些缺陷只會在項目生命週期的後期出現。

#### 不符合代碼 {#non-compliant-code-13}

```java
public boolean dontDoThis(Resource resource) {
  return resource.isResourceType("/libs/foundation/components/text");
}
```

#### 符合代碼 {#compliant-code-10}

```java
public void doThis(Resource resource) {
  return resource.isResourceType("foundation/components/text");
}
```

### 不應使用Sling調度程式 {#sonarqube-sling-scheduler}

* **鍵**:CQRules:AMSCORE-554
* **類型**:代碼氣味/Cloud Service相容性
* **嚴重性**:小
* **自**:2020.5.0版

Sling Scheduler不能用於需要保證執行的任務。 Sling Scheduled Jobs可確保執行，並更適合群集和非群集環境。

請參閱 [Apache Sling事件和作業處理](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html) 瞭解有關如何在群集環境中處理Sling Jobs的詳細資訊。

### 不AEM應使用棄用的API {#sonarqube-aem-deprecated}

* **鍵**:AMSCORE-553
* **類型**:代碼氣味/Cloud Service相容性
* **嚴重性**:小
* **自**:2020.5.0版

APIAEM表面處於常數修訂下，以標識不鼓勵使用的API，因此被視為已棄用。

在許多情況下，這些API使用標準Java被棄用 `@Deprecated` 注釋，因此，由 `squid:CallToDeprecatedMethod`。

但是，在某些情況下， API在上下文中被棄用，AEM但在其他上下文中可能不被棄用。 此規則標識此第二類。


## OakPAL內容規則 {#oakpal-rules}

以下部分詳細介紹了Cloud Manager執行的OakPAL檢查。

>[!NOTE]
OakPAL是一個框架，它使用獨立的Oak儲存庫來驗證內容包。 該獎由一名合AEM伙人和2019年羅剋星北美獎AEM得主開發。

### 客戶不應實施或擴展@ProviderType注釋的產品API {#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}

* **鍵**:CQBP-84
* **類型**:蟲
* **嚴重性**:關鍵
* **自**:2018.7.0版

AEM API包含Java介面和類別，這些介面和類別僅能由自訂程式碼使用，但不能實作。例如，介面 `com.day.cq.wcm.api.Page` 僅由 AEM實作。

將新方法添加到這些介面時，這些附加方法不會影響使用這些介面的現有代碼，因此，在這些介面中添加新方法會被視為向後相容。但是，如果自訂程 式碼實作 其中一個介面，該自訂程式碼會給客戶帶來向後相容性風險。

僅由實現的介面和類用AEM於注釋 `org.osgi.annotation.versioning.ProviderType` 或在某些情況下類似的舊式批注 `aQute.bnd.annotation.ProviderType`。 此規則標識實現此類介面或通過自定義代碼擴展類的情況。

#### 不符合代碼 {#non-compliant-code-3}

```java
import com.day.cq.wcm.api.Page;

public class DontDoThis implements Page {
// implementation here
}
```

### 自定義Lucene Oak索引必須具有Tika配置 {#oakpal-indextikanode}

* **鍵**:IndexTikaNode
* **類型**:蟲
* **嚴重性**:阻止程式
* **自**:2021.8.0

多個現成Oak索引包AEM括tika配置，這些索引的定製必須包括tika配置。 此規則檢查 `damAssetLucene`。 `lucene`, `graphqlConfig` 索引並引發問題 `tika`  節點丟失或 `tika` 節點缺少名為的子節點 `config.xml`。

請參閱 [索引文檔](/help/operations/indexing.md#preparing-the-new-index-definition) 的子菜單。

#### 不符合代碼 {#non-compliant-code-indextikanode}

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

#### 符合代碼 {#compliant-code-indextikanode}

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

### 自定義Lucene Oak索引不能是同步的 {#oakpal-indexasync}

* **鍵**:IndexAsyncProperty
* **類型**:蟲
* **嚴重性**:阻止程式
* **自**:2021.8.0

類型的Oak索引 `lucene` 必須始終非同步索引。 如果不這樣做，可能會導致系統不穩定。 有關lucene索引結構的詳細資訊，請參閱 [橡木文檔。](https://jackrabbit.apache.org/oak/docs/query/lucene.html#index-definition)

#### 不符合代碼 {#non-compliant-code-indexasync}

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

#### 符合代碼 {#compliant-code-indexasync}

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

### 自定義DAM資產Lucene Oak索引結構正確  {#oakpal-damAssetLucene-sanity-check}

* **鍵**:IndexDamAssetLucene
* **類型**:蟲
* **嚴重性**:阻止程式
* **自**:2021.6.0

為使資產搜索在AEM Assets正常工作， `damAssetLucene` Oak索引必須遵循一組特定於此索引的准則。 此規則檢查索引定義是否必須具有名為 `tags` 包含值 `visualSimilaritySearch`。

#### 不符合代碼 {#non-compliant-code-damAssetLucene}

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

#### 符合代碼 {#compliant-code-damAssetLucene}

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

* **鍵**:禁用路徑
* **類型**:蟲
* **嚴重性**:關鍵
* **自**:2019.6.0版

長期以來，我們一直在 `/libs` 內容儲存庫AEM中的內容樹應被客戶視為只讀。 修改下的節點和屬性 `/libs` 給主要和次要更新帶來巨大風險。 修改 `/libs` 只能通過官方渠道進行Adobe。

### 包不應包含重複的OSGi配置 {#oakpal-package-osgi}

* **鍵**:重複Osgi配置
* **類型**:蟲
* **嚴重性**:主
* **自**:2019.6.0版

在複雜項目上出現的一個常見問題是多次配置同一OSGi元件。 這會導致對哪些配置適用產生模糊性。 此規則是「運行模式感知」，因為它只標識在同一運行模式或運行模式組合中多次配置同一元件的問題。

>[!NOTE]
此規則將產生在多個包中定義相同配置（在同一路徑上）的問題，包括在生成的包的總清單中複製相同包的情況。
例如，如果生成生成名為 `com.myco:com.myco.ui.apps` 和 `com.myco:com.myco.all` 何處 `com.myco:com.myco.all` 床 `com.myco:com.myco.ui.apps`，然後是 `com.myco:com.myco.ui.apps` 將被報告為重複項。
這通常是不遵守 [內容包結構指南。](/help/implementing/developing/introduction/aem-project-content-package-structure.md). 在此特定示例中， `com.myco:com.myco.ui.apps` 缺少 `<cloudManagerTarget>none</cloudManagerTarget>` 屬性。

#### 不符合代碼 {#non-compliant-code-osgi}

```text
+ apps
  + projectA
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
  + projectB
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

#### 符合代碼 {#compliant-code-osgi}

```text
+ apps
  + shared-config
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

### 配置和安裝資料夾應僅包含OSGi節點 {#oakpal-config-install}

* **鍵**:ConfigAndInstallHouseOnlyContainOsgiNodes
* **類型**:蟲
* **嚴重性**:主
* **自**:2019.6.0版

出於安全原因，包含 `/config/` 和 `/install/` 只能由中的管理用戶AEM讀取，並且只能用於OSGi配置和OSGi捆綁包。 將其他類型的內容放置在包含這些段的路徑下會導致應用程式行為在管理用戶和非管理用戶之間無意中發生變化。

一個常見問題是使用名為 `config` 在元件對話框中或指定用於內聯編輯的富格文本編輯器配置時。 要解決此問題，應將違規節點更名為相容名稱。 對於RTF編輯器配置，請使用 `configPath` 屬性 `cq:inplaceEditing` 的子菜單。

#### 不符合代碼 {#non-compliant-code-config-install}

```text
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    + config [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

#### 符合代碼 {#compliant-code-config-install}

```text
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    ./configPath = inplaceEditingConfig (String)
    + inplaceEditingConfig [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

### 包不應重疊 {#oakpal-no-overlap}

* **鍵**:包重疊
* **類型**:蟲
* **嚴重性**:主
* **自**:2019.6.0版

與 [包不應包含重複的OSGi配置規則，](#oakpal-package-osgi) 這是由多個獨立內容包寫入同一節點路徑的複雜項目中常見的問題。 雖然可以使用內容包依賴項來確保結果一致，但最好避免完全重疊。

### 預設創作模式不應為標準用戶介面 {#oakpal-default-authoring}

* **鍵**:ClassicUIAuthoringMode
* **類型**:代碼氣味/Cloud Service相容性
* **嚴重性**:小
* **自**:2020.5.0版

OSGi配置 `com.day.cq.wcm.core.impl.AuthoringUIModeServiceImpl` 定義中的預設創作模AEM式。 因為 [自6.4以來已棄AEM用經典UI,](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/deprecated-removed-features.html) 將預設創作模式配置為「Classic UI（標準用戶介面）」時，將會引發問題。

### 具有對話框的元件應具有觸摸UI對話框 {#oakpal-components-dialogs}

* **鍵**:ComponentWithOnlyClassicUIDialog
* **類型**:代碼氣味/Cloud Service相容性
* **嚴重性**:小
* **自**:2020.5.0版

具AEM有Classic UI對話框的元件應始終具有相應的Touch UI對話框，以提供最佳創作體驗，並與Cloud Service部署模型相容，其中不支援Classic UI。 此規則驗證以下方案：

* 具有「經典用戶介面」對話框的元件(即 `dialog` 子節點)必須具有相應的觸摸UI對話框(即 `cq:dialog` 子節點)。
* 具有「經典UI設計」對話框的元件(即 `design_dialog` 節點)必須具有相應的觸摸UI設計對話框(即 `cq:design_dialog` 子節點)。
* 具有「經典UI」對話框和「經典UI設計」對話框的元件必須同時具有相應的「觸摸UI」對話框和相應的「觸摸UI設計」對話框。

「現代化工AEM具」文檔提供了如何將元件從傳統用戶介面轉換為觸摸用戶介面的文檔和工具。 請參閱 [現代化工AEM具文檔](https://opensource.adobe.com/aem-modernize-tools/pages/tools.html) 的子菜單。

### 包不應混合可變和不可變內容 {#oakpal-packages-immutable}

* **鍵**:不可變MutableMixedPackage
* **類型**:代碼氣味/Cloud Service相容性
* **嚴重性**:小
* **自**:2020.5.0版

為了與Cloud Service部署模型相容，單個內容包必須包含儲存庫不可變區域的任一內容(即， `/apps` 和 `/libs`)或可變區域(即 `/apps` 或 `/libs`)，但不是兩者兼而有之。 例如，包含兩者的包 `/apps/myco/components/text and /etc/clientlibs/myco` 與Cloud Service不相容，將導致報告問題。

>[!NOTE]
規則 [客戶包不應在/libs下建立或修改節點](#oakpal-customer-package) 總是適用。

請參閱 [項AEM目結構](/help/implementing/developing/introduction/aem-project-content-package-structure.md) 的子菜單。

### 不應使用反向複製代理 {#oakpal-reverse-replication}

* **鍵**:反向複製
* **類型**:代碼氣味/Cloud Service相容性
* **嚴重性**:小
* **自**:2020.5.0版

在Cloud Service部署中不支援反向複製，如as a Cloud Service的AEM一部分所述 [發行說明。](/help/release-notes/aem-cloud-changes.md#replication-agents)

使用反向複製的客戶應聯繫Adobe以獲得其他解決方案。

### 啟用代理的客戶端庫中包含的資源應位於名為資源的資料夾中 {#oakpal-resources-proxy}

* **鍵**:客戶端庫代理資源
* **類型**:蟲
* **嚴重性**:小
* **自**:2021.2.0版

客AEM戶端庫可能包含靜態資源，如影像和字型。 如文檔中所述 [使用預處理器，](/help/implementing/developing/introduction/clientlibs.md#using-preprocessors) 使用代理客戶端庫時，這些靜態資源必須包含在名為 `resources` 以便對發佈實例進行有效引用。

#### 不符合代碼 {#non-compliant-proxy-enabled}

```text
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + images
        + myimage.jpg
```

#### 符合代碼 {#compliant-proxy-enabled}

```tet
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + resources
        + myimage.jpg
```

### Cloud Service不相容的工作流進程的使用 {#oakpal-usage-cloud-service}

* **鍵**:CloudServiceIncomplateWorkflowProcess
* **類型**:蟲
* **嚴重性**:主
* **自**:2021.2.0版

隨著as a Cloud Service上資產微服務的遷移AEM，在內部和AMS版本中使用的多個工作流進程變得不支援AEM或不必要。

中的遷移工具 [AEM Assetsas a Cloud ServiceGitHub儲存庫](https://github.com/adobe/aem-cloud-migration) 可用於在遷移到as a Cloud Service期間更新工作流AEM模型。

### 不鼓勵使用靜態模板，而是使用可編輯模板 {#oakpal-static-template}

* **鍵**:靜態模板用法
* **類型**:代碼氣味
* **嚴重性**:小
* **自**:2021.2.0版

儘管靜態模板的使用在項目中一直非常常見AEM，但強烈建議使用可編輯模板，因為它們提供了最靈活的功能，並支援靜態模板中不存在的其他功能。 更多資訊可在文檔中找到 [頁面模板。](/help/implementing/developing/components/templates.md)

使用 [現代化AEM工具。](https://opensource.adobe.com/aem-modernize-tools/)

### 不鼓勵使用舊式基礎元件 {#oakpal-usage-legacy}

* **鍵**:LegacyFoundationComponentUsage
* **類型**:代碼氣味
* **嚴重性**:小
* **自**:2021.2.0版

舊式基礎元件(即 `/libs/foundation`) [已棄用多個AEM版本](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/deprecated-removed-features.html) 支援核心元件。 不鼓勵將Foundation Components用作自定義元件的基礎（無論是通過覆蓋還是繼承），並應轉換為相應的核心元件。

此轉換可通過 [現代化AEM工具。](https://opensource.adobe.com/aem-modernize-tools/)

### 只應使用支援的運行模式名稱和排序 {#oakpal-supported-runmodes}

* **鍵**:支援的運行模式
* **類型**:代碼氣味
* **嚴重性**:小
* **自**:2021.2.0版

AEMas a Cloud Service對運行模式名稱實施嚴格的命名策略，對這些運行模式實施嚴格的排序。 在文檔中可找到支援的運行模式清單 [部署到AEMas a Cloud Service](/help/implementing/deploying/overview.md#runmodes) 任何偏離都會被確定為問題。

### 自定義搜索索引定義節點必須是/oak:index的直接子節點 {#oakpal-custom-search}

* **鍵**:OakIndexLocation
* **類型**:代碼氣味
* **嚴重性**:小
* **自**:2021.2.0版

AEMas a Cloud Service要求自定義搜索索引定義（即類型的節點） `oak:QueryIndexDefinition`)是直接子節點 `/oak:index`。 必須移動其他位置的索引以與AEMas a Cloud Service相容。 有關搜索索引的詳細資訊，請參閱文檔 [內容搜索和索引。](/help/operations/indexing.md)

### 自定義搜索索引定義節點的compat版本必須為2 {#oakpal-custom-search-compatVersion}

* **鍵**:IndexCompat版本
* **類型**:代碼氣味
* **嚴重性**:小
* **自**:2021.2.0版

AEMas a Cloud Service要求自定義搜索索引定義（即類型的節點） `oak:QueryIndexDefinition`)必須 `compatVersion` 屬性設定為 `2`。 任何其他值都不受AEMas a Cloud Service支援。 有關搜索索引的詳細資訊，請參閱 [內容搜索和索引。](/help/operations/indexing.md)

### 自定義搜索索引定義節點的後代節點必須為nt：非結構化 {#oakpal-descendent-nodes}

* **鍵**:IndexDescendantNodeType
* **類型**:代碼氣味
* **嚴重性**:小
* **自**:2021.2.0版

當自定義搜索索引定義節點具有未排序的子節點時，會出現難以排除的問題。 為避免此情況，建議使用 `oak:QueryIndexDefinition` 節點的類型 `nt:unstructured`。

### 自定義搜索索引定義節點必須包含名為indexRules的子節點，該子節點具有子節點 {#oakpal-custom-search-index}

* **鍵**:索引規則節點
* **類型**:代碼氣味
* **嚴重性**:小
* **自**:2021.2.0版

正確定義的自定義搜索索引定義節點必須包含名為 `indexRules` 而這個家庭至少要生一個孩子。 有關詳細資訊，請參閱 [橡木文檔。](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

### 自定義搜索索引定義節點必須遵循命名約定 {#oakpal-custom-search-definitions}

* **鍵**:索引名
* **類型**:代碼氣味
* **嚴重性**:小
* **自**:2021.2.0版

AEMas a Cloud Service要求自定義搜索索引定義(即 `oak:QueryIndexDefinition`)必須按照文檔中描述的特定模式命名 [內容搜索和索引。](/help/operations/indexing.md)

### 自定義搜索索引定義節點必須使用索引類型lucene  {#oakpal-index-type-lucene}

* **鍵**:索引類型
* **類型**:蟲
* **嚴重性**:阻止程式
* **自**:2021.2.0版(2021.8.0中更改了類型和嚴重性)

AEMas a Cloud Service要求自定義搜索索引定義（即類型的節點） `oak:QueryIndexDefinition`) `type` 值設定為的屬性 `lucene`。 在使用舊索引類型進行索引時，必須在遷移到AEMas a Cloud Service之前更新。 查看文檔 [內容搜索和索引](/help/operations/indexing.md#how-to-use) 的子菜單。

### 自定義搜索索引定義節點不能包含名為seed的屬性 {#oakpal-property-name-seed}

* **鍵**:IndexSeedProperty
* **類型**:代碼氣味
* **嚴重性**:小
* **自**:2021.2.0版

AEMas a Cloud Service禁止自定義搜索索引定義(即 `oak:QueryIndexDefinition`)來自包含名為 `seed`。 使用此屬性的索引必須在遷移到AEMas a Cloud Service之前更新。 查看文檔 [內容搜索和索引](/help/operations/indexing.md#how-to-use) 的子菜單。

### 自定義搜索索引定義節點不能包含名為reindex的屬性 {#oakpal-reindex-property}

* **鍵**:IndexReindexProperty
* **類型**:代碼氣味
* **嚴重性**:小
* **自**:2021.2.0版

AEMas a Cloud Service禁止自定義搜索索引定義(即 `oak:QueryIndexDefinition`)來自包含名為 `reindex`。 使用此屬性的索引必須在遷移到AEMas a Cloud Service之前更新。 查看文檔 [內容搜索和索引](/help/operations/indexing.md#how-to-use) 的子菜單。
