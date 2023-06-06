---
title: 內容搜尋與索引
description: 內容搜尋與索引
exl-id: 4fe5375c-1c84-44e7-9f78-1ac18fc6ea6b
source-git-commit: 34189fd264d3ba2c1b0b22c527c2c5ac710fba21
workflow-type: tm+mt
source-wordcount: '2491'
ht-degree: 1%

---

# 內容搜尋與索引 {#indexing}

## AEMas a Cloud Service中的變更 {#changes-in-aem-as-a-cloud-service}

透過AEMas a Cloud Service，Adobe正在從AEM執行個體為中心的模型移動到具有n-x AEM Containers的服務型檢視，由Cloud Manager中的CI/CD管道驅動。 必須在部署之前指定索引設定，而不是在單一AEM執行個體上設定和維護索引。 生產環境中的設定變更顯然違反CI/CD原則。 同樣的情況也適用於索引變更，因為如果未指定在將索引投入生產之前測試和重新索引，索引變更可能會影響系統穩定性和效能。

以下是與AEM 6.5及舊版比較的主要變更清單：

1. 使用者將無法存取單一AEM執行個體的索引管理員，無法再偵錯、設定或維護索引。 它僅用於本機開發和內部部署。
1. 使用者不會變更單一AEM執行個體上的索引，也不必再擔心一致性檢查或重新編制索引。
1. 一般而言，索引變更會在進入生產階段之前啟動，以免迴避Cloud Manager CI/CD管道中的品質閘道，以及不會影響生產環境中的業務KPI。
1. 客戶可在執行階段取得所有相關量度（包括生產環境中的搜尋效能），以提供搜尋和索引主題的整體檢視。
1. 客戶將能夠根據自己的需求設定警報。
1. SRE全天候監控系統健康狀況，並會視需要及早採取行動。
1. 索引設定已透過部署變更。 索引定義變更的設定方式與其他內容變更相同。
1. 概略說明AEMas a Cloud Service，並匯入 [滾動部署模型](#index-management-using-rolling-deployments) 將存在兩組索引：一組用於舊版本，另一組用於新版本。
1. 客戶可以在Cloud Manager建置頁面上檢視索引工作是否完成，並將在新版本準備好接收流量時收到通知。

限制:

* 目前，僅型別為的索引支援AEMas a Cloud Service上的索引管理 `lucene`.
* 僅支援標準分析器（即產品隨附的分析器）。 不支援自訂分析器。
* 在內部，可以設定其他索引並用於查詢。 例如，根據 `damAssetLucene` 在Skyline上，索引實際上可能針對此索引的Elasticsearch版本執行。 應用程式和使用者通常不會看見此差異，但某些工具(例如 `explain` 功能會報告不同的索引。 如需Lucene索引和Elastic索引之間的差異，請參閱 [Apache Jackrabbit Oak中的Elastic檔案](https://jackrabbit.apache.org/oak/docs/query/elastic.html). 客戶不需要且無法直接設定Elasticsearch索引。

## 使用方式 {#how-to-use}

定義索引可以包含下列三個使用案例：

1. 新增客戶索引定義。
1. 更新現有的索引定義。 這實際上意味著新增現有索引定義的新版本。
1. 移除多餘或過時的現有索引。

對於上面的第1點和第2點，您需要在各自的Cloud Manager發行排程中建立新的索引定義，作為自訂程式碼庫的一部分。 如需詳細資訊，請參閱 [部署至AEMas a Cloud Service檔案](/help/implementing/deploying/overview.md).

## 索引名稱 {#index-names}

索引定義可以是：

1. 現成可用的索引。 一個範例是 `/oak:index/cqPageLucene-2`.
1. 現成可用索引的自訂。 客戶會定義此類自訂。 一個範例是 `/oak:index/cqPageLucene-2-custom-1`.
1. 完全自訂的索引。 一個範例是 `/oak:index/acme.product-1-custom-2`. 為了避免命名衝突，我們要求完全自訂的索引必須有首碼，例如 `acme.`

請注意，現成可用的自訂索引以及完全自訂的索引都需要包含 `-custom-`. 只有完全自訂的索引必須以前置詞開頭。

## 準備新的索引定義 {#preparing-the-new-index-definition}

>[!NOTE]
>
>如果自訂現成可用的索引，例如 `damAssetLucene-6`，請從以下位置複製最新的現成可用索引定義 *Cloud Service環境* 使用CRX DE封裝管理員(`/crx/packmgr/`) 。 然後將設定重新命名為，例如 `damAssetLucene-6-custom-1`，並在上方新增自訂內容。 這樣可確保不會無意中移除所需的設定。 例如， `tika` 節點在 `/oak:index/damAssetLucene-6/tika` 在cloud service的自訂索引中是必要的。 它不存在於Cloud SDK上。

您需要依照此命名模式，準備包含實際索引定義的新索引定義套件：

`<indexName>[-<productVersion>]-custom-<customVersion>`

然後需要將它放在 `ui.apps/src/main/content/jcr_root`. 所有自訂和自訂索引定義都需要儲存在 `/oak:index`.

套件的篩選器必須設定成保留現有（現成可用的索引）。 在檔案中 `ui.apps/src/main/content/META-INF/vault/filter.xml`，則需要列出每個自訂（或自訂）索引，例如 `<filter root="/oak:index/damAssetLucene-6-custom-1"/>`. 如果稍後變更索引版本，則需要調整篩選器。

<!-- Alexandru: temporarily drafting this statement due to CQDOC-17701

The package from the above sample is built as `com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`. -->

>[!NOTE]
>
>任何包含索引定義的內容套件都應該在（位於）內容套件的屬性檔案中設定以下屬性 `/META-INF/vault/properties.xml`：
>
>`noIntermediateSaves=true`

## 部署索引定義 {#deploying-index-definitions}

索引定義會標示為自訂並設定版本：

* 索引定義本身(例如 `/oak:index/ntBaseLucene-custom-1`)

若要部署自訂或自訂索引，索引定義(`/oak:index/definitionname`)必須透過以下方式傳送： `ui.apps` 透過Git和Cloud Manager部署程式。 例如，在FileVault篩選器中， `ui.apps/src/main/content/META-INF/vault/filter.xml`，分別列出每個自訂和自訂索引，例如 `<filter root="/oak:index/damAssetLucene-7-custom-1"/>`. 自訂/自訂索引定義本身隨後將儲存在檔案中 `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-7-custom-1/.content.xml`，如下所示：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:oak="https://jackrabbit.apache.org/oak/ns/1.0" xmlns:dam="http://www.day.com/dam/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:nt="http://www.jcp.org/jcr/nt/1.0" xmlns:rep="internal"
        jcr:primaryType="oak:QueryIndexDefinition"
        async="[async,nrt]"
        compatVersion="{Long}2"
        ...
        </indexRules>
        <tika jcr:primaryType="nt:unstructured">
            <config.xml jcr:primaryType="nt:file"/>
        </tika>
</jcr:root>
```

上述範例包含Apache Tika的設定。 Tika設定檔案會儲存在 `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-7-custom-1/tika/config.xml`.

### 專案設定

視使用的Jackrabbit Filevault Maven Package外掛程式版本而定，需要在專案中進行更多設定。 使用Jackrabbit Filevault Maven套件外掛程式版本時 **1.1.6** 或更新版本，然後檔案 `pom.xml` 「 」的外掛程式設定中必須包含下列區段 `filevault-package-maven-plugin`，在 `configuration/validatorsSettings` (之前 `jackrabbit-nodetypes`)：

```xml
<jackrabbit-packagetype>
    <options>
        <immutableRootNodeNames>apps,libs,oak:index</immutableRootNodeNames>
    </options>
</jackrabbit-packagetype>
```

此外，在此案例中 `vault-validation` 版本需要升級至較新版本：

```xml
<dependency>
    <groupId>org.apache.jackrabbit.vault</groupId>
    <artifactId>vault-validation</artifactId>
    <version>3.5.6</version>
</dependency>
```

然後，在 `ui.apps.structure/pom.xml` 和 `ui.apps/pom.xml`，的設定 `filevault-package-maven-plugin` 需要 `allowIndexDefinitions` 以及 `noIntermediateSaves` 已啟用。 選項 `noIntermediateSaves` 確保自動新增索引設定。

```xml
<groupId>org.apache.jackrabbit</groupId>
    <artifactId>filevault-package-maven-plugin</artifactId>
    <configuration>
        <allowIndexDefinitions>true</allowIndexDefinitions>
        <properties>
            <cloudManagerTarget>none</cloudManagerTarget>
            <noIntermediateSaves>true</noIntermediateSaves>
        </properties>
    ...
```

在 `ui.apps.structure/pom.xml`，則 `filters` 此外掛程式的區段必須包含篩選根，如下所示：

```xml
<filter><root>/oak:index</root></filter>
```

新增索引定義後，需要透過Cloud Manager部署新應用程式。 部署後，會啟動兩個工作，負責將索引定義分別新增（及視需要合併）至MongoDB和Azure區段存放區，以供編寫和發佈。 在切換開始之前，基礎存放庫會使用新的索引定義重新編制索引。

### 注意

如果您在Filevault驗證中觀察到以下錯誤 <br>
`[ERROR] ValidationViolation: "jackrabbit-nodetypes: Mandatory child node missing: jcr:content [nt:base] inside node with types [nt:file]"` <br>
然後，可以執行以下任一步驟來修正問題 —  <br>
1. 將filevault降級為1.0.4版，並將以下內容新增至頂層pom：

```xml
<allowIndexDefinitions>true</allowIndexDefinitions>
```

以下範例說明將上述設定放入pom中的位置。

```xml
<plugin>
    <groupId>org.apache.jackrabbit</groupId>
    <artifactId>filevault-package-maven-plugin</artifactId>
    <configuration>
        <properties>
        ...
        </properties>
        ...
        <allowIndexDefinitions>true</allowIndexDefinitions>
        <repositoryStructurePackages>
        ...
        </repositoryStructurePackages>
        <dependencies>
        ...
        </dependencies>
    </configuration>
</plugin>
```

1. 停用節點型別驗證。 在filevault外掛程式設定的jackrabbit-nodetypes區段中設定以下屬性：

```xml
<isDisabled>true</isDisabled>
```

以下範例說明將上述設定放入pom中的位置。

```xml
<plugin>
    <groupId>org.apache.jackrabbit</groupId>
    <artifactId>filevault-package-maven-plugin</artifactId>
    ...
    <configuration>
    ...
        <validatorsSettings>
        ...
            <jackrabbit-nodetypes>
                <isDisabled>true</isDisabled>
            </jackrabbit-nodetypes>
        </validatorsSettings>
    </configuration>
</plugin>
```

>[!TIP]
>
>如需AEMas a Cloud Service所需套件結構的進一步詳細資訊，請參閱本檔案 [AEM專案結構。](/help/implementing/developing/introduction/aem-project-content-package-structure.md)

## 使用滾動式部署進行索引管理 {#index-management-using-rolling-deployments}

### 索引管理是什麼 {#what-is-index-management}

索引管理是關於新增、移除和變更索引。 變更 *定義* 索引的建立速度很快，但套用變更（通常稱為「建立索引」，或對於現有索引稱為「重新索引」）需要時間。 這不是立即發生的：必須掃描存放庫才能為資料編制索引。

### 什麼是滾動式部署 {#what-are-rolling-deployments}

滾動式部署可減少停機時間。 此外，它還可實現零停機升級並提供快速回覆。 應用程式的舊版本與應用程式的新版本同時執行。

### 唯讀和讀寫區域 {#read-only-and-read-write-areas}

存放庫的某些區域（存放庫的唯讀部分）在舊版本和新版本的應用程式中可能不同。 存放庫的唯讀區域通常是 `/app` 和 `/libs`. 在下列範例中，斜體是用來標籤唯讀區域，而粗體則是用來標籤讀寫區域。

* **/**
* */apps （唯讀）*
* **/content**
* */libs （唯讀）*
* **/oak：index**
* **/oak：index/acme.**
* **/jcr：system**
* **/system**
* **/var**

存放庫的讀寫區域會在所有版本的應用程式之間共用，而每個版本的應用程式都有一組特定的讀寫區域 `/apps` 和 `/libs`.

### 索引管理（不進行滾動部署） {#index-management-without-rolling-deployments}

在開發期間或使用內部部署時，可在執行階段新增、移除或變更索引。 索引一有可用就會立即使用。 如果舊版應用程式中尚未使用索引，則通常會在排程的停機期間建立索引。 移除索引或變更現有索引時，也會發生相同的情況。 移除索引時，一旦被移除，就無法使用索引。

### 使用滾動式部署進行索引管理 {#index-management-with-rolling-deployments}

滾動式部署不會造成停機時間。 在更新期間，應用程式的舊版本（例如，版本1）和新版本（版本2）會針對相同的存放庫同時執行。 如果版本1要求某個索引可用，則不得在版本2中移除此索引。 稍後應該移除索引，例如在版本3中，此時可以保證應用程式版本1不再執行。 此外，應用程式應編寫得即使版本2正在執行以及有版本2的索引可用，版本1也能正常運作。

升級到新版本完成後，系統可以對舊索引進行垃圾回收。 舊索引可能仍會保留一段時間，以加速回滾（如果需要回滾）。

下表顯示五個索引定義： index `cqPageLucene` 索引時用於兩個版本 `damAssetLucene-custom-1` 僅用於版本2。

>[!NOTE]
>
>`<indexName>-custom-<customerVersionNumber>` 需要，AEMas a Cloud Service才能將它標示為現有索引的取代。

| 索引 | 現成可用的索引 | 用於第1版 | 用於第2版 |
|---|---|---|---|
| /oak：index/damAssetLucene | 是 | 是 | 否 |
| /oak：index/damAssetLucene-custom-1 | 是（自訂） | 否 | 是 |
| /oak：index/acme.product-custom-1 | 否 | 是 | 否 |
| /oak：index/acme.product-custom-2 | 否 | 否 | 是 |
| /oak：index/cqPageLucene | 是 | 是 | 是 |

每次變更索引時，版本編號都會增加。 為了避免自訂索引名稱與產品本身的索引名稱衝突，自訂索引以及對現成索引的變更必須以結尾 `-custom-<number>`.

### 現成可用索引的變更 {#changes-to-out-of-the-box-indexes}

一旦Adobe變更開箱即用的索引，例如「damAssetLucene」或「cqPageLucene」，新的索引命名為 `damAssetLucene-2` 或 `cqPageLucene-2` 會建立，或如果已自訂索引，則會將自訂索引定義與現成索引中的變更合併，如下所示。 合併變更會自動進行。 這表示如果現成可用的索引變更，您就不需要執行任何動作。 不過，之後可以再次自訂索引。

| 索引 | 現成可用的索引 | 用於第2版 | 在版本3中使用 |
|---|---|---|---|
| /oak：index/damAssetLucene-custom-1 | 是（自訂） | 是 | 否 |
| /oak：index/damAssetLucene-2-custom-1 | 是（自動從damAssetLucene-custom-1和damAssetLucene-2合併） | 否 | 是 |
| /oak：index/cqPageLucene | 是 | 是 | 否 |
| /oak：index/cqPageLucene-2 | 是 | 否 | 是 |

### 目前限制 {#current-limitations}

目前僅型別為的索引支援索引管理 `lucene`，搭配 `compatVersion` 設定為 `2`. 在內部，可以設定其他索引並用於查詢，例如Elasticsearch索引。 針對以下專案編寫的查詢： `damAssetLucene` 在AEMas a Cloud Service上，索引實際上可能針對此索引的Elasticsearch版本執行。 應用程式一般使用者不會察覺到這種差異，但某些工具(例如 `explain` 功能會報告不同的索引。 如需Lucene和Elasticsearch索引之間的差異，請參閱 [Apache Jackrabbit Oak中的Elasticsearch檔案](https://jackrabbit.apache.org/oak/docs/query/elastic.html). 客戶不能也不需要直接設定Elasticsearch索引。

僅支援內建分析器（即產品隨附的分析器）。 不支援自訂分析器。

為獲得最佳作業效能，索引不應過大。 所有索引的總計大小可作為參考：如果在新增自訂索引並在開發環境中調整標準索引後，這會增加100%以上，則應調整自訂索引定義。 AEMas a Cloud Service可防止部署可能對系統穩定性和效能造成負面影響的索引。

### 新增索引 {#adding-an-index}

若要新增名為的完全自訂索引 `/oak:index/acme.product-custom-1` 若要用於新版本的應用程式和更新版本，必須依照以下方式設定索引：

`acme.product-1-custom-1`

其原理是在索引名稱前面加一個自訂識別碼，後面加一個點(**`.`**)。 識別碼的長度應介於2到5個字元之間。

如上所述，這可確保只有新版本的應用程式才會使用索引。

### 變更索引 {#changing-an-index}

變更現有索引時，需要以變更的索引定義新增新索引。 例如，考慮現有的索引 `/oak:index/acme.product-custom-1` 已變更。 舊索引儲存在 `/oak:index/acme.product-custom-1`，而新索引會儲存在 `/oak:index/acme.product-custom-2`.

應用程式的舊版本會使用以下設定：

`/oak:index/acme.product-custom-1`

應用程式的新版本會使用下列（已變更）設定：

`/oak:index/acme.product-custom-2`

>[!NOTE]
>
>AEMas a Cloud Service上的索引定義可能與本機開發執行個體上的索引定義不完全相符。 開發執行個體沒有Tika設定，而AEMas a Cloud Service執行個體有。 如果您使用Tika設定自訂索引，請保留Tika設定。

### 還原變更 {#undoing-a-change}

有時需要還原索引定義中的變更。 原因可能是錯誤地進行了變更，或不再需要變更。 例如，索引定義 `damAssetLucene-8-custom-3` 錯誤建立且已部署。 因此，您可能想要還原成先前的索引定義 `damAssetLucene-8-custom-2`. 為此，您需要新增一個名為的索引 `damAssetLucene-8-custom-4` 包含上一個索引的定義， `damAssetLucene-8-custom-2`.

### 移除索引 {#removing-an-index}

以下內容僅適用於自訂索引。 產品索引無法移除，因為AEM正在使用它們。

如果要在應用程式的較新版本中移除索引，您可以使用新名稱來定義空白索引（從未使用且不包含任何資料的空白索引）。 在此範例中，您可以將其命名 `/oak:index/acme.product-custom-3`. 這會取代索引 `/oak:index/acme.product-custom-2`. 一次 `/oak:index/acme.product-custom-2` 被系統移除，空索引 `/oak:index/acme.product-custom-3` 然後也可以移除。 這類空白索引的範例為：

```xml
<acme.product-custom-3
        jcr:primaryType="oak:QueryIndexDefinition"
        async="async"
        compatVersion="2"
        includedPaths="/dummy"
        queryPaths="/dummy"
        type="lucene">
        <indexRules jcr:primaryType="nt:unstructured">
            <rep:root jcr:primaryType="nt:unstructured">
                <properties jcr:primaryType="nt:unstructured">
                    <dummy
                        jcr:primaryType="nt:unstructured"
                        name="dummy"
                        propertyIndex="{Boolean}true"/>
                </properties>
            </rep:root>
        </indexRules>
</acme.product-custom-3>
```

如果不再需要自訂現成索引，則必須複製現成索引定義。 例如，如果您已經部署 `damAssetLucene-8-custom-3`，但不再需要自訂，且想要切換回預設值 `damAssetLucene-8` 索引，則必須新增索引 `damAssetLucene-8-custom-4` 包含下列專案的索引定義 `damAssetLucene-8`.

## 索引和查詢最佳化 {#index-query-optimizations}

Apache Jackrabbit Oak可讓彈性的索引設定有效地處理搜尋查詢。 索引對於大型存放庫尤其重要。 請確定所有查詢都有適當的索引作為支援。 沒有適當索引的查詢可能會讀取數千個節點，然後將其記錄為警告。

請參閱 [本檔案](query-and-indexing-best-practices.md) 有關如何最佳化查詢和索引的資訊。
