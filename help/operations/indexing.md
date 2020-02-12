---
title: 內容搜尋與索引
description: '內容搜尋與索引 '
translation-type: tm+mt
source-git-commit: 99dce041a6d7554785fd43eb82c671643e903f23

---


# 內容搜尋與索引 {#indexing}

## AEM As a Cloud Service的變更 {#changes-in-aem-as-a-cloud-service}

以AEM為雲端服務，Adobe將從AEM實例導向服務型檢視，並在Cloud manager的CI/CD管道驅動下，從AEM實例導向檢視。 必須在部署前先指定「索引」設定，而非在單一AEM例項上設定和維護「索引」。 生產中的配置更改明顯違反了CI/CD策略。 索引更改也是如此，因為如果未指定測試並重新編製索引，則可能會影響系統穩定性和效能，然後再將它們投入生產。

以下是與AEM 6.5及舊版比較的主要變更清單：

1. 使用者將無法再存取單一AEM例項的「索引管理員」來除錯、設定或維護索引。 它僅用於本機開發和預先部署。

1. 使用者不會在單一AEM例項上變更「索引」，也不必再擔心一致性檢查或重新建立索引。

1. 一般而言，索引變更是在開始生產之前先開始的，以避免規避Cloud Manager CI/CD管道中的品質閘道，而不會影響生產中的業務KPI。

1. 所有相關度量（包括生產中的搜尋效能）都會在執行時期提供給客戶，以便提供搜尋與索引主題的完整檢視。

1. 客戶將可以根據需要設定警報。

1. SRE正在全年無休地監測系統健康狀況，並將根據需要及早採取行動。

1. 索引配置會透過部署進行變更。 索引定義變更的設定方式與其他內容變更一樣。

1. 在AEM雲端服務的高階層，隨著 [Blue-Green部署模型的推出](#index-management-using-blue-green-deployments) ，將會有兩組索引：一組是舊版（藍色），另一組是新版（綠色）。

使用的索引版本是使用索引定義中的標誌通過標誌配置的 `useIfExist` 。 索引只能用於應用程式的一個版本（例如，僅藍色或綠色），或同時用於兩個版本。 使用藍綠部署的索 [引管理提供詳細的檔案](#index-management-using-blue-green-deployments)。

1. 客戶可以在Cloud manager構建頁面上查看索引作業是否已完成，並在新版本準備好接收流量時收到通知。

1. 限制：目前，AEM雲端服務的索引管理僅支援lucene類型的索引。

<!-- ## Sizing Considerations {#sizing-considerations}

AEM as a Cloud Service comes with a default capacity model to provide sufficient performance for average web applications. This "average" measure relates to the repository size and even more relevant to the indexing size. If we have reasons to believe that we need extended capacity for a specific customer project, an evaluation with SREs and Engineering will take place to determine the required capacity settings. 

AS NOTE: the above is internal for now.

-->

## 如何使用 {#how-to-use}

定義索引可包括3個使用案例：

1. 添加新客戶索引定義
1. 更新現有索引定義。 這實際上意味著添加現有索引定義的新版本
1. 刪除冗餘或過時的現有索引。

對於上述第1點和第2點，您需要在各自的Cloud manager發行排程中，建立新的索引定義，作為自訂程式碼庫的一部分。 如需詳細資訊，請參 [閱「部署至AEM as a Cloud Service」檔案](/help/implementing/deploying/overview.md)。

### 準備新索引定義 {#preparing-the-new-index-definition}

您需要準備一個新的索引定義包，該包包含實際的索引定義，請遵循以下命名模式：

`<indexName>[-<productVersion>]-custom-<customVersion>`

那就得下去 `ui.content/src/main/content/jcr_root`。 目前不支援子根資料夾。

<!-- need to review and link info on naming convention from https://wiki.corp.adobe.com/display/WEM/Merging+Customer+and+OOTB+Index+Changes?focusedCommentId=1784917629#comment-1784917629 -->

上述範例中的套件會建立為 `com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`。

### 部署索引定義 {#deploying-index-definitions}

索引定義現在已標示為自訂和版本化：

* 索引定義本身(例如 `/oak:index/ntBaseLucene-custom-1`)是MUTABLE內容

因此，為了部署索引，索引定義(`/oak:index/definitionname`)應透過可變套件 **傳遞**，通常 `ui.content` 是透過Git和Cloud manager部署程式。

新增索引定義後，新應用程式需要透過Cloud manager部署。 部署時，會啟動兩個工作，負責將索引定義新增（並視需要合併）至MongoDB和Azure區段商店，以供作者和發佈。 在Blue-Green交換機開始使用之前，正在使用新的索引定義重新建立基礎儲存庫的索引。

## 使用藍綠部署的索引管理 {#index-management-using-blue-green-deployments}

### 什麼是索引管理 {#what-is-index-management}

索引管理是關於添加、刪除和更改索引。 更改索 *引的定義* 很快，但應用更改（通常稱為「建立索引」，或對於現有索引，「重新索引」）需要時間。 這不是瞬間的：必須掃描儲存庫以查找要編製索引的資料。

### 什麼是藍綠部署 {#what-is-blue-green-deployment}

藍綠部署可以減少停機時間。 它還允許零停機升級，並提供快速回滾。 舊版應用程式（藍色）與新版應用程式（綠色）同時執行。

### 只讀和讀寫區 {#read-only-and-read-write-areas}

儲存庫的某些區域（儲存庫的只讀部分）在舊版（藍色）和新版（綠色）應用程式中可能不同。 儲存庫的唯讀區域通常為「`/app`」和「`/libs`」。 在以下示例中，斜體用於標籤只讀區域，而粗體用於讀寫區域。

* **/**
* */apps（唯讀）*
* **/content**
* */libs（唯讀）*
* **/oak:index**
* **/oak:index/acme**
* **/jcr:system**
* **/system**
* **/var**

儲存庫的讀寫區域在應用程式的所有版本之間共用，而對於應用程式的每個版本，都有一組特定的和 `/apps` 組 `/libs`。

### 無需藍綠部署的索引管理 {#index-management-without-blue-green-deployment}

在開發期間或在內部部署安裝時，可以在執行時期新增、移除或變更索引。 索引一旦可用，就會立即使用。 如果舊版應用程式中尚未使用索引，則通常會在計畫停機期間生成索引。 在刪除索引或更改現有索引時也會發生同樣的情況。 刪除索引時，該索引在被刪除後即變為不可用。

### 採用藍綠部署的索引管理 {#index-management-with-blue-green-deployment}

使用藍綠部署，不會停機。 但是，對於索引管理，這要求索引僅用於某些版本的應用程式。 例如，在應用程式第2版中新增索引時，您仍不希望該索引用於應用程式第1版。 如果刪除索引，則情況正好相反：第2版中移除的索引在第1版中仍然需要。 更改索引定義時，我們希望舊版索引僅用於版本1，新版索引僅用於版本2。

下表顯示5個索引定義：索引 `cqPageLucene` 在兩個版本中都使用，而索引 `damAssetLucene-custom-1` 僅在版本2中使用。


> [!NOTE]
> `<indexName>-custom-<customerVersionNumber>` AEM需要做為Cloud服務，才能將它標示為現有索引的取代。

| 索引 | 現成可用的索引 | 用於第1版 | 用於第2版 |
|---|---|---|---|
| /oak:index/damAssetLucene | 是 | 是 | 否 |
| /oak:index/damAssetLucene-custom-1 | 是（自訂） | 否 | 是 |
| /oak:index/acmeProduct-custom-1 | 否 | 是 | 否 |
| /oak:index/acmeProduct-custom-2 | 否 | 否 | 是 |
| /oak:index/cqPageLucene | 是 | 是 | 是 |

每次變更索引時，版本號碼都會遞增。 為避免自訂索引名稱與產品本身的索引名稱衝突，自訂索引以及對現成可用索引的變更必須以結尾 `-custom-<number>`。

### 對現成可用索引的更改 {#changes-to-out-of-the-box-indexes}

一旦Adobe變更現成可用的索引（例如「damAssetLucene」或「cqPageLucene」），就會建立名為 `damAssetLucene-2``cqPageLucene-2` 或的新索引，或者，如果已自訂索引，則自訂的索引定義會與現成可用索引中的變更合併，如下所示。 合併變更會自動進行。 這表示，如果現成可用的索引發生變更，您不需要執行任何動作。 不過，以後可以再次自定義索引。

| 索引 | 現成可用的索引 | 用於第2版 | 用於第3版 |
|---|---|---|---|
| /oak:index/damAssetLucene-custom-1 | 是（自訂） | 是 | 否 |
| /oak:index/damAssetLucene-2-custom-1 | 是（自動從damAssetLucene-custom-1和damAssetLucene-2合併） | 否 | 是 |
| /oak:index/cqPageLucene | 是 | 是 | 否 |
| /oak:index/cqPageLucene-2 | 是 | 否 | 是 |

### 限制 {#limitations}

目前僅支援類型索引的索引管理 `lucene`。

### 刪除索引 {#removing-an-index}

如果要在應用程式的較新版本中刪除索引，則可以定義一個空索引（一個沒有要索引的資料的索引），並使用新名稱。 例如，您可以為它命名 `/oak:index/acmeProduct-custom-3`。 這將替換索引 `/oak:index/acmeProduct-custom-2`。 系統 `/oak:index/acmeProduct-custom-2` 刪除後，也可以刪除空 `/oak:index/acmeProduct-custom-3` 索引。

### 添加索引 {#adding-an-index}

若要新增名為&quot;/oak:index/acmeProduct-custom-1&quot;的索引，以便用於新版本的應用程式和更新版本，索引必須依下列方式設定：

`/oak:index/acmeProduct-custom-1`

如上所述，這可確保索引僅供新版本的應用程式使用。

### 更改索引 {#changing-an-index}

更改現有索引時，需要使用更改的索引定義添加新索引。 例如，請考慮變更現有索引&quot;/oak:index/acmeProduct-custom-1&quot;。 舊索引儲存在下面 `/oak:index/acmeProduct-custom-1`，新索引儲存在下面 `/oak:index/acmeProduct-custom-2`。

舊版應用程式使用下列組態：

`/oak:index/acmeProduct-custom-1`

新版應用程式使用下列（已變更）組態：

`/oak:index/acmeProduct-custom-2`