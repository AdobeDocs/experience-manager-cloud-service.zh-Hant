---
title: 將數字資產添加到 [!DNL Adobe Experience Manager]。
description: 將數字資產添加到 [!DNL Adobe Experience Manager] 作為 [!DNL Cloud Service]。
feature: Asset Management,Upload
role: User,Admin
exl-id: 0e624245-f52e-4082-be21-13cc29869b64
source-git-commit: c4f6f5925f7c80bae756610eae9b3b7200e9e8f9
workflow-type: tm+mt
source-wordcount: '2943'
ht-degree: 0%

---

# 將數字資產添加到 [!DNL Adobe Experience Manager] 作為 [!DNL Cloud Service] [!DNL Assets] {#add-assets-to-experience-manager}

[!DNL Adobe Experience Manager Assets] 接受來自多種來源的多種類型的數字資產。 它儲存二進位檔案和建立的格式副本，可以使用各種工作流和 [!DNL Adobe Sensei] 服務，允許通過多個渠道在多個表面上分發。

[!DNL Adobe Experience Manager] 通過豐富的元資料、智慧標籤、格式副本和其他數字資產管理(DAM)服務，豐富了上傳的數字檔案的二進位內容。 您可以從本地資料夾或網路驅動器上載各種類型的檔案，如影像、文檔和原始影像檔案 [!DNL Experience Manager Assets]。

除了最常用的瀏覽器上載外，還有向 [!DNL Experience Manager] 存在儲存庫，包括案頭客戶端，如Adobe資產連結或 [!DNL Experience Manager] 案頭應用、上傳和接收指令碼，以及添加為 [!DNL Experience Manager] 擴展。

當您可以在中上載和管理任何二進位檔案時 [!DNL Experience Manager]，最常用的檔案格式支援其他服務，如元資料提取或預覽/格式副本生成。 請參閱 [支援的檔案格式](file-format-support.md) 的雙曲餘切值。

您也可以選擇對上載的資產執行附加處理。 可以在上載資產的資料夾上配置多個資產處理配置檔案，以添加特定元資料、格式副本或影像處理服務。 請參閱 [上載時處理資產](#process-when-uploaded)。

[!DNL Assets] 提供了以下上載方法。 Adobe建議您在使用上載選項之前瞭解其使用案例和適用性。

| 上載方法 | 何時使用？ | 主要角色 |
|---------------------|----------------|-----------------|
| [資產控制台用戶介面](#upload-assets) | 偶爾上載、輕鬆按下和拖動、查找器上載。 不要用於上載大量資產。 | 所有用戶 |
| [上載API](#upload-using-apis) | 用於上載期間的動態決策。 | 開發人員 |
| [[!DNL Experience Manager] 桌面應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | 低容量資產攝取，但不用於遷移。 | 管理員、營銷員 |
| [[!DNL Adobe Asset Link]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html) | 當創意人員和營銷人員從受支援者內部處理資產時非常有用 [!DNL Creative Cloud] 案頭應用。 | 創意，營銷 |
| [資產批量導入](#asset-bulk-ingestor) | 建議進行大規模遷移和偶爾進行批量遷移。 僅用於支援的資料儲存。 | 管理員、開發人員 |

## 上傳資產 {#upload-assets}

<!-- #ENGCHECK do we support pausing? I couldn't get pause to show with 1.5GB upload.... If not, this should be removed#

   You can pause the uploading of large assets (greater than 500 MB) and resume it later from the same page. Tap the **[!UICONTROL Pause]** icon beside progress bar that appears when an upload starts.

   The size above which an asset is considered a large asset is configurable. For example, you can configure the system to consider assets above 1000 MB (instead of 500 MB) as large assets. In this case, **[!UICONTROL Pause]** appears on the progress bar when assets of size greater than 1000 MB are uploaded.

   The [!UICONTROL Pause] option does not show if a file greater than 1000 MB is uploaded with a file less than 1000 MB. However, if you cancel the less than 1000 MB file upload, the **[!UICONTROL Pause]** option appears.

   To modify the size limit, configure the `chunkUploadMinFileSize` property of the `fileupload` node in the CRX repository.

   When you click the **[!UICONTROL Pause]** icon, it toggles to a **[!UICONTROL Play]** icon. To resume uploading, click **[!UICONTROL Play]** option.
-->

<!-- #ENGCHECK do we support pausing? I couldn't get pause to show with 1.5GB upload.... If not, this should be removed#
   The ability to resume uploading is especially helpful in low-bandwidth scenarios and network glitches, where it takes a long time to upload a large asset. You can pause the upload operation and continue later when the situation improves. When you resume, uploading starts from the point where you paused it.
-->

<!-- #ENGCHECK assuming this is not relevant? remove after confirming#
   During the upload operation, [!DNL Experience Manager] saves the portions of the asset being uploaded as chunks of data in the CRX repository. When the upload completes, [!DNL Experience Manager] consolidates these chunks into a single block of data in the repository.

   To configure the cleanup task for the unfinished chunk upload jobs, go to `https://[aem_server]:[port]/system/console/configMgr/org.apache.sling.servlets.post.impl.helper.ChunkCleanUpTask`.
-->

要上載檔案（或多個檔案），可以在案頭上選擇它們，然後在用戶介面（Web瀏覽器）上拖動到目標資料夾。 或者，可以從用戶介面啟動上載。

1. 在 [!DNL Assets] 用戶介面，導航到要添加數字資產的位置。
1. 要上載資產，請執行以下操作之一：

   * 在工具欄上，按一下 **[!UICONTROL 建立]** > **[!UICONTROL 檔案]**。 如果需要，可在顯示的對話框中更名檔案。
   * 在支援HTML5的瀏覽器中，將資產直接拖到 [!DNL Assets] 用戶介面。 不顯示要更名檔案的對話框。

   ![建立菜單](assets/create_menu.png)

   要選擇多個檔案，請選擇 `Ctrl` 或 `Command` 鍵，然後在檔案選取器對話框中選擇資產。 使用iPad時，一次只能選擇一個檔案。

1. 要取消正在進行的上載，請按一下「關閉」(`X`)。 取消上載操作後， [!DNL Assets] 刪除資產的部分上載部分。
如果在上載檔案之前取消上載操作， [!DNL Assets] 停止上載當前檔案並刷新內容。 但是，不會刪除已上載的檔案。

1. 上載進度對話框 [!DNL Assets] 顯示成功上載的檔案和無法上載的檔案的計數。
另外， [!DNL Assets] 用戶介面顯示您上載的最新資產或您首先建立的資料夾。

>[!NOTE]
>
>要上載嵌套資料夾層次結構，請參閱 [批量上載資產](#bulk-upload)。

<!-- #ENGCHECK I'm assuming this is no longer relevant.... If yes, this should be removed#

### Serial uploads {#serialuploads}

Uploading numerous assets in bulk consumes significant I/O resources, which may adversely impact the performance of [!DNL Assets]. In particular, if you have a slow internet connection, the time to upload drastically increases due to a spike in disk I/O. Moreover, your web browser may introduce additional restrictions to the number of POST requests [!DNL Assets] can handle for concurrent asset uploads. As a result, the upload operation fails or terminate prematurely. In other words, [!DNL Assets] may miss some files while ingesting a bunch of files or altogether fail to ingest any file.

To overcome this situation, [!DNL Assets] ingests one asset at a time (serial upload) during a bulk upload operation, instead of the concurrently ingesting all the assets.

Serial uploading of assets is enabled by default. To disable the feature and allow concurrent uploading, overlay the `fileupload` node in CRX-DE and set the value of the `parallelUploads` property to `true`.

### Streamed uploads {#streamed-uploads}

If you upload many assets to [!DNL Experience Manager], the I/O requests to server increase drastically, which reduces the upload efficiency and can even cause some upload task to time out. [!DNL Assets] supports streamed uploading of assets. Streamed uploading reduces the disk I/O during the upload operation by avoiding asset storage in a temporary folder on the server before copying it to the repository. Instead, the data is transferred directly to the repository. This way, the time to upload large assets and the possibility of timeouts is reduced. Streamed upload is enabled by default in [!DNL Assets].

>[!NOTE]
>
>Streaming upload is disabled for [!DNL Experience Manager] running on JEE server with servlet-api version lower than 3.1.
-->

### 在資產已存在時處理上載 {#handling-upload-existing-file}

您可以上載與現有資產路徑（相同名稱和位置）相同的資產。 但是，將顯示一個警告對話框，其中包含以下選項：

* 替換現有資產：如果替換現有資產，則資產的元資料以及您對現有資產所做的任何先前修改（例如注釋、裁剪等）都將被刪除。

   >[!NOTE]
   >
   >如果資產已鎖定或簽出，則替換資產的選項不可用。

* 建立其他版本：在儲存庫中建立現有資產的新版本。 您可以在 [!UICONTROL 時間軸] 並可以根據需要恢復到以前的現有版本。
* 同時保留：如果選擇保留這兩個資產，則將更名新資產。

將重複資產保留在 [!DNL Assets]按一下 **[!UICONTROL 保留]**。 要刪除上載的重複資產，請按一下 **[!UICONTROL 刪除]**。

### 檔案名處理和禁止字元 {#filename-handling}

[!DNL Experience Manager Assets] 阻止您使用其檔案名中的禁止字元上載資產。 如果嘗試上載檔案名中包含不允許的字元或更多字元的資產， [!DNL Assets] 顯示警告消息並停止上載，直到您刪除這些字元或使用允許的名稱上載。

要適合組織的特定檔案命名約定， [!UICONTROL 上載資產] 對話框用於為上載的檔案指定長名稱。 不支援以下（以空格分隔的）字元清單：

* 資產名稱的字元無效： `* / : [ \\ ] | # % { } ? &`
* 資產資料夾名稱的字元無效： `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

## 批量上載資產 {#bulk-upload}

批量資產接收方可以高效地處理大量資產。 但是，大規模攝取不僅是大檔案轉儲或隨意遷移。 如果要進行大規模接收，以成為符合您業務目的且高效的有意義項目，請規劃遷移並管理資產組織。 所有的選擇都不同，因此在細緻的儲存庫組成和業務需求中，不是籠統地考慮因素。 以下是一些總體建議，用於規劃和執行批量攝取：

* 庫存資產：刪除DAM中不需要的資產。 請考慮刪除未使用、過時或重複的資產。 這減少了資料傳輸和接收的資產，從而加快了接收速度。
* 組織資產：請考慮按某種邏輯順序組織內容，例如按檔案大小、檔案格式、用例或優先順序。 通常，大型複雜檔案需要更多處理。 也可以考慮使用檔案大小篩選選項（如下所述）單獨接收大檔案。
* 錯位攝取：考慮將你的攝取分解為多個批量攝取項目。 這樣，您就可以更快查看內容，並根據需要更新您的攝取。 例如，您可以在非高峰時段或以多個塊逐漸接收處理密集型資產。 但是，您可以一次性接收較小、更簡單的資產，而這些資產不需要多少處理。

要上載更多檔案，請使用以下方法之一。 另請參見 [使用案例和方法](#upload-methods-comparison)

* [資產上載API](developer-reference-material-apis.md#asset-upload):如果需要，請使用利用API添加其他資產處理（例如，轉換元資料或更名檔案）的自定義上載指令碼或工具。
* [[!DNL Experience Manager] 案頭應用](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html):對於從本地檔案系統上傳資產的創意專業人員和營銷人員非常有用。 使用它上載本地可用的嵌套資料夾。
* [批量攝取工具](#asset-bulk-ingestor):在部署時偶爾或最初用於攝取大量資產 [!DNL Experience Manager]。

### 資產批量導入工具 {#asset-bulk-ingestor}

該工具僅提供給管理員組，用於從Azure或S3資料儲存中大規模接收資產。 查看配置和攝取的視頻瀏覽。

>[!VIDEO](https://video.tv.adobe.com/v/329680/?quality=12&learn=on)

下圖說明了從資料儲存中將資產Experience Manager時的各個階段：

![批量攝取工具](assets/bulk-ingestion.png)

**必備條件**

使用此功能需要Azure或AWS的外部儲存帳戶或儲存桶。

>[!NOTE]
>
>將儲存帳戶容器或儲存桶建立為專用，並僅接受來自授權請求的連接。 但是，不支援對入口網路連接的其他限制。

### 配置批量導入工具 {#configure-bulk-ingestor-tool}

要配置批量導入工具，請執行以下步驟：

1. 導航到 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 批量導入]**。 選擇 **[!UICONTROL 建立]** 的雙曲餘切值。

1. 指定批量導入配置的標題 **[!UICONTROL 標題]** 的子菜單。

1. 從 **[!UICONTROL 導入源]** 下拉清單。

1. 提供值以建立與資料源的連接。 例如，如果您選擇 **Azure Blob儲存** 作為資料源，指定Azure儲存帳戶、Azure Blob容器和Azure訪問密鑰的值。

1. 提供根資料夾的名稱，該根資料夾包含位於 **[!UICONTROL 源資料夾]** 的子菜單。

1. （可選）提供以MB為單位的資產的最小檔案大小，以將其包括在 **[!UICONTROL 按最小大小篩選]** 的子菜單。

1. （可選）提供資產的最大檔案大小(MB)，以將其包括在 **[!UICONTROL 按最大大小篩選]** 的子菜單。

1. （可選）指定要從中的接收中排除的以逗號分隔的MIME類型清單 **[!UICONTROL 排除MIME類型]** 的子菜單。 比如說， `image/jpeg, image/.*, video/mp4`。 請參閱 [所有受支援的檔案格式](/help/assets/file-format-support.md)。

1. 指定要從中的接收包含的以逗號分隔的MIME類型清單 **[!UICONTROL 包括MIME類型]** 的子菜單。 請參閱 [所有受支援的檔案格式](/help/assets/file-format-support.md)。

1. 選擇 **[!UICONTROL 導入後刪除源檔案]** 選項，在將原始檔案導入到 [!DNL Experience Manager]。

1. 選擇 **[!UICONTROL 導入模式]**。 選擇 **跳過**。 **替換**&#x200B;或 **建立版本**。 「跳過」模式是預設模式，在此模式下，如果資產已存在，則忽略該資產。 查看 [替換和建立版本選項](#handling-upload-existing-file)。

1. 指定路徑以定義DAM中要使用 **[!UICONTROL 資產目標資料夾]** 的子菜單。 比如說， `/content/dam/imported_assets`。

1. （可選）指定要導入的元資料檔案（以CSV格式提供）, **[!UICONTROL 元資料檔案]** 的子菜單。 在源blob位置中指定CSV檔案，並在配置批量導入工具時參考路徑。 在您 [批量導入和導出資產元資料](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/metadata-import-export.html)。 如果選擇 **導入後刪除源檔案** 選項，使用 **排除** 或 **包括MIME類型** 或 **按路徑/檔案篩選** 的子菜單。 可以使用規則運算式來過濾這些欄位中的CSV檔案。

1. 按一下 **[!UICONTROL 保存]** 的子菜單。

### 管理批量導入工具配置 {#manage-bulk-import-configuration}

在建立批量導入工具配置後，您可以執行評估配置的任務，然後將資產批量導入Experience Manager實例。 選擇可用的配置 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 批量導入]** 查看可用選項以管理批量導入工具配置。

### 編輯配置 {#edit-configuration}

選擇配置並按一下 **[!UICONTROL 編輯]** 修改配置詳細資訊。 執行編輯操作時，無法編輯配置和導入資料源的標題。

### 刪除配置 {#delete-configuration}

選擇配置並按一下 **[!UICONTROL 刪除]** 刪除批量導入配置。

### 驗證與資料源的連接 {#validate-connection}

選擇配置並按一下 **[!UICONTROL 檢查]** 驗證與資料源的連接。 如果連接成功，Experience Manager將顯示以下消息：

![批量導入成功消息](assets/bulk-import-success-message.png)

### 調用批量導入作業的test運行 {#invoke-test-run-bulk-import}

選擇配置並按一下 **[!UICONTROL 乾跑]** 調用批量導入作業的test運行。 Experience Manager顯示有關批量導入作業的以下詳細資訊：

![試執行結果](assets/dry-assets-result.png)

### 在批量導入期間處理檔案名 {#filename-handling-bulkimport}

批量導入資產或資料夾時， [!DNL Experience Manager Assets] 導入輸入源中存在的全部結構。 [!DNL Experience Manager] 遵循資產名稱和資料夾名稱中特殊字元的內置規則，因此這些檔案名需要清理。 對於資料夾名稱和資產名稱，用戶定義的標題保持不變，並儲存在 `jcr:title`。

在批量導入期間， [!DNL Experience Manager] 查找現有資料夾以避免重新導入資產和資料夾，並驗證在進行導入的父資料夾中應用的清理規則。 如果在父資料夾中應用了清除規則，則相同的規則將應用於導入源。 對於新導入，將應用以下簡化規則來管理資產和資料夾的檔案名。

**在批量導入中處理資產名稱**

對於資產檔案名，使用API清理Jcr名稱和路徑： `JcrUtil.escapeIllegalJcrChars`。

* 將Unicode保持原樣
* 將特殊字元替換為其URL轉義代碼，例如， `new*asset.png` 已更新為 `new%2Aasset.png`:

   ```
          URL escape code   
   
   "         %22
   %         %25
   '         %27
   *         %2A
   .         %2E
   /         %2F
   :         %3A
   [         %5B
   \n        %5Cn
   \r        %5Cr
   \t        %5Ct
   ]         %5D
   |         %7C
   ```

**在批量導入中處理資料夾名稱**

對於資料夾檔案名，使用API清理Jcr名稱和路徑： `JcrUtil.createValidName`。

* 將大小寫轉換為小寫
* 保持Unicode原樣
* 將特殊字元替換為短划線(&#39;-&#39;)，例如， `new*asset.png` 已更新為 `new-asset.png`:

   ```
   "                           
   #                         
   %                           
   &                          
   *                           
   +                          
   .                           
   :                           
   ;                          
   ?                          
   [                           
   ]                           
   ^                         
   {                         
   }                         
   |                           
   /      It is used for split folder in cloud storage and is pre-handled, no conversion here.
   \      Not allowed in Azure, allowed in AWS.
   \t                          
   ```

<!-- 
[!DNL Experience Manager Assets] manages the forbidden characters in the filenames while you upload assets or folders. [!DNL Experience Manager] updates only the node names in the DAM repository. However, the `title` of the asset or folder remains unchanged.

Following are the file naming conventions that are applied while uploading assets or folders in [!DNL Experience Manager Assets]:

| Characters &Dagger; | When occurring in file names | When occurring in folder names | Example |
|---|---|---|---|
| `. / : [ ] | *` | Replaced with `-` (hyphen). | Replaced with `-` (hyphen). A `.` (dot) in the filename extension is retained as is. | Replaced with `-` (hyphen). | `myimage.jpg` remains as is and `my.image.jpg` changes to `my-image.jpg`. |
| `% ; # , + ? ^ { } "` and whitespaces | Whitespaces are retained | Replaced with `-` (hyphen). | `My Folder.` changes to `my-folder-`. |
| `# % { } ? & .` | Replaced with `-` (hyphen). | NA. | `#My New File.` changes to `-My New File-`. |
| Uppercase characters | Casing is retained as is. | Changed to lowercase characters. | `My New Folder` changes to `my-new-folder`. |
| Lppercase characters | Casing is retained as is. | Casing is retained as is. | NA. |

&Dagger; The list of characters is a whitespace-separated list.
-->

#### 計劃一次性或循環批量導入 {#schedule-bulk-import}

要計劃一次性或循環批量導入，請執行以下步驟：

1. 建立批量導入配置。
1. 選擇配置並選擇 **[!UICONTROL 計畫]** 的子菜單。
1. 設定一次性攝取或計畫每小時、每天或每週的時間表。 按一下 **[!UICONTROL 提交]**。

   ![計畫批量導入作業](assets/bulk-ingest-schedule1.png)


#### 查看Assets目標資料夾 {#view-assets-target-folder}

選擇配置並按一下 **[!UICONTROL 查看資產]** 查看在執行批量導入作業後導入資產的資產目標位置。

#### 運行批量導入工具 {#run-bulk-import-tool}

之後 [配置批量導入工具](#configure-bulk-ingestor-tool) 可選 [管理批量導入工具配置](#manage-bulk-import-configuration)，您可以運行配置作業以開始大量接收資產。

導航到 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 批量導入]**，選擇 [批量導入配置](#configure-bulk-ingestor-tool) 按一下 **[!UICONTROL 運行]** 啟動批量導入進程。 按一下 **[!UICONTROL 運行]** 確認。

Experience Manager將作業的狀態更新為 **處理** 和 **成功** 工作成功完成後。 按一下 **查看資產** 以Experience Manager形式查看導入的資產。

當作業正在進行時，您也可以選擇配置，然後按一下 **停止** 來停止吞咽過程。 按一下 **運行** 的子菜單。 也可以按一下 **乾跑** 瞭解仍在等待進口的資產的細節。

#### 執行後管理作業 {#manage-jobs-after-execution}

Experience Manager使您能夠查看批量導入作業的歷史記錄。 作業歷史記錄包括作業的狀態、作業建立者、日誌以及其他詳細資訊，如開始日期和時間、建立日期和時間以及完成日期和時間。

要訪問配置的作業歷史記錄，請選擇配置，然後按一下 **[!UICONTROL 作業歷史記錄]**。 選擇作業並按一下 **開啟**。

![計畫批量導入作業](assets/job-history-bulk-import.png)

Experience Manager顯示作業歷史記錄。 在「批量導入作業歷史記錄」頁上，您還可以按一下 **刪除** 刪除批量導入配置的作業。


## 使用案頭客戶端上載資產 {#upload-assets-desktop-clients}

除Web瀏覽器用戶介面外， [!DNL Experience Manager] 支援案頭上的其他客戶端。 它們還提供上載體驗，而無需訪問Web瀏覽器。

* [[!DNL Adobe Asset Link]](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html) 提供對資產的訪問 [!DNL Experience Manager] 在Adobe Photoshop、Adobe Illustrator和Adobe InDesign台式機應用程式中。 您可以將當前開啟的文檔上載到 [!DNL Experience Manager] 直接從這些案頭應用程式中Adobe資產連結用戶介面。
* [[!DNL Experience Manager] 案頭應用](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) 簡化了在案頭上使用資產的操作，獨立於其檔案類型或處理這些資產的本機應用程式。 從本地檔案系統上載嵌套資料夾層次結構中的檔案尤其有用，因為瀏覽器上載僅支援上載平面檔案清單。

## 上載時處理資產 {#process-when-uploaded}

為了對上載的資產執行附加處理，您可以在上載資料夾上應用處理配置檔案。 配置式在 **[!UICONTROL 屬性]** 資料夾的頁面 [!DNL Assets]。 沒有擴展或擴展不正確的數字資產不會按需要處理。 例如，在上載此類資產時，不會發生任何情況，或者不正確的處理配置檔案可能會應用於資產。 用戶仍然可以將二進位檔案儲存在DAM中。

![資產資料夾的屬性，其中包含添加處理配置檔案的選項](assets/assets-folder-properties.png)

以下頁籤可用：

* [元資料配置檔案](metadata-profiles.md) 允許您將預設元資料屬性應用於上載到該資料夾中的資產。
* [處理配置檔案](asset-microservices-configure-and-use.md) 允許您生成的格式副本數量超過預設可能的數量。

此外，如果 [!DNL Dynamic Media] 已在部署中啟用，以下頁籤可用：

* [[!DNL Dynamic Media] 影像配置檔案](dynamic-media/image-profiles.md) 允許應用特定裁剪(**[!UICONTROL 智慧裁剪]** 和像素裁剪)，並將配置銳化到上載的資產。
* [[!DNL Dynamic Media] 視頻配置檔案](dynamic-media/video-profiles.md) 允許您應用特定的視頻編碼配置檔案（解析度、格式、參數）。

>[!NOTE]
>
>[!DNL Dynamic Media] 對資產執行裁剪和其他操作是無損的，即，這些操作不會更改上載的原始操作。 相反，它提供了在傳遞資產時裁剪或轉換的參數。

對於已分配了處理配置檔案的資料夾，配置檔案名稱將顯示在卡視圖中的縮略圖上。 在清單視圖中，配置檔案名稱將出現在 **[!UICONTROL 處理配置檔案]** 的雙曲餘切值。

## 使用API上載或接收資產 {#upload-using-apis}

中提供了上載API和協定的技術詳細資訊，以及指向開源SDK和示例客戶端的連結 [資產上載](developer-reference-material-apis.md#asset-upload) 的子菜單。

## 提示、最佳做法和限制 {#tips-limitations}

* 直接二進位上傳是一種新的資產上傳方法。 預設情況下，產品功能和客戶端支援它，例如 [!DNL Experience Manager] 用戶介面， [!DNL Adobe Asset Link], [!DNL Experience Manager] 案頭應用。 客戶技術團隊自定義或擴展的任何自定義代碼都必須使用新的上載API和協定。

* Adobe建議在中的每個資料夾中添加不超過1000個資產 [!DNL Experience Manager Assets]。 雖然可以向資料夾添加更多資產，但您可能會遇到效能問題，例如此類資料夾的導航速度較慢。

* 選擇時 **[!UICONTROL 替換]** 的 [!UICONTROL 名稱衝突] 對話框，將為新資產重新生成資產ID。 此ID與上一個資產的ID不同。 如果 [資產透視](/help/assets/assets-insights.md) 可跟蹤觀察或點擊 [!DNL Adobe Analytics]，重新生成的資產ID將使為上的資產捕獲的資料失效 [!DNL Analytics]。

* 某些上載方法不會阻止您使用 [禁止字元](#filename-handling) 的雙曲餘切值。 字元替換為 `-` 的雙曲餘切值。

* 使用瀏覽器上載資產僅支援平面檔案清單，而不支援嵌套資料夾層次。 要上載嵌套資料夾內的所有資產，請考慮使用 [案頭應用](#upload-assets-desktop-clients)。

* 批量導入方法導入整個資料夾結構，因為它存在於資料源中。 但是，僅在中建立非空資料夾 [!DNL Experience Manager]。


<!-- TBD: Link to file name handling in DA docs when it is documented. 
-->

>[!MORELIKETHIS]
>
>* [[!DNL Adobe Experience Manager] 桌面應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html)
>* [關於 [!DNL Adobe Asset Link]](https://www.adobe.com/tw/creativecloud/business/enterprise/adobe-asset-link.html)
>* [[!DNL Adobe Asset Link] 文件](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)
>* [資產上載的技術參考](developer-reference-material-apis.md#asset-upload)

