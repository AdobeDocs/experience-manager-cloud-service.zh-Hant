---
title: 使用最佳做法分析器
description: 使用最佳做法分析器
exl-id: e8498e17-f55a-4600-87d7-60584d947897
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '2470'
ht-degree: 41%

---

# 使用最佳做法分析器 {#using-best-practices-analyzer}

>[!CONTEXTUALHELP]
>id="aemcloud_bpa_using"
>title="使用最佳做法分析器"
>abstract="查看有關使用最佳做法分析器（以前稱為雲就緒性分析器）的文檔和生成的報告。 「最佳做法分析器報告」用於從較高層次瞭解一般升級就緒性。"
>additional-url=""

## 使用最佳做法分析器的重要注意事項 {#imp-considerations}

請按照以下部分瞭解運行最佳做法分析器(BPA)的重要注意事項：

* BPA報告是使用Adobe Experience Manager(AEM)的輸出 [圖案檢測器](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/pattern-detector.html)。 BPA使用的圖案檢測器版本包含在BPA安裝包中。

* BPA只能由 **管理員** 用戶或用戶 **管理員** 組。

* 6.1及更高版AEM本的實例支援BPA。

   >[!NOTE]
請參閱 [在AEM6.1上安裝](#installing-on-aem61) 在6.1上安裝BPA的AEM特殊要求。

* BPA可以在任何環境上運行，但最好在 *舞台* 環境。

   >[!NOTE]
為避免對業務關鍵型實例產生影響，建議在 *作者* 最接近的環境 *生產* 在自定義、配置、內容和用戶應用程式等方面。 或者，您可以在複製的生產&#x200B;*製作*&#x200B;環境中執行 CRA。

* 生成BPA報告內容可能需要相當長的時間，從幾分鐘到幾小時不等。 所需的時間主要取決於 AEM 存放庫內容的大小和性質、AEM 版本和其他因素。

* 由於產生報表內容可能需要相當長的時間，因此這些內容會由背景程序產生，並儲存在快取中。檢視和下載報表的速度則相對迅速，因為此時會使用內容快取，直到快取過期或報表明確重新整理為止。在產生報表內容期間，您可以先關閉瀏覽器索引標籤，等稍後內容已存放於快取時，再回過頭檢視報表。

## 可用性 {#availability}

[!CONTEXTUALHELP]
id="aemcloud_bpa_download"
title="下載最佳做法分析器"
abstract="最佳做法分析器可以作為zip檔案從軟體分發門戶下載。 您可以透過「封裝管理程式」，在來源 Adobe Experience Manager AEM) 例項上安裝封裝。"

最佳做法分析器可以作為zip檔案從軟體分發門戶下載。 您可以通過 [包管理器](/help/implementing/developing/tools/package-manager.md) 源Adobe Experience Manager(AEM)實例。

>[!NOTE]
從 [軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) 門戶。

## 查看最佳做法分析器報告 {#viewing-report}

### Adobe Experience Manager 6.3.0 和更新版本 {#aem-later-versions}

按照本節介紹如何查看最佳做法分析器報告：

1. 選擇Adobe Experience Manager並導航至工具 — > **操作** -> **最佳做法分析器**。

   ![影像](/help/journey-migration/best-practices-analyzer/assets/BPA_pic1.png)

1. 按一下 **生成報告** 執行最佳做法分析器。

   ![影像](/help/journey-migration/best-practices-analyzer/assets/BPA_pic2.png)

1. 當BPA正在生成報告時，您可以在螢幕上看到工具所取得的進展。 它顯示分析的項數，並顯示找到的查找結果數。

   ![影像](/help/journey-migration/best-practices-analyzer/assets/BPA_pic3.png)


1. 生成BPA報告後，它將以表格格式顯示摘要和查找結果的數量，按查找結果類型和重要性級別進行組織。 要獲取有關特定查找結果的更多詳細資訊，可以按一下表中與查找結果類型對應的編號。

   ![影像](/help/journey-migration/best-practices-analyzer/assets/BPA_pic4.png)

   上述操作將自動滾動到報告中該查找結果的位置。

   ![影像](/help/journey-migration/best-practices-analyzer/assets/BPA_pic5.png)

1. 您可以選擇通過按一下 **導出為CSV**，如下圖所示。

   ![影像](/help/journey-migration/best-practices-analyzer/assets/BPA_pic6.png)

   >[!NOTE]
您可以通過按一下來強制BPA清除其快取並重新生成報告 **刷新報告**。

   ![影像](/help/journey-migration/best-practices-analyzer/assets/BPA_pic7.png)

   >[!NOTE]
在重新生成報告時，它按完成百分比顯示進度，如下圖所示。

   ![影像](/help/journey-migration/best-practices-analyzer/assets/BPA_pic8.png)



#### 在最佳做法分析器報告中使用篩選器 {#bpa-filters}

篩選與 [ACS公域](https://adobe-consulting-services.github.io/acs-aem-commons/)，請執行以下步驟：

1. 按一下頁面左側的左滑軌表徵圖。 這將顯示 **ACS公域篩選器**。 按一下 **ACS公域篩選器** 顯示互動式複選框，如下圖所示。

   ![影像](/help/journey-migration/best-practices-analyzer/assets/report_filter_1.png)

   >[!NOTE]
僅當BPA檢測到ACS共用的使用時，左滑軌表徵圖才會出現。

1. 取消選中該框以篩選與ACS共用相關的所有查找結果。 你應該看到 **篩選的查找結果計數** 如下圖所示。 當以逗號分隔值(CSV)格式導出時，該篩選器也會應用於報表。

   ![影像](/help/journey-migration/best-practices-analyzer/assets/report_filter_2.png)

   >[!NOTE]
不應忽視ACS公域調查結果。 請參閱 [文檔](https://adobe-consulting-services.github.io/acs-aem-commons/pages/compatibility.html#aem-as-a-cloud-service-feature-incompatibility) 確定與AEMas a Cloud Service的相容性。


<!--
### Adobe Experience Manager 6.2 and 6.1 {#aem-specific-versions}
 
The Best Practices Analyzer tool is limited in Adobe Experience Manager 6.2 to a link that generates and downloads the CSV report.

For Adobe Experience Manager 6.1, the tool is not functional and only the HTTP interface may be used.

>[!NOTE]
>In all versions, the included Pattern Detector may run independently.
-->

## 解釋最佳做法分析器報告 {#cra-report}

[!CONTEXTUALHELP]
id="aemcloud_bpa_interpreting"
title="解釋最佳做法分析器報告"
abstract="查看BPA報告輸出有兩個選項：UI和CSV。 在實例中運行最佳做法分析器工AEM具時，UI報告將作為結果顯示在工具窗口中。 CSV 格式的報表包含從「模式偵測器」輸出產生的資訊，且會依類別類型、子類型和重要性層級排序和組織。"
additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#analysis-report" text="複查最佳做法分析報告"
additional-url="https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html?lang=en" text="瞭解最佳做法分析器報告類別"

在實例中運行最佳做法分析器工AEM具時，報告將作為結果顯示在工具窗口中。

報表格式為：

* **報表概覽**：報表本身的相關資訊，包括下列資訊：
   * **報告時間**：產生報表內容並首次提供的時間。
   * **到期時間**：報表內容快取的到期時間。
   * **產生時段**：報表內容產生程序所花費的時間。
   * **結果計數**：報表中包含的結果總數。
* **系統概述**:有關運行AEMBPA的系統的資訊。
* **結果類別**：分別處理一或多個同類結果的多個區段。每個區段各包含下列項目：類別名稱、子類型、結果計數和重要性、摘要、類別文件的連結，以及個別結果資訊。

系統會為每個結果指派一個重要性層級，以指出動作的概略優先順序。

>[!NOTE]
要瞭解有關每個查找類別的詳細資訊，請參閱 [圖案檢測器類別](https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html)。

請參考下表以了解重要性層級：

| 重要性 | 說明 |
|--- |--- |
| 資訊 | 此結果僅供參考。 |
| 建議 | 此結果可能是升級問題。建議進一步調查。 |
| 重要 | 此結果可能是需要解決的升級問題。 |
| 關鍵 | 此結果很可能是升級問題，必須解決以防止失去功能或效能。 |


## 解釋最佳做法分析器CSV報告 {#cra-csv-report}

按一下 **CSV** 選項，AEM「最佳做法分析器」報告的CSV格式將從內容快取中生成並返回到瀏覽器。 根據您的瀏覽器設定，此報表將會以檔案格式自動下載，且具有預設名稱 `results.csv`。

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

BPA提供HTTP介面，可用作HTTP介面內用戶介面的替AEM代。 該介面同時支援 HEAD 和 GET 命令。它可用於生成BPA報告並以三種格式之一返回：JSON、CSV和制表符分隔值(TSV)。

以下URL可用於HTTP訪問，其中 `<host>` 是安裝BPA的伺服器的主機名和埠（如果需要）:
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

* `Cache-Control: max-age=<seconds>`:以秒為單位指定快取新鮮度生存期。 (請參閱 [RFC 7234](https://tools.ietf.org/html/rfc7234#section-5.2.2.8)。)
* `Prefer: respond-async`:指定伺服器應非同步響應。 (請參閱 [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.1)。)
* `Prefer: return=minimal`:指定伺服器應返回最小響應。 (請參閱 [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.2)。)

在不方便使用 HTTP 標題時，可權衡使用下列 HTTP 查詢參數：

* `max-age` （數字，可選）:以秒為單位指定快取新鮮度生存期。 此數字必須大於或等於 0。預設新鮮度生存期為86400秒。 如果沒有此參數或相應的標頭，則將使用新快取為請求提供24小時服務，此時必須重新生成快取。 使用 `max-age=0` 將使用新生成的快取先前的非零新鮮壽命來強制清除快取並啟動報告的再生。
* `respond-async` （布爾型，可選）:指定應非同步提供響應。 使用 `respond-async=true` 當快取失效時，伺服器將返回 `202 Accepted` 而不等待刷新快取和生成報告。 如果快取為最新狀態，此參數就沒有效用。預設值為 `false`。如果沒有此參數或相應的報頭，伺服器將同步響應，這可能需要相當長的時間並且需要對HTTP客戶端的最大響應時間進行調整。
* `may-refresh-cache` （布爾型，可選）:指定當前快取為空、過時或很快過時時，伺服器可以響應請求刷新快取。 如果 `may-refresh-cache=true`，或如果未指定，則伺服器可啟動後台任務，該任務將調用模式檢測器並刷新快取。 如果 `may-refresh-cache=false` 那麼，如果快取為空或過時，伺服器將不啟動任何本應執行的刷新任務，在這種情況下，報告將為空。 任何已在執行的刷新任務都不會受此參數的影響。
* `return-minimal` （布爾型，可選）:指定來自伺服器的響應應僅包括JSON格式中包含進度指示和快取狀態的狀態。 如果 `return-minimal=true`，則響應體將限於狀態對象。 如果 `return-minimal=false`，或未指定時，將提供完整的響應。
* `log-findings` （布爾型，可選）:指定伺服器應在首次生成或刷新快取時記錄其內容。 快取中的每個查找結果都將記錄為JSON字串。 僅當 `log-findings=true` 並且該請求生成新快取。

當 HTTP 標頭和對應的查詢參數均存在時，將會以查詢參數優先。

要透過 HTTP 介面開始產生報表，有個簡單的方式是使用下列命令：
`curl -u admin:admin 'http://localhost:4502/apps/best-practices-analyzer/analysis/report.json?max-age=0&respond-async=true'`。

在提出要求後，用戶端無須維持作用中狀態，即可產生報表。可以使用HTTPGET請求在一個客戶端上啟動報告生成，一旦生成報告，就可以使用另一個客戶端或用戶介面中的BPA工具從快取中查看AEM報告生成。

### 回應 {#http-responses}

可能的回應值如下：

* `200 OK`:指示響應包含來自模式檢測器的發現，這些發現在快取的新鮮度生命週期內生成。
* `202 Accepted`:用於指示快取過時。 當 `respond-async=true` 和 `may-refresh-cache=true` 此響應表示正在執行刷新任務。 當 `may-refresh-cache=false` 此響應僅表示快取已過時。
* `400 Bad Request`：表示要求發生錯誤。「問題詳細資訊」格式的消息(請參閱 [RFC 7807](https://tools.ietf.org/html/rfc7807))提供詳細資訊。
* `401 Unauthorized`:指示請求未授權。
* `500 Internal Server Error`：表示發生了內部伺服器錯誤。「問題詳細資料」格式的訊息可提供更多詳細資料。
* `503 Service Unavailable`：表示伺服器正在處理另一個回應，而無法及時處理此要求。只有在提出同步要求時，才可能發生這種情況。「問題詳細資料」格式的訊息可提供更多詳細資料。

## 管理員資訊

### 快取存留期調整 {#cache-adjustment}

預設BPA快取生存期為24小時。 在實例和HTTP介面中，使用AEM刷新報告和重新生成快取的選項，此預設值可能適用於BPA的大多數使用。 如果您 AEM 例項中的報表產生時間特別長，您可以調整快取存留期，以盡快重新產生報表。

快取存留期值會儲存為下列存放庫節點上的 `maxCacheAge` 屬性：
`/apps/best-practices-analyzer/content/BestPracticesReport/jcr:content`

此屬性的值是快取存留期 (以秒為單位)。管理員可以使用 CRX/DE Lite 調整快取存留期。

### 在 AEM 6.1 上安裝 {#installing-on-aem61}

BPA使用名為的系統服務用戶帳戶 `repository-reader-service` 執行模式檢測器。 此帳戶適用於 AEM 6.2 和更新版本。在AEM6.1上，必須建立此帳戶 *之前* 安裝BPA，步驟如下：

1. 依照[建立新的服務使用者](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-service-users.html#creating-a-new-service-user)中的指示建立使用者。將 UserID 設為 `repository-reader-service`，並將中繼路徑保留為空白，然後按一下綠色核取記號。

2. 依照[管理使用者和群組](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html#managing-users-and-groups)中的指示 (尤其是「將使用者新增至群組」的指示)，將 `repository-reader-service` 使用者新增至 `administrators` 群組。

3. 通過包管理器在源實例上安裝BPAAEM包。 (這將會在 `repository-reader-service` 系統服務使用者的 ServiceUserMapper 設定中新增必要的設定修正。)
