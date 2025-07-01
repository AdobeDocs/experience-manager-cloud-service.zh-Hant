---
title: 將資產上傳到存放庫
description: 上傳資產到  [!DNL Assets view]、檢視上傳狀態和解決上傳問題。
role: User
exl-id: 01af3b66-dba8-4b09-aadf-ba4ae09b824f
feature: Asset Management, Publishing, Collaboration, Asset Processing
source-git-commit: 31c9e742d8bdf69c12788794670817864c9c027a
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 89%

---

# 上傳資產 {#add-assets}

若要新增要使用的新資產，請從您的本機檔案系統上傳一些資產。<!-- TBD: Many of the [common file formats are supported](/help/assets/supported-file-formats-assets-view.md). -->

您可以使用以下方法上傳一個或更多資產，或包含資產的一個資料夾：

* 在使用者介面上拖曳資產或資料夾，然後依照螢幕上的指示進行。
* 按一下工具列中的「新增Assets ]**」選項，並將部分檔案新增至上傳對話方塊。**[!UICONTROL 

<!-- TBD: Update this GIF
![Asset and nested folder upload demo](assets/do-not-localize/upload-assets.gif) -->

您可以在建立資料夾後使用任一方法上傳資產。若要建立空的資料夾，請從工具列按一下「**[!UICONTROL 建立資料夾]**」。雖然 [!DNL Assets view] 提供強大的全文檢索搜尋功能，但您也可以使用資料夾更妥善組織您的資產。

選取檔案後，即會出現確認對話方塊，以便新增更多檔案或移除已選取的檔案。若要新增更多檔案到選取項目，請按一下「**[!UICONTROL 瀏覽]**」，然後選取「**[!UICONTROL 瀏覽檔案]**」或「**[!UICONTROL 瀏覽資料夾]**」。從相同或不同的資料夾新增更多檔案或資料夾。

將所有檔案排入佇列後，請按一下「**[!UICONTROL 上傳]**」。

![上傳檔案和資料夾](assets/upload-browse-files-folders.png)

*圖：上傳選取的資產前，您可以從佇列新增或移除資產。*

>[!TIP]
>
>如果您將資料夾結構上傳至Assets檢視，則不需要建立具有該資料夾結構的.ZIP檔案，您可以直接上傳資料夾結構。 上傳至Assets檢視的.ZIP檔案會儲存為一個ZIP資產，上傳後也不會自動解壓縮。

## 檢視上傳進度和狀態 {#upload-progress}

上傳許多資產或巢狀資料夾到 [!DNL Assets view] 時，部分資產會因各種原因 (如重複的資產和網路問題) 而無法上傳。

若要追蹤上傳進度，請按一下工具列上的「**[!UICONTROL 上傳進度]**」選項。面板會顯示所有資產的上傳進度。

若要根據上傳進度或狀態檢視資產的子集合，請在「**[!UICONTROL 上傳進度]**」側邊欄中使用篩選器。各種篩選條件用於顯示所有資產、完整的上傳、進行中的上傳、排入要上傳佇列的資產、暫停的上傳、重複資產，以及無法上傳的資產。

![根據上傳狀態篩選上傳進度](assets/filter-upload-progress.png)

*圖：根據上傳狀態或上傳進度篩選您嘗試上傳的資產。*

上傳資產後，[!DNL Assets view] 便會立即處理資產，以產生縮圖並處理中繼資料。許多資產都需要一些處理時間。如果您未看到縮圖並在預留位置縮圖上看到處理訊息，請在數分鐘後再次查看資料夾。處理時，除其他外，[!DNL Assets view] 會產生轉譯、新增智慧型標記，並編製資產詳細資訊的索引，以便進行搜尋。

![資產是在上傳後的程序，且標題會顯示處理](assets/upload-processing.png)

*圖：上傳的資產會在處理資產的標題上顯示處理。*

## 資產轉譯 {#renditions}

[!DNL Assets view] 會近乎即時處理上傳的資產，並對許多支援的檔案類型產生轉譯。為影像建立的轉譯是上傳影像調整大小的版本。您不僅可以下載資產，也可以下載轉譯，以使用合適的版本。[預覽資產](/help/assets/navigate-assets-view.md#preview-assets)時，您可以檢視資產的所有轉譯。

![轉譯](assets/renditions-view-download.png)

*圖：檢視和下載轉譯。*

## 管理失敗的上傳 {#resolve-upload-fails}

如果支援的資產因某項原因而無法上傳，請從「[!UICONTROL 上傳進度]」窗格按一下「**[!UICONTROL 重試]**」。

![重試失敗的上傳](assets/upload-retry.png)

*圖：如果支援的檔案因某項原因而無法上傳，請重試。*

如果您嘗試上傳重複的資產，則不會上傳該資產，直到您明確確認上傳為止。重複的資產最初會標示為失敗的上傳。若要解決問題，您可以僅建立一個版本、刪除和取代現有資產，或重新命名資產以建立重複的複本。您可以一次一個資產解決此類失敗作業，或一次對所有失敗的重複項目大量解決。

![一次一個管理重複的資產](assets/uploads-manage-duplicates.png)

*圖：對於預設無法上傳的重複資產，一次一個資產解決問題。*

![管理所有失敗的大量上傳](assets/upload-progress-manage-failed-uploads.png)

*圖：對於預設無法上傳的重複資產，一次解決所有資產的問題。*

>[!TIP]
>
>您可以在[!DNL Creative Cloud]案頭應用程式內直接將資產上傳到DAM存放庫。
<!--TBD
See how [[!DNL Assets view] integrates with [!DNL Adobe Asset Link]](/help/assets/integration-assets-view.md).
-->

## 刪除資產或資料夾 {#delete-assets}

使用者可以刪除不再需要的個別資產或資料夾。若要刪除資產或資料夾，請執行下列其中一個動作：

* 使用資產或資料夾縮圖上可用的選項。

  ![資產縮圖上用於管理資產的選項](assets/options-on-thumbnail.png)

  *圖：在資產或資料夾圖磚上可用的檔案和資料夾動作。*

* 選取資產或資料夾，然後按一下工具列中的「**[!UICONTROL 刪除]**」![刪除圖示](assets/do-not-localize/delete-icon.png)。

## 後續步驟 {#next-steps}

* [觀看在Assets檢視中上傳資產的相關影片](https://experienceleague.adobe.com/docs/experience-manager-learn/assets-essentials/basics/creating.html)

* 使用資產檢視使用者介面所提供的[!UICONTROL 意見回饋]選項提供產品意見回饋

* 若要提供文件意見回饋，請使用右側邊欄提供的[!UICONTROL 編輯此頁面]![來編輯頁面](assets/do-not-localize/edit-page.png)或[!UICONTROL 記錄問題]![來建立 GitHub 問題](assets/do-not-localize/github-issue.png)

* 聯絡[客戶服務](https://experienceleague.adobe.com/?support-solution=General#support)
