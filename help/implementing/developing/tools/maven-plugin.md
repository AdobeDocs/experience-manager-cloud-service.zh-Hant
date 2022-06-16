---
title: Adobe內容包Maven插件
description: 使用內容包管理插件部署應AEM用程式
exl-id: d631d6df-7507-4752-862b-9094af9759a0
source-git-commit: ba4e2427873fc9f5d91ee4f520df01018000a4c7
workflow-type: tm+mt
source-wordcount: '1851'
ht-degree: 6%

---

# Adobe內容包Maven插件 {#adobe-content-package-maven-plugin}

使用Adobe內容包管理插件將包部署和管理任務整合到Maven項目中。

將構造的包部署AEM到由Adobe內容包Maven插件執行，並使通常使用 [包管理器：](/help/implementing/developing/tools/package-manager.md)

* 從檔案系統中的檔案建立新包。
* 在上安裝和卸載包AEM。
* 生成已在上定義的包AEM。
* 獲取安裝在上的軟體包的列AEM表。
* 從中刪除包AEM。

本文檔詳細介紹了如何使用Maven管理這些任務。 但是，瞭解 [項目及AEM其包的結構。](#aem-project-structure)

>[!NOTE]
>
>包 **建立** 現在由 [Apache Jackrabbit FileVault包Maven插件。](https://jackrabbit.apache.org/filevault-package-maven-plugin/)
>* 的 `content-package-maven-plugin` 不再支援1.0.2版中的打包。
>* 本文介紹 **部署** 由Adobe內容包MavenAEM插件執行的。


## 包和項AEM目結構 {#aem-project-structure}

AEMas a Cloud Service遵循最新「項目原型」實施的包管理和項目結構的最AEM新最佳實踐。

>[!TIP]
>
>有關詳細資訊，請參閱 [項AEM目結構](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) 文AEM章，以及 [項AEM目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) 文檔。 這兩個都完全支AEM持6.5。

## 獲取內容包Maven插件 {#obtaining-the-content-package-maven-plugin}

插件可從 [Maven中央儲存庫。](https://mvnrepository.com/artifact/com.day.jcr.vault/content-package-maven-plugin?repo=adobe-public)

## 內容包Maven插件目標和參數

要使用內容包Maven插件，請在POM檔案的生成元素中添加以下插件元素：

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

要使Maven能夠下載插件，請使用中提供的配置檔案 [獲取內容包Maven插件](#obtaining-the-content-package-maven-plugin) 的子菜單。

## 內容包Maven插件的目標 {#goals-of-the-content-package-maven-plugin}

「內容包」插件提供的目標和目標參數在以下各節中進行了說明。 「公共參數」(Common Parameters)部分中描述的參數可用於大多數目標。 適用於一個目標的參數在該目標的一節中介紹。

### 插件前置詞 {#plugin-prefix}

插件前置詞是 `content-package`。 使用此前置詞從命令行執行目標，如下例所示：

```shell
mvn content-package:build
```

### 參數前置詞 {#parameter-prefix}

除非另有說明，否則插件目標和參數使用 `vault` 前置詞，如下例所示：

```shell
mvn content-package:install -Dvault.targetURL="https://192.168.1.100:4502/crx/packmgr/service.jsp"
```

### 代理 {#proxies}

使用代理使用Maven設AEM置中找到的第一個有效代理配置的目標。 如果未找到代理配置，則不使用代理。 查看 `useProxy` 參數 [公用參數](#common-parameters) 的子菜單。

### 公用參數 {#common-parameters}

下表中的參數對所有目標都是通用的，但在 **目標** 的雙曲餘切值。

| 名稱 | 類型 | 必要 | 預設值 | 說明 | 目標 |
|---|---|---|---|---|---|
| `failOnError` | `boolean` | 否 | `false` | 值 `true` 導致生成在出錯時失敗。 值 `false` 導致生成忽略錯誤。 | 除非 `package` |
| `name` | `String` | `build`:是的， `install`:不， `rm`:是 | `build`:無預設值， `install`:的值 `artifactId` Maven項目的屬性 | 要操作的包的名稱 | 除非 `ls` |
| `password` | `String` | 是 | `admin` | 用於驗證的密AEM碼 | 除非 `package` |
| `serverId` | `String` | 否 | 要從中檢索身份驗證的用戶名和密碼的伺服器ID | 除非 `package` |
| `targetURL` | `String` | 是 | `http://localhost:4502/crx/packmgr/service.jsp` | 包管理器的HTTP服務APIAEM的URL | 除非 `package` |
| `timeout` | `int` | 否 | `5` | 與包管理器服務通信的連接超時（秒） | 除非 `package` |
| `useProxy` | `boolean` | 否 | `true` | 值 `true` 導致Maven使用找到的第一個活動代理配置，以便將請求代理到包管理器。 | 除非 `package` |
| `userId` | `String` | 是 | `admin` | 要驗證的用戶名AEM | 除非 `package` |
| `verbose` | `boolean` | 否 | `false` | 啟用或禁用詳細記錄 | 除非 `package` |

### 構建 {#build}

生成已在實例上定義的內容AEM包。

>[!NOTE]
>
>無需在Maven項目內執行此目標。

#### 參數 {#parameters}

有關生成目標的所有參數，請參見 [公用參數](#common-parameters) 的子菜單。

### 安裝 {#install}

在儲存庫中安裝軟體包。 執行此目標不需要Maven項目。 目標與 `install` Maven生成生命週期的階段。

#### 參數 {#parameters-1}

除以下參數外，請參見 [公用參數](#common-parameters) 的子菜單。

| 名稱 | 類型 | 必要 | 預設值 | 說明 |
|---|---|---|---|---|
| `artifact` | `String` | 否 | 的值 `artifactId` Maven項目的屬性 | 表單的字串 `groupId:artifactId:version[:packaging]` |
| `artifactId` | `String` | 否 | 無 | 要安裝的項目的ID |
| `groupId` | `String` | 否 | 無 | 的 `groupId` 要安裝的工件 |
| `install` | `boolean` | 否 | `true` | 確定是否在上載包時自動解包 |
| `localRepository` | `org.apache.maven.artifact.repository.ArtifactRepository` | 否 | 的值 `localRepository` 系統變數 | 始終使用無法使用插件配置配置作為系統屬性配置的本地Maven儲存庫 |
| `packageFile` | `java.io.File` | 否 | 為Maven項目定義的主對象 | 要安裝的包檔案的名稱 |
| `packaging` | `String` | 否 | `zip` | 要安裝的項目的包裝類型 |
| `pomRemoteRepositories` | `java.util.List` | 是 | 的值 `remoteArtifactRepositories` 為Maven項目定義的屬性 | 無法使用插件配置配置此值，必須在項目中指定該值。 |
| `project` | `org.apache.maven.project.MavenProject` | 是 | 為其配置插件的項目 | Maven項目，該項目由於項目包含插件配置而隱含 |
| `repositoryId` (POM) `repoID` （命令行） | `String` | 否 | `temp` | 從中檢索對象的儲存庫的ID |
| `repositoryUrl` (POM) `repoURL` （命令行） | `String` | 否 | 無 | 從中檢索對象的儲存庫的URL |
| 版本 | 字串 | 否 | 無 | 要安裝的項目的版本 |

### ls {#ls}

列出部署到的包 [包管理器。](/help/implementing/developing/tools/package-manager.md)

#### 參數 {#parameters-2}

ls目標的所有參數在 [公用參數](#common-parameters) 的子菜單。

### rm {#rm}

從中刪除包 [包管理器。](/help/implementing/developing/tools/package-manager.md)

#### 參數 {#parameters-3}

rm目標的所有參數在 [公用參數](#common-parameters) 的子菜單。

### 卸載 {#uninstall}

卸載程式包。 該軟體包仍處於已卸載狀態。

#### 參數 {#parameters-4}

卸載目標的所有參數在 [公用參數](#common-parameters) 的子菜單。

### 包 {#package}

建立內容包。 包目標的預設配置包括保存已編譯檔案的目錄的內容。 執行包目標需要編譯生成階段已完成。 包目標將綁定到Maven生成生命週期的包階段。

#### 參數 {#parameters-5}

除以下參數外，請參閱 `name` 參數 [公用參數](#common-parameters) 的子菜單。

| 名稱 | 類型 | 必要 | 預設值 | 說明 |
|---|---|---|---|---|
| `archive` | `org.apache.maven.archiver.MavenArchiveConfiguration` | 否 | 無 | 要使用的存檔配置 |
| `builtContentDirectory` | `java.io.File` | 是 | Maven生成的輸出目錄的值 | 包含要包含在包中的內容的目錄 |
| `dependencies` | `java.util.List` | 否 | 無 |  |
| `embeddedTarget` | `java.lang.String` | 否 | 無 |  |
| `embeddeds` | `java.util.List` | 否 | 無 |  |
| `failOnMissingEmbed` | `boolean` | 是 | `false` | 值 `true` 在項目相關性中找不到嵌入的項目時，會導致生成失敗。 值 `false` 導致生成忽略此類錯誤。 |
| `filterSource` | `java.io.File` | 否 | 無 | 此參數定義一個指定工作區篩選器源的檔案。 在配置中指定並通過嵌入式或子包注入的過濾器與檔案內容合併。 |
| `filters` | `com.day.jcr.vault.maven.pack.impl.DefaultWorkspaceFilter` | 否 | 無 | 此參數包含定義包內容的篩選器元素。 執行時，篩選器將包含在 `filter.xml` 的子菜單。 查看 [使用篩選器](#using-filters) 的下界。 |
| `finalName` | `java.lang.String` | 是 | 的 `finalName` 在Maven項目（生成階段）中定義 | 生成的包ZIP檔案的名稱， `.zip` 檔案擴展 |
| `group` | `java.lang.String` | 是 | 的 `groupID` 在Maven項目中定義 | 的 `groupId` 內容包的目標安裝路徑的一部分 |
| `outputDirectory` | `java.io.File` | 是 | 在Maven項目中定義的生成目錄 | 保存內容包的本地目錄 |
| `prefix` | `java.lang.String` | 否 | 無 |  |
| `project` | `org.apache.maven.project.MavenProject` | 是 | 無 | 馬文項目 |
| `properties` | `java.util.Map` | 否 | 無 | 這些參數定義可在 `properties.xml` 的子菜單。 這些屬性無法覆蓋以下預定義屬性： `group` （使用） `group` 要設定的參數), `name` （使用） `name` 要設定的參數), `version` （使用） `version` 要設定的參數), `description` （根據項目說明設定）, `groupId` (`groupId` 描述符), `artifactId` (`artifactId` 描述符), `dependencies` （使用） `dependencies` 要設定的參數), `createdBy` 值 `user.name` 系統屬性), `created` （當前系統時間）, `requiresRoot` （使用） `requiresRoot` 要設定的參數), `packagePath` （自動從組和包名稱生成） |
| `requiresRoot` | `boolean` | 是 | false | 定義包是否需要根。 這將成為 `requiresRoot` 屬性 `properties.xml` 的子菜單。 |
| `subPackages` | `java.util.List` | 否 | 無 |  |
| `version` | `java.lang.String` | 是 | 在Maven項目中定義的版本 | 內容包的版本 |
| `workDirectory` | `java.io.File` | 是 | 在Maven項目（生成階段）中定義的目錄 | 包含要包含在包中的內容的目錄 |

#### 使用篩選器 {#using-filters}

使用filters元素定義包內容。 篩選器將添加到 `workspaceFilter` 元素 `META-INF/vault/filter.xml` 檔案。

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

的 `mode` 元素定義導入包時對儲存庫的影響。 可以使用以下值：

* **合併：** 將添加包中尚未在儲存庫中的內容。 包和儲存庫中的內容保持不變。 未從儲存庫中刪除任何內容。
* **替換：** 不在儲存庫中的包中的內容將添加到儲存庫。 儲存庫中的內容將替換為包中的匹配內容。 內容在包中不存在時從儲存庫中刪除。
* **更新：** 不在儲存庫中的包中的內容將添加到儲存庫。 儲存庫中的內容將替換為包中的匹配內容。 現有內容將從儲存庫中刪除。

當篩選器不包含 `mode` 元素，預設值 `replace` 的子菜單。

### 說明 {#help}

#### 參數 {#parameters-6}

| 名稱 | 類型 | 必要 | 預設值 | 說明 |
|---|---|---|---|---|
| `detail` | `boolean` | 否 | `false` | 確定是否顯示每個目標的所有可設定屬性 |
| `goal` | `String` | 否 | 無 | 此參數定義要顯示幫助的目標名稱。 如果未指定值，則顯示所有目標的幫助。 |
| `indentSize` | `int` | 否 | `2` | 每個級別的縮進所用的空格數（如果定義，則必須為正） |
| `lineLength` | `int` | 否 | `80` | 顯示線的最大長度（如果定義，則必須為正） |

## 在包中包括縮略圖或屬性檔案 {#including-a-thumbnail-image-or-properties-file-in-the-package}

替換預設包配置檔案以自定義包屬性。 例如，包括縮略圖以在中區分包 [包管理器。](/help/implementing/developing/tools/package-manager.md)

源檔案可以位於檔案系統的任何位置。 在POM檔案中，定義生成資源以將源檔案複製到 `target/vault-work/META-INF` 包含在包中。

以下POM代碼將檔案添加到 `META-INF` 項目源的資料夾：

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

以下POM代碼只向包添加縮略圖。 縮略圖必須命名 `thumbnail.png`，並且必須位於 `META-INF/vault/definition` 資料夾。 在本示例中，源檔案位於 `/src/main/content/META-INF/vault/definition` 項目的資料夾：

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

## 使用項AEM目原型生成項AEM目 {#using-archetypes}

最新的AEM項目原型為內部實施和AMS實施都實施了最佳做法包結構，並建議用於所有AEM項目。

>[!TIP]
>
>有關詳細資訊，請參閱 [項AEM目結構](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) 文AEM章，以及 [項AEM目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) 文檔。 這兩個都完全支AEM持6.5。
