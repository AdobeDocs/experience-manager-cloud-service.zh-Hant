---
title: 使用內容轉移工具
description: 使用內容轉移工具
exl-id: a19b8424-33ab-488a-91b3-47f0d3c8abf5
source-git-commit: 5b569ab1b1cca7e5ec46b872f8726fddfc8b8d14
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 57%

---

# 使用內容轉移工具 {#using-content-transfer-tool}

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
