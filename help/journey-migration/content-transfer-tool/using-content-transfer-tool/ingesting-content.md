---
title: 將內容引入雲端服務
description: 瞭解如何使用Cloud Acceleration Manager將移轉集中的內容擷取至目標Cloud Service例項。
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
feature: Migration
role: Admin
source-git-commit: 2fafb582ae8fc5e2ecc19157ff34e16be401393a
workflow-type: tm+mt
source-wordcount: '3591'
ht-degree: 12%

---

# 將內容引入雲端服務 {#ingesting-content}

## Cloud Acceleration Manager 中的摘取程序 {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="內容攝入"
>abstract="攝入是指將移轉集中的內容攝入到目標 Cloud Service 執行個體中。「內容轉移工具」具備支援追加差異內容的功能，可以只轉移在上一次內容轉移活動後所進行的變更。"
>additional-url="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content#top-up-extraction-process" text="填滿提取"

請依照下列步驟，使用Cloud Acceleration Manager擷取您的移轉集：

1. 前往Cloud Acceleration Manager。 按一下您的專案卡，然後按一下「內容轉移」卡。 導覽至&#x200B;**擷取工作**，然後按一下&#x200B;**新增擷取**

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. 檢閱擷取檢查清單，並確保完成所有步驟。 若要確保成功擷取，這些步驟是必要的。 只有在檢查清單完成時，才繼續進行&#x200B;**下一步**&#x200B;步驟。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/Ingestion-checklist.png)

1. 提供建立內嵌所需的資訊。

   * **移轉集：**&#x200B;選取包含擷取資料的移轉集作為Source。
      * 移轉集將在長時間不活動後過期，因此預期擷取會在執行擷取後不久進行。 檢閱[移轉集到期日](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry)以取得詳細資料。

   >[!TIP]
   > 如果擷取正在執行，對話方塊將會指出它。 擷取一旦成功完成，就會自動開始內嵌。 如果擷取失敗或停止，擷取工作將會撤銷。

   * **目的地：**&#x200B;選取目的地環境。 此環境是擷取移轉集內容的地方。
      * 內嵌不支援快速開發環境(RDE)或預覽型別的目的地，並且即使使用者有權存取，也不會顯示為可能的目的地選擇。
      * 雖然移轉集可同時內嵌至多個目的地，但目的地一次只能是一個執行或等待內嵌的目標。

   * **層：**&#x200B;選取層。 （作者/發佈）。
      * 如果來源是`Author`，建議將其擷取到目標上的`Author`層。 同樣地，如果來源為`Publish`，目標也應為`Publish`。

   >[!NOTE]
   > 如果目標層是`Author`，則作者執行個體會在擷取期間關閉，且無法供使用者（例如，作者或執行維護的任何人）使用。 原因是為了保護系統，並防止任何可能遺失或導致擷取衝突的變更。 確保您的團隊知道這個事實。 另請注意，環境在作者擷取期間似乎處於休眠狀態。

   >[!NOTE]
   > 如果目標層是`Publish`，則發佈執行個體會在擷取期間繼續執行。  不過，如果擷取期間正在執行壓縮程式，則兩個程式之間可能會發生衝突。  因此，擷取程式1)會停用壓縮計時指令碼，以便在擷取期間不會開始壓縮，而2)會檢查壓縮目前是否正在執行，如果正在執行，則會等待壓縮完成後再繼續擷取。  如果發佈擷取所花的時間比預期長，請檢查擷取記錄檔中的相關記錄陳述式。

   * **擦除：**&#x200B;選擇`Wipe`值
      * **擦去**&#x200B;選項會設定目的地的擷取起點。 如果啟用&#x200B;**擦去**，包含其所有內容的目的地會重設為Cloud Manager中指定的AEM版本。 如果未啟用，目的地會維持目前內容為起點。
      * 此選項&#x200B;**不**&#x200B;會影響內容擷取的執行方式。 擷取一律使用內容取代策略，而&#x200B;_不是_&#x200B;內容合併策略，因此在&#x200B;**擦除**&#x200B;和&#x200B;**非擦除**&#x200B;的情況下，擷取移轉集將會覆寫目的地上相同路徑中的內容。 例如，如果移轉集包含`/content/page1`，而目的地已包含`/content/page1/product1`，則內嵌會移除整個`page1`路徑及其子頁面，包括`product1`，並將其取代為移轉集中的內容。 這表示在執行&#x200B;**非擦去**&#x200B;擷取至包含任何應維護之內容的目的地時，必須仔細規劃。
      * 非擦去擷取是專為追加擷取使用案例而設計。 這些內嵌專案旨在遞增數量的新內容，這些內容自現有移轉集中最後一次內嵌以來已變更。 若在此使用案例之外執行非擦去擷取，可能會導致擷取時間非常長。

   >[!IMPORTANT]
   > 如果已為內嵌啟用設定&#x200B;**擦去**，則會重設整個現有的存放庫，包括目標Cloud Service執行個體的使用者許可權。 此重設對於新增到&#x200B;**管理員**&#x200B;群組的管理員使用者也是true，必須將該使用者再次新增到管理員群組才能開始內嵌。

   * **預先複製：**&#x200B;選擇`Pre-copy`值
      * 您可以執行選用的預先複製步驟，大幅加快內嵌速度。 如需詳細資訊，請參閱[使用AzCopy擷取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy)。
      * 如果使用預先複製擷取（用於S3或Azure資料存放區），建議先單獨執行`Author`擷取。 如此可加快`Publish`擷取稍後執行的速度。

   >[!IMPORTANT]
   > 您必須屬於目的地Cloud Service作者服務上的本機&#x200B;**AEM管理員**&#x200B;群組，才能起始內嵌至目的地環境。 如果您無法開始內嵌，請參閱[無法開始內嵌](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#unable-to-start-ingestion)以取得詳細資料。

1. 選取擷取選擇後，便會顯示預估持續時間。 這是根據類似擷取之歷史資料盡力估計的結果。

   * 系統不會針對&#x200B;**非擦去**&#x200B;擷取計算或顯示此預估值，因為在此情況下，CAM不知道目標系統上有多少內容。
   * 只有在擷取的「檢查大小」值已收集到並且可供使用時，才會計算並顯示此預估值。
   * 此值是預估值，雖然計算方式很聰明，但不應視為精確。 不同的因素可能會改變實際持續時間。
   * 在執行內嵌期間，此值也會在期間對話方塊中提供，該對話方塊可透過內嵌的&quot;**檢視期間**&quot;動作存取。

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_estimate"
>title="攝入持續時間估計"
>abstract="可以顯示特定攝入的大致持續時間，讓您大概了解攝入需要使用多長時間。其準確性有所限制。"

![影像](/help/journey-migration/content-transfer-tool/assets/estimate.png)

1. 按一下&#x200B;**擷取**。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam22.png)

1. 然後，您可以從「內嵌工作」清單檢視中監視內嵌，並使用內嵌的動作功能表來檢視持續時間並記錄內嵌進度。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23.png)

1. 按一下列中的&#x200B;**(i)**&#x200B;按鈕，以取得擷取工作的詳細資訊。 您可以按一下&#x200B;**...**，然後按一下&#x200B;**檢視期間**，以檢視擷取每個步驟的執行或完成期間。 擷取的資訊也會顯示出來，以瞭解正在擷取的內容。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23b.png)

## 填滿攝入 {#top-up-ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_topup"
>title="填滿攝入"
>abstract="使用填滿功能來移動自上次內容轉移活動以來修改的內容。攝入完成後，檢查記錄檔中是否有任何錯誤或警告。如有任何錯誤應立即處理，方法是處理回報的問題或聯絡 Adobe 客戶服務。"
>additional-url="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs" text="檢視記錄檔"

「內容轉移工具」具備可透過執行移轉集的&#x200B;*追加*&#x200B;來擷取差異內容的功能。 如此可修改移轉集，使其僅包含自上次擷取以來已變更的內容，而無須再次擷取所有內容。

>[!NOTE]
>初始轉移內容後，建議您先頻繁地執行追加差異內容，以縮短最終差異化內容轉移的內容凍結時間，然後再於Cloud Service上線。 如果您在第一次擷取使用了預先複製步驟，您可以略過後續追加擷取的預先複製（如果追加移轉集大小小於200 GB）。 原因是它可能會為整個程式增加時間。

若要在部分擷取完成後擷取差異內容，您必須執行[追加擷取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)，然後使用具有&#x200B;**擦去**&#x200B;選項&#x200B;**停用的擷取方法**。 請務必閱讀上述&#x200B;**擦去**&#x200B;說明，以避免遺失目的地上的內容。

從建立內嵌工作開始，並確定在內嵌期間已停用&#x200B;**擦去**，如下所示：

![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam24.png)

## 疑難排解 {#troubleshooting}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_troubleshooting"
>title="內容攝取故障排除"
>abstract="請參閱攝入記錄和文件，了解攝入失敗的常見原因，並尋找修正問題的解決方案。修正之後，就可以再次執行攝入。"
>additional-url="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers" text="驗證內容轉移"

### CAM無法擷取移轉權杖 {#cam-unable-to-retrieve-the-migration-token}

自動擷取移轉權杖可能會因為其他原因而失敗，包括您[在目標Cloud Service環境中透過Cloud Manager](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)設定IP允許清單。 在這種情況下，當您嘗試開始內嵌時，會看到下列對話方塊：

![影像](/help/journey-migration/content-transfer-tool/assets-ctt/troubleshooting-token.png)

按一下對話方塊上的「取得權杖」連結，手動擷取移轉權杖。 另一個標籤會開啟，顯示Token。 然後，您可以複製權杖並將其貼到&#x200B;**移轉權杖輸入**&#x200B;欄位。 現在，您應該能夠開始內嵌。

>[!NOTE]
>
>此權杖可供屬於目的地Cloud Service作者服務上本機&#x200B;**AEM管理員**&#x200B;群組的使用者使用。

### 無法開始內嵌 {#unable-to-start-ingestion}

您必須屬於目的地Cloud Service作者服務上的本機&#x200B;**AEM管理員**&#x200B;群組，才能起始內嵌至目的地環境。 如果您不屬於AEM管理員群組，當您嘗試開始內嵌時，會看到如下所示的錯誤。 您可以要求您的管理員將您新增至本機&#x200B;**AEM管理員**，或要求權杖本身，然後您可以將權杖貼到&#x200B;**移轉權杖輸入**&#x200B;欄位。

![影像](/help/journey-migration/content-transfer-tool/assets-ctt/error_nonadmin_ingestion.png)

### 無法連線至移轉服務 {#unable-to-reach-migration-service}

請求內嵌後，可能會向使用者顯示類似以下訊息：「無法聯絡目標環境上的移轉服務。 若是如此，請稍後再試或聯絡Adobe支援人員。」

![影像](/help/journey-migration/content-transfer-tool/assets-ctt/error_cannot_reach_migser.png)

此訊息指出Cloud Acceleration Manager無法連線到目標環境的移轉服務來開始內嵌。 發生此狀況可能有各種原因。

>[!NOTE]
> 
> 顯示「移轉權杖」欄位，因為在少數情況下，實際上不允許擷取該權杖。 透過允許手動提供，這可讓使用者無需任何其他協助即可快速開始內嵌。 如果提供Token，但訊息仍顯示，則擷取Token並非問題。

* AEM as a Cloud Service會維護環境狀態，而且偶爾會因為各種正常原因而重新啟動移轉服務。 如果服務正在重新啟動，則無法連線到該服務，但最終會提供該服務。
* 執行個體上可能正在執行另一個處理序。 例如，如果[AEM版本更新](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates)正在套用更新，則系統可能忙碌中，且移轉服務定期無法使用。 完成該程式後，可以再次嘗試開始內嵌。
* 如果已透過Cloud Manager套用[IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)，它會封鎖Cloud Acceleration Manager以停止連線至移轉服務。 無法新增用於內嵌的IP位址，因為其位址是動態的。 目前，唯一的解決方案是在擷取和索引過程中停用IP允許清單，方法是在擷取和索引過程執行時暫時將0.0.0.0/0新增到允許清單。
* 可能有其他原因需要調查。 如果內嵌或索引繼續失敗，請聯絡Adobe客戶服務。

### AEM版本更新與擷取 {#aem-version-updates-and-ingestions}

[AEM版本更新](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates)會自動套用至環境，以使其與最新的AEM as a Cloud Service版本保持一致。 如果在執行內嵌時觸發更新，可能會導致無法預測的結果，包括環境損毀。

如果「AEM版本更新」已上線到目的地程式，則擷取程式會嘗試在開始前停用其佇列。 擷取完成時，版本更新程式狀態會傳回至擷取開始前的狀態。

>[!NOTE]
>
> 您不再需要記錄支援票證來停用「AEM版本更新」。

如果「AEM版本更新」作用中（也就是說，更新正在執行或排入佇列等待執行），內嵌將不會開始，且使用者介面會顯示下列訊息。 更新完成後，即可開始內嵌。 Cloud Manager可用來檢視方案管道的目前狀態。

>[!NOTE]
>
> 「AEM版本更新」會在環境的管道中執行，並等候管道清除。 如果更新排入佇列的時間比預期長，請確保自訂工作流程不會無意中鎖定管道。

![影像](/help/journey-migration/content-transfer-tool/assets-ctt/error_releaseorchestrator_active.png)

### 雲端環境處於未就緒狀態而導致擷取失敗 {#ingestion-failure-due-to-cloud-environment-not-in-ready-state}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_cloud_environment_not_in_ready_state"
>title="雲端環境處於未就緒狀態"
>abstract="在極少數的情況下，目標雲端環境可能會遇到非預期的問題而導致擷取失敗。"

在罕見的情況下，內嵌的目標Cloud Service環境可能會遇到未預期的問題。 因此，內嵌將失敗，因為環境未處於預期的就緒狀態。 檢查內嵌記錄檔，以顯示所遇到錯誤狀態的更多詳細資料。

請確保製作環境可用，並等候幾分鐘再重新嘗試內嵌。 如果問題仍然存在，請聯絡客戶支援並遇到錯誤狀態。

### 由於違反唯一條件限制而導致填滿擷取失敗 {#top-up-ingestion-failure-due-to-uniqueness-constraint-violation}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_uuid"
>title="違反唯一條件限制"
>abstract="非擦除擷取失敗的常見原因是節點 ID 衝突。只能存在一個衝突節點。"
>additional-url="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content#top-up-ingestion-process" text="填滿擷取"

[追加擷取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process)失敗的常見原因是節點ID發生衝突。 若要識別此錯誤，請使用Cloud Acceleration Manager UI下載擷取記錄，並尋找類似以下的專案：

>java.lang.RuntimeException： org.apache.jackrabbit.oak.api.CommitFailedException： OakConstraint0030：唯一性條件約束違反了屬性[jcr:uuid]，其值為a1a1a1-b2b2-c3c3-d4d4-e5e5e5e5e5： /some/path/jcr:content、 /some/other/path/jcr:content

AEM中的每個節點都必須有一個唯一的uuid。 此錯誤指出正在擷取的節點與目的地執行個體上不同路徑中存在的節點具有相同的uuid。 發生此狀況有兩個原因：

* 節點在來源上從擷取到後續[追加擷取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)之間移動
   * _記住_：對於追加擷取，即使節點不再存在於來源上，仍會存在於移轉集中。
* 目的地上的節點會在擷取與後續追加擷取之間移動。

此衝突必須手動解決。 熟悉內容的人必須決定必須刪除兩個節點中的哪一個，同時留意參考該內容的其他內容。 解決方案可能要求再次執行追加擷取，而不需要違反規定的節點。

### 無法刪除引用節點而導致填滿擷取失敗 {#top-up-ingestion-failure-due-to-unable-to-delete-referenced-node}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_referenced_node"
>title="無法刪除引用的節點"
>abstract="非擦除擷取失敗的常見原因是目標實例上特定節點的版本衝突。必須修復節點的版本。"
>additional-url="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content#top-up-ingestion-process" text="填滿擷取"

[追加擷取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process)失敗的另一個常見原因是目的地執行個體上特定節點的版本衝突。 若要識別此錯誤，請使用Cloud Acceleration Manager UI下載擷取記錄，並尋找類似以下的專案：

>java.lang.RuntimeException： org.apache.jackrabbit.oak.api.CommitFailedException： OakIntegrity0001：無法刪除參照的節點： 8a2289f4-b904-4bd0-8410-15e41e0976a8

如果目的地的節點在內嵌與後續&#x200B;**非擦去**&#x200B;內嵌之間被修改，以致已建立新版本，就可能發生這種情況。 如果在啟用「包含版本」的情況下擷取移轉集，則可能會發生衝突，因為目的地現在具有由版本記錄和其他內容參考的更新版本。 由於違規版本節點被引用，擷取程式無法刪除該節點。

解決方案可能要求再次執行追加擷取，而不需要違反規定的節點。 或者，建立違規節點的小型移轉集，但停用「包含版本」。

最佳實務指出，如果必須使用包含版本的移轉集來執行&#x200B;**非擦去**&#x200B;內嵌，請務必儘可能減少修改目的地上的內容，直到移轉歷程完成為止。 否則，這些衝突可能會發生。

### 由於節點屬性值過大而導致擷取失敗 {#ingestion-failure-due-to-large-node-property-values}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_bson"
>title="大節點屬性"
>abstract="擷取失敗的常見原因是超過節點屬性值的大小上限。請遵依文件 (包括與 BPA 報告相關的文件) 說明來修復這種情況。"
>additional-url="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool" text="移轉先決條件"

儲存在MongoDB中的節點屬性值不能超過16 MB。 如果節點值超過支援的大小，擷取會失敗，且記錄會包含：

* `BSONObjectTooLarge`錯誤並指定哪個節點超過最大值，或
* `BsonMaximumSizeExceededException`錯誤，表示節點可能包含超過大小上限**的unicode字元

這是MongoDB限制。

請參閱`Node property value in MongoDB`內容轉移工具必備條件[中的](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/prerequisites-content-transfer-tool.md)附註，以取得詳細資訊以及可協助尋找所有大型節點的Oak工具連結。 修正所有大型節點後，請再次執行擷取和擷取。

若要避免此限制，請在來源AEM執行個體上執行[Best Practices Analyzer](/help/journey-migration/best-practices-analyzer/using-best-practices-analyzer.md)，並檢閱它提供的發現，特別是[「不支援的存放庫結構」(URS)](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-pattern-detection/table-of-contents/urs)模式。

>[!NOTE]
>
>[Best Practices Analyzer](/help/journey-migration/best-practices-analyzer/using-best-practices-analyzer.md) 2.1.50+版會報告包含超過大小上限Unicode字元的大型節點。 請確定您執行的是最新版本。 2.1.50之前的BPA版本將無法識別並報告這些大型節點，而且您必須使用上述的先決條件Oak工具個別探索這些節點。

### 因預期外的間歇性錯誤導致擷取失敗 {#ingestion-failure-due-to-unexpected-intermittent-errors}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_intermittent_errors"
>title="預期外的間歇性錯誤"
>abstract="有時可能會發生預期外的間歇性下游服務錯誤，而不幸的是，唯一能做的處理方法就是重新嘗試一次擷取動作。"

有時，非預期的間歇性問題可能會導致擷取失敗，很遺憾，唯一的補救方法就是重試擷取。 調查擷取記錄以找出失敗的原因，並檢視它是否符合下面列出的任何錯誤，其中應嘗試重試。

#### MongoDB問題 {#mongo-db-issues}

* `Atlas prescale timeout error` — 擷取階段會嘗試預先縮放目標雲端資料庫，使其大小與正在擷取的移轉集內容大小相符。 少數情況下，此作業未在預期時間範圍內完成。
* `Exhausted mongo restore retries` — 嘗試將擷取的移轉集內容還原到雲端資料庫的本機傾印已經用盡。 這表示MongoDB的整體健康情況/網路問題，通常會在幾分鐘後自行解決。
* `Mongo network error` — 有時，建立與MongoDB的連線可能會失敗，導致擷取程式提早結束並回報為失敗。 應嘗試簡單的擷取重試。
* `Mongo server selection error` — 這是罕見的Mongo使用者端逾時錯誤，可能會因為許多基礎原因而發生。 後續重試將很可能更正問題。

### 擷取已撤銷 {#ingestion-rescinded}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_rescinded"
>title="擷取已撤銷"
>abstract="擷取等待的摘取未成功完成。由於無法執行，擷取已被撤銷。"

使用執行中的擷取作為來源移轉集而建立的擷取會耐心等待，直到擷取成功，而且在那一刻會正常開始。 如果擷取失敗或停止，則擷取及其索引工作將不會開始，但會取消。 在這種情況下，請檢查擷取以確定失敗的原因，修正問題並重新開始擷取。 執行固定擷取後，即可排程新的內嵌。

### 等待的攝取無法開始 {#waiting-ingestion-not-started}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_waiting_ingestion_not_started"
>title="等待的攝取未開始"
>abstract="即使等待擷取完成，此攝取仍無法開始。"

使用執行中的擷取作為來源移轉集而建立的內嵌會等到擷取成功為止，而此時擷取會嘗試正常開始。 如果內嵌無法啟動，則會標示為失敗。 不啟動的可能原因包括：在目標製作環境中設定了IP允許清單；由於其他原因，目標環境無法使用。  在此情況下，請檢查擷取無法開始的原因、修正問題，然後再次開始擷取（不需要重新執行擷取）。

### 重新執行內嵌後已刪除的資產不存在

一般而言，不建議在內嵌之間修改雲端環境資料。

使用Assets觸控式UI從Cloud Service目的地刪除資產時，會刪除節點資料，但不會立即刪除包含影像的資產blob。 它會標示為刪除，因此不再出現在UI中；但是，它會保留在資料存放區中，直到發生記憶體回收並移除blob為止。

在先前移轉的資產被刪除，且下次內嵌是在記憶體回收行程完成刪除資產之前執行的情境中，內嵌相同的移轉集將不會還原已刪除的資產。 當內嵌檢查雲端環境上的資產時，沒有節點資料；因此，內嵌會將節點資料複製到雲端環境。 不過，在檢查blob存放區時，它會看到blob存在，並略過複製blob。 這就是為什麼中繼資料會在您從觸控式UI檢視資產時出現在擷取後，但影像卻沒有。 請記住，移轉集和內容擷取並非設計用於處理這種情況。 他們的目標是將新內容新增到雲端環境，而不是還原先前移轉的內容。

## 後續步驟 {#whats-next}

擷取成功後，AEM索引會自動開始。 如需詳細資訊，請參閱移轉內容後的[索引](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/indexing-content.md)。

完成將內容內嵌至Cloud Service後，您可以檢視每個步驟的記錄（擷取和內嵌）並尋找錯誤。 請參閱[檢視移轉集記錄](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/viewing-logs.md)以瞭解更多資訊。
