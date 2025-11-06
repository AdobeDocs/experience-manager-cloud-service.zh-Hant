---
title: AEM 專案結構
description: 瞭解如何定義封裝結構以部署至Adobe Experience Manager Cloud Service。
exl-id: 38f05723-5dad-417f-81ed-78a09880512a
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2859'
ht-degree: 4%

---

# AEM 專案結構

>[!TIP]
>
>熟悉基本的[AEM Project Archetype use](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)和[FileVault Content Maven外掛程式](/help/implementing/developing/tools/maven-plugin.md)，因為本文將以這些學問和概念為基礎。

本文概述讓Adobe Experience Manager Maven專案與AEM as a Cloud Service相容所需的變更，確保專案遵守可變和不可變內容的分割。 此外，相依性會建立為建立不衝突、確定性的部署，並封裝成可部署結構。

AEM應用程式部署必須由單一AEM套件組成。 此套件繼而應包含子套件，這些子套件包含應用程式運作所需的一切，包括程式碼、設定及任何支援的基準線內容。

AEM需要將&#x200B;**內容**&#x200B;和&#x200B;**程式碼**&#x200B;分開，這表示單一內容套件&#x200B;**無法**&#x200B;部署至存放庫的&#x200B;**同時** `/apps`和執行階段可寫入區域（例如，`/content`、`/conf`、`/home`或非`/apps`的任何區域）。 而應用程式必須將程式碼和內容分隔為獨立套件，以便部署至AEM。

本檔案中概述的套件結構與本機開 **發部署** 和AEM cloud服務部署都相容。

>[!TIP]
>
>本檔案中概述的設定是由[AEM Project Maven Archetype 24或更新版本](https://github.com/adobe/aem-project-archetype/releases)提供。

## 存放庫的可變與不可變區域 {#mutable-vs-immutable}

AEM的`/apps`和`/libs`區域視為&#x200B;**不可變**，因為在AEM啟動（即在執行階段）後就無法變更（建立、更新、刪除）。 任何在執行階段變更不可變區域的嘗試都會失敗。

存放庫中的所有其他專案（`/content`、`/conf`、`/var`、`/etc`、`/oak:index`、`/system`、`/tmp`等等）都是&#x200B;**可變**&#x200B;區域，這表示可在執行階段變更這些區域。

>[!WARNING]
>
>如同舊版AEM一樣，`/libs`不應修改。 只有AEM產品程式碼可以部署至`/libs`。

### Oak索引 {#oak-indexes}

Oak索引(`/oak:index`)由AEM as a Cloud Service部署程式管理。 這是因為Cloud Manager必須等到任何新索引部署並完全重新索引後，才能切換至新程式碼影像。

因此，雖然Oak索引在執行階段是可變的，但是它們必須部署為程式碼，以便在安裝任何可變套件之前可以安裝。 因此`/oak:index`設定是程式碼封裝的一部分，而不是如下所述[的內容封裝](#recommended-package-structure)的一部分。

>[!TIP]
>
>如需AEM as a Cloud Service索引的詳細資訊，請參閱[內容搜尋與索引](/help/operations/indexing.md)。

## 建議的封裝結構 {#recommended-package-structure}

![Experience Manager專案封裝結構](assets/content-package-organization.png)

此圖表提供建議的專案結構和套件部署成品概觀。

建議的應用程式部署結構如下：

### 程式碼套件/ OSGi套件組合

+ 會產生OSGi套件Jar檔案，並直接內嵌於所有專案中。

+ `ui.apps`封裝包含要部署的所有程式碼，且僅部署至`/apps`。 `ui.apps`封裝的通用元素包含但不限於：
   + [元件定義和HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html)指令碼
      + `/apps/my-app/components`
   + JavaScript和CSS （透過[使用者端資料庫](/help/implementing/developing/introduction/clientlibs.md)）
      + `/apps/my-app/clientlibs`
   + [重疊](/help/implementing/developing/introduction/overlays.md) / `/libs`
      + `/apps/cq`、`/apps/dam/`等。
   + 遞補內容感知設定
      + `/apps/settings`
   + ACL （許可權）
      + `rep:policy`下的任何路徑的任何`/apps`
   + [預先編譯的套裝指令碼](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/precompiled-bundled-scripts.html)

>[!NOTE]
>
>所有環境都必須部署相同的程式碼。 此程式碼可確保將預備環境上的驗證也用於生產環境的信賴等級。 如需詳細資訊，請參閱[執行模式](/help/implementing/deploying/overview.md#runmodes)的區段。


### 內容封裝

+ `ui.content`封裝包含所有內容和組態。 內容封裝包含不在`ui.apps`或`ui.config`封裝中的所有節點定義，換句話說，包含不在`/apps`或`/oak:index`中的所有節點定義。 `ui.content`封裝的通用元素包含但不限於：
   + 內容感知設定
      + `/conf`
   + 必要的複雜內容結構（亦即，建置並延伸超過存放庫初始中定義的基準內容結構的內容建置）。
      + `/content`、`/content/dam`等。
   + 控管的標籤分類
      + `/content/cq:tags`
   + 舊版ETC節點（理想情況下，請將這些節點移轉至非/etc位置）
      + `/etc`

### 容器封裝

+ `all`封裝是容器封裝，僅包含可部署的成品、OSGI組合Jar檔案、`ui.apps`、`ui.config`以及`ui.content`封裝作為內嵌。 `all`封裝不得具有&#x200B;**任何內容或自己的程式碼**，而是將所有部署委派給儲存庫的子封裝或OSGi套件組合Jar檔案。

  套件現在包含使用Maven [FileVault Package Maven外掛程式的內嵌組態](#embeddeds)，而非`<subPackages>`組態。

  對於複雜的Experience Manager部署，最好在AEM中建立代表特定網站或租使用者的多個`ui.apps`、`ui.config`和`ui.content`專案/套件。 如果完成此方法，請確保遵循可變和不可變內容之間的分割，並將必要的內容套件和OSGi套件Jar檔案嵌入為`all`容器內容套件中的子套件。

  例如，複雜的部署內容套件結構可能如下所示：

   + `all`內容套件內嵌下列套件，以建立單一部署成品
      + `common.ui.apps`部署&#x200B;**網站A和網站B都需要的程式碼**
      + 網站A需要`site-a.core` OSGi套件Jar
      + `site-a.ui.apps`部署網站A所需的程式碼
      + `site-a.ui.config`部署網站A所需的OSGi設定
      + `site-a.ui.content`部署網站A所需的內容和設定
      + 網站B需要`site-b.core` OSGi套件Jar
      + `site-b.ui.apps`部署網站B所需的程式碼
      + `site-b.ui.config`部署網站B所需的OSGi設定
      + `site-b.ui.content`部署網站B所需的內容和設定

+ `ui.config`封裝包含所有[OSGi設定](/help/implementing/deploying/configuring-osgi.md)：
   + 視為程式碼且屬於OSGi套件組合，但不包含一般內容節點。 因此會標示為容器封裝
   + 包含執行模式特定OSGi設定定義的組織資料夾
      + `/apps/my-app/osgiconfig`
   + 通用OSGi設定資料夾，其中包含套用至所有目標AEM as a Cloud Service部署目標的預設OSGi設定
      + `/apps/my-app/osgiconfig/config`
   + 執行模式特定的OSGi設定資料夾，其中包含套用至所有目標AEM as a Cloud Service部署目標的預設OSGi設定
      + `/apps/my-app/osgiconfig/config.<author|publish>.<dev|stage|prod>`
   + Repo Init OSGi設定指令碼
      + [Repo Init](#repo-init)是部署（可變）內容的建議方式，這些內容在邏輯上屬於AEM應用程式的一部分。 Repo Init OSGi設定應放置在如上所述的適當`config.<runmode>`資料夾中，並用於定義：
         + 基準內容結構
         + 使用者
         + 服務使用者
         + 群組
         + ACL （許可權）

### 額外的應用程式套件{#extra-application-packages}

如果AEM部署使用其他AEM專案（專案本身由自己的程式碼和內容套件組成），則其容器套件應內嵌在專案的`all`套件中。

例如，包含兩個廠商AEM應用程式的AEM專案看起來可能像這樣：

+ `all`內容套件內嵌下列套件，以建立單一部署成品
   + `core` AEM應用程式所需的OSGi套件Jar
   + `ui.apps`部署AEM應用程式所需的程式碼
   + `ui.config`部署AEM應用程式所需的OSGi設定
   + `ui.content`部署AEM應用程式所需的內容和設定
   + `vendor-x.all`部署廠商X應用程式所需的一切（程式碼和內容）
   + `vendor-y.all`部署廠商Y應用程式所需的一切（程式碼和內容）

## 封裝型別 {#package-types}

套件將標示其宣告的套件型別。 套件型別有助於釐清套件的用途和部署。

+ 容器套件必須將其`packageType`設定為`container`。 容器套件不得包含一般節點。 僅允許OSGi套件組合、設定和子套件。 AEM as a Cloud Service中的容器不允許使用[安裝鉤點](https://jackrabbit.apache.org/filevault/installhooks.html)。
+ 程式碼（不可變）套件必須將其`packageType`設定為`application`。
+ 內容（可變）套件必須將其`packageType`設定為`content`。


如需詳細資訊，請參閱以下的[Apache Jackrabbit FileVault - Package Maven外掛程式檔案](https://jackrabbit.apache.org/filevault-package-maven-plugin/package-mojo.html#packageType)、[Apache Jackrabbit封裝型別](https://jackrabbit.apache.org/filevault/packagetypes.html)和[FileVault Maven設定程式碼片段](#marking-packages-for-deployment-by-adoube-cloud-manager)。

>[!TIP]
>
>如需完整的程式碼片段，請參閱下方的[POM XML程式碼片段](#xml-package-types)區段。

## 將套件標籤為由Adobe Cloud Manager部署 {#marking-packages-for-deployment-by-adoube-cloud-manager}

依預設，Adobe Cloud Manager會收集由Maven組建版本產生的所有套件。 但是，因為容器(`all`)封裝是包含所有程式碼和內容封裝的單一部署成品，所以您必須確保僅&#x200B;**部署**&#x200B;容器(`all`)封裝。 為確保此，Maven構建版本生成的其他軟體包必須用的FileVault Content Package Maven插件配置進行標籤 `<properties><cloudManagerTarget>none</cloudManageTarget></properties>`。

>[!TIP]
>
>如需完整的程式碼片段，請參閱下方的[POM XML程式碼片段](#pom-xml-snippets)區段。

## 存放庫初始{#repo-init}

Repo Init提供定義JCR結構的指示或指令碼，範圍從一般節點結構（如資料夾樹狀結構）到使用者、服務使用者、群組和ACL定義。

Repo Init的主要優點是，他們擁有隱含許可權，可執行其指令碼定義的所有動作。 此外，這類指令碼會在部署生命週期的初期叫用，確保所有必要的JCR結構會在程式碼執行時存在。

雖然Repo Init指令碼本身在`ui.config`專案中是以指令碼的形式存在，但是它們可以而且應該用來定義下列可變結構：

+ 基準內容結構
+ 服務使用者
+ 使用者
+ 群組
+ ACL

Repo Init指令碼會儲存為`scripts` OSGi Factory設定的`RepositoryInitializer`個專案。 因此，它們可以透過執行模式隱含定位，以便在AEM Author和AEM Publish Services的Repo Init指令碼之間或甚至在環境（開發、階段和生產環境）之間提供差異。

Repo Init OSGi設定最好以[`.config` OSGi設定格式](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-config-1)撰寫，因為它們支援多行，這是使用[`.cfg.json`定義OSGi設定](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1)之最佳做法的例外情況。

定義「使用者」和「群組」時，只有群組會被視為應用程式的一部分，並且是其功能的組成部分。 您仍可在AEM中於執行階段定義組織使用者和群組。 例如，如果自訂工作流程將工作指派給已命名的群組，請在AEM應用程式中透過Repo Init定義該群組。 不過，如果群組只是組織性的，例如「Wendy的團隊」和「Sean的團隊」，這些群組最好在AEM的執行階段中定義和管理。

>[!TIP]
>
>Repo Init指令碼&#x200B;*必須*&#x200B;在內嵌`scripts`欄位中定義，否則`references`設定無法運作。

[Apache Sling Repo Init檔案](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language)提供Repo Init指令碼的完整辭彙。

>[!TIP]
>
>如需完整的程式碼片段，請參閱下方的[Repo初始程式碼片段](#snippet-repo-init)區段。

## 存放庫結構套件 {#repository-structure-package}

程式碼套件需要設定FileVault Maven外掛程式的設定，以參照強制結構相依性正確性的`<repositoryStructurePackage>` （以確保一個程式碼套件不會安裝在另一個程式碼套件上）。 您可以[為您的專案](repository-structure-package.md)建立您自己的存放庫結構套件。

**只需要**&#x200B;才能使用程式碼封裝，這表示任何標示為`<packageType>application</packageType>`的封裝。

若要瞭解如何建立應用程式的存放庫結構封裝，請參閱[開發存放庫結構封裝](repository-structure-package.md)。

內容封裝(`<packageType>content</packageType>`) **不**&#x200B;需要此存放庫結構封裝。

>[!TIP]
>
>如需完整的程式碼片段，請參閱下方的[POM XML程式碼片段](#xml-repository-structure-package)區段。

## 將子套件嵌入於容器套件{#embeddeds}

內容或程式碼套件會放置在特殊的「side-car」資料夾中，並使用FileVault Maven外掛程式的`<embeddeds>`設定，鎖定為安裝在AEM作者、AEM發佈或兩者上。 請勿使用`<subPackages>`設定。

常見的使用案例包括：

+ AEM作者使用者與AEM發佈使用者之間的ACL/許可權
+ 僅用於支援AEM作者活動的設定
+ 僅需要在AEM作者上執行的程式碼（例如與後台系統的整合）

![內嵌封裝](assets/embeddeds.png)

若要鎖定AEM作者、AEM發行或兩者，套件會以下列格式內嵌於特殊資料夾位置的`all`容器套件中：

`/apps/<app-name>-packages/(content|application|container)/install(.author|.publish)?`

劃分此檔案夾結構：

+ 第一層資料夾&#x200B;**必須是** `/apps`。
+ 第二層資料夾代表應用程式，其資料夾名稱后加上`-packages`。 通常，所有子封裝都內嵌在單一的第二層資料夾底下，但可以建立任意數量的第二層資料夾以最好地代表應用程式的邏輯結構：
   + `/apps/my-app-packages`
   + `/apps/my-other-app-packages`
   + `/apps/vendor-packages`

  >[!WARNING]
  >
  >根據慣例，子封裝內嵌資料夾的名稱為尾碼為`-packages`。 此命名可確保部署程式碼和內容封裝&#x200B;**不是**&#x200B;部署任何子封裝`/apps/<app-name>/...`的目標資料夾，這會導致破壞性和循環安裝行為。

+ 第3層資料夾必須是
  `application`、`content`或`container`
   + `application`資料夾包含程式碼封裝
   + `content`資料夾包含內容封裝
   + `container`資料夾包含AEM應用程式可能包含的任何[額外應用程式套件](#extra-application-packages)。
此資料夾名稱對應到它包含的[封裝型別](#package-types)。
+ 第4層資料夾包含子封裝，且必須是下列其中一項：
   + `install`以便安裝在&#x200B;**both** AEM作者和AEM發佈上
   + `install.author`，因此您只在AEM作者上安裝&#x200B;**2&rbrace;**
   + `install.publish`，因此您只在AEM發佈上安裝&#x200B;**2&rbrace;
只有&#x200B;**&#x200B;和`install.author`支援的目標。 `install.publish`不支援其 &#x200B;** 他執行模** 式。

例如，包含AEM作者和發佈特定套件的部署看起來可能像這樣：

+ `all`容器封裝內嵌下列封裝，以建立單一部署成品
   + 內嵌在`ui.apps`中的`/apps/my-app-packages/application/install`將程式碼部署至AEM作者和AEM發佈
   + 內嵌在`ui.apps.author`中的`/apps/my-app-packages/application/install.author`將程式碼僅部署給AEM作者
   + `ui.content`中內嵌的`/apps/my-app-packages/content/install`會將內容和設定部署至AEM作者和AEM發佈
   + 內嵌在`ui.content.publish`中的`/apps/my-app-packages/content/install.publish`只會將內容和設定部署到AEM發佈

>[!TIP]
>
>如需完整的程式碼片段，請參閱下方的[POM XML程式碼片段](#xml-embeddeds)區段。

### 容器封裝的篩選器定義 {#container-package-filter-definition}

由於程式碼和內容子套件內嵌在容器套件中，因此內嵌的目標路徑必須新增到容器專案的`filter.xml`。 這樣做可確保內巢狀件在建置時包含在容器套件中。

只要為包含要部署的子封裝的任何第二級資料夾新增`<filter root="/apps/<my-app>-packages"/>`專案。

>[!TIP]
>
>如需完整的程式碼片段，請參閱下方的[POM XML程式碼片段](#xml-container-package-filters)區段。

## 內嵌第三方套件 {#embedding-3rd-party-packages}

所有套件都必須可透過[Adobe的公用Maven成品存放庫](https://repo1.maven.org/maven2/com/adobe/)或可存取的公用、可參照的第三方Maven成品存放庫使用。

如果協力廠商套件位於&#x200B;**Adobe的公用Maven成品存放庫**，則Adobe Cloud Manager無需進一步設定即可解析成品。

如果協力廠商套件位於&#x200B;**公用協力廠商Maven成品存放庫**，則必須在專案的`pom.xml`中註冊此存放庫，並將其嵌入到上面概述的方法[之後](#embeddeds)。

應該使用協力廠商應用程式/聯結器的`all`封裝作為專案容器(`all`)封裝中的容器來內嵌協力廠商應用程式/聯結器。

新增Maven相依性會遵循標準Maven實務，而嵌入協力廠商成品（程式碼和內容套件）則是上述[概述的](#embedding-3rd-party-packages)。

>[!TIP]
>
>如需完整的程式碼片段，請參閱下方的[POM XML程式碼片段](#xml-3rd-party-maven-repositories)區段。

## 來自`ui.apps`個套件的`ui.content`之間的套件相依性 {#package-dependencies}

為確保正確安裝套件，建議建立套件間相依性。

一般規則是包含可變內容的套件(`ui.content`)應依存於支援呈現和使用可變內容的不可變程式碼(`ui.apps`)。

此一般規則的重大例外是如果不可變程式碼套件（`ui.apps`或任何其他），__only__&#x200B;包含OSGi套裝。 若是如此，任何AEM套件都不應宣告其上的相依性。 原因是因為&#x200B;__僅__&#x200B;包含OSGi套裝的不可變程式碼套件未向AEM [套件管理員](/help/implementing/developing/tools/package-manager.md)註冊。 因此，任何依賴它的AEM套件都有不滿意的相依性，且無法安裝。

>[!TIP]
>
>如需完整的程式碼片段，請參閱下方的[POM XML程式碼片段](#xml-package-dependencies)區段。

內容套件相依性的常見模式如下：

### 簡易部署套件相依性 {#simple-deployment-package-dependencies}

簡單大小寫會將`ui.content`可變內容套件設定為相依於`ui.apps`不可變程式碼套件。

+ `all`沒有相依性
   + `ui.apps`沒有相依性
   + `ui.content`依存於`ui.apps`

### 複雜的部署套件相依性 {#complex-deploxment-package-dependencies}

複雜的部署會依簡單案例展開，並設定相對應可變內容與不可變程式碼套件之間的相依性。 如有需要，也可在不可變程式碼套件之間建立相依性。

+ `all`沒有相依性
   + `common.ui.apps.common`沒有相依性
   + `site-a.ui.apps`依存於`common.ui.apps`
   + `site-a.ui.content`依存於`site-a.ui.apps`
   + `site-b.ui.apps`依存於`common.ui.apps`
   + `site-b.ui.content`依存於`site-b.ui.apps`

## 本機開發和部署 {#local-development-and-deployment}

本文中概述的專案結構和組織是&#x200B;**完全相容的**&#x200B;本機開發AEM執行個體。

## POM XML代碼片段 {#pom-xml-snippets}

以下是Maven `pom.xml`設定片段，可新增到Maven專案中以符合上述建議。

### 封裝型別 {#xml-package-types}

程式碼和內容封裝（部署為子封裝）必須宣告&#x200B;**應用程式**&#x200B;或&#x200B;**內容**&#x200B;的封裝型別（視其包含的內容而定）。

#### 容器封裝型別 {#container-package-types}

容器`all/pom.xml`專案&#x200B;**未**&#x200B;宣告`<packageType>`。

#### 程式碼（不可變）封裝型別 {#immutable-package-types}

程式碼套件必須將其`packageType`設定為`application`。

在`ui.apps/pom.xml`中，`<packageType>application</packageType>`外掛程式宣告的`filevault-package-maven-plugin`組建組態指示詞宣告其封裝型別。

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

#### 內容（可變）封裝型別 {#mutable-package-types}

內容套件必須將其`packageType`設定為`content`。

在`ui.content/pom.xml`中，`<packageType>content</packageType>`外掛程式宣告的`filevault-package-maven-plugin`組建組態指示詞會宣告其封裝型別。

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

### 將套件標籤為Adobe Cloud Manager部署 {#cloud-manager-target}

在每個產生套件的專 **案中** ，除容器(`all`)專案外，將外掛程式聲明的 `<cloudManagerTarget>none</cloudManagerTarget>` 組態新增至外掛程式宣告的組態，以確 `<properties>` `filevault-package-maven-plugin`**&#x200B;** 保Adobe Cloud Manager不會部署它們。容器(`all`)封裝應該是透過Cloud Manager部署的單一封裝，而這會嵌入所有必要的程式碼和內容封裝。

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

### 存放庫初始{#snippet-repo-init}

包含存放庫初始指令碼的Repo Init指令碼是透過`RepositoryInitializer`屬性在`scripts` OSGi工廠設定中定義。 因為這些指令碼是在OSGi設定中定義，所以它們可以透過執行模式使用常見的`../config.<runmode>`資料夾語意輕鬆設定範圍。

因為指令碼通常是多行宣告，在`.config`檔案中定義指令碼會比JSON型`.cfg.json`格式更容易。

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

`scripts` OSGi屬性包含由[Apache Sling的Repo Init語言](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language)定義的指示。

### 存放庫結構套件 {#xml-repository-structure-package}

在`ui.apps/pom.xml`與宣告程式碼套件(`pom.xml`)的任何其他`<packageType>application</packageType>`中，將下列存放庫結構套件組態新增至FileVault Maven外掛程式。 您可以[為您的專案](repository-structure-package.md)建立您自己的存放庫結構套件。

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

### 將子套件嵌入於容器套件 {#xml-embeddeds}

在`all/pom.xml`中，將下列`<embeddeds>`指令新增至`filevault-package-maven-plugin`外掛程式宣告。 請記住，**不要**&#x200B;使用`<subPackages>`設定。 原因是因為它包含`/etc/packages`中的子封裝，而非`/apps/my-app-packages/<application|content|container>/install(.author|.publish)?`。

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

### 容器封裝的篩選器定義 {#xml-container-package-filters}

在`all`專案的`filter.xml` (`all/src/main/content/jcr_root/META-INF/vault/definition/filter.xml`)中，**包含**&#x200B;任何包含要部署的子套件的`-packages`資料夾：

```xml
<filter root="/apps/my-app-packages"/>
```

如果內嵌目標中使用了多個`/apps/*-packages`，則必須在此列舉它們。

### 協力廠商Maven存放庫 {#xml-3rd-party-maven-repositories}

>[!WARNING]
>
>新增更多Maven存放庫可能會延長Maven建置時間，因為會檢查其他Maven存放庫是否相依性。

在Reactor專案的`pom.xml`中，新增任何必要的第三方公用Maven存放庫指示。 第三方存放庫提供者應該可以使用完整的`<repository>`設定。

```xml
<repositories>
  ...
  <repository>
      <id>3rd-party-repository</id>
      <name>Public Third-Party Repository</name>
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

### 來自`ui.apps`個套件的`ui.content`之間的套件相依性 {#xml-package-dependencies}

在`ui.content/pom.xml`中，將下列`<dependencies>`指令新增至`filevault-package-maven-plugin`外掛程式宣告。

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

### 正在清除容器專案的目標資料夾 {#xml-clean-container-package}

在`all/pom.xml`中，新增在Maven組建之前清除目標目錄的`maven-clean-plugin`外掛程式。

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
+ [FileVault Content Package Maven外掛程式](https://jackrabbit.apache.org/filevault-package-maven-plugin/)
