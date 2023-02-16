---
title: UI 測試
description: 自訂 UI 測試是一項選擇性功能，可讓您為自訂應用程式建立和自動執行 UI 測試。
exl-id: 3009f8cc-da12-4e55-9bce-b564621966dd
source-git-commit: b1eacc8432a73f015529975e6960afbe9dee7565
workflow-type: tm+mt
source-wordcount: '2143'
ht-degree: 56%

---


# UI 測試 {#ui-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_uitesting"
>title="UI 測試"
>abstract="自訂 UI 測試是一項選擇性功能，可讓您為應用程式建立和自動執行 UI 測試。UI 測試是封裝在 Docker 影像中的 Selenium 型測試，以便在語言和架構 (例如 Java 和 Maven、Node 和 WebDriver.io 或任何其他根據 Selenium 建置的架構和技術) 中提供廣泛的選擇。"

自訂 UI 測試是一項選擇性功能，可讓您為應用程式建立和自動執行 UI 測試。

## 概觀 {#custom-ui-testing}

AEM 提供了[Cloud Manager 品質關卡](/help/implementing/cloud-manager/custom-code-quality-rules.md)整合套件，以確保自訂應用程序順利更新。尤其是，IT測試閘道已支援使用AEM API建立和自動化自訂測試。

UI 測試是封裝在 Docker 影像中的 Selenium 型測試，以便在語言和架構 (例如 Java 和 Maven、Node 和 WebDriver.io 或任何其他根據 Selenium 建置的架構和技術) 中提供廣泛的選擇。此外，使用 [AEM專案原型。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hant)

UI 測試作為每個 Cloud Manager 管道的特定品質門的一部分執行，具有[投入的&#x200B;**自訂 UI 測試**&#x200B;步。](/help/implementing/cloud-manager/deploy-code.md)包括回歸和新功能在內的任何 UI 測試都可以檢測和報告錯誤。

與使用 Java 編寫的 HTTP 測試的自訂功能測試不同，UI 測試可以是 Docker 映像，其中包含以任何語言編寫的測試，只要它們遵循本節中定義的約定[構建 UI 測試。](#building-ui-tests)

>[!TIP]
>
>Adobe 建議遵循本文件中提供的結構和語言（JavaScript 和 WDIO）[ AEM Project 原型。](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)
>
>Adobe還提供了基於Java和WebDriver的UI測試模組示例。 請參閱 [AEM測試範例存放庫](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-selenium-webdriver) 以取得詳細資訊。

## 開始使用UI測試 {#get-started-ui-tests}

本節說明在Cloud Manager中設定執行UI測試所需執行的步驟。

1. 決定您要使用的程式設計語言。

   * 若是JavaScript和WDIO，請使用中自動產生的范常式式碼 `ui.tests` Cloud Manager儲存庫的資料夾。

      >[!NOTE]
      >
      >如果您的存放庫是在Cloud Manager自動建立之前建立 `it.tests` 資料夾，您也可以使用 [AEM專案原型。](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/it.tests)

   * 對於Java和WebDriver，請使用 [AEM測試範例存放庫。](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-selenium-webdriver)

   * 有關其他程式設計語言，請參閱 [建立UI測試](#building-ui-tests) 來設定測試專案。

1. 確認已依照區段啟動UI測試 [客戶選擇加入](#customer-opt-in) 在此文檔中。

1. 開發您的測試案例，並 [在本機執行測試。](#run-ui-tests-locally)

1. 將您的程式碼提交至Cloud Manager存放庫並執行Cloud Manager管道。

## 構建 UI 測試 {#building-ui-tests}

一個 Maven 項目會生成一個 Docker 構建上下文。此Docker建置內容說明如何建立包含UI測試的Docker影像，Cloud Manager會使用這些測試來產生包含實際UI測試的Docker影像。

本節介紹將 UI 測試項目新增到存放庫所需的步驟。

>[!TIP]
>
>此 [AEM專案原型](https://github.com/adobe/aem-project-archetype) 如果您對程式設計語言沒有特殊要求，可為您產生符合下列說明的UI測試專案。

### 生成 Docker 構建上下文 {#generate-docker-build-context}

為了生成 Docker 構建上下文，您需要一個 Maven 模組：

* 生成一個包含`Dockerfile`以及使用您的測試構建 Docker 映像所需的所有其他文件。
* 用`ui-test-docker-context`分類器。

最簡單的方法是配置[Maven 組裝插件](https://maven.apache.org/plugins/maven-assembly-plugin/)建立 Docker 構建上下文封存並為其指派正確的分類器。

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
* 由 Node.js 項目實現的實際 UI 測試`test-module`檔案夾

程序集描述符還排除了在本機執行 UI 測試時可能生成的一些文件。這保證了更小的封存和更快的建構。

包含 Docker 建構上下文的封存由 Cloud Manager 自動獲取，它將在其部署管道期間構建包含您的測試的 Docker 影像。最終，Cloud Manager 將執行 Docker 映像以針對您的應用程序執行 UI 測試。

建構應生成零個或一個封存。如果產生零個封存，則測試步驟預設透過。如果建置產生多個封存，則無法確定要選擇哪個封存。

### 客戶選擇加入 {#customer-opt-in}

若要讓Cloud Manager建立並執行您的UI測試，您必須借由將檔案新增至存放庫來選擇加入此功能。

* 檔案名稱必須是 `testing.properties`。
* 檔案內容必須是 `ui-tests.version=1`。
* 檔案必須位於maven子模組下，才能進行UI測試，緊鄰 `pom.xml` 檔案。
* 該文件必須位於構建的根目錄`tar.gz`文件。

如果此文件不存在，將跳過 UI 測試構建和執行。

包括一個`testing.properties`在構建工件中的文件，新增一個`include`中的聲明`assembly-ui-test-docker-context.xml`文件。

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
>如果您的項目不包含此行，則需要編輯文件以選擇進行 UI 測試。
>
>該文件可能包含一條建議不要編輯它的行。這是因為它是在引入選擇加入 UI 測試之前被引入您的項目的，並且客戶端不打算編輯該文件。這可以安全地忽略。

如果您使用Adobe提供的範例：

* 針對以JavaScript為基礎 `ui.tests` 根據 [AEM專案原型](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)，您可以執行以下命令以新增所需的設定。

   ```shell
   echo "ui-tests.version=1" > testing.properties
   
   if ! grep -q "testing.properties" "assembly-ui-test-docker-context.xml"; then
     awk -v line='                <include>testing.properties</include>' '/<include>wait-for-grid.sh<\/include>/ { printf "%s\n%s\n", $0, line; next }; 1' assembly-ui-test-docker-context.xml > assembly-ui-test-docker-context.xml.new && mv assembly-ui-test-docker-context.xml.new assembly-ui-test-docker-context.xml
   fi
   ```

* 提供的Java測試範例已設定選擇加入標幟。

## 編寫 UI 測試 {#writing-ui-tests}

本節介紹包含 UI 測試的 Docker 映像必須遵循的約定。Docker 映像是根據上一節中描述的 Docker 建構上下文建構的。

### 環境變數 {#environment-variables}

以下環境變量將在執行時傳遞給您的 Docker 映像。

| 變數 | 範例 | 說明 |
|---|---|---|
| `SELENIUM_BASE_URL` | `http://my-ip:4444` | Selenium 伺服器的 URL |
| `SELENIUM_BROWSER` | `chrome` | Selenium 伺服器使用的瀏覽器實作 |
| `AEM_AUTHOR_URL` | `http://my-ip:4502/context-path` | AEM 作者執行個體的 URL |
| `AEM_AUTHOR_USERNAME` | `admin` | 要登入AEM製作例項的使用者名稱 |
| `AEM_AUTHOR_PASSWORD` | `admin` | 登入AEM製作例項的密碼 |
| `AEM_PUBLISH_URL` | `http://my-ip:4503/context-path` | AEM 發佈執行個體的 URL |
| `AEM_PUBLISH_USERNAME` | `admin` | 要登入AEM發佈例項的使用者名稱 |
| `AEM_PUBLISH_PASSWORD` | `admin` | 登入AEM發佈執行個體的密碼 |
| `REPORTS_PATH` | `/usr/src/app/reports` | 測試結果 XML 報告必須儲存的路徑 |
| `UPLOAD_URL` | `http://upload-host:9090/upload` | 必須將文件上傳到的 URL 使 Selenium 可以存取 |

Adobe測試範例提供存取設定參數的輔助功能：

* JavaScript:請參閱 [lib/config.js](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/test-module/lib/config.js) 模組
* Java:請參閱 [設定](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/Config.java) 類

### 等待 Selenium 準備就緒 {#waiting-for-selenium}

在測試開始之前，Docker 影像負責確保 Selenium 伺服器啟動並執行。等待 Selenium 服務有兩個步驟。

1. 從 `SELENIUM_BASE_URL` 環境變數中讀取 Selenium 服務的 URL。
1. 定期輪詢 Selenium API 公開的[狀態端點](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready)。

一旦 Selenium 的狀態端點得到肯定的響應，測試就可以開始了。

AdobeUI測試範例會使用指令碼來處理此問題 `wait-for-grid.sh`,Docker啟動時會執行，且只有當格線準備就緒後，才會開始實際測試執行。

### 生成測試報告 {#generate-test-reports}

Docker 鏡像必須生成 JUnit XML 格式的測試報告，並保存在環境變數 `REPORTS_PATH` 指定的路徑中。JUnit XML 格式是一種廣泛使用的報告測試結果的格式。如果 Docker 鏡像使用 Java 和 Maven，標準測試模組如[Maven Surefire 插件](https://maven.apache.org/surefire/maven-surefire-plugin/)和[Maven 故障安全插件](https://maven.apache.org/surefire/maven-failsafe-plugin/)可以開箱即用地生成此類報告。

如果 Docker 映像是使用其他編程語言或測試執行計劃實現的，請查看所選工具的文件以了解如何生成 JUnit XML 報告。

>[!NOTE]
>
>UI測試步驟的結果僅會根據測試報表來評估。 請確定您為測試執行產生相應的報表。
>
>使用斷言，而非僅將錯誤記錄到STDERR或傳回非零退出代碼，否則您的部署管道可能會正常進行。

### 擷取螢幕擷圖和視訊 {#capture-screenshots}

Docker影像可產生其他測試輸出（例如螢幕擷取畫面或視訊），並儲存至環境變數所指定的路徑 `REPORTS_PATH`. 在 `REPORTS_PATH` 下找到的任何檔案都包含在測試結果封存檔中。

預設情況下，Adobe提供的測試示例為任何失敗的測試建立螢幕截圖。

您可以使用協助程式功能，透過測試建立螢幕擷取畫面。

* JavaScript: [take螢幕擷取命令](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/test-module/lib/commons.js)
* Java: [命令](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/Commands.java)

如果在UI測試執行期間建立了測試結果存檔，則測試日誌檔案包含對測試結果存檔在結尾的位置的引用。

```
[...]

===============================================================
The detailed test results can be downloaded from the URL below.
Note: the link will expire after 60 days

    https://results-host/test-results.zip

===============================================================
```

### 上傳檔案 {#upload-files}

測試有時必須將文件上傳到被測試的應用程式。為了使 Selenium 的部署相對於您的測試保持靈活，不能直接將資產直接上傳到 Selenium。相反，上傳文件需要以下步驟。

1. 在指定的 URL 上傳檔案 `UPLOAD_URL` 環境變數。
   * 上傳必須在一個帶有多部分表單的 POST 要求中執行。
   * 多部分表單必須有一個檔案欄位。
   * 這相當於 `curl -X POST ${UPLOAD_URL} -F "data=@file.txt"`。
   * 請查閱 Docker 映像中使用的編程語言的檔案和資料庫，以了解如何執行此類 HTTP 要求。
   * Adobe測試範例提供上傳檔案的輔助功能：
      * JavaScript:請參閱 [getFileHandleForUpload](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/test-module/lib/wdio.commands.js) 命令。
      * Java:請參閱 [檔案處理程式](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/FileHandler.java) 類別。
1. 如果上傳成功，請求傳回一個`200 OK`類型響應 `text/plain`。
   * 回應的內容是一個不透明的檔案。
   * 您可以使用此句柄代替文件路徑`<input>`在您的應用程序中測試文件上傳的元素。

## 在本機執行UI測試 {#run-ui-tests-locally}

在Cloud Manager管道中啟用UI測試之前，建議先在本機上對 [AEMas a Cloud ServiceSDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) 或實際的AEMas a Cloud Service例項。

### 必備條件 {#prerequisites}

Cloud Manager中的測試將使用技術管理員使用者執行。

若要從本機電腦執行UI測試，請建立具有類似管理員權限的使用者，以達成相同的行為。

### JavaScript測試範例 {#javascript-sample}

1. 開啟殼層並導覽至 `ui.tests` 儲存庫中的資料夾

1. 執行以下命令以使用Maven啟動測試

   ```shell
   mvn verify -Pui-tests-local-execution \
   -DAEM_AUTHOR_URL=https://author-<program-id>-<environment-id>.adobeaemcloud.com \
   -DAEM_AUTHOR_USERNAME=<user> \
   -DAEM_AUTHOR_PASSWORD=<password> \
   -DAEM_PUBLISH_URL=https://publish-<program-id>-<environment-id>.adobeaemcloud.com \
   -DAEM_PUBLISH_USERNAME=<user> \
   -DAEM_PUBLISH_PASSWORD=<password> \
   -DHEADLESS_BROWSER=true \
   -DSELENIUM_BROWSER=chrome
   ```

>[!NOTE]
>
>* 這會啟動獨立的selenium執行個體並針對其執行測試。
>* 記錄檔會儲存在 `target/reports` 儲存庫的資料夾
>* 測試會自動下載最新版的ChromeDriver以進行測試時，您必須確保使用最新的Chrome版本。
>
>如需詳細資訊，請參閱 [AEM專案原型存放庫。](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/README.md)

### Java測試範例 {#java-sample}

1. 開啟殼層並導覽至 `ui.tests/test-module` 儲存庫中的資料夾

1. 執行以下命令以使用Maven啟動測試

   ```shell
   # Start selenium docker image (for x64 CPUs)
   docker run --platform linux/amd64 -d -p 4444:4444 selenium/standalone-chrome-debug:latest
   
   # Start selenium docker image (for ARM CPUs)
   docker run -d -p 4444:4444 seleniarm/standalone-chromium
   
   # Run the tests using the previously started Selenium instance
   mvn verify -Pui-tests-local-execution -DSELENIUM_BASE_URL=http://<server>:<port>
   ```

>[!NOTE]
>
>* 記錄檔將儲存在 `target/reports` 儲存庫的資料夾。
>
>如需詳細資訊，請參閱 [AEM測試範例存放庫。](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-selenium-webdriver/README.MD)
