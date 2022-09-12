---
title: 使用Best Practices Analyzer
description: 使用Best Practices Analyzer
exl-id: e8498e17-f55a-4600-87d7-60584d947897
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '2470'
ht-degree: 41%

---

# 使用Best Practices Analyzer {#using-best-practices-analyzer}

>[!CONTEXTUALHELP]
>id="aemcloud_bpa_using"
>title="使用Best Practices Analyzer"
>abstract="檢閱使用Best Practices Analyzer（原稱為Cloud Readiness Analyzer）的說明檔案以及產生的報表。 Best Practices Analyzer報表可用來取得對一般升級整備程度的高層了解。"
>additional-url="https://my.adobeconnect.com/pqgrfezoxghs?proto=true" text="[Webinar] Introducing Tools to Accelerate the Journey to Adobe Experience Manager as a Cloud Service"

## 使用Best Practices Analyzer的重要考量 {#imp-considerations}

請依照以下章節了解執行Best Practices Analyzer(BPA)時的重要考量：

* BPA報表是使用Adobe Experience Manager(AEM)的輸出所建立 [圖樣偵測器](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/pattern-detector.html). BPA使用的模式檢測器版本包含在BPA安裝包中。

* BPA只能由 **管理員** 使用者或 **管理員** 群組。

* 6.1版及更新版本的AEM例項支援BPA。

   >[!NOTE]
請參閱 [在AEM 6.1上安裝](#installing-on-aem61) 在AEM 6.1上安裝BPA的特殊要求。

* BPA可在任何環境中運行，但最好在 *階段* 環境。

   >[!NOTE]
為避免對業務關鍵實例造成影響，建議您在 *作者* 最接近的環境 *生產* 環境，包括自訂、設定、內容和使用者應用程式。 或者，您可以在複製的生產&#x200B;*製作*&#x200B;環境中執行 CRA。

* 生成BPA報告內容可能需要相當長的時間，從幾分鐘到數小時不等。 所需的時間主要取決於 AEM 存放庫內容的大小和性質、AEM 版本和其他因素。

* 由於產生報表內容可能需要相當長的時間，因此這些內容會由背景程序產生，並儲存在快取中。檢視和下載報表的速度則相對迅速，因為此時會使用內容快取，直到快取過期或報表明確重新整理為止。在產生報表內容期間，您可以先關閉瀏覽器索引標籤，等稍後內容已存放於快取時，再回過頭檢視報表。

## 可用性 {#availability}

[!CONTEXTUALHELP]
id="aemcloud_bpa_download"
title="下載Best Practices Analyzer"
abstract="您可以從軟體發佈入口網站下載Best Practices Analyzer的ZIP檔案。 您可以透過「封裝管理程式」，在來源 Adobe Experience Manager AEM) 例項上安裝封裝。"

您可以從軟體發佈入口網站下載Best Practices Analyzer的ZIP檔案。 您可以透過 [封裝管理員](/help/implementing/developing/tools/package-manager.md) 在來源Adobe Experience Manager(AEM)例項上。

>[!NOTE]
從下載Best Practices Analyzer [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) 入口網站。

## 檢視Best Practices Analyzer報表 {#viewing-report}

### Adobe Experience Manager 6.3.0 和更新版本 {#aem-later-versions}

請依照本節，了解如何檢視Best Practices Analyzer報表：

1. 選取Adobe Experience Manager並導覽至工具 — > **操作** -> **Best Practices Analyzer**.

   ![影像](/help/journey-migration/best-practices-analyzer/assets/BPA_pic1.png)

1. 按一下 **產生報表** 以執行最佳實務分析器。

   ![影像](/help/journey-migration/best-practices-analyzer/assets/BPA_pic2.png)

1. 當BPA產生報表時，您可以在畫面上看到工具所取得的進展。 它會顯示分析的項目數，也會顯示找到的結果數。

   ![影像](/help/journey-migration/best-practices-analyzer/assets/BPA_pic3.png)


1. 生成BPA報告後，它將以表格格式顯示結果的摘要和數目，按結果類型和重要性級別組織。 若要取得特定結果的詳細資訊，您可以按一下與表格中結果類型相對應的數字。

   ![影像](/help/journey-migration/best-practices-analyzer/assets/BPA_pic4.png)

   上述動作會自動捲動至該結果在報表中的位置。

   ![影像](/help/journey-migration/best-practices-analyzer/assets/BPA_pic5.png)

1. 您可以選擇按一下 **匯出至CSV**，如下圖所示。

   ![影像](/help/journey-migration/best-practices-analyzer/assets/BPA_pic6.png)

   >[!NOTE]
您可以按一下，以強制BPA清除其快取並重新產生報表 **重新整理報表**.

   ![影像](/help/journey-migration/best-practices-analyzer/assets/BPA_pic7.png)

   >[!NOTE]
重新產生報表時，會以完成百分比顯示進度，如下圖所示。

   ![影像](/help/journey-migration/best-practices-analyzer/assets/BPA_pic8.png)



#### 在Best Practices Analyzer報表中使用篩選器 {#bpa-filters}

篩選與 [ACS公域](https://adobe-consulting-services.github.io/acs-aem-commons/)，請遵循下列步驟：

1. 按一下頁面左側的左側邊欄圖示。 這會顯示 **ACS公域篩選器**. 按一下 **ACS公域篩選器** 顯示互動式核取方塊，如下圖所示。

   ![影像](/help/journey-migration/best-practices-analyzer/assets/report_filter_1.png)

   >[!NOTE]
只有當BPA偵測到ACS公域的使用時，左側邊欄圖示才會出現。

1. 取消選中該框，以過濾與ACS公域相關的所有結果。 您應會看到 **篩選的結果計數** 如下圖所示。 以逗號分隔值(CSV)格式匯出時，篩選器也會套用至報表。

   ![影像](/help/journey-migration/best-practices-analyzer/assets/report_filter_2.png)

   >[!NOTE]
不應忽視ACS公域的調查結果。 請參閱 [檔案](https://adobe-consulting-services.github.io/acs-aem-commons/pages/compatibility.html#aem-as-a-cloud-service-feature-incompatibility) 以判斷與AEMas a Cloud Service的相容性。


<!--
### Adobe Experience Manager 6.2 and 6.1 {#aem-specific-versions}
 
The Best Practices Analyzer tool is limited in Adobe Experience Manager 6.2 to a link that generates and downloads the CSV report.

For Adobe Experience Manager 6.1, the tool is not functional and only the HTTP interface may be used.

>[!NOTE]
>In all versions, the included Pattern Detector may run independently.
-->

## 解譯Best Practices Analyzer報表 {#cra-report}

[!CONTEXTUALHELP]
id="aemcloud_bpa_interpreting"
title="解譯Best Practices Analyzer報表"
abstract="查看BPA報表輸出有兩個選項：UI和CSV。 在AEM例項中執行Best Practices Analyzer工具時，UI報表會在工具視窗中顯示為結果。 CSV 格式的報表包含從「模式偵測器」輸出產生的資訊，且會依類別類型、子類型和重要性層級排序和組織。"
additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#analysis-report" text="檢閱最佳實務分析報表"
additional-url="https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html?lang=en" text="了解Best Practices Analyzer報表類別"

在AEM例項中執行Best Practices Analyzer工具時，報表會在工具視窗中顯示為結果。

報表格式為：

* **報表概覽**：報表本身的相關資訊，包括下列資訊：
   * **報告時間**：產生報表內容並首次提供的時間。
   * **到期時間**：報表內容快取的到期時間。
   * **產生時段**：報表內容產生程序所花費的時間。
   * **結果計數**：報表中包含的結果總數。
* **系統概述**:運行BPA的AEM系統的相關資訊。
* **結果類別**：分別處理一或多個同類結果的多個區段。每個區段各包含下列項目：類別名稱、子類型、結果計數和重要性、摘要、類別文件的連結，以及個別結果資訊。

系統會為每個結果指派一個重要性層級，以指出動作的概略優先順序。

>[!NOTE]
若要進一步了解每個「結果類別」，請參閱 [模式偵測器類別](https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html).

請參考下表以了解重要性層級：

| 重要性 | 說明 |
|--- |--- |
| 資訊 | 此結果僅供參考。 |
| 建議 | 此結果可能是升級問題。建議進一步調查。 |
| 重要 | 此結果可能是需要解決的升級問題。 |
| 關鍵 | 此結果很可能是升級問題，必須解決以防止失去功能或效能。 |


## 解譯Best Practices Analyzer CSV報表 {#cra-csv-report}

當您按一下 **CSV** 選項，最佳實務分析器報表的CSV格式會從內容快取建置，並傳回至您的瀏覽器。 根據您的瀏覽器設定，此報表將會以檔案格式自動下載，且具有預設名稱 `results.csv`。

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

BPA提供HTTP介面，可作為AEM內使用者介面的替代介面。 該介面同時支援 HEAD 和 GET 命令。它可用於生成BPA報告，並以三種格式之一返回：JSON、CSV和定位點分隔值(TSV)。

下列URL可用於HTTP存取，其中 `<host>` 是安裝了BPA的伺服器的主機名和埠（如果需要）:
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

* `Cache-Control: max-age=<seconds>`:指定快取時效性存留期（以秒為單位）。 (請參閱 [RFC 7234](https://tools.ietf.org/html/rfc7234#section-5.2.2.8)。)
* `Prefer: respond-async`:指定伺服器應以非同步方式回應。 (請參閱 [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.1)。)
* `Prefer: return=minimal`:指定伺服器應返回最小響應。 (請參閱 [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.2)。)

在不方便使用 HTTP 標題時，可權衡使用下列 HTTP 查詢參數：

* `max-age` （數字，選用）:指定快取時效性存留期（以秒為單位）。 此數字必須大於或等於 0。預設的時效性存留期為86400秒。 若沒有此參數或對應的標頭，則會使用新快取在24小時內為請求提供服務，此時必須重新產生快取。 使用 `max-age=0` 將使用新產生快取的先前非零時效性存留期，強制清除快取，並起始重新產生報表的作業。
* `respond-async` （布林值，選用）:指定應以非同步方式提供回應。 使用 `respond-async=true` 快取已過期時，會導致伺服器傳回 `202 Accepted` 而不等待快取重新整理及報表產生。 如果快取為最新狀態，此參數就沒有效用。預設值為 `false`.若沒有此參數或對應的標頭，伺服器將同步回應，這可能需要相當長的時間，且需要調整HTTP用戶端的最大回應時間。
* `may-refresh-cache` （布林值，選用）:指定當前快取為空、過時或很快即將過時時，伺服器可以響應請求刷新快取。 若 `may-refresh-cache=true`，或者，如果未指定，則伺服器可啟動後台任務，該任務將調用模式檢測器並刷新快取。 若 `may-refresh-cache=false` 那麼，如果快取為空或過時，伺服器將不會啟動任何原本會完成的重新整理任務，在這種情況下，報表將為空。 任何已在處理中的刷新任務都不受此參數的影響。
* `return-minimal` （布林值，選用）:指定來自伺服器的回應應僅包含JSON格式中包含進度指示和快取狀態的狀態。 若 `return-minimal=true`，則回應內文將限制為狀態物件。 若 `return-minimal=false`，或若未指定，則會提供完整回應。
* `log-findings` （布林值，選用）:指定伺服器應在首次建立或刷新快取時記錄其內容。 快取中的每個結果都會記錄為JSON字串。 只有在 `log-findings=true` 而請求會產生新的快取。

當 HTTP 標頭和對應的查詢參數均存在時，將會以查詢參數優先。

要透過 HTTP 介面開始產生報表，有個簡單的方式是使用下列命令：
`curl -u admin:admin 'http://localhost:4502/apps/best-practices-analyzer/analysis/report.json?max-age=0&respond-async=true'`。

在提出要求後，用戶端無須維持作用中狀態，即可產生報表。報表產生作業可由一個用戶端使用HTTPGET請求起始，且報表產生後，可從快取與另一個用戶端或AEM使用者介面中的BPA工具檢視。

### 回應 {#http-responses}

可能的回應值如下：

* `200 OK`:指出回應包含「模式偵測器」在快取的時效性存留期內產生的結果。
* `202 Accepted`:用於指示快取已過時。 當 `respond-async=true` 和 `may-refresh-cache=true` 此響應表示正在執行刷新任務。 當 `may-refresh-cache=false` 此回應僅表示快取已過時。
* `400 Bad Request`：表示要求發生錯誤。「問題詳細資訊」格式的消息(請參閱 [RFC 7807](https://tools.ietf.org/html/rfc7807))提供更多詳細資料。
* `401 Unauthorized`:表示請求未獲得授權。
* `500 Internal Server Error`：表示發生了內部伺服器錯誤。「問題詳細資料」格式的訊息可提供更多詳細資料。
* `503 Service Unavailable`：表示伺服器正在處理另一個回應，而無法及時處理此要求。只有在提出同步要求時，才可能發生這種情況。「問題詳細資料」格式的訊息可提供更多詳細資料。

## 管理員資訊

### 快取存留期調整 {#cache-adjustment}

預設的BPA快取存留期為24小時。 在AEM例項和HTTP介面中使用重新整理報表和重新產生快取的選項時，此預設值可能適用於BPA的大部分使用。 如果您 AEM 例項中的報表產生時間特別長，您可以調整快取存留期，以盡快重新產生報表。

快取存留期值會儲存為下列存放庫節點上的 `maxCacheAge` 屬性：
`/apps/best-practices-analyzer/content/BestPracticesReport/jcr:content`

此屬性的值是快取存留期 (以秒為單位)。管理員可以使用 CRX/DE Lite 調整快取存留期。

### 在 AEM 6.1 上安裝 {#installing-on-aem61}

BPA使用名為的系統服務用戶帳戶 `repository-reader-service` 來執行模式偵測器。 此帳戶適用於 AEM 6.2 和更新版本。在AEM 6.1中，必須建立此帳戶 *之前* 安裝BPA，方法如下：

1. 依照[建立新的服務使用者](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-service-users.html#creating-a-new-service-user)中的指示建立使用者。將 UserID 設為 `repository-reader-service`，並將中繼路徑保留為空白，然後按一下綠色核取記號。

2. 依照[管理使用者和群組](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html#managing-users-and-groups)中的指示 (尤其是「將使用者新增至群組」的指示)，將 `repository-reader-service` 使用者新增至 `administrators` 群組。

3. 在您的來源AEM例項上，透過封裝管理器安裝BPA封裝。 (這將會在 `repository-reader-service` 系統服務使用者的 ServiceUserMapper 設定中新增必要的設定修正。)
