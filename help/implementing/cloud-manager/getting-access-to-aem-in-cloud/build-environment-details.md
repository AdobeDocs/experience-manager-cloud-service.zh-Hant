---
title: Cloud Manager的組建環境
description: 了解 Cloud Manager 的構建環境以及它如何構建和測試您的程式碼。
exl-id: a4e19c59-ef2c-4683-a1be-3ec6c0d2f435
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1547'
ht-degree: 29%

---


# 建置環境 {#build-environment}

了解 Cloud Manager 的構建環境以及它如何構建和測試您的程式碼。

>[!TIP]
>
>本檔案說明Cloud Manager為開發AEM as a Cloud Service專案而建立的組建環境。 如需AEM as a Cloud Service支援的內容製作使用者端平台的詳細資料，請參閱檔案[支援的使用者端平台。](/help/overview/supported-platforms.md)

## 建置環境詳細資訊 {#build-environment-details}

Cloud Manager 使用專門的構建環境構建和測試您的程式碼。

* 建置環境以 Linux 為基礎，衍生自 Ubuntu 22.04。
* 已安裝 Apache Maven 3.9.4。
   * Adobe 建議使用者[更新其 Maven 存放庫以使用 HTTPS 而非 HTTP](#https-maven)。
<!-- OLD Removed 1/16/25 * The Java versions installed are Oracle JDK 11.0.22 and Oracle JDK 8u401. -->
* 已安裝的Java版本為Oracle JDK 11.0.22、Oracle JDK 17.0.10和Oracle JDK 21.0.4。

<!-- OLD Removed 1/16/25 * **IMPORTANT:** By default, the JAVA_HOME environment variable is set to `/usr/lib/jvm/jdk1.8.0_401`, which contains Oracle JDK 8u401. This default should be overridden for AEM Cloud Projects to use JDK 11. See the Setting the Maven JDK Version section for more details. -->
* **重要：**&#x200B;依預設，`JAVA_HOME`環境變數設為`/usr/lib/jvm/jdk1.8.0_401`，其中包含Oracle JDK 8u401。 ***AEM雲端專案應覆寫此預設以使用JDK 21 （偏好設定）、17或11***。 如需詳細資訊，請參閱[設定Maven JDK版本](#alternate-maven-jdk-version)區段。
* 安裝了一些必要的附加系統套件。
   * `bzip2`
   * `unzip`
   * `libpng`
   * `imagemagick`
   * `graphicsmagick`
* 在建置時間可安裝其他套件，如[安裝附加系統套件](#installing-additional-system-packages)部份中所述。
* 每個組建都可在乾淨的環境中執行，組建容器在執行之間不保留任何狀態。
* 一直使用下列三個命令執行 Maven：
   * `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
   * `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
   * `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent package`
* 透過 `settings.xml` 檔案在系統層級設定 Maven，這會利用名為 `adobe-public` 的設定檔自動納入公共 Adobe 成品存放庫。如需更多詳細資訊，請參閱 [Adobe 公共 Maven 存放庫](https://repo1.maven.org/)。

>[!NOTE]
>
>Cloud Manager未指定`jacoco-maven-plugin`的特定版本，但所需版本取決於專案的Java版本。 對於Java 8，外掛程式版本必須至少為`0.7.5.201505241946`，而較新的Java版本可能需要較新的版本。

## HTTPS Maven 存放庫 {#https-maven}

Cloud Manager [2023.10.0 版](/help/implementing/cloud-manager/release-notes/2023/2023-10-0.md)開始推出組建環境的更新 (在 2023.12.0 版時完成)，其中包含 Maven 3.8.8 的更新。Maven 3.8.1 引入一項重大變更，即為安全性增強，其目的在減少潛在漏洞。具體而言，Maven 現在預設停用所有不安全的 `http://*` 鏡像，如 [Maven 發行說明](https://maven.apache.org/docs/3.8.1/release-notes.html#cve-2021-26291)中所述。

由於此安全性增強，某些使用者可能會在建置步驟中遇到問題，特別是從使用不安全 HTTP 連線的 Maven 存放庫下載成品時。

為了確保更新的版本有流暢的使用體驗，Adobe 建議使用者更新其 Maven 存放庫以使用 HTTPS 而非 HTTP。這項調整符合產業日益轉向使用安全通訊協定的趨勢，有助於維持安全可靠的建置程序。

<!-- OLD below Removed 1/16/25

### Use a specific Java version

The Cloud Manager build process uses the Oracle 8 JDK to build projects by default, but AEM Cloud Service customers should set the Maven execution JDK version to 11. -->

<!-- OLD below Removed 1/16/25

#### Set the Maven JDK version

Adobe recommends that you set the JDK version for the entire Maven execution to `11` in a `.cloudmanager/java-version file`.

To do so, create a file named `.cloudmanager/java-version` in the git repository branch used by the pipeline. Edit the file so that it contains only the text, `11`. While Cloud Manager also accepts a value of `8`, this version is no longer supported for AEM Cloud Service projects. Any other value is ignored. When `11` is specified, Oracle 11 is used and the `JAVA_HOME` environment variable is set to `/usr/lib/jvm/jdk-11.0.22`. -->

### 使用特定的Java版本 {#using-java-support}

Cloud Manager建置流程預設會使用Oracle 8 JDK建置專案，但AEM Cloud Service客戶應將Maven執行JDK版本設為21 （偏好設定）、17或11。

#### 設定Maven JDK版本 {#alternate-maven-jdk-version}

若要設定Maven執行JDK，請在管道使用的Git存放庫分支中建立名為`.cloudmanager/java-version`的檔案。 編輯檔案，使其僅包含文字`21`或`17`。 雖然Cloud Manager也接受`8`的值，但AEM Cloud Service專案不再支援此版本。 任何其他值會受到忽略。指定`21`或`17`時，會使用Oracle Java 21或Oracle Java 17。


#### 移轉至使用Java 21或Java 17建置的先決條件 {#prereq-for-building}

為了使用Java 21或Java 17進行建置，Cloud Manager現在使用SonarQube 9.9，其與這些Java版本相容。 此變更已在Cloud Manager 2025.1.0版中引入。升級SonarQube不需要客戶採取任何動作。 如需詳細資訊及瞭解變更，請參閱[Cloud Manager 2025.1.0](/help/implementing/cloud-manager/release-notes/2025/2025-1-0.md)發行說明。

將應用程式移轉至新的Java組建版本和執行階段版本時，請先在開發和測試環境中徹底測試，然後再部署到生產環境。

Adobe建議下列部署策略：

1. 使用Java 21執行您的本機SDK (可從https://experience.adobe.com/#/downloads下載)，並將您的應用程式部署至其中並驗證其功能。 檢查記錄檔中是否有錯誤，指出類別載入或位元組碼編排發生問題。
1. 在Cloud Manager存放庫中設定分支以使用Java 21作為建置時間Java版本，設定開發管道以使用此分支並執行管道。 執行驗證測試。
1. 如果情況良好，請設定您的stage/prod管道以使用Java 21作為建置時間Java版本並執行管道。

##### 關於某些翻譯功能 {#translation-features}

在Java 21執行階段上部署下列功能時，這些功能可能會無法正常運作，而Adobe預計可在2025年初解決這些問題：

* 使用人工翻譯時，`XLIFF` （XML本地化交換檔案格式）失敗。
* `I18n` （國際化）無法正確處理希伯來文(`he`)、印尼(`in`)和意第緒文(`yi`)的語言環境，因為較新Java版本中的語言環境建構函式有所變更。

#### 執行階段需求 {#runtime-requirements}

Java 21執行階段已套用至所有符合資格的環境，這些環境是指在AEM發行說17098或更新版本上符合以下條件的環境。 如果環境不符合條件，請務必進行調整，以確保效能、可用性和安全性。

* **ASM的最低版本：**
將Java套件`org.objectweb.asm` （通常整合在`org.ow2.asm.*`成品中）的使用更新至9.5版或更新版本，以確保支援較新的JVM執行階段。

* **Groovy的最低版本：**
將Java套件`org.apache.groovy`或`org.codehaus.groovy`的使用更新至4.0.22版或更新版本，以確保支援較新的JVM執行階段。

  新增第三方相依性 (例如 AEM Groovy 主控台) 可以間接包含此搭售方案。

* **Aries SPIFly的最低版本：**
將Java套件`org.apache.aries.spifly.dynamic.bundle`的使用更新至1.3.6版或更新版本，以確保支援更新的JVM執行階段。

AEM Cloud Service SDK支援Java 21，讓您在執行Cloud Manager管道之前，先驗證專案與Java 21的相容性。

* **編輯執行階段引數：**
使用Java 21在本機執行AEM時，由於`crx-quickstart/bin/start`引數，啟動指令碼（`crx-quickstart/bin/start.bat`或`MaxPermSize`）會失敗。 作為補救方法，請從指令碼移除`-XX:MaxPermSize=256M`或定義環境變數`CQ_JVM_OPTS`，將其設定為`-Xmx1024m -Djava.awt.headless=true`。

  AEM Cloud Service SDK版本19149和更新版本可解決此問題。

>[!IMPORTANT]
>
>如果環境尚未自動更新為Java 21執行階段，您可以使用Java 17或21建置以觸發它。 將`.cloudmanager/java-version`設定為`21`或`17`即可完成這項作業。 如有疑問，請連絡Adobe： [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com)。

#### 建置時間需求 {#build-time-reqs}

需要進行下列調整，才能使用Java 21和Java 17建置專案。 甚至在您執行Java 21和Java 17之前，這些檔案就已經可以更新了，因為它們與舊版Java相容。

AEM Cloud Service客戶建議儘早使用Java 21建置專案，以運用新的語言功能。

* **最低版本`bnd-maven-plugin`：**
將`bnd-maven-plugin`的使用更新至6.4.0版，以確保支援較新的JVM執行階段。

  版本7或更新版本與Java 11或更低版本不相容，因此不建議升級至該版本。

* **最低版本`aemanalyser-maven-plugin`：**
將`aemanalyser-maven-plugin`的使用更新至1.6.6版或更新版本，以確保支援較新的JVM執行階段。

* **最低版本`maven-bundle-plugin`：**
將`maven-bundle-plugin`的使用更新至5.1.5版或更新版本，以確保支援較新的JVM執行階段。

  版本6或更高版本與Java 11或更低版本不相容，因此不建議升級至該版本。

* **更新`maven-scr-plugin`中的相依性：**
`maven-scr-plugin`與Java 21或Java 17不直接相容。 不過，可以透過更新外掛程式組態中的ASM相依性版本來產生描述項檔案，如下列範例所示：

```XML
<project>
  ...
  <build>
    ...
    <plugins>
      ...
      <plugin>
        <groupId>org.apache.felix</groupId>
        <artifactId>maven-scr-plugin</artifactId>
        <version>1.26.4</version>
        <executions>
          <execution>
            <id>generate-scr-scrdescriptor</id>
            <goals>
              <goal>scr</goal>
            </goals>
          </execution>
        </executions>
        <dependencies>
          <dependency>
            <groupId>org.ow2.asm</groupId>
            <artifactId>asm-analysis</artifactId>
            <version>9.7.1</version>
            <scope>compile</scope>
          </dependency>
        </dependencies>
      </plugin>
      ...
    </plugins>
    ...
  </build>
  ...
</project>
```

## 環境變數 — 標準 {#environment-variables}

您可能會發現有必要根據有關計畫或管道的資訊來改變建置流程。

例如，如果在建置時間使用gulp之類的工具進行JavaScript縮制，則不同環境可能偏好使用不同的縮制層級。 與中繼和生產環境相比，開發組建可能會使用較輕的縮制層級。

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

## 環境變數 — 管道 {#pipeline-variables}

您的建置流程可能需要不應儲存在Git存放庫中的特定設定變數。 此外，您可能需要在使用同一分支的管道執行之間調整這些變數。

另請參閱[設定管道變數](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md)以取得詳細資訊。

## 安裝其他系統套件 {#installing-additional-system-packages}

部分組建需要其他系統套件才能完全運作。 例如，組建可能會叫用Python或Ruby指令碼，而且必須安裝適當的語言解譯器。 您可以呼叫[`exec-maven-plugin`中的](https://www.mojohaus.org/exec-maven-plugin/)`pom.xml`來叫用APT，以管理此安裝程式。 這項執行通常應包裝在 Cloud Manager 特定的 Maven 設定檔中。若要安裝 Python。

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
