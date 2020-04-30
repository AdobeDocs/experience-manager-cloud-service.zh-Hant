---
title: AEM 專案結構
description: 瞭解如何定義封裝結構以部署至Adobe Experience Manager Cloud Service。
translation-type: tm+mt
source-git-commit: 94182b95cb00923d3e055cb3c2e1d943db70c7a9

---


# AEM 專案結構

>[!TIP]
>
>請熟悉基本的 [AEM Project Archetype使用](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/overview.html)，以及 [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/vlt-mavenplugin.html) FileVault Content Maven Plug-in，因為本文以這些學習與概念為基礎。

本文概述Adobe Experience Manager Maven專案所需的變更，以確保其符合可變和不可變內容的分割；建立必要的相依性，以建立不衝突、確定性的部署；它們被封裝成可展開的結構。

AEM應用程式部署必須由單一AEM套件組成。 此套件應包含子套件，這些子套件包含應用程式運作所需的一切，包括程式碼、組態和任何支援的基準內容。

AEM需要分離內 **容和程式碼** ，這表示單一內容套件 **無法**&#x200B;部署至 ********`/apps` Runtime可寫區域 (例如，可寫區域)。`/content`、 `/conf`、 `/home`或其他非 `/apps`)。而應用程式必須將程式碼和內容分隔為獨立套件，以便部署至AEM。

本檔案中概述的套件結構與本機開 **發部署** 和AEM cloud服務部署都相容。

>[!TIP]
>
>本檔案中概述的組態由 [AEM Project Maven Archetype 21或更新版本提供](https://github.com/adobe/aem-project-archetype/releases)。

## 儲存庫的可變區與不可變區 {#mutable-vs-immutable}

`/apps` and `/libs` are consed **inmumable areas of AEM** as they cannot be changed(create, update, delete)after AEM starts(i.e. at runtime)。在運行時更改不可變區域的任何嘗試都將失敗。

儲存庫中的其 `/content`它所有 `/conf`內容 `/var`、 、 `/etc`、 `/oak:index`、 `/system``/tmp`、等。 皆為可 **變區** ，也就是說可在執行時期變更。

>[!WARNING]
>
> 和舊版AEM一樣， `/libs` 不應修改。 只有AEM產品程式碼可部署至 `/libs`。

## 建議的套件結構 {#recommended-package-structure}

![Experience Manager專案套件結構](assets/content-package-organization.png)

此圖概述了建議的項目結構和包部署對象。

建議的應用程式部署結構如下：

+ 該包 `ui.apps` 或代碼包包含要部署的所有代碼，並且僅部署到 `/apps`。 包的常見元 `ui.apps` 素包括，但不限於：
   + OSGi組合
      + `/apps/my-app/install`
   + OSGi配置
      + `/apps/my-app/config`
   + HTL指令碼
      + `/apps/my-app/components`
   + JavaScript和CSS（透過用戶端程式庫）
      + `/apps/my-app/clientlibs`
   + /libs的覆蓋
      + `/apps/cq`、 `/apps/dam/`等。
   + 備援內容感知組態
      + `/apps/settings`
   + ACL（權限）
      + 任 `rep:policy` 何路徑 `/apps`
   + 回購初始化OSGi配置指令（及隨附的指令碼）
      + [回購初始](#repo-init) (Repo Init)是部署（可變）AEM應用程式邏輯部分內容的建議方式。 回購初始化應用於定義：
         + 基線內容結構
            + `/conf/my-app`
            + `/content/my-app`
            + `/content/dam/my-app`
         + 使用者
         + 服務使用者
         + 群組
         + ACL（權限）
            + 任何 `rep:policy` 路徑（可變或不可變）
+ 套件 `ui.content` 或內容套件包含所有內容和設定。 「內容套件」包含套件中未包含的一 `ui.apps` 切，換言之，任何不在或中的 `/apps` 項目 `/oak:index`。 包的常見元 `ui.content` 素包括，但不限於：
   + 內容感知配置
      + `/conf`
   + 必要、複雜的內容結構(即 內容構建以回購初始化中定義的基線內容結構為基礎，並將其擴展到基線內容結構之上。
      + `/content`、 `/content/dam`等。
   + 受管理的標籤分類
      + `/content/cq:tags`
   + Etc legacy nodes
      + `/etc`
+ 包 `all` 裝是容器包裝，僅包含 `ui.apps` 和 `ui.content` 包作為內嵌。包 `all` 不得具有 **任何內容** ，而是將所有部署委派給儲存庫的子包。

   現在，軟體包是使用Maven [FileVault Package Maven插件的嵌入式配置](#embeddeds)，而不是使用配置 `<subPackages>` 的。

   對於複雜的Experience Manager部署，可能需要在AEM中建立多個 `ui.apps` 和 `ui.content` 專案／套件，以代表特定網站或租戶。 如果完成此操作，請確保可變內容和不可變內容之間的分割得到尊重，並且所需的內容包將作為子包添加到容器內 `all` 容包中。

   例如，複雜的部署內容套件結構可能如下所示：

   + `all` 內容套件內嵌下列套件，以建立單一部署工件
      + `ui.apps.common` 部署站點A和 **站點** B所需的代碼
      + `ui.apps.site-a` 部署站點A所需的代碼
      + `ui.content.site-a` 部署站點A所需的內容和配置
      + `ui.apps.site-b` 部署站點B所需的代碼
      + `ui.content.site-b` 部署站點B所需的內容和配置

## 包類型 {#package-types}

包將用其聲明的包類型標籤。

+ 容器封裝不得有 `packageType` 設定。
+ 代碼（不可變）包必須將其 `packageType` 設定為 `application`。
+ 內容（可變）包必須將其 `packageType` 設定為 `content`。

如需詳細資訊，請 [參閱下方的Apache Jackrabbit FileVault - Package Maven Plugin檔案](https://jackrabbit.apache.org/filevault-package-maven-plugin/package-mojo.html#packageType) , [以及FileVault Maven組態程式碼片段](#marking-packages-for-deployment-by-adoube-cloud-manager) 。

>[!TIP]
>
>請參閱下 [面的POM XML程式碼片段](#xml-package-types) ，以取得完整的程式碼片段。

## 由Adobe Cloud Manager標籤要部署的套件 {#marking-packages-for-deployment-by-adoube-cloud-manager}

依預設，Adobe Cloud manager會收集由Maven組建版本產生的所有套件，但是，由於容器(`all`)套件是包含所有程式碼和內容套件的單一部署工件，因此我們必須確保僅部署容器( ****`all`)套件。為確保此，Maven構建版本生成的其他軟體包必須用的FileVault Content Package Maven插件配置進行標籤 `<properties><cloudManagerTarget>none</cloudManageTarget></properties>`。

>[!TIP]
>
>請參閱下 [面的POM XML程式碼片段](#pom-xml-snippets) ，以取得完整的程式碼片段。

## 回購初始化{#repo-init}

Repo Init提供了定義JCR結構的指令或指令碼，這些結構從常見的節點結構（如資料夾樹）到用戶、服務用戶、組和ACL定義。

回購初始化的主要優點是，它們具有執行其指令碼定義的所有操作的隱式權限，並且在部署生命週期的早期被調用，以確保在執行時間代碼時存在所有必需的JCR結構。

雖然Repo Init指令碼本身作為指令碼 `ui.apps` 在項目中生存，但它們可以而且應該用於定義以下可變結構：

+ 基線內容結構
   + Examples: `/content/my-app`, `/content/dam/my-app`, `/conf/my-app/settings`
+ 服務使用者
+ 使用者
+ 群組
+ ACL

回購初始化指令碼會儲存為 `scripts``RepositoryInitializer` OSGi工廠組態的項目，因此可透過執行模式隱式定位，允許AEM Author和AEM Publish Services的回購初始化指令碼之間，或甚至是Envs（Dev、Stage和Prod）之間的差異。

請注意，在定義「使用者」和「群組」時，只有群組會視為應用程式的一部分，而且應在此處定義其功能的整數。 「組織使用者」和「群組」仍應在AEM的執行時期中定義；例如，如果自訂工作流程將工作指派給指名的群組，則該群組應透過AEM應用程式中的回購初始化定義，但是，如果群組僅是組織性的，例如「Wendy&#39;s Team」和「Sean&#39;s Team」，則這些工作是最佳定義，並在AEM的執行時期進行管理。

>[!TIP]
>
>回購初始化 *指令碼必須在內* 嵌欄位中定義 `scripts` ，並且配置將 `references` 無法運行。

Apache Sling Repo Init檔案中提供回購初始化指令碼的 [完整辭彙](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language)。

>[!TIP]
>
>請參閱下 [面的「回購初始化代碼片段](#snippet-repo-init) 」一節，以取得完整的程式碼片段。

## 儲存庫結構包 {#repository-structure-package}

「代碼包」要求配置FileVault Maven插件的配置，以引用實施結構依賴性正確性的 `<repositoryStructurePackage>` 配置（以確保一個代碼包不會安裝在另一個代碼包上）。 您可以 [為項目建立自己的儲存庫結構包](repository-structure-package.md)。

這只是程 **式碼套件的必要** ，也就是任何標有的套件 `<packageType>application</packageType>`。

要瞭解如何為應用程式建立儲存庫結構包，請參 [閱開發儲存庫結構包](repository-structure-package.md)。

請注意，內容包(`<packageType>content</packageType>`)不 **需要此儲存庫** 結構包。

>[!TIP]
>
>請參閱下 [面的POM XML程式碼片段](#xml-repository-structure-package) ，以取得完整的程式碼片段。

## 將子包嵌入容器包中{#embeddeds}

內容或程式碼套件會放在特殊的「側車」檔案夾中，並可定位為使用FileVault Maven增效模組的組態，在AEM作者、AEM發佈或兩者上安 `<embeddeds>` 裝。 請注意， `<subPackages>` 不應使用此配置。

常見使用案例包括：

+ AEM作者使用者與AEM發佈使用者之間不同的ACL/權限
+ 僅用於支援AEM作者活動的設定
+ 程式碼，例如與後端系統整合，只需在AEM作者上執行

![內嵌套件](assets/embeddeds.png)

若要定位AEM作者、AEM發佈或兩者，套件會內嵌在容器套件中的特殊資料夾位置，格式如下： `all`

`/apps/<app-name>-packages/(content|application)/install(.author|.publish)?`

劃分此資料夾結構：

+ 第1級資料夾必 **須是**`/apps`。
+ 第2層資料夾代表具有後置修正檔 `-packages` 案夾名稱的應用程式。 通常，所有子包都只嵌入一個第2級資料夾，但可以建立任意數量的第2級資料夾以最好地表示應用程式的邏輯結構：
   + `/apps/my-app-packages`
   + `/apps/my-other-app-packages`
   + `/apps/vendor-packages`
   >[!WARNING]
   >
   >根據慣例，子包嵌入資料夾的名稱為尾碼為 `-packages`。這可確保部署代碼和內容包 **未部署** ，而是不會部署任何子包的目標資料夾， `/apps/<app-name>/...` 從而導致破壞性和循環安裝行為。

+ 第3級資料夾必須是
   `application` 或 `content`
   + 檔案 `application` 夾包含代碼包
   + 檔案 `content` 夾golds內容包此資料夾名稱必須與包 [含的包](#package-types) 的包類型對應。
+ 第4層資料夾包含子包，且必須是下列其中一個：
   + `install` 若要同時安裝 **在** AEM作者和AEM發佈上
   + `install.author` 僅 **安裝** 在AEM作者上
   + `install.publish` to **only** install on AEM publishNote that only `install.author` and are supported `install.publish` targets. 不支援其 **他執行模** 式。

例如，包含AEM作者和發佈特定套件的部署可能如下所示：

+ `all` 容器套件內嵌下列套件，以建立單一的部署工件
   + `ui.apps` 內嵌於 `/apps/my-app-packages/application/install` 將程式碼同時部署至AEM作者和AEM發佈
   + `ui.apps.author` 內嵌於 `/apps/my-app-packages/application/install.author` 將程式碼部署至僅限AEM作者
   + `ui.content` 內嵌於 `/apps/my-app-packages/content/install` 將內容和設定部署至AEM作者和AEM發佈
   + `ui.content.publish` 內嵌於 `/apps/my-app-packages/content/install.publish` 將內容和設定部署至僅AEM發佈

>[!TIP]
>
>請參閱下 [面的POM XML程式碼片段](#xml-embeddeds) ，以取得完整的程式碼片段。

### 容器套件的篩選定義 {#container-package-filter-definition}

由於容器封裝中內嵌了程式碼和內容子封裝，因此必須將內嵌的目標路徑新增至容器專案，以確保內嵌的封裝在建立時 `filter.xml` ，會包含在容器封裝中。

只需為包 `<filter root="/apps/<my-app>-packages"/>` 含要部署的子包的任何2級資料夾添加條目。

>[!TIP]
>
>請參閱下 [面的POM XML程式碼片段](#xml-container-package-filters) ，以取得完整的程式碼片段。

## 嵌入第三方軟體包 {#embedding-3rd-party-packages}

所有套件都必須透過 [Adobe的公用Maven物件存放庫](https://repo.adobe.com/nexus/content/groups/public/com/adobe/) ，或可存取的公用、參考的第三方Maven物件存放庫取得。

如果第三方套件位於 **Adobe的公用Maven工件存放庫**，則Adobe Cloud manager無需進一步設定即可解析工件。

如果第三方包位於公 **用的第三方Maven對象儲存庫**，則必須按照上述方法在項目中註冊並嵌入此存 `pom.xml` 儲庫 [](#embeddeds)。如果第三方應用程式/連接器同時需要程式碼和內容封裝，則每個應用程式/連接器都必須嵌入到容器(`all`)封裝中的正確位置。

添加Maven依賴項遵循標準Maven做法，上面概述了嵌入第三方對象(代碼和內容 [包)](#embedding-3rd-party-packages)。

>[!TIP]
>
>請參閱下 [面的POM XML程式碼片段](#xml-3rd-party-maven-repositories) ，以取得完整的程式碼片段。

## 來自包之間的包相 `ui.apps` 依性 `ui.content` 關係 {#package-dependencies}

為了確保軟體包的正確安裝，建議建立軟體包間相關性。

一般規則是包含可變內容(`ui.content`)的包，應取決於支援可變內容的轉換和使用的不可變內容(`ui.apps`)。

>[!TIP]
>
>請參閱下 [面的POM XML程式碼片段](#xml-package-dependencies) ，以取得完整的程式碼片段。

內容包依賴項的常見模式有：

### 簡單部署包依賴項 {#simple-deployment-package-dependencies}

簡單案例將可變內 `ui.content` 容包設定為依賴於不可 `ui.apps` 變代碼包。

+ `all` 沒有依賴性
   + `ui.apps` 沒有依賴性
   + `ui.content` depsions on `ui.apps`

### 複雜的部署包相關性 {#complex-deploxment-package-dependencies}

複雜的部署會根據簡單的情況展開，並設定對應可變內容與不可變代碼套件之間的相依性。 根據需要，也可以在不可變代碼包之間建立相依性。

+ `all` 沒有依賴性
   + `ui.apps.common` 沒有依賴性
   + `ui.apps.site-a` depsions on `ui.apps.common`
   + `ui.content.site-a` depsions on `ui.apps.site-a`
   + `ui.apps.site-b` depsions on `ui.apps.common`
   + `ui.content.site-b` depsions on `ui.apps.site-b`

## 本機開發與部署 {#local-development-and-deployment}

本文中概述的專案結構和組織完全相 **容於本機** 開發AEM實例。

## POM XML片段 {#pom-xml-snippets}

以下是Maven `pom.xml` 組態程式碼片段，可新增至Maven專案，以符合上述建議。

### 包類型 {#xml-package-types}

程式碼和內容封裝 (部署為子封裝) 必須依其包含的內容來宣告 **應用****程式或內容**&#x200B;的封裝類型。

#### 容器封裝類型 {#container-package-types}

容器專 `all/pom.xml` 案 **不會宣** 告 `<packageType>`。

#### 代碼（不可變）包類型 {#immutable-package-types}

代碼包必須將其 `packageType` 設定為 `application`。

在中，外 `ui.apps/pom.xml`掛程 `<packageType>application</packageType>` 式聲明的生成配置指 `filevault-package-maven-plugin` 令會聲明其軟體包類型。

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        <group>${project.groupId}</group>
        <name>${my-app.ui.apps}</name>
        <packageType>application</packageType>
        <accessControlHandling>merge</accessControlHandling>
        <properties>
          <cloudManagerTarget>none</cloudManagerTarget>
        </properties>
      </configuration>
    </plugin>
    ...
```

#### 內容（可變）包類型 {#mutable-package-types}

內容套件必須設 `packageType` 為 `content`。

在中， `ui.content/pom.xml`外掛程 `<packageType>content</packageType>` 式聲明的build configuration指令 `filevault-package-maven-plugin` 會聲明其軟體包類型。

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        <group>${project.groupId}</group>
        <name>${my-app.ui.content}</name>
        <packageType>content</packageType>
        <accessControlHandling>merge</accessControlHandling>
        <properties>
          <cloudManagerTarget>none</cloudManagerTarget>
        </properties>
      </configuration>
    </plugin>
    ...
```

### 標籤Adobe Cloud Manager部署的套件 {#cloud-manager-target}

在每個產生套件的專 **案中** ，除容器(`all`)專案外，將外掛程式聲明的 `<cloudManagerTarget>none</cloudManagerTarget>` 組態新增至外掛程式宣告的組態，以確 `<properties>``filevault-package-maven-plugin`**** 保Adobe Cloud Manager不會部署它們。THe容器(`all`)套件應是透過Cloud manager部署的單一套件，而Cloud manager又內嵌所有必要的程式碼和內容套件。

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        ...
        <properties>
          <cloudManagerTarget>none</cloudManagerTarget>
        </properties>
      </configuration>
    </plugin>
    ...
```

### 回購初始化{#snippet-repo-init}

包含回購初始化指令碼的回購初始化指令碼是通過屬性在 `RepositoryInitializer` OSGi工廠配置中定 `scripts` 義的。 請注意，由於這些指令碼是在OSGi配置中定義的，因此可以使用常規資料夾語義，通過運行模式輕鬆 `../config.<runmode>` 地確定其範圍。

請注意，由於指令碼通常是多行聲明，因此在檔案中定義它們比在XML `.config` 基礎格式中更容 `sling:OsgiConfig` 易。

`/apps/my-app/config.author/org.apache.sling.jcr.repoinit.RepositoryInitializer-author.config`

```plain
scripts=["
    create service user my-data-reader-service

    set ACL on /var/my-data
        allow jcr:read for my-data-reader-service
    end

    create path (sling:Folder) /conf/my-app/settings
"]
```

OSGi `scripts` 屬性包含 [Apache Sling&#39;s Repo Init語言所定義的指令](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language)。

### 儲存庫結構包 {#xml-repository-structure-package}

在聲明 `ui.apps/pom.xml` 代碼包( `pom.xml``<packageType>application</packageType>`)的和任何其它軟體包中，將以下儲存庫結構軟體包配置添加到FileVault Maven插件中。 您可以 [為項目建立自己的儲存庫結構包](repository-structure-package.md)。

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        ...
        <repositoryStructurePackages>
          <repositoryStructurePackage>
              <groupId>${project.groupId}</groupId>
              <artifactId>ui.apps.structure</artifactId>
              <version>${project.version}</version>
          </repositoryStructurePackage>
        </repositoryStructurePackages>
      </configuration>
    </plugin>
    ...
```

### 將子包嵌入容器包中 {#xml-embeddeds}

在中， `all/pom.xml`將以下指 `<embeddeds>` 令添加到插 `filevault-package-maven-plugin` 件聲明中。 請記 **住** ，請勿使 `<subPackages>` 用設定，因為這將包含子封裝， `/etc/packages` 而非 `/apps/my-app-packages/<application|content>/install(.author|.publish)?`。

```xml
...
<plugin>
  <groupId>org.apache.jackrabbit</groupId>
  <artifactId>filevault-package-maven-plugin</artifactId>
  <extensions>true</extensions>
  <configuration>
      ...
      <embeddeds>

          <!-- Include the application's ui.apps and ui.content packages -->
          <!-- Ensure the artifactIds are correct -->

          <!-- Code package that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.apps</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/application/install</target>
          </embedded>

          <!-- Code package that deploys ONLY to AEM Author -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.apps.author</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/application/install.author</target>
          </embedded>

          <!-- Content package that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.content</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/content/install</target>
          </embedded>

          <!-- Content package that deploys ONLY to AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.content.publish-only</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/content/install.publish</target>
          </embedded>

          <!-- Include any other extra packages such as AEM WCM Core Components -->
          <embedded>
              <groupId>com.adobe.cq</groupId>
              <!-- Not to be confused; WCM Core Components' Code package's artifact is named `.content` -->
              <artifactId>core.wcm.components.content</artifactId>
              <type>zip</type>
              <target>/apps/vendor-packages/application/install</target>
          </embedded>

          <embedded>
              <groupId>com.adobe.cq</groupId>
              <!-- Not to be confused; WCM Core Components' Content package's artifact is named `.conf` -->
              <artifactId>core.wcm.components.conf</artifactId>
              <type>zip</type>
              <target>/apps/vendor-packages/content/install</target>
          </embedded>
      <embeddeds>
  </configuration>
</plugin>
...
```

### 容器套件的篩選定義 {#xml-container-package-filters}

在項目 `all` 的( `filter.xml` )中，`all/src/main/content/jcr_root/META-INF/vault/definition/filter.xml`包 **含要部**`-packages` 署的子包的所有資料夾：

```xml
<filter root="/apps/my-app-packages"/>
```

如果嵌入 `/apps/*-packages` 目標中使用了多個，則必須在此處列舉這些目標。

### 第三方Maven儲存庫 {#xml-3rd-party-maven-repositories}

>[!WARNING]
> 添加更多Maven儲存庫可能會延長Maven構建時間，因為將檢查其他Maven儲存庫是否有派駐服務。

在反應堆項目的中，添 `pom.xml`加任何必要的第三方公共Maven儲存庫指令。 完整配 `<repository>` 置應可從第三方儲存庫提供方獲得。

```xml
<repositories>
  ...
  <repository>
      <id>3rd-party-repository</id>
      <name>Public 3rd Party Repository</name>
      <url>https://repo.3rdparty.example.com/...</url>
      <releases>
          <enabled>true</enabled>
          <updatePolicy>never</updatePolicy>
      </releases>
      <snapshots>
          <enabled>false</enabled>
      </snapshots>
  </repository>
  ...
</repositories>
```

### 來自包之間的包相 `ui.apps` 依性 `ui.content` 關係 {#xml-package-dependencies}

在中， `ui.content/pom.xml`將以下指 `<dependencies>` 令添加到插 `filevault-package-maven-plugin` 件聲明中。

```xml
...
<plugin>
  <groupId>org.apache.jackrabbit</groupId>
  <artifactId>filevault-package-maven-plugin</artifactId>
  <extensions>true</extensions>
  <configuration>
      ...
      <dependencies>
        <!-- Declare the content package dependency in the ui.content/pom.xml on the ui.apps project -->
        <dependency>
            <groupId${project.groupId}</groupId>
            <artifactId>my-app.ui.apps</artifactId>
            <version>${project.version}</version>
        </dependency>
      </dependencies>
    ...
  </configuration>
</plugin>
...
```

### 清除容器專案的目標資料夾 {#xml-clean-container-package}

在中添 `all/pom.xml` 加插件， `maven-clean-plugin` 該插件將在Maven構建之前清除目標目錄。

```xml
<plugins>
  ...
  <plugin>
    <artifactId>maven-clean-plugin</artifactId>
    <executions>
      <execution>
        <id>auto-clean</id>
        <!-- Run at the beginning of the build rather than the default, which is after the build is done -->
        <phase>initialize</phase>
        <goals>
          <goal>clean</goal>
        </goals>
      </execution>
    </executions>
  </plugin>
  ...
</plugins>
```

## 其他資源 {#additional-resources}

+ [使用Maven管理包](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/vlt-mavenplugin.html)
+ [FileVault Content Package Maven Plug-in](http://jackrabbit.apache.org/filevault-package-maven-plugin/)