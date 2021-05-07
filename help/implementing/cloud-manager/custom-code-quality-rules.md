---
title: 自訂代碼品質規則-Cloud Services
description: 自訂代碼品質規則-Cloud Services
exl-id: f40e5774-c76b-4c84-9d14-8e40ee6b775b
translation-type: tm+mt
source-git-commit: f6c700f82bc5a1a3edf05911a29a6e4d32dd3f72
workflow-type: tm+mt
source-wordcount: '3302'
ht-degree: 4%

---

# 自訂程式碼品質規則 {#custom-code-quality-rules}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_customcodequalityrules"
>title="自訂程式碼品質規則"
>abstract="本頁說明由Cloud Manager根據「工程」的最佳實務所建立的自訂程式碼品質規則AEM。"

本頁說明由Cloud Manager根據「工程」的最佳實務所建立的自訂程式碼品質規則AEM。

>[!NOTE]
>此處提供的程式碼範例僅供說明之用。 請參閱[概念](https://docs.sonarqube.org/7.4/user-guide/concepts/)以瞭解SonarQube概念和品質規則。

## SonarQube規則{#sonarqube-rules}

以下章節重點說明SonarQube規則：

### 請勿使用潛在的危險函式{#do-not-use-potentially-dangerous-functions}

**密鑰**:CQRules:CWE-676

**類型**:弱點

**嚴重性**:主修

**自**:2018.4.0版

方法 ***Thread.stop()*** 和 ***Thread.interrupt()*** 可產生難以重制的問題，在某些情況下，還可能產生安全漏洞。它們的使用應受到嚴密監控和驗證。總的來說，傳遞資訊是實現類似目標的更安全的方式。

#### 不符合代碼{#non-compliant-code}

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

#### 相容代碼{#compliant-code}

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

### 請勿使用可能由外部控制的格式字串{#do-not-use-format-strings-which-may-be-externally-controlled}

**密鑰**:CQRules:CWE-134

**類型**:弱點

**嚴重性**:主修

**自**:2018.4.0版

使用來自外部源（如請求參數或用戶生成的內容）的格式字串可以使應用程式暴露於拒絕服務攻擊。 在某些情況下，格式字串可能受到外部控制，但僅允許來自受信任來源。

#### 不符合代碼{#non-compliant-code-1}

```java
protected void doPost(SlingHttpServletRequest request, SlingHttpServletResponse response) {
  String messageFormat = request.getParameter("messageFormat");
  request.getResource().getValueMap().put("some property", String.format(messageFormat, "some text"));
  response.sendStatus(HttpServletResponse.SC_OK);
}
```

### HTTP請求應始終具有套接字和連接超時{#http-requests-should-always-have-socket-and-connect-timeouts}

**密鑰**:CQRules:ConnectionTimeoutMechanism

**類型**:錯誤

**嚴重性**:重要

**自**:2018.6.0版

當從應用程式內部執行HTTP請AEM求時，請務必確保已設定適當逾時，以避免不必要的執行緒耗用。 很遺憾，Java的預設HTTP客戶端(java.net.HttpUrlConnection)和常用的Apache HTTP Components客戶端的預設行為都是永不超時，因此必須明確設定超時。 此外，作為最佳實務，這些逾時秒數不應超過60秒。

#### 不符合代碼{#non-compliant-code-2}

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

#### 相容代碼{#compliant-code-1}

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

### 客戶{#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}不應實作或擴充以@ProviderType註解的產品API

**密鑰**:CQBP-84、CQBP-84-dependicies

**類型**:錯誤

**嚴重性**:重要

**自**:2018.7.0版

AEM API包含Java介面和類別，這些介面和類別僅能由自訂程式碼使用，但不能實作。例如，介面 *com.day.cq.wcm.api.Page* 僅由 ***AEM實作***。

將新方法添加到這些介面時，這些附加方法不會影響使用這些介面的現有代碼，因此，在這些介面中添加新方法會被視為向後相容。但是，如果自訂程 ***式碼實作*** 其中一個介面，該自訂程式碼會給客戶帶來向後相容性風險。

僅要由實施的介面（和類）AEM將用&#x200B;*org.osgi.annotation.versioning.ProviderType*(或者，在某些情況下，類似的舊式注釋&#x200B;*aQute.bnd.annotation.ProviderType*&#x200B;進行注釋。 此規則可識別自訂程式碼實作（或擴充類別）此類介面的情況。

#### 不符合代碼{#non-compliant-code-3}

```java
import com.day.cq.wcm.api.Page;

public class DontDoThis implements Page {
// implementation here
}
```

### ResourceResolver對象應始終關閉{#resourceresolver-objects-should-always-be-closed}

**密鑰**:CQRules:CQBP-72

**類型**:程式碼氣味

**嚴重性**:主修

**自**:2018.4.0版

從ResourceResolverFactory中獲取的ResourceResolver對象會佔用系統資源。 雖然在ResourceResolver不再使用時，有措施可回收這些資源，但通過調用close()方法明確關閉任何已開啟的ResourceResolver對象會更有效。

一個相對常見的誤解是，使用現有JCR會話建立的ResourceResolver對象不應顯式關閉，或者這樣做會關閉基礎的JCR會話。 不是這樣的——無論如何開啟資源解析器，都應在不再使用時關閉它。 由於ResourceResolver實施了可關閉介面，因此也可以使用try-with-resources語法，而不是顯式調用close()。

#### 不符合代碼{#non-compliant-code-4}

```java
public void dontDoThis(Session session) throws Exception {
  ResourceResolver resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object)session));
  // do some stuff with the resolver
}
```

#### 相容代碼{#compliant-code-2}

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

**密鑰**:CQRules:CQBP-75

**類型**:程式碼氣味

**嚴重性**:主修

**自**:2018.4.0版

如[Sling documentation](http://sling.apache.org/documentation/the-sling-engine/servlets.html)中所述，不建議依路徑來系結servlet。 路徑綁定的servlet不能使用標準JCR訪問控制，因此需要額外的安全性嚴格性。 建議您不要使用路徑綁定的servlet，而是在儲存庫中建立節點並按資源類型註冊servlet。

#### 不符合代碼{#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### 捕獲的異常應記錄或拋出，但不應同時記錄{#caught-exceptions-should-be-logged-or-thrown-but-not-both}

**密鑰**:CQRules:CQBP-44—CatchAndEitherLogOrThrow

**類型**:程式碼氣味

**嚴重性**:次要

**自**:2018.4.0版

一般而言，例外應只記錄一次。 多次記錄例外可能會造成混淆，因為不清楚發生例外的次數。 導致這種情況的最常見模式是記錄並拋出一個捕獲到的異常。

#### 不符合代碼{#non-compliant-code-6}

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

#### 相容代碼{#compliant-code-3}

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

### 請避免在日誌語句後面立即加上throw語句{#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

**密鑰**:CQRules:CQBP-44—ConcentilueLogAndThrow

**類型**:程式碼氣味

**嚴重性**:次要

**自**:2018.4.0版

另一個避免的常見模式是記錄訊息，然後立即擲回例外。 這通常表示異常消息將在日誌檔案中重複。

#### 不符合代碼{#non-compliant-code-7}

```java
public void dontDoThis() throws Exception {
  logger.error("something went wrong");
  throw new RuntimeException("something went wrong");
}
```

#### 相容代碼{#compliant-code-4}

```java
public void doThis() throws Exception {
  throw new RuntimeException("something went wrong");
}
```

### 在處理GET或HEAD請求{#avoid-logging-at-info-when-handling-get-or-head-requests}時，避免在INFO上登錄

**密鑰**:CQRules:CQBP-44—LogInfoInGetOrHeadRequests

**類型**:程式碼氣味

**嚴重性**:次要

一般而言，INFO記錄檔層級應用於區分重要動作，並依預設設定AEM為在INFO層級或以上記錄檔。 GET和HEAD方式只能是唯讀操作，因此不構成重要行動。 響應GET或HEAD請求而在INFO級別登錄可能會產生明顯的日誌雜訊，從而更難識別日誌檔案中的有用資訊。 處理GET或HEAD請求時，如果更深入的疑難排解資訊有幫助，則記錄應位於發生錯誤時的「警告」或「錯誤」層級，或位於「除錯」或「TRACE」層級。

>[!CAUTION]
>
>這不適用於每個請求的access.log類型記錄。

#### 不符合代碼{#non-compliant-code-8}

```java
public void doGet() throws Exception {
  logger.info("handling a request from the user");
}
```

#### 相容代碼{#compliant-code-5}

```java
public void doGet() throws Exception {
  logger.debug("handling a request from the user.");
}
```

### 請勿將Exception.getMessage()用作記錄語句{#do-not-use-exception-getmessage-as-the-first-parameter-of-a-logging-statement}的第一個參數

**密鑰**:CQRules:CQBP-44 - ExceptionGetMessageIsFirstLogParam

**類型**:程式碼氣味

**嚴重性**:次要

**自**:2018.4.0版

作為最佳做法，日誌消息應提供有關應用程式中發生異常的位置的上下文資訊。 雖然上下文也可以透過使用堆疊追蹤來判斷，但一般而言，記錄訊息會更容易讀取和瞭解。 因此，在記錄例外時，將例外消息用作日誌消息的做法是不好的——例外消息將包含出錯的內容，而日誌消息應用於告知日誌讀取器發生例外時應用程式正在執行什麼操作。 例外消息仍將記錄；指定您自己的訊息，讓記錄檔更容易理解。

#### 不符合代碼{#non-compliant-code-9}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error(e.getMessage(), e);
  }
}
```

#### 相容代碼{#compliant-code-6}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 登錄捕獲塊應位於WARN或ERROR級別{#logging-in-catch-blocks-should-be-at-the-warn-or-error-level}

**密鑰**:CQRules:CQBP-44—WrongLogLevelInCatchBlock

**類型**:程式碼氣味

**嚴重性**:次要

**自**:2018.4.0版

如名稱所示，在&#x200B;*exceptional*&#x200B;的情況下，應始終使用Java例外。 因此，在捕獲到異常時，務必確保日誌消息記錄在適當的級別- WARN或ERROR。 這可確保這些消息在日誌中正確顯示。

#### 不符合代碼{#non-compliant-code-10}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.debug(e.getMessage(), e);
  }
}
```

#### 相容代碼{#compliant-code-7}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 不將堆棧跟蹤打印到控制台{#do-not-print-stack-traces-to-the-console}

**密鑰**:CQRules:CQBP-44 - ExceptionPrintStackTrace

**類型**:程式碼氣味

**嚴重性**:次要

**自**:2018.4.0版

如前所述，瞭解日誌消息時，上下文至關重要。 使用Exception.printStackTrace()僅使&#x200B;****&#x200B;堆棧跟蹤輸出到標準錯誤流，從而丟失所有上下文。 此外，在多線程應用中，如AEM果使用該方法並行打印多個例外，其堆棧跡線可能重疊，從而產生明顯的混淆。 只應通過記錄框架記錄異常。

#### 不符合代碼{#non-compliant-code-11}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    e.printStackTrace();
  }
}
```

#### 相容代碼{#compliant-code-8}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 不輸出到「標準輸出」或「標準錯誤{#do-not-output-to-standard-output-or-standard-error}」

**密鑰**:CQRules:CQBP-44—LogLevelConsolePrinters

**類型**:程式碼氣味

**嚴重性**:次要

**自**:2018.4.0版

登入應AEM一律透過登入架構(SLF4J)進行。 直接輸出到標準輸出或標準錯誤流會丟失記錄框架提供的結構和上下文資訊，在某些情況下可能導致效能問題。

#### 不符合代碼{#non-compliant-code-12}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    System.err.println("Unable to do something");
  }
}
```

#### 相容代碼{#compliant-code-9}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 避免硬式編碼/apps和/libs路徑{#avoid-hardcoded-apps-and-libs-paths}

**密鑰**:CQRules:CQBP-71

**類型**:程式碼氣味

**嚴重性**:次要

**自**:2018.4.0版

一般而言，以/libs和/apps開頭的路徑不應硬式編碼為它們所參照的路徑，最常儲存為相對於Sling搜尋路徑的路徑（依預設會設為/libs,/apps）。 使用絕對路徑可能會帶來細微的缺陷，這些缺陷只會在項目生命週期的後期出現。

#### 不符合代碼{#non-compliant-code-13}

```java
public boolean dontDoThis(Resource resource) {
  return resource.isResourceType("/libs/foundation/components/text");
}
```

#### 相容代碼{#compliant-code-10}

```java
public void doThis(Resource resource) {
  return resource.isResourceType("foundation/components/text");
}
```

### Sling Scheduler Should Not Be Used {#sonarqube-sling-scheduler}

**密鑰**:CQRules:AMSCORE-554

**類型**:程式碼氣味/Cloud Service相容性

**嚴重性**:次要

**自**:2020.5.0版

Sling Scheduler不得用於需要保證執行的任務。 Sling Scheduled Jobs可確保執行，更適合叢集和非叢集環境。

請參閱[Apache Sling Eventing和Job Handling](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html)以進一步瞭解Sling Jobs如何在叢集環境中處理。

### 不AEM應使用已過時的API {#sonarqube-aem-deprecated}

**密鑰**:AMSCORE-553

**類型**:程式碼氣味/Cloud Service相容性

**嚴重性**:次要

**自**:2020.5.0版

APIAEM表面處於常數修訂之下，以識別不建議使用且因此被視為已過時的API。

在許多情況下，這些API會使用標準Java *@Deprecated*&#x200B;注釋來取代，如`squid:CallToDeprecatedMethod`所識別。

但是，有時API在上下文中已過時，但在其AEM他上下文中可能不再過時。 此規則可識別此第二類。

## OakPAL內容規則{#oakpal-rules}

請在Cloud Manager執行的OakPAL檢查下方尋找。

>[!NOTE]
>OakPAL是由合作夥伴(AEM2019年Rockstar North America的得獎者)開發的架構，可使用獨立的Oak資料庫來驗證內容套件。

### 客戶軟體包不應在/libs {#oakpal-customer-package}下建立或修改節點

**密鑰**:UnbandedPaths

**類型**:錯誤

**嚴重性**:封鎖程式

**自**:2019.6.0版

客戶應將內容存放庫中的/libs內容樹視為唯讀，這AEM是一種長期的最佳做法。 修改&#x200B;*/libs*&#x200B;下的節點和屬性會對主要和次要更新造成重大風險。 對&#x200B;*/libs*&#x200B;的修改僅應通過正式渠道Adobe。

### 軟體包不應包含重複的OSGi配置{#oakpal-package-osgi}

**密鑰**:DuplicateOsgiConfigurations

**類型**:錯誤

**嚴重性**:主修

**自**:2019.6.0版

在複雜項目上發生的常見問題是，同一個OSGi元件被多次配置。 這就產生了關於哪些配置可操作的模糊性。 此規則是「執行模式感知」，因為它只會識別在相同執行模式（或執行模式組合）中多次設定相同元件的問題。

>[!NOTE]
>此規則將產生在多個軟體包中定義相同配置（位於同一路徑）的問題，包括在構建的軟體包的整個清單中複製相同軟體包的情況。 例如，如果構建版本生成名為`com.myco:com.myco.ui.apps`和`com.myco:com.myco.all`的包，其中`com.myco:com.myco.all`嵌入`com.myco:com.myco.ui.apps`，則`com.myco:com.myco.ui.apps`內的所有配置都將報告為重複的。 這通常是不遵循[內容封裝結構准則](/help/implementing/developing/introduction/aem-project-content-package-structure.md)的情況；在此特定示例中，包`com.myco:com.myco.ui.apps`缺少`<cloudManagerTarget>none</cloudManagerTarget>`屬性。

#### 不符合代碼{#non-compliant-code-osgi}

```+ apps
  + projectA
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
  + projectB
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

#### 相容代碼{#compliant-code-osgi}

```+ apps
  + shared-config
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

### 配置和安裝資料夾應僅包含OSGi節點{#oakpal-config-install}

**密鑰**:ConfigAndInstallShouldOnlyContainOsgiNodes

**類型**:錯誤

**嚴重性**:主修

**自**:2019.6.0版

出於安全原因，包含&#x200B;*/config/和/install/*&#x200B;的路徑只能由中的管理用戶讀取AEM，並且應僅用於OSGi配置和OSGi捆綁包。 將其他類型的內容置於包含這些區段的路徑下，會導致應用程式行為在管理使用者與非管理使用者之間無意間有所不同。

常見的問題是，在元件對話框中或指定用於內嵌編輯的富格文本編輯器配置時，使用名為`config`的節點。 要解決此問題，應將違規節點更名為相容名稱。 對於富格文本編輯器配置，請使用`cq:inplaceEditing`節點上的`configPath`屬性來指定新位置。

#### 不符合代碼{#non-compliant-code-config-install}

```
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    + config [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

#### 相容代碼{#compliant-code-config-install}

```
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    ./configPath = inplaceEditingConfig (String)
    + inplaceEditingConfig [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

### 軟體包不應重疊{#oakpal-no-overlap}

**密鑰**:PackageOverlaps

**類型**:錯誤

**嚴重性**:主修

**自**:2019.6.0版

與&#x200B;*軟體包不應包含重複的OSGi配置*&#x200B;類似，在由多個獨立內容軟體包寫入相同節點路徑的複雜項目中，這是一個常見問題。 雖然使用內容封裝相依性可確保結果一致，但最好避免完全重疊。

### 預設的編寫模式不應是Classic UI {#oakpal-default-authoring}

**密鑰**:ClassicUIAuthoringMode

**類型**:程式碼氣味/Cloud Service相容性

**嚴重性**:次要

**自**:2020.5.0版

OSGi配置`com.day.cq.wcm.core.impl.AuthoringUIModeServiceImpl`定義了中的預設編寫模AEM式。 自6.4以來，Classic UI已不再支援AEM，現在當預設編寫模式設定為Classic UI時，會引發問題。

### 具有對話框的元件應具有觸摸UI對話框{#oakpal-components-dialogs}

**密鑰**:ComponentWithOnlyClassicUIDialog

**類型**:程式碼氣味/Cloud Service相容性

**嚴重性**:次要

**自**:2020.5.0版

具AEM有Classic UI對話方塊的元件應一律具有對應的Touch UI對話方塊，以提供最佳的製作體驗，並與不支援Classic UI的Cloud Service部署模型相容。 此規則會驗證下列案例：

* 具有Classic UI對話框的元件（即，對話子節點）必須具有相應的Touch UI對話框（即`cq:dialog`子節點）。
* 具有Classic UI設計對話框的元件（即design_dialog節點）必須具有相應的Touch UI設計對話框（即`cq:design_dialog`子節點）。
* 具有「傳統型」UI對話框和「傳統型」UI設計對話框的元件必須具有相應的「觸控型」UI對話框和相應的「觸控型」UI設計對話框。

「現代化工AEM具」檔案提供如何將元件從傳統UI轉換為Touch UI的檔案和工具。 如需詳細資訊，請參AEM閱「現代化工具」。[](https://opensource.adobe.com/aem-modernize-tools/pages/tools.html)

### 軟體包不應混合可變內容和不可變內容{#oakpal-packages-immutable}

**密鑰**:ImmutableMutableMixedPackage

**類型**:程式碼氣味/Cloud Service相容性

**嚴重性**:次要

**自**:2020.5.0版

為了與Cloud Service部署模型相容，單個內容包必須包含儲存庫不可變區域的內容（即`/apps and /libs, although /libs`不應由客戶代碼修改，並將導致單獨違規）或可變區域（即，其他所有內容），但不能同時包含兩者。 例如，同時包含`/apps/myco/components/text and /etc/clientlibs/myco`的套件與Cloud Service不相容，且會造成問題報告。

如需詳細資訊，請參AEM閱[專案結構](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)。

### 不應使用反向複製代理{#oakpal-reverse-replication}

**密鑰**:反向複製

**類型**:程式碼氣味/Cloud Service相容性

**嚴重性**:次要

**自**:2020.5.0版

在Cloud Service部署中不支援反向複製，如[發行說明中所述：刪除複製代理](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/release-notes/aem-cloud-changes.html#replication-agents)。

使用反向複製的客戶應與Adobe聯繫，以獲得其他解決方案。

### OakPAL —— 啟用Proxy的用戶端程式庫中包含的資源應位於名為resources {#oakpal-resources-proxy}的資料夾中

**密鑰**:ClientlibProxyResource

**類型**:錯誤

**嚴重性**:次要

**自**:2021.2.0版

用戶AEM端程式庫可能包含靜態資源，例如影像和字型。 如[使用預處理器](/help/implementing/developing/introduction/clientlibs.md#using-preprocessors)中所述，在使用預處理器客戶端庫時，這些靜態資源必須包含在名為resources的子資料夾中，以便在發佈實例上有效地引用。

#### 不符合代碼{#non-compliant-proxy-enabled}

```
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + images
        + myimage.jpg
```

#### 相容代碼{#compliant-proxy-enabled}

```
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + resources
        + myimage.jpg
```

### OakPAL -Cloud Service不相容工作流程的使用{#oakpal-usage-cloud-service}

**密鑰**:CloudServiceIncomplativeWorkflowProcess

**類型**:錯誤

**嚴重性**:主修

**自**:2021.2.0版

隨著移至資產微服務以進行資產處理的AEMCloud Service，在內部部署和AMS版本中使用的數個工作流程程式變成不支援AEM或不必要。 位於[aem-cloud-migration](https://github.com/adobe/aem-cloud-migration)的移轉工具可用於在Cloud Service移轉期間更新工作AEM流程模型。

### OakPAL —— 不建議使用靜態範本，而改用可編輯的範本{#oakpal-static-template}

**密鑰**:StaticTemplateUsage

**類型**:程式碼氣味

**嚴重性**:次要

**自**:2021.2.0版

雖然靜態範本的使用在專案中很常見，但強烈建議使用可編輯AEM的範本，因為這些範本可提供最大的彈性，並支援靜態範本中未顯示的其他功能。 如需詳細資訊，請參閱[頁面範本。](/help/implementing/developing/components/templates.md) 從靜態範本到可編輯範本的移轉，可使用「現代化工具」 [AEM大幅自動化](https://opensource.adobe.com/aem-modernize-tools/)。

### OakPAL —— 不建議使用舊版基礎元件{#oakpal-usage-legacy}

**密鑰**:LegacyFoundationComponentUsage

**類型**:程式碼氣味

**嚴重性**:次要

**自**:2021.2.0版

在多個版本中，支援WCM核心元件的舊式基礎元件（即`/libs/foundation`下的元件）已AEM被淘汰。 不建議使用舊式基礎元件做為自訂元件的基礎——不論是透過覆蓋或繼承——並應轉換為對應的核心元件。 [現代化工具](https://opensource.adobe.com/aem-modernize-tools/)AEM可促進這種轉換。

### OakPAL —— 應使用{#oakpal-supported-runmodes}僅支援的執行模式名稱和順序

**密鑰**:支援的執行模式

**類型**:程式碼氣味

**嚴重性**:次要

**自**:2021.2.0版

AEMCloud Service會針對執行模式名稱執行嚴格的命名原則，並對這些執行模式執行嚴格的排序。 支援的執行模式清單可在[Runmodes](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#runmodes)上找到，任何偏離此模式的情況都會視為問題。

### OakPAL —— 自訂搜尋索引定義節點必須是/oak:index {#oakpal-custom-search}的直接子項

**密鑰**:OakIndexLocation

**類型**:程式碼氣味

**嚴重性**:次要

**自**:2021.2.0版

AEMCloud Service要求自訂搜尋索引定義（即oak:QueryIndexDefinition類型的節點）是`/oak:index`的直接子節點。 其他位置的索引必須移動，才能與AEMCloud Service相容。 有關搜索索引的詳細資訊，請參閱[內容搜索和索引](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en)。

### OakPAL —— 自訂搜尋索引定義節點必須有2 {#oakpal-custom-search-compatVersion}的compat版本

**密鑰**:IndexCompatVersion

**類型**:程式碼氣味

**嚴重性**:次要

**自**:2021.2.0版

AEMCloud Service要求自訂搜尋索引定義（即oak:QueryIndexDefinition類型的節點）必須將compatVersion屬性設為2。 Cloud Service不支援任何其他值AEM。 有關搜索索引的詳細資訊，請參閱[內容搜索和索引](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en)。

### OakPAL —— 自定義搜索索引定義節點的後代節點必須為Nt:Unstructured {#oakpal-descendent-nodes}類型

**密鑰**:IndexDescendantNodeType

**類型**:程式碼氣味

**嚴重性**:次要

**自**:2021.2.0版

當自訂搜尋索引定義節點具有無序的子節點時，可能會發生難以疑難排解的問題。 為避免這些情況，建議`oak:QueryIndexDefinition`節點的所有子節點都為nt:unstructured類型。

### OakPAL —— 自訂搜尋索引定義節點必須包含名為indexRules的子節點，該子節點具有{#oakpal-custom-search-index}子節點

**密鑰**:IndexRulesNode

**類型**:程式碼氣味

**嚴重性**:次要

**自**:2021.2.0版

正確定義的自定義搜索索引定義節點必須包含名為indexRules的子節點，而該子節點必須至少有一個子節點。 如需詳細資訊，請參閱[Oak Documentation](https://jackrabbit.apache.org/oak/docs/query/lucene.html)。

### OakPAL —— 自訂搜尋索引定義節點必須遵循命名慣例{#oakpal-custom-search-definitions}

**密鑰**:IndexName

**類型**:程式碼氣味

**嚴重性**:次要

**自**:2021.2.0版

AEMCloud Service要求自定義搜索索引定義（即，`oak:QueryIndexDefinition`類型的節點）必須按照[內容搜索和索引](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#how-to-use)中描述的特定模式命名。

### OakPAL —— 自訂搜尋索引定義節點必須使用索引類型lucene {#oakpal-index-type-lucene}

**密鑰**:IndexType

**類型**:程式碼氣味

**嚴重性**:次要

**自**:2021.2.0版

AEMCloud Service要求自訂搜尋索引定義（即oak:QueryIndexDefinition類型的節點）具有type屬性，其值設定為&#x200B;**lucene**。 使用舊索引類型的索引必須在遷移到Cloud Service之前AEM更新。 如需詳細資訊，請參閱[內容搜尋與索引](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#how-to-use)。

### OakPAL —— 自訂搜尋索引定義節點不得包含名為seed {#oakpal-property-name-seed}的屬性

**密鑰**:IndexSeedProperty

**類型**:程式碼氣味

**嚴重性**:次要

**自**:2021.2.0版

AEMCloud Service禁止自定義搜索索引定義（即`oak:QueryIndexDefinition`類型的節點）包含名為seed的屬性。 使用此屬性進行索引必須在遷移到Cloud Service之AEM前更新。 如需詳細資訊，請參閱[內容搜尋與索引](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#how-to-use)。

### OakPAL —— 自訂搜尋索引定義節點不得包含名為reindex {#oakpal-reindex-property}的屬性

**密鑰**:IndexReindexProperty

**類型**:程式碼氣味

**嚴重性**:次要

**自**:2021.2.0版

AEMCloud Service禁止自定義搜索索引定義（即`oak:QueryIndexDefinition`類型的節點）包含名為reindex的屬性。 使用此屬性進行索引必須在遷移到Cloud Service之AEM前更新。 如需詳細資訊，請參閱[內容搜尋與索引](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#how-to-use)。
