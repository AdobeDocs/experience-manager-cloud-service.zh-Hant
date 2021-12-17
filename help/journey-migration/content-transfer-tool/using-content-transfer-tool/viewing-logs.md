---
title: 在內容轉移工具中檢視移轉集記錄
description: 在內容轉移工具中檢視移轉集記錄
source-git-commit: bcbf4e4ba1330bef9f2c8c473419903e40ac0e58
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 52%

---


# 檢視移轉集記錄 {#view-logs-content-transfer-tool}


>[!CONTEXTUALHELP]
>id="aemcloud_ctt_logs"
>title="檢視記錄"
>abstract="擷取擷取完成後，檢查記錄中是否有任何錯誤/警告。 您應處理所回報的問題，或聯絡Adobe支援，以立即解決任何錯誤。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#troubleshooting" text="疑難排解"
>additional-url="https://helpx.adobe.com/ca/enterprise/admin-guide.html/ca/enterprise/using/support-for-experience-cloud.ug.html" text="聯絡Adobe支援"

完成每個步驟（擷取和擷取）後，請檢查記錄並尋找錯誤。  您應處理所回報的問題，或聯絡Adobe支援，以立即解決任何錯誤。

## 檢視記錄檔的步驟 {#viewing-logs}

您可以在&#x200B;*綜覽*頁面中檢視現有移轉集記錄。
請遵循下列步驟：

1. 導覽至&#x200B;*綜覽*&#x200B;頁面，並選取您要刪除的移轉集，然後按一下動作列中的&#x200B;**檢視記錄**。

   ![影像](/help/journey-migration/content-transfer-tool/assets/view-log1.png)

1. **記錄**&#x200B;對話框隨即顯示。按一下&#x200B;**提取記錄**，即可在新索引標籤中檢視記錄。

   ![影像](/help/journey-migration/content-transfer-tool/assets/view-log2.png)
或者，

   您也可以在&#x200B;*綜覽*&#x200B;畫面中檢視移轉集記錄。請選取移轉集，然後按一下&#x200B;**提取**&#x200B;欄位下的狀態。在這個情況下，按一下&#x200B;**已完成**&#x200B;即可在新索引標籤中檢視記錄。

   ![影像](/help/journey-migration/content-transfer-tool/assets/view-log3.png)

1. 若要追蹤記錄而不使用使用者介面，您可以透過 SSH 連線至來源 AEM 環境，並追蹤 `crx-quickstart/cloud-migration/extraction-XXXXX/output.log file`。
