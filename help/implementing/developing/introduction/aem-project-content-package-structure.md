---
title: AEM 專案結構
description: 了解如何定義部署至Adobe Experience ManagerCloud Service的套件結構。
exl-id: 38f05723-5dad-417f-81ed-78a09880512a
source-git-commit: ed8150e3b1e7d318a15ad84ebda7df52cf40128b
workflow-type: tm+mt
source-wordcount: '2877'
ht-degree: 12%

---

# AEM 專案結構

>[!TIP]
>
>熟悉基本 [AEM專案原型使用](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)，和 [FileVault Content Maven插件](/help/implementing/developing/tools/maven-plugin.md) 因為本文以這些學習和概念為基礎。

本文概述Adobe Experience Manager Maven專案為與AEMas a Cloud Service相容所需的變更，確保專案遵守可變和不可變內容的分割、建立相依性以建立不衝突、確定性的部署，並封裝成可部署結構。

AEM應用程式部署必須由單一AEM套件組成。 此程式包又應包含子程式包，這些子程式包包括應用程式運行所需的所有內容，包括代碼、配置和任何支援的基準內容。

AEM需要分離內 **容和程式碼** ，這表示單一內容套件 **無法**&#x200B;部署至 ********`/apps` Runtime可寫區域 (例如，可寫區域)。`/content`、 `/conf`、 `/home`或其他非 `/apps`)。而應用程式必須將程式碼和內容分隔為獨立套件，以便部署至AEM。

本檔案中概述的套件結構與本機開 **發部署** 和AEM cloud服務部署都相容。

>[!TIP]
>
>本文檔中概述的配置由 [AEM Project Maven原型24或更新版本](https://github.com/adobe/aem-project-archetype/releases).

## 儲存庫的可變區與不可變區 {#mutable-vs-immutable}

`/apps` and `/libs`**are consed inmumable areas of AEM as they cannot be changed(create, update, delete)after AEM starts(i.e. at runtime)。**&#x200B;在運行時更改不可變區域的任何嘗試都將失敗。

儲存庫中的其他一切， `/content`, `/conf`, `/var`, `/etc`, `/oak:index`, `/system`, `/tmp`、等 全部 **可變** 區域，這表示在執行階段可以變更區域。

>[!WARNING]
>
>如舊版AEM, `/libs` 不應修改。 只有AEM產品代碼可部署至 `/libs`.

### Oak Indexes {#oak-indexes}

Oak索引(`/oak:index`)由AEMas a Cloud Service部署程式特別管理。 這是因為Cloud Manager必須等到部署任何新索引並完全重新編列索引後，才能切換至新程式碼影像。

因此，雖然Oak索引在執行時可變，但必須部署為程式碼，才能在安裝任何可變套件前先行安裝。 因此 `/oak:index` 設定是程式碼套件的一部分，而非內容套件的一部分 [如下所述](#recommended-package-structure).

>[!TIP]
>
>有關在AEMas a Cloud Service中建立索引的詳細資訊，請參閱本檔案 [內容搜尋與索引](/help/operations/indexing.md).

## 建議的封裝結構 {#recommended-package-structure}

![Experience Manager項目包結構](assets/content-package-organization.png)

此圖表概述了建議的項目結構和包部署對象。

建議的應用程式部署結構如下：

### 程式碼套件/ OSGi套件組合

+ 會產生OSGi套件Jar檔案，並直接內嵌於所有專案中。

+ 此 `ui.apps` 套件包含所有要部署的程式碼，且只會部署至 `/apps`. 共同元素 `ui.apps` 套件包括，但不限於：
   + [元件定義和HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=zh-Hant) 指令碼
      + `/apps/my-app/components`
   + JavaScript和CSS(透過 [用戶端程式庫](/help/implementing/developing/introduction/clientlibs.md))
      + `/apps/my-app/clientlibs`
   + [覆蓋](/help/implementing/developing/introduction/overlays.md) of `/libs`
      + `/apps/cq`, `/apps/dam/`、等
   + 後援內容感知設定
      + `/apps/settings`
   + ACL（權限）
      + 任何 `rep:policy` 適用於 `/apps`
   + [預編譯的套件指令碼](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/precompiled-bundled-scripts.html)

+ 此 `ui.config` 包，包含全部 [OSGi配置](/help/implementing/deploying/configuring-osgi.md):
   + 包含運行模式特定OSGi配置定義的組織資料夾
      + `/apps/my-app/osgiconfig`
   + 包含套用至所有目標AEMas a Cloud Service部署目標的預設OSGi設定的通用OSGi設定資料夾
      + `/apps/my-app/osgiconfig/config`
   + 運行模式特定的OSGi配置資料夾，該資料夾包含適用於所有目標AEMas a Cloud Service部署目標的預設OSGi配置
      + `/apps/my-app/osgiconfig/config.<author|publish>.<dev|stage|prod>`
   + Repo Init OSGi配置指令碼
      + [存放庫初始化](#repo-init) 是部署（可變）內容(邏輯上屬於AEM應用程式一部分)的建議方式。 Repo Init OSGi設定應放置在適當的 `config.<runmode>` 資料夾（如上所述），並用於定義：
         + 基線內容結構
         + 使用者
         + 服務用戶
         + 群組
         + ACL（權限）

>[!NOTE]
>
>必須將相同的程式碼部署至所有環境。 這是為了確保預備環境上的信賴驗證也正在生產中，所需的項目。 如需詳細資訊，請參閱 [執行模式](/help/implementing/deploying/overview.md#runmodes).


### 內容套件

+ 此 `ui.content` 套件包含所有內容和設定。 內容套件包含所有節點定義，但不在 `ui.apps` 或 `ui.config` 包，換句話說， `/apps` 或 `/oak:index`. 共同元素 `ui.content` 套件包括，但不限於：
   + 內容感知設定
      + `/conf`
   + 必要、複雜的內容結構(即 以存放庫初始化中定義的基準內容結構為基礎並延伸其過去的內容建立。)
      + `/content`, `/content/dam`、等
   + 受管轄的標籤分類
      + `/content/cq:tags`
   + 舊式等節點（理想情況下，將這些節點遷移到非/等位置）
      + `/etc`

### 容器包裝

+ 此 `all` 套件是容器套件，僅包含可部署的成品、OSGI套件組合Jar檔案、 `ui.apps`, `ui.config` 和 `ui.content` 包作為內嵌。 此 `all` 包不能 **任何內容或程式碼** ，而是將所有部署委派給存放庫的子套件或OSGi套件組合Jar檔案。

   現在已使用Maven包含套件 [FileVault Package Maven插件的嵌入式配置](#embeddeds)，而非 `<subPackages>` 設定。

   對於複雜的Experience Manager部署，可能需要建立多個 `ui.apps`, `ui.config` 和 `ui.content` 代表AEM中特定網站或租戶的專案/套件。 如果執行此操作，請確保可變內容和不可變內容之間的分割符合要求，並且所需的內容包和OSGi捆綁Jar檔案作為子包嵌入到 `all` 容器內容套件。

   例如，複雜的部署內容包結構可能如下所示：

   + `all` 內容包嵌入以下包，以建立單一部署對象
      + `common.ui.apps` 部署所需的代碼 **both** 網站A和網站B
      + `site-a.core` 站點A所需的OSGi捆綁Jar
      + `site-a.ui.apps` 部署網站A所需的代碼
      + `site-a.ui.config` 部署站點A所需的OSGi配置
      + `site-a.ui.content` 部署站點A所需的內容和配置
      + `site-b.core` 站點B所需的OSGi捆綁Jar
      + `site-b.ui.apps` 部署站點B所需的代碼
      + `site-b.ui.config` 部署站點B所需的OSGi配置
      + `site-b.ui.content` 部署站點B所需的內容和配置

### 額外的應用程式包{#extra-application-packages}

如果AEM部署使用其他AEM專案（其本身由其自己的程式碼和內容套件組成），則其容器套件應內嵌在專案的 `all` 包。

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

+ 容器包必須設定 `packageType` to `container`. 容器包不能直接包含OSGi包、OSGi配置，並且不允許使用 [安裝掛接](http://jackrabbit.apache.org/filevault/installhooks.html).
+ 代碼（不可變）包必須設定 `packageType` to `application`.
+ 內容（可變）包必須設定其 `packageType` to `content`.


如需詳細資訊，請參閱 [Apache Jackrabbit FileVault - Package Maven外掛程式檔案](https://jackrabbit.apache.org/filevault-package-maven-plugin/package-mojo.html#packageType) 和 [FileVault Maven配置代碼段](#marking-packages-for-deployment-by-adoube-cloud-manager) 下方。

>[!TIP]
>
>請參閱 [POM XML片段](#xml-package-types) 以取得完整的程式碼片段。

## 標示要由Analytics Cloud Manager部署的套件Adobe {#marking-packages-for-deployment-by-adoube-cloud-manager}

依預設，Adobe Cloud manager會收集由Maven組建版本產生的所有套件，但是，由於容器(`all`)套件是包含所有程式碼和內容套件的單一部署工件，因此我們必須確保僅部署容器( ****`all`)套件。為確保此，Maven構建版本生成的其他軟體包必須用的FileVault Content Package Maven插件配置進行標籤 `<properties><cloudManagerTarget>none</cloudManageTarget></properties>`。

>[!TIP]
>
>請參閱 [POM XML片段](#pom-xml-snippets) 以取得完整的程式碼片段。

## 存放庫初始化{#repo-init}

Repo Init提供了定義JCR結構的指令（或指令碼），從資料夾樹等常見節點結構到用戶、服務用戶、組和ACL定義。

Repo Init的主要優點是，它們具有執行其指令碼所定義所有動作的隱式權限，且會在部署生命週期早期叫用，以確保執行程式碼時存在所有必要的JCR結構。

而Repo Init指令碼本身則會存放在 `ui.config` 專案做為指令碼，可以且應該用來定義下列可變結構：

+ 基線內容結構
+ 服務用戶
+ 使用者
+ 群組
+ ACL

存放庫初始化指令碼儲存為 `scripts` 條目 `RepositoryInitializer` 因此，OSGi工廠設定可以透過執行模式以隱含方式鎖定目標，以允許AEM製作與AEM Publish Services的存放庫初始化指令碼之間，或甚至環境（Dev、Stage和Prod）之間的差異。

最好在 [`.config` OSGi配置格式](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-config-1) 因為它們支援多行，這是使用的最佳做法的例外情況 [`.cfg.json` 定義OSGi配置](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1).

請注意，在定義「用戶」和「組」時，只有組被視為應用程式的一部分，並應在此處定義其函式的整體。 組織使用者和群組仍應在AEM中執行階段定義；例如，如果自訂工作流程將工作指派給指定的群組，則應透過AEM應用程式中的存放庫初始化來定義該群組，但如果群組只是組織性的，例如「Wendy&#39;s Team」和「Sean&#39;s Team」，則這些是最佳定義，並在AEM的執行階段中加以管理。

>[!TIP]
>
>存放庫初始化指令碼 *必須* 在內嵌中定義 `scripts` 欄位，以及 `references` 配置將無法運作。

存放庫初始化指令碼的完整辭匯可在 [Apache Sling Repo Init檔案](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language).

>[!TIP]
>
>請參閱 [存放庫初始化程式片段](#snippet-repo-init) 以取得完整的程式碼片段。

## 儲存庫結構包 {#repository-structure-package}

程式碼套件需要配置FileVault Maven外掛程式的配置以參考 `<repositoryStructurePackage>` 這可強制結構相依性的正確性（以確保一個程式碼套件不會安裝在另一個程式碼套件上）。 您可以 [建立專案專用的存放庫結構套件](repository-structure-package.md).

這只是程 **式碼套件的必要** ，也就是任何標有的套件 `<packageType>application</packageType>`。

若要了解如何為應用程式建立存放庫結構套件，請參閱 [開發存放庫結構套件](repository-structure-package.md).

請注意，內容套件(`<packageType>content</packageType>`) **不** 需要此儲存庫結構包。

>[!TIP]
>
>請參閱 [POM XML片段](#xml-repository-structure-package) 以取得完整的程式碼片段。

## 在容器包中嵌入子包{#embeddeds}

內容或程式碼套件會放置在特殊的「側車」資料夾中，且可定位為使用FileVault Maven外掛程式的，以安裝在AEM作者、AEM發佈或兩者上 `<embeddeds>` 設定。 請注意， `<subPackages>` 不應使用設定。

常見的使用案例包括：

+ AEM製作使用者與AEM發佈使用者之間有所差異的ACL/權限
+ 僅用於支援AEM作者上活動的設定
+ 程式碼（例如與後台系統的整合），只需在AEM作者上執行

![內嵌套件](assets/embeddeds.png)

若要鎖定AEM作者、AEM發佈或兩者，套件會內嵌於 `all` 容器封裝（位於特殊資料夾位置），格式如下：

`/apps/<app-name>-packages/(content|application|container)/install(.author|.publish)?`

劃分此資料夾結構：

+ 第1層資料夾 **必須** `/apps`.
+ 第2層資料夾代表具有 `-packages` 後置修正至資料夾名稱。 通常只有一個第2級資料夾所有子包都嵌入在下，但是可以建立任意數量的第2級資料夾以最好地表示應用程式的邏輯結構：
   + `/apps/my-app-packages`
   + `/apps/my-other-app-packages`
   + `/apps/vendor-packages`

   >[!WARNING]
   >
   >根據慣例，子包嵌入資料夾的名稱為尾碼為 `-packages`。這可確保部署代碼和內容包 **未部署** ，而是不會部署任何子包的目標資料夾， `/apps/<app-name>/...` 從而導致破壞性和循環安裝行為。

+ 第3級資料夾必須是
   `application`, `content` 或 `container`
   + 此 `application` 資料夾保存代碼包
   + 此 `content` 資料夾保留內容包
   + 此 `container` 資料夾中包含 [額外的應用程式套件](#extra-application-packages) AEM應用程式可能包含的項目。
此資料夾名稱對應至 [封裝類型](#package-types) 包中。
+ 第4層資料夾包含子包，且必須是下列其中一個：
   + `install` 若要同時安裝 **在** AEM作者和AEM發佈上
   + `install.author` 僅 **安裝** 在AEM作者上
   + `install.publish` to **僅限** 在AEM發佈時安裝，請注意 `install.author` 和 `install.publish` 是支援的目標。 不支援其 **他執行模** 式。

例如，包含AEM製作和發佈特定套件的部署可能如下所示：

+ `all` 容器包嵌入以下包，以建立單一部署對象
   + `ui.apps` 嵌入 `/apps/my-app-packages/application/install` 將程式碼部署至AEM製作和AEM發佈
   + `ui.apps.author` 嵌入 `/apps/my-app-packages/application/install.author` 將程式碼部署至僅限AEM作者
   + `ui.content` 嵌入 `/apps/my-app-packages/content/install` 將內容和設定部署至AEM作者和AEM publish
   + `ui.content.publish` 嵌入 `/apps/my-app-packages/content/install.publish` 只將內容和設定部署至AEM發佈

>[!TIP]
>
>請參閱 [POM XML片段](#xml-embeddeds) 以取得完整的程式碼片段。

### 容器包的篩選器定義 {#container-package-filter-definition}

由於程式碼和內容子封裝內嵌在容器封裝中，因此必須將內嵌的目標路徑新增到容器專案的 `filter.xml` 確保內嵌套件在建置時包含在容器套件中。

只需新增 `<filter root="/apps/<my-app>-packages"/>` 包含要部署的子包的任何第2級資料夾的條目。

>[!TIP]
>
>請參閱 [POM XML片段](#xml-container-package-filters) 以取得完整的程式碼片段。

## 嵌入第三方包 {#embedding-3rd-party-packages}

所有套件皆必須透過 [Adobe的公用Maven工件儲存庫](https://repo1.maven.org/maven2/com/adobe/) 或是可供參考的公開第三方Maven工件存放庫。

如果第三方套件位於 **Adobe的公用Maven工件存放庫**，則Adobe Cloud manager無需進一步設定即可解析工件。

如果第三方包位於公 **用的第三方Maven對象儲存庫**，則必須按照上述方法在項目中註冊並嵌入此存 `pom.xml` 儲庫 [](#embeddeds)。

第三方應用程式/連接器應使用 `all` 封裝為專案容器中的容器(`all`)套件。

新增Maven相依性會遵循標準Maven實務，並內嵌第三方成品（程式碼和內容套件） [概述](#embedding-3rd-party-packages).

>[!TIP]
>
>請參閱 [POM XML片段](#xml-3rd-party-maven-repositories) 以取得完整的程式碼片段。

## 封裝之間的相依性 `ui.apps` 從 `ui.content` 套件 {#package-dependencies}

為確保正確安裝軟體包，建議建立軟體包間依賴項。

一般規則是包含可變內容(`ui.content`)應取決於不可修改的代碼(`ui.apps`)，支援可變內容的轉譯和使用。

此一般規則的一個明顯例外是不可變的代碼包(`ui.apps` 或任何其他), __僅限__ 包含OSGi套件組合。 若存在，則任何AEM套件都不應宣告相依性。 這是因為不可變的代碼包 __僅限__ 包含OSGi套件組合未向AEM註冊 [包管理器，](/help/implementing/developing/tools/package-manager.md) 因此，任何根據AEM套件的相依性將會不滿足，且無法安裝。

>[!TIP]
>
>請參閱 [POM XML片段](#xml-package-dependencies) 以取得完整的程式碼片段。

內容包依賴項的常見模式為：

### 簡單部署包依賴項 {#simple-deployment-package-dependencies}

簡單大小寫會設定 `ui.content` 可變的內容套件，依 `ui.apps` 不可變代碼包。

+ `all` 沒有依賴項
   + `ui.apps` 沒有依賴項
   + `ui.content` 取決於 `ui.apps`

### 複雜的部署包依賴項 {#complex-deploxment-package-dependencies}

複雜的部署會根據簡單的情況展開，並在對應的可變內容和不可變代碼包之間設定相依性。 視需要，也可在不可變代碼包之間建立相依性。

+ `all` 沒有依賴項
   + `common.ui.apps.common` 沒有依賴項
   + `site-a.ui.apps` 取決於 `common.ui.apps`
   + `site-a.ui.content` 取決於 `site-a.ui.apps`
   + `site-b.ui.apps` 取決於 `common.ui.apps`
   + `site-b.ui.content` 取決於 `site-b.ui.apps`

## 本地開發和部署 {#local-development-and-deployment}

本文概述的項目結構和組織為 **完全相容** 本機開發AEM例項。

## POM XML片段 {#pom-xml-snippets}

以下是Maven `pom.xml` 可新增至Maven專案的設定片段，以符合上述建議。

### 套件類型 {#xml-package-types}

程式碼和內容封裝 (部署為子封裝) 必須依其包含的內容來宣告 **應用****程式或內容**&#x200B;的封裝類型。

#### 容器包裝類型 {#container-package-types}

容器 `all/pom.xml` 專案 **不** 聲明 `<packageType>`.

#### 代碼（不可變）包類型 {#immutable-package-types}

程式碼套件必須設定 `packageType` to `application`.

在 `ui.apps/pom.xml`, `<packageType>application</packageType>` 構建配置指令 `filevault-package-maven-plugin` 插件聲明聲明其包類型。

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

內容套件必須設定 `packageType` to `content`.

在 `ui.content/pom.xml`, `<packageType>content</packageType>` 構建配置指令 `filevault-package-maven-plugin` 插件聲明聲明其包類型。

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

包含存放庫初始化指令碼的存放庫初始化指令碼，會在 `RepositoryInitializer` OSGi工廠配置(通過 `scripts` 屬性。 請注意，由於這些指令碼是在OSGi設定中定義的，因此可使用通常的執行模式，輕鬆限定範圍 `../config.<runmode>` 資料夾語義。

請注意，由於指令碼通常為多行聲明，因此在 `.config` 檔案，而非JSON型 `.cfg.json` 格式。

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

此 `scripts` OSGi屬性包含由 [Apache Sling的Repo Init語言](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language).

### 儲存庫結構包 {#xml-repository-structure-package}

在 `ui.apps/pom.xml` 和其他 `pom.xml` 聲明代碼包(`<packageType>application</packageType>`)，將以下儲存庫結構包配置添加到FileVault Maven插件中。 您可以 [建立專案專用的存放庫結構套件](repository-structure-package.md).

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

在 `all/pom.xml`，新增下列內容 `<embeddeds>` 指令 `filevault-package-maven-plugin` 外掛程式聲明。 記住， **不** 使用 `<subPackages>` 設定，因為這會包含子封裝於 `/etc/packages` 而非 `/apps/my-app-packages/<application|content|container>/install(.author|.publish)?`.

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

若為多個 `/apps/*-packages` 在內嵌目標中使用，則必須在此處列舉所有目標。

### 第三方Maven儲存庫 {#xml-3rd-party-maven-repositories}

>[!WARNING]
>
>新增更多Maven存放庫可能會延長Maven建置時間，因為會檢查其他Maven存放庫是否有相依性。

在反應堆項目 `pom.xml`，新增任何必要的第三方公用Maven存放庫指示。 完整 `<repository>` 配置應可從第三方儲存庫提供程式中使用。

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

### 封裝之間的相依性 `ui.apps` 從 `ui.content` 套件 {#xml-package-dependencies}

在 `ui.content/pom.xml`，新增下列內容 `<dependencies>` 指令 `filevault-package-maven-plugin` 外掛程式聲明。

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

在 `all/pom.xml` 新增 `maven-clean-plugin` 外掛程式，可在Maven組建之前清除目標目錄。

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
