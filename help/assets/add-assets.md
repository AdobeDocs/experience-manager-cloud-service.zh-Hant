---
title: 將您的數位資產新增至 [!DNL Adobe Experience Manager]。
description: 將您的數位資產新增至 [!DNL Adobe Experience Manager] 作為 [!DNL Cloud Service]。
translation-type: tm+mt
source-git-commit: 7e8c794752073da0b4815c97dc53282989cd3fb5
workflow-type: tm+mt
source-wordcount: '1930'
ht-degree: 1%

---


# 將數位資產新增至Adobe Experience Manager {#add-assets-to-experience-manager}

[!DNL Adobe Experience Manager] 透過豐富的中繼資料、智慧標籤、轉譯和其他數位資產管理(DAM)服務，豐富上傳數位檔案的二進位內容。您可以從本機資料夾或網路磁碟機上傳各種檔案類型，例如影像、檔案和原始影像檔案至[!DNL Experience Manager Assets]。

提供了多種上載方法。 除了最常用的瀏覽器上傳外，還有其他將資產新增至[!DNL Experience Manager]儲存庫的方法，包括案頭用戶端（例如Adobe Asset Link或[!DNL Experience Manager]案頭應用程式）、上傳和擷取指令碼，以及自動擷取整合新增至[!DNL Experience Manager]擴充功能。

我們將著重於此處為使用者上傳方法，並提供文章連結，說明使用[!DNL Experience Manager] API和SDK進行資產上傳和擷取的技術層面。

雖然您可以上傳並管理[!DNL Experience Manager]中的任何二進位檔案，但最常用的檔案格式支援其他服務，例如中繼資料擷取或預覽／轉譯產生。 如需詳細資訊，請參閱[支援的檔案格式](file-format-support.md)。

您也可以選擇對已上傳的資產進行其他處理。 可在上傳資產的資料夾上設定多個資產處理設定檔，以新增特定中繼資料、轉譯或影像處理服務。 請參閱[上載時處理資產](#process-when-uploaded)。

>[!NOTE]
>
>[!DNL Experience Manager] 運用 [!DNL Cloud Service] 新的上傳資產方式——直接二進位上傳。預設會支援現成可用的產品功能和用戶端，例如[!DNL Experience Manager]使用者介面、[!DNL Adobe Asset Link]、[!DNL Experience Manager]案頭應用程式，因此對一般使用者是透明的。
>
>上傳由技術團隊自訂或擴充的程式碼，客戶需要使用新的上傳API和通訊協定。

資產(a [!DNL Cloud Service])提供下列上傳方法。 Adobe建議您先瞭解上傳選項的使用案例和適用性，再加以使用。

| 上傳方法 | 何時使用？ | 主要角色 |
|---------------------|----------------|-----------------|
| [Assets Console使用者介面](#upload-assets) | 偶爾上傳、輕鬆壓制和拖曳、搜尋器上傳。 請勿用來上傳大量資產。 | 所有使用者 |
| [上傳API](#upload-using-apis) | 用於上傳期間的動態決策。 | 開發人員 |
| [[!DNL Experience Manager] 案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | 大量資產擷取量低，但適用於移轉。 | 管理員、行銷人員 |
| [[!DNL Adobe Asset Link]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html) | 當創意人員和行銷人員從支援的[!DNL Creative Cloud]案頭應用程式中處理資產時，就很有用。 | 創意，行銷人員 |
| [資產大量內嵌](#asset-bulk-ingestor) | 建議進行大規模遷移和偶爾批量提取。 僅適用於支援的資料儲存區。 | 管理員、開發人員 |

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

您可以上傳與現有資產路徑相同（相同名稱和位置）的資產。 但是，會顯示一個警告對話方塊，其中包含下列選項：

* 取代現有資產：如果您取代現有資產，資產的中繼資料以及您對現有資產所做的任何先前修改（例如註解、裁切等）都會被刪除。
* 建立其他版本：系統會在儲存庫中建立現有資產的新版本。 您可以在[!UICONTROL 時間軸]中檢視兩個版本，並視需要回復為先前現有的版本。
* 保留兩者：如果您選擇保留這兩個資產，新資產會重新命名，名稱會附加數字`1`。

>[!NOTE]
>
>當您在[!UICONTROL 名稱衝突]對話方塊中選取&#x200B;**[!UICONTROL 取代]**&#x200B;時，會重新產生新資產的資產ID。 此ID與先前資產的ID不同。
>
>如果啟用「資產前瞻分析」以追蹤[!DNL Adobe Analytics]的曝光或點按次數，則重新產生的資產ID會使[!DNL Analytics]上為資產擷取的資料無效。

若要保留[!DNL Assets]中的重複資產，請按一下「保留&#x200B;**[!UICONTROL 」。]**&#x200B;若要刪除您上傳的重複資產，請點選／按一下「刪除&#x200B;**[!UICONTROL 」。]**

### 檔案名稱處理與禁止字元{#filename-handling}

[!DNL Experience Manager Assets] 嘗試防止上傳檔案名稱中包含禁止字元的資產。如果您嘗試上傳包含不允許之字元或以上之檔案名稱的資產，[!DNL Assets]會顯示警告訊息並停止上傳，直到您移除這些字元或以允許的名稱上傳為止。 有些上傳方法不會阻止您上傳檔案名稱中包含禁止字元的資產，但會以`-`取代字元。

為符合貴組織的特定檔案命名慣例，[!UICONTROL 「上傳資產」對話方塊可讓您為上傳的檔案指定長名稱。 ]不支援下列（以空格分隔的）字元清單：

* 資產檔案名`* / : [ \\ ] | # % { } ? &`的字元無效
* 資產資料夾名稱`* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`的字元無效

## 大量上傳資產{#bulk-upload}

大量資產收錄者可有效處理數千個資產。 但是，大規模的擷取不只是廣泛、大型的檔案轉儲或盲目移轉。 若要讓它成為符合您商業目的的有意義專案，規劃和管理資產可帶來更有效率的擷取。 所有的收錄都不相同，如果不考慮細微的儲存庫組成和業務需求，就不能進行概括。 以下是規劃和執行大量擷取的主要建議：

* 組織資產：移除DAM中不需要的資產。 考慮移除未使用、過時或重複的資產。 如此可減少所傳輸的資料和所吸收的資產，進而加速擷取。
* 組織資產：請考慮依邏輯順序來組織內容，例如依檔案大小、檔案格式、使用案例或優先順序。 一般而言，大型的複雜檔案需要更多的處理。 您也可以考慮使用檔案大小篩選選項（如下所述）個別接收大型檔案。
* 交錯內嵌：請考慮將擷取分為多個大量擷取專案。 這可讓您更快查看內容，並視需要更新您的擷取。 例如，您可以在非尖峰時段內，或逐步在多個區塊內內嵌處理密集的資產。 不過，您可以一次收集較小且較簡單的資產，而不需要進行太多處理。

若要上傳更多檔案，請使用下列其中一種方法。 另請參閱[使用案例和方法](#upload-methods-comparison)

* [資產上傳API](developer-reference-material-apis.md#asset-upload-technical):使用自訂的上傳指令碼或工具，以利用API新增對資產的額外處理（例如，翻譯中繼資料或重新命名檔案）。
* [[!DNL Experience Manager] 案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html):適用於從本機檔案系統上傳資產的創意專業人員和行銷人員。使用它上傳可在本機使用的巢狀檔案夾。
* [大量擷取工具](#asset-bulk-ingestor):在部署時，偶爾或最初會用來擷取大量資產 [!DNL Experience Manager]。

### 資產大量收錄工具{#asset-bulk-ingestor}

此工具僅提供給管理員群組，用於從Azure或S3資料存放區大規模擷取資產。

若要設定工具，請依照下列步驟進行：

1. 導覽至「**[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 批量匯入]**」。 選擇&#x200B;**[!UICONTROL 建立]**&#x200B;選項。

![批量匯入程式的設定](assets/bulk-import-config.png)

1. 在[!UICONTROL 批量導入配置]頁上，提供所需值。

   * [!UICONTROL 標題]:描述性標題。
   * [!UICONTROL 匯入來源]:選擇適用的資料來源。
   * [!UICONTROL 依最小大小篩選]:以MB為單位，提供資產的最小檔案大小。
   * [!UICONTROL 依最大大小篩選]:以MB為單位，提供資產的檔案大小上限。
   * [!UICONTROL 排除Mime類型]:要從擷取中排除的MIME類型清單（以逗號分隔）。例如，`image/jpeg, image/.*, video/mp4`。
   * [!UICONTROL 包含Mime類型]:要包含在擷取中的MIME類型清單（以逗號分隔）。請參閱[所有支援的檔案格式](/help/assets/file-format-support.md)。
   * [!UICONTROL 匯入模式]:選擇「跳過」、「替換」或「建立版本」。「跳過」模式是預設模式，在此模式中，ingestor會跳過以匯入資產（如果資產已存在）。 請參閱[replace和create version options](#handling-upload-existing-file)的含義。
   * [!UICONTROL 資產目標資料夾]:在要匯入資產的DAM中匯入資料夾。例如， `/content/dam/imported_assets`

1. 您可以刪除、修改、執行和執行您所建立的收錄機組態。 當您選取大量匯入登入設定時，工具列中會提供下列選項。

   * [!UICONTROL 編輯]:編輯選定的配置。
   * [!UICONTROL 刪除]:刪除選定的配置。
   * [!UICONTROL 檢查]:驗證與資料儲存的連接。
   * [!UICONTROL 乾涸]:叫用大量擷取的測試執行。
   * [!UICONTROL 執行]:執行所選配置。
   * [!UICONTROL 停止]:終止活動配置。
   * [!UICONTROL 工作狀態]:查看配置在正在進行的導入作業中使用或用於已完成作業時的狀態。
   * [!UICONTROL 檢視資產]:查看目標資料夾（如果存在）。

>[!NOTE]
>
>在設定並部署至[!DNL Experience Manager]時，若要從其他系統進行內容移轉，則需要仔細規劃、考慮和選擇工具，以進行大量上傳。 請參閱[部署指南](/help/implementing/deploying/overview.md)以取得內容移轉方法的指引。

## 使用案頭用戶端上傳資產{#upload-assets-desktop-clients}

除了網頁瀏覽器使用者介面外，[!DNL Experience Manager]還支援案頭上的其他用戶端。 它們也提供上傳體驗，而不需前往網頁瀏覽器。

* [[!DNL Adobe Asset Link]](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html) 可讓您存取Adobe Photoshop、 [!DNL Experience Manager] Adobe Illustrator和Adobe InDesign案頭應用程式中的資產。您可以直接從這些案頭應用程式內的Adobe Asset Link使用者介面，將目前開啟的檔案上傳至[!DNL Experience Manager]。
* [[!DNL Experience Manager] 案頭應](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) 用程式可簡化在案頭上處理資產的作業，不受檔案類型或處理資產的原生應用程式所限。從本機檔案系統上傳巢狀檔案夾階層中的檔案特別有用，因為瀏覽器上傳僅支援上傳平面檔案清單。

## 上傳{#process-when-uploaded}時處理資產

若要對已上傳的資產進行其他處理，您可以在上傳檔案夾上套用處理設定檔。 配置檔案可在[!DNL Assets]資料夾的&#x200B;**[!UICONTROL 屬性]**&#x200B;頁中使用。

![assets-folder-properties](assets/assets-folder-properties.png)

可使用下列標籤：

* [中繼資](metadata-profiles.md) 料設定檔可讓您將預設中繼資料屬性套用至上傳至該資料夾的資產
* [處理](asset-microservices-configure-and-use.md) 分析工具可讓您產生的轉譯數，預設為多於可能的轉譯數。

此外，如果您的部署已啟用[!DNL Dynamic Media]，則可使用下列標籤：

* [動態媒體影像](dynamic-media/image-profiles.md) 分析工具可讓您套用特定的裁切(**[!UICONTROL 智慧]** 裁切和像素裁切)，並銳利化已上傳資產的設定。
* [動態媒體視訊](dynamic-media/video-profiles.md) 設定檔可讓您套用特定的視訊編碼設定檔（解析度、格式、參數）。

>[!NOTE]
>
>動態媒體裁切和資產的其他操作不具破壞性，即不會變更上傳的原始內容，而是提供在傳送資產時要進行裁切或媒體轉換的參數

對於已指派處理設定檔的檔案夾，描述檔名稱會出現在卡片檢視的縮圖上。 在清單視圖中，配置檔案名稱將顯示在&#x200B;**[!UICONTROL 處理配置檔案]**&#x200B;列中。

## 使用API {#upload-using-apis}上傳或收錄資產

開發人員參考的[asset upload](developer-reference-material-apis.md#asset-upload-technical)區段中提供上傳API和通訊協定的技術詳細資訊，以及開放原始碼SDK和範例用戶端的連結。

>[!MORELIKETHIS]
>
>* [[!DNL Adobe Experience Manager] 案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html)
>* [關於 [!DNL Adobe Asset Link]](https://www.adobe.com/tw/creativecloud/business/enterprise/adobe-asset-link.html)
>* [[!DNL Adobe Asset Link] 文件](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)
>* [資產上傳的技術參考](developer-reference-material-apis.md#asset-upload-technical)

