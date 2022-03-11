---
title: 在 [!DNL Adobe Experience Manager Assets] 作為 [!DNL Cloud Service]
description: 對 [!DNL Adobe Experience Manager Assets] 在 [!DNL Experience Manager] 作為 [!DNL Cloud Service] 與 [!DNL Adobe Experience Manager] 6.5
feature: Release Information
role: User,Leader,Architect,Admin
exl-id: 93e7dbcd-016e-4ef2-a1cd-c554efb5ad34
source-git-commit: fe662a515a52bcf4648585366422064edce1a7fd
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 6%

---

# 對 [!DNL Experience Manager Assets] 作為 [!DNL Cloud Service] {#notable-changes}

[!DNL Adobe Experience Manager] 作為 [!DNL Cloud Service] 為管理您的Experience Manager項目帶來了許多新功能和可能性。 兩者之間有很多不同 [!DNL Experience Manager Assets] 本地或托管為Adobe托管服務，與 [!DNL Experience Manager] 作為 [!DNL Cloud Service]。 本文著重介紹了在 [!DNL Assets] 功能。

主要差異為 [!DNL Experience Manager] 6.5在以下方面：

* [資產接收、上載和處理](#asset-ingestion)。
* [用於雲本機處理的資產微服務](#asset-microservices)。
* [移除傳統 UI](#classic-ui).

## 資產接收、處理和分配 {#asset-ingestion-distribution}

資產上載通過實現更好的接收擴展、更快的上載、使用微服務更快的處理和批量接收而優化，以提高效率。 產品功能（Web用戶介面、案頭客戶端）將更新。 此外，這可能會影響一些現有的自定義。

* [!DNL Experience Manager] 使用直接二進位訪問原則上載和下載資產，使用資產微服務處理資產。 請參閱 [微服務概述](/help/assets/asset-microservices-overview.md)。
   * 資產上載 [直接二進位訪問](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access)。
   * 有關技術詳細資訊，請參閱 [直接二進位上載協定和API](/help/assets/developer-reference-material-apis.md#upload-binary)。
   * 有關基本CRUD操作的可用API方法的比較，請參見 [API和資產操作](/help/assets/developer-reference-material-apis.md#use-cases-and-apis)。
* 舊版 已不提供預設的工作流程 **[!UICONTROL DAM Asset Update]**。[!DNL Experience Manager]相反，資產微服務提供了可擴展、隨時可用的服務，涵蓋大部分預設資產處理（格式副本、元資料提取和用於索引的文本提取）。
   * 請參閱 [配置和使用資產微服務](/help/assets/asset-microservices-configure-and-use.md)
   * 要在處理中執行自定義工作流步驟， [後處理工作流](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) 可使用。

* 提供二進位檔案而不進行任何轉換的網站元件可以使用直接下載。 SlingGETServlet將更新，以使開發人員在預設情況下執行此操作。 提供帶有某些轉換的二進位檔案的網站元件（例如，通過servlet調整其大小）可以繼續按原樣運行。

使用資產微服務生成的標準格式副本使用相同的命名約定以向後相容的方式儲存在資產儲存庫節點中。

## 開發和test資產微型服務 {#asset-microservices}

資產微服務使用雲服務提供可擴展且具有彈性的資產處理。 Adobe管理雲服務，以優化對不同資產類型和處理選項的處理。 資產微服務有助於避免對第三方渲染工具和方法的需求(例如 [!DNL ImageMagick])和簡化配置，同時為常見檔案類型提供現成功能。 現在可以處理 [各種檔案類型](/help/assets/file-format-support.md) 與以前版本的Experience Manager相比，可涵蓋更多的開箱即用格式。 例如，現在可以對PSD和PSB格式進行縮略提取，以前需要第三方解決方案，如 [!DNL ImageMagick]。 不能使用 [!DNL ImageMagick] 為 [!UICONTROL 處理配置檔案] 配置。 使用 [!DNL Dynamic Media] 用於視頻的高級FFmpeg轉碼和使用處理配置檔案 [MP4視頻的基本轉碼](/help/assets/manage-video-assets.md#transcode-video)。

資產微服務是一種雲本地服務，可自動配置並連接到 [!DNL Experience Manager] 在Cloud Manager中管理的客戶程式和環境中。 擴展或自定義 [!DNL Experience Manager]，開發人員可以使用在雲環境中生成的格式副本的現有內容或資產，使用、顯示和下載資產test和驗證其代碼。

要對代碼和流程（包括資產接收和處理）進行端到端驗證，請使用 [管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) test，全面執行資產微服務處理。

## 功能奇偶校驗 [!DNL Experience Manager] 6.5 {#cloud-service-feature-status}

[!DNL Experience Manager] 作為 [!DNL Cloud Service] 為現有功能引入了許多新功能和更多效能方法。 但是，從 [!DNL Experience Manager] 6.5至 [!DNL Experience Manager] 作為 [!DNL Cloud Service]，您可能會注意到某些功能的工作方式不同、不可用或部分可用。 以下是這些功能的清單。 此外，請參見 [不建議使用和刪除的功能](/help/release-notes/deprecated-removed-features.md)。

| 功能或使用案例 | 狀態 [!DNL Experience Manager] 作為 [!DNL Cloud Service] | 評論 |
|-----|-----|-----|
| [重複資產檢測](/help/assets/manage-digital-assets.md#detect-duplicate-assets) | 工作方式不同 | 請參閱 [它是如何運作的 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html)。 |
| [僅用於放置(FPO)格式副本](/help/assets/configure-fpo-renditions.md) | 工作方式不同 | 處理配置檔案使用資產微服務生成FPO格式副本。 在Experience Manager6.5中，第三方解決方案，如 [!DNL ImageMagick] 可用於生成格式副本。 |
| 元資料寫回 | 工作方式不同 | 預設為停用. 如果需要，啟用相應的工作流啟動程式。 寫回由資產微服務處理。 |
| 使用包管理器上載的資產的處理 | 需要手動干預 | 使用 **[!UICONTROL 重新處理資產]** 操作。 |
| MIME類型檢測 | 不支援. | 如果您上載的數字資產沒有副檔名或副檔名不正確，則可能不會根據需要進行處理。 用戶仍可以在DAM中不帶副檔名地儲存二進位檔案。 請參閱 [MIME類型檢測 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/detect-asset-mime-type-with-tika.html)。 |
| 複合資產的子集生成 | 不支援. | 注釋等從屬使用案例可能無法完成。 請參閱 [子集建立 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-linked-subassets.html#generate-subassets)。 PDF可以開始預覽某些檔案類型 [2021.7.0版](/help/release-notes/release-notes-cloud/release-notes-current.md)。 |
| 編輯影像 | 不支援 | 在Experience Manageras a Cloud Service中不支援編輯資產。 請參閱 [它在6.5Experience Manager中的作用](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#editing-images)。 |
| 首頁 | 不支援 | 請參閱 [[!DNL Assets] Home Page experience in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-home-page.html) |
| 從ZIP存檔提取資產 | 不支援 | 請參閱 [ZIP提取 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#extractzip)。 |
| 資產評級 | 不支援 | 不支援元資料架構編輯器中的評級構件。 |
| 內容處置篩選器 | 不支援 | 常用的使用案例 `ContentDispositionFilter` 是讓管理員配置 [!DNL Experience Manager] 提供HTML檔案，並以內聯方式開啟PDF檔案，而不是下載這些檔案。 在「發佈」實例上，您可以使用Dispatcher配置管理處置。 在「作者」實例上，Adobe不建議修改「內容處置」標題。 請參閱 [中的內容處置篩選器 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/content-disposition-filter.html)。 |
| [下載報告](/help/assets/asset-reports.md) | 不支援 | 目前，下載報告中的資產使用資訊不可用。 請參閱 [下載報表 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/asset-reports.html)。 |
| 產品照片模板 | 不支援 | 請參閱 [產品照片模板 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/projects/managing-product-information.html)。 |
| 智慧翻譯 | 不支援 | [智慧翻譯](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/translation/smart-translation-search-feature-video-use.html) 不支援 [!DNL Experience Manager] 作為 [!DNL Cloud Service]。 |
| WebDAV | 不支援 | 有關替代方案，請參見 [[!DNL Creative Cloud] 整合](/help/assets/aem-cc-integration-best-practices.md) 或 [顯影劑參考材料](/help/assets/developer-reference-material-apis.md)。 |
| 傳統 UI | 不支援 | 只有啟用觸摸的用戶介面可用。 |

>[!MORELIKETHIS]
>
>以下資源可用於 [!DNL Experience Manager] 作為 [!DNL Cloud Service]:
>
>* [已棄用和已刪除功能清單](/help/release-notes/deprecated-removed-features.md)
>* [簡介](/help/overview/introduction.md)
>* [新增功能與不同之處](/help/overview/what-is-new-and-different.md)
>* [建築](/help/overview/architecture.md)
>* [重大變更](/help/release-notes/aem-cloud-changes.md)
>* [重大變更 [!DNL Sites]](/help/sites-cloud/sites-cloud-changes.md)
>* [視頻教程](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html)

