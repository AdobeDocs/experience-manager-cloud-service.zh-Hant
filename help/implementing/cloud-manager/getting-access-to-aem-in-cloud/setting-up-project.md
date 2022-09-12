---
title: 專案設定
description: 了解如何使用Maven建立AEM專案，以及在建立專案時必須遵守的標準。
exl-id: 76af0171-8ed5-4fc7-b5d5-7da5a1a06fa8
source-git-commit: 430179bf13c1fff077c515eed0676430e9e7f341
workflow-type: tm+mt
source-wordcount: '1415'
ht-degree: 1%

---

# 專案設定 {#project-setup}

了解如何使用Maven建立AEM專案，以及在建立專案時必須遵守的標準。

## 專案設定詳細資訊 {#project-setup-details}

為了能順利透過Cloud Manager建立和部署AEM專案，必須遵循下列准則：

* 必須使用 [阿帕奇·馬文。](https://maven.apache.org)
* 一定有 `pom.xml` 檔案（位於git存放庫的根目錄中）。 此 `pom.xml` 檔案可以參照任意數量的子模組（而子模組又可能有其他子模組等） 視需要。
* 您可以在您的 `pom.xml` 檔案。
   * 存取 [受密碼保護的對象儲存庫](#password-protected-maven-repositories) 設定時支援。 但是，不支援訪問受網路保護的對象儲存庫。
* 掃描內容包可發現可部署的內容包 `.zip` 檔案，包含在名為 `target`.
   * 任何數量的子模組都可產生內容包。
* 可部署的Dispatcher工件是透過掃描 `.zip` 檔案(也包含在名為的目錄中 `target`)，其目錄名為 `conf` 和 `conf.d`.
* 如果有多個內容包，則無法保證包部署的順序。
   * 如果需要特定順序，則可使用內容套件相依性來定義順序。
* 包可以 [已略過](#skipping-content-packages) 部署期間。

## 在Cloud Manager中啟用Maven設定檔 {#activating-maven-profiles-in-cloud-manager}

在某些有限的情況下，在Cloud Manager內執行時，您可能需要稍微改變您的建置程式，而非在開發人員工作站上執行。 對於這些情況， [Maven設定檔](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) 可用來定義不同環境（包括Cloud Manager）中，組建應如何不同。

在Cloud Manager建置環境中啟動Maven設定檔時，應先尋找 `CM_BUILD` [環境變數。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) 同樣地，您也應尋找缺少此變數，以完成僅在Cloud Manager建置環境之外使用的設定檔。

例如，如果您只想在組建在Cloud Manager內執行時輸出簡單訊息，您可以執行此操作。

```xml
        <profile>
            <id>cmBuild</id>
            <activation>
                  <property>
                        <name>env.CM_BUILD</name>
                  </property>
            </activation>
            <build>
                <plugins>
                    <plugin>
                        <artifactId>maven-antrun-plugin</artifactId>
                        <version>1.8</version>
                        <executions>
                            <execution>
                                <phase>initialize</phase>
                                <configuration>
                                    <target>
                                        <echo>I'm running inside Cloud Manager!</echo>
                                    </target>
                                </configuration>
                                <goals>
                                    <goal>run</goal>
                                </goals>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
```

>[!NOTE]
>
>若要在開發人員工作站上測試此設定檔，您可以在命令列上啟用它(使用 `-PcmBuild`)或整合開發環境(IDE)中。

如果您只想在組建在Cloud Manager外部執行時輸出簡單訊息，您可以這麼做。

```xml
        <profile>
            <id>notCMBuild</id>
            <activation>
                  <property>
                        <name>!env.CM_BUILD</name>
                  </property>
            </activation>
            <build>
                <plugins>
                    <plugin>
                        <artifactId>maven-antrun-plugin</artifactId>
                        <version>1.8</version>
                        <executions>
                            <execution>
                                <phase>initialize</phase>
                                <configuration>
                                    <target>
                                        <echo>I'm running outside Cloud Manager!</echo>
                                    </target>
                                </configuration>
                                <goals>
                                    <goal>run</goal>
                                </goals>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
```

## 受密碼保護的Maven儲存庫支援 {#password-protected-maven-repositories}

>[!NOTE]
>
>密碼保護的Maven儲存庫中的成品應該非常謹慎地使用，因為目前通過此機制部署的代碼並未在所有 [代碼品質規則](/help/implementing/cloud-manager/custom-code-quality-rules.md) 在Cloud Manager的品質閘道中實作。 因此，它只應用在少數情況下，以及不系結至AEM的程式碼。 建議您同時使用二進位檔來部署Java來源以及整個專案原始碼。

若要在Cloud Manager中使用受密碼保護的Maven存放庫：

1. 將密碼（以及選擇性的使用者名稱）指定為機密 [管線變數。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)
1. 然後在名為的檔案中引用該秘密 `.cloudmanager/maven/settings.xml` 位於git存放庫中，緊接在 [Maven設定檔案](https://maven.apache.org/settings.html) 綱要。

當Cloud Manager建置程式開始時：

* 此 `<servers>` 此檔案中的元素將合併到預設值 `settings.xml` 檔案。
   * 伺服器ID從 `adobe` 和 `cloud-manager` 會視為保留，不應供自訂伺服器使用。
   * 伺服器ID與其中一個前置詞或預設ID不匹配 `central` Cloud Manager永遠不會鏡像。
* 備妥此檔案後，系統會從內部參考伺服器ID `<repository>` 和/或 `<pluginRepository>` 元素內 `pom.xml` 檔案。
* 通常， `<repository>` 和/或 `<pluginRepository>` 元素會包含在 [Cloud Manager專屬設定檔](#activating-maven-profiles-in-cloud-manager)，但並非嚴格必要。

例如，假設存放庫位於 `https://repository.myco.com/maven2`,Cloud Manager應使用的使用者名稱為 `cloudmanager`，密碼為 `secretword`. 請執行下列步驟。

1. 在管道中將密碼設定為機密。

   ```text
   $ aio cloudmanager:set-pipeline-variables PIPELINEID --secret CUSTOM_MYCO_REPOSITORY_PASSWORD secretword`
   ```

1. 請從 `.cloudmanager/maven/settings.xml` 檔案。

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <settings xmlns="https://maven.apache.org/SETTINGS/1.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="https://maven.apache.org/SETTINGS/1.0.0 https://maven.apache.org/xsd/settings-1.0.0.xsd">
       <servers>
           <server>
               <id>myco-repository</id>
               <username>cloudmanager</username>
              <password>${env.CUSTOM_MYCO_REPOSITORY_PASSWORD}</password>
           </server>
       </servers>
   </settings>
   ```

1. 最後，參考 `pom.xml` 檔案：

   ```xml
   <profiles>
       <profile>
           <id>cmBuild</id>
           <activation>
                   <property>
                       <name>env.CM_BUILD</name>
                   </property>
           </activation>
           <repositories>
                <repository>
                    <id>myco-repository</id>
                    <name>MyCo Releases</name>
                    <url>https://repository.myco.com/maven2</url>
                    <snapshots>
                        <enabled>false</enabled>
                    </snapshots>
                    <releases>
                        <enabled>true</enabled>
                    </releases>
                </repository>
            </repositories>
            <pluginRepositories>
                <pluginRepository>
                    <id>myco-repository</id>
                    <name>MyCo Releases</name>
                    <url>https://repository.myco.com/maven2</url>
                    <snapshots>
                        <enabled>false</enabled>
                    </snapshots>
                    <releases>
                        <enabled>true</enabled>
                    </releases>
                </pluginRepository>
            </pluginRepositories>
       </profile>
   </profiles>
   ```

### 部署來源 {#deploying-sources}

將Java來源與二進位檔一起部署至Maven存放庫是個不錯的作法。

若要這麼做，請在專案中設定maven-source-plugin。

```xml
         <plugin>
             <groupId>org.apache.maven.plugins</groupId>
             <artifactId>maven-source-plugin</artifactId>
             <executions>
                 <execution>
                     <id>attach-sources</id>
                     <goals>
                         <goal>jar-no-fork</goal>
                     </goals>
                 </execution>
             </executions>
         </plugin>
```

### 部署專案來源 {#deploying-project-sources}

最好將整個專案來源與二進位檔一併部署至Maven存放庫。 這可讓as重建確切的工件。

若要這麼做，請在專案中設定maven-assembly-plugin。

```xml
         <plugin>
             <groupId>org.apache.maven.plugins</groupId>
             <artifactId>maven-assembly-plugin</artifactId>
             <executions>
                 <execution>
                     <id>project-assembly</id>
                     <phase>package</phase>
                     <goals>
                         <goal>single</goal>
                     </goals>
                     <configuration>
                         <descriptorRefs>
                             <descriptorRef>project</descriptorRef>
                         </descriptorRefs>
                     </configuration>
                 </execution>
             </executions>
         </plugin>
```

## 跳過內容包 {#skipping-content-packages}

在Cloud Manager中，組建可能會產生任何數量的內容套件。 出於各種原因，可能希望生成內容包，但不要部署它。 例如，建立內容套件時，可能只會用於測試，或者會透過建置程式中的其他步驟（即另一個套件的子套件）重新封裝。

為了適應這些情況，Cloud manager將在內建內容包的屬性中 `cloudManagerTarget`查找名為 的屬性。如果此屬性設為 `none`，則會略過套件而未部署。

設定此屬性的機制取決於組建產生內容套件的方式。 例如，使用 `filevault-maven-plugin` 您可依下列方式設定外掛程式。

```xml
        <plugin>
            <groupId>org.apache.jackrabbit</groupId>
            <artifactId>filevault-package-maven-plugin</artifactId>
            <extensions>true</extensions>
            <configuration>
                <properties>
                    <cloudManagerTarget>none</cloudManagerTarget>
                </properties>
        <!-- other configuration -->
            </configuration>
        </plugin>
```

此 `content-package-maven-plugin` 有類似的設定。

```xml
        <plugin>
            <groupId>com.day.jcr.vault</groupId>
            <artifactId>content-package-maven-plugin</artifactId>
            <extensions>true</extensions>
            <configuration>
                <properties>
                    <cloudManagerTarget>none</cloudManagerTarget>
                </properties>
        <!-- other configuration -->
            </configuration>
        </plugin>
```

## 建置對象重用 {#build-artifact-reuse}

在許多情況下，相同的程式碼會部署至多個AEM環境。 如果可能，當Cloud Manager偵測到同一個git提交用於多個完整堆疊管道執行時，將避免重建程式碼基底。

啟動執行時，會擷取分支管道的目前HEAD提交。 提交雜湊會顯示在UI中，並透過API顯示。 成功完成構建步驟時，將根據提交哈希儲存生成的成品，並可在後續管道執行中重複使用。

如果包在同一程式中，則跨管道重複使用。 在尋找可重複使用的套件時，AEM會捨棄分支，並在分支之間重新使用成品。

重複使用發生時，系統會以原始執行的結果來有效取代建立和程式碼品質步驟。 建置步驟的記錄檔會列出原本用於建立的成品及執行資訊。

以下是此類日誌輸出的示例。

```shell
The following build artifacts were reused from the prior execution 4 of pipeline 1 which used commit f6ac5e6943ba8bce8804086241ba28bd94909aef:
build/aem-guides-wknd.all-2021.1216.1101633.0000884042.zip (content-package)
build/aem-guides-wknd.dispatcher.cloud-2021.1216.1101633.0000884042.zip (dispatcher-configuration)
```

程式碼品質步驟的記錄將包含類似資訊。

### 範例 {#example-reuse}

#### 範例1 {#example-1}

請考慮您的計畫有兩個開發管道：

* 分支上的管線1 `foo`
* 分支上的管道2 `bar`

兩個分支都在相同的提交ID上。

1. 先執行Pipeline 1將可正常建置套件。
1. 然後，運行管道2將重複使用管道1建立的包。

#### 範例2 {#example-2}

假設您的計畫有兩個分支：

* 分支 `foo`
* 分支 `bar`

兩個分支都具有相同的提交ID。

1. 開發管道建置及執行 `foo`.
1. 隨後，生產管線建置並執行 `bar`.

在這個例子裡，藏物 `foo` 會由於識別了相同的commit雜湊，而重新用於生產管道。

### 選擇退出 {#opting-out}

如果需要，可通過設定管道變數來禁用特定管道的重用行為 `CM_DISABLE_BUILD_REUSE` to `true`. 如果設定了此變數，仍會提取提交哈希，並儲存生成的對象以供以後使用，但以前儲存的任何對象將不會重複使用。 若要了解此行為，請考量下列案例。

1. 建立新管道。
1. 管道會執行(執行#1)，而目前的HEAD提交為 `becdddb`. 執行成功，並儲存產生的成品。
1. 此 `CM_DISABLE_BUILD_REUSE` 變數。
1. 管道會重新執行，而不會變更程式碼。 儘管儲存的對象與 `becdddb`，則由於 `CM_DISABLE_BUILD_REUSE` 變數。
1. 程式碼會變更並執行管道。 HEAD提交現在為 `f6ac5e6`. 執行成功，並儲存產生的成品。
1. 此 `CM_DISABLE_BUILD_REUSE` 變數。
1. 管道會重新執行，而不會變更程式碼。 因為儲存的對象與 `f6ac5e6`，則這些成品會被重複使用。

### 警告 {#caveats}

* 無論提交哈希是否相同，生成對象都不會跨不同的程式重複使用。
* 即使分支和/或管線不同，建置成品也會在相同程式內重複使用。
* [Maven版本處理](/help/implementing/cloud-manager/managing-code/project-version-handling.md) 僅在生產管道中取代專案版本。 因此，如果開發部署執行和生產管道執行都使用相同的提交，並且首先執行開發部署管道，則版本將部署到預備和生產，而不會更改。 不過，在此情況下仍會建立標籤。
* 如果檢索所儲存的對象不成功，則執行生成步驟，就像沒有儲存對象一樣。
* 管道變數(非 `CM_DISABLE_BUILD_REUSE` 當Cloud manager決定重複使用先前建立的組建成品時，不會考慮使用。
