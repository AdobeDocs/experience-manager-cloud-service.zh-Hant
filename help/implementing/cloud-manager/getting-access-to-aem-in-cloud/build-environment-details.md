---
title: 建置環境
description: 了解Cloud Manager的建置環境，以及如何建置和測試您的程式碼。
exl-id: a4e19c59-ef2c-4683-a1be-3ec6c0d2f435
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 46%

---

# 建置環境 {#build-environment}

了解Cloud Manager的建置環境，以及如何建置和測試您的程式碼。

## 建置環境詳細資訊 {#build-environment-details}

Cloud Manager會使用專用的建置環境來建立和測試您的程式碼。

* 組建環境以 Linux 為基礎，衍生自 Ubuntu 18.04。
* 已安裝 Apache Maven 3.6.0。
* 已安裝的 Java 版本為 Oracle JDK 8u202 和 Oracle JDK 11.0.2。
* 預設的情況下，`JAVA_HOME` 環境變數設為 `/usr/lib/jvm/jdk1.8.0_202`，其中包含 Oracle JDK 8u202。請參閱 [備用Maven執行JDK版本](#alternate-maven-jdk-version) 一節以取得詳細資訊。
* 安裝了一些必要的附加系統套件。

   * `bzip2`
   * `unzip`
   * `libpng`
   * `imagemagick`
   * `graphicsmagick`

* 在建置時間可安裝其他套件，如[安裝附加系統套件](#installing-additional-system-packages)區段中所述。
* 每棟建築都是在原始環境下建造的；建置容器不會在執行之間保留任何狀態。
* Maven一律使用下列三個命令執行。

* `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
* `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
* `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent package`
* Maven是在系統層級使用 `settings.xml` 檔案，該檔案使用名為的配置檔案自動包括公共Adobe對象儲存庫 `adobe-public`. (請參閱 [Adobe公用Maven存放庫](https://repo1.maven.org/) 如需詳細資訊)。

>[!NOTE]
>
>雖然 Cloud Manager 並未定義 `jacoco-maven-plugin` 的特定版本，但使用的版本必須至少為 `0.7.5.201505241946`。

### 使用特定 Java 版本 {#using-java-support}

預設情況下，專案會由 Cloud Manager 建置流程使用 Oracle 8 JDK 來建置。希望使用備用 JDK 的客戶有兩種選擇。

* [使用Maven工具鏈。](#maven-toolchains)
* [為整個Maven執行過程選擇替代的JDK版本。](#alternate-maven-jdk-version)

#### Maven 工具鏈 {#maven-toolchains}

此 [Maven工具鏈插件](https://maven.apache.org/plugins/maven-toolchains-plugin/) 允許項目選擇要在工具鏈感知的Maven插件的上下文中使用的特定JDK（或工具鏈）。 這可透過指定廠商和版本值，在專案的 `pom.xml` 檔案中完成。

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-toolchains-plugin</artifactId>
    <version>1.1</version>
    <executions>
        <execution>
            <goals>
                <goal>toolchain</goal>
            </goals>
        </execution>
    </executions>
    <configuration>
        <toolchains>
            <jdk>
                <version>11</version>
                <vendor>oracle</vendor>
            </jdk>
        </toolchains>
    </configuration>
</plugin>
```

這將導致所有工具鏈感知的 Maven 外掛程式使用 Oracle JDK 版本 11。

使用此方法時，Maven 本身仍使用預設的 JDK (Oracle 8) 執行，並且 `JAVA_HOME` 環境變數未受到變更。因此，透過 Apache Maven 強制器外掛程式之類的外掛程式來檢查或強制執行 Java 版本並不可行，且不得使用這類外掛程式。

目前可提供的廠商/版本組合為：

| 廠商 | 版本 |
|---|---|
| `oracle` | `8` |
| `oracle` | `11` |
| `sun` | `8` |
| `sun` | `11` |

此表格指的是產品版本號。 Java組建編號或安裝路徑可能會反映舊的Java版本慣例，例如Java 8適用的1.8。

>[!NOTE]
>
>從 2022 年 4 月開始，Oracle JDK 將成為 AEM 應用程式開發和操作的預設 JDK。即使在Maven工具鏈中明確選取了替代選項，Cloud Manager的建置程式仍會自動切換為使用OracleJDK。 如需詳細資訊，請參閱4月的發行說明。

#### 備用 Maven 執行 JDK 版本 {#alternate-maven-jdk-version}

您也可以選取Java 8或Java 11作為JDK，以執行整個Maven執行。 和工具鏈選項不同，這會變更用於所有外掛程式的 JDK，除非還設定了工具鏈設定，若是這種情況，則工具鏈設定仍適用於工具鏈感知的 Maven 外掛程式。結果，利用 [Apache Maven 強制器外掛程式](https://maven.apache.org/enforcer/maven-enforcer-plugin/)來檢查和強制執行 Java 版本將變得可行。

為此，可在管道使用的 Git 存放庫分支中建立名為 `.cloudmanager/java-version` 的檔案。此檔案可包含內容11或8。 任何其他值會受到忽略。若指定11，則使用Oracle11，且 `JAVA_HOME` 環境變數設為 `/usr/lib/jvm/jdk-11.0.2`. 若指定8，則使用Oracle8，且 `JAVA_HOME` 環境變數設為 `/usr/lib/jvm/jdk1.8.0_202`.

## 環境變數 {#environment-variables}

### 標準環境變數 {#standard-environ-variables}

您可能會發現，必鬚根據程式或管道的相關資訊來變更建置程式。

例如，如果是透過Gulp等工具進行建置時間JavaScript縮制，則在針對開發環境建置時，可能會想使用不同的縮制層級，而非針對測試和生產建置。

為了支援此功能，Cloud Manager會將這些標準環境變數新增至每次執行的組建容器。

| 變數名稱 | 定義 |
|---|---|
| `CM_BUILD` | 需永遠設為 `true` |
| `BRANCH` | 為執行設定的分支 |
| `CM_PIPELINE_ID` | 數值的管道識別碼 |
| `CM_PIPELINE_NAME` | 管道名稱 |
| `CM_PROGRAM_ID` | 數值的方案識別碼 |
| `CM_PROGRAM_NAME` | 方案名稱 |
| `ARTIFACTS_VERSION` | 對於階段或生產管道，由Cloud Manager產生的合成版本 |
| `CM_AEM_PRODUCT_VERSION` | 發行版本 |

### 管道變數 {#pipeline-variables}

您的建立程式可能取決於特定設定變數，這些變數不適合放置在Git存放庫中，或您可能需要使用相同分支，在不同管道執行之間加以變更。

Cloud Manager 讓這些變數能夠經由 Cloud Manager API 或 Cloud Manager CLI 依據每個管道來設定。變數可能以純文字或加密待用的方式儲存。在任何一種情況下，都可在組建環境中以環境變數的形式取得，然後可以從 `pom.xml` 檔案或其他建置指令碼中加以引用。

此CLI命令設定一個變數。

```shell
$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test
```

此命令列出變數。

```shell
$ aio cloudmanager:list-pipeline-variables PIPELINEID
```

變數名稱必須遵循下列慣例。

* 變數只能包含英數字元和底線(`_`)。
* 名字應全部大寫。
* 每個管道限制為 200 個變數。
* 每個名稱的長度都必須少於 100 個字元。
* 每個 `string` 變數值必須少於2048個字元。
* 每個 `secretString` 類型變數值必須小於500個字元。

在Maven內使用時 `pom.xml` 檔案中，使用類似此的語法將這些變數對應至Maven屬性通常會很有幫助。

```xml
        <profile>
            <id>cmBuild</id>
            <activation>
                <property>
                    <name>env.CM_BUILD</name>
                </property>
            </activation>
            <properties>
                <my.custom.property>${env.MY_CUSTOM_VARIABLE}</my.custom.property> 
            </properties>
        </profile>
```

## 安裝附加系統套件 {#installing-additional-system-packages}

某些組建需要安裝額外的系統套件，才能完全運作。 例如，生成可以調用Python或Ruby指令碼，並且需要安裝適當的語言解釋器。 您可以呼叫 [`exec-maven-plugin`](https://www.mojohaus.org/exec-maven-plugin/) 在 `pom.xml` 調用APT。 這項執行通常應包裝在 Cloud Manager 特定的 Maven 設定檔中。此示例安裝Python。

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

此相同技術可用於安裝語言特定套件，例如使用 `gem` (RubyGems或 `pip` 用於Python包。

>[!NOTE]
>
>以這種方式安裝系統套件不會將其安裝在用於執行 Adobe&#x200B; Experience Manager 的執行階段環境中。如果您需要在 AEM 環境中安裝系統套件，請和您的 Adob&#x200B;&#x200B;e 代表聯絡。
