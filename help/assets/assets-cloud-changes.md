---
title: Adobe Experience Manager資產雲端服務的顯著變更
description: AEM Cloud服務中的Adobe Experience Manager Assets與Adobe Experience Manager 6.5相比有顯著變更。
translation-type: tm+mt
source-git-commit: ab79c3dabb658e242df08ed065ce99499c9b7357

---


# Notable changes to Experience Manager Assets as a Cloud Service {#notable-changes}

Adobe Experience Manager即雲端服務，為您的AEM專案帶來許多新功能與可能。 但是，與Experience Manager雲端服務相比，Experience Manager Assets的內部部署或Adobe Managed Service之間有許多不同。 本文件主要說明這些重要差異。

>[!NOTE]
>
>本檔案著重說明Experience Manager Assets（即雲端服務）所特有的顯著變更。 將Experience Manager的一 [般變更視為雲端服務](/help/release-notes/aem-cloud-changes.md)。

與Experience Manager 6.5相比，主要差異在於：

* [資產擷取](#asset-ingestion)
* [移除傳統 UI](#classic-ui)

## 資產擷取 {#asset-ingestion}

資產上傳已最佳化，因為可以更佳地縮放資產擷取，並加快上傳速度。 產品功能（網路使用者介面、案頭用戶端）已更新。 不過，這可能會影響到一些現有的自訂。

* Experience Manager使用直接二進位存取原則來上傳和下載資產，並使用資產微服務來處理資產。 請參 [閱資產擷取概觀](/help/assets/asset-microservices-overview.md)。
   * 直接二進位 [存取的資產上傳](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access)。
   * 如需技術詳細資訊，請參 [閱直接二進位上傳通訊協定和API](/help/assets/developer-reference-material-apis.md#overview-binary-upload)。
* 舊版 AEM 已不提供預設的工作流程 **[!UICONTROL DAM Asset Update]**。相反，資產微服務提供可擴充、可立即使用的服務，涵蓋大部分預設資產處理（轉譯、中繼資料擷取、文字擷取以建立索引）。
   * 請參 [閱配置和使用資產微服務](/help/assets/asset-microservices-configure-and-use.md)
   * 若要在處理中自訂工作流程步驟， [可使用後處理工](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) 作流程。
* Assets that come in via Package Manager require manual reprocessing using the **[!UICONTROL Reprocess Asset]** action in the Assets interface.

使用資產微服務產生的標準轉譯會以向後相容的方式儲存在資產儲存庫節點中（相同的命名慣例）。

## 開發和測試資產微型服務 {#developing-testing-asset-microservices}

Asset Microservices是原生雲端服務，可在Cloud Manager中管理的客戶程式和環境中自動布建並連線至Experience Manager。 負責擴充Experience Manager或進行自訂的開發人員可使用現有內容（或包含雲端環境中產生之轉譯的資產）來測試並驗證其程式碼，使用、顯示、下載資產。

若要對程式碼和程式進行端對端驗證，包括資產擷取和處理，請使用管道將程式碼變更部署至雲端開發環境，並完整執行資產微服務處理來進行測試。

## 移除傳統 UI {#classic-ui}

Experience Manager中不再以雲端服務的形式提供傳統UI。
