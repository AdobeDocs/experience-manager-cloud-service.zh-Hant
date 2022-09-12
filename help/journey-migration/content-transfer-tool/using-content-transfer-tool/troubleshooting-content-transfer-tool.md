---
title: 疑難排解內容轉移工具
description: 疑難排解內容轉移工具
exl-id: 01bc9be7-a576-45eb-90a0-386ea951040d
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 93%

---

# 疑難排解內容轉移工具 {#troubleshoot-content-transfer-tool}


## 遺失 Blob ID {#missing-blobs}

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


## UI 行為 {#ui-behavior}

身為使用者，您可能會在「內容轉移工具」的使用者介面 (UI) 中看到下列行為變更：

* 「內容轉移工具」UI 中的圖示可能與本指南中顯示的螢幕擷圖不同，也可能完全不顯示 (取決於來源 AEM 例項的版本)。
