---
title: 使用內容轉移工具
description: 使用內容轉移工具
exl-id: a19b8424-33ab-488a-91b3-47f0d3c8abf5
source-git-commit: 04494e116fcdd38622ae2d4434d7cf8e4034d5aa
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 使用內容轉移工具 {#using-content-transfer-tool}

## 內容轉移中的提取程序 {#extraction-process}

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

### 追加提取 {#top-up-extraction-process}

「內容轉移工具」具備支援追加差異內容的功能，可以只轉移在上一次內容轉移活動後所進行的變更。

>[!NOTE]
>初始轉移內容後，建議您先頻繁地執行追加差異內容，以縮短最終差異化內容轉移的內容凍結時間，然後再於雲端服務上線。
>此外，必須不要將現有內容的內容結構從採取初始擷取時變更為執行追加擷取時。 自初始擷取後，結構已變更的內容無法執行追加。 請務必在移轉程式期間加以限制。

提取程序一旦完成，您即可使用追加提取方法來轉移差異內容。請遵循下列步驟：

1. 導覽至&#x200B;*綜覽*&#x200B;頁面，並選取您要執行追加提取的移轉集。按一下&#x200B;**提取**&#x200B;即可開始追加提取。**移轉集提取**&#x200B;對話框隨即顯示。

   >[!IMPORTANT]
   >
   >您必須停用&#x200B;**在提取期間覆寫預備容器**&#x200B;選項。
   >
   >![影像](/help/move-to-cloud-service/content-transfer-tool/assets/11-topup-extraction.png)

## 內容轉移中的擷取程序 {#ingestion-process}

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

### 追加擷取 {#top-up-ingestion-process}

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
