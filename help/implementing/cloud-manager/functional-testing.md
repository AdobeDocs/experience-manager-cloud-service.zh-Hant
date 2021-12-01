---
title: 功能測試 — Cloud Services
description: 功能測試 — Cloud Services
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: 778fa187df675eada645c73911e6f02e8a112753
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 3%

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

請參閱 [產品功能測試](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) 以取得範例測試。

## 自訂功能測試 {#custom-functional-testing}

管道中的自訂功能測試步驟一律存在，且無法略過。

組建應產生零個或一個測試JAR。 如果它產生零個測試JAR，則測試步驟預設會通過。 如果組建產生多個測試JAR，則所選的JAR不確定。

>[!NOTE]
>「下 **載日誌** 」按鈕允許訪問包含測試執行詳細表單日誌的ZIP檔案。這些記錄檔不包含實際AEM執行階段程式的記錄檔，這些記錄檔可使用一般的下載或尾隨記錄檔功能來存取。 請參閱 [存取和管理記錄](/help/implementing/cloud-manager/manage-logs.md) 以取得更多詳細資訊。


## 編寫功能測試 {#writing-functional-tests}

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

在此JAR檔案中，要執行的實際測試的類名必須以結尾 `IT`.

例如，名為 `com.myco.tests.aem.it.ExampleIT` 會被執行，但是一個 `com.myco.tests.aem.it.ExampleTest` 不會。

此外，要將測試代碼排除在代碼掃描的覆蓋檢查之外，測試代碼必須位於名為的包的下方 `it` (涵蓋範圍排除篩選器為 `**/it/**/*.java`)。

測試類需要是正常的JUnit測試。 測試基礎架構經過設計並設定，可與aem測試用戶端測試程式庫使用的慣例相容。 強烈建議開發人員使用此程式庫並遵循其最佳實務。 請參閱 [Git連結](https://github.com/adobe/aem-testing-clients) 以取得更多詳細資訊。

## 本地測試執行 {#local-test-execution}

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
