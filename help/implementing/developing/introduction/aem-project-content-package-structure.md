---
title: AEM 專案結構
description: 瞭解如何定義部署至Adobe Experience ManagerCloud Service的套件結構。
exl-id: 38f05723-5dad-417f-81ed-78a09880512a
translation-type: tm+mt
source-git-commit: 800c6db7fed43d706dcf1c26235b2f88ed0a5b62
workflow-type: tm+mt
source-wordcount: '2873'
ht-degree: 13%

---

# AEM 專案結構

>[!TIP]
>
>請熟悉基本的[AEM Project Archetype use](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/developing/archetype/overview.html)和[FileVault Content Maven Plug-in](/help/implementing/developing/tools/maven-plugin.md)，因為本文以這些學習和概念為基礎。

本文概述了Adobe Experience Manager馬文項目作為Cloud Service相容項所需的變化AEM，通過確保它們遵守可變內容和不可變內容的分割，建立依賴項以建立不衝突、確定性的部署，並將它們封裝在可部署結構中。

應AEM用程式部署必須由單一套件AEM組成。 此套件應包含子套件，這些子套件包含應用程式運作所需的一切，包括程式碼、組態和任何支援的基準內容。

AEM需要分離內 **容和程式碼** ，這表示單一內容套件 **無法**&#x200B;部署至 ********`/apps` Runtime可寫區域 (例如，可寫區域)。`/content`、 `/conf`、 `/home`或其他非 `/apps`)。而應用程式必須將程式碼和內容分隔為獨立套件，以便部署至AEM。

本檔案中概述的套件結構與本機開 **發部署** 和AEM cloud服務部署都相容。

>[!TIP]
>
>本文中概述的配置由[AEM Project Maven Archetype 24或更高版本](https://github.com/adobe/aem-project-archetype/releases)提供。

## 儲存庫的可變區與不可變區{#mutable-vs-immutable}

`/apps` and `/libs`**are consed inmumable areas of AEM as they cannot be changed(create, update, delete)after AEM starts(i.e. at runtime)。**&#x200B;在運行時更改不可變區域的任何嘗試都將失敗。

儲存庫中的其它所有內容，如`/content`、`/conf`、`/var`、`/etc`、`/oak:index`、`/system`、`/tmp`等。 皆為&#x200B;**mutable**&#x200B;區域，這表示這些區域可在執行時期變更。

>[!WARNING]
>
>與舊版一AEM樣，`/libs`不應修改。 只有AEM產品代碼可部署至`/libs`。

### Oak Indexes {#oak-indexes}

Oak索引(`/oak:index`)是由作為Cloud Service部AEM署過程專門管理的。 這是因為Cloud Manager必須等到部署任何新索引並完全重新建立索引後，才能切換到新的代碼映像。

因此，雖然Oak索引在運行時是可變的，但必須將其部署為代碼，以便在安裝任何可變軟體包之前安裝它們。 因此，`/oak:index`組態是程式碼套件的一部分，而不是內容套件[的一部分，如下所述](#recommended-package-structure)。

>[!TIP]
>
>有關以Cloud Service形式AEM在中建立索引的詳細資訊，請參閱檔案[內容搜尋與索引](/help/operations/indexing.md)。

## 建議的包結構{#recommended-package-structure}

![Experience Manager項目包結構](assets/content-package-organization.png)

此圖概述了建議的項目結構和包部署對象。

建議的應用程式部署結構如下：

### 代碼包/ OSGi捆綁包

+ 將生成OSGi捆綁Jar檔案，並直接嵌入到所有項目中。

+ `ui.apps`軟體包包含要部署的所有代碼，並僅部署到`/apps`。 `ui.apps`軟體包的常見元素包括，但不限於：
   + [元件定義與](https://docs.adobe.com/content/help/zh-Hant/experience-manager-htl/using/overview.html) HTLscripts
      + `/apps/my-app/components`
   + JavaScript和CSS（透過[用戶端程式庫](/help/implementing/developing/introduction/clientlibs.md)）
      + `/apps/my-app/clientlibs`
   + [覆](/help/implementing/developing/introduction/overlays.md) 蓋  `/libs`
      + `/apps/cq`、 `/apps/dam/`等。
   + 備援內容感知組態
      + `/apps/settings`
   + ACL（權限）
      + `/apps`下任何路徑的`rep:policy`

+ `ui.config`軟體包包含所有[OSGi配置](/help/implementing/deploying/configuring-osgi.md):
   + 包含特定於運行模式的OSGi配置定義的組織資料夾
      + `/apps/my-app/osgiconfig`
   + 通用OSGi配置資料夾，包含預設OSGi配置，這些配置作為Cloud Service部署目標應AEM用於所有目標
      + `/apps/my-app/osgiconfig/config`
   + 運行特定於模式的OSGi配置資料夾，該資料夾包含預設的OSGi配置，這些配置適用於所有目標，AEM作為Cloud Service部署目標
      + `/apps/my-app/osgiconfig/config.<author|publish>.<dev|stage|prod>`
   + 回購初始化OSGi配置指令碼
      + [回購](#repo-init) 性視網膜炎是部署（可變）內容（邏輯上是應用程式一部分）的推薦AEM方式。Repo Init OSGi配置應如上所述放置在相應的`config.<runmode>`資料夾中，並用於定義：
         + 基線內容結構
         + 使用者
         + 服務使用者
         + 群組
         + ACL（權限）

>[!NOTE]
>
>必須將相同的程式碼部署至所有環境。 為確保在生產階段環境上進行可信度驗證，需要這樣做。 如需詳細資訊，請參閱[回滾的保守編碼](/help/implementing/deploying/overview.md#conservative-coding-for-rollbacks)。


### 內容套件

+ `ui.content`套件包含所有內容和設定。 「內容套件」包含`ui.apps`或`ui.config`套件中未包含的所有節點定義，換言之，包含`/apps`或`/oak:index`中未包含的任何內容。 `ui.content`軟體包的常見元素包括，但不限於：
   + 內容感知配置
      + `/conf`
   + 必要、複雜的內容結構(即 內容構建以回購初始化中定義的基線內容結構為基礎，並將其擴展到基準內容結構。)
      + `/content`、 `/content/dam`等。
   + 受管理的標籤分類
      + `/content/cq:tags`
   + 舊式等節點（理想情況下，將這些節點遷移到非／等位置）
      + `/etc`

### 容器封裝

+ `all`套件是容器套件，僅包含可部署的工件、OSGI套件Jar檔案、`ui.apps`、`ui.config`和`ui.content`套件。 `all`軟體包不得具有&#x200B;**任何內容或代碼**，而是將所有部署到儲存庫的子軟體包或OSGi包Jar檔案。

   現在，軟體包是使用Maven [FileVault Package Maven插件的嵌入式配置](#embeddeds)而不是`<subPackages>`配置來包含的。

   對於複雜的Experience Manager部署，可能需要建立多個`ui.apps`、`ui.config`和`ui.content`項目／包，這些項目／包代表中的特定站點或租戶AEM。 如果完成此操作，請確保可變內容和不可變內容之間的分割得到尊重，並且所需的內容包和OSGi捆綁Jar檔案將作為子包嵌入`all`容器內容包中。

   例如，複雜的部署內容套件結構可能如下所示：

   + `all` 內容套件內嵌下列套件，以建立單一部署工件
      + `common.ui.apps` 部署站點A和站 **** 點B所需的代碼
      + `site-a.core` 站點A需要的OSGi捆綁Jar
      + `site-a.ui.apps` 部署站點A所需的代碼
      + `site-a.ui.config` 部署站點A所需的OSGi配置
      + `site-a.ui.content` 部署站點A所需的內容和配置
      + `site-b.core` 站點B需要的OSGi捆綁Jar
      + `site-b.ui.apps` 部署站點B所需的代碼
      + `site-b.ui.config` 部署站點B所需的OSGi配置
      + `site-b.ui.content` 部署站點B所需的內容和配置

### 額外應用程式套件{#extra-application-packages}

如果部AEM署使用其他項目（本身由自己的代碼和內容包組成）AEM，則其容器包應嵌入項目的`all`包中。

例如，包含2AEM個供應商應用程AEM式的專案可能如下：

+ `all` 內容套件內嵌下列套件，以建立單一部署工件
   + `core` 應用程式需要的OSGi搭AEM售Jar
   + `ui.apps` 部署應用程式所需的程AEM式碼
   + `ui.config` 部署應用程式所需的OSGiAEM配置
   + `ui.content` 部署應用程式所需的內容和配AEM置
   + `vendor-x.all` 部署供應商X應用程式所需的一切（程式碼和內容）
   + `vendor-y.all` 部署供應商Y應用程式所需的一切（程式碼和內容）

## 包類型{#package-types}

包將用其聲明的包類型標籤。

+ 容器封裝必須將其`packageType`設為`container`。 容器包不能直接包含OSGi捆綁包、OSGi配置，也不能使用[安裝掛接](http://jackrabbit.apache.org/filevault/installhooks.html)。
+ 代碼（不可變）包必須將其`packageType`設定為`application`。
+ 內容（可變）包必須將其`packageType`設定為`content`。


如需詳細資訊，請參閱下方的[Apache Jackrabbit FileVault - Package Maven Plugin檔案](https://jackrabbit.apache.org/filevault-package-maven-plugin/package-mojo.html#packageType)和[FileVault Maven組態程式碼片段](#marking-packages-for-deployment-by-adoube-cloud-manager)。

>[!TIP]
>
>有關完整的程式碼片段，請參閱下面的[POM XML程式碼片段](#xml-package-types)一節。

## 使用Adobe雲管理器{#marking-packages-for-deployment-by-adoube-cloud-manager}標籤要部署的包

依預設，Adobe Cloud manager會收集由Maven組建版本產生的所有套件，但是，由於容器(`all`)套件是包含所有程式碼和內容套件的單一部署工件，因此我們必須確保僅部署容器( ****`all`)套件。為確保此，Maven構建版本生成的其他軟體包必須用的FileVault Content Package Maven插件配置進行標籤 `<properties><cloudManagerTarget>none</cloudManageTarget></properties>`。

>[!TIP]
>
>有關完整的程式碼片段，請參閱下面的[POM XML程式碼片段](#pom-xml-snippets)一節。

## 回購初始化{#repo-init}

Repo Init提供了定義JCR結構的指令或指令碼，這些結構從常見的節點結構（如資料夾樹）到用戶、服務用戶、組和ACL定義。

回購初始化的主要優點是，它們具有執行其指令碼定義的所有操作的隱式權限，並且在部署生命週期的早期被調用，以確保在執行時間代碼時存在所有必需的JCR結構。

雖然Repo Init指令碼本身作為指令碼在`ui.config`項目中生存，但它們可以而且應該用於定義以下可變結構：

+ 基線內容結構
+ 服務使用者
+ 使用者
+ 群組
+ ACL

回購初始化指令碼會儲存為`RepositoryInitializer` OSGi工廠組態的`scripts`項目，因此可透過執行模式隱式定位，允許AEM作者與AEM Publish Services的回購初始化指令碼之間，或甚至是環境（開發、階段與產品）之間的差異。

回購初始化OSGi配置以[`.config` OSGi配置格式](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-config-1)寫得最好，因為它們支援多行，這是使用[`.cfg.json`定義OSGi配置](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1)的最佳做法的例外。

請注意，在定義「使用者」和「群組」時，只有群組會視為應用程式的一部分，而且應在此處定義其功能的整數。 組織使用者和群組仍應在執行時期中定義AEM;例如，如果自訂工作流程將工作指派給指名的群組，則該群組應透過應用程式中的回購初始化定義AEM，但如果群組僅是組織性的，例如「Wendy&#39;s Team」和「Sean&#39;s Team」，則這些工作最好定義，並在執行時期中加以管AEM理。

>[!TIP]
>
>回購初始化指令碼&#x200B;*必須*&#x200B;定義在內嵌`scripts`欄位中，並且`references`配置將無法工作。

[Apache Sling Repo Init檔案](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language)中提供回購初始指令碼的完整辭彙。

>[!TIP]
>
>有關完整的代碼片段，請參見下面的[回購初始化代碼片段](#snippet-repo-init)部分。

## 儲存庫結構包{#repository-structure-package}

代碼包要求將FileVault Maven插件的配置配置為引用`<repositoryStructurePackage>` ，以強制實施結構依賴性的正確性（以確保一個代碼包不會安裝在另一個代碼包上）。 您可以[為項目](repository-structure-package.md)建立自己的儲存庫結構包。

這只是程 **式碼套件的必要** ，也就是任何標有的套件 `<packageType>application</packageType>`。

要瞭解如何為應用程式建立儲存庫結構包，請參閱[開發儲存庫結構包](repository-structure-package.md)。

請注意，內容包(`<packageType>content</packageType>`)**不**&#x200B;需要此儲存庫結構包。

>[!TIP]
>
>有關完整的程式碼片段，請參閱下面的[POM XML程式碼片段](#xml-repository-structure-package)一節。

## 將子包嵌入容器包{#embeddeds}

內容或程式碼套件會放在特殊的「側車」檔案夾中，並可定位為在作者、AEMAEM發佈或兩者上，使用FileVault Maven增效模組的`<embeddeds>`組態進行安裝。 請注意，`<subPackages>`組態不應使用。

常見使用案例包括：

+ 作者使用者與發佈使用者AEM不同的AEMACL/權限
+ 僅用於支援作者的活動的配AEM置
+ 程式碼，例如與後端系統整合，只需在作者上執AEM行

![內嵌套件](assets/embeddeds.png)

若要定AEM位作者AEM、發佈或兩者，套件會以下列格式內嵌在`all`容器套件中的特殊資料夾位置：

`/apps/<app-name>-packages/(content|application|container)/install(.author|.publish)?`

劃分此資料夾結構：

+ 第1級資料夾&#x200B;**必須** `/apps`。
+ 第2層資料夾代表在資料夾名稱后面已修正`-packages`的應用程式。 通常，所有子包都只嵌入一個第2級資料夾，但可以建立任意數量的第2級資料夾以最好地表示應用程式的邏輯結構：
   + `/apps/my-app-packages`
   + `/apps/my-other-app-packages`
   + `/apps/vendor-packages`

   >[!WARNING]
   >
   >根據慣例，子包嵌入資料夾的名稱為尾碼為 `-packages`。這可確保部署代碼和內容包 **未部署** ，而是不會部署任何子包的目標資料夾， `/apps/<app-name>/...` 從而導致破壞性和循環安裝行為。

+ 第3級資料夾必須是
   `application`、 `content` 或  `container`
   + `application`資料夾包含代碼包
   + `content`資料夾包含內容封裝
   + `container`資料夾包含應用程式可能包含的任何[額外應用程式套件&lt;a2/AEM>。
](#extra-application-packages)此資料夾名稱與包含的包的[包類型](#package-types)相對應。
+ 第4層資料夾包含子包，且必須是下列其中一個：
   + `install` 若要同時安裝 **在** AEM作者和AEM發佈上
   + `install.author` 僅 **安裝** 在AEM作者上
   + `install.publish` 若要 **** 僅安裝在AEM發佈附註中，則只 `install.author` 有 `install.publish` 和是支援的目標。不支援其 **他執行模** 式。

例如，包含作者和發佈AEM特定套件的部署可能如下所示：

+ `all` 容器套件內嵌下列套件，以建立單一的部署工件
   + `ui.apps` 內嵌於 `/apps/my-app-packages/application/install` 部署程式碼至AEM作者和AEM發佈
   + `ui.apps.author` 內嵌於 `/apps/my-app-packages/application/install.author` 僅將程式碼部署AEM至
   + `ui.content` 內嵌於 `/apps/my-app-packages/content/install` 將內容和設定部署至作AEM者和發AEM布
   + `ui.content.publish` 內嵌於 `/apps/my-app-packages/content/install.publish` 部署內容和設定以僅發佈AEM中

>[!TIP]
>
>有關完整的程式碼片段，請參閱下面的[POM XML程式碼片段](#xml-embeddeds)一節。

### 容器包的過濾器定義{#container-package-filter-definition}

由於容器封裝中內嵌了程式碼和內容子封裝，所以必須將內嵌的目標路徑新增至容器專案的`filter.xml`，以確保內嵌的封裝在建立時會包含在容器封裝中。

只需為包含要部署的子包的任何第2級資料夾添加`<filter root="/apps/<my-app>-packages"/>`條目。

>[!TIP]
>
>有關完整的程式碼片段，請參閱下面的[POM XML程式碼片段](#xml-container-package-filters)一節。

## 嵌入第三方軟體包{#embedding-3rd-party-packages}

所有軟體包都必須通過[Adobe的公共Maven對象儲存庫](https://repo.adobe.com/nexus/content/groups/public/com/adobe/)或可訪問的公共、可引用的第三方Maven對象儲存庫來使用。

如果第三方套件位於 **Adobe的公用Maven工件存放庫**，則Adobe Cloud manager無需進一步設定即可解析工件。

如果第三方包位於公 **用的第三方Maven對象儲存庫**，則必須按照上述方法在項目中註冊並嵌入此存 `pom.xml` 儲庫 [](#embeddeds)。

第三方應用程式／連接器應使用其`all`封裝內嵌為專案的容器(`all`)封裝。

添加Maven依賴項遵循標準Maven做法，並且嵌入第三方對象（代碼和內容包）的[如上所述](#embedding-3rd-party-packages)。

>[!TIP]
>
>有關完整的程式碼片段，請參閱下面的[POM XML程式碼片段](#xml-3rd-party-maven-repositories)一節。

## `ui.content`包{#package-dependencies}中`ui.apps`之間的包依賴性

為了確保軟體包的正確安裝，建議建立軟體包間相關性。

一般規則是包含可變內容(`ui.content`)的包，該包應依賴於支援可變內容的渲染和使用的不可變代碼(`ui.apps`)。

此一般規則的一個明顯例外是，如果不可變代碼包（`ui.apps`或任何其他）,__僅__&#x200B;包含OSGi捆綁。 如果是，則AEM不應聲明對它的依賴。 這是因為不可變的代碼包&#x200B;__僅__&#x200B;包含OSGi捆綁包未向AEM Package Manager註冊，因此，任AEM何取決於它的軟體包都將具有不滿足的依賴性，並且無法安裝。

>[!TIP]
>
>有關完整的程式碼片段，請參閱下面的[POM XML程式碼片段](#xml-package-dependencies)一節。

內容包依賴項的常見模式有：

### 簡單部署包相關性{#simple-deployment-package-dependencies}

簡單案例將`ui.content`可變內容包設定為依賴於`ui.apps`不可變代碼包。

+ `all` 沒有依賴性
   + `ui.apps` 沒有依賴性
   + `ui.content` depsants on  `ui.apps`

### 複雜部署包依賴性{#complex-deploxment-package-dependencies}

複雜的部署會根據簡單的情況展開，並設定對應可變內容與不可變代碼套件之間的相依性。 根據需要，也可以在不可變代碼包之間建立相依性。

+ `all` 沒有依賴性
   + `common.ui.apps.common` 沒有依賴性
   + `site-a.ui.apps` depsants on  `common.ui.apps`
   + `site-a.ui.content` depsants on  `site-a.ui.apps`
   + `site-b.ui.apps` depsants on  `common.ui.apps`
   + `site-b.ui.content` depsants on  `site-b.ui.apps`

## 本地開發和部署{#local-development-and-deployment}

本文概述的項目結構和組織為&#x200B;**完全相容的**&#x200B;本地開發實AEM例。

## POM XML代碼片段{#pom-xml-snippets}

以下是Maven `pom.xml`組態程式碼片段，可新增至Maven專案，以符合上述建議。

### 包類型{#xml-package-types}

程式碼和內容封裝 (部署為子封裝) 必須依其包含的內容來宣告 **應用****程式或內容**&#x200B;的封裝類型。

#### 容器封裝類型{#container-package-types}

容器`all/pom.xml`專案&#x200B;**不**&#x200B;宣告`<packageType>`。

#### 代碼（不可變）包類型{#immutable-package-types}

代碼包必須將其`packageType`設定為`application`。

在`ui.apps/pom.xml`中，`filevault-package-maven-plugin`外掛程式聲明的`<packageType>application</packageType>`組建配置指令會聲明其軟體包類型。

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

#### 內容（可變）包類型{#mutable-package-types}

內容包必須將其`packageType`設定為`content`。

在`ui.content/pom.xml`中， `filevault-package-maven-plugin`外掛程式聲明的`<packageType>content</packageType>`組建配置指令會聲明其軟體包類型。

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

### 標籤Adobe雲管理器部署的軟體包{#cloud-manager-target}

在每個產生套件的專 **案中** ，除容器(`all`)專案外，將外掛程式聲明的 `<cloudManagerTarget>none</cloudManagerTarget>` 組態新增至外掛程式宣告的組態，以確 `<properties>``filevault-package-maven-plugin`**** 保Adobe Cloud Manager不會部署它們。容器(`all`)套件應是透過Cloud Manager部署的單一套件，而Cloud Manager又嵌入所有必要的程式碼和內容套件。

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

包含回購初始化指令碼的回購初始化指令碼是在`RepositoryInitializer` OSGi工廠配置中通過`scripts`屬性定義的。 請注意，由於這些指令碼是在OSGi配置中定義的，因此可以使用通常的`../config.<runmode>`資料夾語義，按運行模式輕鬆確定其範圍。

請注意，由於指令碼通常是多行宣告，因此在`.config`檔案中定義它們比在JSON架構的`.cfg.json`格式更容易。

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

`scripts` OSGi屬性包含由[Apache Sling&#39;s Repo Init language](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language)定義的指令。

### 儲存庫結構包{#xml-repository-structure-package}

在`ui.apps/pom.xml`和聲明代碼包(`<packageType>application</packageType>`)的任何其他`pom.xml`中，將以下儲存庫結構包配置添加到FileVault Maven插件中。 您可以[為項目](repository-structure-package.md)建立自己的儲存庫結構包。

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

### 在容器包{#xml-embeddeds}中嵌入子包

在`all/pom.xml`中，將以下`<embeddeds>`指令添加到`filevault-package-maven-plugin`插件聲明中。 請記住，**不**&#x200B;使用`<subPackages>`組態，因為這將包含`/etc/packages`中的子封裝，而非`/apps/my-app-packages/<application|content|container>/install(.author|.publish)?`。

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

### 容器包的過濾器定義{#xml-container-package-filters}

在項目 `all` 的( `filter.xml` )中，`all/src/main/content/jcr_root/META-INF/vault/definition/filter.xml`包 **含要部**`-packages` 署的子包的所有資料夾：

```xml
<filter root="/apps/my-app-packages"/>
```

如果嵌入目標中使用多個`/apps/*-packages`，則必須在此處列舉所有。

### 第三方主資料庫{#xml-3rd-party-maven-repositories}

>[!WARNING]
>
>添加更多Maven儲存庫可能會延長Maven構建時間，因為將檢查其他Maven儲存庫是否具有相關性。

在反應堆項目的`pom.xml`中，添加任何必要的第三方公共Maven儲存庫指令。 完整`<repository>`配置應可從第三方儲存庫提供方獲得。

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

### `ui.content`包{#xml-package-dependencies}中`ui.apps`之間的包依賴性

在`ui.content/pom.xml`中，將以下`<dependencies>`指令添加到`filevault-package-maven-plugin`插件聲明中。

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

### 清除容器專案的目標資料夾{#xml-clean-container-package}

在`all/pom.xml`中添加`maven-clean-plugin`插件，該插件將在Maven構建之前清除目標目錄。

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
+ [FileVault Content Package Maven增效模組](http://jackrabbit.apache.org/filevault-package-maven-plugin/)
