---
title: 使用資產微服務處理資產
description: 使用雲端原生和可擴展的資產處理微服務來處理您的數位資產。
contentOwner: AG
feature: Asset Compute Microservices, Asset Ingestion, Asset Processing
role: Architect, Admin
exl-id: 1e069b95-a018-40ec-be01-9a74ed883b77
source-git-commit: 9c1104f449dc2ec625926925ef8c95976f1faf3d
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 100%

---

# 使用資產微服務進行資產擷取和處理的概觀 {#asset-microservices-overview}

Adobe Experience Manager as a [!DNL Cloud Service] 提供一種雲端原生方法可使用 Experience Manager 應用程式和功能。這種新架構的關鍵要素之一是由資產微服務提供支援的資產擷取和處理。資產微服務使用雲端服務來提供可擴展和具恢復力的資產處理操作。Adobe 管理雲端服務以對不同的資產類型和處理選項進行最佳處理。雲端原生資產微服務的主要優勢是：

* 可擴展的架構，可無縫處理資源密集型操作。
* 有效率地建立索引和擷取文字，不會影響 Experience Manager 環境的效能。
* 儘量降低對在 Experience Manager 環境中進行資產處理之工作流程的需求。這可以釋放資源，將 Experience Manager 的負荷降至最低，並提供可擴展性。
* 提高資產處理的復原性。處理非典型檔案 (例如損壞的檔案或超大檔案) 時可能會發生問題不會再影響部署效能。
* 為管理員簡化資產處理設定。
* 資產處理設定由 Adobe 管理和維護，以提供大家最熟悉的設定來處理各種檔案類型的轉譯、中繼資料和文字擷取
* 在適合的情況下使用原生 Adobe 檔案處理服務，提供高保真輸出和[有效率處理 Adobe 專屬格式](file-format-support.md)。
* 能夠設定後處理工作流程以新增使用者特定的動作和整合。

資產微服務可讓您不需要協力廠商的呈現工具和方法 (例如 [!DNL ImageMagick] 和 FFmpeg 轉碼)，同時依預設提供適用於常見檔案格式的基本功能。

## 高層架構 {#asset-microservices-architecture}

高層架構描述了資產擷取和處理的關鍵要素，以及資產在系統中的流動。

<!-- Proposed DRAFT diagram for asset microservices overview - see section "Asset processing - high-level diagram" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![使用資產微服務進行資產擷取和處理](assets/asset-microservices-overview.png "使用資產微服務進行資產擷取和處理")

使用資產微服務進行擷取和處理的關鍵步驟是：

* 用戶端 (例如網頁瀏覽器或 Adobe Asset Link) 向 [!DNL Experience Manager] 傳送上傳要求，並開始將二進位檔直接上傳到二進位檔雲端儲存空間。
* 當直接二進位檔上傳完成時，用戶端會通知 [!DNL Experience Manager]。
* [!DNL Experience Manager] 向資產微服務傳送處理要求。要求內容取決於 [!DNL Experience Manager] 中的處理設定檔設定，其指定要產生什麼轉譯。
* 資產微服務後端接收要求，然後根據要求將其分派給一個或多個微服務。每個微服務直接從二進位檔雲端儲存空間存取原始二進位檔。
* 處理結果 (例如轉譯) 儲存在二進位檔雲端儲存空間中。
* Experience Manager 會收到處理已完成的通知，以及指向產生的二進位檔 (轉譯) 的直接指標。為上傳的資產所產生的轉譯可在 [!DNL Experience Manager] 中取得。

這是資產擷取和處理的基本流程。如果已設定，Experience Manager 也可以啟動自訂工作流程模型來對資產進行後處理。例如，執行您環境專屬的自訂步驟，例如從企業系統擷取資訊並新增到資產屬性中。

擷取和處理流程是 Experience Manager 資產微服務架構的關鍵概念。

* **直接二進位檔存取**：針對 Experience Manager 環境設定好資產後，資產將傳輸 (並上傳) 到雲端二進位檔儲存空間，然後是 [!DNL Experience Manager]、資產微服務，最後用戶端可以直接存取資產以執行工作。這會儘可能減少網路負載和所儲存二進檔的重複
* **外部化處理**：資產處理在 [!DNL Experience Manager] 環境之外完成，並節省其資源 (CPU、記憶體) 以提供重要的數位資產管理 (DAM) 功能並支援一般使用者與系統的互動工作

## 直接二進位存取的資產上傳 {#asset-upload-with-direct-binary-access}

Experience Manager 用戶端是產品的一部分，依預設全都支援直接二進位存取的上傳。其中包括使用 Web 介面、Adobe Asset Link 和 [!DNL Experience Manager] 桌面應用程式上傳。

您可以使用自訂上傳工具，這些工具直接與 [!DNL Experience Manager] HTTP API 搭配運作。您可以直接使用這些 API，也可以使用及擴展以下實作上傳通訊協定的開放原始碼專案：

* [開放原始碼上傳庫](https://github.com/adobe/aem-upload)
* [開放原始碼命令列工具](https://github.com/adobe/aio-cli-plugin-aem)

如需詳細資訊，請參閱[上傳資產](add-assets.md)。

## 新增自訂資產後處理 {#add-custom-asset-post-processing}

雖然大部分的客戶應該從可設定的資產微服務中獲得所有資產處理需求，但有些客戶可能需要額外的資產處理。如果資產必須根據其他系統 (透過整合) 的資訊進行處理，就特別需要。在這種情況下，可以使用自訂後處理工作流程。

後處理工作流程是一般 [!DNL Experience Manager] 工作流程模型，在 [!DNL Experience Manager] 工作流程編輯器中建立和管理。客戶可以設定工作流程以對資產執行額外的處理步驟，包括使用立即可用的工作流程步驟和自訂工作流程。

Adobe Experience Manager 可以設定成在資產處理完成後自動觸發後處理工作流程。

<!-- TBD asgupta, Engg: Create some asset-microservices-data-flow-diagram.
-->

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
>* [開始使用資產微服務](asset-microservices-configure-and-use.md)
>* [支援的檔案格式](file-format-support.md)
>* [Adobe Asset Link](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html)
>* [[!DNL Experience Manager] 桌面應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=zh-Hant)
>* [關於直接二進位檔存取的 Apache Oak 文件](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html)
