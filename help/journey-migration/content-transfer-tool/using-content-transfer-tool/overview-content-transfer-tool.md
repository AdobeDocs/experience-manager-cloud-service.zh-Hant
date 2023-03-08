---
title: 內容轉移工具綜覽
description: 內容轉移工具綜覽
exl-id: cfc0366a-2139-4d9d-b5bc-0b65bef4013c
source-git-commit: 5a4592531377109fba88b5cdc9df027803feca7a
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 47%

---

# 概觀 {#overview-content-transfer-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_overview"
>title="概觀"
>abstract="「內容轉移工具」是由Adobe開發的工具，可用來將現有內容從來源AEM例項（內部部署或AMS）移至目標AEM Cloud Service例項。 此工具也會自動轉移主體 (使用者或群組)。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html" text="准則與最佳作法"

「內容轉移工具」是 Adobe 開發的工具，可用來將現有內容從來源 AEM 例項 (內部部署或 AMS) 移至目標 AEM 雲端服務例項。

此工具也會自動轉移主體 (使用者或群組)。

新版「內容轉移工具」已推出，其整合了內容轉移程式與Cloud Acceleration Manager。 強烈建議您切換至此新版本，以充分運用其提供的所有優點：

* 自助式方式，只需擷取一次移轉集，並同時內嵌至多個環境
* 透過更好的載入狀態、護欄和錯誤處理改善使用者體驗
* 擷取記錄會持續存在，且隨時都可用於疑難排解

若要開始使用新版本，您需要解除安裝舊版「內容轉移工具」，因為工具的架構有重大變更。

>[!NOTE]
>
> 若移轉作業已在進行中，您可以繼續使用舊版CTT，直到移轉完成為止。 如需與舊版CTT相關的檔案，請參閱 [舊版檔案](/help/journey-migration/content-transfer-tool/ctt-legacy/overview-content-transfer-tool-legacy.md).

## 內容轉移工具中的階段 {#phases-content-transfer-tool}

有兩個階段與內容轉移相關聯：

1. **提取**：提取指的是從來源 AEM 例項提取內容，並存放至名為&#x200B;*移轉集*&#x200B;的暫存區域。*移轉集*&#x200B;是 Adobe 提供的雲端儲存空間，可供暫時儲存在來源 AEM 例項與雲端服務 AEM 例項間轉移的內容。

   如需詳細資訊，請參考[內容轉移中的提取程序](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md)。

   >[!NOTE]
   >使用者對應現在會在製作的提取階段期間自動執行（但可選擇在製作時停用，或在發佈時啟用）。 請參閱 [用戶映射和主體遷移](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md) 以取得更多詳細資訊。

1. **擷取**：擷取指的是從&#x200B;*移轉集*&#x200B;擷取內容，並存放至目標雲端服務例項。

   請參閱 [內容轉移中的擷取程式](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) 以取得更多詳細資訊。

## 移轉集的屬性 {#attributes-migration-set}

移轉集有下列屬性：

* 透過新版本，您可以在Cloud Acceleration Manager中建立的專案中，最多建立5個移轉集。
* 每個移轉集的名稱必須是唯一的。

「內容轉移工具」具備支援追加差異內容的功能，可以只轉移在上一次內容轉移活動後所進行的變更。

>[!NOTE]
>初始轉移內容後，建議您先頻繁地執行追加差異內容，以縮短最終差異化內容轉移的內容凍結時間，然後再於雲端服務上線。

如果要在提取階段中&#x200B;***追加***&#x200B;現有的移轉集，則必須停用&#x200B;*覆蓋*&#x200B;選項。如需詳細資訊，請參考[追加提取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)。

如果要在擷取階段中，將差異內容套用至目前內容的頂端，則必須停用&#x200B;*「擦去」*&#x200B;選項。如需詳細資訊，請參考[追加擷取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process)。

## 下一步 {#whats-next}

了解「內容轉移工具」及其概觀（說明此工具）後，您就必須檢閱，才能將現有內容從來源AEM例項（內部部署或AMS）移至目標AEM Cloud Service例項 [內容轉移工具的必要條件](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/prerequisites-content-transfer-tool.md).
