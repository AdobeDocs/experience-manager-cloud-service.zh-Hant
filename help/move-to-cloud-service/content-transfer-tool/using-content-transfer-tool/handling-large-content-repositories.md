---
title: 處理大型內容存放庫
description: 本節介紹如何處理大型內容儲存庫
exl-id: 2eca7fa6-fb34-4b08-b3ec-4e9211e94275
source-git-commit: bdcc5cfc229fd5b1fd1f70e37c7231ed3f727e72
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 處理大型內容存放庫 {#handling-large-content-repositories}

## 概覽 {#overview}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_precopy"
>title="處理大型內容存放庫"
>abstract="為了顯著加快內容轉移活動的提取和擷取階段以將內容移至AEMas a Cloud Service,CTT可以利用AzCopy作為可選的預複製步驟。 配置此預先步驟後，在提取階段中，AzCopy將Blob從Amazon S3或Azure Blob儲存複製到遷移集Blob儲存。 在獲取階段，AzCopy將Blob從遷移集Blob儲存區複製到目標AEMas a Cloud ServiceBlob儲存區。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#setting-up-pre-copy-step" text="以AzCopy作為預複製步驟入門"

使用內容轉移工具(CTT)複製大量Blob可能需要數天時間。
為了大幅加快內容轉移活動的提取和擷取階段，以將內容移至AEMas a Cloud Service,CTT可以運用[AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10)作為選用的預先複製步驟。 將來源AEM例項設定為使用Amazon S3或Azure Blob儲存資料存放區時，可使用此預先複製步驟。  配置此預先步驟後，在提取階段中，AzCopy將Blob從Amazon S3或Azure Blob儲存複製到遷移集Blob儲存。 在獲取階段，AzCopy將Blob從遷移集Blob儲存區複製到目標AEMas a Cloud ServiceBlob儲存區。

>[!NOTE]
> 此功能已於CTT 1.5.4版中推出。

## 開始前的重要考量 {#important-considerations}

開始之前，請依照下節了解重要考量事項：

* 來源AEM版本必須為6.3 - 6.5
* 來源AEM資料存放區已設定為使用Amazon S3或Azure Blob儲存。 如需詳細資訊，請參閱[設定AEM 6](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html?lang=en)中的節點存放區和資料存放區。
* 提取期間會複製整個資料存放區。 由於從Amazon S3和Azure Blob儲存中傳輸資料會產生相關成本，因此傳輸成本會與儲存容器中的資料總量(無論是否在AEM中參考)相關。 如需詳細資訊，請參閱[Amazon S3](https://aws.amazon.com/s3/pricing/)和[Azure Blob儲存](https://azure.microsoft.com/en-us/pricing/details/bandwidth/)。
* 每個移轉集都會複製整個資料存放區，因此只應使用單一移轉集。
* 您需要訪問運行源AEM實例的實例（或VM）上的[AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10)。
* 您將需要源Amazon S3儲存桶的訪問密鑰和密鑰對，或源Azure Blob儲存容器的SAS URI（只讀訪問可以正常）。
* 資料儲存垃圾收集已在源上前7天內運行。 有關詳細資訊，請參閱[資料儲存垃圾收集](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html?lang=en#data-store-garbage-collection)。
* 移轉程式中會包含來源例項上的大部分資料。

## 設定使用AzCopy作為預複製步驟 {#setting-up-pre-copy-step}

請遵照本節所述，了解如何設定使用AzCopy作為內容轉移工具的預拷貝步驟，以將內容遷移到AEMas a Cloud Service:

### 0.決定資料儲存區中所有內容的總大小 {#determine-total-size}

#### Azure Blob儲存資料儲存 {#azure-blob-storage}

從Azure入口網站的容器屬性頁面，使用&#x200B;**計算大小**&#x200B;按鈕來判斷容器中所有內容的大小。 例如：

![影像](/help/move-to-cloud-service/content-transfer-tool/assets/Azure-blob-storage-data-store.png)

#### Amazon S3 Data Store {#amazon-data}

您可以使用容器的「量度」標籤來判斷容器中所有內容的大小。 例如：


![影像](/help/move-to-cloud-service/content-transfer-tool/assets/amazon-s3-data-store.png)

### 1.安裝AzCopy {#install-azcopy}

[](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) AzCopy是Microsoft提供的命令行工具，需要在源實例上提供該工具才能啟用此功能。

簡而言之，您很可能會想從[AzCopy檔案頁面](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10)下載Linux x86-64二進位檔，並將其解除標籤至/usr/bin之類的位置。 請注意二進位檔的放置位置，因為您在後續步驟中需要其完整路徑。

### 2.安裝內容轉移工具(CTT)版本，並支援AzCopy {#install-ctt-azcopy-support}

CTT 1.5.4版中包含了AzCopy支援。 您可以從[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)入口網站下載最新版的CTT。

### 3.設定azcopy.config檔案 {#configure-azcopy-config-file}

在來源AEM例項中，在crx-quickstart/cloud-migration中，建立名為azcopy.config的新檔案。

此設定檔案的內容會因您的來源AEM例項是否使用Azure或Amazon S3資料存放區而異。

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

### 4.使用AzCopy提取 {#extracting-azcopy}

在配置了上述配置檔案後，AzCopy預複製階段將作為後續提取的一部分運行。 若要防止其執行，您可以重新命名此檔案或將其移除。

1. 從CTT UI開始擷取。 如需詳細資訊，請參閱[執行內容轉移工具](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#running-tool)和[提取程式](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#extraction-process)。
1. 確認以下行已打印在提取日誌中：

```
c.a.g.s.m.commons.ContentExtractor - *************** Beginning AzCopy Pre-Copy phase ***************
```

恭喜！ 此日誌條目表示您的配置被視為有效，並且AzCopy當前正在將源容器中的所有Blob複製到遷移容器。

來自AzCopy的日誌條目將出現在提取日誌中，並且前置詞為c.a.g.s.m.c.azcopy.AzCopyBlobPreCopy - [AzCopy pre-copy]

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

### 5.使用AzCopy獲取 {#ingesting-azcopy}

隨著內容轉移工具1.5.4的推出，我們為製作擷取新增了AzCopy支援。

>[!NOTE]
>建議先單獨執行「作者」擷取。 這會在稍後執行時加速發佈擷取。

為了在獲取過程中利用AzCopy，我們要求您使用至少2021.6.5561版的AEMas a Cloud Service版。

從CTT UI開始擷取作者。 如需詳細資訊，請參閱[擷取程式](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#ingestion-process)。
AzCopy中的日誌條目將出現在獲取日誌中。 它們看起來會像這樣：

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
