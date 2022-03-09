---
title: UI測試
description: 自定義UI測試是一項可選功能，使您能夠建立並自動運行自定義應用程式的UItest
exl-id: 3009f8cc-da12-4e55-9bce-b564621966dd
source-git-commit: a7555507f4fb0fb231e27d7c7a6413b4ec6b94e6
workflow-type: tm+mt
source-wordcount: '1401'
ht-degree: 0%

---


# UI測試 {#ui-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_uitesting"
>title="UI測試"
>abstract="自定義UI測試是一項可選功能，使您能夠建立並自動運行應用程式的UItest。 UItest是基於Selenium的test，打包在Docker映像中，以允許在語言和框架（如Java和Maven、Node和WebDriver.io，或基於Selenium構建的任何其它框架和技術）中進行廣泛選擇。"

自定義UI測試是一項可選功能，使您能夠建立並自動運行應用程式的UItest。

>[!NOTE]
> 需要更新2021年2月10日之前建立的階段和生產管道，以便使用本頁中所述的UItest。
> 請參閱 [雲管理器中的CI-CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) 的子菜單。

## 概覽 {#custom-ui-testing}

AEM提供 [Cloud Manager質量門](/help/implementing/cloud-manager/custom-code-quality-rules.md) 確保對自定義應用程式的平滑更新。 特別是，ITtest門已使用API建立和自動化自定AEM義test。

UItest是基於Selenium的test，打包在Docker映像中，以允許在語言和框架（如Java和Maven、Node和WebDriver.io，或基於Selenium構建的任何其它框架和技術）中進行廣泛選擇。 另外，通過使用UItest，可以容易地生成UI項目 [原型AEM計畫。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)

UItest作為每個Cloud Manager管道的特定質量門的一部分執行， [專用 **自定義UI測試** 的子菜單。](/help/implementing/cloud-manager/deploy-code.md) 任何UItest（包括回歸和新功能）都允許檢測和報告錯誤。

與以Java編寫的HTTPtest的自定義功能test不同，UItest可以是Docker影像，其中test以任何語言編寫，只要它們遵循該部分中定義的約定 [正在生成UITest。](#building-ui-tests)

>[!TIP]
>
>Adobe建議遵循中提供的結構和語言（JavaScript和WDIO） [原型AEM計畫。](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)

### 客戶選擇加入 {#customer-opt-in}

為了使Cloud Manager能夠生成並執行您的UItest，您必須通過向儲存庫中添加檔案來選擇加入此功能。

* 檔案名必須為 `testing.properties`。
* 檔案內容必須是 `ui-tests.version=1`。
* 檔案必須位於UItest的maven子模組下 `pom.xml` UItest子模組的檔案。
* 檔案必須位於生成的根 `tar.gz` 的子菜單。

如果此檔案不存在，將跳過UItest生成和執行。

要包括 `testing.properties` 檔案，添加 `include` 語句 `assembly-ui-test-docker-context.xml` 的子菜單。

```xml
[...]
<includes>
    <include>Dockerfile</include>
    <include>wait-for-grid.sh</include>
    <include>testing.properties</include> <!- opt-in test module in Cloud Manager -->
</includes>
[...]
```

>[!NOTE]
>
>如果項目不包括此行，則需要編輯此檔案以選擇加入UI測試。 如果檔案有行建議不編輯，請忽略該建議。

>[!NOTE]
>
>需要更新在2021年2月10日之前建立的生產管道，以便使用本節中所述的UItest。 這實際上意味著用戶必須編輯生產管線，然後按一下 **保存** 即使未進行任何更改，
>請參閱 [配置CI-CD管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en#using-cloud-manager) 瞭解有關管道配置的詳細資訊。

## 正在生成UITest {#building-ui-tests}

Maven項目生成Docker生成上下文。 此Docker生成上下文介紹如何建立包含UItest的Docker映像，Cloud Manager用戶要生成包含實際UItest的Docker映像。

本節介紹將UItest項目添加到儲存庫所需的步驟。

>[!TIP]
>
>的 [項AEM目原型](https://github.com/adobe/aem-project-archetype) 可以為您生成UITest項目，但您對寫程式語言沒有特殊要求。

### 生成Docker生成上下文 {#generate-docker-build-context}

要生成Docker生成上下文，您需要一個Maven模組：

* 生成包含 `Dockerfile` 以及用test構建Docker映像所需的其他檔案。
* 使用 `ui-test-docker-context` 分類器。

最簡單的方法是配置 [Maven程式集插件](http://maven.apache.org/plugins/maven-assembly-plugin/) 建立Docker生成上下文存檔並為其分配正確的類元。

您可以使用不同的技術和框架構建UItest，但本節假定您的項目是以類似於以下方式佈局的。

```text
├── Dockerfile
├── assembly-ui-test-docker-context.xml
├── pom.xml
├── test-module
│   ├── package.json
│   ├── index.js
│   └── wdio.conf.js
└── wait-for-grid.sh
```

的 `pom.xml` 檔案負責馬文的建造。 向Maven程式集插件添加執行，如下所示。

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

此執行將指示Maven程式集插件根據包含於 `assembly-ui-test-docker-context.xml`，調用 **裝配描述符** 插件的術語。 程式集描述符列出必須是存檔的一部分的所有檔案。

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

程式集描述符指示插件建立類型的存檔 `.tar.gz` 並分配 `ui-test-docker-context` 分類器。 此外，它還列出了必須包含在存檔中的檔案，包括以下內容。

* A `Dockerfile`，是構建Docker映像的必需項
* 的 `wait-for-grid.sh` 指令碼，其目的如下所述
* 實際UItest，由中的Node.js項目實現 `test-module` 資料夾

程式集test還排除了在本地運行UI描述符時可能生成的一些檔案。 這保證了較小的存檔和更快的生成。

包含Docker生成上下文的存檔檔案由Cloud Manager自動提取，Cloud Manager將在其部署管道期間生成包含您的test的Docker映像。 最終，Cloud Manager將運行Docker映像，以針對您的應用程式執行UItest。

生成應生成零或一個存檔。 如果它產生零存檔，則預設情況下test步驟會通過。 如果生成多個存檔，則選擇哪個存檔是不確定的。

## 編寫UITest {#writing-ui-tests}

本節介紹包含UItest的Docker映像必須遵循的約定。 Docker映像是基於上一節中描述的Docker生成上下文構建的。

### 環境變數 {#environment-variables}

以下環境變數將在運行時傳遞給您的Docker映像。

| 變數 | 示例 | 說明 |
|---|---|---|
| `SELENIUM_BASE_URL` | `http://my-ip:4444` | Selenium伺服器的URL |
| `SELENIUM_BROWSER` | `chrome`, `firefox` | Selenium Server使用的瀏覽器實現 |
| `AEM_AUTHOR_URL` | `http://my-ip:4502/context-path` | 作者實例AEM的URL |
| `AEM_AUTHOR_USERNAME` | `admin` | 登錄到作者實例的AEM用戶名 |
| `AEM_AUTHOR_PASSWORD` | `admin` | 登錄作者實例AEM的密碼 |
| `AEM_PUBLISH_URL` | `http://my-ip:4503/context-path` | 發佈實例AEM的URL |
| `AEM_PUBLISH_USERNAME` | `admin` | 登錄到發佈實例的AEM用戶名 |
| `AEM_PUBLISH_PASSWORD` | `admin` | 登錄到發佈實例的AEM密碼 |
| `REPORTS_PATH` | `/usr/src/app/reports` | 必須保存test結果的XML報告的路徑 |
| `UPLOAD_URL` | `http://upload-host:9090/upload` | 必須將檔案上載到的URL，以便Selenium可訪問這些檔案 |

### 等待硒準備好 {#waiting-for-selenium}

在test啟動之前， Docker映像有責任確保Selenium伺服器啟動並運行。 等待Selenium服務是一個兩步過程。

1. 從 `SELENIUM_BASE_URL` 環境變數。
1. 按常規間隔輪詢 [狀態終結點](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready) 由硒API暴露。

一旦Selenium的狀態終結點以正響應回答，test就可以開始。

### 生成Test報告 {#generate-test-reports}

Docker映像必須以JUnit XML格式生成test報告，並將它們保存在環境變數指定的路徑中 `REPORTS_PATH`。 JUnit XML格式是用於報告test結果的廣泛使用的格式。 如果Docker映像使用Java和Maven，則 [Maven Surefire插件](https://maven.apache.org/surefire/maven-surefire-plugin/) 和 [Maven Failsafe插件](https://maven.apache.org/surefire/maven-failsafe-plugin/)。

如果Docker影像是使用其他寫程式語言或test程式實現的，請查看所選工具的文檔，瞭解如何生成JUnit XML報告。

### 上載檔案 {#upload-files}

Test有時必須將檔案上載到正在測試的應用程式。 為了保持Selenium相對於test的部署靈活性，不可能直接將資產上載到Selenium。 而上載檔案需要執行以下步驟。

1. 在由 `UPLOAD_URL` 環境變數。
   * 上載必須在一個包含多部件表單的POST請求中執行。
   * 多部件窗體必須具有單個檔案欄位。
   * 這相當於 `curl -X POST ${UPLOAD_URL} -F "data=@file.txt"`。
   * 請查閱Docker映像中使用的寫程式語言的文檔和庫，瞭解如何執行此類HTTP請求。
1. 如果上載成功，請求將返回 `200 OK` 類型響應 `text/plain`。
   * 響應的內容是不透明的檔案句柄。
   * 可以使用此句柄代替 `<input>` 要test應用程式中上載的檔案的元素。
