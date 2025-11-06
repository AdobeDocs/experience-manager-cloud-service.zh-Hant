---
title: 使用最佳做法分析工具
description: 瞭解如何使用Best Practices Analyzer以瞭解升級整備程度。
exl-id: e8498e17-f55a-4600-87d7-60584d947897
feature: Migration
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2796'
ht-degree: 37%

---

# 使用最佳做法分析工具 {#using-best-practices-analyzer}

>[!CONTEXTUALHELP]
>id="aemcloud_bpa_using"
>title="使用此最佳做法分析工具"
>abstract="檢閱使用最佳做法分析工具 (以前稱為雲端整備程度分析工具) 的文件和產生的報表。最佳做法分析工具報表可用於取得對一般升級整備程度的概略了解。"
>additional-url="https://my.adobeconnect.com/pqgrfezoxghs?proto=true" text="[網絡研討會] 推出加速 Adobe Experience Manager as a Cloud Service 歷程的工具"

## 使用Best Practices Analyzer的重要考量 {#imp-considerations}

請參考以下章節，瞭解執行Best Practices Analyzer (BPA)時的重要考量：

* BPA報告是使用Adobe Experience Manager (AEM) [模式偵測器](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/pattern-detector.html)的輸出所建置。 BPA使用的模式偵測器版本包含在BPA安裝封裝中。

* BPA只能由&#x200B;**管理員**&#x200B;使用者或&#x200B;**管理員**&#x200B;群組中的使用者執行。

* 6.1版及更高版本的AEM執行個體支援BPA。

  >[!NOTE]
  >如需在AEM 6.1上安裝BPA的特殊需求，請參閱[在AEM 6.1上安裝](#installing-on-aem61)。

* BPA可以在任何環境中執行，但最好在&#x200B;*階段*&#x200B;環境中執行。

  >[!NOTE]
  >為避免對業務關鍵執行個體造成影響，建議您在儘可能接近&#x200B;*生產*&#x200B;環境的&#x200B;*階段*&#x200B;環境中，在自訂、設定、內容和使用者應用程式等方面執行BPA。 或者，您可以在複製的生產&#x200B;*製作*&#x200B;環境中執行 CRA。

* 產生BPA報告內容可能需要相當長的時間，從幾分鐘到幾小時不等。 所需的時間主要取決於 AEM 存放庫內容的大小和性質、AEM 版本和其他因素。

* 由於產生報表內容可能需要相當長的時間，因此這些內容會由背景程序產生，並儲存在快取中。檢視和下載報表的速度則相對迅速，因為此時會使用內容快取，直到快取過期或報表明確重新整理為止。在產生報表內容期間，您可以先關閉瀏覽器索引標籤，等稍後內容已存放於快取時，再回過頭檢視報表。

## 可用性 {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_bpa_download"
>title="下載最佳做法分析工具"
>abstract="您可以從軟體發佈入口網站下載最佳做法分析工具的 ZIP 檔案。您可以透過「封裝管理程式」，在來源 Adobe Experience Manager AEM) 例項上安裝封裝。"

您可以從軟體發佈入口網站下載最佳做法分析工具的 ZIP 檔案。您可以在來源Adobe Experience Manager (AEM)執行個體上透過[封裝管理員](/help/implementing/developing/tools/package-manager.md)安裝封裝。

>[!NOTE]
>從[軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)入口網站下載最佳做法分析程式。

## Source環境連線 {#source-environment-connectivity}

來源AEM執行個體可能正在防火牆後面執行，而它只能連線至已新增至允許清單的特定主機。 若要將BPA產生的報告自動上傳至Cloud Acceleration Manager，下列端點必須可從執行AEM的執行個體存取：

* Azure Blob儲存服務： `casstorageprod.blob.core.windows.net`


## 檢視Best Practices Analyzer報表 {#viewing-report}

### Adobe Experience Manager 6.3.0 和以上 {#aem-later-versions}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_bpa_upload_setup"
>title="自動將最佳做法分析工具報告上傳至 CAM"
>abstract="提供 BPA 上傳金鑰，將所產生的 BPA 報告自動上傳到 Cloud Acceleration Manager (CAM)。"

請詳閱本節，瞭解如何檢視Best Practices Analyzer報告：

1. 選取Adobe Experience Manager並導覽至工具> **作業** > **最佳做法分析工具**。

   ![最佳做法分析工具](/help/journey-migration/best-practices-analyzer/assets/BPA_pic1.png)

1. 按一下&#x200B;**產生報告**&#x200B;以執行Best Practices Analyzer。

   ![產生報表](/help/journey-migration/best-practices-analyzer/assets/BPA_pic2.png)

>[!NOTE]
> 從BPA 2.1.54版開始，已引入新功能以取得Lighthouse分數。


1. 按一下&#x200B;**產生報表**&#x200B;後，會出現快顯視窗，要求AEM公用網站URL提供Lighthouse分數。 使用者必須在提供的欄位中輸入有效的URL。

   ![影像](/help/journey-migration/best-practices-analyzer/assets/bpa_popup_url.png)

   1. 如果URL有效，則會顯示成功訊息。

      ![影像](/help/journey-migration/best-practices-analyzer/assets/valid_url.png)

   1. 如果URL無效，便會顯示錯誤訊息。

      ![影像](/help/journey-migration/best-practices-analyzer/assets/invalid_url.png)

1. 提供BPA上傳金鑰以將產生的BPA報告自動上傳至[Cloud Acceleration Manager (CAM)](/help/journey-migration/cloud-acceleration-manager/introduction/benefits-cam.md)。 若要取得上傳金鑰，請瀏覽至[CAM中的最佳實務分析](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#best-practices-analysis)

   ![設定BPA上傳金鑰](/help/journey-migration/best-practices-analyzer/assets/BPA_upload_key.png)

>[!NOTE]
>您可選擇略過自動上傳至CAM，方法是選取&#x200B;**略過報告自動上傳至CAM**。 如果您選擇略過，則需要以逗號分隔的值檔案手動下載BPA報表，然後以CAM上傳該檔案。 建議您使用上傳金鑰選項，因為這可簡化作業。

>[!IMPORTANT]
>手動上傳至CAM時，報表大小限製為約200MB。 如需大型報告，您必須運用自動上傳。

1. 提供有效金鑰時，**產生**&#x200B;按鈕會變成使用中。 按一下&#x200B;**產生**&#x200B;以開始產生報表。

   ![產生報表](/help/journey-migration/best-practices-analyzer/assets/BPA_upload_key1.png)

1. 在BPA產生報表時，您可以在畫面上看到工具執行的進度。 它以完成百分比顯示進度。 它也會顯示已分析的專案數，也會顯示找到的結果數。

   ![正在產生報告](/help/journey-migration/best-practices-analyzer/assets/BPA_generate_upload.png)

>[!NOTE]
>BPA上傳金鑰到期時間戳記會顯示在右上角。 您應該在BPA上傳金鑰接近到期時進行更新。 若要更新金鑰，您可以按一下&#x200B;**更新**，瀏覽至CAM以更新金鑰。

1. 產生BPA報告後，會以表格格式顯示結果的摘要和數目，並依據結果型別和重要性層級加以整理。 若要取得特定發現專案的詳細資訊，您可以按一下與表格中的發現專案型別相對應的數字。

   ![報告總覽](/help/journey-migration/best-practices-analyzer/assets/BPA_report_upload.png)

1. 您可以按一下&#x200B;**匯出至CSV**，選擇下載逗號分隔值(CSV)格式的報表。 您也可以按一下&#x200B;**移至CAM**，選擇在CAM中檢視報表。 這會帶您進入CAM中的[最佳實務分析](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#best-practices-analysis)頁面。

您可以按一下&#x200B;**重新整理報告**，以強制BPA清除其快取並重新產生報告。

![重新整理報告](/help/journey-migration/best-practices-analyzer/assets/BPA_report_upload.png)

1. 如果快取過期，您可以選擇在CAM中檢視上次產生的報告，方法是按一下&#x200B;**在CAM中檢視上次產生的報告**，或按一下&#x200B;**產生新報告**&#x200B;來啟動新的報告產生作業。

![沒有報告](/help/journey-migration/best-practices-analyzer/assets/BPA_regeneratereport.png)


#### 在Best Practices Analyzer報告中使用篩選器 {#bpa-filters}

若要篩選出與[ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/)相關的發現，請遵循下列步驟：

1. 按一下頁面左側的左側欄圖示。 這會顯示&#x200B;**ACS Commons篩選器**。 按一下&#x200B;**ACS Commons Filter**&#x200B;以顯示互動式核取方塊，如下圖所示。

   ![ACS Commons篩選器](/help/journey-migration/best-practices-analyzer/assets/report_filter_1.png)

   >[!NOTE]
   >只有在BPA偵測到ACS Commons的使用時，左側邊欄圖示才會出現。

1. 取消選取此方塊，以篩選掉與ACS Commons相關的所有發現。 您應該會在報表上看到&#x200B;**篩選的發現專案計數**，如下圖所示。 當篩選器匯出為逗號分隔值(CSV)格式時，也會套用至報表。

   ![篩選結果計數](/help/journey-migration/best-practices-analyzer/assets/report_filter_2.png)

   >[!NOTE]
   >不應忽略ACS Commons的發現。 請參閱[檔案](https://adobe-consulting-services.github.io/acs-aem-commons/pages/compatibility.html#aem-as-a-cloud-service-feature-incompatibility)以判斷與AEM as a Cloud Service的相容性。

<!--
### Adobe Experience Manager 6.2 and 6.1 {#aem-specific-versions}
 
The Best Practices Analyzer tool is limited in Adobe Experience Manager 6.2 to a link that generates and downloads the CSV report.

For Adobe Experience Manager 6.1, the tool is not functional and only the HTTP interface may be used.

>[!NOTE]
>In all versions, the included Pattern Detector may run independently.
-->

## 最佳做法分析工具報告解讀 {#cra-report}

>[!CONTEXTUALHELP]
>id="aemcloud_bpa_interpreting"
>title="最佳做法分析工具報告解讀"
>abstract="檢視 BPA 報表輸出有兩種選項：UI 和 CSV。在 AEM 執行個體中執行最佳做法分析工具時，UI 報表會在工具視窗中顯示為結果。CSV 格式的報表包含從「模式偵測器」輸出產生的資訊，且會依類別類型、子類型和重要性層級排序和編排。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html#analysis-report" text="檢閱最佳做法分析報表"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html" text="了解最佳做法分析工具報表類別"

在AEM例項中執行Best Practices Analyzer工具時，報表會在工具視窗中顯示為結果。

報表格式為：

* **報表概觀**：報表本身的相關資訊，包括下列資訊：
   * **報告時間**：產生報表內容並首次提供的時間。
   * **過期時間**：報表內容快取的過期時間。
   * **產生時段**：報表內容產生程序所花費的時間。
   * **結果計數**：報表中包含的結果總數。
* **系統概覽**：執行BPA之AEM系統的相關資訊。
* **結果類別**：分別處理一或多個同類結果的多個區段。每個區段各包含下列項目：類別名稱、子類型、結果計數和重要性、摘要、類別文件的連結，以及個別結果資訊。

系統會為每個結果指派一個重要性層級，以指出動作的概略優先順序。

>[!NOTE]
>若要深入瞭解每個發現專案類別，請參閱[模式偵測器類別](https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html)。

請參考下表以了解重要性層級：

| 重要性 | 說明 |
|--- |--- |
| 資訊 | 此結果僅供參考。 |
| 建議 | 此結果可能是升級問題。建議進一步調查。 |
| 重要 | 此結果可能是需要解決的升級問題。 |
| 關鍵 | 此結果很可能是升級問題，必須解決以防止失去功能或效能。 |

## 解譯Best Practices Analyzer CSV報表 {#cra-csv-report}

當您按一下AEM執行個體中的&#x200B;**CSV**&#x200B;選項時，將會從內容快取建置CSV格式的Best Practices Analyzer報告並傳回至您的瀏覽器。 根據您的瀏覽器設定，此報表會自動下載為預設名稱為`results.csv`的檔案。

如果快取已過期，則會在CSV檔案建置和下載之前重新產生報表。

CSV 格式的報表包含從「模式偵測器」輸出產生的資訊，且會依類別類型、子類型和重要性層級排序和組織。其格式適用於 Microsoft Excel 等應用程式的檢視和編輯作業。其目的是要以可重複的格式提供所有結果資訊，以利比較不同時間的報表，藉此衡量進度。

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

## HTTP介面 {#http-interface}

BPA提供HTTP介面，可作為AEM使用者介面的替代介面。 該介面同時支援 HEAD 和 GET 命令。它可用來產生BPA報表，並以三種格式之一傳回：JSON、CSV和定位鍵分隔值(TSV)。

下列URL可用於HTTP存取，其中`<host>`是安裝BPA之伺服器的主機名稱和連線埠（如有需要）：

* `http://<host>/apps/best-practices-analyzer/analysis/report.json` (JSON 格式)
* `http://<host>/apps/best-practices-analyzer/analysis/report.csv` (CSV 格式)
* `http://<host>/apps/best-practices-analyzer/analysis/report.tsv` (TSV 格式)

### 執行HTTP要求 {#executing-http-request}

HTTP 介面可用於多種方法中。

其中一個簡單的方式，是在您已用管理員身分登入 AEM 的相同瀏覽器中開啟瀏覽器索引標籤。您可以在瀏覽器索引標籤中輸入 URL，並且讓瀏覽器顯示或下載結果。

您也可以使用命令列工具，例如`curl`或`wget`，以及任何HTTP使用者端應用程式。 未在已驗證的工作階段中使用瀏覽器索引標籤時，您必須在註解中提供管理使用者名稱和密碼。

以下是其操作方式的範例：
`curl -u admin:admin 'http://localhost:4502/apps/best-practices-analyzer/analysis/report.csv' > report.csv`。

### 標題和引數 {#http-headers-and-parameters}

此介面使用下列 HTTP 標題：

* `Cache-Control: max-age=<seconds>`：指定快取時效性存留期（秒）。 (請參閱 [RFC 7234](https://tools.ietf.org/html/rfc7234#section-5.2.2.8)。)
* `Prefer: respond-async`：指定伺服器應以非同步方式回應。 (請參閱 [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.1)。)
* `Prefer: return=minimal`：指定伺服器應傳回最低的回應。 (請參閱 [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.2)。)

在不方便使用 HTTP 標題時，可權衡使用下列 HTTP 查詢參數：

* `max-age` （數字，選用）：指定快取時效性存留期（以秒為單位）。 此數字必須大於或等於 0。預設的時效性存留期為86400秒。 如果沒有此引數或對應的標頭，新的快取將會在24小時內用來處理請求，屆時必須重新產生快取。 使用`max-age=0`會強制清除快取，並使用新產生的快取先前的非零新鮮度存留期來開始重新產生報表。
* `respond-async` （布林值，選用）：指定應以非同步方式提供回應。 在快取已過期時使用`respond-async=true`將導致伺服器傳回`202 Accepted`的回應，而不等待快取重新整理及產生報告。 如果快取為最新狀態，此參數就沒有效用。預設值為`false`。 若沒有此引數或對應標頭，伺服器將會同步回應，而這可能需要相當長的時間，且需要調整HTTP使用者端的最大回應時間。
* `may-refresh-cache` （布林值，選用）：指定如果目前的快取是空的、過時或即將過時，伺服器可以重新整理快取來回應要求。 如果`may-refresh-cache=true`或未指定，則伺服器可能會起始背景工作，以叫用模式偵測器並重新整理快取。 如果`may-refresh-cache=false`，則伺服器不會起始任何重新整理工作，否則如果快取為空白或過時（報表為空白）該工作會完成。 任何已在處理的重新整理任務都不會受此引數影響。
* `return-minimal` （布林值，選用）：指定伺服器的回應應僅包含進度指示的狀態，以及JSON格式的快取狀態。 如果`return-minimal=true`，則回應本文僅限於狀態物件。 如果`return-minimal=false`或未指定，則會提供完整的回應。
* `log-findings` （布林值，選擇性）：指定伺服器應該在第一次建置或重新整理快取時，記錄快取的內容。 快取中的每個結果都會記錄為JSON字串。 只有在`log-findings=true`且請求產生新快取時，才會進行此記錄。

當 HTTP 標頭和對應的查詢參數均存在時，將會以查詢參數優先。

要透過 HTTP 介面開始產生報表，有個簡單的方式是使用下列命令：
`curl -u admin:admin 'http://localhost:4502/apps/best-practices-analyzer/analysis/report.json?max-age=0&respond-async=true'`。

在提出要求後，用戶端無須維持作用中狀態，即可產生報表。報表產生作業可以由一個使用者端使用HTTP GET要求來起始，且報表產生後，可由另一個使用者端從快取中檢視，或透過AEM使用者介面中的BPA工具檢視。

### 回應 {#http-responses}

可能的回應值如下：

* `200 OK`：指出回應包含模式偵測器在快取的時效性存留期內產生的發現。
* `202 Accepted`：用於表示快取已過時。 當`respond-async=true`和`may-refresh-cache=true`此回應表示重新整理任務正在進行時。 當`may-refresh-cache=false`時，此回應僅表示快取已過時。
* `400 Bad Request`：表示要求發生錯誤。「問題詳細資料」格式的訊息（請參閱[RFC 7807](https://tools.ietf.org/html/rfc7807)）可提供更多詳細資料。
* `401 Unauthorized`：指出未授權要求。
* `500 Internal Server Error`：表示發生了內部伺服器錯誤。「問題詳細資料」格式的訊息可提供更多詳細資料。
* `503 Service Unavailable`：表示伺服器正在處理另一個回應，而無法及時處理此要求。只有在提出同步要求時，才可能發生這種情況。「問題詳細資料」格式的訊息可提供更多詳細資料。

## 管理員資訊

### 快取存留期調整 {#cache-adjustment}

預設的BPA快取存留期為24小時。 在AEM例項和HTTP介面中使用重新整理報告及重新產生快取的選項時，此預設值可能適用於大多數BPA使用。 如果您AEM例項的報表產生時間特別長，您可以調整快取存留期以最小化報表的重新產生。

快取存留期值會儲存為下列存放庫節點上的 `maxCacheAge` 屬性：
`/apps/best-practices-analyzer/content/BestPracticesReport/jcr:content`

此屬性的值是快取存留期 (以秒為單位)。管理員可以使用 CRX/DE Lite 調整快取存留期。

### 在AEM 6.1上安裝 {#installing-on-aem61}

BPA使用名為`repository-reader-service`的系統服務使用者帳戶來執行模式偵測器。 此帳戶適用於 AEM 6.2 和更新版本。在AEM 6.1上，您必須執行下列步驟，在安裝BPA *之前*&#x200B;建立此帳戶：

1. 依照[建立新的服務使用者](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-service-users.html#creating-a-new-service-user)中的指示建立使用者。將 UserID 設為 `repository-reader-service`，並將中繼路徑保留為空白，然後按一下綠色核取記號。

2. 依照[管理使用者和群組](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html#managing-users-and-groups)中的指示 (尤其是「將使用者新增至群組」的指示)，將 `repository-reader-service` 使用者新增至 `administrators` 群組。

3. 透過封裝管理程式，在您的來源AEM執行個體上安裝BPA套件。 (這將會在 `repository-reader-service` 系統服務使用者的 ServiceUserMapper 設定中新增必要的設定修正。)
