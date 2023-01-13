---
title: 自訂程式碼品質規則
description: 本頁說明了 Cloud Manager 在程式碼品質測試過程中執行的自訂程式碼品質規則。這些建議以Adobe Experience Manager工程的最佳實務為基礎。
exl-id: f40e5774-c76b-4c84-9d14-8e40ee6b775b
source-git-commit: 2935338b847f7e852dfd31c93a61e737e8a3ec80
workflow-type: tm+mt
source-wordcount: '3485'
ht-degree: 44%

---

# 自訂程式碼品質規則 {#custom-code-quality-rules}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_customcodequalityrules"
>title="自訂程式碼品質規則"
>abstract="本頁說明了 Cloud Manager 在程式碼品質測試過程中執行的自訂程式碼品質規則。這些建議以Adobe Experience Manager工程的最佳實務為基礎。"

本頁說明 Cloud Manager 在[程式碼品質測試](/help/implementing/cloud-manager/code-quality-testing.md)過程中執行的自訂程式碼品質規則。 這些建議以Experience Manager工程的最佳實務為基礎。

>[!NOTE]
>
>在此提供的程式碼範例僅供說明用途。請參閱 SonarQube [概念文件](https://docs.sonarqube.org/latest/)以了解 SonarQube 概念和品質規則。

## SonarQube規則 {#sonarqube-rules}

下節會詳細介紹由 Cloud Manager 執行的 SonarQube 規則。

### 不要使用潛在的危險功能 {#do-not-use-potentially-dangerous-functions}

* **索引碼**：CQRules:CWE-676
* **類型**：漏洞
* **嚴重度**：重大
* **始自**：2018.4.0 版本

方法 `Thread.stop()` 和 `Thread.interrupt()` 會產生難以重現的問題，有時還會產生安全漏洞。 它們的使用應受到嚴密監控和驗證。總的來說，傳遞資訊是實現類似目標的更安全的方式。

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

* **索引碼**：CQRules:CWE-134
* **類型**：漏洞
* **嚴重度**：重大
* **始自**：2018.4.0 版本

使用來自外部來源的格式字串 (例如要求參數或使用者產生的內容) 可能會讓應用計劃遭受拒絕服務的攻擊。在某些情況下，格式字串可能會受到外部控制，但僅允許來自受信任的來源。

#### 不符合代碼 {#non-compliant-code-1}

```java
protected void doPost(SlingHttpServletRequest request, SlingHttpServletResponse response) {
  String messageFormat = request.getParameter("messageFormat");
  request.getResource().getValueMap().put("some property", String.format(messageFormat, "some text"));
  response.sendStatus(HttpServletResponse.SC_OK);
}
```

### HTTP要求應一律有通訊端和連線逾時 {#http-requests-should-always-have-socket-and-connect-timeouts}

* **索引碼**：CQRules:ConnectionTimeoutMechanism
* **類型**：錯誤
* **嚴重度**：嚴重
* **始自**：2018.6.0 版本

從Experience Manager應用程式內執行HTTP請求時，務必確保配置正確的逾時，以避免不必要的執行緒耗用。 很可惜，兩個Java™預設HTTP用戶端的預設行為(`java.net.HttpUrlConnection`)，且常用的Apache HTTP元件用戶端永遠不會逾時，因此必須明確設定逾時。 此外，依據最佳做法的要求，上述逾時不應超過 60 秒。

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

### 一律關閉ResourceResolver物件 {#resourceresolver-objects-should-always-be-closed}

* **索引碼**：CQRules:CQBP-72
* **類型**：程式碼異味
* **嚴重度**：重大
* **始自**：2018.4.0 版本

`ResourceResolver` 物件 (獲自 `ResourceResolverFactory`) 會消耗系統資源。儘管現有一些措施可以在 `ResourceResolver` 不再使用時回收這些資源，但透過呼叫 `close()` 方法明確關閉任何開啟的 `ResourceResolver` 物件會更有效率。

一個相對常見的誤解是 `ResourceResolver` 使用現有JCR會話建立的對象不應顯式關閉，或者這樣會關閉基礎的JCR會話。 情況並非如此。無論 `ResourceResolver` 如何開啟，不使用時都經將其關閉。由於 `ResourceResolver` 實作 `Closeable` 介面，也有可能使用 `try-with-resources` 語法而不是明確地叫用 `close()`。

#### 不符合代碼 {#non-compliant-code-4}

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

### 請勿使用Sling servlet路徑來註冊servlet {#do-not-use-sling-servlet-paths-to-register-servlets}

* **索引碼**：CQRules:CQBP-75
* **類型**：程式碼異味
* **嚴重度**：重大
* **始自**：2018.4.0 版本

如同在 [Sling 文件紀錄](https://sling.apache.org/documentation/the-sling-engine/servlets.html)中的說明，不建議按路徑繫結 servlet。路徑繫結的 servlet 不能使用標準的 JCR 存取控制，因此需要額外嚴格的安全性。建議不要使用路徑繫結的 servlet，而是在存放庫中建立節點並按資源類型註冊 servlet。

#### 不符合代碼 {#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### 捕獲的例外應記錄或擲回，而非兩者 {#caught-exceptions-should-be-logged-or-thrown-but-not-both}

* **索引碼**：CQRules:CQBP-44---CatchAndEitherLogOrThrow
* **類型**：程式碼異味
* **嚴重度**：輕微
* **始自**：2018.4.0 版本

一般而言，應該只記錄一次例外狀況。記錄多次例外狀況可能會導致混淆，因為會不清楚發生了多少次例外狀況。會導致這種情況的最常見模式是將攔截到的例外狀況記錄並擲回。

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

### 避免日誌陳述式後面緊接著拋出語句 {#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

* **索引碼**：CQRules:CQBP-44---ConsecutivelyLogAndThrow
* **類型**：程式碼異味
* **嚴重度**：輕微
* **始自**：2018.4.0 版本

另一個要避免的常見模式是記錄一則訊息後立即擲回例外狀況。此慣例通常表示異常消息最終在日誌檔案中重複。

#### 不符合代碼 {#non-compliant-code-7}

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

* **索引碼**：CQRules:CQBP-44---LogInfoInGetOrHeadRequests
* **類型**：程式碼異味
* **嚴重度**：輕微

通常，INFO日誌級別應用於標定重要操作，預設情況下，Experience Manager配置為在INFO級別或更高級別上進行日誌。 GET 和 HEAD 方法應僅能唯讀操作，因此不構成重要操作。響應GET或HEAD請求而以INFO級別記錄可能會產生顯著的日誌雜訊，因此在日誌檔案中更難識別有用資訊。 在處理 GET 或 HEAD 要求時若出現錯誤，應該在 WARN 或 ERROR 層級進行記錄，或者若是更深入的疑難排解資訊會有幫助，則應在 DEBUG 或 TRACE 層級。

>[!NOTE]
>
>這不適用於 `access.log`-type記錄。

#### 不符合代碼 {#non-compliant-code-8}

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

* **索引碼**：CQRules:CQBP-44---ExceptionGetMessageIsFirstLogParam
* **類型**：程式碼異味
* **嚴重度**：輕微
* **始自**：2018.4.0 版本

依據最佳做法的要求，紀錄訊息應提供有關應用計劃中發生例外狀況的位置的內容相關資訊。雖然上下文也可透過堆疊追蹤來判斷，但一般而言，記錄訊息將更容易讀取和理解。 因此，在記錄例外狀況時，若將例外狀況的訊息當成紀錄訊息來使用，是不好的做法。異常消息包含出錯的內容，而日誌消息應用於告知日誌讀取器發生異常時應用程式正在執行什麼操作。 異常消息仍被記錄。 透過指定您自己的訊息，可讓您更輕鬆了解記錄。

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

* **索引碼**：CQRules:CQBP-44---WrongLogLevelInCatchBlock
* **類型**：程式碼異味
* **嚴重度**：輕微
* **始自**：2018.4.0 版本

如名稱所示，在例外情況下，一律應使用Java™例外。 因此，當攔截到例外狀況時，確保將紀錄訊息記錄在以下適當層級 (WARN 或 ERROR) 非常重要。這可確保這些訊息正確地顯示在紀錄中。

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

* **索引碼**：CQRules:CQBP-44---ExceptionPrintStackTrace
* **類型**：程式碼異味
* **嚴重度**：輕微
* **始自**：2018.4.0 版本

如前所述，在了解紀錄訊息時，內容極為重要。使用 `Exception.printStackTrace()` 僅導致堆棧跟蹤輸出到標準錯誤流，從而丟失所有上下文。 此外，在諸如Experience Manager的多線程應用程式中，如果使用此方法並行打印多個例外，則其堆棧跡線可能重疊，這會產生明顯的混淆。 僅能透過紀錄架構記錄例外狀況。

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

* **索引碼**：CQRules:CQBP-44—LogLevelConsolePrinters
* **類型**：程式碼異味
* **嚴重度**：輕微
* **始自**：2018.4.0 版本

登入Experience Manager應一律透過記錄架構(SLF4J)完成。 直接輸出到標準輸出或標準錯誤流會丟失由記錄框架提供的結構和上下文資訊。 有時候會造成效能問題。

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

### 避免以硬式編碼撰寫的/apps和/libs路徑 {#avoid-hardcoded-apps-and-libs-paths}

* **索引碼**：CQRules:CQBP-71
* **類型**：程式碼異味
* **嚴重度**：輕微
* **始自**：2018.4.0 版本

一般而言，以 `/libs` 和 `/apps` 開頭的路徑不應為硬式編碼，因為它們參考的路徑最常儲存為和 Sling 搜尋路徑 (預設情況下會設定為 `/libs,/apps`) 相關的路徑。使用絕對路徑可能會引進難以察覺的缺陷，而且只會在專案生命週期的後期出現。

#### 不符合代碼 {#non-compliant-code-13}

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

### 不使用Sling排程器 {#sonarqube-sling-scheduler}

* **索引碼**：CQRules:AMSCORE-554
* **類型**：程式碼異味/雲端服務相容性
* **嚴重度**：輕微
* **始自**：2020.5.0 版本

對於需要保證執行的工作，請勿使用Sling排程器。 Sling 已排程的作業可保證執行並更適合叢集和非叢集環境。

請參閱 [Apache Sling事件和作業處理](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html) 以進一步了解在叢集環境中如何處理Sling作業。

### 請勿使用Experience Manager已棄用的API {#sonarqube-aem-deprecated}

* **索引碼**：AMSCORE-553
* **類型**：程式碼異味/雲端服務相容性
* **嚴重度**：輕微
* **始自**：2020.5.0 版本

Experience ManagerAPI表面正在不斷修訂，以識別不鼓勵使用並因此被視為已過時的API。

這些API通常會使用標準Java™來取代 `@Deprecated` 注釋，因此，由 `squid:CallToDeprecatedMethod`.

不過，在某些情況下，API會在Experience Manager內容中遭到取代，但在其他內容中可能不會遭到取代。 此規則會識別此第二分類。


## OakPAL內容規則 {#oakpal-rules}

下節會詳細介紹由 Cloud Manager 執行的 OakPAL 檢查。

>[!NOTE]
>
>OakPAL 是一種架構，會使用獨立的 Oak 存放庫來驗證內容套件。由一名Experience Manager合作夥伴及2019年Experience ManagerRockstar北美獎得主開發。

### 客戶不應實作或擴充@ProviderType註解的產品API {#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}

* **索引碼**：CQBP-84
* **類型**：錯誤
* **嚴重度**：嚴重
* **始自**：2018.7.0 版本

Experience ManagerAPI包含Java™介面和類別，這些介面和類別僅能由自訂程式碼使用（但不能實作）。 例如，介面 `com.day.cq.wcm.api.Page` 應僅由Experience Manager實作。

將新方法添加到這些介面時，這些附加方法不會影響使用這些介面的現有代碼。 因此，在這些介面中添加新方法被視為向後相容。 但是，如果自訂程式碼實作其中一個介面，該自訂程式碼會給客戶帶來向後相容性風險。

介面和類(由Experience Manager實現)用注釋 `org.osgi.annotation.versioning.ProviderType` 或有時類似的舊式附註 `aQute.bnd.annotation.ProviderType`. 此規則會識別實作此類介面或由自訂程式碼擴展的分類的情況。

#### 不符合代碼 {#non-compliant-code-3}

```java
import com.day.cq.wcm.api.Page;

public class DontDoThis implements Page {
// implementation here
}
```

### 自訂Lucene Oak索引必須有Tika設定 {#oakpal-indextikanode}

* **索引碼**：IndexTikaNode
* **類型**：錯誤
* **嚴重度**：阻斷因素
* **始自**：2021.8.0

多個現成可用的Experience ManagerOak索引包含Tika設定，而這些索引的自訂必須包含Tika設定。 此規則會檢查 `damAssetLucene`、`lucene` 和 `graphqlConfig` 索引的自訂，並在 `tika` 節點缺少或 `tika` 節點缺少名為 `config.xml` 的子節點時引發問題。

有關自訂索引定義的詳細資訊，請參閱[索引文件](/help/operations/indexing.md#preparing-the-new-index-definition)。

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

* **索引碼**：IndexAsyncProperty
* **類型**：錯誤
* **嚴重度**：阻斷因素
* **始自**：2021.8.0

`lucene` 類型的 Oak 索引必須一律進行非同步索引。如果不這樣做可能會導致系統不穩定。有關Lucene索引結構的詳細資訊，請參閱 [Oak檔案。](https://jackrabbit.apache.org/oak/docs/query/lucene.html#index-definition)

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

* **索引碼**：IndexDamAssetLucene
* **類型**：錯誤
* **嚴重度**：阻斷因素
* **始自**：2021.6.0

為讓資產搜尋在Experience Manager Assets中正常運作，請自訂 `damAssetLucene` Oak索引必須遵循本索引專屬的准則集。 此規則會檢查索引定義是否必須具有包含值 `visualSimilaritySearch`，名為 `tags` 的多值屬性。

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

* **索引碼**：BannedPath
* **類型**：錯誤
* **嚴重度**：嚴重
* **始自**：2019.6.0 版本

長期以來，最佳做法是 `/libs` Experience Manager內容存放庫中的內容樹應被客戶視為唯讀。 修改 `/libs` 下的節點和屬性都會對大幅和小幅更新產生顯著風險。修改 `/libs` 必須通過官方渠道Adobe。

### 套件不應包含重複的OSGi設定 {#oakpal-package-osgi}

* **索引碼**：DuplicateOsgiConfigurations
* **類型**：錯誤
* **嚴重度**：重大
* **始自**：2019.6.0 版本

複雜專案中會出現的一個常見問題是多次設定同一個 OSGi 元件。此問題會造成哪個設定適用的模糊情況。 此規則「會感知執行模式」，因為它只會識別在同一執行模式或執行模式組合中多次設定相同元件的問題。

>[!NOTE]
>
>此規則會產生多個套件中定義相同設定（位於相同路徑）的問題，包括在建置套件的整體清單中複製相同套件的情況。
>
>例如，如果組建產生名為 `com.myco:com.myco.ui.apps` 和 `com.myco:com.myco.all` where `com.myco:com.myco.all` 內嵌 `com.myco:com.myco.ui.apps`，則 `com.myco:com.myco.ui.apps` 報告為重複項目。
>
>這通常是不遵循 [內容套件結構指南](/help/implementing/developing/introduction/aem-project-content-package-structure.md). 在此特定範例中，套件 `com.myco:com.myco.ui.apps` 中缺少 `<cloudManagerTarget>none</cloudManagerTarget>` 屬性。

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

#### 相容代碼 {#compliant-code-osgi}

```text
+ apps
  + shared-config
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

### 配置和安裝資料夾應僅包含OSGi節點 {#oakpal-config-install}

* **索引碼碼**：ConfigAndInstallShouldOnlyContainOsgiNodes
* **類型**：錯誤
* **嚴重度**：重大
* **始自**：2019.6.0 版本

基於安全原因，包含 `/config/` 和 `/install/` 僅供Experience Manager中的管理使用者閱讀，且僅應用於OSGi設定和OSGi套件組合。 將其他類型的內容放在包含這些區段的路徑下會導致應用計劃行為在管理員使用者和非管理員使用者之間無意間發生變化。

一個常見問題是在元件對話框中或在為內嵌編輯指定 RTF 文字編輯器設定時會使用名為 `config` 的節點。要解決此問題，應將違規節點重新命名為符合規範的名稱。 對於RTF編輯器設定，請使用 `configPath` 屬性 `cq:inplaceEditing` 節點，指定新位置。

#### 不符合代碼 {#non-compliant-code-config-install}

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

* **索引碼**：PackageOverlaps
* **類型**：錯誤
* **嚴重度**：重大
* **始自**：2019.6.0 版本

類似[套件不應包含重複的 OSGi 設定規則，](#oakpal-package-osgi)這是複雜專案中常見的問題，這類專案會由多個單獨的內容套件寫入相同的節點路徑。雖然使用內容套件相依性可用於確保一致的結果，但最好還是完全避免重疊。

### 預設編寫模式不應為傳統UI {#oakpal-default-authoring}

* **索引碼**：ClassicUIAuthoringMode
* **類型**：程式碼異味/雲端服務相容性
* **嚴重度**：輕微
* **始自**：2020.5.0 版本

OSGi設定 `com.day.cq.wcm.core.impl.AuthoringUIModeServiceImpl` 會定義Experience Manager內的預設製作模式。 因為 [傳統UI自Experience Manager6.4起已過時](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/deprecated-removed-features.html?lang=zh-Hant)，現在當將預設編寫模式設為傳統UI時會發生問題。

### 具有對話方塊的元件應具有觸控式UI對話方塊 {#oakpal-components-dialogs}

* **索引碼**：ComponentWithOnlyClassicUIDialog
* **類型**：程式碼異味/雲端服務相容性
* **嚴重度**：輕微
* **始自**：2020.5.0 版本

Experience Manager元件若有傳統UI對話方塊，應一律有對應的觸控式UI對話方塊。 兩者都提供最佳的製作體驗，並與不支援傳統UI的Cloud Service部署模型相容。 本規則可證實以下情境：

* 具有 Classic UI 對話框 (即 `dialog` 子節點) 的元件必須具有相對應的 Touch UI 對話框 (即 `cq:dialog` 子節點)。
* 具有 Classic UI 設計對話框 (即 `design_dialog` 節點) 的元件必須具有相對應的 Touch UI 對話框 (即 `cq:design_dialog` 子節點)。
* 同時具有 Classic UI 對話框以及 Classic UI 設計對話框的元件必須同時有相對應的 Touch UI 對話框以及相對應的 Touch UI 設計對話框。

「Experience Manager現代化工具」檔案提供檔案和工具，說明如何將元件從傳統UI轉換為觸控式UI。 請參閱 [Experience Manager現代化工具檔案](https://opensource.adobe.com/aem-modernize-tools/) 以取得更多詳細資訊。

### 套件不應混用可變和不可變的內容 {#oakpal-packages-immutable}

* **索引碼**：ImmutableMutableMixedPackage
* **類型**：程式碼異味/雲端服務相容性
* **嚴重度**：輕微
* **始自**：2020.5.0 版本

要與Cloud Service部署模型相容，單個內容包必須包含儲存庫不可變區域的任一內容(`/apps` 和 `/libs`)，或可變區域(不包含 `/apps` 或 `/libs`)，但不能兩者兼而有之。 例如，包含兩者的套件 `/apps/myco/components/text` 和 `/etc/clientlibs/myco` 與Cloud Service不相容，且會導致回報問題。

>[!NOTE]
>
>此[客戶套件不應在 /libs 下建立或修改節點](#oakpal-customer-package)規則永遠適用。

請參閱 [Experience Manager專案結構](/help/implementing/developing/introduction/aem-project-content-package-structure.md) 以取得更多詳細資訊。

### 不使用反向複製代理 {#oakpal-reverse-replication}

* **索引碼**：ReverseReplication
* **類型**：程式碼異味/雲端服務相容性
* **嚴重度**：輕微
* **始自**：2020.5.0 版本

Cloud Service部署中不支援反向復寫，如Experience Manageras a Cloud Service的 [發行說明。](/help/release-notes/aem-cloud-changes.md#replication-agents)

使用反向複寫的客戶應和 Adobe 聯絡，以取得替代解決方案。

### 啟用代理的客戶端庫中所包含的資源應位於名為資源的資料夾中 {#oakpal-resources-proxy}

* **索引碼**：ClientlibProxyResource
* **類型**：錯誤
* **嚴重度**：輕微
* **始自**：2021.2.0 版本

Experience Manager用戶端程式庫可包含靜態資源，例如影像和字型。 如[使用前置處理器](/help/implementing/developing/introduction/clientlibs.md#using-preprocessors)文件中所述，使用透過 Proxy 的用戶端資料庫時，這些靜態資源必須包含在名為 `resources` 的子檔案夾中，以便在發佈執行個體上有效地參考。

#### 不符合代碼 {#non-compliant-proxy-enabled}

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

### 使用Cloud Service不相容的工作流程程式 {#oakpal-usage-cloud-service}

* **索引碼**：CloudServiceIncompatibleWorkflowProcess
* **類型**：錯誤
* **嚴重度**：重大
* **始自**：2021.2.0 版本

隨著移轉至資產微服務以進行Experience Manageras a Cloud Service的資產處理，內部部署和AMS版本Experience Manager中使用的數個工作流程程式，已變得不支援或不必要。

移轉工具，位於 [Experience Manageras a Cloud Service資產GitHub存放庫](https://github.com/adobe/aem-cloud-migration) 可在移轉至Experience Manageras a Cloud Service時，用來更新工作流程模型。

### 不建議使用靜態範本，而改用可編輯的範本 {#oakpal-static-template}

* **索引碼**：StaticTemplateUsage
* **類型**：程式碼異味
* **嚴重度**：輕微
* **始自**：2021.2.0 版本

雖然靜態範本的使用在Experience Manager專案中向來很常見，但Adobe建議使用可編輯的範本，因為這些範本提供最大的彈性，並支援靜態範本中未顯示的其他功能。 在[頁面範本](/help/implementing/developing/components/templates.md)文件中可找到更多資訊。

從靜態範本移轉至可編輯的範本，可透過 [Experience Manager現代化工具。](https://opensource.adobe.com/aem-modernize-tools/)

### 不建議使用舊版基礎元件 {#oakpal-usage-legacy}

* **索引碼**：LegacyFoundationComponentUsage
* **類型**：程式碼異味
* **嚴重度**：輕微
* **始自**：2021.2.0 版本

舊版Foundation元件(即 `/libs/foundation`)已 [多個Experience Manager版本已棄用](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/deprecated-removed-features.html?lang=zh-Hant) 以支援核心元件。 不建議使用基礎元件作為自訂元件的基礎 (無論是透過覆蓋還是繼承)，並應轉換為相對應的核心元件。

此轉換可由 [Experience Manager現代化工具。](https://opensource.adobe.com/aem-modernize-tools/)

### 僅使用支援的運行模式名稱和順序 {#oakpal-supported-runmodes}

* **索引碼**：SupportedRunmode
* **類型**：程式碼異味
* **嚴重度**：輕微
* **始自**：2021.2.0 版本

Experience Manageras a Cloud Service對運行模式名稱強制執行嚴格的命名策略，並對這些運行模式執行嚴格的排序。 可在文檔中找到支援的運行模式清單 [部署至Experience Manageras a Cloud Service](/help/implementing/deploying/overview.md#runmodes) 任何偏離都會被認定為問題。

### 自訂搜尋索引定義節點必須是/oak:index的直接子項 {#oakpal-custom-search}

* **索引碼**：OakIndexLocation
* **類型**：程式碼異味
* **嚴重度**：輕微
* **始自**：2021.2.0 版本

Experience Manageras a Cloud Service要求自訂搜尋索引定義（即類型的節點） `oak:QueryIndexDefinition`)是直接的子節點 `/oak:index`. 其他位置中的索引必須移動以與Experience Manageras a Cloud Service相容。 有關搜尋索引的更多資訊可在[內容搜尋和索引](/help/operations/indexing.md)文件中找到。

### 自定義搜索索引定義節點必須具有2的compatVersion {#oakpal-custom-search-compatVersion}

* **索引碼**：IndexCompatVersion
* **類型**：程式碼異味
* **嚴重度**：輕微
* **始自**：2021.2.0 版本

Experience Manageras a Cloud Service要求自訂搜尋索引定義（例如類型的節點） `oak:QueryIndexDefinition`)必須有 `compatVersion` 屬性設定為 `2`. Experience Manageras a Cloud Service不支援任何其他值。 有關搜尋索引的更多資訊可在以下連結中找到：[內容搜尋和索引。](/help/operations/indexing.md)

### 自定義搜索索引定義節點的子節點必須為nt:unstructured {#oakpal-descendent-nodes}

* **索引碼**：IndexDescendantNodeType
* **類型**：程式碼異味
* **嚴重度**：輕微
* **始自**：2021.2.0 版本

自訂搜尋索引定義節點具有無序的子節點時，可能會發生難以疑難排解的問題。 為避免此情況，建議 `oak:QueryIndexDefinition` 節點類型 `nt:unstructured`.

### 自定義搜索索引定義節點必須包含一個名為indexRules的子節點，該子節點具有子節點 {#oakpal-custom-search-index}

* **索引碼**：IndexRulesNode
* **類型**：程式碼異味
* **嚴重度**：輕微
* **始自**：2021.2.0 版本

正確定義的自訂搜尋索引定義節點必須包含一個名為 `indexRules` 的子節點，而該子節點又必須至少有一個子系。在以下連結中可找到更多資訊：[Oak 文件。](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

### 自定義搜索索引定義節點必須遵循命名慣例 {#oakpal-custom-search-definitions}

* **索引碼**：IndexName
* **類型**：程式碼異味
* **嚴重度**：輕微
* **始自**：2021.2.0 版本

Experience Manageras a Cloud Service要求自定義搜索索引定義（即，類型的節點） `oak:QueryIndexDefinition`)必須依照檔案中所述的特定模式命名 [內容搜尋和索引。](/help/operations/indexing.md)

### 自定義搜索索引定義節點必須使用索引類型Lucene  {#oakpal-index-type-lucene}

* **索引碼**：IndexType
* **類型**：錯誤
* **嚴重度**：阻斷因素
* **始自**：2021.2.0 版本 (在 2021.8.0 變更類型和嚴重性)

Experience Manageras a Cloud Service要求自訂搜尋索引定義（即類型的節點） `oak:QueryIndexDefinition`)有 `type` 值設為的屬性 `lucene`. 必須在遷移到Experience Manageras a Cloud Service之前更新使用舊索引類型的索引。 請參閱 [內容搜尋與索引](/help/operations/indexing.md#how-to-use) 以取得更多資訊。

### 自定義搜索索引定義節點不得包含名為seed的屬性 {#oakpal-property-name-seed}

* **索引碼**：IndexSeedProperty
* **類型**：程式碼異味
* **嚴重度**：輕微
* **始自**：2021.2.0 版本

Experience Manageras a Cloud Service禁止自定義搜索索引定義（即，類型的節點） `oak:QueryIndexDefinition`)，從包含名為 `seed`. 在遷移到Experience Manageras a Cloud Service之前，必須更新使用此屬性的索引。 如需詳細資訊，請參閱[內容搜尋和索引](/help/operations/indexing.md#how-to-use)文件。

### 自定義搜索索引定義節點不能包含名為reindex的屬性 {#oakpal-reindex-property}

* **索引碼**：IndexReindexProperty
* **類型**：程式碼異味
* **嚴重度**：輕微
* **始自**：2021.2.0 版本

Experience Manageras a Cloud Service禁止自定義搜索索引定義（即，類型的節點） `oak:QueryIndexDefinition`)，從包含名為 `reindex`. 在遷移到Experience Manageras a Cloud Service之前，必須更新使用此屬性的索引。 如需詳細資訊，請參閱[內容搜尋和索引](/help/operations/indexing.md#how-to-use)文件。
