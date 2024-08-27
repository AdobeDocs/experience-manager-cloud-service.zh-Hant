---
title: 內容轉移工具綜覽
description: 瞭解如何使用「內容轉移工具」，將內容從內部部署AEM例項轉移至AEM as a Cloud Service
exl-id: cfc0366a-2139-4d9d-b5bc-0b65bef4013c
feature: Migration
role: Admin
source-git-commit: d9565e86c4b7e513cb1a95ecbe7a30c9586d9fb1
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 38%

---

# 概觀 {#overview-content-transfer-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_overview"
>title="概觀"
>abstract="「內容轉移工具」是 Adobe 開發的工具，可用來起始將現有內容從來源 AEM 執行個體 (內部部署或 AMS) 移轉至目標 AEM Cloud Service 執行個體的作業。此工具也會自動轉移主體 (使用者或群組)。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html" text="準則和最佳做法"

「內容轉移工具」是Adobe開發的工具，可用來起始將現有內容從來源AEM例項（內部部署或AMS）移轉至目標AEM Cloud Service例項的作業。

此工具也會自動轉移主體（使用者或群組）。  如需詳細資訊，請參閱[使用者對應和主體移轉](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md)。

「內容轉移工具」整合了內容轉移程式與Cloud Acceleration Manager。 這可讓使用者享有其提供的所有優點：

* 自助式方式擷取一次移轉集，並同時將其擷取至多個環境中
* 透過更好的載入狀態、護欄和錯誤處理，改善使用者體驗
* 內嵌記錄檔會持續存在，且隨時可用於疑難排解
* 驗證和主要移轉報告可用於驗證

## 內容轉移工具中的階段 {#phases-content-transfer-tool}

有兩個階段與內容轉移相關聯：

1. **提取**：提取指的是從來源 AEM 例項提取內容，並存放至名為&#x200B;*移轉集*&#x200B;的暫存區域。*移轉集*&#x200B;是 Adobe 提供的雲端儲存空間，可供暫時儲存在來源 AEM 例項與雲端服務 AEM 例項間轉移的內容。

   如需詳細資訊，請參閱內容轉移中的[擷取程式](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md)。

   >[!NOTE]
   >現在，使用者對應會在作者上的擷取階段中自動執行（但可選擇在作者上停用或在發佈上啟用）。 如需詳細資訊，請參閱[使用者對應和主體移轉](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md)。

1. **擷取**：擷取指的是從&#x200B;*移轉集*&#x200B;擷取內容，並存放至目標雲端服務例項。

   如需詳細資訊，請參閱內容轉移](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)中的[擷取程式。

## 移轉集的屬性 {#attributes-migration-set}

移轉集有下列屬性：

* 透過新版本，您可以在Cloud Acceleration Manager中建立的專案中建立最多十個移轉集。
* 每個移轉集的名稱必須是唯一的。

「內容轉移工具」具備支援追加差異內容的功能，可以只轉移在上一次內容轉移活動後所進行的變更。

>[!NOTE]
>初始轉移內容後，建議您先頻繁地執行追加差異內容，以縮短最終差異化內容轉移的內容凍結時間，然後再於雲端服務上線。

如果要在提取階段中&#x200B;***追加***&#x200B;現有的移轉集，則必須停用&#x200B;*覆蓋*&#x200B;選項。如需詳細資訊，請參閱[追加提取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)。

如果要在擷取階段中，將差異內容套用至目前內容的頂端，則必須停用&#x200B;*「擦去」*&#x200B;選項。如需詳細資訊，請參閱[追加擷取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process)。

## 移轉集到期 {#migration-set-expiry}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_migrationset_expiry"
>title="移轉集到期"
>abstract="了解移轉集到期。"

所有移轉集都將在約45天的長時間不活動後最終到期。 指標在專案卡片和移轉工作表格列中顯示一段時間後，移轉集將到期，其資料將不再可用。 透過以下方式根據移轉集採取行動，可輕鬆延長到期時間：

* 編輯其說明
* 取得其擷取金鑰
* 對其執行擷取
* 從中執行內嵌

您可以在移轉集列上監視移轉集的到期日。 移轉集即將到期的一個實用視覺指示器也新增了專案的卡片。

![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam29.png)


## 下一步 {#whats-next}

瞭解內容轉移工具及其概述後，瞭解此工具可用來將現有內容從來源AEM執行個體（內部部署或AMS）移至目標AEM Cloud Service執行個體時，您必須檢閱[內容轉移工具的先決條件](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/prerequisites-content-transfer-tool.md)。
