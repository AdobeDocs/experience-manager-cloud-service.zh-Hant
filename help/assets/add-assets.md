---
title: 將您的數位資產新增至 [!DNL Adobe Experience Manager]。
description: 將您的數位資產新增至 [!DNL Adobe Experience Manager] 做為雲端服務。
translation-type: tm+mt
source-git-commit: 9c42bd216edd0174c9a4c9b706c0e08ca36428f6
workflow-type: tm+mt
source-wordcount: '1494'
ht-degree: 1%

---


# 將數位資產新增至Adobe Experience Manager {#add-assets-to-experience-manager}

[!DNL Adobe Experience Manager] 透過豐富的中繼資料、智慧標籤、轉譯和其他數位資產管理(DAM)服務，豐富上傳數位檔案的二進位內容。您可以從本機資料夾或網路磁碟機上傳各種檔案類型，例如影像、檔案和原始影像檔案至[!DNL Experience Manager Assets]。

提供了多種上載方法。 除了最常用的瀏覽器上傳外，還有其他將資產新增至Experience Manager儲存庫的方法，包括案頭用戶端（例如Adobe Asset Link或Experience Manager案頭應用程式）、上傳和擷取指令碼，以及自動擷取整合（新增為Experience Manager擴充功能）。

我們將著重在此處為使用者上傳方法，並提供文章連結，說明使用Experience Manager API和SDK進行資產上傳和擷取的技術層面。

雖然您可以在Experience Manager中上傳和管理任何二進位檔案，但最常用的檔案格式支援其他服務，例如中繼資料擷取或預覽／轉譯產生。 如需詳細資訊，請參閱[支援的檔案格式](file-format-support.md)。

您也可以選擇對已上傳的資產進行其他處理。 可在上傳資產的資料夾上設定多個資產處理設定檔，以新增特定中繼資料、轉譯或影像處理服務。 如需詳細資訊，請參閱下方的[其他處理](#additional-processing)。

>[!NOTE]
>
>Experience Manager作為雲端服務，運用了新的上傳資產方式——直接二進位上傳。 預設會支援立即可用的產品功能和用戶端，例如Experience Manager使用者介面、Adobe Asset Link、Experience Manager案頭應用程式，因此對一般使用者是透明的。
>
>上傳由技術團隊自訂或擴充的程式碼，客戶需要使用新的上傳API和通訊協定。

## 上傳資產{#upload-assets}

<!-- #ENGCHECK do we support pausing? I couldn't get pause to show with 1.5GB upload.... If not, this should be removed#

   You can pause the uploading of large assets (greater than 500 MB) and resume it later from the same page. Tap the **[!UICONTROL Pause]** icon beside progress bar that appears when an upload starts.

   ![chlimage_1-211](assets/chlimage_1-211.png)

   The size above which an asset is considered a large asset is configurable. For example, you can configure the system to consider assets above 1000 MB (instead of 500 MB) as large assets. In this case, **[!UICONTROL Pause]** appears on the progress bar when assets of size greater than 1000 MB are uploaded.

   The Pause button does not show if a file greater than 1000 MB is uploaded with a file less than 1000 MB. However, if you cancel the less than 1000 MB file upload, the **[!UICONTROL Pause]** button appears.

   To modify the size limit, configure the `chunkUploadMinFileSize` property of the `fileupload`node in the CRX repository.

   When you click the **[!UICONTROL Pause]** icon, it toggles to a **[!UICONTROL Play]** icon. To resume uploading, click the **[!UICONTROL Play]** icon.

   ![chlimage_1-212](assets/chlimage_1-212.png)
-->

<!-- #ENGCHECK do we support pausing? I couldn't get pause to show with 1.5GB upload.... If not, this should be removed#
   The ability to resume uploading is especially helpful in low-bandwidth scenarios and network glitches, where it takes a long time to upload a large asset. You can pause the upload operation and continue later when the situation improves. When you resume, uploading starts from the point where you paused it.
-->

<!-- #ENGCHECK assuming this is not relevant? remove after confirming#
   During the upload operation, [!DNL Experience Manager] saves the portions of the asset being uploaded as chunks of data in the CRX repository. When the upload completes, [!DNL Experience Manager] consolidates these chunks into a single block of data in the repository.

   To configure the cleanup task for the unfinished chunk upload jobs, go to `https://[aem_server]:[port]/system/console/configMgr/org.apache.sling.servlets.post.impl.helper.ChunkCleanUpTask`.
-->

若要上傳檔案（或多個檔案），您可以在案頭上選取檔案，然後拖曳使用者介面（網頁瀏覽器）至目標資料夾。 或者，您也可以從使用者介面開始上傳。

1. 在[!DNL Assets]使用者介面中，導覽至您要新增數位資產的位置。
1. 若要上傳資產，請執行下列其中一項作業：

   * 在工具列上，按一下「建立&#x200B;**** > **[!UICONTROL 檔案]**」。 如有需要，可在顯示的對話框中更名檔案。
   * 在支援HTML5的瀏覽器中，直接將資產拖曳至[!DNL Assets]使用者介面。 不會顯示要更名檔案的對話框。

   ![create_menu](assets/create_menu.png)

   要選擇多個檔案，請選擇`Ctrl`或`Command`鍵，然後在檔案選擇器對話框中選擇資產。 使用iPad時，一次只能選取一個檔案。

1. 若要取消正在進行的上傳，請按一下進度列旁的關閉(`X`)。 當您取消上傳作業時，[!DNL Assets]會刪除部分上傳的資產。
如果您在上傳檔案之前取消上傳作業，[!DNL Assets]會停止上傳目前的檔案並重新整理內容。 不過，已上傳的檔案不會刪除。

1. [!DNL Assets]中的上載進度對話框顯示成功上載檔案的計數以及無法上載的檔案。
此外，[!DNL Assets]使用者介面會顯示您上傳的最新資產或您先建立的資料夾。

>[!NOTE]
>
>若要上傳巢狀資料夾階層，請參閱[大量上傳資產](#bulk-upload)。

<!-- #ENGCHECK I'm assuming this is no longer relevant.... If yes, this should be removed#

### Serial uploads {#serialuploads}

Uploading numerous assets in bulk consumes significant I/O resources, which may adversely impact the performance of [!DNL Assets]. In particular, if you have a slow internet connection, the time to upload drastically increases due to a spike in disk I/O. Moreover, your web browser may introduce additional restrictions to the number of POST requests [!DNL Assets] can handle for concurrent asset uploads. As a result, the upload operation fails or terminate prematurely. In other words, [!DNL Assets] may miss some files while ingesting a bunch of files or altogether fail to ingest any file.

To overcome this situation, [!DNL Assets] ingests one asset at a time (serial upload) during a bulk upload operation, instead of the concurrently ingesting all the assets.

Serial uploading of assets is enabled by default. To disable the feature and allow concurrent uploading, overlay the `fileupload` node in Crx-de and set the value of the `parallelUploads` property to `true`.

### Streamed uploads {#streamed-uploads}

If you upload many assets to [!DNL Experience Manager], the I/O requests to server increase drastically, which reduces the upload efficiency and can even cause some upload task to time out. [!DNL Assets] supports streamed uploading of assets. Streamed uploading reduces the disk I/O during the upload operation by avoiding asset storage in a temporary folder on the server before copying it to the repository. Instead, the data is transferred directly to the repository. This way, the time to upload large assets and the possibility of timeouts is reduced. Streamed upload is enabled by default in [!DNL Assets].

>[!NOTE]
>
>Streaming upload is disabled for [!DNL Experience Manager] running on JEE server with servlet-api version lower than 3.1.
-->

### 處理資產已存在時的上載{#handling-upload-existing-file}

如果您上傳的資產名稱與資產名稱相同，且資產已在上傳資產的位置使用，則會顯示警告對話方塊。

您可以選擇取代現有資產、建立其他版本，或借由重新命名已上傳的新資產來保留兩者。 如果您取代現有資產，資產的中繼資料以及您對現有資產所做的任何先前修改（例如註解、裁切等）都會被刪除。 如果您選擇保留這兩個資產，新資產會重新命名，名稱會附加數字`1`。

>[!NOTE]
>
>當您在[!UICONTROL 名稱衝突]對話方塊中選取&#x200B;**[!UICONTROL 取代]**&#x200B;時，會重新產生新資產的資產ID。 此ID與先前資產的ID不同。
>
>如果「資產前瞻分析」已啟用，可以使用Adobe Analytics追蹤曝光／點按次數，則重新產生的資產ID會使Analytics上為資產擷取的資料無效。

若要保留[!DNL Assets]中的重複資產，請按一下「保留&#x200B;**[!UICONTROL 」。]**&#x200B;若要刪除您上傳的重複資產，請點選／按一下「刪除&#x200B;**[!UICONTROL 」。]**

### 檔案名稱處理與禁止字元{#filename-handling}

[!DNL Experience Manager Assets] 防止您上傳檔案名稱中包含禁止字元的資產。如果您嘗試上傳包含不允許之字元或以上之檔案名稱的資產，[!DNL Assets]會顯示警告訊息並停止上傳，直到您移除這些字元或以允許的名稱上傳為止。

為符合貴組織的特定檔案命名慣例，[!UICONTROL 「上傳資產」對話方塊可讓您為上傳的檔案指定長名稱。]

但是，不支援下列（以空格分隔的）字元清單：

* 資產檔案名稱不可包含`* / : [ \\ ] | # % { } ? &`
* 資產資料夾名稱不可包含`* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

## 大量上傳資產{#bulk-upload}

若要上傳更多檔案，請使用下列其中一種方法。 另請參閱[使用案例和方法](#upload-methods-comparison)

* [資產上傳API](developer-reference-material-apis.md#asset-upload-technical):使用自訂的上傳指令碼或工具，以利用API新增對資產的額外處理（例如，翻譯中繼資料或重新命名檔案）。
* [Experience Manager案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html):適用於從本機檔案系統上傳資產的創意專業人員和行銷人員。使用它上傳可在本機使用的巢狀檔案夾。
* [大量擷取工具](#bulk-ingestion-tool):在部署時，偶爾或最初會用來擷取大量資產 [!DNL Experience Manager]。

### 大量資產擷取工具{#bulk-ingestion-tool}

新增下列詳細資訊：

* 此方法的使用案例。
* 適用角色
* 配置步驟
* 如何管理擷取工作並查看狀態。
* 要記住的管理或組織要收錄的資產。

若要設定工具，請依照下列步驟進行：

1. 建立大量匯入設定。  導覽至「工具>資產>大量匯入>選取「建立」按鈕。

![批量匯入程式的設定](assets/bulk-import-config.png)

1. 提供適當的詳細資訊。

>[!NOTE]
>
>在設定和部署至Experience Manager時，若要從其他系統進行內容移轉，就必須仔細規劃、考慮和選擇工具，才能進行大量上傳。 請參閱[部署指南](/help/implementing/deploying/overview.md)以取得內容移轉方法的指引。

## 使用案頭用戶端上傳資產{#upload-assets-desktop-clients}

除了網頁瀏覽器使用者介面外，Experience Manager還支援案頭上的其他用戶端。 它們也提供上傳體驗，而不需前往網頁瀏覽器。

* [Adobe Asset ](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html) Link可讓您存取Adobe Photoshop、Adobe Illustrator [!DNL Experience Manager] 和Adobe InDesign案頭應用程式中的資產。您可以直接從這些案頭應用程式內的Adobe Asset Link使用者介面，將目前開啟的檔案上傳至[!DNL Experience Manager]。
* [Experience Manager案頭應](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) 用程式可簡化在案頭上處理資產的作業，不受檔案類型或處理資產的原生應用程式所限。從本機檔案系統上傳巢狀檔案夾階層中的檔案特別有用，因為瀏覽器上傳僅支援上傳平面檔案清單。

## 其他處理{#additional-processing}

為了對已上傳的資產進行額外處理，您可以在上傳資產的資料夾上使用資產處理設定檔。 它們可在資料夾&#x200B;**[!UICONTROL 屬性]**&#x200B;中使用。

![assets-folder-properties](assets/assets-folder-properties.png)

可使用下列描述檔：

* [中繼資](metadata-profiles.md) 料設定檔可讓您將預設中繼資料屬性套用至上傳至該資料夾的資產
* [處理](asset-microservices-configure-and-use.md) 分析工具可讓您產生的轉譯數，預設為多於可能的轉譯數。

此外，如果您的環境中啟用了動態媒體：

* [動態媒體影像](dynamic-media/image-profiles.md) 分析工具可讓您套用特定的裁切(**[!UICONTROL 智慧]** 裁切和像素裁切)，並銳利化已上傳資產的設定。
* [動態媒體視訊](dynamic-media/video-profiles.md) 設定檔可讓您套用特定的視訊編碼設定檔（解析度、格式、參數）。

>[!NOTE]
>
>動態媒體裁切和資產的其他操作不具破壞性，即不會變更上傳的原始內容，而是提供在傳送資產時要進行裁切或媒體轉換的參數

對於已指派處理設定檔的檔案夾，描述檔名稱會出現在卡片檢視的縮圖上。 在清單視圖中，配置檔案名稱將顯示在&#x200B;**[!UICONTROL 處理配置檔案]**&#x200B;列中。

## 使用API {#upload-using-apis}上傳或收錄資產

開發人員參考的[asset upload](developer-reference-material-apis.md#asset-upload-technical)區段中提供上傳API和通訊協定的技術詳細資訊，以及開放原始碼SDK和範例用戶端的連結。

## 基於方案的上載方法{#upload-methods-comparison}

| 上傳方法 | 何時使用？ | 主要角色（管理員、開發人員、創意使用者、行銷人員） |
|---------------------|-------------------------------------------------------------------------------------------|------------|
| 資產主控台/UI | 偶爾上傳、輕鬆壓制和拖曳、搜尋器上傳。 不適用於大量擷取。 | 全部 |
| 上傳API | 在上傳期間動態決策資產 | 開發人員 |
| 案頭應用程式 | 大量資產攝取量低，但適用於遷移 | 管理員、行銷人員 |
| 資產連結 | 創意人員和行銷人員可從支援的Creative Cloud案頭應用程式中協作資產。 | 創意，行銷人員 |
| 大量擷取工具 | 從資料儲存區大量擷取資產。  建議進行遷移和偶爾大量收錄。 | 管理員、開發人員 |

說明何時使用哪種方法。

>[!MORELIKETHIS]
>
>* [Adobe Experience manager 桌面應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html)
>* [Adobe Asset Link](https://www.adobe.com/tw/creativecloud/business/enterprise/adobe-asset-link.html)
>* [Adobe Asset Link檔案](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)
>* [資產上傳的技術參考](developer-reference-material-apis.md#asset-upload-technical)

