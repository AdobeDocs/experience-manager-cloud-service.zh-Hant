---
title: 開發人員參考 [!DNL Assets]
description: '[!DNL資產] API和開發人員參考內容可讓您管理資產，包括二進位檔案、中繼資料、轉譯、注釋 [!DNL Content Fragments]。'
contentOwner: AG
translation-type: tm+mt
source-git-commit: 8b1cc8af67c6d12d7e222e12ac4ff77e32ec7e0e
workflow-type: tm+mt
source-wordcount: '1236'
ht-degree: 1%

---


# [!DNL Assets] API和開發人員參考資料 {#assets-cloud-service-apis}

文章包含開發人員的Cloud Service參考 [!DNL Assets] 資料和資源。 它包含新的上傳方法、API參考，以及後處理工作流程中提供的支援相關資訊。

## 資產上傳 {#asset-upload-technical}

[!DNL Experience Manager] 雲端服務提供新方法，可將資產上傳至儲存庫。 使用者可使用HTTP API直接將資產上傳至雲端儲存空間。 上傳二進位檔案的步驟如下：

1. [提交HTTP請求](#initiate-upload)。 它通知 [!DNL Experience Manage]或部署您上傳新二進位檔案的意圖。
1. [將二進位格的內容張貼](#upload-binary) ，至啟動請求所提供的一或多個URI。
1. [提交HTTP請求](#complete-upload) ，通知伺服器已成功上傳二進位檔的內容。

![直接二進位上傳通訊協定概觀](assets/add-assets-technical.png)

此方法提供可擴充且效能更高的資產上傳處理。 與 [!DNL Experience Manager] 6.5相比的差異為：

* 二進位檔案不會執行， [!DNL Experience Manager]現在只需將上傳程式與為部署設定的二進位雲端儲存空間進行協調。
* 二進位雲端儲存空間可與內容放送網路(CDN)或Edge網路搭配使用。 CDN選擇更接近用戶端的上傳端點。 當資料傳輸至附近端點的距離較短時，上傳效能和使用者體驗會有所改善，尤其是對於分散各地的團隊而言。

>[!NOTE]
>
>請參閱在開放原始碼 [aem-upload程式庫中實作此方法的用戶端程式碼](https://github.com/adobe/aem-upload)。

### 開始上傳 {#initiate-upload}

將HTTP POST請求提交至所需的資料夾。 資產會在此資料夾中建立或更新。 請加入選 `.initiateUpload.json` 取器，以指出要求是啟動二進位檔案的上傳。 例如，資產應建立所在資料夾的路徑 `/assets/folder`。 POST請求為 `POST https://[aem_server]:[port]/content/dam/assets/folder.initiateUpload.json`。

請求主體的內容類型應為表單資 `application/x-www-form-urlencoded` 料，包含下列欄位：

* `(string) fileName`: 必要. 資產的名稱，如其中所示 [!DNL Experience Manager]。
* `(number) fileSize`: 必要. 要上傳的資產的檔案大小（以位元組為單位）。

只要每個二進位檔包含必要欄位，單一請求就可用來啟動多個二進位檔的上傳。 如果成功，請求會以狀態碼 `201` 和包含下列格式JSON資料的內文回應：

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

* `completeURI` （字串）:當二進位檔完成上傳時，請呼叫此URI。 URI可以是絕對或相對URI，客戶端也可以處理它們。 即，值可以是或查 `"https://author.acme.com/content/dam.completeUpload.json"` 看完 `"/content/dam.completeUpload.json"` 整 [上載](#complete-upload)。
* `folderPath` （字串）:上傳二進位檔案夾的完整路徑。
* `(files)` （陣列）:長度和順序與初始化請求中提供的二進位資訊清單的長度和順序匹配的元素清單。
* `fileName` （字串）:相應二進位檔案的名稱，如啟動請求中提供的。 此值應包含在完整請求中。
* `mimeType` （字串）:相應二進位的MIME類型，如啟動請求中提供。 此值應包含在完整請求中。
* `uploadToken` （字串）:對應二進位碼的上傳Token。 此值應包含在完整請求中。
* `uploadURIs` （陣列）:字串的清單，其值為應上傳二進位檔內容的完整URI(請參 [閱上傳二進位](#upload-binary))。
* `minPartSize` （數字）:如果有多個URI，則可提供給任何一個uploadURI的資料的最小長度（以位元組為單位）。
* `maxPartSize` （數字）:如果有多個URI，則可提供給上載URI中任何一個的資料的最大長度（以位元組為單位）。

### 上傳二進位檔 {#upload-binary}

啟動上載的輸出包括一個或多個上載URI值。 如果提供多個URI，則客戶端將二進位檔案拆分為多個部件，並按順序對每個URI發出POST請求。 使用所有URI。 確保每個部件的大小都在初始響應中指定的最小和最大大小範圍內。 CDN邊緣節點可協助加速要求的二進位檔上傳。

實現此目的的可能方法是根據API提供的上傳URI數量計算零件大小。 例如，假設二進位檔的總大小為20,000位元組，而上傳URI的數目為2。 然後，請遵循下列步驟：

* 通過總大小除以URI數計算零件大小：20,000 / 2 = 10,000。
* 上傳URI清單中第一個URI的二進位元組範圍0-9,999。
* 上傳URI清單中二進位元組到第二個URI的POST位元組範圍10,000 - 19,999。

如果上傳成功，伺服器會以狀態碼回應每個 `201` 請求。

### 完整上傳 {#complete-upload}

在上傳二進位檔案的所有部分後，將HTTP POST要求提交至啟動資料所提供的完整URI。 請求主體的內容類型應為表單資 `application/x-www-form-urlencoded` 料，包含下列欄位。

| 欄位 | 類型 | 必要與否 | 說明 |
|---|---|---|---|
| `fileName` | 字串 | 必要 | 資產名稱，如啟動資料所提供。 |
| `mimeType` | 字串 | 必要 | 二進位檔的HTTP內容類型，如啟動資料所提供。 |
| `uploadToken` | 字串 | 必要 | 上傳二進位碼的Token，如啟動資料所提供。 |
| `createVersion` | 布林值 (Boolean) | 可選 | 如果 `True` 資產具有指定名稱，則會 [!DNL Experience Manager] 建立資產的新版本。 |
| `versionLabel` | 字串 | 可選 | 如果建立了新版本，則與資產新版本相關聯的標籤。 |
| `versionComment` | 字串 | 可選 | 如果已建立新版本，則與該版本關聯的注釋。 |
| `replace` | 布林值 (Boolean) | 可選 | 如果 `True` 資產具有指定名稱，請刪 [!DNL Experience Manager] 除該資產，然後重新建立。 |

>!![NOTE]
如果資產存在且未指 `createVersion` 定或 `replace` 未指定， [!DNL Experience Manager] 則使用新二進位檔更新資產的目前版本。

如同啟動程式，完整的請求資料可能包含多個檔案的資訊。

上傳二進位檔的程式，直到呼叫檔案的完整URL為止。 上傳程式完成後會處理資產。 即使資產的二進位檔案已完全上傳，但上傳程式未完成，處理仍不會開始。

如果成功，伺服器會以狀態代碼 `200` 進行響應。

### 開放原始碼上傳程式庫 {#open-source-upload-library}

若要進一步瞭解上傳演算法或建立您自己的上傳指令碼和工具，Adobe提供開放原始碼程式庫和工具：

* [開放原始碼aem-upload程式庫](https://github.com/adobe/aem-upload)。
* [開放原始碼命令列工具](https://github.com/adobe/aio-cli-plugin-aem)。

### 不建議使用的資產上傳API {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below. -->

新的上傳方法僅支援 [!DNL Adobe Experience Manager] 雲端服務。 6.5版的 [!DNL Adobe Experience Manager] API已過時。 與上傳或更新資產或轉譯（任何二進位上傳）相關的方法在下列API中已過時：

* [Experience Manager Assets HTTP API](mac-api-assets.md)
* `AssetManager` Java API，例如 `AssetManager.createAsset(..)`

>[!MORELIKETHIS]
* [開放原始碼aem-upload程式庫](https://github.com/adobe/aem-upload)。
* [開放原始碼命令列工具](https://github.com/adobe/aio-cli-plugin-aem)。


## 資產處理和後處理工作流程 {#post-processing-workflows}

在中 [!DNL Experience Manager]，資產處理是以使用資產微服務 **[!UICONTROL 的「處理設定檔]** 」設 [定為基礎](asset-microservices-configure-and-use.md#get-started-using-asset-microservices)。 處理程式不需要開發人員擴充功能。

若是後處理工作流程設定，請使用具有自訂步驟擴充功能的標準工作流程。

## 後處理工作流程中的工作流程步驟支援 {#post-processing-workflows-steps}

從舊版升級的客戶可 [!DNL Experience Manager] 以使用資產微服務來處理資產。 雲端原生資產微服務的設定和使用更簡單。 不支援舊版 [!UICONTROL DAM更新資產工作流程中使用的幾個工作流程步驟] 。

[!DNL Experience Manager] 雲端服務支援下列工作流程步驟：

* `com.day.cq.dam.similaritysearch.internal.workflow.process.AutoTagAssetProcess`
* `com.day.cq.dam.core.impl.process.CreateAssetLanguageCopyProcess`
* `com.day.cq.wcm.workflow.process.CreateVersionProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.StartTrainingProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.TransferTrainingDataProcess`
* `com.day.cq.dam.core.impl.process.TranslateAssetLanguageCopyProcess`
* `com.day.cq.dam.core.impl.process.UpdateAssetLanguageCopyProcess`
* `com.adobe.cq.workflow.replication.impl.ReplicationWorkflowProcess`
* `com.day.cq.dam.core.impl.process.DamUpdateAssetWorkflowCompletedProcess`

以下技術工作流程模型會由資產微型服務取代，或是無法提供支援：

* `com.day.cq.dam.core.impl.process.DamMetadataWritebackWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.DeleteImagePreviewProcess`
* `com.day.cq.dam.s7dam.common.process.DMEncodeVideoWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.GateKeeperProcess`
* `com.day.cq.dam.core.process.AssetOffloadingProcess`
* `com.day.cq.dam.core.process.MetadataProcessorProcess`
* `com.day.cq.dam.core.process.XMPWritebackProcess`
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
* `com.day.cq.dam.core.impl.process.SendTransientWorkflowCompletedEmailProcess`

<!-- PPTX source: slide in add-assets.md - overview of direct binary upload section of 
https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

>[!MORELIKETHIS]
* [Experience Cloud即雲端服務SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)。

