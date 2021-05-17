---
title: ' [!DNL Adobe Experience Manager Assets] 中a [!DNL Cloud Service]的顯著變化'
description: 與[!DNLAdobe Experience Manager6.5相比， [!DNL Adobe Experience Manager Assets] in [!DNL Experience Manager] as a [!DNL Cloud Service] 的顯著變化。
feature: 發行資訊
role: Business Practitioner,Leader,Architect,Administrator
exl-id: 93e7dbcd-016e-4ef2-a1cd-c554efb5ad34
source-git-commit: bcb747517595943e1ed65d19424f002136877903
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 6%

---

# [!DNL Experience Manager Assets]變更為[!DNL Cloud Service] {#notable-changes}

[!DNL Adobe Experience Manager] 因此，您 [!DNL Cloud Service] 可運用許多新功能和可能性來管理Experience Manager專案。與[!DNL Experience Manager][!DNL Cloud Service]相比，[!DNL Experience Manager Assets]內部部署或托管為Adobe托管服務之間有許多不同。 本文著重說明[!DNL Assets]功能的重要差異。

與[Experience Manager] 6.5相比，主要差異在於：

* [資產擷取、上傳和處理](#asset-ingestion)。
* [適用於雲端原生處理的資產微服務](#asset-microservices)。
* [移除傳統 UI](#classic-ui).

## 資產擷取與處理{#asset-ingestion}

資產上傳已最佳化，因為它可以更佳地縮放擷取、更快速的上傳、使用微型服務更快速的處理以及大量擷取。 產品功能（網頁使用者介面、案頭用戶端）已更新。 此外，這可能會影響一些現有的自訂。

* [!DNL Experience Manager] 使用直接二進位存取原則來上傳和下載資產，並使用資產微型服務來處理資產。請參閱[微服務概述](/help/assets/asset-microservices-overview.md)。
   * 資產上傳[並直接二進位存取](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access)。
   * 如需技術詳細資訊，請參閱[直接二進位上傳通訊協定和API](/help/assets/developer-reference-material-apis.md#upload-binary)。
   * 如需基本CRUD作業的可用API方法比較，請參閱[API和資產作業](/help/assets/developer-reference-material-apis.md#use-cases-and-apis)。
* 舊版 已不提供預設的工作流程 **[!UICONTROL DAM Asset Update]**。[!DNL Experience Manager]相反，資產微服務提供可擴充、可立即使用的服務，涵蓋大部分預設資產處理（轉譯、中繼資料擷取和文字擷取，以利建立索引）。
   * 請參閱[配置和使用資產微服務](/help/assets/asset-microservices-configure-and-use.md)
   * 若要在處理中自訂工作流程步驟，可使用[後處理工作流程](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)。

使用相同的命名慣例，以向後相容的方式在資產儲存庫節點中儲存與資產Microservices生成的標準轉譯。

## 開發和測試資產微服務{#asset-microservices}

資產微服務使用雲端服務提供資產的可擴充且彈性化處理。 Adobe管理雲端服務，以最佳化處理不同的資產類型和處理選項。 Asset microservices可協助您避免需要協力廠商轉換工具和方法（例如ImageMagick）並簡化組態，同時為一般檔案類型提供現成可用的功能。 您現在可以處理[廣泛的檔案類型](/help/assets/file-format-support.md)，其中涵蓋的格式比舊版的Experience Manager更多。 例如，PSD和PSB格式的縮圖擷取現在可能是先前需要的協力廠商解決方案（例如ImageMagick）。 不能對[!UICONTROL 處理配置檔案]配置使用ImageMagick的複雜配置。 使用[!DNL Dynamic Media]進行進階的FFmpeg視訊轉碼，並使用處理設定檔進行MP4視訊的[基本轉碼。](/help/assets/manage-video-assets.md#transcode-video)

資產微服務是雲端原生服務，在Cloud Manager中管理的客戶程式和環境中自動布建並連線至[!DNL Experience Manager]。 若要擴充或自訂[!DNL Experience Manager]，開發人員可以使用現有內容或資產與雲端環境中產生的轉譯，以測試並驗證其程式碼，使用、顯示、下載資產。

若要對程式碼和程式進行端對端驗證，包括資產擷取和處理，請使用[管道](/help/implementing/cloud-manager/configure-pipeline.md)將程式碼變更部署至雲端開發環境，並完整執行資產微服務處理來進行測試。


## 功能奇偶校驗([!DNL Experience Manager] 6.5 {#cloud-service-feature-status})

[!DNL Experience Manager] 為現 [!DNL Cloud Service] 有功能提供許多新功能和更高效能的方式。但是，當從[!DNL Experience Manager] 6.5移至[!DNL Experience Manager]作為[!DNL Cloud Service]時，您可能會注意到有些功能的運作方式不同、不可用或部分可用。 以下是這些功能的清單：

| 功能或使用案例 | [!DNL Experience Manager]的狀態為[!DNL Cloud Service] | 評論 |
|-----|-----|-----|
| [重複資產偵測](/help/assets/manage-digital-assets.md#detect-duplicate-assets) | 工作方式不同。 | 請參閱[它在 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html)中的運作方式。 |
| [僅限位置(FPO)轉譯](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/configure-aem-assets-for-asset-link.ug.html#configfporendition) | 工作方式不同 |  |
| 中繼資料回寫 | 工作方式不同 | 預設為停用. 視需要啟用對應的工作流程啟動程式。 回寫由資產微服務處理。 |
| 處理使用Package Manager上傳的資產 | 需要人工干預。 | 使用&#x200B;**[!UICONTROL 重新處理資產]**&#x200B;動作手動重新處理。 |
| MIME類型檢測 | 不支援. | 如果您上傳的數位資產沒有副檔名或副檔名不正確，可能無法視需要處理。 使用者仍可在DAM中儲存二進位檔案，但無副檔名。 請參閱 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/detect-asset-mime-type-with-tika.html)中的[MIME類型檢測。 |
| 複合資產的子資產產生 | 不支援. | 相依使用案例未完成。 例如，多頁PDF檔案的註解會受到影響。 請參閱 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-linked-subassets.html#generate-subassets)中的[子資產建立。 |
| 首頁 | 不支援. | 請參閱[[!DNL Assets] Home Page experience in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-home-page.html) |
| 從ZIP封存擷取資產 | 不支援. | 請參閱 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#extractzip)中的[ZIP解壓縮。 |
| 傳統 UI | 不支援. | 僅提供可觸控的UI。 |

>[!MORELIKETHIS]
>
>[!DNL Experience Manager]作為[!DNL Cloud Service]提供以下資源：
>
>* [已過時和已移除功能的清單](/help/release-notes/deprecated-removed-features.md)
* [簡介](/help/overview/introduction.md)
* [新增功能與不同之處](/help/overview/what-is-new-and-different.md)
* [建築](/help/core-concepts/architecture.md)
* [顯著變更](/help/release-notes/aem-cloud-changes.md)
* [顯著更改 [!DNL Sites]](/help/sites-cloud/sites-cloud-changes.md)
* [教學影片](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html)

