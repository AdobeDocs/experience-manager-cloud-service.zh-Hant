---
title: 的開發人員參考 [!DNL Assets]
description: "[!DNL Assets] API和開發人員參考內容可讓您管理資產，包括二進位檔案、中繼資料、轉譯、留言和 [!DNL Content Fragments]."
contentOwner: AG
feature: APIs,Assets HTTP API
role: Developer,Architect,Admin
exl-id: c75ff177-b74e-436b-9e29-86e257be87fb
source-git-commit: 153cc482047c3235b0f62bb94051c884b4cf29d4
workflow-type: tm+mt
source-wordcount: '1869'
ht-degree: 2%

---

# [!DNL Adobe Experience Manager Assets] 開發人員使用案例、API和參考資料 {#assets-cloud-service-apis}

本文包含為以下項目的開發人員提供的建議、參考資料和資源： [!DNL Assets] as a [!DNL Cloud Service]. 其中包含新的資產上傳模組、API參考，以及後置處理工作流程中所提供支援的相關資訊。

## [!DNL Experience Manager Assets] API與操作 {#use-cases-and-apis}

[!DNL Assets] as a [!DNL Cloud Service] 提供數個API，以程式設計方式與數位資產互動。 每個API都支援特定使用案例，如下表所述。 此 [!DNL Assets] 使用者介面， [!DNL Experience Manager] 案頭應用程式和 [!DNL Adobe Asset Link] 支援所有或部分操作。

>[!CAUTION]
>
>有些API仍然存在，但不受主動支援(以×表示)。 請盡可能勿使用這些API。

| 支援層級 | 說明 |
| ------------- | --------------------------- |
| ✓ | 支援 |
| × | 不支援. 請勿使用。 |
| - | 不可用 |

| 使用案例 | [aem-upload](https://github.com/adobe/aem-upload) | [Experience Manager/ Sling / JCR](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) Java API | [Asset compute服務](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html) | [[!DNL Assets] HTTP API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html#create-an-asset) | Sling [GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) / [POST](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html) servlet | [GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) |
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

在 [!DNL Experience Manager] as a [!DNL Cloud Service]，您可以使用HTTP API將資產直接上傳至雲端儲存空間。 上傳二進位檔案的步驟如下。 在外部應用程式中執行這些步驟，而不是在 [!DNL Experience Manager] JVM。

1. [提交HTTP請求](#initiate-upload). 會通知 [!DNL Experience Manage]或部署您上傳新二進位檔的目的。
1. [PUT二進位檔的內容](#upload-binary) 到由啟動請求提供的一個或多個URI。
1. [提交HTTP請求](#complete-upload) 通知伺服器已成功上傳二進位檔的內容。

![直接二進位上傳通訊協定概述](assets/add-assets-technical.png)

>[!IMPORTANT]
在外部應用程式中執行上述步驟，而非在 [!DNL Experience Manager] JVM。

此方法提供可擴充且效能更高的資產上傳處理功能。 與 [!DNL Experience Manager] 6.5為：

* 二進位檔不會通過 [!DNL Experience Manager]，現在只需將上傳程式與為部署設定的二進位雲端儲存空間進行協調即可。
* 二進位雲端儲存空間可與內容傳遞網路(CDN)或邊緣網路搭配使用。 CDN會選取離用戶端較近的上傳端點。 當資料傳至附近端點的距離較短時，上傳效能和使用者體驗會有所改善，尤其是針對分散於不同地理位置的團隊。

>[!NOTE]
請參閱用戶端代碼，以在開放原始碼中實作此方法 [aem-upload資料庫](https://github.com/adobe/aem-upload).
[!IMPORTANT]
在某些情況下，由於儲存在Experience Manager中的最終一致性，更改可能無法在請求到Cloud Service之間完全傳播。 這會導致404個回應以起始或完成上傳呼叫，因為建立的必要資料夾無法傳播。 用戶端應有404個回應，並透過後退策略實作重試來處理。

### 起始上傳 {#initiate-upload}

將HTTPPOST請求提交至所需的資料夾。 資產會在此資料夾中建立或更新。 納入選取器 `.initiateUpload.json` 以指出要求是起始上傳二進位檔案。 例如，應建立資產的資料夾路徑為 `/assets/folder`. POST要求為 `POST https://[aem_server]:[port]/content/dam/assets/folder.initiateUpload.json`.

要求內文的內容類型應為 `application/x-www-form-urlencoded` 表單資料，包含下列欄位：

* `(string) fileName`: 必要. 資產的名稱，如下所示： [!DNL Experience Manager].
* `(number) fileSize`: 必要. 上傳資產的檔案大小（以位元組為單位）。

只要每個二進位檔都包含必要欄位，就可以使用單一請求來起始多個二進位檔的上傳。 如果成功，要求會以 `201` 狀態代碼和包含JSON資料的內文，格式如下：

```json
{
    "completeURI": "(string)",
    "folderPath": "(string)",
    "files": [
        {
            "fileName": "(string)",
            "mimeType": "(string)",
            "uploadToken": "(string)",
            "uploadURIs": [
                "(string)"
            ],
            "minPartSize": (number),
            "maxPartSize": (number)
        }
    ]
}
```

* `completeURI` （字串）:當二進位檔完成上傳時，呼叫此URI。 URI可以是絕對URI或相對URI，客戶端應能夠處理它們。 也就是說，值可以是 `"https://[aem_server]:[port]/content/dam.completeUpload.json"` 或 `"/content/dam.completeUpload.json"` 請參閱 [完整上傳](#complete-upload).
* `folderPath` （字串）:上傳二進位檔的資料夾完整路徑。
* `(files)` （陣列）:元素清單，其長度和順序與起始請求中提供的二進位資訊清單的長度和順序相匹配。
* `fileName` （字串）:相應二進位的名稱，如起始請求中提供。 此值應包含在完成請求中。
* `mimeType` （字串）:相應二進位的mime類型，如起始請求中提供。 此值應包含在完成請求中。
* `uploadToken` （字串）:對應二進位的上傳代號。 此值應包含在完成請求中。
* `uploadURIs` （陣列）:字串的清單，其值是應上載二進位檔內容的完整URI(請參閱 [上傳二進位檔](#upload-binary))。
* `minPartSize` （數字）:可提供給任何一個 `uploadURIs`，如果有多個URI。
* `maxPartSize` （數字）:可提供給任何一個 `uploadURIs`，如果有多個URI。

### 上傳二進位檔 {#upload-binary}

啟動上載的輸出包括一個或多個上載URI值。 如果提供了多個URI，則客戶端可將二進位檔案拆分為多個部分，並按順序向提供的上載URI發出每個部分的PUT請求。 如果您選擇將二進位檔分割為多個部分，請遵循下列准則：

* 每個部件（最後一個部件除外）的大小必須大於或等於 `minPartSize`.
* 每個零件的尺寸必須小於或等於 `maxPartSize`.
* 如果二進位檔的大小超過 `maxPartSize`，將二進位檔分割為多個部分以上傳。
* 您不必使用所有URI。

如果二進位檔的大小小於或等於 `maxPartSize`，您可以將整個二進位檔上傳至單一上傳URI。 如果提供了多個上載URI，請使用第一個URI，忽略其餘的URI。 您不必使用所有URI。

CDN邊緣節點有助於加速請求上傳二進位檔。

要達成此目標，最簡單的方法是使用 `maxPartSize` 作為零件尺寸。 如果您將此值用作零件大小，API合約可保證有足夠的上傳URI來上傳您的二進位檔。 要執行此操作，將二進位檔分割為部分大小 `maxPartSize`，按順序為每個部件使用一個URI。 最終零件可以是小於或等於的任何尺寸 `maxPartSize`. 例如，假設二進位檔的總大小為20,000位元組，則 `minPartSize` 是5,000位元組， `maxPartSize` 為8,000個位元組，上載URI的數量為5。 執行下列步驟：

* 使用第一個上傳URI上傳二進位檔的前8,000個位元組。
* 使用第二個上載URI上載二進位檔的第二個8,000位元組。
* 使用第三個上傳URI上傳二進位檔的最後4,000個位元組。 因為這是最後一部分，所以它不需要大於 `minPartSize`.
* 您不需要使用最後兩個上傳URI。 你可以忽略它們。

常見的錯誤是根據API提供的上傳URI數量計算零件大小。 API合約不保證此方法有效，且實際上可能會產生超出之間範圍的零件大小 `minPartSize` 和 `maxPartSize`. 這可能會導致二進位上傳失敗。

同樣，最簡單、最安全的方法就是簡單地使用大小等於 `maxPartSize`.

如果上傳成功，伺服器會以 `201` 狀態代碼。

>[!NOTE]
如需上傳演算法的詳細資訊，請參閱 [官方功能檔案](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html#Upload) 和 [API檔案](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/api/binary/BinaryUpload.html) 在阿帕奇傑克拉布特橡樹項目。

### 完成上傳 {#complete-upload}

上傳二進位檔案的所有部分後，請將HTTPPOST請求提交到啟動資料提供的完整URI。 要求內文的內容類型應為 `application/x-www-form-urlencoded` 表單資料，包含下列欄位。

| 欄位 | 類型 | 必要或非 | 說明 |
|---|---|---|---|
| `fileName` | 字串 | 必要 | 資產名稱，如啟動資料所提供。 |
| `mimeType` | 字串 | 必要 | 二進位檔的HTTP內容類型，如啟動資料所提供。 |
| `uploadToken` | 字串 | 必要 | 如啟動資料所提供，上傳二進位的代號。 |
| `createVersion` | 布林值 | 可選 | 若 `True` 而資產具有指定名稱，則 [!DNL Experience Manager] 會建立資產的新版本。 |
| `versionLabel` | 字串 | 可選 | 如果已建立新版本，則與資產新版本相關聯的標籤。 |
| `versionComment` | 字串 | 可選 | 如果建立了新版本，則與該版本關聯的注釋。 |
| `replace` | 布林值 | 可選 | 若 `True` 而且有指定名稱的資產， [!DNL Experience Manager] 刪除資產，然後重新建立。 |
| `uploadDuration` | 數量 | 可選 | 檔案完整上傳的總時間量（以毫秒為單位）。 如果指定，則上傳期間會包含在系統的記錄檔中，以用於傳輸率分析。 |
| `fileSize` | 數量 | 可選 | 檔案的大小（以位元組為單位）。 如果指定，則檔案大小將包含在系統的日誌檔案中，以進行傳輸速率分析。 |

>[!NOTE]
如果資產存在，且 `createVersion` no `replace` ，則 [!DNL Experience Manager] 使用新二進位檔更新資產的目前版本。

與起始程式一樣，完成請求資料可能包含多個檔案的資訊。

上傳二進位檔的程式要等到為該檔案叫用完整URL後，才會完成。 上傳程式完成後會處理資產。 即使資產的二進位檔案已完整上傳，但上傳程式尚未完成，處理也不會開始。 如果上傳成功，伺服器會以 `200` 狀態代碼。

### 開放原始碼上傳程式庫 {#open-source-upload-library}

若要進一步了解上傳演算法或建立專屬的上傳指令碼和工具，Analytics提供開放原始碼程式庫和工具：

* [開放原始碼aem上傳程式庫](https://github.com/adobe/aem-upload).
* [開放原始碼命令列工具](https://github.com/adobe/aio-cli-plugin-aem).

>[!NOTE]
aem上傳程式庫和命令列工具都使用 [node-httptransfer庫](https://github.com/adobe/node-httptransfer/)

### 汰除的資產上傳API {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below. -->

新的上傳方法僅支援 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]. 來自 [!DNL Adobe Experience Manager] 6.5已過時。 下列API中會淘汰與上傳或更新資產或轉譯（任何二進位上傳）相關的方法：

* [Experience Manager Assets HTTP API](mac-api-assets.md)
* `AssetManager` Java API，例如 `AssetManager.createAsset(..)`

>[!MORELIKETHIS]
* [開放原始碼aem上傳程式庫](https://github.com/adobe/aem-upload).
* [開放原始碼命令列工具](https://github.com/adobe/aio-cli-plugin-aem).
* [要直接上傳的Apache Jackrabbit Oak檔案](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html#Upload).


## 資產處理與後續處理工作流程 {#post-processing-workflows}

在 [!DNL Experience Manager]，則資產處理會根據 **[!UICONTROL 處理設定檔]** 使用 [資產微服務](asset-microservices-configure-and-use.md#get-started-using-asset-microservices). 處理程式不需要開發人員擴充功能。

若要進行後置處理工作流程設定，請使用具有擴充功能的標準工作流程及自訂步驟。

## 支援後置處理工作流程中的工作流程步驟 {#post-processing-workflows-steps}

如果您從舊版升級 [!DNL Experience Manager]，您可以使用資產微服務來處理資產。 雲端原生資產微服務的設定和使用更簡單。 中使用的幾個工作流程步驟 [!UICONTROL DAM更新資產] 不支援舊版的工作流程。 有關支援類的詳細資訊，請參見 [Java API參考或Javadoc](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html).

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
* [[!DNL Experience Cloud] as a [!DNL Cloud Service] SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md).

