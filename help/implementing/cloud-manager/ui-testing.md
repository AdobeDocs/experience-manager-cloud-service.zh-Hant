---
title: UI 測試
description: 自訂 UI 測試是一項選擇性功能，可讓您為自訂應用程式建立和自動執行 UI 測試。
exl-id: 3009f8cc-da12-4e55-9bce-b564621966dd
source-git-commit: 31e84b7383cd9774b0eaf8ee0f2fe39bcd77fa15
workflow-type: tm+mt
source-wordcount: '1407'
ht-degree: 100%

---


# UI 測試 {#ui-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_uitesting"
>title="UI 測試"
>abstract="自訂 UI 測試是一項選擇性功能，可讓您為應用程式建立和自動執行 UI 測試。UI 測試是封裝在 Docker 影像中的 Selenium 型測試，以便在語言和架構 (例如 Java 和 Maven、Node 和 WebDriver.io 或任何其他根據 Selenium 建置的架構和技術) 中提供廣泛的選擇。"

自訂 UI 測試是一項選擇性功能，可讓您為應用程式建立和自動執行 UI 測試。

## 概觀 {#custom-ui-testing}

AEM 提供了[Cloud Manager 品質關卡](/help/implementing/cloud-manager/custom-code-quality-rules.md)整合套件，以確保自訂應用程序順利更新。尤其是 IT 測試門已經使用 AEM API 建立和自動化自訂測試。

UI 測試是封裝在 Docker 影像中的 Selenium 型測試，以便在語言和架構 (例如 Java 和 Maven、Node 和 WebDriver.io 或任何其他根據 Selenium 建置的架構和技術) 中提供廣泛的選擇。此外，可以透過使用 [AEM 專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hant)輕鬆生成 UI 測試專案。

UI 測試作為每個 Cloud Manager 管道的特定品質門的一部分執行，具有[投入的&#x200B;**自訂 UI 測試**&#x200B;步。](/help/implementing/cloud-manager/deploy-code.md)包括回歸和新功能在內的任何 UI 測試都可以檢測和報告錯誤。

與使用 Java 編寫的 HTTP 測試的自訂功能測試不同，UI 測試可以是 Docker 映像，其中包含以任何語言編寫的測試，只要它們遵循本節中定義的約定[構建 UI 測試。](#building-ui-tests)

>[!TIP]
>
>Adobe 建議遵循本文件中提供的結構和語言（JavaScript 和 WDIO）[ AEM Project 原型。](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)

### 客戶選擇加入 {#customer-opt-in}

為了讓 Cloud Manager 構建和執行 UI 測試，您必須透過將文件新增到存放庫來選擇使用此功能。

* 檔案名稱必須是 `testing.properties`。
* 檔案內容必須是 `ui-tests.version=1`。
* 該文件必須位於 maven 子模組下，用於 UI 測試`pom.xml`UI 測試子模組的文件。
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

## 構建 UI 測試 {#building-ui-tests}

一個 Maven 項目會生成一個 Docker 構建上下文。此 Docker 構建上下文描述瞭如何建立包含 UI 測試的 Docker 映像，Cloud Manager 使用者可以透過該映像生成包含實際 UI 測試的 Docker 映像。

本節介紹將 UI 測試項目新增到存放庫所需的步驟。

>[!TIP]
>
>這[AEM Project 原型](https://github.com/adobe/aem-project-archetype)可以為您對編程語言沒有特殊要求的生成 UI 測試項目。

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

## 編寫 UI 測試 {#writing-ui-tests}

本節介紹包含 UI 測試的 Docker 映像必須遵循的約定。Docker 映像是根據上一節中描述的 Docker 建構上下文建構的。

### 環境變數 {#environment-variables}

以下環境變量將在執行時傳遞給您的 Docker 映像。

| 變數 | 範例 | 說明 |
|---|---|---|
| `SELENIUM_BASE_URL` | `http://my-ip:4444` | Selenium 伺服器的 URL |
| `SELENIUM_BROWSER` | `chrome` | Selenium 伺服器使用的瀏覽器實作 |
| `AEM_AUTHOR_URL` | `http://my-ip:4502/context-path` | AEM 作者執行個體的 URL |
| `AEM_AUTHOR_USERNAME` | `admin` | 用於登入 AEM 作者執行個體的使用者名稱 |
| `AEM_AUTHOR_PASSWORD` | `admin` | 用於登入 AEM 作者執行個體的密碼 |
| `AEM_PUBLISH_URL` | `http://my-ip:4503/context-path` | AEM 發佈執行個體的 URL |
| `AEM_PUBLISH_USERNAME` | `admin` | 用於登入 AEM 發佈執行個體的使用者名稱 |
| `AEM_PUBLISH_PASSWORD` | `admin` | 用於登入 AEM 發佈執行個體的密碼 |
| `REPORTS_PATH` | `/usr/src/app/reports` | 測試結果 XML 報告必須儲存的路徑 |
| `UPLOAD_URL` | `http://upload-host:9090/upload` | 必須將文件上傳到的 URL 使 Selenium 可以存取 |

### 等待 Selenium 準備就緒 {#waiting-for-selenium}

在測試開始之前，Docker 影像負責確保 Selenium 伺服器啟動並執行。等待 Selenium 服務有兩個步驟。

1. 從 `SELENIUM_BASE_URL` 環境變數中讀取 Selenium 服務的 URL。
1. 定期輪詢 Selenium API 公開的[狀態端點](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready)。

一旦 Selenium 的狀態端點得到肯定的響應，測試就可以開始了。

### 生成測試報告 {#generate-test-reports}

Docker 鏡像必須生成 JUnit XML 格式的測試報告，並保存在環境變數 `REPORTS_PATH` 指定的路徑中。JUnit XML 格式是一種廣泛使用的報告測試結果的格式。如果 Docker 鏡像使用 Java 和 Maven，標準測試模組如[Maven Surefire 插件](https://maven.apache.org/surefire/maven-surefire-plugin/)和[Maven 故障安全插件](https://maven.apache.org/surefire/maven-failsafe-plugin/)可以開箱即用地生成此類報告。

如果 Docker 映像是使用其他編程語言或測試執行計劃實現的，請查看所選工具的文件以了解如何生成 JUnit XML 報告。

### 擷取螢幕擷圖和視訊 {#capture-screenshots}

Docker 映像必須產生額外的測試輸出 (例如，螢幕擷圖、影片)，並保存在環境變數 `REPORTS_PATH` 指定的路徑中。在 `REPORTS_PATH` 下找到的任何檔案都包含在測試結果封存檔中。

如果在 UI 測試執行期間建立了測試結果封存檔，則測試記錄檔案末尾會包含對測試結果封存檔位置的參照。

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
1. 如果上傳成功，請求傳回一個`200 OK`類型響應 `text/plain`。
   * 回應的內容是一個不透明的檔案。
   * 您可以使用此句柄代替文件路徑`<input>`在您的應用程序中測試文件上傳的元素。
