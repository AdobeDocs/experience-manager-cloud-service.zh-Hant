---
title: 自訂程式碼品質規則
description: 了解 Cloud Manager 根據 Adobe Experience Manager Engineering 最佳實務的自訂程式碼品質規則，以透過徹底的測試確保高品質的程式碼。
exl-id: f40e5774-c76b-4c84-9d14-8e40ee6b775b
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '4349'
ht-degree: 64%

---

# 自訂程式碼品質規則 {#custom-code-quality-rules}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_customcodequalityrules"
>title="自訂程式碼品質規則"
>abstract="了解 Cloud Manager 根據 Adobe Experience Manager Engineering 最佳實務的自訂程式碼品質規則，以透過徹底的測試確保高品質的程式碼。"

瞭解Cloud Manager以Adobe Experience Manager工程最佳實務為基礎的自訂程式碼品質規則，透過徹底測試確保高品質的程式碼。 另請參閱[程式碼品質測試](/help/implementing/cloud-manager/code-quality-testing.md)。

由於 Adobe 專屬資訊，完整的 SonarQube 規則無法下載。您可以使用此連結&#x200B;*下載*&#x200B;目前[規則](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest-CS.xlsx)的完整清單。 繼續閱讀本文件以取得規則的說明和範例。

>[!IMPORTANT]
>
>從 2025 年 2 月 13 日 (星期四) (Cloud Manager 2025.2.0) 開始，Cloud Manager 程式碼品質將使用更新後的 SonarQube 9.9 版本和更新後的規則清單 (可[在此處下載](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest-CS-2024-12-0.xlsx))。

>[!NOTE]
>
>在此提供的程式碼範例僅供說明用途。請參閱 SonarQube [概念文件](https://docs.sonarsource.com/sonarqube/latest/)以了解 SonarQube 概念和品質規則。

## SonarQube 規則 {#sonarqube-rules}

下節會詳細介紹由 Cloud Manager 執行的 SonarQube 規則。

### 請勿使用有潛在危險的功能 {#do-not-use-potentially-dangerous-functions}

* **索引鍵**： CQRules:CWE-676
* **類型**：漏洞
* **嚴重度**：重大
* **始自**：2018.4.0 版本

方法 `Thread.stop()` 和 `Thread.interrupt()` 可能產生難以重現的問題，有時還可能產生安全性漏洞。它們的使用應受到嚴密監控和驗證。總的來說，傳遞資訊是實現類似目標的更安全的方式。

#### 不符合規範的程式碼 {#non-compliant-code}

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

#### 符合規範的程式碼 {#compliant-code}

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

* **索引鍵**： CQRules:CWE-134
* **類型**：漏洞
* **嚴重度**：重大
* **始自**：2018.4.0 版本

使用來自外部來源的格式字串 (例如請求參數或使用者產生的內容) 可能會讓應用程式面臨阻絕服務攻擊。在某些情況下，格式字串可能會受到外部控制，但是僅限受信任的來源。

#### 不符合規範的程式碼 {#non-compliant-code-1}

```java
protected void doPost(SlingHttpServletRequest request, SlingHttpServletResponse response) {
  String messageFormat = request.getParameter("messageFormat");
  request.getResource().getValueMap().put("some property", String.format(messageFormat, "some text"));
  response.sendStatus(HttpServletResponse.SC_OK);
}
```

### HTTP 要求始終都應該有通訊端和連線逾時 {#http-requests-should-always-have-socket-and-connect-timeouts}

* **索引鍵**： CQRules:ConnectionTimeoutMechanism
* **類型**：錯誤
* **嚴重度**：嚴重
* **始自**：2018.6.0 版本

在Experience Manager應用程式中提出HTTP請求時，必須設定適當的逾時以防止不必要的執行緒消耗。
根據預設，Java™ HTTP使用者端(java.net.HttpUrlConnection)和廣泛使用的Apache HTTP元件使用者端不會強制逾時，因此必須手動設定。 逾時最好設定為60秒以內。

#### 不符合規範的程式碼 {#non-compliant-code-2}

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

#### 符合規範的程式碼 {#compliant-code-1}

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

public void orDoThis () {
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

### 一律關閉 ResourceResolver 物件 {#resourceresolver-objects-should-always-be-closed}

* **索引鍵**： CQRules:CQBP-72
* **類型**：`Code Smell`
* **嚴重度**：重大
* **始自**：2018.4.0 版本

從`ResourceResolverFactory`取得的ResourceResolver物件會消耗系統資源。 儘管現有一些措施可供不再使用 `ResourceResolver` 時回收這些資源，但透過呼叫 `close()` 方法明確關閉任何開啟的 `ResourceResolver` 物件會更有效率。

一個常見的誤解是，不應將使用現有JCR工作階段建立的`ResourceResolver`物件明確關閉，或關閉這些物件會影響JCR工作階段。 此資訊不正確。 `ResourceResolver`在不再需要時應一律關閉。 由於`ResourceResolver`實作`Closeable`介面，因此您也可以使用`try-with-resources`語法，而非直接呼叫`close()`。

#### 不符合規範的程式碼 {#non-compliant-code-4}

```java
public void dontDoThis(Session session) throws Exception {
  ResourceResolver resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object)session));
  // do some stuff with the resolver
}
```

#### 符合規範的程式碼 {#compliant-code-2}

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

### 請勿使用 Sling Servlet 路徑來註冊 Servlet {#do-not-use-sling-servlet-paths-to-register-servlets}

* **索引鍵**： CQRules:CQBP-75
* **類型**：`Code Smell`
* **嚴重度**：重大
* **始自**：2018.4.0 版本

如[`Sling`檔案](https://sling.apache.org/documentation/the-sling-engine/servlets.html)中所述，不建議按路徑繫結servlet。 路徑繫結的 servlet 不能使用標準的 JCR 存取控制，因此需要額外嚴格的安全性。建議不要使用路徑繫結的 servlet，而是在存放庫中建立節點並按資源類型註冊 servlet。

#### 不符合規範的程式碼 {#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### 應記錄或擲回攔截到的例外狀況，而非執行兩者。 {#caught-exceptions-should-be-logged-or-thrown-but-not-both}

* **索引鍵**： CQRules:CQBP-44---CatchAndEitherLogOrThrow
* **類型**：`Code Smell`
* **嚴重度**：輕微
* **始自**：2018.4.0 版本

一般而言，應該只記錄一次例外狀況。多次記錄例外狀況可能會導致混淆。 原因是因為不清楚發生了多少次例外狀況。 導致此效果的最常見模式是記錄並擲回攔截到的例外狀況。

#### 不符合規範的程式碼 {#non-compliant-code-6}

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

#### 符合規範的程式碼 {#compliant-code-3}

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

### 避免 Log 陳述式後緊跟著 Throw 陳述式 {#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

* **索引鍵**： CQRules:CQBP-44---ConsecutivelyLogAndThrow
* **類型**：`Code Smell`
* **嚴重度**：輕微
* **始自**：2018.4.0 版本

另一個要避免的常見模式是記錄一則訊息後立即擲回例外狀況。此做法通常表示例外狀況訊息最終會在記錄檔案中重複。

#### 不符合規範的程式碼 {#non-compliant-code-7}

```java
public void dontDoThis() throws Exception {
  logger.error("something went wrong");
  throw new RuntimeException("something went wrong");
}
```

#### 符合規範的程式碼 {#compliant-code-4}

```java
public void doThis() throws Exception {
  throw new RuntimeException("something went wrong");
}
```

### 處理 GET 或 HEAD 要求時避免在 INFO 上進行記錄 {#avoid-logging-at-info-when-handling-get-or-head-requests}

* **索引鍵**： CQRules:CQBP-44---LogInfoInGetOrHeadRequests
* **類型**：`Code Smell`
* **嚴重度**：輕微

一般而言，應該使用 INFO 記錄層級來區分重要操作，並且預設情況下，會將 Experience Manager 設定為在 INFO 或以上層級記錄。GET 和 HEAD 方法應僅能唯讀操作，因此不構成重要操作。在 INFO 層級記錄以回應 GET 或 HEAD 要求可能會產生大量記錄雜訊，而使得在記錄檔中識別有用資訊變得更加困難。在處理GET或HEAD請求時，如果出現錯誤，請在WARN或ERROR層級記錄。 如需詳細的疑難排解資訊，請使用DEBUG或TRACE層級。

>[!NOTE]
>
>不適用於每個要求的`access.log`型別記錄。

#### 不符合規範的程式碼 {#non-compliant-code-8}

```java
public void doGet() throws Exception {
  logger.info("handling a request from the user");
}
```

#### 符合規範的程式碼 {#compliant-code-5}

```java
public void doGet() throws Exception {
  logger.debug("handling a request from the user.");
}
```

### 請勿使用 Exception.getMessage() 作為記錄陳述式的第一個參數 {#do-not-use-exception-getmessage-as-the-first-parameter-of-a-logging-statement}

* **索引鍵**： CQRules:CQBP-44---ExceptionGetMessageIsFirstLogParam
* **類型**：`Code Smell`
* **嚴重度**：輕微
* **始自**：2018.4.0 版本

依據最佳做法的要求，紀錄訊息應提供有關應用程式中發生例外狀況的位置的內容相關資訊。雖然也可以透過使用堆疊追蹤來確定內容，但記錄訊息通常將更容易讀取和理解。因此，在記錄例外狀況時，將例外狀況的訊息當成記錄訊息來使用是不好的做法。例外狀況訊息會說明所發生的問題，而紀錄訊息則應將例外狀況發生時應用程式正在執行的動作通知給讀者。 例外狀況訊息仍會記錄。透過指定您自己的訊息，更容易理解這些紀錄。

#### 不符合規範的程式碼 {#non-compliant-code-9}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error(e.getMessage(), e);
  }
}
```

#### 符合規範的程式碼 {#compliant-code-6}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### Catch 區塊中的記錄應在 WARN 或 ERROR 層級進行 {#logging-in-catch-blocks-should-be-at-the-warn-or-error-level}

* **索引鍵**： CQRules:CQBP-44---WrongLogLevelInCatchBlock
* **類型**：`Code Smell`
* **嚴重度**：輕微
* **始自**：2018.4.0 版本

顧名思義，在例外情況下，始終都應該使用 Java™ 例外狀況。因此，當攔截到例外狀況時，確保將紀錄訊息記錄在以下適當層級 (WARN 或 ERROR) 非常重要。此程式會確保這些訊息正確地顯示在紀錄中。

#### 不符合規範的程式碼 {#non-compliant-code-10}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.debug(e.getMessage(), e);
  }
}
```

#### 符合規範的程式碼 {#compliant-code-7}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 不可將堆疊追蹤列印到控制台 {#do-not-print-stack-traces-to-the-console}

* **索引鍵**： CQRules:CQBP-44---ExceptionPrintStackTrace
* **類型**：`Code Smell`
* **嚴重度**：輕微
* **始自**：2018.4.0 版本

如前所述，在了解紀錄訊息時，內容極為重要。使用 `Exception.printStackTrace()` 只會導致堆疊追蹤輸出至標準錯誤流，而遺失所有內容。此外，在像 Experience Manager 這類多執行緒應用程式中，如果使用此方法同時列印多個例外狀況，它們的堆疊追蹤可能會重疊，從而產生嚴重的混亂。僅能透過記錄架構記錄例外狀況。

#### 不符合規範的程式碼 {#non-compliant-code-11}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    e.printStackTrace();
  }
}
```

#### 符合規範的程式碼 {#compliant-code-8}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 不可輸出到標準輸出或標準錯誤 {#do-not-output-to-standard-output-or-standard-error}

* **索引鍵**： CQRules:CQBP-44—LogLevelConsolePrinters
* **類型**：`Code Smell`
* **嚴重度**：輕微
* **始自**：2018.4.0 版本

Experience Manager 中的記錄應該始終透過記錄架構 (SLF4J) 完成。直接輸出到標準輸出或標準錯誤串流會遺失記錄架構提供的結構和相關內容資訊。有時還可能導致效能問題。

#### 不符合規範的程式碼 {#non-compliant-code-12}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    System.err.println("Unable to do something");
  }
}
```

#### 符合規範的程式碼 {#compliant-code-9}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 避免硬式編碼應用程式和程式庫路徑 {#avoid-hardcoded-apps-and-libs-paths}

* **索引鍵**： CQRules:CQBP-71
* **類型**：`Code Smell`
* **嚴重度**：輕微
* **始自**：2018.4.0 版本

以 `/libs` 和 `/apps` 開頭的路徑通常不應使用硬式編碼。這些路徑通常會相對於`Sling`搜尋路徑（預設為`/libs,/apps`）儲存。 使用絕對路徑可能會產生難以察覺的缺陷，而且後期才會在專案生命週期中顯現。

#### 不符合規範的程式碼 {#non-compliant-code-13}

```java
public boolean dontDoThis(Resource resource) {
  return resource.isResourceType("/libs/foundation/components/text");
}
```

#### 符合規範的程式碼 {#compliant-code-10}

```java
public void doThis(Resource resource) {
  return resource.isResourceType("foundation/components/text");
}
```

### 請勿使用 Sling 排程器 {#sonarqube-sling-scheduler}

* **索引鍵**： CQRules:AMSCORE-554
* **型別**： `Code Smell`/Cloud Service相容性
* **嚴重度**：輕微
* **始自**：2020.5.0 版本

請勿將`Sling`排程器用於要求保證執行的任務。 Sling 已排程的作業可保證執行並更適合叢集和非叢集環境。

請參閱[`Apache Sling`事件和作業處理](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html)，深入瞭解如何在叢集環境中處理Sling作業。

### 請勿使用 Experience Manager 已過時的 API {#sonarqube-aem-deprecated}

* **索引碼**：AMSCORE-553
* **型別**： `Code Smell`/Cloud Service相容性
* **嚴重度**：輕微
* **始自**：2020.5.0 版本

Experience Manager API 表面經過不斷修正，以識別不鼓勵使用並因此被視為已過時的 API。

通常，會使用標準 Java™ `@Deprecated` 註解來取代這些 API，而且會由 `squid:CallToDeprecatedMethod` 進行識別。

但是，在某些情況下，API 在 Experience Manager 的內容中會遭到取代，但在其他內容中卻可能不會。此規則會識別此第二分類。

### 請勿在Sling模型中搭配@Optional使用@Inject註釋 {#sonarqube-slingmodels-inject-optional}

* **Key**： InjectAnnotationWithOptionalInjectionCheck
* **型別**：軟體品質
* **嚴重度**：輕微
* **自**： 2023.11版

`Apache Sling`專案不鼓勵在Sling模型內容中使用`@Inject`註解，因為當與`DefaultInjectionStrategy.OPTIONAL`結合時（在欄位或類別層級），可能會導致效能不佳。 應該改用更具體的插入（例如`@ValueMapValue`或`@OsgiInjector`註解）。

請檢視[`Apache Sling`檔案](https://sling.apache.org/documentation/bundles/models.html#discouraged-annotations-1)，以取得關於建議之註解的詳細資訊，以及最初提出此建議的原因。


### 重複使用HTTPClient的執行個體 {#sonarqube-reuse-httpclient}

* **索引鍵**： AEMSRE-870
* **型別**：軟體品質
* **嚴重度**：輕微
* **自**： 2023.11版

AEM應用程式經常使用HTTP通訊協定與其他應用程式聯絡，Apache HttpClient是達到此目的的常用程式庫。 但是建立這樣的HttpClient物件會產生一些額外負荷，因此這些物件應儘可能重複使用。

此規則會檢查這類HttpClient物件在方法內是否不是私人，而是類別層級的全域，以便可以重複使用。 在這種情況下，HttpClient欄位應在類別的建構函式或`activate()`方法（如果此類別是OSGi元件/服務）中設定。

請檢視HttpClient的[最佳化指南](https://hc.apache.org/httpclient-legacy/performance.html)，以瞭解有關使用HttpClient的一些最佳實務。

#### 不符合規範的程式碼 {#non-compliant-code-14}

```java
public void doHttpCall() {
  HttpClient httpclient = HttpClients.createDefault();
  // do something with the httpclient
}
```

#### 符合規範的程式碼 {#compliant-code-11}

```java
public class myClass {

  HttpClient httpclient;

  public void doHttpCall() {
    // do something with the httpclient
  }

}
```

## OakPAL 內容規則 {#oakpal-rules}

下節會詳細介紹由 Cloud Manager 執行的 OakPAL 檢查。

>[!NOTE]
>
>OakPAL 是一種架構，會使用獨立的 Oak 存放庫來驗證內容套件。榮獲2019年Experience Manager Rockstar北美獎的Experience Manager合作夥伴開發出這款產品。

### 客戶不應實作或擴充以@ProviderType註解的產品API{#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}

* **索引碼**：CQBP-84
* **類型**：錯誤
* **嚴重度**：嚴重
* **始自**：2018.7.0 版本

Experience Manager API包含Java™介面和類別，這些介面和類別僅能由自訂程式碼使用，但不能實作。 例如，只有Experience Manager應該實作`com.day.cq.wcm.api.Page`介面。

將新方法新增到這些介面時，這些附加方法不會影響使用這些介面的現有程式碼。 因此，在這些介面中新增新方法會視為回溯相容。但是，如果自訂程式碼實作其中一個介面，該自訂程式碼會給客戶帶來回溯相容性的風險。

由 Experience Manager 實作的介面和分類會使用 `org.osgi.annotation.versioning.ProviderType` 進行註解，或有時會使用類似的舊註解 `aQute.bnd.annotation.ProviderType`。此規則會識別自訂程式碼實作此類介面或擴充類別的情況。

#### 不符合規範的程式碼 {#non-compliant-code-3}

```java
import com.day.cq.wcm.api.Page;

public class DontDoThis implements Page {
// implementation here
}
```

### 自訂 Lucene Oak 索引必須具有 Tika 設定 {#oakpal-indextikanode}

* **索引碼**：IndexTikaNode
* **類型**：錯誤
* **嚴重度**：阻斷因素
* **始自**：2021.8.0

多個現成的 Experience Manager Oak 索引包括 Tika 設定，且這些索引的自訂必須包括 Tika 設定。此規則會檢查 `damAssetLucene`、`lucene` 和 `graphqlConfig` 索引的自訂，並在 `tika` 節點缺少或 `tika` 節點缺少名為 `config.xml` 的子節點時引發問題。

如需有關自訂索引定義的詳細資訊，請參閱[索引文件](/help/operations/indexing.md#preparing-the-new-index-definition)。

#### 不符合規範的程式碼 {#non-compliant-code-indextikanode}

```text
+ oak:index
    + damAssetLucene-1-custom
      - async: [async]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - tags: [visualSimilaritySearch]
      - type: lucene
```

#### 符合規範的程式碼 {#compliant-code-indextikanode}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### 自訂 Lucene Oak 索引不能同步 {#oakpal-indexasync}

* **索引碼**：IndexAsyncProperty
* **類型**：錯誤
* **嚴重度**：阻斷因素
* **始自**：2021.8.0

`lucene` 類型的 Oak 索引必須一律進行非同步索引。若未這麼做，可能會導致系統不穩定。 有關Lucene索引結構的更多資訊可在[Oak檔案](https://jackrabbit.apache.org/oak/docs/query/lucene.html#index-definition)中找到。

#### 不符合規範的程式碼 {#non-compliant-code-indexasync}

```text
+ oak:index
    + damAssetLucene-1-custom
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - type: lucene
      - tags: [visualSimilaritySearch]
      + tika
        + config.xml
```

#### 符合規範的程式碼 {#compliant-code-indexasync}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### 自訂 DAM 資產 Lucene Oak 索引結構正確 {#oakpal-damAssetLucene-sanity-check}

* **索引碼**：IndexDamAssetLucene
* **類型**：錯誤
* **嚴重度**：阻斷因素
* **始自**：2021.6.0

要使資產搜尋在Experience Manager Assets中正常運作，`damAssetLucene` Oak索引的自訂必須遵循一組特定於此索引的准則。 此規則會檢查索引定義是否必須具有包含值`tags`且名為`visualSimilaritySearch`的多值屬性。

#### 不符合規範的程式碼 {#non-compliant-code-damAssetLucene}

```text
+ oak:index
    + damAssetLucene-1-custom
      - async: [async, nrt]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - type: lucene
      + tika
        + config.xml
```

#### 符合規範的程式碼 {#compliant-code-damAssetLucene}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async, nrt]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### 客戶套件不應在libs下建立或修改節點 {#oakpal-customer-package}

* **索引碼**：BannedPath
* **類型**：錯誤
* **嚴重度**：嚴重
* **始自**：2019.6.0 版本

客戶應將 Experience Manager 內容存放庫中的 `/libs` 內容樹視為唯讀，這是一個存在已久的最佳做法。修改 `/libs` 下的節點和屬性都會對大幅和小幅更新產生顯著風險。透過正式通道使用Adobe修改`/libs`。

### 套件不應包含重複的 OSGi 設定 {#oakpal-package-osgi}

* **索引碼**：DuplicateOsgiConfigurations
* **類型**：錯誤
* **嚴重度**：重大
* **始自**：2019.6.0 版本

複雜專案中經常出現的一個問題是多次設定同一個 OSGi 元件。此問題會產生模稜兩可的結果，無法確定可套用哪種設定。此規則為「執行模式感知」，因為它只會識別在同一執行模式或多個執行模式組合中多次設定相同元件的問題。

>[!NOTE]
>
>此規則會在多個套件中定義相同路徑的相同設定時造成問題，包括相同套件在建置套件的整體清單中重複的情況。
>
>例如，如果組建產生名為 `com.myco:com.myco.ui.apps` 和 `com.myco:com.myco.all` 的套件，其中 `com.myco:com.myco.all` 嵌入了 `com.myco:com.myco.ui.apps`，則 `com.myco:com.myco.ui.apps` 中的所有設定都會回報為重複專案。
>
>一般而言，此情況是不遵循[內容套件結構指導方針](/help/implementing/developing/introduction/aem-project-content-package-structure.md)的情況。 在此範例中，封裝`com.myco:com.myco.ui.apps`缺少`<cloudManagerTarget>none</cloudManagerTarget>`屬性。

#### 不符合規範的程式碼 {#non-compliant-code-osgi}

```text
+ apps
  + projectA
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
  + projectB
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

#### 符合規範的程式碼 {#compliant-code-osgi}

```text
+ apps
  + shared-config
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

### 設定和安裝資料夾應只包含 OSGi 節點 {#oakpal-config-install}

* **索引碼碼**：ConfigAndInstallShouldOnlyContainOsgiNodes
* **類型**：錯誤
* **嚴重度**：重大
* **始自**：2019.6.0 版本

基於安全性理由，包含 `/config/` 和 `/install/` 的路徑只有 Experience Manager 中的管理員使用者可讀取，並且僅能用於 OSGi 設定和 OSGi 套裝。將其他型別的內容放在包含這些區段的路徑下，會導致應用程式行為在管理員使用者和非管理員使用者之間無意間有所不同。

一個常見問題是在元件對話框中或在為內嵌編輯指定 RTF 文字編輯器設定時會使用名為 `config` 的節點。若要解決此問題，應將違規節點重新命名為合規名稱。對於 RTF 文字編輯器設定，請使用 `configPath` 屬性 (在 `cq:inplaceEditing` 節點上) 來指定新位置。

#### 不符合規範的程式碼 {#non-compliant-code-config-install}

```text
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    + config [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

#### 符合規範的程式碼 {#compliant-code-config-install}

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

類似於[套件不應包含重複的OSGi設定規則](#oakpal-package-osgi)，這種情況是複雜專案中常見的問題，其中相同的節點路徑會由多個單獨的內容套件寫入。 雖然使用內容套件相依性可以確保結果一致，但最好還是完全避免重疊。

### 預設的撰寫模式不應該是傳統UI {#oakpal-default-authoring}

* **索引碼**：ClassicUIAuthoringMode
* **型別**： `Code Smell`/Cloud Service相容性
* **嚴重度**：輕微
* **始自**：2020.5.0 版本

OSGi 設定 `com.day.cq.wcm.core.impl.AuthoringUIModeServiceImpl` 會定義 Experience Manager 中的預設撰寫模式。由於從 Experience Manager 6.4 起，Classic UI 就已被取代，若將預設的撰寫模式設定為 Classic UI，會產生問題。

### 包含對話方塊的元件應該有Touch UI對話方塊 {#oakpal-components-dialogs}

* **索引碼**：ComponentWithOnlyClassicUIDialog
* **型別**： `Code Smell`/Cloud Service相容性
* **嚴重度**：輕微
* **始自**：2020.5.0 版本

有Classic UI對話方塊的Experience Manager元件應該隨時有相對應的Touch UI對話方塊。 兩者皆提供與Cloud Service部署模式相容的最佳撰寫體驗，不再支援Classic UI。 本規則可證實以下情境：

* 具有 Classic UI 對話框 (即 `dialog` 子節點) 的元件必須具有相對應的 Touch UI 對話框 (即 `cq:dialog` 子節點)。
* 具有 Classic UI 設計對話框 (即 `design_dialog` 節點) 的元件必須具有相對應的 Touch UI 對話框 (即 `cq:design_dialog` 子節點)。
* 同時具有 Classic UI 對話框以及 Classic UI 設計對話框的元件必須同時有相對應的 Touch UI 對話框以及相對應的 Touch UI 設計對話框。

Experience Manager 現代化工具文件提供了有關如何將元件從 Classic UI 轉換為 Touch UI 的文件和工具。如需更多詳細資訊，請參閱 [Experience Manager 現代化工具文件](https://opensource.adobe.com/aem-modernize-tools/)。

### 套件不應該混合可變和不可變的內容 {#oakpal-packages-immutable}

* **索引碼**：ImmutableMutableMixedPackage
* **型別**： `Code Smell`/Cloud Service相容性
* **嚴重度**：輕微
* **始自**：2020.5.0 版本

要與雲端服務部署模式相容，個別內容套件必須包含存放庫不可變區域 (`/apps` 和 `/libs`) 或可變區域 (不在 `/apps` 或 `/libs` 中的所有內容) 的內容，但不能同時包含兩者。例如，同時包含`/apps/myco/components/text`和`/etc/clientlibs/myco`的套件與Cloud Service不相容，並會導致需通報的問題。

>[!NOTE]
>
>規則[客戶套件不應在libs](#oakpal-customer-package)下建立或修改節點。

如需更多詳細資訊，請參閱 [Experience Manager 專案結構](/help/implementing/developing/introduction/aem-project-content-package-structure.md)。

### 不應使用反向複寫代理 {#oakpal-reverse-replication}

* **索引碼**：ReverseReplication
* **型別**： `Code Smell`/Cloud Service相容性
* **嚴重度**：輕微
* **始自**：2020.5.0 版本

Cloud Service 部署中不支援反向複寫，如 Experience Manager as a Cloud Service 的[發行說明](/help/release-notes/aem-cloud-changes.md#replication-agents)中所述。

使用反向複寫的客戶應和 Adobe 聯絡，以取得替代解決方案。

### 已啟用 Proxy 的用戶端資料庫中所包含的資源應位於名為資源的資料夾中 {#oakpal-resources-proxy}

* **索引碼**：ClientlibProxyResource
* **類型**：錯誤
* **嚴重度**：輕微
* **始自**：2021.2.0 版本

Experience Manager 用戶端資料庫可能包含影像和字體之類的靜態資源。如檔案[使用前置處理器](/help/implementing/developing/introduction/clientlibs.md#using-preprocessors)中所述，在使用代理的使用者端程式庫時，這些靜態資源必須包含在名為`resources`的子資料夾中，才能在發佈執行個體上有效參考。

#### 不符合規範的程式碼 {#non-compliant-proxy-enabled}

```text
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + images
        + myimage.jpg
```

#### 符合規範的程式碼 {#compliant-proxy-enabled}

```tet
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + resources
        + myimage.jpg
```

### Cloud Service 的使用與工作流程不相容 {#oakpal-usage-cloud-service}

* **索引碼**：CloudServiceIncompatibleWorkflowProcess
* **類型**：錯誤
* **嚴重度**：重大
* **始自**：2021.2.0 版本

隨著在Adobe Experience Manager as a Cloud Service中轉換為資產微服務以進行資產處理，現在不支援內部部署和AMS版本中使用的多個工作流程流程。 其中許多工作流程也變得不必要。

[Experience Manager Assets as a Cloud Service GitHub 存放庫](https://github.com/adobe/aem-cloud-migration)中的移轉工具可在移轉至 Experience Manager as a Cloud Service 期間用於更新工作流程模式。

### 不建議使用靜態範本而支持可編輯範本 {#oakpal-static-template}

* **索引碼**：StaticTemplateUsage
* **類型**：`Code Smell`
* **嚴重度**：輕微
* **始自**：2021.2.0 版本

雖然靜態範本的使用歷來在 Experience Manager 專案中極為普遍，Adobe 建議使用可編輯範本，因為它們可提供最大的靈活度並支援靜態範本中不存在的附加功能。在[頁面範本](/help/implementing/developing/components/templates.md)文件中可找到更多資訊。

使用[Experience Manager現代化工具](https://opensource.adobe.com/aem-modernize-tools/)可將從靜態範本到可編輯範本的移轉大幅自動化。

### 不建議使用舊版基礎元件 {#oakpal-usage-legacy}

* **索引碼**：LegacyFoundationComponentUsage
* **類型**：`Code Smell`
* **嚴重度**：輕微
* **始自**：2021.2.0 版本

舊版基礎元件 (即 `/libs/foundation` 下的元件) 已在多個 Experience Manager 版本中被取代，以支援核心元件。不建議使用基礎元件作為自訂元件的基礎 (無論是透過覆蓋還是繼承)，並應轉換為相對應的核心元件。

[Experience Manager現代化工具](https://opensource.adobe.com/aem-modernize-tools/)可以促進此轉換。

### 僅使用受支援的執行模式名稱和順序 {#oakpal-supported-runmodes}

* **索引碼**：SupportedRunmode
* **類型**：`Code Smell`
* **嚴重度**：輕微
* **始自**：2021.2.0 版本

Experience Manager as a Cloud Service 對執行模式名稱實施嚴格的命名原則，並對這些執行模式要求嚴格的排序。支援的執行模式清單建立在檔案[部署到Experience Manager as a Cloud Service](/help/implementing/deploying/overview.md#runmodes)中，任何與此清單的偏離都會被識別為問題。

### 自訂搜尋索引定義節點必須是 `/oak:index` 的直接子節點 {#oakpal-custom-search}

* **索引碼**：OakIndexLocation
* **類型**：`Code Smell`
* **嚴重度**：輕微
* **始自**：2021.2.0 版本

Experience Manager as a Cloud Service 要求自訂搜尋索引定義 (即類型 `oak:QueryIndexDefinition` 的節點) 是 `/oak:index` 的直接子節點。必須移動其他位置中的索引才能和 Experience Manager as a Cloud Service 相容。如需有關搜尋索引的詳細資訊，可在[內容搜尋和索引](/help/operations/indexing.md)文件中找到。

### 自訂搜尋索引定義節點的 compatVersion 必須為 2 {#oakpal-custom-search-compatVersion}

* **索引碼**：IndexCompatVersion
* **類型**：`Code Smell`
* **嚴重度**：輕微
* **始自**：2021.2.0 版本

Experience Manager as a Cloud Service 要求自訂搜尋索引定義 (例如類型 `oak:QueryIndexDefinition` 的節點) 必須將 `compatVersion` 屬性設定為 `2`。Adobe Experience Manager as a Cloud Service不支援任何其他值。 如需搜尋索引的詳細資訊，請參閱[內容搜尋與索引](/help/operations/indexing.md)。

### 自訂搜尋索引定義節點的子孫節點必須屬於 `nt:unstructured ` 類型{#oakpal-descendent-nodes}

* **索引碼**：IndexDescendantNodeType
* **類型**：`Code Smell`
* **嚴重度**：輕微
* **始自**：2021.2.0 版本

當自訂搜尋索引定義節點具有無序子節點時，可能會出現難以解決的問題。若要避免出現這種情況，建議 `oak:QueryIndexDefinition` 節點的所有下階節點屬於 `nt:unstructured` 類型。

### 自訂搜尋索引定義節點必須包含名為 indexRules 並有子系的子節點 {#oakpal-custom-search-index}

* **索引碼**：IndexRulesNode
* **類型**：`Code Smell`
* **嚴重度**：輕微
* **始自**：2021.2.0 版本

正確定義的自訂搜尋索引定義節點必須包含一個名為`indexRules`的子節點，而該子節點又必須至少有一個子系。 以下連結中可找到更多資訊：[Oak 文件。](https://jackrabbit.apache.org/oak/docs/query/lucene.html)。

### 自訂搜尋索引定義節點必須遵循命名慣例 {#oakpal-custom-search-definitions}

* **索引碼**：IndexName
* **類型**：`Code Smell`
* **嚴重度**：輕微
* **始自**：2021.2.0 版本

Experience Manager as a Cloud Service 要求自訂搜尋索引定義 (即 `oak:QueryIndexDefinition` 類型的節點) 必須按照以下文件中說明的特定模式命名：[內容搜尋和索引](/help/operations/indexing.md)。

### 自訂搜尋索引定義節點必須使用索引類型 Lucene {#oakpal-index-type-lucene}

* **索引碼**：IndexType
* **類型**：錯誤
* **嚴重度**：阻斷因素
* **始自**：2021.2.0 版本 (在 2021.8.0 變更類型和嚴重性)

Experience Manager as a Cloud Service 要求自訂搜尋索引定義 (即類型 `oak:QueryIndexDefinition` 的節點) 必須具備 `type` 屬性，且值設定為 `lucene`。在移轉到 Experience Manager as a Cloud Service 之前，必須更新使用舊式索引類型的索引。如需詳細資訊，請參閱[內容搜尋和索引](/help/operations/indexing.md#how-to-use)。

### 自訂搜尋索引定義節點不得包含名為 seed 的屬性 {#oakpal-property-name-seed}

* **索引碼**：IndexSeedProperty
* **類型**：`Code Smell`
* **嚴重度**：輕微
* **始自**：2021.2.0 版本

Experience Manager as a Cloud Service 禁止自訂搜尋索引定義 (即 `oak:QueryIndexDefinition` 類型的節點) 包含名為 `seed` 的屬性。在移轉到 Experience Manager as a Cloud Service 之前，必須更新使用此屬性的索引。如需詳細資訊，請參閱[內容搜尋和索引](/help/operations/indexing.md#how-to-use)文件。

### 自訂搜尋索引定義節點不得包含名為 reindex 的屬性 {#oakpal-reindex-property}

* **索引碼**：IndexReindexProperty
* **類型**：`Code Smell`
* **嚴重度**：輕微
* **始自**：2021.2.0 版本

Experience Manager as a Cloud Service 禁止自訂搜尋索引定義 (即 `oak:QueryIndexDefinition` 類型的節點) 包含名為 `reindex` 的屬性。在移轉到Experience Manager as a之前，必須更新使用此屬性的索引
Cloud Service。 如需詳細資訊，請參閱[內容搜尋和索引](/help/operations/indexing.md#how-to-use)文件。

### 自訂DAM資產lucene節點不得指定`queryPaths` {#oakpal-damAssetLucene-queryPaths}

* **索引碼**：IndexDamAssetLucene
* **類型**：錯誤
* **嚴重度**：阻斷因素
* **始自**：2022.1.0 版本

#### 不符合規範的程式碼 {#non-compliant-code-damAssetLucene-queryPaths}

```text
+ oak:index
    + damAssetLucene-1-custom-1
      - async: [async, nrt]
      - evaluatePathRestrictions: true
      - includedPaths: [/content/dam]
      - queryPaths: [/content/dam]
      - type: lucene
      + tika
        + config.xml
```

#### 符合規範的程式碼 {#compliant-code-damAssetLucene-queryPaths}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async, nrt]
      - evaluatePathRestrictions: true
      - includedPaths: [/content/dam]
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### 如果自訂搜尋索引定義包含`compatVersion`，則必須將其設為2 {#oakpal-compatVersion}

* **索引碼**：IndexCompatVersion
* **類型**：`Code Smell`
* **嚴重度**：重大
* **始自**：2022.1.0 版本


### 指定`includedPaths`的索引節點也應該指定具有相同值的`queryPaths` {#oakpal-included-paths-without-query-paths}

* **索引鍵**： IndexIncludedPathsWithoutQueryPaths
* **類型**：`Code Smell`
* **嚴重度**：輕微
* **始自**：2023.1.0 版本

對於自訂索引，請以相同的值設定`includedPaths`和`queryPaths`。 若已指定其中一個，另一個必須符合它。 但是，`damAssetLucene`的索引（包括其自訂版本）有特殊情況。 對於這些情況，僅提供`includedPaths`。

### 在泛型節點型別上指定`nodeScopeIndex`的索引節點也應該指定`includedPaths`和`queryPaths` {#oakpal-full-text-on-generic-node-type}

* **Key**： IndexFulltextOnGenericType
* **類型**：`Code Smell`
* **嚴重度**：輕微
* **始自**：2023.1.0 版本

在`nodeScopeIndex`或`nt:unstructured`之類的「一般」節點型別上設定`nt:base`屬性時，您也必須指定`includedPaths`和`queryPaths`屬性。
節點型別`nt:base`可以視為「一般」，因為所有節點型別都繼承自它。 因此，在`nodeScopeIndex`上設定`nt:base`會使它索引存放庫中的所有節點。 同樣地，`nt:unstructured`也視為「一般」，因為存放庫中有許多節點屬於此型別。

#### 不符合規範的程式碼 {#non-compliant-code-full-text-on-generic-node-type}

```text
+ oak:index/acme.someIndex-custom-1
  - async: [async, nrt]
  - evaluatePathRestrictions: true
  - tags: [visualSimilaritySearch]
  - type: lucene
    + indexRules
      - jcr:primaryType: nt:unstructured
      + nt:base
        - jcr:primaryType: nt:unstructured
        + properties
          + acme.someIndex-custom-1
            - nodeScopeIndex: true
```

#### 符合規範的程式碼 {#compliant-code-full-text-on-generic-node-type}

```text
+ oak:index/acme.someIndex-custom-1
  - async: [async, nrt]
  - evaluatePathRestrictions: true
  - tags: [visualSimilaritySearch]
  - type: lucene
  - includedPaths: ["/content/dam/"] 
  - queryPaths: ["/content/dam/"]
    + indexRules
      - jcr:primaryType: nt:unstructured
      + nt:base
        - jcr:primaryType: nt:unstructured
        + properties
          + acme.someIndex-custom-1
            - nodeScopeIndex: true
```

### 不應覆寫查詢引擎的queryLimitReads屬性 {#oakpal-query-limit-reads}

* **索引鍵**： OverrideOfQueryLimitReads
* **類型**：`Code Smell`
* **嚴重度**：輕微
* **始自**：2023.1.0 版本

覆寫預設值可能會導致頁面讀取速度緩慢，尤其是在新增更多內容時。

### 相同索引的多個作用中版本 {#oakpal-multiple-active-versions}

* **索引鍵**： IndexDetectMultipleActiveVersionsOfSameIndex
* **類型**：`Code Smell`
* **嚴重度**：輕微
* **始自**：2023.1.0 版本

#### 不符合規範的程式碼 {#non-compliant-code-multiple-active-versions}

```text
+ oak:index
  + damAssetLucene-1-custom-1
    ...
  + damAssetLucene-1-custom-2
    ...
  + damAssetLucene-1-custom-3
    ...
```

#### 符合規範的程式碼 {#compliant-code-multiple-active-versions}

```text
+ damAssetLucene-1-custom-3
    ...
```


### 完整自訂索引定義的名稱應符合官方方針 {#oakpal-fully-custom-index-name}

* **Key**： IndexValidFullyCustomName
* **類型**：`Code Smell`
* **嚴重度**：輕微
* **始自**：2023.1.0 版本

完整自訂索引名稱的預期模式是： `[prefix].[indexName]-custom-[version]`。 如需詳細資訊，請參閱檔案[內容搜尋與索引](/help/operations/indexing.md)。

### 具有相同索引定義中不同分析值的相同屬性 {#oakpal-same-property-different-analyzed-values}

#### 不符合規範的程式碼 {#non-compliant-code-same-property-different-analyzed-values}

```text
+ indexRules
  + dam:Asset
    + properties
      + status
        - name: status
        - analyzed: true
  + dam:cfVariationNode
    + properties
      + status
        - name: status
```

#### 符合規範的程式碼 {#compliant-code-same-property-different-analyzed-values}

範例：

```text
+ indexRules
  + dam:Asset
    + properties
      + status
        - name: status
        - analyzed: true
  + dam:cfVariationNode
    + properties
      + status
        - name: status
        - analyzed: true
```

範例：

```text
+ indexRules
  + dam:Asset
    + properties
      + status
        - name: status
  + dam:cfVariationNode
    + properties
      + status
        - name: status
        - analyzed: true
```

如果未明確設定分析的屬性，其預設值為false。

### 標籤屬性 {#tags-property}

* **Key**： IndexHasValidTagsProperty
* **類型**：`Code Smell`
* **嚴重度**：輕微
* **始自**：2023.1.0 版本

對於特定索引，請確定您保留標籤屬性及其目前值。 雖然可以將新值新增到標籤屬性，但刪除任何現有值（或完全刪除屬性）可能會導致意外結果。

### 索引定義節點不得部署在 UI 內容套件中 {#oakpal-ui-content-package}

* **金鑰**：IndexNotUnderUIContent
* **類型**：改善
* **嚴重度**：輕微
* **始自**：2024.6.0 版本

AEM Cloud Service 禁止將自訂搜尋索引定義 (`oak:QueryIndexDefinition` 類型的節點) 部署在 UI 內容套件中。

>[!WARNING]
>
>您應儘快解決此問題，因為它可能會導致從[Cloud Manager 2024年8月發行版本](/help/implementing/cloud-manager/release-notes/current.md)開始的管道失敗。

### 型別damAssetLucene的自訂全文檢索索引定義必須正確加上前置詞「damAssetLucene」 {#oakpal-dam-asset-lucene}

* **金鑰**：CustomFulltextIndexesOfTheDmAssetCheck
* **型別**：改進專案
* **嚴重度**：輕微
* **始自**：2024.6.0 版本

AEM Cloud Service 禁止 `damAssetLucene` 類型的自訂全文索引定義使用 `damAssetLucene` 以外的任何內容作為前置詞。

>[!WARNING]
>
>從[Cloud Manager 2024年8月發行版本](/help/implementing/cloud-manager/release-notes/current.md)開始，此問題可能會導致管道失敗，請儘快解決。

### 索引定義節點不得包含同名的屬性 {#oakpal-index-property-name}

* **金鑰**：DuplicateNameProperty
* **類型**：改善
* **嚴重度**：輕微
* **始自**：2024.6.0 版本

AEM as a Cloud Service 禁止自訂搜尋索引定義 (即 `oak:QueryIndexDefinition` 類型的節點) 包含有同名的屬性。

>[!WARNING]
>
>從[Cloud Manager 2024年8月發行版本](/help/implementing/cloud-manager/release-notes/current.md)開始，此問題可能會導致管道失敗，請儘快解決。

### 禁止自訂某些現成可用的索引定義 {#oakpal-customizing-ootb-index}

* **金鑰**：RestrictIndexCustomization
* **類型**：改善
* **嚴重度**：輕微
* **始自**：2024.6.0 版本

AEM Cloud Service 禁止對以下 OOTB 索引進行未經授權的修改：

* `nodetypeLucene`
* `slingResourceResolver`
* `socialLucene`
* `appsLibsLucene`
* `authorizables`
* `pathReference`

>[!WARNING]
>
>從[Cloud Manager 2024年8月發行版本](/help/implementing/cloud-manager/release-notes/current.md)開始，此問題可能會導致管道失敗，請儘快解決。

### 分析器中代碼器的設定應以「tokenizer」名稱建立 {#oakpal-tokenizer}

* **金鑰**：AnalyzerTokenizerConfigCheck
* **類型**：改善
* **嚴重度**：輕微
* **始自**：2024.6.0 版本

AEM Cloud Service禁止在分析器中建立名稱不正確的代碼器。 tokenizer 應始終定義為 `tokenizer`。

>[!WARNING]
>
>從[Cloud Manager 2024年8月發行版本](/help/implementing/cloud-manager/release-notes/current.md)開始，此問題可能會導致管道失敗，請儘快解決。

### 索引定義的設定不應包含空格 {#oakpal-indexing-definitions-spaces}

* **索引鍵**：PathSpacesCheck
* **類型**：改善
* **嚴重度**：輕微
* **始自**：2024.7.0 版本

AEM Cloud Service 禁止建立屬性含空格的索引定義。
