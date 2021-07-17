---
title: ' [!DNL Assets]的開發者引用'
description: '[!DNL Assets] APIs and developer reference content lets you manage assets, including binary files, metadata, renditions, comments, and [!DNL Content Fragments]。'
contentOwner: AG
feature: API,Assets HTTP API
role: Developer,Architect,Admin
exl-id: c75ff177-b74e-436b-9e29-86e257be87fb
source-git-commit: 3051475d20d5b534b74c84f9d541dcaf1a5492f9
workflow-type: tm+mt
source-wordcount: '1436'
ht-degree: 1%

---

# [!DNL Adobe Experience Manager Assets] 開發人員使用案例、API和參考資料 {#assets-cloud-service-apis}

本文包含[!DNL Assets]作為[!DNL Cloud Service]的開發人員的建議、參考資料和資源。 其中包含新的資產上傳模組、API參考，以及後置處理工作流程中所提供支援的相關資訊。

## [!DNL Experience Manager Assets] API與操作 {#use-cases-and-apis}

[!DNL Assets] as a提供 [!DNL Cloud Service] 數個API，以程式設計方式與數位資產互動。每個API都支援特定使用案例，如下表所述。 [!DNL Assets]用戶介面、[!DNL Experience Manager]案頭應用程式和[!DNL Adobe Asset Link]支援所有或部分操作。

>[!CAUTION]
>
>有些API仍然存在，但不受主動支援(以×表示)。 請盡可能勿使用這些API。

| 支援層級 | 說明 |
| ------------- | --------------------------- |
| ✓ | 支援 |
| × | 不支援. 請勿使用。 |
| - | 不可用 |

| 使用案例 | [aem-upload](https://github.com/adobe/aem-upload) | [Experience Manager/ Sling / ](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/index.html) JCRJava API | [Asset compute服務](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html) | [[!DNL Assets] HTTP API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html#create-an-asset) | Sling [GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) / [POST](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html) servlet | [GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) _（預覽）_ |
| ----------------|:---:|:---:|:---:|:---:|:---:|:---:|
| **原始二進位** |  |  |  |  |  |  |
| 建立原始 | ✓ | × | - | × | × | - |
| 讀取原始 | - | × | ✓ | ✓ | ✓ | - |
| 更新原始 | ✓ | × | ✓ | × | × | - |
| 刪除原始 | - | ✓ | - | ✓ | ✓ | - |
| 複製原始 | - | ✓ | - | ✓ | ✓ | - |
| 移動原始 | - | ✓ | - | ✓ | ✓ | - |
| **中繼資料** |  |  |  |  |  |  |
| 建立中繼資料 | - | ✓ | ✓ | ✓ | ✓ | - |
| 讀取中繼資料 | - | ✓ | - | ✓ | ✓ | - |
| 更新中繼資料 | - | ✓ | ✓ | ✓ | ✓ | - |
| 刪除中繼資料 | - | ✓ | ✓ | ✓ | ✓ | - |
| 複製中繼資料 | - | ✓ | - | ✓ | ✓ | - |
| 移動中繼資料 | - | ✓ | - | ✓ | ✓ | - |
| **內容片段(CF)** |  |  |  |  |  |  |
| 建立CF | - | ✓ | - | ✓ | - | - |
| 讀取CF | - | ✓ | - | ✓ | - | ✓ |
| 更新CF | - | ✓ | - | ✓ | - | - |
| 刪除CF | - | ✓ | - | ✓ | - | - |
| 複製CF | - | ✓ | - | ✓ | - | - |
| 移動CF | - | ✓ | - | ✓ | - | - |
| **版本** |  |  |  |  |  |  |
| 建立版本 | ✓ | ✓ | - | - | - | - |
| 讀取版本 | - | ✓ | - | - | - | - |
| 刪除版本 | - | ✓ | - | - | - | - |
| **資料夾** |  |  |  |  |  |  |
| 建立資料夾 | ✓ | ✓ | - | ✓ | - | - |
| 讀取資料夾 | - | ✓ | - | ✓ | - | - |
| 刪除資料夾 | ✓ | ✓ | - | ✓ | - | - |
| 複製資料夾 | ✓ | ✓ | - | ✓ | - | - |
| 移動資料夾 | ✓ | ✓ | - | ✓ | - | - |

## 資產上傳 {#asset-upload}

在[!DNL Experience Manager]中，以[!DNL Cloud Service]的形式使用HTTP API將資產直接上傳至雲端儲存空間。 上傳二進位檔案的步驟如下。 在外部應用程式中執行這些步驟，而不是在[!DNL Experience Manager] JVM中執行。

1. [提交HTTP要求](#initiate-upload)。它會通知[!DNL Experience Manage]r部署您上傳新二進位檔的目的。
1. [將二進位檔的內](#upload-binary) 容PUT到啟動請求提供的一個或多個URI。
1. [提交HTTP](#complete-upload) 請求，通知伺服器已成功上傳二進位檔的內容。

![直接二進位上傳通訊協定概述](assets/add-assets-technical.png)

>[!IMPORTANT]
在外部應用程式中而不是在[!DNL Experience Manager] JVM中執行上述步驟。

此方法提供可擴充且效能更高的資產上傳處理功能。 與[!DNL Experience Manager] 6.5相比的差異如下：

* 二進位檔不會通過[!DNL Experience Manager]，現在只是將上傳程式與為部署設定的二進位雲端儲存空間進行協調。
* 二進位雲端儲存空間可與內容傳遞網路(CDN)或邊緣網路搭配使用。 CDN會選取離用戶端較近的上傳端點。 當資料傳至附近端點的距離較短時，上傳效能和使用者體驗會有所改善，尤其是針對分散於不同地理位置的團隊。

>[!NOTE]
請參閱用戶端程式碼，在開放原始碼[aem-upload library](https://github.com/adobe/aem-upload)中實作此方法。

### 起始上傳 {#initiate-upload}

將HTTPPOST請求提交至所需的資料夾。 資產會在此資料夾中建立或更新。 納入選取器`.initiateUpload.json`以指出要求是起始上傳二進位檔案。 例如，應建立資產的資料夾路徑為`/assets/folder`。 POST請求為`POST https://[aem_server]:[port]/content/dam/assets/folder.initiateUpload.json`。

請求內文的內容類型應為`application/x-www-form-urlencoded`表單資料，包含下列欄位：

* `(string) fileName`: 必要. [!DNL Experience Manager]中顯示的資產名稱。
* `(number) fileSize`: 必要. 上傳資產的檔案大小（以位元組為單位）。

只要每個二進位檔都包含必要欄位，就可以使用單一請求來起始多個二進位檔的上傳。 如果成功，要求會以`201`狀態代碼和內含JSON資料的內文，以下列格式回應：

```json
{
    "completeURI": "(string)",
    "folderPath": (string)",
    "files": [
        {
            "fileName": "(string)",
            "mimeType": "(string)",
            "uploadToken": "(string)",
            "uploadURIs": [
                "(string)"
            ]
        }
    ]
}
```

* `completeURI` （字串）:當二進位檔完成上傳時，呼叫此URI。URI可以是絕對URI或相對URI，客戶端應能夠處理它們。 也就是說，值可以是`"https://[aem_server]:[port]/content/dam.completeUpload.json"`或`"/content/dam.completeUpload.json"`請參閱[complete upload](#complete-upload)。
* `folderPath` （字串）:上傳二進位檔的資料夾完整路徑。
* `(files)` （陣列）:元素清單，其長度和順序與起始請求中提供的二進位資訊清單的長度和順序相匹配。
* `fileName` （字串）:相應二進位的名稱，如起始請求中提供。此值應包含在完成請求中。
* `mimeType` （字串）:相應二進位的mime類型，如起始請求中提供。此值應包含在完成請求中。
* `uploadToken` （字串）:對應二進位的上傳代號。此值應包含在完成請求中。
* `uploadURIs` （陣列）:字串的清單，其值是應將二進位檔內容上傳到的完整URI(請參閱上 [傳二進位檔](#upload-binary))。
* `minPartSize` （數字）:如果有多個URI，則可提供給任何一個URI的資料的最 `uploadURIs`小長度（以位元組為單位）。
* `maxPartSize` （數字）:如果有多個URI，則可提供給任何一個URI的資料的 `uploadURIs`最大長度（以位元組為單位）。

### 上傳二進位檔 {#upload-binary}

啟動上載的輸出包括一個或多個上載URI值。 如果提供了多個URI，則客戶端將二進位檔分割為多個部分，並按順序向每個URI發出每個部分的PUT請求。 使用所有URI。 確保每個部件的大小在初始響應中指定的最小和最大大小範圍內。 CDN邊緣節點有助於加速請求上傳二進位檔。

實現此目的的可能方法是根據API提供的上傳URI數量計算零件大小。 例如，假設二進位檔的總大小為20,000位元組，而上傳URI的數量為2。 然後，請依照下列步驟操作：

* 通過總大小除以URI數來計算零件大小：20,000 / 2 = 10,000。
* POST位元組範圍0-9,999到上載URI清單中的第一個URI。
* POST位元組範圍10,000 - 19,999（二進位元組至上傳URI清單中的第二個URI）。

如果上傳成功，伺服器會以`201`狀態代碼回應每個請求。

### 完成上傳 {#complete-upload}

上傳二進位檔案的所有部分後，請將HTTPPOST請求提交到啟動資料提供的完整URI。 請求內文的內容類型應為`application/x-www-form-urlencoded`表單資料，包含下列欄位。

| 欄位 | 類型 | 必要或非 | 說明 |
|---|---|---|---|
| `fileName` | 字串 | 必要 | 資產名稱，如啟動資料所提供。 |
| `mimeType` | 字串 | 必要 | 二進位檔的HTTP內容類型，如啟動資料所提供。 |
| `uploadToken` | 字串 | 必要 | 如啟動資料所提供，上傳二進位的代號。 |
| `createVersion` | 布林值 (Boolean) | 可選 | 如果`True`且資產存在指定名稱，則[!DNL Experience Manager]會建立資產的新版本。 |
| `versionLabel` | 字串 | 可選 | 如果已建立新版本，則與資產新版本相關聯的標籤。 |
| `versionComment` | 字串 | 可選 | 如果建立了新版本，則與該版本關聯的注釋。 |
| `replace` | 布林值 (Boolean) | 可選 | 如果`True`且資產存在指定名稱， [!DNL Experience Manager]會刪除資產並重新建立。 |

>[!NOTE]
如果資產存在且未指定`createVersion`或`replace`，則[!DNL Experience Manager]會使用新二進位檔更新資產的目前版本。

與起始程式一樣，完成請求資料可能包含多個檔案的資訊。

上傳二進位檔的程式要等到為該檔案叫用完整URL後，才會完成。 上傳程式完成後會處理資產。 即使資產的二進位檔案已完整上傳，但上傳程式尚未完成，處理也不會開始。 如果上傳成功，伺服器會以`200`狀態代碼回應。

### 開放原始碼上傳程式庫 {#open-source-upload-library}

若要進一步了解上傳演算法或建立專屬的上傳指令碼和工具，Analytics提供開放原始碼程式庫和工具：

* [開放原始碼aem上傳程式庫](https://github.com/adobe/aem-upload)。
* [開放原始碼命令列工具](https://github.com/adobe/aio-cli-plugin-aem)。

### 汰除的資產上傳API {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below. -->

只有[!DNL Adobe Experience Manager]作為[!DNL Cloud Service]支援新的上傳方法。 來自[!DNL Adobe Experience Manager] 6.5的API已淘汰。 下列API中會淘汰與上傳或更新資產或轉譯（任何二進位上傳）相關的方法：

* [Experience Manager資產HTTP API](mac-api-assets.md)
* `AssetManager` Java API，例如  `AssetManager.createAsset(..)`

>[!MORELIKETHIS]
* [開放原始碼aem上傳程式庫](https://github.com/adobe/aem-upload)。
* [開放原始碼命令列工具](https://github.com/adobe/aio-cli-plugin-aem)。


## 資產處理與後續處理工作流程 {#post-processing-workflows}

在[!DNL Experience Manager]中，資產處理是以使用[資產微服務](asset-microservices-configure-and-use.md#get-started-using-asset-microservices)的&#x200B;**[!UICONTROL 處理設定檔]**&#x200B;組態為基礎。 處理程式不需要開發人員擴充功能。

若要進行後置處理工作流程設定，請使用具有擴充功能的標準工作流程及自訂步驟。

## 支援後置處理工作流程中的工作流程步驟 {#post-processing-workflows-steps}

如果您從舊版[!DNL Experience Manager]升級，可以使用資產微服務來處理資產。 雲端原生資產微服務的設定和使用更簡單。 不支援舊版[!UICONTROL DAM更新資產]工作流程中使用的一些工作流程步驟。 如需支援類別的詳細資訊，請參閱[Java API參考](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/index.html)。

下列技術工作流程模型會由資產微服務取代，或無法取得支援：

* `com.day.cq.dam.cameraraw.process.CameraRawHandlingProcess`
* `com.day.cq.dam.core.process.CommandLineProcess`
* `com.day.cq.dam.pdfrasterizer.process.PdfRasterizerHandlingProcess`
* `com.day.cq.dam.core.process.AddPropertyWorkflowProcess`
* `com.day.cq.dam.core.process.CreateSubAssetsProcess`
* `com.day.cq.dam.core.process.DownloadAssetProcess`
* `com.day.cq.dam.word.process.ExtractImagesProcess`
* `com.day.cq.dam.word.process.ExtractPlainProcess`
* `com.day.cq.dam.ids.impl.process.IDSJobProcess`
* `com.day.cq.dam.indd.process.INDDMediaExtractProcess`
* `com.day.cq.dam.indd.process.INDDPageExtractProcess`
* `com.day.cq.dam.core.impl.lightbox.LightboxUpdateAssetProcess`
* `com.day.cq.dam.pim.impl.sourcing.upload.process.ProductAssetsUploadProcess`
* `com.day.cq.dam.core.process.SendDownloadAssetEmailProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.StartTrainingProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.TransferTrainingDataProcess`
* `com.day.cq.dam.switchengine.process.SwitchEngineHandlingProcess`
* `com.day.cq.dam.core.process.GateKeeperProcess`
* `com.day.cq.dam.s7dam.common.process.DMEncodeVideoWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.DeleteImagePreviewProcess`
* `com.day.cq.dam.video.FFMpegTranscodeProcess`
* `com.day.cq.dam.core.process.ThumbnailProcess`
* `com.day.cq.dam.video.FFMpegThumbnailProcess`
* `com.day.cq.dam.core.process.CreateWebEnabledImageProcess`
* `com.day.cq.dam.core.process.CreatePdfPreviewProcess`
* `com.day.cq.dam.s7dam.common.process.VideoUserUploadedThumbnailProcess`
* `com.day.cq.dam.s7dam.common.process.VideoThumbnailDownloadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoProxyServiceProcess`
* `com.day.cq.dam.scene7.impl.process.Scene7UploadProcess`
* `com.day.cq.dam.s7dam.common.process.S7VideoThumbnailProcess`
* `com.day.cq.dam.core.process.MetadataProcessorProcess`
* `com.day.cq.dam.core.process.AssetOffloadingProcess`
* `com.adobe.cq.dam.dm.process.workflow.DMImageProcess`

<!-- Commenting the previous list documented at the time of GA. Replacing it with the updated list via cqdoc-18231.

* `com.day.cq.dam.core.process.DeleteImagePreviewProcess`
* `com.day.cq.dam.s7dam.common.process.DMEncodeVideoWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.GateKeeperProcess`
* `com.day.cq.dam.core.process.AssetOffloadingProcess`
* `com.day.cq.dam.core.process.MetadataProcessorProcess`
* `com.adobe.cq.dam.dm.process.workflow.DMImageProcess`
* `com.day.cq.dam.s7dam.common.process.S7VideoThumbnailProcess`
* `com.day.cq.dam.scene7.impl.process.Scene7UploadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoProxyServiceProcess`
* `com.day.cq.dam.s7dam.common.process.VideoThumbnailDownloadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoUserUploadedThumbnailProcess`
* `com.day.cq.dam.core.process.CreatePdfPreviewProcess`
* `com.day.cq.dam.core.process.CreateWebEnabledImageProcess`
* `com.day.cq.dam.video.FFMpegThumbnailProcess`
* `com.day.cq.dam.core.process.ThumbnailProcess`
* `com.day.cq.dam.cameraraw.process.CameraRawHandlingProcess`
* `com.day.cq.dam.core.process.CommandLineProcess`
* `com.day.cq.dam.pdfrasterizer.process.PdfRasterizerHandlingProcess`
* `com.day.cq.dam.core.process.AddPropertyWorkflowProcess`
* `com.day.cq.dam.core.process.CreateSubAssetsProcess`
* `com.day.cq.dam.core.process.DownloadAssetProcess`
* `com.day.cq.dam.word.process.ExtractImagesProcess`
* `com.day.cq.dam.word.process.ExtractPlainProcess`
* `com.day.cq.dam.video.FFMpegTranscodeProcess`
* `com.day.cq.dam.ids.impl.process.IDSJobProcess`
* `com.day.cq.dam.indd.process.INDDMediaExtractProcess`
* `com.day.cq.dam.indd.process.INDDPageExtractProcess`
* `com.day.cq.dam.core.impl.lightbox.LightboxUpdateAssetProcess`
* `com.day.cq.dam.pim.impl.sourcing.upload.process.ProductAssetsUploadProcess`
* `com.day.cq.dam.core.process.ScheduledPublishBPProcess`
* `com.day.cq.dam.core.process.ScheduledUnPublishBPProcess`
* `com.day.cq.dam.core.process.SendDownloadAssetEmailProcess`
-->

<!-- PPTX source: slide in add-assets.md - overview of direct binary upload section of 
https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

>[!MORELIKETHIS]
* [[!DNL Experience Cloud] as a [!DNL Cloud Service] SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)。

