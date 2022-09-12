---
title: 在內容轉移工具中檢視移轉集記錄
description: 在內容轉移工具中檢視移轉集記錄
exl-id: aed1ac83-a2fb-425e-aca4-39cd0bb42fd3
source-git-commit: 9a098eefbb730ae2930169cf7402ab4799043291
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 12%

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

若要檢視提取記錄，請前往您的來源Adobe Experience Manager例項，然後選取所需的移轉集。

接著，請依照下列步驟操作：

1. 選取移轉集，然後按一下 **檢視記錄** 從動作列。 這會顯示記錄檔對話方塊。 按一下 **提取記錄** 以在新索引標籤中檢視記錄。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam25.png) \
   或者，按一下 **已完成** 狀態以在新索引標籤中檢視記錄。

1. 若要追蹤記錄而不使用使用者介面，您可以透過 SSH 連線至來源 AEM 環境，並追蹤 `crx-quickstart/cloud-migration/extraction-XXXXX/output.log file`。

1. 若要檢視擷取記錄，請前往Cloud Acceleration Manager中的擷取工作清單，然後按一下三個點(**...**)。 然後，您可以按一下 **下載記錄檔** 下載日誌。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam28.png)
