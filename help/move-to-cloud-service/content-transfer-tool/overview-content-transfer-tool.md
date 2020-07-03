---
title: 內容轉移工具綜覽
description: 內容轉移工具綜覽
translation-type: tm+mt
source-git-commit: 7648adc4b1d9c5849363beb4162de2f42eac7cfd
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 69%

---


# 概覽 {#overview-content-transfer-tool}

「內容轉移工具」是 Adobe 開發的工具，可用來將現有內容從來源 AEM 例項 (內部部署或 AMS) 移至目標 AEM 雲端服務例項。

此工具也會自動轉移主體 (使用者或群組)。

有兩個階段與內容轉移相關聯：

1. **提取**：提取指的是從來源 AEM 例項提取內容，並存放至名為&#x200B;*移轉集*&#x200B;的暫存區域。*移轉集*&#x200B;是 Adobe 提供的雲端儲存空間，可供暫時儲存在來源 AEM 例項與雲端服務 AEM 例項間轉移的內容。

   如需詳細資訊，請參考[內容轉移中的提取程序](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#extraction-process)。

2. **擷取**：擷取指的是從&#x200B;*移轉集*&#x200B;擷取內容，並存放至目標雲端服務例項。

   如需詳細資訊，請參考[內容轉移中的擷取程序](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#ingestion-process)。

*移轉集*&#x200B;有下列屬性：

* 在內容轉移活動期間，最多可以一次建立並維護四個移轉集。
* 每個移轉集的名稱必須是唯一的。
* 如果移轉集已停用超過 30 天，則會自動刪除。
* 無論何時建立移轉集，它都與特定環境有關聯。您只能將內容擷取至相同環境中的製作或發佈例項。

「內容轉移工具」具備支援追加差異內容的功能，可以只轉移在上一次內容轉移活動後所進行的變更。

>[!NOTE]
> 初始轉移內容後，建議您先頻繁地執行追加差異內容，以縮短最終差異化內容轉移的內容凍結時間，然後再於雲端服務上線。

如果要在提取階段中&#x200B;***追加***&#x200B;現有的移轉集，則必須停用&#x200B;*覆蓋*&#x200B;選項。如需詳細資訊，請參考[追加提取](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#top-up-extraction-process)。

如果要在擷取階段中，將差異內容套用至目前內容的頂端，則必須停用&#x200B;*「擦去」*&#x200B;選項。如需詳細資訊，請參考[追加擷取](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#top-up-ingestion-process)。


## 准則與最佳作法 {#best-practices}

請依照以下章節了解使用「內容轉移工具」的准則與最佳作法：

* 建議在源儲存庫上 [運行「修訂清理](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/deploying/revision-cleanup.html) 」和 [](https://helpx.adobe.com/experience-manager/kb/How-to-run-a-datastore-consistency-check-via-oak-run-AEM.html)**** 「資料儲存一致性檢查」，以發現潛在問題並減少儲存庫的大小。

* 如果AEM Cloud作者內容傳送網路(CDN)設定已設定為擁有IP的白名單，則應確保來源環境IP也新增至allowlist，如此來源環境與AEM Cloud環境就可以彼此通訊。

* 在擷取階段中，建議使用&#x200B;*擦去*&#x200B;模式來執行擷取，讓目標 AEM 雲端服務環境中的現有存放庫 (製作或發佈) 被完全刪除，然後以移轉集資料更新。此模式比非擦去模式快速許多，因為在非擦去模式中，移轉集會套用在目前內容的頂端。

* 內容轉移活動完成後，雲端服務環境將需要正確的專案結構，以確保內容在雲端服務環境中成功轉譯。

* 在執行「內容傳輸工具」之前，您必須確定來源AEM例項的子目錄中 `crx-quickstart` 有足夠的磁碟空間。 這是因為內容傳輸工具建立了儲存庫的本地副本，該副本稍後將上載到遷移集。
計算所需可用磁碟空間的一般公式如下：
   `data store size + node store size * 1.5`

   * *資料儲存大小*: 內容傳輸工具使用64 GB，即使實際資料儲存空間較大。
   * *節點儲存大小*: 段儲存目錄大小或MongoDB資料庫大小。
因此，若區段儲存區大小為20GB，則需要的可用磁碟空間為94GB。