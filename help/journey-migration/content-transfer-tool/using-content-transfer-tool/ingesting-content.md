---
title: 將內容引入雲端服務
description: 瞭解如何使用Cloud Acceleration Manager將移轉集中的內容擷取到目標Cloud Service例項。
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
source-git-commit: 8795d9d2078d9f49699ffa77b1661dbe5451a4a2
workflow-type: tm+mt
source-wordcount: '2534'
ht-degree: 6%

---

# 將內容引入雲端服務 {#ingesting-content}

## Cloud Acceleration Manager 中的摘取程序 {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="內容攝入"
>abstract="攝入是指將移轉集中的內容攝入到目標 Cloud Service 執行個體中。「內容轉移工具」具備支援追加差異內容的功能，可以只轉移在上一次內容轉移活動後所進行的變更。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content.html#top-up-extraction-process" text="填滿提取"

請依照下列步驟，使用Cloud Acceleration Manager擷取您的移轉集：

1. 前往Cloud Acceleration Manager。 按一下您的專案卡，然後按一下「內容轉移」卡。 瀏覽至 **內嵌工作** 並按一下 **新增內嵌**

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. 檢閱擷取檢查清單，並確保完成所有步驟。 若要確保成功擷取，這些步驟是必要的。 繼續前往 **下一個** 只有在檢查清單完成時才會執行此步驟。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/Ingestion-checklist.png)

1. 提供建立內嵌所需的資訊。

   * **移轉集：** 選取包含擷取資料的移轉集作為來源。
      * 移轉集將在長時間不活動後過期，因此預期擷取會在執行擷取後不久進行。 檢閱 [移轉集到期](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) 以取得詳細資訊。

   >[!TIP]
   > 如果擷取正在執行，對話方塊將會指出它。 擷取一旦成功完成，就會自動開始內嵌。 如果擷取失敗或停止，擷取工作將會撤銷。

   * **目的地：** 選取目標環境。 此環境是擷取移轉集內容的地方。
      * 內嵌不支援快速開發環境(RDE)或預覽型別的目的地，並且即使使用者有權存取，也不會顯示為可能的目的地選擇。
      * 雖然移轉集可同時內嵌至多個目的地，但目的地一次只能是一個執行或等待內嵌的目標。

   * **階層：** 選取階層。 （作者/發佈）。
      * 如果來源是 `Author`，建議將其擷取至 `Author` 在目標上層。 同樣地，如果來源為 `Publish`，目標應該是 `Publish` 以及。

   >[!NOTE]
   > 如果目標層為 `Author`，作者例項會在擷取期間關閉，且無法供使用者（例如作者或執行維護的任何人）使用。 原因是為了保護系統，並防止任何可能遺失或導致擷取衝突的變更。 確保您的團隊知道這個事實。 另請注意，環境在作者擷取期間似乎處於休眠狀態。

   * **擦去：** 選擇 `Wipe` 值
      * 此 **擦去** 選項會設定目的地的擷取起點。 如果 **擦去** 已啟用，包含其所有內容的目的地會重設為Cloud Manager中指定的AEM版本。 如果未啟用，目的地會維持目前內容為起點。
      * 此選項會 **NOT** 會影響執行內容內嵌的方式。 內嵌一律會使用內容取代策略，並 _非_ 內容合併策略，因此 **擦去** 和 **非擦去** 在這種情況下，擷取移轉集將會覆寫目的地上相同路徑的內容。 例如，如果移轉集包含 `/content/page1` 目的地已包含 `/content/page1/product1`，內嵌會移除整個 `page1` 路徑及其子頁面，包括 `product1`，並以移轉集中的內容取代。 這表示執行時，必須仔細規劃 **非擦去** 內嵌至包含任何應維護之內容的目的地。

   >[!IMPORTANT]
   > 如果設定 **擦去** 會啟用擷取，並重設整個現有存放庫，包括目標Cloud Service例項的使用者許可權。 對於新增至的管理員使用者，此重設也是true **管理員** 群組，並且必須再次將該使用者新增到管理員群組，才能開始內嵌。

   * **預先複製：** 選擇 `Pre-copy` 值
      * 您可以執行選用的預先複製步驟，大幅加快內嵌速度。 另請參閱 [使用AzCopy內嵌](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) 以取得更多詳細資料。
      * 如果使用具有預先複製的內嵌（適用於S3或Azure資料存放區），建議執行 `Author` 請先單獨內嵌。 如此一來，您就可以加快 `Publish` 擷取（稍後執行）。

   >[!IMPORTANT]
   > 只有當您屬於本機時，才能起始對目的地環境的內嵌 **AEM管理員** 目的地Cloud Service作者服務上的群組 如果您無法開始內嵌，請參閱 [無法開始內嵌](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#unable-to-start-ingestion) 以取得更多詳細資料。

1. 按一下 **擷取**.

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam22.png)

1. 然後，您可以從「內嵌工作」清單檢視中監視內嵌，並使用內嵌的動作功能表來檢視持續時間並記錄內嵌進度。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23.png)

1. 按一下 **(i)** 列中的按鈕，以取得擷取工作的詳細資訊。 您可以按一下「 」，在執行或完成擷取的每個步驟時檢視其持續時間 **...**，然後按一下 **檢視持續時間**. 擷取的資訊也會顯示出來，以瞭解正在擷取的內容。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23b.png)

## 填滿攝入 {#top-up-ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_topup"
>title="填滿攝入"
>abstract="使用填滿功能來移動自上次內容轉移活動以來修改的內容。攝入完成後，檢查記錄檔中是否有任何錯誤或警告。如有任何錯誤應立即處理，方法是處理回報的問題或聯絡 Adobe 客戶服務。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs.html?lang=zh-Hant" text="檢視記錄檔"

「內容轉移工具」具備可透過執行 *追加* 移轉集的。 如此可修改移轉集，使其僅包含自上次擷取以來已變更的內容，而無須再次擷取所有內容。

>[!NOTE]
>初始轉移內容後，建議您先頻繁地執行追加差異內容，以縮短最終差異化內容轉移的內容凍結時間，然後再於Cloud Service上線。 如果您在第一次擷取使用了預先複製步驟，您可以略過後續追加擷取的預先複製（如果追加移轉集大小小於200 GB）。 原因是它可能會為整個程式增加時間。

若要在某些內嵌完成之後內嵌差異內容，您必須執行 [追加提取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)，然後搭配使用內嵌方法與 **擦去** 選項 **已停用**. 請務必閱讀 **擦去** 上方說明，以避免遺失目的地上的內容。

從建立內嵌工作開始，並確保 **擦去** 會在擷取期間停用，如下所示：

![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam24.png)

## 疑難排解 {#troubleshooting}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_troubleshooting"
>title="內容攝取故障排除"
>abstract="請參閱攝入記錄和文件，了解攝入失敗的常見原因，並尋找修正問題的解決方案。修正之後，就可以再次執行攝入。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers.html" text="驗證內容轉移"

### CAM無法擷取移轉權杖 {#cam-unable-to-retrieve-the-migration-token}

自動擷取移轉權杖可能會因不同原因而失敗，包括您 [透過Cloud Manager設定IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) 在目標Cloud Service環境中。 在這種情況下，當您嘗試開始內嵌時，會看到下列對話方塊：

![影像](/help/journey-migration/content-transfer-tool/assets-ctt/troubleshooting-token.png)

按一下對話方塊上的「取得權杖」連結，手動擷取移轉權杖。 另一個標籤會開啟，顯示Token。 然後，您可以複製代號並將其貼到 **移轉權杖輸入** 欄位。 現在，您應該能夠開始內嵌。

>[!NOTE]
>
>權杖可供屬於本機的使用者使用 **AEM管理員** 目的地Cloud Service作者服務上的群組

### 無法開始內嵌 {#unable-to-start-ingestion}

只有當您屬於本機時，才能起始對目的地環境的內嵌 **AEM管理員** 目的地Cloud Service作者服務上的群組 如果您不屬於AEM管理員群組，當您嘗試開始內嵌時，會看到如下所示的錯誤。 您可以要求管理員將您新增至本機 **AEM管理員** 或要求代號本身，然後您可將它貼到 **移轉權杖輸入** 欄位。

![影像](/help/journey-migration/content-transfer-tool/assets-ctt/error_nonadmin_ingestion.png)

### 無法連線至移轉服務 {#unable-to-reach-migration-service}

請求內嵌後，可能會向使用者顯示類似以下訊息：「無法聯絡目標環境上的移轉服務。 如果是這樣的話，請稍後再試或聯絡Adobe支援。」

![影像](/help/journey-migration/content-transfer-tool/assets-ctt/error_cannot_reach_migser.png)

此訊息指出Cloud Acceleration Manager無法連線到目標環境的移轉服務來開始內嵌。 發生此狀況可能有各種原因。

>[!NOTE]
> 
> 顯示「移轉權杖」欄位，因為在少數情況下，實際上不允許擷取該權杖。 透過允許手動提供，這可讓使用者無需任何其他協助即可快速開始內嵌。 如果提供Token，但訊息仍顯示，則擷取Token並非問題。

* AEMas a Cloud Service會維護環境狀態，而且偶爾會因為各種正常原因而重新啟動移轉服務。 如果服務正在重新啟動，則無法連線到該服務，但最終會提供該服務。
* 執行個體上可能正在執行另一個處理序。 例如，如果 [AEM版本更新](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates.html) 正在套用更新，系統可能忙碌中，且移轉服務定期無法使用。 完成該程式後，可以再次嘗試開始內嵌。
* 如果 [已套用IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) 透過Cloud Manager，它會封鎖Cloud Acceleration Manager，使其無法連線至移轉服務。 無法新增用於內嵌的IP位址，因為其位址是動態的。 目前，唯一的解決方案是在擷取和索引過程中停用IP允許清單。
* 可能有其他原因需要調查。 如果內嵌或索引繼續失敗，請聯絡Adobe客戶服務。

### AEM版本更新與擷取 {#aem-version-updates-and-ingestions}

[AEM版本更新](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates.html) 會自動套用至環境，以使用最新的AEMas a Cloud Service版本。 如果在執行內嵌時觸發更新，可能會導致無法預測的結果，包括環境損毀。

如果「AEM版本更新」已上線到目的地程式，則擷取程式會嘗試在開始前停用其佇列。 擷取完成時，版本更新程式狀態會傳回至擷取開始前的狀態。

>[!NOTE]
>
> 您不再需要記錄支援票證來停用「AEM版本更新」。

如果「AEM版本更新」作用中（即更新正在執行或排入佇列等待執行），則擷取不會開始，且使用者介面會顯示下列訊息。 更新完成後，即可開始內嵌。 Cloud Manager可用於檢視計畫管道的目前狀態。

>[!NOTE]
>
> 「AEM版本更新」會在環境的管道中執行，並等候管道清除。 如果更新排入佇列的時間比預期長，請確保自訂工作流程不會無意中鎖定管道。

![影像](/help/journey-migration/content-transfer-tool/assets-ctt/error_releaseorchestrator_active.png)

### 由於違反唯一性限制，追加擷取失敗 {#top-up-ingestion-failure-due-to-uniqueness-constraint-violation}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_uuid"
>title="唯一性限制違規"
>abstract="非擦去擷取失敗的常見原因是節點ID發生衝突。 只有一個衝突節點可以存在。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content.html#top-up-ingestion-process" text="追加擷取"

造成問題的常見原因 [追加擷取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) 失敗是節點id中的衝突。 若要識別此錯誤，請使用Cloud Acceleration Manager UI下載擷取記錄，並尋找類似以下的專案：

>java.lang.RuntimeException： org.apache.jackrabbit.oak.api.CommitFailedException： OakConstraint0030：違反唯一性條件約束 [jcr：uuid] 具有值a1a1a1a1-b2b2-c3c3-d4d4-e5e5e5e5： /some/path/jcr：content， /some/other/path/jcr：content

AEM中的每個節點都必須有唯一的uuid。 此錯誤指出正在擷取的節點與目的地執行個體上不同路徑中存在的節點具有相同的uuid。 發生此狀況有兩個原因：

* 節點會在擷取和後續作業之間移動至來源上 [追加提取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)
   * _記住_：針對追加提取，即使節點已不存在於來源中，該節點仍將存在於移轉集中。
* 目的地上的節點會在擷取與後續追加擷取之間移動。

此衝突必須手動解決。 熟悉內容的人必須決定必須刪除兩個節點中的哪一個，同時留意參考該內容的其他內容。 解決方案可能要求再次執行追加擷取，而不需要違反規定的節點。

### 由於無法刪除參照的節點，追加擷取失敗 {#top-up-ingestion-failure-due-to-unable-to-delete-referenced-node}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_referenced_node"
>title="無法刪除參考的節點"
>abstract="非擦去擷取失敗的常見原因是目的地執行個體上特定節點的版本衝突。 必須修正節點的版本。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content.html#top-up-ingestion-process" text="追加擷取"

另一個常見原因 [追加擷取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) 失敗是目的地執行個體上特定節點的版本衝突。 若要識別此錯誤，請使用Cloud Acceleration Manager UI下載擷取記錄，並尋找類似以下的專案：

>java.lang.RuntimeException： org.apache.jackrabbit.oak.api.CommitFailedException： OakIntegrity0001：無法刪除參照的節點： 8a2289f4-b904-4bd0-8410-15e41e0976a8

如果目的地的節點在內嵌和後續內嵌之間被修改，就可能發生這種情況 **非擦去** 內嵌，使得已建立新版本。 如果在啟用「包含版本」的情況下擷取移轉集，則可能會發生衝突，因為目的地現在具有由版本記錄和其他內容參考的更新版本。 由於違規版本節點被引用，擷取程式無法刪除該節點。

解決方案可能要求再次執行追加擷取，而不需要違反規定的節點。 或者，建立違規節點的小型移轉集，但停用「包含版本」。

最佳實務指出，如果 **非擦去** 內嵌必須使用包含版本的移轉集執行，儘可能減少修改目的地上的內容至關重要，直到移轉歷程完成。 否則，這些衝突可能會發生。

### 由於大型節點屬性值而導致擷取失敗 {#ingestion-failure-due-to-large-node-property-values}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_bson"
>title="大型節點屬性"
>abstract="擷取失敗的常見原因是超過節點屬性值的大小上限。 請依照檔案（包括與BPA報告相關的檔案）來補救這種情況。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html" text="移轉必要條件"

儲存在MongoDB中的節點屬性值不能超過16 MB。 如果節點值超過支援的大小，擷取會失敗，且記錄會包含 `BSONObjectTooLarge` 錯誤並指定哪個節點超過最大值。 這是MongoDB限制。

請參閱 `Node property value in MongoDB` 中的附註 [內容轉移工具的先決條件](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/prerequisites-content-transfer-tool.md) 以取得詳細資訊，以及可協助尋找所有大型節點的Oak工具連結。 修正所有大型節點後，請再次執行擷取和擷取。

### 內嵌已取消 {#ingestion-rescinded}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_rescinded"
>title="內嵌已取消"
>abstract="內嵌正在等候的擷取未成功完成。 內嵌已取消，因為無法執行。"

使用執行中的擷取作為來源移轉集而建立的擷取會耐心等待，直到擷取成功，而且在那一刻會正常開始。 如果擷取失敗或停止，則擷取及其索引工作將不會開始，但會取消。 在這種情況下，請檢查擷取以確定失敗的原因，修正問題並重新開始擷取。 執行固定擷取後，即可排程新的內嵌。

## 下一步 {#whats-next}

擷取成功後，AEM索引會自動開始。 另請參閱 [移轉內容後建立索引](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/indexing-content.md) 以取得詳細資訊。

完成將內容擷取到Cloud Service中後，您可以檢視每個步驟的記錄（擷取和擷取）並尋找錯誤。 另請參閱 [檢視移轉集記錄](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/viewing-logs.md) 以進一步瞭解。
