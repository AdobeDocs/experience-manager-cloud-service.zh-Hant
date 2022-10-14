---
title: 專案設定
description: 了解如何使用 Maven 構建 AEM 項目，以及在建立自己的項目時必須遵守的標準。
exl-id: 76af0171-8ed5-4fc7-b5d5-7da5a1a06fa8
source-git-commit: 430179bf13c1fff077c515eed0676430e9e7f341
workflow-type: tm+mt
source-wordcount: '1415'
ht-degree: 100%

---

# 專案設定 {#project-setup}

了解如何使用 Maven 構建 AEM 項目，以及在建立自己的項目時必須遵守的標準。

## 專案設定詳細資料 {#project-setup-details}

為了使用 Cloud Manager 成功構建和部署，AEM 項目需要遵循以下準則：

* 必須使用 [Apache Maven](https://maven.apache.org) 建置專案。
* 在 Git 存放庫的根目錄中必須有一個 `pom.xml` 檔案。如有必要，此 `pom.xml` 檔案可參照的子模組 (這些子模組又可能有其他子模組) 數量並無限制。視需求。
* 您可在您的 `pom.xml` 檔案中新增對其他 Maven 成品存放庫的參照。
   * 設定後，可支援對[受密碼保護的成品存放庫](#password-protected-maven-repositories)的存取權。但是，不支援對受網路保護的成品存放庫的存取權。
* 透過掃描在名為 `target` 的目錄中所包含的內容套件 `.zip` 檔案來探索可部署的內容套件。
   * 任何數量的子模組都可產生內容套件。
* 透過掃描`.zip`檔案 (也包含在名為名為 `target`) `conf` 和 `conf.d`) 探索可部署 Dispatcher 成品。
* 如果有超過一個內容套件，則不保證套件部署的排序。
   * 如果需要特定的順序，可以使用內容套件相依性來定義順序。
* 部署時可能會[略過](#skipping-content-packages)套件。

## 在 Cloud Manager 中啟動 Maven 設定檔 {#activating-maven-profiles-in-cloud-manager}

在某些有限的情況下，當您在 Cloud Manager 中執行而不是在開發人員工作站上執行時，可能需要稍微改變建置流程。對於這些情況，[Maven 設定檔](https://maven.apache.org/guides/introduction/introduction-to-profiles.html)可用於定義組建在不同環境中應如何不同，包括 Cloud Manager。

在 Cloud Manager 組件環境內啟動 Maven 設定檔應透過尋求`CM_BUILD`[環境變數來完成。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)同樣地，僅供在 Cloud Manager 組建環境之外使用的設定檔應透過尋求不存在此變數來完成。

例如，如果您只想在 Cloud Manager 內部執行組建時輸出一則簡單的訊息，您可以採取以下步驟。

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

而如果您只想在 Cloud Manager 以外執行組建時輸出一則簡單的訊息，您可以採取以下步驟。

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

## 密碼保護的 Maven 存放庫支援 {#password-protected-maven-repositories}

>[!NOTE]
>
>對於來自受密碼保護的 Maven 存放庫的成品，應極為謹慎地使用，因為透過此機制部署的計劃碼不會透過 Cloud Manager 品質閘道中實作的所有[計劃碼品質規則](/help/implementing/cloud-manager/custom-code-quality-rules.md)。因此，它只應在極少數情況下用於不與 AEM 綁定的計劃碼。建議同時部署 Java 原始計劃碼以及整個專案的原始計劃碼還有二進位。

為了在 Cloud Manager 中使用受密碼保護的 Maven 存放庫：

1. 將密碼 (以及可選的使用者名) 指定為機密[管道變數。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)
1. 然後在一個名為`.cloudmanager/maven/settings.xml`在 git 存放庫中，它遵循[Maven 設定檔案](https://maven.apache.org/settings.html)架構。

當 Cloud Manager 建置過程開始時：

* `<servers>` 元素合併至由 Cloud Manager 提供的預設 `settings.xml` 檔案中。
   * 以 `adobe` 和 `cloud-manager` 開頭的伺服器 ID 會視為是保留的，不應由自訂伺服器使用。
   * Cloud Manager 對於和這些首碼中的任何一個或預設 ID `central` 都不相符的伺服器 ID 將無法進行鏡像。
* 備妥這個檔案後，將從 `<repository>` 內部和/或 `<pluginRepository>` 元素 (在 `pom.xml` 檔案內) 參照伺服器 ID。
* 一般來說，這些 `<repository>` 和/或 `<pluginRepository>` 元素將包含在 [Cloud Manager 的特定設定檔](#activating-maven-profiles-in-cloud-manager)內，不過這並非絕對必要。

舉例來說，我們假設存放庫位於 `https://repository.myco.com/maven2`，則 Cloud Manager 應使用的使用者名稱為 `cloudmanager`，而密碼為 `secretword`。您將採取以下步驟。

1. 在管道上將密碼設為秘密。

   ```text
   $ aio cloudmanager:set-pipeline-variables PIPELINEID --secret CUSTOM_MYCO_REPOSITORY_PASSWORD secretword`
   ```

1. 從 `.cloudmanager/maven/settings.xml` 檔案對其參照。

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

### 部署原始計劃碼 {#deploying-sources}

同時部署 Java 原始計劃碼以及二進位至 Maven 存放庫是建議的做法。

為此，請在項目中配置 maven-source-plugin。

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

### 部署專案原始計劃碼 {#deploying-project-sources}

同時部署整個專案的原始計劃碼以及二進位至 Maven 存放庫是建議的做法。 這允許重建精確的成品。

為此，請在項目中配置 maven-assembly-plugin。

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

在 Cloud Manager 中，組建可能會產生任何數量的內容套件。 由於各種原因，可能需要產生內容套件但不將其部署。一個例子可能是當建置僅用於測試的內容套件或將由建置流程中的另一個步驟重新封裝的內容套件時 (即成為另一個套件的子套件)。

為了適應這些情況，Cloud manager將在內建內容包的屬性中查找名為 `cloudManagerTarget` 的屬性。如果此屬性設定為 `none`，則會略過該套件且不部署。

設定此屬性的機制取決於建立內容封裝的方式。例如，使用時，您可以像這樣設定外掛計劃：`filevault-maven-plugin`

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

在許多情況下，會將相同的計劃碼部署到多個 AEM 環境中。在可能的情況下，當 Cloud Manager 偵測到在多個全堆疊管道執行中都使用了相同的 Git 認可時，即會避免重新建置計劃碼庫。

開始執行時，將擷取分支管道的最新 HEAD 認可。在 UI 中以及透過 API 看得見該認可雜湊。當建置步驟成功完成時，所產生的成品將根據該認可雜湊進行儲存，並可能在後續管道執行中重複使用。

如果套件在同一個方案中，可跨管道重複使用。在尋找可重複使用的套件時，AEM 會忽略分支並且會跨分支重複使用成品。

當發生重複使用時，將以原始執行的結果有效地取代建置和計劃碼品質步驟。建置步驟的紀錄檔將包含成品以及最初用於建置這些成品的執行資訊的清單。

以下是這類紀錄輸出的範例。

```shell
The following build artifacts were reused from the prior execution 4 of pipeline 1 which used commit f6ac5e6943ba8bce8804086241ba28bd94909aef:
build/aem-guides-wknd.all-2021.1216.1101633.0000884042.zip (content-package)
build/aem-guides-wknd.dispatcher.cloud-2021.1216.1101633.0000884042.zip (dispatcher-configuration)
```

計劃碼品質步驟的紀錄將包含類似的資訊。

### 範例 {#example-reuse}

#### 範例 1 {#example-1}

假定您的方案有兩個開發管道：

* 管道 1 在分支 `foo` 上
* 管道 2 在分支 `bar` 上

兩個分支都在相同的認可 ID 上。

1. 先執行管道 1 通常將建置套件。
1. 接著執行管道 2 將重複使用管道 1 建立的套件。

#### 範例 2 {#example-2}

假定您的方案有兩個分支：

* 分支 `foo`
* 分支 `bar`

兩個分支的認可 ID 相同。

1. 會建置開發管道並執行 `foo`。
1. 隨後會建置生產管道並執行 `bar`。

在這種情況下，由於識別出相同的認可雜湊，會將來自 `foo` 的成品重複用於生產管道。

### 退出 {#opting-out}

如有需要，可透過將管道變數 `CM_DISABLE_BUILD_REUSE` 設定為 `true` 來停用特定管道的重複使用行為。 如果設定此變數，則仍會擷取認可雜湊，並將儲存所產生的成品以供稍後使用，但不會重複使用之前儲存的任何成品。若要了解此行為，請思考以下案例。

1. 已建立新管道。
1. 執行管道 (執行 #1)，且目前的 HEAD 認可為 `becdddb`。此執行成功完成，並儲存產生的成品。
1. 設定 `CM_DISABLE_BUILD_REUSE` 變數。
1. 在不變更計劃碼的情況下重新執行管道。雖然有和 `becdddb` 相關的已儲存成品，但由於 `CM_DISABLE_BUILD_REUSE` 變數，並不會重新使用它們。
1. 會變更計劃碼並重新執行管道。該 HEAD 認可現在是 `f6ac5e6`。此執行成功完成，並儲存產生的成品。
1. 已刪除 `CM_DISABLE_BUILD_REUSE` 變數。
1. 在不變更該計劃碼的情況下重新執行管道。由於有和 `f6ac5e6` 相關的已儲存成品，因此會重新使用這些成品。

### 警告 {#caveats}

* 無論認可雜湊是否相同，都不會在不同的方案中重新使用組建成品。
* 即使分支和/或管道不同，在相同方案中會重新使用組建成品。
* [Maven 版本處理](/help/implementing/cloud-manager/managing-code/project-version-handling.md)只有在生產管道中才會取代專案版本。因此，如果在開發部署執行和生產管道執行上都使用相同的認可，並且先執行開發部署管道，則會在不變更版本的情況下將版本部署到中繼和生產環境。但在這種情況下，仍將會建立標記。
* 如果未成功擷取已儲存的成品，則將執行建置步驟，彷彿尚未儲存任何成品一樣。
* 當 Cloud Manager 決定重新使用之前已建立的組件成品時，不會考慮 `CM_DISABLE_BUILD_REUSE` 以外的管道變數。
