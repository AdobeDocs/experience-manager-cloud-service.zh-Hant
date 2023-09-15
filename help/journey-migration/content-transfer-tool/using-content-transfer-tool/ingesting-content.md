---
title: 將內容擷取至Cloud Service
description: 瞭解如何使用Cloud Acceleration Manager將移轉集中的內容擷取到目標Cloud Service例項。
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
source-git-commit: 5c482e5f883633c04d70252788b01f878156bac8
workflow-type: tm+mt
source-wordcount: '2142'
ht-degree: 6%

---

# 將內容擷取至Cloud Service {#ingesting-content}

## Cloud Acceleration Manager中的擷取程式 {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="內容攝入"
>abstract="擷取指的是從移轉集擷取內容，並存放至目的地Cloud Service例項。 「內容轉移工具」具備支援追加差異內容的功能，可以只轉移在上一次內容轉移活動後所進行的變更。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content.html#top-up-extraction-process" text="填滿提取"

請依照下列步驟，使用Cloud Acceleration Manager擷取您的移轉集：

>[!NOTE]
>您記得為此擷取記錄支援票證嗎？ 另請參閱 [使用內容轉移工具前的重要考量](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html#important-considerations) 以及有助於成功擷取的其他考量事項。

1. 前往Cloud Acceleration Manager。 按一下您的專案卡，然後按一下「內容轉移」卡。 瀏覽至 **內嵌工作** 並按一下 **新增內嵌**

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. 檢閱擷取檢查清單，並確保完成所有步驟。 若要確保成功擷取，這些步驟是必要的。 繼續前往 **下一個** 只有在檢查清單完成時才會執行此步驟。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/Ingestion-checklist.png)

1. 提供建立內嵌所需的資訊。

   * 選取包含擷取資料的移轉集作為來源。
      * 移轉集將在長時間不活動後過期，因此預期擷取會在執行擷取後不久進行。 檢閱 [移轉集到期](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) 以取得詳細資訊。
   * 選取目標環境。 此環境是擷取移轉集內容的地方。 選取階層。 （作者/發佈）。 不支援快速開發環境。

   >[!NOTE]
   >下列附註適用於擷取內容：
   > 如果來源是「作者」，建議將其擷取至目標上的「作者」階層。 同樣地，如果來源是「發佈」，則目標也應該是「發佈」。
   > 如果目標層為 `Author`，作者例項會在擷取期間關閉，且無法供使用者（例如作者或執行維護的任何人）使用。 原因是為了保護系統，並防止任何可能遺失或導致擷取衝突的變更。 確保您的團隊知道這個事實。 另請注意，環境在作者擷取期間似乎處於休眠狀態。
   > 您可以執行選用的預先複製步驟，大幅加快內嵌速度。 另請參閱 [使用AzCopy內嵌](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) 以取得更多詳細資料。
   > 如果使用具有預先複製的內嵌（用於S3或Azure資料存放區），建議先單獨執行作者內嵌。 這麼做可加快發佈擷取稍後執行的速度。
   > 內嵌不支援快速開發環境(RDE)目的地，即使使用者擁有存取權，也不會顯示為可能的目的地選擇。

   >[!IMPORTANT]
   > 只有當您屬於本機時，才能起始對目的地環境的內嵌 **AEM管理員** 目的地Cloud Service作者服務上的群組 如果您無法開始內嵌，請參閱 [無法開始內嵌](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#unable-to-start-ingestion) 以取得更多詳細資料。

   * 選擇 `Wipe` 值
      * 此 **擦去** 選項會設定目的地的擷取起點。 如果 **擦去** 已啟用，包含其所有內容的目的地會重設為Cloud Manager中指定的AEM版本。 如果未啟用，目的地會維持目前內容為起點。
      * 請注意，此選項可以 **NOT** 會影響執行內容內嵌的方式。 內嵌一律會使用內容取代策略，並 _非_ 內容合併策略，因此 **擦去** 和 **非擦去** 在這種情況下，擷取移轉集將會覆寫目的地上相同路徑的內容。 例如，如果移轉集包含 `/content/page1` 目的地已包含 `/content/page1/product1`，內嵌將會移除整個 `page1` 路徑及其子頁面，包括 `product1`，並以移轉集中的內容取代。 這表示執行時，必須仔細規劃 **非擦去** 內嵌至包含任何應維護之內容的目的地。

   >[!IMPORTANT]
   > 如果設定 **擦去** 會啟用擷取，並重設整個現有存放庫，包括目標Cloud Service例項的使用者許可權。 對於新增至的管理員使用者，此重設也是true **管理員** 群組，並且必須再次將該使用者新增到管理員群組，才能開始內嵌。

1. 按一下 **擷取**.

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam22.png)

1. 然後，您可以從「內嵌工作」清單檢視中監視內嵌，並使用內嵌的動作功能表來檢視持續時間並記錄內嵌進度。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23.png)

1. 按一下 **(i)** 列中的按鈕，以取得擷取工作的詳細資訊。 您可以按一下「 」，在執行或完成擷取的每個步驟時檢視其持續時間 **...**，然後按一下 **檢視持續時間**. 擷取的資訊也會顯示出來，以瞭解正在擷取的內容。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23b.png)

## 追加擷取 {#top-up-ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_topup"
>title="追加擷取"
>abstract="使用填滿功能來移動自上次內容轉移活動以來修改的內容。攝入完成後，檢查記錄檔中是否有任何錯誤/警告。如有任何錯誤應立即處理，方法是處理回報的問題或聯絡 Adobe 客戶服務。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs.html?lang=zh-Hant" text="檢視記錄檔"

「內容轉移工具」具備可透過執行 *追加* 移轉集的。 如此可修改移轉集，使其僅包含自上次擷取以來已變更的內容，而無須再次擷取所有內容。

>[!NOTE]
>初始轉移內容後，建議您先頻繁地執行追加差異內容，以縮短最終差異化內容轉移的內容凍結時間，然後再於雲端服務上線。如果您在第一次擷取使用了預先複製步驟，您可以略過後續追加擷取的預先複製（如果追加移轉集大小小於200 GB）。 原因是它可能會為整個程式增加時間。

若要在某些內嵌完成之後內嵌差異內容，您必須執行 [追加提取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)，然後搭配使用內嵌方法與 **擦去** 選項 **已停用**. 請務必閱讀 **擦去** 上方說明，以避免遺失目的地上的內容。

從建立內嵌工作開始，並確保 **擦去** 會在擷取期間停用，如下所示：

![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam24.png)

## 疑難排解 {#troubleshooting}

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
* 執行個體上可能正在執行另一個處理序。 例如，如果Release Orchestrator套用更新，系統可能會忙碌，而且移轉服務會定期無法使用。 再加上可能會損毀中繼或生產執行個體，因此強烈建議在內嵌期間暫停更新。
* 如果 [已套用IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) 透過Cloud Manager，它會封鎖Cloud Acceleration Manager，使其無法連線至移轉服務。 無法新增用於內嵌的IP位址，因為其位址是動態的。 目前，唯一的解決方案是在內嵌執行期間停用IP允許清單。
* 可能有其他原因需要調查。 如果內嵌仍持續失敗，請聯絡Adobe客戶服務。

### 透過Release Orchestrator的自動更新仍然啟用

Release Orchestrator會自動套用更新，讓環境保持最新狀態。 如果在執行內嵌時觸發更新，可能會導致無法預測的結果，包括環境損毀。 有充分理由在開始內嵌前先記錄客戶支援票證（請參閱上述「附註」），如此便可排程暫時停用Release Orchestrator。

如果內嵌開始時Release Orchestrator仍在執行，使用者介面會顯示此訊息。 您仍然可以選擇繼續，接受風險，方法是檢查欄位並再次按按鈕。

>[!NOTE]
>
> Release Orchestrator現在正部署至開發環境，因此也應該暫停這些環境的更新。

![影像](/help/journey-migration/content-transfer-tool/assets-ctt/error_releaseorchestrator_ingestion.png)

### 由於違反唯一性限制，追加擷取失敗

造成問題的常見原因 [追加擷取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) 失敗是節點id中的衝突。 若要識別此錯誤，請使用Cloud Acceleration Manager UI下載擷取記錄，並尋找類似以下的專案：

>java.lang.RuntimeException： org.apache.jackrabbit.oak.api.CommitFailedException： OakConstraint0030：違反唯一性條件約束 [jcr：uuid] 具有值a1a1a1a1-b2b2-c3c3-d4d4-e5e5e5e5： /some/path/jcr：content， /some/other/path/jcr：content

AEM中的每個節點都必須有唯一的uuid。 此錯誤指出正在內嵌的節點與目的地執行個體不同路徑的其他位置所具有的uuid相同。
如果在擷取和後續作業之間在來源上移動節點，便會發生此情況 [追加提取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process).
如果目的地上的節點在擷取與後續追加擷取之間移動，也可能會發生這種情況。

此衝突必須手動解決。 熟悉內容的人必須決定必須刪除兩個節點中的哪一個，同時留意參考該內容的其他內容。 解決方案可能要求再次執行追加擷取，而不需要違反規定的節點。

### 由於無法刪除參照的節點，追加擷取失敗

另一個常見原因 [追加擷取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) 失敗是目的地執行個體上特定節點的版本衝突。 若要識別此錯誤，請使用Cloud Acceleration Manager UI下載擷取記錄，並尋找類似以下的專案：
>java.lang.RuntimeException： org.apache.jackrabbit.oak.api.CommitFailedException： OakIntegrity0001：無法刪除參照的節點： 8a2289f4-b904-4bd0-8410-15e41e0976a8

如果目的地的節點在內嵌和後續內嵌之間被修改，就可能發生這種情況 **非擦去** 內嵌，使得已建立新版本。 如果在啟用「包含版本」的情況下擷取移轉集，則可能會發生衝突，因為目的地現在具有由版本記錄和其他內容參考的更新版本。 由於正在參考違規版本節點，擷取程式無法刪除該節點。

解決方案可能要求再次執行追加擷取，而不需要違反規定的節點。 或者，建立違規節點的小型移轉集，但停用「包含版本」。

最佳實務指示如果 **非擦去** 內嵌必須使用包含版本的移轉集執行（亦即以「包含版本」=true擷取），在移轉歷程完成之前，儘可能減少修改目的地上的內容至關重要。 否則，這些衝突可能會發生。


## 下一步 {#whats-next}

擷取成功後，AEM索引會自動開始。 另請參閱 [移轉內容後建立索引](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/indexing-content.md) 以取得詳細資訊。

完成將內容擷取到Cloud Service中後，您可以檢視每個步驟的記錄（擷取和擷取）並尋找錯誤。 另請參閱 [檢視移轉集記錄](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/viewing-logs.md) 以進一步瞭解。
