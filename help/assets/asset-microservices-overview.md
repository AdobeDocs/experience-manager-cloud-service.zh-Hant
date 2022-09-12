---
title: 使用資產微服務處理資產
description: 使用雲端原生和可擴充的資產處理微服務處理您的數位資產。
contentOwner: AG
feature: Asset Compute Microservices,Workflow,Release Information,Asset Processing
role: Architect,Admin
exl-id: 1e069b95-a018-40ec-be01-9a74ed883b77
source-git-commit: 4be76f19c27aeab84de388106a440434a99a738c
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 3%

---

# 使用資產微服務擷取和處理資產概述 {#asset-microservices-overview}

Adobe Experience Manager as a [!DNL Cloud Service] 提供雲端原生方法，以運用Experience Manager應用程式和功能。 此新架構的其中一項關鍵元素是資產擷取與處理，由資產微服務提供技術支援。 資產微服務使用雲端服務提供資產的可擴充且可復原處理功能。 Adobe管理雲端服務，以最佳處理不同資產類型和處理選項。 雲端原生資產微服務的主要優點為：

* 可擴展的體系結構，允許對資源密集型操作進行無縫處理。
* 有效的索引和文字擷取，不會影響Experience Manager環境的效能。
* 將在Experience Manager環境中處理資產處理所需的工作流程降到最低。 這樣可以釋放資源，最大限度地減少Experience Manager負載，並提供可擴充性。
* 改善資產處理的彈性。 處理非典型檔案（如損壞的檔案或極大的檔案）時可能出現的問題不再影響部署的效能。
* 簡化管理員的資產處理設定。
* Adobe可管理及維護資產處理設定，以提供處理各種檔案類型之轉譯、中繼資料及文字擷取的最已知設定
* 在適用的情況下，使用本機Adobe檔案處理服務，提供高保真輸出， [高效處理Adobe專有格式](file-format-support.md).
* 可設定後置處理工作流程，以新增使用者專屬動作和整合。

資產微服務有助於避免需要協力廠商轉譯工具和方法(例如 [!DNL ImageMagick] 和FFmpeg轉碼)，並簡化設定，同時依預設為通用檔案格式提供基本功能。

## 高級體系結構 {#asset-microservices-architecture}

高階架構圖表可描繪資產擷取、處理以及整個系統中資產流程的關鍵元素。

<!-- Proposed DRAFT diagram for asset microservices overview - see section "Asset processing - high-level diagram" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![使用資產微服務擷取和處理資產](assets/asset-microservices-overview.png "使用資產微服務擷取和處理資產")

使用資產微服務擷取和處理的關鍵步驟為：

* 用戶端(例如網頁瀏覽器或Adobe資產連結)會將上傳請求傳送至 [!DNL Experience Manager] 然後開始將二進位檔案直接上傳至二進位雲端儲存空間。
* 當直接二進位上傳完成時，用戶端會通知 [!DNL Experience Manager].
* [!DNL Experience Manager] 傳送處理要求至資產微服務。 請求內容取決於 [!DNL Experience Manager] 指定，要產生哪些轉譯。
* 資產微服務後端接收請求，根據請求將其分派給一個或多個微服務。 每個微服務直接從二進位雲儲存中訪問原始二進位。
* 處理結果（例如轉譯）會儲存在二進位雲端儲存空間中。
* Experience Manager會收到處理完成的通知，並附上產生二進位檔（轉譯）的直接指標。 產生的轉譯可在 [!DNL Experience Manager] 上傳的資產。

這是資產擷取與處理的基本流程。 如果已設定，Experience Manager也可以啟動自訂工作流程模型，以執行資產的後置處理。 例如，執行您環境專屬的自訂步驟，例如從企業系統擷取資訊並新增至資產屬性。

擷取和處理流程是Experience Manager資產微服務架構的重要概念。

* **直接二進位存取**:一旦為Experience Manager環境設定資產，便會將資產傳輸（並上傳）至雲端二進位存放區，然後 [!DNL Experience Manager]、資產微服務，最後客戶可直接存取資產以執行其工作。 這樣可最大限度地減少網路負載和儲存的二進位檔的重複
* **外部化處理**:資產處理在 [!DNL Experience Manager] 環境，並節省其資源（CPU、記憶體），以提供關鍵數位資產管理(DAM)功能，並支援與系統的互動式工作以供最終用戶使用

## 具有直接二進位存取的資產上傳 {#asset-upload-with-direct-binary-access}

Experience Manager用戶端是產品產品的一部分，預設情況下，所有支援以直接二進位存取方式上傳。 這些包括使用網頁介面上傳、Adobe資產連結，以及 [!DNL Experience Manager] 案頭應用程式。

您可以使用自訂上傳工具，這些工具可直接搭配 [!DNL Experience Manager] HTTP API。 您可以直接使用這些API，或使用和擴充下列實作上傳通訊協定的開放原始碼專案：

* [開放原始碼上傳程式庫](https://github.com/adobe/aem-upload)
* [開放原始碼命令列工具](https://github.com/adobe/aio-cli-plugin-aem)

如需詳細資訊，請參閱 [上傳資產](add-assets.md).

## 新增自訂資產後續處理 {#add-custom-asset-post-processing}

雖然大部分的客戶應該能透過可設定的資產微服務獲得其所有資產處理需求，但有些客戶可能需要額外的資產處理。 如果需要根據透過整合來自其他系統的資訊處理資產，則此情況尤為常見。 在這類情況下，可使用自訂的後置處理工作流程。

後續處理工作流程正常 [!DNL Experience Manager] 工作流模型，在中建立和管理 [!DNL Experience Manager] 工作流程編輯器。 客戶可以設定工作流程以對資產執行其他處理步驟，包括使用可用的現成可用工作流程步驟和自訂工作流程。

Adobe Experience Manager可設定為在資產處理完成後自動觸發後續處理工作流程。

<!-- TBD asgupta, Engg: Create some asset-microservices-data-flow-diagram.
-->

>[!MORELIKETHIS]
>
>* [開始使用資產微服務](asset-microservices-configure-and-use.md)
>* [支援的檔案格式](file-format-support.md)
>* [Adobe資產連結](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html)
>* [[!DNL Experience Manager] 桌面應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html)
>* [直接二進位存取的Apache Oak檔案](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html)

