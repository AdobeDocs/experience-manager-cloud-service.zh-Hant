---
title: 構建環境詳細資訊
description: 構建環境詳細資訊-Cloud Services
exl-id: a4e19c59-ef2c-4683-a1be-3ec6c0d2f435
source-git-commit: c3b70f513455dfeaac6bc20c05fc9c35dcddf73e
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---

# 瞭解構建環境{#understanding-build-environment}

## 構建環境詳細資訊{#build-environment-details}

Cloud Manager使用專業的構建環境來構建和測試代碼。 此環境具有以下屬性：

* 構建環境基於Linux，源自Ubuntu 18.04。
* 已安裝Apache Maven 3.6.0。
* 安裝的Java版本是OracleJDK 8u202和11.0.2。
* 安裝了一些其他系統軟體包是必要的：

   * bzip2
   * unzip
   * libpng
   * imagick
   * graphicsmagick

* 其他軟體包可在構建時安裝，如[下面所述](#installing-additional-system-packages)。
* 每棟建築都是在原始環境下完成的；建置容器不會在執行之間保留任何狀態。
* Maven一律使用下列三個命令執行：

   * `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
   * `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
   * `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent packageco-maven-plugin:prepare-agent package`
* Maven在系統級別配置了settings.xml檔案，該檔案使用名為`adobe-public`的配置檔案自動包括公共Adobe **Artifact**&#x200B;儲存庫。 (有關詳細資訊，請參閱[Adobe公共Maven儲存庫](https://repo.adobe.com/))。

>[!NOTE]
>雖然Cloud Manager未定義`jacoco-maven-plugin`的特定版本，但使用的版本至少必須是`0.7.5.201505241946`。

### 使用Java 11支援{#using-java-support}

Cloud Manager現在支援使用Java 8和Java 11建立客戶專案。 依預設，專案是使用Java 8建立。

想要在其專案中使用Java 11的客戶可使用[Apache Maven Toolchains Plugin](https://maven.apache.org/plugins/maven-toolchains-plugin/)來這麼做。

若要這麼做，請在pom.xml檔案中新增如下所示的`<plugin>`項目：

```
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

>[!NOTE]
>支援的供應商值為`oracle`和`sun`，支援的版本值為`1.8`、`1.11`和`11`。

>[!NOTE]
>Cloud Manager專案組建仍使用Java 8來叫用Maven，因此，透過例如[Apache Maven Enforcer Plugin](https://maven.apache.org/enforcer/maven-enforcer-plugin/)等外掛程式，檢查或強制在工具鏈外掛程式中設定的Java版本無法運作，且不得使用此類外掛程式。

## 環境變數{#environment-variables}

### 標準環境變數{#standard-environ-variables}

在某些情況下，客戶會發現必鬚根據方案或管道的相關資訊來變更建立程式。

例如，如果正在進行建置時期的JavaScript精簡化，透過例如gulp等工具，在建立開發環境時，可能會想要使用不同的精簡化層級，而非建立舞台和生產環境。

為支援此功能，Cloud Manager會將這些標準環境變數新增至每個執行的建立容器。

| **變數名稱** | **定義** |
|---|---|
| CM_BUILD | 一律設為&quot;true&quot; |
| 分支 | 為執行配置的分支 |
| CM_PIPELINE_ID | 數值管線標識符 |
| CM_PIPELINE_NAME | 管線名稱 |
| CM_PROGRAM_ID | 數值程式標識符 |
| CM_PROGRAM_NAME | 程式名 |
| 對象_版本 | 對於舞台或生產管道，由Cloud Manager生成的合成版本 |
| CM_AEM_PRODUCT_VERSION | 發行名稱 |

### 管線變數{#pipeline-variables}

在某些情況下，客戶的構建過程可能取決於特定的配置變數，這些變數不適合放置在Git儲存庫中，或者需要使用同一分支在不同的管線執行之間有所不同。

Cloud Manager允許通過Cloud Manager API或Cloud Manager CLI按管道配置這些變數。 變數可儲存為純文字或在閒置時加密。 在這兩種情況下，變數都可在建立環境中做為環境變數使用，然後可從`pom.xml`檔案或其他建立指令碼中參考。

要使用CLI設定變數，請運行如下命令：

`$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test`

目前的變數可以列出：

`$ aio cloudmanager:list-pipeline-variables PIPELINEID`

變數名稱只能包含英數字元和底線(_)字元。 按照慣例，名稱應全部大寫。 每個管線有200個變數的限制，每個名稱必須少於100個字元，而字串類型變數的每個值必須少於2048個字元，secretString類型變數的每個值必須少於500個字元。

當在`Maven pom.xml`檔案中使用時，使用類似下列的語法將這些變數對應至Maven屬性通常會很有幫助：

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

## 安裝其他系統軟體包{#installing-additional-system-packages}

某些構建需要安裝其他系統軟體包才能完全運作。 例如，構建版本可以調用Python或ruby指令碼，因此需要安裝適當的語言解釋器。 若要這麼做，請呼叫[exec-maven-plugin](https://www.mojohaus.org/exec-maven-plugin/)以叫用APT。 此執行通常應包在Cloud Manager特定的Maven配置式中。 例如，要安裝python:

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

同樣的技術也可用於安裝語言特定的軟體包，即使用`gem`（對於RubyGems）或`pip`（對於Python軟體包）。

>[!NOTE]
>以此方式安裝系統軟體包會&#x200B;**not**&#x200B;在運行Adobe Experience Manager的運行時環境中安裝它。 如果您需要在環境中安裝系統包，請AEM與Adobe代表聯繫。
