---
title: 內容轉移工具綜覽
description: 內容轉移工具綜覽
exl-id: cfc0366a-2139-4d9d-b5bc-0b65bef4013c
source-git-commit: 3bf12642e94076a67010e4701715a54138a490ee
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 43%

---

# 概觀 {#overview-content-transfer-tool}


>[!CONTEXTUALHELP]
>id="aemcloud_ctt_overview"
>title="概觀"
>abstract="內容傳輸工具是Adobe開發的工具，可用於將現有內容從源實例AEM（本地或AMS）移到目標AEM Cloud Service實例。 此工具也會自動轉移主體 (使用者或群組)。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en" text="准則與最佳作法"

<!-- Alexandru: Old version of contextual help, keep for failover/debugging
>[!CONTEXTUALHELP]
>id="aemcloud_ctt_overview"
>title="Overview"
>abstract="Content Transfer Tool is a tool developed by Adobe that can be used to move existing content over from a source AEM instance (on-premise or AMS) to the target AEM Cloud Service instance. This tool also transfers principals (users or groups) automatically."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#extraction-process" text="Extraction Process"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#ingestion-process" text="Ingestion Process" -->

「內容轉移工具」是 Adobe 開發的工具，可用來將現有內容從來源 AEM 例項 (內部部署或 AMS) 移至目標 AEM 雲端服務例項。

此工具也會自動轉移主體 (使用者或群組)。

新版內容傳輸工具可將內容傳輸過程與Cloud Acceleration Manager整合。 強烈建議切換到此新版本，以利用它提供的所有好處：

* 自助式方法，一次提取遷移集並將其並行接收到多個環境中
* 通過更好的載入狀態、護欄和錯誤處理改進用戶體驗
* 攝取日誌被保留，並始終可用於排除故障

開始使用新版本(v2.0.10) <!-- update when version is available --> 您需要卸載舊版本的內容傳輸工具，因為該工具中發生了重大體系結構更改。

>[!NOTE]
>
> 對於已在進行遷移的情況，您可以繼續使用CTT的以前版本，直到遷移完成。 有關與CTT的上一版本相關的文檔，請參閱 [舊文檔](/help/journey-migration/content-transfer-tool/ctt-legacy/overview-content-transfer-tool-legacy.md)。

## 內容傳輸工具中的階段 {#phases-content-transfer-tool}

有兩個階段與內容轉移相關聯：

1. **提取**：提取指的是從來源 AEM 例項提取內容，並存放至名為&#x200B;*移轉集*&#x200B;的暫存區域。*移轉集*&#x200B;是 Adobe 提供的雲端儲存空間，可供暫時儲存在來源 AEM 例項與雲端服務 AEM 例項間轉移的內容。

   如需詳細資訊，請參考[內容轉移中的提取程序](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/extracting-content.html)。

   >[!NOTE]
   > 建議在抽取階段運行用戶映射工具。 請參閱 [使用用戶映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.html) 的子菜單。

1. **擷取**：擷取指的是從&#x200B;*移轉集*&#x200B;擷取內容，並存放至目標雲端服務例項。

   請參閱 [內容傳輸中的攝取過程](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/ingesting-content.html) 的子菜單。

## 遷移集的屬性 {#attributes-migration-set}

移轉集有下列屬性：

* 使用新版本，您可以在在Cloud Acceleration Manager中建立的項目中最多建立五個遷移集。
* 每個移轉集的名稱必須是唯一的。

「內容轉移工具」具備支援追加差異內容的功能，可以只轉移在上一次內容轉移活動後所進行的變更。

>[!NOTE]
>初始轉移內容後，建議您先頻繁地執行追加差異內容，以縮短最終差異化內容轉移的內容凍結時間，然後再於雲端服務上線。

如果要在提取階段中&#x200B;***追加***&#x200B;現有的移轉集，則必須停用&#x200B;*覆蓋*&#x200B;選項。如需詳細資訊，請參考[追加提取](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/extracting-content.html?lang=en#top-up-extraction-process)。

如果要在擷取階段中，將差異內容套用至目前內容的頂端，則必須停用&#x200B;*「擦去」*&#x200B;選項。如需詳細資訊，請參考[追加擷取](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/ingesting-content.html?lang=en#top-up-ingestion-process)。

## 下一步 {#whats-next}

瞭解內容傳輸工具及其描述此工具的概述後，您就可以將現有內容從源實例AEM（本地或AMS）移到目標AEM Cloud Service實例，您必須查看 [內容傳輸工具的先決條件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=en)。
