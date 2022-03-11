---
title: 內容傳輸工具的先決條件
description: 內容傳輸工具的先決條件
exl-id: 41a9cff1-4d89-480c-b9fc-5e8efc2a0705
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 1%

---

# 內容傳輸工具的先決條件 {#prerequisites}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_prereqs"
>title="使用內容傳輸工具的重要注意事項"
>abstract="查看使用內容傳輸工具的重要注意事項，包括Java和版本、AEM支援的資料儲存類型、用戶組注意事項等。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#pre-reqs" text="使用內容轉移工具的重要考量"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en#best-practices" text="最佳做法和准則"

下表概述了使用內容傳輸工具的先決條件。

請查看下面列出的所有注意事項：

| 注意事項 | 當前支援的內容 |
|--- |--- |
| 版AEM本 | 內容傳輸工具只能在AEM6.3或更高版本上運行。 |
| 段儲存的大小 | 現有儲存庫，其JCR節點少於5500萬，最大83 GB（聯機壓縮大小） *作者* 和31 GB *發佈* 當前支援。 建立支援票證，與Adobe客戶服務一起討論超過這些限制的段儲存大小選項。 |
| 內容儲存庫的總大小 <br>*（段儲存+資料儲存）* | 內容傳輸工具旨在為檔案資料儲存類型的資料儲存傳輸高達20 TB的內容。 當前不支援高於20 TB的任何內容。 通過Adobe客戶服務建立支援票證，以討論超過20 TB的內容選項。 <br>要顯著加快大型儲存庫的內容傳輸過程，可選 [預拷貝](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#setting-up-pre-copy-step) 中。 這適用於檔案資料儲存、AmazonS3和Azure資料儲存類型的資料儲存。 對於AmazonS3和Azure資料儲存，支援大於20TB的儲存庫大小。 |
| Lucene索引總大小 | 當前支援最大25GB的Lucene索引總大小。 建立支援票證，與Adobe客戶服務討論索引大小超過此限制的選項。 |
| 節點名稱長度 | 節點名稱的長度必須小於或等於150位元組。 長於150位元組的節點名稱必須縮短為&lt;= 150位元組，以便Document節點儲存在AEMas a Cloud Service中受支援。 如果這些長節點名稱未固定，則接收將失敗。 |
| 不可變路徑中的內容 | 內容傳輸工具不能用於遷移不可變路徑中的內容。 從 `/etc` 只有 `/etc` 允許選擇路徑，但僅支援 [AEM Forms與AEM Formsas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/migrate-to-forms-as-a-cloud-service.html?lang=en#paths-of-various-aem-forms-specific-assets)。 有關所有其他使用情形，請參閱 [通用儲存庫重組](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/all-repository-restructuring-in-aem-6-4.html?lang=en#restructuring) 瞭解有關儲存庫重組的詳細資訊。 |
| MongoDB中的節點屬性值 | MongoDB中儲存的節點屬性值不能超過16MB。 這由MongoDB強制執行。 如果屬性值大於此限制，則接收將失敗。 運行抽取之前，請運行此 [橡樹](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/1.38.0/oak-run-1.38.0.jar) 的下界。 查看所有大型屬性值，並驗證是否需要這些值。 超過16MB的需要轉換為二進位值。 |

## 下一步是什麼 {#whats-next}

在您查看了先決條件並確定是否可以在遷移項目中使用內容傳輸工具後，請參閱 [使用內容傳輸工具的指導原則和最佳做法](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en)。
