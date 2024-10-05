---
title: 組建環境
description: 了解 Cloud Manager 的構建環境以及它如何構建和測試您的程式碼。
exl-id: a4e19c59-ef2c-4683-a1be-3ec6c0d2f435
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 500e1b78fb9688601848fc17f312fc23be83bcb0
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 77%

---


# 組建環境 {#build-environment}

了解 Cloud Manager 的構建環境以及它如何構建和測試您的程式碼。

## 檢視環境詳細資訊 {#build-environment-details}

Cloud Manager 使用專門的構建環境構建和測試您的程式碼。

* 建置環境以 Linux 為基礎，衍生自 Ubuntu 22.04。
* 已安裝 Apache Maven 3.9.4。
   * Adobe 建議使用者[更新其 Maven 存放庫以使用 HTTPS 而非 HTTP](#https-maven)。
* 安裝的Java版本為OracleJDK 11.0.22和OracleJDK 8u401。
* **重要**：依預設，`JAVA_HOME`環境變數設為`/usr/lib/jvm/jdk1.8.0_401`，其中包含OracleJDK 8u401。 *_AEM雲端專案應覆寫此預設以使用JDK 11_*。 如需詳細資訊，請參閱[設定Maven JDK版本](#alternate-maven-jdk-version)區段。
* 安裝了一些必要的附加系統套件。
   * `bzip2`
   * `unzip`
   * `libpng`
   * `imagemagick`
   * `graphicsmagick`
* 在建置時間可安裝其他套件，如[安裝附加系統套件](#installing-additional-system-packages)部份中所述。
* 每次構建都是在原始環境中完成的；構建容器在執行之間不保持任何狀態。
* 一直使用下列三個命令執行 Maven：
   * `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
   * `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
   * `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent package`
* 透過 `settings.xml` 檔案在系統層級設定 Maven，這會利用名為 `adobe-public` 的設定檔自動納入公共 Adobe 成品存放庫。如需更多詳細資訊，請參閱 [Adobe 公共 Maven 存放庫](https://repo1.maven.org/)。

>[!NOTE]
>
>雖然 Cloud Manager 並未定義 `jacoco-maven-plugin` 的特定版本，但使用的版本必須至少為 `0.7.5.201505241946`。

## HTTPS Maven 存放庫 {#https-maven}

Cloud Manager [2023.10.0 版](/help/implementing/cloud-manager/release-notes/2023/2023-10-0.md)開始推出組建環境的更新 (在 2023.12.0 版時完成)，其中包含 Maven 3.8.8 的更新。Maven 3.8.1 引入一項重大變更，即為安全性增強，其目的在減少潛在漏洞。具體而言，Maven 現在預設停用所有不安全的 `http://*` 鏡像，如 [Maven 發行說明](http://maven.apache.org/docs/3.8.1/release-notes.html#cve-2021-26291)中所述。

由於此安全性增強，某些使用者可能會在建置步驟中遇到問題，特別是從使用不安全 HTTP 連線的 Maven 存放庫下載成品時。

為了確保更新的版本有流暢的使用體驗，Adobe 建議使用者更新其 Maven 存放庫以使用 HTTPS 而非 HTTP。這項調整符合產業日益轉向使用安全通訊協定的趨勢，有助於維持安全可靠的建置程序。

### 使用特定 Java 版本 {#using-java-support}

根據預設，專案是由Cloud Manager建置流程使用Oracle8 JDK建置，但強烈建議AEM Cloud Service客戶將用於執行Maven的JDK版本設定為`11`。

#### 設定Maven JDK版本 {#alternate-maven-jdk-version}

建議在`.cloudmanager/java-version`檔案中將整個Maven執行的JDK版本設為`11`。

為此，可在管道使用的 Git 存放庫分支中建立名為 `.cloudmanager/java-version` 的檔案。編輯檔案，使其僅包含文字`11`。 雖然Cloud Manager也接受`8`的值，但AEM Cloud Service專案不再支援此版本。 任何其他值會受到忽略。指定`11`時，會使用Oracle11，且`JAVA_HOME`環境變數設為`/usr/lib/jvm/jdk-11.0.22`。

## 環境變數 {#environment-variables}

### 標準環境變數 {#standard-environ-variables}

您可能會發現有必要根據有關計畫或管道的資訊來改變建置流程。

例如，如果透過 gulp 之類的工具完成建置時間 JavaScript 縮製，則在為開發環境建置而不是為中繼和生產環境建置時，可能希望使用不同的縮製等級。

為了支援這一點，Clo&#x200B;&#x200B;ud Manager 會在每次執行時將標準環境變數新增到組建容器中。

| 變數名稱 | 定義 |
|---|---|
| `CM_BUILD` | 需永遠設為 `true` |
| `BRANCH` | 為執行設定的分支 |
| `CM_PIPELINE_ID` | 數值的管道識別碼 |
| `CM_PIPELINE_NAME` | 管道名稱 |
| `CM_PROGRAM_ID` | 數值的方案識別碼 |
| `CM_PROGRAM_NAME` | 計畫名稱 |
| `ARTIFACTS_VERSION` | 對於中繼或生產管道，由 Cloud Manager 產生的綜合版本 |
| `CM_AEM_PRODUCT_VERSION` | 發行版本 |

### 管道變數 {#pipeline-variables}

在某些情況下，您的建置流程可能會依據特定的設定變數而定，這些變數不適合放入 Git 存放庫中，或者在使用同一分支的管道執行之間需要有所變化。

另請參閱[設定管道變數](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md)以取得詳細資訊

## 安裝附加系統套件 {#installing-additional-system-packages}

為了充分發揮作用，部分組建需要安裝附加系統套件。例如，組建可能會叫用Python或Ruby指令碼，而且必須安裝適當的語言解譯器。 這可透過呼叫 [`exec-maven-plugin`](https://www.mojohaus.org/exec-maven-plugin/) `pom.xml`以叫用 APT 來完成。這項執行通常應包裝在 Cloud Manager 特定的 Maven 設定檔中。若要安裝 Python。

```xml
        <profile>
            <id>install-python</id>
            <activation>
                <property>
                        <name>env.CM_BUILD</name>
                </property>
            </activation>
            <build>
                <plugins>
                    <plugin>
                        <groupId>org.codehaus.mojo</groupId>
                        <artifactId>exec-maven-plugin</artifactId>
                        <version>1.6.0</version>
                        <executions>
                            <execution>
                                <id>apt-get-update</id>
                                <phase>validate</phase>
                                <goals>
                                    <goal>exec</goal>
                                </goals>
                                <configuration>
                                    <executable>apt-get</executable>
                                    <arguments>
                                        <argument>update</argument>
                                    </arguments>
                                </configuration>
                            </execution>
                            <execution>
                                <id>install-python</id>
                                <phase>validate</phase>
                                <goals>
                                    <goal>exec</goal>
                                </goals>
                                <configuration>
                                    <executable>apt-get</executable>
                                    <arguments>
                                        <argument>install</argument>
                                        <argument>-y</argument>
                                        <argument>--no-install-recommends</argument>
                                        <argument>python</argument>
                                    </arguments>
                                </configuration>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
```

此同一技術可用於安裝特定語言的套件，例如將 `gem` 用於 RubyGems 或將 `pip` 用於 Python 套件。

>[!NOTE]
>
>以這種方式安裝系統套件不會將其安裝在用於執行 Adobe&#x200B; Experience Manager 的執行階段環境中。如果您需要在 AEM 環境中安裝系統套件，請和您的 Adob&#x200B;&#x200B;e 代表聯絡。

>[!TIP]
>
>如需有關前端建置環境的詳細資料，請參閱[使用前端管道開發網站](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md)。
