---
title: 內容搜尋與索引
description: 內容搜尋與索引
exl-id: 4fe5375c-1c84-44e7-9f78-1ac18fc6ea6b
source-git-commit: a2a57b2a35bdfba0466c46d5f79995ffee121cb7
workflow-type: tm+mt
source-wordcount: '2442'
ht-degree: 1%

---

# 內容搜尋與索引 {#indexing}

## as a Cloud ServiceAEM更改 {#changes-in-aem-as-a-cloud-service}

隨著AEMas a Cloud Service,Adobe正從以實例為中心的AEM模型移到基於服務的視圖(帶n-x AEM Containers)，該視圖由Cloud Manager中的CI/CD管道驅動。 在部署之前，必須指定索AEM引配置，而不是在單個實例上配置和維護索引。 生產中的配置更改明顯違反了CI/CD策略。 對於索引更改，情況也是如此，因為如果未指定測試和重新編製索引，在將其投入生產前，它可能會影響系統穩定性和效能。

以下是與6.5和早期版本相比AEM的主要更改清單：

1. 用戶將無權訪問單個實例的索引管AEM理器以再調試、配置或維護索引。 它僅用於本地開發和預部署。

1. 用戶不會更改單個實例上的索AEM引，也不必再擔心一致性檢查或重新索引。

1. 通常，在進入生產階段之前會先啟動索引更改，以避免繞過Cloud Manager CI/CD管道中的優質網關，並且不影響生產中的業務KPI。

1. 所有相關指標（包括生產中的搜索效能）將在運行時提供給客戶，以便提供有關搜索和索引主題的整體視圖。

1. 客戶將能夠根據其需要設定警報。

1. SRE正在全天候監測系統健康情況，並將根據需要及早採取行動。

1. 通過部署更改索引配置。 索引定義更改與其他內容更改一樣配置。

1. 在as a Cloud Service的高AEM級別上， [藍綠部署模型](#index-management-using-blue-green-deployments) 將存在兩組索引：一個設定為舊版本（藍色），另一個設定為新版本（綠色）。

1. 客戶可以在Cloud Manager生成頁上查看索引作業是否已完成，並將在新版本準備好接收通信時收到通知。

1. 限制:
* 目前，只支援AEM類型的索引對as a Cloud Service進行索引管理 `lucene`。
* 僅支援標準分析器（即隨產品一起發運的分析器）。 不支援自定義分析器。
* 在內部，可以配置其他索引並將其用於查詢。 例如，針對 `damAssetLucene` 在Skyline上，索引實際上可能針對此索引的Elasticsearch版本執行。 這種差異通常對應用程式和用戶不可見，但某些工具(如 `explain` 功能將報告其他索引。 有關Lucene索引和Elastic索引之間的差異，請參見 [Apache Jackrabbit Oak中的彈性文檔](https://jackrabbit.apache.org/oak/docs/query/elastic.html)。 客戶不需要也不能直接配置Elasticsearch索引。

## 使用方式 {#how-to-use}

定義索引可包括以下三種使用情形：

1. 添加新的客戶索引定義。
1. 正在更新現有索引定義。 這實際上意味著添加現有索引定義的新版本。
1. 刪除冗餘或過時的現有索引。

對於以上第1點和第2點，您需要在相應的Cloud Manager發佈計畫中建立新索引定義，作為自定義代碼庫的一部分。 有關詳細資訊，請參見 [部署到AEMas a Cloud Service文檔](/help/implementing/deploying/overview.md)。

## 索引名稱 {#index-names}

索引定義可以是：

1. 現成索引。 一個例子是 `/oak:index/cqPageLucene-2`。
1. 自定義現成索引。 此類自定義由客戶定義。 一個例子是 `/oak:index/cqPageLucene-2-custom-1`。
1. 完全自定義索引。 一個例子是 `/oak:index/acme.product-1-custom-2`。 為避免命名衝突，我們要求完全自定義索引具有前置詞，如 `acme.`

請注意，現成索引的自定義和完全自定義索引都需要包含 `-custom-`。 只有完全自定義索引必須以前置詞開頭。

## 準備新索引定義 {#preparing-the-new-index-definition}

>[!NOTE]
>
>如果自定義現成索引，例如 `damAssetLucene-6`，請從 *Cloud Service環境* 使用CRX DE包管理器的開發環境(`/crx/packmgr/`)。 然後將配置更名為 `damAssetLucene-6-custom-1`，並在頂部添加您的自定義項。 這可確保不會無意中刪除所需的配置。 例如， `tika` 節點 `/oak:index/damAssetLucene-6/tika` 在雲服務的自定義索引中需要。 雲SDK上不存在該選項。

您需要按照以下命名模式準備包含實際索引定義的新索引定義包：

`<indexName>[-<productVersion>]-custom-<customVersion>`

那就得倒下 `ui.apps/src/main/content/jcr_root`。 目前不支援子根資料夾。

需要設定包的篩選器，以便保留現有（現成索引）。 有兩種方法可以做到這一點：或者，篩選器設定為 `<filter root="/oak:index/" mode="merge"/>` 檔案 `ui.apps/src/main/content/META-INF/vault/filter.xml`，或每個自定義（或自定義）索引需要在篩選器部分中單獨列出，例如 `<filter root="/oak:index/damAssetLucene-6-custom-1"/>`。 如果是後一種情況，則每次更改版本時，都需要調整篩選器。

上面示例中的包生成為 `com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`。

>[!NOTE]
>
>包含索引定義的任何內容包都應在內容包的屬性檔案中設定以下屬性，該屬性位於 `/META-INF/vault/properties.xml`:
>
>`noIntermediateSaves=true`

## 部署索引定義 {#deploying-index-definitions}

>[!NOTE]
>
>Jackrabbit Filevault Maven包插件版本存在已知問題 **1.1.0** 不允許添加 `oak:index` 到模組 `<packageType>application</packageType>`。 您應該更新到該插件的最新版本。

索引定義現在標籤為自定義和版本化：

* 索引定義本身(例如 `/oak:index/ntBaseLucene-custom-1`)

因此，為了部署索引，索引定義(`/oak:index/definitionname`)需要通過 `ui.apps` 通過Git和Cloud Manager部署過程。

添加新索引定義後，需要通過雲管理器部署新應用程式。 在部署兩個作業後，將啟動兩個作業，負責將索引定義分別添加（並在需要時合併）到MongoDB和Azure段儲存，供作者和發佈。 在「藍綠」切換開始之前，正在使用新索引定義重新為基礎儲存庫編製索引。

>[!TIP]
>
>有關as a Cloud Service所需包結構的詳細信AEM息，請參閱文檔 [項AEM目結構。](/help/implementing/developing/introduction/aem-project-content-package-structure.md)

## 使用藍綠部署的索引管理 {#index-management-using-blue-green-deployments}

### 什麼是索引管理 {#what-is-index-management}

索引管理是關於添加、刪除和更改索引。 更改 *定義* 索引的索引速度很快，但應用更改（通常稱為「建立索引」，或對於現有索引，稱為「重新索引」）需要時間。 它不是瞬間的：必須掃描儲存庫以查找要索引的資料。

### 什麼是藍綠部署 {#what-is-blue-green-deployment}

藍綠部署可減少停機時間。 它還允許零停機升級，並提供快速回滾。 應用程式的舊版本（藍色）與應用程式的新版本（綠色）同時運行。

### 只讀和讀寫區域 {#read-only-and-read-write-areas}

儲存庫的某些區域（儲存庫的只讀部分）在舊（藍色）和新（綠色）應用程式版本中可能不同。 儲存庫的只讀區域通常為「 」`/app`&quot;和&quot;`/libs`。 在以下示例中，斜體用於標籤只讀區域，而粗體用於讀寫區域。

* **/**
* */apps（只讀）*
* **/content**
* */libs（只讀）*
* **/oak：索引**
* **/oak:index/acme。**
* **/jcr：系統**
* **/系統**
* **/var**

儲存庫的讀寫區域在應用程式的所有版本之間共用，而對於應用程式的每個版本，都有一組特定的 `/apps` 和 `/libs`。

### 無藍綠部署的索引管理 {#index-management-without-blue-green-deployment}

在開發期間或使用內部安裝時，可以在運行時添加、刪除或更改索引。 索引一旦可用即被使用。 如果舊版本的應用程式尚未使用索引，則通常會在計畫的停機時間內生成索引。 在刪除索引或更改現有索引時也會發生同樣的情況。 刪除索引時，一旦刪除索引，它就變為不可用。

### 採用藍綠部署的索引管理 {#index-management-with-blue-green-deployment}

藍綠部署時，不會停機。 在升級期間，應用程式的舊版本（例如，版本1）和新版本（版本2）在同一儲存庫上同時運行。 如果版本1要求某個索引可用，則不能在版本2中刪除此索引：以後應刪除索引，例如在版本3中，此時將保證應用程式版本1不再運行。 此外，應編寫應用程式，使版本1工作正常，即使版本2正在運行，並且版本2的索引可用。

升級到新版本後，舊索引可被系統垃圾回收。 舊索引可能仍會保留一段時間，以加快回滾（如果需要回滾）。

下表顯示了五個索引定義：索引 `cqPageLucene` 在兩個版本中使用，而索引 `damAssetLucene-custom-1` 僅在版本2中使用。

>[!NOTE]
>
>`<indexName>-custom-<customerVersionNumber>` 將AEM其標籤為現有索引的替換。

| 索引 | 現成索引 | 在版本1中使用 | 在版本2中使用 |
|---|---|---|---|
| /oak:index/damAssetLucene | 是 | 是 | 否 |
| /oak:index/damAssetLucene-custom-1 | 是（自定義） | 否 | 是 |
| /oak:index/acme.product-custom-1 | 否 | 是 | 否 |
| /oak:index/acme.product-custom-2 | 否 | 否 | 是 |
| /oak:index/cqPageLucene | 是 | 是 | 是 |

每次更改索引時版本號都會遞增。 為了避免自定義索引名與產品本身的索引名衝突，自定義索引以及對出廠設定索引的更改必須以 `-custom-<number>`。

### 對現成索引的更改 {#changes-to-out-of-the-box-indexes}

一旦Adobe更改了「damAssetLucene」或「cqPageLucene」等現成索引，此索引名為 `damAssetLucene-2` 或 `cqPageLucene-2` 建立，或者，如果已自定義索引，則自定義索引定義與出廠設定索引中的更改合併，如下所示。 更改的合併會自動進行。 這意味著，如果現成索引發生更改，則無需執行任何操作。 但是，以後可以再次自定義索引。

| 索引 | 現成索引 | 在版本2中使用 | 在版本3中使用 |
|---|---|---|---|
| /oak:index/damAssetLucene-custom-1 | 是（自定義） | 是 | 否 |
| /oak:index/damAssetLucene-2-custom-1 | 是（自動從damAssetLucene-custom-1和damAssetLucene-2合併） | 否 | 是 |
| /oak:index/cqPageLucene | 是 | 是 | 否 |
| /oak:index/cqPageLucene-2 | 是 | 否 | 是 |

### 當前限制 {#current-limitations}

當前僅支援類型索引的索引管理 `lucene`。 在內部，可以配置其他索引並將其用於查詢，例如彈性索引。

### 添加索引 {#adding-an-index}

添加名為的完全自定義索引 `/oak:index/acme.product-custom-1` 要在新版本的應用程式和更高版本中使用，必須按以下方式配置索引：

`acme.product-1-custom-1`

這通過在索引名稱前預先添加自定義標識符，後跟一個點(**`.`**)。 標識符的長度應介於2到5個字元之間。

如上所述，這確保索引僅由新版本的應用程式使用。

### 更改索引 {#changing-an-index}

更改現有索引時，需要添加新索引，並添加更改的索引定義。 例如，考慮現有索引 `/oak:index/acme.product-custom-1` 的子菜單。 舊索引儲存在 `/oak:index/acme.product-custom-1`，並且新索引儲存在 `/oak:index/acme.product-custom-2`。

應用程式的舊版本使用以下配置：

`/oak:index/acme.product-custom-1`

新版本的應用程式使用以下（已更改）配置：

`/oak:index/acme.product-custom-2`

>[!NOTE]
>
>as a Cloud Service上的索AEM引定義可能與本地開發實例上的索引定義不完全匹配。 開發實例沒有Tika配置，而AEMas a Cloud Service實例有。 如果使用Tika配置自定義索引，請保留Tika配置。

### 撤消更改 {#undoing-a-change}

有時，需要還原索引定義中的更改。 原因可能是，改變是錯誤的，或者不再需要改變。 例如，索引定義 `damAssetLucene-8-custom-3` 錯誤建立並已部署。 因此，您可能希望恢復到以前的索引定義 `damAssetLucene-8-custom-2`。 為此，需要添加一個名為 `damAssetLucene-8-custom-4` 包含上一個索引的定義， `damAssetLucene-8-custom-2`。

### 刪除索引 {#removing-an-index}

以下僅適用於自定義索引。 不能刪除產品索引，因為它們由使用AEM。

如果要在應用程式的較新版本中刪除索引，則可以使用新名稱定義空索引（一個從未使用且不包含任何資料的空索引）。 為此示例的目的，可以將其命名為 `/oak:index/acme.product-custom-3`。 這將替換索引 `/oak:index/acme.product-custom-2`。 一次 `/oak:index/acme.product-custom-2` 被系統刪除，空索引 `/oak:index/acme.product-custom-3` 也可以移除。 此類空索引的示例是：

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

如果不再需要自定義出廠設定索引，則必須複製出廠設定索引定義。 例如，如果您已部署 `damAssetLucene-8-custom-3`，但不再需要自定義，並希望切換回預設 `damAssetLucene-8` 索引，則必須添加索引 `damAssetLucene-8-custom-4` 包含的索引定義 `damAssetLucene-8`。

## 索引優化 {#index-optimizations}

Apache Jackrabbit Oak支援靈活的索引配置，以高效地處理搜索查詢。 索引對於較大的儲存庫尤為重要。 請確保所有查詢都有相應的索引作為備份。 沒有合適索引的查詢可以讀取數千個節點，然後記錄為警告。 應通過分析日誌檔案來標識此類查詢，以便可以優化索引定義。 請參閱 [此頁](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/practices/best-practices-for-queries-and-indexing.html?lang=en#tips-for-creating-efficient-indexes) 的子菜單。

### Lucene全文索引AEM在as a Cloud Service {#index-lucene}

全文索引 `/oak:index/lucene-2` 可能會變得非常大，因為預設情況下它為儲存庫中的所AEM有節點編製索引。  在Adobe計畫退出此索引後，它將不再在as a Cloud Service產品端使AEM用，並且不應要求運行客戶代碼。 對於AEM具有通用Lucene索引的as a Cloud Service環境，Adobe正在與客戶單獨協作，以找到一種協調的方法來補償此索引並使用更好的優化索引。 客戶無需在未另行通知的情況下採取任何行動。 在AEM此優化方面需要採取行動時，as a Cloud Service客戶將獲得Adobe通知。 如果自定義查詢需要此索引，作為臨時解決方案，應使用其他名稱建立此索引的副本，例如， `/oak:index/acme.lucene-1-custom-1`，如所述 [這裡](/help/operations/indexing.md)。
預設情況下，此優化不適用於其AEM他托管在本地或由Adobe Managed Services管理的環境。

## 查詢優化 {#index-query}

的 **查詢效能** 工具允許您觀察常用和慢速的JCR查詢。 此外，它還能夠分析查詢並顯示有關的各種資訊，最顯著的是，如果某個索引正用於此查詢或不使用該索引。

與本AEM地不AEM同，as a Cloud Service **查詢效能** 工具。 現在，它可通過Cloud Manager上的Developer Console（在Cloud Manager中） [查詢](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html#queries) 頁籤。
