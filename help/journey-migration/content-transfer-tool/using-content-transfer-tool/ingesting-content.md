---
title: 將內容內嵌至目標
description: 將內容內嵌至目標
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
source-git-commit: addfa18ed8fa45b1cfc17d4e35cbdde47b491507
workflow-type: tm+mt
source-wordcount: '1753'
ht-degree: 12%

---

# 將內容內嵌至目標 {#ingesting-content}

## 內容傳輸工具中的攝取過程 {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="內容攝入"
>abstract="攝入是指將移轉集中的內容攝入到 Cloud Service 執行個體中。「內容轉移工具」具備支援追加差異內容的功能，可以只轉移在上一次內容轉移活動後所進行的變更。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html#top-up-ingestion-process" text="追加擷取"

請依照下列步驟，從「內容轉移工具」中擷取您的移轉集：

>[!NOTE]
>你記得為這次攝取記錄支援票嗎？ 請參閱 [使用內容傳輸工具之前的重要注意事項](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html#important-considerations) 以及其他的考慮，使攝入成功。

1. 轉至雲加速管理器。 按一下項目卡，然後按一下內容傳輸卡。 導航到 **攝取作業** 按一下 **新攝取**

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. 檢查攝入檢查表，確保所有步驟均已完成。 這些是確保成功攝取的必要步驟。 您將能夠繼續 **下一個** 步驟，僅在完成核對表時執行。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/Ingestion-checklist.png)

1. 提供建立新攝取的所需資訊。

   * 選擇包含提取資料的遷移集作為源。
      * 遷移集將在長時間不活動後過期，因此預期在執行提取後較快發生攝取。 審閱 [遷移集到期](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) 的雙曲餘切值。
   * 選擇目標環境。 這是遷移集內容的攝取位置。 選擇層。 （作者/發佈）。 不支援快速開發環境。

   >[!NOTE]
   >以下注釋適用於插入內容：
   > 如果源是「作者」，則建議將其插入目標上的「作者」層。 同樣，如果源為「發佈」，則目標也應為「發佈」。
   > 如果目標層為 `Author`，提交實例將在接收期間關閉，用戶將無法使用（例如，作者或執行維護的任何人）。 這是為了保護系統，並防止任何可能丟失或導致攝取衝突的更改。 請確保您的團隊瞭解這一事實。 另請注意，在作者攝取期間，環境將出現冬眠。
   > 您可以運行可選的預複製步驟，以顯著加快接收階段。 請參閱 [使用AzCopy插入](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) 的子菜單。
   > 如果使用預拷貝進行接收（對於S3或Azure資料儲存），建議先單獨運行Author接收。 這將在稍後運行「發佈」接收時加速。
   > Ingestions不支援快速開發環境(RDE)目標。 即使用戶有權訪問，它們也不會顯示為可能的目標選項。

   >[!IMPORTANT]
   > 以下重要通知適用於接收內容：
   > 只有您屬於本地環境，您才能啟動對目標環境的攝取 **AEM管理員** 目標Cloud Service作者服務上的組。 如果無法開始攝取，請參閱 [無法啟動攝取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#unable-to-start-ingestion) 的子菜單。
   > 如果設定 **擦除** 在接收前啟用，它將刪除整個現有儲存庫並建立新儲存庫以將內容接收到。 這意味著它會重置所有設定，包括對目標Cloud Service實例的權限。 對於添加到 **管理員** 組。 需要將您重新添加到管理員組，以開始攝取。

1. 按一下 **英格斯特**

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam22.png)

1. 然後，可以從「攝取作業」清單視圖中監視攝取階段，並使用攝取的操作菜單查看攝取進度的日誌。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23.png)

1. 按一下 **(i)** 的子菜單。 通過按一下，可以查看接收執行或完成的每個步驟的持續時間 **...** 然後 **查看持續時間**。 還顯示來自提取的資訊以實現正在攝取的內容。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23b.png)

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
   
   Also, refer to [Important Considerations for Using Content Transfer Tool](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html#important-considerations) to learn more.

1. Once the ingestion is complete, the status under **Author ingestion** updates to **FINISHED**.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-05.png) -->

## 追加擷取 {#top-up-ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_topup"
>title="追加擷取"
>abstract="使用填滿功能來移動自上次內容轉移活動以來修改的內容。攝入完成後，檢查記錄檔中是否有任何錯誤/警告。如有任何錯誤應立即處理，方法是處理回報的問題或聯絡 Adobe 客戶服務。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs.html" text="檢視記錄檔"

「內容轉移工具」具備支援&#x200B;*追加*&#x200B;差異內容的功能，可以只轉移在上一次內容轉移活動後所進行的變更。

>[!NOTE]
>初始轉移內容後，建議您先頻繁地執行追加差異內容，以縮短最終差異化內容轉移的內容凍結時間，然後再於雲端服務上線。如果已將預拷貝步驟用於第一次完整接收，則可以跳過預拷貝步驟以用於後續的自頂向上接收（如果自頂向上遷移集大小小於200GB），因為它可能會為整個過程增加時間。

接收過程完成後，要接收需要運行的增量內容 [自頂向上提取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process) 然後用自頂式攝食法。

您可以通過建立新的攝取作業來完成此操作，並確保 **擦除** 在接收階段禁用，如下所示：

![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam24.png)

## 疑難排解 {#troubleshooting}

### CAM無法檢索遷移令牌 {#cam-unable-to-retrieve-the-migration-token}

遷移令牌的自動檢索可能因不同原因而失敗，包括您 [通過雲管理器設定IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) 在目標Cloud Service環境中。 在這些情況下，當您嘗試開始攝取時，將看到以下對話框：

![影像](/help/journey-migration/content-transfer-tool/assets-ctt/troubleshooting-token.png)

您需要通過按一下對話框上的「獲取令牌」連結手動檢索遷移令牌。 這將開啟另一個顯示令牌的頁籤。 然後，可以複製標籤並將其貼上到 **遷移令牌輸入** 的子菜單。 現在，你應該能開始消化。

>[!NOTE]
>
>該令牌將可供屬於本地的用戶使用 **AEM管理員** 目標Cloud Service作者服務上的組。

### 無法啟動攝取 {#unable-to-start-ingestion}

只有您屬於本地環境，您才能啟動對目標環境的攝取 **AEM管理員** 目標Cloud Service作者服務上的組。 如果您不屬於管理AEM員組，則在嘗試開始攝取時將出現如下所示的錯誤。 您可以要求管理員將您添加到本地 **AEM管理員** 或者要求令牌本身，然後你可以將令牌貼上到 **遷移令牌輸入** 的子菜單。

![影像](/help/journey-migration/content-transfer-tool/assets-ctt/error_nonadmin_ingestion.png)

### 無法訪問遷移服務 {#unable-to-reach-migration-service}

在請求攝取後，可向用戶顯示如下消息：&quot;目標環境上的遷移服務當前無法訪問。 請稍後再試或與Adobe支援聯繫。」

![影像](/help/journey-migration/content-transfer-tool/assets-ctt/error_cannot_reach_migser.png)

這表示雲加速管理器無法到達目標環境的遷移服務以啟動接收。 這可能有多種原因。

>[!NOTE]
> 
> 顯示「遷移令牌」欄位，因為在少數情況下檢索該令牌是實際不允許的。 通過允許手動提供，它可允許用戶快速開始攝取，而無需任何附加幫助。 如果提供令牌，但仍顯示消息，則檢索令牌不是問題。

* AEMas a Cloud Service維護環境狀態，有時由於一些正常原因可能需要重新啟動遷移服務。 如果該服務正在重新啟動，則無法訪問它，但將很快可用。
* 可能正在實例上運行另一個進程。 例如，如果Release Orchestrator正在應用更新，則系統可能正忙，並且遷移服務定期不可用。 因此，強烈建議在攝取期間暫停更新。
* 如果 [已應用IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) 通過雲管理器，阻止雲加速管理器到達遷移服務。 無法為接收添加IP地址，因為其地址非常動態。 目前，唯一的解決方案是在接收正在運行時禁用IP允許清單。
* 可能還有其他原因需要調查。 如果攝取仍然失敗，請與Adobe客戶服務部聯繫。

### 通過Release Orchestrator進行的自動更新仍處於啟用狀態

Release Orchestrator通過自動應用更新自動保持環境的最新。 如果在執行攝取時觸發更新，則可能導致無法預知的結果，包括環境損壞。 這是啟動接收之前應記錄支援票證的原因之一（請參閱上面的「注釋」），以便可以計畫臨時禁用Release Orchestrator。

如果啟動接收時Release Orchestrator仍在運行，則UI將顯示此消息。 無論如何，您都可以選擇繼續，接受風險，方法是檢查欄位並再次按按鈕。

>[!NOTE]
>
> Release Orchestrator現在正在部署到開發環境，因此也應暫停這些環境的更新。

![影像](/help/journey-migration/content-transfer-tool/assets-ctt/error_releaseorchestrator_ingestion.png)

### 自頂向上攝取失敗

一個 [向上攝取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) 失敗是節點ID中的衝突。 要識別此錯誤，請使用雲加速管理器UI下載接收日誌，並查找以下條目：

>java.lang.RuntimeException:org.apache.jackrabbit.oak.api.CommitFailedException:OakConstraint0030:違反唯一性約束的屬性 [jcr:uuid] 具有值a1a1a1-b2b2-c3c3-d4d4-e5e5e5e5/some/path/jcr:content, /some/other/path/jcr:content

中的每個節AEM點必須具有唯一UUID。 此錯誤表示正在攝取的節點與目標實例上其他路徑上已存在的節點具有相同的uuid。
如果節點在源上在抽取和後續操作之間移動，則會發生這種情況 [自頂向上提取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)。
如果目標上的節點在攝取和隨後的自上而上攝取之間移動，也可能發生這種情況。

必須手動解決此衝突。 熟悉內容的人必須決定必須刪除兩個節點中的哪個節點，同時要記住引用該節點的其他內容。 該解決方案可能要求在沒有違規節點的情況下再次進行自頂提取。

## 下一步 {#whats-next}

完成「將內容導入目標」後，您可以查看每個步驟（提取和接收）的日誌並查找錯誤。 請參閱 [查看遷移集的日誌](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/viewing-logs.html) 來瞭解更多資訊。
