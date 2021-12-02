---
title: 內容轉移工具的必要條件
description: 內容轉移工具的必要條件
exl-id: ef6d0e1a-0ed2-4485-adab-df6e0cf3ac4d
source-git-commit: 3b1ef6eef7249a33908102b287ee4b373d7e843b
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 1%

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
| AEM版本 | 「內容轉移工具」僅能在AEM 6.3或更新版本上執行。 |
| 區段存放區大小 | 現有的存放庫，其JCR節點少於5500萬個，在 *作者* 31 GB開啟 *發佈* 目前受支援。 與Adobe客戶服務建立支援票證，討論區段存放區大小超過這些限制的選項。 |
| 內容存放庫總大小 <br>*（區段存放區+資料存放區）* | 「內容轉移工具」的設計目的是，針對「檔案資料儲存」類型的資料儲存傳輸高達20 TB的內容。 目前不支援高於20 TB的任何項目。 與Adobe客戶服務建立支援票證，討論大於20 TB內容的選項。 <br>為了顯著加快大型儲存庫的內容傳輸流程，可選 [預復](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#setting-up-pre-copy-step) 步驟。 這適用於檔案資料存放區、Amazon S3和Azure資料存放區的資料存放類型。 若為Amazon S3和Azure資料存放區，則支援大於20TB的存放庫大小。 |
| Lucene索引總大小 | 當前支援最大25GB的Lucene索引總大小。 與Adobe客戶服務建立支援票證，以討論索引大小超過此限制的選項。 |
| 節點名稱長度 | 節點名稱的長度必須為150個位元組或更小。 長度超過150個位元組的節點名稱必須縮短為&lt;= 150個位元組，AEMas a Cloud Service中的Document節點存放區才能支援此功能。 如果這些長節點名稱未修正，擷取將會失敗。 |
| 不可變路徑中的內容 | 「內容轉移工具」無法用來移轉不可變路徑中的內容。 要從 `/etc` 僅限 `/etc` 允許選取路徑，但僅支援 [AEM Forms至AEM Formsas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/migrate-to-forms-as-a-cloud-service.html?lang=en#paths-of-various-aem-forms-specific-assets). 如需其他所有使用案例，請參閱 [常見儲存庫重組](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/all-repository-restructuring-in-aem-6-4.html?lang=en#restructuring) 了解有關重新調整儲存庫的更多資訊。 |
| MongoDB中的節點屬性值 | 儲存在MongoDB中的節點屬性值不能超過16MB。 這由MongoDB強制執行。 如果有大於此限制的屬性值，則擷取會失敗。 執行解壓縮前，請執行此 [oak-run](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/1.38.0/oak-run-1.38.0.jar) 指令碼。 檢閱所有大型屬性值，並視需要加以驗證。 超過16MB的資料需要轉換為二進位值。 |

## 下一步 {#whats-next}

檢閱必要條件，並決定是否可以在移轉專案中使用內容轉移工具後，請參閱 [使用內容轉移工具的准則和最佳作法](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en).
