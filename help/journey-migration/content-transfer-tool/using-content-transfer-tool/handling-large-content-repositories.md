---
title: 處理大型內容存放庫
description: 本節介紹如何處理大型內容儲存庫
exl-id: 21bada73-07f3-4743-aae6-2e37565ebe08
source-git-commit: be66d3e255d43156dfd181711d5a372f2c85f6d5
workflow-type: tm+mt
source-wordcount: '1778'
ht-degree: 1%

---

# 處理大型內容存放庫 {#handling-large-content-repositories}

## 總覽 {#overview}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_precopy"
>title="處理大型內容存放庫"
>abstract="為了顯著加快內容轉移活動的提取和擷取階段以將內容移至AEMas a Cloud Service,CTT可以利用AzCopy作為可選的預複製步驟。 配置此預先步驟後，在提取階段中，AzCopy將Blob從Amazon S3或Azure Blob儲存複製到遷移集Blob儲存。 在獲取階段，AzCopy將Blob從遷移集Blob儲存區複製到目標AEMas a Cloud ServiceBlob儲存區。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#setting-up-pre-copy-step" text="以AzCopy作為預複製步驟入門"

使用內容轉移工具(CTT)複製大量Blob可能需要數天時間。
為了大幅加快內容轉移活動的提取和擷取階段，以將內容移至AEMas a Cloud Service,CTT可運用 [AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) 作為選用的預先複製步驟。 當來源AEM例項設定為使用Amazon S3、Azure Blob儲存資料存放區或檔案資料存放區時，可使用此預先複製步驟。 預複製步驟對於第1次完全擷取和擷取最有效。 但是，不建議對後續追加使用預拷貝（如果追加大小小於200GB），因為這可能會為整個過程增加時間。 配置此預先步驟後，在提取階段中，AzCopy將Blob從Amazon S3、Azure Blob儲存或檔案資料儲存複製到遷移集blob儲存。 在獲取階段，AzCopy將Blob從遷移集Blob儲存區複製到目標AEMas a Cloud ServiceBlob儲存區。

>[!NOTE]
> 此功能已於CTT 1.5.4版中推出。

## 開始前的重要考量 {#important-considerations}

開始之前，請依照下節了解重要考量事項：

* 來源AEM版本必須為6.3 - 6.5。

* 來源AEM資料存放區已設定為使用Amazon S3或Azure Blob儲存。 如需詳細資訊，請參閱 [在AEM 6中配置節點儲存區和資料儲存區](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html?lang=en).

* 每個移轉集都會複製整個資料存放區，因此只應使用單一移轉集。

* 您需要存取權才能安裝 [AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) 在執行來源AEM例項的執行個體（或VM）上。

* 資料儲存垃圾收集已在源上前7天內運行。 如需詳細資訊，請參閱 [資料儲存垃圾收集](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html?lang=en#data-store-garbage-collection).


### 如果來源AEM例項設定為使用Amazon S3或Azure Blob儲存資料存放區，則需額外考量 {#additional-considerations-amazons3-azure}

* 由於從Amazon S3和Azure Blob儲存中傳輸資料會產生相關成本，因此傳輸成本會與儲存容器中的資料總量(無論是否在AEM中參考)相關。 請參閱 [Amazon S3](https://aws.amazon.com/s3/pricing/) 和 [Azure Blob儲存](https://azure.microsoft.com/en-us/pricing/details/bandwidth/) 以取得更多詳細資訊。

* 您將需要源Amazon S3儲存桶的訪問密鑰和密鑰對，或源Azure Blob儲存容器的SAS URI（只讀訪問可以正常）。

### 若來源AEM例項已設定為使用檔案資料存放區，則需額外考量 {#additional-considerations-aem-instance-filedatastore}

* 本地系統的可用空間必須嚴格大於源資料儲存區的1/256大小。 例如，如果資料存放區的大小為3 TB，則中必須存在大於11.72 GB的可用空間 `crx-quickstart/cloud-migration` 資料夾，以便AzCopy工作。 源系統至少應有1 GB的可用空間。 可使用 `df -h` 命令和Windows實例中的dir命令。

* 每次在啟用AzCopy的情況下運行提取時，整個檔案資料儲存區都會平面化並複製到雲遷移容器中。 如果您的遷移集大大小於資料儲存的大小，則AzCopy提取不是最佳方法。

* 一旦使用AzCopy通過資料儲存庫進行複製，請禁用它進行增量或追加提取。

## 設定使用AzCopy作為預複製步驟 {#setting-up-pre-copy-step}

請遵照本節所述，了解如何設定使用AzCopy作為內容轉移工具的預拷貝步驟，以將內容遷移到AEMas a Cloud Service:

### 0.決定資料儲存區中所有內容的總大小 {#determine-total-size}

由於以下兩個原因，請務必判斷資料存放區的總大小：

* 如果源AEM配置為使用檔案資料儲存，則本地系統的可用空間必須嚴格大於源資料儲存的1/256大小。

* 了解資料存放區的總大小有助於預估擷取和擷取時間。 使用 [內容轉移工具電腦](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-implementation-phase.html?lang=en#content-transfer) in [Cloud Acceleration Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/introduction-cam/overview-cam.html?lang=en) 以取得提取和擷取時間的預估值。

#### Azure Blob儲存資料儲存 {#azure-blob-storage}

從Azure入口網站的容器屬性頁面，使用 **計算大小** 按鈕，確定容器中所有內容的大小。 例如：

![影像](/help/journey-migration/content-transfer-tool/assets/Azure-blob-storage-data-store.png)

#### Amazon S3 Data Store {#amazon-data}

您可以使用容器的「量度」標籤來判斷容器中所有內容的大小。 例如：


![影像](/help/journey-migration/content-transfer-tool/assets/amazon-s3-data-store.png)

#### 檔案資料存放區 {#file-data-store-determine-size}

* 對於mac、UNIX系統，在資料儲存目錄上運行du命令以獲取其大小：
   `du -sh [path to datastore on the instance]`. 例如，如果資料存放區位於 `/mnt/author/crx-quickstart/repository/datastore`，下列命令會取得大小： `du -sh /mnt/author/crx-quickstart/repository/datastore`.

* 對於Windows，請使用資料儲存目錄上的dir命令獲取其大小：
   `dir /a/s [location of datastore]`。

### 1.安裝AzCopy {#install-azcopy}

[AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) 是Microsoft提供的命令列工具，必須可在來源執行個體上使用，才能啟用此功能。

簡而言之，您很可能想從 [AzCopy文檔頁](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) 並將其解除標籤至/usr/bin等位置。

>[!IMPORTANT]
>請注意二進位檔的放置位置，因為您在後續步驟中需要其完整路徑。

### 2.安裝內容轉移工具(CTT)版本，並支援AzCopy {#install-ctt-azcopy-support}

CTT 1.5.4版包含對Amazon S3和Azure Blob儲存的AzCopy支援。
CTT 1.7.2版支援檔案資料存放區您可從以下網址下載最新版本的CTT: [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) 入口網站。


### 3.設定azcopy.config檔案 {#configure-azcopy-config-file}

在來源AEM例項上，位於 `crx-quickstart/cloud-migration`，建立名為的新檔案 `azcopy.config`.

>[!NOTE]
>此設定檔案的內容會因您的來源AEM例項使用Azure或Amazon S3資料存放區或檔案資料存放區而異。

#### Azure Blob儲存資料儲存 {#azure-blob-storage-data}

您的azcopy.config檔案應包含下列屬性（請務必為執行個體使用正確的azCopyPath和azureSas）。

>[!NOTE]
>
> 如果您不想授予Blob儲存容器的寫入訪問權限，則可以生成只具有讀取和清單權限的新SAS URI。

```
azCopyPath=/usr/bin/azcopy
azureSas=https://example-resource.blob.core.windows.net/example-container?sig=--REDACTED--
```

#### Amazon S3 Data Store {#amazon-sdata-store}

您的azcopy.config檔案應包含下列屬性（請務必為執行個體使用正確的值）。

>[!NOTE]
>
> 如果您的實例使用IAM角色來使AEM能夠訪問S3，則您需要建立策略和用戶，並為S3儲存桶啟用ListBucket和GetObject操作。 設定後，請使用此使用者的存取金鑰和機密金鑰。

```
azCopyPath=/usr/bin/azcopy
s3Bucket=aem-63
s3Region=us-west-2
s3AccessKey=--REDACTED--
s3SecretKey=--REDACTED--
```

#### 檔案資料存放區 {#file-data-store-azcopy-config}

您的 `azcopy.config` 檔案必須包含azcopyPath屬性，以及指向檔案資料存放區位置的可選repository.home屬性。 請為您的例項使用正確的值。
檔案資料存放區

```
azCopyPath=/usr/bin/azcopy
repository.home=/mnt/crx/author/crx-quickstart/repository/datastore
```

azcopyPath屬性必須包含源AEM實例上安裝azCopy命令行工具的位置的完整路徑。 如果缺少azCopyPath屬性，則不執行blob預復步驟。

若 `repository.home` azcopy.config中缺少屬性，然後是預設資料存放區位置 `/mnt/crx/author/crx-quickstart/repository/datastore` 將用於執行預復。

### 4.使用AzCopy提取 {#extracting-azcopy}

在配置了上述配置檔案後，AzCopy預複製階段將作為後續提取的一部分運行。 若要防止其執行，您可以重新命名此檔案或將其移除。

>[!NOTE]
>如果AzCopy未正確配置，您將在日誌中看到以下消息：
>`INFO c.a.g.s.m.c.a.AzCopyCloudBlobPreCopy - Blob pre-copy is not supported`.

1. 從CTT UI開始擷取。 請參閱 [內容轉移工具快速入門](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en) 和 [提取程式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/extracting-content.html?lang=en) 以取得更多詳細資訊。

1. 確認以下行已打印在提取日誌中：

```
c.a.g.s.m.commons.ContentExtractor - *************** Beginning AzCopy Pre-Copy phase ***************
```

恭喜！ 此日誌條目表示您的配置被視為有效，並且AzCopy當前正在將源容器中的所有Blob複製到遷移容器。

來自AzCopy的日誌條目將出現在提取日誌中，並且前置詞將為c.a.gs.m.c.azcopy.AzCopyBlobPreCopy - [AzCopy預拷貝]

>[!CAUTION]
>
> 在提取的前幾分鐘，請密切留意提取記錄中是否有任何問題跡象。 例如，如果找不到來源Azure容器，將記錄以下內容：

```
[AzCopy pre-copy] failed to perform copy command due to error: cannot start job due to error: cannot list files due to reason -> github.com/Azure/azure-storage-blob-go/azblob.newStorageError, github.com/Azure/azure-storage-blob-go@v0.10.1-0.20210407023846-16cf969ec1c3/azblob/zc_storage_error.go:42
[AzCopy pre-copy] ===== RESPONSE ERROR (ServiceCode=ContainerNotFound) =====
[AzCopy pre-copy] Description=The specified container does not exist.
[AzCopy pre-copy] RequestId:5fb674b9-201e-001b-2a5b-527400000000
[AzCopy pre-copy] Time:2021-05-26T18:18:07.5931967Z, Details: 
[AzCopy pre-copy] Code: ContainerNotFound
```

如果AzCopy出現問題，提取將立即失敗，提取日誌將包含有關故障的詳細資訊。

AzCopy會在後續運行時自動跳過在錯誤之前複製的任何Blob，而且不需要再次複製。

#### 用於檔案資料儲存 {#file-data-store-extract}

當為源檔案dataStore運行AzCopy時，您應該會在日誌中看到這樣的消息，指示正在處理資料夾：
`c.a.g.s.m.c.a.AzCopyFileSourceBlobPreCopy - [AzCopy pre-copy] Processing folder (1/24) crx-quickstart/repository/datastore/5d`

### 5.使用AzCopy獲取 {#ingesting-azcopy}

隨著內容轉移工具1.5.4的推出，我們為製作擷取新增了AzCopy支援。

>[!NOTE]
>建議先單獨執行「作者」擷取。 這會在稍後執行時加速發佈擷取。

為了在獲取過程中利用AzCopy，我們要求您使用至少2021.6.5561版的AEMas a Cloud Service版。

從CTT UI開始擷取作者。 請參閱 [擷取程式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/ingesting-content.html?lang=en) 以取得更多詳細資訊。
AzCopy的日誌條目將出現在獲取日誌中。 它們看起來會像這樣：

```
*************** Beginning AzCopy pre-copy phase ***************
INFO: Scanning...
INFO: Failed to create one or more destination container(s). Your transfers may still succeed if the container already exists.
INFO: Any empty folders will not be processed, because source and/or destination doesn't have full folder support
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

## 禁用AzCopy {#disable-azcopy}

要禁用AzCopy，請更名或刪除 `azcopy.config` 檔案。

例如，azcopy擷取可透過： `mv /mnt/crx/author/crx-quickstart/cloud-migration/azcopy.config /mnt/crx/author/crx-quickstart/cloud-migration/noazcopy.config`.

## 下一步 {#whats-next}

學習「處理大型內容存放庫」以大幅加快內容轉移活動的提取和擷取階段，以便將內容移至AEMas a Cloud Service後，您現在就可以了解「內容轉移工具」的提取程式。 請參閱 [在內容轉移工具中從來源擷取內容](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md) 了解如何從「內容轉移工具」中擷取您的移轉集。
