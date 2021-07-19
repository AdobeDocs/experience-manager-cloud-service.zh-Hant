---
title: ' [!DNL Adobe Experience Manager Assets] 中a [!DNL Cloud Service]顯著變更'
description: ' [!DNL Adobe Experience Manager Assets] in [!DNL Experience Manager] as a [!DNL Cloud Service] as compared to [!DNL Adobe Experience Manager] 6.5的重大變更。'
feature: 發行資訊
role: User,Leader,Architect,Admin
exl-id: 93e7dbcd-016e-4ef2-a1cd-c554efb5ad34
source-git-commit: 4be76f19c27aeab84de388106a440434a99a738c
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 5%

---

# [!DNL Experience Manager Assets]作為[!DNL Cloud Service]的重大變更 {#notable-changes}

[!DNL Adobe Experience Manager] as提供 [!DNL Cloud Service] 許多管理Experience Manager專案的新功能，並帶來許多可能性。與[!DNL Experience Manager]作為[!DNL Cloud Service]的相比，[!DNL Experience Manager Assets]內部部署或托管作為Adobe托管服務之間有許多差異。 本文著重說明[!DNL Assets]功能的重要差異。

與[Experience Manager] 6.5相比，主要差異如下：

* [資產擷取、上傳和處理](#asset-ingestion)。
* [適用於雲端原生處理的資產微服務](#asset-microservices)。
* [移除傳統 UI](#classic-ui).

## 資產擷取、處理和發佈 {#asset-ingestion-distribution}

資產上傳已最佳化，能提供更佳的擷取縮放、更快速的上傳、使用微服務更快的處理以及大量擷取，以提高效率。 產品功能（網頁使用者介面、案頭用戶端）已更新。 此外，這可能會影響一些現有的自訂。

* [!DNL Experience Manager] 使用直接二進位存取原則來上傳和下載資產，並使用資產微服務來處理資產。請參閱[微服務概述](/help/assets/asset-microservices-overview.md)。
   * 具有直接二進位存取的資產上傳[](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access)。
   * 如需技術詳細資訊，請參閱[直接二進位上傳通訊協定和API](/help/assets/developer-reference-material-apis.md#upload-binary)。
   * 如需基本CRUD作業可用API方法的比較，請參閱[API和資產作業](/help/assets/developer-reference-material-apis.md#use-cases-and-apis)。
* 舊版 已不提供預設的工作流程 **[!UICONTROL DAM Asset Update]**。[!DNL Experience Manager]相反地，資產微服務提供可擴充且隨時可用的服務，涵蓋大部分預設資產處理（轉譯、中繼資料擷取和索引文字擷取）。
   * 請參閱[配置和使用資產微服務](/help/assets/asset-microservices-configure-and-use.md)
   * 若要在處理中自訂工作流程步驟，可使用[後置處理工作流程](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)。

* 若要傳送二進位檔案（不需任何轉換），網站元件可使用直接下載。 SlingGETservlet已更新，依預設可讓開發人員執行此作業。 傳送二進位並搭配一些轉換的網站元件（例如透過servlet調整其大小）仍可繼續原樣運作。

透過資產微服務產生的標準轉譯，會使用相同的命名慣例，以向後相容的方式儲存在資產存放庫節點中。

## 開發和測試資產微服務 {#asset-microservices}

資產微服務使用雲端服務提供資產的可擴充且可復原處理功能。 Adobe管理雲端服務，以最佳處理不同資產類型和處理選項。 資產微服務有助於避免需要第三方轉譯工具和方法（例如[!DNL ImageMagick]）並簡化設定，同時為常見檔案類型提供現成可用的功能。 您現在可以處理[範圍廣泛的檔案類型](/help/assets/file-format-support.md)，其中包含比舊版Experience Manager更多現成的格式。 例如，現在可以擷取PSD和PSB格式的縮圖，先前需要的協力廠商解決方案，例如[!DNL ImageMagick]。 對於[!UICONTROL 處理配置檔案]配置，不能使用[!DNL ImageMagick]的複雜配置。 使用[!DNL Dynamic Media]進階FFmpeg影片轉碼，並使用處理設定檔來將MP4影片](/help/assets/manage-video-assets.md#transcode-video)基本轉碼。[

資產微服務是雲端原生服務，會在Cloud Manager中管理的客戶程式和環境中，自動布建並連線至[!DNL Experience Manager]。 若要擴充或自訂[!DNL Experience Manager]，開發人員可使用在雲端環境中產生的現有內容或資產與轉譯，以使用、顯示、下載資產來測試及驗證其程式碼。

若要對程式碼和程式（包括資產擷取和處理）進行端對端驗證，請使用[管道](/help/implementing/cloud-manager/configure-pipeline.md)將程式碼變更部署至雲端開發環境，並透過完全執行資產微服務處理來測試。

## [!DNL Experience Manager] 6.5的功能奇偶校驗 {#cloud-service-feature-status}

[!DNL Experience Manager] as a引 [!DNL Cloud Service] 入了許多新功能和更高效能的方式，使現有功能能夠正常運作。但是，當從[!DNL Experience Manager] 6.5移至[!DNL Experience Manager]作為[!DNL Cloud Service]時，您可能會注意到有些功能的運作方式不同、無法使用或部分可用。 以下是這些功能的清單。 此外，請參閱[已棄用和已移除的功能](/help/release-notes/deprecated-removed-features.md)。

| 功能或使用案例 | [!DNL Experience Manager]中的狀態為[!DNL Cloud Service] | 評論 |
|-----|-----|-----|
| [重複資產偵測](/help/assets/manage-digital-assets.md#detect-duplicate-assets) | 運作方式不同。 | 請參閱[其在 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html)中的運作方式。 |
| [僅適用於版位(FPO)轉譯](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/configure-aem-assets-for-asset-link.ug.html#configfporendition) | 不同的運作方式 |  |
| 中繼資料回寫 | 不同的運作方式 | 預設為停用. 視需要啟用對應的工作流程啟動器。 回寫由資產微服務處理。 |
| 使用封裝管理程式上傳的資產處理 | 需要手動干預。 | 使用&#x200B;**[!UICONTROL 重新處理資產]**&#x200B;動作手動重新處理。 |
| MIME類型檢測 | 不支援. | 如果您上傳的數位資產沒有副檔名或副檔名不正確，可能無法視需要處理。 使用者仍可以儲存二進位檔案，而DAM中沒有副檔名。 請參閱 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/detect-asset-mime-type-with-tika.html)中的[MIME類型檢測。 |
| 複合資產的子資產產生或註解 | 不支援. | 相依使用案例未履行。 例如，無法檢視或註解多頁PDF、INDD、PPT、PPTX和AI檔案。 請參閱 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-linked-subassets.html#generate-subassets)中的[子資產建立。 |
| 首頁 | 不支援. | 請參閱[[!DNL Assets] Home Page experience in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-home-page.html) |
| 從ZIP封存解壓縮資產 | 不支援. | 請參閱 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#extractzip)中的[ZIP解壓縮。 |
| 資產評等 | 不支援. | 不支援中繼資料結構編輯器中的評等Widget。 |
| 內容處置篩選器 | 不支援. | `ContentDispositionFilter`的一個常見使用案例是讓管理員設定[!DNL Experience Manager]以提供HTML檔案，並內嵌開啟PDF檔案，而非下載這些檔案。 在發佈例項上，您可以使用Dispatcher設定來管理處置。 在「製作」例項上，Adobe不建議修改「內容處置」標題。 請參閱 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/content-disposition-filter.html)中的[內容處置篩選器。 |
| [下載報表](/help/assets/asset-reports.md) | 不支援. | 目前無法使用通知資產使用的下載報表。 請參閱 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/asset-reports.html)中的[下載報表。 |
| 產品攝影模板 | 不支援. | 請參閱 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/projects/managing-product-information.html)中的[產品像片模板。 |
| 傳統 UI | 不支援. | 僅提供觸控式使用者介面。 |

>[!MORELIKETHIS]
>
>[!DNL Experience Manager]作為[!DNL Cloud Service]可使用下列資源：
>
>* [已棄用和已移除功能的清單](/help/release-notes/deprecated-removed-features.md)
* [簡介](/help/overview/introduction.md)
* [新增功能與不同之處](/help/overview/what-is-new-and-different.md)
* [架構](/help/core-concepts/architecture.md)
* [重大變更](/help/release-notes/aem-cloud-changes.md)
* [重大更改 [!DNL Sites]](/help/sites-cloud/sites-cloud-changes.md)
* [教學影片](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html)

