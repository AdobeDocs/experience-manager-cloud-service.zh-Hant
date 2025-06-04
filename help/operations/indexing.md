---
title: 內容搜尋與索引
description: 瞭解AEM as a Cloud Service中的內容搜尋和索引。
exl-id: 4fe5375c-1c84-44e7-9f78-1ac18fc6ea6b
feature: Operations
role: Admin
source-git-commit: 8d881caf5181e9c3cdc6dcb69f0deabc2d5eeed8
workflow-type: tm+mt
source-wordcount: '2918'
ht-degree: 1%

---

# 內容搜尋與索引 {#indexing}

## AEM as a Cloud Service中的變更 {#changes-in-aem-as-a-cloud-service}

透過AEM as a Cloud Service，Adobe正在從AEM執行個體為中心的模式移至具有n-x AEM容器的服務型檢視，由Cloud Manager中的CI/CD管道驅動。 您必須在部署之前指定索引設定，而不是在單一AEM執行個體上設定和維護索引。 生產環境中的設定變更違反CI/CD原則。 同樣的情況也適用於索引變更，因為如果未指定、測試並重新編制索引，在將索引投入生產之前，它可能會影響系統穩定性和效能。

以下是與AEM 6.5及舊版比較的主要變更清單：

1. 使用者無法再存取單一AEM執行個體的索引管理器，以除錯、設定或維護索引。 它僅用於本機開發和內部部署。
1. 使用者不會變更單一AEM例項上的索引，也不必再擔心一致性檢查或重新編制索引。
1. 一般而言，索引變更會在進入生產階段前開始，以免迴避Cloud Manager CI/CD管道中的品質閘道，及不影響生產階段的業務KPI。
1. 客戶可在執行階段使用所有相關量度（包括生產環境中的搜尋效能），提供搜尋和建立索引主題的整體檢視。
1. 客戶可以根據需求設定警報。
1. SRE全天候監控系統健康狀況，並儘早採取動作。
1. 索引設定已透過部署變更。 索引定義變更的設定方式與其他內容變更相同。
1. 在AEM as a Cloud Service的高階層，隨著推出[滾動部署模型](#index-management-using-rolling-deployments)，有兩組索引存在：一組用於舊版本，另一組用於新版本。
1. 客戶可以在Cloud Manager建置頁面上檢視索引工作是否完成，並會在新版本準備好接收流量時收到通知。

限制:

* 目前，僅型別`lucene`的索引支援AEM as a Cloud Service上的索引管理。 這表示所有索引自訂都必須是型別`lucene`。 `async`屬性只能是下列其中一項： `[async]`、`[async,nrt]`或`[fulltext-async]`。
* 在內部，可以設定其他索引並用於查詢。 例如，在AEM as a Cloud Service上，針對`damAssetLucene`索引編寫的查詢實際上可能會針對此索引的Elasticsearch版本執行。 使用者看不到此差異。 但是，某些工具（例如`explain`功能）會報告不同的索引。 如需Lucene索引與Elastic索引之間的差異，請參閱[Apache Jackrabbit Oak中的Elastic檔案](https://jackrabbit.apache.org/oak/docs/query/elastic.html)。 客戶不需要直接設定Elasticsearch索引，也無法直接設定。
* 僅支援標準分析器（即產品隨附的分析器）。 不支援自訂分析器。
* 不支援按類似特徵向量(`useInSimilarity = true`)搜尋。

>[!TIP]
>
>如需Oak索引和查詢的詳細資訊，包括進階搜尋和索引功能的詳細說明，請參閱[Apache Oak檔案](https://jackrabbit.apache.org/oak/docs/query/query.html)。


## 使用方式 {#how-to-use}

索引定義可以分為三個主要使用案例，如下所示：

1. **新增**&#x200B;新的自訂索引定義。
2. **新增新版本，以更新**&#x200B;現有的索引定義。
3. **移除**&#x200B;不再需要的索引定義。

針對上述第1點和第2點，您需要在個別的Cloud Manager發行排程中，建立索引定義，作為自訂程式碼庫的一部分。 如需詳細資訊，請參閱[部署至AEM as a Cloud Service](/help/implementing/deploying/overview.md)檔案。

## 索引名稱 {#index-names}

索引定義可以屬於以下類別之一：

1. 開箱即用(OOTB)索引。 這些是AEM提供的預先定義索引。 例如： `/oak:index/cqPageLucene-2`或`/oak:index/damAssetLucene-8`。

2. OOTB索引的自訂。 若要自訂OOTB索引，請附加`-custom-`及數字。 例如，`/oak:index/damAssetLucene-8-custom-1`是OOTB索引`/oak:index/damAssetLucene-8`的自訂。 自訂通常是OOTB索引的副本，加上需要編制索引的其他屬性。

3. 完全自訂索引：您可以從頭開始建立全新的索引。 這些索引還需要以`-custom-`和版本編號結尾。 此外，為了避免命名衝突，請在索引名稱中使用首碼。 例如： `/oak:index/acme.product-1-custom-2`，其中`acme.`是前置詞。

>[!NOTE]
>
>強烈建議不要在`dam:Asset`節點型別上引入新索引（尤其是全文檢索索引），因為這些索引可能會與OOTB產品功能衝突，導致功能和效能問題。 相反地，在`dam:Asset` nodetype上索引查詢的最適當方式是新增其他屬性，以自訂`damAssetLucene-*`索引。 這些變更將在後續發行中自動合併到新產品版本中。 如有疑問，請聯絡Adobe支援以尋求建議。

## 準備新的索引定義 {#preparing-the-new-index-definition}

>[!NOTE]
>
>自訂立即可用索引（例如`damAssetLucene-8`）時，請使用CRX DE封裝管理員(`/crx/packmgr/`)從&#x200B;*Cloud Service環境*&#x200B;複製最新的立即可用索引定義。 將其重新命名為`damAssetLucene-8-custom-1` （或更高版本），並在XML檔案中新增自訂內容。 如果雲端環境中的索引是型別`elasticsearch`，則需要其他變更：將`type`屬性變更為`lucene`，將`async`屬性變更為`[async,nrt]`，並將屬性`similarityTags`變更為`true`。 這可確保不會無意中移除所需的設定。 例如，部署至AEM Cloud Service環境的自訂索引中需要`/oak:index/damAssetLucene-8/tika`底下的`tika`節點，但本機AEM SDK上並不存在。

若要自訂OOTB索引，請準備包含自訂或自訂索引定義的新套件。 索引名稱必須遵循命名模式：

`<indexName>-<productVersion>-custom-<customVersion>`

對於完全自訂的索引，請準備新的索引定義套件，其中包含遵循此命名模式的索引定義：

`<prefix>.<indexName>-<productVersion>-custom-<customVersion>`

如限制區段中所述，即使使用封裝管理員擷取的索引定義是其他型別（例如`elasticsearch`），自訂索引定義的`type`必須一律設為`lucene`。
如果擷取的索引定義設為`elastic-async`，也必須變更`async`屬性。 對於自訂索引定義，`async`屬性必須設定為下列其中一個： `[async]`、`[async,nrt]`或`[fulltext-async]`。

<!-- Alexandru: temporarily drafting this statement due to CQDOC-17701

The package from the above sample is built as `com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`. -->

>[!NOTE]
>
>任何包含索引定義的內容封裝，都應在內容封裝的`properties.xml`檔案中設定下列屬性。 `properties.xml`預設是在新封裝中建立的，位於`<package_name>/META-INF/vault/properties.xml`：
>
> * `noIntermediateSaves=true`
>
> * `allowIndexDefinitions=true`

## 部署自訂索引定義 {#deploying-custom-index-definitions}

為了說明如何部署現成可用的索引`damAssetLucene-8`的自訂版本，我們將提供逐步指南。 在此範例中，我們將它重新命名為`damAssetLucene-8-custom-1`。 然後程式如下：

1. 在`ui.apps`目錄中建立具有更新索引名稱的新資料夾：
   * 範例：`ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-8-custom-1/`

2. 新增組態檔`.content.xml`，其自訂組態位於建立的資料夾內。 以下是自訂的範例：
檔案名稱： `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-8-custom-1/.content.xml`

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

3. 在`ui.apps/src/main/content/META-INF/vault/filter.xml`中新增專案至FileVault篩選器：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <workspaceFilter version="1.0">
       ...
       <filter root="/oak:index/damAssetLucene-8-custom-1"/> 
   </workspaceFilter>
   ```

4. 在`ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-8-custom-1/tika/config.xml`中新增Apache Tika的設定檔：

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

5. 請確定您的設定符合[專案設定](#project-configuration)區段中提供的准則。 相應地進行任何必要的調整。

## 專案設定

我們強烈建議使用Jackrabbit `filevault-package-maven-plugin`的>= `1.3.2`版。 將其整合至專案的步驟如下：

1. 更新最上層`pom.xml`中的版本：

   ```xml
   <plugin>
       <groupId>org.apache.jackrabbit</groupId>
           <artifactId>filevault-package-maven-plugin</artifactId>
           ...
           <version>1.3.2</version>
       ...
   </plugin>
   ```

2. 新增下列專案至最上層`pom.xml`：

   ```xml
   <jackrabbit-packagetype>
       <options>   
           <immutableRootNodeNames>apps,libs,oak:index</immutableRootNodeNames>
       </options>
   </jackrabbit-packagetype>
   ```

   以下是包含上述設定的專案最上層`pom.xml`檔案的範例：

   檔案名稱： `pom.xml`

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

3. 在`ui.apps/pom.xml`和`ui.apps.structure/pom.xml`中，必須在`filevault-package-maven-plugin`中啟用`allowIndexDefinitions`和`noIntermediateSaves`選項。 啟用`allowIndexDefinitions`可允許自訂索引定義，而`noIntermediateSaves`可確保自動新增設定。

   檔案名稱： `ui.apps/pom.xml`和`ui.apps.structure/pom.xml`

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

4. 在`ui.apps.structure/pom.xml`中新增`/oak:index`的篩選器：

   ```xml
   <filters>
       ...
       <filter><root>/oak:index</root></filter>
   </filters>
   ```

新增索引定義後，請使用Cloud Manager部署新的應用程式。 此部署會起始兩個工作，負責將索引定義分別新增（並在必要時合併）至MongoDB和Azure區段存放區以供製作和發佈。 在切換之前，基礎存放庫會使用更新的索引定義重新索引。

>[!TIP]
>
>如需AEM as a Cloud Service所需套件結構的詳細資訊，請參閱[AEM專案結構](/help/implementing/developing/introduction/aem-project-content-package-structure.md)。

## 使用滾動式部署的索引管理 {#index-management-using-rolling-deployments}

### 索引管理是什麼 {#what-is-index-management}

索引管理是關於新增、移除和變更索引。 變更索引的&#x200B;*定義*&#x200B;很快速，但套用變更（通常稱為「建立索引」，或針對現有索引稱為「重新索引」）需要時間。 此動作並非即時：必須掃描存放庫才能為資料編制索引。

### 哪些是滾動式部署 {#what-are-rolling-deployments}

滾動式部署可實現零停機升級，並提供快速回覆。 應用程式的舊版本與應用程式的新版本同時執行。

### 唯讀和讀寫區域 {#read-only-and-read-write-areas}

存放庫的特定區域（存放庫的唯讀部分）在舊版本和新版本的應用程式中可能不同。 存放庫的唯讀區域通常是`/app`和`/libs`。 在下列範例中，斜體是用來標籤唯讀區域，而粗體則是用來標籤讀寫區域。

* **/**
* */應用程式（唯讀）*
* **/content**
* */libs （唯讀）*
* **/oak：index**
* **/oak：index/acme.**
* **/jcr：system**
* **/系統**
* **/var**

存放庫的讀寫區域會在所有版本的應用程式之間共用，而每個版本的應用程式都有特定的`/apps`和`/libs`集。

### 索引管理，不進行滾動部署 {#index-management-without-rolling-deployments}

在開發期間或使用內部部署安裝時，可在執行階段新增、移除或變更索引。 當索引可用時，即會加以使用。 如果舊版應用程式尚未使用索引，則通常會在排程的停機期間建立索引。 移除索引或變更現有索引時，也會發生相同的情況。 移除索引時，該索引在移除後會變成無法使用。

### 使用滾動式部署的索引管理 {#index-management-with-rolling-deployments}

滾動式部署沒有停機時間。 在更新期間，應用程式的舊版本（例如版本1）和新版本（版本2）會針對相同的存放庫同時執行。 如果版本1要求某個索引可用，則不得在版本2中移除此索引。 稍後應移除索引，例如，在版本3中，此時可保證應用程式的版本1不再執行。 此外，應用程式的編寫應使版本1運作良好，即使版本2正在執行以及有版本2的索引可用。

升級到新版本後，系統可以對舊索引進行垃圾回收。 舊索引通常會保留一週，以加速倒回（如果需要倒回）。

下表顯示五個索引定義：在兩個版本中都使用索引`cqPageLucene`，而僅在版本2中使用索引`damAssetLucene-custom-1`。

>[!NOTE]
>
>AEM as a Cloud Service需要`<indexName>-custom-<customerVersionNumber>`才能將其標示為現有索引的取代。

| 索引 | 現成索引 | 用於版本1 | 用於版本2 |
|---|---|---|---|
| /oak：index/damAssetLucene-8 | 是 | 是 | 否 |
| /oak：index/damAssetLucene-8-custom-1 | 是（自訂） | 否 | 是 |
| /oak：index/acme.product-1-custom-1 | 否 | 是 | 否 |
| /oak：index/acme.product-1-custom-2 | 否 | 否 | 是 |
| /oak：index/cqPageLucene-2 | 是 | 是 | 是 |

每次變更索引時，版本號碼都會增加。 若要避免自訂索引名稱與產品本身的索引名稱衝突，自訂索引以及對現成索引的變更必須以`-custom-<number>`結尾。

### 現成可用索引的變更 {#changes-to-out-of-the-box-indexes}

在Adobe變更現成可用的索引（例如`damAssetLucene`或`cqPageLucene`）後，會建立名為`damAssetLucene-2`或`cqPageLucene-2`的新索引。 或者，如果已經自訂索引，自訂的索引定義會與現成索引中的變更合併，如下所示。 合併變更會自動進行。 這表示如果現成索引變更，您不需要執行任何動作。 不過，之後可以再次自訂索引。 在此情況下，請務必使用最新（合併的）版本作為基準。

| 索引 | 現成索引 | 用於版本2 | 用於版本3 |
|---|---|---|---|
| /oak：index/damAssetLucene-1-custom-1 | 是（自訂） | 是 | 否 |
| /oak：index/damAssetLucene-2-custom-1 | 是（自動從damAssetLucene-1-custom-1和damAssetLucene-2合併） | 否 | 是 |
| /oak：index/cqPageLucene-1 | 是 | 是 | 否 |
| /oak：index/cqPageLucene-2 | 是 | 否 | 是 |

請務必注意，環境可能使用不同的AEM版本。 例如： `dev`環境在發行版本`X+1`上，而階段和生產仍在發行版本`X`上，且在`dev`上執行必要的測試後，正在等待升級至發行版本`X+1`。 如果版本`X+1`隨附已自訂的較新版本產品索引，且需要對該索引進行新的自訂，則下表將說明根據AEM版本需要設定哪些版本：

| 環境(AEM發行版本) | 產品索引版本 | 現有的自訂索引版本 | 新的自訂索引版本 |
|-----------------------------------|-----------------------|-------------------------------|----------------------------|
| 開發(X+1) | damAssetLucene-11 | damAssetLucene-11-custom-1 | damAssetLucene-11-custom-2 |
| 階段(X) | damAssetLucene-10 | damAssetLucene-10-custom-1 | damAssetLucene-10-custom-2 |
| Prod (X) | damAssetLucene-10 | damAssetLucene-10-custom-1 | damAssetLucene-10-custom-2 |


### 目前限制 {#current-limitations}

僅型別`lucene`的索引支援索引管理，並將`compatVersion`設定為`2`。 在內部，可以設定其他索引並用於查詢，例如Elasticsearch索引。 在AEM as a Cloud Service上，針對`damAssetLucene`索引編寫的查詢實際上可能會針對此索引的Elasticsearch版本執行。 應用程式使用者不會看見這個差異，但某些工具（例如`explain`功能）會報告不同的索引。 如需Lucene與Elasticsearch索引之間的差異，請參閱[Apache Jackrabbit Oak中的Elasticsearch檔案](https://jackrabbit.apache.org/oak/docs/query/elastic.html)。 客戶不能也不需要直接設定Elasticsearch索引。

僅支援內建分析器（即產品隨附的分析器）。 不支援自訂分析器。

目前不支援為`/oak:index`的內容編制索引。

為獲得最佳作業效能，索引不應過大。 所有索引的總計大小均可作為參考使用。 如果在新增自訂索引後，此大小增加超過100%，並且在開發環境中調整了標準索引，則應調整自訂索引定義。 AEM as a Cloud Service可防止部署或移除會對系統穩定性和效能產生負面影響的索引。

### 新增索引 {#adding-an-index}

若要新增名為`/oak:index/acme.product-1-custom-1`的完整自訂索引，以用於應用程式的新版本和更新版本，必須依照以下方式設定索引：

`acme.product-1-custom-1`

此設定的運作方式是在索引名稱前面加上自訂識別碼，後面接著點(**`.`**)。 識別碼的長度應該介於2到5個字元之間。

如上所述，此設定可確保只有新版本的應用程式才會使用索引。

### 變更索引 {#changing-an-index}

變更現有索引時，必須新增已變更索引定義的新索引。 例如，假設現有索引`/oak:index/acme.product-1-custom-1`已變更。 舊索引儲存在`/oak:index/acme.product-1-custom-1`下，而新索引儲存在`/oak:index/acme.product-1-custom-2`下。

應用程式的舊版本會使用以下設定：

`/oak:index/acme.product-1-custom-1`

應用程式的新版本會使用下列（已變更）組態：

`/oak:index/acme.product-1-custom-2`

>[!NOTE]
>
>AEM as a Cloud Service上的索引定義可能與本機開發執行個體上的索引定義不完全相符。 開發執行個體沒有Tika設定，而AEM as a Cloud Service執行個體有。 如果您使用Tika設定自訂索引，請保留Tika設定。

### 復原變更 {#undoing-a-change}

有時候，必須復原索引定義中的修改，例如由於錯誤或不再需要該修改。 例如，如果索引定義`damAssetLucene-8-custom-3`包含錯誤，您可能想要回復到先前的定義`damAssetLucene-8-custom-2`。 若要完成此作業，請建立名稱為`damAssetLucene-8-custom-4`的新索引，此索引為先前索引`damAssetLucene-8-custom-2.`的復本

### 移除索引 {#removing-an-index}

以下內容僅適用於現成可用的(OOTB)索引以及完全自訂的索引的自訂。 請注意，原始OOTB索引無法移除，因為AEM正在使用它們。

為確保系統完整性和穩定性，部署後應將索引定義視為不可變。 如果您需要移除自訂索引或自訂，請建立該索引的新版本，其定義會有效模擬移除
（請參閱下列範例）。

一旦部署新版本的索引後，查詢將不再使用舊版本的相同索引。
較舊的版本不會立即從環境中刪除，
但會透過定期執行的清理機制符合記憶體回收的資格。
經過寬限期後，在發生錯誤時進行復原
（目前是從索引移除時算起的7天，但可能會有所變更），
此清理機制會刪除未使用的索引資料，
和會停用或從環境中移除舊版本的索引。

以下說明兩種可能的情況：移除OOTB索引的自訂專案，以及移除完全自訂的索引。

#### 移除現成索引的自訂專案

請依照[使用OOTB索引的定義作為新版本來復原變更](#undoing-a-change-undoing-a-change)中說明的步驟操作。 例如，如果您已經部署`damAssetLucene-8-custom-3`，但不再需要自訂，並且要切換回預設的`damAssetLucene-8`索引，則需要新增包含`damAssetLucene-8`的索引定義的索引`damAssetLucene-8-custom-4`。

#### 移除完全自訂索引

請依照[使用虛擬索引作為新版本來復原變更](#undoing-a-change-undoing-a-change)中說明的步驟操作。 虛擬索引從未用於查詢，且不包含任何資料，因此其效果與索引不存在時相同。 在此範例中，您可以將其命名為`/oak:index/acme.product-1-custom-3`。 此名稱會取代索引`/oak:index/acme.product-1-custom-2`。 這種虛擬索引的範例是：

```xml
<acme.product-1-custom-3
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
</acme.product-1-custom-3>
```

## 索引和查詢最佳化 {#index-query-optimizations}

Apache Jackrabbit Oak可讓彈性的索引設定有效地處理搜尋查詢。 索引對於大型存放庫尤其重要。 請確定所有查詢都有適當的索引作為支援。 沒有適當索引的查詢可能會讀取數千個節點，然後將其記錄為警告。

請參閱[此檔案](query-and-indexing-best-practices.md)，瞭解如何最佳化查詢和索引。
