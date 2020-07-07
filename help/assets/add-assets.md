---
title: 將您的數位資產新增至Adobe Experience Manager
description: 將您的數位資產新增至Adobe Experience Manager做為雲端服務
translation-type: tm+mt
source-git-commit: 23349f3350631f61f80b54b69104e5a19841272f
workflow-type: tm+mt
source-wordcount: '1358'
ht-degree: 2%

---


# 將數位資產新增至Adobe Experience Manager {#add-assets-to-experience-manager}

Adobe Experience Manager運用豐富的中繼資料、智慧標籤、轉譯和其他數位資產管理(DAM)服務，豐富上傳數位檔案的二進位內容。 您可以從本機資料夾或網路磁碟將各種檔案類型（例如影像、檔案和原始影像檔）上傳至Experience Manager Assets。

提供了多種上載方法。 除了最常用的瀏覽器上傳外，還有其他將資產新增至Experience Manager儲存庫的方法，包括案頭用戶端（例如Adobe Asset Link或Experience Manager案頭應用程式）、上傳和擷取指令碼，以及自動擷取整合（新增為AEM擴充功能）。

我們將著重在此處為使用者上傳方法，並提供文章連結，說明使用Experience Manager API和SDK進行資產上傳和擷取的技術層面。

雖然您可以在Experience Manager中上傳和管理任何二進位檔案，但最常用的檔案格式支援其他服務，例如中繼資料擷取或預覽／轉譯產生。 請參閱支 [援的檔案格式](file-format-support.md) ，以取得詳細資訊。

您也可以選擇對已上傳的資產進行其他處理。 可在上傳資產的資料夾上設定多個資產處理設定檔，以新增特定中繼資料、轉譯或影像處理服務。 如需詳 [細資訊](#additional-processing) ，請參閱以下的其他處理。

>[!NOTE]
>
>Experience Manager作為雲端服務，運用了新的上傳資產方式——直接二進位上傳。 預設會支援立即可用的產品功能和用戶端，例如AEM使用者介面、Adobe Asset Link、AEM案頭應用程式，因此對一般使用者是透明的。
>
>上傳由技術團隊自訂或擴充的程式碼，客戶需要使用新的上傳API和通訊協定。

## Upload assets {#upload-assets}

若要上傳檔案（或多個檔案），您可以在案頭上選取檔案，然後拖放至使用者介面（網頁瀏覽器）至目標資料夾。 或者，您也可以從使用者介面開始上傳。

1. 在「資產」使用者介面中，導覽至您要新增數位資產的位置。
1. 若要上傳資產，請執行下列其中一項作業：

   * 在工具列上，點選「建 **[!UICONTROL 立]** 」圖示。 然後，在功能表上，點選「 **[!UICONTROL 檔案」]**。 如有需要，可在顯示的對話框中更名檔案。
   * 在支援HTML5的瀏覽器中，直接將資產拖曳至「資產」使用者介面。 不會顯示要更名檔案的對話框。

   ![create_menu](assets/create_menu.png)

   要選擇多個檔案，請按Ctrl或Command鍵，然後在檔案選擇器對話框中選擇資產。 使用iPad時，一次只能選取一個檔案。

<!-- #ENGCHECK do we support pausing? I couldn't get pause to show with 1.5GB upload.... If not, this should be removed#

   You can pause the uploading of large assets (greater than 500 MB) and resume it later from the same page. Tap the **[!UICONTROL Pause]** icon beside progress bar that appears when an upload starts.

   ![chlimage_1-211](assets/chlimage_1-211.png)

   The size above which an asset is considered a large asset is configurable. For example, you can configure the system to consider assets above 1000 MB (instead of 500 MB) as large assets. In this case, **[!UICONTROL Pause]** appears on the progress bar when assets of size greater than 1000 MB are uploaded.

   The Pause button does not show if a file greater than 1000 MB is uploaded with a file less than 1000 MB. However, if you cancel the less than 1000 MB file upload, the **[!UICONTROL Pause]** button appears.

   To modify the size limit, configure the `chunkUploadMinFileSize` property of the `fileupload`node in the CRX repository.

   When you click the **[!UICONTROL Pause]** icon, it toggles to a **[!UICONTROL Play]** icon. To resume uploading, click the **[!UICONTROL Play]** icon.

   ![chlimage_1-212](assets/chlimage_1-212.png)
-->

1. 若要取消進行中的上傳，請按一下進`X`度列旁的關閉()。 當您取消上傳作業時，AEM Assets會刪除部分上傳的資產。

   如果您在上傳檔案之前取消上傳作業，AEM Assets會停止上傳目前的檔案並重新整理內容。 不過，已上傳的檔案不會刪除。


<!-- #ENGCHECK do we support pausing? I couldn't get pause to show with 1.5GB upload.... If not, this should be removed#
   The ability to resume uploading is especially helpful in low-bandwidth scenarios and network glitches, where it takes a long time to upload a large asset. You can pause the upload operation and continue later when the situation improves. When you resume, uploading starts from the point where you paused it.
-->

<!-- #ENGCHECK assuming this is not relevant? remove after confirming#
   During the upload operation, AEM saves the portions of the asset being uploaded as chunks of data in the CRX repository. When the upload completes, AEM consolidates these chunks into a single block of data in the repository.

   To configure the cleanup task for the unfinished chunk upload jobs, go to `https://[aem_server]:[port]/system/console/configMgr/org.apache.sling.servlets.post.impl.helper.ChunkCleanUpTask`.
-->


1. 「AEM資產」中的上傳進度對話方塊會顯示成功上傳檔案的計數，以及無法上傳的檔案。

此外，「資產」使用者介面會顯示您上傳的最近資產或您先建立的檔案夾。

>[!NOTE]
>
>若要將巢狀資料夾階層上傳至AEM，請參閱 [大量上傳資產](#bulk-upload)。

<!-- #ENGCHECK I'm assuming this is no longer relevant.... If yes, this should be removed#

### Serial uploads {#serialuploads}

Uploading numerous assets in bulk consumes significant I/O resources, which may adversely impact the performance of your AEM Assets instance. In particular, if you have a slow internet connection, the time to upload drastically increases due to a spike in disk I/O. Moreover, your web browser may introduce additional restrictions to the number of POST requests AEM Assets can handle for concurrent asset uploads. As a result, the upload operation fails or terminate prematurely. In other words, AEM assets may miss some files while ingesting a bunch of files or altogether fail to ingest any file.

To overcome this situation, AEM Assets ingests one asset at a time (serial upload) during a bulk upload operation, instead of the concurrently ingesting all the assets.

Serial uploading of assets is enabled by default. To disable the feature and allow concurrent uploading, overlay the `fileupload` node in Crx-de and set the value of the `parallelUploads` property to `true`.

### Streamed uploads {#streamed-uploads}

If you upload many assets to AEM, the I/O requests to server increase drastically, which reduces the upload efficiency and can even cause some upload task to time out. AEM Assets supports streamed uploading of assets. Streamed uploading reduces the disk I/O during the upload operation by avoiding asset storage in a temporary folder on the server before copying it to the repository. Instead, the data is transferred directly to the repository. This way, the time to upload large assets and the possibility of timeouts is reduced. Streamed upload is enabled by default in AEM Assets.

>[!NOTE]
>
>Streaming upload is disabled for AEM running on JEE server with servlet-api version lower than 3.1.
-->

### 在資產已存在時處理上載 {#handling-upload-existing-file}

如果您上傳的資產名稱與資產名稱相同，且資產已在上傳資產的位置使用，則會顯示警告對話方塊。

您可以選擇取代現有資產、建立其他版本，或借由重新命名已上傳的新資產來保留兩者。 如果您取代現有資產，資產的中繼資料以及您對現有資產所做的任何先前修改（例如註解、裁切等）都會被刪除。 如果您選擇保留這兩個資產，新資產會重新命名，並加上 `1` 其名稱的數字。

>[!NOTE]
>
>在「名稱衝 **[!UICONTROL 突]** 」( [!UICONTROL Name Conflict] )對話框中選擇「替換」(Replace)時，會為新資產重新生成資產ID。 此ID與先前資產的ID不同。
>
>如果「資產前瞻分析」已啟用，可以使用Adobe Analytics追蹤曝光／點按次數，則重新產生的資產ID會使Analytics上為資產擷取的資料無效。

若要保留AEM Assets中的重複資產，請點選／按一下「 **[!UICONTROL 保留]**」。 若要刪除您上傳的重複資產，請點選／按一下「刪 **[!UICONTROL 除」]**。

### 檔案名稱處理與禁止字元 {#filename-handling}

AEM Assets會防止您上傳檔案名稱中包含禁止字元的資產。 如果您嘗試上傳包含不允許之字元或以上之檔案名稱的資產，AEM Assets會顯示警告訊息並停止上傳，直到您移除這些字元或上傳包含允許名稱為止。

為符合貴組織的特定檔案命名慣例，「上 [!UICONTROL 傳資產] 」對話方塊可讓您指定上傳之檔案的長名稱。

但是，不支援下列（以空格分隔的）字元清單：

* 資產檔案名稱不可包含 `* / : [ \\ ] | # % { } ? &`
* 資產資料夾名稱不可包含 `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

## 大量上傳資產 {#bulk-upload}

要上傳更多檔案，特別是如果這些檔案存在於磁碟上的嵌套資料夾層次結構中，可以使用以下方法：

* 使用自訂的上傳指令碼或工具，以利 [用資產上傳API](developer-reference-material-apis.md#asset-upload-technical)。 此類自訂工具可視需要新增對資產的額外處理（例如，翻譯中繼資料或重新命名檔案）。
* 使用 [Experience Manager案頭應用程式](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html) ，上傳巢狀資料夾階層。

>[!NOTE]
>
>在設定和部署至Experience Manager時，若要從其他系統進行內容移轉，就必須仔細規劃、考慮和選擇工具，才能進行大量上傳。 請參閱部 [署指南](/help/implementing/deploying/overview.md) ，以取得內容移轉方法的指引。

## 使用案頭用戶端上傳資產 {#upload-assets-desktop-clients}

除了網頁瀏覽器使用者介面外，Experience Manager還支援案頭上的其他用戶端。 它們也提供上傳體驗，而不需前往網頁瀏覽器。

* [Adobe Asset Link](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html) 可讓您存取Adobe Photoshop、Adobe Illustrator和Adobe InDesign案頭應用程式中AEM的資產。 您可以直接從這些案頭應用程式中的Adobe Asset Link使用者介面，將目前開啟的檔案上傳至AEM。
* [Experience Manager案頭應用程式](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html) ，可簡化在案頭上處理資產的作業，不受檔案類型或處理資產的原生應用程式所限。 從本機檔案系統上傳巢狀檔案夾階層中的檔案特別有用，因為瀏覽器上傳僅支援上傳平面檔案清單。

## 其他處理 {#additional-processing}

為了對已上傳的資產進行額外處理，您可以在上傳資產的資料夾上使用資產處理設定檔。 它們可在資料夾「屬性」( **[!UICONTROL Properties]** )對話框中使用。

![assets-folder-properties](assets/assets-folder-properties.png)

可使用下列描述檔：

* [中繼資料設定檔](metadata-profiles.md) ，可讓您將預設中繼資料屬性套用至上傳至該資料夾的資產
* [處理設定檔](asset-microservices-configure-and-use.md#processing-profiles) ，可讓您套用轉譯處理，並除預設的轉譯外，還能產生轉譯

此外，如果您的環境中啟用了動態媒體：

* [動態媒體影像設定檔](dynamic-media/image-profiles.md) ，可讓您套用特定的裁切(**[!UICONTROL 智慧型裁切和像素裁切]** )，並將組態銳利化至上傳的資產。
* [動態媒體視訊設定檔](dynamic-media/video-profiles.md) ，可讓您套用特定的視訊編碼設定檔（解析度、格式、參數）。

>[!NOTE]
>
>動態媒體裁切和資產的其他操作不具破壞性，即不會變更上傳的原始內容，而是提供在傳送資產時要進行裁切或媒體轉換的參數

對於已指派處理設定檔的檔案夾，描述檔名稱會出現在卡片檢視的縮圖上。 在清單視圖中，配置檔案名稱將顯示在「處 **[!UICONTROL 理配置檔案]** 」列中。

## 使用API上傳或收錄資產 {#upload-using-apis}

開發人員參考的資產上傳區段中提供上傳API和通訊協定的技術詳細資訊，以及開放原始碼SDK和 [範例用戶端的連結](developer-reference-material-apis.md#asset-upload-technical) 。

>[!MORELIKETHIS]
>
>* [Adobe Experience manager 桌面應用程式](https://docs.adobe.com/content/help/zh-Hant/experience-manager-desktop-app/using/introduction.html)
>* [Adobe Asset Link](https://www.adobe.com/tw/creativecloud/business/enterprise/adobe-asset-link.html)
>* [Adobe Asset Link檔案](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html)
>* [資產上傳的技術參考](developer-reference-material-apis.md#asset-upload-technical)

