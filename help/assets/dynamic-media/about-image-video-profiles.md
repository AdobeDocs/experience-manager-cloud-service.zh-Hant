---
title: 關於動態媒體影像描述檔和視訊描述檔
description: 「影像描述檔」或「視訊描述檔」是套用至您上傳至資料夾之資產的選項的方式。 例如，您可以指定要套用至您上傳之動態媒體視訊資產的視訊編碼。 或者，要套用至動態媒體影像資產的影像描述檔，以便正確裁切。
translation-type: tm+mt
source-git-commit: dfaaafce8e9a7f0d90e4c3d6967c8236d48e6e40
workflow-type: tm+mt
source-wordcount: '1278'
ht-degree: 2%

---


# 關於動態媒體影像描述檔和視訊描述檔{#about-dm-image-video-profiles}

「影像描述檔」或「視訊描述檔」是套用至您上傳至資料夾之資產的選項的方式。 例如，您可以指定要套用至您上傳之動態媒體視訊資產的視訊編碼。 或者，要套用至動態媒體影像資產的影像描述檔，以便正確裁切。

在動態媒體中，您可以建立兩種描述檔類型，這些描述檔在下列連結中有詳細說明：

* [動態媒體影像設定檔](/help/assets/dynamic-media/image-profiles.md)
* [動態媒體視訊設定檔](/help/assets/dynamic-media/video-profiles.md)

另請參閱[元資料配置檔案](/help/assets/metadata-profiles.md)。

您必須擁有管理員權限，才能建立、編輯和刪除動態媒體影像描述檔或動態媒體視訊描述檔。

建立影像描述檔或視訊描述檔後，您會將其指派給一或多個檔案夾，以用於新上傳的動態媒體資產。

另請參閱[組織數位資產使用影像描述檔或視訊描述檔的最佳做法](/help/assets/dynamic-media/best-practices-for-file-management.md)。

>[!NOTE]
>
>您從一個資料夾移至另一個資料夾的資產不會重新處理。 例如，假設您的資料夾1已為其分配了配置檔案A，資料夾2已為其分配了配置檔案B。 如果您將資產從資料夾1移至資料夾2，則移動的資產會保留其從資料夾1的原始處理。
>
>即使在兩個資料夾之間移動資產時，也會有相同的設定檔指派給它。

## 正在重新處理資料夾{#reprocessing-assets}中的動態媒體資產

您可以重新處理已有現有動態媒體影像描述檔或稍後變更之動態媒體視訊描述檔的資料夾中的資產。

例如，假設您建立了動態媒體影像描述檔，並將其指派給資料夾。 上傳至資料夾的任何影像資產都會自動將影像描述檔套用至資產。 不過，稍後您決定將新的智慧型裁切比例新增至影像描述檔。 現在，您只需執行&#x200B;*Scene7:重新處理資產*&#x200B;工作流程。

您可以對第一次處理失敗的資產執行重新處理工作流程。 即使您尚未編輯影像描述檔或視訊描述檔，或已套用影像描述檔或視訊描述檔，您仍可隨時對資產資料夾執行重新處理工作流程。

您可以選擇調整重新處理工作流的批大小，從預設的50個資產調整到1000個資產。 當您執行&#x200B;_Scene7時：在資料夾上重新處理資產_&#x200B;工作流程，資產會分批分組，然後傳送至Dynamic Media伺服器進行處理。 在處理後，整個批次集中每個資產的中繼資料會在AEM上更新。 如果批次大小較大，您會遇到處理延遲。 或者，如果批次大小過小，可能會導致往返Dynamic Media伺服器的次數過多。

請參閱[調整重新處理工作流的批大小](#adjusting-load)。

>[!NOTE]
>
>如果您正在從Dynamic Media Classic將資產大量遷移到Experience Manager，請在Dynamic Media伺服器上啟用遷移複製代理。 移轉完成後，請務必停用代理。
>
>移轉發佈代理必須在Dynamic Media伺服器上停用，讓重新處理工作流程如預期般運作。

<!-- LEAVE IN PLACE, MAY BE USED IN THE FUTURE

Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media’s Image Production System) job. When you run the Scene7: Reprocess Assets workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job and so on until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. 

-->

**要重新處理資料夾中的動態媒體資產**:
1. 在Adobe Experience Manager的「資產」頁面中，導覽至動態媒體資產的檔案夾，其中已指派影像描述檔或視訊描述檔，且您要套用&#x200B;**Scene7:重新處理資產**&#x200B;工作流程，

   指派影像描述檔或視訊描述檔的檔案夾，其名稱會直接顯示在「卡片檢視」中的檔案夾名稱下方。

1. 選擇資料夾。

   * 工作流會遞歸地考慮選定資料夾中的所有檔案。
   * 如果主要選取的檔案夾中有一個或多個子檔案夾包含資產，工作流程會重新處理檔案夾階層中的每個資產。
   * 最佳實務是，請避免在擁有超過1000個資產的檔案夾階層上執行此工作流程。

1. 在頁面左上角附近，從下拉式清單中按一下「時間 **[!UICONTROL 軸」]**。
1. 在頁面左下角的[!UICONTROL Comment]欄位右側，點選Carat圖示(**^**)。

   ![重新處理資產工作流程1](/help/assets/dynamic-media/assets/reprocess-assets1.png)

1. 按一下&#x200B;**[!UICONTROL 啟動工作流]**。
1. 從&#x200B;**[!UICONTROL 開始工作流程]**&#x200B;下拉式清單中，選擇&#x200B;**[!UICONTROL Scene7:重新處理資產]**。
1. （可選）在&#x200B;**輸入工作流的標題**&#x200B;文本欄位中，輸入工作流的名稱。 如有必要，可以使用名稱來引用工作流實例。

   ![重新處理資產2](/help/assets/dynamic-media/assets/reprocess-assets2.png)

1. 按一下&#x200B;**[!UICONTROL 開始]** ，然後按一下&#x200B;**[!UICONTROL 確認]**。

   若要監控工作流程或檢查其進度，請從Experience Manager主控台頁面，按一下「工具>工作流程」]**。**[!UICONTROL &#x200B;在「工作流實例」頁上，選擇工作流。 在菜單欄上，按一下&#x200B;**[!UICONTROL 開啟歷史記錄]**。 您也可以終止、暫停或重新命名同一「工作流實例」頁中選定的工作流。

### 調整重新處理工作流的批大小{#adjusting-load}

（可選）重新處理工作流程中的預設批次大小是每個工作50個資產。 此最佳批次大小由執行重新處理之資產的平均資產大小和MIME類型所控制。 值越高，表示您在單一重新處理工作中擁有許多檔案。 因此，處理橫幅會在Experience Manager資產上停留較久。 但是，如果平均檔案大小為1 MB或以下- Adobe建議您將值增加到幾百，但不要超過1000。 如果平均檔案大小是數百兆位元組，Adobe建議您將批次大小降低至10。

**（可選）要調整重新處理工作流的批大小**:

1. 在Experience Manager中，點選 **[!UICONTROL Adobe Experience Manager]** ，存取全域導覽主控台，然後點選「工具 **[!UICONTROL (槌子) 」圖示>「工]** 作流程>模型」 ****。
1. 在「工作流程模型」頁面的「卡片檢視」或「清單檢視」中，選取&#x200B;**[!UICONTROL Scene7:重新處理資產]**。

   ![「工作流程模型」頁面與Scene7:重新處理卡片檢視中選取的資產工作流程](/help/assets/dynamic-media/assets/reprocess-assets7.png)

1. 在工具列中，按一下「編輯」。 ****&#x200B;新的瀏覽器標籤會開啟Scene7:「重新處理資產」工作流模型頁。
1. 在Scene7:重新處理「資產」工作流程頁面，靠近右上角，點選「**[!UICONTROL 編輯]**」以「解除鎖定」工作流程。
1. 在工作流程中，選取Scene7批次上傳元件以開啟工具列，然後點選工具列中的「設定」。****

   ![Scene7批次上傳元件](/help/assets/dynamic-media/assets/reprocess-assets8.png)

1. 在&#x200B;**[!UICONTROL 批次上傳至Scene7 —— 步驟屬性]**&#x200B;對話方塊中，設定下列項目：
   * 在&#x200B;**[!UICONTROL Title]**&#x200B;和&#x200B;**[!UICONTROL Description]**&#x200B;文字欄位中，視需要輸入新的職務和說明。
   * 如果您的處理常式會進入下一個步驟，請選取「**[!UICONTROL 處理常式進階]**」。
   * 在&#x200B;**[!UICONTROL Timeout]**&#x200B;欄位中，輸入外部進程超時（秒）。
   * 在&#x200B;**[!UICONTROL Period]**&#x200B;欄位中，輸入輪詢間隔（秒）以測試外部進程的完成。
   * 在&#x200B;**[!UICONTROL 批次欄位]**&#x200B;中，輸入Dynamic Media伺服器批次處理上傳作業中要處理的資產數目上限(50-1000)。
   * 如果要在到達超時時提前，請選擇&#x200B;**[!UICONTROL 超時時提前]**。 如果要在到達逾時時時繼續進入收件箱，請取消選擇。

   ![屬性對話框](/help/assets/dynamic-media/assets/reprocess-assets3.png)

1. 在&#x200B;**[!UICONTROL 批次上傳至Scene7 —— 步驟屬性]**&#x200B;對話方塊的右上角，點選&#x200B;**[!UICONTROL 完成]**。

1. 在Scene7的右上角：重新處理「資產」工作流模型頁，點選&#x200B;**[!UICONTROL Sync]**。 當您看到&#x200B;**[!UICONTROL Synced]**&#x200B;時，工作流程執行階段模型已成功同步，並可重新處理資料夾中的資產。

   ![同步化工作流程模型](/help/assets/dynamic-media/assets/reprocess-assets1.png)

1. 關閉顯示Scene7的瀏覽器標籤：重新處理資產工作流程模型。

<!-- MAY BE NEEDED IN THE FUTURE

1. Return to the browser tab that has the open Workflow Models page, then press **Esc** to exit the selection.
1. In the upper-left corner of the page, tap **[!UICONTROL Adobe Experience Manager]** to access the global navigation console, then tap the **[!UICONTROL Tools]** (hammer) icon > **[!UICONTROL General > CRXDE Lite]**.
1. In the folder tree on the left side of the CRXDE Lite page, navigate to the following location:

   `/conf/global/settings/workflow/models/scene7_reprocess_assets/jcr:content/flow/reprocess/metaData`

   ![CRXDE Lite](/help/security/assets/workflow-models9.png)

1. On the right side of the CRXDE Lite page, in the lower portion, enter the following name, type, and value in its respective field:
    * **[!UICONTROL Name]**: `reprocess-batch-size`
    * **[!UICONTROL Type]**: `Long`
    * **[!UICONTROL Value]**: enter a default value (50-1000) for the batch size
1. In the lower-right corner, tap **[!UICONTROL Add]**. The new property appears as the following:

    ![Saving the new property](/help/security/assets/workflow-models10.png)

1. On the menu bar of the CRXDE Lite page, tap **[!UICONTROL Save All]**.
1. In the upper-left corner of the page, tap **[!UICONTROL CRXDE Lite]** to return to the main Experience Manager console
1. Repeat steps 1-7 to re-synchronize the new batch size to the Scene7: Reprocess Assets workflow model.

-->
