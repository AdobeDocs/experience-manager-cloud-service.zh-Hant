---
title: 將內容內嵌至目標
description: 將內容內嵌至目標
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
source-git-commit: 20e54ff697c0dc7ab9faa504d9f9e0e6ee585464
workflow-type: tm+mt
source-wordcount: '1181'
ht-degree: 11%

---

# 將內容內嵌至目標 {#ingesting-content}

## 內容轉移工具中的擷取程式 {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="內容擷取"
>abstract="擷取是指從移轉集擷取內容，並放入目標Cloud Service例項。 「內容轉移工具」具備支援追加差異內容的功能，可以只轉移在上一次內容轉移活動後所進行的變更。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-ingestion-process" text="追加擷取"

請依照下列步驟，從「內容轉移工具」中擷取您的移轉集：
>[!NOTE]
>您可以執行選用的預先複製步驟，大幅加快擷取階段。 預複製步驟對於第1次完全擷取和擷取最有效。 請參閱 [使用AzCopy擷取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) 以取得更多詳細資訊。

>[!NOTE]
>您是否記得記錄此擷取的支援票證？ 請參閱 [使用內容轉移工具前的重要考量](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html#important-considerations) 以及其他考量事項，協助讓擷取成功。

1. 前往Cloud Acceleration Manager。 按一下您的專案卡，然後按一下「內容轉移」卡。 導覽至 **擷取工作** 按一下 **新擷取**

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)


1. 檢閱擷取檢查清單，並確保所有步驟皆已完成。 這些是確保成功擷取的必要步驟。 您可以繼續 **下一個** 步驟（僅在檢查清單已完成時執行）。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/Ingestion-checklist.png)

1. 提供建立新擷取所需的資訊。

   * 選取您剛提取作為來源的移轉集
   * 選取目標環境。 這是將擷取移轉集內容的位置。 選擇層。 （製作/發佈）。

   >[!NOTE]
   >
   >如果來源為「作者」，建議將其內嵌至目標上的「作者」階層。 同樣地，如果來源為「發佈」，則target也應為「發佈」。

   >[!NOTE]
   >
   >如果目標層為 `Author`，則擷取期間會關閉author例項，且使用者無法使用（例如，作者或執行維護的任何人等）。 這是為了保護系統，並防止任何可能遺失或導致擷取衝突的變更。 請確保您的團隊了解這一事實。 另請注意，環境在製作擷取期間會顯示為休眠。

   >[!NOTE]
   >
   >您可以執行選用的預先複製步驟，大幅加快擷取階段。 請參閱 [使用AzCopy擷取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) 以取得更多詳細資訊。
   > 
   >如果使用預復本擷取（適用於S3或Azure資料存放區），建議您先單獨執行製作擷取。 這會在稍後執行時加速發佈擷取。

   >[!IMPORTANT]
   >
   >只有在您屬於本機環境時，才能開始擷取至目的地環境 **AEM管理員** 群組(在目標Cloud Service作者服務上)。 如果您無法開始擷取，請參閱 [無法開始擷取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#unable-to-start-ingestion) 以取得更多詳細資訊。

   >[!IMPORTANT]
   >
   >若設定 **擦去** 系統會在擷取前啟用，而會刪除整個現有存放庫，並建立新存放庫以將內容擷取至中。 這表示會重設所有設定，包括目標Cloud Service例項的權限。 對於新增至 **管理員** 群組。 您需要重新新增至管理員群組，才能開始擷取。

1. 按一下 **內嵌**

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam22.png)

1. 接著，您可以從擷取工作清單檢視中監控擷取階段，並使用擷取的動作功能表，隨著擷取進行而檢視記錄。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23.png)

1. 擷取完成後，按一下畫面右上角的(i)按鈕，以取得擷取工作的詳細資訊。

<!-- Alexandru: hiding temporarily, until it's reviewed 

1. The **Migration Set ingestion** dialog box displays. Content can be ingested to either Author instance or Publish instance at a time. Select the instance to ingest content to. Click on **Ingest** to start the ingestion phase. 

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-02.png)

   >[!IMPORTANT]
   >If ingesting with pre-copy is used (for S3 or Azure Data Store), it is recommended to run Author ingestion first alone. This will speed up the Publish ingestion when it is run later. 

   >[!IMPORTANT]
   >When the **Wipe existing content on Cloud instance before ingestion** option is enabled, it deletes the entire existing repository and creates a new repository to ingest content into. This means that it resets all settings including permissions on the target Cloud Service instance. This is also true for an admin user added to the **administrators** group.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-03.png)

   Additionally, click on **Customer Care** to log a ticket, as shown in the figure below. 

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-04.png)
   
   Also, refer to [Important Considerations for Using Content Transfer Tool](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en#important-considerations) to learn more.

1. Once the ingestion is complete, the status under **Author ingestion** updates to **FINISHED**.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-05.png) -->

## 追加擷取 {#top-up-ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_topup"
>title="追加擷取"
>abstract="使用追加功能來移動自上次內容轉移活動以來修改的內容。 擷取完成後，檢查記錄中是否有任何錯誤/警告。 您應處理回報的問題，或聯絡Adobe客戶服務，以立即解決任何錯誤。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs.html?lang=en" text="檢視記錄"

「內容轉移工具」具備支援&#x200B;*追加*&#x200B;差異內容的功能，可以只轉移在上一次內容轉移活動後所進行的變更。

>[!NOTE]
>初始轉移內容後，建議您先頻繁地執行追加差異內容，以縮短最終差異化內容轉移的內容凍結時間，然後再於雲端服務上線。如果您已將預複製步驟用於第一次完整內嵌，則可以跳過預複製以用於後續追加內嵌（如果追加遷移集大小小於200GB），因為它可能會為整個流程增加時間。

擷取程式一旦完成，若要擷取需執行 [追加提取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process) 然後使用追加擷取方法。

您可以建立新的擷取工作，並確保 **擦去** 在擷取階段期間會停用，如下所示：

![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam24.png)

## 疑難排解 {#troubleshooting}

### CAM無法檢索遷移令牌 {#cam-unable-to-retrieve-the-migration-token}

自動擷取移轉代號可能會因不同原因而失敗，包括您 [透過Cloud Manager設定IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) 在目標Cloud Service環境中。 在這類情況下，當您嘗試開始擷取時，會看到下列對話方塊：

![影像](/help/journey-migration/content-transfer-tool/assets-ctt/troubleshooting-token.png)

您必須按一下對話方塊上的「取得Token」連結，以手動擷取移轉Token。 這會開啟另一個顯示代號的標籤。 接著，您可以複製代號，並貼到 **移轉代號輸入** 欄位。 現在，您應該可以開始擷取。

>[!NOTE]
>
>此代號將可供屬於本機的使用者使用 **AEM管理員** 群組(在目標Cloud Service作者服務上)。

### 無法開始擷取 {#unable-to-start-ingestion}

只有在您屬於本機環境時，才能開始擷取至目的地環境 **AEM管理員** 群組(在目標Cloud Service作者服務上)。 如果您不屬於AEM管理員群組，當您嘗試開始擷取時，會看到錯誤，如下所示。 您可以要求管理員將您新增至本機 **AEM管理員** 或要求代號本身，然後您可將其貼入 **移轉代號輸入** 欄位。

![影像](/help/journey-migration/content-transfer-tool/assets-ctt/error_nonadmin_ingestion.png)

### 仍啟用通過Release Orchestrator進行自動更新

Release Orchestrator通過自動應用更新來使環境保持最新。 如果執行擷取時觸發更新，可能會造成無法預測的結果，包括環境損毀。 這是啟動獲取之前應記錄支援票證的原因之一（請參閱上面的「注意」），以便可以安排臨時禁用Release Orchestrator的時間。

如果開始擷取時Release Orchestrator仍在執行中，UI會顯示此錯誤訊息。 您仍然可以選擇繼續操作，接受風險，方法是檢查欄位並再次按按鈕。

![影像](/help/journey-migration/content-transfer-tool/assets-ctt/error_releaseorchestrator_ingestion.png)

## 下一步 {#whats-next}

在您將內容擷取到Target中後，您就可以檢視每個步驟的記錄（擷取和擷取）並尋找錯誤。 請參閱 [檢視移轉集記錄](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/viewing-logs.html?lang=en) 了解更多。