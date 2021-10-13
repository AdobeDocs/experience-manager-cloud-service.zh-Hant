---
title: 內容轉移工具綜覽
description: 內容轉移工具綜覽
exl-id: 4715937e-4c4c-4680-af15-016db4fe7db9
source-git-commit: bdcc5cfc229fd5b1fd1f70e37c7231ed3f727e72
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 概覽 {#overview-content-transfer-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_overview"
>title="概覽"
>abstract="「內容轉移工具」是由Adobe開發的工具，可用來將現有內容從來源AEM例項（內部部署或AMS）移至目標AEM Cloud Service例項。 此工具也會自動轉移主體 (使用者或群組)。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#extraction-process" text="提取程式"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#ingestion-process" text="擷取程式"

「內容轉移工具」是 Adobe 開發的工具，可用來將現有內容從來源 AEM 例項 (內部部署或 AMS) 移至目標 AEM 雲端服務例項。

此工具也會自動轉移主體 (使用者或群組)。

有兩個階段與內容轉移相關聯：

1. **提取**：提取指的是從來源 AEM 例項提取內容，並存放至名為&#x200B;*移轉集*&#x200B;的暫存區域。*移轉集*&#x200B;是 Adobe 提供的雲端儲存空間，可供暫時儲存在來源 AEM 例項與雲端服務 AEM 例項間轉移的內容。

   如需詳細資訊，請參考[內容轉移中的提取程序](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#extraction-process)。

>[!NOTE]
>
> 建議在提取階段中執行使用者對應工具。 如需詳細資訊，請參閱[使用使用者對應工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration) 。

1. **擷取**：擷取指的是從&#x200B;*移轉集*&#x200B;擷取內容，並存放至目標雲端服務例項。

   如需詳細資訊，請參考[內容轉移中的擷取程序](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#ingestion-process)。

*移轉集*&#x200B;有下列屬性：

* 在內容轉移活動期間，一次最多可建立並維護10個移轉集。
* 每個移轉集的名稱必須是唯一的。
* 如果移轉集已停用超過 30 天，則會自動刪除。
* 無論何時建立移轉集，它都與特定環境有關聯。您只能將內容擷取至相同環境中的製作或發佈例項。


「內容轉移工具」具備支援追加差異內容的功能，可以只轉移在上一次內容轉移活動後所進行的變更。

>[!NOTE]
>
>初始轉移內容後，建議您先頻繁地執行追加差異內容，以縮短最終差異化內容轉移的內容凍結時間，然後再於雲端服務上線。

如果要在提取階段中&#x200B;***追加***&#x200B;現有的移轉集，則必須停用&#x200B;*覆蓋*&#x200B;選項。如需詳細資訊，請參考[追加提取](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#top-up-extraction-process)。

如果要在擷取階段中，將差異內容套用至目前內容的頂端，則必須停用&#x200B;*「擦去」*&#x200B;選項。如需詳細資訊，請參考[追加擷取](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#top-up-ingestion-process)。


