---
title: UI測試——雲端服務
description: UI測試——雲端服務
translation-type: tm+mt
source-git-commit: ea0c9675ca03b1d247c7e5fd13e03072fb4a13ae
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 0%

---


# UI測試{#ui-testing}

UI測試是以Selenium為基礎的測試，封裝在Docker影像中，以允許在語言和架構（例如Java和Maven、Node和WebDriver.io，或任何以Selenium為基礎的其他架構和技術）中有廣泛選擇。 Docker映像可以使用標準工具建立，但在執行時必須遵守某些約定。 運行Docker映像時，會自動設定Selenium伺服器。 下列說明的執行時期慣例可讓您的測試程式碼同時存取Selenium伺服器和測試中的AEM例項。

>[!NOTE]
> 2021年2月10日之前建立的階段和生產管道需要更新，才能使用本頁所述的UI測試。
> 有關管線配置的資訊，請參見[配置CI-CD管線](/help/implementing/cloud-manager/configure-pipeline.md)。

## 建立UI測試{#building-ui-tests}

UI測試是以Maven專案產生的Docker建置內容為基礎。 Cloud Manager使用Docker建置上下文來產生包含實際UI測試的Docker影像。 總之，Maven項目生成Docker構建上下文，Docker構建上下文描述如何建立包含UI測試的Docker映像。

本節將介紹將UI測試項目添加到儲存庫所需的步驟。 如果您匆忙或對程式設計語言沒有特殊要求，[AEM Project Archetype](https://github.com/adobe/aem-project-archetype)可為您產生UI測試專案。

### 生成Docker構建上下文{#generate-docker-build-context}

為了生成Docker構建上下文，您需要一個Maven模組，該模組具有：

- 生成一個包含`Dockerfile`的歸檔檔案，以及使用測試構建Docker映像所需的每個其他檔案。
- 使用`ui-test-docker-context`類元標籤存檔。

要做到這一點，最簡單的方法是配置[Maven Assembly Plugin](http://maven.apache.org/plugins/maven-assembly-plugin/)以建立Docker構建上下文歸檔檔案並為其分配正確的類元。

您可以使用不同的技術和架構來建立UI測試，但本節假設您的專案是以類似下列的方式排版。

```
├── Dockerfile
├── assembly-ui-test-docker-context.xml
├── pom.xml
├── test-module
│   ├── package.json
│   ├── index.js
│   └── wdio.conf.js
└── wait-for-grid.sh
```

`pom.xml`檔案負責Maven組建。 向Maven Assembly Plugin添加執行，如下所示。

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-assembly-plugin</artifactId>
    <configuration>
        <descriptors>
            <descriptor>${project.basedir}/assembly-ui-test-docker-context.xml</descriptor>
        </descriptors>
        <tarLongFileMode>gnu</tarLongFileMode>
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
```

此執行會指示Maven Assembly Plugin根據`assembly-ui-test-docker-context.xml`中包含的說明（在插件術語中稱為&quot;assembly descriptor&quot;）建立歸檔檔案。 元件描述符列出了必須屬于歸檔檔案的所有檔案。

```xml
<assembly>
    <id>ui-test-docker-context</id>
    <includeBaseDirectory>false</includeBaseDirectory>
    <formats>
        <format>tar.gz</format>
    </formats>
    <fileSets>
        <fileSet>
            <directory>${basedir}</directory>
            <includes>
                <include>Dockerfile</include>
                <include>wait-for-grid.sh</include>
            </includes>
        </fileSet>
        <fileSet>
            <directory>${basedir}/test-module</directory>
            <excludes>
                <exclude>node/**</exclude>
                <exclude>node_modules/**</exclude>
                <exclude>reports/**</exclude>
            </excludes>
        </fileSet>
    </fileSets>
</assembly>
```

元件描述符指示插件建立類型`.tar.gz`的歸檔檔案，並將`ui-test-docker-context`類元指派給它。 此外，它還列出了必須包含在存檔中的檔案：

- `Dockerfile`，是建立Docker映像的必備項。
- `wait-for-grid.sh`指令碼，其用途如下所述。
- 實際的UI測試由`test-module`資料夾中的Node.js專案實作。

元件描述符還排除在本地運行UI測試時可能生成的某些檔案。 這可保證檔案的精簡和建置的速度更快。

包含Docker構建上下文的歸檔檔案由Cloud Manager自動拾取，Cloud Manager將在部署管線期間生成包含測試的Docker映像。 最終，Cloud Manager將運行Docker映像，以對您的應用程式執行UI測試。

## 編寫UI測試{#writing-ui-tests}

本節說明包含UI測試的Docker影像必須遵循的慣例。 Docker映像是基於上一節所述的Docker構建上下文構建的。

### 環境變數{#environment-variables}

以下環境變數將在運行時傳遞到Docker映像。

| 變數 | 範例 | 說明 |
|---|---|---|
| `SELENIUM_BASE_URL` | `http://my-ip:4444` | Selenium伺服器的URL |
| `SELENIUM_BROWSER` | `chrome`, `firefox` | Selenium Server使用的瀏覽器實作 |
| `AEM_AUTHOR_URL` | `http://my-ip:4502/context-path` | AEM作者例項的URL |
| `AEM_AUTHOR_USERNAME` | `admin` | 要登入AEM作者例項的使用者名稱 |
| `AEM_AUTHOR_PASSWORD` | `admin` | 登入AEM作者例項的密碼 |
| `AEM_PUBLISH_URL` | `http://my-ip:4503/context-path` | AEM發佈例項的URL |
| `AEM_PUBLISH_USERNAME` | `admin` | 要登入AEM發佈例項的使用者名稱 |
| `AEM_PUBLISH_PASSWORD` | `admin` | 登入AEM發佈例項的密碼 |
| `REPORTS_PATH` | `/usr/src/app/reports` | 必須儲存測試結果的XML報表的路徑 |
| `UPLOAD_URL` | `http://upload-host:9090/upload` | 必須上傳檔案至的URL，才能讓Selenium存取檔案 |

### 等待硒準備就緒{#waiting-for-selenium}

在測試開始之前，Docker映像有責任確保Selenium伺服器已啟動並運行。 等待Selenium服務是兩個步驟：

1. 從`SELENIUM_BASE_URL`環境變數中讀取Selenium服務的URL。
2. 定期輪詢Selenium API公開的[狀態端點](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready)。

一旦Selenium的狀態端點以正面回應回答，測試就可以開始。

### 產生測試報表{#generate-test-reports}

Docker映像必須以JUnit XML格式生成測試報告，並將其保存在環境變數`REPORTS_PATH`指定的路徑中。 JUnit XML格式是報告測試結果的一種廣泛格式。 如果Docker映像使用Java和Maven，則[Maven Surefire Plugin](https://maven.apache.org/surefire/maven-surefire-plugin/)和[Maven Failsafe Plugin](https://maven.apache.org/surefire/maven-failsafe-plugin/)。 如果Docker映像是使用其他寫程式語言或測試運行者實施的，請查看文檔中的所選工具以瞭解如何生成JUnit XML報告。

### 上傳檔案(#upload-files)

測試有時必須將檔案上傳至測試中的應用程式。 為了維持Selenium相對於測試的部署彈性，無法直接將資產上傳至Selenium。 而上傳檔案則會執行一些中介步驟：

1. 在`UPLOAD_URL`環境變數指定的URL上傳檔案。 上傳必須在含多部分表單的單一POST請求中執行。 多部件表單必須有一個檔案欄位。 這等效於`curl -X POST ${UPLOAD_URL} -F "data=@file.txt"`。 請參閱Docker影像中使用之程式設計語言的檔案和程式庫，瞭解如何執行此類HTTP要求。
2. 如果上傳成功，請求會傳回類型`text/plain`的`200 OK`回應。 響應的內容是不透明檔案句柄。 您可以使用此控制代碼來取代`<input>`元素中的檔案路徑，以測試應用程式中的檔案上傳。
