---
title: ' [!DNL Adobe Experience Manager Assets] 中a [!DNL Cloud Service]的顯著變化'
description: 與[!DNL Adobe Experience Manager 6.5相比， [!DNL Adobe Experience Manager Assets] in [!DNL Experience Manager] as a [!DNL Cloud Service] 的顯著變更。
translation-type: tm+mt
source-git-commit: 3e7613aa50e69e2c9789df4f2fb429ab74654110
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 4%

---


# [!DNL Experience Manager Assets]變更為[!DNL Cloud Service] {#notable-changes}

[!DNL Adobe Experience Manager] 這為管 [!DNL Cloud Service] 理您的Experience Manager專案帶來了許多新功能和可能。與[!DNL Experience Manager]作為[!DNL Cloud Service]的相比，[!DNL Experience Manager Assets]內部部署或代管為Adobe Managed Service有許多不同。 本文著重說明[!DNL Assets]功能的重要差異。

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
* 不支援中繼資料回寫。 請參閱 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/xmp-writeback.html)中的[中繼資料回寫。
* 使用「封裝管理器」上傳的資產需要使用[!DNL Assets]使用者介面中的「重新處理資產」動作，手動重新處理。****
* [!DNL Assets] 不會自動偵測已上傳資產的MIME類型。沒有副檔名或副檔名錯誤的數位資產不會視需要處理。 例如，上傳此類資產時，資產不會發生任何情況，或是會套用錯誤的處理設定檔。 使用者仍可在DAM中儲存二進位檔案，但無副檔名。 請參閱 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/detect-asset-mime-type-with-tika.html)中的[MIME類型檢測。
* [!DNL Assets] 無法使用首頁體驗。請參閱[[!DNL Assets] Home Page experience in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-home-page.html)。
* 與 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html)中的[工作方式相比，重複資產偵測的運作方式不同。
* 僅用於位置(FPO)轉譯的產生方式與舊版[!DNL Experience Manager]不同。 請參閱[ [!DNL Experience Manager] 的FPO轉譯，如a [!DNL Cloud Service]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/configure-aem-assets-for-asset-link.ug.html)。

使用相同的命名慣例，以向後相容的方式在資產儲存庫節點中儲存與資產Microservices生成的標準轉譯。

## 開發和測試資產微服務{#asset-microservices}

資產微服務使用雲端服務提供資產的可擴充且彈性化處理。 Adobe管理雲端服務，以最佳化處理不同的資產類型和處理選項。 Asset microservices可協助您避免需要協力廠商轉換工具和方法（例如ImageMagick）並簡化組態，同時為一般檔案類型提供現成可用的功能。 您現在可以處理[廣泛的檔案類型](/help/assets/file-format-support.md)，這些類型涵蓋比舊版Experience Manager更多的現成格式。 例如，PSD和PSB格式的縮圖擷取現在可能是先前需要的協力廠商解決方案（例如ImageMagick）。 不能對[!UICONTROL 處理配置檔案]配置使用ImageMagick的複雜配置。 使用[!DNL Dynamic Media]進行進階的FFmpeg視訊轉碼，並使用處理設定檔進行MP4視訊的[基本轉碼。](/help/assets/manage-video-assets.md#transcode-video)

資產微服務是雲端原生服務，在Cloud Manager中管理的客戶程式和環境中自動布建並連線至[!DNL Experience Manager]。 若要擴充或自訂[!DNL Experience Manager]，開發人員可以使用現有內容或資產與雲端環境中產生的轉譯，以測試並驗證其程式碼，使用、顯示、下載資產。

若要對程式碼和程式進行端對端驗證，包括資產擷取和處理，請使用[管道](/help/implementing/cloud-manager/configure-pipeline.md)將程式碼變更部署至雲端開發環境，並完整執行資產微服務處理來進行測試。

## 移除傳統 UI {#classic-ui}

在[!DNL Experience Manager]中，Classic UI不再以[!DNL Cloud Service]的形式提供。 只有啟用觸控的UI才可用。

>[!MORELIKETHIS]
>
>[!DNL Experience Manager]作為[!DNL Cloud Service]提供以下資源：
>
>* [簡介](/help/overview/introduction.md)
>* [新增功能與不同之處](/help/overview/what-is-new-and-different.md)
>* [建築](/help/core-concepts/architecture.md)
>* [顯著變更](/help/release-notes/aem-cloud-changes.md)
>* [顯著變更 [!DNL Sites]](/help/sites-cloud/sites-cloud-changes.md)
>* [教學影片](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html)

