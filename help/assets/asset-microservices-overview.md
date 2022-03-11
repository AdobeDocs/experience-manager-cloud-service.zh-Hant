---
title: 使用資產微服務處理資產
description: 使用雲本地和可擴展的資產處理微服務處理您的數字資產。
contentOwner: AG
feature: Asset Compute Microservices,Workflow,Release Information,Asset Processing
role: Architect,Admin
exl-id: 1e069b95-a018-40ec-be01-9a74ed883b77
source-git-commit: 4be76f19c27aeab84de388106a440434a99a738c
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 2%

---

# 資產微服務資產接收和處理概述 {#asset-microservices-overview}

Adobe Experience Manager [!DNL Cloud Service] 提供了雲本地方法來利用Experience Manager應用程式和功能。 這一新架構的一個關鍵要素是資產接收和處理，由資產微服務提供支援。 資產微服務使用雲服務提供可擴展且具有彈性的資產處理。 Adobe管理雲服務，以優化對不同資產類型和處理選項的處理。 雲本機資產微服務的主要優勢是：

* 可擴展的體系結構，允許對資源密集型操作進行無縫處理。
* 高效的索引和文本提取，不會影響Experience Manager環境的效能。
* 將工作流處理Experience Manager環境中資產處理的需要降至最低。 這可釋放資源，最大限度地減少Experience Manager負載，並提供可擴充性。
* 提高資產處理的恢復力。 處理非典型檔案時可能出現的問題（如損壞的檔案或非常大的檔案）不再影響部署的效能。
* 簡化管理員的資產處理配置。
* 資產處理設定由Adobe管理和維護，以提供處理各種檔案類型的格式副本、元資料和文本提取的最知名配置
* 本機Adobe檔案處理服務在適用時使用，提供高保真輸出和 [高效處理Adobe專有格式](file-format-support.md)。
* 能夠配置後處理工作流以添加特定於用戶的操作和整合。

資產微服務有助於避免對第三方渲染工具和方法的需求(例如 [!DNL ImageMagick] 和FFmpeg轉碼)，並簡化配置，同時在預設情況下為通用檔案格式提供基本功能。

## 高級體系結構 {#asset-microservices-architecture}

高級體系結構圖描述了整個系統中資產接收、處理和資產流的關鍵要素。

<!-- Proposed DRAFT diagram for asset microservices overview - see section "Asset processing - high-level diagram" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![利用資產微服務進行資產接收和處理](assets/asset-microservices-overview.png "利用資產微服務進行資產接收和處理")

使用資產微服務接收和處理的關鍵步驟是：

* 客戶端(如Web瀏覽器或Adobe資產連結)將上載請求發送到 [!DNL Experience Manager] 並開始將二進位檔案直接上傳到二進位雲儲存。
* 當直接二進位上載完成時，客戶端將通知 [!DNL Experience Manager]。
* [!DNL Experience Manager] 向資產微服務發送處理請求。 請求內容取決於中的處理配置檔案配置 [!DNL Experience Manager] 指定要生成的格式副本。
* 資產微服務後端接收該請求，並基於該請求將其分派給一個或多個微服務。 每個微服務直接從二進位雲儲存中訪問原始二進位。
* 處理結果（如格式副本）儲存在二進位雲儲存中。
* Experience Manager會通知處理已完成，並有指向生成的二進位檔案（格式副本）的直接指針。 生成的格式副本可在 [!DNL Experience Manager] 上載的資產。

這是資產消化處理的基本流程。 如果配置，Experience Manager還可以啟動自定義工作流模型以對資產進行後處理。 例如，執行特定於您的環境的自定義步驟，例如從企業系統獲取資訊並添加到資產屬性。

接收和處理流是資產微服務體系結構的關鍵概念，用於Experience Manager。

* **直接二進位訪問**:一旦為Experience Manager環境配置，資產就會被傳輸（並上傳）到雲二進位儲存 [!DNL Experience Manager]、資產微服務，最終讓客戶直接訪問他們進行工作。 這將減少網路負載和儲存二進位檔案的複製
* **外部化處理**:資產處理於境外完成 [!DNL Experience Manager] 並節省其資源（CPU、記憶體），用於為最終用戶提供關鍵數字資產管理(DAM)功能並支援與系統交互工作

## 具有直接二進位訪問的資產上載 {#asset-upload-with-direct-binary-access}

Experience Manager客戶端是產品產品的一部分，預設情況下，所有客戶端都支援直接二進位訪問。 這包括使用Web介面上載、Adobe資產連結和 [!DNL Experience Manager] 案頭應用。

您可以使用直接與 [!DNL Experience Manager] HTTP API。 您可以直接使用這些API，或者使用和擴展以下實現上載協定的開源項目：

* [開源上載庫](https://github.com/adobe/aem-upload)
* [開源命令行工具](https://github.com/adobe/aio-cli-plugin-aem)

有關詳細資訊，請參見 [上載資產](add-assets.md)。

## 添加自定義資產後處理 {#add-custom-asset-post-processing}

雖然大多數客戶應該從可配置的資產微服務獲得其所有資產處理需求，但有些客戶可能需要額外的資產處理。 如果資產需要根據通過整合從其他系統獲取的資訊進行處理，則情況尤其如此。 在這樣的情況下，可以使用自定義的後處理工作流。

後處理工作流是常規的 [!DNL Experience Manager] 工作流模型，在中建立和管理 [!DNL Experience Manager] 工作流編輯器。 客戶可以配置工作流以對資產執行附加處理步驟，包括使用可用的現成工作流步驟和自定義工作流。

Adobe Experience Manager可以配置為在資產處理完成後自動觸發後處理工作流。

<!-- TBD asgupta, Engg: Create some asset-microservices-data-flow-diagram.
-->

>[!MORELIKETHIS]
>
>* [開始使用資產微服務](asset-microservices-configure-and-use.md)
>* [支援的檔案格式](file-format-support.md)
>* [Adobe資產連結](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html)
>* [[!DNL Experience Manager] 桌面應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html)
>* [Apache Oak直接二進位訪問文檔](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html)

