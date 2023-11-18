---
title: UI 測試
description: 自訂 UI 測試是一項選擇性功能，可讓您為自訂應用程式建立和自動執行 UI 測試。
exl-id: 3009f8cc-da12-4e55-9bce-b564621966dd
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '2385'
ht-degree: 98%

---


# UI 測試 {#ui-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_uitesting"
>title="UI 測試"
>abstract="自訂 UI 測試是一項選擇性功能，可讓您為應用程式建立和自動執行 UI 測試。UI 測試是封裝在 Docker 影像中的 Selenium 型測試，以便在語言和架構 (例如 Java 和 Maven、Node 和 WebDriver.io 或任何其他根據 Selenium 建置的架構和技術) 中提供廣泛的選擇。"

自訂 UI 測試是一項選擇性功能，可讓您為應用程式建立和自動執行 UI 測試。

## 概觀 {#custom-ui-testing}

AEM 提供了[Cloud Manager 品質關卡](/help/implementing/cloud-manager/custom-code-quality-rules.md)整合套件，以確保自訂應用程序順利更新。尤其是 IT 測試門已經支援使用 AEM API 建立和自動化自訂測試。

UI 測試是封裝在 Docker 映像檔中，提供廣泛的語言和架構 (例如 Cypress、Selenium、Java 和 Maven 以及 JavaScript) 選擇。此外，UI測試專案可以透過使用輕鬆生成 [AEM專案原型。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)

Adobe 鼓勵使用 Cypress，因為它提供即時重新載入和自動等待功能，有助於節省時間及提高測試期間的工作效率。Cypress 也提供簡單直覺的語法，容易學習和使用，即使是測試的初學者也能輕易上手。

UI 測試是每個 Cloud Manager 管道特定品質把關程序的一環，在[生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)或可選擇[非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)中具有&#x200B;[**自訂 UI 測試**&#x200B;步驟](/help/implementing/cloud-manager/deploy-code.md)。包括回歸和新功能在內的任何 UI 測試都可以偵測和報告錯誤。

自訂功能測試是使用 Java 編寫的 HTTP 測試，但 UI 測試並不相同，它可以是使用任何語言編寫的 Docker 映像，只要遵循「[建置 UI 測試](#building-ui-tests)」小節中定義的慣例即可。

>[!TIP]
>
>Adobe 建議使用 Cypress 進行 UI 測試，按照 [AEM 測試範例存放庫](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-cypress)所提供的代碼。
> 
>Adobe 也提供以 JavaScript 搭配 WebdriverIO 為基礎 (請參閱 [AEM 專案原型](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)) 和以 Java 搭配 WebDriver 為基礎 (請參閱 [AEM 測試範例存放庫](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-selenium-webdriver)) 的 UI 測試模組。

## 開始使用 UI 測試 {#get-started-ui-tests}

本節旨在說明設定 UI 測試以便在 Cloud Manager 中執行所需的步驟。

1. 確定您要使用的編程語言。

   * 若為 Cypress，請使用 [AEM 測試範例存放庫](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-cypress)中的範例程式碼。

   * 若為 JavaScript 和 WDIO，請使用在 Cloud Manager 存放庫 `ui.tests` 資料夾中自動產生的範例程式碼。

     >[!NOTE]
     >
     >如果您的存放庫是在 Cloud Manager 自動建立 `ui.tests` 資料夾之前所建立，您還可以使用 [AEM 專案原型產生最新版本](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)。

   * 若是 Java 和 WebDriver，請使用 [AEM 測試範例存放庫](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-selenium-webdriver)中的範例程式碼。

   * 若為其他程式語言，請參閱本文件的「[建立 UI 測試](#building-ui-tests)」章節來設定測試專案。

1. 務必根據本文件的「[客戶選擇加入](#customer-opt-in)」章節來啟動 UI 測試。

1. 開發您的測試案例並[在本機執行這些測試](#run-ui-tests-locally)。

1. 將您的程式碼提交到 Cloud Manager 存放庫並執行 Cloud Manager 管道。

## 構建 UI 測試 {#building-ui-tests}

一個 Maven 項目會產生一個 Docker 建置內容。此 Docker 建置內容旨在說明如何建立包含 UI 測試的 Docker 映像，Cloud Manager 會用來透過該影像產生包含實際 UI 測試的 Docker 映像。

本節介紹將 UI 測試項目新增到存放庫所需的步驟。

>[!TIP]
>
>這 [AEM Project 原型](https://github.com/adobe/aem-project-archetype)可以為您產生 UI 測試專案 (遵照以下說明來測試)，但前提是您對編程語言沒有特殊要求。

### 產生 Docker 建置內容 {#generate-docker-build-context}

若要產生 Docker 建置環境，您需要一個 Maven 模組：

* 產生一個包含`Dockerfile`以及使用您的測試構建 Docker 映像所需的所有其他文件。
* 用`ui-test-docker-context`分類器。

最簡單的方法是配置 [Maven 組裝插件](https://maven.apache.org/plugins/maven-assembly-plugin/)建立 Docker 建置內容封存並為其指派正確的分類器。

您可以使用不同的技術和框架構建 UI 測試，但本節假定您的項目以類似於以下方式佈局。

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

這`pom.xml`文件負責 Maven 構建。將執行新增到 Maven 程序集插件，類似於以下內容。

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

此執行指示 Maven 程序集插件根據包含在`assembly-ui-test-docker-context.xml`，稱為&#x200B;**程序集描述符**&#x200B;在插件的行話中。程序集描述符列出了必須是歸檔一部分的所有文件。

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

程序集描述符指示插件建立類型的封存`.tar.gz`並指派`ui-test-docker-context`分類器。此外，它列出了必須包含在封存中的文件，包括以下內容。

* 一個 `Dockerfile`，構建 Docker 鏡像所必需的
* `wait-for-grid.sh` 腳本，其用途如下所述
* 由 Node.js 項目實現的實際 UI 測試`test-module`資料夾

程序集描述符還排除了在本機執行 UI 測試時可能產生的一些文件。這保證了更小的封存和更快的建構。

包含 Docker 建置內容的封存由 Cloud Manager 自動獲取，它將在其部署管道期間構建包含您的測試的 Docker 映像。最終，Cloud Manager 將執行 Docker 映像以針對您的應用程序執行 UI 測試。

建構應產生零個或一個封存。如果產生零個封存，則測試步驟預設透過。如果建置產生多個封存，則無法確定要選擇哪個封存。

### 客戶選擇加入 {#customer-opt-in}

為了讓 Cloud Manager 建置和執行您的 UI 測試，您必須在存放庫新增一個檔案來選擇加入此功能。

* 檔案名稱必須是 `testing.properties`。
* 檔案內容必須是 `ui-tests.version=1`。
* 該檔案必須位於 maven 子模組下，用於 UI 測試`pom.xml`UI 測試子模組的文件。
* 該檔案必須位於建置的 `tar.gz` 檔案根目錄。

如果此檔案不存在，將跳過 UI 測試組建和執行。

若要在組建成品包含 `testing.properties` 檔案，在 `assembly-ui-test-docker-context.xml` 檔案中新增 `include` 陳述式。

```xml
[...]
<includes>
    <include>Dockerfile</include>
    <include>wait-for-grid.sh</include>
    <include>testing.properties</include> <!-- opt-in test module in Cloud Manager -->
</includes>
[...]
```

>[!NOTE]
>
>如果您的專案不包含此行，請編輯檔案以選擇進行UI測試。
>
>該檔案可能包含一條建議不要編輯它的行。這是因為在採用選擇加入的 UI 測試之前，便已採用此項目，而客戶不打算編輯該檔案。您可以安心忽略這件事。

如果您是使用 Adobe 提供的範例：

* 若是基於來自 [AEM 專案原型](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests) 產生以 JavaScript 為主的 `ui.tests` 資料夾，您可以執行以下命令以新增所需的設定。

  ```shell
  echo "ui-tests.version=1" > testing.properties
  
  if ! grep -q "testing.properties" "assembly-ui-test-docker-context.xml"; then
    awk -v line='                <include>testing.properties</include>' '/<include>wait-for-grid.sh<\/include>/ { printf "%s\n%s\n", $0, line; next }; 1' assembly-ui-test-docker-context.xml > assembly-ui-test-docker-context.xml.new && mv assembly-ui-test-docker-context.xml.new assembly-ui-test-docker-context.xml
  fi
  ```

* Adobe 所提供的 Cypress 與 Java Selenium 測試範例已經設定好選擇加入的標幟。

## 編寫 UI 測試 {#writing-ui-tests}

本節介紹包含 UI 測試的 Docker 映像必須遵循的約定。Docker 映像是根據上一節中描述的 Docker 建置內容建構的。

### 環境變數 {#environment-variables}

以下環境變數會在執行階段傳遞給您的 Docker 映像，視您的架構而定。

| 變數 | 範例 | 說明 | 測試架構 |
|---|---|---|---|
| `SELENIUM_BASE_URL` | `http://my-ip:4444` | Selenium 伺服器的 URL | 僅限 Selenium |
| `SELENIUM_BROWSER` | `chrome` | Selenium 伺服器使用的瀏覽器實作 | 僅限 Selenium |
| `AEM_AUTHOR_URL` | `http://my-ip:4502/context-path` | AEM 編寫執行個體的 URL | 全部 |
| `AEM_AUTHOR_USERNAME` | `admin` | 用於登入 AEM 編寫執行個體的使用者名稱 | 全部 |
| `AEM_AUTHOR_PASSWORD` | `admin` | 用於登入 AEM 編寫執行個體的密碼 | 全部 |
| `AEM_PUBLISH_URL` | `http://my-ip:4503/context-path` | AEM 發佈執行個體的 URL | 全部 |
| `AEM_PUBLISH_USERNAME` | `admin` | 用於登入 AEM 發佈執行個體的使用者名稱 | 全部 |
| `AEM_PUBLISH_PASSWORD` | `admin` | 用於登入 AEM 發佈執行個體的密碼 | 全部 |
| `REPORTS_PATH` | `/usr/src/app/reports` | 測試結果 XML 報告必須儲存的路徑 | 全部 |
| `UPLOAD_URL` | `http://upload-host:9090/upload` | 必須將檔案上傳到的 URL，以便測試架構可以存取 | 全部 |

Adobe 測試範例提供輔助函數以存取設定參數：

* Cypress: 使用標準函數 `Cypress.env('VARIABLE_NAME')`
* JavaScript：參閱 [lib/config.js](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/test-module/lib/config.js) 模組
* Java：參閱 [Config](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/Config.java) 類別

### 產生測試報告 {#generate-test-reports}

Docker 鏡像必須產生 JUnit XML 格式的測試報告，並保存在環境變數 `REPORTS_PATH` 指定的路徑中。JUnit XML 格式是廣泛使用的測試結果報告格式。如果 Docker 鏡像使用 Java 和 Maven，標準測試模組如 [Maven Surefire 插件](https://maven.apache.org/surefire/maven-surefire-plugin/)和 [Maven 故障安全插件](https://maven.apache.org/surefire/maven-failsafe-plugin/)可以開箱即用地產生此類報告。

如果 Docker 映像是使用其他編程語言或測試執行計畫實現的，請查看所選工具的文件以了解如何產生 JUnit XML 報告。

>[!NOTE]
>
>UI 測試步驟的結果僅根據測試報告進行評估。確保為您的測試執行產生相應的報告。
>
>使用斷言而不是僅將錯誤記錄到 STDERR 或返回非零退出程式碼，否則您的部署管道可能會正常進行。

### 必備條件 {#prerequisites}

* Cloud Manager 中的測試是透過技術管理員使用者來執行。

>[!NOTE]
>
>若要從本機電腦執行功能測試，請建立一個具備類似管理員權限的使用者來達到相同的行為。

* 用於功能測試的容器化基礎架構受以下界限限制：

| 類型 | 值 | 說明 |
|----------------------|-------|-----------------------------------------------------------------------|
| CPU | 2.0 | 每次測試執行保留的 CPU 時間量 |
| 記憶體 | 1Gi | 分配給測試的記憶體數量，其值以 gibibyte 為單位 |
| 逾時 | 30m | 測試持續時間。 |
| 建議的持續時間 | 15m | Adobe 建議所編寫的測試不應花費超過這個時間。 |

>[!NOTE]
>
> 如果您需要更多資源，請建立客戶服務案例並描述您的使用案例；Adobe 的團隊將檢閱您的要求並提供適當的幫助。

## Selenium 特定的詳細資訊

>[!NOTE]
>
>本節僅在選擇 Selenium 作為測試基礎結構時適用。

### 等待 Selenium 準備就緒 {#waiting-for-selenium}

在測試開始之前，Docker 影像負責確保 Selenium 伺服器啟動並執行。等待 Selenium 服務有兩個步驟。

1. 從 `SELENIUM_BASE_URL` 環境變數中讀取 Selenium 服務的 URL。
1. 定期輪詢 Selenium API 公開的[狀態端點](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready)。

一旦 Selenium 的狀態端點得到肯定的響應，測試就可以開始了。

Adobe UI 測試範例使用指令碼 `wait-for-grid.sh` 處理此問題，該指令碼在 Docker 啟動時執行，並且僅在網格準備就緒後才開始實際測試執行。

### 擷取螢幕擷圖和影片 {#capture-screenshots}

Docker 映像檔可能會產生額外的測試輸出 (例如螢幕擷圖或影片)，並保存在環境變數 `REPORTS_PATH` 指定的路徑中。在 `REPORTS_PATH` 下找到的任何檔案都包含在測試結果封存檔中。

Adobe 提供的測試範例依預設為任何失敗的測試建立螢幕擷圖。

您可以使用輔助函數通過測試建立螢幕擷圖。

* JavaScript：[takeScreenshot 命令](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/test-module/lib/commons.js)
* Java：[命令](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/Commands.java)

如果在 UI 測試執行期間建立測試結果存檔，您可以使用&#x200B;[**自訂 UI 測試**&#x200B;步驟](/help/implementing/cloud-manager/deploy-code.md)下的 `Download Details` 按鈕從 Cloud Manager 下載。

### 上傳檔案 {#upload-files}

測試有時必須將文件上傳到被測試的應用程式。為了使 Selenium 的部署對您的測試保持相對的靈活性，無法直接把資產上傳到 Selenium。相反，上傳文件需要以下步驟。

1. 在指定的 URL 上傳檔案 `UPLOAD_URL` 環境變數。
   * 上傳必須在一個帶有多部分表單的 POST 要求中執行。
   * 多部分表單必須有一個檔案欄位。
   * 這相當於 `curl -X POST ${UPLOAD_URL} -F "data=@file.txt"`。
   * 請查閱 Docker 映像中使用的編程語言的檔案和資料庫，以了解如何執行此類 HTTP 要求。
   * Adobe 測試範本提供了用於上傳文件的輔助函數：
      * JavaScript：請參閱 [getFileHandleForUpload](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/test-module/lib/wdio.commands.js) 命令。
      * Java：參閱 [FileHandler](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/FileHandler.java) 類別。
1. 如果上傳成功，請求傳回一個`200 OK`類型響應 `text/plain`。
   * 回應的內容是一個不透明的檔案。
   * 您可以使用此句柄代替文件路徑`<input>`在您的應用程序中測試文件上傳的元素。

## 在本機執行 UI 測試 {#run-ui-tests-locally}

在 Cloud Manager 管道啟用 UI 測試之前，建議在本機針對 [AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) 或實際的 AEM as a Cloud Service 執行個體執行 UI 測試。

### Cypress 測試範例 {#cypress-sample}

1. 打開 shell 並瀏覽至存放庫中的 `ui.tests/test-module` 資料夾

1. 安裝 Cypress 和其他必備條件

   ```shell
   npm install
   ```

1. 設定測試執行所需的環境變數

   ```shell
   export AEM_AUTHOR_URL=https://author-<program-id>-<environment-id>.adobeaemcloud.com
   export AEM_AUTHOR_USERNAME=<user>
   export AEM_AUTHOR_PASSWORD=<password>
   export AEM_PUBLISH_URL=https://publish-<program-id>-<environment-id>.adobeaemcloud.com
   export AEM_PUBLISH_USERNAME=<user>
   export AEM_PUBLISH_PASSWORD=<password>
   export REPORTS_PATH=target/
   ```

1. 使用以下其中一項命令執行測試

   ```shell
   npm test              # Using default Cypress browser
   npm run test-chrome   # Using Google Chrome browser
   npm run test-firefox  # Using Firefox browser
   ```

>[!NOTE]
>
>記錄檔案會儲存在您的存放庫的 `target/` 資料夾中。
>
>如需詳細資訊，請參閱 [AEM 測試範例存放庫](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-cypress/test-module/README.md)。

### JavaScript WebdriverIO 測試範例 {#javascript-sample}

1. 打開 shell 並瀏覽至存放庫中的 `ui.tests` 資料夾

1. 執行以下命令以使用 Maven 啟動測試

   ```shell
   mvn verify -Pui-tests-local-execution \
    -DAEM_AUTHOR_URL=https://author-<program-id>-<environment-id>.adobeaemcloud.com \
    -DAEM_AUTHOR_USERNAME=<user> \
    -DAEM_AUTHOR_PASSWORD=<password> \
    -DAEM_PUBLISH_URL=https://publish-<program-id>-<environment-id>.adobeaemcloud.com \
    -DAEM_PUBLISH_USERNAME=<user> \
    -DAEM_PUBLISH_PASSWORD=<password>
   ```

>[!NOTE]
>
>* 這樣會啟動一個獨立的 selenium 執行個體並對其執行測試。
>* 記錄檔案會儲存在您的存放庫的 `target/reports` 資料夾中
>* 請務必確定您的電腦執行最新版本的 Chrome，因為測試會自動下載最新版的 ChromeDriver 以進行測試。
>
>如需詳細資訊，請參閱 [AEM 專案原型存放庫](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/README.md)。

### Java Selenium WebDriver 測試範例 {#java-sample}

1. 打開 shell 並瀏覽至存放庫中的 `ui.tests/test-module` 資料夾

1. 執行以下命令以使用 Maven 啟動測試

   ```shell
   # Start selenium docker image (for x64 CPUs)
   docker run --platform linux/amd64 -d -p 4444:4444 selenium/standalone-chrome-debug:latest
   
   # Start selenium docker image (for ARM CPUs)
   docker run -d -p 4444:4444 seleniarm/standalone-chromium
   
   # Run the tests using the previously started Selenium instance
   mvn verify -Pui-tests-local-execution -DSELENIUM_BASE_URL=http://<server>:4444
   ```

>[!NOTE]
>
>記錄檔案會儲存在您的存放庫的 `target/reports` 資料夾中.
>
>如需詳細資訊，請參閱 [AEM 測試範例存放庫](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/README.md)。
