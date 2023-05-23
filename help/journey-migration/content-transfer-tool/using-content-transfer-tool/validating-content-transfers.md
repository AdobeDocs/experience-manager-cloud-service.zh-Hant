---
title: 驗證內容轉移
description: 使用內容傳輸工具驗證內容傳輸
exl-id: a12059c3-c15a-4b6d-b2f4-df128ed0eea5
source-git-commit: c1f60a1ead466b47694b8918e5b39011041c5f25
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 2%

---

# 驗證內容轉移 {#validating-content-transfers}

## 快速入門 {#getting-started}

用戶能夠可靠地確定內容傳輸工具提取的所有內容是否已成功地被攝取到目標實例中。 此驗證功能通過比較提取過程中涉及的所有節點的路徑摘要和接收過程中涉及的所有節點的路徑摘要來工作。 如果提取摘要中包含的任何節點路徑在攝取摘要中缺失，則認為驗證已失敗，可能需要進行額外的手動驗證。

>[!INFO]
>
>此功能將在內容傳輸工具(CTT)1.8.x版中提供。 AEM Cloud Service目標環境必須至少運行6158版或更高版本。 它還要求設定源環境以運行 [預拷貝](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#setting-up-pre-copy-step)。 驗證功能在源上查找azcopy.config檔案。 如果找不到此檔案，則驗證將不運行。 要瞭解有關如何配置azcopy.config檔案的詳細資訊，請參見 [此頁](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#configure-azcopy-config-file)。

驗證內容傳輸是一項可選功能。 啟用此功能將增加執行提取和攝取所花的時間。 要使用該功能，請按照以下步驟在源環境的系統控制台AEM中啟用該功能：

1. 轉到源實例上的Adobe Experience ManagerWeb控制台 **工具 — 操作 — Web控制台** 或直接到URL *https://serveraddress:serverport/system/console/configMgr*
1. 搜索 **內容傳輸工具抽取服務配置**
1. 使用鉛筆表徵圖按鈕編輯其配置值
1. 啟用 **在提取期間啟用遷移驗證** 設定，然後按 **保存**:

   ![影像](/help/journey-migration/content-transfer-tool/assets/CTTvalidation1.png)

啟用此設定並且目標AEM Cloud Service環境運行相容版本後，將在後續的所有提取和接收過程中進行遷移驗證。

有關如何安裝內容傳輸工具的詳細資訊，請參見 [內容傳輸工具入門](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md)。

## 如何驗證內容傳輸 {#how-to-validate-a-content-transfer}

在源環境上啟用遷移驗AEM證後，開始提取。

如果 **提取期間覆蓋暫存容器** 啟用後，所有與提取相關的節點都將記錄到提取路徑摘要中。 使用此設定時，啟用 **在接收之前擦除雲實例上的現有內容** 設定，否則可能會在攝取摘要中缺少節點。 這些節點是以前接收中在目標上已存在的節點。

有關此問題的圖形說明，請參閱以下示例：

### 範例 1 {#example-1}

* **提取（覆蓋）**

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/validation-01.png)

* **攝取（擦除）**

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/validation-02.png)

* **附註**

   「覆蓋」和「擦除」的這種組合將導致一致的驗證結果，即使對於重複的接收也是如此。

### 範例 2 {#example-2}

* **擷取**

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/validation-03.png)

* **攝取**

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/validation-04.png)

* **附註**

   「覆蓋」和「擦除」的這種組合將導致初始攝取的驗證結果一致。

   如果重複攝取，則攝取摘要將為空，驗證似乎已失敗。 接收摘要將為空，因為此提取中的所有節點都已存在於目標上。

提取完成後，開始攝取。

接收日誌頂部將包含一個條目，類似於 `aem-ethos/tools:1.2.438`。 確保此版本號為 **1.2.438** 或更高版本，否則您使用的AEMas a Cloud Service版本不支援驗證。

一旦接收完成並驗證開始，將在接收日誌中記錄以下日誌條目：

```
Gathering artifacts for migration validation...
```

驗證的詳細資訊將跟隨此條目。 從以下大型遷移中查找示例：

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

這是已成功驗證的示例，因為提取摘要中不存在攝取摘要中缺少的條目。

要進行比較，以下是驗證報告在驗證失敗時的看法：

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

上述故障示例是通過運行攝取，然後在禁用擦除的情況下再次運行相同的攝取，以便在攝取期間不涉及節點 — 目標上已存在所有內容。

除了包含在接收日誌中，還可以從 **攝取作業** Cloud Acceleration Manager中的用戶介面。 為此，請按一下三點(**...**)，然後按一下 **驗證報告** 的子菜單。


![影像](/help/journey-migration/content-transfer-tool/assets-ctt/CTTvalidationreportnew.png)

## 如何驗證主遷移 {#how-to-validate-principal-migration}

請參閱 [用戶映射和主遷移](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md) 閱讀主遷移詳細資訊以及需要遷移的原因。

一旦提取和攝取成功完成，將提供主遷移的摘要和報告。 此資訊可用於驗證哪些用戶和組已成功遷移，或許還可用於確定為什麼沒有遷移。

要查看此資訊，請轉至Cloud Acceleration Manager。 按一下項目卡，然後按一下內容傳輸卡。 導航到 **攝取作業** 找到要驗證的攝取。 按一下三點(**...**)，然後按一下 **查看主體摘要** 中。

![影像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-principal-action.png)

您將看到一個包含摘要資訊的對話框。 使用幫助表徵圖可閱讀更完整的說明。 按一下 **下載報告** 按鈕來下載完整的逗號分隔(CSV)報告。

![影像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-principal-dialog.png)

>[!NOTE]
>
>如果禁用用戶映射，則將顯示此對話框的另一個變體。 它將指示禁用了用戶映射，並且不會顯示提供用戶映射值的3個欄位。

## 疑難排解 {#troubleshooting}

### 驗證失敗. 現在怎麼辦？ {#validation-fail}

第一步是確定攝入是否確實失敗，或提取的內容是否已存在於目標環境中。 如果與 **在接收之前擦除雲實例上的現有內容** 選項。

要驗證，請從驗證報告中選擇一個路徑，然後檢查該路徑是否存在於目標環境中。 如果這是發佈環境，則您可能僅限於直接檢查頁面和資產。 如果您需要此步驟的幫助，請與客戶服務部門開啟票證。

### 節點計數低於我預期。 為什麼？ {#node-count-lower-than-expected}

有目的地排除抽取和攝取摘要中的某些路徑，以保持這些檔案的大小可管理，目標是能夠在攝取完成後的兩小時內計算遷移驗證結果。

當前從摘要中排除的路徑包括： `cqdam.text.txt` 格式副本，節點 `/home`，以及 `/jcr:system`。
