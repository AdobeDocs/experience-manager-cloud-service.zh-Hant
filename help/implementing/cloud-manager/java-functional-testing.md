---
title: Java &amp；trade；功能測試
description: 瞭解如何為AEM as a Cloud Service編寫Java &amp；trade；功能測試
exl-id: e014b8ad-ac9f-446c-bee8-adf05a6b4d70
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 77%

---


# Java™ 功能測試

了解如何針對 AEM as a Cloud Service 編寫 Java™ 功能測試

## 功能測試快速入門 {#getting-started-functional-tests}

在 Cloud Manager 中建立新程式碼存放庫後，系婌將自動建立一個包含範例測試案例的 `it.tests` 資料夾。

>[!NOTE]
>
>如果您的存放庫是在 Cloud Manager 自動建立 `it.tests` 資料夾之前所建立，您還可以使用 [AEM 專案原型產生最新版本](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/it.tests)。

獲得 `it.tests` 資料夾的內容後，您可以將其用作自己測試的基礎，然後：

1. [開發您的測試案例](#writing-functional-tests)。
1. [在本機執行測試](#local-test-execution)。
1. 將您的程式碼提交到 Cloud Manager 存放庫並執行 Cloud Manager 管道。

## 寫入自訂功能測試 {#writing-functional-tests}

Adobe 用於編寫產品功能測試的工具也可用於編寫您的自訂功能測試。使用 GitHub 中的[產品功能測試](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke)作為寫入測試的範例。

自訂功能測試的程式碼是位於專案 `it.tests` 資料夾中的 Java™ 程式碼。它應該產生一個包含所有功能測試的 JAR。如果建置產生多個測試 JAR，則無法確定要選擇哪個 JAR。如果產生零個測試 JAR，則測試步驟預設透過。如需測試範例，請參閱[AEM專案原型](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/it.tests)。

這些測試會在 Adobe 維護的測試基礎結構上執行，包括至少兩個編寫執行個體、兩個發佈執行個體和一個 Dispatcher 設定。此設定代表您的自訂功能測試針對整個 AEM 堆疊執行。

### 功能測試結構 {#functional-tests-structure}

自訂功能測試必須封裝為單獨的 JAR 檔案，該檔案由與要部署到 AEM 的成品相同的 Maven 組建產生。通常，此組建是一個單獨的 Maven 模組。產生的 JAR 檔案必須包含所有必要的相依性，通常使用 `maven-assembly-plugin` 和 `jar-with-dependencies` 描述項建立。

此外，JAR 必須將 `Cloud-Manager-TestType` 資訊清單標頭設為 `integration-test`。

以下為 `maven-assembly-plugin` 的設定範例。

```XML
<build>
    <plugins>
        <!-- Create self-contained jar with dependencies -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-assembly-plugin</artifactId>
            <version>3.1.0</version>
            <configuration>
                <descriptorRefs>
                    <descriptorRef>jar-with-dependencies</descriptorRef>
                </descriptorRefs>
                <archive>
                    <manifestEntries>
                        <Cloud-Manager-TestType>integration-test</Cloud-Manager-TestType>
                    </manifestEntries>
                </archive>
            </configuration>
            <executions>
                <execution>
                    <id>make-assembly</id>
                    <phase>package</phase>
                    <goals>
                        <goal>single</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```

在這個 JAR 檔案中，要執行的實際測試的類別名稱必須以 `IT` 結尾。

例如，將執行名為 `com.myco.tests.aem.it.ExampleIT` 的類別，但不會執行名為 `com.myco.tests.aem.it.ExampleTest` 的類別。

此外，要從程式碼掃描的覆蓋檢查中排除測試程式碼，測試程式碼必須位於名為`it` 的套件之下 (覆蓋排除篩選是`**/it/**/*.java`)。

測試類別必須是一般的 JUnit 測試。測試基礎結構的設計和設定與 `aem-testing-clients` 測試庫使用的慣例相容。鼓勵開發人員使用此程式庫並遵循其最佳實務。

如需更多詳細資訊，請參閱 [`aem-testing-clients`GitHub 存放庫](https://github.com/adobe/aem-testing-clients)。

>[!TIP]
>
>[觀看此影片](https://www.youtube.com/watch?v=yJX6r3xRLHU)，了解如何使用自訂功能測試來提高您對 CI/CD 管道的信心。

### 必備條件 {#prerequisites}

1. Cloud Manager 中的測試是透過技術管理員使用者來執行。

>[!NOTE]
>
>若要從本機電腦執行功能測試，請建立一個具備類似管理員權限的使用者來達到相同的行為。

1. 用於功能測試的容器化基礎架構受以下界限限制：

| 類型 | 值 | 說明 |
|----------------------|-------|--------------------------------------------------------------------|
| CPU | 0.5 | 每次測試執行保留的 CPU 時間量 |
| 記憶體 | 0.5Gi | 分配給測試的記憶體數量，其值以 gibibyte 為單位 |
| 逾時 | 30m | 測試停止的時間限制。 |
| 建議的持續時間 | 15m | Adobe建議撰寫測試時，不要超過這個時間。 |

#### 相依性

* aem-cloud-testing-clients：

即將變更用於執行功能測試的容器化基礎結構，需要將自訂功能測試中的[aem-cloud-testing-clients](https://github.com/adobe/aem-testing-clients)程式庫更新為&#x200B;**1.2.1**&#x200B;或更新版本。 請確定您的`it.tests/pom.xml`檔案中的相依性已相應更新。

```
<dependency>
   <groupId>com.adobe.cq</groupId>
   <artifactId>aem-cloud-testing-clients</artifactId>
   <version>1.2.1</version>
</dependency>
```

>[!NOTE]
>
>此變更需要在 2024 年 4 月 6 日之前執行。
>如果未更新相依性程式庫，可能會在「自訂功能測試」步驟導致管道失敗。

### 本機測試執行 {#local-test-execution}

在 Cloud Manager 管道啟用功能測試之前，建議在本機使用 [AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) 或實際的 AEM as a Cloud Service 執行個體中執行功能測試。

#### 在 IDE 中執行 {#running-in-an-ide}

由於測試類別是JUnit測試，因此它們可以從主流的Java™IDE （如Eclipse、IntelliJ和NetBeans）執行。 因為產品功能測試和自訂功能測試都基於相同的技術，所以兩者都可以透過將產品測試複製到自訂測試中，以在本機執行。

但是，在執行這些測試時，需要設定 `aem-testing-clients` (和底層 Sling 測試用戶端) 程式庫應有的各種系統屬性。

系統屬性如下。

| 屬性 | 說明 | 範例 |
|-------------------------------------|------------------------------------------------------------------|-------------------------|
| `sling.it.instances` | 符合雲端服務的執行個體數目應設為`2`。 | `2` |
| `sling.it.instance.url.1` | 設定為作者URL。 | `http://localhost:4502` |
| `sling.it.instance.runmode.1` | 第一個執行個體的執行模式。 設定為`author`。 | `author` |
| `sling.it.instance.adminUser.1` | 設定為作者管理員使用者。 | `admin` |
| `sling.it.instance.adminPassword.1` | 設定為作者管理密碼。 |                         |
| `sling.it.instance.url.2` | 設定為發佈URL。 | `http://localhost:4503` |
| `sling.it.instance.runmode.2` | 第二個執行個體的執行模式。 設定為`publish`。 | `publish` |
| `sling.it.instance.adminUser.2` | 設定為發佈管理員使用者。 | `admin` |
| `sling.it.instance.adminPassword.2` | 設定為發佈管理員密碼。 |                         |

#### 使用 Maven 執行所有測試 {#using-maven}

1. 打開 shell 並瀏覽至存放庫中的 `it.tests` 資料夾。

1. 執行以下命令，提供必要的參數以使用 Maven 啟動測試。

```shell
mvn verify -Plocal \
    -Dit.author.url=https://author-<program-id>-<environment-id>.adobeaemcloud.com \
    -Dit.author.user=<user> \
    -Dit.author.password=<password> \
    -Dit.publish.url=https://publish-<program-id>-<environment-id>.adobeaemcloud.com \
    -Dit.publish.user=<user> \
    -Dit.publish.password=<password>
```
