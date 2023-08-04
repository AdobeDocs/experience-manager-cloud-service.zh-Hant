---
title: 內容搜尋與索引
description: 瞭解AEMas a Cloud Service中的內容搜尋和索引。
exl-id: 4fe5375c-1c84-44e7-9f78-1ac18fc6ea6b
source-git-commit: 8c73805b6ed1b7a03c65b4d21a4252c1412a5742
workflow-type: tm+mt
source-wordcount: '2325'
ht-degree: 1%

---

# 內容搜尋與索引 {#indexing}

## AEMas a Cloud Service中的變更 {#changes-in-aem-as-a-cloud-service}

透過AEMas a Cloud Service，Adobe正在從AEM執行個體為中心的模式轉移到具有n-x AEM容器（由Cloud Manager中的CI/CD管道驅動）的服務型檢視。 必須在部署之前指定索引設定，而不是在單一AEM執行個體上設定和維護索引。 生產環境中的設定變更顯然違反CI/CD政策。 同樣的情況也適用於索引變更，因為如果未指定在將索引投入生產之前測試和重新索引，索引變更可能會影響系統穩定性和效能。

以下是與AEM 6.5和更早版本相比的主要變更清單：

1. 使用者無法再存取單一AEM執行個體的索引管理員來偵錯、設定或維護索引。 它僅用於本機開發和內部部署。
1. 使用者不會變更單一AEM執行個體上的索引，也不必再擔心一致性檢查或重新編制索引。
1. 一般而言，索引變更會在進入生產階段前開始，以免迴避Cloud Manager CI/CD管道中的品質閘道，及不影響生產階段的業務KPI。
1. 客戶可在執行階段使用所有相關量度（包括生產環境中的搜尋效能），提供搜尋和建立索引主題的整體檢視。
1. 客戶可以根據需求設定警報。
1. SRE全天候監控系統健康狀況，並儘早採取動作。
1. 索引設定已透過部署變更。 索引定義變更的設定方式與其他內容變更相同。
1. 概略介紹AEMas a Cloud Service，並匯入 [滾動部署模型](#index-management-using-rolling-deployments)，則有兩組索引：一組用於舊版本，另一組用於新版本。
1. 客戶可以在Cloud Manager建置頁面上檢視索引工作是否完成，並在新版本準備好接收流量時收到通知。

限制:

* 目前，只有型別的索引才支援AEMas a Cloud Service上的索引管理 `lucene`.
* 僅支援標準分析器（即產品隨附的分析器）。 不支援自訂分析器。
* 在內部，可以設定其他索引並用於查詢。 例如，根據下列條件編寫的查詢： `damAssetLucene` 在Skyline上，索引實際上可能會針對此索引的Elasticsearch版本執行。 應用程式和使用者通常不會看到這種差異，但是，某些工具，例如 `explain` 功能會報告不同的索引。 如需Lucene索引與Elastic索引之間的差異，請參閱 [Apache Jackrabbit Oak中的Elastic檔案](https://jackrabbit.apache.org/oak/docs/query/elastic.html). 客戶不需要且無法直接設定Elasticsearch索引。
* 依類似的特徵向量搜尋(`useInSimilarity = true`)不受支援。

## 使用方式 {#how-to-use}

索引定義可以分為三個主要使用案例，如下所示：

1. **新增** 新的自訂索引定義。
2. **更新** 藉由新增新版本來建立現有的索引定義。
3. **移除** 不再需要的索引定義。

對於上面的第1點和第2點，您需要在各自的Cloud Manager發行排程中建立新的索引定義，作為自訂程式碼庫的一部分。 如需詳細資訊，請參閱 [部署至AEMas a Cloud Service](/help/implementing/deploying/overview.md) 檔案。

## 索引名稱 {#index-names}

索引定義可以屬於以下類別之一：

1. 開箱即用(OOTB)索引。 例如： `/oak:index/cqPageLucene-2` 或 `/oak:index/damAssetLucene-8`.

2. OOTB索引的自訂。 這些由附加表示 `-custom-` 後面接著原始索引名稱的數值識別碼。 例如：`/oak:index/damAssetLucene-8-custom-1`。

3. 完全自訂索引：您可以從頭開始建立全新的索引。 它們的名稱必須有首碼以避免命名衝突。 例如： `/oak:index/acme.product-1-custom-2`，首碼為 `acme.`

## 準備新的索引定義 {#preparing-the-new-index-definition}

>[!NOTE]
>
>如果自訂現成可用的索引，例如 `damAssetLucene-8`，請從以下位置複製最新的現成可用索引定義： *Cloud Service環境* 使用CRX DE封裝管理員(`/crx/packmgr/`) 。 將其重新命名為 `damAssetLucene-8-custom-1` ，並將您的自訂專案新增至XML檔案中。 這可確保不會無意中移除所需的設定。 例如， `tika` 節點在 `/oak:index/damAssetLucene-8/tika` 在雲端服務的自訂索引中是必要專案。 它不存在於Cloud SDK上。

針對OOTB索引的自訂，請準備包含遵循此命名模式之實際索引定義的新套件：

`<indexName>-<productVersion>-custom-<customVersion>`

對於完全自訂的索引，請準備新的索引定義封裝，其中包含遵循此命名模式的索引定義：

`<prefix>.<indexName>-<productVersion>-custom-<customVersion>`

<!-- Alexandru: temporarily drafting this statement due to CQDOC-17701

The package from the above sample is built as `com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`. -->

>[!NOTE]
>
>任何包含索引定義的內容封裝，都應在位於的內容封裝屬性檔案中設定下列屬性 `<package_name>/META-INF/vault/properties.xml`：
>
> * `noIntermediateSaves=true`
>
> * `allowIndexDefinitions=true`

## 部署自訂索引定義 {#deploying-custom-index-definitions}

說明如何部署自訂版本的現成可用索引 `damAssetLucene-8`，我們會提供逐步指南。 在此範例中，我們會將其重新命名為 `damAssetLucene-8-custom-1`. 然後程式如下：

1. 在中建立具有更新索引名稱的新資料夾 `ui.apps` 目錄：
   * 範例: `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-8-custom-1/`

2. 新增設定檔 `.content.xml` ，並將自訂組態置於新建立的資料夾中。 以下是自訂的範例：檔案名稱： `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-8-custom-1/.content.xml`

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:dam="http://www.day.com/dam/1.0" xmlns:nt="http://www.jcp.org/jcr/nt/1.0" xmlns:oak="http://jackrabbit.apache.org/oak/ns/1.0" xmlns:rep="internal"
       jcr:mixinTypes="[rep:AccessControllable]"
       jcr:primaryType="oak:QueryIndexDefinition"
       async="[async,nrt]"
       compatVersion="{Long}2"
       evaluatePathRestrictions="{Boolean}true"
       includedPaths="[/content/dam]"
       maxFieldLength="{Long}100000"
       type="lucene">
       <facets
           jcr:primaryType="nt:unstructured"
           secure="statistical"
           topChildren="100"/>
       <indexRules jcr:primaryType="nt:unstructured">
           <dam:Asset jcr:primaryType="nt:unstructured">
               <properties jcr:primaryType="nt:unstructured">
                   <cqTags
                       jcr:primaryType="nt:unstructured"
                       name="jcr:content/metadata/cq:tags"
                       nodeScopeIndex="{Boolean}true"
                       propertyIndex="{Boolean}true"
                       useInSpellcheck="{Boolean}true"
                       useInSuggest="{Boolean}true"/>
               </properties>
           </dam:Asset>
       </indexRules>
       <tika jcr:primaryType="nt:folder">
           <config.xml jcr:primaryType="nt:file"/>
       </tika>
   </jcr:root>
   ```

3. 將專案新增至中的FileVault篩選器 `ui.apps/src/main/content/META-INF/vault/filter.xml`：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <workspaceFilter version="1.0">
       ...
       <filter root="/oak:index/damAssetLucene-8-custom-1"/> 
   </workspaceFilter>
   ```

4. 在中新增Apache Tika的設定檔： `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-8-custom-1/tika/config.xml`：

   ```xml
   <properties>
       <detectors>
           <detector class="org.apache.tika.detect.TypeDetector"/>
       </detectors>
       <parsers>
           <parser class="org.apache.tika.parser.DefaultParser">
           <mime>text/plain</mime>
           </parser>
       </parsers>
       <service-loader initializableProblemHandler="ignore" dynamic="true"/>
   </properties>
   ```

5. 確保您的設定符合 [專案設定](#project-configuration) 區段。 相應地進行任何必要的調整。

## 專案設定

我們強烈建議使用>=版 `1.3.2` Jackrabbit的 `filevault-package-maven-plugin`. 將其整合至專案的步驟如下：

1. 更新最上層的版本 `pom.xml`：

   ```xml
   <plugin>
       <groupId>org.apache.jackrabbit</groupId>
           <artifactId>filevault-package-maven-plugin</artifactId>
           ...
           <version>1.3.2</version>
       ...
   </plugin>
   ```

2. 新增下列專案至最上層 `pom.xml`：

   ```xml
   <jackrabbit-packagetype>
       <options>   
           <immutableRootNodeNames>apps,libs,oak:index</immutableRootNodeNames>
       </options>
   </jackrabbit-packagetype>
   ```

   以下是專案最上層的範例 `pom.xml` 包含上述設定的檔案：

   檔案名稱: `pom.xml`

   ```xml
   <plugin>
       <groupId>org.apache.jackrabbit</groupId>
           <artifactId>filevault-package-maven-plugin</artifactId>
           ...
           <version>1.3.2</version>
           <configuration>
               ...
               <validatorsSettings>
                   <jackrabbit-packagetype>
                       <options>
                           <immutableRootNodeNames>apps,libs,oak:index</immutableRootNodeNames>
                       </options>
                   </jackrabbit-packagetype>
                   ...
               ...
   </plugin>
   ```

3. 在 `ui.apps/pom.xml` 和 `ui.apps.structure/pom.xml` 您必須啟用 `allowIndexDefinitions` 和 `noIntermediateSaves` 中的選項 `filevault-package-maven-plugin`. 正在啟用 `allowIndexDefinitions` 允許自訂索引定義，而 `noIntermediateSaves` 確保自動新增設定。

   檔案名稱： `ui.apps/pom.xml` 和 `ui.apps.structure/pom.xml`

   ```xml
   <plugin>
       <groupId>org.apache.jackrabbit</groupId>
           <artifactId>filevault-package-maven-plugin</artifactId>
           <configuration>
               <allowIndexDefinitions>true</allowIndexDefinitions>
               <properties>
                   <cloudManagerTarget>none</cloudManagerTarget>
                   <noIntermediateSaves>true</noIntermediateSaves>
               </properties>
       ...
   </plugin>
   ```

4. 新增篩選器 `/oak:index` 在 `ui.apps.structure/pom.xml`：

   ```xml
   <filters>
       ...
       <filter><root>/oak:index</root></filter>
   </filters>
   ```

新增索引定義後，請使用Cloud Manager部署新的應用程式。 此部署會起始兩個工作，負責將索引定義分別新增（並在必要時合併）至MongoDB和Azure區段存放區以供製作和發佈。 在切換之前，基礎存放庫會使用更新的索引定義重新索引。

>[!TIP]
>
>如需AEMas a Cloud Service所需套件結構的更多詳細資訊，請參閱檔案 [AEM專案結構](/help/implementing/developing/introduction/aem-project-content-package-structure.md).

## 使用滾動式部署的索引管理 {#index-management-using-rolling-deployments}

### 索引管理是什麼 {#what-is-index-management}

索引管理是關於新增、移除和變更索引。 變更 *定義* 索引的建立速度很快，但套用變更（通常稱為「建立索引」，或針對現有索引稱為「重新索引」）需要時間。 此動作並非即時：必須掃描存放庫才能為資料編制索引。

### 哪些是滾動式部署 {#what-are-rolling-deployments}

滾動式部署可減少停機時間。 此外，它還可實現零停機升級並提供快速回覆。 應用程式的舊版本與應用程式的新版本同時執行。

### 唯讀和讀寫區域 {#read-only-and-read-write-areas}

存放庫的特定區域（存放庫的唯讀部分）在舊版本和新版本的應用程式中可能不同。 存放庫的唯讀區域通常是 `/app` 和 `/libs`. 在下列範例中，斜體是用來標籤唯讀區域，而粗體則是用來標籤讀寫區域。

* **/**
* */apps （唯讀）*
* **/content**
* */libs （唯讀）*
* **/oak：index**
* **/oak：index/acme。**
* **/jcr：system**
* **/system**
* **/var**

存放庫的讀寫區域會在所有應用程式版本之間共用，而每個應用程式版本都有一組特定的讀寫區域 `/apps` 和 `/libs`.

### 索引管理，不進行滾動部署 {#index-management-without-rolling-deployments}

在開發期間或使用內部部署安裝時，可在執行階段新增、移除或變更索引。 當索引可用時，即會加以使用。 如果舊版應用程式尚未使用索引，則通常會在排程的停機期間建立索引。 移除索引或變更現有索引時，也會發生相同的情況。 移除索引時，該索引在移除後會變成無法使用。

### 使用滾動式部署的索引管理 {#index-management-with-rolling-deployments}

滾動式部署沒有停機時間。 在更新期間，應用程式的舊版本（例如版本1）和新版本（版本2）會針對相同的存放庫同時執行。 如果版本1要求某個索引可用，則不得在版本2中移除此索引。 稍後應移除索引，例如版本3，此時可保證應用程式的版本1不再執行。 此外，應用程式的編寫應使版本1運作良好，即使版本2正在執行以及有版本2的索引可用。

升級到新版本後，系統可以對舊索引進行垃圾回收。 舊索引可能仍會保留一段時間，以加速倒回（如果需要倒回）。

下表顯示五個索引定義： index `cqPageLucene` 索引時用於兩個版本 `damAssetLucene-custom-1` 僅用於版本2。

>[!NOTE]
>
>此 `<indexName>-custom-<customerVersionNumber>` 需要，AEMas a Cloud Service才能將其標示為現有索引的取代。

| 索引 | 現成索引 | 用於版本1 | 用於版本2 |
|---|---|---|---|
| /oak：index/damAssetLucene | 是 | 是 | 否 |
| /oak：index/damAssetLucene-custom-1 | 是（自訂） | 否 | 是 |
| /oak：index/acme.product-custom-1 | 否 | 是 | 否 |
| /oak：index/acme.product-custom-2 | 否 | 否 | 是 |
| /oak：index/cqPageLucene | 是 | 是 | 是 |

每次變更索引時，版本號碼都會增加。 為了避免自訂索引名稱與產品本身的索引名稱衝突，自訂索引以及對現成索引的變更必須以結尾 `-custom-<number>`.

### 現成可用索引的變更 {#changes-to-out-of-the-box-indexes}

Adobe變更開箱即用的索引（例如「damAssetLucene」或「cqPageLucene」）後，新的索引命名為 `damAssetLucene-2` 或 `cqPageLucene-2` 「 」已建立。 或者，如果已經自訂索引，自訂的索引定義會與現成索引中的變更合併，如下所示。 合併變更會自動進行。 這表示如果現成索引變更，您不需要執行任何動作。 不過，之後可以再次自訂索引。

| 索引 | 現成索引 | 用於版本2 | 用於版本3 |
|---|---|---|---|
| /oak：index/damAssetLucene-custom-1 | 是（自訂） | 是 | 否 |
| /oak：index/damAssetLucene-2-custom-1 | 是（自動從damAssetLucene-custom-1和damAssetLucene-2合併） | 否 | 是 |
| /oak：index/cqPageLucene | 是 | 是 | 否 |
| /oak：index/cqPageLucene-2 | 是 | 否 | 是 |

### 目前限制 {#current-limitations}

只有型別的索引才支援索引管理 `lucene`，使用 `compatVersion` 設為 `2`. 在內部，可以設定其他索引並用於查詢，例如Elasticsearch索引。 針對寫入的查詢 `damAssetLucene` 在AEMas a Cloud Service上，索引實際上可能會針對此索引的Elasticsearch版本執行。 應用程式一般使用者不會看到這種差異，但某些工具(例如 `explain` 功能會報告不同的索引。 如需Lucene和Elasticsearch索引之間的差異，請參閱 [Apache Jackrabbit Oak中的Elasticsearch檔案](https://jackrabbit.apache.org/oak/docs/query/elastic.html). 客戶不能也不需要直接設定Elasticsearch索引。

僅支援內建分析器（即產品隨附的分析器）。 不支援自訂分析器。

為獲得最佳作業效能，索引不應過大。 所有索引的總計大小均可作為參考使用。 如果在新增自訂索引後，此大小增加超過100%，並且在開發環境中調整了標準索引，則應調整自訂索引定義。 AEMas a Cloud Service可防止部署可能對系統穩定性和效能造成負面影響的索引。

### 新增索引 {#adding-an-index}

若要新增名為的完整自訂索引 `/oak:index/acme.product-custom-1`，而要在新版本的應用程式和更新版本中使用，必須依照以下方式設定索引：

`acme.product-1-custom-1`

此設定的運作方式是在索引名稱前面加上自訂識別碼，後面接著一個點(**`.`**)。 識別碼的長度應該介於2到5個字元之間。

如上所述，此設定可確保只有新版本的應用程式才會使用索引。

### 變更索引 {#changing-an-index}

變更現有索引時，必須新增已變更索引定義的新索引。 例如，考慮現有的索引 `/oak:index/acme.product-custom-1` 已變更。 舊索引儲存在 `/oak:index/acme.product-custom-1`，而新索引會儲存在 `/oak:index/acme.product-custom-2`.

應用程式的舊版本會使用以下設定：

`/oak:index/acme.product-custom-1`

應用程式的新版本會使用下列（已變更）組態：

`/oak:index/acme.product-custom-2`

>[!NOTE]
>
>AEMas a Cloud Service上的索引定義可能與本機開發執行個體上的索引定義不完全相符。 開發執行個體沒有Tika設定，而AEMas a Cloud Service執行個體有。 如果您使用Tika設定自訂索引，請保留Tika設定。

### 復原變更 {#undoing-a-change}

有時候，必須復原索引定義中的修改。 這可能是由於意外錯誤或不再需要修改所造成。 以索引定義為例 `damAssetLucene-8-custom-3,` 錯誤建立且已部署。 因此，您想要回復到先前的索引定義， `damAssetLucene-8-custom-2.` 若要完成此操作，您必須引入名為的新索引 `damAssetLucene-8-custom-4` 合併先前索引的定義， `damAssetLucene-8-custom-2.`

### 移除索引 {#removing-an-index}

下列專案僅適用於自訂索引。 當AEM使用產品索引時，無法移除這些索引。

如果在較新版本的應用程式中移除索引，您可以使用新名稱定義空白索引（從未使用且不含任何資料的空白索引）。 在此範例中，您可以將其命名 `/oak:index/acme.product-custom-3`. 此名稱會取代索引 `/oak:index/acme.product-custom-2`. 晚於 `/oak:index/acme.product-custom-2` 由系統移除，空索引 `/oak:index/acme.product-custom-3` 然後可以移除。 這類空白索引的範例為：

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

如果不再需要自訂現成索引，則必須複製現成索引定義。 例如，如果您已經部署 `damAssetLucene-8-custom-3`，但不再需要自訂，並且要切換回預設值 `damAssetLucene-8` 索引，則必須新增索引 `damAssetLucene-8-custom-4` 包含下列專案的索引定義： `damAssetLucene-8`.

## 索引和查詢最佳化 {#index-query-optimizations}

Apache Jackrabbit Oak可讓彈性的索引設定有效處理搜尋查詢。 索引對於大型存放庫尤其重要。 請確定所有查詢都有適當的索引作為支援。 沒有適當索引的查詢可能會讀取數千個節點，然後將其記錄為警告。

另請參閱 [本檔案](query-and-indexing-best-practices.md) 有關如何最佳化查詢和索引的資訊。
