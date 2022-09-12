---
title: UI測試
description: 自訂UI測試是選用功能，可讓您建立並自動執行自訂應用程式的UI測試
exl-id: 3009f8cc-da12-4e55-9bce-b564621966dd
source-git-commit: 430179bf13c1fff077c515eed0676430e9e7f341
workflow-type: tm+mt
source-wordcount: '1338'
ht-degree: 1%

---


# UI測試 {#ui-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_uitesting"
>title="UI測試"
>abstract="自訂UI測試是選用功能，可讓您建立並自動執行應用程式的UI測試。 UI測試是封裝在Docker影像中的基於硒的測試，以允許在語言和框架（如Java和Maven、Node和WebDriver.io，或基於Selenium構建的任何其他框架和技術）中進行廣泛選擇。"

自訂UI測試是選用功能，可讓您建立並自動執行應用程式的UI測試。

## 總覽 {#custom-ui-testing}

AEM提供整合的 [Cloud Manager品質入口](/help/implementing/cloud-manager/custom-code-quality-rules.md) 確保自訂應用程式的流暢更新。 尤其是，IT測試已開始使用AEM API建立和自動化自訂測試。

UI測試是封裝在Docker影像中的基於硒的測試，以允許在語言和框架（如Java和Maven、Node和WebDriver.io，或基於Selenium構建的任何其他框架和技術）中進行廣泛選擇。 此外，使用 [AEM專案原型。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)

UI測試會在每個Cloud Manager管道(具有 [專屬 **自訂UI測試** 步驟。](/help/implementing/cloud-manager/deploy-code.md) 任何UI測試（包括回歸和新功能）都能偵測到錯誤並加以報告。

自訂功能測試（以Java寫入的HTTP測試）不同，UI測試可以是Docker影像，測試以任何語言寫入，只要測試遵循區段中定義的慣例 [建立UI測試。](#building-ui-tests)

>[!TIP]
>
>Adobe建議遵循 [AEM專案原型。](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)

### 客戶選擇加入 {#customer-opt-in}

若要讓Cloud Manager建立並執行您的UI測試，您必須借由將檔案新增至存放庫來選擇加入此功能。

* 檔案名必須是 `testing.properties`.
* 檔案內容必須 `ui-tests.version=1`.
* 檔案必須位於maven子模組下，才能進行UI測試，緊鄰 `pom.xml` 檔案。
* 檔案必須位於建置的根目錄 `tar.gz` 檔案。

如果此檔案不存在，則會略過UI測試建置和執行。

若要包含 `testing.properties` 檔案（在生成對象中），添加 `include` 語句 `assembly-ui-test-docker-context.xml` 檔案。

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
>如果您的專案未包含此行，您需要編輯檔案以選擇加入UI測試。
>
>檔案可能包含一行，告知不要編輯它。 這是因為在引入選擇加入UI測試之前，已將其導入您的專案中，且用戶端的並非用來編輯檔案。 這可以安全地忽略。

## 建立UI測試 {#building-ui-tests}

Maven專案會產生Docker建置內容。 此Docker建置內容說明如何建立包含UI測試的Docker影像，Cloud Manager使用者要產生包含實際UI測試的Docker影像。

本節說明將UI測試專案新增至存放庫所需的步驟。

>[!TIP]
>
>此 [AEM專案原型](https://github.com/adobe/aem-project-archetype) 可以為您沒有程式設計語言的特殊需求產生UI測試專案。

### 生成Docker生成上下文 {#generate-docker-build-context}

若要產生Docker建置內容，您需要Maven模組，該模組應：

* 產生包含 `Dockerfile` 以及使用測試建立Docker映像所需的所有其他檔案。
* 使用標籤封存 `ui-test-docker-context` 分類器。

最簡單的方法是設定 [Maven程式集外掛程式](https://maven.apache.org/plugins/maven-assembly-plugin/) 來建立Docker構建上下文歸檔檔案，並為其分配正確的分類器。

您可以使用不同的技術和架構來建立UI測試，但本節假設您的專案是以類似下列的方式規劃。

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

此 `pom.xml` 檔案會處理Maven組建。 將執行新增至Maven程式集外掛程式，如下所示。

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

此執行會指示Maven程式集外掛程式根據 `assembly-ui-test-docker-context.xml`，稱為 **裝配描述符** 用外掛程式的術語。 程式集描述符列出必須是歸檔檔案一部分的所有檔案。

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

程式集描述符指示插件建立類型的存檔 `.tar.gz` 並指派 `ui-test-docker-context` 分類器。 此外，它還列出了必須包含在存檔中的檔案，包括以下內容。

* A `Dockerfile`，是建置Docker影像的必填項目
* 此 `wait-for-grid.sh` 指令碼，其用途如下所述
* 實際的UI測試，由 `test-module` 資料夾

程式集描述符還排除了在本地運行UI測試時可能生成的一些檔案。 這可保證檔案的規模更小，組建更快。

包含Docker建置上下文的封存會由Cloud Manager自動擷取，Cloud Manager會在部署管道期間建立包含您測試的Docker影像。 最終，Cloud Manager會執行Docker影像，對您的應用程式執行UI測試。

組建應產生零或一個封存。 如果它生成零存檔，則預設情況下測試步驟會通過。 如果組建產生多個封存，選取的封存則不確定。

## 編寫UI測試 {#writing-ui-tests}

本節說明包含您UI測試的Docker影像必須遵循的慣例。 Docker映像是使用前一節中描述的Docker生成上下文構建的。

### 環境變數 {#environment-variables}

下列環境變數將在執行時傳遞至您的Docker影像。

| 變數 | 範例 | 說明 |
|---|---|---|
| `SELENIUM_BASE_URL` | `http://my-ip:4444` | Selenium伺服器的URL |
| `SELENIUM_BROWSER` | `chrome` | Selenium Server使用的瀏覽器實施 |
| `AEM_AUTHOR_URL` | `http://my-ip:4502/context-path` | AEM製作例項的URL |
| `AEM_AUTHOR_USERNAME` | `admin` | 登入AEM製作例項的使用者名稱 |
| `AEM_AUTHOR_PASSWORD` | `admin` | 登入AEM製作例項的密碼 |
| `AEM_PUBLISH_URL` | `http://my-ip:4503/context-path` | AEM發佈例項的URL |
| `AEM_PUBLISH_USERNAME` | `admin` | 登入AEM發佈執行個體的使用者名稱 |
| `AEM_PUBLISH_PASSWORD` | `admin` | 登入AEM發佈執行個體的密碼 |
| `REPORTS_PATH` | `/usr/src/app/reports` | 必須保存測試結果的XML報告的路徑 |
| `UPLOAD_URL` | `http://upload-host:9090/upload` | 必須上傳檔案的URL，以便供Selenium存取 |

### 等待硒準備就緒 {#waiting-for-selenium}

在測試開始之前，Docker映像有責任確保Selenium伺服器已啟動並運行。 等待Selenium服務是兩步驟的過程。

1. 從 `SELENIUM_BASE_URL` 環境變數。
1. 以定期間隔輪詢至 [狀態端點](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready) 由Selenium API公開。

一旦Selenium的狀態端點以正面回應回答，測試就可以開始。

### 產生測試報表 {#generate-test-reports}

Docker映像必須以JUnit XML格式生成測試報告，並將其保存在環境變數指定的路徑中 `REPORTS_PATH`. JUnit XML格式是報告測試結果的廣泛使用的格式。 如果Docker影像使用Java和Maven，則標準測試模組如 [Maven Surefire外掛程式](https://maven.apache.org/surefire/maven-surefire-plugin/) 和 [Maven Failsafe Plugin](https://maven.apache.org/surefire/maven-failsafe-plugin/) 可立即產生這類報表。

如果Docker影像是使用其他寫程式語言或測試運行者實現的，請查看所選工具的文檔，以了解如何生成JUnit XML報告。

### 上傳檔案 {#upload-files}

測試有時必須將檔案上傳至要測試的應用程式。 為了讓Selenium的部署相對於您的測試保持靈活，無法直接將資產上傳至Selenium。 但是，上傳檔案需要下列步驟。

1. 在 `UPLOAD_URL` 環境變數。
   * 上傳必須以一個包含多部分表單的POST請求執行。
   * 多部分表單必須有單一檔案欄位。
   * 這等同於 `curl -X POST ${UPLOAD_URL} -F "data=@file.txt"`.
   * 請參閱Docker影像中使用之程式設計語言的檔案和程式庫，了解如何執行此類HTTP要求。
1. 如果上傳成功，要求會傳回 `200 OK` 類型的回應 `text/plain`.
   * 回應的內容是不透明的檔案控點。
   * 您可以使用此控制代碼來取代 `<input>` 元素來測試應用程式中的檔案上傳。
