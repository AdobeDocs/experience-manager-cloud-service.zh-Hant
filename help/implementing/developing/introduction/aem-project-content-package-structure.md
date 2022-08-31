---
title: AEM 專案結構
description: 瞭解如何定義部署到Adobe Experience ManagerCloud Service的包結構。
exl-id: 38f05723-5dad-417f-81ed-78a09880512a
source-git-commit: 430179bf13c1fff077c515eed0676430e9e7f341
workflow-type: tm+mt
source-wordcount: '2930'
ht-degree: 13%

---

# AEM 專案結構

>[!TIP]
>
>熟悉基本 [項AEM目原型使用](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)的 [FileVault內容管理插件](/help/implementing/developing/tools/maven-plugin.md) 因為本文是以這些學習和概念為基礎的。

本文概述了Adobe Experience ManagerMaven項目所需的變化AEM，這些變化要as a Cloud Service相容，要確保它們尊重可變和不可變內容的分割，建立依賴關係以建立不衝突、確定性部署，並將它們打包成可部署結構。

應AEM用程式部署必須由單個AEM包組成。 此包應包含子包，這些子包包含應用程式運行所需的所有內容，包括代碼、配置和任何支援的基線內容。

AEM需要分離內 **容和程式碼** ，這表示單一內容套件 **無法**&#x200B;部署至 ********`/apps` Runtime可寫區域 (例如，可寫區域)。`/content`、 `/conf`、 `/home`或其他非 `/apps`)。而應用程式必須將程式碼和內容分隔為獨立套件，以便部署至AEM。

本檔案中概述的套件結構與本機開 **發部署** 和AEM cloud服務部署都相容。

>[!TIP]
>
>本文檔中概述的配置由 [馬文AEM原型24或更高版本](https://github.com/adobe/aem-project-archetype/releases)。

## 儲存庫的可變區與不可變區 {#mutable-vs-immutable}

`/apps` and `/libs`**are consed inmumable areas of AEM as they cannot be changed(create, update, delete)after AEM starts(i.e. at runtime)。**&#x200B;在運行時更改不可變區域的任何嘗試都將失敗。

儲存庫里的其他一切， `/content`。 `/conf`。 `/var`。 `/etc`。 `/oak:index`。 `/system`。 `/tmp`的子菜單。 全部 **可變** 區域，即可以在運行時更改這些區域。

>[!WARNING]
>
>與以前版本AEM一樣， `/libs` 不應修改。 只AEM能將產品代碼部署到 `/libs`。

### 橡樹索引 {#oak-indexes}

橡樹索引(`/oak:index`)由as a Cloud Service部署進AEM程專門管理。 這是因為Cloud Manager必須等待任何新索引部署完畢並重新編製索引後才能切換到新代碼映像。

因此，儘管Oak索引在運行時是可變的，但必須將其部署為代碼，以便在安裝任何可變的軟體包之前可以安裝它們。 因此 `/oak:index` 配置是代碼包的一部分，而不是內容包的一部分 [如下所述](#recommended-package-structure)。

>[!TIP]
>
>有關在as a Cloud Service中索引的AEM詳細資訊，請參閱文檔 [內容搜索和索引](/help/operations/indexing.md)。

## 推薦的包結構 {#recommended-package-structure}

![Experience Manager項目包結構](assets/content-package-organization.png)

此圖概述了建議的項目結構和包部署對象。

建議的應用程式部署結構如下：

### 代碼包/OSGi捆綁包

+ 生成OSGi捆綁Jar檔案，並直接嵌入到所有項目中。

+ 的 `ui.apps` 包包含要部署的所有代碼，且僅部署到 `/apps`。 的常用元素 `ui.apps` 包括但不限於：
   + [元件定義和HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=zh-Hant) 指令碼
      + `/apps/my-app/components`
   + JavaScript和CSS(通過 [客戶端庫](/help/implementing/developing/introduction/clientlibs.md))
      + `/apps/my-app/clientlibs`
   + [覆蓋](/help/implementing/developing/introduction/overlays.md) 共 `/libs`
      + `/apps/cq`。 `/apps/dam/`的子菜單。
   + 回退上下文感知配置
      + `/apps/settings`
   + ACL（權限）
      + 任意 `rep:policy` 對於任何路徑 `/apps`
   + [預編譯的捆綁指令碼](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/precompiled-bundled-scripts.html)

>[!NOTE]
>
>必須將相同的代碼部署到所有環境。 這是為了確保在階段環境上的可信度驗證也在生產中所必需的。 有關詳細資訊，請參閱 [運行模式](/help/implementing/deploying/overview.md#runmodes)。


### 內容包

+ 的 `ui.content` 包包含所有內容和配置。 內容包包含不在 `ui.apps` 或 `ui.config` 或者換句話說，任何 `/apps` 或 `/oak:index`。 的常用元素 `ui.content` 包括但不限於：
   + 上下文感知配置
      + `/conf`
   + 必需的複雜內容結構(即 在回購初始化中定義的基線內容結構基礎上構建並擴展到其以後的內容構建。)
      + `/content`。 `/content/dam`的子菜單。
   + 受管制的標籤分類
      + `/content/cq:tags`
   + 舊式等節點（理想情況下，將這些節點遷移到非/等位置）
      + `/etc`

### 容器包

+ 的 `all` 包是一個容器包，它只包括可部署的對象、 OSGI捆綁包Jar檔案、 `ui.apps`。 `ui.config` 和 `ui.content` 包裝。 的 `all` 包不能 **任何內容或代碼** 將所有部署委託到儲存庫的子包或OSGi捆綁Jar檔案。

   現在，包已使用Maven [FileVault包Maven插件的嵌入式配置](#embeddeds)，而不是 `<subPackages>` 配置。

   對於複雜的Experience Manager部署，建立多個 `ui.apps`。 `ui.config` 和 `ui.content` 表示中特定站點或租戶的項目/包AEM。 如果執行此操作，請確保可變內容和不可變內容之間的拆分得到尊重，並且所需的內容包和OSGi捆綁包Jar檔案作為子包嵌入到 `all` 容器內容包。

   例如，複雜的部署內容包結構可能如下所示：

   + `all` 內容包嵌入以下包，以建立單一部署對象
      + `common.ui.apps` 部署所需代碼 **兩者** 站點A和站點B
      + `site-a.core` 站點A需要的OSGi捆綁Jar
      + `site-a.ui.apps` 部署站點A所需的代碼
      + `site-a.ui.config` 部署站點A所需的OSGi配置
      + `site-a.ui.content` 部署站點A所需的內容和配置
      + `site-b.core` 站點B需要的OSGi捆綁Jar
      + `site-b.ui.apps` 部署站點B所需的代碼
      + `site-b.ui.config` 部署站點B所需的OSGi配置
      + `site-b.ui.content` 部署站點B所需的內容和配置

+ 的 `ui.config` 包包含所有 [OSGi配置](/help/implementing/deploying/configuring-osgi.md):
   + 已考慮的代碼，屬於OSGi捆綁包，但不包含常規內容節點。 因此，它被標籤為容器包裝
   + 包含特定於運行模式的OSGi配置定義的組織資料夾
      + `/apps/my-app/osgiconfig`
   + 公用OSGi配置資料夾，包含適用於所有目標as a Cloud Service部署目標的AEM預設OSGi配置
      + `/apps/my-app/osgiconfig/config`
   + 運行特定於模式的OSGi配置資料夾，該資料夾包含適用於所有目標as a Cloud Service部署目標的AEM預設OSGi配置
      + `/apps/my-app/osgiconfig/config.<author|publish>.<dev|stage|prod>`
   + 回購初始化OSGi配置指令碼
      + [回購初始化](#repo-init) 是部署（可變）內容的推薦方AEM法。 Repo Init OSGi配置應位於適當的位置 `config.<runmode>` 資料夾，用於定義：
         + 基線內容結構
         + 使用者
         + 服務用戶
         + 群組
         + ACL（權限）

### 額外的應用程式套件{#extra-application-packages}

如果部AEM署使用其他項目（這些項目本身由它們自己的代碼和內容包組成）AEM，則應將其容器包嵌入項目 `all` 檔案。

例如，包含AEM2個供應商應用程AEM序的項目可能如下：

+ `all` 內容包嵌入以下包，以建立單一部署對象
   + `core` 應用程式需要的OSGi捆綁AEMJar
   + `ui.apps` 部署應用程式所需的代AEM碼
   + `ui.config` 部署應用程式所需的OSGi配AEM置
   + `ui.content` 部署應用程式所需的內容和AEM配置
   + `vendor-x.all` 部署供應商X應用程式所需的所有內容（代碼和內容）
   + `vendor-y.all` 部署供應商Y應用程式所需的所有內容（代碼和內容）

## 包類型 {#package-types}

將使用其聲明的包類型標籤包。 包類型有助於闡明包的用途和部署。

+ 容器包必須設定 `packageType` 至 `container`。 容器包不能包含常規節點。 僅允許OSGi捆綁包、配置和子包。 不允AEM許as a Cloud Service中的容器 [安裝掛接](https://jackrabbit.apache.org/filevault/installhooks.html)。
+ 代碼（不可變）包必須設定 `packageType` 至 `application`。
+ 內容（可變）包必須設定其 `packageType` 至 `content`。


有關詳細資訊，請參閱 [Apache Jackrabbit FileVault — 包Maven插件文檔](https://jackrabbit.apache.org/filevault-package-maven-plugin/package-mojo.html#packageType)。 [Apache Jackrabbit包類型](https://jackrabbit.apache.org/filevault/packagetypes.html)的 [FileVault Maven配置段](#marking-packages-for-deployment-by-adoube-cloud-manager) 下。

>[!TIP]
>
>查看 [POM XML片段](#xml-package-types) 的子目錄。

## 通過Adobe雲管理器標籤要部署的包 {#marking-packages-for-deployment-by-adoube-cloud-manager}

依預設，Adobe Cloud manager會收集由Maven組建版本產生的所有套件，但是，由於容器(`all`)套件是包含所有程式碼和內容套件的單一部署工件，因此我們必須確保僅部署容器( ****`all`)套件。為確保此，Maven構建版本生成的其他軟體包必須用的FileVault Content Package Maven插件配置進行標籤 `<properties><cloudManagerTarget>none</cloudManageTarget></properties>`。

>[!TIP]
>
>查看 [POM XML片段](#pom-xml-snippets) 的子目錄。

## 回購初始化{#repo-init}

回購初始化提供了定義JCR結構的說明或指令碼，這些結構從資料夾樹等常見節點結構到用戶、服務用戶、組和ACL定義。

回購初始化的主要好處是，它們具有執行其指令碼定義的所有操作的隱式權限，並在部署生命週期的早期調用，以確保在執行時間代碼時存在所有必需的JCR結構。

而Repo Init指令碼本身位於 `ui.config` 項目作為指令碼，它們可以且應用於定義以下可變結構：

+ 基線內容結構
+ 服務用戶
+ 使用者
+ 群組
+ ACL

回購初始化指令碼儲存為 `scripts` 條目 `RepositoryInitializer` 因此，OSGi工廠配置可以通過運行模式隱式定向，從而允許AEM Author和AEM Publish Services的Repo Init指令碼之間，甚至環境（Dev、Stage和Prod）之間的差異。

最好在 [`.config` OSGi配置格式](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-config-1) 因為它們支援多行，這是使用 [`.cfg.json` 定義OSGi配置](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1)。

請注意，在定義「用戶」和「組」時，只有組被視為應用程式的一部分，並且應在此處定義其功能的整體。 組織用戶和組仍應在運行時定義AEM;例如，如果自定義工作流將工作分配給指定組，則應通過應用程式中的回購初始化在中定義該組AEM，但是，如果分組只是組織性的，如「Wendy&#39;s Team」和「Sean&#39;s Team」，則這些工作最好在運行時進行定義和管AEM理。

>[!TIP]
>
>回購初始化指令碼 *必須* 在行內定義 `scripts` 的 `references` 配置無法工作。

Repo Init指令碼的完整辭彙可在 [Apache Sling Repo初始化文檔](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language)。

>[!TIP]
>
>查看 [回購初始化代碼段](#snippet-repo-init) 的子目錄。

## 儲存庫結構包 {#repository-structure-package}

代碼包要求配置FileVault Maven插件的配置以引用 `<repositoryStructurePackage>` 強制實施結構依賴項的正確性（以確保一個代碼包不會安裝在另一個代碼包上）。 你可以 [為項目建立自己的儲存庫結構包](repository-structure-package.md)。

這只是程 **式碼套件的必要** ，也就是任何標有的套件 `<packageType>application</packageType>`。

要瞭解如何為應用程式建立儲存庫結構包，請參見 [開發儲存庫結構包](repository-structure-package.md)。

注意內容包(`<packageType>content</packageType>`) **不** 需要此儲存庫結構包。

>[!TIP]
>
>查看 [POM XML片段](#xml-repository-structure-package) 的子目錄。

## 將子套件內嵌於容器套件{#embeddeds}

內容或代碼包被放在特殊的「側車」資料夾中，並可以以FileVault Maven插件的AEM作者、AEM發佈或兩者同時安裝為目標 `<embeddeds>` 配置。 請注意 `<subPackages>` 不應使用配置。

常見使用情形包括：

+ 作者用戶和發佈用AEM戶之間不AEM同的ACL
+ 僅用於支援作者活動的配AEM置
+ 代碼（如與後台系統的整合），僅需在作者上運AEM行

![嵌入包](assets/embeddeds.png)

要針對作AEM者、發AEM布或兩者，將包嵌入到 `all` 容器包，格式如下：

`/apps/<app-name>-packages/(content|application|container)/install(.author|.publish)?`

分解此資料夾結構：

+ 第1級資料夾 **必須** `/apps`。
+ 第2級資料夾表示 `-packages` 後固定到資料夾名。 通常只有一個第2級資料夾所有子包都嵌入在下面，但是可以建立任意數量的第2級資料夾以最好地表示應用程式的邏輯結構：
   + `/apps/my-app-packages`
   + `/apps/my-other-app-packages`
   + `/apps/vendor-packages`

   >[!WARNING]
   >
   >根據慣例，子包嵌入資料夾的名稱為尾碼為 `-packages`。這可確保部署代碼和內容包 **未部署** ，而是不會部署任何子包的目標資料夾， `/apps/<app-name>/...` 從而導致破壞性和循環安裝行為。

+ 第3級資料夾必須是
   `application`, `content` 或 `container`
   + 的 `application` 資料夾包含代碼包
   + 的 `content` 資料夾包含內容包
   + 的 `container` 資料夾包含 [額外的應用程式套件](#extra-application-packages) 可能包含在應用程式AEM中。
此資料夾名稱與 [包類型](#package-types) 包含的包。
+ 第4層資料夾包含子包，且必須是下列其中一個：
   + `install` 若要同時安裝 **在** AEM作者和AEM發佈上
   + `install.author` 僅 **安裝** 在AEM作者上
   + `install.publish` 至 **僅** 在發佈AEM時安裝，僅 `install.author` 和 `install.publish` 是支援的目標。 不支援其 **他執行模** 式。

例如，包含作者和發佈AEM特定包的部署可能如下所示：

+ `all` 容器包嵌入以下包，以建立單一的部署項目
   + `ui.apps` 嵌入 `/apps/my-app-packages/application/install` 將代碼部署到AEM作者和AEM發佈
   + `ui.apps.author` 嵌入 `/apps/my-app-packages/application/install.author` 僅將代碼部署到AEM作者
   + `ui.content` 嵌入 `/apps/my-app-packages/content/install` 將內容和配置部署到AEM作者和AEM發佈
   + `ui.content.publish` 嵌入 `/apps/my-app-packages/content/install.publish` 只發佈內容和配AEM置

>[!TIP]
>
>查看 [POM XML片段](#xml-embeddeds) 的子目錄。

### 容器包的篩選器定義 {#container-package-filter-definition}

由於代碼和內容子包嵌入到容器包中，因此必須將嵌入的目標路徑添加到容器項目的 `filter.xml` 確保在構建時將嵌入的包包含在容器包中。

只需添加 `<filter root="/apps/<my-app>-packages"/>` 包含要部署的子包的任何第2級資料夾的條目。

>[!TIP]
>
>查看 [POM XML片段](#xml-container-package-filters) 的子目錄。

## 嵌入第三方包 {#embedding-3rd-party-packages}

所有包都必須通過 [Adobe的公共馬文藏物庫](https://repo1.maven.org/maven2/com/adobe/) 或可訪問的可參考的第三方Maven人工資料庫。

如果第三方套件位於 **Adobe的公用Maven工件存放庫**，則Adobe Cloud manager無需進一步設定即可解析工件。

如果第三方包位於公 **用的第三方Maven對象儲存庫**，則必須按照上述方法在項目中註冊並嵌入此存 `pom.xml` 儲庫 [](#embeddeds)。

第三方應用程式/連接器應使用其 `all` 包作為項目容器(`all`)包。

添加Maven依賴項遵循標準Maven做法，並嵌入第三方對象（代碼和內容包） [概述](#embedding-3rd-party-packages)。

>[!TIP]
>
>查看 [POM XML片段](#xml-3rd-party-maven-repositories) 的子目錄。

## 以下項之間的包依賴項 `ui.apps` 從 `ui.content` 包 {#package-dependencies}

為了確保正確安裝軟體包，建議建立軟體包間依賴關係。

一般規則是包含可變內容(`ui.content`)應依賴於不可變代碼(`ui.apps`)支援可變內容的呈現和使用。

此一般規則的一個顯著例外是，如果不可變代碼包(`ui.apps` 或其他任何), __僅__ 包含OSGi捆綁包。 如果是，則AEM不應聲明對它的依賴。 這是因為不可變的代碼包 __僅__ 包含未註冊到的OSGi捆AEM綁 [包管理器，](/help/implementing/developing/tools/package-manager.md) 因此，任AEM何依賴它的軟體包都將具有未滿足的依賴關係，並且無法安裝。

>[!TIP]
>
>查看 [POM XML片段](#xml-package-dependencies) 的子目錄。

內容包依賴項的常見模式有：

### 簡單部署包依賴項 {#simple-deployment-package-dependencies}

簡單的事例設定 `ui.content` 可變的內容包取決於 `ui.apps` 不可變代碼包。

+ `all` 沒有依賴項
   + `ui.apps` 沒有依賴項
   + `ui.content` 取決於 `ui.apps`

### 複雜部署包依賴項 {#complex-deploxment-package-dependencies}

複雜部署會根據簡單情況展開，並設定相應可變內容和不可變代碼包之間的依賴關係。 根據需要，還可以在不可變代碼包之間建立依賴項。

+ `all` 沒有依賴項
   + `common.ui.apps.common` 沒有依賴項
   + `site-a.ui.apps` 取決於 `common.ui.apps`
   + `site-a.ui.content` 取決於 `site-a.ui.apps`
   + `site-b.ui.apps` 取決於 `common.ui.apps`
   + `site-b.ui.content` 取決於 `site-b.ui.apps`

## 本地開發和部署 {#local-development-and-deployment}

本文概述的項目結構和組織 **完全相容** 本地開發AEM實例。

## POM XML片段 {#pom-xml-snippets}

以下是馬文 `pom.xml` 可添加到Maven項目中以符合上述建議的配置片段。

### 包類型 {#xml-package-types}

程式碼和內容封裝 (部署為子封裝) 必須依其包含的內容來宣告 **應用****程式或內容**&#x200B;的封裝類型。

#### 容器包類型 {#container-package-types}

容器 `all/pom.xml` 項目 **不** 宣佈 `<packageType>`。

#### 代碼（不可變）包類型 {#immutable-package-types}

代碼包必須設定 `packageType` 至 `application`。

在 `ui.apps/pom.xml`，也請參見Wiki頁。 `<packageType>application</packageType>` 生成配置指令 `filevault-package-maven-plugin` plugin聲明聲明其包類型。

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
        <name>my-app.ui.apps</name>
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

內容包必須設定 `packageType` 至 `content`。

在 `ui.content/pom.xml`，也請參見Wiki頁。 `<packageType>content</packageType>` 生成配置指令 `filevault-package-maven-plugin` plugin聲明聲明其包類型。

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
        <name>my-app.ui.content</name>
        <packageType>content</packageType>
        <accessControlHandling>merge</accessControlHandling>
        <properties>
          <cloudManagerTarget>none</cloudManagerTarget>
        </properties>
      </configuration>
    </plugin>
    ...
```

### 標籤用於Adobe雲管理器部署的包 {#cloud-manager-target}

在每個產生套件的專 **案中** ，除容器(`all`)專案外，將外掛程式聲明的 `<cloudManagerTarget>none</cloudManagerTarget>` 組態新增至外掛程式宣告的組態，以確 `<properties>``filevault-package-maven-plugin`**** 保Adobe Cloud Manager不會部署它們。容器(`all`)包應是通過Cloud Manager部署的單個包，而Cloud Manager則嵌入所有所需的代碼和內容包。

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

包含回購初始化指令碼的回購初始化指令碼在 `RepositoryInitializer` OSGi出廠配置 `scripts` 屬性。 請注意，由於這些指令碼是在OSGi配置中定義的，因此可以使用通常的運行模式輕鬆地確定它們的範圍 `../config.<runmode>` 資料夾語義。

請注意，由於指令碼通常是多行聲明，因此在 `.config` 檔案，而不是基於JSON的檔案 `.cfg.json` 的子菜單。

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

的 `scripts` OSGi屬性包含由 [Apache Sling的Repo Init語言](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language)。

### 儲存庫結構包 {#xml-repository-structure-package}

在 `ui.apps/pom.xml` 和 `pom.xml` 聲明代碼包(`<packageType>application</packageType>`)，將以下儲存庫結構包配置添加到FileVault Maven插件。 你可以 [為項目建立自己的儲存庫結構包](repository-structure-package.md)。

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

### 將子套件內嵌於容器套件 {#xml-embeddeds}

在 `all/pom.xml`，添加以下內容 `<embeddeds>` 對 `filevault-package-maven-plugin` 插件聲明。 記住， **不** 使用 `<subPackages>` 配置，因為這將包括 `/etc/packages` 而 `/apps/my-app-packages/<application|content|container>/install(.author|.publish)?`。

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

          <!-- OSGi Bundle Jar file that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.core</artifactId>
              <type>jar</type>
              <target>/apps/my-app-packages/application/install</target>
          </embedded>

          <!-- Code package that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.apps</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/application/install</target>
          </embedded>

           <!-- OSGi configuration code package that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.config</artifactId>
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

          <!-- Include any other extra packages  -->
          <embedded>
              <groupId>com.vendor.x</groupId>
              <artifactId>vendor.plug-in.all</artifactId>
              <type>zip</type>
              <target>/apps/vendor-packages/container/install</target>
          </embedded>
      <embeddeds>
  </configuration>
</plugin>
...
```

### 容器包的篩選器定義 {#xml-container-package-filters}

在項目 `all` 的( `filter.xml` )中，`all/src/main/content/jcr_root/META-INF/vault/definition/filter.xml`包 **含要部**`-packages` 署的子包的所有資料夾：

```xml
<filter root="/apps/my-app-packages"/>
```

如果為多 `/apps/*-packages` 在嵌入的目標中使用，則必須在此處枚舉所有目標。

### 第三方Maven儲存庫 {#xml-3rd-party-maven-repositories}

>[!WARNING]
>
>添加更多Maven儲存庫可能會延長主生成時間，因為將檢查其他Maven儲存庫是否存在依賴項。

在反應堆工程中 `pom.xml`，添加任何必要的第三方公共Maven儲存庫指令。 滿 `<repository>` 配置應可從第三方儲存庫提供程式獲得。

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

### 以下項之間的包依賴項 `ui.apps` 從 `ui.content` 包 {#xml-package-dependencies}

在 `ui.content/pom.xml`，添加以下內容 `<dependencies>` 對 `filevault-package-maven-plugin` 插件聲明。

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

### 清除容器項目的目標資料夾 {#xml-clean-container-package}

在 `all/pom.xml` 添加 `maven-clean-plugin` 插件，該插件將清除Maven生成之前的目標目錄。

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

+ [使用Maven管理包](/help/implementing/developing/tools/maven-plugin.md)
+ [FileVault內容包主插件](https://jackrabbit.apache.org/filevault-package-maven-plugin/)
