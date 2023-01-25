---
title: 關於Dynamic Media影像設定檔和影片設定檔
description: 影像設定檔或視訊設定檔是套用至上傳至資料夾之資產的選項方式。 例如，您可以指定要將哪些視訊編碼套用至您上傳的Dynamic Media視訊資產。 或者，要套用至Dynamic Media影像資產的影像設定檔，以便正確裁切。
feature: Asset Management,Image Profiles,Video Profiles
role: Admin,User
exl-id: 8c8f0a57-13f5-4903-8d76-bfb6ee83323c
source-git-commit: 419ec6604ee8c93510cb8bf4e1d46bc9b9c9383a
workflow-type: tm+mt
source-wordcount: '1376'
ht-degree: 0%

---

# 關於Dynamic Media影像設定檔和影片設定檔{#about-dm-image-video-profiles}

影像設定檔或影片設定檔是套用至上傳至資料夾之資產的選項方式。 例如，您可以指定要將哪些視訊編碼套用至您上傳的Dynamic Media視訊資產。 或者，要套用至Dynamic Media影像資產的影像設定檔，以便正確裁切。

在Dynamic Media中，您可以建立兩種設定檔類型，以下連結會詳細說明：

* [Dynamic Media影像設定檔](/help/assets/dynamic-media/image-profiles.md)
* [Dynamic Media影片設定檔](/help/assets/dynamic-media/video-profiles.md)

另請參閱 [中繼資料設定檔](/help/assets/metadata-profiles.md).

您必須擁有管理員權限，才能建立、編輯和刪除Dynamic Media影像設定檔或Dynamic Media影片設定檔。

建立影像設定檔或影片設定檔後，您會將其指派給一或多個資料夾，以用於新上傳的Dynamic Media資產。

另請參閱 [組織數位資產以使用處理設定檔的最佳實務](/help/assets/organize-assets.md).


>[!NOTE]
>
>您從一個資料夾移至另一個資料夾的資產不會重新處理。 例如，假設您的資料夾1已為其分配配置檔案A，而資料夾2已為其分配配置檔案B。 如果您將資產從「資料夾1」移至「資料夾2」，則移動的資產會保留其從「資料夾1」中的原始處理。
>
>即使您在指派了相同設定檔的兩個資料夾之間移動資產，也會是相同的情況。

## 在資料夾中重新處理Dynamic Media資產 {#reprocessing-assets}

您可以重新處理已有現有Dynamic Media影像設定檔或您之後已變更之Dynamic Media影片設定檔的資料夾中的資產。

例如，假設您建立了Dynamic Media影像設定檔，並將其指派給資料夾。 您上傳至資料夾的任何影像資產都會自動將影像設定檔套用至資產。 不過，之後您決定將新的智慧型裁切比例新增至「影像描述檔」。 現在，您只需執行「 」，而不需再次選取資產並重新上傳至資料夾 *Scene7:重新處理資產* 工作流程。

您可以對第一次處理失敗的資產執行重新處理工作流程。 即使您尚未編輯影像設定檔或視訊設定檔，或已套用影像設定檔或視訊設定檔，您仍可以隨時對資產資料夾執行重新處理工作流程。

您可以選擇調整重新處理工作流程的批大小，從預設的50個資產調整為最多1000個資產。 當您執行 _Scene7:重新處理資產_ 資料夾上的工作流程，會將資產分批分組，然後傳送至Dynamic Media伺服器進行處理。 處理後，整個批次集中每個資產的中繼資料會在 [!DNL Adobe Experience Manager]. 如果批次大小很大，您可能會遇到處理延遲的問題。 或者，如果批次大小太小，可能會導致往返Dynamic Media伺服器的次數過多。

請參閱 [調整重新處理工作流的批大小](#adjusting-load).

>[!NOTE]
>
>如果您要將資產從Dynamic Media Classic大量移轉至 [!DNL Experience Manager]，請在Dynamic Media伺服器上啟用「移轉復寫代理」 。 遷移完成後，請確保禁用代理。
>
>必須在Dynamic Media伺服器上停用移轉發佈代理，重新處理工作流程才能正常運作。

<!-- LEAVE IN PLACE, MAY BE USED IN THE FUTURE

Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media's Image Production System) job. When you run the Scene7: Reprocess Assets workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job and so on until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. 

-->

**若要重新處理資料夾中的Dynamic Media資產：**

1. 在 [!DNL Experience Manager]，從「資產」頁面導覽至指派了影像設定檔或視訊設定檔，且您要套用的資產資料夾 **Scene7:重新處理資產** 工作流程。

   為其分配了「影像配置檔案」或「視頻配置檔案」(Video Profile)的資料夾的名稱會顯示在「卡片視圖」中資料夾名稱的正下方。

1. 選取資料夾。

   * 工作流程會遞回考慮所選資料夾中的所有檔案。
   * 如果主要選取的資料夾中有一或多個子資料夾含有資產，工作流程會重新處理資料夾階層中的每個資產。
   * 最佳實務是，請避免在資料夾階層（擁有超過1000個資產）上執行此工作流程。

1. 在頁面左上角附近，從下拉式清單中選取 **[!UICONTROL 時間表]**.
1. 在頁面左下角附近，位於 [!UICONTROL 註解] 欄位，選取「加號」圖示( **^** )。

   ![Experience Manager中的「資產」螢幕擷圖，顯示選取的資產資料夾、強調顯示的「時間軸」下拉式清單、強調顯示的「開始工作流程」按鈕，以及「註解」欄位右側的「克拉」圖示，也強調顯示。](/help/assets/dynamic-media/assets/reprocess-assets1.png)

1. 選擇 **[!UICONTROL 開始工作流程]**.
1. 從 **[!UICONTROL 開始工作流程]** 下拉清單，選擇 **[!UICONTROL Scene7:重新處理資產]**.
1. （選用）在 **輸入工作流的標題** 文本欄位，輸入工作流的名稱。 如有必要，您可以使用名稱來參考工作流程例項。

   ![時間軸使用者介面的螢幕擷取畫面顯示「Scene7:從「開始工作流程」下拉式清單中選取的「重新處理資產」，並反白顯示「開始」按鈕。](/help/assets/dynamic-media/assets/reprocess-assets2.png)

1. 選擇 **[!UICONTROL 開始]**，然後選取 **[!UICONTROL 確認]**.

   若要監控工作流程或檢查其進度，請從 [!DNL Experience Manager] 主控台頁面，選擇 **[!UICONTROL 「工具>工作流程」]**. 在「工作流實例」頁上，選擇工作流。 在菜單欄上，選擇 **[!UICONTROL 開啟歷史記錄]**. 您也可以從同一「工作流實例」頁終止、掛起或更名選定的工作流。

### 調整重新處理工作流的批大小（可選） {#adjusting-load}

（選用）重新處理工作流程的預設批次大小為每個工作50個資產。 此最佳批次大小由執行重新處理的資產的平均資產大小和MIME類型所控制。 值越高，表示在單個重新處理作業中會有許多檔案。 因此，處理橫幅會持續 [!DNL Experience Manager] 資產。 但是，如果平均檔案大小為1 MB或以下，則建議將值增加到幾個100，但Adobe不超過1000。 如果檔案的平均大小為數百MB,Adobe建議您將批處理大小降低至10。

**（可選）要調整重新處理工作流的批大小：**

1. 在 [!DNL Experience Manager]，選取 **[!UICONTROL Adobe Experience Manager]** 若要存取全域導覽主控台，請選取 **[!UICONTROL 工具]** （槌子）表徵圖> **[!UICONTROL 工作流程>模型]**.
1. 在「工作流模型」頁的「卡片視圖」或「清單視圖」中，選擇 **[!UICONTROL Scene7:重新處理資產]**.

   ![帶有「Scene7:在Experience Manager的「卡片」檢視中選取的「重新處理資產」工作流程。](/help/assets/dynamic-media/assets/reprocess-assets7.png)

1. 在工具列中，選取 **[!UICONTROL 編輯]**. 新的瀏覽器標籤會開啟Scene7:「重新處理資產」工作流模型頁面。
1. 在Scene7:重新處理資產工作流程頁面，在右上角附近，選取 **[!UICONTROL 編輯]** 「解除鎖定」工作流程。
1. 在工作流程中，選取「Scene7批次上傳」元件以開啟工具列，然後選取 **[!UICONTROL 設定]** 的下一頁。

   ![「Scene7:重新處理資產」頁面，將滑鼠指標暫留在「設定」圖示上。](/help/assets/dynamic-media/assets/reprocess-assets8.png)

1. 在 **[!UICONTROL 批次上傳至Scene7 — 步驟屬性]** 對話框，請設定以下內容：
   * 在 **[!UICONTROL 標題]** 和 **[!UICONTROL 說明]** 文本欄位，輸入新的職務和說明（如果需要）。
   * 選擇 **[!UICONTROL 處理常式進階]** 如果您的處理常式會前進至下一個步驟。
   * 在 **[!UICONTROL 逾時]** 欄位，輸入外部進程超時（秒）。
   * 在 **[!UICONTROL 時段]** 欄位，輸入輪詢間隔（秒）以測試外部進程的完成。
   * 在 **[!UICONTROL 批次欄位]**，輸入Dynamic Media伺服器批次處理上傳工作中要處理的資產數量上限(50-1000)。
   * 選擇 **[!UICONTROL 逾時前進]** 如果您想在逾時時間前進。 如果要在達到逾時時繼續進入收件匣，請取消選取。

   ![「批次上傳至Scene7 — 步驟屬性」頁面的螢幕擷圖。](/help/assets/dynamic-media/assets/reprocess-assets3.png)

1. 位於 **[!UICONTROL 批次上傳至Scene7 — 步驟屬性]** 對話框，選擇 **[!UICONTROL 完成]**.

1. 在Scene7的右上角：「重新處理資產」工作流模型頁，請選擇 **[!UICONTROL 同步]**. 當您看到 **[!UICONTROL 已同步]**，工作流程執行階段模型已成功同步，且已準備好重新處理資料夾中的資產。

   ![Experience Manager中的「資產」螢幕擷圖，顯示選取的資產資料夾、強調顯示的「時間軸」下拉式清單、強調顯示的「開始工作流程」按鈕，以及「註解」欄位右側的「克拉」圖示，也強調顯示。](/help/assets/dynamic-media/assets/reprocess-assets1.png)

1. 關閉顯示Scene7的瀏覽器標籤：重新處理資產工作流程模型。

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
1. Repeat steps 1-7 to re-synchronize the new batch size to the Scene7: Reprocess Assets workflow model.

-->
