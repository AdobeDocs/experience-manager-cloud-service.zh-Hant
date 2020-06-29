---
title: Adobe Experience Manager資產雲端服務的顯著變更
description: AEM Cloud服務中的Adobe Experience Manager Assets與Adobe Experience Manager 6.5相比有顯著變更。
translation-type: tm+mt
source-git-commit: e381807d7c199113689304e9481dfe2022ee5f93
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 10%

---


# Notable changes to Experience Manager Assets as a Cloud Service {#notable-changes}

Adobe Experience Manager即雲端服務，為您的AEM專案帶來許多新功能與可能。 但是，與Experience Manager雲端服務相比，Experience Manager Assets的內部部署或Adobe Managed Service之間有許多不同。 本檔案強調資產功能的重要差異。

與Experience Manager 6.5相比，主要差異在於：

* [資產擷取和上傳](#asset-ingestion)。
* [適用於雲端處理的資產微服務](#asset-microservices)。
* [移除傳統 UI](#classic-ui).

>[!NOTE]
>本檔案著重說明對AEM Assets的顯著變更。 如需AEM的「雲端服務」及其他模組的一般變更，請參閱：
>
>* [Adobe Experience Manager 雲端服務簡介](/help/overview/introduction.md)
>* AEM [雲端服務概觀——新增功能與不同功能](/help/overview/what-is-new-and-different.md)
>* Adobe Experience Manager 雲端服務[架構](/help/core-concepts/architecture.md)
>* [AEM as a Cloud服務的顯著變更（發行說明）](/help/release-notes/aem-cloud-changes.md)
>* [ 雲端服務 AEM Sites 重大變更](/help/sites-cloud/sites-cloud-changes.md)
>* [Adobe Experience Manager 雲端服務教學課程](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/overview.html)


## 資產擷取與上傳 {#asset-ingestion}

資產上傳已最佳化，因為可以更佳地縮放資產擷取，並加快上傳速度。 產品功能（網路使用者介面、案頭用戶端）已更新。 但是，這可能會影響到一些現有的自訂。

* Experience Manager使用直接二進位存取原則來上傳和下載資產，並使用資產微服務來處理資產。 請參 [閱資產擷取概觀](/help/assets/asset-microservices-overview.md)。
   * 直接二進位 [存取的資產上傳](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access)。
   * 如需技術詳細資訊，請參 [閱直接二進位上傳通訊協定和API](/help/assets/developer-reference-material-apis.md#overview-binary-upload)。
* 舊版 AEM 已不提供預設的工作流程 **[!UICONTROL DAM Asset Update]**。相反，資產微服務提供可擴充、可立即使用的服務，涵蓋大部分預設資產處理（轉譯、中繼資料擷取、文字擷取以建立索引）。
   * 請參 [閱配置和使用資產微服務](/help/assets/asset-microservices-configure-and-use.md)
   * 若要在處理中自訂工作流程步驟， [可使用後處理工](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) 作流程。
* Assets that come in via Package Manager require manual reprocessing using the **[!UICONTROL Reprocess Asset]** action in the Assets interface.

使用資產微服務產生的標準轉譯會以向後相容的方式儲存在資產儲存庫節點中（相同的命名慣例）。

## 開發和測試資產微型服務 {#asset-microservices}

資產微服務使用雲端服務提供資產的可擴充且彈性化處理。 Adobe管理雲端服務，以最佳化處理不同的資產類型和處理選項。 Asset microservices可協助您避免需要協力廠商轉換工具和方法（例如ImageMagick）並簡化組態，同時為一般檔案類型提供現成可用的功能。 您現在可以處 [理多種檔案類型](/help/assets/file-format-support.md) ，其中包含比舊版Experience Manager更多的現成格式。 例如，PSD和PSB格式的縮圖擷取現在可能是先前需要的協力廠商解決方案（例如ImageMagick）。 處理配置檔案配置不能使用ImageMagick的復 [!UICONTROL 雜配置] 。 此外，還可 [!DNL Dynamic Media] 用於FFmpeg視訊轉碼。

Asset Microservices是雲端原生服務，會在Cloud Manager中管理的客戶程式和環境中自動布建並連線至Experience Manager。 若要擴充或自訂Experience Manager，開發人員可以使用現有內容或資產與在雲端環境中產生的轉譯，以測試並驗證其程式碼，使用、顯示、下載資產。

若要對程式碼和程式進行端對端驗證，包括資產擷取和處理，請使用管道將程式碼變更部署至雲端開發環境，並完整執行資產微服務處理 [](/help/implementing/cloud-manager/configure-pipeline.md) ，進行測試。

## 移除傳統 UI {#classic-ui}

Experience Manager中不再以雲端服務的形式提供傳統UI。 標準介面是可觸控的UI。
