---
title: 關於Dynamic Media影像設定檔和視訊設定檔
description: 影像設定檔或視訊設定檔是將哪些選項套用至您上傳至資料夾之資產的配方。 例如，您可以指定要套用至上傳之Dynamic Media視訊資產的視訊編碼。 或是套用至Dynamic Media影像資產的影像設定檔，以正確加以裁切。
contentOwner: Rick Brough
feature: Asset Management,Image Profiles,Video Profiles
role: Admin,User
exl-id: 8c8f0a57-13f5-4903-8d76-bfb6ee83323c
source-git-commit: f9f82c144e6f919ed9b82caf9e1bc0408a352fd6
workflow-type: tm+mt
source-wordcount: '1391'
ht-degree: 0%

---

# 關於Dynamic Media影像設定檔和視訊設定檔{#about-dm-image-video-profiles}

影像設定檔或視訊設定檔是套用至上傳至資料夾之資產的選項。 例如，您可以指定要套用至上傳之Dynamic Media視訊資產的視訊編碼。 或是套用至Dynamic Media影像資產的影像設定檔，以正確加以裁切。

在Dynamic Media中，您可以建立兩種型別的設定檔，以下連結將詳細介紹這些設定檔：

* [Dynamic Media影像設定檔](/help/assets/dynamic-media/image-profiles.md)
* [Dynamic Media影片設定檔](/help/assets/dynamic-media/video-profiles.md)

另請參閱 [中繼資料設定檔](/help/assets/metadata-profiles.md).

您必須擁有管理員許可權，才能建立、編輯和刪除Dynamic Media影像設定檔或Dynamic Media視訊設定檔。

建立影像設定檔或視訊設定檔後，請將其指派至一或多個用於新上傳Dynamic Media資產的資料夾。

另請參閱 [組織數位資產以使用處理設定檔的最佳實務](/help/assets/organize-assets.md).


>[!NOTE]
>
>您將資產從一個資料夾移至另一個資料夾時，系統不會重新處理該資產。 例如，假設您有已指派設定檔A的資料夾1和已指派設定檔B的資料夾2。 如果您將資產從「資料夾1」移至「資料夾2」，則已移動的資產會保留「資料夾1」的原始處理作業。
>
>即使在您將資產移動到具有相同設定檔的兩個資料夾之間時，也是如此。

## 重新處理資料夾中的Dynamic Media資產 {#reprocessing-assets}

若資料夾中已存在您後來變更過的Dynamic Media影像設定檔或Dynamic Media視訊設定檔，您可以重新處理該資料夾中的資產。

例如，假設您建立了Dynamic Media影像設定檔並將其指派至資料夾。 您上傳至資料夾的任何影像資產都會自動將影像設定檔套用至資產。 不過，您稍後會決定在「影像描述檔」中加入新的智慧型裁切比例。 現在，您只需執行「 」即可將資產重新上傳至資料夾，而不需再次選取並重新上傳 *Dynamic Media重新處理* 工作流程。

您可以對首次處理失敗的資產執行重新處理工作流程。 即使您尚未編輯「影像設定檔」或「視訊設定檔」，或您已套用「影像設定檔」或「視訊設定檔」，您仍可隨時對資產的資料夾執行重新處理工作流程。

您可以選擇調整重新處理工作流程的批次大小，從預設的50個資產調整為1000個資產。 當您執行 _Scene7：重新處理資產_ 工作流程在資料夾中，資產會依批次分組，然後傳送至Dynamic Media伺服器以供處理。 處理之後，整個批次集中每個資產的中繼資料會更新於 [!DNL Adobe Experience Manager]. 如果批次大小很大，您可能會遇到處理延遲。 或者，如果批次大小太小，可能會導致Dynamic Media伺服器的往返次數過多。

另請參閱 [調整重新處理工作流程的批次大小](#adjusting-load).

>[!NOTE]
>
>如果您正在將資產從Dynamic Media Classic大量移轉至 [!DNL Experience Manager]，在Dynamic Media伺服器上啟用移轉復寫代理程式。 移轉完成後，請務必停用代理程式。
>
>必須在Dynamic Media伺服器上停用移轉發佈代理程式，才能讓重新處理工作流程如預期般運作。

<!-- LEAVE IN PLACE, MAY BE USED IN THE FUTURE

Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media's Image Production System) job. When you run the Dynamic Media Reprocess workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job and so on until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. 

-->

**若要重新處理資料夾中的Dynamic Media資產：**

1. 在 [!DNL Experience Manager]，從「資產」頁面，導覽至已指派影像設定檔或視訊設定檔且您想要套用之資產資料夾。 **Dynamic Media重新處理** 工作流程。

   已指派影像設定檔或視訊設定檔的資料夾，其設定檔名稱會直接顯示在「卡片檢視」的資料夾名稱下方。

1. 選取資料夾。

   * 工作流程會遞回考慮所選資料夾中的所有檔案。
   * 如果主要選取檔案夾中有一個或多個子檔案夾具有資產，工作流程會重新處理檔案夾階層中的每個資產。
   * 最佳實務是避免在擁有超過1000個資產的資料夾階層上執行此工作流程。

1. 在頁面左上角附近，從下拉式清單中選取 **[!UICONTROL 時間表]**.
1. 在頁面的左下角附近， [!UICONTROL 註解] 欄位，選取克拉圖示( **^** ) 。

   ![「Experience Manager中的資產」熒幕擷圖顯示選取的資產資料夾、「時間軸」下拉式清單熒游標示、「開始工作流程」按鈕熒游標示，以及「評論」欄位右側的克拉圖示也熒游標示](/help/assets/dynamic-media/assets/reprocess-assets1.png).

1. 選取 **[!UICONTROL 開始工作流程]**.
1. 從 **[!UICONTROL 開始工作流程]** 下拉式清單，選擇 **[!UICONTROL Dynamic Media重新處理]**.
1. （選用）在 **輸入工作流程的標題** 文字欄位，輸入工作流程的名稱。 如有必要，您可以使用名稱來參照工作流程例項。

   ![從「開始工作流程」下拉式清單中選取「Dynamic Media重新處理」且醒目提示「開始」按鈕的「時間軸」使用者介面熒幕擷圖](/help/assets/dynamic-media/assets/reprocess-assets2.png).

1. 選取 **[!UICONTROL 開始]**，然後選取 **[!UICONTROL 確認]**.

   若要監視工作流程或檢查其進度，請從 [!DNL Experience Manager] 主控台首頁面，選取 **[!UICONTROL 「工具」>「工作流程」]**. 在「工作流程例項」頁面上，選取工作流程。 在功能表列上，選取 **[!UICONTROL 開啟歷史記錄]**. 您也可以從同一個「工作流程例項」頁面終止、暫停或重新命名選取的工作流程。

### 調整重新處理工作流程的批次大小（選擇性） {#adjusting-load}

（選用）重新處理工作流程中的預設批次大小是每個工作50個資產。 此最佳批次大小是由平均資產大小和執行重新處理的資產MIME型別所控制。 較高的值表示您在一個重新處理工作中擁有許多檔案。 因此，處理橫幅會維持開啟 [!DNL Experience Manager] 資產保留較長時間。 但是，如果平均檔案大小是小於1 MB或小於Adobe，建議您將值增加到幾個100，但絕不要超過1000。 如果平均檔案大小為數百MB，Adobe建議您減少批次大小，最多為10。

**若要選擇性地調整重新處理工作流程的批次大小，請執行下列步驟：**

1. 在 [!DNL Experience Manager]，選取 **[!UICONTROL Adobe Experience Manager]** 若要存取全域導覽主控台，請選取 **[!UICONTROL 工具]** （槌子）圖示> **[!UICONTROL 工作流程>模型]**.
1. 在「工作流程模型」頁面的「卡片檢視」或「清單檢視」中，選取 **[!UICONTROL Dynamic Media重新處理]**.

   ![在Experience Manager的卡片檢視中選取「Dynamic Media重新處理」工作流程的「工作流程模型」頁面熒幕擷圖](/help/assets/dynamic-media/assets/reprocess-assets7.png).

1. 在工具列中，選取 **[!UICONTROL 編輯]**. 新的瀏覽器標籤會開啟「Dynamic Media重新處理工作流程」模型頁面。
1. 在「Dynamic Media重新處理工作流程」頁面的右上角附近，選取「 」 **[!UICONTROL 編輯]** 以「解鎖」工作流程。
1. 在工作流程中，選取Scene7批次上傳元件以開啟工具列，然後選取「 」 **[!UICONTROL 設定]** （在工具列中）。

   ![「Scene7重新處理」頁面上的「Dynamic Media批次上傳」元件熒幕擷圖，將滑鼠指標暫留在「設定」圖示上](/help/assets/dynamic-media/assets/reprocess-assets8.png).

1. 在 **[!UICONTROL 批次上傳至Scene7 — 步驟屬性]** 對話方塊中，設定下列專案：
   * 在 **[!UICONTROL 標題]** 和 **[!UICONTROL 說明]** 文字欄位，視需要輸入新的職稱和說明。
   * 選取 **[!UICONTROL 處理常式前進]** 如果您的處理常式將進行到下一個步驟。
   * 在 **[!UICONTROL 逾時]** 欄位，輸入外部程式逾時（秒）。
   * 在 **[!UICONTROL 期間]** 欄位，輸入輪詢間隔（秒）以測試外部程式的完成。
   * 在 **[!UICONTROL 批次欄位]**，輸入Dynamic Media伺服器批次處理上傳工作中要處理的資產數目上限(50-1000)。
   * 選取 **[!UICONTROL 逾時前進]** 如果您想要在達到逾時值時推進。 如果達到逾時時間時想要轉至收件匣，請取消選取。

   ![「批次上傳至Scene7 — 步驟屬性」頁面的熒幕擷圖](/help/assets/dynamic-media/assets/reprocess-assets3.png).

1. 在右上角 **[!UICONTROL 批次上傳至Scene7 — 步驟屬性]** 對話方塊，選取 **[!UICONTROL 完成]**.

1. 在「Dynamic Media重新處理工作流程模型」頁面的右上角，選取「 」 **[!UICONTROL 同步]**. 當您看到 **[!UICONTROL 已同步]**，工作流程執行階段模型已成功同步化，並準備好重新處理資料夾中的資產。

   ![「Experience Manager中的資產」熒幕擷圖顯示選取的資產資料夾、「時間軸」下拉式清單熒游標示、「開始工作流程」按鈕熒游標示，以及「評論」欄位右側的克拉圖示也熒游標示](/help/assets/dynamic-media/assets/reprocess-assets1.png).

1. 關閉顯示Dynamic Media重新處理工作流程模型的瀏覽器標籤。

<!-- MAY BE NEEDED IN THE FUTURE

1. Return to the browser tab that has the open Workflow Models page, then press **Esc** to exit the selection.
1. In the upper-left corner of the page, select **[!UICONTROL Adobe Experience Manager]** to access the global navigation console, then select the **[!UICONTROL Tools]** (hammer) icon > **[!UICONTROL General > CRXDE Lite]**.
1. In the folder tree on the left side of the CRXDE Lite page, navigate to the following location:

   `/conf/global/settings/workflow/models/scene7_reprocess_assets/jcr:content/flow/reprocess/metaData`

   ![CRXDE Lite](/help/security/assets/workflow-models9.png)

1. On the right side of the CRXDE Lite page, in the lower portion, enter the following name, type, and value in its respective field:
    * **[!UICONTROL Name]**: `reprocess-batch-size`
    * **[!UICONTROL Type]**: `Long`
    * **[!UICONTROL Value]**: enter a default value (50-1000) for the batch size
1. In the lower-right corner, select **[!UICONTROL Add]**. The new property appears as the following:

    ![Saving the new property](/help/security/assets/workflow-models10.png)

1. On the menu bar of the CRXDE Lite page, select **[!UICONTROL Save All]**.
1. In the upper-left corner of the page, select **[!UICONTROL CRXDE Lite]** to return to the main Experience Manager console
1. Repeat steps 1-7 to re-synchronize the new batch size to the Dynamic Media Reprocess workflow model.

-->
