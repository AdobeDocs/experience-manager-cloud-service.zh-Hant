---
title: 功能測試 — Cloud Services
description: 功能測試 — Cloud Services
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: cf2e206b0ad186e0f4caa4a2ec9c34faf2078b76
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 2%

---

# 功能測試 {#functional-testing}


>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="功能測試"
>abstract="功能測試分為三種類型：產品功能測試、自訂功能測試和自訂UI測試"

功能測試分為三種類型：


* 產品功能測試
* 自訂功能測試
* 自訂UI測試

## 產品功能測試 {#product-functional-testing}

產品功能測試是一組圍繞AEM核心功能（例如製作和復寫）而穩定的HTTP整合測試(IT)，若客戶變更的應用程式程式碼中斷此核心功能，就無法部署。

每當客戶將新程式碼部署至Cloud Manager且無法略過時，產品功能測試就會自動執行。

有關示例測試，請參閱[產品功能測試](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke)。

## 自訂功能測試 {#custom-functional-testing}

管道中的自訂功能測試步驟一律存在，且無法略過。

但是，如果組建未產生測試JAR，則測試預設會通過。

>[!NOTE]
>「下 **載日誌** 」按鈕允許訪問包含測試執行詳細表單日誌的ZIP檔案。這些記錄檔不包含實際AEM執行階段程式的記錄檔，這些記錄檔可使用一般的下載或尾隨記錄檔功能來存取。 如需詳細資訊，請參閱[存取和管理記錄](/help/implementing/cloud-manager/manage-logs.md) 。

## 自訂UI測試 {#custom-ui-testing}

AEM為其客戶提供整合的Cloud Manager品質閘門套裝，確保應用程式能順暢地更新。 尤其是，IT測試閘道已允許客戶建立並使用AEM API的自動化測試。

自訂UI測試功能是選用功能[客戶選擇加入](#customer-opt-in)，可讓客戶建立並自動執行其應用程式的UI測試。 UI測試是封裝在Docker影像中的基於硒的測試，以允許在語言和框架（如Java和Maven、Node和WebDriver.io，或基於Selenium構建的任何其他框架和技術）中進行廣泛選擇。 您可以從這裡進一步了解如何建立UI和撰寫UI測試。 此外，使用AEM專案原型即可輕鬆產生UI測試專案。

客戶可以建立（透過GIT）自訂測試，以及使用者介面的測試套裝。 UI測試將隨著每個Cloud Manager管道的特定品質閘道執行，並包含其特定步驟和意見資訊。 任何UI測試（包括回歸和新功能）都可讓您在客戶內容中偵測和報告錯誤。

在「自訂UI測試」步驟下，客戶UI測試會自動在生產管道上執行。

與以java寫入的HTTP測試不同，只要UI測試遵循[建置UI測試](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/ui-testing.html?lang=en#building-ui-tests)中定義的慣例，UI測試就可以是測試以任何語言寫入的Docker影像。

>[!NOTE]
>建議您以[AEM專案原型](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)中提供的結構和語言&#x200B;*（js和wdio）*&#x200B;為起點，輕鬆操作。

### 客戶選擇加入 {#customer-opt-in}

若要建置並執行其UI測試，客戶需要在UI測試的maven子模組下（UI測試子模組的pom.xml檔案旁），將檔案新增至其程式碼存放庫，以「選擇加入」，並確認此檔案位於建置`tar.gz`檔案的根目錄。

*檔案名*:  `testing.properties`

*內容*:  `ui-tests.version=1`

如果內建的`tar.gz`檔案中未包含此選項，則會跳過UI測試組建和執行

若要在內建工件中新增`testing.properties`檔案，請在`assembly-ui-test-docker-context.xml`檔案中新增`include`陳述式（在UI測試子模組中）:

    &quot;&#39;
    [...]
    &lt;includes>
    &lt;include>&lt;/include>
    &lt;include>Dockerfilewait-for-grid.&lt;/include>
    &lt;include>shtesting.properties&lt;/include> &lt;!- Cloud Manager中的選擇加入測試模組 — >
    &lt;/includes>
    [...]
    &quot;&#39;

>[!NOTE]
>2021年2月10日之前建立的生產管道必須更新，才能使用本節所述的UI測試。 這基本上表示使用者必須編輯生產管道，並在未進行變更的情況下，從UI按一下&#x200B;**儲存**。
>請參閱[設定CI-CD管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en#using-cloud-manager)以深入了解管道設定。

### 編寫功能測試 {#writing-functional-tests}

客戶寫入的功能測試必須封裝為由相同Maven版本編號產生的獨立JAR檔案，作為要部署至AEM的成品。 一般而言，這會是個別的Maven模組。 生成的JAR檔案必須包含所有必要的依賴項，並且通常使用maven-assembly-plugin使用jar-with-dependencies描述符建立。

此外，JAR必須將Cloud-Manager-TestType資訊清單標題設為integration-test。 未來預期會支援其他標題值。 maven-assembly-plugin的範例設定為：

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

在此JAR檔案中，要執行的實際測試的類名必須在IT中結束。

例如，將執行名為`com.myco.tests.aem.ExampleIT`的類，但名為`com.myco.tests.aem.ExampleTest`的類不會執行。

測試類需要是正常的JUnit測試。 測試基礎架構經過設計並設定，可與aem測試用戶端測試程式庫使用的慣例相容。 強烈建議開發人員使用此程式庫並遵循其最佳實務。 如需詳細資訊，請參閱[Git連結](https://github.com/adobe/aem-testing-clients)。

### 本地測試執行 {#local-test-execution}

由於測試類是JUnit測試，因此可以從主流Java IDE（如Eclipse、IntelliJ、NetBeans等）運行。

不過，執行這些測試時，必須設定aem測試用戶端（和基礎Sling測試用戶端）預期的各種系統屬性。

系統屬性如下：

* `sling.it.instances - should be set to 2`
* `sling.it.instance.url.1 - should be set to the author URL, for example, http://localhost:4502`
* `sling.it.instance.runmode.1 - should be set to author`
* `sling.it.instance.adminUser.1 - should be set to the author admin user, e.g. admin`
* `sling.it.instance.adminPassword.1 - should be set to the author admin password`
* `sling.it.instance.url.2 - should be set to the author URL, for example, http://localhost:4503`
* `sling.it.instance.runmode.2 - should be set to publish`
* `sling.it.instance.adminUser.2 - should be set to the publish admin user, for example, admin`
* `sling.it.instance.adminPassword.2 - should be set to the publish admin password`
