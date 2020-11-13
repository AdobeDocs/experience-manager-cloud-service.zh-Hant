---
title: 使用最佳實踐分析器
description: 使用最佳實踐分析器
translation-type: tm+mt
source-git-commit: 07180809ff8b4a42a07eb9c691ab7a99262742ec
workflow-type: tm+mt
source-wordcount: '2207'
ht-degree: 47%

---


# 使用最佳實踐分析器 {#using-best-practices-analyzer}

## 使用最佳實踐分析器的重要考慮事項 {#imp-considerations}

請依照以下章節瞭解執行最佳實務分析器(BPA)的重要考量事項：

* The BPA report is built using the output of the Adobe Experience Manager (AEM) [Pattern Detector](https://docs.adobe.com/content/help/zh-Hant/experience-manager-65/deploying/upgrading/pattern-detector.html). BPA使用的Pattern Detector版本包含在BPA安裝包中。

* BPA may only be run by the **admin** user or a user in the **administrators** group.

* BPA在6.1版及更高版本的AEM例項上受支援。

   >[!NOTE]
   > Please see [Installing on AEM 6.1](#installing-on-aem61) for special requirements for installing BPA on AEM 6.1.

* BPA can run on any environment, but it is preferred to have it run on a *Stage* environment.

   >[!NOTE]
   >In order to avoid an impact on business critical instances, it is recommended that you run BPA on an *Author* environment that is as close as possible to the *Production* environment in the areas of customizations, configurations, content and user applications. 或者，您可以在複製的生產&#x200B;*製作*&#x200B;環境中執行 CRA。

* 生成BPA報告內容可能需要相當長的時間，從幾分鐘到幾小時。 所需的時間主要取決於 AEM 存放庫內容的大小和性質、AEM 版本和其他因素。

* 由於產生報表內容可能需要相當長的時間，因此這些內容會由背景程序產生，並儲存在快取中。檢視和下載報表的速度則相對迅速，因為此時會使用內容快取，直到快取過期或報表明確重新整理為止。在產生報表內容期間，您可以先關閉瀏覽器索引標籤，等稍後內容已存放於快取時，再回過頭檢視報表。

## 可用性 {#availability}

Best Practices Analyzer可從「軟體散發」入口網站下載為zip檔案。 您可以透過「封裝管理程式」，在來源 Adobe Experience Manager AEM) 例項上安裝封裝。

>[!NOTE]
>Download the Best Practices Analyzer from the [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) portal.

## 查看最佳實踐分析器報告 {#viewing-report}

### Adobe Experience Manager 6.3.0 和更新版本 {#aem-later-versions}

請依照本節內容瞭解如何查看最佳實踐分析器報告：

1. Select Adobe Experience Manager and navigate to tools -> **Operations** -> **Best Practices Analyzer**.

   ![影像](/help/move-to-cloud-service/best-practices-analyzer/assets/BPA_pic1.png)

1. 按一下「 **產生報表** 」以執行最佳實務分析器。

   ![影像](/help/move-to-cloud-service/best-practices-analyzer/assets/BPA_pic2.png)

1. 當BPA產生報表時，您可在螢幕上看到工具所做的進度。 它顯示分析的項目數，也顯示找到的發現數。

   ![影像](/help/move-to-cloud-service/best-practices-analyzer/assets/BPA_pic3.png)


1. 生成BPA報告後，它以按查找類型和重要性級別組織的表格格式顯示摘要和查找結果數。 若要取得有關特定尋找的詳細資訊，您可以按一下表格中與尋找類型對應的數字。

   ![影像](/help/move-to-cloud-service/best-practices-analyzer/assets/BPA_pic4.png)

   上述動作會自動捲動至報表中該尋找的位置。

   ![影像](/help/move-to-cloud-service/best-practices-analyzer/assets/BPA_pic5.png)

1. You have the option of downloading the report in a comma-separated values (CSV) format by clicking on **CSV**, as shown in the figure below.

   ![影像](/help/move-to-cloud-service/best-practices-analyzer/assets/BPA_pic6.png)

   >[!NOTE]
   >You may force the BPA to clear its cache and regenerate the report by clicking **Refresh Report**.

   ![影像](/help/move-to-cloud-service/best-practices-analyzer/assets/BPA_pic7.png)

   >[!NOTE]
   >在重新產生報表時，會以完成百分比顯示進度，如下圖所示。

   ![影像](/help/move-to-cloud-service/best-practices-analyzer/assets/BPA_pic8.png)


### Adobe Experience Manager 6.2 和 6.1 {#aem-specific-versions}

Adobe Experience Manager 6.2中的「最佳實務分析器」工具僅限於產生和下載CSV報表的連結。

在 Adobe Experience Manager 6.1 中，此工具無法運作，而只能使用 HTTP 介面。

>[!NOTE]
>在所有版本中，隨附的模式偵測器皆可獨立執行。

## 解讀最佳實踐分析器報告 {#cra-report}

在AEM例項中執行「最佳實務分析器」工具時，報表會在工具視窗中顯示為結果。

報表格式為：

* **報表概覽**：報表本身的相關資訊，包括下列資訊：
   * **報告時間**：產生報表內容並首次提供的時間。
   * **到期時間**：報表內容快取的到期時間。
   * **產生時段**：報表內容產生程序所花費的時間。
   * **結果計數**：報表中包含的結果總數。
* **系統概述**:有關執行BPA的AEM系統的資訊。
* **結果類別**：分別處理一或多個同類結果的多個區段。每個區段各包含下列項目：類別名稱、子類型、結果計數和重要性、摘要、類別文件的連結，以及個別結果資訊。

系統會為每個結果指派一個重要性層級，以指出動作的概略優先順序。

>[!NOTE]
>若要進一步瞭解每個「尋找類別」，請參閱「模 [式偵測器類別」](https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html)。

請參考下表以了解重要性層級：

| 重要性 | 說明 |
|--- |--- |
| 資訊 | 此結果僅供參考。 |
| 建議 | 此結果可能是升級問題。建議進一步調查。 |
| 重要 | 此結果可能是需要解決的升級問題。 |
| 關鍵 | 此結果很可能是升級問題，必須解決以防止失去功能或效能。 |


## 解讀最佳實務分析器CSV報告 {#cra-csv-report}

When you click the **CSV** option from your AEM instance, the CSV format of the Best Practices Analyzer report is built from the content cache and returned to your browser. 根據您的瀏覽器設定，此報表將會以檔案格式自動下載，且具有預設名稱 `results.csv`。

如果快取已過期，則會在 CSV 檔案建置和下載之前重新產生報表。

CSV 格式的報表包含從「模式偵測器」輸出產生的資訊，且會依類別類型、子類型和重要性層級排序和組織。其格式適用於 Microsoft Excel 等應用程式的檢視和編輯作業。其目的是要以可重複的格式提供所有的結果資訊，以利進行長時間的報表比較，藉此衡量進度。

CSV 格式報表的欄包括：

* **代碼**：類別代碼
* **類型**：類別名稱
* **子類型**：類別的子類型
* **重要性**：重要性層級
* **識別碼**：結果的主要識別碼
* **其他**：關於結果的其他資訊
* **訊息**：為結果提供的訊息
* **更多資訊**：可用來存取類別相關線上說明的連結
* **內容**：結果資料的 JSON 字串

個別結果的欄中若有 &quot;\N&quot; 值，表示未提供任何資料。

## HTTP 介面 {#http-interface}

BPA提供HTTP介面，可用作AEM中使用者介面的替代選項。 該介面同時支援 HEAD 和 GET 命令。它可用於生成BPA報告並以三種格式之一返回：JSON、CSV和Tab分隔值(TSV)。

The following URLs are available for HTTP access, where `<host>` is the hostname, and port if necessary, of the server on which the BPA is installed:
* `http://<host>/apps/best-practices-analyzer/analysis/report.json` (JSON 格式)
* `http://<host>/apps/best-practices-analyzer/analysis/report.csv` (CSV 格式)
* `http://<host>/apps/best-practices-analyzer/analysis/report.tsv` (TSV 格式)

### 執行 HTTP 要求 {#executing-http-request}

HTTP 介面可用於多種方法中。

其中一個簡單的方式，是在您已用管理員身分登入 AEM 的相同瀏覽器中開啟瀏覽器索引標籤。您可以在瀏覽器索引標籤中輸入 URL，並且讓瀏覽器顯示或下載結果。

您也可以使用命令列工具 (例如 `curl` 或 `wget`) 以及任何 HTTP 用戶端應用程式。未在已驗證的工作階段中使用瀏覽器索引標籤時，您必須在註解中提供管理使用者名稱和密碼。

以下是其操作方式的範例：
`curl -u admin:admin 'http://localhost:4502/apps/best-practices-analyzer/analysis/report.csv' > report.csv`。

### 標題和參數 {#http-headers-and-parameters}

此介面使用下列 HTTP 標題：

* `Cache-Control: max-age=<seconds>`:以秒為單位指定快取新鮮度存留期。 (請參閱 [RFC 7234](https://tools.ietf.org/html/rfc7234#section-5.2.2.8)。)
* `Prefer: respond-async`:指定伺服器應非同步響應。 (請參閱 [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.1)。)
* `Prefer: return=minimal`:指定伺服器應返回最小響應。 (請參閱 [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.2)。)

在不方便使用 HTTP 標題時，可權衡使用下列 HTTP 查詢參數：

* `max-age` （數字、可選）:以秒為單位指定快取新鮮度存留期。 此數字必須大於或等於 0。預設新鮮度存留期為86400秒。 若沒有此參數或對應的標題，則會使用新的快取來提供24小時的請求，此時必須重新產生快取。 使 `max-age=0` 用將強制清除快取，並使用新產生的快取的先前非零新鮮度期限，開始重新產生報表。
* `respond-async` （布林值，可選）:指定應非同步提供響應。 Using `respond-async=true` when the cache is stale will cause the server to return a response of `202 Accepted` without waiting for the cache to be refreshed and for the report to be generated. 如果快取為最新狀態，此參數就沒有效用。The default value is `false`. Without this parameter or the corresponding header the server will respond synchronously, which may require a significant amount of time and require an adjustment to the maximum response time for the HTTP client.
* `may-refresh-cache` （布林值，可選）:指定當當前快取為空、過時或即將過時時，伺服器可以響應請求刷新快取。 如 `may-refresh-cache=true`果或未指定，則伺服器可以啟動將調用模式檢測器並刷新快取的後台任務。 如 `may-refresh-cache=false` 果快取為空或過時，伺服器將不會啟動原本會執行的任何重新整理工作，此時報表會為空。 任何已在處理中的刷新任務都將不受此參數的影響。
* `return-minimal` （布林值，可選）:指定來自伺服器的回應應僅包含包含進度指示和JSON格式快取狀態的狀態。 如 `return-minimal=true`果，則響應主體將限制為狀態對象。 如 `return-minimal=false`果或未指定，則會提供完整回應。
* `log-findings` （布林值，可選）:指定伺服器在首次構建或刷新快取時應記錄其內容。 快取中的每個尋找都會記錄為JSON字串。 只有在請求產生新快取 `log-findings=true` 時，才會發生此記錄。

當 HTTP 標頭和對應的查詢參數均存在時，將會以查詢參數優先。

要透過 HTTP 介面開始產生報表，有個簡單的方式是使用下列命令：
`curl -u admin:admin 'http://localhost:4502/apps/best-practices-analyzer/analysis/report.json?max-age=0&respond-async=true'`。

在提出要求後，用戶端無須維持作用中狀態，即可產生報表。報表產生可以由一個用戶端使用HTTP GET請求啟動，報表產生後，就可透過另一個用戶端的快取或AEM使用者介面中的BPA工具從快取中檢視。

### 回應 {#http-responses}

可能的回應值如下：

* `200 OK`:指出回應包含來自模式偵測器的發現，這些發現是在快取的新鮮期內產生的。
* `202 Accepted`:用於指示快取過時。 當且 `respond-async=true` 此 `may-refresh-cache=true` 回應表示正在進行刷新任務。 當此 `may-refresh-cache=false` 回應僅表示快取過時。
* `400 Bad Request`：表示要求發生錯誤。A message in Problem Details format (see [RFC 7807](https://tools.ietf.org/html/rfc7807)) provides more details.
* `401 Unauthorized`:表示請求未獲得授權。
* `500 Internal Server Error`：表示發生了內部伺服器錯誤。「問題詳細資料」格式的訊息可提供更多詳細資料。
* `503 Service Unavailable`：表示伺服器正在處理另一個回應，而無法及時處理此要求。只有在提出同步要求時，才可能發生這種情況。「問題詳細資料」格式的訊息可提供更多詳細資料。

## 管理員資訊

### 快取存留期調整 {#cache-adjustment}

預設的BPA快取存留期為24小時。 透過AEM例項和HTTP介面中重新整理報表和重新產生快取的選項，此預設值可能適用於BPA的大部分使用。 如果您 AEM 例項中的報表產生時間特別長，您可以調整快取存留期，以盡快重新產生報表。

快取存留期值會儲存為下列存放庫節點上的 `maxCacheAge` 屬性：
`/apps/best-practices-analyzer/content/BestPracticesReport/jcr:content`

此屬性的值是快取存留期 (以秒為單位)。管理員可以使用 CRX/DE Lite 調整快取存留期。

### 在 AEM 6.1 上安裝 {#installing-on-aem61}

BPA utilizes a system service user account named `repository-reader-service` to execute the Pattern Detector. 此帳戶適用於 AEM 6.2 和更新版本。On AEM 6.1, this account must be created *prior to* installation of BPA by taking the following steps:

1. 依照[建立新的服務使用者](https://docs.adobe.com/content/help/zh-Hant/experience-manager-65/administering/security/security-service-users.html#creating-a-new-service-user)中的指示建立使用者。將 UserID 設為 `repository-reader-service`，並將中繼路徑保留為空白，然後按一下綠色核取記號。

2. 依照[管理使用者和群組](https://docs.adobe.com/content/help/zh-Hant/experience-manager-65/administering/security/security.html#managing-users-and-groups)中的指示 (尤其是「將使用者新增至群組」的指示)，將 `repository-reader-service` 使用者新增至 `administrators` 群組。

3. 透過Package Manager在您的來源AEM例項上安裝BPA套件。 (這將會在 `repository-reader-service` 系統服務使用者的 ServiceUserMapper 設定中新增必要的設定修正。)
