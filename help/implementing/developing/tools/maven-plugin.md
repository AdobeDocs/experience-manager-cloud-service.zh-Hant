---
title: Adobe Content Package Maven Plugin
description: 使用Content Package Maven增效模組來部署AEM應用程式
translation-type: tm+mt
source-git-commit: 2cdbbe9b8f6608cbdd299889be515d421e3d9ad3
workflow-type: tm+mt
source-wordcount: '1857'
ht-degree: 5%

---


# Adobe Content Package Maven Plugin {#adobe-content-package-maven-plugin}

使用Adobe Content Package Maven增效模組，將套件部署與管理工作整合至您的Maven專案。

將已建構的封裝部署至AEM是由Adobe Content Package Maven增效模組執行，並可自動執行通常使用AEM Package Manager執行的工作：

* 從檔案系統中的檔案建立新包。
* 在AEM上安裝和解除安裝套件。
* 建立已在AEM上定義的套件。
* 取得AEM上安裝的套件清單。
* 從AEM移除套件。

本檔案詳細說明如何使用Maven來管理這些工作。 但是，請務必瞭解[AEM專案及其套件的結構。](#aem-project-structure)

>[!NOTE]
>
>軟體包建立現在由[Apache Jackrabbit FileVault Package Maven plugin](https://jackrabbit.apache.org/filevault-package-maven-plugin/)擁有。 將已建構的封裝部署至AEM是由Adobe Content Package Maven外掛程式執行，如此處所述。

## 套件和AEM Project Structure {#aem-project-structure}

AEM 6.5遵循封裝管理和專案結構的最新最佳實務，由最新的AEM Project Archetype實作，適用於內部和AMS實作。

>[!TIP]
>
>如需詳細資訊，請參閱AEM中的[AEM Project Structure](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)文章，作為雲端服務檔案，以及[AEM Project Archetype](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/overview.html)檔案。 這兩者都完全支援AEM 6.5。

## 取得Content Package Maven Plugin {#obtaining-the-content-package-maven-plugin}

插件可從[Maven Central Repository獲得。](https://mvnrepository.com/artifact/com.day.jcr.vault/content-package-maven-plugin?repo=adobe-public)

## Content Package Maven外掛程式目標與參數

要使用Content Package Maven Plugin，請在POM檔案的構建元素中添加以下插件元素：

```xml
<plugin>
 <groupId>com.day.jcr.vault</groupId>
 <artifactId>content-package-maven-plugin</artifactId>
 <version>0.0.24</version>
 <configuration>
       <!-- parameters and values common to all goals, as required -->
 </configuration>
</plugin>
```

若要啟用Maven下載外掛程式，請使用本頁的[取得內容封裝Maven外掛程式](#obtaining-the-content-package-maven-plugin)區段中提供的描述檔。

## Content Package Maven Plugin {#goals-of-the-content-package-maven-plugin}的目標

「內容套件」外掛程式提供的目標和目標參數在後面的章節中有說明。 「常用參數」(Common Parameters)部分中描述的參數可用於大多數目標。 適用於一個目標的參數在該目標的一節中有說明。

### 外掛程式首碼{#plugin-prefix}

外掛程式首碼為`content-package`。 使用此前置詞從命令行執行目標，如下例所示：

```shell
mvn content-package:build
```

### 參數前置詞{#parameter-prefix}

除非另有說明，否則外掛程式目標和參數會使用`vault`首碼，如下列範例所示：

```shell
mvn content-package:install -Dvault.targetURL="https://192.168.1.100:4502/crx/packmgr/service.jsp"
```

### Proxy {#proxies}

使用AEM之Proxy的目標會使用Maven設定中找到的第一個有效的Proxy設定。 如果未找到代理配置，則不使用代理。 請參閱[Common Parameters](#common-parameters)部分中的`useProxy`參數。

### 常見參數{#common-parameters}

下表中的參數是所有目標的通用參數，但&#x200B;**Goals**&#x200B;欄中注明的除外。

| 名稱 | 類型 | 必要 | 預設值 | 說明 | 目標 |
|---|---|---|---|---|---|
| `failOnError` | `boolean` | 否 | `false` | 值`true`會在發生錯誤時導致組建失敗。 值`false`會使構建版本忽略錯誤。 | 除`package`以外的所有目標 |
| `name` | `String` | `build`:是的，  `install`:不，  `rm`:是 | `build`:無預設值，  `install`:Maven項目 `artifactId` 的屬性 | 要執行操作的包的名稱 | 除`ls`以外的所有目標 |
| `password` | `String` | 是 | `admin` | 用於AEM驗證的密碼 | 除`package`以外的所有目標 |
| `serverId` | `String` | 否 | 要從中檢索用戶名和口令以進行驗證的伺服器ID | 除`package`以外的所有目標 |
| `targetURL` | `String` | 是 | `http://localhost:4502/crx/packmgr/service.jsp` | AEM套件管理員的HTTP服務API URL | 除`package`以外的所有目標 |
| `timeout` | `int` | 否 | `5` | 與包管理器服務通信的連接超時（以秒為單位） | 除`package`以外的所有目標 |
| `useProxy` | `boolean` | 否 | `true` | 值`true`使Maven使用找到的第一個活動代理配置，以便將請求代理到包管理器。 | 除`package`以外的所有目標 |
| `userId` | `String` | 是 | `admin` | 要向AEM驗證的使用者名稱 | 除`package`以外的所有目標 |
| `verbose` | `boolean` | 否 | `false` | 啟用或停用詳細記錄 | 除`package`以外的所有目標 |

### 組建{#build}

建立已在AEM例項上定義的內容套件。

>[!NOTE]
>
>此目標不需要在Maven專案中執行。

#### 參數 {#parameters}

[常見參數](#common-parameters)部分介紹了構建目標的所有參數。

### 安裝{#install}

在儲存庫中安裝軟體包。 執行此目標不需要Maven項目。 目標綁定到Maven構建生命週期的`install`階段。

#### 參數 {#parameters-1}

除了下列參數外，請參閱[Common Parameters](#common-parameters)部分中的說明。

| 名稱 | 類型 | 必要 | 預設值 | 說明 |
|---|---|---|---|---|---|
| `artifact` | `String` | 否 | Maven項目的`artifactId`屬性的值 | `groupId:artifactId:version[:packaging]`格式的字串 |
| `artifactId` | `String` | 否 | 無 | 要安裝的對象的ID |
| `groupId` | `String` | 否 | 無 | 要安裝的對象的`groupId` |
| `install` | `boolean` | 否 | `true` | 確定是否在上載包時自動解壓縮包 |
| `localRepository` | `org.apache.maven.artifact.repository.ArtifactRepository` | 否 | `localRepository`系統變數的值 | 始終使用無法使用插件配置作為系統屬性配置的本地Maven儲存庫 |
| `packageFile` | `java.io.File` | 否 | 為Maven項目定義的主對象 | 要安裝的軟體包檔案的名稱 |
| `packaging` | `String` | 否 | `zip` | 要安裝的對象的封裝類型 |
| `pomRemoteRepositories` | `java.util.List` | 是 | 為Maven項目定義的`remoteArtifactRepositories`屬性的值 | 此值不能使用插件配置進行配置，必須在項目中指定。 |
| `project` | `org.apache.maven.project.MavenProject` | 是 | 為其配置插件的項目 | 由於專案包含外掛程式組態，所以隱含的Maven專案 |
| `repositoryId` (POM)、 `repoID` （命令行） | `String` | 否 | `temp` | 從中檢索對象的儲存庫的ID |
| `repositoryUrl` (POM)、 `repoURL` （命令行） | `String` | 否 | 無 | 從中檢索對象的儲存庫的URL |
| 版本 | 字串 | 否 | 無 | 要安裝的對象的版本 |

### ls {#ls}

列出部署到包管理器的包。

#### 參數 {#parameters-2}

[公共參數](#common-parameters)部分介紹了ls目標的所有參數。

### rm {#rm}

從包管理器中刪除包。

#### 參數 {#parameters-3}

[公共參數](#common-parameters)部分介紹了rm目標的所有參數。

### 卸載{#uninstall}

卸載軟體包。 該軟體包仍處於卸載狀態。

#### 參數 {#parameters-4}

卸載目標的所有參數都在[Common Parameters](#common-parameters)部分中介紹。

### package {#package}

建立內容套件。 軟體包目標的預設配置包括保存已編譯檔案的目錄的內容。 執行軟體包目標需要編譯構建階段完成。 軟體包目標綁定到Maven構建生命週期的軟體包階段。

#### 參數 {#parameters-5}

除了下列參數外，請參閱[公共參數](#common-parameters)部分中`name`參數的說明。

| 名稱 | 類型 | 必要 | 預設值 | 說明 |
|---|---|---|---|---|
| `archive` | `org.apache.maven.archiver.MavenArchiveConfiguration` | 否 | 無 | 要使用的存檔配置 |
| `builtContentDirectory` | `java.io.File` | 是 | Maven組建的輸出目錄的值 | 包含要包含在包中的內容的目錄 |
| `dependencies` | `java.util.List` | 否 | 無 |  |
| `embeddedTarget` | `java.lang.String` | 否 | 無 |  |
| `embeddeds` | `java.util.List` | 否 | 無 |  |
| `failOnMissingEmbed` | `boolean` | 是 | `false` | 如果值`true`，當在項目相關性中找不到嵌入對象時，會導致構建失敗。 值`false`會使構建版本忽略這些錯誤。 |
| `filterSource` | `java.io.File` | 否 | 無 | 此參數定義一個指定工作區過濾器源的檔案。 在配置中指定並通過嵌入式或子包插入的過濾器與檔案內容合併。 |
| `filters` | `com.day.jcr.vault.maven.pack.impl.DefaultWorkspaceFilter` | 否 | 無 | 此參數包含定義套件內容的篩選元素。 執行時，篩選器會包含在`filter.xml`檔案中。 請參閱下面的[使用過濾器](#using-filters)一節。 |
| `finalName` | `java.lang.String` | 是 | Maven項目（構建階段）中定義的`finalName` | 生成的包ZIP檔案的名稱，沒有`.zip`檔案副檔名 |
| `group` | `java.lang.String` | 是 | Maven項目中定義的`groupID` | 作為內容包目標安裝路徑一部分的生成內容包的`groupId` |
| `outputDirectory` | `java.io.File` | 是 | Maven項目中定義的構建目錄 | 保存內容包的本地目錄 |
| `prefix` | `java.lang.String` | 否 | 無 |  |
| `project` | `org.apache.maven.project.MavenProject` | 是 | 無 | Maven專案 |
| `properties` | `java.util.Map` | 否 | 無 | 這些參數定義了可在`properties.xml`檔案中設定的其他屬性。 這些屬性無法覆寫下列預先定義的屬性：`group`（使用`group`參數來設定）、`name`（使用`name`參數來設定）、`version`（使用`version`參數來設定）、`description`（從專案說明設定）、`groupId`（Maven專案描述符的`groupId`）、`artifactId`（`artifactId`Maven項目描述符）、`dependencies`（使用`dependencies`參數來設定）、`createdBy`（`user.name`系統屬性的值）、`created`（當前系統時間）、`requiresRoot`（使用`requiresRoot`參數來設定）、`packagePath`（自動從組和包名稱生成） |
| `requiresRoot` | `boolean` | 是 | false | 定義軟體包是否需要root。 這會成為`properties.xml`檔案的`requiresRoot`屬性。 |
| `subPackages` | `java.util.List` | 否 | 無 |  |
| `version` | `java.lang.String` | 是 | Maven專案中定義的版本 | 內容套件的版本 |
| `workDirectory` | `java.io.File` | 是 | Maven項目中定義的目錄（構建階段） | 包含要包含在包中的內容的目錄 |

#### 使用篩選器{#using-filters}

使用篩選元素來定義套件內容。 這些篩選器將添加到包`META-INF/vault/filter.xml`檔案中的`workspaceFilter`元素。

以下篩選器示例顯示要使用的XML結構：

```xml
<filter>
   <root>/apps/myapp</root>
   <mode>merge</mode>
       <includes>
              <include>/apps/myapp/install/</include>
              <include>/apps/myapp/components</include>
       </includes>
       <excludes>
              <exclude>/apps/myapp/config/*</exclude>
       </excludes>
</filter>
```

##### 匯入模式 {#import-mode}

`mode`元素定義導入包時對儲存庫內容的影響。 可使用下列值：

* **合併：** 添加包中尚未在儲存庫中的內容。包和儲存庫中的內容保持不變。 系統不會從儲存庫中刪除任何內容。
* **Replace：不** 在儲存庫中的包中的內容將添加到儲存庫。儲存庫中的內容將替換為包中的匹配內容。 當內容不存在於包中時，內容將從儲存庫中刪除。
* **更新：不** 在儲存庫中的包中的內容將添加到儲存庫中。儲存庫中的內容將替換為包中的匹配內容。 現有內容從儲存庫中刪除。

當篩選器不含`mode`元素時，會使用預設值`replace`。

### 說明 {#help}

#### 參數 {#parameters-6}

| 名稱 | 類型 | 必要 | 預設值 | 說明 |
|---|---|---|---|---|
| `detail` | `boolean` | 否 | `false` | 確定是否顯示每個目標的所有可設定屬性 |
| `goal` | `String` | 否 | 無 | 此參數定義要顯示幫助的目標名稱。 如果未指定任何值，則會顯示所有目標的說明。 |
| `indentSize` | `int` | 否 | `2` | 用於每個級別縮排的空格數（如果已定義，則必須為正） |
| `lineLength` | `int` | 否 | `80` | 顯示線的最大長度（如果已定義，則必須為正） |

## 在包{#including-a-thumbnail-image-or-properties-file-in-the-package}中包括縮圖影像或屬性檔案

替換預設包配置檔案以自定義包屬性。 例如，在「套件管理員」和「套件共用」中加入縮圖影像以區分套件。

源檔案可以位於檔案系統中的任意位置。 在POM檔案中，定義構建資源，將源檔案複製到`target/vault-work/META-INF`中，以便包含在包中。

以下POM代碼將項目源的`META-INF`資料夾中的檔案添加到包中：

```xml
<build>
    <resources>
        <!-- vault META-INF resources (thumbnail etc.) -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF</directory>
            <targetPath>../vault-work/META-INF</targetPath>
        </resource>
    </resources>
</build>
```

以下POM代碼僅將縮圖影像添加到包中。 縮圖影像必須命名為`thumbnail.png`，且必須位於套件的`META-INF/vault/definition`資料夾中。 在此示例中，源檔案位於項目的`/src/main/content/META-INF/vault/definition`資料夾中：

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

## 使用AEM Project Archetype產生AEM Projects {#using-archetypes}

最新的AEM Project Archetype會針對內部實作和AMS實作實作實作最佳實作套件結構，而且建議用於所有AEM專案。

>[!TIP]
>
>如需詳細資訊，請參閱AEM中的[AEM Project Structure](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)文章，作為雲端服務檔案，以及[AEM Project Archetype](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/overview.html)檔案。 這兩者都完全支援AEM 6.5。
