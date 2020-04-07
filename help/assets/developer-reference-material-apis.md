---
title: 'Adobe Experience Manager雲端服務中用於數位資產管理的資產API '
description: 資產API可讓基本的建立——讀取——更新——刪除(CRUD)操作來管理資產，包括二進位、中繼資料、轉譯、註解和內容片段。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 26833f59f21efa4de33969b7ae2e782fe5db8a14

---


# Assets as a Cloud Service APIs {#assets-cloud-service-apis}

<!-- 
Give a list of and overview of all reference information available.
* New upload method
* Javadocs
* Assets HTTP API documented at [https://helpx.adobe.com/experience-manager/6-5/assets/using/mac-api-assets.html](https://helpx.adobe.com/experience-manager/6-5/assets/using/mac-api-assets.html)

-->

## 資產上傳 {#asset-upload-technical}

Experience Manager雲端服務提供將資產上傳至儲存庫的新方式——將二進位上傳至二進位雲端儲存空間。 本節提供其技術概觀。

### 直接二進位上傳概觀 {#overview-binary-upload}

上傳二進位檔的高階演算法是：

1. 提交HTTP要求，通知AEM上傳新二進位檔的意圖。
1. 將二進位內容發佈到由啟動請求提供的一個或多個URI。
1. 提交HTTP請求，通知伺服器已成功上傳二進位檔的內容。

![直接二進位上傳通訊協定概觀](assets/add-assets-technical.png)

與舊版AEM相較的重要差異包括：

* 二進位檔案不會經過AEM，現在只需將上傳程式與為部署設定的二進位雲端儲存空間進行協調
* 二進位雲端儲存空間由內容傳送網路(CDN,Edge Network)作為前端，可讓上傳端點更接近用戶端，進而協助改善上傳效能和使用者體驗，尤其是針對分散式團隊上傳資產

此方法應提供更具擴充性和效能的資產上傳處理。

> !![NOTE]
若要檢閱實作此方法的用戶端程式碼，請參閱開放原始碼 [aem-upload程式庫](https://github.com/adobe/aem-upload)

### 開始上傳 {#initiate-upload}

第一步是將HTTP POST請求提交到資產應建立或更新的資料夾；包含選擇 `.initiateUpload.json` 器以指出請求是開始二進位上傳。 例如，資產應建立所在資料夾的路徑為 `/assets/folder`:

```
POST https://[aem_server]/content/dam/assets/folder.initiateUpload.json
````

請求主體的內容類型應為表單資 `application/x-www-form-urlencoded` 料，包含下列欄位：

* `(string) fileName`: 必要. 資產在例項中顯示的名稱。
* `(number) fileSize`: 必要. 要上載的二進位檔案的總長度（以位元組為單位）。

只要每個二進位檔包含必要欄位，單一請求就可用來啟動多個二進位檔的上傳。 如果成功，請求會以狀態碼 `201` 和包含下列格式JSON資料的內文回應：

```
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

* `completeURI` （字串）:當二進位檔完成上傳時叫用此URI。 URI可以是絕對或相對URI，客戶端也可以處理它們。 即，值可以是或查 `"https://author.acme.com/content/dam.completeUpload.json"` 看完 `"/content/dam.completeUpload.json"` 整 [上載](#complete-upload)。
* `folderPath` （字串）:上傳二進位檔的資料夾完整路徑。
* `(files)` （陣列）:元素的清單，其長度和順序將與啟動請求中提供的二進位資訊清單的長度和順序相匹配。
* `fileName` （字串）:相應二進位檔案的名稱，如啟動請求中提供的。 此值應包含在完整請求中。
* `mimeType` （字串）:相應二進位的MIME類型，如initiate請求中提供。 此值應包含在完整請求中。
* `uploadToken` （字串）:對應二進位碼的上傳Token。 此值應包含在完整請求中。
* `uploadURIs` （陣列）:字串的清單，其值為應上傳二進位檔內容的完整URI(請參 [閱上傳二進位](#upload-binary))。
* `minPartSize` （數字）:如果有多個URI，則可提供給任何一個uploadURI的資料的最小長度（以位元組為單位）。
* `maxPartSize` （數字）:如果有多個URI，則可提供給上載URI中任何一個的資料的最大長度（以位元組為單位）。

### 上傳二進位檔 {#upload-binary}

啟動上載的輸出將包含一個或多個上載URI值。 如果提供多個URI，則客戶有責任將二進位檔案「拆分」為多個部件，並按順序將每個部件POST分配給每個URI。 必須使用所有URI，且每個部件必須大於最小大小，小於啟動響應中指定的最大大小。 這些要求將由CDN邊緣節點負責，以加速二進位檔案的上傳。

實現此目的的一個潛在方法是，根據API提供的上傳URI數量計算零件大小。 範例假設二進位檔的總大小為20,000位元組，而上傳URI的數目為2:

* 通過總大小除以URI數計算零件大小：20,000 / 2 = 10,000
* 上傳URI清單中第一個URI的二進位元組範圍0-9,999
* 上傳URI清單中二進位元組到第二個URI的POST位元組範圍10,000-19,999

如果成功，伺服器會以狀態碼回應每個 `201` 要求。

### 完整上傳 {#complete-upload}

上傳二進位檔的所有部分後，最後步驟是將HTTP POST要求提交至啟動資料所提供的完整URI。 請求主體的內容類型應為應用程式／表單資料`x-www-form-urlencoded` ，其中包含下列欄位：

* `(string) fileName`: 必要. 資產名稱，如啟動資料所提供。
* `(string) mimeType`: 必要. 二進位檔的HTTP內容類型，如啟動資料所提供。
* `(string) uploadToken`: 必要. 上傳二進位碼的Token，如啟動資料所提供。
* `(bool) createVersion`: 可選. 如果為true且已存在具有指定名稱的資產，則實例將建立該資產的新版本。
* `(string) versionLabel`: 可選. 如果已建立新版本，則將與版本關聯的標籤。
* `(string) versionComment`: 可選. 如果建立了新版本，則會與該版本相關聯的注釋。
* `(bool) replace`:可選：如果為true且已存在具有指定名稱的資產，則實例將刪除該資產，然後重新建立該資產。

>!![NOTE]
>
> 如果資產已存在且未指定createVersion或replace，則執行個體會以新的二進位檔更新資產的目前版本。

如同啟動程式，完整的請求資料可能包含多個檔案的資訊。

上傳二進位檔的程式，直到呼叫檔案的完整URL為止。 即使完整上傳檔案的二進位檔，在上傳程式完成前，執行個體不會處理資產。

如果成功，伺服器會以狀態代碼 `200` 進行響應。

### 開放原始碼上傳程式庫 {#open-source-upload-library}

若要進一步瞭解上傳演算法或建立您自己的上傳指令碼和工具，Adobe提供開放原始碼程式庫和工具作為起點：

* [開放原始碼aem-upload程式庫](https://github.com/adobe/aem-upload)
* [開放原始碼命令列工具](https://github.com/adobe/aio-cli-plugin-aem)

### 不建議使用的資產上傳API {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below -->

>[!NOTE]
對於Experience Manager作為雲端服務，僅支援新的上傳API。 Experience Manager 6.5的API已過時。

與上傳或更新資產或轉譯（任何二進位上傳）相關的方法在下列API中已過時：

* [AEM Assets HTTP API](mac-api-assets.md)
* `AssetManager` Java API，例如 `AssetManager.createAsset(..)`

>[!MORELIKETHIS]
* [開放原始碼aem-upload程式庫](https://github.com/adobe/aem-upload)
* [開放原始碼命令列工具](https://github.com/adobe/aio-cli-plugin-aem)


## 資產處理和後處理工作流程 {#post-processing-workflows}

大部分的資產處理都是根據資產 **[!UICONTROL Microsoft Services的「處理設定檔]** 」 [](asset-microservices-configure-and-use.md#get-started-using-asset-microservices)設定來執行，而不需要開發人員擴充功能。

對於後處理工作流程設定，標準AEM工作流程含有擴充功能（例如，可使用自訂步驟）。 請檢閱下列子節，以瞭解資產後處理工作流程中可使用哪些工作流程步驟。

### 後處理工作流程中的工作流程步驟 {#post-processing-workflows-steps}

>[!NOTE]
本節內容主要適用於從舊版AEM以雲端服務形式更新至AEM的客戶。

由於Experience Manager以Cloud Service的身分引入了新的部署模型，因此在推出資產微型服務之前，工作流程中使用的某些工作流程步驟可能不再支援後處理工作流程。 `DAM Update Asset` 請注意，大部分服務都會以更簡單的方式取代，以設定和使用資產微型服務。

以下是AEM雲端服務中的技術工作流程模型及其支援等級清單：

### 支援的工作流程步驟 {#supported-workflow-steps}

雲端服務支援下列工作流程步驟。

* `com.day.cq.dam.similaritysearch.internal.workflow.process.AutoTagAssetProcess`
* `com.day.cq.dam.core.impl.process.CreateAssetLanguageCopyProcess`
* `com.day.cq.wcm.workflow.process.CreateVersionProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.StartTrainingProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.TransferTrainingDataProcess`
* `com.day.cq.dam.core.impl.process.TranslateAssetLanguageCopyProcess`
* `com.day.cq.dam.core.impl.process.UpdateAssetLanguageCopyProcess`
* `com.adobe.cq.workflow.replication.impl.ReplicationWorkflowProcess`
* `com.day.cq.dam.core.impl.process.DamUpdateAssetWorkflowCompletedProcess`

### 不支援或取代的機型 {#unsupported-replaced-models}

以下技術工作流程模型會由資產微型服務取代，或是無法提供支援。

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
