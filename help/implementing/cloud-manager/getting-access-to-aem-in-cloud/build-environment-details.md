---
title: 建置環境
description: 了解Cloud Manager的建置環境，以及如何建置和測試您的程式碼。
exl-id: a4e19c59-ef2c-4683-a1be-3ec6c0d2f435
source-git-commit: 0e1fbef77cb42dd8bb280bb971dc0643019901a3
workflow-type: tm+mt
source-wordcount: '985'
ht-degree: 0%

---

# 建置環境 {#build-environment}

了解Cloud Manager的建置環境，以及如何建置和測試您的程式碼。

## 建置環境詳細資訊 {#build-environment-details}

Cloud Manager會使用專用的建置環境來建立和測試您的程式碼。

* 建置環境是以Linux為基礎，衍生自Ubuntu 18.04。
* 已安裝Apache Maven 3.6.0。
* 安裝的Java版本是OracleJDK 8u202和OracleJDK 11.0.2。
* 依預設， `JAVA_HOME` 環境變數設為 `/usr/lib/jvm/jdk1.8.0_202`  包含OracleJDK 8u202。 請參閱 [備用Maven執行JDK版本](#alternate-maven-jdk-version) 一節以取得詳細資訊。
* 安裝了一些必要的附加系統軟體包。

   * `bzip2`
   * `unzip`
   * `libpng`
   * `imagemagick`
   * `graphicsmagick`

* 可在生成時安裝其他軟體包，如一節中所述 [安裝其他系統包。](#installing-additional-system-packages)
* 每棟建築都是在原始環境下建造的；建置容器不會在執行之間保留任何狀態。
* Maven一律使用下列三個命令執行。

* `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
* `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
* `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent package`
* Maven是在系統層級使用 `settings.xml` 檔案，該檔案使用名為的配置檔案自動包括公共Adobe對象儲存庫 `adobe-public`. (請參閱 [Adobe公用Maven存放庫](https://repo1.maven.org/) 如需詳細資訊)。

>[!NOTE]
>
>雖然Cloud Manager不會定義 `jacoco-maven-plugin`，使用的版本必須至少 `0.7.5.201505241946`.

### 使用特定Java版本 {#using-java-support}

依預設，專案是由Cloud Manager建置程式使用Oracle8 JDK建置。 希望使用替代JDK的客戶有兩個選項。

* [使用Maven工具鏈。](#maven-toolchains)
* [為整個Maven執行過程選擇替代的JDK版本。](#alternate-maven-jdk-version)

#### Maven工具鏈 {#maven-toolchains}

此 [Maven工具鏈插件](https://maven.apache.org/plugins/maven-toolchains-plugin/) 允許項目選擇要在工具鏈感知的Maven插件的上下文中使用的特定JDK（或工具鏈）。 這是在專案的 `pom.xml` 檔案，方法是指定供應商和版本值。

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

這會導致所有工具鏈感知的Maven外掛程式都使用OracleJDK（第11版）。

使用此方法時，Maven本身仍會使用預設的JDK(Oracle8)執行，且 `JAVA_HOME`  環境變數未變更。 因此，透過外掛程式（例如Apache Maven Enforcer外掛程式）檢查或強制執行Java版本時無法運作，且不得使用這類外掛程式。

當前可用的供應商/版本組合包括：

| 廠商 | 版本 |
|---|---|
| `oracle` | `8` |
| `oracle` | `11` |
| `sun` | `8` |
| `sun` | `11` |

此表格指的是產品版本號。 Java組建編號或安裝路徑可能會反映舊的Java版本慣例，例如Java 8適用的1.8。

>[!NOTE]
>
>自2022年4月起，OracleJDK將是AEM應用程式開發與運作的預設JDK。 即使在Maven工具鏈中明確選取了替代選項，Cloud Manager的建置程式仍會自動切換為使用OracleJDK。 如需詳細資訊，請參閱4月的發行說明。

#### 備用Maven執行JDK版本 {#alternate-maven-jdk-version}

您也可以選取Java 8或Java 11作為JDK，以執行整個Maven執行。 與工具鏈選項不同，這會更改用於所有插件的JDK，除非還設定了工具鏈配置，在這種情況下，工具鏈配置仍應用於具有工具鏈的Maven插件。 因此，請使用 [Apache Maven Enforcer Plugin](https://maven.apache.org/enforcer/maven-enforcer-plugin/) 都行。

要執行此操作，請建立名為 `.cloudmanager/java-version` 在管道使用的git存放庫分支中。 此檔案可包含內容11或8。 會忽略任何其他值。 若指定11，則使用Oracle11，且 `JAVA_HOME` 環境變數設為 `/usr/lib/jvm/jdk-11.0.2`. 若指定8，則使用Oracle8，且 `JAVA_HOME` 環境變數設為 `/usr/lib/jvm/jdk1.8.0_202`.

## 環境變數 {#environment-variables}

### 標準環境變數 {#standard-environ-variables}

您可能會發現，必鬚根據程式或管道的相關資訊來變更建置程式。

例如，如果是透過Gulp等工具進行建置時間JavaScript縮制，則在針對開發環境建置時，可能會想使用不同的縮制層級，而非針對測試和生產建置。

為了支援此功能，Cloud Manager會將這些標準環境變數新增至每次執行的組建容器。

| 變數名稱 | 定義 |
|---|---|
| `CM_BUILD` | 一律設為 `true` |
| `BRANCH` | 為執行配置的分支 |
| `CM_PIPELINE_ID` | 數值管線識別碼 |
| `CM_PIPELINE_NAME` | 管道名稱 |
| `CM_PROGRAM_ID` | 數值程式標識符 |
| `CM_PROGRAM_NAME` | 方案名稱 |
| `ARTIFACTS_VERSION` | 對於階段或生產管道，由Cloud Manager產生的合成版本 |
| `CM_AEM_PRODUCT_VERSION` | 發行版本 |

### 管道變數 {#pipeline-variables}

您的建立程式可能取決於特定設定變數，這些變數不適合放置在Git存放庫中，或您可能需要使用相同分支，在不同管道執行之間加以變更。

Cloud Manager允許透過Cloud Manager API或Cloud Manager CLI，依每個管道設定這些變數。 變數可儲存為純文字，或閒置時加密。 無論是哪種情況，變數都會在建置環境內以環境變數的形式提供，然後可從內部參照 `pom.xml` 檔案或其他建置指令碼。

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
* 每個管道有200個變數的限制。
* 每個名稱必須少於100個字元。
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

## 安裝其他系統包 {#installing-additional-system-packages}

某些組建需要安裝額外的系統套件，才能完全運作。 例如，生成可以調用Python或Ruby指令碼，並且需要安裝適當的語言解釋器。 您可以呼叫 [`exec-maven-plugin`](https://www.mojohaus.org/exec-maven-plugin/) 在 `pom.xml` 調用APT。 此執行通常會包裝在Cloud Manager專屬的Maven設定檔中。 此示例安裝Python。

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
>以此方式安裝系統套件時，不會將其安裝在用於執行Adobe Experience Manager的執行階段環境中。 若您需要AEM環境上安裝系統套件，請連絡您的Adobe代表。
