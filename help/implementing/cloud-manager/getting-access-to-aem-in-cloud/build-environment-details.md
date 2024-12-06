---
title: Cloud Manager的組建環境
description: 了解 Cloud Manager 的構建環境以及它如何構建和測試您的程式碼。
exl-id: a4e19c59-ef2c-4683-a1be-3ec6c0d2f435
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 3bc9ec12de604818f6be1c0717566a5f16c6a7b9
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 58%

---


# 建置環境 {#build-environment}

了解 Cloud Manager 的構建環境以及它如何構建和測試您的程式碼。

## 建置環境詳細資訊 {#build-environment-details}

Cloud Manager 使用專門的構建環境構建和測試您的程式碼。

* 建置環境以 Linux 為基礎，衍生自 Ubuntu 22.04。
* 已安裝 Apache Maven 3.9.4。
   * Adobe 建議使用者[更新其 Maven 存放庫以使用 HTTPS 而非 HTTP](#https-maven)。
* <!-- OLD --> 安裝的Java版本為OracleJDK 11.0.22和OracleJDK 8u401。
<!-- NEW but needed to be removed 12/5/24 * The Java versions installed are Oracle JDK 11.0.22, Oracle JDK 17.0.10, and Oracle JDK 21.0.4. -->
<!-- OLD --> * **重要：**&#x200B;依預設，JAVA_HOME環境變數設為`/usr/lib/jvm/jdk1.8.0_401`，其中包含OracleJDK 8u401。 AEM Cloud專案應覆寫此預設值，才能使用JDK 11。 如需更多詳細資訊，請參閱設定Maven JDK版本區段。
<!-- NEW but needed to be removed 12/5/24 * **IMPORTANT:** By default, the `JAVA_HOME` environment variable is set to `/usr/lib/jvm/jdk1.8.0_401`, which contains Oracle JDK 8u401. ***This default should be overridden for AEM Cloud Projects to use JDK 21 (preferred), 17, or 11***. See the [Setting the Maven JDK Version](#alternate-maven-jdk-version) section for more details. -->
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
>雖然 Cloud Manager 並未定義 `jacoco-maven-plugin` 的特定版本，但使用的版本必須至少為 `0.7.5.201505241946`。

## HTTPS Maven 存放庫 {#https-maven}

Cloud Manager [2023.10.0 版](/help/implementing/cloud-manager/release-notes/2023/2023-10-0.md)開始推出組建環境的更新 (在 2023.12.0 版時完成)，其中包含 Maven 3.8.8 的更新。Maven 3.8.1 引入一項重大變更，即為安全性增強，其目的在減少潛在漏洞。具體而言，Maven 現在預設停用所有不安全的 `http://*` 鏡像，如 [Maven 發行說明](https://maven.apache.org/docs/3.8.1/release-notes.html#cve-2021-26291)中所述。

由於此安全性增強，某些使用者可能會在建置步驟中遇到問題，特別是從使用不安全 HTTP 連線的 Maven 存放庫下載成品時。

為了確保更新的版本有流暢的使用體驗，Adobe 建議使用者更新其 Maven 存放庫以使用 HTTPS 而非 HTTP。這項調整符合產業日益轉向使用安全通訊協定的趨勢，有助於維持安全可靠的建置程序。

<!-- OLD below -->

### 使用特定的Java版本

Cloud Manager建置流程預設會使用Oracle8 JDK來建置專案，但AEM Cloud Service客戶應將Maven執行JDK版本設定為11。

<!-- OLD below -->

#### 設定Maven JDK版本

Adobe建議您將整個Maven執行的JDK版本設定為`.cloudmanager/java-version file`中的`11`。

若要這麼做，請在管道使用的Git存放庫分支中建立名為`.cloudmanager/java-version`的檔案。 編輯檔案，使其僅包含文字`11`。 雖然Cloud Manager也接受`8`的值，但AEM Cloud Service專案不再支援此版本。 任何其他值會受到忽略。指定`11`時，會使用Oracle11，且`JAVA_HOME`環境變數設為`/usr/lib/jvm/jdk-11.0.22`。

<!-- NEW but needed to be removed 12/5/24 ### Use a specific Java version {#using-java-support}

The Cloud Manager build process uses the Oracle 8 JDK to build projects by default, but AEM Cloud Service customers should set the Maven execution JDK version to 21 (preferred), 17, or 11.

#### Set the Maven JDK version {#alternate-maven-jdk-version}

Adobe recommends setting the Maven execution JDK version to `21` or `17` in a `.cloudmanager/java-version` file.

To do so, create a file named `.cloudmanager/java-version` in the Git repository branch used by the pipeline. Edit the file so that it contains only the text, `21` or `17`. While Cloud Manager also accepts a value of `8`, this version is no longer supported for AEM Cloud Service projects. Any other value is ignored. When `21` or `17` is specified, Oracle Java 21 or Oracle Java 17 is used and the `JAVA_HOME` environment variable is set to `/usr/lib/jvm/jdk-21` or `/usr/lib/jvm/jdk-17`.

#### Prerequisites for migrating to building with Java 21 or Java 17 {#prereq-for-building}

>[!NOTE]
>
>*When migrating your application to a new Java build version and runtime version, thoroughly test in dev and stage environments before deploying to production.
>Of special note, the following features have not yet been formally validated with Java 21 runtime: [Forms](/help/forms/home.md), [Workflows](/help/sites-cloud/authoring/workflows/overview.md), [Inbox](/help/sites-cloud/authoring/inbox.md), and [Projects](/help/sites-cloud/authoring/projects/overview.md). If your application relies on these features, ensure comprehensive testing to verify functionality.*

##### About some translation features {#translation-features}

The following features might not function correctly when building with Java 21 or Java 17, and Adobe expects to resolve them by early 2025:

* `XLIFF` (XML Localization Interchange File Format) fails when using Human Translation.  
* `I18n` (Internationalization) does not properly handle language locales Hebrew (`he`), Indonesian (`in`), and Yiddish (`yi`) due to changes in the Locale constructor in newer Java versions.

#### Runtime requirements {#runtime-requirements}

The Java 21 runtime is used for builds on Java 21, Java 17, and Java 11 starting in February 2025. To ensure compatibility, the following adjustments are necessary. 

Library updates can be applied anytime, as they remain compatible with older Java versions.

* **Minimum version of `org.objectweb.asm`:**
Update the usage of `org.objectweb.asm` to version 9.5 or higher to ensure support for newer JVM runtimes.

* **Minimum version of `org.apache.groovy`:**
Update the usage of `org.apache.groovy` to version 4.0.22 or higher to ensure support for newer JVM runtimes.

  This bundle can be indirectly included by adding third party dependencies such as the AEM Groovy Console.

* **Edit a runtime parameter:**
When running AEM locally with Java 21, the start scripts (`crx-quickstart/bin/start` or `crx-quickstart/bin/start.bat`) fail due to the `MaxPermSize` parameter. As a remedy, either remove `-XX:MaxPermSize=256M` from the script or define the environment variable `CQ_JVM_OPTS`, setting it to `-Xmx1024m -Djava.awt.headless=true`.

  Adobe plans to resolve this issue in a future release.

>[!NOTE]
>
>When `.cloudmanager/java-version` is set to `21` or `17`, the Java 21 runtime is deployed. In February or March 2025, the Java 21 runtime is planned for deployment to all customers, even if Java 11 is used to build your code. 

#### Build time requirements

The following adjustments are required to allow building the project with Java 21 and Java 17. They can be updated at any time as they are compatible with older versions of Java.

* **Minimum version of `bnd-maven-plugin`:**
Update the usage of `bnd-maven-plugin` to version 6.4.0 to ensure support for newer JVM runtimes. 

  Versions 7 or higher are not compatible with Java 11 or lower so an upgrade to that version is not recommended.

* **Minimum version of `aemanalyser-maven-plugin`:**
Update the usage of `aemanalyser-maven-plugin` to version 1.6.6 or higher to ensure support for newer JVM runtimes.

* **Minimum version of `maven-bundle-plugin`:**
Update the usage of `maven-bundle-plugin` to version 5.1.5 or higher to ensure support for newer JVM runtimes. 

  Versions 6 or higher are not compatible with Java 11 or lower so an upgrade to that version is not recommended.

* **Update dependencies in `maven-scr-plugin`:**
The `maven-scr-plugin` is not directly compatible with Java 21 or Java 17. However, descriptor files can be generated by updating the ASM dependency version in the plugin configuration, as shown in the following example:

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
-->


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

部分組建需要其他系統套件才能完全運作。 例如，組建可能會叫用Python或Ruby指令碼，而且必須安裝適當的語言解譯器。 您可以呼叫`pom.xml`中的[`exec-maven-plugin`](https://www.mojohaus.org/exec-maven-plugin/)來叫用APT，以管理此安裝程式。 這項執行通常應包裝在 Cloud Manager 特定的 Maven 設定檔中。若要安裝 Python。

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
