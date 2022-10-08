---
title: 功能測試
description: 了解AEMas a Cloud Service部署程式中內建的三種不同功能測試類型，以確保程式碼的品質和可靠性。
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 0%

---


# 功能測試 {#functional-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="功能測試"
>abstract="了解AEMas a Cloud Service部署程式中內建的三種不同功能測試類型，以確保程式碼的品質和可靠性。"

了解內建在 [AEMas a Cloud Service部署程式](/help/implementing/cloud-manager/deploy-code.md) 以確保程式碼的品質和可靠性。

## 總覽 {#overview}

AEMas a Cloud Service中有三種不同的功能測試類型。

* [產品功能測試](#product-functional-testing)
* [自訂功能測試](#custom-functional-testing)
* [自訂UI測試](#custom-ui-testing)

對於所有功能測試，測試的詳細結果可下載為 `.zip` 檔案，使用 **下載組建記錄** 「建置概述」畫面中的按鈕，作為 [部署程式。](/help/implementing/cloud-manager/deploy-code.md)

這些記錄檔不包含實際AEM執行階段程式的記錄檔。 要訪問這些日誌，請參閱文檔 [存取和管理記錄](/help/implementing/cloud-manager/manage-logs.md) 以取得更多詳細資訊。

產品功能測試和自訂功能測試範例都以 [AEM測試用戶端。](https://github.com/adobe/aem-testing-clients)

## 產品功能測試 {#product-functional-testing}

產品功能測試是AEM中核心功能（例如製作和復寫工作）的一組穩定HTTP整合測試(IT)。 這些測試由Adobe維護，目的是防止在自訂應用程式程式碼中斷核心功能時，部署變更。

每當您將新程式碼部署至Cloud Manager且無法略過時，產品功能測試就會自動執行。

產品功能測試會保留為開放原始碼專案。 請參閱 [產品功能測試](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) 以取得詳細資訊。

## 自訂功能測試 {#custom-functional-testing}

雖然產品功能測試由Adobe定義，但您可以為自己的應用程式編寫自己的品質測試。 這會作為生產管道的一部分，以自訂功能測試的形式執行，以確保應用程式的品質。

自訂功能測試會同時針對自訂程式碼部署和推送升級執行，因此撰寫良好的功能測試來防止AEM程式碼變更破壞您的應用程式程式碼，尤其重要。 自訂功能測試步驟一律存在，且無法略過。

### 撰寫自訂功能測試 {#writing-functional-tests}

Adobe用來編寫產品功能測試的工具，可用來編寫自訂功能測試。 使用 [產品功能測試](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) 以示如何撰寫測試的範例。

自訂功能測試的程式碼為位於 `it.tests` 檔案夾。 它應生成包含所有功能測試的單個JAR。 如果生成多個測試JAR，則選定的JAR不是確定性的。 如果它產生零個測試JAR，則測試步驟預設會通過。 [請參閱AEM專案原型](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/it.tests) 以取得範例測試。

這些測試會在Adobe維護的測試基礎架構上執行，其中至少包含兩個製作例項、兩個發佈例項和一個Dispatcher設定。 這表示您的自訂功能測試會針對整個AEM堆疊執行。

自訂功能測試必須封裝為由要部署至AEM的成品所產生的個別JAR檔案。 一般而言，這會是個別的Maven模組。 產生的JAR檔案必須包含所有必要的相依性，且通常會使用 `maven-assembly-plugin` 使用 `jar-with-dependencies` 描述符。

此外，JAR必須具有 `Cloud-Manager-TestType` 資訊清單標題設為 `integration-test`.

以下是 `maven-assembly-plugin`.

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

在此JAR檔案中，要執行的實際測試的類名必須以結尾 `IT`.

例如，名為 `com.myco.tests.aem.it.ExampleIT` 會被執行，但是一個 `com.myco.tests.aem.it.ExampleTest` 不會。

此外，要將測試代碼排除在代碼掃描的覆蓋檢查之外，測試代碼必須位於名為的包的下方 `it` (涵蓋範圍排除篩選器為 `**/it/**/*.java`)。

測試類需要是正常的JUnit測試。 測試基礎架構經過設計並配置以與 `aem-testing-clients` 測試程式庫。 強烈建議開發人員使用此程式庫並遵循其最佳實務。

請參閱 [`aem-testing-clients` GitHub存放庫](https://github.com/adobe/aem-testing-clients) 以取得更多詳細資訊。

>[!TIP]
>
>[觀看此視頻](https://www.youtube.com/watch?v=yJX6r3xRLHU) 關於如何使用自訂功能測試來提升您對CI/CD管道的信心。

## 自訂UI測試 {#custom-ui-testing}

自訂UI測試是選用功能，可讓您建立並自動執行應用程式的UI測試。 UI測試是封裝在Docker影像中的基於硒的測試，以允許在語言和框架（如Java和Maven、Node和WebDriver.io，或基於Selenium構建的任何其他框架和技術）中進行廣泛選擇。

請參閱該文檔 [自訂UI測試](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing) 以取得更多資訊。

## 本地測試執行 {#local-test-execution}

由於測試類是JUnit測試，因此可以從主流Java IDE（如Eclipse、IntelliJ、NetBeans等）運行。 由於產品功能測試和自訂功能測試都以相同技術為基礎，因此可將產品測試複製到您的自訂測試，以便在本機執行。

不過，執行這些測試時，必須設定 `aem-testing-clients` （和基礎的Sling Testing Clients）程式庫。

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
