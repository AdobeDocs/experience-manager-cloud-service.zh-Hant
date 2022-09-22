---
title: 驗證內容傳輸
description: 使用「內容轉移工具」來驗證內容轉移
exl-id: a12059c3-c15a-4b6d-b2f4-df128ed0eea5
source-git-commit: 015f3b0232861ac961922245650cb02db44daf77
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 驗證內容傳輸 {#validating-content-transfers}

## 快速入門 {#getting-started}

使用者能夠可靠判斷「內容轉移工具」擷取的所有內容是否已成功內嵌至目標例項。 此驗證功能的運作方式是比較提取期間所涉及所有節點的路徑摘要，以及擷取期間所涉及所有節點的路徑摘要。 如果擷取摘要中包含的任何節點路徑從擷取摘要中遺失，則會將驗證視為失敗，且可能需要進行額外的手動驗證。

>[!INFO]
>
>自內容轉移工具(CTT)1.8.x版發行起，即可使用此功能。 AEM Cloud Service目標環境至少必須執行6158版或更新版本。 還需要設定源環境才能運行 [預復](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#setting-up-pre-copy-step). 驗證功能會在來源上尋找azcopy.config檔案。 如果找不到此檔案，則不會運行驗證。 若要進一步了解如何設定azcopy.config檔案，請參閱 [本頁](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#configure-azcopy-config-file).

驗證內容轉移是選用功能。 啟用此功能將增加執行提取和擷取所需的時間。 若要使用此功能，請依照下列步驟，在來源AEM環境的「系統主控台」中啟用此功能：

1. 導覽至來源例項上的Adobe Experience Manager Web Console，方法是前往 **工具 — 操作 — Web控制台** 或直接傳至URL() *https://serveraddress:serverport/system/console/configMgr*
1. 搜尋 **內容轉移工具提取服務設定**
1. 使用鉛筆圖示按鈕來編輯其設定值
1. 啟用 **在提取期間啟用遷移驗證** 設定，然後按 **儲存**:

   ![影像](/help/journey-migration/content-transfer-tool/assets/CTTvalidation1.png)

啟用此設定，且目標AEM Cloud Service環境執行相容的版本後，所有後續的擷取和擷取作業都會進行移轉驗證。

如需如何安裝「內容轉移工具」的詳細資訊，請參閱 [內容轉移工具快速入門](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md).

## 如何驗證內容轉移 {#how-to-validate-a-content-transfer}

在來源AEM環境上啟用移轉驗證後，開始擷取。

若 **提取期間覆寫預備容器** 啟用後，所有與提取相關的節點將記錄到提取路徑摘要中。 使用此設定時，請務必啟用 **擷取前先擦去雲端例項上的現有內容** 擷取期間進行設定，否則擷取摘要中可能會有節點遺失。 這些節點已存在於目標上，且來自先前擷取。

如需此項目的圖形圖示，請參閱下列範例：

### 範例1 {#example-1}

* **提取（覆寫）**

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/validation-01.png)

* **擷取（擦去）**

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/validation-02.png)

* **附註**

   這種「覆寫」和「擦去」的組合將產生一致的驗證結果，即使重複擷取亦然。

### 範例2 {#example-2}

* **擷取**

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/validation-03.png)

* **擷取**

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/validation-04.png)

* **附註**

   此「覆寫」和「擦去」的組合將產生初始擷取的一致驗證結果。

   如果重複擷取，擷取摘要將會是空的，且驗證似乎已失敗。 擷取摘要將為空，因為此擷取中的所有節點都已存在於目標上。

提取一旦完成，即開始擷取。

擷取記錄頂端將包含項目，類似於 `aem-ethos/tools:1.2.438`. 請確定此版本號碼為 **1.2.438** 或更新版本，否則您所使用的AEM as a Cloud Service版不支援驗證。

擷取完成且驗證開始後，擷取記錄中會記錄下列記錄項目：

```
Gathering artifacts for migration validation...  
```

驗證的詳細資訊將遵循此項。 請尋找下列大型移轉的範例：

```
Beginning publish migration validation. Migration job id=[3aba1f96-84b6-4bd0-8642-c61c0d528387]
Extraction path digest is being processed...
Extraction path digest processing took 982 seconds
Ingestion path digest is being processed...
Ingestion path digest processing took 999 seconds
Comparing the Extraction and Ingestion path digests...
----------------------------------------------------------
EXTRACTION: Number of nodes extracted: 51674784
INGESTION: Number of nodes ingested: 51674784
----------------------------------------------------------
Validation succeeded! No entries were detected to be missing from the ingestion digest.
----------------------------------------------------------
Comparing the path digests took 29 seconds
Migration validation took 33 minutes
```

這是已成功驗證的範例，因為擷取摘要中沒有遺漏任何存在於擷取摘要中的項目。

若要比較，驗證報表在驗證失敗時的外觀如下：

```
Beginning publish migration validation. Migration job id=[ac217e5a-a08d-4e81-cbd6-f39f88b174ce]
Extraction path digest is being processed...
Extraction path digest processing took 0 seconds
Ingestion path digest is being processed...
Ingestion path digest processing took 0 seconds
Comparing the Extraction and Ingestion path digests...
----------------------------------------------------------
EXTRACTION: Number of nodes extracted: 4635
INGESTION: Number of nodes ingested: 0
----------------------------------------------------------
Validation failed. However, the following nodes may already be present in the target environment.
Please refer to our Migration Validation FAQ (https://www.adobe.com/go/aem_cloud_ctt_validation_en) or open a ticket with Customer Care.
There are 4635 entries present in the extraction digest that are missing from the ingestion digest.
/content/dam/bruce
/content/dam/bruce-assets
... more paths listed (up to 10k) ...
----------------------------------------------------------
Comparing the path digests took 0 seconds
Migration validation took 0 minutes
```

上述失敗範例是透過執行擷取來達成，然後在停用「擦去」的情況下重新執行相同的擷取，如此一來擷取期間就不會涉及任何節點 — 目標上已存在所有內容。

除了包含在擷取記錄中，驗證報表也可從 **擷取工作** Cloud Acceleration Manager中的使用者介面。 若要這麼做，請按一下三個點(**...**)，然後按一下 **驗證報表** ，檢視驗證報表。


![影像](/help/journey-migration/content-transfer-tool/assets-ctt/CTTvalidationreportnew.png)

## 疑難排解 {#troubleshooting}

### 驗證失敗. 現在呢？ {#validation-fail}

第一步是判斷擷取是否確實失敗，或擷取的內容是否已存在於目標環境中。 如果對 **擷取前先擦去雲端例項上的現有內容** 選項已禁用。

若要驗證，請從驗證報表中選擇路徑，並檢查其是否存在於目標環境中。 如果這是發佈環境，您可能受限於僅能直接檢查頁面和資產。 如果您需要此步驟的協助，請向客戶服務開立票證。

### 節點計數低於我的預期。 為什麼？ {#node-count-lower-than-expected}

系統會有目的地排除擷取和擷取摘要中的某些路徑，以便讓這些檔案的大小保持可管理，目標是能夠在擷取完成後的兩小時內計算移轉驗證結果。

當前從摘要中排除的路徑包括： `cqdam.text.txt` 轉譯，內的節點 `/home`，以及 `/jcr:system`.
