---
title: 功能測試-Cloud Services
description: 功能測試-Cloud Services
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: 006fd74a9c4f4d5321bb3d0b35b5c9d49def7bc4
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 2%

---

# 功能測試{#functional-testing}


>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="功能測試"
>abstract="功能測試分為三種類型：產品功能測試、自訂功能測試和自訂UI測試"

功能測試分為三種類型：


* 產品功能測試
* 自訂功能測試
* 自訂UI測試

## 產品功能測試{#product-functional-testing}

產品功能測試是一組穩定的HTTP整合測試(IT)，其核心功能（例如，製作和複製）AEM，可防止客戶在應用程式程式碼中斷此核心功能時，對其應用程式碼所做的變更被部署。

每當客戶將新程式碼部署至Cloud Manager且無法略過時，產品功能測試就會自動執行。

有關示例測試，請參閱[產品功能測試](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke)。

## 自訂功能測試{#custom-functional-testing}

管線中的「自訂功能」測試步驟始終存在，且無法跳過。

但是，如果構建版本未生成測試JAR，則預設情況下測試通過。

>[!NOTE]
>「下 **載日誌** 」按鈕允許訪問包含測試執行詳細表單日誌的ZIP檔案。這些記錄檔不包含實際執行階段程AEM序的記錄檔——這些記錄檔可使用一般的下載或尾隨記錄檔功能加以存取。 有關詳細資訊，請參閱[訪問和管理日誌](/help/implementing/cloud-manager/manage-logs.md)。

## 自訂UI測試{#custom-ui-testing}

為客AEM戶提供一套整合的Cloud Manager品質門檻，以確保其應用程式的順暢更新。 尤其是，IT測試閘道已允許客戶建立並自動化使用API的自AEM己測試。

「自訂UI測試」功能是選用功能[「客戶選擇加入」](#customer-opt-in)，可讓我們的客戶為其應用程式建立並自動執行UI測試。 UI測試是以Selenium為基礎的測試，封裝在Docker影像中，以允許在語言和架構（例如Java和Maven、Node和WebDriver.io，或任何以Selenium為基礎的其他架構和技術）中有廣泛選擇。 您可從這裡進一步瞭解如何建立UI和編寫UI測試。 此外，使用「專案原型」可輕鬆產生「UI測試AEM」專案。

客戶可以建立（透過GIT）UI的自訂測試和測試套件。 UI測試將作為每個Cloud Manager管道的特定質量門的一部分執行，並包含其特定步驟和反饋資訊。 任何UI測試（包括回歸和新功能）都可讓您在客戶內容中偵測並報告錯誤。

客戶UI測試會在「自訂UI測試」步驟下，自動在生產管線上執行。

與以java編寫的HTTP測試自訂功能測試不同，UI測試可以是使用任何語言編寫的測試的Docker映像，只要測試遵循[建立UI測試](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/ui-testing.html?lang=en#building-ui-tests)中定義的慣例。

>[!NOTE]
>建議以[AEM Project Archetype](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)中方便提供的結構和語言&#x200B;*(js and wdio)*&#x200B;為起點。

### 客戶選擇加入{#customer-opt-in}

為了建立並執行其UI測試，客戶需要在UI測試的主子模組（UI測試子模組的pom.xml檔案旁）下，將檔案新增至其程式碼儲存庫，以「選擇加入」，並確保此檔案位於內建`tar.gz`檔案的根目錄。

*檔案名*:  `testing.properties`

*內容*:  `one line: ui-tests.version=1`

如果這不在內建的`tar.gz`檔案中，則會略過UI測試建立和執行

>[!NOTE]
>在2021年2月10日之前建立的生產管道必須更新，才能使用本節所述的UI測試。 這基本上表示使用者必須編輯生產管線，並從UI按一下「儲存」(**Save**)，即使未進行任何變更亦然。
>請參閱[配置CI-CD Pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en#using-cloud-manager)以瞭解有關管線配置的更多資訊。

### 編寫功能測試{#writing-functional-tests}

客戶編寫的功能測試必須打包為由要部署到的對象所在的同一Maven構建版本生成的單獨JAR文AEM件。 通常，此模組是單獨的Maven模組。 生成的JAR檔案必須包含所有必需的從屬關係，通常使用maven-assembly-plugin使用jar-with-dependencies描述符建立。

此外，JAR必須將Cloud-Manager-TestType資訊清單標題設為integration-test。 未來預計會支援其他標題值。 maven-assembly-plugin的範例組態為：

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

在此JAR檔案中，要執行的實際測試的類名必須以IT結束。

例如，將執行名為`com.myco.tests.aem.ExampleIT`的類，但不執行名為`com.myco.tests.aem.ExampleTest`的類。

測試類必須是常規JUnit測試。 測試基礎架構的設計與設定可與aem-testing-clients測試程式庫所使用的慣例相容。 強烈建議開發人員使用此程式庫並遵循其最佳實務。 如需詳細資訊，請參閱[Git Link](https://github.com/adobe/aem-testing-clients)。

### 本地測試執行{#local-test-execution}

由於測試類是JUnit測試，因此可以從主流Java IDE（如Eclipse、IntelliJ、NetBeans等）中運行。

不過，在執行這些測試時，必須設定aem-testing-clients（和基礎Sling Testing Clients）預期的各種系統屬性。

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
