---
title: 內容轉移工具的必要條件
description: 內容轉移工具的必要條件
source-git-commit: 0d664997a66d790d5662e10ac0afd0dca7cc7fac
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 2%

---

# 內容轉移工具的必要條件 {#prerequisites}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_prereqs"
>title="使用內容轉移工具的重要考量"
>abstract="檢閱使用「內容轉移」工具的重要考量事項，包括Java和AEM版本、支援的資料存放區類型、使用者群組考量事項等。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#pre-reqs" text="使用內容轉移工具的重要考量"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en#best-practices" text="最佳實務與准則"

下表概述使用「內容轉移工具」的先決條件。

請檢閱下列所有考量事項：

| 考量事項 | 目前支援的項目 |
|--- |--- |
| AEM版本 | 「內容轉移工具」僅能在AEM 6.3或更新版本上執行。 若要搭配AEM 6.2或更舊版本使用「內容轉移工具」，需要將內容存放庫就地升級至AEM 6.5。 不需要將程式碼升級至AEM 6.5即可。 |
| 區段存放區大小 | 「內容轉移工具」目前在&#x200B;*Author*&#x200B;上支援高達83 GB，在&#x200B;*Publish*&#x200B;上支援高達31 GB。 |
| 內容存放庫總大小&#x200B;<br>*（區段存放區+資料存放區）* | 「內容轉移工具」的設計目的是將內容轉移至高達10 TB。 目前不支援高於10 TB的任何項目。 與Adobe客戶服務建立支援票證，討論大於10 TB內容的選項。 |
| 不可變路徑中的內容 | 「內容轉移工具」無法用來移轉不可修改路徑（例如`“/etc”`）中的內容。 有某些`"/etc"`路徑可供選取，但僅支援[AEM Forms以AEM Forms為Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/migrate-to-forms-as-a-cloud-service.html?lang=en#paths-of-various-aem-forms-specific-assets)。 有關其他所有使用案例，請參閱[Common Repository Restruct](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/all-repository-restructuring-in-aem-6-4.html?lang=en#restructuring)以了解有關資料庫重組的更多資訊。 |

## 下一步是什麼{#whats-next}

檢閱必要條件，並決定是否可在移轉專案中使用內容轉移工具後，請在使用內容轉移工具時參閱[其他最佳作法和考量事項](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md)。
