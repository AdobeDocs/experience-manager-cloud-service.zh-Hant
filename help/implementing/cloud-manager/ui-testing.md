---
title: UI 測試
description: 自訂 UI 測試是一項選擇性功能，可讓您為自訂應用程式建立和自動執行 UI 測試。
exl-id: 3009f8cc-da12-4e55-9bce-b564621966dd
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: 770318fd14e28c8406650eb563df36fe88227359
workflow-type: tm+mt
source-wordcount: '2662'
ht-degree: 53%

---


# UI 測試 {#ui-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_uitesting"
>title="UI 測試"
>abstract="自訂 UI 測試是一項選擇性功能，可讓您為應用程式建立和自動執行 UI 測試。UI測試是封裝在Docker影像中的Selenium型測試，以便在語言和架構中提供廣泛的選擇。 例如Java和Maven、Node和WebDriver.io，或任何其他以Selenium為基礎的架構和技術。"

自訂 UI 測試是一項選擇性功能，可讓您為應用程式建立和自動執行 UI 測試。

## 概觀 {#custom-ui-testing}

AEM 提供了[Cloud Manager 品質關卡](/help/implementing/cloud-manager/custom-code-quality-rules.md)整合套件，以確保自訂應用程序順利更新。尤其是 IT 測試門已經支援使用 AEM API 建立和自動化自訂測試。

UI 測試是封裝在 Docker 映像檔中，提供廣泛的語言和架構 (例如 Cypress、Selenium、Java 和 Maven 以及 JavaScript) 選擇。此外，使用[AEM專案原型](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/developing/archetype/overview)可輕鬆產生UI測試專案。

Adobe 鼓勵使用 Cypress，因為它提供即時重新載入和自動等待功能，有助於節省時間及提高測試期間的工作效率。Cypress也提供簡單且直覺式的語法，讓您輕鬆學習及使用，即使是初次測試的使用者亦然。

UI測試會在&#x200B;[**自訂UI測試**](/help/implementing/cloud-manager/deploy-code.md)&#x200B;步驟中作為品質閘道執行 — 在[生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)中是必要的，在[非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)中是選用的。 包括回歸和新功能在內的任何 UI 測試都可以偵測和報告錯誤。

與使用Java編寫的HTTP測試的自訂功能測試不同，UI測試可以是Docker映像。 只要測試遵循區段[建置UI測試](#building-ui-tests)中定義的慣例，就可以使用任何語言編寫測試。

>[!TIP]
>
>Adobe 建議使用 Cypress 進行 UI 測試，按照 [AEM 測試範例存放庫](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-cypress)所提供的代碼。
> 
>Adobe 也提供以 JavaScript 搭配 WebdriverIO 為基礎 (請參閱 [AEM 專案原型](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)) 和以 Java 搭配 WebDriver 為基礎 (請參閱 [AEM 測試範例存放庫](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-selenium-webdriver)) 的 UI 測試模組。

## 開始使用UI測試 {#get-started-ui-tests}

本節旨在說明設定 UI 測試以便在 Cloud Manager 中執行所需的步驟。

1. 決定您要使用的測試架構。

   * 對於Cypress （預設），請使用[AEM測試範例存放庫](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-cypress)中的範常式式碼，或使用在Cloud Manager存放庫的`ui.tests`資料夾中自動產生的範常式式碼。

   * 對於Playwright，請使用[AEM測試範例存放庫](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-playwright)中的範常式式碼。

   * 對於Webdriver.IO，請使用[AEM測試範例存放庫](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-wdio)中的範常式式碼。

   * 對於Selenium WebDriver，請使用[AEM測試範例存放庫](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-selenium-webdriver)中的範常式式碼。

   * 若為其他程式語言，請參閱本文件的「[建立 UI 測試](#building-ui-tests)」章節來設定測試專案。

1. 務必根據本文件的「[客戶選擇加入](#customer-opt-in)」章節來啟動 UI 測試。

1. 開發您的測試案例並[在本機執行這些測試](#run-ui-tests-locally)。

1. 將您的程式碼提交到 Cloud Manager 存放庫並執行 Cloud Manager 管道。

## 建立UI測試 {#building-ui-tests}

一個 Maven 項目會產生一個 Docker 建置內容。此 Docker 建置內容旨在說明如何建立包含 UI 測試的 Docker 映像，Cloud Manager 會用來透過該影像產生包含實際 UI 測試的 Docker 映像。

本節介紹將 UI 測試項目新增到存放庫所需的步驟。

>[!TIP]
>
>這 [AEM Project 原型](https://github.com/adobe/aem-project-archetype)可以為您產生 UI 測試專案 (遵照以下說明來測試)，但前提是您對編程語言沒有特殊要求。

### 生成Docker構建上下文 {#generate-docker-build-context}

若要產生 Docker 建置環境，您需要一個 Maven 模組：

* 產生一個包含`Dockerfile`以及使用您的測試構建 Docker 映像所需的所有其他文件。
* 用`ui-test-docker-context`分類器。

最簡單的方法是配置[Maven組裝外掛](https://maven.apache.org/plugins/maven-assembly-plugin/)建立Docker構建上下文封存並為其指派正確的分類器。

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

程序集描述符指示插件建立類型的封存`.tar.gz`並指派`ui-test-docker-context`分類器。此外，它列出了必須包含在封存中的檔案，包括以下內容：

* 一個 `Dockerfile`，構建 Docker 映像所必需的
* `wait-for-grid.sh` 腳本，其用途如下所述
* 由 Node.js 項目實現的實際 UI 測試`test-module`資料夾

程序集描述符還排除了在本機執行 UI 測試時可能產生的一些文件。這保證了更小的封存和更快的建構。

Cloud Manager在部署管道期間自動提取Docker build-context封存並構建測試映像。 最後，Cloud Manager會執行Docker影像，對您的應用程式執行UI測試。

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

>[!IMPORTANT]
>
>如果您的專案不包含此行，請編輯檔案以選擇進行UI測試。
>
>檔案可能包含一行，顯示&#x200B;*DO NOT MODIFY*。 這只是舊版範本/範例的舊版警告，並&#x200B;*不會*&#x200B;阻止您進行Cloud Manager UI測試所需的選擇加入編輯。 您可以安全地忽略建議；遵循選擇加入步驟時（例如，加入`assembly-ui-test-docker-context.xml`），您可以在`pom.xml`您的專案&#x200B;*中編輯*&#x200B;和`testing.properties`。

如果您是使用 Adobe 提供的範例：

* 若是基於來自 [AEM 專案原型](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests) 產生以 JavaScript 為主的 `ui.tests` 資料夾，您可以執行以下命令以新增所需的設定。

  ```shell
  echo "ui-tests.version=1" > testing.properties
  
  if ! grep -q "testing.properties" "assembly-ui-test-docker-context.xml"; then
    awk -v line='                <include>testing.properties</include>' '/<include>wait-for-grid.sh<\/include>/ { printf "%s\n%s\n", $0, line; next }; 1' assembly-ui-test-docker-context.xml > assembly-ui-test-docker-context.xml.new && mv assembly-ui-test-docker-context.xml.new assembly-ui-test-docker-context.xml
  fi
  ```

* Adobe提供的Cypress和Java Selenium測試範例已設定選擇加入旗標。

## 編寫UI測試 {#writing-ui-tests}

本節介紹包含 UI 測試的 Docker 映像必須遵循的約定。Docker 映像是根據上一節中描述的 Docker 建置內容建構的。

### 環境變數 {#environment-variables}

以下環境變數會在執行階段傳遞給您的 Docker 映像，視您的架構而定。

>[!NOTE]
>
> 這些值在管道執行期間自動設定；不需要手動設定為管道變數。

| 變數 | 範例 | 說明 | 測試架構 |
|----------------------------|----------------------------------|----------------------------------------------------------------------------------------------------|---------------------|
| `SELENIUM_BASE_URL` | `http://my-ip:4444` | Selenium伺服器的URL | 僅限 Selenium |
| `SELENIUM_BROWSER` | `chrome` | Selenium伺服器使用的瀏覽器實作 | 僅限 Selenium |
| `AEM_AUTHOR_URL` | `http://my-ip:4502/context-path` | AEM作者執行個體的URL | 全部 |
| `AEM_AUTHOR_USERNAME` | `admin` | 用來登入AEM作者例項的使用者名稱 | 全部 |
| `AEM_AUTHOR_PASSWORD` | `admin` | 登入AEM作者執行個體的密碼 | 全部 |
| `AEM_PUBLISH_URL` | `http://my-ip:4503/context-path` | AEM發佈執行個體的URL | 全部* |
| `AEM_PUBLISH_USERNAME` | `admin` | 登入AEM發佈執行個體的使用者名稱 | 全部* |
| `AEM_PUBLISH_PASSWORD` | `admin` | 登入AEM發佈執行個體的密碼 | 全部* |
| `REPORTS_PATH` | `/usr/src/app/reports` | 測試結果XML報告必須儲存的路徑 | 全部 |
| `UPLOAD_URL` | `http://upload-host:9090/upload` | 必須上傳檔案才能讓測試框架存取的URL | 全部 |
| `PROXY_HOST` | `proxy-host` | 測試框架要使用的內部HTTP Proxy的主機名稱 | 除Selenium外的所有專案 |
| `PROXY_HTTPS_PORT` | `8071` | HTTPS連線的Proxy伺服器接聽連線埠（可為空白） | 除Selenium外的所有專案 |
| `PROXY_HTTP_PORT` | `8070` | HTTP連線的Proxy伺服器接聽連線埠（可為空白） | 除Selenium外的所有專案 |
| `PROXY_CA_PATH` | `/path/to/root_ca.pem` | 測試架構所使用CA憑證的路徑 | 除Selenium外的所有專案 |
| `PROXY_OBSERVABILITY_PORT` | `8081` | Proxy伺服器的HTTP `healthcheck`連線埠 | 除Selenium外的所有專案 |
| `PROXY_RETRY_ATTEMPTS` | `12` | 等待Proxy伺服器準備就緒時的建議重試次數 | 除Selenium外的所有專案 |
| `PROXY_RETRY_DELAY` | `5` | 等待Proxy伺服器整備時重試嘗試之間的建議延遲 | 除Selenium外的所有專案 |

`* these values will be empty if there is no publish instance`

Adobe 測試範例提供輔助函數以存取設定參數：

Cypress: 使用標準函數 `Cypress.env('VARIABLE_NAME')`
<!-- BOTH URLs are 404 JavaScript: See the [`lib/config.js`](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests.wdio/test-module/lib/config.js) module
* Java: See the [`Config`](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/Config.java) class -->

### 產生測試報告 {#generate-test-reports}

Docker 映像必須產生 JUnit XML 格式的測試報告，並保存在環境變數 `REPORTS_PATH` 指定的路徑中。JUnit XML 格式是廣泛使用的測試結果報告格式。如果 Docker 映像使用 Java 和 Maven，標準測試模組如 [Maven Surefire 插件](https://maven.apache.org/surefire/maven-surefire-plugin/)和 [Maven 故障安全插件](https://maven.apache.org/surefire/maven-failsafe-plugin/)可以開箱即用地產生此類報告。

如果 Docker 映像是使用其他編程語言或測試執行計畫實現的，請查看所選工具的文件以了解如何產生 JUnit XML 報告。

>[!NOTE]
>
>UI 測試步驟的結果僅根據測試報告進行評估。確保為您的測試執行產生相應的報告。
>
>使用斷言而不是僅將錯誤記錄到 STDERR 或返回非零退出程式碼，否則您的部署管道可能會正常進行。
>
>如果在測試執行期間使用了HTTP Proxy，則結果包含`request.log`檔案。

### 必備條件 {#prerequisites}

* Cloud Manager 中的測試是透過技術管理員使用者來執行。

>[!NOTE]
>
>若要從本機電腦執行功能測試，請建立一個具備類似管理員權限的使用者來達到相同的行為。

* 用於功能測試的容器化基礎架構受以下界限限制：

| 類型 | 值 | 說明 |
|----------------------|-------|-----------------------------------------------------------------------|
| CPU | 2.0 | 每次測試執行的CPU保留時間量。 |
| 記憶體 | 1Gi | 配置給測試的記憶體數量。 值以GB為單位。 |
| 逾時 | 30m | 測試執行多久。 |
| 建議的持續時間 | 15m | Adobe建議在此時間限制內進行測試。 |

* 如果目標作者/發佈受到IP允許清單的保護，則管道UI測試基礎結構必須列入允許清單，否則UI測試可能會失敗並出現403禁止名單。
另請參閱[由於IP允許清單](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26654#)和[IP允許清單簡介](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)，AEMaaCS中的UI測試失敗。

>[!NOTE]
>
> 若您需要更多資源，請建立客戶服務案例並描述您的使用案例；Adobe會稽核您的請求並提供適當的協助。

## Selenium 特定的詳細資訊

>[!NOTE]
>
>本節僅在選擇 Selenium 作為測試基礎結構時適用。

### 等待Selenium準備就緒 {#waiting-for-selenium}

在測試開始之前，Docker 映像負責確保 Selenium 伺服器啟動並執行。等待 Selenium 服務有兩個步驟。

1. 從 `SELENIUM_BASE_URL` 環境變數中讀取 Selenium 服務的 URL。
1. 定期輪詢Selenium API公開的[狀態端點](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready)。

一旦 Selenium 的狀態端點得到肯定的響應，測試就可以開始了。

Adobe的UI測試範例使用`wait-for-grid.sh`。 它在Docker啟動時執行，並在網格準備就緒後啟動測試。


### 擷取螢幕擷圖和影片 {#capture-screenshots}

Docker 映像檔可能會產生額外的測試輸出 (例如螢幕擷圖或影片)，並保存在環境變數 `REPORTS_PATH` 指定的路徑中。在 `REPORTS_PATH` 下找到的任何檔案都包含在測試結果封存檔中。

Adobe 提供的測試範例依預設為任何失敗的測試建立螢幕擷圖。

您可以使用輔助函數通過測試建立螢幕擷圖。

<!-- BOTH URLS ARE 404
* JavaScript: [takeScreenshot command](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/test-module/lib/commons.js)
* Java: [Commands](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/Commands.java) -->

如果在UI測試執行期間建立測試結果封存檔，您可以按一下`Download Details`自訂UI測試&#x200B;[**步驟**&#x200B;下的](/help/implementing/cloud-manager/deploy-code.md)按鈕，從Cloud Manager下載它。

### 上傳檔案 {#upload-files}

測試有時必須將文件上傳到被測試的應用程式。為了使Selenium的部署相對於您的測試保持靈活，不能直接將資產上傳到Selenium。 相反，上傳文件需要以下步驟。

1. 在指定的 URL 上傳檔案 `UPLOAD_URL` 環境變數。
   * 上傳必須在一個帶有多部分表單的 POST 要求中執行。
   * 多部分表單必須有一個檔案欄位。
   * 相當於`curl -X POST ${UPLOAD_URL} -F "data=@file.txt"`。
   * 請查閱 Docker 映像中使用的編程語言的檔案和資料庫，以了解如何執行此類 HTTP 要求。

   <!-- BOTH URLS ARE 404
   * The Adobe test samples provide helper functions for uploading files:
     * JavaScript: See the [getFileHandleForUpload](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/test-module/lib/wdio.commands.js) command.
     * Java: See the [FileHandler](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/FileHandler.java) class. -->

1. 如果上傳成功，請求傳回一個`200 OK`類型響應 `text/plain`。
   * 回應的內容是一個不透明的檔案。
   * 您可以使用此句柄代替文件路徑`<input>`在您的應用程序中測試文件上傳的元素。

## Cypress專屬詳細資料

>[!NOTE]
>
>此節僅適用於Cypress為選取的測試基礎結構。

### 設定HTTP Proxy

Docker容器的入口點需要檢查`PROXY_HOST`環境變數的值。

如果此值為空，則不需要進行其他步驟，且測試應在不使用HTTP Proxy的情況下執行。

如果不是空白，entrypoint指令碼需要：

1. 匯出使用下列值建立的`HTTP_PROXY`環境變數，以設定HTTP Proxy連線來執行UI測試：
   * 由`PROXY_HOST`變數提供的Proxy主機
   * 由`PROXY_HTTPS_PORT`或`PROXY_HTTP_PORT`變數提供的Proxy連線埠（使用具有非空白值的變數）
2. 設定連線至HTTP Proxy時使用的CA憑證。 其位置由`PROXY_CA_PATH`變數提供。
   * 匯出`NODE_EXTRA_CA_CERTS`環境變數。
3. 等候HTTP Proxy準備就緒。
   * 若要檢查整備程度，可以使用環境變數`PROXY_HOST`、`PROXY_OBSERVABILITY_PORT`、`PROXY_RETRY_ATTEMPTS`和`PROXY_RETRY_DELAY`。
   * 您可以使用cURL要求檢查，確定在您的`Dockerfile`中安裝cURL。

您可以在[GitHub](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-cypress/test-module/run.sh)上的Cypress範例測試模組的Entrypoint中找到實作範例。

## 播放權特定的詳細資料

>[!NOTE]
>
> 此區段僅適用於`Playwright`為選擇的測試基礎結構時。

### 設定HTTP Proxy

>[!NOTE]
>
> 在顯示的範例中，Adobe假設使用Chrome作為專案瀏覽器。

與Cypress類似，如果提供了非空白的`PROXY_HOST`環境變數，則測試需要使用HTTP Proxy。

在這種情況下，需要進行以下編輯。

#### Dockerfile

安裝cURL和`libnss3-tools`，提供`certutil.`

```dockerfile
RUN apt -y update \
    && apt -y --no-install-recommends install curl libnss3-tools \
    && rm -rf /var/lib/apt/lists/*
```

#### Entrypoint指令碼

納入bash指令碼，在已提供`PROXY_HOST`環境變數的情況下，其會執行下列動作：

1. 匯出Proxy相關的變數，例如`HTTP_PROXY`和`NODE_EXTRA_CA_CERTS`
2. 使用`certutil`安裝Chromium™的Proxy CA憑證。
3. 等候HTTP Proxy準備就緒（或失敗時結束）。

實作範例：

```bash
# setup proxy environment variables and CA certificate
if [ -n "${PROXY_HOST:-}" ]; then
  if [ -n "${PROXY_HTTPS_PORT:-}" ]; then
    export HTTP_PROXY="https://${PROXY_HOST}:${PROXY_HTTPS_PORT}"
  elif [ -n "${PROXY_HTTP_PORT:-}" ]; then
    export HTTP_PROXY="http://${PROXY_HOST}:${PROXY_HTTP_PORT}"
  fi
  if [ -n "${PROXY_CA_PATH:-}" ]; then
    echo "installing certificate"
    mkdir -p $HOME/.pki/nssdb
    certutil -d sql:$HOME/.pki/nssdb -A -t "CT,c,c" -n "EaaS Client Proxy Root" -i $PROXY_CA_PATH
    export NODE_EXTRA_CA_CERTS=${PROXY_CA_PATH}
  fi
  if [ -n "${PROXY_OBSERVABILITY_PORT:-}" ] && [ -n "${HTTP_PROXY:-}" ]; then
    echo "waiting for proxy"
    curl --silent  --retry ${PROXY_RETRY_ATTEMPTS:-3} --retry-connrefused --retry-delay ${PROXY_RETRY_DELAY:-10} \
      --proxy ${HTTP_PROXY} --proxy-cacert ${PROXY_CA_PATH:-""} \
      ${PROXY_HOST}:${PROXY_OBSERVABILITY_PORT}
    if [ $? -ne 0 ]; then
      echo "proxy is not ready"
      exit 1
    fi
  fi
fi
```

#### 播放器設定

修改播放權設定（例如`playwright.config.js`中的）以使用Proxy，以防已設定`HTTP_PROXY`環境變數。

實作範例：

```javascript
const proxyServer = process.env.HTTP_PROXY || ''
```

```javascript
// enable proxy if set
if (proxyServer !== '') {
 cfg.use.proxy = {
  server: proxyServer,
 }
}
```

>[!NOTE]
>
> 您可以在[GitHub](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-playwright)上的Playwright範例測試模組中找到實作範例。


## 在本機執行UI測試 {#run-ui-tests-locally}

在Cloud Manager管道中啟用UI測試之前，Adobe建議您對[AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)在本機執行UI測試。 或者，針對實際的AEM as a Cloud Service執行個體執行。

### Cypress測試範例 {#cypress-sample}

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
>如需詳細資訊，請參閱[AEM測試範例存放庫](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-cypress/test-module/README.md)。

### JavaScript WebdriverIO測試範例 {#javascript-sample}

1. 打開 shell 並瀏覽至存放庫中的 `ui.tests` 資料夾。

1. 執行以下命令以使用Maven啟動測試。

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
>* 此命令會啟動獨立的Selenium執行個體並對其執行測試。
>* 記錄檔案會儲存在您的存放庫的 `target/reports` 資料夾中
>* 請務必確定您的電腦執行最新版本的 Chrome，因為測試會自動下載最新版的 ChromeDriver 以進行測試。
>
>如需詳細資訊，請參閱[AEM測試範例存放庫](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-wdio)。

### Playwright測試範例 {#playwright-sample}

1. 打開 shell 並瀏覽至存放庫中的 `ui.tests` 資料夾

1. 執行以下命令以使用Maven構建Docker映像

   ```shell
   mvn clean package -Pui-tests-docker-build
   ```

1. 執行以下命令以使用 Maven 啟動測試

   ```shell
   mvn verify -Pui-tests-docker-execution \
    -DAEM_AUTHOR_URL=https://author-<program-id>-<environment-id>.adobeaemcloud.com \
    -DAEM_AUTHOR_USERNAME=<user> \
    -DAEM_AUTHOR_PASSWORD=<password> \
    -DAEM_PUBLISH_URL=https://publish-<program-id>-<environment-id>.adobeaemcloud.com \
    -DAEM_PUBLISH_USERNAME=<user> \
    -DAEM_PUBLISH_PASSWORD=<password>
   ```

>[!NOTE]
>
>記錄檔案會儲存在您的存放庫的 `target/` 資料夾中。
>
>如需詳細資訊，請參閱[AEM測試範例存放庫](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-playwright)。


### Java Selenium WebDriver測試範例 {#java-sample}

1. 打開 shell 並瀏覽至存放庫中的 `ui.tests/test-module` 資料夾

1. 執行以下命令以使用 Maven 啟動測試

   ```shell
   # Start selenium docker image
   # we mount /tmp/shared as a shared volume that will be used between selenium and the test module for uploads
   docker run -d -p 4444:4444 -v /tmp/shared:/tmp/shared selenium/standalone-chromium:latest
   
   # Run the tests using the previously started Selenium instance
   mvn verify -Pui-tests-local-execution -DSELENIUM_BASE_URL=http://<server>:4444
   ```

>[!NOTE]
>
>記錄檔案會儲存在您的存放庫的 `target/reports` 資料夾中.
>
>如需詳細資訊，請參閱[AEM測試範例存放庫](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/README.md)。
