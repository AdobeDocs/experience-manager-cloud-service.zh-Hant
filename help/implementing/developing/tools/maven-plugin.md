---
title: Adobe Content Package Maven增效模組
description: 使用Content Package Maven外掛程式來部署AEM應用程式
exl-id: d631d6df-7507-4752-862b-9094af9759a0
feature: Developing
role: Admin, Developer
source-git-commit: 2e257634313d3097db770211fe635b348ffb36cf
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 4%

---

# Adobe Content Package Maven增效模組 {#adobe-content-package-maven-plugin}

使用Adobe Content Package Maven外掛程式，將套件部署和管理工作整合到您的Maven專案中。

將建構的套件部署至AEM是由Adobe Content Package Maven外掛程式執行，並可讓通常使用AEM [封裝管理員](/help/implementing/developing/tools/package-manager.md)執行的工作自動化

* 從檔案系統中的檔案建立新封裝。
* 在AEM上安裝及解除安裝套件。
* 建置已在AEM上定義的套件。
* 取得安裝在AEM上的套件清單。
* 從AEM移除套件。

本檔案詳細說明如何使用Maven管理這些任務。 不過，瞭解[AEM專案及其套件的結構也很重要](#aem-project-structure)。

>[!NOTE]
>
>請一律使用這些外掛程式的最新可用版本。

>[!NOTE]
>
>套件&#x200B;**建立**&#x200B;現在由[Apache Jackrabbit FileVault Package Maven外掛程式](https://jackrabbit.apache.org/filevault-package-maven-plugin/)擁有。
>
>本文說明由AEM Content Package Maven外掛程式執行的將建構套件部署至Adobe的&#x200B;**部署**。

## 套件和AEM專案結構 {#aem-project-structure}

AEM as a Cloud Service遵循由最新AEM專案原型實作的套件管理和專案結構的最新最佳實務。

>[!TIP]
>
>請參閱AEM檔案中的[AEM as a Cloud Service專案結構](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=zh-Hant)文章和[AEM專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hant)檔案。 AEM 6.5完全支援這兩項功能。

## 取得內容套件Maven外掛程式 {#obtaining-the-content-package-maven-plugin}

外掛程式可從[Maven中央存放庫](https://mvnrepository.com/artifact/com.day.jcr.vault/content-package-maven-plugin?repo=adobe-public)取得。

## 內容套件Maven外掛程式目標與引數

若要使用Content Package Maven外掛程式，請在POM檔案的組建元素中新增下列外掛程式元素：

```xml
<plugin>
 <groupId>com.day.jcr.vault</groupId>
 <artifactId>content-package-maven-plugin</artifactId>
 <version>1.0.4</version>
 <configuration>
       <!-- parameters and values common to all goals, as required -->
 </configuration>
</plugin>
```

若要讓Maven下載外掛程式，請使用此頁面上[取得內容套件Maven外掛程式](#obtaining-the-content-package-maven-plugin)區段中提供的設定檔。

## 內容套件Maven外掛程式的目標 {#goals-of-the-content-package-maven-plugin}

後續章節將說明「內容套件」外掛程式提供的目標與目標引數。 「一般引數」一節中說明的引數可用於大部分的目標。 套用至一個目標的引數會在該目標的區段進行說明。

### 外掛程式前置詞 {#plugin-prefix}

外掛程式首碼為`content-package`。 使用此首碼從命令列執行目標，如下列範例所示：

```shell
mvn content-package:build
```

### 引數前置詞 {#parameter-prefix}

除非另有說明，否則外掛程式目標和引數會使用`vault`前置詞，如下列範例所示：

```shell
mvn content-package:install -Dvault.targetURL="https://192.168.1.100:4502/crx/packmgr/service.jsp"
```

### 代理 {#proxies}

使用AEM代理的目標會使用Maven設定中找到的第一個有效Proxy設定。 如果未找到Proxy設定，則不會使用Proxy。 檢視`useProxy`通用引數[區段中的](#common-parameters)引數。

### 通用引數 {#common-parameters}

下表中的引數對所有目標都是通用的，除非在&#x200B;**目標**&#x200B;欄中註明。

| 名稱 | 類型 | 必要 | 預設值 | 說明 | 目標 |
|---|---|---|---|---|---|
| `failOnError` | `boolean` | 否 | `false` | 發生錯誤時，`true`的值會導致組建失敗。 值為`false`會導致組建忽略錯誤。 | 除`package`以外的所有目標 |
| `name` | `String` | `build`：是，`install`：否，`rm`：是 | `build`：無預設值，`install`： Maven專案的`artifactId`屬性值 | 要對其採取動作的套件的名稱 | 除`ls`以外的所有目標 |
| `password` | `String` | 是 | `admin` | 用於透過AEM進行驗證的密碼 | 除`package`以外的所有目標 |
| `serverId` | `String` | 否 | 要從中擷取使用者名稱和密碼以進行驗證的伺服器ID | 除`package`以外的所有目標 |  |
| `targetURL` | `String` | 是 | `http://localhost:4502/crx/packmgr/service.jsp` | AEM封裝管理員的HTTP服務API的URL | 除`package`以外的所有目標 |
| `timeout` | `int` | 否 | `5` | 與封裝管理程式服務通訊的連線逾時（以秒為單位） | 除`package`以外的所有目標 |
| `useProxy` | `boolean` | 否 | `true` | 值為`true`會讓Maven使用找到的第一個作用中Proxy設定，將請求代理至封裝管理員。 | 除`package`以外的所有目標 |
| `userId` | `String` | 是 | `admin` | 要向AEM驗證的使用者名稱 | 除`package`以外的所有目標 |
| `verbose` | `boolean` | 否 | `false` | 啟用或停用詳細記錄 | 除`package`以外的所有目標 |

### 版本編號 {#build}

建置已在AEM執行個體上定義的內容套件。

>[!NOTE]
>
>此目標不需要在Maven專案中執行。

#### 參數 {#parameters}

組建目標的所有引數都在[一般引數](#common-parameters)區段中說明。

### 安裝 {#install}

在存放庫中安裝套件。 執行此目標不需要Maven專案。 目標已繫結至Maven組建生命週期的`install`階段。

#### 參數 {#parameters-1}

除了下列引數之外，請參閱[一般引數](#common-parameters)區段中的說明。

| 名稱 | 類型 | 必要 | 預設值 | 說明 |
|---|---|---|---|---|
| `artifact` | `String` | 否 | Maven專案的`artifactId`屬性值 | 字串格式為`groupId:artifactId:version[:packaging]` |
| `artifactId` | `String` | 否 | 無 | 要安裝的成品的ID |
| `groupId` | `String` | 否 | 無 | 要安裝的成品`groupId` |
| `install` | `boolean` | 否 | `true` | 決定是否在上傳封裝時自動將其解壓縮 |
| `localRepository` | `org.apache.maven.artifact.repository.ArtifactRepository` | 否 | `localRepository`系統變數的值 | 無法使用外掛程式設定來設定本機Maven存放庫，因為一律使用系統屬性 |
| `packageFile` | `java.io.File` | 否 | 為Maven專案定義的主要成品 | 要安裝的封裝檔案名稱 |
| `packaging` | `String` | 否 | `zip` | 要安裝的成品封裝型別 |
| `pomRemoteRepositories` | `java.util.List` | 是 | 為Maven專案定義的`remoteArtifactRepositories`屬性值 | 此值無法使用外掛程式設定進行設定，必須在專案中指定。 |
| `project` | `org.apache.maven.project.MavenProject` | 是 | 已設定外掛程式的專案 | 隱含的Maven專案，因為專案包含外掛程式設定 |
| `repositoryId` (POM)， `repoID` （命令列） | `String` | 否 | `temp` | 從中擷取成品的存放庫識別碼 |
| `repositoryUrl` (POM)， `repoURL` （命令列） | `String` | 否 | 無 | 從中擷取成品的存放庫URL |
| 版本 | 字串 | 否 | 無 | 要安裝的成品版本 |

### ls {#ls}

列出部署至[封裝管理員](/help/implementing/developing/tools/package-manager.md)的封裝。

#### 參數 {#parameters-2}

在[一般引數](#common-parameters)區段中說明ls目標的所有引數。

### rm {#rm}

從[封裝管理員](/help/implementing/developing/tools/package-manager.md)移除封裝。

#### 參數 {#parameters-3}

在[一般引數](#common-parameters)區段中說明rm目標的所有引數。

### 解除安裝 {#uninstall}

解除安裝套裝。 套件會留在伺服器上並處於解除安裝狀態。

#### 參數 {#parameters-4}

解除安裝目標的所有引數在[一般引數](#common-parameters)區段中都有說明。


### 說明 {#help}

#### 參數 {#parameters-6}

| 名稱 | 類型 | 必要 | 預設值 | 說明 |
|---|---|---|---|---|
| `detail` | `boolean` | 否 | `false` | 決定是否顯示每個目標的所有可設定屬性 |
| `goal` | `String` | 否 | 無 | 此引數會定義要顯示其說明的目標名稱。 如果未指定任何值，則會顯示所有目標的說明。 |
| `indentSize` | `int` | 否 | `2` | 用於每個層級縮排的空格數（如果已定義，則必須為正數） |
| `lineLength` | `int` | 否 | `80` | 顯示線的最大長度（如果已定義，則必須為正數） |

## 在套件中包含縮圖影像或屬性檔案 {#including-a-thumbnail-image-or-properties-file-in-the-package}

取代預設的封裝組態檔以自訂封裝屬性。 例如，在[封裝管理員](/help/implementing/developing/tools/package-manager.md)中加入縮圖影像以區分封裝。

來源檔案可以位於檔案系統中的任何位置。 在POM檔案中，定義建置資源以將來源檔案複製到`target/vault-work/META-INF`以包含在封裝中。

下列POM程式碼會將專案來源之`META-INF`資料夾中的檔案新增至封裝：

```xml
<build>
    <resources>
        <!-- vault META-INF resources (thumbnail and so on) -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF</directory>
            <targetPath>../vault-work/META-INF</targetPath>
        </resource>
    </resources>
</build>
```

下列POM程式碼僅會將縮圖影像新增至封裝。 縮圖影像必須命名為`thumbnail.png`，且必須位於封裝的`META-INF/vault/definition`資料夾中。 在此範例中，來源檔案位於專案的`/src/main/content/META-INF/vault/definition`資料夾：

```xml
<build>
    <resources>
        <!-- thumbnail only -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF/vault/definition</directory>
            <targetPath>../vault-work/META-INF/vault/definition</targetPath>
        </resource>
    </resources>
</build>
```

## 使用AEM專案原型來產生AEM專案 {#using-archetypes}

最新的AEM專案原型會為內部部署和AMS實作實作實施最佳實務套件結構，並建議用於所有AEM專案。

>[!TIP]
>
>請參閱AEM檔案中的[AEM as a Cloud Service專案結構](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=zh-Hant)文章和[AEM專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hant)檔案。 AEM 6.5完全支援這兩項功能。
