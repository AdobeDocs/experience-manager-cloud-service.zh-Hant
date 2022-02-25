---
title: 開發人員引用 [!DNL Assets]
description: '"[!DNL Assets] API和開發人員參考內容允許您管理資產，包括二進位檔案、元資料、格式副本、注釋和 [!DNL Content Fragments]"'
contentOwner: AG
feature: APIs,Assets HTTP API
role: Developer,Architect,Admin
exl-id: c75ff177-b74e-436b-9e29-86e257be87fb
source-git-commit: daa26a9e4e3d9f2ce13e37477a512a3e92d52351
workflow-type: tm+mt
source-wordcount: '1744'
ht-degree: 2%

---

# [!DNL Adobe Experience Manager Assets] 開發人員使用案例、 API和參考材料 {#assets-cloud-service-apis}

文章包含為開發商提供的建議、參考資料和資源 [!DNL Assets] 作為 [!DNL Cloud Service]。 它包括新的資產上載模組、API參考以及有關後處理工作流中提供的支援的資訊。

## [!DNL Experience Manager Assets] API和操作 {#use-cases-and-apis}

[!DNL Assets] 作為 [!DNL Cloud Service] 提供了幾個API以寫程式方式與數字資產交互。 每個API都支援特定的使用案例，如下表所述。 的 [!DNL Assets] 用戶介面， [!DNL Experience Manager] 案頭應用和 [!DNL Adobe Asset Link] 支援所有或部分行動。

>[!CAUTION]
>
>某些API繼續存在，但不受活動支援（用×表示）。 盡可能不要使用這些API。

| 支援級別 | 說明 |
| ------------- | --------------------------- |
| ✓ | 支援 |
| × | 不支援. 別用。 |
| - | 不可用 |

| 用例 | [aem上載](https://github.com/adobe/aem-upload) | [Experience Manager/吊具/JCR](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) Java API | [Asset compute服務](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html) | [[!DNL Assets] HTTP API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html#create-an-asset) | 吊帶 [GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) / [POST](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html) servel | [GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) |
| ----------------|:---:|:---:|:---:|:---:|:---:|:---:|
| **原始二進位** |  |  |  |  |  |  |
| 建立原始 | ✓ | × | - | × | × | - |
| 讀取原件 | - | × | ✓ | ✓ | ✓ | - |
| 更新原始 | ✓ | × | ✓ | × | × | - |
| 刪除原始 | - | ✓ | - | ✓ | ✓ | - |
| 複製原始 | - | ✓ | - | ✓ | ✓ | - |
| 移動原始 | - | ✓ | - | ✓ | ✓ | - |
| **中繼資料** |  |  |  |  |  |  |
| 建立元資料 | - | ✓ | ✓ | ✓ | ✓ | - |
| 讀取元資料 | - | ✓ | - | ✓ | ✓ | - |
| 更新元資料 | - | ✓ | ✓ | ✓ | ✓ | - |
| 刪除元資料 | - | ✓ | ✓ | ✓ | ✓ | - |
| 複製元資料 | - | ✓ | - | ✓ | ✓ | - |
| 移動元資料 | - | ✓ | - | ✓ | ✓ | - |
| **內容片段(CF)** |  |  |  |  |  |  |
| 建立CF | - | ✓ | - | ✓ | - | - |
| 閱讀CF | - | ✓ | - | ✓ | - | ✓ |
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

## 資產上載 {#asset-upload}

在 [!DNL Experience Manager] 作為 [!DNL Cloud Service]，您可以使用HTTP API直接將資產上載到雲儲存。 下面是上載二進位檔案的步驟。 在外部應用程式中執行這些步驟，而不是在 [!DNL Experience Manager] JVM。

1. [提交HTTP請求](#initiate-upload)。 它通知 [!DNL Experience Manage]r部署您上載新二進位檔案的意圖。
1. [PUT二進位檔案的內容](#upload-binary) 到由啟動請求提供的一個或多個URI。
1. [提交HTTP請求](#complete-upload) 通知伺服器已成功上載二進位檔案的內容。

![直接二進位上載協定概述](assets/add-assets-technical.png)

>[!IMPORTANT]
在外部應用程式中執行以上步驟，而不是在 [!DNL Experience Manager] JVM。

該方法提供了對資產上載的可擴展且效能更高的處理。 與現時比較之 [!DNL Experience Manager] 6.5是：

* 二進位檔案不通過 [!DNL Experience Manager]，現在只需將上載過程與為部署配置的二進位雲儲存進行協調。
* 二進位雲儲存可與內容分發網路(CDN)或邊緣網路配合使用。 CDN選擇對客戶機更近的上載終結點。 當資料傳輸到附近端點的距離較短時，上載效能和用戶體驗將得到改善，特別是對於地理位置分散的團隊。

>[!NOTE]
請參見在開源中實現此方法的客戶端代碼 [aem上載庫](https://github.com/adobe/aem-upload)。

### 啟動上載 {#initiate-upload}

將HTTPPOST請求提交到所需資料夾。 在此資料夾中建立或更新資產。 包括選擇器 `.initiateUpload.json` 指示請求是啟動二進位檔案的上載。 例如，應建立資產的資料夾的路徑是 `/assets/folder`。 POST請求為 `POST https://[aem_server]:[port]/content/dam/assets/folder.initiateUpload.json`。

請求正文的內容類型應為 `application/x-www-form-urlencoded` 表單資料，包含以下欄位：

* `(string) fileName`: 必要. 中顯示的資產名稱 [!DNL Experience Manager]。
* `(number) fileSize`: 必要. 正在上載的資產的檔案大小（以位元組為單位）。

只要每個二進位檔案包含必填欄位，就可以使用單個請求啟動多個二進位檔案的上載。 如果成功，請求將以 `201` 狀態代碼和包含以下格式的JSON資料的主體：

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

* `completeURI` （字串）:在二進位檔案完成上載後調用此URI。 URI可以是絕對URI或相對URI，客戶端應能夠處理兩者之一。 即，值可以是 `"https://[aem_server]:[port]/content/dam.completeUpload.json"` 或 `"/content/dam.completeUpload.json"` 請參閱 [完成上載](#complete-upload)。
* `folderPath` （字串）:上載二進位檔案的資料夾的完整路徑。
* `(files)` （陣列）:其長度和順序與初始化請求中提供的二進位資訊清單的長度和順序相匹配的元素清單。
* `fileName` （字串）:相應二進位檔案的名稱，如啟動請求中提供的。 此值應包括在完整請求中。
* `mimeType` （字串）:相應二進位檔案的MIME類型，如啟動請求中提供的。 此值應包括在完整請求中。
* `uploadToken` （字串）:相應二進位檔案的上載令牌。 此值應包括在完整請求中。
* `uploadURIs` （陣列）:值為二進位內容應上載到的完整URI的字串清單（請參見） [上載二進位](#upload-binary))。
* `minPartSize` （數）:可提供給以下任一資料的最小長度（以位元組為單位） `uploadURIs`，如果有多個URI。
* `maxPartSize` （數）:可提供給以下任一資料的最大長度（以位元組為單位） `uploadURIs`，如果有多個URI。

### 上載二進位 {#upload-binary}

啟動上載的輸出包括一個或多個上載URI值。 如果提供了多於一個URI，則客戶機可以將二進位檔案拆分成多個部件，並按順序向提供的上載URI發出每個部件的PUT請求。 如果選擇將二進位檔案拆分為零件，請確保遵循以下准則：
* 除最後一個部件外，每個部件的大小必須大於或等於 `minPartSize`。
* 每個零件的大小必須小於或等於 `maxPartSize`。
* 如果二進位大小超過 `maxPartSize`，必須將二進位檔案拆分為多個部分才能上載。
* 您不必使用所有URI。

如果二進位檔案的大小小於或等於 `maxPartSize`，您可以將整個二進位檔案上載到單個上載URI。 如果提供了多個上載URI，請使用第一個上載URI，然後忽略其餘的上載URI。 您不必使用所有URI。

CDN邊緣節點有助於加速請求的二進位檔案上載。

最簡單的方法是使用 `maxPartSize` 作為零件尺寸。 如果將此值用作部件大小，則API合同將確保有足夠的上載URI來上載二進位檔案。 為此，將二進位檔案拆分為大小部分 `maxPartSize`，按順序為每個部件使用一個URI。 最後部分的大小可以小於或等於 `maxPartSize`。 例如，假設二進位檔案的總大小為20,000位元組， `minPartSize` 是5,000位元組， `maxPartSize` 為8,000位元組，上載URI的數量為5。 然後執行以下步驟：
* 使用第一個上載URI上載二進位檔案的前8,000位元組。
* 使用第二個上載URI上載二進位檔案的第二個8,000位元組。
* 使用第三個上載URI上載二進位檔案的最後4,000位元組。 因為這是最後一部分，所以它不必大於 `minPartSize`。
* 您無需使用最後兩個上載URI。 別理他們。

常見的錯誤是根據API提供的上載URI數計算部件大小。 API合同不保證此方法有效，並且實際上可能導致部件大小超出範圍 `minPartSize` 和 `maxPartSize`。 這可能導致二進位上載失敗。

同樣，最簡單和最安全的方法是簡單地使用尺寸等於 `maxPartSize`。

如果上載成功，伺服器將用 `201` 狀態代碼。

>[!NOTE]
有關上載算法的詳細資訊，請參見 [官方特徵文檔](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html#Upload) 和 [API文檔](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/api/binary/BinaryUpload.html) Apache Jackrabbit Oak項目。

### 完成上載 {#complete-upload}

在上載二進位檔案的所有部分後，將HTTPPOST請求提交到由啟動資料提供的完整URI。 請求正文的內容類型應為 `application/x-www-form-urlencoded` 表單資料，包含以下欄位。

| 欄位 | 類型 | 需要或不需要 | 說明 |
|---|---|---|---|
| `fileName` | 字串 | 必要 | 資產名稱，如初始資料所提供。 |
| `mimeType` | 字串 | 必要 | 啟動資料提供的二進位檔案的HTTP內容類型。 |
| `uploadToken` | 字串 | 必要 | 正如啟動資料提供的那樣，為二進位檔案上載令牌。 |
| `createVersion` | 布林值 (Boolean) | 可選 | 如果 `True` 並且存在具有指定名稱的資產， [!DNL Experience Manager] 建立資產的新版本。 |
| `versionLabel` | 字串 | 可選 | 如果建立了新版本，則與資產的新版本關聯的標籤。 |
| `versionComment` | 字串 | 可選 | 如果建立了新版本，則與該版本關聯的注釋。 |
| `replace` | 布林值 (Boolean) | 可選 | 如果 `True` 並且存在指定名稱的資產， [!DNL Experience Manager] 刪除該資產，然後重新建立它。 |

>[!NOTE]
如果資產存在且 `createVersion` 無 `replace` 指定，然後 [!DNL Experience Manager] 使用新的二進位檔案更新資產的當前版本。

與啟動過程一樣，完整請求資料可能包含多個檔案的資訊。

在為檔案調用完整的URL之前，不會完成上載二進位檔案的過程。 在上載過程完成後處理資產。 即使資產的二進位檔案已完全上載但上載過程未完成，處理也不會啟動。 如果上載成功，伺服器將以 `200` 狀態代碼。

### 開源上載庫 {#open-source-upload-library}

要瞭解有關上載算法的更多資訊或構建您自己的上載指令碼和工具，Adobe提供了開源庫和工具：

* [開源aem-upload庫](https://github.com/adobe/aem-upload)。
* [開源命令行工具](https://github.com/adobe/aio-cli-plugin-aem)。

### 棄用的資產上載API {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below. -->

僅支援新上載方法 [!DNL Adobe Experience Manager] 作為 [!DNL Cloud Service]。 來自的API [!DNL Adobe Experience Manager] 不建議使用6.5。 以下API中不建議使用與上載或更新資產或格式副本（任何二進位上載）相關的方法：

* [Experience Manager AssetsHTTP API](mac-api-assets.md)
* `AssetManager` Java API，例如 `AssetManager.createAsset(..)`

>[!MORELIKETHIS]
* [開源aem-upload庫](https://github.com/adobe/aem-upload)。
* [開源命令行工具](https://github.com/adobe/aio-cli-plugin-aem)。
* [Apache Jackrabbit Oak文檔，用於直接上載](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html#Upload)。


## 資產處理和後處理工作流 {#post-processing-workflows}

在 [!DNL Experience Manager]，資產處理基於 **[!UICONTROL 處理配置檔案]** 使用的配置 [資產微服務](asset-microservices-configure-and-use.md#get-started-using-asset-microservices)。 處理不需要開發人員擴展。

對於後處理工作流配置，請使用帶有擴展的標準工作流和自定義步驟。

## 後處理工作流中工作流步驟的支援 {#post-processing-workflows-steps}

如果從以前的版本升級 [!DNL Experience Manager]，您可以使用資產微服務處理資產。 雲本地資產微服務的配置和使用更簡單。 中使用的幾個工作流步驟 [!UICONTROL DAM更新資產] 不支援以前版本中的工作流。 有關受支援類的詳細資訊，請參見 [Java API引用或Javadocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html)。

以下技術工作流模型將被資產微服務替換，或者沒有支援：

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

