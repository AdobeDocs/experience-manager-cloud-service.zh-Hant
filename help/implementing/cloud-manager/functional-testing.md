---
title: 功能測試——雲端服務
description: 功能測試——雲端服務
translation-type: tm+mt
source-git-commit: 25ba5798de175b71be442d909ee5c9c37dcf10d4
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 4%

---


# 功能測試{#functional-testing}

功能測試分為兩種類型：

* 產品功能測試
* 自訂功能測試

## 產品功能測試{#product-functional-testing}

產品功能測試是一組穩定的HTTP整合測試(IT)，以AEM的核心功能（例如製作和複製）為中心，可防止客戶在應用程式程式程式碼中斷此核心功能時進行變更。

每當客戶將新程式碼部署至Cloud Manager且無法略過時，產品功能測試就會自動執行。

有關示例測試，請參閱[產品功能測試](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke)。

## 自訂功能測試{#custom-functional-testing}

管線中的「自訂功能」測試步驟始終存在，且無法跳過。

但是，如果構建版本未生成測試JAR，則預設情況下測試通過。

>[!NOTE]
>「下 **載日誌** 」按鈕允許訪問包含測試執行詳細表單日誌的ZIP檔案。這些記錄檔不包含實際AEM執行階段程式的記錄檔——這些記錄檔可使用一般的「下載」或「尾部記錄檔」功能來存取。 有關詳細資訊，請參閱[訪問和管理日誌](/help/implementing/cloud-manager/manage-logs.md)。


### 編寫功能測試{#writing-functional-tests}

客戶撰寫的功能測試必須封裝為由要部署至AEM的對象所產生的個別JAR檔案。 通常，此模組是單獨的Maven模組。 生成的JAR檔案必須包含所有必需的從屬關係，通常使用maven-assembly-plugin使用jar-with-dependencies描述符建立。

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

由於測試類是JUnit測試，因此可以從主流Java IDE（如Eclipse、IntelliJ、NetBeans等）運行。

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

