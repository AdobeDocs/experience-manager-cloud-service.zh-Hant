---
title: 功能測試
description: 了解內建在 AEM as a Cloud Service 部署流程中的三種不同類型的功能測試，以確保計劃碼的品質和可靠性。
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: ht
source-wordcount: '898'
ht-degree: 100%

---


# 功能測試 {#functional-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="功能測試"
>abstract="了解內置在 AEM as a Cloud Service 部署過程中的三種不同類型的功能測試，以確保計劃碼的品質和可靠性。"

了解內建在 [AEM as a Cloud Service 部署流程](/help/implementing/cloud-manager/deploy-code.md)中的三種不同類型的功能測試，以確保計劃碼的品質和可靠性。

## 總覽 {#overview}

AEM as a Cloud Service 中有三種不同類型的功能測試。

* [產品功能測試](#product-functional-testing)
* [自訂功能測試](#custom-functional-testing)
* [自訂 UI 測試](#custom-ui-testing)

對於所有功能測試，作為[部署流程](/help/implementing/cloud-manager/deploy-code.md)的一部分，可以使用組建總覽畫面中的&#x200B;**下載組建記錄**&#x200B;按鈕，將測試的詳細結果下載為 `.zip` 檔案。

這些記錄不包括實際 AEM 執行時進程的記錄。若要存取這些記錄，請參閱[存取和管理記錄](/help/implementing/cloud-manager/manage-logs.md)文件以了解詳細資訊。

產品功能測試和範例自訂功能測試均以 [AEM 測試用戶端](https://github.com/adobe/aem-testing-clients)為基礎。

## 產品功能測試 {#product-functional-testing}

產品功能測試是 AEM 中核心功能 (例如製作和複製任務) 的一組穩定 HTTP 整合測試 (IT)。這些測試由 Adobe 維護，旨在防止自訂應用計劃計劃碼變更而破壞核心功能時進行部署。

每當您將新計劃碼部署到 Cloud Manager 時，都會自動執行產品功能測試，且不能跳過。

產品功能測試會作為開放原始碼專案進行維護。如需詳細資訊，請參閱 GitHub 中的[產品功能測試](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke)。

## 自訂功能測試 {#custom-functional-testing}

雖然產品功能測試由 Adobe 定義，但您可以為自己的應用計劃編寫自己的品質測試。這將作為自訂功能測試作為生產管道的一部分執行，以確保您應用計劃的品質。

自訂功能測試會針對自訂計劃碼部署和推送升級執行，這對於編寫良好的功能測試，以防止 AEM 計劃碼變更而破壞應用計劃計劃碼尤為重要。自訂功能測試步驟一律存在且不能跳過。

### 寫入自訂功能測試 {#writing-functional-tests}

Adobe 用於編寫產品功能測試的工具也可用於編寫您的自訂功能測試。使用 GitHub 中的[產品功能測試](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke)作為寫入測試的範例。

自訂功能測試的計劃碼是位於專案 `it.tests` 檔案夾中的 Java 計劃碼。它應該產生一個包含所有功能測試的 JAR。如果建置產生多個測試 JAR，則無法確定要選擇哪個 JAR。如果產生零個測試 JAR，則測試步驟預設透過。如需測試範例，[請參閱 AEM 專案原型](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/it.tests)。

這些測試會在 Adobe 維護的測試基礎結構上執行，包括至少兩個作者執行個體、兩個發佈執行個體和一個 Dispatcher 設定。這代表您的自訂功能測試針對整個 AEM 堆疊執行。

自訂功能測試必須封裝為單獨的 JAR 檔案，該檔案由與要部署到 AEM 的成品相同的 Maven 組建產生。通常這將是一個單獨的 Maven 模組。產生的 JAR 檔案必須包含所有必要的相依性，通常使用 `maven-assembly-plugin` 和 `jar-with-dependencies` 描述項建立。

此外，JAR 必須將 `Cloud-Manager-TestType` 資訊清單標題設為 `integration-test`。

以下為 `maven-assembly-plugin` 的設定範例。

```java
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
```

在這個 JAR 檔案中，要執行的實際測試的類別名稱必須以 `IT` 結尾。

例如，將執行名為 `com.myco.tests.aem.it.ExampleIT` 的類別，但不會執行名為 `com.myco.tests.aem.it.ExampleTest` 的類別。

此外，要從計劃碼掃描的覆蓋檢查中排除測試計劃碼，測試計劃碼必須位於名為`it` 的套件之下 (覆蓋排除篩選是`**/it/**/*.java`)。

測試類別必須是一般的 JUnit 測試。測試基礎結構的設計和設定與 `aem-testing-clients` 測試庫使用的慣例相容。強烈鼓勵開發人員使用此計劃庫並遵循其最佳實務。

如需更多詳細資訊，請參閱 [`aem-testing-clients`GitHub 存放庫](https://github.com/adobe/aem-testing-clients)。

>[!TIP]
>
>[觀看此影片](https://www.youtube.com/watch?v=yJX6r3xRLHU)，了解如何使用自訂功能測試來提高您對 CI/CD 管道的信心。

## 自訂 UI 測試 {#custom-ui-testing}

自訂 UI 測試是一項選擇性功能，可讓您為應用計劃建立和自動執行 UI 測試。UI 測試是封裝在 Docker 影像中的 Selenium 型測試，以便在語言和架構 (例如 Java 和 Maven、Node 和 WebDriver.io 或任何其他根據 Selenium 建置的架構和技術) 中提供廣泛的選擇。

如需更多詳細資訊，請參閱文件：[自訂 UI 測試](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing)。

## 本機測試執行 {#local-test-execution}

由於測試類別是 JUnit 測試，所以它們可以從主流的 Java IDE (如 Eclipse、IntelliJ、NetBeans 等) 執行。因為產品功能測試和自訂功能測試都基於相同的技術，所以兩者都可以透過將產品測試複製到自訂測試中，以在本機執行。

但是，在執行這些測試時，需要設定 `aem-testing-clients` (和底層 Sling 測試用戶端) 計劃庫應有的各種系統屬性。

系統屬性如下。

* `sling.it.instances - should be set to 2`
* `sling.it.instance.url.1 - should be set to the author URL, for example, http://localhost:4502`
* `sling.it.instance.runmode.1 - should be set to author`
* `sling.it.instance.adminUser.1 - should be set to the author admin user, for example, admin`
* `sling.it.instance.adminPassword.1 - should be set to the author admin password`
* `sling.it.instance.url.2 - should be set to the publish URL, for example, http://localhost:4503`
* `sling.it.instance.runmode.2 - should be set to publish`
* `sling.it.instance.adminUser.2 - should be set to the publish admin user, for example, admin`
* `sling.it.instance.adminPassword.2 - should be set to the publish admin password`
