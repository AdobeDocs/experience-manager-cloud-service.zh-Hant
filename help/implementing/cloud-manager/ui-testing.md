---
title: UI測試 — Cloud Services
description: UI測試 — Cloud Services
exl-id: 3009f8cc-da12-4e55-9bce-b564621966dd
source-git-commit: 02db915e114c2af8329eaddbb868045944a3574d
workflow-type: tm+mt
source-wordcount: '1617'
ht-degree: 0%

---

# UI測試 {#ui-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_uitesting"
>title="UI測試"
>abstract="UI測試是封裝在Docker影像中的基於硒的測試，以允許在語言和框架（如Java和Maven、Node和WebDriver.io，或基於Selenium構建的任何其他框架和技術）中進行廣泛選擇。 Docker映像可以使用標準工具建立，但在執行時必須遵守某些慣例。 運行Docker映像時，會自動布建Selenium伺服器。 下述的執行階段慣例可讓您的測試程式碼存取所測試的Selenium伺服器和AEM例項。"

UI測試是封裝在Docker影像中的基於硒的測試，以允許在語言和框架（如Java和Maven、Node和WebDriver.io，或基於Selenium構建的任何其他框架和技術）中進行廣泛選擇。 Docker映像可以使用標準工具建立，但在執行時必須遵守某些慣例。 運行Docker映像時，會自動布建Selenium伺服器。 下述的執行階段慣例可讓您的測試程式碼存取所測試的Selenium伺服器和AEM例項。

>[!NOTE]
> 2021年2月10日之前建立的預備和生產管道必須更新，才能使用本頁面所述的UI測試。
> 請參閱 [Cloud Manager中的CI-CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) 以取得管道設定的相關資訊。

## 自訂UI測試 {#custom-ui-testing}

AEM為其客戶提供整合的Cloud Manager品質閘門套裝，確保應用程式能順暢地更新。 尤其是，IT測試閘道已允許客戶建立並使用AEM API的自動化測試。

自訂UI測試功能是 [可選功能](#customer-opt-in) 可讓客戶建立並自動執行其應用程式的UI測試。 UI測試是封裝在Docker影像中的基於硒的測試，以允許在語言和框架（如Java和Maven、Node和WebDriver.io，或基於Selenium構建的任何其他框架和技術）中進行廣泛選擇。 您可以從這裡進一步了解如何建立UI和撰寫UI測試。 此外，使用AEM專案原型即可輕鬆產生UI測試專案。

客戶可以建立（透過GIT）自訂測試，以及使用者介面的測試套裝。 UI測試將隨著每個Cloud Manager管道的特定品質閘道執行，並包含其特定步驟和意見資訊。 任何UI測試（包括回歸和新功能）都可讓您在客戶內容中偵測和報告錯誤。

在「自訂UI測試」步驟下，客戶UI測試會自動在生產管道上執行。

自訂功能測試是以java撰寫的HTTP測試，而UI測試可以是Docker影像，且測試以任何語言撰寫，只要測試遵循 [建立UI測試](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/ui-testing.html?lang=en#building-ui-tests).

>[!NOTE]
>建議您遵循架構和語言 *（js和wdio）* 方便地提供於 [AEM專案原型](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests) 作為起點。

### 客戶選擇加入 {#customer-opt-in}

若要建置並執行其UI測試，客戶需要在UI測試的maven子模組（位於UI測試子模組的pom.xml檔案旁）下，將檔案新增至其程式碼存放庫，以「選擇加入」，並確認此檔案位於建置的根目錄 `tar.gz` 檔案。

*檔案名*: `testing.properties`

*內容*: `ui-tests.version=1`

如果不在建置中 `tar.gz` 檔案中，系統會略過UI測試建置和執行

若要新增 `testing.properties` 檔案，添加 `include` 語句 `assembly-ui-test-docker-context.xml` 檔案（在UI測試子模組中）。 如果您的專案未包含該行，則您需要編輯此檔案以選擇加入UI測試。 如果檔案中可能有一行建議不要編輯，請忽略該建議。

    &quot;
    [...]
    &lt;includes>
    &lt;include>Dockerfile&lt;/include>
    &lt;include>wait-for-grid.sh&lt;/include>
    &lt;include>testing.properties&lt;/include> &lt;!>- Cloud Manager中的選擇加入測試模組 — >
    &lt;/includes>
    [...]
    &quot;

>[!NOTE]
>2021年2月10日之前建立的生產管道必須更新，才能使用本節所述的UI測試。 這基本上表示使用者必須編輯生產管道，然後按一下 **儲存** 即使未進行任何變更，仍可從UI執行。
>請參閱 [設定CI-CD管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en#using-cloud-manager) 深入了解管道設定。

## 建立UI測試 {#building-ui-tests}

UI測試是以Maven專案產生的Docker建置內容建置而成。 Cloud Manager會使用Docker建置內容來產生包含實際UI測試的Docker影像。 總之，Maven專案會產生Docker建置內容，而Docker建置內容則說明如何建立包含UI測試的Docker影像。

本節將說明將UI測試專案新增至存放庫所需的步驟。 如果您匆忙或對程式設計語言沒有特殊要求， [AEM專案原型](https://github.com/adobe/aem-project-archetype) 可以為您產生UI測試專案。

### 生成Docker生成上下文 {#generate-docker-build-context}

若要產生Docker建置內容，您需要Maven模組，該模組應：

- 產生包含 `Dockerfile` 以及使用測試建立Docker映像所需的所有其他檔案。
- 使用標籤封存 `ui-test-docker-context` 分類器。

要達成此目標，最簡單的方式是設定 [Maven程式集外掛程式](http://maven.apache.org/plugins/maven-assembly-plugin/) 來建立Docker構建上下文歸檔檔案，並為其分配正確的分類器。

您可以使用不同的技術和架構來建立UI測試，但本節假設您的專案是以類似下列的方式規劃。

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

此執行會指示Maven程式集外掛程式根據 `assembly-ui-test-docker-context.xml`，在外掛程式的行話中稱為「程式集描述元」。 程式集描述符列出必須是歸檔檔案一部分的所有檔案。

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

程式集描述符指示插件建立類型的存檔 `.tar.gz` 並指派 `ui-test-docker-context` 分類器。 此外，它還列出了必須包含在存檔中的檔案：

- A `Dockerfile`，此為建置Docker影像的必要項目。
- 此 `wait-for-grid.sh` 指令碼，其用途如下所述。
- 實際的UI測試，由 `test-module` 檔案夾。

程式集描述符還排除了在本地運行UI測試時可能生成的一些檔案。 這可保證檔案的規模更小，組建更快。

包含Docker建置上下文的封存會由Cloud Manager自動擷取，Cloud Manager會在其部署管道期間建立包含您測試的Docker影像。 最終，Cloud Manager會執行Docker影像，對您的應用程式執行UI測試。

組建應產生零或一個封存。 如果產生零封存，則測試步驟預設會通過。 如果組建產生多個封存，選取的封存則不確定。

## 編寫UI測試 {#writing-ui-tests}

本節說明包含您UI測試的Docker影像必須遵循的慣例。 Docker映像是使用前一節中描述的Docker生成上下文構建的。

### 環境變數 {#environment-variables}

下列環境變數將在執行時傳遞至您的Docker影像。

| 變數 | 範例 | 說明 |
|---|---|---|
| `SELENIUM_BASE_URL` | `http://my-ip:4444` | Selenium伺服器的URL |
| `SELENIUM_BROWSER` | `chrome`, `firefox` | Selenium Server使用的瀏覽器實施 |
| `AEM_AUTHOR_URL` | `http://my-ip:4502/context-path` | AEM製作例項的URL |
| `AEM_AUTHOR_USERNAME` | `admin` | 登入AEM製作例項的使用者名稱 |
| `AEM_AUTHOR_PASSWORD` | `admin` | 登入AEM製作例項的密碼 |
| `AEM_PUBLISH_URL` | `http://my-ip:4503/context-path` | AEM發佈例項的URL |
| `AEM_PUBLISH_USERNAME` | `admin` | 登入AEM發佈例項的使用者名稱 |
| `AEM_PUBLISH_PASSWORD` | `admin` | 登入AEM發佈執行個體的密碼 |
| `REPORTS_PATH` | `/usr/src/app/reports` | 必須保存測試結果的XML報告的路徑 |
| `UPLOAD_URL` | `http://upload-host:9090/upload` | 必須上傳檔案的URL，以便供Selenium存取 |

### 等待硒準備就緒 {#waiting-for-selenium}

在測試開始之前，Docker映像有責任確保Selenium伺服器已啟動並運行。 等待Selenium服務是兩個步驟的過程：

1. 從 `SELENIUM_BASE_URL` 環境變數。
2. 以定期間隔輪詢至 [狀態端點](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready) 由Selenium API公開。

一旦Selenium的狀態端點以正面回應回應，測試就可以最終開始。

### 產生測試報表 {#generate-test-reports}

Docker映像必須以JUnit XML格式生成測試報告，並將其保存在環境變數指定的路徑中 `REPORTS_PATH`. JUnit XML格式是報告測試結果的廣泛格式。 如果Docker影像使用Java和Maven，則兩者 [Maven Surefire外掛程式](https://maven.apache.org/surefire/maven-surefire-plugin/) 和 [Maven Failsafe Plugin](https://maven.apache.org/surefire/maven-failsafe-plugin/). 如果Docker映像是使用其他寫程式語言或測試運行程式實現的，請查看所選工具的文檔，以了解如何生成JUnit XML報告。

### 上傳檔案 {#upload-files}

測試有時必須將檔案上傳至要測試的應用程式。 為了維持相對於測試的Selenium部署具有彈性，無法直接將資產上傳至Selenium。 請改為上傳檔案，以執行一些中間步驟：

1. 在 `UPLOAD_URL` 環境變數。 上傳必須以一個包含多部分表單的POST請求執行。 多部分表單必須有單一檔案欄位。 這等同於 `curl -X POST ${UPLOAD_URL} -F "data=@file.txt"`. 請參閱Docker影像中使用之程式設計語言的檔案和程式庫，了解如何執行此類HTTP要求。
2. 如果上傳成功，要求會傳回 `200 OK` 類型的回應 `text/plain`. 回應的內容是不透明的檔案控點。 您可以使用此控制代碼來取代 `<input>` 元素來測試應用程式中的檔案上傳。
