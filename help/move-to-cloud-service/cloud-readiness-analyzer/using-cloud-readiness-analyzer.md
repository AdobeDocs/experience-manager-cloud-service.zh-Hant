---
title: 使用Cloud Readiness Analyzer
description: 使用Cloud Readiness Analyzer
translation-type: tm+mt
source-git-commit: daa281745540e6446adecd2501e26135d6000844
workflow-type: tm+mt
source-wordcount: '1775'
ht-degree: 0%

---


# 使用Cloud Readiness Analyzer {#using-cloud-readiness-analyzer}

## 使用Cloud Readiness Analyzer的重要注意事項 {#imp-considerations}

請依照以下章節瞭解運行雲就緒性分析器(CRA)時的重要考慮事項：

* CRA報表是使用Adobe Experience Manager(AEM)模式偵測器的輸 [出建立](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/pattern-detector.html)。 CRA使用的Pattern Detector版本已包含在CRA安裝包中。

* CRA只能由管理員使用 *者* 或「管理員」群組中的使 **用者執行** 。

* CRA在6.1版及更高版本的AEM例項上受支援。

* CRA可以在任何環境下運行，但最好在 *Stage* 。

   >[!NOTE]
   >為避免對業務關鍵型實例造成影響，建議在與生產環境盡可能接近的Author測試環境上運行CRA，在定制、配置、內容和用戶應用程式方面。 或者，它可在生產作者環境的克隆上運行。

* CRA報告的生成可能需要相當長的時間，從幾分鐘到幾小時。 所需的時間量高度取決於AEM儲存庫內容的大小和性質、AEM版本和其他因素。

* 由於產生報表需要大量時間，因此結果會保留在快取中，並可供後續檢視和下載，直到快取過期或明確重新整理報表為止。

## 可用性 {#availability}

Cloud Readiness Analyzer可從軟體分發門戶下載為zip檔案。 您可以透過Package Manager在來源Adobe Experience Manager(AEM)例項上安裝套件。

>[!NOTE]
>從待定的軟體分發門戶下載Cloud Readiness Analyzer **。

## 運行Cloud Readiness Analyzer {#running-tool}

請依照本節內容瞭解如何運行Cloud Readiness Analyzer:

1. 選擇Adobe Experience Manager並導覽至工具-> **Operations** -> **Cloud Readiness Analyzer**。

   ![影像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-1.png)

1. 按一下「 **Cloud Readiness Analyzer**」後，該工具就會開始產生報表，幾分鐘後AEM例項就會提供摘要報表。

   >[!NOTE]
   >您必須向下捲動頁面才能檢視完整報表。

   ![影像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-2.png)

## 解讀Cloud Readiness Analyzer組織報告 {#organized-report}

在AEM例項中執行Cloud Readiness Analyzer時，報表會在工具視窗中顯示為結果。

報表格式為：

* *報表概述*: 報表本身的相關資訊，包括報表產生的時間。
* *系統概述*: CRA所在AEM系統的相關資訊。
* *尋找類別*: 每個區段都處理同一類別的一或多個發現。 每個區段都包含下列項目： 類別名稱、子類型、尋找計數和重要性、摘要、類別檔案的連結，以及個別尋找資訊。

系統會為每個尋找指派重要度，以指出動作的粗略優先順序。

請遵循下表來瞭解重要性等級：

| 重要性 | 說明 |
|--- |--- |
| 資訊 | This finding is provided for informational purposes. |
| 建議 | This finding is potentially an upgrade issue. 建議進一步調查。 |
| 主要 | This finding is likely to be an upgrade issue that should be addressed. |
| CRITICAL | This finding is very likely to be an upgrade issue that must be addressed to prevent loss of function or performance. |

### Adobe Experience Manager 6.3 and later {#aem-older-version}

For AEM 6.3 and above, the primary way to run Cloud Readiness Analyzer is to:

1. 選擇Adobe Experience Manager實例，並導覽至工具-> **操作** -> **Cloud Readiness Analyzer**。

   >[!NOTE]
   >The CRA will begin a background process to generate the report as soon as the tool is opened. 它會顯示報表產生在準備就緒之前的指示。 您可以關閉瀏覽器標籤，稍後再返回，在報表完成時檢視報表。

1. 產生並顯示CRA報表後，您就可以選擇以逗號分隔值(CSV)下載報表。 按一下 **CSV** ，以逗號分隔值(CSV)格式下載完整的摘要報表，如下圖所示。

   ![影像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-3.png)

   >[!NOTE]
   >您可以按一下左上角的「重新整理報表」按鈕，強制CRA清除其快取並重新產生 **報表** 。

### Adobe Experience Manager 6.2和6.1 {#aem-specific-versions}

Cloud Readiness Analyzer在Adobe Experience Manager(AEM)6.2中僅限於產生和下載CSV報表的連結。

>[!NOTE]
>
>* 對於Adobe Experience Manager 6.1，工具無法運作，只能使用HTTP介面。
   >
   >
* 在所有版本中，隨附的圖樣偵測器可獨立執行。


請依照下列步驟下載Adobe Experience Manager(AEM)6.1和6.2的CSV報表：

1.導覽至 **Adobe Experience Manager Web Console使用設定**`https://serveraddress:serverport/system/console/configMgr`。

1. 選擇「 **狀態** 」標籤，並從下拉式清單中搜尋「模式偵測器 **** 」，如下圖所示。

   ![影像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-4.png)

1. 您可以將摘要報表下載至Zip資料夾或JSON格式。

## 解讀Cloud Readiness Analyzer CSV報告 {#crs-csv-report}

當您按一下AEM例項的 **CSV** 選項時，「雲端就緒性分析器」報表的CSV格式會從結果快取建立，並傳回至您的瀏覽器。 根據您的瀏覽器設定，此報告會自動下載為預設名稱的檔案 `results.csv`。 如果快取已過期，則報表將在建立和下載CSV檔案之前重新產生。

The CSV format of the report includes information that is generated from the Pattern Detector output, sorted and organized by category type, sub-type, and importance level. 其格式適用於在Microsoft Excel等應用程式中檢視和編輯。 它旨在以可重複的格式提供所有的查找資訊，在比較報告以衡量進度時，這些資訊會有所幫助。

The columns of the CSV format report are:

* **程式碼**: 類別代碼
* **類型**: 類別名稱
* **子類型**: 類別子類型
* **重要性**: 重要性級別
* **識別碼**: 尋找的主要識別碼
* **其他**: 關於尋找的其他資訊
* **message**: the message provided for the finding
* **moreInfo**: 可用來存取類別相關線上說明的連結
* **context**: a JSON string of finding data

個別尋找的欄中值&quot;\N&quot;表示未提供任何資料。

## HTTP介面 {#http-interface}

CRA提供HTTP介面，可用作AEM例項的替代項目。 該介面同時支援HEAD和GET命令。 它可用於生成CRA報告，並以三種格式之一返回： JSON、CSV和Tab分隔值(TSV)。

以下URL可用於HTTP訪問，其中 `<host>` 是安裝CRA的伺服器的主機名和埠（如果需要）:
* `http://<host>/apps/readiness-analyzer/analysis/result.json` for JSON format
* `http://<host>/apps/readiness-analyzer/analysis/result.csv` CSV格式
* `http://<host>/apps/readiness-analyzer/analysis/result.tsv` TSV格式

### 執行HTTP請求 {#executing-http-request}

HTTP介面可用於多種方法。

一個簡單的方式是在您已以管理員身分登入AEM的相同瀏覽器中開啟瀏覽器標籤。 您可以在瀏覽器標籤中輸入URL，並讓瀏覽器顯示或下載結果。

您也可以使用命令列工具，例如或 `curl` 以 `wget` 及任何HTTP用戶端應用程式。 當未使用瀏覽器標籤和已驗證的作業時，您必須提供管理使用者名稱和密碼作為注釋的一部分。

以下是如何做到的範例：
`curl -u admin:admin 'http://localhost:4502/apps/readiness-analyzer/analysis/result.csv' > result.csv`.

### 標題和參數 {#http-headers-and-parameters}

此介面使用下列HTTP標題：

* `Cache-Control: max-age=<seconds>`: 以秒為單位指定快取新鮮度存留期。 (See [RFC 7234](https://tools.ietf.org/html/rfc7234#section-5.2.2.8).)
* `Prefer: respond-async`: 表示伺服器應非同步響應。 (請參見 [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.1)。)

The following HTTP query parameters are available as a convenience for when HTTP headers might not be easily used:

* `max-age` (number, optional): Specify the cache freshness lifetime in seconds. This number must be 0 or greater. The default freshness lifetime is 86400 seconds, meaning that without this parameter or the corresponding header a fresh cache will be used to serve requests for 24 hours before the report must be regenerated. Using `max-age=0` will force the cache to be cleared and initiate a regeneration of the report. Immediately following this request the freshness lifetime will be reset to the previous non-zero value.
* `respond-async` （布林值，可選）: 指定應以非同步方式提供回應。 當快 `respond-async=true` 取過期時，伺服器會傳回回的回應，而不 `202 Accepted, processing cache` 需等待報表產生和快取重新整理。 如果快取是新鮮的，則此參數無效。 The default value is `false`, meaning that without this parameter or the corresponding header, the server will respond synchronously, which may require a significant amount of time and require an adjustment to the maximum response time for the HTTP client.

當HTTP標題和對應的查詢參數同時存在時，查詢參數優先。

透過HTTP介面開始產生報表的簡單方式是使用下列命令：
`curl -u admin:admin 'http://localhost:4502/apps/readiness-analyzer/analysis/result.json?max-age=0&respond-async=true'`.

在提出請求後，用戶端就不需要維持作用中狀態，即可產生報表。 報表產生可以由一個用戶端使用HTTP GET請求啟動，報表產生後，可從另一個用戶端的快取或AEM例項的CSV工具檢視。

### 回應(#http-responses)

可能有下列回應值：

* `200 OK`: 響應包含在快取的新鮮期內生成的來自模式檢測器的發現。
* `202 Accepted, processing cache`: 提供非同步回應，以指出快取已過時且正在重新整理。
* `400 Bad Request`: 指出請求發生錯誤。 「問題詳細資訊」格式的消息(請 [參見RFC 7807](https://tools.ietf.org/html/rfc7807))提供了詳細資訊。
* `401 Unauthorized`: 請求未獲得授權。
* `500 Internal Server Error`: 表示發生內部伺服器錯誤。 「問題詳細資訊」格式的消息提供了詳細資訊。
* `503 Service Unavailable`: 表示伺服器正忙於另一個響應，無法及時為此請求提供服務。 只有在發出同步請求時，才會發生這種情況。 「問題詳細資訊」格式的消息提供了詳細資訊。

## 快取存留期調整 {#cache-adjustment}

預設的CRA快取存留期為24小時。 With the option for refreshing a report, and regenerating the cache, in both the AEM instance and the HTTP interface, this default value is likely to be appropriate for most uses of the CRA. If the report generation time is particularly long for your AEM instance, you may wish to adjust the cache lifetime in order to minimize the regeneration of the report.

快取存留期值儲存為以下儲存庫 `maxCacheAge` 節點上的屬性：
`/apps/readiness-analyzer/content/CloudReadinessReport/jcr:content`

此屬性的值是快取存留期（以秒為單位）。 管理員可以使用CRX/DE Lite調整快取存留期。





