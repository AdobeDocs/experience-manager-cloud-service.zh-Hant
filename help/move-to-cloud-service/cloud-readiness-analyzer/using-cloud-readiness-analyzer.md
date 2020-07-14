---
title: 使用 Cloud Readiness Analyzer
description: 使用 Cloud Readiness Analyzer
translation-type: ht
source-git-commit: a0e58c626f94b778017f700426e960428b657806
workflow-type: ht
source-wordcount: '1871'
ht-degree: 100%

---


# 使用 Cloud Readiness Analyzer {#using-cloud-readiness-analyzer}

## 使用 Cloud Readiness Analyzer 的重要考量 {#imp-considerations}

請參考以下章節，瞭解執行 Cloud Readiness Analyzer (CRA) 時的重要考量：

* CRA 報表是使用 Adobe Experience Manager (AEM) [模式偵測器](https://docs.adobe.com/content/help/zh-Hant/experience-manager-65/deploying/upgrading/pattern-detector.html)的輸出所建置。CRA 使用的模式偵測器版本包含在 CRA 安裝封裝中。

* CRA 只能由&#x200B;**管理員**&#x200B;使用者或&#x200B;**管理員**&#x200B;群組中的使用者執行。

* CRA 在 6.1 版和更高版本的 AEM 例項上受支援。

   >[!NOTE]
   > 如需在 AEM 6.1 上安裝 CRA 的特殊需求，請參閱[在 AEM 6.1 上安裝](#installing-on-aem61)。

* CRA 可在任何環境中執行，但最好執行於&#x200B;*預備*&#x200B;環境中。

   >[!NOTE]
   >為避免對業務關鍵例項造成影響，建議您在盡可能接近&#x200B;*生產*&#x200B;環境的&#x200B;*製作*&#x200B;環境中，對自訂、設定、內容和使用者應用程式等方面執行 CRA。或者，您可以在複製的生產&#x200B;*製作*&#x200B;環境中執行 CRA。

* 產生 CRA 報表內容可能需要相當長的時間，從幾分鐘到數小時不等。所需的時間主要取決於 AEM 存放庫內容的大小和性質、AEM 版本和其他因素。

* 由於產生報表內容可能需要相當長的時間，因此這些內容會由背景程序產生，並儲存在快取中。檢視和下載報表的速度則相對迅速，因為此時會使用內容快取，直到快取過期或報表明確重新整理為止。在產生報表內容期間，您可以先關閉瀏覽器索引標籤，等稍後內容已存放於快取時，再回過頭檢視報表。

## 可用性 {#availability}

您可以從軟體發佈入口網站下載 Cloud Readiness Analyzer 的 ZIP 檔案。您可以透過「封裝管理程式」，在來源 Adobe Experience Manager AEM) 例項上安裝封裝。

>[!NOTE]
>從[軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)入口網站下載 Cloud Readiness Analyzer。

## 檢視 Cloud Readiness Analyzer 報表 {#viewing-report}

### Adobe Experience Manager 6.3.0 和更新版本 {#aem-later-versions}

請參考本節內容，瞭解如何檢視 Cloud Readiness Analyzer 報表：

1. 選取 Adobe Experience Manager，並導覽至「工具 -> **操作** -> **Cloud Readiness Analyzer」**。

   ![影像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-1.png)

1. 在您按一下 **Cloud Readiness Analyzer** 後，此工具就會開始產生報表，並在報表可用時加以顯示。

   >[!NOTE]
   >您必須向下捲動頁面才能檢視完整報表。

   ![影像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-tool-1.png)

1. CRA 報表產生並顯示後，您可以選擇按一下 **CSV** 下載逗點分隔值 (CSV) 格式的報表，如下圖所示。

   ![影像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-tool-2.png)

   >[!NOTE]
   >您可以按一下&#x200B;**「重新整理報表」**，以強制 CRA 清除其快取並重新產生報表。

### Adobe Experience Manager 6.2 和 6.1 {#aem-specific-versions}

Cloud Readiness Analyzer 工具限用於 Adobe Experience Manager 6.2 中，可透過連結產生和下載 CSV 報表。

在 Adobe Experience Manager 6.1 中，此工具無法運作，而只能使用 HTTP 介面。

>[!NOTE]
>在所有版本中，隨附的模式偵測器皆可獨立執行。

## 解譯 Cloud Readiness Analyzer 報表 {#cra-report}

在 AEM 例項中執行 Cloud Readiness Analyzer 工具時，報表會在工具視窗中顯示為結果。

報表格式為：

* **報表概覽**：報表本身的相關資訊，包括下列資訊：
   * **報告時間**：產生報表內容並首次提供的時間。
   * **到期時間**：報表內容快取的到期時間。
   * **產生時段**：報表內容產生程序所花費的時間。
   * **結果計數**：報表中包含的結果總數。
* **系統概覽**：CRA 執行所在之 AEM 系統的相關資訊。
* **結果類別**：分別處理一或多個同類結果的多個區段。每個區段各包含下列項目：類別名稱、子類型、結果計數和重要性、摘要、類別文件的連結，以及個別結果資訊。

系統會為每個結果指派一個重要性層級，以指出動作的概略優先順序。

請參考下表以了解重要性層級：

| 重要性 | 說明 |
|--- |--- |
| 資訊 | 此結果僅供參考。 |
| 建議 | 此結果可能是升級問題。建議進一步調查。 |
| 重要 | 此結果可能是需要解決的升級問題。 |
| 關鍵 | 此結果很可能是升級問題，必須解決以防止失去功能或效能。 |


## 解譯 Cloud Readiness Analyzer CSV 報表 {#cra-csv-report}

當您按一下 AEM 例項的 **CSV** 選項時，將會從內容快取建置 CSV 格式的 Cloud Readiness Analyzer 報表，並傳回至您的瀏覽器。根據您的瀏覽器設定，此報表將會以檔案格式自動下載，且具有預設名稱 `results.csv`。

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

CRA 提供 HTTP 介面，可作為 AEM 使用者介面的替代介面。該介面同時支援 HEAD 和 GET 命令。它可用來產生 CRA 報表，並以三種格式之一加以傳回：JSON、CSV 和定位鍵分隔值 (TSV)。

下列 URL 可用於 HTTP 存取，其中，`<host>` 是 CRA 安裝所在之伺服器的主機名稱和連接埠 (如有需要)：
* `http://<host>/apps/readiness-analyzer/analysis/result.json` (JSON 格式)
* `http://<host>/apps/readiness-analyzer/analysis/result.csv` (CSV 格式)
* `http://<host>/apps/readiness-analyzer/analysis/result.tsv` (TSV 格式)

### 執行 HTTP 要求 {#executing-http-request}

HTTP 介面可用於多種方法中。

其中一個簡單的方式，是在您已用管理員身分登入 AEM 的相同瀏覽器中開啟瀏覽器索引標籤。您可以在瀏覽器索引標籤中輸入 URL，並且讓瀏覽器顯示或下載結果。

您也可以使用命令列工具 (例如 `curl` 或 `wget`) 以及任何 HTTP 用戶端應用程式。未在已驗證的工作階段中使用瀏覽器索引標籤時，您必須在註解中提供管理使用者名稱和密碼。

以下是其操作方式的範例：
`curl -u admin:admin 'http://localhost:4502/apps/readiness-analyzer/analysis/result.csv' > result.csv`。

### 標題和參數 {#http-headers-and-parameters}

此介面使用下列 HTTP 標題：

* `Cache-Control: max-age=<seconds>`：指定快取時效性存留期 (以秒為單位)。(請參閱 [RFC 7234](https://tools.ietf.org/html/rfc7234#section-5.2.2.8)。)
* `Prefer: respond-async`：指出伺服器應以非同步方式回應。(請參閱 [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.1)。)

在不方便使用 HTTP 標題時，可權衡使用下列 HTTP 查詢參數：

* `max-age` (數字，選用)：指定快取時效性存留期 (以秒為單位)。此數字必須大於或等於 0。預設的時效性存留期為 86400 秒，這表示在沒有此參數或對應標頭的情況下，有效快取將在 24 小時內用來回應要求，其後則必須重新產生報表。使用 `max-age=0` 將會強制清除快取，並起始重新產生報表的作業。處理完此要求後，時效性存留期會隨即重設為先前的非零值。
* `respond-async` (布林值，選用)：指定應以非同步方式提供回應。在快取已過期時使用 `respond-async=true`，會使伺服器逕行傳回 `202 Accepted, processing cache` 的回應，而不等待報表產生和快取重新整理。如果快取為最新狀態，此參數就沒有效用。預設值為 `false`，這表示在沒有此參數或對應標頭的情況下，伺服器將會同步回應，而這可能需要相當長的時間，且需要調整 HTTP 用戶端的最大回應時間。

當 HTTP 標頭和對應的查詢參數均存在時，將會以查詢參數優先。

要透過 HTTP 介面開始產生報表，有個簡單的方式是使用下列命令：
`curl -u admin:admin 'http://localhost:4502/apps/readiness-analyzer/analysis/result.json?max-age=0&respond-async=true'`。

在提出要求後，用戶端無須維持作用中狀態，即可產生報表。報表產生作業可以由一個用戶端使用 HTTP GET 要求來起始，且報表產生後，可由另一個用戶端從快取加以檢視，或以 AEM 使用者介面中的 CSV 工具檢視。

### 回應 {#http-responses}

可能的回應值如下：

* `200 OK`：此回應包含「模式偵測器」在快取的時效性存留期內產生的結果。
* `202 Accepted, processing cache`：針對非同步回應而提供，用以指出快取已過時且正在重新整理。
* `400 Bad Request`：表示要求發生錯誤。「問題詳細資料」格式的訊息 (請參閱 [RFC 7807](https://tools.ietf.org/html/rfc7807)) 可提供更多詳細資料。
* `401 Unauthorized`：要求未獲授權。
* `500 Internal Server Error`：表示發生了內部伺服器錯誤。「問題詳細資料」格式的訊息可提供更多詳細資料。
* `503 Service Unavailable`：表示伺服器正在處理另一個回應，而無法及時處理此要求。只有在提出同步要求時，才可能發生這種情況。「問題詳細資料」格式的訊息可提供更多詳細資料。

## 管理員資訊

### 快取存留期調整 {#cache-adjustment}

預設的 CRA 快取存留期為 24 小時。在 AEM 例項和 HTTP 介面中使用重新整理報表和重新產生快取的選項時，此預設值應該都適用於 CRA 大部分的使用案例。如果您 AEM 例項中的報表產生時間特別長，您可以調整快取存留期，以盡快重新產生報表。

快取存留期值會儲存為下列存放庫節點上的 `maxCacheAge` 屬性：
`/apps/readiness-analyzer/content/CloudReadinessReport/jcr:content`

此屬性的值是快取存留期 (以秒為單位)。管理員可以使用 CRX/DE Lite 調整快取存留期。

### 在 AEM 6.1 上安裝 {#installing-on-aem61}

CRA 會使用名為 `repository-reader-service` 的系統服務使用者帳戶來執行模式偵測器。此帳戶適用於 AEM 6.2 和更新版本。在 AEM 6.1 中，您必須執行下列步驟，在安裝 CRA *之前*&#x200B;建立此帳戶：

1. 依照[建立新的服務使用者](https://docs.adobe.com/content/help/zh-Hant/experience-manager-65/administering/security/security-service-users.html#creating-a-new-service-user)中的指示建立使用者。將 UserID 設為 `repository-reader-service`，並將中繼路徑保留為空白，然後按一下綠色核取記號。

2. 依照[管理使用者和群組](https://docs.adobe.com/content/help/zh-Hant/experience-manager-65/administering/security/security.html#managing-users-and-groups)中的指示 (尤其是「將使用者新增至群組」的指示)，將 `repository-reader-service` 使用者新增至 `administrators` 群組。

3. 透過封裝管理程式，在您的來源 AEM 例項上安裝 CRA 封裝。(這將會在 `repository-reader-service` 系統服務使用者的 ServiceUserMapper 設定中新增必要的設定修正。)
