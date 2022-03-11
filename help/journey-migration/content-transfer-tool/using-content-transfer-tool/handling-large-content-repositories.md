---
title: 處理大型內容儲存庫
description: 本節介紹大型內容儲存庫的處理
exl-id: 21bada73-07f3-4743-aae6-2e37565ebe08
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1739'
ht-degree: 1%

---

# 處理大型內容儲存庫 {#handling-large-content-repositories}

## 概覽 {#overview}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_precopy"
>title="處理大型內容儲存庫"
>abstract="為顯著加快內容傳輸活動的提取和接收階段以將內容移到AEMas a Cloud Service,CTT可以利用AzCopy作為可選的預複製步驟。 配置此前步驟後，在提取階段，AzCopy將Blob從AmazonS3或Azure Blob儲存複製到遷移集blob儲存區。 在接收階段，AzCopy將Blob從遷移集Blob儲存區複製到目標AEMas a Cloud ServiceBlob儲存區。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#setting-up-pre-copy-step" text="作為預複製步驟開始使用AzCopy"

使用內容傳輸工具(CTT)複製大量Blo可能需要多天時間。
為顯著加快內容傳輸活動的提取和接收階段，以將內容移動到AEMas a Cloud Service, CTT可以利用 [可用區複製](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) 作為可選的預複製步驟。 在將源實例配置為使用AmazonS3、Azure Blob儲存資料儲存AEM區或檔案資料儲存區時，可以使用此預複製步驟。 配置此前步驟後，在提取階段，AzCopy將Blob從AmazonS3、Azure Blob儲存或檔案資料儲存複製到遷移集blob儲存。 在接收階段，AzCopy將Blob從遷移集Blob儲存區複製到目標AEMas a Cloud ServiceBlob儲存區。

>[!NOTE]
> 此功能已在CTT 1.5.4版中引入。

## 開始之前的重要注意事項 {#important-considerations}

在開始之前，請按照以下部分瞭解重要注意事項：

* 源AEM版本需要為6.3 - 6.5。

* 源數AEM據儲存已配置為使用AmazonS3或Azure Blob儲存。 有關詳細資訊，請參閱 [在6中配置節點儲存和數AEM據儲存](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html?lang=en)。

* 每個遷移集都將複製整個資料儲存，因此只應使用一個遷移集。

* 您需要訪問才能安裝 [可用區複製](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) 在運行源實例的實例（或VM）AEM上。

* 資料儲存垃圾收集已在源上的前7天內運行。 有關詳細資訊，請參閱 [資料儲存垃圾收集](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html?lang=en#data-store-garbage-collection)。


### 如果將源實例AEM配置為使用AmazonS3或Azure Blob儲存資料儲存，則需要考慮其他事項 {#additional-considerations-amazons3-azure}

* 因為從AmazonS3和Azure Blob儲存中傳輸資料有相關的成本，因此傳輸成本將與儲存容器中的資料總量(無論是否在中引用AEM)相關。 請參閱 [AmazonS3](https://aws.amazon.com/s3/pricing/) 和 [Azure Blob儲存](https://azure.microsoft.com/en-us/pricing/details/bandwidth/) 的子菜單。

* 您需要源AmazonS3儲存桶的訪問密鑰和密鑰對，或源Azure Blob儲存容器的SAS URI（只讀訪問可行）。

### 如果將源實例AEM配置為使用檔案資料儲存，則需考慮其他事項 {#additional-considerations-aem-instance-filedatastore}

* 本地系統的可用空間必須嚴格大於源資料儲存的1/256大小。 例如，如果資料儲存的大小為3 TB，則中必須存在大於11.72 GB的可用空間 `crx-quickstart/cloud-migration` 資料夾。 源系統至少應有1 GB的可用空間。 可以通過使用 `df -h` 命令，以及Windows實例中的dir命令。

* 每次在啟用AzCopy的情況下運行提取時，整個檔案資料儲存都會展平並複製到雲遷移容器。 如果您的遷移集大大小於資料儲存的大小，則AzCopy提取不是最佳方法。

* 一旦AzCopy用於通過資料儲存進行複製，請禁用它進行增量或向上提取。

## 設定為將AzCopy用作預複製步驟 {#setting-up-pre-copy-step}

請按照本節的說明，瞭解如何設定將AzCopy作為內容傳輸工具的預複製步驟，將內容遷移到AEMas a Cloud Service:

### 0。確定資料儲存中所有內容的總大小 {#determine-total-size}

確定資料儲存的總大小非常重要，原因有二：

* 如果將源AEM配置為使用檔案資料儲存，則本地系統的可用空間必須嚴格大於源資料儲存的1/256大小。

* 瞭解資料儲存的總大小有助於估計提取和攝取時間。 使用 [內容傳輸工具計算器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-implementation-phase.html?lang=en#content-transfer) 在 [雲加速管理器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/introduction-cam/overview-cam.html?lang=en) 來估計提取和攝取時間。

#### Azure Blob儲存資料儲存 {#azure-blob-storage}

從Azure門戶中的容器屬性頁，使用 **計算大小** 按鈕確定容器中所有內容的大小。 例如：

![影像](/help/journey-migration/content-transfer-tool/assets/Azure-blob-storage-data-store.png)

#### AmazonS3資料儲存 {#amazon-data}

可以使用容器的「度量」頁籤來確定容器中所有內容的大小。 例如：


![影像](/help/journey-migration/content-transfer-tool/assets/amazon-s3-data-store.png)

#### 檔案資料存放區 {#file-data-store-determine-size}

* 對於mac、UNIX系統，在資料儲存目錄上運行du命令以獲取其大小：
   `du -sh [path to datastore on the instance]`. 例如，如果資料儲存位於 `/mnt/author/crx-quickstart/repository/datastore`，以下命令將使其大小： `du -sh /mnt/author/crx-quickstart/repository/datastore`。

* 對於Windows，使用資料儲存目錄上的dir命令獲取其大小：
   `dir /a/s [location of datastore]`。

### 1。安裝AzCopy {#install-azcopy}

[可用區複製](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) 是Microsoft提供的命令行工具，需要在源實例上提供該工具才能啟用此功能。

簡而言之，您很可能希望從 [AzCopy文檔頁](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) 並將其卸載到/usr/bin等位置。

>[!IMPORTANT]
>請注意二進位檔案的放置位置，因為在稍後的步驟中需要該二進位檔案的完整路徑。

### 2.安裝支援AzCopy的內容傳輸工具(CTT)版本 {#install-ctt-azcopy-support}

CTT 1.5.4版中包含對AmazonS3和Azure Blob儲存的AzCopy支援。
CTT 1.7.2版中包含對檔案資料儲存的支援。您可以從 [軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) 門戶。


### 3.配置azcopy.config檔案 {#configure-azcopy-config-file}

在源實AEM例上，在 `crx-quickstart/cloud-migration`，建立名為 `azcopy.config`。

>[!NOTE]
>此配置檔案的內容將因源實例是使用Azure還是AmazonAEM S3資料儲存還是檔案資料儲存而異。

#### Azure Blob儲存資料儲存 {#azure-blob-storage-data}

您的azcopy.config檔案應包括以下屬性（確保將正確的azCopyPath和azureSas用於實例）。

>[!NOTE]
>
> 如果您不願授予對Blob儲存容器的寫訪問權限，則可以生成只具有讀取和清單權限的新SAS URI。

```
azCopyPath=/usr/bin/azcopy
azureSas=https://example-resource.blob.core.windows.net/example-container?sig=--REDACTED--
```

#### AmazonS3資料儲存 {#amazon-sdata-store}

azcopy.config檔案應包括以下屬性（確保為實例使用正確的值）。

>[!NOTE]
>
> 如果實例使用IAM角色AEM來啟用對S3的訪問，則您需要建立策略和用戶，並為S3儲存段啟用ListBucket和GetObject操作。 設定後，請使用此用戶的訪問密鑰和密鑰。

```
azCopyPath=/usr/bin/azcopy
s3Bucket=aem-63
s3Region=us-west-2
s3AccessKey=--REDACTED--
s3SecretKey=--REDACTED--
```

#### 檔案資料存放區 {#file-data-store-azcopy-config}

您 `azcopy.config` 檔案必須包含azcopyPath屬性和指向檔案資料儲存庫位置的可選repository.home屬性。 為實例使用正確的值。
檔案資料存放區

```
azCopyPath=/usr/bin/azcopy
repository.home=/mnt/crx/author/crx-quickstart/repository/datastore
```

azcopyPath屬性必須包含源實例上安裝azCopy命令行工具的位置的完整路AEM徑。 如果azCopyPath屬性缺失，將不執行blob預複製步驟。

如果 `repository.home` azcopy.config中缺少屬性，則預設資料儲存位置 `/mnt/crx/author/crx-quickstart/repository/datastore` 將用於執行預複製。

### 4.使用AzCopy提取 {#extracting-azcopy}

在配置檔案到位後，AzCopy預複製階段將作為後續提取的一部分運行。 要防止該檔案運行，可以更名或刪除該檔案。

>[!NOTE]
>如果AzCopy未正確配置，您將在日誌中看到以下消息：
>`INFO c.a.g.s.m.c.a.AzCopyCloudBlobPreCopy - Blob pre-copy is not supported`。

1. 開始從CTT UI中提取。 請參閱 [內容傳輸工具入門](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en) 和 [提取過程](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/extracting-content.html?lang=en) 的子菜單。

1. 確認提取日誌中打印了以下行：

```
c.a.g.s.m.commons.ContentExtractor - *************** Beginning AzCopy Pre-Copy phase ***************
```

恭喜！ 此日誌條目表示您的配置被視為有效，並且AzCopy當前正在將源容器中的所有Blob複製到遷移容器。

AzCopy中的日誌條目將出現在提取日誌中，並將以c.a.g.s.m.c.azcopy.AzCopyBlobPreCopy為前置詞 —  [AzCopy預拷貝]

>[!CAUTION]
>
> 在提取的最初幾分鐘，請仔細觀察提取日誌，以發現任何問題的跡象。 例如，如果找不到源Azure容器，將記錄以下內容：

```
[AzCopy pre-copy] failed to perform copy command due to error: cannot start job due to error: cannot list files due to reason -> github.com/Azure/azure-storage-blob-go/azblob.newStorageError, github.com/Azure/azure-storage-blob-go@v0.10.1-0.20210407023846-16cf969ec1c3/azblob/zc_storage_error.go:42
[AzCopy pre-copy] ===== RESPONSE ERROR (ServiceCode=ContainerNotFound) =====
[AzCopy pre-copy] Description=The specified container does not exist.
[AzCopy pre-copy] RequestId:5fb674b9-201e-001b-2a5b-527400000000
[AzCopy pre-copy] Time:2021-05-26T18:18:07.5931967Z, Details: 
[AzCopy pre-copy] Code: ContainerNotFound
```

如果AzCopy出現問題，提取將立即失敗，提取日誌將包含有關失敗的詳細資訊。

AzCopy將在後續運行中自動跳過在錯誤之前複製的任何Blob，並且不需要再次複製。

#### 對於檔案資料儲存 {#file-data-store-extract}

當AzCopy為源檔案資料儲存運行時，您應在日誌中看到以下消息：
`c.a.g.s.m.c.a.AzCopyFileSourceBlobPreCopy - [AzCopy pre-copy] Processing folder (1/24) crx-quickstart/repository/datastore/5d`

### 5.使用AzCopy插入 {#ingesting-azcopy}

隨著內容傳輸工具1.5.4的發佈，我們為Author接收添加了AzCopy支援。

>[!NOTE]
>建議先單獨運行Author攝取。 這將在稍後運行「發佈」接收時加速。

要在接收期間利用AzCopy，我們要求您使用AEM至少版本2021.6.5561的as a Cloud Service版本。

從CTT UI開始提交程式。 請參閱 [攝取過程](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/ingesting-content.html?lang=en) 的子菜單。
來自AzCopy的日誌條目將出現在接收日誌中。 他們會這樣：

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

要禁用AzCopy，請更名或刪除 `azcopy.config` 的子菜單。

例如，可以通過以下方式禁用azcopy提取： `mv /mnt/crx/author/crx-quickstart/cloud-migration/azcopy.config /mnt/crx/author/crx-quickstart/cloud-migration/noazcopy.config`。

## 下一步是什麼 {#whats-next}

學習「處理大型內容儲存庫」以顯著加快內容傳輸活動的提取和接收階段以將內容移到AEMas a Cloud Service後，您現在已準備好學習內容傳輸工具中的提取過程。 請參閱 [在內容傳輸工具中從源中提取內容](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md) 瞭解如何從內容傳輸工具中提取遷移集。
