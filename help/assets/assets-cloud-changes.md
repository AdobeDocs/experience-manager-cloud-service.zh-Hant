---
title: 中的重大變更 [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service]
description: 重大變更 [!DNL Adobe Experience Manager Assets] in [!DNL Experience Manager] as a [!DNL Cloud Service] as compared to [!DNL Adobe Experience Manager] 6.5。
feature: Release Information
role: User,Leader,Architect,Admin
exl-id: 93e7dbcd-016e-4ef2-a1cd-c554efb5ad34
source-git-commit: fe662a515a52bcf4648585366422064edce1a7fd
workflow-type: tm+mt
source-wordcount: '1026'
ht-degree: 5%

---

# 重大變更 [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#notable-changes}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 提供許多新功能，並帶來許多管理Experience Manager專案的可能性。 兩者之間有許多差異 [!DNL Experience Manager Assets] 內部部署或托管為Adobe托管服務，與 [!DNL Experience Manager] as a [!DNL Cloud Service]. 本文著重說明 [!DNL Assets] 功能。

與以下主要差異： [!DNL Experience Manager] 6.5分為以下幾方面：

* [資產擷取、上傳和處理](#asset-ingestion).
* [適用於雲端原生處理的資產微服務](#asset-microservices).
* [移除傳統 UI](#classic-ui).

## 資產擷取、處理和發佈 {#asset-ingestion-distribution}

資產上傳已最佳化，能提供更佳的擷取縮放、更快速的上傳、使用微服務更快的處理以及大量擷取，以提高效率。 產品功能（網頁使用者介面、案頭用戶端）已更新。 此外，這可能會影響一些現有的自訂。

* [!DNL Experience Manager] 使用直接二進位存取原則來上傳和下載資產，並使用資產微服務來處理資產。 請參閱 [微服務概述](/help/assets/asset-microservices-overview.md).
   * 資產上傳 [直接二進位存取](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access).
   * 如需技術詳細資訊，請參閱 [直接二進位上傳通訊協定和API](/help/assets/developer-reference-material-apis.md#upload-binary).
   * 如需基本CRUD作業可用API方法的比較，請參閱 [API與資產作業](/help/assets/developer-reference-material-apis.md#use-cases-and-apis).
* 舊版 已不提供預設的工作流程 **[!UICONTROL DAM Asset Update]**。[!DNL Experience Manager]相反地，資產微服務提供可擴充且隨時可用的服務，涵蓋大部分預設資產處理（轉譯、中繼資料擷取和索引文字擷取）。
   * 請參閱 [設定及使用資產微服務](/help/assets/asset-microservices-configure-and-use.md)
   * 若要在處理中自訂工作流程步驟， [後置處理工作流程](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) 可供使用。

* 若要傳送二進位檔案（不需任何轉換），網站元件可使用直接下載。 SlingGETservlet已更新，依預設可讓開發人員執行此作業。 傳送二進位並搭配一些轉換的網站元件（例如透過servlet調整其大小）仍可繼續原樣運作。

透過資產微服務產生的標準轉譯，會使用相同的命名慣例，以向後相容的方式儲存在資產存放庫節點中。

## 開發和測試資產微服務 {#asset-microservices}

資產微服務使用雲端服務提供資產的可擴充且可復原處理功能。 Adobe管理雲端服務，以最佳處理不同資產類型和處理選項。 資產微服務有助於避免需要協力廠商轉譯工具和方法(例如 [!DNL ImageMagick])並簡化設定，同時為常見檔案類型提供現成可用的功能。 您現在可以處理 [檔案類型廣泛](/help/assets/file-format-support.md) 比舊版Experience Manager可能涵蓋的現成格式更多。 例如，現在可以擷取PSD和PSB格式的縮圖，而之前需要的協力廠商解決方案，例如 [!DNL ImageMagick]. 您無法使用 [!DNL ImageMagick] 針對 [!UICONTROL 處理設定檔] 設定。 使用 [!DNL Dynamic Media] 進階FFmpeg影片轉碼，以及使用處理設定檔 [基本MP4影片轉碼](/help/assets/manage-video-assets.md#transcode-video).

資產微服務是雲端原生服務，會自動布建並連線至 [!DNL Experience Manager] 在Cloud Manager中管理的客戶程式和環境中。 延伸或自訂 [!DNL Experience Manager]，開發人員可使用在雲端環境中產生的轉譯現有內容或資產，以使用、顯示、下載資產來測試及驗證其程式碼。

若要對程式碼和程式（包括資產擷取和處理）進行端對端驗證，請使用 [管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) 並以完全執行資產微服務處理來測試。

## 與 [!DNL Experience Manager] 6.5 {#cloud-service-feature-status}

[!DNL Experience Manager] as a [!DNL Cloud Service] 引入了許多新功能和更高效能的方法，使現有功能能夠正常工作。 不過，若從 [!DNL Experience Manager] 6.5至 [!DNL Experience Manager] as a [!DNL Cloud Service]，您可能會發現有些功能的運作方式不同、無法使用或部分可用。 以下是這些功能的清單。 此外，請參閱 [過時和移除的功能](/help/release-notes/deprecated-removed-features.md).

| 功能或使用案例 | 狀態(在 [!DNL Experience Manager] as a [!DNL Cloud Service] | 評論 |
|-----|-----|-----|
| [重複資產偵測](/help/assets/manage-digital-assets.md#detect-duplicate-assets) | 不同的運作方式 | 請參閱 [如何運作 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html). |
| [僅適用於版位(FPO)轉譯](/help/assets/configure-fpo-renditions.md) | 不同的運作方式 | 處理設定檔會使用資產微服務產生FPO轉譯。 在Experience Manager6.5中，是協力廠商解決方案，例如 [!DNL ImageMagick] 可用於產生轉譯。 |
| 中繼資料回寫 | 不同的運作方式 | 預設為停用. 視需要啟用對應的工作流程啟動器。 回寫由資產微服務處理。 |
| 使用封裝管理程式上傳的資產處理 | 需要手動干預 | 使用 **[!UICONTROL 重新處理資產]** 動作。 |
| MIME類型檢測 | 不支援. | 如果您上傳的數位資產沒有副檔名或副檔名不正確，可能無法視需要處理。 使用者仍可以儲存二進位檔案，而DAM中沒有副檔名。 請參閱 [中的MIME類型檢測 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/detect-asset-mime-type-with-tika.html). |
| 複合資產的子資產產生 | 不支援. | 注釋之類的相依使用案例可能無法履行。 請參閱 [子資產建立 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-linked-subassets.html#generate-subassets). 某些檔案類型的PDF預覽已開始 [2021.7.0版](/help/release-notes/release-notes-cloud/release-notes-current.md). |
| 編輯影像 | 不支援 | Experience Manageras a Cloud Service不支援編輯資產。 請參閱 [在Experience Manager6.5中的運作方式](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#editing-images). |
| 首頁 | 不支援 | 請參閱 [[!DNL Assets] Home Page experience in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-home-page.html) |
| 從ZIP封存解壓縮資產 | 不支援 | 請參閱 [郵遞區號提取(位於 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#extractzip). |
| 資產評等 | 不支援 | 不支援中繼資料結構編輯器中的評等Widget。 |
| 內容處置篩選器 | 不支援 | 的常見使用案例 `ContentDispositionFilter` 是讓管理員設定 [!DNL Experience Manager] 提供HTML檔案並內嵌開啟PDF檔案，而非下載這些檔案。 在發佈例項上，您可以使用Dispatcher設定來管理處置。 在「製作」例項上，Adobe不建議修改「內容處置」標題。 請參閱 [中的內容處置篩選器 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/content-disposition-filter.html). |
| [下載報表](/help/assets/asset-reports.md) | 不支援 | 目前無法使用通知資產使用的下載報表。 請參閱 [下載報表 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/asset-reports.html). |
| 產品攝影模板 | 不支援 | 請參閱 [產品拍攝模板 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/projects/managing-product-information.html). |
| 智慧翻譯 | 不支援 | [智慧翻譯](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/translation/smart-translation-search-feature-video-use.html) 不支援 [!DNL Experience Manager] as a [!DNL Cloud Service]. |
| WebDAV | 不支援 | 如需其他選項，請參閱 [[!DNL Creative Cloud] 整合](/help/assets/aem-cc-integration-best-practices.md) 或 [顯影劑參考資料](/help/assets/developer-reference-material-apis.md). |
| 傳統 UI | 不支援 | 僅提供觸控式使用者介面。 |

>[!MORELIKETHIS]
>
>下列資源可供 [!DNL Experience Manager] as a [!DNL Cloud Service]:
>
>* [已棄用和已移除功能的清單](/help/release-notes/deprecated-removed-features.md)
>* [簡介](/help/overview/introduction.md)
>* [新增功能與不同之處](/help/overview/what-is-new-and-different.md)
>* [架構](/help/overview/architecture.md)
>* [重大變更](/help/release-notes/aem-cloud-changes.md)
>* [重大變更 [!DNL Sites]](/help/sites-cloud/sites-cloud-changes.md)
>* [教學影片](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html)

