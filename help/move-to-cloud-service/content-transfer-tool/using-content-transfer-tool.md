---
title: 使用內容轉移工具
description: 使用內容轉移工具
translation-type: tm+mt
source-git-commit: f3a4fdf57dc84bba9811530fccb2fe6a4404376f
workflow-type: tm+mt
source-wordcount: '1902'
ht-degree: 70%

---


# 使用內容轉移工具 {#using-content-transfer-tool}

## 使用內容轉移工具的重要考量 {#pre-reqs}

請跟隨以下章節，了解執行「內容轉移工具」時的重要考量：

* 「內容轉移工具」的最低系統需求為 AEM 6.3 + 和 JAVA 8。如果您使用較舊版本的 AEM，您必須將內容存放庫升級至 AEM 6.5 才能使用「內容轉移工具」。

* Java必須在AEM環境上設定，如此， `java` 啟動AEM的使用者就可執行命令。

* 內容傳輸工具可與下列類型的資料儲存區搭配使用：檔案資料儲存、S3資料儲存、共用S3資料儲存和Azure Blob儲存資料儲存。

* 如果您使用沙盒環 *境*，請確定您的環境是最新的，並升級至最新的版本。 如果您使用&#x200B;*生產環境*，則會自動更新。

* 若要使用「內容傳輸工具」，您必須是來源例項的管理員使用者，且屬於您要傳輸內容至之Cloud服務例項中的本機AEM管理員群組。 無權限的使用者將無法擷取能使用「內容轉移工具」的存取 Token。

* 目前，AEM做為雲端服務作者例項的預設MongoDB大小為32GB。 建議您針對大於20GB的區段儲存區大小，提交支援票證以增加MongoDB大小。

* 內容傳輸工具所傳輸的使用者和群組僅是內容滿足權限所需的使用者和群組。 提取 *過程將整* 個複製到遷移集中， `/home` Ingestion ** 過程將複製遷移內容ACL中引用的所有用戶和組。

* 在提取階段中，「內容轉移工具」會在作用中的 AEM 來源例項上執行。

* 在完成內容傳輸程式的 *Extraction* phase以及開始 *Ing Phase* ，將內容以Cloud ServiceStageOr ******** ProductionInstances的形式傳入您的AEM之前，您需要記錄支援票證，以便Adobe將您的意向通知執行Adobe，以確保在Adobe Inging期間不會發生內容的CloudStageStStageSt問題處理。 您必須在計畫的接收日期前1週記錄支 *持票* 。 一旦您提交了支援票證，支援團隊將提供後續步驟的指導。
   * 使用下列詳細資訊記錄支援票證：
      * 您計劃開始擷取階段時，確切的日期和估計時間(與您的時 *區* )。
      * 您打算將資料收錄到的環境類型（「舞台」或「生產」）。
      * 程式ID。

* 製作的&#x200B;*擷取階段*&#x200B;將縮小整個製作部署。這表示在整段擷取程序中，將無法使用製作 AEM。此外，請確保在您運行接收階段時不執行Cloud Manager管 *道* 。


## 可用性 {#availability}

內容傳輸工具可從軟體散發入口網站下載為zip檔案。 您可以透過「封裝管理程式」，在來源 Adobe Experience Manager AEM) 例項上安裝封裝。請確定下載最新版本。 如需最新版本的詳細資訊，請參閱版 [本說明](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html)。

>[!NOTE]
>從[軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)入口網站下載內容轉移工具。

## 執行「內容轉移工具」 {#running-tool}

>[!VIDEO](https://video.tv.adobe.com/v/35460/?quality=12&learn=on)


請依照以下章節了解如何使用「內容轉移工具」，將內容移轉至 AEM as a Cloud Service (製作/發佈)：

1. 選擇 Adobe Experience Manager 並導覽至工具 -> **操作** -> **內容轉移**。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/content1.png)

1. 當您建立第一個移轉集時，會顯示下列主控台。 按一下&#x200B;**建立移轉集**&#x200B;以建立新的移轉集。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/01-migration-set-overview.png)

   >[!NOTE]
   >如果您有現有的移轉集，主控台將顯示現有移轉集的清單，其目前狀態為。

1. 請依照下方敘述，填入&#x200B;**內容移轉集詳細資訊**&#x200B;畫面中的欄位。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/02-migration-set-creation.png)


   1. **名稱**：輸入移轉集名稱。
      >[!NOTE]
      >移轉集名稱不允許使用特殊字元。

   1. **Cloud Service 設定**：輸入目標 AEM as a Cloud Service 製作 URL。

      >[!NOTE]
      >在內容轉移活動期間，您一次最多可以建立並維護四個移轉集。
      >此外，您還須針對每個特定環境 (*預備*、*開發*&#x200B;或&#x200B;*生產*) 分別建立移轉。

   1. **存取 Token**：輸入存取 Token。

      >[!NOTE]
      >您可以使用「開啟存取Token」按鈕來 **擷取存取Token** 。 您必須確定您屬於目標Cloud服務例項中的AEM管理員群組。

   1. **參數**：選取以下參數以建立移轉集：

      1. **包含版本**：視需要選取。

      1. **欲包含的路徑**：使用路徑瀏覽器來選取需要移轉的路徑。路徑選擇器可通過輸入或選擇接受輸入。

         >[!IMPORTANT]
         >建立移轉集時會限制下列路徑：
         >* `/apps`
         >* `/libs`
         >* `/home`
         >* `/etc`


1. 在填入&#x200B;**內容移轉集詳細資訊**&#x200B;畫面中的所有欄位後，請按一下&#x200B;**儲存**。

1. 您的移轉集會顯示在&#x200B;*綜覽*&#x200B;頁面中。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/04-item-selection-and-quick-actions.png)

   *「綜覽」*&#x200B;頁面中將顯示此畫面中上的所有現有移轉集，以及它們的目前狀態與狀態資訊。您可能會看到以下說明的部分圖示。

   * *紅色雲朵*&#x200B;表示您無法完成提取程序。
   * *綠色雲朵*&#x200B;表示您可以完成提取程序。
   * *黃色圖示*&#x200B;表示您並未建立現有移轉集，且該特定移轉集是由相同例項中的其他使用者所建立。

1. 從「綜覽」頁面選取移轉集，然後按一下&#x200B;**屬性**&#x200B;以檢視或編輯移轉集屬性。編輯屬性時，無法變更容器名稱或服務URL。



### 內容轉移中的提取程序 {#extraction-process}

請依照下列步驟，從「內容轉移工具」中提取您的移轉集：

1. 從&#x200B;*「綜覽」*&#x200B;頁面選取一個移轉集，然後按一下&#x200B;**提取**&#x200B;即可開始提取。The **Migration Set extraction** dialog box displays and click on **Extract** to start the extraction phase.

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/06-content-extraction.png)

   >[!NOTE]
   >您可以選擇在提取階段中覆寫預備容器。


1. 現 **在，EXTRACTION** 欄位顯示 **RUNNING** 狀態，以指示提取正在進行。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/07-extraction-job-running.png)

   提取一旦完成，移轉集的狀態會更新為&#x200B;**已完成**，而&#x200B;**資訊**&#x200B;欄位下會顯示一個&#x200B;*實心綠色*&#x200B;的雲朵圖示。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/10-extraction-complete.png)

   >[!NOTE]
   >UI有自動重新載入功能，每30秒重新載入一次概述頁面。
   >提取階段開始時將建立寫入鎖定，並在 *60 秒*&#x200B;後釋放。因此，如果提取停止，則需等待一分鐘才能釋放鎖定並重新開始提取。

#### 追加提取 {#top-up-extraction-process}

「內容轉移工具」具備支援追加差異內容的功能，可以只轉移在上一次內容轉移活動後所進行的變更。

>[!NOTE]
>初始轉移內容後，建議您先頻繁地執行追加差異內容，以縮短最終差異化內容轉移的內容凍結時間，然後再於雲端服務上線。

提取程序一旦完成，您即可使用追加提取方法來轉移差異內容。請遵循下列步驟：

1. 導覽至&#x200B;*綜覽*&#x200B;頁面，並選取您要執行追加提取的移轉集。按一下&#x200B;**提取**&#x200B;即可開始追加提取。**移轉集提取**&#x200B;對話框隨即顯示。

   >[!IMPORTANT]
   >
   >您必須停用&#x200B;**在提取期間覆寫預備容器**&#x200B;選項。
   >
   >![影像](/help/move-to-cloud-service/content-transfer-tool/assets/11-topup-extraction.png)

### 內容轉移中的擷取程序 {#ingestion-process}

請依照下列步驟，從「內容轉移工具」中擷取您的移轉集：

1. 從&#x200B;*綜覽*&#x200B;頁面選取一個移轉集，然後按一下&#x200B;**擷取**&#x200B;即可開始擷取。**移轉集擷取**&#x200B;對話框隨即顯示。Click on **Ingest** to start the ingestion phase. 為了示範，已停用&#x200B;**將內容擷取至製作例項**。您可以同時將內容擷取至「製作」和「發佈」。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/12-content-ingestion.png)

1. 擷取完成後，「發佈擷取」欄位中的 **狀態會更新** ，以 **便完成**。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/15-ingestion-complete.png)

#### 追加擷取 {#top-up-ingestion-process}

「內容轉移工具」具備支援&#x200B;*追加*&#x200B;差異內容的功能，可以只轉移在上一次內容轉移活動後所進行的變更。

>[!NOTE]
>
>初始轉移內容後，建議您先頻繁地執行追加差異內容，以縮短最終差異化內容轉移的內容凍結時間，然後再於雲端服務上線。

擷取程序一旦完成，您即可使用追加擷取方法來轉移差異內容。請遵循下列步驟：

1. 導覽至&#x200B;*綜覽*&#x200B;頁面，並選取您要執行追加擷取的移轉集。按一下&#x200B;**擷取**&#x200B;即可開始追加提取。**移轉集擷取**&#x200B;對話框隨即顯示。

   >[!IMPORTANT]
   >
   >您應停用「擷取 **前先擦除Cloud例項上的現有內容** 」選項，以防止從先前的擷取活動刪除現有內容。
   >
   >![影像](/help/move-to-cloud-service/content-transfer-tool/assets/16-topup-ingestion.png)

### 檢視移轉集記錄 {#viewing-logs-migration-set}

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

* 使用者為製作 URL (開發/預備/生產) 建立移轉集，並成功執行提取和擷取。

* 然後，使用者會為相同的製作 URL 建立新的移轉集，並對新移轉集執行提取和擷取。UI 會顯示第一個移轉集的擷取狀態已變更為&#x200B;**「失敗」**，並且沒有可用記錄。

* 這並不表示第一個移轉集擷取失敗。之所以會出現此行為，是因為開始新的擷取工作時，將刪除上一個擷取工作。因此，請忽略第一個移轉集的變更狀態。

* 「內容轉移工具」UI 中的圖示可能與本指南中顯示的螢幕擷圖不同，也可能完全不顯示 (取決於來源 AEM 例項的版本)。


