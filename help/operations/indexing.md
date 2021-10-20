---
title: 內容搜尋與索引
description: 內容搜尋與索引
exl-id: 4fe5375c-1c84-44e7-9f78-1ac18fc6ea6b
source-git-commit: 8eafe30b69014f5affad6da7e80f8f9a1c42eb38
workflow-type: tm+mt
source-wordcount: '2164'
ht-degree: 1%

---

# 內容搜尋與索引 {#indexing}

## AEMas a Cloud Service中的變更 {#changes-in-aem-as-a-cloud-service}

透過AEMas a Cloud Service,Adobe正從AEM執行個體導向的模型，移至以服務為基礎的檢視，其中n-x AEM容器由Cloud Manager中的CI/CD管道驅動。 必須在部署之前指定索引配置，而不是在單個AEM實例上配置和維護索引。 生產環境中的組態變更明顯違反CI/CD原則。 索引更改也同樣適用，因為如果未指定測試和重新索引，在將其投入生產之前，它可能會影響系統穩定性和效能。

以下是與AEM 6.5及舊版相比的主要變更清單：

1. 用戶將無法訪問單個AEM實例的Index Manager以調試、配置或維護索引。 它僅用於本機開發和內部部署。

1. 使用者不會變更單一AEM例項上的索引，也不必再擔心一致性檢查或重新索引。

1. 一般而言，在開始生產前會先啟動索引變更，以避免在Cloud Manager CI/CD管道中規避品質閘道，而不會影響生產中的業務KPI。

1. 所有相關量度（包括生產環境中的搜尋效能）將在執行階段供客戶使用，以提供搜尋和索引主題的整體檢視。

1. 客戶將能根據其需求設定警報。

1. SRE正在監測系統健康24/7，並將根據需要和盡早採取行動。

1. 索引配置已通過部署更改。 索引定義變更的設定方式與其他內容變更相同。

1. 在AEMas a Cloud Service的高層級，導入 [藍綠色部署模型](#index-management-using-blue-green-deployments) 將存在兩組索引：一個為舊版（藍色）設定，另一個為新版（綠色）設定。

1. 客戶可以在Cloud Manager建置頁面上查看索引工作是否已完成，並會在新版本準備好接收流量時收到通知。

1. 限制:
* 目前，AEMas a Cloud Service上的索引管理僅支援lucene類型的索引。
* 僅支援標準分析器（即隨產品提供的分析器）。 不支援自訂分析器。

## 使用方式 {#how-to-use}

定義索引可包括以下三種使用案例：

1. 新增客戶索引定義
1. 更新現有索引定義。 這實際上意味著添加新版本的現有索引定義
1. 刪除冗餘或過時的現有索引。

對於以上第1點和第2點，您需要在各自Cloud Manager發行排程的自訂程式碼基底中建立新的索引定義。 如需詳細資訊，請參閱 [部署至AEMas a Cloud Service檔案](/help/implementing/deploying/overview.md).

### 準備新索引定義 {#preparing-the-new-index-definition}

>[!NOTE]
>
>例如，如果自訂現成可用的索引 `damAssetLucene-6`，請從 *Cloud Service環境* 並在上方新增您的自訂項目，以確保不會不慎移除所需的設定。 例如， `tika` 節點 `/oak:index/damAssetLucene-6/tika` 是必要節點，也應是自訂索引的一部分，且Cloud SDK上不存在。

您需要按照以下命名模式準備包含實際索引定義的新索引定義包：

`<indexName>[-<productVersion>]-custom-<customVersion>`

那麼就得下去 `ui.apps/src/main/content/jcr_root`. 目前不支援子根資料夾。

上述範例中的套件會建置為 `com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`.

>[!NOTE]
>
>任何包含索引定義的內容包都應在內容包的屬性檔案中設定以下屬性，該檔案位於 `/META-INF/vault/properties.xml`:
>
>`noIntermediateSaves=true`

### 部署索引定義 {#deploying-index-definitions}

>[!NOTE]
>
>Jackrabbit Filevault Maven套件外掛程式版本有已知問題 **1.1.0** 不允許您新增 `oak:index` 至模組 `<packageType>application</packageType>`. 您應更新至該外掛程式的最新版本。

索引定義現在已標示為自訂和版本控制：

* 索引定義本身(例如 `/oak:index/ntBaseLucene-custom-1`)

因此，為了部署索引，索引定義(`/oak:index/definitionname`)需要透過 `ui.apps` 透過Git和Cloud Manager部署程式。

新增新索引定義後，需透過Cloud Manager部署新應用程式。 部署後，將啟動兩個作業，負責將索引定義分別新增（並視需要合併）至MongoDB和Azure區段存放區，以供製作和發佈。 在藍綠色切換開始之前，正在使用新索引定義重新索引基礎儲存庫。

>[!TIP]
>
>如需AEMas a Cloud Service所需套件結構的詳細資訊，請參閱本檔案 [AEM專案結構。](/help/implementing/developing/introduction/aem-project-content-package-structure.md)

## 使用藍綠色部署進行索引管理 {#index-management-using-blue-green-deployments}

### 什麼是索引管理 {#what-is-index-management}

索引管理是關於添加、刪除和更改索引。 變更 *定義* 索引的索引是快速的，但應用更改（通常稱為「建立索引」，或對於現有索引，則稱為「重新索引」）需要時間。 它不是瞬間的：必須掃描儲存庫，才能為資料建立索引。

### 什麼是藍綠色部署 {#what-is-blue-green-deployment}

藍綠色部署可減少停機時間。 它還允許零停機升級，並提供快速回滾。 應用程式的舊版本（藍色）與新版本的應用程式（綠色）同時運行。

### 只讀和讀寫區域 {#read-only-and-read-write-areas}

儲存庫的某些區域（儲存庫的只讀部分）在應用程式的舊（藍色）和新（綠色）版本中可能不同。 存放庫的唯讀區域通常為「`/app`&quot;和&quot;`/libs`」。 在以下範例中，斜體用於標籤唯讀區域，而粗體用於讀寫區域。

* **/**
* */apps（只讀）*
* **/content**
* */libs（唯讀）*
* **/oak:index**
* **/oak:index/acme。**
* **/jcr:system**
* **/system**
* **/var**

儲存庫的讀寫區域在所有版本的應用程式之間共用，而對於每個版本的應用程式，都有一組特定的 `/apps` 和 `/libs`.

### 無藍綠色部署的索引管理 {#index-management-without-blue-green-deployment}

在開發期間或使用內部部署安裝時，可以在執行階段新增、移除或變更索引。 索引一旦可用即可使用。 如果舊版應用程式中尚未使用索引，則通常會在計畫停機期間建立索引。 刪除索引或更改現有索引時也會發生相同情況。 刪除索引時，該索引一旦刪除即不可用。

### 使用藍綠色部署進行索引管理 {#index-management-with-blue-green-deployment}

使用藍綠色的部署，不會發生停機。 但是，對於索引管理，這要求索引僅供某些版本的應用程式使用。 例如，在應用程式的第2版中新增索引時，您不希望該索引供應用程式的第1版使用。 移除索引時的情況則相反：第1版仍需要第2版中移除的索引。 更改索引定義時，我們希望舊版索引只用於版本1，新版索引只用於版本2。

下表顯示了五種索引定義：索引 `cqPageLucene` 當索引時，在兩個版本中都使用 `damAssetLucene-custom-1` 僅用於版本2。

>[!NOTE]
>
>`<indexName>-custom-<customerVersionNumber>` 需要AEM as a Cloud Service，才能將此標籤為現有索引的替代項目。

| 索引 | 現成可用的索引 | 用於第1版 | 用於第2版 |
|---|---|---|---|
| /oak:index/damAssetLucene | 是 | 是 | 否 |
| /oak:index/damAssetLucene-custom-1 | 是（自訂） | 否 | 是 |
| /oak:index/acme.product-custom-1 | 否 | 是 | 否 |
| /oak:index/acme.product-custom-2 | 否 | 否 | 是 |
| /oak:index/cqPageLucene | 是 | 是 | 是 |

每次變更索引時，版本號碼都會增加。 為避免自訂索引名稱與產品本身的索引名稱發生衝突，自訂索引以及對現成可用索引的變更必須以 `-custom-<number>`.

### 對現成可用索引的變更 {#changes-to-out-of-the-box-indexes}

一旦Adobe變更現成可用的索引（例如「damAssetLucene」或「cqPageLucene」）後，即會出現新的索引，名為 `damAssetLucene-2` 或 `cqPageLucene-2` 已建立，或者，如果已自定義索引，則自定義索引定義將與現成索引中的更改合併，如下所示。 變更合併會自動進行。 這表示如果現成可用的索引變更，您不需要執行任何動作。 但是，以後可以再次自定義索引。

| 索引 | 現成可用的索引 | 用於第2版 | 用於第3版 |
|---|---|---|---|
| /oak:index/damAssetLucene-custom-1 | 是（自訂） | 是 | 否 |
| /oak:index/damAssetLucene-2-custom-1 | 是（自動從damAssetLucene-custom-1和damAssetLucene-2合併） | 否 | 是 |
| /oak:index/cqPageLucene | 是 | 是 | 否 |
| /oak:index/cqPageLucene-2 | 是 | 否 | 是 |

### 目前限制 {#current-limitations}

當前僅支援類型的索引的索引管理 `lucene`.

### 添加索引 {#adding-an-index}

要添加名為 `/oak:index/acme.product-custom-1` 要在新版本的應用程式和更新版本中使用，必須按以下方式配置索引：

`acme.product-1-custom-1`

其原理是將自訂識別碼預先標示為索引名稱，後面接著點(**`.`**)。 識別碼長度應介於2到5個字元之間。

如上所述，這可確保索引僅供新版本的應用程式使用。

### 更改索引 {#changing-an-index}

更改現有索引時，需要添加新索引，並更改索引定義。 例如，請考慮現有索引 `/oak:index/acme.product-custom-1` 已變更。 舊索引儲存在 `/oak:index/acme.product-custom-1`，而新索引儲存在 `/oak:index/acme.product-custom-2`.

舊版應用程式使用下列設定：

`/oak:index/acme.product-custom-1`

新版本的應用程式使用下列（已變更）設定：

`/oak:index/acme.product-custom-2`

>[!NOTE]
>
>AEMas a Cloud Service上的索引定義可能不完全符合本機開發例項上的索引定義。 開發執行個體沒有Tika設定，AEMas a Cloud Service執行個體則有。 如果您使用Tika配置自定義索引，請保留Tika配置。

### 撤消更改 {#undoing-a-change}

有時，需要還原索引定義中的變更。 原因可能是錯誤地做出了改變，或者不再需要改變。 例如，索引定義 `damAssetLucene-8-custom-3` 已錯誤建立且已部署。 因此，您可能希望恢復到以前的索引定義 `damAssetLucene-8-custom-2`. 要執行此操作，您需要新增名為 `damAssetLucene-8-custom-4` 包含前一個索引的定義， `damAssetLucene-8-custom-2`.

### 刪除索引 {#removing-an-index}

以下內容僅適用於自訂索引。 產品索引不能被刪除，因為AEM使用。

如果要在以後版本的應用程式中刪除索引，可以定義一個空索引（一個從未使用過的空索引，並且不包含任何資料），並帶有新名稱。 針對此範例，您可將其命名為 `/oak:index/acme.product-custom-3`. 這會取代索引 `/oak:index/acme.product-custom-2`. 一次 `/oak:index/acme.product-custom-2` 被系統刪除，則空索引 `/oak:index/acme.product-custom-3` 也可以移除。 此類空索引的示例如下：

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

如果不再需要自訂現成可用的索引，則必須複製現成可用的索引定義。 例如，如果您已部署 `damAssetLucene-8-custom-3`，但不再需要自訂，而且想要切換回預設值 `damAssetLucene-8` 索引，則必須添加索引 `damAssetLucene-8-custom-4` 包含 `damAssetLucene-8`.

## 索引最佳化 {#index-optimizations}

Apache Jackrabbit Oak可啟用彈性的索引設定，以有效處理搜尋查詢。 索引對於較大的儲存庫尤其重要。 請確保所有查詢都由適當的索引備份。 沒有適當索引的查詢可讀取數千個節點，然後記錄為警告。 應通過分析日誌檔案來識別此類查詢，以便可以優化索引定義。 請參閱 [本頁](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/practices/best-practices-for-queries-and-indexing.html?lang=en#tips-for-creating-efficient-indexes) 以取得更多資訊。

### AEM上的Lucene全文索引as a Cloud Service {#index-lucene}

全文索引 `/oak:index/lucene-2` 可能會變得非常大，因為預設情況下，它會為AEM儲存庫中的所有節點建立索引。  自2021年9月起，Adobe計畫淘汰此索引後，將不再部署於AEMas a Cloud Service。 因此，AEM as a Cloud Service中不再用於產品端，也不需要執行客戶程式碼。 對於具有通用Lucene索引的AEMas a Cloud Service環境，Adobe正在與客戶個別合作，以採用協調的方法來補償此索引，並使用更好、最佳化的索引。 客戶無需採取任何動作，但須另行通知Adobe。 AEMas a Cloud Service客戶在需要針對此最佳化採取動作時，會收到Adobe通知。 如果自訂查詢需要此索引，作為暫時解決方案，應使用不同名稱建立此索引的副本，例如 `/oak:index/acme.lucene-1-custom-1`，如所述 [此處](/help/operations/indexing.md).
依預設，此最佳化不適用於在內部部署或由Adobe Managed Services管理的其他AEM環境。

## 查詢最佳化 {#index-query}

此 **查詢效能** 工具可讓您同時觀察熱門和緩慢的JCR查詢。 此外，它還能夠分析查詢並顯示有關的各種資訊，尤其是當是否正使用此查詢使用索引時。

不同於AEM內部部署，AEMas a Cloud Service不會顯示 **查詢效能** 工具。 現在可透過以下位置的開發人員控制台取得： [查詢](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html#queries) 標籤。
