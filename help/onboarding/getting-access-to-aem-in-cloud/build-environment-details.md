---
title: 構建環境詳細資訊
description: 構建環境詳細資訊——雲服務
translation-type: tm+mt
source-git-commit: 1c4d45fd994529815e7428b1d239cf89265fb775
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 0%

---


# 瞭解構建環境詳細資訊 {#understanding-build-environment}

## 構建環境詳細資訊 {#build-environment-details}

Cloud Manager使用專業的構建環境來構建和測試代碼。 此環境具有以下屬性：

* 構建環境基於Linux，源自Ubuntu 18.04。
* 已安裝Apache Maven 3.6.0。
* 安裝的Java版本是Oracle JDK 8u202和11.0.2。
* 安裝了一些其他系統軟體包是必要的：

   * bzip2
   * unzip
   * libpng
   * imagick
   * graphicsmagick

* 其他軟體包可在構建時安裝，如下 [所述](#installing-additional-system-packages)。
* 每棟建築都是在原始環境下完成的；建置容器不會在執行之間保留任何狀態。
* Maven始終使用以下命令運行： *mvn -batch-mode clean org.jaco:jaco-maven-plugin:prepare-agent套件*
* Maven是在系統層級以settings.xml檔案來設定，該檔案會自動包含公用的Adobe **Artifact** 儲存庫。 (如需詳 [細資訊，請參閱Adobe Public Maven Repository](https://repo.adobe.com/) )。

>[!NOTE]
>雖然Cloud Manager未定義特定版本， `jacoco-maven-plugin`但使用的版本至少必須是 `0.7.5.201505241946`。

### 使用Java 11支援 {#using-java-support}

Cloud Manager現在支援使用Java 8和Java 11建立客戶專案。 依預設，專案是使用Java 8建立。

想要在其專案中使用Java 11的客戶，可使用 [Apache Maven Toolchains外掛程式](https://maven.apache.org/plugins/maven-toolchains-plugin/)。

若要這麼做，請在pom.xml檔案中新增 `<plugin>` 如下的項目：

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
>支援的供應商 `oracle` 值是 `sun`。
>
>支援的版 `1.8`本值 `1.11`有、和 `11`。

## 環境變數 {#environment-variables}

### 標準環境變數 {#standard-environ-variables}

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

### 管線變數 {#pipeline-variables}

在某些情況下，客戶的構建過程可能取決於特定的配置變數，這些變數不適合放置在Git儲存庫中，或者需要使用同一分支在不同的管線執行之間有所不同。

Cloud Manager允許通過Cloud Manager API或Cloud Manager CLI按管道配置這些變數。 變數可儲存為純文字或在閒置時加密。 在這兩種情況下，變數都可在建立環境中做為環境變數使用，然後可從檔案或其他建立指令 `pom.xml` 碼中參考。

要使用CLI設定變數，請運行如下命令：

`$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test`

目前的變數可以列出：

`$ aio cloudmanager:list-pipeline-variables PIPELINEID`

變數名稱只能包含英數字元和底線(_)字元。 按照慣例，名稱應全部大寫。 每個管線有200個變數的限制，每個名稱必須小於100個字元，每個值必須小於2048個字元。

在檔案中使用時， `Maven pom.xml` 通常使用類似下列的語法將這些變數對應至Maven屬性會很有幫助：

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

## 安裝其他系統軟體包 {#installing-additional-system-packages}

某些構建需要安裝其他系統軟體包才能完全運作。 例如，構建版本可以調用Python或ruby指令碼，因此需要安裝適當的語言解釋器。 若要這麼做，請呼 [叫exec-maven-plugin](https://www.mojohaus.org/exec-maven-plugin/) 以叫用APT。 此執行通常應包在Cloud Manager特定的Maven配置式中。 例如，要安裝python:

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

此相同技術可用於安裝語言特定的軟體包，即使用RubyGems或 `gem` Python軟體包 `pip` 進行安裝。

>[!NOTE]
>
>以此方式安裝系統套件 **不會** ，將它安裝在執行Adobe Experience Manager時所用的執行階段環境中。 如果您需要在AEM環境中安裝系統套件，請連絡您的Adobe代表。