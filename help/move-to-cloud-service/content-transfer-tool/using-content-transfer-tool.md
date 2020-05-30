---
title: 使用內容傳輸工具
description: 使用內容傳輸工具
translation-type: tm+mt
source-git-commit: f154ffacbeeee1993a9cc3bd3bd274be33dca7a7
workflow-type: tm+mt
source-wordcount: '1527'
ht-degree: 1%

---


# 使用內容傳輸工具 {#using-content-transfer-tool}

## 使用內容傳輸工具的重要考量 {#pre-reqs}

請依照下節來瞭解執行內容傳輸工具時的重要考量事項：

* 內容傳輸工具的最低系統需求為AEM 6.3 +和JAVA 8。 如果您使用較低的AEM版本，您將需要將內容儲存庫升級至AEM 6.5，才能使用內容傳輸工具。

* 如果您使用沙盒環 *境*，請確定您的環境已升級至2020年5月29日或更新版本。 如果您使用的是 *生產環境*，則會自動更新。

* 若要使用內容傳輸工具，您必須是來源例項的管理員使用者，且屬於您要傳輸內容至之Cloud服務例項的管理群組。 未授權的使用者將無法擷取存取Token以使用內容傳輸工具。

* 在擷取階段中，內容傳輸工具會在作用中的AEM來源例項上執行。

* 作 *者的Ingestion Phase* （擷取階段）將縮小整個作者部署。 這表示在整個擷取程式期間，作者AEM將無法使用。

## 可用性 {#availability}

內容傳輸工具可從軟體散發入口網站下載為zip檔案。 您可以透過Package Manager在來源Adobe Experience Manager(AEM)例項上安裝套件。

>[!NOTE]
>從 [Adobe Experience Cloud下載內容傳輸工具](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)。

## 執行內容傳輸工具 {#running-tool}

請依照本節內容，瞭解如何使用內容傳輸工具將內容移轉至AEM做為雲端服務（作者／發佈）:

1. 選擇Adobe Experience Manager並導覽至工具-> **營運** -> **內容傳輸**。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/content1.png)

1. 按一下「 **建立移轉集** 」以建立新的移轉集。 將顯 **示「內容遷移集** 」詳細資訊。

   >[!NOTE]
   >您將檢視此畫面上現有的移轉集及其目前狀態。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-img4.png)

1. 填入「內容遷移集 **詳細資訊」螢幕中的欄位** ，如下所述。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/content-3.png)


   1. **名稱**: 輸入遷移集的名稱。
      >[!NOTE]
      >遷移集名稱不允許使用特殊字元。

   1. **雲端服務設定**: 輸入目標AEM作為Cloud Service Author URL。

      >[!NOTE]
      >在內容傳輸活動期間，您一次最多可建立和維護四個移轉集。
      >此外，您必須針對每個特定環境( *Stage*、 *Development*&#x200B;或 *Production*)分別建立移轉。

   1. **存取Token**: 輸入存取Token。

      >[!NOTE]
      >您可以導覽至，從作者例項擷取存取Token `/libs/granite/migration/token.json`。

   1. **參數**: 選擇以下參數以建立遷移集：

      1. **包含版本**: 視需要選擇。

      1. **要包含的路徑**: 使用路徑瀏覽器來選擇需要移轉的路徑。

         >[!IMPORTANT]
         >建立移轉集時，會限制下列路徑：
         >* `/apps`
         >* `/libs`
         >* `/home`
         >* `/etc`


1. 在「內 **容遷移集** 」詳細資訊螢幕中填入所有字 **段後，按一下保存** 。

1. 您將在「概述」頁面中檢視移 *轉集* 。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-img4.png)

   此螢幕上的所有現有遷移集都顯示在「概述」頁 *上* ，其當前狀態和狀態資訊。

   * 紅 *色雲* ，表示您無法完成擷取程式。
   * 綠 *色雲表示* ，您可以完成擷取程式。
   * 黃 *色圖示* ，表示您未建立現有的移轉集，而特定移轉集是由同一實例中的其他使用者建立。

1. 從概述頁面選擇遷移集，然後按一下 **屬性** ，以查看或編輯遷移集屬性。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-img6.png)

### 內容傳輸中的提取過程 {#extraction-process}

請依照下列步驟，從「內容傳輸工具」擷取您的移轉集：

1. 從「概述」頁面選取移 *轉集* ，然後按一下「 **擷取** 」以開始擷取。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/extraction-img1.png)

1. 將顯 **示「遷移集抽取** 」對話框，然後按一下「 **抽取** 」以完成抽取階段。

   >[!NOTE]
   >您可以選擇在擷取階段覆寫測試容器。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/extract-2.png)

1. 現 **在，EXTRACTION** 欄位顯示正在進行的抽取進程的 **RUNNING** 狀態。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/extract-3.png)

   提取完成後，移轉集的狀態會更新為 **FINISHED** ，而「 *INFO* 」（資訊）欄 **位下會顯示綠色穩** 定的雲端圖示。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/extract-4.png)

   >[!NOTE]
   >您必須重新整理頁面才能檢視更新的狀態。
   >啟動提取階段時，將建立寫鎖定並在 *60秒後釋放*。 因此，如果解壓停止，則需要等待一分鐘才能釋放鎖定，然後再次開始解壓。

#### 向上提取 {#top-up-extraction-process}

「內容傳輸工具」的功能可支援差異內容的向上調整，只能傳輸自先前的內容傳輸活動以來所做的變更。

>[!NOTE]
>在初次傳輸內容後，建議您先執行頻繁的差異化內容頂層，以縮短最終差異化內容傳輸的內容凍結期，然後再在雲端服務上線。

一旦提取過程完成，您就可以使用自頂向上的提取方法來傳輸Delta內容。 請遵循下列步驟：

1. 導覽至「 *概述* 」頁面，然後選擇要執行向上提取的遷移集。

1. 按一 **下「擷取** 」以開始從上方擷取。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/extraction-img1.png)

1. 將顯 **示「遷移集抽取** 」對話框。

   >[!IMPORTANT]
   >您應停用「擷取 **期間覆寫測試容器** 」選項。
   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/extract-topup-1.png)

### 內容傳輸中的擷取程式 {#ingestion-process}

請依照下列步驟，從「內容傳輸工具」中擷取您的移轉集：

1. 從「概述」頁面選取移 *轉集* ，然後按一下「 **收錄** 」以開始擷取。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-1.png)

1. 將顯 **示「遷移集提取** 」對話框。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-2.png)

   為了展示，「將內容 **收錄至作者」例項的選項** 已停用。 您可同時將內容收錄至「作者」和「發佈」。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-3.png)

   按一下「 **收錄** 」以完成擷取階段。

1. 擷取完成後，「作者擷取 **」欄位中的狀態會更新為「完成」，而「資訊」下方會顯示穩定的綠色雲端圖** 示 ********。
   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-4.png)

   >[!NOTE]
   > 您必須重新整理頁面才能檢視更新的狀態。

#### 向上擷取 {#top-up-ingestion-process}

「內容傳輸工具」的功能支援差異內容 *向上* ，只能傳輸自先前內容傳輸活動以來所做的變更。

>[!NOTE]
>在初次傳輸內容後，建議您先執行頻繁的差異化內容頂層，以縮短最終差異化內容傳輸的內容凍結期，然後再在雲端服務上線。

擷取程式完成後，您就可使用向上擷取方法來使用Delta內容。 請遵循下列步驟：

1. 導覽至「 *概述* 」頁面，並選取您要執行向上擷取的移轉集。

1. 按一 **下「收錄** 」以開始從上方擷取。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-1.png)

1. 將顯 **示「遷移集提取** 」對話框。

   >[!NOTE]
   >您應停用「 *擦除* 」選項，以防止從先前的擷取活動刪除現有內容。
   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-topup-1.png)

### 查看遷移集的日誌 {#viewing-logs-migration-set}

您可以從「概述」頁面檢視現有移轉集的 *記錄* 檔。
請遵循下列步驟：

1. 導覽至「 *概述* 」頁面，然後選取您要刪除的移轉集，然後從動作列按 **一下「檢視記錄** 」。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/view-log1.png)

1. 將顯 **示「日** 志」對話框。 按一下 **抽取日誌** ，在新頁籤中查看日誌。

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/view-log2.png)Or,

   您也可以從「概述」畫面中檢視移轉集的 *記錄* 。 選擇遷移集，然後按一下「抽取」( **EXTRACTION** )欄位下的狀態。 在這種情況下，按一下「 **完成** 」(FINISHED)查看新頁籤中的日誌。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/view-log3.png)

### 刪除遷移集 {#deleting-migration-set}

您可以從「概述」頁面刪除移 *轉集* 。
請遵循下列步驟：

1. 導覽至「 *概述* 」頁面，然後選取您要刪除的移轉集，然後從動作列按一下「 **刪除** 」。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/delete-1.png)

1. 按一下 **從刪** 除遷移集對話框中刪除 **** ，以確認刪除。

   ![影像](/help/move-to-cloud-service/content-transfer-tool/assets/delete-3.png)

## 疑難排解 {#troubleshooting}

### 缺少Blob ID {#missing-blobs}

如果報告缺少的blob ID（如下所述），則需要在現有儲存庫中執行一致性檢查並恢復缺少的blob。
`ERROR o.a.j.o.p.b.AbstractSharedCachingDataStore - Error retrieving record [ba45c53f8b687e7056c85dceebf8156a0e6abc7e]`

執行下列命令

>[!NOTE]
> `--verbose` 標籤是報告引用blob的節點路徑所必需的。

**針對儲存庫AEM 6.5（Oak 1.8及以下版本）**

```shell
java -jar oak-run.jar datastorecheck --consistency --store [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds] <DATASTORE_CFG> --verbose <OUT_DIR> --dump
```

**對於具有Oak > 1.10的儲存庫**

```shell
java -jar oak-run.jar datastore --check-consistency [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds|azureds] <DATASTORE_CFG> --out-dir <OUT_DIR> --work-dir <TEMP_DIR> --verbose
```

如需詳細 [資訊，請參閱Oak Runnable Jar](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run) 。

然後，可以檢查在上述 ** OUT_DIR中為一致性而建立的檔案是否缺少二進位檔案，以及採取的適當操作（如從備份中恢復、刪除路徑、重新編製索引等）。

### UI行為 {#ui-behavior}

身為使用者，您可能會在內容傳輸工具的使用者介面(UI)中看到下列行為變更：

* 使用者為作者URL（開發／階段／生產）建立移轉集，並成功執行擷取和擷取。

* 然後，使用者會針對相同的作者URL建立新的移轉集，並對新移轉集執行擷取和擷取。 UI顯示第一個遷移集的接收狀態更改為 **FAILED** ，沒有可用日誌。

* 這並不意味著第一個遷移集的提取失敗。 出現此行為是因為啟動新的提取作業時，它會刪除先前的提取作業。 因此，應忽略第一個遷移集上的更改狀態。

* 「內容傳輸工具UI」中的圖示可能與本指南中顯示的螢幕擷取畫面不同，或根據來源AEM例項的版本而完全不顯示。


