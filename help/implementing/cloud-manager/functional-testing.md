---
title: 功能測試
description: 瞭解as a Cloud Service部署流程中內置的三種不同類型的功能測AEM試，以確保代碼的質量和可靠性。
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: f8d5b94d176dfbd5bcecf552f974dc77c5afe4e2
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 0%

---


# 功能測試 {#functional-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="功能測試"
>abstract="瞭解as a Cloud Service部署流程中內置的三種不同類型的功能測AEM試，以確保代碼的質量和可靠性。"

瞭解內置於 [AEMas a Cloud Service部署](/help/implementing/cloud-manager/deploy-code.md) 確保代碼的質量和可靠性。

## 概覽 {#overview}

在as a Cloud Service中有三種不同的功能測試AEM。

* [產品功能測試](#product-functional-testing)
* [自定義功能測試](#custom-functional-testing)
* [自定義UI測試](#custom-ui-testing)

對於所有功能test，可以將test的詳細結果下載為 `.zip` 檔案 **下載生成日誌** 按鈕 [部署過程。](/help/implementing/cloud-manager/deploy-code.md)

這些日誌不包括實際運行時進AEM程的日誌。 要訪問這些日誌，請參閱文檔 [訪問和管理日誌](/help/implementing/cloud-manager/manage-logs.md) 的子菜單。

產品功能test和示例自定義功能test均基於 [正在AEM測試客戶端。](https://github.com/adobe/aem-testing-clients)

## 產品功能測試 {#product-functional-testing}

產品功能test是一組穩定的HTTP整合test(IT)，它們是創作和複製任務AEM中的核心功能。 這些test由Adobe維護，旨在防止在自定義應用程式碼中斷核心功能時部署更改。

產品功能test在將新代碼部署到雲管理器時自動運行，無法跳過。

產品功能test作為開源項目進行維護。 請參閱 [產品功能test](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) 在GitHub中獲取詳細資訊。

## 自定義功能測試 {#custom-functional-testing}

雖然產品功能測試由Adobe定義，但您可以為自己的應用程式編寫自己的質量測試。 此操作將作為生產流水線的一部分執行，以確保應用程式的質量。

自定義功能測試既針對自定義代碼部署也針對推式升級執行，這對於編寫良好的功能test來防止代碼更改破壞您的AEM應用程式碼尤為重要。 自定義功能測試步驟始終存在，無法跳過。

### 編寫自定義功能Test {#writing-functional-tests}

Adobe用於編寫產品功能test的工具可用於編寫自定義功能test。 使用 [產品功能test](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) 在GitHub中，作為如何編寫test的示例。

自定義功能test的代碼是位於 `it.tests` 資料夾。 它應生成具有所有功能test的單個JAR。 如果生成多個testJAR，則選擇的JAR不是確定性的。 如果它產生零testJAR，則預設情況下test步驟會通過。 [查看項AEM目原型](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/it.tests) 示例test。

該test在Adobe維護的測試基礎設施上執行，該測試基礎設施包括至少兩個作者實例、兩個發佈實例和調度器配置。 這意味著您的自定義功能test針對整個堆棧AEM運行。

自定義功能test必須打包為由與要部署到的對象相同的Maven內部版本生成的單獨JAR文AEM件。 通常，這是一個單獨的Maven模組。 生成的JAR檔案必須包含所有必需的依賴關係，並且通常使用 `maven-assembly-plugin` 使用 `jar-with-dependencies` 描述符。

此外，JAR必須 `Cloud-Manager-TestType` 將清單頭設定為 `integration-test`。

以下是 `maven-assembly-plugin`。

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

在此JAR檔案中，要執行的實際test的類名必須以 `IT`。

例如，名為 `com.myco.tests.aem.it.ExampleIT` 將被執行，但是一個 `com.myco.tests.aem.it.ExampleTest` 不會的。

此外，要從代碼掃描的覆蓋率檢查中排除test代碼，test代碼必須位於名為 `it` (覆蓋範圍排除篩選器為 `**/it/**/*.java`)。

test類必須是普通JUnittest。 test基礎架構設計並配置為與 `aem-testing-clients` test庫。 強烈鼓勵開發人員使用此庫並遵循其最佳做法。

請參閱 [`aem-testing-clients` GitHub回購](https://github.com/adobe/aem-testing-clients) 的子菜單。

>[!TIP]
>
>[觀看此視頻](https://www.youtube.com/watch?v=yJX6r3xRLHU) 關於如何使用自定義功能test來提高您對CI/CD管道的信心。

## 自定義UI測試 {#custom-ui-testing}

自定義UI測試是一項可選功能，使您能夠建立並自動運行應用程式的UItest。 UItest是基於Selenium的test，打包在Docker映像中，以允許在語言和框架（如Java和Maven、Node和WebDriver.io，或基於Selenium構建的任何其它框架和技術）中進行廣泛選擇。

請參閱文檔 [自定義UI測試](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing) 的子菜單。

## 本地Test執行 {#local-test-execution}

因為test類是JUnittest，所以它們可以從主流Java IDE（如Eclipse、IntelliJ、NetBeans等）中運行。 由於產品功能test和定制功能test都基於相同的技術，因此，通過將產品test複製到您的定製test中，都可以在本地運行。

但是，在運行這些test時，需要設定 `aem-testing-clients` （和基礎Sling測試客戶端）庫。

系統屬性如下所示。

* `sling.it.instances - should be set to 2`
* `sling.it.instance.url.1 - should be set to the author URL, for example, http://localhost:4502`
* `sling.it.instance.runmode.1 - should be set to author`
* `sling.it.instance.adminUser.1 - should be set to the author admin user, e.g. admin`
* `sling.it.instance.adminPassword.1 - should be set to the author admin password`
* `sling.it.instance.url.2 - should be set to the publish URL, for example, http://localhost:4503`
* `sling.it.instance.runmode.2 - should be set to publish`
* `sling.it.instance.adminUser.2 - should be set to the publish admin user, for example, admin`
* `sling.it.instance.adminPassword.2 - should be set to the publish admin password`
