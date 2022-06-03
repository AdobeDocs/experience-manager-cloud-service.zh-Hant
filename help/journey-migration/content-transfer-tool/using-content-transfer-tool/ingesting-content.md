---
title: 將內容插入目標
description: 將內容插入目標
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
source-git-commit: 05765bdaa681502b60fc5a7c943e2265c09764ec
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 16%

---

# 將內容插入目標 {#ingesting-content}

## 內容傳輸工具中的攝取過程 {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="內容攝取"
>abstract="Ingestion是指從遷移集中接收內容到目標Cloud Service實例。 「內容轉移工具」具備支援追加差異內容的功能，可以只轉移在上一次內容轉移活動後所進行的變更。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-ingestion-process" text="追加擷取"

請依照下列步驟，從「內容轉移工具」中擷取您的移轉集：
>[!NOTE]
>您可以運行可選的預複製步驟，以顯著加快接收階段。 預拷貝步驟對第一次完全提取和攝取最有效。 請參閱 [使用AzCopy插入](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) 的子菜單。

1. 轉至雲加速管理器。 按一下項目卡，然後按一下內容傳輸卡。 導航到 **攝取作業** 按一下 **新攝取**

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. 提供建立新攝取的所需資訊。

   * 選擇剛提取為源的遷移集
   * 選擇目標環境。 這是遷移集內容的攝取位置。 選擇層。 （作者/發佈）。

   >[!NOTE]
   >
   >如果源是「作者」，則建議將其插入目標上的「作者」層。 同樣，如果源為「發佈」，則目標也應為「發佈」。

   >[!NOTE]
   >
   >您可以運行可選的預複製步驟，以顯著加快接收階段。 請參閱 [使用AzCopy插入](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) 的子菜單。
   > 
   >如果使用預拷貝進行接收（對於S3或Azure資料儲存），建議先單獨運行Author接收。 這將在稍後運行「發佈」接收時加速。

   >[!IMPORTANT]
   >
   >只有您屬於本地環境，您才能啟動對目標環境的接收 **AEM管理員** 正在傳輸內容的Cloud Service實例中的組。 如果您不屬於管理AEM員組，則在嘗試開始攝取時將出現如下所示的錯誤。
   >![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam21.png)

   >[!IMPORTANT]
   >
   >如果設定 **擦除** 在接收前啟用，它將刪除整個現有儲存庫並建立新儲存庫以將內容接收到。 這意味著它會重置所有設定，包括對目標Cloud Service實例的權限。 對於添加到 **管理員** 組。 需要將您重新添加到管理員組，以開始攝取。

1. 按一下 **英格斯特**

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam22.png)

1. 然後，可以從「攝取作業」清單視圖監視攝取階段

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23.png)

1. 完成攝取後，按一下螢幕右上角的(i)按鈕以獲取有關攝取作業的詳細資訊。

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
>id="aemcloud_ctt_ingestion_topup" title="Top Up Ingestion"
>abstract="使用自上一個內容傳輸活動以來的向上移動功能來移動修改的內容。 接收完成後，檢查日誌中是否有錯誤/警告。 任何錯誤都應通過處理報告的問題或與Adobe客戶服務部聯繫立即解決。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs.html?lang=en" text="查看日誌"

「內容轉移工具」具備支援&#x200B;*追加*&#x200B;差異內容的功能，可以只轉移在上一次內容轉移活動後所進行的變更。

>[!NOTE]
>初始轉移內容後，建議您先頻繁地執行追加差異內容，以縮短最終差異化內容轉移的內容凍結時間，然後再於雲端服務上線。如果已將預拷貝步驟用於第一次完整接收，則可以跳過預拷貝步驟以用於後續的自頂向上接收（如果自頂向上遷移集大小小於200GB），因為它可能會為整個過程增加時間。

接收過程完成後，要接收需要運行的增量內容 [自頂向上提取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process) 然後用自頂式攝食法。

您可以通過建立新的攝取作業來完成此操作，並確保 **擦除** 在接收階段禁用，如下所示：

![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam24.png)



## 下一步 {#whats-next}

在內容傳輸工具中學習「將內容導入目標」後，您可以在完成每個步驟（提取和接收）後查看日誌，並查找錯誤。 請參閱 [查看遷移集的日誌](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/viewing-logs.html?lang=en) 來瞭解更多資訊。
