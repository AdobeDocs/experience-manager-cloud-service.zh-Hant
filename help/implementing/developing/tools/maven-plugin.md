---
title: Adobe內容套件Maven外掛程式
description: 使用Content Package Maven外掛程式來部署AEM應用程式
exl-id: d631d6df-7507-4752-862b-9094af9759a0
source-git-commit: ba4e2427873fc9f5d91ee4f520df01018000a4c7
workflow-type: tm+mt
source-wordcount: '1851'
ht-degree: 6%

---

# Adobe內容套件Maven外掛程式 {#adobe-content-package-maven-plugin}

使用Adobe內容套件Maven外掛程式，將套件部署和管理工作整合至您的Maven專案。

將已建構的套件部署至AEM是由Adobe內容套件Maven外掛程式執行，並可自動執行使用AEM通常執行的工作 [包管理器：](/help/implementing/developing/tools/package-manager.md)

* 從檔案系統中的檔案建立新包。
* 在AEM上安裝和解除安裝套件。
* 建立已在AEM上定義的套件。
* 取得AEM上安裝的套件清單。
* 從AEM移除套件。

本檔案詳細說明如何使用Maven管理這些工作。 不過，了解這一點也很重要 [AEM專案及其套件的結構方式。](#aem-project-structure)

>[!NOTE]
>
>套件 **建立** 現在歸 [Apache Jackrabbit FileVault Package Maven外掛程式。](https://jackrabbit.apache.org/filevault-package-maven-plugin/)
>* 此 `content-package-maven-plugin` 不再支援1.0.2版的封裝。
>* 本文說明 **部署** 的已建構套件會由Adobe內容套件Maven外掛程式執行。


## 套件和AEM專案結構 {#aem-project-structure}

AEM as a Cloud Service遵循最新AEM專案原型所實作的套件管理和專案結構最新最佳實務。

>[!TIP]
>
>如需詳細資訊，請參閱 [AEM專案結構](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) AEMas a Cloud Service檔案中的文章，以及 [AEM專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) 檔案。 兩者皆完全支援AEM 6.5。

## 取得內容套件Maven外掛程式 {#obtaining-the-content-package-maven-plugin}

外掛程式可從 [Maven中央儲存庫。](https://mvnrepository.com/artifact/com.day.jcr.vault/content-package-maven-plugin?repo=adobe-public)

## 內容套件Maven外掛程式目標與參數

若要使用「內容套件Maven外掛程式」，請在POM檔案的建置元素內新增下列外掛程式元素：

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

若要啟用Maven下載外掛程式，請使用 [取得內容套件Maven外掛程式](#obtaining-the-content-package-maven-plugin) 區段。

## 內容套件Maven外掛程式的目標 {#goals-of-the-content-package-maven-plugin}

內容套件外掛程式提供的目標和目標參數將於後續章節中說明。 公用參數區段中所述的參數可用於大部分目標。 適用於一個目標的參數在該目標的一節中有說明。

### 外掛程式首碼 {#plugin-prefix}

外掛程式首碼為 `content-package`. 使用此前置詞從命令行執行目標，如下例所示：

```shell
mvn content-package:build
```

### 參數前置詞 {#parameter-prefix}

除非另有說明，否則外掛程式目標和參數會使用 `vault` 前置詞，如下列範例所示：

```shell
mvn content-package:install -Dvault.targetURL="https://192.168.1.100:4502/crx/packmgr/service.jsp"
```

### Proxy {#proxies}

使用AEM代理的目標會使用Maven設定中找到的第一個有效代理設定。 如果未找到代理配置，則不使用代理。 請參閱 `useProxy` 參數 [公用參數](#common-parameters) 區段。

### 公用參數 {#common-parameters}

下表中的參數是所有目標的共同參數，除 **目標** 欄。

| 名稱 | 類型 | 必要 | 預設值 | 說明 | 目標 |
|---|---|---|---|---|---|
| `failOnError` | `boolean` | 否 | `false` | 值 `true` 造成發生錯誤時組建失敗。 值 `false` 導致組建忽略錯誤。 | 除了 `package` |
| `name` | `String` | `build`:是， `install`:不， `rm`:是 | `build`:無預設值， `install`:的值 `artifactId` Maven項目的屬性 | 要執行操作的包的名稱 | 除了 `ls` |
| `password` | `String` | 是 | `admin` | 用於與AEM進行身份驗證的密碼 | 除了 `package` |
| `serverId` | `String` | 否 | 要從中檢索用戶名和口令以進行身份驗證的伺服器ID | 除了 `package` |
| `targetURL` | `String` | 是 | `http://localhost:4502/crx/packmgr/service.jsp` | AEM套件管理員的HTTP服務API URL | 除了 `package` |
| `timeout` | `int` | 否 | `5` | 用於與包管理器服務通信的連接超時（以秒為單位） | 除了 `package` |
| `useProxy` | `boolean` | 否 | `true` | 值 `true` 導致Maven使用找到的第一個活動代理配置，以便代理向包管理器發出的請求。 | 除了 `package` |
| `userId` | `String` | 是 | `admin` | 要使用AEM進行驗證的使用者名稱 | 除了 `package` |
| `verbose` | `boolean` | 否 | `false` | 啟用或禁用詳細記錄 | 除了 `package` |

### 建置 {#build}

建置已在AEM例項上定義的內容套件。

>[!NOTE]
>
>不需要在Maven專案內執行此目標。

#### 參數 {#parameters}

有關建置目標的所有參數，請參閱 [公用參數](#common-parameters) 區段。

### 安裝 {#install}

在儲存庫中安裝軟體包。 執行此目標不需要Maven專案。 目標是與 `install` Maven建置生命週期的階段。

#### 參數 {#parameters-1}

除了下列參數外，請參閱 [公用參數](#common-parameters) 區段。

| 名稱 | 類型 | 必要 | 預設值 | 說明 |
|---|---|---|---|---|
| `artifact` | `String` | 否 | 的值 `artifactId` Maven項目的屬性 | 表單的字串 `groupId:artifactId:version[:packaging]` |
| `artifactId` | `String` | 否 | 無 | 要安裝的對象的ID |
| `groupId` | `String` | 否 | 無 | 此 `groupId` 要安裝的工件 |
| `install` | `boolean` | 否 | `true` | 確定是否在包上載時自動解包 |
| `localRepository` | `org.apache.maven.artifact.repository.ArtifactRepository` | 否 | 的值 `localRepository` 系統變數 | 無法使用外掛程式設定來設定的本機Maven存放庫，因為系統屬性一律使用 |
| `packageFile` | `java.io.File` | 否 | 為Maven項目定義的主對象 | 要安裝的包檔案的名稱 |
| `packaging` | `String` | 否 | `zip` | 要安裝的對象的包裝類型 |
| `pomRemoteRepositories` | `java.util.List` | 是 | 的值 `remoteArtifactRepositories` 為Maven項目定義的屬性 | 無法使用外掛程式設定來設定此值，且必須在專案中指定。 |
| `project` | `org.apache.maven.project.MavenProject` | 是 | 為其配置插件的項目 | 隱含的Maven專案，因為專案包含外掛程式組態 |
| `repositoryId` (POM)、 `repoID` （命令列） | `String` | 否 | `temp` | 從中檢索對象的儲存庫的ID |
| `repositoryUrl` (POM)、 `repoURL` （命令列） | `String` | 否 | 無 | 從中檢索工件的儲存庫的URL |
| 版本 | 字串 | 否 | 無 | 要安裝的對象的版本 |

### ls {#ls}

列出部署到的包 [封裝管理員。](/help/implementing/developing/tools/package-manager.md)

#### 參數 {#parameters-2}

ls目標的所有參數都在 [公用參數](#common-parameters) 區段。

### rm {#rm}

從 [封裝管理員。](/help/implementing/developing/tools/package-manager.md)

#### 參數 {#parameters-3}

rm目標的所有參數均在 [公用參數](#common-parameters) 區段。

### 解除安裝 {#uninstall}

卸載軟體包。 軟體包仍在伺服器上處於卸載狀態。

#### 參數 {#parameters-4}

解除安裝目標的所有參數均在 [公用參數](#common-parameters) 區段。

### 套件 {#package}

建立內容套件。 包目標的預設配置包括保存已編譯檔案的目錄的內容。 要執行包目標，需要完成編譯生成階段。 套件目標會系結至Maven組建生命週期的套件階段。

#### 參數 {#parameters-5}

除了下列參數外，請參閱 `name` 參數 [公用參數](#common-parameters) 區段。

| 名稱 | 類型 | 必要 | 預設值 | 說明 |
|---|---|---|---|---|
| `archive` | `org.apache.maven.archiver.MavenArchiveConfiguration` | 否 | 無 | 要使用的封存設定 |
| `builtContentDirectory` | `java.io.File` | 是 | Maven構建版本的輸出目錄的值 | 包含要包含在包中的內容的目錄 |
| `dependencies` | `java.util.List` | 否 | 無 |  |
| `embeddedTarget` | `java.lang.String` | 否 | 無 |  |
| `embeddeds` | `java.util.List` | 否 | 無 |  |
| `failOnMissingEmbed` | `boolean` | 是 | `false` | 值 `true` 在項目依賴項中找不到嵌入對象時導致生成失敗。 值 `false` 導致組建忽略這些錯誤。 |
| `filterSource` | `java.io.File` | 否 | 無 | 此參數定義一個指定工作區過濾器源的檔案。 在設定中指定並透過內嵌或子封裝插入的篩選器會與檔案內容合併。 |
| `filters` | `com.day.jcr.vault.maven.pack.impl.DefaultWorkspaceFilter` | 否 | 無 | 此參數包含定義套件內容的篩選元素。 執行時，篩選器會包含在 `filter.xml` 檔案。 請參閱 [使用篩選](#using-filters) 一節。 |
| `finalName` | `java.lang.String` | 是 | 此 `finalName` 在Maven專案中定義（建置階段） | 產生的套件ZIP檔案的名稱，不含 `.zip` 檔案副檔名 |
| `group` | `java.lang.String` | 是 | 此 `groupID` 在Maven專案中定義 | 此 `groupId` 內容包的目標安裝路徑的一部分 |
| `outputDirectory` | `java.io.File` | 是 | Maven專案中定義的組建目錄 | 保存內容包的本地目錄 |
| `prefix` | `java.lang.String` | 否 | 無 |  |
| `project` | `org.apache.maven.project.MavenProject` | 是 | 無 | 馬文項目 |
| `properties` | `java.util.Map` | 否 | 無 | 這些參數會定義您可在 `properties.xml` 檔案。 這些屬性無法覆寫下列預先定義的屬性： `group` (使用 `group` 參數), `name` (使用 `name` 參數), `version` (使用 `version` 參數), `description` （從項目描述設定）, `groupId` (`groupId` 描述符), `artifactId` (`artifactId` 描述符), `dependencies` (使用 `dependencies` 參數), `createdBy` ( `user.name` 系統屬性), `created` （當前系統時間）, `requiresRoot` (使用 `requiresRoot` 參數), `packagePath` （自動從組和包名生成） |
| `requiresRoot` | `boolean` | 是 | false | 定義包是否需要根。 這會成為 `requiresRoot` 屬性 `properties.xml` 檔案。 |
| `subPackages` | `java.util.List` | 否 | 無 |  |
| `version` | `java.lang.String` | 是 | Maven專案中定義的版本 | 內容套件的版本 |
| `workDirectory` | `java.io.File` | 是 | Maven專案（建置階段）中定義的目錄 | 包含要包含在包中的內容的目錄 |

#### 使用篩選 {#using-filters}

使用篩選元素來定義套件內容。 篩選器會新增至 `workspaceFilter` 元素 `META-INF/vault/filter.xml` 檔案。

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

此 `mode` 元素會定義匯入套件時對存放庫內容的影響。 可使用下列值：

* **合併：** 套件中尚未在存放庫中的內容會新增。 套件和存放庫中的內容未變更。 系統不會從存放庫中移除任何內容。
* **替換：** 套件中不在存放庫的內容會新增至存放庫。 儲存庫中的內容會取代為套件中的相符內容。 內容不存在於套件中時，會從存放庫中移除內容。
* **更新：** 套件中不在存放庫的內容會新增至存放庫。 儲存庫中的內容會取代為套件中的相符內容。 現有內容會從存放庫中移除。

當篩選器包含否 `mode` 元素，預設值為 `replace` 中所有規則的URL區段。

### 說明 {#help}

#### 參數 {#parameters-6}

| 名稱 | 類型 | 必要 | 預設值 | 說明 |
|---|---|---|---|---|
| `detail` | `boolean` | 否 | `false` | 確定是否顯示每個目標的所有可設定屬性 |
| `goal` | `String` | 否 | 無 | 此參數會定義要顯示說明的目標名稱。 如果未指定任何值，則顯示所有目標的幫助。 |
| `indentSize` | `int` | 否 | `2` | 用於每個級別縮進的空格數（如果已定義，則必須為正） |
| `lineLength` | `int` | 否 | `80` | 顯示線的最大長度（如果已定義，則必須為正） |

## 在包中包括縮略圖或屬性檔案 {#including-a-thumbnail-image-or-properties-file-in-the-package}

替換預設包配置檔案以自定義包屬性。 例如，納入縮圖影像以區分中的套件 [封裝管理員。](/help/implementing/developing/tools/package-manager.md)

源檔案可以位於檔案系統中的任何位置。 在POM檔案中，定義建置資源，以將來源檔案複製到 `target/vault-work/META-INF` 包含在包中。

下列POM程式碼會將檔案新增至 `META-INF` 項目源的資料夾到包：

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

下列POM程式碼只會將縮圖影像新增至套件。 縮圖影像必須命名 `thumbnail.png`，和必須位於 `META-INF/vault/definition` 包的資料夾。 在此示例中，源檔案位於 `/src/main/content/META-INF/vault/definition` 項目資料夾：

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

## 使用AEM專案原型產生AEM專案 {#using-archetypes}

最新的AEM專案原型會針對內部部署和AMS實作實作實作最佳實務套件結構，且建議用於所有AEM專案。

>[!TIP]
>
>如需詳細資訊，請參閱 [AEM專案結構](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) AEMas a Cloud Service檔案中的文章，以及 [AEM專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) 檔案。 兩者皆完全支援AEM 6.5。
