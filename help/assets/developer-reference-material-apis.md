---
title: 以下專案的開發人員參考： [!DNL Assets]
description: '"[!DNL Assets] API和開發人員參考內容可讓您管理資產，包括二進位檔案、中繼資料、轉譯、註釋和 [!DNL Content Fragments].」'
contentOwner: AG
feature: APIs,Assets HTTP API
role: Developer,Architect,Admin
exl-id: c75ff177-b74e-436b-9e29-86e257be87fb
source-git-commit: a63a237e8da9260fa5f88060304b8cf9f508da7f
workflow-type: tm+mt
source-wordcount: '1899'
ht-degree: 6%

---

# [!DNL Adobe Experience Manager Assets] 開發人員使用案例、API和參考資料 {#assets-cloud-service-apis}

本文包含適用於開發人員之建議、參考資料和資源， [!DNL Assets] as a [!DNL Cloud Service]. 其中包含新的資產上傳模組、API參考資料，以及有關後處理工作流程中所提供支援的資訊。

## [!DNL Experience Manager Assets] API與作業 {#use-cases-and-apis}

[!DNL Assets] as a [!DNL Cloud Service] 提供數個API，以程式設計方式與數位資產互動。 每個API都支援特定使用案例，如下表所述。 此 [!DNL Assets] 使用者介面， [!DNL Experience Manager] 案頭應用程式和 [!DNL Adobe Asset Link] 支援所有或部分作業。

>[!CAUTION]
>
>有些API持續存在，但未主動支援(以×表示)。 請儘量不要使用這些API。

| 支援等級 | 說明 |
| ------------- | --------------------------- |
| ✓ | 支援 |
| × | 不支援. 請勿使用。 |
| - | 不可用 |

| 使用案例 | [aem-upload](https://github.com/adobe/aem-upload) | [Experience Manager / Sling / JCR](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) Java API | [asset compute服務](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html) | [[!DNL Assets] HTTP API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html#create-an-asset) | Sling [GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) / [POST](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html) servlet | [GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) |
| ----------------|:---:|:---:|:---:|:---:|:---:|:---:|
| **原始二進位** |  |  |  |  |  |  |
| 建立原始檔案 | ✓ | × | - | × | × | - |
| 讀取原始檔案 | - | × | ✓ | ✓ | ✓ | - |
| 更新原始檔案 | ✓ | × | ✓ | × | × | - |
| 刪除原始檔案 | - | ✓ | - | ✓ | ✓ | - |
| 複製原始檔案 | - | ✓ | - | ✓ | ✓ | - |
| 移動原始檔案 | - | ✓ | - | ✓ | ✓ | - |
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
| 行動資料夾 | ✓ | ✓ | - | ✓ | - | - |

## 資產上傳 {#asset-upload}

在 [!DNL Experience Manager] as a [!DNL Cloud Service]，您可以使用HTTP API直接將資產上傳到雲端儲存空間。 上傳二進位檔案的步驟如下。 在外部應用程式中執行這些步驟，而不是在 [!DNL Experience Manager] JVM。

1. [提交HTTP要求](#initiate-upload). 它會通知 [!DNL Experience Manage]或部署您打算上傳新的二進位檔。
1. [PUT二進位檔的內容](#upload-binary) 初始化要求提供的一或多個URI。
1. [提交HTTP要求](#complete-upload) 通知伺服器已成功上傳二進位檔的內容。

![直接二進位上傳通訊協定概觀](assets/add-assets-technical.png)

>[!IMPORTANT]
>
在外部應用程式中而不是在 [!DNL Experience Manager] JVM。

方法提供可擴充且效能更高的資產上傳處理方式。 相較於以下的差異： [!DNL Experience Manager] 6.5為：

* 二進位檔不會通過 [!DNL Experience Manager]，現在只需配合為部署設定的二進位雲端儲存空間來協調上傳程式。
* 二進位雲端儲存空間可與內容傳遞網路(CDN)或邊緣網路搭配使用。 CDN會選取較接近使用者端的上傳端點。 當資料傳輸至附近端點的距離較短時，上傳效能和使用者體驗會改善，尤其是對於分散各地的團隊。

>[!NOTE]
>
請參閱使用者端代碼，以在開放原始碼中實施此方法 [aem-upload資料庫](https://github.com/adobe/aem-upload).
>
[!IMPORTANT]
>
在某些情況下，由於Experience Manager中儲存的最終一致性性質，變更可能不會在Cloud Service請求之間完全傳播。 這會導致404個起始或完成上傳呼叫的回應，因為必要的資料夾建立未傳播。 使用者端應該會收到404個回應，並透過實作附有後退策略的重試來處理這些回應。

### 啟動上傳 {#initiate-upload}

將HTTPPOST請求提交到所需的資料夾。 資產會在此資料夾中建立或更新。 包含選擇器 `.initiateUpload.json` 指示要求要啟動二進位檔案的上傳。 例如，要建立資產的資料夾路徑為 `/assets/folder`. POST要求為 `POST https://[aem_server]:[port]/content/dam/assets/folder.initiateUpload.json`.

請求內文的內容型別應為 `application/x-www-form-urlencoded` 表單資料，包含下列欄位：

* `(string) fileName`: 必填. 資產在中出現的名稱 [!DNL Experience Manager].
* `(number) fileSize`: 必填. 上傳資產的檔案大小（位元組）。

只要每個二進位檔案都包含必要欄位，就可以使用單一要求來起始多個二進位檔案的上傳。 如果成功，請求會回應 `201` 狀態代碼和包含下列格式JSON資料的內文：

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

* `completeURI` （字串）：當二進位檔完成上傳時，呼叫此URI。 URI可以是絕對URI或相對URI，使用者端應該能夠處理任一個。 也就是說，值可以是 `"https://[aem_server]:[port]/content/dam.completeUpload.json"` 或 `"/content/dam.completeUpload.json"` 另請參閱 [完整上傳](#complete-upload).
* `folderPath` （字串）：二進位檔案上傳所在資料夾的完整路徑。
* `(files)` （陣列）：其長度和順序符合起始請求中提供的二進位資訊清單長度和順序的元素清單。
* `fileName` （字串）：對應的二進位檔名稱，如起始要求中所提供。 此值應包含在完整請求中。
* `mimeType` （字串）：對應二進位檔的mime型別，如起始要求中所提供。 此值應包含在完整請求中。
* `uploadToken` （字串）：對應二進位檔案的上傳權杖。 此值應包含在完整請求中。
* `uploadURIs` （陣列）：字串清單，其值是二進位內容應上傳到的完整URI (請參閱 [上傳二進位檔](#upload-binary))。
* `minPartSize` （數字）：可提供給任一個資料庫之資料的最小長度（位元組）。 `uploadURIs`，如果有超過一個URI。
* `maxPartSize` （數字）：可提供給任一個的資料長度上限（位元組）。 `uploadURIs`，如果有超過一個URI。

### 上傳二進位檔 {#upload-binary}

起始上傳的輸出包含一或多個上傳URI值。 如果提供了多個URI，使用者端可以依序將二進位分割成多個部分，並向提供的上傳URI提出每個部分的PUT請求。 如果您選擇將二進位檔案分割成零件，請遵循下列准則：

* 除了最後一個零件外，每個零件的大小必須大於或等於 `minPartSize`.
* 每個零件的大小必須小於或等於 `maxPartSize`.
* 如果二進位檔案的大小超過 `maxPartSize`，將二進位檔案分割為多個部分以上傳。
* 您不需要使用所有URI。

如果二進位檔的大小小於或等於 `maxPartSize`，您可以改為將整個二進位檔案上傳至單一上傳URI。 如果提供了多個上傳URI，請使用第一個並忽略其餘的URI。 您不需要使用所有URI。

CDN邊緣節點有助於加速要求的二進位檔上傳。

最簡單的實行方式是使用 `maxPartSize` 作為零件大小。 如果您使用此值作為部分大小，API合約可確保有足夠的上傳URI來上傳您的二進位檔。 若要這麼做，請將二進位分割成大小部分 `maxPartSize`，依序為每個零件使用一個URI。 最終零件的大小可小於或等於 `maxPartSize`. 例如，假設二進位檔案的總大小為20,000位元組， `minPartSize` 為5,000位元組， `maxPartSize` 為8,000位元組，而且上傳URI的數量為5。 執行以下步驟：

* 使用第一個上傳URI上傳二進位的前8,000個位元組。
* 使用第二個上傳URI上傳二進位檔案的第二個8,000位元組。
* 使用第三個上傳URI上傳二進位檔案的最後4,000個位元組。 由於這是最後部分，因此不需要大於 `minPartSize`.
* 您不需要使用最後兩個上傳URI。 您可以忽略它們。

常見的錯誤是根據API提供的上傳URI數量來計算零件大小。 API合約無法保證此方法有效，而且實際上可能會導致零件大小超出範圍 `minPartSize` 和 `maxPartSize`. 這可能會造成二進位上傳失敗。

同樣地，最簡單最安全的方法就是使用大小等於 `maxPartSize`.

如果上傳成功，伺服器會以回應每個要求 `201` 狀態代碼。

>[!NOTE]
>
如需上傳演演算法的詳細資訊，請參閱 [正式功能檔案](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html#Upload) 和 [API檔案](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/api/binary/BinaryUpload.html) Apache Jackrabbit Oak專案中的。

### 完成上傳 {#complete-upload}

上傳二進位檔案的所有部分後，將HTTPPOST請求提交至初始化資料提供的完整URI。 請求內文的內容型別應為 `application/x-www-form-urlencoded` 表單資料，包含下列欄位。

| 欄位 | 類型 | 必要 或非 | 說明 |
|---|---|---|---|
| `fileName` | 字串 | 必填 | 由初始資料提供的資產名稱。 |
| `mimeType` | 字串 | 必填 | 由起始資料提供的二進位檔的HTTP內容型別。 |
| `uploadToken` | 字串 | 必填 | 上傳二進位的Token，如初始化資料所提供。 |
| `createVersion` | 布林值 | 選用 | 如果 `True` 而且具有指定名稱的資產已存在，則 [!DNL Experience Manager] 會建立資產的新版本。 |
| `versionLabel` | 字串 | 選用 | 如果建立新版本，則會提供與資產新版本相關聯的標籤。 |
| `versionComment` | 字串 | 選用 | 如果建立了新版本，註釋會與該版本相關聯。 |
| `replace` | 布林值 | 選用 | 如果 `True` 而且具有指定名稱的資產已存在， [!DNL Experience Manager] 會刪除資產，然後重新建立資產。 |
| `uploadDuration` | 數字 | 選用 | 檔案完整上傳的總時間，以毫秒為單位。 如果指定，上傳持續時間會包含在系統的記錄檔中，以進行傳輸率分析。 |
| `fileSize` | 數字 | 選用 | 檔案的大小（位元組）。 如果指定，檔案大小會包含在系統的記錄檔中，以進行傳輸速率分析。 |

>[!NOTE]
>
如果資產存在，但兩者皆非 `createVersion` 也不 `replace` 已指定，則 [!DNL Experience Manager] 以新的二進位檔案更新資產的目前版本。

如同起始程式，完整的請求資料可能包含多個檔案的資訊。

在呼叫檔案的完整URL之前，不會完成上傳二進位檔的程式。 資產會在上傳程式完成後處理。 即使資產的二進位檔案已完全上傳，但上傳程式未完成，處理作業也不會開始。 如果上傳成功，伺服器會以回應 `200` 狀態代碼。

### 開放原始碼上傳庫 {#open-source-upload-library}

若要深入瞭解上傳演演算法，或若要建置您自己的上傳指令碼和工具，Adobe提供開放原始碼程式庫和工具：

* [開放原始碼aem-upload資料庫](https://github.com/adobe/aem-upload).
* [開放原始碼命令列工具](https://github.com/adobe/aio-cli-plugin-aem).

>[!NOTE]
>
aem-upload程式庫和命令列工具都會使用 [node-httptransfer程式庫](https://github.com/adobe/node-httptransfer/)

### 已棄用的資產上傳API {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below. -->

只有以下專案才支援新的上傳方法 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]. 來自的API [!DNL Adobe Experience Manager] 6.5已過時。 下列API中不建議使用與上傳或更新資產或轉譯（任何二進位上傳）相關的方法：

* [EXPERIENCE MANAGER ASSETS HTTP API](mac-api-assets.md)
* `AssetManager` Java API，例如 `AssetManager.createAsset(..)`， `AssetManager.createAssetForBinary(..)`， `AssetManager.getAssetForBinary(..)`， `AssetManager.removeAssetForBinary(..)`， `AssetManager.createOrUpdateAsset(..)`， `AssetManager.createOrReplaceAsset(..)`

>[!MORELIKETHIS]
>
* [開放原始碼aem-upload資料庫](https://github.com/adobe/aem-upload).
* [開放原始碼命令列工具](https://github.com/adobe/aio-cli-plugin-aem).
* [直接上傳的Apache Jackrabbit Oak檔案](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html#Upload).

## 資產處理和後續處理工作流程 {#post-processing-workflows}

在 [!DNL Experience Manager]，資產處理會根據 **[!UICONTROL 處理設定檔]** 使用的設定 [資產微服務](asset-microservices-configure-and-use.md#get-started-using-asset-microservices). 處理不需要開發人員擴充功能。

若要設定後續處理工作流程，請將標準工作流程與擴充功能搭配使用，並搭配自訂步驟。

## 支援後處理工作流程中的工作流程步驟 {#post-processing-workflows-steps}

如果您從舊版升級 [!DNL Experience Manager]，您可以使用資產微服務來處理資產。 雲端原生資產微服務可更輕鬆設定和使用。 中使用的幾個工作流程步驟 [!UICONTROL DAM更新資產] 不支援舊版的工作流程。 如需有關支援類別的詳細資訊，請參閱 [Java API參考或Javadocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html).

以下技術工作流程模型已由資產微服務取代，或無法提供支援：

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

>[!MORELIKETHIS]
>
* [[!DNL Experience Cloud] as a [!DNL Cloud Service] SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md).
