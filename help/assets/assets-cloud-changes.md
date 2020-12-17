---
title: Adobe Experience Manager資產中顯著變更為a [!DNL Cloud Service]
description: '與Adobe Experience Manager 6.5相比，Experience Manager中Adobe Experience Manager Assets的變更明顯。 [!DNL Cloud Service] '
translation-type: tm+mt
source-git-commit: 0838f384b31c59fe95087e1a71741656eedcd13b
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 3%

---


# Experience Manager Assets的顯著變更為[!DNL Cloud Service] {#notable-changes}

Adobe Experience Manager是[!DNL Cloud Service]，為您管理Experience Manager專案帶來許多新功能與可能。 與[!DNL Cloud Service]的[!DNL Experience Manager]相比，Experience Manager Assets內部部署或代管為Adobe Managed Service之間有許多不同。 本文著重說明[!DNL Assets]功能的重要差異。

與[Experience Manager] 6.5相比，主要差異在於：

* [資產擷取、上傳和處理](#asset-ingestion)。
* [適用於雲端原生處理的資產微服務](#asset-microservices)。
* [移除傳統 UI](#classic-ui).

## 資產擷取與處理{#asset-ingestion}

資產上傳已最佳化，因為它可以更佳地縮放資產擷取、更快速的上傳、使用微型服務更快速的處理，以及大量擷取。 產品功能（網路使用者介面、案頭用戶端）已更新。 但是，這可能會影響到一些現有的自訂。

* Experience Manager使用直接二進位存取原則來上傳和下載資產，並使用資產微服務來處理資產。 請參閱[資產擷取概觀](/help/assets/asset-microservices-overview.md)。
   * 資產上傳[並直接二進位存取](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access)。
   * 如需技術詳細資訊，請參閱[直接二進位上傳通訊協定和API](/help/assets/developer-reference-material-apis.md#upload-binary)。
   * 如需基本CRUD作業的可用API方法比較，請參閱[API和資產作業](/help/assets/developer-reference-material-apis.md#use-cases-and-apis)。
* 舊版 已不提供預設的工作流程 **[!UICONTROL DAM Asset Update]**。[!DNL Experience Manager]相反，資產微服務提供可擴充、可立即使用的服務，涵蓋大部分預設資產處理（轉譯、中繼資料擷取和文字擷取，以利建立索引）。
   * 請參閱[配置和使用資產微服務](/help/assets/asset-microservices-configure-and-use.md)
   * 若要在處理中自訂工作流程步驟，可使用[後處理工作流程](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)。
* 透過「封裝管理員」傳入的資產需要使用「資產」介面中的「重新處理資產」動作，手動重新處理。****

使用資產微服務產生的標準轉譯會以向後相容的方式儲存在資產儲存庫節點中（相同的命名慣例）。

## 開發和測試資產微服務{#asset-microservices}

資產微服務使用雲端服務提供資產的可擴充且彈性化處理。 Adobe管理雲端服務，以最佳化處理不同的資產類型和處理選項。 Asset microservices可協助您避免需要協力廠商轉換工具和方法（例如ImageMagick）並簡化組態，同時為一般檔案類型提供現成可用的功能。 您現在可以處理[廣泛的檔案類型](/help/assets/file-format-support.md)，這些類型涵蓋比舊版Experience Manager更多的現成格式。 例如，PSD和PSB格式的縮圖擷取現在可能是先前需要的協力廠商解決方案（例如ImageMagick）。 不能對[!UICONTROL 處理配置檔案]配置使用ImageMagick的複雜配置。 使用[!DNL Dynamic Media]進行進階的FFmpeg視訊轉碼，並使用處理設定檔進行MP4視訊的[基本轉碼。](/help/assets/manage-video-assets.md#transcode-video)

Asset Microservices是雲端原生服務，會在Cloud Manager中管理的客戶程式和環境中自動布建並連線至Experience Manager。 若要擴充或自訂Experience Manager，開發人員可以使用現有內容或資產與在雲端環境中產生的轉譯，以測試並驗證其程式碼，使用、顯示、下載資產。

若要對程式碼和程式進行端對端驗證，包括資產擷取和處理，請使用[管道](/help/implementing/cloud-manager/configure-pipeline.md)將程式碼變更部署至雲端開發環境，並完整執行資產微服務處理來進行測試。

## 移除傳統 UI {#classic-ui}

Experience Manager中不再提供Classic UI作為[!DNL Cloud Service]。 標準介面是可觸控的UI。

>[!MORELIKETHIS]
>
>* [簡介 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]](/help/overview/introduction.md)
>* [ [!DNL Experience Manager] as a [!DNL Cloud Service] 概觀——新增功能與不同功能](/help/overview/what-is-new-and-different.md)
>* [!DNL Experience Manager]的[架構](/help/core-concepts/architecture.md)作為[!DNL Cloud Service]
>* [As  [!DNL Experience Manager] a的顯著變更 [!DNL Cloud Service]](/help/release-notes/aem-cloud-changes.md)
>* [As  [!DNL Experience Manager Sites] a的顯著變更 [!DNL Cloud Service]](/help/sites-cloud/sites-cloud-changes.md)
>* [[!DNL Experience Manager] as a [!DNL Cloud Service] 教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html)

