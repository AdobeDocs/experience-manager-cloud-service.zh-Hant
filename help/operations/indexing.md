---
title: 內容搜尋與索引
description: 內容搜尋與索引
exl-id: 4fe5375c-1c84-44e7-9f78-1ac18fc6ea6b
translation-type: tm+mt
source-git-commit: 28c3fb4c5c0da175ee84463d7c100bdb1b93bb30
workflow-type: tm+mt
source-wordcount: '1738'
ht-degree: 2%

---

# 內容搜尋與索引 {#indexing}

## 變更AEM為Cloud Service{#changes-in-aem-as-a-cloud-service}

作為一AEM個Cloud Service,Adobe正在從以實例為中心的模型，轉向以Cloud Manager中的CI/CD管道為驅動的基於AEMn-x AEM Containers的服務視圖。 必須在部署之前指定索引配置，AEM而不是在單個實例上配置和維護索引。 生產中的配置更改明顯違反了CI/CD策略。 索引更改也是如此，因為如果未指定測試並重新編製索引，則可能會影響系統穩定性和效能，然後再將它們投入生產。

以下列出與6.5及舊版相AEM比的主要變更：

1. 用戶將無法再訪問單個實例的「索引管理器」AEM來調試、配置或維護索引。 它僅用於本機開發和預先部署。

1. 用戶不會更改單個實例上的索AEM引，也不必再擔心一致性檢查或重新編製索引。

1. 一般而言，索引變更是在開始生產之前先開始的，以避免規避Cloud Manager CI/CD管道中的品質閘道，而不會影響生產中的業務KPI。

1. 所有相關度量（包括生產中的搜尋效能）都會在執行時期提供給客戶，以便提供搜尋與索引主題的完整檢視。

1. 客戶將可以根據需要設定警報。

1. SRE正在全年無休地監測系統健康狀況，並將根據需要及早採取行動。

1. 索引配置會透過部署進行變更。 索引定義變更的設定方式與其他內容變更一樣。

1. 作為Cloud Service,AEM在高級別上，隨著[Blue-Green部署模型](#index-management-using-blue-green-deployments)的引入，將存在兩組索引：一組是舊版（藍色），另一組是新版（綠色）。

1. 客戶可以在Cloud Manager構建頁面上查看索引作業是否已完成，並在新版本準備好接收流量時收到通知。

1. 限制：目前，僅支AEM持對類型lucene的索引進行作為Cloud Service的索引管理。

## 使用方式 {#how-to-use}

定義索引可包括以下三種使用案例：

1. 添加新客戶索引定義
1. 更新現有索引定義。 這實際上意味著添加現有索引定義的新版本
1. 刪除冗餘或過時的現有索引。

對於上述第1點和第2點，您需要在各自的Cloud Manager發行排程中，建立新的索引定義，作為自訂程式碼庫的一部分。 如需詳細資訊，請參閱[部署AEM至Cloud Service檔案](/help/implementing/deploying/overview.md)。

### 準備新索引定義{#preparing-the-new-index-definition}

您需要準備一個新的索引定義包，該包包含實際的索引定義，請遵循以下命名模式：

`<indexName>[-<productVersion>]-custom-<customVersion>`

那麼就得在`ui.apps/src/main/content/jcr_root`下。 目前不支援子根資料夾。

上述示例中的軟體包構建為`com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`。

### 部署索引定義{#deploying-index-definitions}

>[!NOTE]
>
>Jackrabbit Filevault Maven Package Plugin版本&#x200B;**1.1.0**&#x200B;有已知問題，不允許您將`oak:index`新增至`<packageType>application</packageType>`的模組。 若要解決這個問題，請使用&#x200B;**1.0.4**&#x200B;版。

索引定義現在已標示為自訂和版本化：

* 索引定義本身（例如`/oak:index/ntBaseLucene-custom-1`）

因此，為了部署索引，索引定義(`/oak:index/definitionname`)需要通過Git和Cloud Manager部署過程通過`ui.apps`傳遞。

新增索引定義後，新應用程式需要透過Cloud Manager部署。 部署時，會啟動兩個工作，負責將索引定義新增（並視需要合併）至MongoDB和Azure區段商店，以供作者和發佈。 在Blue-Green交換機開始使用之前，正在使用新的索引定義重新建立基礎儲存庫的索引。

>[!TIP]
>
>有關作為Cloud Service所需的包AEM結構的詳細資訊，請參閱[AEM項目結構。](/help/implementing/developing/introduction/aem-project-content-package-structure.md)

## 使用藍綠部署的索引管理{#index-management-using-blue-green-deployments}

### 什麼是索引管理{#what-is-index-management}

索引管理是關於添加、刪除和更改索引。 更改索引的&#x200B;*定義*&#x200B;很快，但應用更改（通常稱為「建立索引」，對於現有索引，則稱為「重新索引」）需要時間。 這不是瞬間的：必須掃描儲存庫以查找要編製索引的資料。

### 什麼是藍綠部署{#what-is-blue-green-deployment}

藍綠部署可以減少停機時間。 它還允許零停機升級，並提供快速回滾。 舊版應用程式（藍色）與新版應用程式（綠色）同時執行。

### 只讀和讀寫區域{#read-only-and-read-write-areas}

儲存庫的某些區域（儲存庫的只讀部分）在舊版（藍色）和新版（綠色）應用程式中可能不同。 儲存庫的只讀區域通常為&quot;`/app`&quot;和&quot;`/libs`&quot;。 在以下示例中，斜體用於標籤只讀區域，而粗體用於讀寫區域。

* **/**
* */apps（唯讀）*
* **/content**
* */libs（唯讀）*
* **/oak:index**
* **/oak:index/acme。**
* **/jcr:system**
* **/system**
* **/var**

儲存庫的讀寫區域在應用程式的所有版本之間共用，而對於每個版本的應用程式，都有一組特定的`/apps`和`/libs`。

### 不使用藍綠部署的索引管理{#index-management-without-blue-green-deployment}

在開發期間或在內部部署安裝時，可以在執行時期新增、移除或變更索引。 索引一旦可用，就會立即使用。 如果舊版應用程式中尚未使用索引，則通常會在計畫停機期間生成索引。 在刪除索引或更改現有索引時也會發生同樣的情況。 刪除索引時，該索引在被刪除後即變為不可用。

### 使用藍綠部署的索引管理{#index-management-with-blue-green-deployment}

使用藍綠部署，不會停機。 但是，對於索引管理，這要求索引僅用於某些版本的應用程式。 例如，在應用程式第2版中新增索引時，您仍不希望該索引用於應用程式第1版。 如果刪除索引，則情況正好相反：第2版中移除的索引在第1版中仍然需要。 更改索引定義時，我們希望舊版索引僅用於版本1，新版索引僅用於版本2。

下表顯示了五個索引定義：索引`cqPageLucene`用於兩個版本，而索引`damAssetLucene-custom-1`僅用於版本2。

>[!NOTE]
>
>`<indexName>-custom-<customerVersionNumber>` 需要將AEM此標籤為現有索引的替換Cloud Service。

| 索引 | 現成可用的索引 | 用於第1版 | 用於第2版 |
|---|---|---|---|
| /oak:index/damAssetLucene | 是 | 是 | 否 |
| /oak:index/damAssetLucene-custom-1 | 是（自訂） | 否 | 是 |
| /oak:index/acme.product-custom-1 | 否 | 是 | 否 |
| /oak:index/acme.product-custom-2 | 否 | 否 | 是 |
| /oak:index/cqPageLucene | 是 | 是 | 是 |

每次變更索引時，版本號碼都會遞增。 為避免自訂索引名稱與產品本身的索引名稱發生衝突，自訂索引以及對開箱後索引的變更必須以`-custom-<number>`結尾。

### 對出廠索引{#changes-to-out-of-the-box-indexes}的更改

一旦Adobe變更現成可用的索引（例如&quot;damAssetLucene&quot;或&quot;cqPageLucene&quot;），就會建立名為`damAssetLucene-2`或`cqPageLucene-2`的新索引，或者，如果已自訂索引，則自訂的索引定義會與現成可用索引中的變更合併，如下所示。 合併變更會自動進行。 這表示，如果現成可用的索引發生變更，您不需要執行任何動作。 不過，以後可以再次自定義索引。

| 索引 | 現成可用的索引 | 用於第2版 | 用於第3版 |
|---|---|---|---|
| /oak:index/damAssetLucene-custom-1 | 是（自訂） | 是 | 否 |
| /oak:index/damAssetLucene-2-custom-1 | 是（自動從damAssetLucene-custom-1和damAssetLucene-2合併） | 否 | 是 |
| /oak:index/cqPageLucene | 是 | 是 | 否 |
| /oak:index/cqPageLucene-2 | 是 | 否 | 是 |

### 當前限制{#current-limitations}

目前僅支援類型`lucene`的索引的索引管理。

### 添加索引{#adding-an-index}

要添加名為`/oak:index/acme.product-custom-1`的索引以用於新版本的應用程式和更高版本，必須按如下方式配置索引：

`acme.product-1-custom-1`

這可借由將自訂識別碼預先加入索引名稱，後面接著點(**`.`**)來運作。 識別碼長度應介於2到5個字元之間。

如上所述，這可確保索引僅供新版本的應用程式使用。

### 更改索引{#changing-an-index}

更改現有索引時，需要使用更改的索引定義添加新索引。 例如，請考慮更改現有索引`/oak:index/acme.product-custom-1`。 舊索引儲存在`/oak:index/acme.product-custom-1`下，新索引儲存在`/oak:index/acme.product-custom-2`下。

舊版應用程式使用下列組態：

`/oak:index/acme.product-custom-1`

新版應用程式使用下列（已變更）組態：

`/oak:index/acme.product-custom-2`

>[!NOTE]
>
>作為Cloud ServiceAEM的索引定義可能與本地開發實例上的索引定義不完全匹配。 開發實例沒有Tika配置，而作為AEMCloud Service實例則有。 如果您使用Tika組態自訂索引，請保留Tika組態。

### 撤消更改{#undoing-a-change}

有時，需要回復索引定義中的更改。 原因可能是錯誤地做出了改變，或者不再需要改變。 例如，索引定義`damAssetLucene-8-custom-3`是錯誤建立的，已部署。 因此，您可能希望恢復到上一個索引定義`damAssetLucene-8-custom-2`。 為此，您需要添加一個名為`damAssetLucene-8-custom-4`的新索引，該索引包含前一個索引`damAssetLucene-8-custom-2`的定義。

### 刪除索引{#removing-an-index}

以下僅適用於自定義索引。 產品索引不能被刪除，因為它們由使用AEM。

如果要在應用程式的較新版本中刪除索引，則可以使用新名稱定義空索引（一個從未使用過且不包含任何資料的空索引）。 在本範例中，您可將其命名為`/oak:index/acme.product-custom-3`。 這將替換索引`/oak:index/acme.product-custom-2`。 系統刪除`/oak:index/acme.product-custom-2`後，也可以刪除空索引`/oak:index/acme.product-custom-3`。 此類空索引的示例為：

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

如果不再需要自訂現成可用的索引，則必須複製現成可用的索引定義。 例如，如果您已部署`damAssetLucene-8-custom-3`，但不再需要自定義，而想要切換回預設的`damAssetLucene-8`索引，則必須添加包含`damAssetLucene-8`索引定義的索引`damAssetLucene-8-custom-4`。

### 索引可用性和容錯{#index-availability-and-fault-tolerance}

建議為重要功能建立重複索引（請記住上述索引的命名慣例），因此，在發生索引損毀或任何此類未預見的事件時，都有備援索引可用來回應查詢。
