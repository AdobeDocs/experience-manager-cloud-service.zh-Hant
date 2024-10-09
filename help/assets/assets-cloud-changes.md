---
title: ' [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service]中的重大變更'
description: 與 [!DNL Adobe Experience Manager] 6.5相比，對 [!DNL Experience Manager] 中的 [!DNL Adobe Experience Manager Assets] 做為 [!DNL Cloud Service] 的重大變更。
feature: Release Information
role: User, Leader, Architect, Admin
exl-id: 93e7dbcd-016e-4ef2-a1cd-c554efb5ad34
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 9%

---

# [!DNL Experience Manager Assets]的重大變更為[!DNL Cloud Service] {#notable-changes}

| [搜尋最佳實務](/help/assets/search-best-practices.md) | [中繼資料最佳實務](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [具有OpenAPI功能的Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets開發人員檔案](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service]提供許多管理您的Experience Manager專案的新功能，並帶來許多可能性。 [!DNL Experience Manager Assets]內部部署或作為Adobe受管理服務裝載與作為[!DNL Cloud Service]裝載的[!DNL Experience Manager]之間有許多差異。 本文強調[!DNL Assets]功能的重要差異。

與[!DNL Experience Manager] 6.5的主要差異如下：

* [資產擷取、上傳和處理](#asset-ingestion)。
* [用於雲端原生處理的資產微服務](#asset-microservices)。
* [移除傳統UI](#classic-ui)。

## 資產擷取、處理和分發 {#asset-ingestion-distribution}

資產上傳透過實現更好的內嵌縮放、更快的上傳、使用微服務的更快處理和大量內嵌，以最佳化效率。 產品功能（網頁使用者介面、案頭使用者端）已更新。 此外，這可能會影響部分現有的自訂。

* [!DNL Experience Manager]使用直接二進位存取原則來上傳和下載資產，並使用資產微服務來處理資產。 請參閱[微服務概述](/help/assets/asset-microservices-overview.md)。
   * 透過直接二進位存取資產上傳[](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access)。
   * 如需技術詳細資訊，請參閱[直接二進位上傳通訊協定與API](/help/assets/developer-reference-material-apis.md#upload-binary)。
   * 若要比較基本CRUD作業的可用API方法，請參閱[API和資產作業](/help/assets/developer-reference-material-apis.md#use-cases-and-apis)。
* 舊版[!DNL Experience Manager]中的預設工作流程&#x200B;**[!UICONTROL DAM Asset Update]**&#x200B;已無法使用。 相反，資產微服務提供可擴充、隨時可用的服務，涵蓋大部分的預設資產處理（轉譯、中繼資料擷取和索引文字擷取）。
   * 請參閱[設定及使用資產微服務](/help/assets/asset-microservices-configure-and-use.md)
   * 若要在處理中有自訂的工作流程步驟，可使用[後處理工作流程](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)。

* 在不進行任何轉換的情況下傳送二進位檔案的網站元件可使用直接下載。 SlingGETServlet已更新，開發人員可依預設執行此動作。 在轉換後傳送二進位的網站元件（例如透過servlet調整大小）仍可繼續運作。

透過資產微服務產生的標準轉譯會使用相同的命名慣例，以向後相容的方式儲存在資產存放庫節點中。

## 開發和測試資產微服務 {#asset-microservices}

資產微服務使用雲端服務來提供可擴展和具恢復力的資產處理操作。Adobe 管理雲端服務以對不同的資產類型和處理選項進行最佳處理。資產微服務可協助您避免使用協力廠商的轉譯工具和方法（例如[!DNL ImageMagick]），並簡化設定，同時為一般檔案型別提供現成可用的功能。 您現在可以處理[多種檔案型別](/help/assets/file-format-support.md)，涵蓋比舊版Experience Manager更多的現成格式。 例如，PSD和PSB格式的縮圖擷取現在可能是先前需要的協力廠商解決方案，例如[!DNL ImageMagick]。 您無法對[!UICONTROL 處理設定檔]設定使用[!DNL ImageMagick]的複雜設定。 使用[!DNL Dynamic Media]進行視訊的進階FFmpeg轉碼，並使用處理設定檔進行[MP4視訊的基本轉碼](/help/assets/manage-video-assets.md#transcode-video)。

資產微服務是雲端原生服務，會在Cloud Manager中管理的客戶程式和環境中，自動布建並連線至[!DNL Experience Manager]。 若要擴充或自訂[!DNL Experience Manager]，開發人員可以使用現有內容或資產以及在雲端環境中產生的轉譯，以使用、顯示、下載資產來測試及驗證其程式碼。

若要執行端對端驗證程式碼和程式（包括資產擷取和處理），請使用[管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)將程式碼變更部署到雲端開發環境，並測試以完全執行資產微服務處理。

## 與[!DNL Experience Manager]的功能同位6.5 {#cloud-service-feature-status}

[!DNL Experience Manager] as a [!DNL Cloud Service]引進許多新功能以及更高效能的方式來讓現有功能運作。 但是，當以[!DNL Cloud Service]從[!DNL Experience Manager] 6.5移至[!DNL Experience Manager]時，您可能會注意到某些功能的運作方式不同、無法使用或部分可用。 以下是此類功能的清單。 此外，請參閱[已過時和已移除的功能](/help/release-notes/deprecated-removed-features.md)。

| 功能或使用案例 | 在[!DNL Experience Manager]中的狀態為[!DNL Cloud Service] | 評論 |
|-----|-----|-----|
| [重複資產偵測](/help/assets/detect-duplicate-assets.md) | 運作方式不同 | 檢視[在 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html)中的運作方式。 |
| [僅供置入(FPO)轉譯](/help/assets/configure-fpo-renditions.md) | 運作方式不同 | 處理設定檔時會使用資產微服務來產生FPO轉譯。 在Experience Manager6.5中，有協力廠商解決方案（例如[!DNL ImageMagick]）可用來產生轉譯。 |
| 中繼資料回寫 | 運作方式不同 | 預設為停用。 如有需要，請啟用對應的工作流程啟動器。 回寫是由資產微服務處理。 |
| 處理使用封裝管理員上傳的資產 | 需要手動介入 | 使用&#x200B;**[!UICONTROL 重新處理資產]**&#x200B;動作手動重新處理。 |
| mime型別偵測 | 不支援。 | 如果您上傳沒有副檔名或副檔名不正確的數位資產，系統可能不會依需求處理該資產。 使用者仍然可以在DAM中儲存不帶副檔名的二進位檔案。 請參閱 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/detect-asset-mime-type-with-tika.html)中的[MIME型別偵測。 |
| 複合資產的子資產產生 | 不支援。 | 可能不會滿足註解等相依使用案例。 檢視 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-linked-subassets.html#generate-subassets)中的[子資產建立。 從[2021.7.0版本](/help/release-notes/release-notes-cloud/release-notes-current.md)開始，某些檔案型別的PDF預覽可用。 |
| 編輯影像 | 不支援 | Experience Manageras a Cloud Service不支援編輯資產。 檢視[它在Experience Manager6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#editing-images)中的運作方式。 |
| 首頁 | 不支援 | 檢視 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-home-page.html)中的[[!DNL Assets] 首頁體驗 |
| 從ZIP封存擷取資產 | 不支援 | 請參閱 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#extractzip)中的[ZIP解壓縮。 |
| Assets評等 | 不支援 | 不支援中繼資料結構編輯器中的評等Widget。 |
| 內容處置篩選 | 不支援 | `ContentDispositionFilter`的常見使用案例是讓系統管理員設定[!DNL Experience Manager]以提供HTML檔案，並內嵌開啟PDF檔案而非下載這些檔案。 在Publish執行個體上，您可以使用Dispatcher設定來管理處置。 在作者執行個體上，Adobe不建議修改Content Disposition標題。 請參閱 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/content-disposition-filter.html)中的[內容配置篩選器。 |
| 產品拍照範本 | 不支援 | 請參閱 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/projects/managing-product-information.html)中的[產品拍照範本。 |
| 智慧型翻譯 | 不支援 | [智慧型翻譯](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/translation/smart-translation-search-feature-video-use.html)在[!DNL Experience Manager]中不支援做為[!DNL Cloud Service]。 |
| WebDAV | 不支援 | 如需其他選擇，請參閱[[!DNL Creative Cloud] 整合](/help/assets/aem-cc-integration-best-practices.md)或[開發人員參考資料](/help/assets/developer-reference-material-apis.md)。 |
| 傳統 UI | 不支援 | 僅提供觸控式使用者介面。 |

**另請參閱**

* [翻譯資產](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [資產支援的檔案格式](file-format-support.md)
* [搜尋資產](search-assets.md)
* [連接的資產](use-assets-across-connected-assets-instances.md)
* [資產報表](asset-reports.md)
* [中繼資料結構描述](metadata-schemas.md)
* [下載資產](download-assets-from-aem.md)
* [管理中繼資料](manage-metadata.md)
* [搜尋 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [大量中繼資料匯入](metadata-import-export.md)
* [發佈資產至 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>下列資源可作為[!DNL Cloud Service]用於[!DNL Experience Manager]：
>
>* [已棄用和已移除功能的清單](/help/release-notes/deprecated-removed-features.md)
>* [簡介](/help/overview/introduction.md)
>* [新增功能與不同之處](/help/overview/what-is-new-and-different.md)
>* [架構](/help/overview/architecture.md)
>* [重大變更](/help/release-notes/aem-cloud-changes.md)
>* [重大變更 [!DNL Sites]](/help/sites-cloud/sites-cloud-changes.md)
>* [教學課程影片](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html)
