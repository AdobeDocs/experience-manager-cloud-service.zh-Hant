---
title: 處理大型內容存放庫
description: 本節說明如何處理大型內容存放庫
exl-id: 21bada73-07f3-4743-aae6-2e37565ebe08
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1800'
ht-degree: 8%

---

# 處理大型內容存放庫 {#handling-large-content-repositories}

## 概觀 {#overview}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_precopy"
>title="處理大型內容存放庫"
>abstract="為了大幅加快內容轉移活動的解壓縮和擷取階段，以將內容移至 AEM as a Cloud Service，內容轉移工具 (CTT) 可以使用 AzCopy 作為預複製步驟 (選用)。設定此預先步驟後，在提取階段，AzCopy 會從 Amazon S3 或 Azure Blob 儲存空間將 blob 複製到移轉集 blob 存放區。在攝入階段，AzCopy 將 blob 會從移轉集 blob 存放區將 blob 複製到目的地 AEM as a Cloud Service blob 存放區。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=zh-Hant#setting-up-pre-copy-step" text="開始使用 AzCopy 作為預複製步驟"

使用內容轉移工具(CTT)複製許多Blob可能需要數天的時間。
為了加速內容轉移活動的擷取和擷取階段，以將內容移至AEMas a Cloud Service，CTT可以使用 [AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) 作為選用的預先複製步驟。 當來源AEM執行個體設定為使用Amazon S3、Azure Blob儲存體資料存放區或檔案資料存放區時，可使用此預先複製步驟。 預先複製步驟在第一次完整擷取和擷取時最有效。 不過，不建議對後續追加使用預先複製（如果追加大小小於200 GB），因為這樣可能會增加整個程式的時間。 設定此預先步驟後，在擷取階段中，AzCopy會將blob從Amazon S3、Azure Blob儲存體或檔案資料存放區複製至移轉集blob存放區。 在攝入階段，AzCopy 將 blob 會從移轉集 blob 存放區將 blob 複製到目的地 AEM as a Cloud Service blob 存放區。

## 開始前的重要考量 {#important-considerations}

請詳閱以下章節，瞭解在開始前的重要考量事項：

* 從CTT 2.0.16版開始，安裝套件組合時，會自動完成預先複製設定。 此外，如果移轉集大小大於200 GB，擷取程式會自動使用預先複製功能。 azcopy.config檔案是在crx-quickstart/cloud-migration/目錄中建立。 如果您使用CTT 2.0.16版或更新版本，則不需要手動進行預先複製設定。

* 來源AEM版本必須為6.3 - 6.5。

* 來源AEM資料存放區已設定為使用Amazon S3或Azure Blob Storage。 如需詳細資訊，請參閱 [在AEM 6中設定節點存放區和資料存放區](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html).

* 每個移轉集都會複製整個資料存放區，因此只應使用單一移轉集。

* 您需要存取權才能安裝 [AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) 執行來源AEM執行個體的執行個體（或VM）。

* 已在來源上的前七天內執行資料存放區記憶體回收。 如需詳細資訊，請參閱 [資料存放區記憶體回收](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html#data-store-garbage-collection).

### 如果來源AEM執行個體設定為使用Amazon S3或Azure Blob儲存資料存放區，則需考慮其他事項 {#additional-considerations-amazons3-azure}

* 將資料從Amazon S3和Azure Blob儲存體傳輸需支付相關費用。 傳輸成本會與您現有儲存容器中的資料總量相關(無論是否在AEM中參照)。 另請參閱 [Amazon S3](https://aws.amazon.com/s3/pricing/) 和 [Azure Blob儲存體](https://azure.microsoft.com/en-us/pricing/details/bandwidth/) 以取得更多詳細資料。

* 您需要現有來源Amazon S3儲存貯體的存取金鑰和機密金鑰組，或現有來源Azure Blob儲存容器的SAS URI （可透過唯讀方式存取）。

### 如果來源AEM執行個體設定為使用檔案資料存放區，則需考慮其他事項 {#additional-considerations-aem-instance-filedatastore}

* 本機系統的可用空間必須嚴格大於來源資料存放區的1/256大小。 例如，如果資料存放區的大小為3 TB，則大於11.72 GB的可用空間必須存在於 `crx-quickstart/cloud-migration` AzCopy要運作之來源上的資料夾。 來源系統至少應有1 GB的可用空間。 可使用取得可用空間 `df -h` Linux®執行個體上的command和Windows執行個體中的dir command。

* 每次在啟用AzCopy的情況下執行擷取時，整個檔案資料存放區都會平面化，並複製到雲端移轉容器。 如果您的移轉集小於資料存放區的大小，則AzCopy擷取並非最佳方法。

* 使用AzCopy複製現有資料存放區後，請針對差異或追加擷取將其停用。

## 設定以使用AzCopy作為預先複製步驟 {#setting-up-pre-copy-step}

>[!NOTE]
>從CTT 2.0.16版開始，安裝套件組合時，會自動完成預先複製設定。 此外，如果移轉集大小大於200 GB，擷取程式會自動使用預先複製功能。 azcopy.config檔案是在crx-quickstart/cloud-migration/目錄中建立。 如果您想要手動更新檔案的設定，請檢閱以下區段。

請詳閱本節，以瞭解如何設定搭配內容轉移工具使用AzCopy作為預先複製步驟，將內容移轉至AEMas a Cloud Service：

### 0.決定資料存放區中所有內容的總大小 {#determine-total-size}

判斷資料存放區的總大小很重要，原因有二：

* 如果來源AEM設定為使用檔案資料存放區，則本機系統的可用空間必須嚴格大於來源資料存放區的1/256大小。

#### Azure Blob儲存體資料存放區 {#azure-blob-storage}

從Azure入口網站中的現有容器屬性頁面，使用 **計算大小** 按鈕來決定容器中所有內容的大小。 例如：

![影像](/help/journey-migration/content-transfer-tool/assets/Azure-blob-storage-data-store.png)

#### Amazon S3資料存放區 {#amazon-data}

您可以使用容器的「量度」標籤來決定容器中所有內容的大小。 例如：


![影像](/help/journey-migration/content-transfer-tool/assets/amazon-s3-data-store.png)

#### 檔案資料存放區 {#file-data-store-determine-size}

* 對於Mac、UNIX®系統，請在資料存放區目錄上執行du命令以取得其大小：
  `du -sh [path to datastore on the instance]`。例如，如果您的資料存放區位於 `/mnt/author/crx-quickstart/repository/datastore`，下列指令會讓您取得其大小： `du -sh /mnt/author/crx-quickstart/repository/datastore`.

* 對於Windows，請使用資料存放區目錄上的dir命令來取得其大小：
  `dir /a/s [location of datastore]`。

### 1.安裝AzCopy {#install-azcopy}

[AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) 是Microsoft提供的命令列工具®必須在來源例項上可用才能啟用此功能。

簡而言之，您要從下載Linux® x86-64二進位檔 [AzCopy檔案頁面](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) 並將其解壓縮至某個位置，例如/usr/bin。

>[!IMPORTANT]
>請記下您放置二進位檔的位置，因為您需要在後續步驟中取得該二進位檔的完整路徑。

### 2.安裝支援AzCopy的內容轉移工具(CTT)版本 {#install-ctt-azcopy-support}

>[!IMPORTANT]
>應使用最近發行的CTT版本。

最新CTT發行版本包含對Amazon S3、Azure Blob Storage和檔案資料存放區的AzCopy支援。
您可以從以下網址下載最新版的CTT： [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) 入口網站。
請注意，僅支援2.0.0版及更新版本，建議您使用最新版本。

### 3.設定azcopy.config檔案 {#configure-azcopy-config-file}

在來源AEM例項中 `crx-quickstart/cloud-migration`，建立名為的檔案 `azcopy.config`.

>[!NOTE]
>此設定檔的內容會有所不同，端視您的來源AEM執行個體使用Azure、Amazon S3資料存放區或檔案資料存放區而定。

#### Azure Blob儲存體資料存放區 {#azure-blob-storage-data}

您的azcopy.config檔案應包括下列屬性（請確定您執行個體使用正確的azCopyPath和azureSas）。

>[!NOTE]
>
> 如果您不想要授與現有blob儲存容器的寫入許可權，可以產生只具有讀取和清單許可權的新SAS URI。

```
azCopyPath=/usr/bin/azcopy
azureSas=https://example-resource.blob.core.windows.net/example-container?sig=--REDACTED--
```

#### Amazon S3資料存放區 {#amazon-sdata-store}

您的azcopy.config檔案應包括下列屬性（請務必針對您的執行個體使用正確的值）。

>[!NOTE]
>
> 如果您的執行個體使用IAM角色來啟用AEM存取S3，則必須建立原則和使用者，且為S3儲存貯體啟用ListBucket和GetObject動作。 設定之後，請使用此使用者的存取金鑰和秘密金鑰。

```
azCopyPath=/usr/bin/azcopy
s3Bucket=aem-63
s3Region=us-west-2
s3AccessKey=--REDACTED--
s3SecretKey=--REDACTED--
```

#### 檔案資料存放區 {#file-data-store-azcopy-config}

您的 `azcopy.config` 檔案必須包含azCopyPath屬性，以及指向檔案資料存放區位置的選擇性repository.home屬性。 針對您的執行個體使用正確的值。
檔案資料存放區

```
azCopyPath=/usr/bin/azcopy
repository.home=/mnt/crx/author/crx-quickstart/repository/datastore
```

azCopyPath屬性必須包含來源AEM例項上安裝azCopy命令列工具所在位置的完整路徑。 如果缺少azCopyPath屬性，則不會執行blob預先複製步驟。

如果 `repository.home` azcopy.config中缺少屬性，則為預設的資料存放區位置 `/mnt/crx/author/crx-quickstart/repository/datastore` 用於執行預先複製。

### 4.使用AzCopy擷取 {#extracting-azcopy}

設定好上述組態檔後，AzCopy預先複製階段就會在後續每次擷取作業中執行。 若要防止它執行，您可以重新命名此檔案或將其移除。

>[!NOTE]
>如果AzCopy未正確設定，您會在記錄中看到下列訊息：
>`INFO c.a.g.s.m.c.a.AzCopyCloudBlobPreCopy - Blob pre-copy is not supported`.

1. 開始從CTT UI擷取。 另請參閱 [內容轉移工具快速入門](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md) 和 [提取程式](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md) 以取得更多詳細資料。

1. 確認下列行已列印在擷取記錄中：

```
c.a.g.s.m.commons.ContentExtractor - *************** Beginning AzCopy Pre-Copy phase ***************
```

恭喜！此記錄專案表示您的設定被視為有效，且AzCopy正在將所有blob從來源容器複製到移轉容器。

來自AzCopy的記錄專案會顯示在擷取記錄中，並加上前置詞c.a.g.s.m.c.azcopy.AzCopyBlobPreCopy - [AzCopy預先複製]

>[!CAUTION]
>
> 在擷取的最初幾分鐘，請密切觀察擷取記錄檔，以找出任何問題的跡象。 例如，如果找不到來源Azure容器，將記錄以下內容：

```
[AzCopy pre-copy] failed to perform copy command due to error: cannot start job due to error: cannot list files due to reason > github.com/Azure/azure-storage-blob-go/azblob.newStorageError, github.com/Azure/azure-storage-blob-go@v0.10.1-0.20210407023846-16cf969ec1c3/azblob/zc_storage_error.go:42
[AzCopy pre-copy] ===== RESPONSE ERROR (ServiceCode=ContainerNotFound) =====
[AzCopy pre-copy] Description=The specified container does not exist.
[AzCopy pre-copy] RequestId:5fb674b9-201e-001b-2a5b-527400000000
[AzCopy pre-copy] Time:2021-05-26T18:18:07.5931967Z, Details: 
[AzCopy pre-copy] Code: ContainerNotFound
```

如果AzCopy發生問題，擷取會立即失敗，而擷取記錄檔會包含失敗的詳細資訊。

後續執行時，AzCopy會自動略過錯誤前所複製的任何Blob，而且不需要再次複製。

>[!TIP]
>現在，內嵌可排程在擷取成功後立即自動開始。 另請參閱 [將內容內嵌至目標](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) 以取得詳細資訊。

#### 針對檔案資料存放區 {#file-data-store-extract}

當針對來源檔案dataStore執行AzCopy時，您應該會在記錄中看到類似這些的訊息，指出正在處理資料夾：
`c.a.g.s.m.c.a.AzCopyFileSourceBlobPreCopy - [AzCopy pre-copy] Processing folder (1/24) crx-quickstart/repository/datastore/5d`

### 5.使用AzCopy擷取 {#ingesting-azcopy}

另請參閱 [將內容內嵌至目標](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) 有關從Cloud Acceleration Manager (CAM)將內容擷取到目標的一般資訊，包括在「新擷取」對話方塊中如何使用AzCopy （預先複製）或不使用的指示。

若要在內嵌期間使用AzCopy，Adobe需要您使用至少為2021.6.5561版的AEMas a Cloud Service版本。

請檢視Cloud Acceleration Manager中的「擷取工作」清單和擷取記錄，以便您檢視進度。 與成功的AzCopy工作相關的記錄專案如下所示（允許一些差異）。 有時檢查記錄檔可能會及早警示您問題，並協助您找到任何問題的快速解決方案。

```
*************** Beginning AzCopy pre-copy phase ***************
INFO: Scanning...
INFO: Failed to create one or more destination container(s). Your transfers may still succeed if the container already exists.
INFO: Any empty folders will not be processed, because source and/or destination does not have full folder support
INFO: azcopy: A newer version 10.11.0 is available to download
 
Job 419d98da-fc05-2a45-70cc-797fee632031 has started
Log file is located at: /root/.azcopy/419d98da-fc05-2a45-70cc-797fee632031.log
 
0.0 %, 0 Done, 0 Failed, 886 Pending, 0 Skipped, 886 Total,
 
Job 419d98da-fc05-2a45-70cc-797fee632031 summary
Elapsed Time (Minutes): 0.0334
Number of File Transfers: 886
Number of Folder Property Transfers: 0
Total Number of Transfers: 886
Number of Transfers Completed: 17
Number of Transfers Failed: 0
Number of Transfers Skipped: 869
TotalBytesTransferred: 248350
Final Job Status: CompletedWithSkipped
 
*************** Completed AzCopy pre-copy phase ***************
```

## 下一步 {#whats-next}

您現在已瞭解如何處理大型內容存放庫，以加快內容轉移活動的擷取和擷取階段，將內容移至AEMas a Cloud Service。 您現在已準備好學習使用內容轉移工具的擷取程式。 另請參閱 [在內容轉移工具中從來源擷取內容](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md) 以便您瞭解如何從「內容轉移工具」中擷取移轉集。
