---
title: AEM 專案結構
description: 了解如何定義部署至Adobe Experience ManagerCloud Service的套件結構。
exl-id: 38f05723-5dad-417f-81ed-78a09880512a
source-git-commit: 798cd0f459b668dc372a88773ed6221927e7d02e
workflow-type: tm+mt
source-wordcount: '2880'
ht-degree: 12%

---

# AEM 專案結構

>[!TIP]
>
>請熟悉基本的[AEM專案原型use](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)和[FileVault Content Maven外掛程式](/help/implementing/developing/tools/maven-plugin.md)，因為本文是以這些學習與概念為基礎而撰寫的。

本文概述Adobe Experience Manager Maven專案需要哪些變更才能與AEMCloud Service相容，方法是確保專案遵守可變和不可變內容的分割，建立相依性以建立不衝突、確定性的部署，並封裝成可部署結構。

AEM應用程式部署必須由單一AEM套件組成。 此程式包又應包含子程式包，這些子程式包包括應用程式運行所需的所有內容，包括代碼、配置和任何支援的基準內容。

AEM需要分離內 **容和程式碼** ，這表示單一內容套件 **無法**&#x200B;部署至 ********`/apps` Runtime可寫區域 (例如，可寫區域)。`/content`、 `/conf`、 `/home`或其他非 `/apps`)。而應用程式必須將程式碼和內容分隔為獨立套件，以便部署至AEM。

本檔案中概述的套件結構與本機開 **發部署** 和AEM cloud服務部署都相容。

>[!TIP]
>
>本檔案中概述的設定由[AEM Project Maven原型24或更新版本](https://github.com/adobe/aem-project-archetype/releases)提供。

## 儲存庫的可變區與不可變區 {#mutable-vs-immutable}

`/apps` and `/libs`**are consed inmumable areas of AEM as they cannot be changed(create, update, delete)after AEM starts(i.e. at runtime)。**&#x200B;在運行時更改不可變區域的任何嘗試都將失敗。

儲存庫中的其他所有項目，如`/content`、`/conf`、`/var`、`/etc`、`/oak:index`、`/system`、`/tmp`等。 都是&#x200B;**可變**&#x200B;區域，這表示在執行階段可以變更它們。

>[!WARNING]
>
>與舊版AEM相同，`/libs`不應修改。 只有AEM產品代碼可部署至`/libs`。

### Oak Indexes {#oak-indexes}

Oak索引(`/oak:index`)由AEM特別管理，作為Cloud Service部署程式。 這是因為Cloud Manager必須等到部署任何新索引並完全重新編列索引後，才能切換至新程式碼影像。

因此，雖然Oak索引在執行時可變，但必須部署為程式碼，才能在安裝任何可變套件前先行安裝。 因此，`/oak:index`配置是代碼包的一部分，而不是內容包[的一部分，如下所述](#recommended-package-structure)。

>[!TIP]
>
>有關在AEM as aCloud Service中建立索引的進一步詳細資訊，請參閱文檔[內容搜索和索引](/help/operations/indexing.md)。

## 建議的封裝結構 {#recommended-package-structure}

![Experience Manager項目包結構](assets/content-package-organization.png)

此圖表概述了建議的項目結構和包部署對象。

建議的應用程式部署結構如下：

### 程式碼套件/ OSGi套件組合

+ 會產生OSGi套件Jar檔案，並直接內嵌於所有專案中。

+ `ui.apps`套件包含要部署的所有代碼，並且只部署到`/apps`。 `ui.apps`包的常見元素包括，但不限於：
   + [元件定義和](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=zh-Hant) HTLscript
      + `/apps/my-app/components`
   + JavaScript和CSS（透過[用戶端程式庫](/help/implementing/developing/introduction/clientlibs.md)）
      + `/apps/my-app/clientlibs`
   + [](/help/implementing/developing/introduction/overlays.md) 覆蓋  `/libs`
      + `/apps/cq`、  `/apps/dam/`等
   + 後援內容感知設定
      + `/apps/settings`
   + ACL（權限）
      + `/apps`下任何路徑的任何`rep:policy`
   + [預編譯的套件指令碼](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/using/developing/archetype/precompiled-bundled-scripts.html)

+ `ui.config`包包含所有[OSGi配置](/help/implementing/deploying/configuring-osgi.md):
   + 包含運行模式特定OSGi配置定義的組織資料夾
      + `/apps/my-app/osgiconfig`
   + 包含預設OSGi設定的通用OSGi設定資料夾，這些設定會套用至所有目標AEM作為Cloud Service部署目標
      + `/apps/my-app/osgiconfig/config`
   + 運行模式特定的OSGi配置資料夾，該資料夾包含應用於所有目標AEM作為Cloud Service部署目標的預設OSGi配置
      + `/apps/my-app/osgiconfig/config.<author|publish>.<dev|stage|prod>`
   + Repo Init OSGi配置指令碼
      + [回購](#repo-init) 性炎是部署（可變）內容(邏輯上屬於AEM應用程式一部分)的建議方式。Repo Init OSGi設定應如上所述放置在適當的`config.<runmode>`資料夾中，並用於定義：
         + 基線內容結構
         + 使用者
         + 服務用戶
         + 群組
         + ACL（權限）

>[!NOTE]
>
>必須將相同的程式碼部署至所有環境。 這是為了確保預備環境上的信賴驗證也正在生產中，所需的項目。 如需詳細資訊，請參閱[Runmodes](/help/implementing/deploying/overview.md#runmodes)上的一節。


### 內容套件

+ `ui.content`套件包含所有內容和配置。 內容包，包含`ui.apps`或`ui.config`包中未包含的所有節點定義，換言之，包含`/apps`或`/oak:index`中未包含的任何內容。 `ui.content`包的常見元素包括，但不限於：
   + 內容感知設定
      + `/conf`
   + 必要、複雜的內容結構(即 內容建置以為基礎，並延伸超過回購初始化中定義的基線內容結構。)
      + `/content`、  `/content/dam`等
   + 受管轄的標籤分類
      + `/content/cq:tags`
   + 舊式等節點（理想情況下，將這些節點遷移到非/等位置）
      + `/etc`

### 容器包裝

+ `all`套件是容器套件，僅包含可部署的成品、OSGI套件組合Jar檔案、`ui.apps`、`ui.config`和`ui.content`套件作為內嵌。 `all`套件不得具有任何內容或代碼&#x200B;**，而是將所有部署委派給儲存庫的子套件或OSGi套件組合Jar檔案。**

   現在，包中使用的是Maven [FileVault Package Maven插件的嵌入配置](#embeddeds)，而不是`<subPackages>`配置。

   對於複雜的Experience Manager部署，可能需要建立多個`ui.apps`、`ui.config`和`ui.content`專案/套件，以代表AEM中的特定網站或租戶。 如果執行此操作，請確保可變內容和不可變內容之間的分割符合要求，並且所需的內容包和OSGi捆綁Jar檔案作為子包嵌入`all`容器內容包中。

   例如，複雜的部署內容包結構可能如下所示：

   + `all` 內容包嵌入以下包，以建立單一部署對象
      + `common.ui.apps` 部署網站A和 **** 網站B所需的程式碼
      + `site-a.core` 站點A所需的OSGi捆綁Jar
      + `site-a.ui.apps` 部署網站A所需的代碼
      + `site-a.ui.config` 部署站點A所需的OSGi配置
      + `site-a.ui.content` 部署站點A所需的內容和配置
      + `site-b.core` 站點B所需的OSGi捆綁Jar
      + `site-b.ui.apps` 部署站點B所需的代碼
      + `site-b.ui.config` 部署站點B所需的OSGi配置
      + `site-b.ui.content` 部署站點B所需的內容和配置

### 額外的應用程式包{#extra-application-packages}

如果AEM部署使用其他AEM專案（其本身由其自己的程式碼和內容套件組成），則其容器套件應內嵌在專案的`all`套件中。

例如，包含2個供應商AEM應用程式的AEM專案看起來可能如下：

+ `all` 內容包嵌入以下包，以建立單一部署對象
   + `core` AEM應用程式所需的OSGi捆綁Jar
   + `ui.apps` 部署AEM應用程式所需的程式碼
   + `ui.config` 部署AEM應用程式所需的OSGi設定
   + `ui.content` 部署AEM應用程式所需的內容和設定
   + `vendor-x.all` 部署供應商X應用程式所需的所有內容（代碼和內容）
   + `vendor-y.all` 部署供應商Y應用程式所需的所有內容（代碼和內容）

## 套件類型 {#package-types}

要用其聲明的包類型標籤包。

+ 容器包必須將其`packageType`設定為`container`。 容器包不能直接包含OSGi包、OSGi配置，並且不允許使用[安裝掛接](http://jackrabbit.apache.org/filevault/installhooks.html)。
+ 代碼（不可變）包必須將其`packageType`設定為`application`。
+ 內容（可變）包必須將其`packageType`設定為`content`。


如需詳細資訊，請參閱下方的[Apache Jackrabbit FileVault - Package Maven外掛程式檔案](https://jackrabbit.apache.org/filevault-package-maven-plugin/package-mojo.html#packageType)及[FileVault Maven設定片段](#marking-packages-for-deployment-by-adoube-cloud-manager)。

>[!TIP]
>
>如需完整的程式碼片段，請參閱下方的[POM XML程式碼片段](#xml-package-types)一節。

## 標示要由Analytics Cloud Manager部署的套件Adobe {#marking-packages-for-deployment-by-adoube-cloud-manager}

依預設，Adobe Cloud manager會收集由Maven組建版本產生的所有套件，但是，由於容器(`all`)套件是包含所有程式碼和內容套件的單一部署工件，因此我們必須確保僅部署容器( ****`all`)套件。為確保此，Maven構建版本生成的其他軟體包必須用的FileVault Content Package Maven插件配置進行標籤 `<properties><cloudManagerTarget>none</cloudManageTarget></properties>`。

>[!TIP]
>
>如需完整的程式碼片段，請參閱下方的[POM XML程式碼片段](#pom-xml-snippets)一節。

## 存放庫初始化{#repo-init}

Repo Init提供了定義JCR結構的指令（或指令碼），從資料夾樹等常見節點結構到用戶、服務用戶、組和ACL定義。

Repo Init的主要優點是，它們具有執行其指令碼所定義所有動作的隱式權限，且會在部署生命週期早期叫用，以確保執行程式碼時存在所有必要的JCR結構。

雖然Repo Init指令碼本身在`ui.config`專案中以指令碼形式存留，但它們可以且應該用於定義下列可變結構：

+ 基線內容結構
+ 服務用戶
+ 使用者
+ 群組
+ ACL

存放庫初始化指令碼會儲存為`RepositoryInitializer` OSGi工廠設定的`scripts`項目，因此，可透過執行模式以隱含方式鎖定目標，以允許AEM製作與AEM Publish Services的存放庫初始化指令碼之間，或甚至是環境（開發、預備與生產）之間的差異。

Repo Init OSGi設定最好以[`.config` OSGi設定格式](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-config-1)寫入，因為它們支援多行，這是使用[`.cfg.json`定義OSGi設定](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1)的最佳實務的例外。

請注意，在定義「用戶」和「組」時，只有組被視為應用程式的一部分，並應在此處定義其函式的整體。 組織使用者和群組仍應在AEM中執行階段定義；例如，如果自訂工作流程將工作指派給指定的群組，則應透過AEM應用程式中的存放庫初始化來定義該群組，但如果群組只是組織性的，例如「Wendy&#39;s Team」和「Sean&#39;s Team」，則這些是最佳定義，並在AEM的執行階段中加以管理。

>[!TIP]
>
>必須在內嵌`scripts`欄位中定義Repo Init指令碼&#x200B;*，且`references`設定將無法運作。*

[Apache Sling Repo Init檔案](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language)中提供Repo Init指令碼的完整辭匯。

>[!TIP]
>
>如需完整的程式碼片段，請參閱下方的[回購初始化程式碼片段](#snippet-repo-init)一節。

## 儲存庫結構包 {#repository-structure-package}

代碼包要求配置FileVault Maven插件的配置，以引用`<repositoryStructurePackage>`，該可強制結構依賴項的正確性（以確保一個代碼包不會跨另一個安裝）。 您可以[為您的專案](repository-structure-package.md)建立自己的存放庫結構套件。

這只是程 **式碼套件的必要** ，也就是任何標有的套件 `<packageType>application</packageType>`。

要了解如何為應用程式建立儲存庫結構包，請參閱[開發儲存庫結構包](repository-structure-package.md)。

請注意，內容包(`<packageType>content</packageType>`)**不**&#x200B;需要此儲存庫結構包。

>[!TIP]
>
>如需完整的程式碼片段，請參閱下方的[POM XML程式碼片段](#xml-repository-structure-package)一節。

## 在容器包中嵌入子包{#embeddeds}

內容或程式碼套件會放置在特殊的「側車」資料夾中，且可以鎖定目標，使用FileVault Maven外掛程式的`<embeddeds>`設定，以安裝在AEM作者、AEM發佈或兩者上。 請注意，不應使用`<subPackages>`設定。

常見的使用案例包括：

+ AEM製作使用者與AEM發佈使用者之間有所差異的ACL/權限
+ 僅用於支援AEM作者上活動的設定
+ 程式碼（例如與後台系統的整合），只需在AEM作者上執行

![內嵌套件](assets/embeddeds.png)

若要鎖定AEM作者、AEM發佈或兩者，套件會以下列格式嵌入至`all`容器套件中的特殊資料夾位置：

`/apps/<app-name>-packages/(content|application|container)/install(.author|.publish)?`

劃分此資料夾結構：

+ 第1級資料夾&#x200B;**必須是** `/apps`。
+ 第2層資料夾代表資料夾名稱后面已固定`-packages`的應用程式。 通常只有一個第2級資料夾所有子包都嵌入在下，但是可以建立任意數量的第2級資料夾以最好地表示應用程式的邏輯結構：
   + `/apps/my-app-packages`
   + `/apps/my-other-app-packages`
   + `/apps/vendor-packages`

   >[!WARNING]
   >
   >根據慣例，子包嵌入資料夾的名稱為尾碼為 `-packages`。這可確保部署代碼和內容包 **未部署** ，而是不會部署任何子包的目標資料夾， `/apps/<app-name>/...` 從而導致破壞性和循環安裝行為。

+ 第3級資料夾必須是
   `application`、  `content` 或  `container`
   + `application`資料夾包含代碼包
   + `content`資料夾包含內容包
   + `container`資料夾包含AEM應用程式可能包含的任何[額外應用程式套件](#extra-application-packages)。
此資料夾名稱對應於包含的[包類型](#package-types)。
+ 第4層資料夾包含子包，且必須是下列其中一個：
   + `install` 若要同時安裝 **在** AEM作者和AEM發佈上
   + `install.author` 僅 **安裝** 在AEM作者上
   + `install.publish` 僅 **** 安裝在AEM發佈上請注意，只有和 `install.author` 是 `install.publish` 受支援的目標。不支援其 **他執行模** 式。

例如，包含AEM製作和發佈特定套件的部署可能如下所示：

+ `all` 容器包嵌入以下包，以建立單一部署對象
   + `ui.apps` 內嵌於 `/apps/my-app-packages/application/install` 中，會將程式碼同時部署至AEM作者和AEM發佈
   + `ui.apps.author` 內嵌於 `/apps/my-app-packages/application/install.author` 中部署程式碼至僅AEM作者
   + `ui.content` 內嵌於 `/apps/my-app-packages/content/install` 中，可部署內容和設定至AEM製作和AEM發佈
   + `ui.content.publish` 內嵌於 `/apps/my-app-packages/content/install.publish` 中，部署內容和設定只能發佈AEM

>[!TIP]
>
>如需完整的程式碼片段，請參閱下方的[POM XML程式碼片段](#xml-embeddeds)一節。

### 容器包的篩選器定義 {#container-package-filter-definition}

由於容器包中嵌入了代碼和內容子包，因此必須將嵌入的目標路徑添加到容器項目的`filter.xml`中，以確保在構建時將嵌入的包包含在容器包中。

只需為包含要部署的子包的任何第2級資料夾添加`<filter root="/apps/<my-app>-packages"/>`條目。

>[!TIP]
>
>如需完整的程式碼片段，請參閱下方的[POM XML程式碼片段](#xml-container-package-filters)一節。

## 嵌入第三方包 {#embedding-3rd-party-packages}

所有包都必須通過[Adobe的公用Maven對象儲存庫](https://repo.adobe.com/nexus/content/groups/public/com/adobe/)或可訪問的可引用的公用第三方Maven對象儲存庫來使用。

如果第三方套件位於 **Adobe的公用Maven工件存放庫**，則Adobe Cloud manager無需進一步設定即可解析工件。

如果第三方包位於公 **用的第三方Maven對象儲存庫**，則必須按照上述方法在項目中註冊並嵌入此存 `pom.xml` 儲庫 [](#embeddeds)。

應使用其`all`套件來內嵌第三方應用程式/連接器，作為專案容器(`all`)套件中的容器。

新增Maven相依性會遵循標準Maven實務，而內嵌第三方成品（程式碼和內容套件）是[概述於上方](#embedding-3rd-party-packages)。

>[!TIP]
>
>如需完整的程式碼片段，請參閱下方的[POM XML程式碼片段](#xml-3rd-party-maven-repositories)一節。

## `ui.content`包中`ui.apps`之間的包依賴關係 {#package-dependencies}

為確保正確安裝軟體包，建議建立軟體包間依賴項。

一般規則是包含可變內容(`ui.content`)的包，該包應取決於支援可變內容的呈現和使用的不可變代碼(`ui.apps`)。

此一般規則的一個明顯例外是，如果不可變的代碼包（`ui.apps`或任何其他）,__僅__&#x200B;包含OSGi套件組合。 若存在，則任何AEM套件都不應宣告相依性。 這是因為不可變的代碼包&#x200B;__僅__&#x200B;包含OSGi套件組合未向AEM Package Manager註冊，因此，任何根據其的AEM套件都將具有未滿足的依賴性，且無法安裝。

>[!TIP]
>
>如需完整的程式碼片段，請參閱下方的[POM XML程式碼片段](#xml-package-dependencies)一節。

內容包依賴項的常見模式為：

### 簡單部署包依賴項 {#simple-deployment-package-dependencies}

簡單案例將`ui.content`可變內容包設定為依賴於`ui.apps`不可變代碼包。

+ `all` 沒有依賴項
   + `ui.apps` 沒有依賴項
   + `ui.content` 取決於  `ui.apps`

### 複雜的部署包依賴項 {#complex-deploxment-package-dependencies}

複雜的部署會根據簡單的情況展開，並在對應的可變內容和不可變代碼包之間設定相依性。 視需要，也可在不可變代碼包之間建立相依性。

+ `all` 沒有依賴項
   + `common.ui.apps.common` 沒有依賴項
   + `site-a.ui.apps` 取決於  `common.ui.apps`
   + `site-a.ui.content` 取決於  `site-a.ui.apps`
   + `site-b.ui.apps` 取決於  `common.ui.apps`
   + `site-b.ui.content` 取決於  `site-b.ui.apps`

## 本地開發和部署 {#local-development-and-deployment}

本文概述的專案結構和組織為&#x200B;**完全相容的**&#x200B;本機開發AEM例項。

## POM XML片段 {#pom-xml-snippets}

以下是可新增至Maven專案的Maven `pom.xml`設定片段，以符合上述建議。

### 套件類型 {#xml-package-types}

程式碼和內容封裝 (部署為子封裝) 必須依其包含的內容來宣告 **應用****程式或內容**&#x200B;的封裝類型。

#### 容器包裝類型 {#container-package-types}

容器`all/pom.xml`項目&#x200B;**不**&#x200B;聲明`<packageType>`。

#### 代碼（不可變）包類型 {#immutable-package-types}

代碼包必須將其`packageType`設定為`application`。

在`ui.apps/pom.xml`中，`filevault-package-maven-plugin`插件聲明的`<packageType>application</packageType>`構建配置指令聲明其包類型。

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

內容包必須將其`packageType`設定為`content`。

在`ui.content/pom.xml`中，`filevault-package-maven-plugin`插件聲明的`<packageType>content</packageType>`構建配置指令聲明其包類型。

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

### 標示AdobeCloud Manager部署的套件 {#cloud-manager-target}

在每個產生套件的專 **案中** ，除容器(`all`)專案外，將外掛程式聲明的 `<cloudManagerTarget>none</cloudManagerTarget>` 組態新增至外掛程式宣告的組態，以確 `<properties>``filevault-package-maven-plugin`**** 保Adobe Cloud Manager不會部署它們。容器(`all`)套件應是透過Cloud Manager部署的單一套件，而Cloud Manager又內嵌所有必要的程式碼和內容套件。

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

### 存放庫初始化{#snippet-repo-init}

包含Repo Init指令碼的Repo Init指令碼是通過`scripts`屬性在`RepositoryInitializer` OSGi工廠配置中定義的。 請注意，由於這些指令碼在OSGi配置中定義，因此可使用通常的`../config.<runmode>`資料夾語義，通過運行模式輕鬆限定它們的範圍。

請注意，由於指令碼通常為多行聲明，因此在`.config`檔案中定義它們比以JSON為基礎的`.cfg.json`格式要容易。

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

`scripts` OSGi屬性包含由[Apache Sling的Repo Init語言](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language)定義的指令。

### 儲存庫結構包 {#xml-repository-structure-package}

在聲明代碼包(`<packageType>application</packageType>`)的`ui.apps/pom.xml`和任何其他`pom.xml`中，將以下儲存庫結構包配置添加到FileVault Maven插件中。 您可以[為您的專案](repository-structure-package.md)建立自己的存放庫結構套件。

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

### 在容器包中嵌入子包 {#xml-embeddeds}

在`all/pom.xml`中，將以下`<embeddeds>`指令添加到`filevault-package-maven-plugin`插件聲明中。 請記住，**不**&#x200B;使用`<subPackages>`配置，因為這將包括`/etc/packages`中的子包，而不是`/apps/my-app-packages/<application|content|container>/install(.author|.publish)?`。

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

如果在嵌入目標中使用多個`/apps/*-packages`，則必須在此處枚舉這些目標。

### 第三方Maven儲存庫 {#xml-3rd-party-maven-repositories}

>[!WARNING]
>
>新增更多Maven存放庫可能會延長Maven建置時間，因為會檢查其他Maven存放庫是否有相依性。

在Reactor專案的`pom.xml`中，新增任何必要的第三方公用Maven存放庫指示。 完整的`<repository>`配置應可從第三方儲存庫提供程式中使用。

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

### `ui.content`包中`ui.apps`之間的包依賴關係 {#xml-package-dependencies}

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

### 清除容器專案的目標資料夾 {#xml-clean-container-package}

在`all/pom.xml`中新增`maven-clean-plugin`外掛程式，該外掛程式將在Maven組建之前清除目標目錄。

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

+ [使用Maven管理套件](/help/implementing/developing/tools/maven-plugin.md)
+ [FileVault Content Package Maven插件](http://jackrabbit.apache.org/filevault-package-maven-plugin/)
