---
title: 使用內容轉移工具
description: 使用內容轉移工具
exl-id: a19b8424-33ab-488a-91b3-47f0d3c8abf5
source-git-commit: 5243efa12fdca7e2e2d6ab23b38e8d09c6ea4945
workflow-type: tm+mt
source-wordcount: '3199'
ht-degree: 35%

---

# 使用內容轉移工具 {#using-content-transfer-tool}

## 使用內容轉移工具的重要考量 {#pre-reqs}

請跟隨以下章節，了解執行「內容轉移工具」時的重要考量：

* 「內容轉移工具」的最低系統需求為 AEM 6.3 + 和 JAVA 8。如果您使用較低的AEM版本，您需要將內容存放庫升級至AEM 6.5，才能使用「內容轉移工具」。

* 必須在AEM環境上配置Java，以便啟動AEM的用戶可以執行`java`命令。

* 安裝1.3.0版時，建議解除安裝舊版「內容轉移工具」，因為工具的架構有重大變更。 使用1.3.0時，您也應建立新的移轉集，並對新移轉集重新執行提取和擷取。

* 「內容轉移工具」可搭配下列類型的資料存放區使用：檔案資料儲存、S3資料儲存、共用S3資料儲存和Azure Blob儲存資料儲存。

* 如果您使用&#x200B;*沙箱環境*，請確定您的環境為最新版本，並升級至最新版本。 如果您使用&#x200B;*生產環境*，則會自動更新。

* 若要使用「內容轉移工具」，您必須是來源例項的管理員使用者，且屬於要轉移內容的Cloud Service例項中的本機AEM **administrators**&#x200B;群組。 無權限的使用者將無法擷取能使用「內容轉移工具」的存取 Token。

* 如果啟用「在擷取&#x200B;**之前擦去雲端例項上的現有內容」選項，則會刪除整個現有存放庫並建立新存放庫，以將內容擷取至中。**&#x200B;這表示會重設所有設定，包括目標Cloud Service例項的權限。 對於新增至&#x200B;**administrators**&#x200B;群組的管理員使用者，也是如此。 必須將用戶重新添加到&#x200B;**administrators**&#x200B;組中，才能檢索CTT的訪問令牌。

* 存取權杖可能會在特定時段之後或Cloud Service環境升級後定期過期。 如果存取權杖已過期，您將無法連線至Cloud Service執行個體，因此您需要擷取新的存取權杖。 與現有移轉集相關聯的狀態圖示會變更為紅色雲端，當您將游標暫留在紅色雲端上時，會顯示訊息。

* 內容轉移工具(CTT)在將內容從來源例項轉移至目標例項之前，不會執行任何類型的內容分析。 例如，CTT不會在將內容擷取至發佈環境時，區分已發佈和未發佈的內容。 無論移轉集中指定什麼內容，都會擷取至選取的目標例項。 使用者能將移轉集內嵌至製作例項、發佈例項或兩者。 建議將內容移至生產執行個體時，應在來源製作執行個體上安裝CTT，以將內容移至目標製作執行個體，同樣地，請在來源發佈執行個體上安裝CTT，將內容移至目標發佈執行個體。 如需詳細資訊，請參閱在發佈執行個體](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#running-ctt-on-publish)上執行內容轉移工具。[

* 「內容轉移工具」轉移的「使用者」和「群組」只是內容滿足權限所需的使用者和群組。 *提取*&#x200B;程式將整個`/home`複製到遷移集中，而&#x200B;*獲取*&#x200B;程式複製遷移內容ACL中引用的所有用戶和組。 若要自動將現有使用者和群組對應至其IMS ID，請參閱[使用使用者對應工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration)。

* 在提取階段中，「內容轉移工具」會在作用中的 AEM 來源例項上執行。

* 完成內容傳輸程式的&#x200B;*提取*&#x200B;階段之後，以及開始&#x200B;*擷取階段*&#x200B;將內容內嵌至您的AEMas a Cloud Service *階段*&#x200B;或&#x200B;*生產*&#x200B;例項之前，您需要記錄支援票證，以通知Adobe有意執行&#x200B;*擷取*，讓Adobe可確保在&#x200B;*擷取*&#x200B;過程期間不會發生中斷。 您需要在計畫的&#x200B;*擷取*&#x200B;日期前1週記錄支援票證。 一旦您提交了支援票證，支援團隊就會提供後續步驟的指引。 您可以記錄支援票證，並提供下列詳細資訊：

   * 計劃開始&#x200B;*擷取*&#x200B;階段時，確切的日期和估計時間（搭配您的時區）。
   * 您打算將資料內嵌至的環境類型（預備或生產）。
   * 方案ID。

* 製作的&#x200B;*擷取階段*&#x200B;會縮小整個製作部署。 這表示在整段擷取程序中，將無法使用製作 AEM。另外，請確定在您執行&#x200B;*擷取*&#x200B;階段時，不會執行任何Cloud Manager管道。

* 將`Amazon S3`或`Azure`用作源AEM系統上的資料儲存時，應配置資料儲存，以便無法刪除儲存的Blob（垃圾收集）。 這樣可確保索引資料的完整性，並且如果未能配置此方式，則可能由於此索引資料的完整性不完整而導致提取失敗。

* 如果您使用自訂索引，則在執行「內容轉移工具」之前，必須確保以`tika`節點配置自訂索引。 有關詳細資訊，請參閱[準備新索引定義](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#preparing-the-new-index-definition)。

* 如果您要追加提取，則必須不要變更現有內容的內容結構，從進行初始提取到執行追加提取的時間皆然。 自初始擷取後，無法對結構已變更的內容執行追加。 請務必在移轉程式期間加以限制。

* 如果您要將版本納入移轉集，並要使用`wipe=false`執行追加，則必須由於「內容轉移工具」中的目前限制而停用版本清除。 如果您偏好保持版本清除已啟用，並在遷移集中執行追加，則必須以`wipe=true`的形式執行擷取。

## 可用性 {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_download"
>title="下載"
>abstract="您可以從軟體發佈入口網站下載「內容轉移工具」的ZIP檔案。 您可以透過「封裝管理程式」，在來源 Adobe Experience Manager AEM) 例項上安裝封裝。請務必下載最新版本。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html" text="發行說明"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html" text="Software Distribution入口網站"

您可以從軟體發佈入口網站下載「內容轉移工具」的ZIP檔案。 您可以透過「封裝管理程式」，在來源 Adobe Experience Manager AEM) 例項上安裝封裝。請務必下載最新版本。 如需最新版本的詳細資訊，請參閱[發行說明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=zh-Hant)。

>[!NOTE]
>從[軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)入口網站下載內容轉移工具。

## 執行「內容轉移工具」  {#running-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_demo"
>title="執行內容轉移工具"
>abstract="了解如何使用「內容轉移工具」將內容移轉至AEMas a Cloud Service（製作/發佈）。"
>additional-url="https://video.tv.adobe.com/v/35460/?quality=12&amp;learn=on" text=" 請參閱示範"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration" text="教學課程 — 使用內容轉移工具"

>[!VIDEO](https://video.tv.adobe.com/v/35460/?quality=12&learn=on)


請依照以下章節了解如何使用「內容轉移工具」，將內容移轉至 AEM as a Cloud Service (製作/發佈)：

1. 選取Adobe Experience Manager並導覽至工具 — > **操作** -> **內容移轉**。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt01.png)

1. 從&#x200B;**內容遷移**&#x200B;嚮導中選擇&#x200B;**內容轉移**&#x200B;選項。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt02.png)


1. 建立第一個移轉集時，會顯示下列主控台。 按一下&#x200B;**建立移轉集**&#x200B;以建立新的移轉集。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt03.png)

   >[!NOTE]
   >如果您有現有的移轉集，主控台會顯示現有移轉集清單及其目前狀態。


1. 按照下面所述，填入&#x200B;**建立移轉集**&#x200B;畫面中的欄位。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt04.png)

   1. **名稱**：輸入移轉集名稱。
      >[!NOTE]
      >移轉集名稱不允許使用特殊字元。

   1. **Cloud Service 設定**：輸入目標 AEM as a Cloud Service 製作 URL。

      >[!NOTE]
      >在內容轉移活動期間，您一次最多可以建立並維護10個移轉集。
      >此外，您還須針對每個特定環境 (*預備*、*開發*&#x200B;或&#x200B;*生產*) 分別建立移轉。

   1. **存取 Token**：輸入存取 Token。

      >[!NOTE]
      >您可以使用&#x200B;**開啟存取權杖**&#x200B;按鈕來擷取存取權杖。 您必須確保您屬於目標Cloud Service例項中的AEM管理員群組。

   1. **參數**：選取以下參數以建立移轉集：

      1. **包含版本**：視需要選取。包含版本時，會自動包含路徑`/var/audit`以遷移審核事件。

      ![影像](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt05.png)

      >[!NOTE]
      >如果您要將版本納入移轉集，並要使用`wipe=false`執行追加，則必須由於「內容轉移工具」中的目前限制而停用版本清除。 如果您偏好保持版本清除已啟用，並在遷移集中執行追加，則必須以`wipe=true`的形式執行擷取。

      1. **包含來自IMS使用者和群組的對應**:選取要包含IMS使用者和群組對應的選項。如需詳細資訊，請參閱[使用者對應工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html) 。

      1. **欲包含的路徑**：使用路徑瀏覽器來選取需要移轉的路徑。路徑選擇器通過鍵入或選擇接受輸入。

         >[!IMPORTANT]
         >建立移轉集時會限制下列路徑：
         >* `/apps`
         >* `/libs`
         >* `/home`
         >* `/etc` (在 `/etc` CTT中允許選取某些路徑)




1. 填入&#x200B;**建立移轉集**&#x200B;詳細資訊畫面中的所有欄位後，按一下「**儲存**」。

1. 您將在&#x200B;**內容轉移**&#x200B;精靈中檢視移轉集，如下圖所示。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/04-item-selection-and-quick-actions.png)

   所有現有遷移集都顯示在&#x200B;**內容轉移**&#x200B;嚮導中，並顯示其當前狀態和狀態資訊。 您可能會看到以下說明的其中一些圖示。

   * *紅色雲朵*&#x200B;表示您無法完成提取程序。
   * *green cloud*&#x200B;表示您可以完成提取程式。
   * *黃色圖示*&#x200B;表示您並未建立現有移轉集，且該特定移轉集是由相同例項中的其他使用者所建立。

1. 選擇遷移集，然後按一下&#x200B;**屬性**&#x200B;以查看或編輯遷移集屬性。 編輯屬性時，無法變更&#x200B;**移轉集名稱**&#x200B;或&#x200B;**服務URL**。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt06.png)


### 內容轉移中的提取程序 {#extraction-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction"
>title="內容擷取"
>abstract="提取是指從來源AEM例項擷取內容，放入名為移轉集的暫存區域。 移轉集是 Adobe 提供的雲端儲存空間，可供暫時儲存在來源 AEM 例項與雲端服務 AEM 例項間轉移的內容。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-extraction-process" text="追加提取"

請依照下列步驟，從「內容轉移工具」中提取您的移轉集：
>[!NOTE]
>如果使用Amazon S3或Azure資料存放區作為資料存放區類型，您可以執行選用的預複製步驟，大幅加速提取階段。 若要執行此操作，您必須先設定`azcopy.config`檔案，才能執行擷取。 如需詳細資訊，請參閱[處理大型內容存放庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) 。

1. 從&#x200B;*「綜覽」*&#x200B;頁面選取一個移轉集，然後按一下&#x200B;**提取**&#x200B;即可開始提取。顯示&#x200B;**遷移集提取**&#x200B;對話框，然後按一下&#x200B;**提取**&#x200B;以啟動提取階段。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/06-content-extraction.png)

   >[!NOTE]
   >您可以選擇在提取階段中覆寫預備容器。


1. **EXTRACTION**&#x200B;欄位現在會顯示&#x200B;**RUNNING**&#x200B;狀態，以指出正在進行擷取。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/07-extraction-job-running.png)

   提取一旦完成，移轉集的狀態會更新為&#x200B;**已完成**，而&#x200B;**資訊**&#x200B;欄位下會顯示一個&#x200B;*實心綠色*&#x200B;的雲朵圖示。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/10-extraction-complete.png)

   >[!NOTE]
   >UI具有自動重新載入功能，每30秒重新載入一次概觀頁面。
   >提取階段開始時將建立寫入鎖定，並在 *60 秒*&#x200B;後釋放。因此，如果提取停止，則需等待一分鐘才能釋放鎖定並重新開始提取。

#### 追加提取 {#top-up-extraction-process}

「內容轉移工具」具備支援追加差異內容的功能，可以只轉移在上一次內容轉移活動後所進行的變更。

>[!NOTE]
>初始轉移內容後，建議您先頻繁地執行追加差異內容，以縮短最終差異化內容轉移的內容凍結時間，然後再於雲端服務上線。
>此外，必須不要將現有內容的內容結構從採取初始擷取時變更為執行追加擷取時。 自初始擷取後，無法對結構已變更的內容執行追加。 請務必在移轉程式期間加以限制。

提取程序一旦完成，您即可使用追加提取方法來轉移差異內容。請遵循下列步驟：

1. 導覽至&#x200B;*綜覽*&#x200B;頁面，並選取您要執行追加提取的移轉集。按一下&#x200B;**提取**&#x200B;即可開始追加提取。**移轉集提取**&#x200B;對話框隨即顯示。

   >[!IMPORTANT]
   >
   >您必須停用&#x200B;**在提取期間覆寫預備容器**&#x200B;選項。
   >
   >![影像](/help/move-to-cloud-service/content-transfer-tool/assets/11-topup-extraction.png)

### 內容轉移中的擷取程序 {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="內容擷取"
>abstract="擷取是指從移轉集擷取內容，並放入目標Cloud Service例項。 「內容轉移工具」具備支援追加差異內容的功能，可以只轉移在上一次內容轉移活動後所進行的變更。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-ingestion-process" text="追加擷取"

請依照下列步驟，從「內容轉移工具」中擷取您的移轉集：
>[!NOTE]
>如果使用Amazon S3或Azure資料存放區作為資料存放區類型，您可以執行選用的預複製步驟，大幅加快擷取階段。 有關詳細資訊，請參閱[使用AzCopy擷取](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#ingesting-azcopy) 。

1. 從&#x200B;*概述*&#x200B;頁面中選取移轉集，然後按一下&#x200B;**擷取**&#x200B;以開始擷取。 **移轉集擷取**&#x200B;對話框隨即顯示。一次可將內容擷取至製作例項或發佈例項。 選取要擷取內容的例項。 按一下&#x200B;**擷取**&#x200B;以開始擷取階段。

   >[!IMPORTANT]
   >如果使用預復本擷取（適用於S3或Azure資料存放區），建議您先單獨執行製作擷取。 這會在稍後執行時加速發佈擷取。

   >[!IMPORTANT]
   >啟用「在擷取&#x200B;**之前擦去雲端例項上的現有內容」選項時，它會刪除整個現有存放庫，並建立新存放庫以將內容擷取至中。**&#x200B;這表示會重設所有設定，包括目標Cloud Service例項的權限。 對於新增至&#x200B;**administrators**&#x200B;群組的管理員使用者，也是如此。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/content-ingestion-03.png)

   此外，按一下&#x200B;**客戶服務**&#x200B;來記錄票證，如上圖所示。 另請參閱[使用內容轉移工具的重要考量](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#pre-reqs)以深入了解。

1. 擷取完成後，狀態會更新為&#x200B;**FINISHED**。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/15-ingestion-complete.png)

#### 追加擷取 {#top-up-ingestion-process}

「內容轉移工具」具備支援&#x200B;*追加*&#x200B;差異內容的功能，可以只轉移在上一次內容轉移活動後所進行的變更。

>[!NOTE]
>
>初始轉移內容後，建議您先頻繁地執行追加差異內容，以縮短最終差異化內容轉移的內容凍結時間，然後再於雲端服務上線。

擷取程序一旦完成，您即可使用追加擷取方法來轉移差異內容。請遵循下列步驟：

1. 導覽至&#x200B;*綜覽*&#x200B;頁面，並選取您要執行追加擷取的移轉集。按一下&#x200B;**擷取**&#x200B;即可開始追加提取。**移轉集擷取**&#x200B;對話框隨即顯示。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/content-ingestion-02.png)

   >[!IMPORTANT]
   >您應停用「擷取&#x200B;**之前擦去雲端例項上的現有內容」選項，以防止從先前的擷取活動中刪除現有內容。**&#x200B;此外，按一下&#x200B;**客戶服務**&#x200B;來記錄票證，如上圖所示。


### 檢視移轉集記錄 {#viewing-logs-migration-set}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_logs"
>title="檢視記錄"
>abstract="擷取擷取完成後，檢查記錄中是否有任何錯誤/警告。 您應處理所回報的問題，或聯絡Adobe支援，以立即解決任何錯誤。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#troubleshooting" text="疑難排解"
>additional-url="https://helpx.adobe.com/ca/enterprise/admin-guide.html/ca/enterprise/using/support-for-experience-cloud.ug.html" text="聯絡Adobe支援"

完成每個步驟（擷取和擷取）後，請檢查記錄並尋找錯誤。  您應處理所回報的問題，或聯絡Adobe支援，以立即解決任何錯誤。

您可以在&#x200B;*綜覽*頁面中檢視現有移轉集記錄。
請遵循下列步驟：

1. 導覽至&#x200B;*綜覽*&#x200B;頁面，並選取您要刪除的移轉集，然後按一下動作列中的&#x200B;**檢視記錄**。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/view-log1.png)

1. **記錄**&#x200B;對話框隨即顯示。按一下&#x200B;**提取記錄**，即可在新索引標籤中檢視記錄。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/view-log2.png)
或者，

   您也可以在&#x200B;*綜覽*&#x200B;畫面中檢視移轉集記錄。請選取移轉集，然後按一下&#x200B;**提取**&#x200B;欄位下的狀態。在這個情況下，按一下&#x200B;**已完成**&#x200B;即可在新索引標籤中檢視記錄。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/view-log3.png)

1. 若要追蹤記錄而不使用使用者介面，您可以透過 SSH 連線至來源 AEM 環境，並追蹤 `crx-quickstart/cloud-migration/extraction-XXXXX/output.log file`。

### 刪除移轉集 {#deleting-migration-set}

您可以在&#x200B;*綜覽頁面*中刪除移轉集。
請遵循下列步驟：

1. 導覽至&#x200B;*綜覽*&#x200B;頁面，並選取您要刪除的移轉集，然後按一下動作列中的&#x200B;**刪除**。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/delete-1.png)

1. 在&#x200B;**刪除移轉集**&#x200B;對話框中按一下&#x200B;**刪除**&#x200B;以確認刪除。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/delete-3.png)


## 在發佈執行個體上執行內容轉移工具 {#running-ctt-on-publish}

建議將內容移至發佈例項時，應在來源發佈例項上安裝CTT，以將內容移至目標發佈例項。 請遵循以下說明的建議方法：

* 使用與Author例項上所使用的CTT相同版本。

* 只需移轉單一發佈節點。 在開始提取之前，應從負載平衡器中移除它。

* 建立移轉集時，請使用製作AEMaaCS環境的URL。

* 擷取至發佈期間，發佈層級不會縮小（與作者不同）。 為了防患於未然，請避免任何用戶啟動的寫入操作，例如：

   * 從AEMaaCS製作到在該環境中發佈的內容發佈
   * 發佈執行個體之間的使用者同步


## 疑難排解 {#troubleshooting}

### 遺失 Blob ID {#missing-blobs}

如有回報指出遺失 Blob ID (如下所述)，則需要在現有存放庫中執行一致性檢查，並還原遺失的 Blob。
`ERROR o.a.j.o.p.b.AbstractSharedCachingDataStore - Error retrieving record [ba45c53f8b687e7056c85dceebf8156a0e6abc7e]`

以下命令將會執行

>[!NOTE]
>
>如果要回報引用 Blob 的節點路徑，則須使用 `--verbose` 旗標。

**存放庫 AEM 6.5 (Oak 1.8 及以下的版本)**

```shell
java -jar oak-run.jar datastorecheck --consistency --store [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds] <DATASTORE_CFG> --verbose <OUT_DIR> --dump
```

**具有 Oak > 1.10 的存放庫**

```shell
java -jar oak-run.jar datastore --check-consistency [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds|azureds] <DATASTORE_CFG> --out-dir <OUT_DIR> --work-dir <TEMP_DIR> --verbose
```

如需詳細資訊，請參考 [Oak Runnable Jar](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run)。

接著，即可針對上述在 *OUT_DIR* 中建立、有一致性問題的檔案，檢查是否有路徑遺失二進位檔案，以及是否有採取適當操作如透過備份還原、刪除路徑、重新索引等等。


### UI 行為 {#ui-behavior}

身為使用者，您可能會在「內容轉移工具」的使用者介面 (UI) 中看到下列行為變更：

* 「內容轉移工具」UI 中的圖示可能與本指南中顯示的螢幕擷圖不同，也可能完全不顯示 (取決於來源 AEM 例項的版本)。
