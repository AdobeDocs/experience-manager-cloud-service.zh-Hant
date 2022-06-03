---
title: 在內容傳輸工具中查看遷移集的日誌
description: 在內容傳輸工具中查看遷移集的日誌
exl-id: aed1ac83-a2fb-425e-aca4-39cd0bb42fd3
source-git-commit: 9a098eefbb730ae2930169cf7402ab4799043291
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 12%

---

# 檢視移轉集記錄 {#view-logs-content-transfer-tool}


>[!CONTEXTUALHELP]
>id="aemcloud_ctt_logs"
>title="查看日誌"
>abstract="完成「Extract of Ingestion（提取攝取）」後，檢查日誌中是否有錯誤/警告。 任何錯誤都應通過處理報告的問題或與Adobe支援部門聯繫立即解決。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#troubleshooting" text="疑難排解"
>additional-url="https://helpx.adobe.com/ca/enterprise/admin-guide.html/ca/enterprise/using/support-for-experience-cloud.ug.html" text="聯繫Adobe支援"

完成每個步驟（提取和攝取）後，檢查日誌並查找錯誤。  任何錯誤都應通過處理報告的問題或與Adobe支援部門聯繫立即解決。

## 查看日誌的步驟 {#viewing-logs}

要查看提取日誌，請轉到源Adobe Experience Manager實例，然後選擇所需的遷移集。

然後，執行以下步驟：

1. 選擇遷移集並按一下 **查看日誌** 按鈕。 這將顯示「日誌」對話框。 按一下 **提取日誌** 的子菜單。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam25.png) \
   或者，按一下 **已完成** 狀態：查看新頁籤中的日誌。

1. 若要追蹤記錄而不使用使用者介面，您可以透過 SSH 連線至來源 AEM 環境，並追蹤 `crx-quickstart/cloud-migration/extraction-XXXXX/output.log file`。

1. 要查看攝取日誌，請轉到Cloud Acceleration Manager中的攝取作業清單，然後按一下三點(**...**)。 然後，可按一下 **下載日誌** 下載日誌。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam28.png)
