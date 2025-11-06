---
title: 專案設定
description: 瞭解如何使用Maven構建AEM專案，以及在建立自己的專案時必須遵守的標準。
exl-id: 76af0171-8ed5-4fc7-b5d5-7da5a1a06fa8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1395'
ht-degree: 68%

---

# 專案設定 {#project-setup}

瞭解如何使用Maven構建AEM專案，以及在建立自己的專案時必須遵守的標準。

## 專案設定詳細資料 {#project-setup-details}

AEM專案若要使用Cloud Manager成功建置和部署，必須遵守下列准則：

* 必須使用[Apache Maven](https://maven.apache.org)建置專案。
* 在 Git 存放庫的根目錄中必須有一個 `pom.xml` 檔案。如有必要，此 `pom.xml` 檔案可參照的子模組 (這些子模組又可能有其他子模組等) 數量並無限制。
* 您可以在`pom.xml`檔案中新增對其他Maven成品存放庫的參照。 設定後，可支援對[受密碼保護的成品存放庫](#password-protected-maven-repositories)的存取權。但是，不支援對受網路保護的成品存放庫的存取權。
* 透過掃描在名為`.zip`的目錄中所包含的內容套件`target`檔案來探索可部署的內容套件。 任何數量的子模組都可產生內容套件。
* 透過掃描`.zip`個檔案（也包含在名為`target`的目錄中）探索可部署的Dispatcher成品，這些檔案包含名為`conf`和`conf.d`的目錄。
* 如果有超過一個內容套件，則不保證套件部署的順序。 如果需要特定的順序，可以使用內容套件相依性來定義順序。
* 部署時可能會[略過](#skipping-content-packages)套件。

## 在Cloud Manager中啟動Maven設定檔 {#activating-maven-profiles-in-cloud-manager}

在某些有限的情況下，當您在 Cloud Manager 中執行而不是在開發人員工作站上執行時，可能需要稍微改變建置流程。對於這些情況，[Maven 設定檔](https://maven.apache.org/guides/introduction/introduction-to-profiles.html)可用於定義組建在不同環境中應如何不同，包括 Cloud Manager。

在 Cloud Manager 組建環境內啟動 Maven 設定檔應透過尋求 `CM_BUILD` [環境變數](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)來完成。同樣地，僅供在 Cloud Manager 組建環境之外使用的設定檔應透過尋求不存在此變數來完成。

例如，若您只想在 Cloud Manager 內部執行建置時輸出一則簡單的訊息，您可以採取以下步驟：

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
>若要在開發人員工作站上測試此設定檔，您可在命令列 (包含 `-PcmBuild`) 上或在您的整合式開發環境 (IDE) 中將其啟用。

而若您只想在 Cloud Manager 以外執行建置時輸出一則簡單的訊息，您可以採取以下步驟：

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

## 在Cloud Manager中使用受密碼保護的Maven存放庫 {#password-protected-maven-repositories}

>[!NOTE]
>
>從受密碼保護的Maven存放庫謹慎部署成品，因為Cloud Manager不會使用其[程式碼品質規則](/help/implementing/cloud-manager/custom-code-quality-rules.md)評估此程式碼。 此方法應在極少數情況下保留，並僅套用至與AEM無關的程式碼。 Adobe建議同時包含Java原始程式碼和整個專案的原始程式碼以及二進位。 這麼做可確保整個部署流程更透明、更易於維護。

**若要在Cloud Manager中使用受密碼保護的Maven存放庫：**

1. 將密碼 (以及可選的使用者名) 指定為機密[管道變數](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)。
1. 然後在一個名為`.cloudmanager/maven/settings.xml`在 git 存放庫中，它遵循[Maven 設定檔案](https://maven.apache.org/settings.html)結構。

當 Cloud Manager 建置過程開始時：

* 此檔案中的 `<servers>` 元素合併至由 Cloud Manager 提供的預設 `settings.xml` 檔案中。
   * 以`adobe`和`cloud-manager`開頭的伺服器ID視為保留的。 請勿在自訂伺服器上使用它們。
   * Cloud Manager只會映象符合特定首碼或預設ID `central`的伺服器ID；所有其他伺服器ID將不會進行映象。
* 備妥這個檔案後，將從 `<repository>` 內部和/或 `<pluginRepository>` 元素 (在 `pom.xml` 檔案內) 參照伺服器 ID。
* 一般而言，這`<repository>`和`<pluginRepository>`個元素包含在[Cloud Manager專屬的設定檔](#activating-maven-profiles-in-cloud-manager)中，不過這些元素並非絕對必要。

舉例來說，我們假設存放庫位於 `https://repository.myco.com/maven2`，則 Cloud Manager 應使用的使用者名稱為 `cloudmanager`，而密碼為 `secretword`。您將採取以下步驟：

1. 在管道上將密碼設為秘密。

   ```text
   $ aio cloudmanager:set-pipeline-variables PIPELINEID --secret CUSTOM_MYCO_REPOSITORY_PASSWORD secretword`
   ```

1. 從下列`.cloudmanager/maven/settings.xml`檔案中參照此密碼：

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

1. 最後需在 `pom.xml` 檔案內參照伺服器 ID：

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

### 部署原始程式碼 {#deploying-sources}

同時部署 Java 原始程式碼以及二進位至 Maven 存放庫是建議的做法。

若要這麼做，請在您的專案中設定maven-source-plugin。

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

### 部署專案原始程式碼 {#deploying-project-sources}

同時部署整個專案的原始程式碼以及二進位至 Maven 存放庫是建議的做法。 如此可讓您重建精確的成品。

以下列方式在您的專案中設定maven-assembly-plugin：

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

## 略過內容套件 {#skipping-content-packages}

在 Cloud Manager 中，組建可能會產生任何數量的內容套件。由於各種原因，可能需要產生內容套件但不將其部署。例如，內容套件僅為了測試目的而建置，或建置流程中的另一個步驟重新封裝它們。 也就是另一個套件的子套件。

為了適應這些情況，Cloud Manager 會在內建內容套件的屬性中查找名為 `cloudManagerTarget` 的屬性。如果此屬性設定為 `none`，則會跳過該套件且不部署。

設定此屬性的機制取決於建立內容封裝的方式。例如，使用時，您可以像這樣設定外掛程式：`filevault-maven-plugin`

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

這`content-package-maven-plugin`有類似的配置。

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

## 組建成品重複使用 {#build-artifact-reuse}

在許多情況下，會將相同的程式碼部署到多個 AEM 環境中。在可能的情況下，當 Cloud Manager 偵測到於多個全端管道執行中都使用相同的 Git 認可時，會避免重新建置程式碼庫。

開始執行時，將擷取分支管道的最新 HEAD 認可。在 UI 中以及透過 API 看得見該認可雜湊。當建置步驟成功完成時，所產生的成品將根據該認可雜湊進行儲存，並可能在後續管道執行中重複使用。

如果套件在同一個計畫中，可跨管道重複使用。在尋找可重複使用的套件時，AEM 會忽略分支並且會跨分支重複使用成品。

當發生重複使用時，將以原始執行的結果有效地取代建置和程式碼品質步驟。建置步驟的記錄檔列出成品以及最初用於建置這些成品的執行資訊。

以下是這類記錄輸出的範例。

```shell
The following build artifacts were reused from the prior execution 4 of pipeline 1 which used commit f6ac5e6943ba8bce8804086241ba28bd94909aef:
build/aem-guides-wknd.all-2021.1216.1101633.0000884042.zip (content-package)
build/aem-guides-wknd.dispatcher.cloud-2021.1216.1101633.0000884042.zip (dispatcher-configuration)
```

程式碼品質步驟的記錄包含類似的資訊。

### 範例 {#example-reuse}

#### 範例 1 {#example-1}

假定您的計畫有兩個開發管道：

* 管道 1 在分支 `foo` 上
* 管道 2 在分支 `bar` 上

兩個分支都在相同的認可 ID 上。

1. 執行管道1會先正常建置套件。
1. 然後，執行管道2會重複使用管道1建立的套件。

#### 範例 2 {#example-2}

假定您的計畫有兩個分支：

* 分支 `foo`
* 分支 `bar`

兩個分支的認可 ID 相同。

1. 會建置開發管道並執行 `foo`。
1. 隨後，生產管道會建置並執行 `bar`。

在這種情況下，由於識別出相同的認可雜湊，會將來自 `foo` 的成品重複用於生產管道。

### 退出 {#opting-out}

如有需要，可透過將管道變數 `CM_DISABLE_BUILD_REUSE` 設定為 `true` 來停用特定管道的重複使用行為。如果設定此變數，系統會擷取認可雜湊並儲存所產生的成品以供稍後使用，但會略過重複使用任何先前儲存的成品。 若要了解此行為，請思考以下情境：

1. 已建立新管道。
1. 執行管道 (執行 #1)，且目前的 HEAD 認可為 `becdddb`。此執行成功完成，並儲存產生的成品。
1. 設定 `CM_DISABLE_BUILD_REUSE` 變數。
1. 在不變更程式碼的情況下重新執行管道。雖然有和 `becdddb` 相關的已儲存成品，但由於 `CM_DISABLE_BUILD_REUSE` 變數，並不會重新使用它們。
1. 會變更程式碼並重新執行管道。該 HEAD 認可現在是 `f6ac5e6`。此執行成功完成，並儲存產生的成品。
1. 已刪除 `CM_DISABLE_BUILD_REUSE` 變數。
1. 在不變更該程式碼的情況下重新執行管道。由於有和 `f6ac5e6` 相關的已儲存成品，因此會重新使用這些成品。

### 警告 {#caveats}

* 無論認可雜湊是否相同，都不會在不同的計畫中重新使用組建成品。
* 即使分支和/或管道不同，在相同計畫中會重新使用組建成品。
* [Maven版本處理](/help/implementing/cloud-manager/managing-code/project-version-handling.md)只有在生產管道中才會取代專案版本。
如果相同的認可同時用於開發部署和生產管道，且開發部署會先執行，則版本會部署到中繼和生產環境且不會變更。 但在這種情況下，仍會建立標記。
* 如果無法擷取已儲存的成品，則會執行建置步驟，就像未儲存任何成品一樣。
* 當 Cloud Manager 決定重複使用之前建立的建置成品時，不會考慮 `CM_DISABLE_BUILD_REUSE` 以外的管道變數。
